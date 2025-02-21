---
title: Funciones de diseño de los formularios adaptables
description: El diseño y el aspecto visual de los formularios adaptables en diferentes dispositivos se rigen por la configuración de diseño. Obtenga información sobre los distintos diseños y cómo aplicarlos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 99%

---

# Funciones de diseño de los formularios adaptables{#layout-capabilities-of-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/layout-capabilities-adaptive-forms.html) |
| AEM 6.5 | Este artículo |


Adobe Experience Manager (AEM) permite crear formularios adaptables fáciles de usar que ofrecen experiencias dinámicas a los usuarios finales. El diseño del formulario controla cómo se muestran los elementos o los componentes de un formulario adaptable.

## Conocimientos previos requeridos {#prerequisite-knowledge}

Antes de familiarizarse con las diferentes funciones de diseño de los formularios adaptables, lea los siguientes artículos para obtener más información sobre los formularios adaptables.

[Introducción a AEM Forms](../../forms/using/introduction-aem-forms.md)

[Introducción a la creación de formularios](../../forms/using/introduction-forms-authoring.md)

## Tipos de diseños {#types-of-layouts}

Un formulario adaptable proporciona los siguientes tipos de diseños:

**Diseño de panel**: controla cómo se muestran los elementos o componentes de un panel en un dispositivo.

**Diseño móvil**: controla la navegación de un formulario en un dispositivo móvil. Si la anchura del dispositivo es de 768 píxeles o más, el diseño se considera un diseño para móviles y se optimiza para un dispositivo móvil.

**Diseño de barra de herramientas**: controla la ubicación de los botones de acción en la barra de herramientas o la barra de herramientas del panel de un formulario.

Todos estos diseños de panel se definen en la siguiente ubicación:

`/libs/fd/af/layouts`.

>[!NOTE]
>
>Para cambiar el diseño de un formulario adaptable, utilice el modo Autor de AEM.

![Ubicación de los diseños en el repositorio CRX](assets/layouts_location_in_crx.png)

## Diseño de panel {#panel-layout}

Un autor de formularios puede asociar un diseño a cada uno de los paneles de un formulario adaptable, incluido el panel raíz.

Los diseños de panel están disponibles en la ubicación `/libs/fd/af/layouts/panel`. 

![Lista de diseños de panel del panel raíz de un formulario adaptable](assets/layouts.png)

Lista de diseños de panel de los formularios adaptables

### Adaptable: todo en una página sin navegación {#responsive-everything-on-one-page-without-navigation-br}

Utilice este diseño de panel para crear un diseño adaptable que se ajuste al tamaño de pantalla del dispositivo sin necesidad de utilizar ningún tipo de navegación especializada.

Con este diseño, puede colocar varios componentes **[!UICONTROL Formulario adaptable con panel]** uno tras otro en el panel.

![Un formulario con diseño adaptable, tal como se ve en una pantalla pequeña](assets/responsive_layout_seen_on_small_screen.png)

Un formulario con diseño adaptable, tal como se ve en una pantalla pequeña

![Un formulario con diseño adaptable, tal como se ve en una pantalla grande](assets/responsive_layout_seen_on_large_screen.png)

Un formulario con diseño adaptable, tal como se ve en una pantalla grande

### Asistente: un formulario con varios pasos que se muestra paso por paso {#wizard-a-multi-step-form-showing-one-step-at-a-time}

Utilice este diseño de panel para proporcionar navegación guiada dentro de un formulario. Por ejemplo, utilice este diseño cuando desee capturar información obligatoria en un formulario y guiar a los usuarios paso a paso.

Utilice el componente `Panel adaptive form` para proporcionar navegación paso a paso dentro de un panel. Cuando se utiliza este diseño, el usuario solo puede pasar al siguiente paso una vez que ha completado el paso actual.

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Expresión de finalización de los pasos en el diseño Asistente de un formulario de varios pasos](assets/layout-sidebar.png)

Expresión de finalización de los pasos en el diseño Asistente de un formulario de varios pasos

![Un formulario con el diseño Asistente](assets/wizard-layout.png)

Un formulario con el diseño Asistente

### Diseño de acordeón {#layout-for-accordion-design}

Con este diseño, puede colocar el componente `Panel adaptive form` en un panel con navegación de estilo acordeón. Este diseño también permite crear paneles repetibles. Los paneles repetibles permiten agregar o quitar paneles de forma dinámica según sea necesario. Puede definir el número mínimo y máximo de veces que se repite un panel. Además, el título del panel se puede determinar dinámicamente en función de la información proporcionada en los elementos del panel.

La expresión de resumen se puede utilizar para mostrar los valores proporcionados por el usuario final en el título del panel minimizado.

![Paneles repetibles con el diseño Acordeón en un formulario adaptable](assets/repeatable_panels_using_accordion_layout.png)

Paneles repetibles creados con el diseño Acordeón

### Diseño con pestañas: las pestañas aparecen a la izquierda {#tabbed-layout-tabs-appear-on-the-left}

Con este diseño, puede colocar el componente `Panel adaptive form` en un panel con navegación basada en pestañas. Las pestañas se colocan a la izquierda del contenido del panel.

![En el Diseño con pestañas, las pestañas aparecen a la izquierda](assets/tabbed_layout_left.png)

Las pestañas aparecen a la izquierda del panel

### Diseño con pestañas: las pestañas aparecen en la parte superior {#tabbed-layout-tabs-appear-on-the-top}

Con este diseño, puede colocar el componente `Panel adaptive form` en un panel con navegación basada en pestañas. Las pestañas se colocan sobre el contenido del panel.

![Diseño con pestañas en un formulario adaptable con pestañas en la parte superior](assets/tabbed_layout_top.png)

Las pestañas aparecen en la parte superior del panel

## Diseños móviles {#mobile-layouts}

Los diseños móviles proporcionan una navegación fácil de usar en los dispositivos móviles con pantallas relativamente más pequeñas. Los diseños móviles utilizan estilos con pestañas o de asistente para la navegación del formulario. La aplicación de un diseño para móvil proporciona un diseño único para todo el formulario.

Este diseño controla la navegación mediante una barra y un menú de navegación. La barra de navegación muestra los iconos **&lt;** y **>** para indicar los pasos de navegación **Siguiente** y **Anterior** en el formulario.

Los diseños móviles están disponibles en la ubicación `/libs/fd/af/layouts/mobile/`. Los siguientes diseños móviles están disponibles en los formularios adaptables de forma predeterminada.

![Lista de diseños móviles de un formulario adaptable](assets/mobile-navigation.png)

Lista de diseños móviles de un formulario adaptable

Cuando se utiliza un diseño móvil, el menú del formulario está disponible para acceder a los diferentes paneles del formulario pulsando el icono ![aem6forms_menú_formulario](assets/aem6forms_form_menu.png).

### Diseño con títulos de panel en el encabezado del formulario {#layout-with-panel-titles-in-the-form-header}

Este diseño, como su nombre indica, muestra los títulos de los paneles junto con el menú y la barra de navegación. También incluye los iconos Siguiente y Anterior para la navegación.

![Diseños móviles con títulos de panel en los encabezados del formulario](assets/mobile_layout_with.png)

Diseños móviles con títulos de panel en los encabezados del formulario

### Diseño sin títulos de panel en el encabezado del formulario {#layout-without-panel-titles-in-the-form-header}

Este diseño, como su nombre indica, muestra únicamente el menú y la barra de navegación, sin títulos de panel. También incluye los iconos Siguiente y Anterior para la navegación.

![Diseños móviles sin títulos de panel en los encabezados del formulario](assets/mobile_layout_without.png)

Diseños móviles sin títulos de panel en los encabezados del formulario

## Diseños de barra de herramientas {#toolbar-layouts}

El diseño de barra de herramientas controla la colocación y la visualización de cualquier botón de acción que agregue a los formularios adaptables. El diseño se puede agregar en el nivel de formulario o de panel.

![Una lista de diseños de barra de herramientas en formularios adaptables para controlar el diseño de los botones](assets/toolbar-layouts.png)

Una lista de diseños de barra de herramientas en formularios adaptables

Los diseños de barra de herramientas están disponibles en la ubicación `/libs/fd/af/layouts/toolbar`. Los formularios adaptables proporcionan los siguientes diseños de barra de herramientas de forma predeterminada.

### Diseño predeterminado para la barra de herramientas {#default-layout-for-toolbar}

Este diseño está seleccionado como el diseño predeterminado cuando se añaden botones de acción a un formulario adaptable. Al seleccionar este diseño, se muestra el mismo diseño tanto para los equipos de escritorio como para los dispositivos móviles.

Además, puede agregar varias barras de herramientas que contengan botones de acción configurados con este diseño. Un botón de acción está asociado a un control de formulario. Puede configurar las barras de herramientas para que aparezcan antes o después de un panel.

![Vista predeterminada de la barra de herramientas](assets/toolbar_layout_default.png)

Vista predeterminada de la barra de herramientas

### Diseño fijo móvil para la barra de herramientas {#mobile-fixed-layout-for-toolbar}

Seleccione este diseño para proporcionar diseños alternativos para los equipos de escritorio y los dispositivos móviles.

En el caso del diseño de escritorio, puede agregar botones de acción utilizando una serie de etiquetas específicas. Solo se puede configurar una barra de herramientas con este diseño. Si hay más de una barra de herramientas configurada con este diseño, se produce una superposición en los dispositivos móviles y se muestra únicamente una barra de herramientas. Por ejemplo, puede colocar una barra de herramientas en la parte inferior o superior del formulario, o antes o después de los paneles.

En el caso del diseño móvil, puede añadir botones de acción mediante iconos.

![Diseño fijo móvil para la barra de herramientas](assets/toolbar_layout_mobile_fixed.png)

Diseño fijo móvil para la barra de herramientas
