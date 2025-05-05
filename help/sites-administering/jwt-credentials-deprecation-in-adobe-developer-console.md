---
title: Credenciales JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de las credenciales de JWT en desuso en Adobe Developer Console en AEM.
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: 7b6b02fd-fcb2-45ae-a239-e0c68de2bcbb
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 75%

---

# Credenciales JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service debe hacer referencia a [el artículo comparable de la versión de AEMaaCS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=es) para obtener más información.

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de la nueva cuenta de servicio (JWT) no se pueden crear el 3 de junio de 2024 o después, y las credenciales de JWT existentes no funcionarán el 27 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artículo proporciona contexto adicional sobre cómo los clientes de Adobe Experience Manager (AEM) 6.5 deben gestionar el periodo de desuso.

La principal desventaja es que AEM ahora es compatible con las nuevas credenciales de servidor a servidor de OAuth para AEM. Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT. Esta migración ya se puede realizar.

En las secciones siguientes se enumeran los escenarios en los que los clientes deben (o en algunos casos, no) reemplazar sus credenciales de cuenta de servicio (JWT) por credenciales de servidor a servidor de OAuth, ahora que AEM los admite. [Lea cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrar las credenciales.

## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción**: migre la configuración ahora que AEM admite las credenciales de OAuth.

**Versiones relevantes de AEM**: Adobe Managed Services.

Los clientes de AEM utilizan AEM para configurar integraciones con todas las demás soluciones de Adobe. Por ejemplo, Adobe Target y Adobe Analytics, entre otras.

![Integración de AEM con otras soluciones](/help/sites-administering/assets/jwt-deprecation.png)

Consulte [Configuración de integraciones de IMS para AEM](/help/sites-administering/setting-up-ims-integrations-for-aem.md) para obtener más información sobre cómo:

* crear configuraciones con credenciales de OAuth.
* Migrar las configuraciones creadas con credenciales de JWT para utilizar las credenciales de OAuth.

## Las API de Cloud Manager {#cloud-manager-apis}

**Acción**: confirme cuándo se puede realizar la migración de JWT a las credenciales de OAuth.

**Versiones relevantes de AEM**: Adobe Managed Services.

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor de OAuth, antes de que las credenciales de JWT caduquen en enero de 2025.
