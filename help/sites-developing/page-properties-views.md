---
title: Personalizar vistas de propiedades de página
description: Cada página tiene un conjunto de propiedades que puede editar según sea necesario
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Personalizar vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-authoring/editing-page-properties.md) que los usuarios pueden ver y editar; algunas son necesarias al crear la página (crear vista), otras se pueden ver y editar (editar vista) en una etapa posterior. Estas propiedades de página se definen y se ponen a disposición mediante el cuadro de diálogo ( `cq:dialog`) del componente de página correspondiente.

>[!CAUTION]
>
>La personalización de la vista de las propiedades de página no está disponible en la IU clásica.

El estado predeterminado de cada propiedad de página es:

* oculto en la vista crear (por ejemplo, **Asistente para crear página**)

* disponible en la vista de edición (por ejemplo, **Ver propiedades**)

Los campos deben configurarse específicamente si se requiere algún cambio. Esto se realiza mediante las propiedades de nodo adecuadas:

* Propiedad de página que estará disponible en la vista de creación (por ejemplo, **Asistente para crear página**):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propiedad de página que estará disponible en la vista de edición (por ejemplo, **Vista**/**Editar**) **Propiedades** (opción)):

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por ejemplo, vea la configuración de los campos agrupados en **Más títulos y descripción** en la ficha **Básico** para el componente Página base. Están visibles en el asistente para **Crear página**, ya que `cq:showOnCreate` se ha establecido en `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte el tutorial [Ampliación de propiedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía sobre cómo personalizar las propiedades de página.

## Configuración de las propiedades de página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo adecuadas.

Por ejemplo, de forma predeterminada, el asistente [**Crear página**](/help/sites-authoring/managing-pages.md#creating-a-new-page) muestra los campos agrupados en **Más títulos y descripción**. Para ocultarlos, configure lo siguiente:

1. Cree su componente de página en `/apps`.
1. Cree una anulación (usando *dialog diff* proporcionada por la [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md)) para la sección `basic` del componente de su página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referencia, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   >Sin embargo, ***no debe*** cambiar nada en la ruta de acceso `/libs`.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
   >1. Realizar cambios en `/apps`

1. Establezca la propiedad `path` en `basic` para que apunte a la anulación de la ficha básica (vea también el paso siguiente). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación de la sección `basic` - `moretitles` en la ruta de acceso correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo adecuada:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   La sección **Más títulos y descripciones** ya no se mostrará en el asistente **Crear página**.

>[!NOTE]
>
>Al configurar las propiedades de página para usarlas con Live Copies, consulte [Configuración de bloqueos MSM en las propiedades de página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de diálogo de la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md); incluido el uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). También ilustra el uso de `cq:showOnCreate` y `cq:hideOnEdit`.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto aem-authoring-extension-page-dialog en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
