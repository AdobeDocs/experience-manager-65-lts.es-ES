---
title: Compatibilidad con RDBMS en AEM 6.4
description: Obtenga información acerca de la compatibilidad con la persistencia de bases de datos relacionales en AEM 6.4 y las opciones de configuración disponibles.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Compatibilidad con RDBMS en AEM 6.4{#rdbms-support-in-aem}

## Información general {#overview}

La compatibilidad con la persistencia de bases de datos relacionales en AEM se implementa mediante el Microkernel del documento. El Microkernel del documento es la base que también se utiliza para implementar la persistencia de MongoDB.

Consiste en una API de Java basada en la API de Java de Mongo. También se proporciona una implementación de una API de BlobStore. De forma predeterminada, los blobs se almacenan en la base de datos.

Para obtener más información sobre los detalles de la implementación, consulte la [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) y la [documentación de RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>También se proporciona compatibilidad con **PostgreSQL 9.4**, pero solo con fines de demostración. No estará disponible para entornos de producción.

## Bases de datos compatibles {#supported-databases}

Para obtener más información sobre el nivel de compatibilidad con bases de datos relacionales en AEM, consulte la [página de requisitos técnicos](/help/sites-deploying/technical-requirements.md).

## Pasos de configuración {#configuration-steps}

El repositorio se crea configurando el servicio OSGi `DocumentNodeStoreService`. Se ha ampliado para admitir la persistencia de bases de datos relacionales, además de MongoDB.

Para que funcione, es necesario configurar una fuente de datos con AEM. Esto se realiza a través del archivo `org.apache.sling.datasource.DataSourceFactory.config`. Los controladores JDBC para la base de datos correspondiente deben proporcionarse por separado como paquetes OSGi dentro de la configuración local.

Para ver los pasos de creación de paquetes OSGi para controladores JDBC, consulte esta [documentación](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) en el sitio web de Apache Sling.

Una vez que los paquetes estén configurados, siga los siguientes pasos para configurar AEM con persistencia de RDB:

1. Asegúrese de que se ha iniciado el daemon de base de datos y de que dispone de una base de datos activa para su uso con AEM.
1. Copie el JAR de AEM 6.3 en el directorio de instalación.
1. Cree una carpeta llamada `crx-quickstart\install` en el directorio de instalación.
1. Configure el almacén de nodos del documento creando un archivo de configuración con el siguiente nombre en el directorio `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configure la fuente de datos y los parámetros JDBC creando otro archivo de configuración con el siguiente nombre en la carpeta `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >Para obtener información detallada sobre la configuración del origen de datos para cada base de datos compatible, consulte [Opciones de configuración de Data Source](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. A continuación, prepare los paquetes OSGi de JDBC para utilizarlos con AEM:

   1. En la carpeta `crx-quickstart/install`, cree una carpeta denominada `9`.

   1. Coloque el JDBC jar en la nueva carpeta.

1. Finalmente, inicie AEM con los modos de ejecución `crx3` y `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opciones de configuración de Data Source {#data-source-configuration-options}

La configuración OSGi `org.apache.sling.datasource.DataSourceFactory-oak.config` se usa para configurar los parámetros necesarios para la comunicación entre AEM y la capa de persistencia de la base de datos.

Estas son las opciones de configuración disponibles:

* `datasource.name:` El nombre del origen de datos. El valor predeterminado es `oak`.

* `url:` La cadena URL de la base de datos que debe usarse con JDBC. Cada tipo de base de datos tiene su propio formato de cadena de URL. Para obtener más información, consulte [Formatos de cadena de URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) a continuación.

* `driverClassName:` nombre de clase del controlador JDBC. Esto variará según la base de datos que desee utilizar y, posteriormente, el controlador necesario para conectarse a ella. A continuación se muestran los nombres de clase de todas las bases de datos compatibles con AEM:

   * `org.postgresql.Driver` para PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` para DB2;
   * `oracle.jdbc.OracleDriver` para Oracle;
   * `com.mysql.jdbc.Driver` para MySQL y MariaDB (experimental);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` para Microsoft SQL Server (experimental).

* `username:` El nombre de usuario con el que se ejecuta la base de datos.

* `password:` Contraseña de la base de datos.

### Formatos de cadena de URL {#url-string-formats}

En la configuración de la fuente de datos se utiliza un formato de cadena de URL diferente en función del tipo de base de datos que se deba utilizar. A continuación se muestra una lista de formatos para las bases de datos que admite actualmente AEM:

* `jdbc:postgresql:databasename` para PostgreSQL;
* `jdbc:db2://localhost:port/databasename` para DB2;
* `jdbc:oracle:thin:localhost:port:SID` para Oracle;
* `jdbc:mysql://localhost:3306/databasename` para MySQL y MariaDB (experimental);
* `jdbc:sqlserver://localhost:1453;databaseName=name` para Microsoft SQL Server (experimental).

## Limitaciones conocidas {#known-limitations}

Aunque la persistencia de RDBMS admite el uso simultáneo de varias instancias de AEM con una sola base de datos, las instalaciones simultáneas no lo son.

Para solucionar esto, asegúrese de ejecutar primero la instalación con un solo miembro y agregue los demás después de que el primero haya finalizado la instalación.
