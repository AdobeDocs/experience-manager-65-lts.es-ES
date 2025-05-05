---
title: Configuración de varias tiendas de Commerce
description: Obtenga información sobre cómo asignar varias vistas de tiendas de Adobe Commerce a AEM. Esto permite que los proyectos admitan casos de uso de varios inquilinos y multilingües.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 15%

---

# Configuración de varias tiendas de Commerce {#multi-store}

Los componentes principales de AEM CIF se pueden utilizar en varias estructuras del sitio de AEM y la implementación de cliente de GraphQL subyacente se puede conectar a diferentes tiendas de Adobe Commerce o vistas de tiendas. Esto permite que los proyectos implementen configuraciones complejas de varias tiendas y sitios.

Un tutorial en vídeo que detalla las opciones para integrar varias vistas de la tienda Adobe Commerce con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Las funciones de administración de varios sitios de AEM de Live Copy y de copia de idioma se utilizan con Commerce integration framework para administrar globalmente los sitios en las regiones y las configuraciones regionales.

La configuración recomendada es utilizar una relación 1:1 entre el sitio de AEM y la vista de la tienda de Adobe Commerce.

Para conectar un sitio de AEM y los componentes principales de AEM CIF también a una vista de tienda dedicada, siga los pasos a continuación:

## Configuración {#configuration}

1. Configure varias tiendas y vistas de tiendas según el patrón descrito en [Sitios web, tiendas y vistas de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=es)

2. Asegúrese de que funcione la conexión entre AEM y Adobe Commerce.

3. Cree una configuración secundaria de la configuración del CIF de Cloud Service siguiendo estos pasos:

   * En AEM, vaya a Herramientas > General > [Explorador de configuración](/help/sites-administering/configurations.md#using-configuration-browser)
   * Seleccione la configuración base que ha creado
   * Cree una configuración siguiendo los pasos descritos anteriormente en el punto 2

   Esta nueva configuración se crea como una configuración secundaria de la base. Ahora puede ir a Herramientas > General > Explorador de configuración y crear los ajustes de configuración.

   >[!TIP]
   >
   >Los catálogos Commerce se pueden abordar mediante el uso de ID o UID. Los UID se han introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

4. Asigne la configuración secundaria a un sitio de AEM.

   * Vaya a la consola de AEM Sites
   * Navegue hasta la región o la raíz de idioma de la estructura del sitio, por ejemplo, /content/venia/us _o_ /content/venia/us/es para la página de muestra de Venia
   * Seleccione la página y abra las propiedades de página
   * Seleccione la pestaña Avanzadas.
   * En la sección `Configuration`, seleccione la configuración que creó en el paso

## Recursos adicionales

* [Sitios web, tiendas y vistas de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=es)
* [Componentes principales del CIF de AEM: configuración de varias tiendas y sitios](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Uso del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=es)
* [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-administering/msm.md)
