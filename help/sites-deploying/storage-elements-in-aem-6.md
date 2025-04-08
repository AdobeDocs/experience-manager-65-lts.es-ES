---
title: Elementos de almacenamiento en AEM 6.5 LTS
description: Obtenga información acerca de las implementaciones de almacenamiento de nodos disponibles en AEM 6.5 LTS y cómo mantener el repositorio.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: e51842b5-fa91-42d2-a490-5a7e867dada7
source-git-commit: 0e60c406a9cf1e5fd13ddc09fd85d2a2f8a410f6
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Elementos de almacenamiento en AEM 6.5 LTS{#storage-elements-in-aem}

Este artículo trata sobre lo siguiente:

* [Descripción general del almacenamiento en AEM 6.5 LTS](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Descripción general del almacenamiento en AEM 6.5 LTS {#overview-of-storage-in-aem}

Uno de los cambios más importantes en AEM 6.5 LTS son las innovaciones a nivel de repositorio.

Actualmente, hay dos implementaciones de almacenamiento de nodos disponibles en AEM 6.5 LTS: almacenamiento Tar y almacenamiento MongoDB.

### Almacenamiento de tar {#tar-storage}

#### Ejecutar una instancia de AEM recién instalada con Almacenamiento Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

De forma predeterminada, AEM 6.5 LTS utiliza el almacenamiento Tar para almacenar nodos y binarios, con las opciones de configuración predeterminadas. Puede configurar manualmente su configuración de almacenamiento haciendo lo siguiente:

1. Descargue AEM 6.5 LTS quickstart jar y colóquelo en una nueva carpeta.
1. Desempaquete AEM ejecutando:

   `java -jar <aem-65-lts>.jar -unpack`

1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.

1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` en la carpeta recién creada.

1. Edite el archivo y defina las opciones de configuración. Las siguientes opciones están disponibles para el almacén de nodos de segmentos, que es la base de la implementación del almacenamiento Tar de AEM:

   * `repository.home`: ruta al inicio del repositorio en el que se almacenan varios datos relacionados con el repositorio. De forma predeterminada, los archivos de segmento se almacenarían en el directorio crx-quickstart/segmentstore.
   * `tarmk.size`: tamaño máximo de un segmento en MB. El valor predeterminado es 256 MB.

1. Inicie AEM.

### Almacenamiento de Mongo {#mongo-storage}

>[!NOTE]
>
>La versión mínima admitida de Mongo es Mongo 6.

#### Ejecución de una instancia de AEM recién instalada con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6.5 LTS se puede configurar para que se ejecute con el almacenamiento MongoDB siguiendo el siguiente procedimiento:

1. Descargue AEM 6.5 LTS quickstart jar y colóquelo en una nueva carpeta.
1. Desempaquete AEM ejecutando el siguiente comando:

   `java -jar <aem-65-lts>.jar -unpack`

1. Asegúrese de que MongoDB está instalado y de que se está ejecutando una instancia de `mongod`. Para obtener más información, consulte [Instalar MongoDB](https://docs.mongodb.org/manual/installation/).
1. Cree una carpeta con el nombre `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos creando un archivo de configuración con el nombre de la configuración que desea utilizar en el directorio `crx-quickstart\install`.

   El almacén de nodos de documentos (que es la base de la implementación de almacenamiento MongoDB de AEM) utiliza un archivo denominado `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Edite el archivo y defina las opciones de configuración. Las opciones disponibles son las siguientes:

   * `mongouri`: el [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necesario para conectarse a la base de datos de Mongo. El valor predeterminado es `mongodb://localhost:27017`
   * `db`: nombre de la base de datos Mongo. De forma predeterminada, las nuevas instalaciones de AEM 6.5 LTS usan **aem-author** como nombre de base de datos.
   * `cache`: tamaño de la caché en megabytes. Este tamaño de caché se distribuye entre varias cachés utilizadas en DocumentNodeStore. El valor predeterminado es 256.
   * `changesSize`: tamaño en MB de la colección limitada utilizada en Mongo para almacenar en caché la salida de diferencia. El valor predeterminado es 256.
   * `customBlobStore`: valor booleano que indica que se utiliza un almacén de datos personalizado. El valor predeterminado es false.

1. Cree un archivo de configuración con el PID del almacén de datos que desea utilizar y edite el archivo para establecer las opciones de configuración. Para obtener más información, consulte [Configuración de almacenes de nodos y almacenes de datos](/help/sites-deploying/data-store-config.md).

1. Inicie el JAR de AEM 6.5 LTS con un back-end de almacenamiento MongoDB ejecutando:

   ```shell
   java -jar <aem-65-lts>.jar -r crx3,crx3mongo
   ```

   Donde el modo de ejecución back-end es **`-r`**, el ejemplo comienza con compatibilidad con MongoDB.

#### Desactivación de páginas enormes transparentes {#disabling-transparent-huge-pages}

Red Hat® Linux® utiliza un algoritmo de administración de memoria denominado Transparent Huge Pages (THP). Mientras que AEM realiza lecturas y escrituras específicas, HTTP está optimizado para operaciones grandes. Por lo tanto, se recomienda deshabilitar THP en el almacenamiento Tar y Mongo. Para desactivar el algoritmo, siga estos pasos:

1. Abra el archivo `/etc/grub.conf` en el editor de texto que prefiera.
1. Agregue la línea siguiente al archivo **grub.conf**:

   ```
   transparent_hugepage=never
   ```

1. Finalmente, compruebe si la configuración ha surtido efecto ejecutando:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP está deshabilitado, el resultado del comando anterior debería ser:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Consulte los siguientes recursos:
>
>* Para obtener más información sobre Transparent Huge Pages en Red Hat® Linux®, consulte el siguiente artículo del portal del cliente de Red Hat®: [Cómo usar, monitorizar y deshabilitar las páginas de Red Hat Enterprise Linux 6 ,7 y 8?](https://access.redhat.com/solutions/46111)
>* Para obtener sugerencias de optimización de Linux®, consulte [Optimización del rendimiento](/help/sites-deploying/configuring-performance.md).
>

## Mantenimiento del repositorio {#maintaining-the-repository}

Cada actualización del repositorio crea una revisión de contenido. Como resultado, con cada actualización el tamaño del repositorio aumenta. Para evitar el crecimiento incontrolado del repositorio, las revisiones antiguas deben limpiarse para liberar recursos de disco. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. El mecanismo Revision Cleanup recupera el espacio en disco eliminando los datos obsoletos del repositorio. Para obtener más información acerca de Revision Cleanup, lea la [página Revision Cleanup](/help/sites-deploying/revision-cleanup.md).
