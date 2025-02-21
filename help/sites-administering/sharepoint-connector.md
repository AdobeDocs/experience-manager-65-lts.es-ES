---
title: Conector de SharePoint
description: Conector JCR de día para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 1%

---

# Conector de SharePoint{#sharepoint-connector}

Este artículo incluye detalles sobre el conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.

El conector SharePoint admite las siguientes funcionalidades básicas:

* Lectura de contenido y metadatos desde SharePoint.
* Reconocimiento de la configuración de seguridad de SharePoint para el contenido accedido mediante la aplicación de la autenticación y autorización nativas de SharePoint
* Integración de contenido mediante el buscador de contenido
* Uso de componentes de AEM, como Recurso externo, para mostrar imágenes y vídeos de SharePoint
* Sincronización de SharePoint con AEM Assets

Todas las funcionalidades se implementan utilizando los servicios web nativos de SharePoint como interfaz para el contenido y los servicios de SharePoint.

>[!NOTE]
>
>SharePoint Connector también es compatible con AEM 6.1 service pack 2. El conector ya no admite el montaje del repositorio virtual y, por lo tanto, no se puede montar. Si desea acceder al repositorio de Sharepoint mediante las API de Java, utilice la implementación del repositorio JCR del conector de Sharepoint en su proyecto.
>
>La instalación, configuración, administración y operaciones de TI del servidor de SharePoint y la infraestructura de TI relacionada están fuera del ámbito de este documento. Consulte la documentación del proveedor de [SharePoint](https://www.microsoft.com/sharepoint) para obtener información sobre estos temas. El conector requiere que estas partes de la infraestructura se instalen, configuren y operen correctamente.
>

## Introducción {#getting-started}

Para empezar a usar el conector, haga lo siguiente:

* Asegúrese de que tiene instalado al menos Java 7.
* Descargue el archivo de distribución del paquete del conector desde Distribución de software.
* Copie un archivo *license.properties* válido en el directorio que contiene el archivo *cq-quickstart-6.4.0.jar*.

* Haga doble clic en el archivo .jar para iniciar AEM o inícielo desde la línea de comandos.
* Instale el paquete del conector desde el Administrador de paquetes.
* Configure las opciones del conector.

## Instalación del conector de SharePoint {#installing-sharepoint-connector}

El conector es un paquete de contenido que facilita la instalación. Instale el paquete mediante el Administrador de paquetes y, a continuación, defina la URL del servidor de SharePoint
y otras opciones de configuración. El contenido de SharePoint está disponible en el repositorio de AEM.

### Requisitos de instalación {#installation-requirements}

El conector requiere lo siguiente:

* Java Runtime Environment 1.7 o posterior
* Servicios web de SharePoint disponibles a través de la red
* URL del servidor de SharePoint
* Credenciales y permisos de usuario para repositorios de CRX y SharePoint
* [Plataformas compatibles](#supported-platforms)

El conector SharePoint está disponible para su descarga desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plataformas compatibles {#supported-platforms}

El conector admite lo siguiente:

* Versiones de AEM:

   * AEM 6.4, 6.3

* Versiones de Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Si necesita soporte para implementaciones personalizadas del conector (OEM, requisitos especiales, métodos de autenticación personalizados), póngase en contacto con la oficina de Adobe de su región.

>[!NOTE]
>
>El conector solo admite configuraciones oficialmente admitidas por Microsoft. Ver [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) y [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisitos del sistema.

### Instalación estándar {#standard-installation}

Distribución de software se utiliza para distribuir funciones de productos, ejemplos y correcciones rápidas. Para obtener más información, consulte la [documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integración con AEM {#integrating-with-aem}

Para instalar el paquete de contenido del conector.

1. Abra un ticket de asistencia de Adobe para solicitar el paquete de funciones del conector.
1. Descargue el paquete cuando esté disponible y, a continuación, abra el Administrador de paquetes de la instancia de AEM.
1. Haga clic en **Instalar** en la página de descripción del paquete.
1. En el cuadro de diálogo **Instalar paquete**, haga clic en **Instalar**.

   **Nota**: Asegúrese de haber iniciado sesión como administrador.

1. Cuando el paquete esté instalado, haga clic en **Cerrar**.

## Configuración del conector de SharePoint {#configuring-sharepoint-connector}

Después de instalar el conector de SharePoint, configure las capas de la aplicación y de SharePoint para el conector.

Establezca la URL del servidor de SharePoint para que el repositorio de SharePoint sea compatible con JCR. Puede definir parámetros adicionales para configurar la conexión con el servidor de SharePoint. Además, configure la autenticación con el conector de SharePoint.

### Configuración de la conexión con el servidor de SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Para establecer la dirección URL del servidor de SharePoint y las opciones avanzadas, realice estos pasos:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque el paquete **Day JCR Connector for Microsoft Sharepoint**.
1. Edite los valores de configuración.
1. Establezca la URL del servidor de SharePoint como el valor de **Workspaces**.
1. Haga clic en **Guardar**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parámetros &quot;Workspaces&quot; y &quot;Nombre de Workspace predeterminado&quot;:

De forma predeterminada, el conector expone un solo espacio de trabajo JCR. El servidor de SharePoint que expone este espacio de trabajo se establece mediante el parámetro de configuración &quot;URL del servidor de SharePoint&quot;.

El conector también se puede configurar para varios espacios de trabajo. En este caso, cada espacio de trabajo está asociado con la dirección URL del servidor de SharePoint correspondiente que se expone a través del espacio de trabajo. Para agregar un espacio de trabajo, agregue una definición de espacio de trabajo al parámetro Workspaces. Una definición de espacio de trabajo tiene el siguiente formato:
`<name>`= `<url>` donde
`<name>` es el nombre del espacio de trabajo JCR y
`<url>` es la dirección URL del servidor de SharePoint para ese espacio de trabajo.

En AEM, realice un paso más aparte de los pasos de configuración anteriores. Lista de permitidos el paquete &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;.

Para realizar la lista de permitidos de paquetes en AEM, realice los siguientes pasos:

1. Vaya a la consola de administración de OSGi: http://localhost:4502/system/console/configMgr.
1. Busque el servicio &quot;Lista blanca de administración de inicio de sesión de Apache Sling&quot;.
1. Seleccione **Omitir la lista blanca**.
1. Agregar `com.day.cq.dam.cq-dam-jcr-connectors` en los paquetes de la lista blanca de forma predeterminada
1. Haga clic en Guardar.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Si configura varios espacios de trabajo, especifique el nombre del espacio de trabajo predeterminado en el parámetro Nombre de Workspace predeterminado.

Para obtener información adicional acerca de los parámetros relacionados con la autenticación, consulte [Autenticación](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verificar la configuración de Sharepoint {#verifying-the-sharepoint-setup}

Después de configurar el conector, compruebe lo siguiente:

* Se ejecuta el servidor de SharePoint y la instancia del conector puede acceder a los servicios web
* Las credenciales de usuario de SharePoint son válidas y el usuario tiene los permisos de SharePoint necesarios
* El conector está instalado y configurado correctamente

### Configuración de la sincronización DAM con el servidor de SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Para sincronizar SharePoint Assets con AEM, realice los siguientes pasos:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque el servicio &quot;Default DAMAsetSynchronization&quot;.
1. Edite los valores de configuración.
1. Configure el nombre de usuario y la contraseña correspondientes del usuario que tiene acceso al sitio de SharePoint.
1. Haga clic en Guardar.

Habilitar el servicio de sincronización DAM, que está deshabilitado de forma predeterminada:

1. Vaya a los componentes de la consola web de OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Busque &quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService&quot;.
1. Haga clic en Habilitar.

De forma opcional, puede configurar la Demora de sincronización entre diferentes ciclos de sincronización:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Busque &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Edite los valores de configuración.
1. Establezca el valor del Período de sincronización (en segundos).
1. Haga clic en Guardar.

### Configurar la autenticación {#configuring-authentication}

Sharepoint incluye los métodos de autenticación Classic y Claims Based, que admiten los siguientes tipos de autenticación:

* Básica
* Basado en Forms

En particular, están disponibles los siguientes tipos de autenticación:

* Classic-Basic
* Basado en Forms clásico
* Reclamaciones básicas
* Argumentos basados en Forms

El conector JCR de AEM para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0. admite la autenticación basada en notificaciones (sugerida por Microsoft), que funciona en los siguientes modos:

* **Autenticación básica/NTLM**: El conector intenta conectarse primero mediante la autenticación básica. Si no está disponible, cambia a la autenticación basada en NTLM.
* **Autenticación basada en Forms**: Sharepoint valida a los usuarios basándose en las credenciales que los usuarios escriben en un formulario de inicio de sesión (normalmente una página web). El sistema emite un token para solicitudes autenticadas que contiene una clave para restablecer la identidad en solicitudes posteriores.

**Configuración de la autenticación basada en Forms**

Ir a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Haga clic en OSGI > Configuración
1. Buscar &quot;Conector JCR de día para Microsoft Sharepoint&quot;
1. Haga clic en Editar los valores de configuración.
1. Establezca el valor de &#39;Sharepoint Connection Factory&#39; como &#39;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&#39;
1. Haga clic en **Guardar**.

**Configuración de la autenticación básica (Windows)**

1. [Deshabilitar autenticación de token](#disable-token-authentication).
1. Vaya a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Haga clic en OSGI > Configuración.
1. Busque **Day JCR Connector for Microsoft Sharepoint**.
1. Haga clic en `Edit the configuration values`.
1. Establezca el valor de la Fábrica de conexiones de Sharepoint en `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Haga clic en **Guardar**.

Solo un usuario autenticado en AEM y SharePoint puede acceder al contenido de SharePoint a través del conector.

También puede utilizar la extensión de conector para la autenticación con el fin de crear un módulo de autenticación personalizado que, por ejemplo, asigne el acceso de los usuarios de AEM a usuarios específicos de SharePoint. Cree los usuarios de AEM correspondientes a los usuarios de SharePoint (el nombre de usuario y la contraseña deben coincidir) para poder ver el contenido de SharePoint asignado a la instancia del conector.

Para crear un usuario en AEM:

1. Inicie sesión en http://localhost:9502/with el usuario administrador.
1. Haga clic en Herramientas.
1. Haga clic en Seguridad.
1. Haga clic en Usuarios.
1. Haga clic en **Crear usuario**.
1. Proporcione el ID de usuario (nombre de usuario con acceso en SharePoint).
1. Proporcione la contraseña correspondiente.
1. Haga clic en el símbolo de graduación Verde para crear el usuario.

Para agregar el usuario al grupo de administradores:

1. Vaya a Administración de grupos.
1. Haga clic en el nodo &quot;a&quot;.
1. Haga clic en &quot;administradores&quot;.
1. Escriba el identificador de usuario creado anteriormente en el cuadro de texto antes del botón **Examinar**.
1. Haga clic en el símbolo de verificación verde para añadir al usuario al grupo de administradores.

### Deshabilitar autenticación de token {#disable-token-authentication}

1. Descargue e instale el paquete `basic auth`. `zip` de Distribución de software.

1. Cerrar inicio rápido.
1. Abra el archivo *\crx-quickstart\repository\repository.xml*.
1. Buscar la etiqueta `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserte la etiqueta `<param name="disableTokenAuth" value="true"/>` dentro de la etiqueta mencionada en el paso 4.
1. Guarde y cierre el archivo xml.
1. Reinicie QuickStart e inicie sesión con sus credenciales.

#### Compatibilidad con distintos métodos de autenticación del servidor de SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

En su versión estándar, el conector admite la autenticación estándar de IIS **Windows** (básica) y la autenticación basada en Forms (basada en token). Se pueden admitir [otros métodos de autenticación](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) a través del mecanismo de extensibilidad.

Los siguientes pasos proporcionan directrices para ampliar la autenticación estándar para admitir varios métodos de autenticación del servidor de SharePoint:

1. Implemente `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` para controlar el lado del cliente de su proceso de autenticación específico.
1. Instale la implementación `SharepointConnectionFactory` como un paquete de fragmentos con el host de fragmentos `com.day.crx.spi.crx2sharepoint-bundle`.

   Al usar Maven, adapte la siguiente configuración de `maven-bundle-plugin` a los requisitos de su proyecto:

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Registre la implementación `SharepointConnectionFactory` en la configuración del conector. En la ventana de configuración del conector, haga clic en **Opciones avanzadas**. En el campo para **Sharepoint Connection Factory**, especifique el nombre de la implementación `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Reinicie el conector.
