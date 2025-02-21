---
title: Configuración de notificaciones por correo electrónico
description: Obtenga información sobre cómo configurar las notificaciones por correo electrónico en Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 8ed6afaa78f8f916b15977dda339cb4a3ae934b0
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 8%

---


# Configuración de notificaciones por correo electrónico{#configuring-email-notification}

AEM envía notificaciones por correo electrónico a los usuarios que:

* Se han suscrito a eventos de página como, por ejemplo, modificaciones o replicaciones. La sección [Bandeja de entrada de notificaciones](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) describe cómo suscribirse a estos eventos.

* Se ha suscrito a eventos de foro.
* Deben realizar un paso en un flujo de trabajo. En la sección [Paso de participante](/help/sites-developing/workflows-step-ref.md#participant-step) se describe cómo almacenar en déclencheur las notificaciones por correo electrónico en un flujo de trabajo.

Requisitos previos:

* Los usuarios deben tener una dirección de correo electrónico válida definida en su perfil.
* El servicio de correo CQ **Day** debe configurarse correctamente.

Cuando se notifica a un usuario, este recibe un correo electrónico en el idioma definido en su perfil. Cada idioma tiene su propia plantilla que se puede personalizar. Se pueden añadir nuevas plantillas de correo electrónico para los nuevos idiomas.

>[!NOTE]
>
>Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Configuración del servicio de correo {#configuring-the-mail-service}

Para que AEM pueda enviar correos electrónicos, el **servicio Day CQ Mail** debe estar configurado correctamente. Puede ver la configuración en la consola web. Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

Se aplican las siguientes restricciones:

* El **puerto del servidor SMTP** debe ser 25 o superior.

* El **nombre de host del servidor SMTP** no debe estar en blanco.
* La dirección **&quot;Desde&quot;** no debe estar en blanco.

Para ayudarle a depurar un problema con el **servicio Day CQ Mail**, puede observar los registros del servicio:

`com.day.cq.mailer.DefaultMailService`

La configuración tiene el siguiente aspecto en la consola web:

![Ventana de configuración OSGi del servicio Day CQ Mail](assets/chlimage_1-276.png)

## Configuración del canal de notificación por correo electrónico {#configuring-the-email-notification-channel}

Al suscribirse a las notificaciones de eventos de páginas o foros, la dirección de correo electrónico de origen se establece en `no-reply@acme.com` de forma predeterminada. Puede cambiar este valor configurando el servicio **Canal de correo electrónico de notificación** en la consola web.

Para configurar la dirección de correo electrónico de origen, agregue un nodo `sling:OsgiConfig` al repositorio. Utilice el siguiente procedimiento para añadir el nodo directamente mediante CRXDE Lite:

1. En CRXDE Lite, agregue una carpeta denominada `config` debajo de la carpeta de la aplicación.
1. En la carpeta de configuración, añada un nodo denominado:

   `com.day.cq.wcm.notification.email.impl.EmailChannel` de tipo `sling:OsgiConfig`

1. Agregue una propiedad `String` al nodo denominado `email.from`. Para el valor, especifique la dirección de correo electrónico que desea utilizar.

1. Haga clic en **Guardar todo**.

Utilice el siguiente procedimiento para definir el nodo en las carpetas de origen del paquete de contenido:

1. En su `jcr_root/apps/*app_name*/config folder`, cree un archivo denominado `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. Agregue el siguiente XML para representar el nodo:

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. Reemplace el valor del atributo `email.from` (`name@server.com`) por su dirección de correo electrónico.

1. Guarde el archivo.

## Configuración del servicio de notificaciones de correo electrónico de flujo de trabajo {#configuring-the-workflow-email-notification-service}

Cuando recibe notificaciones por correo electrónico del flujo de trabajo, tanto la dirección de correo electrónico de origen como el prefijo de URL del host se establecen en valores predeterminados. Puede cambiar estos valores configurando el **Servicio de notificación por correo electrónico del flujo de trabajo CQ por día** en la consola web. Si lo hace, se recomienda mantener el cambio en el repositorio.

La configuración predeterminada tiene el siguiente aspecto en la consola web:

![Ventana de configuración del servicio de notificación por correo electrónico del flujo de trabajo de CQ diario](assets/chlimage_1-277.png)

### Plantillas de correo electrónico para notificación de página {#email-templates-for-page-notification}

Las plantillas de correo electrónico para las notificaciones de página se encuentran a continuación:

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

La plantilla predeterminada en inglés ( `en.txt`) se define de la siguiente manera:

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalizar plantillas de correo electrónico para notificaciones de páginas {#customizing-email-templates-for-page-notification}

Para personalizar la plantilla de correo electrónico en inglés para la notificación de página:

1. Creación de una superposición para notificaciones de página

1. Abra el archivo:

   `en.txt`

1. Modifique el archivo según sus necesidades.
1. Guarde los cambios.

La plantilla debe tener el siguiente formato:

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

Donde &lt;text_x> puede ser una combinación de texto estático y variables de cadena dinámicas. Se pueden utilizar las siguientes variables dentro de la plantilla de correo electrónico para las notificaciones de página:

* `${time}`, la fecha y hora del evento.

* `${userFullName}`, el nombre completo del usuario que activó el evento.

* `${userId}`, el identificador del usuario que activó el evento.
* `${modifications}`, describe el tipo del evento de página y la ruta de página con el formato:

  &lt;tipo de evento de página> => &lt;ruta de página>

  Por ejemplo:

  PageModified => /content/geometrixx/en/products

### Plantillas de correo electrónico para notificación de flujo de trabajo {#email-templates-for-workflow-notification}

La plantilla de correo electrónico para las notificaciones del flujo de trabajo (inglés) se encuentra en:

`/libs/settings/workflow/notification/email/default/en.txt`

Se define de la siguiente manera:

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### Personalizar plantillas de correo electrónico para notificación de flujo de trabajo {#customizing-email-templates-for-workflow-notification}

Para personalizar la plantilla de correo electrónico en inglés para la notificación de eventos de flujo de trabajo:

1. Creación de una superposición para las notificaciones de flujo de trabajo

1. Abra el archivo:

   `en.txt`

1. Modifique el archivo según sus necesidades.
1. Guarde los cambios.

La plantilla debe tener el siguiente formato:

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>Donde `<text_x>` puede ser una combinación de texto estático y variables de cadena dinámicas. Cada línea de un elemento `<text_x>` debe finalizar con una barra invertida (`\`), excepto en la última instancia, cuando la ausencia de la barra invertida indica el final de la variable de cadena `<text_x>`.
>
>Encontrará más información sobre el formato de plantilla en el [javadocs del método Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-).

El método `${payload.path.open}` revela la ruta a la carga útil del elemento de trabajo. Por ejemplo, para una página en Sites, entonces `payload.path.open` sería similar a `/bin/wcmcommand?cmd=open&path=…`.; no tiene el nombre del servidor, por lo que la plantilla antepone `${host.prefix}`.

Se pueden utilizar las siguientes variables dentro de la plantilla de correo electrónico:

* `${event.EventType}`, tipo de evento
* `${event.TimeStamp}`, fecha y hora del evento
* `${event.User}`, el usuario que activó el evento
* `${initiator.home}`, la ruta del nodo iniciador

* `${initiator.name}`, el nombre del iniciador

* `${initiator.email}`, dirección de correo electrónico del iniciador
* `${item.id}`, el id. del elemento de trabajo
* `${item.node.id}`, id del nodo en el modelo de flujo de trabajo asociado con este elemento de trabajo
* `${item.node.title}`, título del elemento de trabajo
* `${participant.email}`, dirección de correo electrónico del participante
* `${participant.name}`, nombre del participante
* `${participant.familyName}`, apellido del participante
* `${participant.id}`, id del participante
* `${participant.language}`, el idioma del participante
* `${instance.id}`, id. de flujo de trabajo
* `${instance.state}`, el estado del flujo de trabajo
* `${model.title}`, título del modelo de flujo de trabajo
* `${model.id}`, el id del modelo de flujo de trabajo

* `${model.version}`, la versión del modelo de flujo de trabajo
* `${payload.data}`, la carga útil

* `${payload.type}`, el tipo de carga útil
* `${payload.path}`, ruta de la carga útil
* `${host.prefix}`, prefijo de host, por ejemplo: `http://localhost:4502`

### Adición de una plantilla de correo electrónico para un nuevo idioma {#adding-an-email-template-for-a-new-language}

Para añadir una plantilla para un nuevo idioma:

1. Cree una [superposición](/help/sites-developing/overlays.md) según corresponda.

   * Notificaciones de página
   * Notificaciones de flujo de trabajo

1. Agregar un archivo `<language-code>.txt`.
1. Adapte el archivo al idioma.
1. Guarde los cambios.

>[!NOTE]
>
>El `<language-code>` utilizado como nombre de archivo para la plantilla de correo electrónico debe ser un código de idioma en minúsculas de dos letras que AEM reconozca. Para los códigos de idioma, AEM se basa en ISO-639-1.

## Configuración de notificaciones de correo electrónico de AEM Assets {#assetsconfig}

Cuando las colecciones de los AEM Assets se comparten o dejan de compartirse, los usuarios pueden recibir notificaciones por correo electrónico de AEM. Para configurar las notificaciones por correo electrónico, siga estos pasos.

1. Configure el servicio de correo electrónico, tal como se describió anteriormente en [Configuración del servicio de correo](/help/sites-administering/notification.md#configuring-the-mail-service).
1. Inicie sesión en AEM como administrador. Haga clic en **Herramientas** > **Operaciones** > **Consola web** para abrir la configuración de la consola web.
1. Editar **servlet de recopilación de recursos de CQ DAM de día**. Seleccione **enviar correo electrónico**. Haga clic en **Guardar**.

## Configuración de OAuth {#setting-up-oauth}

AEM ofrece compatibilidad con OAuth2 para su servicio de correo integrado, que permite a las organizaciones adherirse a los requisitos de correo electrónico seguros.

Puede configurar OAuth para varios proveedores de correo electrónico, como se describe a continuación.

>[!NOTE]
>
>Este procedimiento es un ejemplo para una instancia de publicación. Si desea habilitar las notificaciones por correo electrónico en una instancia de autor, debe seguir los mismos pasos en la instancia de autor.

### Gmail {#gmail}

1. Cree su proyecto en `https://console.developers.google.com/projectcreate`
1. Seleccione el proyecto y vaya a **API y servicios** - **Panel - Credenciales**
1. Configure la pantalla de consentimiento de OAuth según sus necesidades
1. En la siguiente pantalla de actualización, agregue estos dos ámbitos:
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. Una vez que haya agregado los ámbitos, vuelva a **Credenciales** en el menú de la izquierda y luego vaya a **Crear credenciales** - **ID de cliente de OAuth** - **Aplicación de escritorio**
1. Se abre una nueva ventana que contiene el ID de cliente y el Secreto de cliente.
1. Guarde estas credenciales.

**Configuraciones del lado de AEM**

>[!NOTE]
>
>Los clientes de Adobe Managed Service pueden trabajar con su ingeniero de servicio al cliente para realizar estos cambios en los entornos de producción.

En primer lugar, configure el Servicio de correo:

1. Abra la consola web de AEM yendo a `http://serveraddress:serverport/system/console/configMgr`
1. Busque y luego haga clic en **Servicio de correo CQ por día**
1. Añada la siguiente configuración:
   * Nombre de host del servidor SMTP: `smtp.gmail.com`
   * Puerto del servidor SMTP: `25` o `587`, según los requisitos
   * Marque las casillas para **SMPT usa StarTLS** y **SMTP requiere StarTLS**
   * Compruebe **flujo de OAuth** y haga clic en **Guardar**.

A continuación, configure su proveedor de OAuth de SMTP siguiendo el procedimiento a continuación:

>[!WARNING]
>
>Si, después de completar esta configuración, alguna vez cambia *cualquiera* de los valores de la configuración OSGi **Proveedor OAuth2 SMTP de CQ Mailer**, debe volver a autorizar siguiendo estos pasos.
>
>Si no se llevan a cabo, el token de acceso almacenado en `/conf/global/settings/mailer/oauth` no será válido y la conexión OAuth2 al servidor SMTP fallará.

1. Abra la consola web de AEM yendo a `http://serveraddress:serverport/system/console/configMgr`
1. Busque y luego haga clic en **Proveedor OAuth2 de SMTP de CQ Mailer**

1. Rellene la información necesaria de la siguiente manera:
   * URL de autorización: `https://accounts.google.com/o/oauth2/auth`
   * URL de token: `https://accounts.google.com/o/oauth2/token`
   * Ámbitos: `https://www.googleapis.com/auth/gmail.send` y `https://mail.google.com/`. Puede agregar más de un ámbito presionando el botón **+** en el lado derecho de cada ámbito configurado.
   * ID de cliente y Secreto de cliente: configure estos campos con los valores recuperados como se describe en el párrafo anterior.
   * URL de token de actualización: `https://accounts.google.com/o/oauth2/token`
   * Caducidad del token de actualización: nunca
1. Haga clic en **Guardar**.

<!-- clarify refresh token expiry, currently not present in the UI -->

Una vez configurada, la configuración debería ser similar a la siguiente:

![Ventana de configuración del proveedor de Oauth2 de SMTP del distribuidor CQ Mailer](assets/oauth-smtpprov2.png)

Ahora, active los componentes de OAuth. Para ello:

1. Vaya a la consola Componentes visitando esta dirección URL: `http://serveraddress:serverport/system/console/components`
1. Busque los siguientes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pulse el icono Reproducir a la izquierda de los componentes

   ![Lista de componentes que muestran OAuthCodeGenerateServlet y OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Finalmente, confirme la configuración mediante lo siguiente:

1. Vaya a la dirección de la instancia de publicación e inicie sesión como administrador.
1. Abra una ficha nueva en el explorador y vaya a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Esto lo redireccionará a la página de su proveedor SMTP, en este caso Gmail.
1. Inicio de sesión y consentimiento para dar los permisos necesarios
1. Después del consentimiento, el token se almacena en el repositorio. Puede acceder a ella en `accessToken` si accede directamente a esta dirección URL en su instancia de publicación: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. Repita lo anterior para cada instancia de publicación

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. Vaya a [https://portal.azure.com/](https://portal.azure.com/) e inicie sesión.
1. Busque **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado. También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Haga clic en **Registro de aplicaciones** - **Nuevo registro**

   ![El nuevo botón de registro al configurar Microsoft Outlook](assets/oauth-outlook1.png)

1. Rellene la información según sus necesidades y haga clic en **Registrar**
1. Vaya a la aplicación recién creada y seleccione **Permisos de API**
1. Vaya a **Añadir permiso** - **Permiso de gráfico** - **Permisos delegados**
1. Seleccione los siguientes permisos para su aplicación y haga clic en **Añadir permiso**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vaya a **Autenticación** - **Agregar una plataforma** - **Web** y en la sección **Redireccionar direcciones URL**, agregue la siguiente URL para redirigir el código de OAuth y, a continuación, presione **Configurar**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. Repita lo anterior para cada instancia de publicación
1. Configure los ajustes según sus necesidades
1. A continuación, vaya a **Certificados y secretos**, haga clic en **Nuevo secreto de cliente** y siga los pasos que aparecen en la pantalla para crear un secreto. Asegúrese de tomar nota de este secreto para utilizarlo posteriormente
1. Pulse **Información general** en el panel izquierdo y copie los valores de **ID de aplicación (cliente)** y **ID de directorio (inquilino)** para su posterior uso

Para recapitular, debe tener la siguiente información para configurar OAuth2 para el servicio Mailer en el lado de AEM:

* La URL de autenticación, que se construirá con el ID del inquilino. Tendrá esta forma: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* La URL del token, que se construirá con el ID del inquilino. Tendrá esta forma: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* La URL de actualización, que se construirá con el ID del inquilino. Tendrá esta forma: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* El ID de cliente
* El secreto del cliente

**Configuraciones del lado de AEM**

A continuación, integre la configuración de OAuth2 con AEM:

>[!WARNING]
>
>Si, después de completar esta configuración, alguna vez cambia *cualquiera* de los valores de la configuración OSGi **Proveedor OAuth2 SMTP de CQ Mailer**, debe volver a autorizar siguiendo estos pasos.
>
>Si no se llevan a cabo, el token de acceso almacenado en `/conf/global/settings/mailer/oauth` no será válido y la conexión OAuth2 al servidor SMTP fallará.

1. Vaya a la consola web de su instancia local explorando `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en **Servicio Day CQ Mail**
1. Añada la siguiente configuración:
   * Nombre de host del servidor SMTP: `smtp.office365.com`
   * Usuario de SMTP: su nombre de usuario en formato de correo electrónico
   * Dirección &quot;De&quot;: La dirección de correo electrónico que se utilizará en el campo &quot;De:&quot; de los mensajes enviados por el remitente de correo
   * Puerto del servidor SMTP: `25` o `587` según los requisitos
   * Marque las casillas para **SMPT usa StarTLS** y **SMTP requiere StarTLS**
   * Compruebe **flujo de OAuth** y haga clic en **Guardar**.
1. Busque y luego haga clic en **Proveedor OAuth2 de SMTP de CQ Mailer**
1. Rellene la información necesaria de la siguiente manera:
   * Complete la URL de autorización, la URL del token y la URL del token de actualización construyéndolas tal como se describe al [final de este procedimiento](#microsoft-outlook)
   * ID de cliente y Secreto de cliente: configure estos campos con los valores recuperados como se ha descrito anteriormente.
   * Añada los siguientes ámbitos a la configuración:
      * opénido
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * URL de redirección de AuthCode: `http://localhost:4503/services/mailer/oauth2/token`
   * URL de token de actualización: debe tener el mismo valor que la URL de token anterior
1. Haga clic en **Guardar**.

Una vez configurada, la configuración debería ser similar a la siguiente:

![La configuración completa de OAuth2 de SMTP de CQ Mailer](assets/oauth-outlook-smptconfig.png)

Ahora, active los componentes de OAuth. Para ello:

1. Vaya a la consola Componentes visitando esta dirección URL: `http://serveraddress:serverport/system/console/components`
1. Busque los siguientes componentes
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. Pulse el icono Reproducir a la izquierda de los componentes

![Un fragmento de la lista de componentes que contiene OAuthCodeGenerateServlet y OAuthCodeAccessTokenGenerator](assets/oauth-components-play.png)

Finalmente, confirme la configuración mediante lo siguiente:

1. Vaya a la dirección de la instancia de publicación e inicie sesión como administrador.
1. Abra una ficha nueva en el explorador y vaya a `http://serveraddress:serverport/services/mailer/oauth2/authorize`. Esto lo redirigirá a la página de su proveedor SMTP, en este caso Outlook.
1. Inicio de sesión y consentimiento para dar los permisos necesarios
1. Después del consentimiento, el token se almacena en el repositorio. Puede acceder a ella en `accessToken` si accede directamente a esta dirección URL en su instancia de publicación: `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
