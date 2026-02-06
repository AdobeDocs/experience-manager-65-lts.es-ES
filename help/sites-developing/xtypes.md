---
title: Usar xtypes (IU clásica)
description: Obtenga información acerca de todos los xtype disponibles con Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '3668'
ht-degree: 0%

---

# Usar xtypes (IU clásica){#using-xtypes-classic-ui}

Esta página describe todos los xtype disponibles con Adobe Experience Manager (AEM).

En el lenguaje ExtJS, un xtype es un nombre simbólico dado a una clase. Puede leer el párrafo &quot;Tipos XT de componentes&quot; de la [Descripción general de ExtJS 2](https://docs.sencha.com/) para obtener una explicación detallada sobre qué es un xtype y cómo se puede usar.

Para obtener más información sobre todos los widgets disponibles en AEM, consulte la [documentación de la API de widgets](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

Para saber en qué componentes se utiliza un xtype determinado en AEM, puede utilizar la siguiente consulta `Xpath` en CRXDE. Solo tiene que reemplazar &quot;casilla de verificación&quot; con el xtype que le interese:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Esta página describe el uso de xtype de ExtJS dentro de la IU clásica.
>
>Adobe recomienda usar la [interfaz de usuario táctil](/help/sites-developing/touch-ui-concepts.md) moderna y estándar basada en [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) y [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

A continuación se enumeran los xtype disponibles en Adobe Experience Manager:

* `annotation`

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Annotation` es una ventana especial. Tiene un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también puede mostrar solo información.

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Anteriormente conocido como `SimpleStore`.

  Una pequeña clase auxiliar para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s a partir de datos de la matriz. Un(a) `ArrayStore` se configura automáticamente con un(a) [CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor` se usa en el administrador de DAM.

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog` es un cuadro de diálogo que aparece en caso de que una página haga referencia a recursos o etiquetas.

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig` proporciona un panel para ver las Live Copies de un modelo y editar sus propiedades ( sincronizar déclencheur y acciones de sincronización ).

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus proporciona un panel para ver y editar un modelo y sus relaciones de Live Copies. La exploración se realiza mediante un [CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), una edición mediante un [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y un [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase base para cualquier [componente](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) cuyo tamaño debe ser una caja, con anchura y altura.

  BoxComponent proporciona ajustes automáticos del modelo de cuadro para el tamaño y la posición y funciona correctamente dentro del modelo de representación de componentes.

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El cuadro de diálogo Examinar permite al usuario examinar el repositorio para seleccionar una ruta. Se suele usar a través de [BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: use [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) en su lugar**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor` proporciona un motor de búsqueda y una cuadrícula para editar los resultados de búsqueda.

  `BulkEditor` debe insertarse en un formulario de HTML (requerido por la funcionalidad de importación). Esto funciona perfectamente con [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm proporciona [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) rodeado por un formulario de HTML. La versión independiente de [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Se requiere un formulario HTML para el botón Importar.

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase de botón simple

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenedor de un grupo de botones.

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El paquete CQ.Ext.chart proporciona la capacidad de visualizar datos con gráficos basados en Flash. Cada gráfico se vincula directamente a un CQ.Ext.data.Store, lo que permite realizar actualizaciones automáticas del gráfico. Para cambiar el aspecto de un gráfico, vea las opciones de configuración [chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de casilla de verificación único. Se puede utilizar como reemplazo directo de los campos de casilla de verificación tradicionales.

* `checkboxgroup`

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un contenedor de agrupación para los controles [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `clearcombo`

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ClearableComboBox es un cuadro combinado no editable con un déclencheur para borrar su valor.

* `colorfield`

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorField permite al usuario introducir un valor hexadecimal de color directamente o mediante [CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `colorlist`

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorList permite al usuario elegir un color de una lista editable.

* `colormenu`

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Menú que contiene un componente [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `colorpalette`

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase de paleta de colores sencilla para elegir colores. La paleta se puede representar en cualquier contenedor.

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un control combobox con compatibilidad para autocompletar, carga remota, paginación y muchas otras características.

  Un ComboBox funciona de manera similar a un campo &lt;select> tradicional de HTML. La diferencia es que para enviar [valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), debe especificar un [hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para crear una entrada oculta.

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase base para todos los componentes `Ext`. Todas las subclases de Component pueden participar en el ciclo de vida automatizado del componente `Ext` de creación, representación y destrucción que proporciona la clase [Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Los componentes se pueden agregar a un contenedor mediante la opción de configuración [items](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) en el momento en que se crea el contenedor.

* `componentextractor`

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ComponentExtractor permite al usuario extraer componentes de un sitio web o una página.

* `componentselector`

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una selección agrupada y ordenada de los componentes disponibles.

* `componentstyles`

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `compositefield`

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase base para campos de formulario complejos basados en panel que incluyen un campo de formulario o un grupo de campos de formulario.

* `container`

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase base para cualquier [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) que pueda contener otros componentes. Los contenedores administran el comportamiento básico de los elementos contenedores, a saber, agregar, insertar y quitar elementos.

  Las clases de contenedor más utilizadas son [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder es una [ventanilla](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) especializada de dos columnas que contiene el buscador de contenido real a la izquierda y el marco de contenido a la derecha.

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab es un panel especializado que proporciona las características utilizadas en los paneles de pestañas de [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Normalmente, incluye un formulario de búsqueda (el Cuadro de consulta) y una vista de datos para mostrar la búsqueda.

* `cq.workflow.model.combo`

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelCombo es un [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) personalizado que muestra una lista de modelos de flujo de trabajo disponibles.

* `cq.workflow.model.selector`

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelSelector combina WorkflowModelCombo con una imagen en miniatura del flujo de trabajo y botones para crear y editar modelos de flujo de trabajo.

* `createsitewizard`

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateSiteWizard es un asistente paso a paso para crear sitios (MSM).

* `createversiondialog`

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateVersionDialog es un cuadro de diálogo que permite crear una versión de una página.

* `customcontentpanel`

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CustomContentPanel es un panel especial para utilizarlo en [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html): su contenido se recupera y se envía a una dirección URL diferente de la de los demás campos del cuadro de diálogo.

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SplitButton especializado que contiene un menú de [elementos CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). El botón recorre automáticamente cada elemento de menú en cada clic, provocando el evento [change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) del botón (o llamando a la función [changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) del botón, si se proporciona) para el elemento de menú activo.

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Mecanismo para mostrar datos mediante plantillas de diseño y formato personalizados. DataView usa una [CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) como mecanismo de creación de plantillas interno y está enlazada a una [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), de modo que a medida que los datos del almacén cambian, la vista se actualiza automáticamente para reflejar los cambios.

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Proporciona un campo de entrada de fecha con una lista desplegable de [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y validación de fecha automática.

* `datemenu`

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Menú que contiene un componente [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `datepicker`

  [Selector de fecha CQ.Ext.Date](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un selector de fechas emergente. La clase [DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) utiliza esta clase para permitir examinar y seleccionar fechas válidas.

* `datetime`

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DateTime permite al usuario escribir una fecha y una hora combinando [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `dialog`

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El Diálogo es una ventana especial. Tiene un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también puede mostrar solo información.

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet es un [FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para su uso en [cuadros de diálogo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una pequeña clase auxiliar para crear un [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) configurado con un [CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para facilitar la interacción con un [proveedor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)CQ.Ext.Direct[ del lado del servidor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `displayfield`

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de texto de solo visualización que no se valida ni se envía.

* `editbar`

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditBar permite al usuario editar contenido mediante los botones de una barra.

  Aunque no aparece en la lista aquí, EditBar tiene todos los miembros de [CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `editor`

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de editor base que controla la visualización y la ocultación bajo demanda y tiene lógica integrada de tamaño y de administración de eventos.

* `editorgrid`

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Esta clase amplía la clase [GridPanel Class](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para proporcionar la edición de celdas en las [columnas](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) seleccionadas. Las columnas editables se especifican proporcionando un [editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) en la [configuración de columna](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditRollover permite al usuario editar contenido mediante doble clic y proporciona más acciones de edición a través de un menú contextual. El área editable se indica con un marco cuando el ratón se desplaza sobre el contenido.

* `feedimporter`

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FeedImporter permite al usuario importar fuentes RSS o Atom y crear páginas para cada entrada de fuente.

* `field`

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase base para campos de formulario que proporciona control de eventos, tamaño, control de valores y otras funcionalidades predeterminadas.

* `fieldset`

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenedor estándar utilizado para agrupar elementos en un [formulario](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `fileuploaddialogbutton`

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadDialogButton crea un botón que abre un nuevo cuadro de diálogo para cargar un archivo a través de FileUploadField. Se puede utilizar dentro de cuadros de diálogo de edición, donde la carga debe realizarse en un formulario independiente.

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField permite al usuario seleccionar un solo archivo para cargar.

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialog es un cuadro de diálogo para buscar y reemplazar tokens en una página y sus páginas secundarias.

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Esta clase representa la interfaz principal de un control de cuadrícula basado en componentes para representar los datos en un formato tabular de filas y columnas.

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Implementación de tienda especializada que permite agrupar registros por uno de los campos disponibles. Se usa con [CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para probar el modelo de datos de un GridPanel agrupado.

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialog es un cuadro de diálogo para mover una página y sus páginas secundarias, considerando también la reactivación de páginas previamente activadas (movimiento &#39;pesado&#39;).

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo oculto básico para almacenar valores ocultos en formularios que deben pasarse en el envío del formulario.

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButton es una pequeña clase de ayuda para proporcionar fácilmente botones de atrás y adelante. Normalmente se requieren dos instancias relacionadas: La instancia del botón adelante es un botón simple vinculado a la instancia del botón atrás que administra el historial.

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Proporciona un componente ligero de HTML Editor. Safari no admite algunas funciones de la barra de herramientas, por lo que el sistema las oculta automáticamente cuando es necesario. Se indica en las opciones de configuración cuando corresponde.

  Los botones de la barra de herramientas del editor tienen información sobre herramientas definida en la propiedad [buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Cuadro de diálogo sin formato que muestra el contenido de un iframe y permite formularios en iframes.

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Panel que contiene un iframe. Proporciona una fácil creación de iframes, un evento de carga de iframes y un fácil acceso al contenido del iframe.

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField es un campo de texto que se muestra como una etiqueta cuando no está enfocado.

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una pequeña clase de ayuda para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s a partir de datos JSON. Se configura automáticamente un JsonStore con [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo Etiqueta básico.

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialog es un cuadro de diálogo para copiar árboles de idioma.

* `linkchecker`

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LinkChecker es una herramienta para comprobar vínculos externos en un sitio.

* `listview`

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.list.ListView es una implementación rápida y ligera de una vista [similar a una cuadrícula](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `livecopyproperties`

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LiveCopyProperties proporciona un panel para ver y editar las propiedades de Live Copy ( herencia de relaciones, déclencheur de sincronización y acciones de sincronización ).

* `lvbooleancolumn`

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una clase de definición de columna que procesa campos de datos booleanos. Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para obtener más información.

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Esta clase encapsula los datos de configuración de columna que se utilizarán en la inicialización de [ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una clase de definición de columna que procesa una fecha pasada según la configuración regional predeterminada o un [formato](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) configurado. Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para obtener más información.

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una clase de definición de columna que procesa un campo de datos numéricos según una cadena [format](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para obtener más información.

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: en su lugar, usa [Buscador de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para examinar los medios.**

  MediaBrowseDialog es un cuadro de diálogo para examinar la biblioteca de medios.

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un objeto de menú. Contenedor al que se pueden agregar elementos de menú. El menú también puede servir como clase base cuando desee un menú especializado basado en otro componente (como [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), por ejemplo).

  Los menús pueden contener [elementos de menú](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o [componentes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s generales.

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La clase base para todos los elementos que se representan en menús. BaseItem proporciona opciones predeterminadas de procesamiento, administración de estado activada y configuración base compartidas por todos los componentes de menú.

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Agrega un elemento de menú que contiene una casilla de verificación de forma predeterminada, pero que también puede formar parte de un grupo de opciones.

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una clase base para todos los elementos de menú que requieren funciones relacionadas con menús (como submenús) y no son elementos de visualización estáticos. El elemento amplía la funcionalidad base de [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) al agregar la activación específica del menú y el control de clics.

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Agrega una barra de separación a un menú, que se utiliza para dividir grupos lógicos de elementos de menú. Por lo general, se agrega uno utilizando &quot;-&quot; en la llamada a add() o en la configuración de elementos en lugar de crear uno directamente.

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Agrega una cadena de texto estático a un menú, que se utiliza como encabezado o como separador de grupos.

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata` proporciona un conjunto de campos para determinar la información necesaria para un campo de metadatos tal como se utiliza, por ejemplo, en las páginas del Editor de recursos.

  Proporciona los siguientes campos:

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `MultiField` es una lista editable de campos de formulario para editar propiedades de varios valores.

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El componente Multivariate Testing se puede utilizar para definir y editar un conjunto de imágenes que se presentan como titulares alternativos. Las estadísticas de tasa de pulsaciones se recopilan por banner.

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox` permite al usuario suscribirse a las acciones de WCM y administrar las notificaciones.

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de texto numérico que proporciona filtrado automático de pulsación de tecla y validación numérica.

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter` es una herramienta para importar y convertir documentos de Microsoft® Word en páginas de AEM. Esta función permite editar contenido sin conexión mediante un procesador de textos.

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw` puede contener código HTML personalizado (introducido directamente o recuperado de una dirección URL).

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  A medida que aumenta el número de registros, aumenta el tiempo necesario para que el explorador los procese. La paginación se utiliza para reducir la cantidad de datos intercambiados con el cliente.

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un `panel` es un contenedor que tiene una funcionalidad y componentes estructurales específicos que lo convierten en el bloque de creación perfecto para las interfaces de usuario orientadas a aplicaciones.

  Debido a su herencia, los paneles provienen de [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El campo de referencia de párrafo permite examinar las páginas y seleccionar uno de sus párrafos. Consta de un campo de déclencheur y un cuadro de diálogo de exploración de párrafo asociado.

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password` es como [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), pero mantiene su valor en privado, lo que permite a los usuarios introducir datos confidenciales.

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: use [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) en su lugar**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField` es un campo de entrada diseñado para rutas con finalización de ruta y un botón para abrir [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para examinar el repositorio del servidor. También puede examinar los párrafos de la página para obtener información sobre la generación avanzada de vínculos.

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un componente actualizable de la barra de progreso. La barra de progreso admite dos modos diferentes: manual y automático.

  En el modo manual, usted es responsable de mostrar, actualizar (a través de [updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)) y borrar la barra de progreso según sea necesario de su propio código. Este método es el más adecuado cuando desea mostrar el progreso.

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Implementación de cuadrícula especializada diseñada para imitar la cuadrícula de propiedades tradicional, como se suele ver en los IDE de desarrollo. Cada fila de la cuadrícula representa una propiedad de algún objeto y los datos se almacenan como un conjunto de pares de nombre/valor en [CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s.

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid` es una cuadrícula genérica que se utiliza para mostrar y editar propiedades de objetos.

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip`: una clase de información de objeto especializada para información de objeto que se puede especificar en marcado y administrar automáticamente mediante la instancia global de [CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Consulte el encabezado de clase QuickTips para obtener detalles y ejemplos de uso adicionales.

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo `radio` único. Igual que la casilla de verificación, pero se proporciona como una comodidad para configurar automáticamente el tipo de entrada. El explorador agrupa automáticamente los botones de opción cuando cada botón de opción del grupo utiliza el mismo nombre.


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un contenedor de agrupación para los controles [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog` es un cuadro de diálogo para mostrar referencias en una página.

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog` es un cuadro de diálogo para restaurar una versión anterior de un árbol.

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialog es un cuadro de diálogo para restaurar una versión anterior de una página.

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText` proporciona un campo de formulario para editar información de texto con estilo (texto enriquecido).

  El componente `RichText` proporciona actualmente las siguientes características:

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El plan de despliegue proporciona un cuadro de diálogo para observar el progreso de un despliegue de página. Un [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) inicia el RolloutPlan.

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard` proporciona un asistente para desplegar una página. RolloutWizard inicia un [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField` proporciona un campo de búsqueda que proporciona los resultados en una lista desplegable que se puede utilizar para buscar en el repositorio.

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El `Selection` permite que el usuario elija entre varias opciones. Las opciones pueden formar parte de la configuración o cargarse desde una respuesta JSON. La selección se puede representar como una lista desplegable (seleccionar) o un cuadro combinado (seleccionar más la entrada de texto libre).

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick` es un asistente flotante que proporciona al usuario herramientas comunes para la edición de páginas.

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin` es una consola que proporciona funciones de administración de WCM.

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter` permite al usuario importar sitios web completos y crear proyectos iniciales.

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField` permite que el usuario introduzca la anchura y altura (por ejemplo, para una imagen).

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Regulador que admite orientación vertical u horizontal, ajustes de teclado, ajuste configurable, clic en el eje y animación. Se puede agregar como un elemento a cualquier contenedor. Por ejemplo, uso: ...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El componente Presentación de diapositivas permite definir y editar un conjunto de imágenes y títulos de imágenes. Los usuarios pueden ver el conjunto como una presentación.

  El componente Presentación de diapositivas se basa en el componente [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile es un cargador de archivos inteligente.

  Si hay instalado un complemento de Flash (versión >= 9), las cargas se ejecutan mediante la biblioteca de carga SWF, que proporciona una forma cómoda de gestionar las cargas.

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage es un cargador de imágenes inteligente. Proporciona herramientas para procesar una imagen cargada como, por ejemplo, una herramienta para definir mapas de imagen y un recortador de imágenes.

  El componente está diseñado para utilizarse en una pestaña de cuadro de diálogo independiente.

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Se utiliza para proporcionar un espacio considerable en un diseño.

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner` es un campo de déclencheur para valores numéricos, de fecha u hora. El valor se puede aumentar y reducir utilizando los déclencheur ascendentes y descendentes proporcionados, la rueda de desplazamiento o las teclas.

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un `splitbutton` que proporciona una flecha desplegable integrada que puede activar un evento independientemente del evento de clic predeterminado del botón. Normalmente, se utiliza para mostrar un menú desplegable que proporciona opciones adicionales a la acción del botón principal, pero cualquier controlador personalizado puede proporcionar la implementación de `arrowclick`.

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static` se puede usar para mostrar texto arbitrario o HTML.

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics` muestra las impresiones de página como un gráfico. El widget permite seleccionar un periodo para el cual se deben mostrar las estadísticas.

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La clase `Store` encapsula una caché del lado del cliente de objetos [Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) que proporcionan datos de entrada para componentes como [GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), [ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o [DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField` proporciona sugerencias al usuario según su entrada.

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher` proporciona un grupo de botones para la barra de encabezado de una consola con el fin de cambiar entre Sitios web, Digital Assets, Herramientas, Flujo de trabajo y Seguridad.

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: use [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) en su lugar.**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TableEdit2` proporciona un widget para crear tablas.

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un contenedor de pestañas básico. Los TabPanels se pueden usar exactamente igual que un [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) estándar con fines de diseño, pero también tienen compatibilidad especial para contener componentes secundarios ([`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)).

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

  es un widget de formulario para introducir etiquetas. Tiene un menú emergente para seleccionar entre las etiquetas existentes, incluye finalización automática y muchas otras funciones.

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de texto multilínea. Se puede usar como reemplazo directo de los campos `textarea` tradicionales, además agrega compatibilidad con el cambio de tamaño automático.

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton` proporciona un vínculo de texto con las capacidades de [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo de texto básico. Se puede usar como reemplazo directo de entradas de texto tradicionales o como clase base para controles de entrada más sofisticados (como [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)).

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Proporciona un campo de entrada de tiempo con una lista desplegable de tiempo y validación automática de la hora. Ejemplo de uso: ...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype sugerencia Esta es la clase base para [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) que proporciona el diseño y la posición básicos que todas las clases basadas en sugerencias requieren. Esta clase se puede utilizar directamente para sugerencias simples y con posición estática.

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Agrega una barra de separación a un menú, que se utiliza para dividir grupos lógicos de elementos de menú. El separador también puede llevar un título.

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Clase `Toolbar` básica. Aunque [`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para la barra de herramientas es [`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), los elementos de la barra de herramientas (elementos secundarios para el contenedor de la barra de herramientas) pueden ser prácticamente cualquier tipo de componente. Los elementos de la barra de herramientas se pueden crear explícitamente mediante sus constructores.

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Implementación estándar `tooltip` para proporcionar información adicional al pasar el ratón por encima de un elemento de destino. @xtype información sobre herramientas.

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype `treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel` proporciona una representación de la interfaz de usuario con estructura de árbol de los datos con estructura de árbol.

  Los [TreeNode](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) agregados a `TreePanel` pueden contener metadatos usados por su aplicación en su propiedad [attributes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Proporciona un contenedor conveniente para `TextFields` que agrega un botón de déclencheur en el que se puede hacer clic (de forma predeterminada, se parece a un cuadro combinado). El déclencheur no tiene una acción predeterminada, por lo que debe asignar una función para implementar el controlador de clics de déclencheur anulando [onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Puede crear un `TriggerField` directamente, ya que se representa exactamente como un cuadro combinado.

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  El `UploadDialog` permite al usuario cargar archivos en el repositorio. Crea un nuevo UploadDialog.

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Elemento de la barra de herramientas para mostrar el nombre de usuario actual y permitir acciones del usuario como editar propiedades del usuario y suplantar.

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un contenedor especializado que representa el área de aplicación visible (la ventanilla del explorador).

  `Viewport` se representa en el cuerpo del documento y se ajusta automáticamente al tamaño de la ventanilla del explorador y administra el cambio de tamaño de la ventana. Solo puede haber una ventanilla creada.

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Panel especializado diseñado para utilizarse como ventana de aplicación. Las ventanas son flotantes, [modificables](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) y [arrastrables](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) de forma predeterminada. Las ventanas se pueden [maximizar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) para llenar la ventanilla, restaurar a su tamaño anterior y se pueden [minimizar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)d.

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una pequeña clase auxiliar para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s a partir de datos XML. Un(a) `XmlStore` se configura automáticamente con un(a) [CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

  `cqinclude`: un pseudotipo que incluye definiciones de widget de una ruta diferente en el repositorio. Normalmente se utiliza en cuadros de diálogo de página. No hay ninguna clase de widget de JavaScript real para este xtype. La clase `CQ.Util` la procesa mediante la función `formatData()`.
