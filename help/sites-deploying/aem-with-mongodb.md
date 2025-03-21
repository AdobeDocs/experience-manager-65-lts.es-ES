---
title: Adobe Experience Manager con MongoDB
description: Obtenga información acerca de las tareas y consideraciones necesarias para una implementación correcta de Adobe Experience Manager con MongoDB.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
hide: true
hidefromtoc: true
exl-id: af957cd7-ad3d-46f2-9ca5-e175538104f1
source-git-commit: b87199e70b4fefc345c86eabbe89054d4b240e95
workflow-type: tm+mt
source-wordcount: '6217'
ht-degree: 0%

---

# Adobe Experience Manager con MongoDB{#aem-with-mongodb}

Este artículo tiene como objetivo mejorar el conocimiento sobre las tareas y consideraciones necesarias para implementar correctamente AEM (Adobe Experience Manager) con MongoDB.

Para obtener más información relacionada con la implementación, consulte la sección [Implementación y mantenimiento](/help/sites-deploying/deploy.md) de la documentación.

## Cuándo usar MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB se utiliza generalmente para admitir implementaciones de autor de AEM donde se cumple uno de los siguientes criterios:

* Más de 1000 usuarios únicos al día;
* Más de 100 usuarios simultáneos;
* Volúmenes altos de ediciones de página;
* Implementaciones o activaciones grandes.

Los criterios anteriores solo son para las instancias de autor y no para ninguna instancia de publicación que deba basarse en TarMK. El número de usuarios hace referencia a usuarios autenticados, ya que las instancias de autor no permiten el acceso no autenticado.

Si no se cumplen los criterios, se recomienda una implementación activa/en espera de TarMK para abordar la disponibilidad. Por lo general, MongoDB debe considerarse en situaciones en las que los requisitos de escalado son más de lo que se puede lograr con un solo elemento de hardware.

>[!NOTE]
>
>Encontrará información adicional sobre el tamaño de las instancias de autor y la definición de usuarios simultáneos en las [Directrices de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Implementación mínima de MongoDB para AEM {#minimal-mongodb-deployment-for-aem}

A continuación se muestra una implementación mínima para AEM en MongoDB. Para simplificar, se han generalizado los componentes de terminación SSL y proxy HTTP. Consiste en un único conjunto de réplicas de MongoDB, con uno principal y dos secundarios.

![chlimage_1-4](assets/chlimage_1-4.png)

Una implementación mínima requiere tres instancias de `mongod` configuradas como un conjunto de réplicas. Una instancia se selecciona como principal y las demás instancias como secundarias. La elección se administra mediante `mongod`. Cada instancia tiene un disco local adjunto. Por lo tanto, el clúster puede admitir la carga; se recomienda un rendimiento mínimo de 12 MB por segundo con más de 3000 operaciones de E/S por segundo (IOPS).

Los autores de AEM están conectados a las instancias `mongod`, y cada autor de AEM se conecta a las tres instancias `mongod`. Las escrituras se envían a la instancia principal y las lecturas se pueden leer desde cualquiera de las instancias. El tráfico se distribuye en función de la carga mediante una Dispatcher a cualquiera de las instancias de autor de AEM activas. El almacén de datos de Oak es un `FileDataStore` y MMS o el administrador de operaciones de MongoDB proporcionan la supervisión de MongoDB en función de la ubicación de la implementación. Las soluciones de terceros como Splunk o Ganglia proporcionan monitorización del nivel del sistema operativo y del registro.

En esta implementación, todos los componentes son necesarios para una implementación correcta. Cualquier componente que falte deja la implementación sin funcionar.

### Sistemas operativos {#operating-systems}

Para obtener una lista de los sistemas operativos compatibles con AEM 6.5 LTS, consulte la [página de requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Entornos {#environments}

Se admiten entornos virtualizados siempre que haya una buena comunicación entre los diferentes equipos técnicos que ejecutan el proyecto. Esta asistencia incluye al equipo que ejecuta AEM, al equipo propietario del sistema operativo y al equipo que administra la infraestructura virtualizada.

Existen requisitos específicos que cubren la capacidad de E/S de las instancias de MongoDB que debe administrar el equipo que administra el entorno virtualizado. Si el proyecto utiliza una implementación en la nube, como Amazon Web Service, las instancias deben aprovisionarse con suficiente capacidad de E/S y coherencia para admitir las instancias de MongoDB. De lo contrario, los procesos de MongoDB y el repositorio de Oak funcionan de forma poco fiable y errática.

En entornos virtualizados, MongoDB requiere configuraciones específicas de E/S y VM para garantizar que el motor de almacenamiento de MongoDB no se vea afectado por las políticas de asignación de recursos de VMWare. Una implementación correcta garantiza que no haya barreras entre los distintos equipos y que todos estén registrados para ofrecer el rendimiento requerido.

## Consideraciones de hardware {#hardware-considerations}

### Almacenamiento {#storage}

Para lograr el rendimiento de lectura y escritura para un mejor rendimiento sin necesidad de escalado horizontal prematuro, MongoDB generalmente requiere almacenamiento SSD o almacenamiento con un rendimiento equivalente al SSD.

### RAM {#ram}

Las versiones 2.6 y 3.0 de MongoDB que utilizan el motor de almacenamiento MAP requieren que el conjunto de trabajo de la base de datos y sus índices se ajuste a la RAM.

La insuficiencia de RAM provoca una reducción significativa del rendimiento. El tamaño del conjunto de trabajo y de la base de datos depende en gran medida de la aplicación. Aunque se pueden hacer algunas estimaciones, la manera más confiable de determinar la cantidad de RAM necesaria es crear la aplicación AEM y probarla.

Para ayudarle con el proceso de prueba de carga, se puede dar por hecha la siguiente relación entre el espacio de trabajo y el tamaño total de la base de datos:

* 1:10 para almacenamiento SSD
* 1:3 para almacenamiento en disco duro

Estas proporciones significan que para las implementaciones de SSD se requieren 200 GB de RAM para una base de datos de 2 TB.

Aunque las mismas limitaciones se aplican al motor de almacenamiento WiredTiger en MongoDB 3.0, la correlación entre el conjunto de trabajo, la RAM y los errores de página no es tan fuerte. WiredTiger no utiliza la asignación de memoria de la misma manera que lo hace el motor de almacenamiento MAP.

>[!NOTE]
>
>Adobe recomienda utilizar el motor de almacenamiento WiredTiger para implementaciones de AEM 6.1 que utilicen MongoDB 3.0.

### Almacén de datos {#data-store}

Debido a las limitaciones del conjunto de trabajo de MongoDB, se recomienda que el almacén de datos se mantenga independiente de MongoDB. En la mayoría de los entornos, se debe usar un `FileDataStore` que usa un NAS disponible para todas las instancias de AEM. En las situaciones en las que se usa Amazon Web Service, también existe `S3 DataStore`. Si, por cualquier motivo, el almacén de datos se mantiene dentro de MongoDB, el tamaño del almacén de datos debe añadirse al tamaño total de la base de datos y los cálculos del conjunto de trabajo deben ajustarse correctamente. Este tamaño puede significar el aprovisionamiento de más RAM para mantener el rendimiento sin errores de página.

## Monitoreo {#monitoring}

La supervisión es vital para una implementación exitosa del proyecto. Con los conocimientos suficientes, es posible ejecutar AEM en MongoDB sin monitorización. Sin embargo, ese conocimiento normalmente se encuentra en ingenieros especializados para cada sección del despliegue.

Este conocimiento especializado suele incluir a un ingeniero de I+D que trabaja en Apache Oak Core y a un especialista de MongoDB.

Sin supervisión en todos los niveles, se requiere un conocimiento detallado del código base para diagnosticar los problemas. Una vez establecida la supervisión y con las directrices adecuadas sobre las estadísticas principales, los equipos de implementación pueden reaccionar adecuadamente ante las anomalías.

Aunque es posible utilizar herramientas de línea de comandos para obtener una instantánea rápida del funcionamiento de un clúster, hacerlo en tiempo real en muchos hosts es casi imposible. Las herramientas de línea de comandos rara vez proporcionan información histórica a partir de unos minutos y nunca permiten la correlación cruzada entre distintos tipos de métricas. Un breve período de sincronización lenta de `mongod` en segundo plano requiere un esfuerzo manual significativo para correlacionar con la espera de E/S o niveles de escritura excesivos con un recurso de almacenamiento compartido desde una máquina virtual aparentemente no conectada.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager es un servicio gratuito ofrecido por MongoDB que permite la monitorización y administración de instancias de MongoDB. Proporciona una vista del rendimiento y el estado del clúster de MongoDB en tiempo real. Administra tanto las instancias alojadas en la nube como las privadas, siempre que la instancia pueda acceder al servidor de monitorización de Cloud Manager.

Requiere un agente instalado en la instancia de MongoDB que se conecta al servidor de monitorización. Existen tres niveles de agente:

* Un agente de automatización que puede automatizar completamente todo en el servidor MongoDB,
* Un agente de supervisión que puede supervisar la instancia `mongod`,
* Un agente de copia de seguridad que puede realizar copias de seguridad programadas de los datos.

Aunque el uso de Cloud Manager para la automatización del mantenimiento de un clúster de MongoDB facilita muchas de las tareas rutinarias, no es necesario y tampoco lo es utilizar para la copia de seguridad. Sin embargo, se requiere monitorización al elegir un Cloud Manager para monitorizar.

Para obtener más información acerca de MongoDB Cloud Manager, consulte la [documentación de MongoDB](https://docs.cloud.mongodb.com/).

### Administrador de operaciones de MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager es el mismo software que MongoDB Cloud Manager. Una vez registrado, Ops Manager puede descargarse e instalarse localmente en un centro de datos privado o en cualquier otro ordenador portátil o de sobremesa. Utiliza una base de datos local de MongoDB para almacenar datos y comunicarse de la misma manera que Cloud Manager con los servidores administrados. Si tiene políticas de seguridad que prohíben un agente de monitoreo, debe usarse MongoDB Ops Manager.

### Monitorización del sistema operativo {#operating-system-monitoring}

Se requiere monitorización a nivel de sistema operativo para ejecutar un clúster de AEM MongoDB.

Ganglia es un buen ejemplo de este sistema y proporciona una imagen de la gama y el detalle de la información requerida que va más allá de las métricas básicas de salud como CPU, promedio de carga y espacio libre en el disco. Para diagnosticar problemas, se requiere información de nivel inferior, como niveles de grupo de entropía, espera de E/S de CPU, sockets en estado FIN_WAIT2.

### Agregación de registros {#log-aggregation}

Con un clúster de varios servidores, la agregación de registros central es un requisito para un sistema de producción. El software como Splunk admite la agregación de registros y permite a los equipos analizar los patrones de comportamiento de la aplicación sin tener que recopilar manualmente los registros.

## Listas de comprobación {#checklists}

Esta sección trata sobre los pasos que debe seguir para asegurarse de que las implementaciones de AEM y MongoDB estén correctamente configuradas antes de implementar el proyecto.

### Red {#network}

1. Primero, asegúrese de que todos los hosts tengan una entrada DNS
1. Todos los hosts deben poder resolverse mediante su entrada DNS desde todos los demás hosts enrutables
1. Todos los hosts de MongoDB se pueden enrutar desde todos los demás hosts de MongoDB en el mismo clúster
1. Los hosts de MongoDB pueden enrutar paquetes a MongoDB Cloud Manager y a otros servidores de supervisión
1. Los servidores AEM pueden enrutar paquetes a todos los servidores MongoDB
1. La latencia de paquetes entre cualquier servidor de AEM y cualquier servidor MongoDB es menor de dos milisegundos, sin pérdida de paquetes y con una distribución estándar de un milisegundo o menos.
1. Asegúrese de que no haya más de dos saltos entre un servidor AEM y uno MongoDB
1. No hay más de dos saltos entre dos servidores MongoDB
1. No hay enrutadores superiores al nivel OSI 3 entre ningún servidor principal (MongoDB, AEM o cualquier combinación).
1. Si se utiliza un enlace VLAN o cualquier forma de túnel de red, debe cumplir con las comprobaciones de latencia de los paquetes.

### Configuración de AEM {#aem-configuration}

#### Configuración del almacén de nodos {#node-store-configuration}

Las instancias de AEM deben configurarse para utilizar AEM con MongoMK. La base de la implementación de MongoMK en AEM es el almacén de nodos de documentos.

Para obtener más información sobre cómo configurar los almacenes de nodos, vea [Configurar los almacenes de nodos y los almacenes de datos en AEM](/help/sites-deploying/data-store-config.md).

A continuación se muestra un ejemplo de la configuración del almacén de nodos de documentos para una implementación mínima de MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Donde:

* `mongodburi`
El servidor MongoDB al que AEM debe conectarse. Se establecen conexiones con todos los miembros conocidos del conjunto de réplicas predeterminado. Si se utiliza MongoDB Cloud Manager, la seguridad del servidor estará habilitada. Por lo tanto, la cadena de conexión debe contener un nombre de usuario y una contraseña adecuados. Las versiones no empresariales de MongoDB solo admiten la autenticación de nombre de usuario y contraseña. Para obtener más información sobre la sintaxis de la cadena de conexión, consulte la [documentación](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nombre de la base de datos. El valor predeterminado de AEM es `aem-author`.

* `customBlobStore`
Si la implementación almacena binarios en la base de datos, forman parte del conjunto de trabajo. Por ese motivo, se recomienda no almacenar binarios dentro de MongoDB, prefiriendo un almacén de datos alternativo como un almacén de datos de `FileSystem` en un NAS.

* `cache`
El tamaño de la caché en megabytes. Este espacio se distribuye entre varias memorias caché utilizadas en `DocumentNodeStore`. El valor predeterminado es 256 MB. Sin embargo, el rendimiento de lectura de Oak se beneficia de una caché más grande.

* `blobCacheSize`
AEM puede almacenar en caché los blobs utilizados con frecuencia para evitar recuperarlos del almacén de datos. Hacerlo afecta más al rendimiento, especialmente al almacenar blobs en la base de datos de MongoDB. Todos los almacenes de datos basados en el sistema de archivos se benefician de la caché de disco en el sistema operativo.

#### Configuración del almacén de datos {#data-store-configuration}

El almacén de datos se utiliza para almacenar archivos de un tamaño mayor que un umbral. Por debajo de ese umbral, los archivos se almacenan como propiedades en el almacén de nodos de documentos. Si se usa `MongoBlobStore`, se crea una colección dedicada en MongoDB para almacenar los blobs. Esta colección contribuye al conjunto de trabajo de la instancia `mongod` y requiere que `mongod` tenga más RAM para evitar problemas de rendimiento. Por ese motivo, la configuración recomendada es evitar `MongoBlobStore` para implementaciones de producción y usar `FileDataStore` respaldado por un NAS compartido entre todas las instancias de AEM. Dado que la caché en el nivel del sistema operativo es eficaz para administrar archivos, el tamaño mínimo de un archivo en disco debe establecerse en un tamaño cercano al tamaño de bloque del disco. Al hacerlo, se asegura de que el sistema de archivos se utiliza de forma eficaz y de que muchos documentos pequeños no contribuyen en exceso al conjunto de trabajo de la instancia `mongod`.

Esta es una configuración típica del almacén de datos para una implementación mínima de AEM con MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

Donde:

* `minRecordLength`
Tamaño en bytes. Los binarios con un tamaño inferior o igual a este se almacenan con el almacén de nodos de documentos. En lugar de almacenar el ID del blob, se almacena el contenido del binario. En el caso de archivos binarios superiores a este tamaño, el identificador del archivo binario se almacena como una propiedad de Document en la colección nodes. Y, el cuerpo del binario se almacena en el `FileDataStore` del disco. 4096 bytes es un tamaño de bloque típico del sistema de archivos.

* `path`
Ruta a la raíz del almacén de datos. Para una implementación de MongoMK, esta ruta debe ser un sistema de archivos compartido disponible para todas las instancias de AEM. Normalmente se utiliza un servidor de Almacenamiento conectado a la red (NAS). Para implementaciones de nube como Amazon Web Service, `S3DataFileStore` también está disponible.

* `cacheSizeInMB`
Tamaño total de la caché binaria en megabytes. Se utiliza para almacenar en caché binarios inferiores a la configuración de `maxCacheBinarySize`.

* `maxCachedBinarySize`
Tamaño máximo en bytes de un archivo binario almacenado en caché en el archivo binario. Si se utiliza un almacén de datos basado en el sistema de archivos, no se recomienda utilizar valores altos para la caché del almacén de datos, ya que el sistema operativo ya almacena en caché los binarios.

#### Desactivación de la sugerencia de consulta {#disabling-the-query-hint}

Se recomienda deshabilitar la sugerencia de consulta enviada con todas las consultas agregando la propiedad `-Doak.mongo.disableIndexHint=true` al iniciar AEM. Al hacerlo, MongoDB calcula el índice más apropiado para usar según las estadísticas internas.

Si la sugerencia de consulta no está deshabilitada, cualquier ajuste de rendimiento de los índices no afecta al rendimiento de AEM.

#### Habilitar caché persistente para MongoMK {#enable-persistent-cache-for-mongomk}

Se recomienda habilitar una configuración de caché persistente para implementaciones MongoDB, a fin de maximizar la velocidad para entornos con alto rendimiento de lectura de E/S. Para obtener más información, consulte la [documentación de Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Optimizaciones del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Compatibilidad con sistemas operativos {#operating-system-support}

MongoDB 2.6 utiliza un motor de almacenamiento asignado a la memoria que es sensible a algunos aspectos de la gestión de nivel del sistema operativo entre la RAM y el disco. El rendimiento de consulta y lectura de la instancia de MongoDB depende de evitar o eliminar las operaciones de E/S lentas, a menudo denominadas errores de página. Estos problemas son errores de página que se aplican al proceso `mongod` en particular. No confunda esto con errores de página del sistema operativo.

Para un funcionamiento rápido, la base de datos MongoDB solo debe acceder a los datos que ya están en la RAM. Los datos a los que debe acceder están formados por índices y datos. Esta colección de índices y datos se denomina conjunto de trabajo. Cuando el conjunto de trabajo es mayor que la RAM disponible, MongoDB tiene que paginar esos datos desde el disco incurriendo en un coste de E/S, desalojando otros datos que ya están en la memoria. Si la expulsión hace que los datos se vuelvan a cargar desde el disco, los errores de página predominan y el rendimiento se degrada. Cuando el conjunto de trabajo es dinámico y variable, se incurre en más errores de página para admitir operaciones.

MongoDB se ejecuta en varios sistemas operativos, incluidos una amplia variedad de sabores Linux®, Windows y macOS. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obtener más información. Según la elección del sistema operativo, MongoDB tiene diferentes recomendaciones de nivel de sistema operativo. Hay documentos en [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) que se resumen aquí por comodidad.

#### Linux® {#linux}

* Desactive las páginas transparentes y desarrástrelas. Para obtener más información, consulte [Configuración de páginas transparentes de gran tamaño](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/).
* [Ajuste la configuración de lectura anticipada](https://docs.mongodb.com/manual/administration/production-notes/#readahead) en los dispositivos que almacenan los archivos de la base de datos para que se ajuste a su caso de uso.

   * Para el motor de almacenamiento MMAPv1, si el conjunto de trabajo es mayor que la RAM disponible y el patrón de acceso a documentos es aleatorio, considere la posibilidad de reducir la lectura anticipada a 32 o 16. Evalúe diferentes configuraciones para poder encontrar un valor óptimo que maximice la memoria residente y reduzca el número de errores de página.
   * Para el motor de almacenamiento WiredTiger, establezca la lectura anticipada en 0 independientemente del tipo de medio de almacenamiento (giratorio, SSD, etc.). En general, utilice la configuración de lectura anticipada recomendada a menos que las pruebas muestren un beneficio mensurable, repetible y fiable en un valor de lectura anticipada más alto. [El Soporte Profesional de MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) puede proporcionar consejos y orientación sobre configuraciones de lectura anticipada distintas a cero.

* Deshabilite la herramienta optimizada si ejecuta RHEL 7/CentOS 7 en un entorno virtual.
* Cuando RHEL 7/CentOS 7 se ejecuta en un entorno virtual, la herramienta optimizada invoca automáticamente un perfil de rendimiento derivado del rendimiento de rendimiento, que establece automáticamente la configuración de lectura anticipada en 4 MB. Esta configuración puede afectar negativamente al rendimiento.
* Utilice los programadores de disco noop o deadline para las unidades SSD.
* Utilice el programador de discos noop para unidades virtualizadas en VM invitadas.
* Deshabilite NUMA o establezca `vm.zone_reclaim_mode` en 0 y ejecute [mongood](https://docs.mongodb.com/manual/administration/production-notes/#readahead) instancias con entrelazado de nodos. Consulte: [MongoDB y NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obtener más información.

* Ajuste los valores límite del hardware para que se ajusten al caso de uso. Si se están ejecutando varias instancias de [mongood](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) en el mismo usuario, escale los valores ulimit en consecuencia. Consulte: [Configuración de UNIX® ulimit](https://docs.mongodb.com/manual/reference/ulimit/) para obtener más información.

* Use noatime para el punto de montaje [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath).
* Configure suficientes identificadores de archivo (fs.file-max), límite pid de kernel (kernel.pid_max) y el máximo de subprocesos por proceso (kernel.threads-max) para su implementación. Para los sistemas grandes, los siguientes valores proporcionan un buen punto de partida:

   * valor fs.file-max de 98000,
   * valor kernel.pid_max de 64000,
   * valor andkernel.threads-max de 64000

* Asegúrese de que el sistema tenga configurado el espacio de intercambio. Consulte la documentación del sistema operativo para obtener detalles sobre el tamaño adecuado.
* Asegúrese de que el TCP keepalive predeterminado del sistema esté configurado correctamente. Un valor de 300 suele proporcionar un mejor rendimiento para conjuntos de réplicas y clústeres compartidos. Consulte: [¿Afecta el tiempo de mantenimiento de TCP a las implementaciones de MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) en las Preguntas más frecuentes para obtener más información.

#### Windows {#windows}

* Considere la posibilidad de deshabilitar las actualizaciones de &quot;hora del último acceso&quot; de NTFS. Esta configuración es análoga a la desactivación del tiempo en sistemas similares a Unix.

### WiredTiger {#wiredtiger}

A partir de MongoDB 3.2 el motor de almacenamiento predeterminado para MongoDB es el motor de almacenamiento WiredTiger. Este motor proporciona algunas funciones sólidas y escalables, lo que lo hace mucho más adecuado para las cargas de trabajo generales de bases de datos. Las secciones siguientes describen estas funciones.

#### Concurrencia de nivel de documento {#document-level-concurrency}

WiredTiger utiliza el control de concurrencia de nivel de documento para las operaciones de escritura. Como resultado, varios clientes pueden modificar diferentes documentos de una colección al mismo tiempo.

Para la mayoría de las operaciones de lectura y escritura, WiredTiger utiliza control de concurrencia optimista. WiredTiger sólo utiliza bloqueos por intención en los niveles global, de base de datos y de colección. Cuando el motor de almacenamiento detecta conflictos entre dos operaciones, uno incurre en un conflicto de escritura que hace que MongoDB vuelva a intentar esa operación de forma transparente. Algunas operaciones globales, normalmente operaciones de corta duración que implican varias bases de datos, siguen precisando un bloqueo global &quot;en toda la instancia&quot;.

Algunas otras operaciones, como soltar una colección, aún requieren un bloqueo de base de datos exclusivo.

#### Instantáneas y puntos de comprobación {#snapshots-and-checkpoints}

WiredTiger utiliza el Control de concurrencia de varias versiones (MVCC). Al comienzo de una operación, WiredTiger proporciona una instantánea puntual de los datos de la transacción. Una instantánea presenta una vista coherente de los datos en memoria.

Al escribir en el disco, WiredTiger escribe todos los datos en una instantánea en el disco de una manera consistente en todos los archivos de datos. Los datos de [durable](https://docs.mongodb.com/manual/reference/glossary/#term-durable) ahora actúan como punto de comprobación en los archivos de datos. El punto de comprobación garantiza que los archivos de datos sean coherentes hasta el último punto de comprobación, incluido. Es decir, los puntos de comprobación pueden actuar como puntos de recuperación.

MongoDB configura WiredTiger para crear puntos de comprobación (es decir, escribir los datos de instantánea en el disco) a intervalos de 60 segundos o 2 GB de datos de diario.

Durante la escritura de un nuevo punto de comprobación, el punto de comprobación anterior sigue siendo válido. Como tal, incluso si MongoDB termina o encuentra un error al escribir un nuevo punto de comprobación, al reiniciar, MongoDB puede recuperarse del último punto de comprobación válido.

El nuevo punto de comprobación se vuelve accesible y permanente cuando la tabla de metadatos de WiredTiger se actualiza automáticamente para hacer referencia al nuevo punto de comprobación. Una vez que el nuevo punto de control es accesible, WiredTiger libera páginas de los antiguos puntos de control.

Con WiredTiger, incluso sin [diario](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB puede recuperarse del último punto de comprobación; sin embargo, para recuperar los cambios realizados después del último punto de comprobación, ejecute [diario](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger usa una combinación de inicio de sesión de transacción de escritura anticipada con [puntos de comprobación](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) para garantizar la durabilidad de los datos.

El diario WiredTiger mantiene todas las modificaciones de datos entre puntos de comprobación. Si MongoDB existe entre puntos de comprobación, utiliza el historial para reproducir todos los datos modificados desde el último punto de comprobación. Para obtener información sobre la frecuencia con la que MongoDB escribe los datos del diario en el disco, vea [Proceso de diario](https://docs.mongodb.com/manual/core/journaling/#journal-process).

El diario WiredTiger está comprimido usando la biblioteca de compresión [snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process). Para especificar un algoritmo de compresión alternativo o sin compresión, use la configuración [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor).

Consulte [Diario con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>El tamaño mínimo de registro para WiredTiger es de 128 bytes. Si un registro es de 128 bytes o menor, WiredTiger no comprime ese registro.
>
>Puede deshabilitar el diario estableciendo [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) en false, lo que puede reducir la sobrecarga de mantenimiento del diario.
>
>Para [instancias independientes](https://docs.mongodb.com/manual/reference/glossary/#term-standalone), no usar el historial significa que se pierden algunas modificaciones de datos cuando MongoDB se cierra inesperadamente entre los puntos de comprobación. Para los miembros de [conjuntos de réplicas](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), el proceso de replicación puede proporcionar suficientes garantías de durabilidad.

#### Compresión {#compression}

Con WiredTiger, MongoDB admite la compresión para todas las colecciones e índices. La compresión minimiza el uso del almacenamiento a expensas de CPU adicional.

De manera predeterminada, WiredTiger usa compresión de bloques con la biblioteca de compresión [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) para todas las colecciones y [compresión de prefijo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) para todos los índices.

Para las colecciones, también está disponible la compresión de bloques con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib). Para especificar un algoritmo de compresión alternativo o sin compresión, use la configuración [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib).

Para los índices, para deshabilitar la [compresión de prefijo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), use la configuración [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression).

Los ajustes de compresión también se pueden configurar por recopilación y por índice durante la recopilación y la creación de índices. Consulte [Especificar las opciones del motor de almacenamiento](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) y [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options).

Para la mayoría de las cargas de trabajo, los ajustes de compresión predeterminados equilibran la eficiencia del almacenamiento y los requisitos de procesamiento.

El diario WiredTiger también está comprimido de forma predeterminada. Para obtener información sobre la compresión de diarios, consulte [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso de memoria {#memory-use}

Con WiredTiger, MongoDB utiliza tanto la caché interna de WiredTiger como la caché del sistema de archivos.

A partir de 3.4, la caché interna de WiredTiger, de forma predeterminada, utiliza el mayor de los siguientes:

* 50% de RAM menos 1 GB, o
* 256 MB

De forma predeterminada, WiredTiger utiliza la compresión de bloques Snappy para todas las colecciones y la compresión de prefijos para todos los índices. Los valores predeterminados de compresión se pueden configurar a nivel global y también se pueden establecer por colección e índice durante la recopilación y la creación de índices.

Se utilizan diferentes representaciones para los datos en la caché interna de WiredTiger en comparación con el formato en disco:

* Los datos en la caché del sistema de archivos son los mismos que el formato en disco, incluidas las ventajas de cualquier compresión para los archivos de datos. El sistema operativo utiliza la caché del sistema de archivos para reducir la E/S del disco.

Los índices cargados en la caché interna de WiredTiger tienen una representación de datos diferente al formato en disco, pero aún pueden aprovechar la compresión del prefijo de índice para reducir el uso de RAM.

La compresión del prefijo de índice deduplica los prefijos comunes de los campos indizados.

Los datos de recopilación de la caché interna de WiredTiger no están comprimidos y utilizan una representación diferente del formato en disco. La compresión de bloques puede proporcionar ahorros significativos en el almacenamiento en disco, pero los datos deben descomprimirse para que el servidor los manipule.

A través de la caché del sistema de archivos, MongoDB utiliza automáticamente toda la memoria libre que no es utilizada por la caché de WiredTiger o por otros procesos.

Para ajustar el tamaño de la caché interna de WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) y [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar el tamaño de la caché interna de WiredTiger por encima de su valor predeterminado.

### NUMA {#numa}

NUMA (Acceso a Memoria No Uniforme) permite que un núcleo administre cómo se asigna la memoria a los núcleos del procesador. Aunque este proceso intenta acelerar el acceso a la memoria de los núcleos, asegurándose de que puedan acceder a los datos necesarios, NUMA interfiere con MAP introduciendo una latencia adicional, ya que las lecturas no se pueden predecir. Como resultado, NUMA debe deshabilitarse para el proceso `mongod` en todos los sistemas operativos compatibles.

En esencia, en una arquitectura NUMA, la memoria se conecta a las CPU y las CPU se conectan a un bus. En una arquitectura SMP o UMA, la memoria se conecta al bus y se comparte con las CPU. Cuando un subproceso asigna memoria en un CPU NUMA, se asigna según una directiva. El valor predeterminado es asignar memoria conectada al CPU local del subproceso a menos que no haya memoria libre, momento en el que utiliza la memoria de un CPU libre a un costo mayor. Una vez asignada, la memoria no se mueve entre las CPU. La asignación se realiza mediante una directiva heredada del subproceso primario, que en última instancia es el subproceso que inició el proceso.

En muchas bases de datos que ven el equipo como una arquitectura de memoria uniforme multinúcleo, este escenario lleva a que el CPU inicial se llene primero y el CPU secundario se llene más tarde. Es especialmente cierto si un subproceso central es responsable de asignar búferes de memoria. La solución consiste en cambiar la directiva NUMA del subproceso principal utilizado para iniciar el proceso `mongod` ejecutando el siguiente comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Esta directiva asigna la memoria de forma circular en todos los nodos de CPU, lo que garantiza una distribución uniforme en todos los nodos. No genera el mayor acceso de rendimiento a la memoria como en sistemas con varios equipos CPU. Alrededor de la mitad de las operaciones de memoria son más lentas y superan el bus, pero `mongod` no se ha escrito para dirigir NUMA de una manera óptima, por lo que es un compromiso razonable.

### Problemas de NUMA {#numa-issues}

Si el proceso `mongod` se inicia desde una ubicación distinta de la carpeta `/etc/init.d`, es probable que no se haya iniciado con la directiva NUMA correcta. Dependiendo de cuál sea la directiva predeterminada, pueden surgir problemas. El motivo es que los distintos instaladores de Linux® Package Manager para MongoDB también instalan un servicio con archivos de configuración en `/etc/init.d` que realizan el paso descrito anteriormente. Si instala y ejecuta MongoDB directamente desde un archivo (`.tar.gz`), debe ejecutar manualmente mongod en el proceso `numactl`.

>[!NOTE]
>
>Para obtener más información sobre las directivas NUMA disponibles, consulte la [documentación de numactl](https://linux.die.net/man/8/numactl).

El proceso MongoDB se comporta de forma diferente en diferentes directivas de asignación:

```

```

* `-membind=<nodes>`
Asigne solo en los nodos enumerados. Mongod no asigna memoria en los nodos enumerados y no puede utilizar toda la memoria disponible.

* `-cpunodebind=<nodes>`
Ejecute solo en los nodos. Mongod solo se ejecuta en los nodos especificados y solo utiliza la memoria disponible en esos nodos.

* `-physcpubind=<nodes>`
Ejecute solo en las CPU (núcleos) enumeradas. Mongod sólo se ejecuta en las CPU enumeradas y sólo utiliza la memoria disponible en esas CPU.

* `--localalloc`
Asigne siempre memoria en el nodo actual, pero utilice todos los nodos en los que se ejecuta el subproceso. Si un subproceso realiza una asignación, sólo se utiliza la memoria disponible para ese CPU.

* `--preferred=<node>`
Prefiere la asignación a un nodo, pero regresa a otros si el nodo preferido está lleno. Se puede utilizar la notación relativa para definir un nodo. Además, los subprocesos se ejecutan en todos los nodos.

Algunas de las directivas pueden dar como resultado que se asigne menos de toda la RAM disponible al proceso `mongod`. A diferencia de MySQL, MongoDB evita activamente la paginación a nivel de sistema operativo y, por lo tanto, el proceso `mongod` puede obtener menos memoria disponible.

#### Intercambio {#swapping}

Debido a la naturaleza intensiva de memoria de las bases de datos, el intercambio a nivel de sistema operativo debe deshabilitarse. El proceso MongoDB evita el intercambio por diseño.

#### Sistemas de archivos remotos {#remote-filesystems}

Los sistemas de archivos remotos como NFS no se recomiendan para los archivos de datos internos de MongoDB (los archivos de base de datos de proceso mongood), porque introducen demasiada latencia. No confunda con el sistema de archivos compartido necesario para el almacenamiento de Oak Blob (FileDataStore), donde se recomienda NFS.

#### Leer más {#read-ahead}

Ajuste la lectura con anticipación para que cuando se registre una página usando una lectura aleatoria, no se lean bloques innecesarios desde el disco. Estos resultados implican un consumo innecesario de ancho de banda de E/S.

### Requisitos ® Linux {#linux-requirements}

#### Versiones mínimas del núcleo {#minimum-kernel-versions}

* **2.6.23** para `ext4` sistemas de archivos

* **2.6.25** para `xfs` sistemas de archivos

#### Configuración recomendada para discos de base de datos {#recommended-settings-for-database-disks}

**Desactivar hora**

Se recomienda desactivar `atime` en los discos que contienen las bases de datos.

**Establecer el programador de discos NOOP**

Haga lo siguiente:

En primer lugar, compruebe el programador de E/S configurado ejecutando el siguiente comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Si la respuesta es `noop`, no debe hacer nada más.

Si NOOP no es el programador de E/S configurado, puede cambiarlo ejecutando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajustar el valor de lectura anticipada**

Se recomienda utilizar un valor de 32 para los discos en los que se ejecutan bases de datos MongoDB. Este valor asciende a 16 KB. Puede establecerlo si ejecuta lo siguiente:

```shell
sudo blockdev --setra <value> <device>
```

#### Habilitar NTP {#enable-ntp}

Asegúrese de tener NTP instalado y en ejecución en el equipo que aloja las bases de datos MongoDB. Por ejemplo, puede instalarlo utilizando el Administrador de paquetes yum en un equipo CentOS:

```shell
sudo yum install ntp
```

Una vez instalado el daemon NTP y iniciado correctamente, puede comprobar el desplazamiento de tiempo del servidor en el archivo de deriva.

#### Deshabilitar páginas enormes transparentes {#disable-transparent-huge-pages}

Red Hat® Linux® utiliza un algoritmo de administración de memoria denominado Transparent Huge Pages (THP). Se recomienda deshabilitarlo si utiliza el sistema operativo para las cargas de trabajo de la base de datos.

Puede desactivarla siguiendo el siguiente procedimiento:

1. Abra el archivo `/etc/grub.conf` en el editor de texto que prefiera.
1. Agregue la línea siguiente al archivo grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Finalmente, compruebe si la configuración ha surtido efecto ejecutando:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Para obtener más información sobre las páginas enormes transparentes, consulte el siguiente artículo del portal del cliente de Red Hat®: [Cómo usar, supervisar y deshabilitar las páginas enormes transparentes en Red Hat Enterprise Linux 6, 7 y 8?](https://access.redhat.com/solutions/46111).

#### Deshabilitar NUMA {#disable-numa}

En la mayoría de las instalaciones donde NUMA está habilitado, el daemon MongoDB lo deshabilita automáticamente si se ejecuta como un servicio desde la carpeta `/etc/init.d`.

Si este no es el caso, puede deshabilitar NUMA en un nivel de proceso individual. Para deshabilitarlo, ejecute los siguientes comandos:

```shell
numactl --interleave=all <path_to_process>
```

Donde `<path_to_process>` es la ruta al proceso mongodo.

A continuación, deshabilite la recuperación de zona ejecutando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajuste la configuración de ulimit para el proceso mongood {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® permite un control configurable sobre la asignación de recursos mediante el comando `ulimit`. Esta configuración se puede realizar por usuario o por proceso.

Se recomienda configurar ulimit para el proceso mongood según la [Configuración de ulimit recomendada de MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Probar el rendimiento de E/S de MongoDB {#test-mongodb-i-o-performance}

MongoDB proporciona una herramienta denominada `mongoperf` que está diseñada para probar el rendimiento de E/S. Se recomienda utilizarlo para probar el rendimiento de todas las instancias de MongoDB que conforman su infraestructura.

Para obtener información sobre cómo usar `mongoperf`, vea la [documentación de MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>`mongoperf` es un indicador del rendimiento de MongoDB en la plataforma en la que se ejecuta. Como consecuencia, los resultados no deben considerarse definitivos para el funcionamiento de un sistema de producción.
>
>Para obtener resultados de rendimiento más precisos, puede ejecutar pruebas complementarias con la herramienta `fio` Linux®.

**Pruebe el rendimiento de lectura en las máquinas virtuales que componen su implementación**

Una vez instalada la herramienta, cambie al directorio de base de datos MongoDB para ejecutar las pruebas. A continuación, inicie la primera prueba ejecutando `mongoperf` con esta configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

La salida deseada debe alcanzar hasta dos gigabytes por segundo (2 GB/s) y 500.000 IOPS ejecutándose a 32 hilos para todas las instancias de MongoDB.

Ejecute una segunda prueba, esta vez con archivos asignados en memoria, estableciendo el parámetro `mmf:true`:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

La salida de la segunda prueba debe ser considerablemente mayor que la primera, lo que indica el rendimiento de la transferencia de memoria.

>[!NOTE]
>
>Al realizar las pruebas, compruebe las estadísticas de uso de E/S de las máquinas virtuales en cuestión en el sistema de supervisión del sistema operativo. Si indican valores inferiores al 100 por ciento para las lecturas de E/S, puede haber un problema con la máquina virtual.

**Probar el rendimiento de escritura de la instancia principal de MongoDB**

A continuación, compruebe el rendimiento de escritura de E/S de la instancia principal de MongoDB ejecutando `mongoperf` desde el directorio de base de datos de MongoDB con la misma configuración:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

El resultado deseado debería ser de 12 megabytes por segundo y alcanzar alrededor de 3000 IOPS, con poca variación entre el número de subprocesos.

## Pasos para entornos virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Si utiliza WMWare ESX para gestionar e implementar sus entornos virtualizados, asegúrese de realizar los siguientes ajustes desde la consola ESX para adaptarse al funcionamiento de MongoDB:

1. Desactivar la ampliación de memoria
1. Asignación previa y reserva de memoria para las máquinas virtuales que hospedan las bases de datos MongoDB
1. Utilice el Control de E/S de almacenamiento para asignar suficiente E/S al proceso `mongod`.
1. Garantizar los recursos de CPU de los equipos que hospedan MongoDB estableciendo [Reserva CPU](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. Considere utilizar controladores de E/S ParaVirtual. <!-- URL is a 404 See [knowledgebase article](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398).-->

### Amazon Web Service {#amazon-web-services}

Para obtener documentación sobre cómo configurar MongoDB con Amazon Web Service, consulte el artículo [Configuración de la integración de AWS](https://www.mongodb.com/docs/cloud-manager/tutorial/configure-aws-integration/) en el sitio web de MongoDB.

## Protección de MongoDB antes de la implementación {#securing-mongodb-before-deployment}

Consulte esta publicación en [Implementación segura de MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) para obtener consejos sobre cómo proteger la configuración de las bases de datos antes de la implementación.

## Dispatcher {#dispatcher}

### Elección del sistema operativo para Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Para ofrecer correctamente su implementación de MongoDB, el sistema operativo que aloja Dispatcher debe ejecutar **Apache httpd** **versión 2.4 o superior.**

Además, asegúrese de que todas las bibliotecas utilizadas en su compilación estén actualizadas para minimizar las implicaciones de seguridad.

### Configuración de Dispatcher {#dispatcher-configuration}

Una configuración típica de Dispatcher sirve entre diez y 20 veces más el rendimiento de solicitudes de una sola instancia de AEM.

Como el Dispatcher no tiene estado, puede escalarse horizontalmente con facilidad. En algunas implementaciones, se debe restringir el acceso de los autores a ciertos recursos. Se recomienda utilizar una Dispatcher con las instancias de autor.

La ejecución de AEM sin Dispatcher requiere que otra aplicación realice la terminación SSL y el equilibrio de carga. Esto es necesario porque las sesiones deben tener afinidad con la instancia de AEM en la que se crean, un concepto conocido como conexiones fijas. El motivo es garantizar que las actualizaciones del contenido muestren una latencia mínima.

Consulte la [documentación de Dispatcher](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher) para obtener más información sobre cómo configurarla.

### Configuración adicional {#additional-configuration}

#### Conexiones fijas {#sticky-connections}

Las conexiones duraderas garantizan que todas las páginas personalizadas y los datos de sesión de un usuario se compongan en la misma instancia de AEM. Estos datos se almacenan en la instancia, por lo que las solicitudes posteriores del mismo usuario vuelven a la misma instancia.

Se recomienda habilitar conexiones fijas para todas las solicitudes de enrutamiento de capas internas a las instancias de AEM, lo que anima a las solicitudes posteriores a llegar a la misma instancia de AEM. Al hacerlo, se ayuda a minimizar la latencia que, de lo contrario, se aprecia cuando se actualiza el contenido entre instancias.

#### Caduca mucho {#long-expires}

De forma predeterminada, el contenido enviado desde una Dispatcher de AEM tiene encabezados Last-Modified y Etag, sin indicación de la caducidad del contenido. Este flujo garantiza que la interfaz de usuario siempre obtenga la última versión del recurso. También significa que el explorador realiza una operación de GET para ver si el recurso ha cambiado. Como resultado, puede generar varias solicitudes a las que la respuesta HTTP es 304 (sin modificar), según la carga de la página. Para los recursos que no caducan, establecer un encabezado Expires y quitar los encabezados Last-Modified y ETag hacen que el contenido se almacene en caché. Además, no se realizan más solicitudes de actualización hasta que se cumpla la fecha del encabezado Caduca.

Sin embargo, el uso de este método significa que no hay una manera razonable de hacer que el recurso caduque en el explorador antes de que caduque el encabezado Expires. Para mitigar este flujo de trabajo, HtmlClientLibraryManager se puede configurar para que utilice direcciones URL inmutables para las bibliotecas de cliente.

Se garantiza que estas direcciones URL no cambiarán. Cuando el cuerpo del recurso contenido en la URL cambia, los cambios se reflejan en la URL, lo que garantiza que el explorador solicite la versión correcta del recurso.

La configuración predeterminada agrega un selector a HtmlClientLibraryManager. Al ser un selector, el recurso se almacena en caché en Dispatcher con el selector intacto. Además, este selector puede utilizarse para garantizar el comportamiento de caducidad correcto. El selector predeterminado sigue el patrón `lc-.*?-lc`. Las siguientes directivas de configuración httpd de Apache garantizan que todas las solicitudes que coinciden con ese patrón se proporcionen con una hora de caducidad adecuada.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sin olfatear {#no-sniff}

Cuando el contenido se envía sin tipo de contenido, muchos exploradores intentan adivinar el tipo de contenido leyendo los primeros bytes. Este método se denomina &quot;olfateo&quot;. El rastreo abre una vulnerabilidad de seguridad, ya que los usuarios que pueden escribir en el repositorio pueden cargar contenido malicioso sin tipo de contenido.

Por este motivo, se recomienda agregar un encabezado `no-sniff` a los recursos que proporciona Dispatcher. Sin embargo, Dispatcher no almacena en caché los encabezados. Como tal, significa que cualquier contenido servido desde el sistema de archivos local tiene su tipo de contenido determinado por su extensión, en lugar de utilizar el encabezado de tipo de contenido original de su servidor AEM de origen.

No se puede activar ningún fragmento de forma segura si se sabe que la aplicación web nunca proporciona recursos en caché sin un tipo de archivo.

Puede activar No olfatear de forma inclusiva:

```xml
Header set X-Content-Type-Options "nosniff"
```

También se puede activar de forma selectiva:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Política de seguridad de contenido {#content-security-policy}

La configuración predeterminada de Dispatcher permite abrir una directiva de seguridad de contenido, también conocida como CSP. Esta configuración permite que una página cargue recursos de todos los dominios sujetos a las directivas predeterminadas de la zona protegida del explorador.

Es deseable restringir desde dónde se pueden cargar los recursos para evitar cargar código en el motor de JavaScript desde servidores externos no fiables o no verificados.

CSP permite ajustar las directivas. Sin embargo, en una aplicación compleja, los encabezados CSP deben desarrollarse con cuidado, ya que las políticas demasiado restrictivas pueden romper partes de la interfaz de usuario.

>[!NOTE]
>
>Para obtener más información sobre cómo funciona, consulte la [Página de OWASP sobre la Política de seguridad de contenido](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Tamaño {#sizing}

Para obtener más información sobre el tamaño, consulte [Instrucciones de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md).

### Optimización de rendimiento de MongoDB {#mongodb-performance-optimization}

Para obtener información genérica sobre el rendimiento de MongoDB, vea [Análisis del rendimiento de MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitaciones conocidas {#known-limitations}

### Instalaciones simultáneas {#concurrent-installations}

Aunque el uso simultáneo de varias instancias de AEM con una sola base de datos es compatible con MongoMK, las instalaciones simultáneas no lo son.

Para solucionar este problema, asegúrese de ejecutar primero la instalación con un solo miembro y agregar los demás después de que el primero haya terminado de instalarse.

### Longitud del nombre de página {#page-name-length}

Si AEM se está ejecutando en una implementación del administrador de persistencia MongoMK, [los nombres de página están limitados a 150 caracteres.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>Consulte la [documentación de MongoDB](https://docs.mongodb.com/manual/reference/limits/) para familiarizarse con las limitaciones y umbrales conocidos de MongoDB.
