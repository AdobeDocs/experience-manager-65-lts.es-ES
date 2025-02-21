---
title: Crear y configurar páginas del Editor de recursos
description: Obtenga información sobre cómo crear páginas personalizadas del editor de recursos y editar varios recursos simultáneamente.
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 1%

---

# Crear y configurar páginas del Editor de recursos {#creating-and-configuring-asset-editor-pages}

Este documento describe lo siguiente:

* Por qué crear páginas personalizadas del editor de recursos.
* Crear y personalizar páginas del Editor de recursos, que son páginas de WCM que permiten ver y editar metadatos y realizar acciones en el recurso.
* Cómo editar varios recursos simultáneamente.

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>El uso compartido de recursos está disponible como implementación de referencia de código abierto. Consulte [Uso compartido de recursos Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). No es compatible oficialmente.

## ¿Por qué crear y configurar páginas del Editor de recursos? {#why-create-and-configure-asset-editor-pages}

La administración de activos digitales se utiliza en más escenarios. Al pasar de una solución a pequeña escala para un pequeño grupo de usuarios formados profesionalmente (por ejemplo, fotógrafos o taxónomos) a grupos de usuarios más grandes y diversos (por ejemplo, usuarios empresariales, autores de WCM y periodistas), la potente interfaz de usuario de [!DNL Adobe Experience Manager Assets] puede proporcionar demasiada información. Las partes interesadas empiezan a solicitar interfaces de usuario o aplicaciones específicas para acceder a los recursos digitales que les interesan.

Estas aplicaciones centradas en recursos pueden ser simples galerías de fotos en una intranet donde los empleados pueden cargar fotos de las visitas a ferias comerciales o de un centro de prensa en un sitio web público. Las aplicaciones centradas en recursos también se pueden ampliar a soluciones completas, incluidos carros de compras, cierres de compra y procesos de verificación.

La creación de una aplicación centrada en recursos se convierte en un proceso de configuración que no requiere codificación, solo conocimiento de los grupos de usuarios y sus necesidades, y conocimiento de los metadatos que se utilizan. Las aplicaciones centradas en recursos creadas con [!DNL Assets] son extensibles: con un esfuerzo de codificación moderado, se pueden crear componentes reutilizables para buscar, ver y modificar recursos.

Una aplicación centrada en recursos de [!DNL Experience Manager] consta de una página Editor de recursos, que se puede utilizar para obtener una vista detallada de un recurso específico. Una página del Editor de recursos también permite editar metadatos, siempre que el usuario que acceda al recurso tenga los permisos necesarios.

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create an Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create an Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create an asset share page by way of the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes several predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example, cq:tags) and a content tree to populate the options from (for example, the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, for example, tiff:ImageLength and the user can then enter a value, for example, 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## Crear y configurar una página del Editor de recursos {#creating-and-configuring-an-asset-editor-page}

Puede personalizar el Editor de recursos para determinar cómo pueden ver y editar los recursos digitales los usuarios. Para ello, cree una página del Editor de recursos y, a continuación, personalice las vistas y las acciones que los usuarios pueden realizar en esa página.

>[!NOTE]
>
>Si desea agregar campos personalizados al editor de recursos DAM, agregue nuevos nodos `cq:Widget` a `/apps/dam/content/asseteditors.`

### Crear una página del editor de recursos {#creating-the-asset-editor-page}

Al crear la página del Editor de recursos, se recomienda crear la página directamente debajo de la página Uso compartido de recursos.

Para crear una página del editor de recursos:

1. En la ficha **[!UICONTROL Sitios web]**, vaya al lugar donde desea crear una página del Editor de recursos y haga clic en **Nuevo**.
1. Seleccione **Geometrixx Asset Editor** y haga clic en **Crear**. La nueva página se creará y aparecerá en la ficha **Sitios web**.

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

La página básica creada con la plantilla del Editor de recursos de Geometrixx tiene el siguiente aspecto:

![recurso compartido5](assets/assetshare5.png)

Para personalizar la página del Editor de recursos, utilice los elementos de la barra de tareas. La página del editor de recursos a la que se tiene acceso desde el **Centro de prensa de Geometrixx** es una versión personalizada de una página basada en esta plantilla:

![recurso compartido6](assets/assetshare6.png)

#### Configurar un editor de recursos para que se abra desde una página de uso compartido de recursos {#setting-which-asset-editor-opens-from-an-asset-share-page}

Después de crear la página del editor de recursos personalizado, asegúrese de que al hacer doble clic en los recursos que ha creado con el uso compartido de recursos personalizado, se abran los recursos en la página del editor personalizado.

Para establecer la página Editor de recursos:

1. En la página Uso compartido de recursos, haga clic en **Editar** junto al Generador de consultas.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. Haga clic en la ficha **General** si aún no está seleccionada.

1. En el campo **Ruta del editor de recursos**, escriba la ruta del editor de recursos en el que desea que se abra la página Uso compartido de recursos y haga clic en **Aceptar**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### Añadir componentes del Editor de recursos {#adding-asset-editor-components}

Para determinar la funcionalidad que tiene un editor de recursos, agregue componentes a la página.

Para agregar componentes del Editor de recursos:

1. En la página Editor de recursos que desee personalizar, seleccione **Editor de recursos** en la barra de tareas. Se muestran todos los componentes disponibles del Editor de recursos.

>[!NOTE]
>
>Lo que se puede personalizar depende de los componentes disponibles. Para activar los componentes, vaya al modo Diseño y seleccione los componentes que necesita activar.

1. Arrastre los componentes de la barra de tareas al Editor de recursos y realice los cambios necesarios en los cuadros de diálogo de componentes. Los componentes se describen en la tabla siguiente y en las instrucciones detalladas que siguen.

>[!NOTE]
>
>Al diseñar la página del Editor de recursos, se crean componentes de solo lectura o editables. Los usuarios saben que un campo se puede editar si aparece una imagen de un lápiz en ese componente. De forma predeterminada, la mayoría de los componentes están configurados como de solo lectura.

| Componente | Descripción |
|---|---|
| **[!UICONTROL Formulario de metadatos] y [!UICONTROL Campo de texto de metadatos]** | Permite agregar metadatos adicionales a un recurso y realizar una acción, como enviar, en ese recurso. |
| **[!UICONTROL Sub Assets]** | Permite personalizar los subrecursos. |
| **Etiquetas** | Permite que los usuarios seleccionen y agreguen etiquetas a un recurso. |
| **[!UICONTROL Miniatura]** | Muestra una miniatura del recurso, su nombre de archivo y permite agregar un texto alternativo. Aquí también puede agregar acciones del Editor de recursos. |
| **[!UICONTROL Título]** | Muestra el título del recurso, que se puede personalizar. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### Formulario de metadatos y campo de texto: configuración del componente Ver metadatos {#metadata-form-and-text-field-configuring-the-view-metadata-component}

El formulario de metadatos es un formulario que incluye una acción de inicio y otra de finalización. En el medio, se introducen **campos de texto**. Consulte [Forms](/help/sites-authoring/default-components-foundation.md#form-component) para obtener más información sobre cómo trabajar con formularios.

1. Para crear una acción de inicio, haga clic en **Editar** en el área de Inicio del formulario. Si lo desea, puede introducir un título de cuadro. De manera predeterminada, el título del cuadro es **Metadatos**. Active la casilla de verificación Validación del cliente si desea que se genere el código de cliente de JavaScript para la validación.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. Para crear una acción Fin, haga clic en **Editar** en el área Fin del formulario. Por ejemplo, es posible que desee crear una opción **[!UICONTROL Enviar]** para permitir que los usuarios envíen sus cambios de metadatos. Opcionalmente, puede agregar una opción **Reset** que restablezca los metadatos a su estado original.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. Entre **Inicio del formulario** y **Fin del formulario**, arrastre los campos de texto de metadatos al formulario. Los usuarios rellenan los metadatos en estos campos de texto, sobre los que pueden enviar o completar otra acción.

1. Haga doble clic en el nombre de campo, por ejemplo, **Título** para abrir el campo de metadatos y realizar cambios. En la ficha **General** de la ventana **Editar componente**, defina el área de nombres y la etiqueta de campo y el tipo, por ejemplo, `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

Consulte [Personalización y ampliación de Assets](/help/assets/extending-assets.md) para obtener información sobre cómo modificar los espacios de nombres disponibles en el formulario de metadatos.

1. Haga clic en la ficha **Restricciones**. Aquí puede seleccionar si un campo es obligatorio y, si es necesario, añadir restricciones.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Haga clic en la ficha **Mostrar**. Aquí puede introducir una nueva anchura y número de filas para el campo de metadatos. Seleccione la casilla de verificación **El campo es de solo lectura** para permitir que los usuarios editen los metadatos.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

A continuación se muestra un ejemplo de un formulario de metadatos con varios campos:

![metadatos](assets/chlimage_1-390.png)

En la página Editor de recursos, los usuarios pueden introducir valores en los campos de metadatos (si se pueden editar) y realizar la acción final (por ejemplo, enviar los cambios).

#### Recursos secundarios {#sub-assets}

El componente Sub Assets es donde puede ver y seleccionar recursos secundarios. Puede determinar qué nombres aparecen bajo los recursos principales [y secundarios](/help/assets/assets.md#what-are-digital-assets).

Haga doble clic en el componente Sub Assets para poder abrir el cuadro de diálogo de subrecursos, donde puede cambiar los títulos del recurso principal y de los subrecursos. Los valores predeterminados aparecen debajo del campo correspondiente.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

El siguiente es un ejemplo de un componente Sub Assets rellenado:

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

Por ejemplo, si selecciona un subrecurso, observe cómo el componente muestra la página adecuada y el título del cuadro cambia de Subrecurso Assets a Hermanos.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### Etiquetas {#tags}

El componente Etiquetas es un componente en el que los usuarios pueden asignar etiquetas existentes a un recurso, lo que le ayudará posteriormente en la organización y recuperación. Puede hacer que este componente sea de solo lectura, de modo que los usuarios no puedan agregar etiquetas, sino solo verlas.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

Haga doble clic en el componente Etiquetas para poder abrir el cuadro de diálogo de etiquetas, donde puede cambiar el título de Etiquetas, si lo desea, y donde puede seleccionar las áreas de nombres asignadas. Para que este campo sea editable, desactive la casilla de verificación **[!UICONTROL Ocultar edición]**. De forma predeterminada, las etiquetas son editables.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

Si los usuarios pueden editar etiquetas, pueden hacer clic en el lápiz para añadirlas seleccionándolas en el menú desplegable Etiquetas.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

El siguiente es un componente Etiquetas rellenado:

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### Miniatura    {#thumbnail}

El componente Miniatura es el lugar donde el recurso muestra la miniatura seleccionada (para muchos de los formatos, la miniatura se extrae automáticamente). Además, el componente muestra el nombre de archivo y [acciones que puede modificar](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

Haga doble clic en el componente de miniatura para poder abrir el cuadro de diálogo de miniaturas, donde podrá cambiar el texto alternativo. De manera predeterminada, el texto alternativo de la miniatura es **Haga clic para descargar** recurso.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

A continuación se muestra un ejemplo de un componente de miniatura rellenado:

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### Título {#title}

El componente Título muestra el título del recurso y una descripción.

De forma predeterminada, está en modo de solo lectura, por lo que los usuarios no pueden editarlo. Para poder editarlo, haga doble clic en el componente y desactive la casilla de verificación **Ocultar botón de edición**. Además, introduzca un título para varios recursos.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

Si el Título se puede editar, puede agregar un título y una descripción haciendo clic en el Lápiz para abrir la ventana **Propiedades del recurso**. Además, puede activar y desactivar el recurso seleccionando la fecha y la hora.

Al editar el [!UICONTROL Título], los usuarios pueden cambiar el **Título**, la **Descripción** e introducir **Tiempo de activación** y **desactivación** para activar y desactivar el recurso.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

A continuación se muestra un ejemplo de un componente Título rellenado:

![chlimage_1-164](assets/chlimage_1-392.png)

#### Agregar acciones del editor de recursos {#adding-asset-editor-actions}

Puede determinar qué acciones pueden realizar los usuarios en los recursos digitales seleccionados a partir de una selección de acciones predefinidas.

Para agregar acciones a la página Editor de recursos:

1. En la página Editor de recursos que desee personalizar, haga clic en **Editor de recursos** en la barra de tareas.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

Estas son las acciones disponibles:

| Acción | Descripción |
|---|---|
| [!UICONTROL Descargar] | Permite a los usuarios descargar los recursos seleccionados en sus equipos. |
| [!UICONTROL Editores] | Permite a los usuarios editar una imagen (edición interactiva) |
| [!UICONTROL Lightbox] | Guarda los recursos en una &quot;light box&quot; en la que puede realizar otras acciones. Esto resulta útil cuando se trabaja con recursos en varias páginas. |
| [!UICONTROL Bloqueo] | Permite que los usuarios bloqueen un recurso. Esta funcionalidad no está habilitada de forma predeterminada y debe habilitarse en la lista de componentes. |
| [!UICONTROL Referencias] | Haga clic aquí para mostrar en qué páginas se está utilizando el recurso. |
| [!UICONTROL Creación de versiones] | Permite crear y restaurar versiones de un recurso. |

1. Arrastre la acción correspondiente al área **Acciones** de la página. Crea una opción que se utiliza para ejecutar la acción que se arrastra a la página.

![chlimage_1-165](assets/chlimage_1-393.png)

## Recursos de edición múltiple con la página Editor de recursos {#multi-editing-assets-with-the-asset-editor-page}

Con [!DNL Experience Manager Assets], puede cambiar varios recursos a la vez. Después de seleccionar los recursos, puede cambiar simultáneamente las etiquetas y los metadatos.

Para realizar varias ediciones de recursos con la página Editor de recursos:

1. Abra la página del **Centro de prensa** de Geometrixx:
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. Seleccione los recursos:

   * en Windows: `Ctrl + click` cada recurso.
   * en Mac: `Cmd + click` cada recurso.

   Para seleccionar un rango de recursos: haga clic en el primer recurso y, a continuación, `Shift + click` en el último.

1. Haga clic en **Editar metadatos** en el campo **Acciones** (parte izquierda de la página).
1. La página de Geometrixx **Editor de recursos del centro de prensa** se abre en una nueva pestaña. Los metadatos de los recursos se muestran de la siguiente manera:

   * Las etiquetas que no se apliquen a todos los recursos, sino solo a algunos, se muestran en cursiva.
   * Se muestra una etiqueta que se aplica a todos los recursos con una fuente normal.
   * Metadatos distintos de etiquetas: el valor del campo solo se muestra si es el mismo para todos los recursos seleccionados.

1. Haga clic en **Descargar** para descargar un archivo ZIP con las representaciones originales de los recursos.
1. Haga clic en editar la opción de etiquetas que está al lado del campo **Etiquetas**.

   * Una etiqueta de que no se aplica a todos los recursos, pero solo a algunos tiene un fondo gris.
   * Una etiqueta de que se aplica a todos los recursos tiene un fondo blanco.

   Puede hacer lo siguiente:

   * Haga clic en `x` para eliminar la etiqueta de todos los recursos.
   * Haga clic en `+` para agregar la etiqueta a todos los recursos.
   * Haga clic en la **flecha** y seleccione una etiqueta para agregar una etiqueta nueva a todos los recursos.

   Haga clic en **Aceptar** para escribir los cambios en el formulario. La casilla al lado del campo **Etiquetas** se marca automáticamente.

1. Edite el campo Description. Por ejemplo, configúrelo en:

   `This is a common description`

   Cuando se edita un campo, su valor sobrescribe los valores existentes de los recursos seleccionados cuando se envía el formulario.

   Nota: La casilla junto al campo se marca automáticamente cuando se edita el campo.

1. Haga clic en **Actualizar metadatos** para enviar el formulario y guardar los cambios de todos los recursos.

   Nota: sólo se modifican los metadatos marcados.
