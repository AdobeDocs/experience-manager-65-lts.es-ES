---
title: Conexión a Bases de Datos SQL
description: Acceda a una base de datos SQL externa para que las aplicaciones de AEM puedan interactuar con los datos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Conexión a Bases de Datos SQL{#connecting-to-sql-databases}

Acceda a una base de datos SQL externa para que las aplicaciones CQ puedan interactuar con los datos:

1. [Cree o consiga un paquete OSGi que exporte el paquete de controladores JDBC](#bundling-the-jdbc-database-driver).
1. [Configurar un proveedor de grupo de origen de datos JDBC](#configuring-the-jdbc-connection-pool-service).
1. [Obtenga un objeto de origen de datos y cree la conexión en su código](#connecting-to-the-database).

## Agrupar el controlador de base de datos JDBC {#bundling-the-jdbc-database-driver}

Algunos proveedores de bases de datos proporcionan controladores JDBC en un paquete OSGi, por ejemplo, [MySQL](https://dev.mysql.com/downloads/connector/j/). Si el controlador JDBC para la base de datos no está disponible como paquete OSGi, obtenga el JAR del controlador y encapsúlelo en un paquete OSGi. El paquete debe exportar los paquetes necesarios para interactuar con el servidor de la base de datos. El paquete también debe importar los paquetes a los que hace referencia.

El ejemplo siguiente utiliza el complemento [Bundle para Maven](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html) para envolver el controlador HSQLDB en un paquete OSGi. El POM indica al complemento que incruste el archivo hsqldb.jar que está identificado como dependencia. Se exportan todos los paquetes de org.hsqldb.

El complemento determina automáticamente qué paquetes importar y los enumera en el archivo MANIFEST.MF del paquete. Si alguno de los paquetes no está disponible en el servidor CQ, el paquete no se inicia en la instalación. Dos posibles soluciones son las siguientes:

* Indique en el POM que los paquetes son opcionales. Utilice esta solución cuando la conexión JDBC realmente no requiera los miembros del paquete. Utilice el elemento Import-Package para indicar paquetes opcionales como en el siguiente ejemplo:

  `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Ajuste los archivos JAR que contienen los paquetes en un paquete OSGi que exporta los paquetes e implemente el paquete. Utilice esta solución cuando los miembros del paquete sean necesarios durante la ejecución del código.

El conocimiento del código fuente le permite decidir qué solución utilizar. También puede probar cualquiera de las soluciones y realizar pruebas para validar la solución.

### POM que agrupa hsqldb.jar {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

Los siguientes vínculos abren las páginas de descarga de algunos productos de base de datos populares:

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### Configuración del servicio del grupo de conexiones JDBC {#configuring-the-jdbc-connection-pool-service}

Agregue una configuración para el servicio Grupo de conexiones JDBC que utilice el controlador JDBC para crear objetos de fuente de datos. El código de la aplicación utiliza este servicio para obtener el objeto y conectarse a la base de datos.

El grupo de conexiones JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) es un servicio de fábrica. Si necesita conexiones que utilicen propiedades diferentes, por ejemplo, acceso de solo lectura o de lectura y escritura, cree varias configuraciones.

Al trabajar con CQ, existen varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

Las siguientes propiedades están disponibles para configurar un servicio de conexión agrupada. Los nombres de las propiedades se muestran tal y como aparecen en la consola web. El nombre correspondiente para un nodo `sling:OsgiConfig` aparece entre paréntesis. Se muestran valores de ejemplo para un servidor HSQLDB y una base de datos que tiene un alias de `mydb`:

* Clase de controlador JDBC (`jdbc.driver.class`): La clase Java™ que se va a utilizar y que implementa la interfaz java.sql.Driver, por ejemplo, `org.hsqldb.jdbc.JDBCDriver`. El tipo de datos es `String`.

* URI de conexión JDBC (`jdbc.connection.uri`): Dirección URL de la base de datos que se va a usar para crear la conexión, por ejemplo, `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. El formato de la dirección URL debe ser válido para su uso con el método getConnection de la clase java.sql.DriverManager. El tipo de datos es `String`.

* Nombre de usuario ( `jdbc.username`): nombre de usuario que se va a utilizar para autenticarse con el servidor de base de datos. El tipo de datos es `String`.

* Contraseña ( `jdbc.password`): la contraseña que se utilizará para la autenticación del usuario. El tipo de datos es `String`.

* Consulta de validación ( `jdbc.validation.query`): instrucción SQL que se va a utilizar para comprobar que la conexión se ha realizado correctamente, por ejemplo, `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. El tipo de datos es `String`.

* Sólo lectura de forma predeterminada (default.readonly): seleccione esta opción cuando desee que la conexión proporcione acceso de sólo lectura. El tipo de datos es `Boolean`.
* Confirmación automática predeterminada ( `default.autocommit`): Seleccione esta opción para crear transacciones independientes para cada comando SQL enviado a la base de datos y cada transacción se confirma automáticamente. No seleccione esta opción cuando confirme transacciones explícitamente en el código. El tipo de datos es `Boolean`.

* Tamaño del grupo ( `pool.size`): número de conexiones simultáneas que estarán disponibles en la base de datos. El tipo de datos es `Long`.

* Espera de grupo (`pool.max.wait.msec`): Cantidad de tiempo antes de que se agote el tiempo de espera de una solicitud de conexión. El tipo de datos es `Long`.

* Nombre de origen de datos ( `datasource.name`): el nombre de este origen de datos. El tipo de datos es `String`.

* Propiedades de servicio adicionales (`datasource.svc.properties`): conjunto de pares de nombre/valor que desea anexar a la dirección URL de conexión. El tipo de datos es `String[]`.

El servicio de grupo de conexiones JDBC es una fábrica. Por lo tanto, si utiliza un nodo `sling:OsgiConfig` para configurar el servicio de conexión, el nombre del nodo debe incluir el PID del servicio de fábrica seguido de *`-alias`*. El alias que utilice debe ser único para todos los nodos de configuración de ese PID. Un nombre de nodo de ejemplo es `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Conexión a la base de datos {#connecting-to-the-database}

En su código Java™, utilice el servicio DataSourcePool para obtener un objeto `javax.sql.DataSource` para la configuración que ha creado. El servicio DataSourcePool proporciona el método `getDataSource` que devuelve un objeto `DataSource` para un nombre de origen de datos determinado. Como argumento del método, utilice el valor de la propiedad Nombre de origen de datos (o `datasource.name`) que especificó para la configuración Grupo de conexiones JDBC.

El siguiente código JSP de ejemplo obtiene una instancia del origen de datos hsqldbds, ejecuta una consulta SQL simple y muestra el número de resultados devueltos.

#### JSP que realiza una búsqueda en la base de datos {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>Si el método getDataSource produce una excepción porque no se encuentra el origen de datos, asegúrese de que la configuración del servicio Pool de Conexiones es correcta. Compruebe los nombres de las propiedades, los valores y los tipos de datos.
>

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
