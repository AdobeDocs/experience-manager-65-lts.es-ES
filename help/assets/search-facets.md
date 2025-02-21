---
title: Facetas de búsqueda para filtrar los resultados
description: Crear, modificar y usar facetas de búsqueda en  [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 16%

---

# Facetas de búsqueda {#search-facets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=en) |
| AEM 6.5 | Este artículo |

Una implementación de [!DNL Adobe Experience Manager Assets] en toda la empresa tiene la capacidad de almacenar muchos recursos. A veces, encontrar el recurso adecuado puede ser arduo y requerir mucho tiempo si solo usa las capacidades de búsqueda genéricas de [!DNL Experience Manager].

Utilice las facetas de búsqueda en el panel Filtros para añadir más granularidad a la experiencia de búsqueda y hacer que la funcionalidad de búsqueda sea más eficiente y versátil. Las facetas de búsqueda añaden varias dimensiones (predicados) que permiten realizar búsquedas más complejas. El panel Filtros incluye algunas facetas estándar. También puede agregar facetas de búsqueda personalizadas.

En resumen, las facetas de búsqueda le permiten buscar recursos de varias formas en lugar de en un único orden taxonómico predeterminado. Puede explorar en profundidad fácilmente el nivel de detalle deseado para lograr una búsqueda más enfocada.

Por ejemplo, si está buscando una imagen, puede elegir si desea un mapa de bits o una imagen vectorial. Puede reducir aún más el ámbito de la búsqueda especificando el tipo MIME de la imagen. Del mismo modo, al buscar documentos, puede especificar el formato, por ejemplo, PDF o MS Word.

## Añadir un predicado {#adding-a-predicate}

Las facetas de búsqueda que aparecen en el panel Filtros se definen en el formulario de búsqueda subyacente mediante predicados. Para mostrar más o diferentes facetas, agregue predicados al formulario predeterminado o utilice un formulario personalizado que incluya las facetas que elija.

Para las búsquedas de texto completo, agregue el predicado **[!UICONTROL Fulltext]** al formulario. Utilice el predicado Propiedad para buscar recursos que coincidan con una sola propiedad especificada. Utilice el predicado Opciones para buscar recursos que coincidan con uno o varios valores de una propiedad en particular. Agregue el predicado Intervalo de fechas para buscar recursos creados dentro de un intervalo de fechas especificado.

1. Haga clic en el logotipo de [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página [!UICONTROL Buscar en Forms], seleccione **[!UICONTROL Carril de búsqueda de administración de Assets]** y luego haga clic en **[!UICONTROL Editar]** ![editar icono](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >Para usar la funcionalidad de búsqueda de carpetas del carril de búsqueda de administración de [!DNL Assets] preconfigurado de una versión anterior, realice estos pasos:
   >
   >1. Vaya a `/conf/global/settings/dam/search/facets/assets/jcr:content/items` en CRXDE.
   >1. Elimine el nodo `type`.
   >1. Desde la ruta de acceso `/libs/settings/dam/search/facets/assets/jcr:content/items`, copie los nodos `asset`, `directory`, `typeor`, `excludepaths` y `searchtype` en la ruta de acceso mencionada en el paso 1.
   >1. Guarde los cambios.

1. En la página [!UICONTROL Editar búsqueda en Forms], arrastre un predicado desde la ficha **[!UICONTROL Seleccionar predicado]** al panel principal. Por ejemplo, arrastre **[!UICONTROL Predicado de propiedad]**.

   ![Seleccione y mueva un predicado para personalizar los filtros de búsqueda](assets/drag_predicate.png)

   *Figura: Seleccione y mueva un predicado para personalizar los filtros de búsqueda.*

1. En la ficha [!UICONTROL Configuración], escriba una etiqueta de campo, texto de marcador de posición y descripción para el predicado. Especifique un nombre válido para la propiedad de metadatos que desee asociar al predicado. La etiqueta de encabezado de la ficha [!UICONTROL Configuración] identifica el tipo de predicado seleccionado.

1. En el campo [!UICONTROL Nombre de propiedad], indique un nombre válido para la propiedad de metadatos que desea asociar al predicado. Es el nombre sobre el cual se realiza la búsqueda. Por ejemplo, escriba `jcr:content/metadata/dc:description` o `./jcr:content/metadata/dc:description`.

   También puede seleccionar un nodo existente del cuadro de diálogo de selección.

   ![Asociar una propiedad de metadatos con un predicado en el campo Nombre de propiedad](assets/property_settings.png)

   Asocie una propiedad de metadatos con un predicado en el campo Nombre de propiedad

1. Haga clic en la **[!UICONTROL vista previa]** ![vista previa](assets/do-not-localize/preview_icon.png) para generar una vista previa del panel Filtros tal y como aparece después de agregar el predicado.
1. Revise el diseño del predicado en el modo Vista previa.

   ![Previsualice el formulario de búsqueda antes de enviar los cambios](assets/preview-1.png)

   Previsualice el formulario de búsqueda antes de enviar los cambios

1. Para cerrar la vista previa, haz clic en **[!UICONTROL Cerrar]** ![cerrar](assets/do-not-localize/close.png) en la esquina superior derecha de la vista previa.
1. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.
1. Vaya al panel Buscar en la interfaz de usuario [!DNL Assets]. El predicado Propiedad se agrega al panel.
1. Escriba una descripción del recurso que se va a buscar en el cuadro de texto. Por ejemplo, escriba `Adobe`. Al realizar una búsqueda, los recursos con una descripción que coincida con `Adobe` se muestran en los resultados de la búsqueda.

## Agregar un predicado de opciones {#adding-an-options-predicate}

El predicado Opciones permite agregar varias opciones de búsqueda en el panel Filtros. Puede seleccionar una o varias de estas opciones en el panel Filtros para buscar recursos. Por ejemplo, para buscar recursos en función del tipo de archivo, configure opciones como Imágenes, Multimedia, Documentos y Archivos en el formulario de búsqueda. Después de configurar estas opciones, la búsqueda se realiza en recursos de tipo GIF, JPEG, PNG, etc. al seleccionar la opción Imágenes en el panel Filtros.

Para asignar las opciones a la propiedad respectiva, cree una estructura de nodos para las opciones y proporcione la ruta del nodo principal en la propiedad Nombre de propiedad del predicado Opciones. El nodo principal debe ser del tipo `sling`: `OrderedFolder`. Las opciones deben ser del tipo `nt:unstructured`. Los nodos de opción deben tener las propiedades `jcr:title` y `value` configuradas.

La propiedad `jcr:title` es un nombre descriptivo para la opción que se muestra en el panel Filtros. El campo `value` se usa en la consulta para coincidir con la propiedad especificada.

Al seleccionar una opción, la búsqueda se realiza en función de la propiedad `value` del nodo de opción y sus nodos secundarios, si los hay. El árbol completo bajo el nodo de opción se atraviesa y la propiedad `value` de cada nodo secundario se combina mediante una operación OR para formar la consulta de búsqueda.

Por ejemplo, si selecciona “Imágenes” para los tipos de archivo, la consulta de búsqueda de los recursos se genera combinando la propiedad `value` mediante una operación O. Por ejemplo, la búsqueda de imágenes se genera combinando los resultados coincidentes para *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, e *image/tiff* `jcr:content/metadata/dc:format` para la propiedad mediante una operación OR.

![La propiedad Value de un tipo de archivo, tal como se ve en CRXDE, se usa para que funcionen las consultas de búsqueda](assets/filetype-value-property.png)

La propiedad Value de un tipo de archivo, tal como se ve en CRXDE, se utiliza para que funcionen las consultas de búsqueda

En lugar de crear manualmente una estructura de nodos para las opciones del repositorio CRXDE, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Nombre de propiedad]**. Por ejemplo, puede definir los pares clave-valor `image/bmp`, `image/gif`, `image/jpeg` y `image/png`, y especificar sus valores como se muestra en el siguiente archivo JSON de muestra. En el campo **[!UICONTROL Nombre de propiedad]**, puede especificar la ruta CRXDE para este archivo.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Si desea utilizar un nodo existente, especifíquelo mediante el cuadro de diálogo de selección.

>[!NOTE]
>
>El predicado Opciones es un contenedor personalizado que incluye predicados de propiedad para demostrar el comportamiento descrito. Actualmente, no hay ningún extremo REST disponible para admitir la funcionalidad de forma nativa.

1. Haga clic en el logotipo de [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página **[!UICONTROL Buscar en Forms]**, seleccione **[!UICONTROL Carril de búsqueda de administración de Assets]** y haga clic en **[!UICONTROL Editar]**.
1. En la página **[!UICONTROL Editar formulario de búsqueda]**, arrastre **[!UICONTROL Predicado de opciones]** desde la pestaña **[!UICONTROL Seleccionar predicado]** al panel principal.
1. En la pestaña **[!UICONTROL Configuración]**, indique una etiqueta y un nombre para la propiedad. Por ejemplo, para buscar recursos según su formato, especifique un nombre descriptivo para la etiqueta, por ejemplo, **[!UICONTROL Tipo de archivo]**. Especifique la propiedad en función de la cual se realizará la búsqueda en el campo de propiedad, por ejemplo, `jcr:content/metadata/dc:format.`
1. Realice una de las siguientes acciones:

   * En el campo **[!UICONTROL Nombre de propiedad]**, mencione la ruta del archivo JSON donde define los nodos para las opciones y especifique los pares de clave-valor correspondientes.
   * Haga clic en el símbolo `+` al lado del campo Opciones para especificar el texto y el valor de visualización de las opciones que desea proporcionar en el panel Filtros. Para agregar otra opción, haga clic en el símbolo `+` y repita el paso.

1. Compruebe que la opción **[!UICONTROL Selección única]** se borra para que el usuario pueda seleccionar varias opciones a la vez para diferentes tipos de archivos (por ejemplo, imágenes, documentos, multimedia y archivos). Si elige **[!UICONTROL Selección única]**, el usuario solo puede seleccionar una opción para diferentes tipos de archivo a la vez.

   ![Los campos disponibles en el predicado de opciones](assets/options_predicate.png)

   Los campos disponibles en el predicado Opciones

1. En el campo **[!UICONTROL Descripción]**, escriba una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Buscar. El predicado Opciones se agrega al panel **Buscar**. Las opciones de **[!UICONTROL Tipo de archivo]** se muestran como casillas de verificación.

## Agregar un predicado de propiedad de varios valores {#adding-a-multi-value-property-predicate}

El predicado Propiedad de varios valores permite buscar recursos para varios valores. Imagine un escenario en el que tiene imágenes de varios productos en [!DNL Assets] y los metadatos de cada imagen incluyen un número de SKU asociado al producto. Puede utilizar este predicado para buscar imágenes de productos basadas en varios números de SKU.

1. Haga clic en el logotipo de [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página Buscar en Forms, seleccione **[!UICONTROL Carril de búsqueda de administración de Assets]** y haga clic en **[!UICONTROL Editar]** ![editar icono](assets/do-not-localize/aemassets_edit.png).
1. En la página Editar formulario de búsqueda, arrastre un **[!UICONTROL predicado de propiedades de varios valores]** desde la pestaña **[!UICONTROL Seleccionar predicado]** hasta el panel principal.
1. En la ficha **[!UICONTROL Configuración]**, escriba una etiqueta y un texto de marcador de posición para el predicado. Especifique el nombre de la propiedad en función del cual se realizará la búsqueda en el campo de propiedad, por ejemplo, `jcr:content/metadata/dc:value`. También puede utilizar el cuadro de diálogo de selección para seleccionar un nodo.
1. Asegúrese de que la opción **[!UICONTROL Compatibilidad con delimitadores]** está seleccionada. En el campo **[!UICONTROL Delimitadores de entrada]**, especifique delimitadores para separar valores individuales. De forma predeterminada, se especifica una coma como delimitador. Puede especificar un delimitador diferente.
1. En el campo **Descripción**, escriba una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Filtros en la interfaz de usuario [!DNL Assets]. El predicado **[!UICONTROL Propiedad de varios valores]** se agrega al panel.
1. Especifique varios valores en el campo Valor múltiple separados por delimitadores y realice la búsqueda. El predicado obtiene una coincidencia de texto exacta para los valores especificados.

## Añadir un predicado de etiquetas {#adding-a-tags-predicate}

El predicado Etiqueta permite realizar búsquedas de recursos basadas en etiquetas. De manera predeterminada, [!DNL Assets] busca recursos para una o más coincidencias de etiquetas en función de las etiquetas especificadas. En otras palabras, la consulta de búsqueda realiza una operación OR utilizando las etiquetas especificadas. Sin embargo, puede utilizar la opción Coincidir con todas las etiquetas para buscar recursos que incluyan todas las etiquetas que especifique.

1. Haga clic en el logotipo de [!DNL Experience Manager] y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Buscar en Forms]**.
1. En la página Buscar en Forms, seleccione **[!UICONTROL Carril de búsqueda de administración de Assets]** y haga clic en **[!UICONTROL Editar]** ![editar icono](assets/do-not-localize/aemassets_edit.png).
1. En la página Editar formulario de búsqueda, arrastre **[!UICONTROL Predicado de etiquetas]** desde la pestaña Seleccionar predicado al panel principal.
1. En la pestaña Configuración, introduzca un texto de marcador de posición para el predicado. Especifique el nombre de la propiedad en función del cual se realizará la búsqueda en el campo de propiedad, por ejemplo, *jcr:content/metadata/cq:tags*. También puede seleccionar un nodo en CRXDE desde el cuadro de diálogo de selección.
1. Configure la propiedad Ruta de etiquetas raíz de este predicado para rellenar varias etiquetas en la lista Etiquetas.
1. Seleccione la opción **[!UICONTROL Mostrar todas las etiquetas]** para buscar recursos que incluyan todas las etiquetas que especifique.

1. En el campo **[!UICONTROL Descripción]**, escriba una descripción opcional y haga clic en **[!UICONTROL Listo]**.
1. Vaya al panel Buscar. El predicado **[!UICONTROL Etiquetas]** se agrega al panel Buscar.
1. Especifique las etiquetas en función de las cuales desea buscar recursos o seleccione en la lista de sugerencias.

1. Seleccione **[!UICONTROL Coincidir todo]** para buscar coincidencias que incluyan todas las etiquetas especificadas.

## Añadir otros predicados {#adding-other-predicates}

De forma similar a la forma de agregar un predicado Propiedad o Opciones, puede agregar los siguientes predicados adicionales al panel Buscar:

| Nombre de predicado | Descripción | Propiedades |
|---|---|---|
| [!UICONTROL Texto Completo] | Predicado de búsqueda para realizar una búsqueda de texto completo en todo un nodo de recursos. Se asigna con el operador jcr:contains. Puede especificar una ruta relativa si desea realizar una búsqueda de texto completo en una parte específica del nodo del recurso. | <ul><li>Etiqueta</li><li>Marcador de posición</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Navegador de rutas] | Predicado de búsqueda para buscar recursos en carpetas y subcarpetas en una ruta raíz preconfigurada | <ul><li>Marcador de posición</li><li>Ruta raíz</li><li>Descripción</li></ul> |
| [!UICONTROL Ruta] | Utilícelo para filtrar los resultados según la ubicación. Puede especificar diferentes rutas como opciones. | <ul><li>Etiqueta</li><li>Ruta</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de publicación] | Predicado de búsqueda para buscar recursos en función de su estado de publicación | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Fecha relativa] | Predicado de búsqueda para buscar recursos en función de la fecha relativa de su creación. Por ejemplo, puede configurar opciones, como hace 2 meses, hace 3 semanas, etc. | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Fecha relativa</li></ul> |
| [!UICONTROL Intervalo] | Predicado de búsqueda para buscar recursos que se encuentren dentro de un rango especificado. En el panel Buscar, puede especificar los valores mínimo y máximo del rango. | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Intervalo de fecha] | Predicado de búsqueda para buscar recursos creados dentro de un intervalo especificado para una propiedad de fecha. En el panel Buscar, puede especificar las fechas de inicio y finalización mediante selectores de fechas. | <ul><li>Etiqueta</li><li>Marcador de posición</li><li>Nombre de la propiedad</li><li>Texto de intervalo (desde)</li><li>Texto de intervalo (hasta)</li><li>Descripción</li></ul> |
| [!UICONTROL Fecha] | Predicado de búsqueda para una búsqueda de recursos basada en un control deslizante y basada en una propiedad de fecha. | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Tamaño de archivo] | Predicado de búsqueda para buscar recursos en función de su tamaño. Es un predicado basado en deslizadores en el que se seleccionan las opciones del deslizador desde un nodo configurable. Las opciones predeterminadas se definen en /libs/dam/options/predicates/filesize en el repositorio CRXDE. El tamaño de archivo se proporciona en bytes. | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Ruta</li><li>Descripción</li></ul> |
| [!UICONTROL Última modificación del recurso] | Predicado de búsqueda para buscar recursos modificados recientemente | <ul><li>Nombre de la propiedad</li><li>Valor de propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de publicación] | Busque predicados para buscar recursos en función de su estado de publicación | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Clasificación] | Predicado de búsqueda para buscar recursos en función de su clasificación promedio | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Ruta de opción</li><li>Descripción</li></ul> |
| [!UICONTROL Estado de caducidad] | Predicado de búsqueda para buscar recursos en función de su estado de caducidad | <ul><li>Etiqueta</li><li>Nombre de la propiedad</li><li>Descripción</li></ul> |
| [!UICONTROL Oculto] | Predicado de búsqueda que define una propiedad de campo oculto para buscar recursos | <ul><li>Nombre de la propiedad</li><li>Valor de propiedad</li><li>Descripción</li></ul> |

## Restaurar las facetas de búsqueda predeterminadas {#restoring-default-search-facets}

De manera predeterminada, aparece un icono de candado ![icono de candado cerrado](assets/do-not-localize/lock_closed_icon.svg) antes de **[!UICONTROL Carril de búsqueda de administración de Assets]** en la página **[!UICONTROL Buscar en Forms]**. El icono de bloqueo de una opción de la página Buscar Forms indica que la configuración predeterminada está intacta y no está personalizada. El icono ![bloquear icono cerrado](assets/do-not-localize/lock_closed_icon.svg) desaparece si agrega facetas de búsqueda al formulario que indican que se ha modificado el formulario predeterminado.

![Icono de candado](assets/locked_admin_rail.png)

Para restaurar la faceta de búsqueda predeterminada, realice estos pasos:

1. Seleccione **[!UICONTROL Carril de búsqueda de administración de Assets]** en la página **[!UICONTROL Buscar en Forms]**.
1. Haga clic en **[!UICONTROL Eliminar]** ![deleteoutline](assets/do-not-localize/deleteoutline.png) en la barra de herramientas.
1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Eliminar]** para quitar los cambios personalizados.

   Después de eliminar los cambios personalizados en las facetas de búsqueda, el icono de candado ![icono de candado cerrado](assets/do-not-localize/lock_closed_icon.svg) vuelve a aparecer antes de **[!UICONTROL Carril de búsqueda de administración de Assets]** en la página **[!UICONTROL Buscar en Forms]**.

## Permisos de usuario {#user-permissions}

Si no se le ha asignado una función de administrador, aquí encontrará una lista de los permisos que necesita para realizar las acciones de edición, eliminación y vista previa que implican facetas de búsqueda.

| Acción | Permisos |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Editar] | Permisos de lectura y escritura en el nodo `/apps` en CRXDE |
| [!UICONTROL Eliminar] | Permisos de lectura, escritura y eliminación en el nodo `/apps` en CRXDE |
| [!UICONTROL Previsualizar] | Permisos de lectura, escritura y eliminación en el nodo `/var/dam/content` en CRXDE. Además, permisos de lectura y escritura en el nodo `/apps`. |

>[!MORELIKETHIS]
>
>* [Ampliar capacidad de búsqueda de recursos](searchx.md)
>* [Buscar recursos](search-assets.md)
