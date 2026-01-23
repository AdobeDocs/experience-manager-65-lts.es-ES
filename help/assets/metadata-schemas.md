---
title: Los esquemas de metadatos definen el diseño de la página de propiedades de metadatos
description: El esquema de metadatos define el diseño de la página de propiedades y las propiedades de metadatos mostradas para los recursos. Obtenga información sobre cómo crear esquemas de metadatos personalizados, editar esquemas de metadatos y cómo aplicar esquemas de metadatos a recursos.
mini-toc-levels: 1
role: User,Admin
feature: Metadata
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: bf5c2dff-db68-4e82-8217-ff35069dcb81
source-git-commit: 86ca5b498d0a51e21e247d07ce186d8a01c95baa
workflow-type: tm+mt
source-wordcount: '3607'
ht-degree: 7%

---

# Esquemas de metadatos {#metadata-schemas}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=en) |
| AEM 6.5 | Este artículo |

Las organizaciones idean un modelo de metadatos que mejora la detección de recursos, el uso, la interoperabilidad, etc. La aplicación correcta de metadatos es sacrosanta para mantener flujos de trabajo y procesos impulsados por metadatos. Para adherirse a la estrategia y los estándares de metadatos de toda la organización, puede utilizar esquemas de metadatos que ayuden a los usuarios de DAM a alinearse. [!DNL Adobe Experience Manager] permite métodos fáciles y flexibles para crear, mantener y aplicar esquemas de metadatos.

En [!DNL Adobe Experience Manager Assets], los esquemas contienen campos específicos para que se rellene la información específica. También contiene información de diseño para mostrar los campos de metadatos de una manera fácil de usar. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y más. Puede usar el editor [!UICONTROL Metadata Schema Forms] para modificar los esquemas existentes o agregar esquemas de metadatos personalizados.

Para ver y editar la página de propiedades de un recurso, siga estos pasos:

1. Haga clic en la opción **[!UICONTROL Ver propiedades]** de las acciones rápidas en el mosaico del recurso en la vista de tarjeta. También puede seleccionar un recurso y, a continuación, hacer clic en **[!UICONTROL Propiedades]** ![ver propiedades](assets/do-not-localize/info-circle-icon.png) en la barra de herramientas.

1. Puede editar las distintas propiedades de metadatos editables en las pestañas disponibles. Sin embargo, no puede modificar el recurso [!UICONTROL Type] en la ficha [!UICONTROL Básico] de la página de propiedades.

   ![Pestaña básica de propiedades del recurso, donde no se puede cambiar el tipo de recurso](assets/asset-properties-basic-tab.png)

   *Imagen: ficha Básico del recurso [!UICONTROL Propiedades].*

   Asegúrese de que solo se asigna una propiedad a un campo mientras crea o edita el esquema de metadatos.

   Para modificar el tipo MIME de un recurso, utilice un formulario de esquema de metadatos personalizado o modifique un formulario existente. Consulte [Editar esquema de metadatos Forms](#edit-metadata-schema-forms) para obtener más información. Si modifica el esquema de metadatos de un tipo MIME, se modifica el diseño de página de propiedades de los recursos y de todos los subtipos. Por ejemplo, si se modifica un esquema JPEG en `default/image`, solo se modifica el diseño de metadatos (propiedades de recursos) de los recursos con el tipo MIME `image/jpeg`. Sin embargo, si edita el esquema predeterminado, los cambios modifican el diseño de los metadatos para todos los tipos de recursos.

## Formularios de esquema de metadatos {#default-metadata-schema-forms}

Para ver una lista de formularios o plantillas, en la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.

[!DNL Experience Manager] proporciona las siguientes plantillas de formulario de esquema de metadatos.

| Plantillas | | Descripción |
|---|---|---|
| [!UICONTROL predeterminado] | | El formulario de esquema de metadatos base para los recursos. |
| | Los siguientes formularios secundarios heredan las propiedades del formulario [!UICONTROL default]: | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Formulario de esquema para vídeos de Dynamic Media. |
| | <ul><li>[!UICONTROL imagen]</li></ul> | Formulario de esquema para imágenes con el tipo MIME como `image/jpeg` y `image/png`. <br> El formulario [!UICONTROL image] tiene las siguientes plantillas de formulario secundarias: <ul><li> [!UICONTROL jpeg]: Formulario de esquema para recursos con subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: formulario de esquema para los recursos con subtipo TIFF.</li></ul> |
| | <ul><li>[!UICONTROL aplicación]</li></ul> | Formulario de esquema para recursos con tipo MIME como `application/pdf` y `application/zip`. <br>[!UICONTROL pdf]: Formulario de esquema para recursos con subtipo PDF. |
| | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulario de esquema para recursos de vídeo con tipo MIME como `video/avi` y `video/mp4`. |
| [!UICONTROL colección] | | Formulario de esquema para colecciones. |
| [!UICONTROL fragmento de contenido] | | [Formulario de esquema para fragmentos de contenido](/help/sites-developing/customizing-content-fragments.md). |
| [!UICONTROL formularios] | | Este formulario de esquema está relacionado con [Adobe Experience Manager Forms](/help/forms/using/introduction-aem-forms.md). |
| [!UICONTROL ugc_contentfragment] | | Formulario de esquema para elementos y recursos de contenido generado por el usuario e integrado en Experience Manager desde medios sociales. |

>[!NOTE]
>
>Para ver los formularios secundarios de un formulario de esquema, haga clic en su nombre.

## Agregar un formulario de esquema de metadatos {#add-a-metadata-schema-form}

Para agregar un formulario de esquema de metadatos, siga estos pasos:

1. Para agregar una plantilla personalizada a la lista, haz clic en **[!UICONTROL Crear]** desde la barra de herramientas.

   >[!NOTE]
   >
   >Se muestra un símbolo de bloqueo con las plantillas sin editar. Si personaliza una plantilla, no estará bloqueada ![bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg).

1. En el cuadro de diálogo, proporcione el título del formulario de esquema y haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

## Editar formularios de esquema de metadatos {#edit-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos recién agregado o existente. El formulario de esquema de metadatos incluye pestañas y elementos de formulario en pestañas. Puede asignar o configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar pestañas o elementos de formulario al formulario de esquema de metadatos. Las pestañas y los elementos de formulario derivados del elemento principal están en estado bloqueado. No se pueden modificar en el nivel secundario.

1. En la página [!UICONTROL Forms de esquema de metadatos], seleccione un formulario y haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

1. En la página **[!UICONTROL Editor de formularios de esquemas de metadatos]**, personalice el formulario de metadatos. Arrastre los componentes necesarios desde la ficha **[!UICONTROL Generar formulario]** hasta una de las fichas.

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]**.

### Componentes dentro de la ficha [!UICONTROL Generar formulario] {#components-within-the-build-form-tab}

La pestaña **[!UICONTROL Generar formulario]** enumera los elementos de formulario que usa en el formulario de esquema. La ficha **[!UICONTROL Configuración]** proporciona los atributos de cada elemento que selecciona en la ficha **[!UICONTROL Generar formulario]**. En la tabla siguiente se enumeran los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]**:

| Nombre del componente | Descripción |
|----|----|
| **[!UICONTROL Encabezado de sección]** | Añada un encabezado de sección para una lista de componentes comunes. |
| **[!UICONTROL Texto de una sola línea]** | Agregue una propiedad de texto de una sola línea. Se almacena como una cadena. |
| **[!UICONTROL Texto con varios valores]** | Agregue una propiedad de texto de varios valores. Se almacena como una matriz de cadenas. |
| **[!UICONTROL Número]** | Añada un componente de número. |
| **[!UICONTROL Fecha]** | Añada un componente de fecha. |
| **[!UICONTROL Menú Desplegable]** | Añada una lista desplegable. |
| **[!UICONTROL Etiquetas estándar]** | Añada una etiqueta. Es posible que los administradores tengan que cambiar el valor de ruta. Por ejemplo, `/etc/tags/mac/<tenant_id>/<custom_tag_namespace>`, si publican el formulario de esquema de metadatos desde Experience Manager Assets, donde la ruta no incluye información de inquilino, por ejemplo, `/etc/tags/<custom_tag_namespace>`. |
| **[!UICONTROL Etiquetas inteligentes]** | Etiquetas detectadas automáticamente si ha adquirido y configurado el complemento Experience Manager Assets smart tags. |
| **[!UICONTROL Campo oculto]** | Agregue un campo oculto. Se envía como parámetro POST cuando se guarda el recurso. |
| **[!UICONTROL Recurso Referido Por]** | Agregue este componente para ver una lista de los recursos a los que hace referencia el recurso. |
| **[!UICONTROL Referencia de recurso]** | Agregar para mostrar una lista de recursos que hacen referencia al recurso. |
| **[!UICONTROL Metadatos contextuales]** | Agregue para controlar la visualización de otras pestañas de metadatos en la página Propiedades de los recursos. |

<!--| **[!UICONTROL Asset Rating]** |  Average rating of an asset added from Experience Manager Assets before it is published to Brand Portal. |-->

#### Editar el componente de metadatos {#edit-the-metadata-component}

Para editar las propiedades de un componente de metadatos en el formulario, haga clic en el componente para editar todas o un subconjunto de las siguientes propiedades en la pestaña **[!UICONTROL Configuración]**. Se recomienda asignar solo un campo a una propiedad determinada en el esquema de metadatos. De lo contrario, el sistema selecciona el último campo añadido asignado a la propiedad.

**Etiqueta de campo**: nombre de la propiedad de metadatos que se muestra en la página de propiedades del recurso.

**Asignar a propiedad**: esta propiedad especifica la ruta relativa o el nombre del nodo del recurso donde se guarda en el repositorio de CRX. Comienza por `./` para indicar que la ruta se encuentra bajo el nodo del recurso.

Los siguientes son ejemplos de valores válidos para una propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos del recurso como propiedad `dc:title`.

* `./jcr:created`: almacena la fecha y hora de creación de un recurso. Es una propiedad protegida. Si configura estas propiedades, Adobe recomienda marcarlas como Deshabilitar edición. De lo contrario, se produce el fallo “Error al modificar los recursos” al guardar las propiedades del recurso.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, la ruta de la propiedad no debe incluir espacios.

* **Marcador de posición**: utilice esta propiedad para especificar el texto de marcador de posición relevante con respecto a la propiedad de metadatos.
* **Requerido**: utilice esta propiedad para marcar una propiedad de metadatos como obligatoria en la página de propiedades.
* **Deshabilitar edición**: utilice esta propiedad para no permitir ninguna edición en una propiedad de la página de propiedades.
* **Mostrar campo vacío en solo lectura**: marque esta propiedad para mostrar una propiedad de metadatos en la página de propiedades aunque no tenga valor. De forma predeterminada, cuando una propiedad de metadatos no tiene valor, no se muestra en la página de propiedades.
* **Mostrar lista ordenada**: utilice esta propiedad para mostrar una lista ordenada de opciones.
* **Opciones**: utilice esta propiedad para especificar opciones en una lista.
* **Descripción**: utilice esta propiedad para agregar una descripción breve para el componente de metadatos.
* **Clase**: clase de objeto a la que está asociada la propiedad.
* **Eliminar**: haga clic en [!UICONTROL Eliminar] para eliminar un componente del formulario de esquema.

>[!NOTE]
>
>El componente [!UICONTROL Campo oculto] no incluye estos atributos. En su lugar, incluye propiedades como los atributos Nombre, Valor, Etiqueta de campo y Descripción. Los valores del componente Campo oculto se envían como parámetro POST cada vez que se guarda el recurso. No se puede guardar como metadatos para el recurso.

Si selecciona la opción **[!UICONTROL Obligatorio]**, puede buscar recursos que no tengan metadatos obligatorios. En el panel **[!UICONTROL Filtros]**, expanda el predicado **[!UICONTROL Validación de metadatos]** y seleccione la opción **[!UICONTROL No válido]**. Los resultados de la búsqueda muestran los recursos que carecen de metadatos obligatorios configurados a través del formulario de esquema.

![Opción seleccionada en el predicado de validación de metadatos del panel Filtros](assets/invalid-metadata-predicate.png)

Si agrega el componente Metadatos contextuales a cualquier pestaña de cualquier formulario de esquema, el componente aparece como una lista en la página de propiedades de los recursos a los que se aplica el esquema en particular. La lista incluye todas las demás pestañas, excepto la pestaña a la que se aplicó el componente Metadatos contextuales. Actualmente, esta función proporciona funcionalidad básica para controlar la visualización de metadatos en función del contexto.

![El componente de metadatos contextuales enumera fichas de propiedades de recursos](assets/metadata-contextual-component-list.png)

Para mostrar cualquier pestaña en la página de propiedades además de la pestaña donde se aplica el componente Metadatos contextuales, seleccione la pestaña en la lista. La pestaña se añade a la página de propiedades.

![La ficha seleccionada en la lista de metadatos contextuales se muestra en la página de propiedades de recursos](assets/contextual-metadata-asset-properties.png)

*Figura: Metadatos contextuales en la página de propiedades del recurso.*

### Especificar propiedades en el archivo JSON {#specify-properties-in-json-file}

En lugar de especificar propiedades para las opciones de la pestaña **[!UICONTROL Configuración]**, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Ruta de JSON]**.

#### Agregar o eliminar una pestaña en el formulario de esquema {#adding-deleting-a-tab-in-the-schema-form}

El editor de esquemas permite agregar o eliminar una pestaña. El formulario de esquema predeterminado incluye las fichas **[!UICONTROL Básico]**, **[!UICONTROL Avanzado]**, **[!UICONTROL IPTC]** y **[!UICONTROL Extensión de IPTC]**.

Haga clic en `+` para agregar una ficha en un formulario de esquema. De manera predeterminada, la nueva ficha tiene el nombre `Unnamed-1`. Puede modificar el nombre desde la ficha **[!UICONTROL Configuración]**. Haga clic en `X` para eliminar una ficha.

![Agregar o eliminar una ficha mediante el Editor de esquemas de metadatos](assets/metadata-schema-form-new-tab.png)

## Metadatos en cascada {#cascading-metadata}

Al capturar la información de metadatos de un recurso, los usuarios proporcionan información en los distintos campos disponibles. Puede mostrar campos de metadatos específicos o valores de campo que dependan de las opciones seleccionadas en los demás campos. Esta visualización condicional de metadatos se denomina metadatos en cascada. En otras palabras, puede crear una dependencia entre un campo o valor de metadatos determinado y uno o varios campos o sus valores.

Utilice esquemas de metadatos para definir reglas para mostrar metadatos en cascada. Por ejemplo, si el esquema de metadatos incluye un campo de tipo de recurso, puede definir un conjunto pertinente de campos que se mostrarán en función del tipo de recurso que seleccione un usuario.

>[!CAUTION]
>
>No se admiten metadatos en cascada para fragmentos de contenido.

Estos son algunos casos de uso para los que puede definir metadatos en cascada:

* Cuando se requiera la ubicación del usuario, se mostrarán los nombres de ciudades relevantes según el país y el estado que haya elegido el usuario.
* Cargue los nombres de marcas relevantes en una lista basada en la categoría de producto que haya elegido el usuario.
* Alterne la visibilidad de un campo concreto en función del valor especificado en otro campo. Por ejemplo, mostrar campos de dirección de envío independientes si el usuario desea que el envío se envíe en una dirección diferente.
* Designe un campo como obligatorio en función del valor especificado en otro campo.
* Cambie las opciones mostradas para un campo en particular en función del valor especificado en otro campo.
* Establezca el valor de metadatos predeterminado en un campo concreto en función del valor especificado en otro campo.

### Configurar metadatos en cascada en [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Imagine un escenario en el que desee mostrar metadatos en cascada en función del tipo de recurso seleccionado. Algunos ejemplos

* Para un vídeo, mostrar campos aplicables como formato, códec, duración, etc.
* Para un documento de Word o PDF, muestre campos como, por ejemplo, recuento de páginas, autor, etc.

Independientemente del tipo de recurso elegido, muestre la información de copyright como un campo obligatorio.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. En la página **[!UICONTROL Esquema Forms]**, seleccione un formulario de esquema y haga clic en **[!UICONTROL Editar]** en la barra de herramientas para editar el esquema.

   ![select_form](assets/select_form.png)

1. (Opcional) En el editor de esquemas de metadatos, cree un campo para condicionalizar. Especifique un nombre y una ruta de acceso de propiedad en la ficha **[!UICONTROL Configuración]**.

   Para crear una ficha, haga clic en `+` para agregar una ficha y luego agregue un campo de metadatos.

   ![add_tab](assets/add_tab.png)

1. Agregue un campo desplegable para el tipo de recurso. Especifique un nombre y una ruta de acceso de propiedad en la ficha **[!UICONTROL Configuración]**. Añada una descripción opcional.

   ![campo_tipo_recurso](assets/asset_type_field.png)

1. Los pares clave-valor son las opciones proporcionadas para un usuario de formulario. Puede proporcionar los pares clave-valor manualmente o desde un archivo JSON.

   * Para especificar los valores manualmente, seleccione **[!UICONTROL Agregar manualmente]**, haga clic en **[!UICONTROL Agregar opción]** y especifique el texto y el valor de la opción. Por ejemplo, especifique los tipos de recursos de vídeo, PDF, Word e Imagen.

   * Para recuperar los valores de un archivo JSON de forma dinámica, seleccione **[!UICONTROL Agregar mediante la ruta de acceso JSON]** y proporcione la ruta de acceso del archivo JSON. [!DNL Experience Manager] recupera los pares clave-valor en tiempo real cuando se presenta el formulario al usuario.

   Ambas opciones son mutuamente excluyentes. No puede importar las opciones de un archivo JSON y editarlas manualmente.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Cuando se agrega un archivo JSON, los pares clave-valor no se muestran en el editor de esquemas de metadatos, pero están disponibles en el formulario publicado.

   >[!NOTE]
   >
   >Al añadir opciones, si hace clic en el campo desplegable, la interfaz se distorsiona y la opción de eliminación de las opciones deja de funcionar. No haga clic en la lista desplegable hasta que guarde los cambios. Si tiene este problema, guarde el esquema y ábralo de nuevo para seguir editando.

1. (Opcional) Añada los demás campos obligatorios. Por ejemplo, formato, códec y duración para el vídeo de tipo de recurso.

   Del mismo modo, agregue campos dependientes para otros tipos de recursos. Por ejemplo, agregue campos, recuento de páginas y autor para los recursos del documento, como archivos de PDF y Word.

   ![campos_dependientes_de_vídeo](assets/video_dependent_fields.png)

1. Para crear una dependencia entre el campo de tipo de recurso y otros campos, elija el campo dependiente y abra la pestaña **[!UICONTROL Reglas]**.

   ![select_depenentfield](assets/select_dependentfield.png)

1. En **[!UICONTROL Requisito]**, elija la opción **[!UICONTROL Requerido, según la nueva regla]**.
1. Haga clic en **[!UICONTROL Agregar regla]** y elija el campo **[!UICONTROL Tipo de recurso]** para crear una dependencia. También elija el valor del campo en el que desea crear la dependencia. En este caso, seleccione **[!UICONTROL Vídeo]**. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >Con las reglas se pueden utilizar listas desplegables con valores predefinidos manualmente. Los menús desplegables con la ruta JSON configurada no se pueden utilizar con reglas que utilicen valores predefinidos para aplicar condiciones. Si los valores se cargan desde JSON en tiempo de ejecución, no es posible aplicar una regla predefinida.

1. En **[!UICONTROL Visibilidad]**, seleccione la opción **[!UICONTROL Visible, según la nueva regla]**.

1. Haga clic en **[!UICONTROL Agregar regla]** y elija el campo **[!UICONTROL Tipo de recurso]** para crear una dependencia. También elija el valor del campo en el que desea crear la dependencia. En este caso, seleccione **[!UICONTROL Vídeo]**. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Al hacer clic en un espacio en blanco (o en cualquier lugar que no sean los valores), se restablecen los valores. Si esto sucede, vuelva a seleccionar los valores.

   >[!NOTE]
   >
   >Puede aplicar condiciones de **[!UICONTROL requisito]** y **[!UICONTROL visibilidad]** independientes entre sí.

1. Del mismo modo, cree una dependencia entre el valor Vídeo en el campo Tipo de recurso y otros campos, como Códec y Duración.
1. Repita los pasos para crear dependencia entre los recursos de documento (PDF y Word) en el campo [!UICONTROL Tipo de recurso] y campos como [!UICONTROL Recuento de páginas] y [!UICONTROL Autor].
1. Haga clic en **[!UICONTROL Guardar]**. Aplicar el esquema de metadatos a una carpeta.

1. Vaya a la carpeta en la que aplicó el esquema de metadatos y abra la página de propiedades de un recurso. Según su elección en el campo Tipo de recurso, se muestran los campos de metadatos en cascada correspondientes.

   ![Metadatos en cascada para el recurso de vídeo](assets/video_asset.png)

   *Figura: Metadatos en cascada de un vídeo.*

   ![Metadatos en cascada para el recurso de documento](assets/doc_type_fields.png)

   *Figura: Metadatos en cascada para un documento.*

## Eliminar formularios de esquema de metadatos {#delete-metadata-schema-forms}

[!DNL Experience Manager] solo permite eliminar formularios de esquema personalizados. No permite eliminar los formularios o las plantillas de esquema predeterminados. Sin embargo, puede eliminar cualquier cambio personalizado en estos formularios.

Para eliminar un formulario, seleccione un formulario y haga clic en Eliminar.

>[!NOTE]
>
>* Después de eliminar los cambios personalizados de un formulario predeterminado, el bloqueo ![bloqueo cerrado](assets/do-not-localize/lock_closed_icon.svg) vuelve a aparecer antes del formulario. Indica que el formulario se revierte a su estado predeterminado.
>* No puede eliminar los formularios de esquema de metadatos predeterminados en [!DNL Assets].

## Formularios de esquema para tipos MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] proporciona formularios predeterminados para varios tipos MIME de forma predeterminada. Sin embargo, puede agregar formularios personalizados para recursos de varios tipos MIME.

### Adición de nuevos formularios para tipos MIME {#add-new-forms-for-mime-types}

Cree un formulario bajo el tipo de formulario correspondiente. Por ejemplo, para agregar una plantilla para el subtipo `image/png`, cree el formulario en los formularios de &quot;imagen&quot;. El título del formulario de esquema es el nombre del subtipo. En este caso, el título es `png`.

#### Usar una plantilla de esquema existente para varios tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Puede utilizar una plantilla existente para un tipo MIME diferente. Por ejemplo, use el formulario `image/jpeg` para los recursos de tipo MIME `image/png`.

En este caso, cree un nodo en `/etc/dam/metadataeditor/mimetypemappings` en el repositorio de CRX. Especifique un nombre para el nodo y defina las siguientes propiedades:

| Nombre | Descripción | Tipo | Valor  |
|------|-------------|------|-------|
| `exposedmimetype` | Nombre del formulario existente que se debe asignar | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que utilizan el formulario definido en el atributo `exposedmimetype` | `String` | `image/png` |

[!DNL Assets] asigna los siguientes tipos MIME y formularios de esquema:

| Formulario de esquema | Tipos MIME |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Concesión de acceso a esquemas de metadatos {#grant-access-to-metadata-schemas}

La función Esquema de metadatos solo está disponible para administradores. Sin embargo, los administradores pueden proporcionar acceso a los usuarios que no son administradores modificando algunos permisos. Proporcione a los usuarios que no son administradores permisos para crear, modificar y eliminar en la carpeta `/conf`.

## Aplicar metadatos específicos de carpeta {#apply-folder-specific-metadata}

[!DNL Assets] le permite definir una variante de un esquema de metadatos y aplicarla a una carpeta específica.

Por ejemplo, puede definir una variante del esquema de metadatos predeterminado y aplicarla a una carpeta. Al aplicar el esquema modificado, se anula el esquema de metadatos predeterminado original que se aplica a los recursos de la carpeta.

Solo los recursos cargados en la carpeta a la que se aplica este esquema se ajustan a los metadatos modificados definidos en el esquema de metadatos de variante. [!DNL Assets] en otras carpetas donde se aplica el esquema original siguen ajustándose a los metadatos definidos en el esquema original.

La herencia de metadatos por recursos se basa en el esquema aplicado a la carpeta de nivel superior en la jerarquía. Las subcarpetas aplican o heredan el mismo esquema. Si se aplica un esquema diferente en el nivel de subcarpeta, se detiene la herencia.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Seleccione la casilla de verificación que hay antes de un formulario, por ejemplo, el formulario de metadatos predeterminado, haga clic en **[!UICONTROL Copiar]** y guárdelo como un formulario personalizado. Especifique un nombre personalizado para el formulario, por ejemplo, `my_default`. También puede crear un formulario personalizado.

1. En la página **[!UICONTROL Forms de esquema de metadatos]**, seleccione el formulario `my_default` y, a continuación, haga clic en **[!UICONTROL Editar]**.

1. En la página **[!UICONTROL Editor de esquemas de metadatos]**, agregue un campo de texto al formulario de esquema. Por ejemplo, agregue un campo con la etiqueta **[!UICONTROL Categoría]**.

   ![Campo de texto agregado al Editor de formularios de esquemas de metadatos](assets/text-field-metadata-schema-editor.png)

   *Figura: Campo de texto agregado al editor de formularios de esquema de metadatos.*

1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado aparece en la página **[!UICONTROL Forms de esquema de metadatos]**.
1. Haga clic en **[!UICONTROL Aplicar a las carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.

1. Seleccione la carpeta en la que desea aplicar el esquema modificado y, a continuación, haga clic en **[!UICONTROL Aplicar]**.

   ![Seleccionar carpeta para aplicar el esquema de metadatos](assets/metadata-schema-select-folder.png)

1. Si la carpeta tiene aplicado el otro esquema de metadatos, aparece un mensaje que advierte de que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **Sobrescribir**.
1. Haga clic en **Aceptar** para cerrar el mensaje de éxito.
1. Navegue hasta la carpeta a la que aplicó el esquema de metadatos modificado.

## Definir metadatos obligatorios {#define-mandatory-metadata}

Puede definir campos obligatorios en el nivel de carpeta, que se aplican a los recursos cargados en la carpeta. Si carga recursos a los que les faltan metadatos para los campos obligatorios definidos anteriormente, aparecerá una indicación visual de que faltan metadatos en los recursos en la vista de tarjeta.

>[!NOTE]
>
>Un campo de metadatos se puede definir como obligatorio en función del valor de otro campo. En la vista de tarjeta, [!DNL Experience Manager] no muestra el mensaje de advertencia sobre la falta de metadatos para estos campos de metadatos obligatorios.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Guarde el formulario de metadatos predeterminado como un formulario personalizado. Por ejemplo, guárdelo como `my_default`.

1. Edite el formulario personalizado. Añada un campo obligatorio. Por ejemplo, agregue un campo **[!UICONTROL Category]** y haga que el campo sea obligatorio.

   ![Agregue un campo obligatorio al formulario de metadatos seleccionando Requerido en la pestaña Reglas del Editor de formularios de esquemas de metadatos](assets/mandatory-field-metadata-schema-editor.png)

   *Figura: Campo obligatorio en el editor de formularios de esquema de metadatos.*

1. Haga clic en **[!UICONTROL Guardar]**. El formulario modificado aparece en la página **[!UICONTROL Forms de esquema de metadatos]**. Seleccione el formulario y haga clic en **[!UICONTROL Aplicar a las carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.

1. Vaya a la carpeta y cargue algunos recursos a los que les faltan metadatos para el campo obligatorio agregado al formulario personalizado. Se muestra un mensaje para los metadatos que faltan para el campo obligatorio en la vista de tarjeta del recurso.

   ![Mensaje para los metadatos obligatorios que faltan en la vista de tarjetas de recursos al cargar recursos en la carpeta](assets/metadata-missing-info-card-view.png)

1. (Opcional) Acceso a `https://[aem_server]:[port]/system/console/components/`. Configure y habilite el componente `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` que está deshabilitado de manera predeterminada. Establezca una frecuencia con la cual [!DNL Experience Manager] compruebe la validez de los metadatos de los recursos. Esta configuración agrega una propiedad `hasValidMetadata` a `jcr:content` de recursos. [!DNL Experience Manager] utiliza esta propiedad para filtrar los recursos no válidos en un resultado de búsqueda. Si agrega un recurso después de una comprobación, este no se marcará con `hasValidMetadata` hasta la siguiente comprobación programada. Por lo tanto, los recursos no aparecen en los filtros de búsqueda para metadatos no válidos hasta después de la siguiente comprobación programada.

   >[!CAUTION]
   >
   >Las comprobaciones de validación de metadatos consumen muchos recursos y pueden afectar al rendimiento del sistema. Programe las comprobaciones según corresponda. Si el servidor no puede soportar la carga, intente deshabilitar este trabajo.

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
