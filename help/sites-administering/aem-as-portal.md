---
title: Portales y portlets de AEM
description: Obtenga información sobre cómo configurar y administrar AEM as a portal y cómo configurar y mostrar contenido de AEM en un portlet.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: cf067a359d9f1fbe46e1614d91ce55bf3ee5bf18
workflow-type: tm+mt
source-wordcount: '6081'
ht-degree: 0%

---

# Portales y portlets de AEM{#aem-portals-and-portlets}

Este documento describe lo siguiente:

* Arquitectura del portal de AEM
* Administración y configuración de AEM as a portal
* Uso de AEM como portal
* Instalación, configuración y visualización del contenido de AEM en un portlet (por ejemplo, un servidor web)

## Arquitectura del portal de AEM {#aem-portal-architecture}

La arquitectura del portal de AEM incluye definiciones de portales y portlets.

### ¿Qué es un portal? {#what-is-a-portal}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido de diferentes fuentes y aloja la capa de presentación de los sistemas de información.

Puede ejecutar portlets compatibles con JSR 286 en AEM. El componente portlet permite incrustar un portlet en la página. Consulte [Administración del portlet de contenido de AEM](#administeringthecqcontentportlet).

### ¿Qué es un portlet? {#what-is-a-portlet}

Los portlets son componentes web implementados dentro de un contenedor que generan contenido dinámico. La interfaz del portlet se empaqueta e implementa como un archivo .war dentro de un contenedor de portlet. Si ejecuta AEM como portal, necesita el archivo .war del portlet para ejecutar el portlet.

Para configurar el contenido de AEM para que aparezca en un portal, consulte [Instalación, configuración y uso de AEM en un portlet](#installingconfiguringandusingcqinaportlet).

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director está en desuso desde AEM 6.4 y ahora ya no es compatible con AEM 6.5 LTS. Ver [Funciones obsoletas y eliminadas](/help/release-notes/release-notes.md#deprecated-and-removed-features).

## Administración del portlet de contenido de AEM {#administering-the-aem-content-portlet}

El portlet de contenido de AEM le permite mostrar el contenido de AEM en un portal. El portlet está disponible en `/crx-quickstart/opt/portal` y se puede personalizar de varias formas. Por ejemplo, puede personalizar la administración de SSO/autenticación implementando su propio servicio de autenticación y generando la información de autenticación necesaria para que AEM sobrescriba el comportamiento predeterminado. Los complementos utilizan una API definida que le permite añadir su propia funcionalidad creando el complemento con la API. El complemento se puede implementar en el portlet en ejecución. Para funcionar correctamente, necesita una configuración de la instancia de autor y publicación de AEM junto con la ruta de contenido para mostrarla al inicio.

Algunas de las configuraciones se pueden cambiar mediante las preferencias del portlet y otras mediante las configuraciones del servicio OSGi. Estas configuraciones se cambian usando los archivos **config** o la consola web OSGi.

### Preferencias de portlet {#portlet-preferences}

Las preferencias del portlet se pueden configurar en el momento de la implementación en el servidor del portal o editando el archivo **WEB-INF/portlet.xml** antes de implementar la aplicación web del portlet. El archivo portlet.xml aparece de la siguiente manera de forma predeterminada:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

El portlet se puede configurar con las siguientes preferencias:

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>Esta es la ruta de inicio del portlet: define el contenido que se muestra inicialmente.</p> <p><strong>Importante</strong>: Si el portlet está configurado para conectarse a instancias de autor y publicación de AEM que se ejecutan en una ruta de contexto diferente de<strong> /</strong>, debe habilitar la fuerza <strong>CQUrlInfo</strong> en la configuración del Administrador de bibliotecas HTML de estas instancias de AEM (por ejemplo, a través de Felix Webconsole) o la edición no funcionará y no aparecerá el cuadro de diálogo de preferencias.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>El selector que se anexa a cada dirección URL. De manera predeterminada, este es <strong>portlet</strong>, por lo que todas las solicitudes a páginas html utilizan direcciones URL que terminan en <strong>.portlet.html.</strong> Esto permite el uso de scripts personalizados en AEM para el procesamiento de portlets.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>De forma predeterminada, los archivos css incluidos en la página de HTML de AEM se incluyen en el portlet. Al deshabilitar esta opción, se excluyen los archivos css predeterminados.</p> <p>Si esta opción está habilitada, los archivos CSS se agregan al encabezado de la página HTML o se incrustan en la página HTML según el comportamiento del portal.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>De forma predeterminada, se muestra una barra de herramientas dentro del portlet de contenido para la funcionalidad de administración. Al deshabilitar esta opción, no se representa ninguna barra de herramientas.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Lista de nombres de parámetros de URL alternativos que podrían contener la nueva URL de contenido que se mostrará para el portlet. La lista se procesa de arriba a abajo, se utiliza el primer parámetro que contiene un valor. Si no se encuentra ninguna dirección URL, se utiliza el parámetro de dirección URL predeterminado. La dirección URL proporcionada se utiliza tal cual sin más modificaciones.</p> <p>Esta configuración es por portlet implementado, también es útil para configurar globalmente algunos parámetros de URL en la configuración OSGi para el "Bridge de portlet de Day Portal Director".</p> </td>
  </tr>
  <tr>
   <td>preferencesDialog</td>
   <td>Ruta al cuadro de diálogo de preferencias en AEM: si se deja vacío, se utiliza el cuadro de diálogo de preferencias integrado. El valor predeterminado es /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>De forma predeterminada, el portlet realiza una redirección de JavaScript de toda la página del portal en la primera invocación. Esto es compatible con el escenario de arrastrar y soltar de los servidores de portal modernos. En producción, esta redirección rara vez se necesita y, por lo tanto, se puede desactivar con esta preferencia configurada como <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Consola web OSGi {#osgi-web-console}

Suponiendo que el servidor de portal se ejecute en el host localhost, puerto 8080 y la aplicación web de portlet de AEM esté montada en el contexto de aplicación web *cqportlet*, la dirección URL de la consola web es `https://localhost:8080/cqportlet/cqbridge/system/console`. El usuario y la contraseña predeterminados son **admin**.

Abra la ficha **Configuraciones** y seleccione **Configuración del servidor CQ de Portal Directory**. Aquí se especifica la dirección URL base del autor y la instancia de publicación. Este procedimiento se describe en [Configuración del portlet](#configuring-the-portlet).

>[!NOTE]
>
>La consola web de OSGi solo está pensada para cambiar configuraciones durante el desarrollo (o la prueba). Asegúrese de bloquear las solicitudes a la consola para sistemas de producción.

### Proporcionar configuraciones {#providing-configurations}

Para admitir implementaciones automatizadas y el aprovisionamiento de configuración, el portlet de contenido de AEM tiene compatibilidad de configuración integrada que intenta leer las configuraciones de la ruta de clase proporcionada a la aplicación portlet.

Al iniciar, se lee la propiedad del sistema **com.day.cq.portet.config** para detectar el entorno actual. Normalmente, el valor de esta propiedad es algo así como **dev**, **prod**, **test**, etc. Si no se establece ningún entorno, no se lee ninguna configuración.

Si se establece un entorno, se busca un archivo de configuración en la ruta de clase en* ***com/day/cq/portlet/{env}.config**, donde **env** se reemplaza con el valor real del entorno. Este archivo debe enumerar todos los archivos de configuración para este entorno. La búsqueda de estos archivos se realiza en relación con la ubicación del archivo de configuración. Por ejemplo, si el archivo contiene una línea `my.service.xml,`, este archivo se lee desde la ruta de clase en `com/day/cq/portlet/my.service.config.`. El nombre del archivo consiste en el identificador de persistencia del servicio, seguido de **.config**. En el ejemplo anterior, el identificador de persistencia es **my.service**. El formato del archivo de configuración es el formato utilizado por el instalador OSGi de Apache Sling.

Esto significa que, para cada entorno, es necesario añadir un archivo de configuración correspondiente. Es necesario introducir una configuración que se aplique a todos los entornos en todos estos archivos; si es solo para un entorno, solo se introduce en ese archivo. Este mecanismo garantiza un control total sobre qué configuración se lee en qué entorno.

Es posible utilizar una propiedad del sistema diferente para detectar el entorno. Especifique la propiedad del sistema **com.day.cq.portet.configproperty** que contiene el nombre de la propiedad del sistema que se va a utilizar en lugar de **com.day.cq.portet.config**.

#### Almacenamiento en caché e invalidación de caché {#caching-and-caching-invalidation}

El portlet, en su configuración predeterminada, almacena en caché las respuestas que recibe del WCM de AEM en una caché específica del usuario. Las cachés deben invalidarse cuando se produzcan cambios en el contenido de la instancia de publicación. Para ello, en AEM WCM se debe configurar un agente de replicación en la instancia de autor. La caché también se puede vaciar manualmente. En esta sección se describen ambos procedimientos.

El portlet se puede configurar con su propia memoria caché, de modo que el contenido del portlet se muestre sin necesidad de acceder a AEM. El portal está disponible como contenido en /libs/portal/director. Para acceder al contenido, inicie una instancia de AEM y descargue, con CRXDE Lite o Webdav, el archivo desde esa ubicación.

Puede implementar este paquete en tiempo de ejecución o agregarlo a la aplicación web del portlet en `WEB-INF/lib/resources/bundles` antes de la implementación.

Una vez implementada la caché, el portlet almacena en caché el contenido de la instancia de publicación. La caché del portlet se puede invalidar con un vaciado de Dispatcher desde AEM. Para configurar el portlet para que utilice su propia caché:

1. Configure un agente de replicación en el autor que se dirija al servidor del portal.
1. Suponiendo que el servidor de portal se ejecute en el host **localhost**, **puerto 8080 &#x200B;** y que la aplicación web del portlet de AEM esté montada en el contexto **cqportlet**, la dirección URL para vaciar la caché es `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilice GET como método.
   **Nota:** En lugar de usar un parámetro de solicitud, puede enviar un encabezado http denominado **Ruta**.

#### Vaciar la caché mediante el agente de replicación {#flushing-the-cache-via-replication-agent}

Al igual que la invalidación normal de Dispatcher, se puede configurar un agente de replicación para que se dirija a la caché del portlet de AEM del portal. Después de configurar el agente de replicación, cada activación de página normal vacía la caché del portal.

Si opera varios nodos de portal que ejecutan el portlet de AEM, debe crear un agente para cada nodo como se describe en este procedimiento.

Para configurar un agente de replicación para el portal:

1. Inicie sesión en la instancia de autor.
1. En la ficha Sitios web, haga clic en la ficha *Herramientas*.
1. Haga clic en **Nueva página...** en el menú de agentes de replicación **Nuevo...**.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. En *Plantilla*, seleccione *Agente de replicación* e introduzca un nombre para el agente. Haga clic en *Crear*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Haga doble clic en el agente de replicación que ha creado. Se muestra como no válido porque aún no se ha configurado.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Haga clic en **Editar.**
1. En la ficha **Configuración**, active la casilla de verificación **Habilitado**, seleccione **Vaciado de Dispatcher** como tipo de serialización e introduzca un tiempo de espera de reintento (por ejemplo, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Haga clic en la ficha **Transporte**.
1. En el campo **URI**, introduzca el URI de vaciado (URL) del portlet. El URI tiene el siguiente formato:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Haga clic en la ficha **Ampliado**.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. En el campo **Método HTTP**, escriba **GET**.
1. En el campo **Encabezados HTTP**, haga clic en **+** para agregar una nueva entrada y escriba **Ruta: {path}**.
1. Si es necesario, haga clic en la ficha **Proxy** e introduzca la información de proxy al agente.
1. Haga clic en **Aceptar** para guardar los cambios.
1. Para probar la conexión, haga clic en el vínculo **Probar conexión**. Aparece un mensaje de registro que indica si la prueba de replicación se realizó correctamente. Por ejemplo:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Vaciar manualmente la caché del portlet {#manually-flushing-the-portlet-cache}

Puede vaciar manualmente la caché del portlet accediendo a la misma URL configurada para el agente de replicación. Consulte [Vaciar la caché](#flushing-the-cache-via-replication-agent) para ver la forma de la dirección URL. Además, la dirección URL debe ampliarse con un parámetro de URL Path=&lt;path> para indicar qué se debe vaciar.

Por ejemplo:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` vacía la caché completa. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` vacía `/content/mypage/xyz` de la caché.

### Seguridad de portal {#portal-security}

El portal es el mecanismo de autenticación impulsor. Puede iniciar sesión en AEM con un usuario técnico, el usuario del portal, un grupo, etc. El portlet no tiene acceso a la contraseña del usuario en el portal, por lo que si el portlet no conoce todas las credenciales para iniciar sesión correctamente en un usuario, se debe utilizar una solución SSO. En este caso, el portlet de AEM reenvía toda la información necesaria a AEM, que a su vez reenvía esta información al repositorio de AEM subyacente. Este comportamiento es conectable y se puede personalizar.

### Autenticación al publicar {#authentication-on-publish}

En esta sección se describen los modos de autenticación disponibles que el portlet puede utilizar para comunicarse con las instancias de WCM de AEM subyacentes.

De forma predeterminada, no se envía ninguna información de usuario a la instancia de publicación de AEM; el contenido siempre se muestra como usuario anónimo. Si la información específica del usuario debe entregarse desde AEM o si se requiere la autenticación del usuario para la publicación, esto debe activarse.

#### Acceso a la configuración de autenticación del portlet {#accessing-the-portlet-s-authentication-configuration}

Las opciones de configuración de autenticación que utiliza el portlet en las instancias de AEM WCM están disponibles en la consola web (configuración OSGi).

>[!NOTE]
>
>Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de los servicios OSGi (nodos de consola o de repositorio).
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

Para acceder a la configuración de autenticación del portlet:

1. Acceda a la consola web en la siguiente dirección URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Por ejemplo, en su configuración predeterminada:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Inicie sesión en la consola web. Las credenciales predeterminadas son `admin/admin`.
1. En la consola, seleccione **Configuración**.
1. En el menú **Configuración**, seleccione un servicio en particular para configurarlo. Los servicios los proporciona el portlet en el marco OSGi.

   | Nombre del servicio | Descripción |
   |---|---|
   | Autenticador de Day Portal Director | Configure qué modo de autenticación se utiliza para las instancias de WCM de AEM. Según el modo seleccionado, se puede especificar un usuario técnico o el nombre de la cookie de SSO. Además, se puede habilitar la autenticación para instancias de publicación de WCM de AEM. |
   | Caché de archivos de Day Portal Director | Configure los parámetros de cómo el portlet almacena en caché las respuestas que recibe de las instancias de WCM de AEM. |
   | Servicio de cliente HTTP de Day Portal Director | Configure cómo se conecta el portlet a través de HTTP a las instancias WCM de AEM subyacentes. Por ejemplo, puede especificar un servidor proxy. |
   | Controlador de configuración regional de Day Portal Director | Configure las configuraciones regionales que admite el portlet. Las solicitudes a instancias de AEM WCM se basan en la configuración regional del usuario; por ejemplo, el idioma del usuario *alemán *solicitaría `/content/geometrixx/de/`.... |
   | Administrador de privilegios de Day Portal Director | Configure si el portlet debe probar la ficha Sitios web en función del usuario que ha iniciado sesión actualmente. |
   | Day Portal Director Toolbar Renderer | Personalice la renderización de la barra de herramientas del portlet. |

1. Además, puede configurar la consola web y el servicio de registro. Por ejemplo, puede cambiar las credenciales de administrador para la consola web haciendo clic en el vínculo Consola de administración Apache Felix OSGi.

#### Modo de usuario técnico {#technical-user-mode}

En el modo predeterminado, todas las solicitudes emitidas por el portlet para la instancia de autor de AEM WCM se autentican con el mismo usuario técnico, independientemente del usuario del portal actual. El modo de usuario técnico está activado de forma predeterminada. Puede habilitar/deshabilitar este modo en la pantalla de configuración correspondiente de la consola de administración OSGi:

El usuario técnico especificado debe existir en la instancia de autor de AEM WCM y en la instancia de publicación si **Autenticar en la publicación** está habilitado. Asegúrese de otorgar al usuario los privilegios de acceso suficientes para el trabajo de creación.

#### SSO {#sso}

El portlet es compatible con SSO con AEM de forma predeterminada. El servicio de autenticación se puede configurar para que utilice SSO y transmita a AEM al usuario del portal actual con el formato **Basic** como una cookie denominada `cqpsso`. AEM debe configurarse para utilizar el controlador de autenticación SSO para la ruta /. El nombre de la cookie también debe configurarse aquí.

`crx-quickstart/repository/repository.xml` para el repositorio de AEM debe configurarse en consecuencia:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modo de autenticación SSO {#sso-authentication-mode}

El portlet puede autenticarse para AEM WCM mediante el esquema de inicio de sesión único (SSO). En este modo, el usuario que ha iniciado sesión en el portal se reenvía a AEM WCM en forma de cookie SSO. Si se utiliza el modo SSO, todos los usuarios del portal con acceso al portlet de AEM deben ser conocidos por las instancias WCM de AEM subyacentes, normalmente en forma de WCM de AEM conectado a LDAP o creando manualmente los usuarios de antemano. Además, antes de habilitar SSO en el portlet, la instancia de autor de AEM WCM subyacente (y la instancia de publicación, si **Autenticar en publicación** está habilitada) deben configurarse para aceptar solicitudes basadas en SSO.

Para configurar el portlet para que utilice el modo de autenticación SSO, complete los siguientes pasos (descritos en detalle en las secciones siguientes):

* Habilite el repositorio de AEM WCM para aceptar credenciales de confianza.
* Habilite la autenticación SSO en el WCM de AEM.
* Habilite la autenticación SSO en el portlet de AEM.

#### Habilitar el repositorio de AEM WCM para aceptar credenciales de confianza {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Para poder habilitar SSO para AEM WCM, es necesario configurar el repositorio subyacente para que acepte las credenciales de confianza proporcionadas por AEM WCM. Para ello, configure el archivo repository.xml de AEM.

1. En el sistema de archivos donde está instalado AEM WCM, abra el siguiente archivo:

   `//crx-quickstart/repository/repository.xml`

1. En el archivo XML, busque la entrada para **LoginModule** y agregue trust_credentials_attribute a su configuración:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Reinicie AEM WCM para que los cambios surtan efecto.

#### Habilitar la autenticación SSO en el WCM de AEM {#enabling-sso-authentication-in-the-aem-wcm}

Para habilitar SSO en AEM WCM, acceda a la entrada de configuración correspondiente en la consola de administración web Apache Felix (OSGi) de AEM WCM:

1. Acceda a la consola a través de su URI en https://&lt;AEM-host>:&lt;port>/system/console.
1. En el menú Configuración, seleccione Controlador de autenticación SSO. En este ejemplo, el controlador SSO acepta solicitudes SSO para todas las rutas en función de la cookie proporcionada por el portlet de AEM. La configuración puede variar.

   | Ruta | / | Habilita el controlador SSO para todas las solicitudes |
   |---|---|---|
   | Nombres de cookies | cqpsso | Nombre de la cookie proporcionada por el portlet tal como se configura en la consola OSGi del portlet. |

1. Haga clic en **Guardar** para habilitar el SSO. SSO es ahora el esquema de autenticación principal.

Por cada solicitud que recibe AEM WCM, primero se intenta la autenticación basada en SSO. Si se produce un error, se vuelve al esquema de autenticación básico habitual. Como tal, las conexiones normales a AEM WCM sin SSO siguen siendo posibles.

#### Habilitar la autenticación SSO en un portlet de AEM {#enabling-sso-authentication-in-a-aem-portlet}

Para que la instancia WCM de AEM subyacente acepte solicitudes de SSO, el modo de autenticación del portlet debe cambiarse de **Técnico** a **SSO**.

Para habilitar la autenticación SSO en un portlet de AEM:

1. Acceda a la consola a través de su URI en https://&lt;aem-host>:&lt;port>/system/console.
1. En el menú Configuración, seleccione Autenticador de Day Portal Director en la lista de configuraciones disponibles.
1. En Modo, seleccione SSO. Deje los demás parámetros con sus valores predeterminados.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Haga clic en Guardar para habilitar SSO para el portlet.

   Para realizar pruebas, acceda al portlet con el usuario administrativo del portal, después de crear el mismo usuario en AEM WCM con privilegios de administrador.

Después de realizar este procedimiento, las solicitudes se autentican mediante SSO. Un fragmento típico de la comunicación HTTP revela la presencia de los siguientes encabezados específicos de SSO y Portlet:

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### Habilitación de la autenticación PIN {#enabling-pin-authentication}

Si no utiliza las funciones de edición en línea predeterminadas del portlet de contenido de AEM, pero desea que la parte de creación y administración del portlet esté fuera del portal directamente en la instancia de autor de AEM, debe habilitar la autenticación PIN. También debe cambiar la configuración de los botones de administración.

Para abrir la página de administración del sitio web o editar una página desde el portlet, el portlet de contenido de AEM utiliza la nueva autenticación de pin. De forma predeterminada, la autenticación de clavijas está desactivada, por lo que deben realizarse los siguientes cambios de configuración en AEM:

1. Habilite la autenticación de confianza en AEM agregando la información de confianza en el archivo repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. En la consola de configuración de OSGi, ubicada de manera predeterminada en https://localhost:4502/system/console/configMgr, seleccione **Controlador de autenticación PIN de CQ** en el menú desplegable.
1. Edite el parámetro **URL Root Path** para que contenga únicamente el valor único **/**.

### Privilegios {#privileges}

Algunas funciones del portlet están protegidas por privilegios. El usuario actual necesita tener este privilegio para poder acceder a esta función. Hay los siguientes privilegios predefinidos:

* &quot;toolbar&quot; : Este es el privilegio general para ver/utilizar la barra de herramientas en el portlet.
* &quot;prefs&quot; : si el usuario tiene este privilegio, se le permite ver o cambiar las preferencias del portlet.
* &quot;cq-author:edit&quot; : Con este privilegio, el usuario puede invocar la vista de edición del contenido.
* &quot;cq-author:preview&quot; : Con este privilegio, el usuario puede ver la vista previa.
* &quot;cq-author:siteadmin&quot; : Con este privilegio, se permite al usuario abrir siteadmin en AEM.

El mejor método para administrar los privilegios es utilizar las funciones de portal y asignarles funciones. Esto se puede hacer mediante una configuración OSGi. El &quot;Administrador de privilegios de Day Portal Director&quot; se puede configurar con un conjunto de funciones para cada privilegio. Si el usuario tiene uno de los roles, el usuario tiene el privilegio correspondiente.

Además, es posible definir esta función en función del acceso por base de instancia de portlet. El cuadro de diálogo de preferencias del portlet contiene un campo de entrada para cada uno de los privilegios anteriores. Para cada privilegio se puede configurar una lista de funciones de portlet separadas por coma. Si se configura un valor, esto anula la configuración global del servicio &quot;Administrador de privilegios de Day Portal Director&quot; y podría ser necesario agregar los mismos roles de esta configuración global, ya que los roles no se combinan. Si no se especifica ningún valor, se utiliza la configuración global.

### Personalizar la aplicación de portlet de AEM {#customizing-the-aem-portlet-application}

La aplicación de portlet de AEM proporcionada inicia un contenedor OSGi dentro de la aplicación web, tal como lo hace AEM. Esta arquitectura le permite utilizar todas las ventajas de OSGi:

* Fácil de actualizar y ampliar
* Proporciona actualizaciones rápidas del portlet sin ninguna interacción del servidor del portal
* Fácil de personalizar el portlet

### Botones de barra {#toolbar-buttons}

La barra de herramientas y sus botones se pueden configurar y personalizar. Puede añadir sus propios botones a la barra de herramientas o definir qué botones se muestran en qué modo. Cada botón es un servicio OSGi configurable mediante una configuración OSGi.

La consola web de OSGi enumera todas las configuraciones de botón en la ficha **Configuración**. Para cada botón, puede definir en qué modo se muestra este botón. Esto permite desactivar un botón, por ejemplo, eliminando todos los modos.

De forma predeterminada, el portlet de contenido de AEM utiliza la funcionalidad de edición en línea. Sin embargo, si prefiere cambiar a la instancia de autor de AEM para editarla, habilite **SiteAdmin Button** y **ContentFinder Button**, pero deshabilite **Edit Button**. En este caso, asegúrese de configurar correctamente la autenticación PIN en AEM.

El diseño de la barra de herramientas del portlet se puede personalizar instalando un paquete a través de la consola web Felix del portlet, que contiene CSS/HTML personalizados en una ubicación predefinida.

#### Estructura del paquete {#bundle-structure}

A continuación se muestra un ejemplo de estructura de paquete:

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

La carpeta META-INF contiene el archivo MANIFEST.MF requerido por OSGi para identificarlo como un paquete. Aparece de la siguiente manera:

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

El portlet exige el hecho de que las imágenes de HTML/CSS se encuentren en la carpeta /com/day/cq/portlet/toolbar/layout, y no se puede cambiar. En la misma línea, los encabezados Import-Package y Export-Package en MANIFEST.MF también deben llamarse /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName debe ser un nombre de paquete único y completo.

Puede crearlo con una herramienta como maven o crear manualmente un archivo jar de este tipo con el encabezado relevante establecido como se muestra en esta sección.

#### Vistas de barra de portlets {#portlet-toolbar-views}

La barra de herramientas del portlet tiene básicamente dos estados de vista. Cada vista y los botones asociados se pueden personalizar con un archivo HTML correspondiente.

#### Vista de publicación {#publish-view}

La vista de publicación solo tiene un botón que cambia la barra de herramientas a la vista Administrar. La vista de publicación está representada por el archivo publish.html en [paquete anterior](/help/sites-deploying/configuring-osgi.md#bundles). En HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesa:

#### Marcadores de posición de vista Publicar {#publish-view-placeholders}

| Cadena de marcador | Descripción |
|---|---|
| {buttonManage} | El marcador de posición se reemplazó con el botón **Administrar**, que cambia el estado del portlet al estado de administración. |

#### Administrar vista {#manage-view}

La vista de administración tiene cuatro botones: Editar, pestaña Sitios web, Actualizar y Atrás. La vista de administración está representada por el archivo manage.html del [paquete anterior](/help/sites-deploying/configuring-osgi.md#bundles). En HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesa:

#### Administrar marcadores de posición de vista {#manage-view-placeholders}

| Cadena de marcador | Descripción |
|---|---|
| {buttonEdit} | El marcador de posición se reemplazó con el botón **Editar**, que abre una nueva ventana con la página actual en el modo de edición de AEM. |
| {buttonWebsites} | Marcador de posición, reemplazado por un botón que abre la pestaña Sitios web de AEM WCM. |
| {buttonRefresh} | Actualiza la vista actual. |
| {buttonBack} | Vuelve a cambiar el portlet a la vista de publicación. |

#### Botones {#buttons}

Los botones, independientemente de la vista en la que aparezcan, utilizan el mismo HTML común, definido en button.html.

En HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesa:

#### Botones Administrar y Publicar vista {#manage-and-publish-view-buttons}

| Cadena de marcador | Descripción |
|---|---|
| {name} | Nombre del botón, por ejemplo,**autor, atrás, actualizar**, etc. |
| {id} | ID de CSS del botón. |
| {url} | URL del destino del botón. |
| {text} | Etiqueta del botón. |
| {onclick} | Función **onclick** de JavaScript (contiene {url}). |

Ejemplo de archivo button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Instalación de un diseño personalizado {#installing-a-custom-layout}

Para instalar un diseño personalizado, acceda a la sección Consola web OSGI del portlet **Paquetes &#x200B;** y cargue el paquete.

#### Paquetes {#packages}

Si necesita cargar o crear paquetes para la instalación, consulte Administrador de paquetes en la documentación de AEM para obtener instrucciones detalladas.

### Administración de vínculos {#link-handling}

Todos los vínculos se reescriben para que funcionen en el contexto del portal. De forma predeterminada, se utilizan vínculos con parámetros de procesamiento. El reescritor de HTML de Portal Director se puede configurar para que utilice vínculos de acción en su lugar.

También puede definir parámetros de solicitud adicionales para consultar la ruta de contenido que se va a mostrar. Esto resulta útil, por ejemplo, si hay un vínculo desde el exterior a contenido específico.

Además, la reescritura de HTML de Portal Director se puede configurar con una lista de expresiones regulares definidas que excluyen la reescritura de vínculos. Por ejemplo, si tiene vínculos relativos a sistemas externos, debe añadirlos a esta lista de exclusión.

### Localización {#localization}

El portlet de contenido de AEM tiene una función de localización integrada que garantiza que el contenido de AEM esté en el idioma correcto.

Esto se realiza en dos pasos:

1. El detector de configuración regional del directorio de portal detecta la configuración regional del usuario del portal al obtener la configuración regional del portal. Este servicio debe configurarse con la lista de idiomas disponibles en AEM.
1. El controlador de configuración regional de Portal Director administra la localización de la solicitud actual. Toma la ruta del contenido solicitado, por ejemplo, `/content/geometrixx/en/company.html` y según la configuración, reescribe **en** con la configuración regional real del usuario.

El controlador de configuración regional de Portal Director se puede configurar con las rutas para comprobar la información de configuración regional; normalmente incluye todo lo que hay bajo `/content` y con la posición de la información de configuración regional en la ruta. De forma predeterminada, el controlador de configuración regional sigue la recomendación de estructurar sitios en varios idiomas dentro de AEM.

Si el sitio no tiene una regla estricta para administrar la información de configuración regional dentro de la ruta, es posible reemplazar el controlador de configuración regional con su propia implementación.

### Servicios OSGi opcionales {#optional-osgi-services}

Se pueden implementar servicios OSGi opcionales para personalizar varias partes del portlet. Cada servicio corresponde a una interfaz de Java. Esta interfaz se puede implementar mediante un paquete en el portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>El rastreador de solicitudes recibe una notificación cada vez que el portlet muestra contenido. Esto permite realizar un seguimiento de las invocaciones del portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Listener que se invoca al principio y al final de cada solicitud al portlet. El agente de escucha se puede usar para cambiar o agregar información para la solicitud actual.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Controlador de error personalizado para errores durante la fase de procesamiento.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Este servicio se puede utilizar para agregar información a cada invocación de http a AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Agregar una acción propia al portlet: esta acción se puede invocar mediante un vínculo de acción del portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Este servicio se puede utilizar para decorar el contenido del portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Añada su propio proveedor de recursos para enviar algún recurso al cliente a través de un vínculo de recurso de portlet.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permite publicar archivos de HTML, CSS y JavaScript de procesamiento.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Agregue su propio botón a la barra de herramientas.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Agregue un servicio para aplicar una asignación de URL personalizada o para reescribir.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Añada su propia información sobre el usuario. Este servicio se puede utilizar para obtener información del portal al portlet.</td>
  </tr>
 </tbody>
</table>

#### Reemplazar servicios predeterminados {#replacing-default-services}

Los siguientes servicios tienen una implementación predeterminada en el portlet de contenido (con una interfaz Java correspondiente). Para personalizar, es necesario implementar un paquete que contenga la nueva implementación de servicio en la aplicación de portlet.

Al implementar un servicio de este tipo, asegúrese de establecer la propiedad **service.ranking** del servicio en un valor positivo. La implementación predeterminada utiliza la clasificación **&#x200B; 0** y el portlet utiliza el servicio con la clasificación más alta.

| **Nombre** | **Descripción** | **Comportamiento predeterminado** |
|---|---|---|
| Autenticador | Proporciona la información de autenticación a AEM | Utiliza un usuario técnico configurable tanto para creación como para publicación. O se puede utilizar SSO. |
| HTMLRewriter | Reescribe vínculos e imágenes | Reescribe los vínculos de AEM en vínculos de portal; se pueden extender mediante un UrlMapper y un TextMapper |
| HttpClientService | Gestiona todas las conexiones http | Implementación estándar |
| LocaleHandler | Gestiona la información de configuración regional | Reescribe un vínculo al contenido con respecto a la configuración regional. |
| LocaleDetector | Detecta la configuración regional del usuario. | Utiliza la configuración regional proporcionada por el portal. |
| PrivilegeManager | Comprueba los derechos de usuario | Comprueba el acceso a la instancia de autor si el usuario puede editar el contenido |
| ToolbarRenderer | Procesa la barra de herramientas | Agrega una funcionalidad de barra de herramientas |

### Eventos de portlet {#portlet-events}

La API de portlet (JSR-286) especifica los eventos de portlet. El portlet de contenido de AEM tiene un puente integrado que distribuye eventos de portlet para el portlet de AEM como eventos OSGi, lo que hace que la administración de eventos de portlet sea conectable.

Si desea controlar eventos específicos, declárelos como eventos de recepción en el descriptor de implementación (o configúrelos a través del servidor de portal) e implemente un servicio OSGi que declare la interfaz EventHandler (consulte la especificación OSGi EventAdmin).

Cada vez que se produce un evento de portlet, se envía un evento OSGi específico invocando al controlador. El controlador obtiene toda la información de contexto y puede actualizar el estado del portlet en consecuencia o enviar nuevos eventos. Básicamente, dentro del método handle se puede utilizar toda la funcionalidad de la fase de evento portlet.

## Uso de AEM como portal {#using-aem-as-a-portal}

Utilice el componente Portlet para agregar ventanas de portlet a las páginas de AEM. Las bibliotecas compartidas que instala en el servidor de aplicaciones permiten que el componente Portlet detecte las aplicaciones de portlet implementadas.

Para utilizar AEM como portal, realice las siguientes tareas:

1. Instale el componente Portlet y las bibliotecas compartidas.
1. Agregue el componente Portlet a Sidekick.
1. Configure e implemente la aplicación web que contiene los portlets que desea que aparezcan en el componente Portal.
1. Agregue el componente Portlet a una página y seleccione el portlet que desea mostrar.

>[!NOTE]
>
>Solo puede utilizar el componente portlet cuando AEM se implemente como aplicación web. ([Consulte Instalación de AEM con un servidor de aplicaciones](/help/sites-deploying/application-server-install.md).)

### Instalación del componente de portlet {#installing-the-portlet-component}

El archivo JAR de inicio rápido de AEM contiene los archivos del componente portlet. Para obtener los archivos (cq-portlet-components.zip), puede ejecutar Quickstart o extraer el contenido.

1. Ejecute o extraiga el contenido del archivo JAR de Quickstart y busque el archivo cq-portlet-components.zip como corresponda:

   * Ejecutar Quickstart: crx-quickstart/opt/portal
   * Extraer contenido de Quickstart: static/opt/portal

1. Abra el Administrador de paquetes de la instancia de autor CQ5 implementada en el servidor de aplicaciones. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Use Administrador de paquetes para [cargar e instalar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) el paquete cq-portlets-components.zip.

   El paquete instala cq-portlet-director-sharedlibs-x.x.x.jar en la carpeta /libs/portal/director del repositorio.

1. Copie cq-portlet-director-sharedlibs-x.x.x.x.jar en el disco duro. Utilice cualquier medio para obtener el archivo, por ejemplo, FileVault o un cliente WebDAV.
1. Mueva el archivo cq-portlet-director-sharedlibs.x.x.x.jar a la carpeta de biblioteca compartida del servidor de aplicaciones para que las clases estén disponibles para las aplicaciones de portlet implementadas.

### Adición del componente Portlet a Sidekick {#adding-the-portlet-component-to-sidekick}

Agregue el componente portlet al sistema de párrafos para que esté disponible para los autores.

1. En Sidekick, haga clic en el icono de regla para acceder al modo de diseño.
1. Junto al encabezado `Design of par` sobre el primer párrafo, haga clic en **Editar**.

1. En la categoría de componente **General**, active la casilla de verificación situada junto al componente Portlet y haga clic en Aceptar.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configuración e implementación de las aplicaciones de portlet {#configuring-and-deploying-your-portlet-applications}

Implemente los portlets en el contenedor web del servidor de aplicaciones para que estén disponibles para el componente Portal. Antes de implementar la aplicación de portlet, debe configurarla para que cargue el servlet contenedor del portal de AEM. Esta configuración permite que el componente Portlet acceda a los portlets.

1. Extraiga el contenido del archivo WAR de la aplicación de portlet.

   **Sugerencia:** El comando jar xf *nameofapp*.war extrae los archivos.

1. Abra el archivo web.xml en un editor de texto.
1. Añada la siguiente configuración de servlet dentro del elemento web-app:

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. Guarde el archivo web.xml y vuelva a empaquetar el archivo WAR.

   **Sugerencia:** El comando `jar cvf nameofapp.war *` agrega contenido del directorio actual al archivo nameofapp.war.

1. Implemente la aplicación de portlet en el servidor de aplicaciones. Para obtener más información, consulte la documentación del servidor de aplicaciones.

### Añadir portlets a la página de AEM {#adding-portlets-to-your-aem-page}

Utilice el componente Portal para añadir una ventana de portlet a la página web. Utilice las propiedades del componente para especificar el portlet que se va a mostrar.

1. En la página web, arrastre el componente **Portlet** del grupo General en Sidekick a la página.

   >[!NOTE]
   >
   >Después de arrastrar el componente a la página, vuelva a cargar la página para asegurarse de que funciona correctamente.

1. Haga doble clic en el componente para abrir las propiedades del portlet.
1. En el menú desplegable **Entidad de portlet**, seleccione el portlet en la lista.
1. Active o desactive la casilla de verificación **Ocultar barra de título &#x200B;** en función de si desea ver la barra de título del portlet.
1. En el campo **Ventana de portlet**, escriba un identificador de ventana de portlet único, si lo desea.

   >[!NOTE]
   >
   >Si planea usar el mismo portlet más de una vez en la misma página, asigne a cada portlet un ID de ventana diferente.

1. Haga clic en **Aceptar**. El portlet se muestra en la página de AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Instalación, configuración y uso de AEM en un portlet {#installing-configuring-and-using-aem-in-a-portlet}

Para acceder al contenido proporcionado por AEM WCM, el servidor del portal debe estar equipado con el portlet de AEM Portal Director. Para ello, instale, configure y agregue el portlet a la página del portal siguiendo los pasos que se indican en esta sección.

De forma predeterminada, el portlet se conecta a la instancia de publicación en localhost:4503 y a la instancia de autor en localhost:4502. Estos valores se pueden cambiar durante la implementación del portlet. El director del portal está disponible como contenido en el repositorio en /libs/portal/directory. Descargue el archivo WAR de la aplicación antes de utilizarlo.

### Descarga del archivo WAR {#downloading-the-war-file}

1. Con Webdav o CRXDE Lite, vaya a /libs/portal/director.

1. Descargar *cq-portlet-webapp.war*.

>[!NOTE]
>
>Estos procedimientos utilizan el portal Websphere como ejemplo, aunque son lo más genéricos posible; los procedimientos varían para otros portales web. Aunque los pasos son esencialmente idénticos para todos los portales web, debe reutilizar los pasos para su portal web en particular.

#### Instalación del portlet {#installing-the-portlet}

Para instalar el portlet:

1. Inicie sesión en el portal con privilegios de administrador.
1. Vaya a la parte de Portlet Management del portal web.
1. Haga clic en Instalar, vaya a la aplicación de portlet de AEM (cq-portlet-webapp.war) que descargó e introduzca otra información importante sobre el portlet.

   Para otra información esencial del portlet, puede aceptar los valores predeterminados o cambiar los valores. Si acepta los valores predeterminados, el portlet estará disponible en https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. La consola de administración OSGi proporcionada por el portlet está disponible en https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (el nombre de usuario y la contraseña predeterminados son admin/admin).

1. Asegúrese de que la aplicación de portlet se inicia automáticamente seleccionando esa opción o casilla de verificación y guarde los cambios. Verá un mensaje que indica que la instalación se ha realizado correctamente.

#### Configuración del portlet {#configuring-the-portlet}

Después de instalar el portlet, debe configurarlo para que conozca las direcciones URL de las instancias de AEM subyacentes (autor y publicación). También puede configurar otras opciones.

Para configurar el portlet:

1. En la ventana Administración de portal del servidor de aplicaciones, vaya a Administración de portlets, donde se muestran todos los portlets, y seleccione el portlet de AEM Portal Director.
1. Configure el portlet según sea necesario. Por ejemplo, es posible que tenga que cambiar la dirección URL de las instancias de autor y publicación y la dirección URL de la ruta de inicio. Las configuraciones predeterminadas se describen en [Preferencias de portlet](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >Si el portlet está configurado para conectarse a instancias de autor y publicación de AEM que se ejecutan en una ruta de contexto diferente de **/**, debe habilitar la fuerza **CQUrlInfo** en la configuración del administrador de bibliotecas HTML de estas instancias de AEM (por ejemplo, a través de Felix Webconsole) o la edición no funcionará y no aparecerá el cuadro de diálogo de preferencias.

1. Guarde los cambios de configuración en el servidor de aplicaciones.

1. Vaya a Admin Console de OSGI para el portlet. La ubicación predeterminada es `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. El nombre de usuario y la contraseña predeterminados son **admin/admin**.

1. Seleccione la configuración de **Day Portal Director CQ Server Configuration** y edite los siguientes valores:

   * **URL base del autor**: URL base de la instancia de autor de AEM.
   * **URL de base de publicación**: URL de base para la instancia de publicación de AEM.
   * **El autor se usa como publicación**: ¿la instancia del autor se usa como publicación?
instancia de (para desarrollo)?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Haga clic en **Guardar**. Ahora puede agregar el portlet a las páginas del portal y utilizar el portal.

### URL de contenido {#content-urls}

Cuando se solicita contenido desde AEM, el portlet utiliza el modo de visualización actual (publicación o autor) y la ruta actual para combinar una dirección URL completa. Con los valores predeterminados, la primera dirección URL es `https://localhost:4503/content/geometrixx/en.portlet.html`. El valor de `htmlSelector` se agrega automáticamente a la dirección URL antes de la extensión.

Si el portlet cambia al modo de ayuda y se selecciona `appendHelpViewModeAsSelector`, también se anexa el selector `help`, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Si la ventana del portlet está maximizada y se selecciona `appendMaxWindowStateAsSelector`, el selector también se anexa, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Los selectores se pueden evaluar en AEM y se puede utilizar una plantilla diferente para distintos selectores.

### Uso de un mapa de URL de contenido en AEM {#using-a-content-url-map-in-aem}

Normalmente, la ruta de inicio apunta directamente al contenido en AEM. Sin embargo, si desea mantener las rutas de inicio en AEM en lugar de en las preferencias del portlet, puede apuntar la ruta de inicio a un mapa de contenido en AEM, como `/var/portlets`. En este caso, un script que se ejecute en AEM puede utilizar la información enviada desde el portlet para decidir qué URL es la de inicio. Debe emitir un redireccionamiento a la dirección URL correcta.

#### Agregar el portlet a la página del portal {#adding-the-portlet-to-the-portal-page}

Para agregar el portlet a la página del portal:

1. Asegúrese de que se encuentra en la ventana de administración del servidor de aplicaciones y vaya a la ubicación donde administra las páginas. (por ejemplo, en WebSphere 6.1, haga clic en **Administrar páginas**).
1. Seleccione el nombre del portlet y seleccione una página existente o cree una página.
1. Edite el diseño de página.
1. Seleccione el portlet y agréguelo a un contenedor.
1. Guarde los cambios.

#### Uso del portlet {#using-the-portlet}

Para acceder a la página que agregó al portlet:

1. En el menú de personalización del portlet, configure el portlet como lo configuró en el portal.
1. Abra la configuración (el portlet muestra la URL de inicio de publicación configurada en la configuración del portlet), realice las modificaciones necesarias y guárdelas.
