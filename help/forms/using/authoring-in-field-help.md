---
title: Crear ayuda en contexto para campos de formulario
description: AEM Forms permite agregar ayuda en contexto a los campos y paneles de los formularios adaptables, como texto o medios enriquecidos, incluidos vídeos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 95%

---

# Crear ayuda en contexto para campos de formulario{#authoring-in-context-help-for-form-fields}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Introducción {#introduction}

Hay situaciones en las que los usuarios finales que rellenan un formulario no están seguros de cómo rellenar los detalles de un campo de formulario concreto. Para solucionar estos problemas, los formularios adaptables proporcionan asistencia para agregar texto o ayuda en contexto enriquecida en un campo de formulario. Esto contribuye a mejorar la experiencia de rellenado de los formularios y evita cualquier tipo de ambigüedad a los usuarios finales.

En este artículo se explica cómo los autores de formularios pueden agregar ayuda en contexto durante la creación de formularios adaptables.

## Agregar ayuda en contexto {#add-in-context-help}

Puede especificar la ayuda en contexto mediante las siguientes opciones de la sección Contenido de ayuda de la pestaña Propiedades de la barra lateral.

* [Descripción breve](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Descripción larga](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Ayuda en contexto para campos de formulario](assets/descriptions.png)

>[!NOTE]
>
>La descripción larga invalida la descripción breve. Si ha especificado ambas, solo se mostrará la descripción larga.

### Descripción breve {#short-description}

El campo Descripción breve proporciona sugerencias rápidas y cortas sobre cómo rellenar un campo de formulario. El texto especificado en el campo Descripción breve se muestra como información sobre herramientas al pasar el ratón por encima del campo.

![Descripción breve para agregar ayuda en contexto para los campos de formulario](assets/tooltip.png)

>[!NOTE]
>
>Seleccione **Mostrar siempre una descripción breve** para mostrar permanentemente el texto de ayuda debajo del campo.

![Ayuda breve permanente en contexto debajo del campo](assets/short1.png)

### Descripción larga {#long-description}

Puede utilizar el campo Descripción larga para especificar texto largo o incrustar contenido con medios enriquecidos, incluidos vídeos, como ayuda en contexto. Por ejemplo, la siguiente imagen muestra cómo incrustar un vídeo como ayuda en contexto.

![Adición de medios enriquecidos como ayuda en contexto para campos de formulario](assets/long-descriptions.png)

Al añadir una descripción larga, se muestra el icono **?** junto al campo. Al hacer clic en el icono, se muestra el contenido añadido en la sección Descripción larga.

![Ejemplo de ayuda en contexto con medios enriquecidos](assets/photoshop.png)

### Ayuda a nivel de panel {#panel-level-help}

Además de la ayuda en contexto de los campos de formulario, puede especificar ayuda a nivel de panel en la pestaña Contenido de ayuda del cuadro de diálogo de edición del panel.

![Adición de ayuda en contexto para el panel de un formulario](assets/panel-level-help.png)

Al añadir ayuda al panel, se muestra el icono **?** junto a la descripción del panel. Al hacer clic en el icono, se muestra el contenido añadido en la sección Contenido de ayuda del cuadro de diálogo de edición del panel.

![Ejemplo de ayuda en contexto a nivel del panel de formulario](assets/photoshop-1.png)
