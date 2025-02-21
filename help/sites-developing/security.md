---
title: Seguridad
description: La seguridad de la aplicación se inicia durante la fase de desarrollo
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Seguridad{#security}

La seguridad de la aplicación se inicia durante la fase de desarrollo. Adobe recomienda aplicar las siguientes prácticas recomendadas de seguridad.

## Usar sesión de solicitud {#use-request-session}

Siguiendo el principio de menor privilegio, Adobe recomienda que cada acceso al repositorio se realice mediante la sesión enlazada a la solicitud del usuario y el control de acceso adecuado.

## Proteger contra scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

El proceso de ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web que han visto otros usuarios. Los usuarios web malintencionados pueden aprovechar esta vulnerabilidad de seguridad para evitar los controles de acceso.

AEM aplica el principio de filtrar todo el contenido proporcionado por el usuario al generar la salida. La prevención de XSS tiene la máxima prioridad tanto durante el desarrollo como durante las pruebas.

El mecanismo de protección XSS proporcionado por AEM se basa en la [biblioteca AntiSamy Java™](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) proporcionada por [OWASP (The Open Web Application Security Project)](https://owasp.org/). La configuración predeterminada de AntiSamy se encuentra en

`/libs/cq/xssprotection/config.xml`

Es importante que adapte esta configuración a sus propias necesidades de seguridad superponiendo el archivo de configuración. La [documentación oficial de AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) le proporciona toda la información que necesita para implementar sus requisitos de seguridad.

>[!NOTE]
>
>Adobe recomienda que siempre acceda a la API de protección XSS usando el [XSSAPI proporcionado por AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

Además, un firewall de aplicaciones web, como [mod_security para Apache](https://www.modsecurity.org), puede proporcionar un control central y confiable sobre la seguridad del entorno de implementación y protegerlo contra ataques de scripts entre sitios que no se habían detectado anteriormente.

## Acceso a la información de Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Las ACL de la información de Cloud Service y la configuración de OSGi necesaria para proteger su instancia están automatizadas como parte del [Modo listo para la producción](/help/sites-administering/production-ready.md). Aunque esto significa que no necesita cambiar la configuración manualmente, se recomienda revisarla antes de activarla con la implementación.

Cuando [integra su instancia de AEM con Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md), utiliza [configuraciones de Cloud Service](/help/sites-developing/extending-cloud-config.md). La información sobre estas configuraciones, junto con las estadísticas recopiladas, se almacenan en el repositorio. Adobe recomienda que, si utiliza esta funcionalidad, compruebe si la seguridad predeterminada de esta información coincide con sus necesidades.

El módulo webservicesupport escribe estadísticas e información de configuración en:

`/etc/cloudservices`

Con los permisos predeterminados:

* Entorno de creación: `read` para `contributors`

* Entorno de publicación: `read` para `everyone`

## Proteger contra ataques de falsificación de solicitud en sitios múltiples {#protect-against-cross-site-request-forgery-attacks}

Para obtener más información sobre los mecanismos de seguridad que utiliza AEM para mitigar los ataques CSRF, consulte la sección [Filtro de referente de Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de la lista de comprobación de seguridad y la [documentación del marco de protección CSRF](/help/sites-developing/csrf-protection.md).
