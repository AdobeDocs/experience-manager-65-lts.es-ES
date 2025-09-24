---
title: Habilitar componentes del portal de formularios
description: De serie, los componentes del portal de formularios están deshabilitados. Habilite los grupos Servicios de documentos y Predicados de servicios de documentos para habilitar los componentes del portal de formularios.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: a537fc63-b894-4e47-a71f-98ea07747baa
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 67%

---

# Habilitar componentes del portal de formularios {#enabling-forms-portal-components}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=es).

De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. Para que los componentes aparezcan en la lista de componentes disponibles en la barra de tareas de AEM, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor del sitio web y abra una página de AEM Sites.

1. Para las páginas que utilizan una plantilla estática, realice los siguientes pasos:

   1. En el encabezado de la página, seleccione ![canvas-drop-down](assets/canvas-drop-down.png) > **Diseño** para abrir la página en modo de diseño.
   1. Seleccione cualquier componente (con un borde azul) y, a continuación, seleccione ![nivel de campo](assets/field-level.png) para seleccionar el sistema de párrafos que contiene el componente actual.
   1. En el sistema de párrafos, seleccione ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del sistema de párrafos.
   1. De la lista de **[!UICONTROL Componentes permitidos]**, habilite las casillas de verificación para los componentes **[!UICONTROL Servicios de documentos]** y **[!UICONTROL Predicados de servicios de documentos]**. Seleccione **[!UICONTROL Aceptar]**.

1. Para las páginas que utilizan una plantilla dinámica, realice los siguientes pasos:

   1. En el encabezado de la página, seleccione ![properties](assets/properties.png) > **Editar plantilla** para abrir la plantilla de la página.
   1. Seleccione **Contenedor de diseño** y seleccione ![FeedManagement](/help/forms/using/assets/feedmanagement.png). En la pestaña **Componentes permitidos**, habilite las opciones **Predicados de servicios de documentos y servicios de documentos** y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>También puede habilitar componentes específicos de estas categorías si selecciona los componentes. Para obtener más información sobre los componentes y su uso, consulte [Crear una página del portal de formularios](/help/forms/using/creating-form-portal-page.md) e [Incrustar un componente de vínculo en una página](/help/forms/using/embedding-link-component-page.md).

Ahora, las categorías de componentes Servicios de documentos y Predicados de servicios de documentos están disponibles en el explorador de componentes. Los componentes están habilitados para todas las páginas que utilizan la misma plantilla.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
