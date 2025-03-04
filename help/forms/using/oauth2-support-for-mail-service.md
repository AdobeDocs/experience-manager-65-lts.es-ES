---
title: Configuración de la autenticación basada en OAuth2 para Microsoft&reg (Forms JEE OAuth); protocolos de servidor de correo de Office 365
description: Configuración de la autenticación basada en OAuth2 para Microsoft&reg (Forms JEE OAuth); protocolos de servidor de correo de Office 365
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Integración de AEM Forms con los protocolos del servidor de correo de Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Para permitir que las organizaciones cumplan con los requisitos de correo electrónico seguro, AEM Forms ofrece compatibilidad con OAuth 2.0 para la integración con los protocolos de servidor de correo de Microsoft® Office 365. Puede utilizar el servicio de autenticación OAuth 2.0 de Azure Active Directory (Azure AD) para conectarse con varios protocolos como IMAP, POP o SMTP y acceder a los datos de correo electrónico de los usuarios de Office 365. A continuación se proporcionan instrucciones paso a paso para configurar los protocolos del servidor de correo de Microsoft® Office 365 para autenticarse mediante el servicio OAuth 2.0:

1. Inicie sesión en [https://portal.azure.com/](https://portal.azure.com/), busque **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado.
También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Haga clic en **Agregar** > **Registro de aplicación** > **Nuevo registro**.

   ![Registro de aplicación](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Rellene la información según sus necesidades y haga clic en **Registro**.
   ![Cuenta compatible](/help/forms/using/assets/azure_suuportedaccountype.png)
En el caso anterior, **Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - Multitenant) y cuentas personales de Microsoft® (por ejemplo, Skype, Xbox)** están seleccionadas.

   >[!NOTE]
   >
   > * Para **cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - multiusuario)** aplicación, Adobe recomienda usar una cuenta de trabajo en lugar de una cuenta de correo electrónico personal.
   > * **Sólo cuentas personales de Microsoft®** aplicación no admitida.
   > * Adobe recomienda usar la aplicación **Multi-tenant and personal Microsoft® account**.

1. A continuación, vaya a **Certificados y secretos**, haga clic en **Nuevo secreto de cliente** y siga los pasos que aparecen en la pantalla para crear un secreto. Asegúrese de tomar nota de este valor de secret para utilizarlo posteriormente.

   ![Clave secreta](/help/forms/using/assets/azure_secretkey.png)

1. Para agregar permisos, vaya a la aplicación recién creada y seleccione **Permisos de API** > **Agregar un permiso** > **Microsoft® Graph** > **Permisos delegados**.
1. Seleccione las casillas de verificación de los siguientes permisos para la aplicación y haga clic en **Agregar permiso**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Permiso de API](/help/forms/using/assets/azure_apipermission.png)

1. Seleccione **Autenticación** > **Agregar una plataforma** > **Web** y, en la sección **Redireccionar direcciones URL**, agregue cualquiera de los siguientes URI (Identificador de recurso universal) como:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   En este caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` se usa como URI de redireccionamiento.

1. Haga clic en **Configurar** después de agregar cada dirección URL y configure los ajustes según sus necesidades.
   ![URI de redireccionamiento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > Es obligatorio seleccionar **tokens de acceso** y **tokens de identificación** casillas de verificación.

1. Haga clic en **Información general** en el panel izquierdo y copie los valores de **ID de aplicación (cliente)**, **ID de directorio (inquilino)** y **Secreto de cliente** para su uso posterior.

   ![Información general](/help/forms/using/assets/azure_overview.png)

## Generación del código de autorización {#generating-the-authorization-code}

A continuación, debe generar el código de autorización, explicado en los pasos siguientes:

1. Abra la siguiente URL en el explorador después de reemplazar `clientID` por `<client_id>` y `redirect_uri` por el URI de redireccionamiento de la aplicación:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > Si existe la aplicación de usuario único, reemplace `common` por su `[tenantid]` en la siguiente URL para generar el código de autorización: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Al escribir la dirección URL anterior, se le redirige a la pantalla de inicio de sesión:
   ![Pantalla de inicio de sesión](/help/forms/using/assets/azure_loginscreen.png)

1. Introduzca el correo electrónico, haga clic en **Siguiente** y aparecerá la pantalla de permiso de la aplicación:

   ![Permitir permiso](/help/forms/using/assets/azure_permission.png)

1. Cuando permite el permiso, se le redirige a una nueva dirección URL como: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copie el valor de `<code>` de la dirección URL anterior de `0.ASY...` a `&session_state` en la dirección URL anterior.

## Generación del token de actualización {#generating-the-refresh-token}

A continuación, debe generar el token de actualización, tal y como se explica en los pasos siguientes:

1. Abra el símbolo del sistema y utilice el siguiente comando cURL para obtener el refreshToken.

1. Reemplace `clientID`, `client_secret` y `redirect_uri` por los valores de su aplicación junto con el valor de `<code>`:

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > En la aplicación de un solo inquilino, para generar el token de actualización, use el siguiente comando cURL y reemplace `common` por `[tenantid]` en:
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Tome nota del token de actualización.

## Configuración del servicio de correo electrónico con compatibilidad con OAuth 2.0 {#configureemailservice}

Ahora, configure el servicio de correo electrónico en el servidor JEE más reciente iniciando sesión en la interfaz de usuario de Admin:

1. Vaya a **Inicio** > **Servicio** > **Aplicación y servicios** > **Administración de servicios** > **Servicio de correo electrónico**, aparecerá la ventana **Servicio de correo electrónico de configuración**, configurada para la autenticación básica.

   >[!NOTE]
   >
   > Para habilitar el servicio de autenticación oAuth 2.0, es obligatorio seleccionar **Si el servidor SMTP requiere autenticación (autenticación SMTP)**.

1. Establecer **configuración de autenticación oAuth 2.0** como `True`.
1. Copie los valores de **ID de cliente** y **Secreto de cliente** de Azure Portal.
1. Copie el valor del **token de actualización** generado.
1. Inicie sesión en **Workbench** y busque **Correo electrónico 1.0** desde **Selector de actividades**.
1. Hay tres opciones disponibles en Correo electrónico 1.0 como:
   * **Enviar con documento**: envía un mensaje de correo electrónico con datos adjuntos únicos.
   * **Enviar con mapa de archivos adjuntos**: envía un correo electrónico con varios archivos adjuntos.
   * **Recibir**: Recibe un correo electrónico de IMAP.

   >[!NOTE]
   >
   >* El protocolo de seguridad de transporte tiene los siguientes valores válidos: &quot;blank&quot;, &quot;SSL&quot; o &quot;TLS&quot;. Establezca los valores de **SMTP Transport Security** y **Receive Transport Security** en **TLS** para habilitar el servicio de autenticación oAuth.
   >* El protocolo **POP3** no es compatible con OAuth cuando se usan extremos de correo electrónico.

   ![Configuración de conexión](/help/forms/using/assets/oauth_connectionsettings.png)

1. Pruebe la aplicación seleccionando **Enviar con documento**.
1. Proporcione las direcciones **TO** y **From**.
1. Invoque la aplicación y se enviará un correo electrónico con la autenticación 0Auth 2.0.

   >[!NOTE]
   >
   >Si lo desea, puede cambiar la configuración de autenticación Auth 2.0 a autenticación básica para un proceso en particular en un área de trabajo. Para ello, establezca el valor **Autenticación OAuth 2.0** como &#39;Falso&#39; en **Usar configuración global** en la ficha **Configuración de conexión**.

## Para habilitar las notificaciones de tareas oAuth {#enable_oauth_task}

1. Vaya a **Inicio** > **Servicios** > **Flujo de trabajo de formularios** > **Configuración del servidor** > **Configuración de correo electrónico**
1. Para habilitar las notificaciones de tareas oAuth, seleccione la casilla de verificación **Habilitar oAuth**.
1. Copie los valores de **ID de cliente** y **Secreto de cliente** de Azure Portal.
1. Copie el valor del **token de actualización** generado.
1. Haga clic en **Guardar** para guardar los detalles.

   ![Notificación de tarea](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Para obtener más información relacionada con las notificaciones de tareas, [haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65-lts/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Para configurar el extremo de correo electrónico {#configure_email_endpoint}

1. Vaya a **Inicio** > **Servicios** > **Aplicación y servicios** > **Administración de extremos**
1. Para configurar el extremo del correo electrónico, establezca **Configuración de autenticación oAuth 2.0** como `True`.
1. Copie los valores de **ID de cliente** y **Secreto de cliente** de Azure Portal.
1. Copie el valor del **token de actualización** generado.
1. Haga clic en **Guardar** para guardar los detalles.

   ![Configuración de conexión](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Para obtener más información sobre la configuración de los extremos de correo electrónico, haga clic en [Configurar un extremo de correo electrónico](https://experienceleague.adobe.com/docs/experience-manager-65-lts/content/forms/administrator-help/configuring-email-endpoints.html).

## Solución de problemas {#troubleshooting}

* Si el servicio de correo electrónico no funciona correctamente, intente volver a generar `Refresh Token` como se ha descrito anteriormente. El nuevo valor tarda unos minutos en implementarse.

* Error al configurar los detalles del servidor de correo electrónico en el extremo de correo electrónico mediante Workbench. Intente configurar el extremo mediante la interfaz de usuario de administración en lugar de Workbench.
