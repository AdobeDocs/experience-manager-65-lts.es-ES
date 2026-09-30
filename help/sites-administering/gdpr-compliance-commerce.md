---
title: AEM Commerce - Preparación para el RGPD
description: Conozca los procedimientos para gestionar las solicitudes de RGPD en AEM Commerce y cómo utilizarlas.
contentOwner: carlino
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin,Developer,Leader,User
exl-id: 2d7ae2ad-a7ad-4b7d-bfa4-167caa49a087
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 80%
---
# AEM Commerce - Preparación para el RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las regulaciones de protección de datos y privacidad, como el RGPD y la CCPA.

El Reglamento General de Protección de Datos de la Unión Europea sobre los derechos de privacidad de datos entra en vigor en mayo de 2018. Consulte la página del [RGPD en el Centro de privacidad de Adobe](https://business.adobe.com/es/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte la [Preparación para el RGPD de AEM](/help/managing/data-protection-and-privacy.md) para obtener más información.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Con las integraciones listas para usar de Adobe Commerce, AEM es el nivel de experiencia que consume servicios y devuelve datos a la plataforma de comercio del cliente que se ejecuta en modo sin encabezado.

En algunas plataformas de comercio, Adobe almacena información de perfil (`/home/users`) y tokens de comercio (para iniciar sesión en la plataforma de comercio) en AEM. Para dichos casos de uso, lea la [Gestión de solicitudes de RGPD para la plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestión de solicitudes de RGPD para AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Para la integración de Salesforce Commerce Cloud, AEM Commerce no almacena información relevante sobre el RGPD. Reenviar la solicitud a [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para las integraciones de Commerce hybris y HCL WebSphere® hay algunos datos en AEM. Use las [instrucciones de RGPD de AEM Platform](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) y tenga en cuenta las siguientes preguntas:

1. **¿Dónde se almacenan o utilizan mis datos?** Información de perfil de usuario en caché, como nombre, identificador de usuario comercial, token, contraseña y datos de dirección, tal como se muestra desde AEM.
1. **¿Con quién comparto los datos del RGPD cubiertos?** Ninguna actualización de los datos relevantes del RGPD en AEM Commerce se almacena (excepto la información de perfil relevante, como se ha mencionado anteriormente), pero se procesa como proxy de vuelta a la plataforma de comercio.
1. **Cómo eliminar mis datos de usuario**? Elimine el perfil de usuario en AEM y recurra a la eliminación del usuario en la plataforma de comercio.

>[!NOTE]
>
>Eche un vistazo a la [wiki de hybris](https://wiki.hybris.com/) o a la [documentación de HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html) si es necesario.
