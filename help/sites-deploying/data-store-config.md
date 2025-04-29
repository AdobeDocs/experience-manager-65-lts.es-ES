---
title: Configuración de almacenes de nodos y almacenes de datos en AEM 6.5 LTS
description: Obtenga información sobre cómo configurar almacenes de nodos y almacenes de datos, y cómo realizar la recopilación de elementos no utilizados del almacén de datos.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 69d94737-41d0-47bb-b914-f7606becd038
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '3330'
ht-degree: 1%

---

# Configuración de almacenes de nodos y almacenes de datos en AEM 6.5 LTS{#configuring-node-stores-and-data-stores-in-aem}

## Introducción {#introduction}

En Adobe Experience Manager (AEM), los datos binarios se pueden almacenar de forma independiente de los nodos de contenido. Los datos binarios se almacenan en un almacén de datos, mientras que los nodos de contenido se almacenan en un almacén de nodos.

Tanto los almacenes de datos como los almacenes de nodos se pueden configurar mediante la configuración OSGi. Se hace referencia a cada configuración de OSGi mediante un identificador persistente (PID).

## Pasos de configuración {#configuration-steps}

Para configurar el almacén de nodos y el almacén de datos, realice estos pasos:

1. Copie el archivo JAR de inicio rápido de AEM en su directorio de instalación.
1. Cree una carpeta `crx-quickstart/install` en el directorio de instalación.
1. En primer lugar, configure el almacén de nodos creando un archivo de configuración con el nombre de la opción de almacén de nodos que desee utilizar en el directorio `crx-quickstart/install`.

   Por ejemplo, el almacén de nodos de documentos (que es la base de la implementación MongoMK de AEM) utiliza el archivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite el archivo y defina las opciones de configuración.
1. Cree un archivo de configuración con el PID del almacén de datos que desee utilizar. Edite el archivo para establecer las opciones de configuración.

   >[!NOTE]
   >
   >Consulte [Configuraciones del almacén de nodos](#node-store-configurations) y [Configuraciones del almacén de datos](#data-store-configurations) para ver las opciones de configuración.

1. Inicie AEM.

## Configuraciones del almacén de nodos {#node-store-configurations}

### Almacén de nodos de segmentos {#segment-node-store}

El almacén de nodos de segmentos es la base de la implementación TarMK de Adobe en AEM 6.5 LTS. Utiliza el PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` para la configuración.


Puede configurar las siguientes opciones:

* `repository.home`: ruta al inicio del repositorio en el que se almacenan los datos relacionados con el repositorio. De manera predeterminada, los archivos de segmentos se almacenan en el directorio `crx-quickstart/segmentstore`.

* `tarmk.size`: tamaño máximo de un segmento en MB. El máximo predeterminado es 256 MB.
* `customBlobStore`: valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es True para AEM 6.3 y versiones posteriores. Antes de AEM 6.3, el valor predeterminado era false.

El siguiente es un archivo de muestra `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Almacén de nodos de documentos {#document-node-store}

El almacén de nodos de documentos es la base de la implementación MongoMK de AEM. Utiliza el *PID de `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`*. Estas son las opciones de configuración disponibles:

* `mongouri`: el [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos de Mongo. El valor predeterminado es `mongodb://localhost:27017`

* `db`: nombre de la base de datos Mongo. El valor predeterminado es **aem-author**.

* `cache`: tamaño de la caché en MB. Se distribuye entre varias memorias caché utilizadas en DocumentNodeStore. El valor predeterminado es `256`

* `changesSize`: tamaño en MB de la colección limitada utilizada en Mongo para almacenar en caché la salida de diferencia. El valor predeterminado es `256`

* `customBlobStore`: valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es `false`.

El siguiente es un archivo de muestra `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configuraciones del almacén de datos {#data-store-configurations}

Cuando se trata de un gran número de binarios, se recomienda utilizar un almacén de datos externo en lugar de los almacenes de nodos predeterminados para maximizar el rendimiento.

Por ejemplo, si el proyecto requiere muchos recursos multimedia, almacenarlos en el almacén de datos de archivos o S3 hace que el acceso a ellos sea más rápido que almacenarlos directamente en un MongoDB.

El almacén de datos de archivos proporciona un mejor rendimiento que MongoDB, y las operaciones de copia de seguridad y restauración de Mongo también son más lentas con un gran número de recursos.

A continuación se describen los detalles de los diferentes almacenes de datos y configuraciones.

>[!NOTE]
>
>Para habilitar los almacenes de datos personalizados, debe asegurarse de que `customBlobStore` está establecido en `true` en el archivo de configuración del almacén de nodos correspondiente ([almacén de nodos de segmentos](/help/sites-deploying/data-store-config.md#segment-node-store) o [almacén de nodos de documentos](/help/sites-deploying/data-store-config.md#document-node-store)).

### Almacén de datos de archivo {#file-data-store}

Esta es la implementación de [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) presente en Jackrabbit 2. Proporciona una forma de almacenar los datos binarios como archivos normales en el sistema de archivos. Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Estas opciones de configuración están disponibles:

* `repository.home`: ruta al inicio del repositorio en el que se almacenan varios datos relacionados con el repositorio. De manera predeterminada, los archivos binarios se almacenarían en el directorio `crx-quickstart/repository/datastore`

* `path`: ruta de acceso al directorio en el que se almacenarán los archivos. Si se especifica, tiene prioridad sobre el valor `repository.home`

* `minRecordLength`: tamaño mínimo en bytes de un archivo almacenado en el almacén de datos. El contenido binario inferior a este valor estaría en la línea.

>[!NOTE]
>
>Cuando utilice un NAS para almacenar almacenes de datos de archivos compartidos, asegúrese de utilizar solo dispositivos de alto rendimiento para evitar problemas de rendimiento.

## Almacén de datos de Amazon S3 {#amazon-s-data-store}

AEM se puede configurar para almacenar datos en el servicio de almacenamiento sencillo (S3) de Amazon. Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` para la configuración.

>[!NOTE]
>
>AEM 6.5 LTS admite el almacenamiento de datos en Amazon S3; sin embargo, la compatibilidad no se amplía al almacenamiento de datos en otras plataformas, cuyos proveedores pueden tener sus propias implementaciones de las API S3 de Amazon.

Para habilitar la funcionalidad del almacén de datos S3, se debe descargar e instalar un paquete de funciones que contenga el conector del almacén de datos S3. Vaya a [Repositorio de Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) y descargue la versión más reciente de las versiones 1.60.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.s3connector-1.60.2.zip). Además, debe descargar e instalar el Service Pack más reciente de AEM que aparece en la página [Notas de la versión de AEM 6.5 LTS](/help/release-notes/release-notes.md).

>[!NOTE]
>
>Al usar AEM con TarMK, los binarios se almacenarán de forma predeterminada en `FileDataStore`. Para usar TarMK con el almacén de datos S3, debe iniciar AEM con el modo de ejecución `crx3tar-nofds`, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector S3 de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y navegue hasta la siguiente ubicación:

   ```xml
   jcr_root/libs/system/install
   ```

   Copie todo el contenido de la ubicación anterior en `<aem-install>/crx-quickstart/install.`

1. Si AEM ya está configurado para trabajar con el almacenamiento Tar o MongoDB, quite los archivos de configuración existentes de la carpeta ***&lt;aem-install>***/*crx-quickstart*/*install* antes de continuar. Los archivos que deben eliminarse son los siguientes:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se ha extraído el paquete de funciones y copie el contenido de la siguiente carpeta:

   * `jcr_root/libs/system/config`

   hasta

   * `<aem-install>/crx-quickstart/install`

   Asegúrese de copiar únicamente los archivos de configuración necesarios para la configuración actual. Tanto para un almacén de datos dedicado como para una configuración de almacén de datos compartido, copie el archivo `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >En una configuración de clúster, realice los pasos anteriores en todos los nodos del clúster uno a uno. Además, asegúrese de utilizar la misma configuración de S3 para todos los nodos.

1. Edite el archivo y añada las opciones de configuración que requiera el programa de instalación.
1. Inicie AEM.

## Actualización a una nueva versión del conector S3 1.60.x {#upgrading-to-a-new-version-of-the-s-connector}

Para actualizar a una nueva versión del conector 1.60.x S3, siga estos pasos:

1. Detenga la instancia de AEM.

1. Vaya a `<aem-install>/crx-quickstart/install/15` en la carpeta de instalación de AEM y haga una copia de seguridad de su contenido.
1. Después de la copia de seguridad, elimine la versión antigua del conector S3 y sus dependencias eliminando todos los archivos jar de la carpeta `<aem-install>/crx-quickstart/install/15`, por ejemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Los nombres de archivo presentados anteriormente se utilizan únicamente con fines ilustrativos.

1. Descargue la última versión del paquete de funciones 1.60.x desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/granite/s3-connector/6-5-lts/com.adobe.granite.oak.s3connector-1.60.2.zip).
1. Descomprima el contenido en una carpeta independiente y luego vaya a `jcr_root/libs/system/install/15`.
1. Copie los archivos jar en **&lt;aem-install>**/crx-quickstart/install/15 en la carpeta de instalación de AEM.
1. Inicie AEM y compruebe la funcionalidad del conector.

Puede utilizar el archivo de configuración con las opciones detalladas a continuación.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Opciones del archivo de configuración del conector S3 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>El conector S3 admite la autenticación de usuario IAM y la autenticación de función IAM. Para usar la autenticación de rol IAM, omita los valores `accessKey` y `secretKey` del archivo de configuración. El conector S3 tendrá de forma predeterminada la [función IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) asignada a la instancia.

| Clave | Descripción | Predeterminado | Requerido |
| --- | --- | --- | --- |
| accessKey | ID de clave de acceso para el usuario de IAM con acceso al bloque. | | Sí, cuando no se usan los roles de IAM. |
| secretKey | Clave de acceso secreta del usuario de IAM con acceso al bloque. | | Sí, cuando no se usan los roles de IAM. |
| cacheSize | El tamaño (en bytes) de la caché local. | 64 GB | No. |
| connectionTimeout | Establezca la cantidad de tiempo de espera (en milisegundos) antes de que se agote el tiempo de espera al establecer inicialmente una conexión. | 10 000 | No. |
| maxCachedBinarySize | Los binarios con un tamaño inferior o igual a este valor (en bytes) se almacenan en la memoria caché. | 17408 (17 KB) | No. |
| maxConnections | Establezca el número máximo de conexiones HTTP abiertas permitidas. | 50 | No. |
| maxErrorRetry | Establezca el número máximo de intentos de reintento para solicitudes fallidas (recuperables). | 3 | No. |
| minRecordLength | El tamaño mínimo de un objeto (en bytes) que debe almacenarse en el almacén de datos. | 16384 | No. |
| path | Ruta de acceso local del almacén de datos de AEM. | `crx-quickstart/repository/datastore` | No. |
| proxyHost | Establezca el host proxy opcional mediante el que se conecta el cliente. | | No. |
| proxyPort | Configure el puerto proxy opcional mediante el que se conecta el cliente. | | No. |
| s3Bucket | Nombre del contenedor de S3. | | Sí |
| s3EndPoint | Extremo de API de REST S3. | | No. |
| s3Region | Región donde reside el bloque. Consulte esta [página](https://docs.aws.amazon.com/general/latest/gr/s3.html) para obtener más información. | Región donde se está ejecutando la instancia de AWS. | No. |
| socketTimeout | Establezca la cantidad de tiempo de espera (en milisegundos) para que los datos se transfieran a través de una conexión abierta establecida antes de que se agote el tiempo de espera de la conexión y se cierre. | 50000 | No. |
| stagingPurgeInterval | El intervalo (en segundos) para purgar las cargas finalizadas de la caché de ensayo. | 300 | No. |
| stagingRetryInterval | Intervalo (en segundos) para reintentar cargas fallidas. | 600 | No. |
| stagingSplitPercentage | Porcentaje de `cacheSize` que se utilizará para la realización de cargas asincrónicas. | 10 | No. |
| uploadThreads | El número de subprocesos de carga utilizados para las cargas asincrónicas. | 10 | No. |
| writeThreads | El número de subprocesos simultáneos utilizados para escribir a través de S3 Transfer Manager. | 10 | No. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### Almacenamiento en caché de DataStore {#data-store-caching}

>[!NOTE]
>
>Las implementaciones DataStore de `S3DataStore`, `CachingFileDataStore` y `AzureDataStore` admiten el almacenamiento en caché del sistema de archivos local. La implementación de `CachingFileDataStore` resulta útil cuando DataStore está en NFS (Network File System).

Al actualizar desde una implementación de caché anterior (anterior a Oak 1.6) hay una diferencia en la estructura del directorio de caché del sistema de archivos local. En la estructura de caché antigua, tanto los archivos descargados como los cargados se colocaban directamente debajo de la ruta de caché. La nueva estructura separa las descargas y cargas y las almacena en dos directorios llamados `upload` y `download` en la ruta de acceso de la caché. El proceso de actualización debe ser fluido, y cualquier carga pendiente debe programarse para su carga, y cualquier archivo descargado anteriormente en la caché se coloca en la caché en la inicialización.

También puede actualizar la caché sin conexión utilizando el comando `datastorecacheupgrade` de oak-run. Para obtener más información sobre cómo ejecutar el comando, compruebe [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) para el módulo oak-run.

La caché tiene un límite de tamaño y se puede configurar utilizando el parámetro cacheSize.

#### Descargas {#downloads}

Se comprueba el registro del archivo/blob solicitado en la caché local antes de acceder a él desde el almacén de datos. Cuando la caché supera el límite configurado (consulte el parámetro `cacheSize`) mientras agrega un archivo a la caché, algunos de los archivos se desalojan para reclamar espacio.

#### Carga asincrónica {#async-upload}

La caché admite cargas asincrónicas al DataStore. Los archivos se almacenan localmente en la caché (en el sistema de archivos) y se inicia un trabajo asincrónico para cargar el archivo. El número de cargas asincrónicas está limitado por el tamaño de la caché de ensayo. El tamaño de la caché de ensayo se configura con el parámetro `stagingSplitPercentage`. Este parámetro define el porcentaje del tamaño de la caché que se utilizará para la caché de ensayo. Además, el porcentaje de caché disponible para las descargas se calcula como **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

Las cargas asincrónicas son de varios procesos y el número de subprocesos se configura con el parámetro `uploadThreads`.

Los archivos se mueven a la caché de descarga principal una vez completadas las cargas. Cuando el tamaño de la caché de ensayo supera su límite, los archivos se cargan sincrónicamente en el almacén de datos hasta que se completan las cargas asincrónicas anteriores y vuelve a haber espacio disponible en la caché de ensayo. Los archivos cargados se quitan del área de ensayo mediante un trabajo periódico cuyo intervalo se configura con el parámetro `stagingPurgeInterval`.

Las cargas que generan errores (por ejemplo, debido a una interrupción de la red) se colocan en una cola de reintentos y se vuelven a intentar periódicamente. El intervalo de reintento se configura usando `stagingRetryInterval parameter`.

#### Configuración de la replicación binaria con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar la replicación binaria con S3, se requieren los siguientes pasos:

1. Instale las instancias de autor y publicación y asegúrese de que se inician correctamente.
1. Vaya a la configuración del agente de replicación abriendo una página en *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Presione el botón **Editar** en la sección **Configuración**.
1. Cambie la opción de tipo **Serialization** a **Binary less**.

1. Agregue el parámetro &quot;`binaryless`= `true`&quot; en el URI de transporte. Después del cambio, el URI debe ser similar al siguiente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas las instancias de autor y publicación para que los cambios surtan efecto.

#### Creación de un clúster con S3 y MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Desempaquete el inicio rápido de CQ con el siguiente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Una vez desempaquetado AEM, cree una carpeta dentro del directorio de instalación *crx-quickstart*/*install*.

1. Cree estos dos archivos dentro de la carpeta `crx-quickstart`:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*configuración*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*configuración*

   Una vez creados los archivos, agregue las opciones de configuración según sea necesario.

1. Instale los dos paquetes necesarios para el almacén de datos S3 tal como se explica más arriba.
1. Asegúrese de que MongoDB está instalado y de que se está ejecutando una instancia de `mongod`.
1. Inicie AEM con el siguiente comando:

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Repita los pasos del 1 al 4 para la segunda instancia de AEM.
1. Inicie la segunda instancia de AEM.

#### Configuración de un almacén de datos compartido {#configuring-a-shared-data-store}

1. En primer lugar, cree el archivo de configuración del almacén de datos en cada instancia necesaria para compartir el almacén de datos:

   * Si usa un(a) `FileDataStore`, cree un archivo con el nombre `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y colóquelo en la carpeta `<aem-install>/crx-quickstart/install`.

   * Si usa S3 como almacén de datos, cree un archivo con el nombre `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` en la carpeta `<aem-install>/crx-quickstart/install` como se ha indicado anteriormente.

1. Modifique los archivos de configuración del almacén de datos en cada instancia para que apunten al mismo almacén de datos. Para obtener más información, consulte [Configuraciones del almacén de datos](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si la instancia se ha clonado de un servidor existente, debe quitar `clusterId` de la nueva instancia con la última herramienta oak-run mientras el repositorio está sin conexión. El comando que debe ejecutar es:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si se configura un almacén de nodos de segmentos, se debe especificar la ruta del repositorio. De manera predeterminada, la ruta es `<aem-install-folder>/crx-quickstart/repository/segmentstore.`. Si se configura un almacén de nodos de documento, puede usar un [URI de cadena de conexión Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >La herramienta de ejecución de Oak se puede descargar desde esta ubicación:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Se deben utilizar distintas versiones de la herramienta en función de la versión de Oak que utilice con la instalación de AEM. Compruebe la lista de requisitos de versión que aparece a continuación antes de utilizar la herramienta:
   >
   >
   >
   >    * Para las versiones de Oak **1.2.x**, use la versión de Oak **1.2.12 o posterior**
   >    * Para las versiones de Oak **más recientes que las anteriores**, use la versión de Oak-run que coincida con el núcleo de Oak de su instalación de AEM.
   >
   >

1. Por último, valide la configuración. Para validarlo, busque un archivo único agregado al almacén de datos por cada repositorio que lo comparta. El formato de los archivos es `repository-[UUID]`, donde UUID es un identificador único de cada repositorio individual.

   Por lo tanto, una configuración adecuada debe tener tantos archivos únicos como repositorios que compartan el almacén de datos.

   Los archivos se almacenan de forma diferente, según el almacén de datos:

   * Para `FileDataStore`, los archivos se crean en la ruta raíz de la carpeta del almacén de datos.
   * Para `S3DataStore`, los archivos se crean en el contenedor configurado de S3 en la carpeta `META`.

## Almacén de datos de Azure {#azure-data-store}

AEM se puede configurar para almacenar datos en el servicio de almacenamiento de Azure de Microsoft®. Utiliza el PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` para la configuración.

Para habilitar la funcionalidad del almacén de datos de Azure, se debe descargar e instalar un paquete de funciones que contenga el conector de Azure. Vaya a [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/granite/azure-connector/6-5-lts/com.adobe.granite.oak.azureblobconnector-1.9.16.zip) y descargue la versión más reciente de las versiones 1.9.x del paquete de funciones (por ejemplo, com.adobe.granite.oak.azureblobconnector-1.9.16.zip).

>[!NOTE]
>
>Cuando se utiliza AEM con TarMK, los binarios se almacenan de forma predeterminada en FileDataStore. Para usar TarMK con el almacén de datos de Azure, debe iniciar AEM con el modo de ejecución `crx3tar-nofds`, por ejemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una vez descargado, puede instalar y configurar el conector de Azure de la siguiente manera:

1. Extraiga el contenido del archivo zip del paquete de funciones en una carpeta temporal.

1. Vaya a la carpeta temporal y copie el contenido de `jcr_root/libs/system/install` en la carpeta `<aem-install>crx-quickstart/install`.
1. Si AEM ya está configurado para trabajar con el almacenamiento Tar o MongoDB, quite los archivos de configuración existentes de la carpeta `/crx-quickstart/install` antes de continuar. Los archivos que deben eliminarse son los siguientes:

   Para MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Vuelva a la ubicación temporal en la que se extrajo el paquete de características y copie el contenido de `jcr_root/libs/system/config` en la carpeta `<aem-install>/crx-quickstart/install`.
1. Edite el archivo de configuración y añada las opciones de configuración que requiera el programa de instalación.
1. Inicie AEM.

Puede utilizar el archivo de configuración con las siguientes opciones:

* azureSas=&quot;&quot;: en la versión 1.6.3 del conector, se agregó compatibilidad con la firma de acceso compartido (SAS) de Azure. **Si existen credenciales de SAS y de almacenamiento en el archivo de configuración, SAS tiene prioridad.** Para obtener más información acerca de SAS, consulte la [documentación oficial](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview). Asegúrese de que el carácter &quot;=&quot; tiene un carácter de escape similar a &quot;\=&quot;.

* azureBlobEndpoint=&quot;&quot;: El extremo del blob de Azure. Por ejemplo, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: nombre de la cuenta de almacenamiento. Para obtener más información acerca de las credenciales de autenticación de Microsoft® Azure, consulte la [documentación oficial](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: La clave de acceso de almacenamiento. Asegúrese de que el carácter &quot;=&quot; tiene un carácter de escape similar a &quot;\=&quot;.
* container=&quot;&quot;: el nombre del contenedor de almacenamiento del blob de Microsoft® Azure. El contenedor es una agrupación de un conjunto de blobs. Para obtener más información, lea la [documentación oficial](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN).
* maxConnections=&quot;&quot;: el número simultáneo de solicitudes simultáneas por operación. El valor predeterminado es 1.
* maxErrorRetry=&quot;&quot;: número de reintentos por solicitud. El valor predeterminado es 3.
* socketTimeout=&quot;&quot;: intervalo de tiempo de espera, en milisegundos, utilizado para la solicitud. El valor predeterminado es 5 minutos.

Además de los ajustes anteriores, también se pueden configurar los siguientes ajustes:

* ruta: la ruta del almacén de datos. El valor predeterminado es `<aem-install>/repository/datastore.`
* RecordLength: tamaño mínimo de un objeto que debe almacenarse en el almacén de datos. El valor predeterminado es 16 KB.
* maxCachedBinarySize: Los binarios con un tamaño menor o igual a este tamaño se almacenan en la memoria caché. El tamaño es en bytes. El valor predeterminado es 17408 (17 KB).
* cacheSize: Tamaño de la caché. El valor se especifica en bytes. El valor predeterminado es 64 GB.
* secret: solo se debe utilizar si se utiliza la replicación binaria para la configuración del almacén de datos compartido.
* stagingSplitPercentage: porcentaje del tamaño de caché configurado para utilizarse en las cargas asincrónicas de ensayo. El valor predeterminado es 10.
* uploadThreads: número de subprocesos de carga que se utilizan para cargas asincrónicas. El valor predeterminado es 10.
* stagingPurgeInterval: intervalo en segundos para purgar cargas finalizadas de la caché de ensayo. El valor predeterminado es 300 segundos (5 minutos).
* stagingRetryInterval: intervalo de reintento en segundos para cargas fallidas. El valor predeterminado es 600 segundos (10 minutos).

>[!NOTE]
>
>Todos los ajustes deben colocarse entre comillas, por ejemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Recopilación de residuos del almacén de datos {#data-store-garbage-collection}

El proceso de recolección de elementos no utilizados del almacén de datos se utiliza para quitar los archivos no utilizados del almacén de datos, lo que libera espacio en disco valioso en el proceso.

Para ejecutar la recolección de elementos no utilizados del almacén de datos:

1. Ir a la consola JMX en *https://&lt;serveraddress:port>/system/console/jmx*
1. Buscando **RepositoryManagement.** Cuando encuentre el MBean del Administrador de repositorios, haga clic en él para que aparezcan las opciones disponibles.
1. Desplácese hasta el final de la página y haga clic en el vínculo **startDataStoreGC(boolean markOnly)**.
1. En el siguiente cuadro de diálogo, escriba `false` para el parámetro `markOnly` y, a continuación, haga clic en **Invocar**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >El parámetro `markOnly` indica si se ejecuta o no la fase de barrido de la recolección de elementos no utilizados.

## Recolección de elementos no utilizados del almacén de datos para un almacén de datos compartido {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Al realizar la recolección de elementos no utilizados en un almacén de datos agrupado o compartido, la configuración (con Mongo o Segment TAR) del registro puede mostrar advertencias sobre la incapacidad para eliminar ciertos ID de blob. Los identificadores de blob eliminados en una recolección de elementos no utilizados anterior vuelven a ser referenciados incorrectamente por otros clústeres o nodos compartidos que no tienen información sobre las eliminaciones de identificadores. Como resultado, cuando se realiza la recolección de elementos no utilizados, se registra una advertencia cuando se intenta eliminar un ID que ya se ha eliminado en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

>[!NOTE]
>
>Si utiliza una configuración de almacén de datos compartida y la recopilación de elementos no utilizados del almacén de datos está deshabilitada, la ejecución de la tarea de limpieza binaria de Lucene puede aumentar repentinamente el espacio en disco utilizado. Considere la posibilidad de deshabilitar BlobTracker en todas las instancias de autor y publicación haciendo lo siguiente:
>
>1. Detenga la instancia de AEM.
>2. Agregue el parámetro `blobTrackSnapshotIntervalInSecs=L"0"` en el archivo `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`. Este parámetro requiere Oak 1.12.0, 1.10.2 o posterior.
>3. Vuelva a iniciar la instancia de AEM.

Con las versiones más recientes de AEM, la recolección de elementos no utilizados del almacén de datos también se puede ejecutar en almacenes de datos compartidos por más de un repositorio. Para poder ejecutar la recolección de elementos no utilizados del almacén de datos en un almacén de datos compartido, siga estos pasos:

1. Asegúrese de que todas las tareas de mantenimiento configuradas para la recopilación de residuos del almacén de datos estén desactivadas en todas las instancias del repositorio que compartan el almacén de datos.
1. Ejecute los pasos mencionados en [Recopilación binaria de basura](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) de forma individual en **todas** las instancias del repositorio que comparten el almacén de datos. Sin embargo, asegúrese de escribir `true` para el parámetro `markOnly` antes de hacer clic en el botón Invocar:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Después de completar el procedimiento anterior en todas las instancias, ejecute de nuevo el recolector de elementos no utilizados del almacén de datos de **cualquiera** de las instancias:

   1. Vaya a la consola JMX y seleccione el MBean Repository Manager.
   1. Haga clic en el vínculo **Click startDataStoreGC(boolean markOnly)**.
   1. En el siguiente cuadro de diálogo, vuelva a escribir `false` para el parámetro `markOnly`.

   Todos los archivos encontrados se recopilan utilizando la fase de marcado utilizada anteriormente y eliminando el resto que no se utilicen del almacén de datos.
