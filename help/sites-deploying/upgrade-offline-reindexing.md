---
title: Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización
description: Aprenda a utilizar la metodología de reindexación sin conexión para reducir el tiempo de inactividad del sistema al realizar una actualización de AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 0001c874-7468-4750-a377-03156674f4b9
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Uso de la reindexación sin conexión para reducir el tiempo de inactividad durante una actualización {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introducción {#introduction}

Uno de los desafíos clave para actualizar Adobe Experience Manager es el tiempo de inactividad asociado con el entorno de creación cuando se realiza una actualización in situ. Los autores de contenido no podrán acceder al entorno durante una actualización. Por lo tanto, es deseable minimizar la cantidad de tiempo que se tarda en realizar la actualización. En el caso de repositorios grandes, especialmente proyectos de AEM Assets, que suelen tener grandes almacenes de datos y un alto nivel de cargas de recursos por hora, la reindexación de índices de Oak tarda un porcentaje significativo del tiempo de actualización.

En esta sección se describe cómo utilizar la herramienta ejecutada por Oak para reindexar el repositorio **antes de** que realice la actualización, reduciendo así la cantidad de tiempo de inactividad durante la actualización real. Los pasos presentados se pueden aplicar a [índices Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) para las versiones AEM 6.4 y superiores.

## Información general {#overview}

Las nuevas versiones de AEM introducen cambios en las definiciones de índice de Oak a medida que se expande el conjunto de funciones. Los cambios en los índices de Oak obligan a la reindexación al actualizar la instancia de AEM. La reindexación es costosa para las implementaciones de recursos, ya que el texto de los recursos (por ejemplo, el texto del archivo pdf) se extrae y se indexa. Con los repositorios MongoMK, los datos se mantienen en la red, lo que aumenta aún más la cantidad de tiempo que tarda la reindexación.

El problema al que se enfrentan la mayoría de los clientes durante una actualización es la reducción del tiempo de inactividad. La solución es **omitir** la actividad de reindexación durante la actualización. Esto se puede lograr creando los nuevos índices **anteriores** a la actualización y después importándolos simplemente durante la actualización.

## Enfoque {#approach}

![extracción de texto para actualización y reindexación sin conexión](assets/offline-reindexing-upgrade-process.png)

La idea es crear el índice antes de la actualización, comparándolo con las definiciones de índice de la versión de AEM de destino con la herramienta [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). El diagrama anterior muestra el método de reindexación sin conexión.

Además, este es el orden de los pasos que se describen en el enfoque:

1. El texto de los binarios se extrae primero
2. Se crean las definiciones de índice de destino
3. Se crean índices sin conexión
4. Los índices se importan durante el proceso de actualización

### Extracción de texto {#text-extraction}

Para habilitar la indexación completa en AEM, el texto de los binarios como PDF se extrae y se añade al índice. Esto suele ser un paso costoso en el proceso de indexación. La extracción de texto es un paso de optimización recomendado especialmente para reindexar repositorios de recursos, ya que almacenan un gran número de binarios.

![extracción de texto para actualización y reindexación sin conexión](assets/offline-reindexing-upgrade-text-extraction.png)

El texto de los binarios almacenados en el sistema se puede extraer utilizando la herramienta oak-run con la biblioteca tika. Se puede tomar un clon de los sistemas de producción antes de la actualización y se puede utilizar para este proceso de extracción de texto. A continuación, este proceso crea el almacén de texto siguiendo los pasos siguientes:

**1. Recorra el repositorio y recopile los detalles de los binarios**

Este paso genera un archivo CSV que contiene una tupla de binarios, una ruta y un ID de blob.

Ejecute el siguiente comando desde el directorio desde el que desea crear el índice. El ejemplo siguiente supone el directorio principal del repositorio.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilice el parámetro `--fake-ds-path=temp` en lugar de `–fds-path` para acelerar el proceso.

**2. Reutilizar el almacén de texto binario disponible en el índice existente**

Volcar los datos de índice del sistema existente y extraer el almacén de texto.

Puede volcar los datos de índice existentes mediante el siguiente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Donde `nodestore path` es `mongo_ur` o `crx-quickstart/repository/segmentstore/`

A continuación, utilice el volcado de índice anterior para rellenar el almacén:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Donde `oak-index-name` es el nombre del índice de texto completo, por ejemplo, &quot;lucene&quot;.

**3. Ejecute el proceso de extracción de texto utilizando la biblioteca tika para los binarios que se omitieron en el paso anterior**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Donde `datastore path` es la ruta de acceso al almacén de datos binarios.

El almacén de texto creado se puede actualizar y reutilizar para escenarios de reindexación en el futuro.

Para obtener más información sobre el proceso de extracción de texto, consulte la [documentación de Oak](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexación sin conexión {#offline-reindexing}

![reindexación sin conexión-actualización-reindexación sin conexión](assets/offline-reindexing-upgrade-offline-reindexing.png)

Cree el índice Lucene sin conexión antes de la actualización. Si utiliza MongoMK, se recomienda ejecutarlo directamente en uno de los nodos de MongoMk, ya que esto evita la sobrecarga de red.

Para crear el índice sin conexión, siga los siguientes pasos:

**1. Generar definiciones de índice de Oak Lucene para la versión de AEM de destino**

Volcar las definiciones de índice existentes. Las definiciones de índice que sufrieron cambios se generaron utilizando el paquete de repositorio Adobe Granite de la versión de AEM de destino y oak-run.

Para volcar la definición del índice desde la instancia de AEM **source**, ejecute este comando:

>[!NOTE]
>
>Para obtener más información sobre las definiciones de índices de volcado, consulte la [documentación de Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Donde `datastore path` y `nodestore path` son de la instancia de AEM **origen**.

A continuación, genere definiciones de índice a partir de la versión de AEM **target** mediante el paquete de repositorio Granite de la versión de target.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>El proceso de creación de la definición de índice anterior solo es compatible a partir de la versión `oak-run-1.12.0`. La segmentación se realiza mediante el paquete del repositorio Granite `com.adobe.granite.repository-x.x.xx.jar`.

Los pasos anteriores crean un archivo JSON llamado `merge-index-definitions_target.json` que es la definición del índice.

**2. Crear un punto de comprobación en el repositorio**

Cree un punto de comprobación en la instancia de AEM **source** de producción con una larga duración. Esto debe hacerse antes de clonar el repositorio.

Mediante la consola JMX ubicada en `http://serveraddress:serverport/system/console/jmx`, vaya a `CheckpointMBean` y cree un punto de comprobación con una duración suficiente (por ejemplo, 200 días). Para esto, invoque `CheckpointMBean#createCheckpoint` con `17280000000` como argumento para la duración en milisegundos.

Una vez hecho esto, copie el ID del punto de comprobación recién creado y valide la duración mediante JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>Este punto de comprobación se eliminará cuando el índice se importe posteriormente.

Para obtener más información, consulte [creación de puntos de comprobación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) en la documentación de Oak.

**Realizar indexación sin conexión para las definiciones de índice generadas**

La reindexación de Lucene se puede realizar sin conexión mediante oak-run. Este proceso crea datos de índice en el disco en `indexing-result/indexes`. **no** escribe en el repositorio y, por lo tanto, no requiere detener la instancia de AEM en ejecución. El almacén de texto creado se inserta en este proceso:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

El uso del parámetro `--doc-traversal-mode` es práctico con las instalaciones de MongoMK, ya que mejora significativamente el tiempo de reindexación al poner en cola el contenido del repositorio en un archivo plano local. Sin embargo, requiere un espacio en disco adicional del doble del tamaño del repositorio.

Si hay MongoMK, este proceso se puede acelerar si este paso se ejecuta en una instancia más cercana a la instancia de MongoDB. Si se ejecuta en el mismo equipo, se puede evitar la sobrecarga de red.

Encontrará más detalles técnicos en la [documentación de oak-run para la indexación](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importación de índices {#importing-indexes}

Con AEM 6.4 y versiones más recientes, AEM tiene la capacidad integrada de importar índices desde el disco en la secuencia de inicio. La carpeta `<repository>/indexing-result/indexes` está vigilada para detectar la presencia de datos de índice durante el inicio. Puede copiar el índice creado previamente en la ubicación anterior durante el [proceso de actualización](in-place-upgrade.md#performing-the-upgrade) antes de comenzar con la nueva versión del JAR de AEM **target**. AEM lo importa al repositorio y elimina el punto de comprobación correspondiente del sistema. Por lo tanto, se evita completamente un reíndice.

## Sugerencias y solución de problemas adicionales {#troubleshooting}

A continuación encontrará algunas sugerencias útiles e instrucciones para la resolución de problemas.

### Reduzca el impacto en el sistema de producción en directo {#reduce-the-impact-on-the-live-production-system}

Se recomienda clonar el sistema de producción y crear el índice sin conexión utilizando el clon. Esto elimina cualquier posible impacto en el sistema de producción. Sin embargo, el punto de comprobación necesario para importar el índice debe estar presente en el sistema de producción. Por lo tanto, es fundamental crear un punto de comprobación antes de tomar el clon.

### Preparar un Runbook y una ejecución de prueba {#prepare-a-runbook-and-trial-run}

Se recomienda preparar un [runbook](/help/sites-deploying/upgrade-planning.md#building-the-upgrade-and-rollback-runbook) y realizar algunas pruebas antes de ejecutar la actualización en producción.

### Modo de recorrido de documentos con indexación sin conexión {#doc-traversal-mode-with-offline-indexing}

La indexación sin conexión requiere varias travesías de todo el repositorio. Con las instalaciones de MongoMK, se accede al repositorio a través de la red, lo que afecta al rendimiento del proceso de indexación. Una opción es ejecutar el proceso de indexación sin conexión en la propia réplica de MongoDB, lo que eliminará la sobrecarga de red. Otra opción es el uso del modo de recorrido doc.

El modo de recorrido de documentos se puede aplicar agregando el parámetro de línea de comandos `—doc-traversal` al comando oak-run para la indexación sin conexión. Este modo pone en cola una copia de todo el repositorio en el disco local como archivo plano y la utiliza para ejecutar la indexación.
