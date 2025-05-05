---
title: Paquete de compatibilidad
description: La instalación del paquete de compatibilidad en AEM Forms 6.5 LTS le permite utilizar los recursos de Administración de correspondencia de AEM Forms 6.5 y versiones anteriores, así como las plantillas y páginas de formularios adaptables obsoletos
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 53%

---

# Paquete de compatibilidad{#compatibility-package}

## Información general {#overview}

Interactive Communications es la forma predeterminada y recomendada de crear comunicaciones con los clientes en AEM Forms 6.5 LTS. Para seguir usando cartas en AEM Forms 6.5 LTS, debes instalar el [paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) más reciente.

El paquete de compatibilidad de AEMFD también le permite [usar los siguientes recursos de AEM Forms 6.5.22.0, 6.4, 6.3 y 6.2 en AEM Forms 6.5 LTS](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

Para obtener más información, consulte [Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete Compatibilidad](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Agregue compatibilidad para los recursos de AEM Forms 6.5, 6.4, 6.3 y 6.2 en AEM Forms 6.5 LTS {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

Después de realizar una actualización, haga lo siguiente para instalar el paquete de compatibilidad de AEMFD y hacer que sus recursos sean compatibles con la versión 6.5:

Asegúrese de que tiene preinstalado el [paquete de compatibilidad de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

1. Instale el [paquete de compatibilidad](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) más reciente de AEM 6.5 LTS.

   Para obtener más información sobre cómo cargar e instalar el paquete, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

1. Una vez estabilizados los registros, reinicie el servidor.
1. Utilice la utilidad de migración para hacer que los recursos sean compatibles con 6.5 LTS.

   >[!NOTE]
   >
   > Se recomienda usar el comando `Ctrl + C` para reiniciar SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

   Para obtener más información, consulte [utilidad de migración](../../forms/using/migration-utility.md).

## Assets es compatible con AEM Forms 6.5 LTS mediante la instalación del paquete Compatibilidad {#assetsmadecompatible}

Al instalar el paquete Compatibilidad, puede hacer que los siguientes recursos y plantillas sean compatibles con AEM Forms 6.5 LTS:

* Recursos de Administración de correspondencia de AEM 6.4 y anteriores:

   * [Cartas](../../forms/using/create-letter.md)
   * [Diccionarios de datos](/help/forms/using/data-dictionary.md)
   * Fragmentos de documento

* Plantillas de formularios adaptables obsoletas:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Páginas obsoletas de formularios adaptables:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
