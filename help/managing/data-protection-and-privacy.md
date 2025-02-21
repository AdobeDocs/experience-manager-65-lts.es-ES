---
title: 'Reglamentos de protección de datos y privacidad de datos: preparación para Adobe Experience Manager'
description: Obtenga información acerca de la compatibilidad de Adobe Experience Manager con las distintas normas de protección de datos y privacidad de datos. Incluye el Reglamento General de Protección de Datos (RGPD) de la UE, la Ley de Privacidad del Consumidor de California y cómo cumplirlos al implementar un nuevo proyecto de AEM.
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
source-git-commit: d1297182b801ff4db163b8ae91332f5aebb94b9b
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 45%

---

# Preparación de Adobe Experience Manager para la protección de datos y las normas de privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituirlo.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento sobre los reglamentos de protección y privacidad de datos.

>[!NOTE]
>
>Para obtener más información acerca de la respuesta de Adobe a los problemas de privacidad y lo que esto supone para usted como cliente o clienta de Adobe, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o el administrador de AEM gestione las solicitudes de protección de datos y privacidad de datos. Puede ayudarle a cumplir con estas regulaciones. Los procedimientos documentados permiten a los clientes ejecutar las solicitudes reglamentarias manualmente o llamando a las API, si están disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager.
>
>Los datos de otro servicio bajo demanda de Adobe, junto con cualquier solicitud de privacidad relacionada, requieren que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

## Introducción {#introduction}

Las instancias de Adobe Experience Manager, y las aplicaciones que se ejecutan en ellas, son propiedad de los clientes de Adobe y son operadas por ellos.

Como consecuencia, los reglamentos de protección de datos, como el RGPD, la CCPA y otras, son en gran medida responsabilidad de los clientes.

Como introducción breve, las regulaciones para la privacidad y protección de datos incluyen nuevas reglas a las que deben seguir las funciones de lo siguiente:

* Entidades comerciales (CCPA) y/o controladores de datos (RGPD)

* Proveedores de servicios (CCPA) o procesadores de datos (RGPD)

Las principales disposiciones de esos reglamentos son las siguientes:

1. Definición ampliada de datos personales para incluir todos los ID únicos; como en datos directa e indirectamente identificables.

2. Fortalecimiento de los requisitos de consentimiento.

3. Mayor enfoque a los derechos de eliminación (eliminación de datos).

4. Exclusión de la venta de datos.

Para Adobe Experience Manager:

* Las instancias, y las aplicaciones que se ejecutan en ellas, son propiedad del cliente y las gestiona.

   * El cliente gestiona las funciones regulatorias, incluidas las entidades del negocio y el proveedor de servicios, el controlador de datos y el procesador de datos, entre otras.

   * Adobe Experience Platform Privacy Service no forma parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para el administrador de privacidad del cliente o el administrador de AEM para ejecutar las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las IU o portales de los clientes que administran solicitudes de regulación de la privacidad.

* AEM no incluye ninguna herramienta predeterminada para admitir el flujo de trabajo de solicitudes de privacidad.

   * Adobe proporciona documentación y procedimientos para el administrador de privacidad y el administrador de AEM del cliente, lo que les permite ejecutar manualmente las solicitudes relacionadas con las normas de privacidad.

Adobe proporciona procedimientos para gestionar solicitudes de privacidad relacionadas con acceso, eliminación y exclusión para Adobe Experience Manager. A veces, hay API disponibles a las que se puede llamar desde un portal o scripts desarrollados por el cliente para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad (ilustrado con Adobe Experience Manager 6.5):

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager y preparación regulatoria {#aem-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación reglamentaria sobre las áreas de producto de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Gestión de solicitudes de privacidad y protección de datos para AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM Opting Into Aggregate Usage Statistics Collection {#aem-opting-into-aggregate-usage-statistics-collection}

Ver [Recopilación de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte [AEM Sites - Preparación para la protección de datos y la privacidad.](/help/sites-administering/gdpr-compliance-sites.md)

## Integración de AEM con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager se realizan con servicios preparados para la protección de datos y la privacidad (por ejemplo, RGPD o CCPA). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.

Para obtener más información, consulte lo siguiente:

* [Adobe Target: Información general de privacidad](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=es)

## AEM Forms {#aem-forms}

AEM Forms incluye componentes y flujos de trabajo que capturan, procesan y almacenan datos para orquestar procesos empresariales y completar transacciones digitales. Los distintos componentes utilizan diferentes almacenes de datos y permiten la integración con almacenes de datos personalizados. En la siguiente documentación se explican los procedimientos y directrices para acceder y gestionar los datos de usuario con el fin de admitir los flujos de trabajo de protección de datos y privacidad (por ejemplo, RGPD o CCPA) de un componente.

* [Portal de Forms ](/help/forms/using/forms-portal-handling-user-data.md)
* [Administración de correspondencia](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrar con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flujos de trabajo centrados en Forms en OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flujos de trabajo de Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (solo AEM Forms JEE)
* [Seguridad de documentos](/help/forms/using/document-security-handling-user-data.md) (solo AEM Forms JEE)
* [Administración de usuarios](/help/forms/using/user-management-handling-user-data.md) (solo AEM Forms JEE)
