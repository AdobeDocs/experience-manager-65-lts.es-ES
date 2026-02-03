---
title: Casos de uso de indexación de Oak-run.jar
description: Obtenga información sobre los distintos casos de usuario para realizar la indexación con la herramienta de ejecución de Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: a7a8a20a-e513-43df-80b7-1e6daf957f20
source-git-commit: c714e51f0c0368988ce552969747ab5fce5c186f
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---

# Casos de uso de indexación de Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run admite la indexación de casos de uso en la línea de comandos sin tener que orquestar la ejecución de estos casos de uso a través de la consola JMX de AEM.

Las ventajas generales de utilizar el método de comandos index `oak-run.jar` para administrar índices Oak son las siguientes:

* El comando index de ejecución de Oak proporciona un nuevo conjunto de herramientas de indexación desde la versión de AEM 6.4.
* La ejecución de Oak reduce el tiempo de reindexación, lo que reduce los tiempos de reindexación en repositorios más grandes.
* La ejecución de Oak reduce el consumo de recursos durante la reindexación en AEM, lo que resulta en un mejor rendimiento general del sistema.
* La ejecución de Oak proporciona reindexación fuera de banda, lo que admite situaciones en las que la producción debe estar disponible y no puede tolerar el mantenimiento o el tiempo de inactividad que, de lo contrario, se requeriría para reindexar.

Las secciones siguientes proporcionan comandos de ejemplo. El comando de índice ejecutado por Oak es compatible con todas las configuraciones de NodeStore y BlobStore. Los ejemplos que se proporcionan a continuación son para configuraciones que tienen FileDataStore y SegmentNodeStore.

## Caso de uso 1: Comprobación de la coherencia del índice {#usercase1indexconsistencycheck}

Este caso de uso está relacionado con la corrupción del índice. A veces, no era posible determinar cuál de los índices está dañado. Por lo tanto, Adobe proporciona herramientas que:

* Realiza comprobaciones de coherencia de índices en todos los índices y proporciona un informe sobre los índices válidos y los no válidos.
* Las herramientas se pueden utilizar incluso si no se puede acceder a AEM;
* Es fácil de usar.

Use `--index-consistency-check` para comprobar si hay índices dañados:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Esta operación genera un informe en `indexing-result/index-consistency-check-report.txt`. Consulte a continuación un ejemplo de informe:

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

Los administradores de sistemas y asistencia técnica pueden utilizar las herramientas para identificar rápidamente los índices corruptos y reindexarlos.

## Caso de uso 2: Estadísticas de índice {#usecase2indexstatistics}

Para diagnosticar algunos de los casos relacionados con el rendimiento de las consultas, Adobe a menudo requería una definición de índice existente y estadísticas relacionadas con el índice de la configuración del cliente. Para facilitar la resolución de problemas, Adobe ha creado herramientas que hacen lo siguiente:

1. Volcar toda la definición de índice presente en el sistema en un solo archivo JSON;

1. Volcar estadísticas importantes de los índices existentes;

1. Volcar contenido de índice para análisis sin conexión;

1. Se puede utilizar incluso si no se puede acceder a AEM

Puede realizar las operaciones anteriores con los siguientes comandos de índice:

* `--index-info`: recopila y vacía varias estadísticas relacionadas con los índices

* `--index-definitions`: recopila y descarga definiciones de índice

* `--index-dump` - Volca el contenido del índice

Vea a continuación un ejemplo de cómo funcionan los comandos en la práctica:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Los informes se generarían en `indexing-result/index-info.txt` y `indexing-result/index-definitions.json`

Además, los mismos detalles se proporcionan a través de la consola web y formarían parte del zip de volcado de configuración. Se puede acceder a ellos en la siguiente ubicación:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Ventajas {#uc2benefits}

Esta herramienta permite recopilar rápidamente todos los detalles necesarios relacionados con los problemas de indexación o consulta, así como reducir el tiempo empleado en extraer esta información.

## Caso de uso 3: Reindexación {#usecase3reindexing}

En función de los [escenarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), a veces se debe realizar la reindexación. Actualmente, se reindexa estableciendo el indicador `reindex` en `true` en el nodo de definición de índice mediante CRXDE o la interfaz de usuario del Administrador de índices. Después de establecer el indicador, la reindexación se ejecuta asincrónicamente. Una vez establecido el indicador, la reindexación se realiza de forma asíncrona.

Algunos puntos a tener en cuenta sobre la reindexación:

* La reindexación es mucho más lenta en las configuraciones de `DocumentNodeStore` en comparación con las configuraciones de `SegmentNodeStore` en las que todo el contenido es local;

* Con el diseño actual, mientras se produce la reindexación, el indexador asíncrono se bloquea y todos los demás índices asíncronos quedan obsoletos y no se actualizan durante la indexación. Como resultado, si el sistema está en uso, es posible que los usuarios no vean resultados actualizados;
* La reindexación implica el recorrido de todo el repositorio, lo que puede suponer una carga alta en la configuración de AEM y, por lo tanto, afectar a la experiencia del usuario final;
* Para una instalación de `DocumentNodeStore` en la que la reindexación puede llevar una cantidad de tiempo considerable, un error de conexión a la base de datos Mongo durante la operación puede interrumpir la indexación. En ese caso, debe reiniciar la indexación desde cero.


* A veces, la reindexación puede llevar mucho tiempo debido a la extracción de texto. Este problema puede producirse cuando es específico para configuraciones que tienen muchos archivos PDF, donde el tiempo empleado en la extracción de texto puede afectar al tiempo de indexación.

Para alcanzar estos objetivos, la herramienta de indexación ejecutada por Oak admite diferentes modos de reindexación que se pueden utilizar según sea necesario. El comando index de ejecución de Oak ofrece las siguientes ventajas:

* **reindexación fuera de banda**: la reindexación ejecutada por Oak se puede realizar independientemente de una configuración de AEM en ejecución y, por lo tanto, minimiza el impacto en la instancia de AEM que está en uso;

* **reindexación fuera del carril**: la reindexación se realiza sin afectar a las operaciones de indexación. El indizador asincrónico puede seguir indizando otros índices;

* **Reindexación simplificada para instalaciones de DocumentNodeStore**: para instalaciones de `DocumentNodeStore`, la reindexación se puede realizar con un solo comando que garantiza que la reindexación se realice de la manera más óptima;

* **Admite la actualización de definiciones de índice y la introducción de nuevas definiciones de índice**

### Reindexar: DocumentNodeStore {#reindexdocumentnodestore}

Para las instalaciones de `DocumentNodeStore`, puede realizar la reindexación mediante un único comando ejecutado por Oak:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Esta operación ofrece las siguientes ventajas:

* Impacto mínimo en la ejecución de instancias de AEM. La mayoría de las lecturas se pueden realizar desde servidores secundarios y las cachés de AEM en ejecución no se ven afectadas negativamente debido a todo el recorrido necesario para la reindexación;
* Los usuarios también pueden proporcionar un JSON de un índice nuevo o actualizado mediante la opción `--index-definitions-file`.

### Reindexar: SegmentNodeStore {#reindexsegmentnodestore}

Para `SegmentNodeStore` instalaciones, la reindexación se puede realizar de una de las siguientes maneras:

#### Reindexación en línea: SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga la forma establecida en que se realiza la reindexación estableciendo el indicador `reindex`.

#### Reindexación en línea - SegmentNodeStore - La instancia de AEM se está ejecutando {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para las instalaciones de `SegmentNodeStore`, solamente un proceso puede acceder a los archivos de segmento en modo de lectura-escritura. Como tal, algunas operaciones en la indexación ejecutada por Oak requieren que se realicen pasos manuales adicionales que impliquen lo siguiente:

1. Texto del paso.
1. Conecte `oak-run` al mismo repositorio utilizado por AEM en modo de solo lectura.
1. Realice la indexación con lo siguiente como ejemplo:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Finalmente, importe los archivos de índice creados mediante la operación `IndexerMBean#importIndex` desde la ruta de acceso en la que Oak-run guardó los archivos de indexación después de ejecutar el comando anterior.

En esta situación, no es necesario detener el servidor de AEM ni aprovisionar ninguna instancia nueva. Sin embargo, como la indexación implica el recorrido de todo el repositorio, aumentaría la carga de E/S en la instalación, lo que afectaría negativamente al rendimiento del tiempo de ejecución.

#### Reindexación en línea - SegmentNodeStore - La instancia de AEM se cierra {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para las instalaciones de `SegmentNodeStore`, puede realizar la reindexación con un solo comando ejecutado por Oak. Sin embargo, la instancia de AEM debe cerrarse.

Puede almacenar en déclencheur la reindexación con el siguiente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La diferencia entre este enfoque y el explicado anteriormente es que la creación de puntos de comprobación y la importación de índices se realizan automáticamente. La desventaja es que AEM debe estar inactivo durante el proceso.

#### Reindexación fuera de banda: SegmentNodeStore {#outofbandreindexsegmentnodestore}

En este caso de uso, puede realizar la reindexación en una configuración clonada para minimizar el impacto en la instancia de AEM en ejecución:

1. Cree un punto de comprobación mediante una operación JMX. Vaya a la [consola JMX](/help/sites-administering/jmx-console.md) y busque `CheckpointManager`. A continuación, haga clic en la operación **createCheckpoint(long p1)** con un valor alto para la caducidad en segundos (por ejemplo, **2592000**).
1. Copie la carpeta `crx-quickstart` en un equipo nuevo.
1. Realice la reindexación mediante el comando index ejecutado en Oak.

1. Copie los archivos de índice generados en un servidor de AEM.

1. Importar los archivos de índice mediante JMX.

En este caso de uso, el almacén de datos debe ser accesible desde otra instancia, lo que puede no ser posible cuando `FileDataStore` reside en una solución de almacenamiento basada en la nube como EBS. Esta situación excluye el escenario en el que `FileDataStore` también se clona. Si la definición del índice no realiza la indización de texto completo, no es necesario tener acceso a `DataStore`.

## Caso de uso 4: Actualización de definiciones de índice {#usecase4updatingindexdefinitions}

Actualmente, puede enviar cambios de definición de índice mediante el paquete [ACS Secure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Puede enviar las definiciones de índice en un paquete de contenido y luego realizar la reindexación estableciendo el indicador `reindex` en `true`.


Esto funciona bien en instalaciones más pequeñas en las que la reindexación no tarda mucho tiempo. Sin embargo, en el caso de repositorios grandes, la reindexación se realiza en un período de tiempo considerablemente mayor. Para estos casos, ahora puede utilizar la herramienta de índice de ejecución de Oak.

La ejecución de Oak ahora es compatible con el suministro de definiciones de índice en formato JSON y la creación de índices en modo fuera de banda en el que no se realizan cambios en una instancia activa.

El proceso a tener en cuenta para este caso de uso es el siguiente:

1. Un desarrollador actualizaría las definiciones de índice en una instancia local y luego generaría un archivo JSON de definición de índice mediante la opción `--index-definitions`.
1. El JSON actualizado se envía entonces al administrador del sistema.
1. El administrador del sistema sigue el método fuera de banda y prepara el índice para una instalación diferente.
1. Cuando se completa, los archivos de índice generados se importan en una instalación de AEM en ejecución.
