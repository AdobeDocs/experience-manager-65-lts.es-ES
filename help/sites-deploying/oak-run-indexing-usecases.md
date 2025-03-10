---
title: Casos de uso de indexación Oak-run.jar
description: Obtenga información sobre los distintos casos de usuario para realizar la indexación con la herramienta de ejecución de Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
hide: true
hidefromtoc: true
exl-id: a7a8a20a-e513-43df-80b7-1e6daf957f20
source-git-commit: f145e5f0d70662aa2cbe6c8c09795ba112e896ea
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Casos de uso de indexación Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run admite la indexación de casos de uso en la línea de comandos sin tener que orquestar la ejecución de estos casos de uso a través de la consola JMX de AEM.

Las ventajas generales de utilizar el método de comandos oak-run.jar index para administrar índices Oak son las siguientes:

1. El comando index de ejecución de Oak proporciona un nuevo conjunto de herramientas de indexación para AEM 6.4.
1. La ejecución de Oak reduce el tiempo de reindexación, lo que reduce los tiempos de reindexación en repositorios más grandes.
1. La ejecución de Oak reduce el consumo de recursos durante la reindexación en AEM, lo que resulta en un mejor rendimiento general del sistema.
1. La ejecución de Oak proporciona reindexación fuera de banda, lo que admite situaciones en las que la producción debe estar disponible y no puede tolerar el mantenimiento o el tiempo de inactividad que, de lo contrario, se requeriría para reindexar.

Las secciones siguientes proporcionarían comandos de ejemplo. El comando de índice ejecutado por Oak es compatible con todas las configuraciones de NodeStore y BlobStore. Los ejemplos que se proporcionan a continuación giran en torno a las configuraciones que tienen FileDataStore y SegmentNodeStore.

## Caso de uso 1: Comprobación de la coherencia del índice {#usercase1indexconsistencycheck}

Este es un caso de uso relacionado con la corrupción del índice. A veces, no era posible determinar cuál de los índices está dañado. Por lo tanto, Adobe proporciona herramientas que:

1. Realiza comprobaciones de coherencia de índices en todos los índices y proporciona un informe sobre los índices que son válidos y los que no lo son;
1. Las herramientas se pueden utilizar incluso si no se puede acceder a AEM;
1. Es fácil de usar.

La comprobación de índices dañados se puede realizar mediante la operación `--index-consistency-check`:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Esto genera un informe en `indexing-result/index-consistency-check-report.txt`. Consulte a continuación un ejemplo de informe:

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Ventajas {#uc1benefits}

Soporte técnico y el administrador del sistema ahora pueden utilizar esta herramienta para determinar rápidamente qué índices están dañados y luego reindexarlos.

## Caso de uso 2: Estadísticas de índice {#usecase2indexstatistics}

Para diagnosticar algunos de los casos relacionados con el rendimiento de las consultas, Adobe a menudo requería una definición de índice existente, estadísticas relacionadas con el índice de la configuración del cliente. Hasta ahora, esta información estaba dispersa en múltiples recursos. Para facilitar la resolución de problemas, Adobe ha creado herramientas que:

1. Volcar toda la definición de índice presente en el sistema en un solo archivo JSON;

1. Volcar estadísticas importantes de los índices existentes;

1. Volcar contenido de índice para análisis sin conexión;

1. Se puede utilizar incluso si no se puede acceder a AEM

Las operaciones anteriores ahora se pueden realizar mediante los siguientes comandos de índice de operaciones:

* `--index-info`: recopila y vacía varias estadísticas relacionadas con los índices

* `--index-definitions`: recopila y descarga definiciones de índice

* `--index-dump` - Volca el contenido del índice

Vea a continuación un ejemplo de cómo funcionan los comandos en la práctica:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Los informes se generarían en `indexing-result/index-info.txt` y `indexing-result/index-definitions.json`

Además, se proporcionan los mismos detalles a través de la consola web y formarían parte del zip de volcado de configuración. Se puede acceder a ellos en la siguiente ubicación:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Ventajas {#uc2benefits}

Esta herramienta permite recopilar rápidamente todos los detalles necesarios relacionados con los problemas de indexación o consulta, así como reducir el tiempo empleado en extraer esta información.

## Caso de uso 3: Reindexación {#usecase3reindexing}

En función de los [escenarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), a veces se debe realizar la reindexación. Actualmente, la reindexación se realiza estableciendo el indicador `reindex` en `true` en el nodo de definición de índice mediante CRXDE o mediante la interfaz de usuario del Administrador de índices. Una vez establecido el indicador, la reindexación se realiza de forma asíncrona.

Algunos puntos a tener en cuenta sobre la reindexación:

* La reindexación es mucho más lenta en las configuraciones de `DocumentNodeStore` en comparación con las configuraciones de `SegmentNodeStore` en las que todo el contenido es local;

* Con el diseño actual, mientras se produce la reindexación, el indexador asíncrono se bloquea y todos los demás índices asíncronos quedan obsoletos y no se actualizan durante la indexación. Debido a esto, si el sistema está en uso, es posible que los usuarios no vean resultados actualizados;
* La reindexación implica el recorrido de todo el repositorio, lo que puede suponer una carga alta en la configuración de AEM y, por lo tanto, afectar a la experiencia del usuario final.
* Para una instalación de `DocumentNodeStore` en la que la reindexación puede llevar una cantidad de tiempo considerable, si la conexión a la base de datos Mongo falla en mitad de la operación, la indexación tendría que reiniciarse desde cero;

* A veces, la reindexación puede llevar mucho tiempo debido a la extracción de texto. Esto es específico para configuraciones que tienen muchos archivos PDF, donde el tiempo empleado en la extracción de texto puede afectar al tiempo de indexación.

Para cumplir estos objetivos, la herramienta de índice oak-run admite diferentes modos de reindexación que pueden utilizarse según sea necesario. El comando oak-run index proporciona las siguientes ventajas:

* **reindexación fuera de banda**: la reindexación de oak-run se puede realizar independientemente de una configuración de AEM en ejecución y, por lo tanto, minimiza el impacto en la instancia de AEM que está en uso;

* **reindexación fuera del carril**: la reindexación se realiza sin afectar a las operaciones de indexación. Esto significa que el indizador asincrónico puede seguir indizando otros índices;

* **Reindexación simplificada para instalaciones de DocumentNodeStore**: para instalaciones de `DocumentNodeStore`, la reindexación se puede realizar con un solo comando que garantiza que la reindexación se realice de la manera más óptima;

* **Admite la actualización de definiciones de índice y la introducción de nuevas definiciones de índice**

### Reindexar: DocumentNodeStore {#reindexdocumentnodestore}

Para `DocumentNodeStore` instalaciones, la reindexación se puede realizar mediante un solo comando oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Esto ofrece las siguientes ventajas

* Impacto mínimo en la ejecución de instancias de AEM. La mayoría de las lecturas se pueden realizar desde servidores secundarios y las cachés de AEM en ejecución no se ven afectadas negativamente debido a todo el recorrido necesario para la reindexación;
* Los usuarios también pueden proporcionar un JSON de un índice nuevo o actualizado mediante la opción `--index-definitions-file`.

### Reindexar: SegmentNodeStore {#reindexsegmentnodestore}

Para `SegmentNodeStore` instalaciones, la reindexación se puede realizar de una de las siguientes maneras:

#### Reindexación en línea - SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga la forma establecida en que se realiza la reindexación estableciendo el indicador `reindex`.

#### Reindexación en línea - SegmentNodeStore - La instancia de AEM se está ejecutando {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para las instalaciones de `SegmentNodeStore`, solamente un proceso puede acceder a los archivos de segmento en modo de lectura-escritura. Debido a esto, algunas operaciones en la indexación de oak-run requieren que se realicen pasos manuales adicionales.

Esto implicaría lo siguiente:

1. Texto del paso
1. Conecte `oak-run` al mismo repositorio utilizado por AEM en modo de solo lectura y realice la indexación. Un ejemplo de cómo lograrlo:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Finalmente, importe los archivos de índice creados mediante la operación `IndexerMBean#importIndex` desde la ruta en la que oak-run guardó los archivos de indexación después de ejecutar el comando anterior.

En esta situación, no es necesario detener el servidor de AEM ni aprovisionar ninguna instancia nueva. Sin embargo, como la indexación implica el recorrido de todo el repositorio, aumentaría la carga de E/S en la instalación, lo que afectaría negativamente al rendimiento del tiempo de ejecución.

#### Reindexación en línea - SegmentNodeStore - La instancia de AEM está cerrada {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para las instalaciones de `SegmentNodeStore`, la reindexación se puede realizar mediante un solo comando oak-run. Sin embargo, la instancia de AEM debe cerrarse.

Puede almacenar en déclencheur la reindexación con el siguiente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La diferencia entre este enfoque y el explicado anteriormente es que la creación de puntos de comprobación y la importación de índices se realizan automáticamente. La desventaja es que AEM debe estar inactivo durante el proceso.

#### Reindexación fuera de banda: SegmentNodeStore {#outofbandreindexsegmentnodestore}

En este caso de uso, puede realizar la reindexación en una configuración clonada para minimizar el impacto en la instancia de AEM en ejecución:

1. Cree un punto de comprobación mediante una operación JMX. Para ello, vaya a la [consola JMX](/help/sites-administering/jmx-console.md) y busque `CheckpointManager`. A continuación, haga clic en la operación **createCheckpoint(long p1)** con un valor alto para la caducidad en segundos (por ejemplo, **2592000**).
1. Copiar la carpeta `crx-quickstart` en un equipo nuevo
1. Realizar reindexación mediante el comando oak-run index

1. Copie los archivos de índice generados en el servidor de AEM

1. Importar los archivos de índice mediante JMX.

En este caso de uso, se supone que el almacén de datos es accesible desde otra instancia, lo que puede no ser posible si `FileDataStore` se coloca en una solución de almacenamiento basada en la nube como EBS. Esto excluye el escenario donde `FileDataStore` también se clona. Si la definición del índice no realiza la indización de texto completo, no es necesario tener acceso a `DataStore`.

## Caso de uso 4: Actualización de definiciones de índice {#usecase4updatingindexdefinitions}

Actualmente, puede enviar cambios de definición de índice mediante el paquete [ACS Secure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Esto permite enviar las definiciones de índice mediante el paquete de contenido, que posteriormente requiere que se reindexe estableciendo el indicador `reindex` en `true`.

Esto funciona bien en instalaciones más pequeñas en las que la reindexación no tarda mucho tiempo. Sin embargo, en el caso de repositorios grandes, la reindexación se realiza en un período de tiempo considerablemente mayor. Para estos casos, ahora podemos utilizar la herramienta de índice oak-run.

La ejecución de Oak ahora es compatible con el suministro de definiciones de índice en formato JSON y la creación de índices en modo fuera de banda en el que no se realizan cambios en una instancia activa.

El proceso a tener en cuenta para este caso de uso es:

1. Un desarrollador actualizaría las definiciones de índice en una instancia local y luego generaría un archivo JSON de definición de índice mediante la opción `--index-definitions`

1. El JSON actualizado se envía entonces al administrador del sistema
1. El administrador del sistema sigue el método fuera de banda y prepara el índice para una instalación diferente
1. Una vez finalizado, los archivos de índice generados se importan en una instalación de AEM en ejecución.
