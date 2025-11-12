---
title: 'Reglamentos de protección de datos y privacidad de datos: preparación de Adobe Experience Manager'
description: Obtenga información sobre la compatibilidad de Adobe Experience Manager con las distintas normas de protección y privacidad de datos. Esto incluye el Reglamento general de protección de datos (RGPD) de la UE y la Ley de privacidad del consumidor de California, y cómo cumplirlos al implementar un nuevo proyecto de AEM.
solution: Experience Manager, Experience Manager 6.5 LTS
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
exl-id: 6faf8e4f-ca2a-4d68-a354-fb0aa6c2644b
source-git-commit: 4a93e17da1157253a681bf8b3a38252962d8fb59
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 98%

---

# Preparación de Adobe Experience Manager para reglamentos de protección y privacidad de datos {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituirlo.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento sobre los reglamentos de protección y privacidad de datos.

>[!NOTE]
>
>Para obtener más información acerca de la respuesta de Adobe a los problemas de privacidad y lo que esto supone para usted como cliente o clienta de Adobe, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

Adobe proporciona documentación y procedimientos (con API cuando están disponibles), para que el administrador de privacidad del cliente o de AEM gestione las solicitudes de protección y privacidad de datos. Esto puede ayudarle a cumplir estas regulaciones. Los procedimientos documentados permiten a los clientes ejecutar las solicitudes reglamentarias manualmente o realizando llamadas API, cuando estén disponibles, desde un portal o servicio externo.

>[!CAUTION]
>
>Los detalles documentados aquí están restringidos a Adobe Experience Manager.
>
>Los datos de otro servicio bajo demanda de Adobe, junto con cualquier solicitud de privacidad relacionada, requieren que se realicen acciones en ese servicio.
>
>Para obtener más información, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

## Introducción {#introduction}

Las instancias de Adobe Experience Manager y las aplicaciones que se ejecutan en ellas son propiedad de los clientes de Adobe y están operadas por ellos.

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

   * El cliente administra las funciones regulatorias, incluidas las entidades de la empresa y de proveedor de servicio, el responsable del tratamiento de datos y el encargado del tratamiento de datos, entre otros.

   * Adobe Experience Platform Privacy Service no forma parte del flujo de trabajo para AEM, como se ilustra en el diagrama siguiente.

* AEM incluye documentación y procedimientos para el administrador de privacidad del cliente o el administrador de AEM para ejecutar las solicitudes de regulación de privacidad; manualmente o a través de API, cuando esté disponible.

* No se ha agregado ningún servicio ni interfaz de usuario nuevos.

   * En su lugar, los procedimientos y las API están documentados para su uso por las IU o portales de los clientes que administran solicitudes de regulación de la privacidad.

* AEM no incluye ninguna herramienta predeterminada para admitir el flujo de trabajo de solicitudes de privacidad.

   * Adobe proporciona documentación y procedimientos para el administrador de privacidad o de AEM del cliente, lo que le permite ejecutar manualmente las solicitudes relacionadas con las normas de privacidad.

Adobe ofrece procedimientos para gestionar solicitudes de privacidad relacionadas con el acceso, la eliminación y la exclusión para Adobe Experience Manager. En ocasiones, hay API disponibles a las que se puede llamar desde un portal o scripts desarrollados por el cliente para ayudar con la automatización.

El diagrama siguiente ilustra el aspecto que podría tener un flujo de trabajo de solicitud de privacidad:

![Protección de datos y privacidad](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager y preparación regulatoria {#aem-and-regulatory-readiness}

Consulte las secciones siguientes para obtener documentación regulatoria sobre las áreas de productos de AEM.

## AEM Foundation {#aem-foundation}

Consulte [Gestión de solicitudes de privacidad y protección de datos para AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## Inclusión de AEM en la recopilación de estadísticas de uso agregadas {#aem-opting-into-aggregate-usage-statistics-collection}

Consulte [Recopilación de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulte [AEM Sites: preparación para la protección y la privacidad de datos.](/help/sites-administering/gdpr-compliance-sites.md)

## Integración de AEM con Adobe Target y Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Estas integraciones de Adobe Experience Manager se realizan con servicios preparados para la protección de datos y la privacidad (por ejemplo, el RGPD o la CCPA). No se almacenan datos personales de Adobe Target o Adobe Analytics en AEM en relación con las integraciones.

Para obtener más información, consulte lo siguiente:

* [Adobe Target: Información general de privacidad](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=es)

* [Flujo de trabajo de privacidad de datos de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=es)

## AEM Forms {#aem-forms}

AEM Forms incluye componentes y flujos de trabajo que capturan, procesan y almacenan datos para organizar procesos empresariales y completar transacciones digitales. Los distintos componentes utilizan diferentes almacenes de datos y, además, permiten la integración con almacenes de datos personalizados. En la siguiente documentación se explican los procedimientos y directrices para acceder a los datos de usuario y gestionarlos con el fin de admitir los flujos de trabajo de protección de datos y privacidad (por ejemplo, el RGPD o la CCPA) de un componente.

* [Portal de Forms](/help/forms/using/forms-portal-handling-user-data.md)
* [Administración de correspondencia](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrar con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flujos de trabajo centrados en Forms en OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flujos de trabajo de Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (solo AEM Forms JEE)
* [Seguridad de documentos](/help/forms/using/document-security-handling-user-data.md) (solo AEM Forms JEE)
* [Administración de usuarios](/help/forms/using/user-management-handling-user-data.md) (solo AEM Forms JEE)
