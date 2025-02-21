---
title: Compatibilidad con cookies de SameSite para AEM 6.5
description: Obtenga información acerca de la compatibilidad con cookies de SameSite para AEM 6.5.
topic-tags: security
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 77%

---

# Compatibilidad con cookies de SameSite para AEM 6.5 {#same-site-cookie-support-for-aem-65}

Desde la versión 80, Chrome y posterior Safari, introdujeron un nuevo modelo para la seguridad de las cookies. Este modo está diseñado para introducir controles de seguridad en torno a la disponibilidad de cookies en sitios de terceros, a través de una configuración denominada `SameSite`. Para obtener información más detallada, consulte este artículo [web.dev - cookies SameSite explicadas](https://web.dev/samesite-cookies-explained/).

El valor predeterminado de esta configuración (`SameSite=Lax`) puede causar que la autenticación entre instancias o servicios de AEM no funcione. Esto se debe a que es posible que los dominios o las estructuras URL de estos servicios no entren dentro de las restricciones de esta directiva de cookies.

Para evitarlo, debe establecer el atributo de la cookie `SameSite` en `None` para el token de inicio de sesión.

>[!CAUTION]
>
>La configuración `SameSite=None` solo se aplica si el protocolo es seguro (HTTPS).
>
>Si el protocolo no es seguro (HTTP), la configuración se ignora y el servidor muestra este mensaje ADVERTENCIA:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Puede agregar la configuración siguiendo los pasos siguientes:

1. Vaya a la consola web en `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en el **controlador de autenticación de token de Granite de Adobe**
1. Configure el **atributo SameSite para la cookie de token de inicio de sesión** a `None`, como se muestra en la imagen siguiente
   ![samesite](assets/samesite1.png)
1. Haga clic en Guardar
1. Una vez que se actualiza esta configuración y se cierra la sesión de los usuarios y se inicia sesión de nuevo, las cookies `login-token` tendrán el conjunto de atributos `None` y se incluirán en solicitudes entre sitios.
