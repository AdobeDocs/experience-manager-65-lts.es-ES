---
title: Configurar la página para la edición masiva de propiedades de página
description: La edición masiva de propiedades de página permite editar las propiedades de varias páginas a la vez
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 3%

---

# Configurar la página para la edición masiva de propiedades de página {#configuring-your-page-for-bulk-editing-of-page-properties}

[La edición masiva de propiedades de página](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) le permite editar las propiedades de varias páginas a la vez.

Debido a la posibilidad de que existan diferentes valores, las propiedades de página no están habilitadas para la edición por lotes de forma predeterminada. Deben permitirse explícitamente (habilitarse). Al definir las propiedades de página para que estén disponibles para la edición masiva, debe tener en cuenta determinadas implicaciones, como:

* Algunos campos suelen ser únicos; por ejemplo, un título de página. Decida si es relevante habilitar estos campos para la edición masiva, cuando se aplicará un valor.
* Algunos campos pueden tener varios valores; esto necesita una representación significativa al procesar.

  Por ejemplo, una casilla de verificación que indique &quot;Listo para publicación&quot;. Esto puede tener varios valores antes de la edición por lotes (por ejemplo, listo, en revisión o en curso).

>[!CAUTION]
>
>La edición masiva de las propiedades de página es:
>
>* No disponible en la IU clásica.
>* No disponible para páginas dentro de una Live Copy.
>* Solo está disponible para páginas con el mismo tipo de recurso.
>

>[!NOTE]
>
>La edición masiva también está disponible para Assets. Es muy similar, pero difiere en algunos puntos. Consulte [Edición de propiedades de varios Assets](/help/assets/metadata.md) para obtener información completa. Puede personalizar los campos en el editor de metadatos masivos para Assets mediante [Editor de esquemas](/help/assets/metadata-schemas.md).

## Activación de un campo {#enabling-a-field}

>[!NOTE]
>
>Algunos campos pueden tener varios valores; esto necesita una representación significativa al procesar. Por este motivo, solo debe habilitar los siguientes tipos de campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

Los campos están habilitados en el componente de página (*no* en la plantilla):

1. Con CRXDE Lite (o un método equivalente), abra el componente de página.

   Por ejemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >En este ejemplo se supone que los componentes principales se han instalado en la instancia, como sucede si la instancia se ejecuta con contenido de muestra de We.Retail. Consulte la [Documentación de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) para obtener más información.

1. Vaya al campo requerido dentro de la definición de `cq:dialog`.
1. Defina la siguiente propiedad en el nodo de campo:

   * **Nombre**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por ejemplo, para la página estándar [foundation component](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   La propiedad se definiría en:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >    1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
   >    1. Realizar cambios en `/apps`

1. Seleccione **Guardar todo** para mantener las actualizaciones.
