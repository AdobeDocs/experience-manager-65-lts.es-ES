---
title: Inicio de sesión único
description: Obtenga información sobre cómo configurar el inicio de sesión único (SSO) para una instancia de Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Inicio de sesión único {#single-sign-on}

Inicio de sesión único (SSO) permite a un usuario acceder a varios sistemas después de proporcionar credenciales de autenticación (como nombre de usuario y contraseña) una vez. Un sistema independiente (conocido como autenticador de confianza) realiza la autenticación y proporciona a Experience Manager las credenciales de usuario. Experience Manager comprueba y aplica los permisos de acceso del usuario (es decir, determina a qué recursos puede acceder el usuario).

El servicio Controlador de autenticación SSO ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) procesa los resultados de autenticación que proporciona el autenticador de confianza. El Controlador de autenticación SSO busca un Identificador de SSO (SSID) como el valor de un atributo especial en las siguientes ubicaciones en este orden:

1. Encabezados de solicitud
1. Cookies
1. Parámetros de solicitud

Cuando se encuentra un valor, la búsqueda finaliza y se utiliza este valor.

Configure los dos servicios siguientes para reconocer el nombre del atributo que almacena el SSID:

* El módulo de inicio de sesión.
* El servicio de autenticación SSO.

Especifique el mismo nombre de atributo para ambos servicios. El atributo está incluido en `SimpleCredentials` que se proporciona a `Repository.login`. El valor del atributo es irrelevante e ignorado, su mera presencia es importante y verificada.

## Configuración de SSO {#configuring-sso}

Para configurar el SSO de una instancia de AEM, configure el [Controlador de autenticación SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

   Por ejemplo, para el conjunto NTLM:

   * **Ruta de acceso:** según sea necesario; por ejemplo, `/`
   * **Nombres de encabezado**: `LOGON_USER`
   * **Formato de identificador**: `^<DOMAIN>\\(.+)$`

     Donde `<*DOMAIN*>` se reemplaza con el nombre de su propio dominio.

   Para firmar conjuntamente:

   * **Ruta de acceso:** según sea necesario; por ejemplo, `/`
   * **Nombres de encabezado**: remote_user
   * **Formato De Id.:** Tal Cual

   Para SiteMinder:

   * **Ruta de acceso:** según sea necesario; por ejemplo, `/`
   * **Nombres de encabezado:** SM_USER
   * **Formato de ID**: Tal cual

1. Confirme que el inicio de sesión único funciona según sea necesario, incluida la autorización.

>[!CAUTION]
>
>Asegúrese de que los usuarios no puedan acceder directamente a AEM si se ha configurado el SSO.
>
>Al requerir que los usuarios pasen por un servidor web que ejecute el agente de su sistema SSO, se garantiza que ningún usuario pueda enviar directamente un encabezado, una cookie o un parámetro que lleve al usuario a ser de confianza para AEM, ya que el agente filtrará esa información si se envía desde el exterior.
>
>Cualquier usuario que pueda acceder directamente a su instancia de AEM sin pasar por el servidor web podrá actuar como cualquier usuario enviando el encabezado, la cookie o el parámetro si se conocen los nombres.
>
>Asegúrese también de que, entre los encabezados, las cookies y los nombres de parámetros de solicitud, solo configure el que sea necesario para la configuración de SSO.
>

>[!NOTE]
>
>El inicio de sesión único se usa a menudo con [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Si también usa [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) con Microsoft® Internet Information Server (IIS), se requiere configuración adicional en:
>
>* `disp_iis.ini`
>* IIS
>
>En el conjunto `disp_iis.ini`:
>(consulte [instalación de Dispatcher con Microsoft® Internet Information Server](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=es#microsoft-internet-information-server) para obtener información detallada)
>
>* `servervariables=1` (reenvía variables del servidor IIS como encabezados de solicitud a la instancia remota)
>* `replaceauthorization=1` (reemplaza cualquier encabezado denominado &quot;Autorización&quot; que no sea &quot;Básico&quot; por su equivalente &quot;Básico&quot;)
>
>En IIS:
>
>* deshabilitar **acceso anónimo**
>
>* habilitar **autenticación de Windows integrada**
>

Puede ver qué controlador de autenticación se está aplicando a cualquier sección del árbol de contenido mediante la opción **Authenticator** de la Consola Felix; por ejemplo:

`http://localhost:4502/system/console/slingauth`

Primero se consulta el controlador que mejor coincida con la ruta. Por ejemplo, si configura el controlador A para la ruta de acceso `/` y el controlador B para la ruta de acceso `/content`, una solicitud a `/content/mypage.html` consultará primero el controlador B.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Ejemplos {#example}

Para una solicitud de cookie (mediante la dirección URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Usar la siguiente configuración:

* **Ruta**: `/`

* **Nombres de encabezado**: `TestHeader`

* **Nombres de cookies**: `TestCookie`

* **Nombres de parámetros**: `TestParameter`

* **Formato de identificador**: `AsIs`

La respuesta sería:

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

Esto también funciona si solicita:
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

O puede usar el siguiente comando curl para enviar el encabezado `TestHeader` a `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>Al utilizar el parámetro de solicitud en un explorador, solo ve parte de HTML, sin CSS. Esto se debe a que todas las solicitudes de HTML se realizan sin el parámetro de solicitud.

## Eliminar vínculos de cierre de sesión de AEM {#removing-aem-sign-out-links}

Al utilizar SSO, el inicio y cierre de sesión se gestionan externamente, de modo que los vínculos de cierre de sesión propios de AEM ya no son aplicables y deben eliminarse.

El vínculo de cierre de sesión en la pantalla de bienvenida se puede eliminar siguiendo estos pasos.

1. Superponer `/libs/cq/core/components/welcome/welcome.jsp` a `/apps/cq/core/components/welcome/welcome.jsp`
1. elimine la siguiente parte del jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Para eliminar el vínculo de cierre de sesión disponible en el menú personal del usuario en la esquina superior derecha, siga estos pasos:

1. Superponer `/libs/cq/ui/widgets/source/widgets/UserInfo.js` a `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Elimine la siguiente parte del archivo:

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
