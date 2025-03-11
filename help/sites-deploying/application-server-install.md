---
title: Instalación del servidor de aplicaciones
description: Obtenga información sobre cómo instalar Adobe Experience Manager con un servidor de aplicaciones.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: d716571f490fe4bf3b7e58ea2ca85bbe6703ec0d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Instalación del servidor de aplicaciones{#application-server-install}

>[!NOTE]
>
>`JAR` y `WAR` son los tipos de archivo en los que Adobe Experience Manager (AEM) está lanzado. Se está garantizando la calidad de estos formatos para ajustarse a los niveles de soporte que Adobe se ha comprometido a seguir.
>

Esta sección le explica cómo instalar Adobe Experience Manager (AEM) con un servidor de aplicaciones. Consulte la sección [Plataformas admitidas](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) para obtener información sobre los niveles de compatibilidad específicos proporcionados para los servidores de aplicaciones individuales.

Se describen los pasos de instalación de los siguientes servidores de aplicaciones:

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

Consulte la documentación adecuada del servidor de aplicaciones para obtener más información sobre la instalación de aplicaciones web, las configuraciones de servidor y cómo iniciar y detener el servidor.

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## Descripción general {#general-description}

### Comportamiento predeterminado al instalar AEM en un servidor de aplicaciones {#default-behaviour-when-installing-aem-in-an-application-server}

AEM se presenta como un solo archivo WAR para implementar.

Si se implementa, lo siguiente ocurre de forma predeterminada:

* el modo de ejecución es `author`
* Si la instancia (Repositorio, entorno Felix OSGI, paquetes, etc.) está instalada en `${user.dir}/crx-quickstart`donde `${user.dir}` es el directorio de trabajo actual, esta ruta de acceso a crx-quickstart se denomina `sling.home`

* la raíz de contexto es el nombre del archivo de guerra, por ejemplo, `aem-65-lts`

#### Configuración {#configuration}

Puede cambiar el comportamiento predeterminado de la siguiente manera:

* modo de ejecución : configure el parámetro `sling.run.modes` en el archivo `WEB-INF/web.xml` del archivo WAR de AEM antes de la implementación

* sling.home: configure el parámetro `sling.home` en el archivo `WEB-INF/web.xml`del archivo war de AEM antes de la implementación

* raíz de contexto: cambie el nombre del archivo war de AEM

#### Instalación de publicación {#publish-installation}

Para implementar una instancia de publicación, debe establecer el modo de ejecución en Publish:

* Desempaquetar WEB-INF/web.xml del archivo WAR de AEM
* Cambie el parámetro sling.run.modes a publish
* Vuelva a empaquetar el archivo web.xml en el archivo WAR de AEM
* Implementar archivo WAR de AEM

#### Comprobación de instalación {#installation-check}

Para comprobar si todo está instalado, puede:

* sigue el `error.log` archivo para ver que todo el contenido está instalado
* busque en `/system/console` que todos los paquetes estén instalados

#### Dos instancias en el mismo servidor de aplicaciones {#two-instances-on-the-same-application-server}

Para fines de demostración, puede ser adecuado instalar la instancia de autor y publicación en un servidor de aplicaciones. Para ello, haga lo siguiente:

1. Cambie las variables sling.home y sling.run.modes de la instancia de publicación.
1. Desempaquete el archivo WEB-INF/web.xml del archivo WAR de AEM.
1. Cambie el parámetro sling.home a una ruta diferente (es posible usar rutas absolutas y relativas).
1. Cambie sling.run.modes a publish para la instancia de publicación.
1. Vuelva a empaquetar el archivo web.xml.
1. Cambie el nombre de los archivos WAR para que tengan nombres diferentes. Por ejemplo, un nombre para aemauthor.war y el otro para aempublish.war.
1. Utilice una configuración de memoria más alta. Por ejemplo, las instancias predeterminadas de AEM utilizan `-Xmx3072m`
1. Implemente las dos aplicaciones web.
1. Después de la implementación, detenga las dos aplicaciones web.
1. Tanto en las instancias de autor como en las de publicación, asegúrese de que la propiedad felix.service.urlhandlers=false de los archivos sling.properties esté establecida en false (el valor predeterminado es que esté establecida en true).
1. Vuelva a iniciar las dos aplicaciones web.

## Procedimientos de instalación de Application Servers {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

**Preparación del servidor**

* Permita que los encabezados de autenticación básicos pasen:

   * Una forma de permitir que AEM autentique a un usuario es desactivar la seguridad administrativa global del servidor WebSphere®, para ello: vaya a Seguridad > Seguridad global y desmarque la casilla de verificación Activar seguridad administrativa, guarde y reinicie el servidor.

* set `"JAVA_OPTS= -Xmx2048m"`
* Si desea instalar AEM con la raíz de contexto = /, cambie la raíz de contexto de la aplicación web predeterminada existente.

**Implementar la aplicación web de AEM**

* Descargar archivo WAR de AEM
* Realice las configuraciones en web.xml si es necesario (consulte la descripción general anterior)

   * Desempaquetar archivo WEB-INF/web.xml
   * cambie el parámetro sling.run.modes a publish
   * elimine los comentarios del parámetro inicial sling.home y establezca esta ruta como necesite
   * Reempaquetar archivo web.xml

* Implementar archivo WAR de AEM

   * Elija una raíz de contexto (si desea definir los modos de ejecución de sling, debe seleccionar los pasos detallados del asistente de implementación y, a continuación, especificarlo en el paso 6 del asistente)

* Iniciar la aplicación web de AEM

#### Tomcat 11.0.x {#tomcat}

Antes de una implementación, lea la [Descripción general](#general-description) anterior.

* **Preparar el servidor Tomcat**

   * Aumente la configuración de memoria de VM:

      * En `bin/catalina.bat` (resp `catalina.sh` en UNIX®) agregue la siguiente configuración:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat no permite el acceso de administrador o responsable durante la instalación. Por lo tanto, debe editar manualmente `tomcat-users.xml` para permitir el acceso a estas cuentas:

      * Edite `tomcat-users.xml` para incluir el acceso de administrador y gerente. La configuración debería ser similar al siguiente ejemplo:

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * Si desea implementar AEM con la raíz de contexto &quot;/&quot;, debe cambiar la raíz de contexto de la aplicación web ROOT existente:

      * Detener y anular la implementación de la aplicación web ROOT
      * Cambie el nombre de la carpeta ROOT.war en la carpeta webapps de tomcat
      * Iniciar aplicación web de nuevo

   * Si instala la aplicación web de AEM mediante la interfaz de usuario del administrador, debe aumentar el tamaño máximo de un archivo cargado, ya que el valor predeterminado solo permite un tamaño de carga de 50 MB. Para que abra el archivo web.xml de la aplicación web del administrador,

     `webapps/manager/WEB-INF/web.xml`

     y aumente el tamaño máximo de archivo y el tamaño máximo de solicitud a al menos 500 MB, vea el siguiente ejemplo de `multipart-config` de este archivo de `web.xml`.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Implementar la aplicación web de AEM**

   * Descargue el archivo WAR de AEM.
   * Realice las configuraciones en web.xml si es necesario (consulte la descripción general anterior).

      * Desempaquete el archivo WEB-INF/web.xml.
      * Cambie el parámetro sling.run.modes a publish.
      * Elimine los comentarios del parámetro inicial sling.home y establezca esta ruta según sea necesario.
      * Vuelva a empaquetar el archivo web.xml.

   * Cambie el nombre del archivo WAR de AEM a ROOT.war si desea implementarlo como aplicación web raíz. Cambie el nombre a aemauthor.war si desea que aemauthor sea la raíz del contexto.
   * Cópielo en la carpeta de aplicaciones web de tomcat.
   * Espere hasta que AEM esté instalado.
