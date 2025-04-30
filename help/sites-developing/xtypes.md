---
title: Uso de xtypes (IU clásica)
description: Obtenga información acerca de todos los xtype disponibles con Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '3865'
ht-degree: 0%

---

# Uso de xtypes (IU clásica){#using-xtypes-classic-ui}

Esta página describe todos los xtype disponibles con Adobe Experience Manager (AEM).

En el lenguaje ExtJS, un xtype es un nombre simbólico dado a una clase. Puede leer el párrafo &quot;Tipos XT de componentes&quot; de la [Descripción general de ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) para obtener una explicación detallada sobre qué es un xtype y cómo se puede usar.

Para obtener información completa sobre todos los widgets disponibles en AEM, consulte la [documentación de la API de widgets](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

Para saber en qué componentes se utiliza un xtype determinado en AEM, puede utilizar la siguiente consulta Xpath en CRXDE sustituyendo &quot;casilla de verificación&quot; por el xtype que le interese:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Esta página describe el uso de xtype de ExtJS dentro de la IU clásica.
>
>Adobe recomienda usar la [interfaz de usuario táctil](/help/sites-developing/touch-ui-concepts.md) moderna y estándar basada en [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) y [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

A continuación se enumeran los xtype disponibles en Adobe Experience Manager:

* anotación

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.Annotation)

  El cuadro de diálogo es un tipo especial de ventana con un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también puede mostrar solo información.

* arraystore

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

  Anteriormente conocida como &quot;SimpleStore&quot;.

  Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos de la matriz. ArrayStore se configura automáticamente con [CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* editor de recursos

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.dam.AssetEditor)

  Editor de recursos utilizado en el administrador de DAM.

* assetreferencesearchdialog

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

  AssetReferenceSearchDialog es un cuadro de diálogo que aparece en caso de que una página haga referencia a recursos o etiquetas.

* blueprintconfig

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

  BlueprintConfig proporciona un panel para ver las Live Copies de un modelo y editar sus propiedades ( sincronizar déclencheur y acciones de sincronización ).

* blueprintstatus

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

  BlueprintStatus proporciona un panel para ver y editar un modelo y sus relaciones de Live Copies. La exploración se realiza mediante un [CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), una edición mediante un [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) y un [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* caja

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.BoxComponent)

  Clase base para cualquier [componente](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Component) cuyo tamaño debe ser una caja, con anchura y altura.

  BoxComponent proporciona ajustes automáticos del modelo de cuadro para el tamaño y la posición y funciona correctamente dentro del modelo de representación de componentes.

* browsedialog

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.BrowseDialog)

  El cuadro de diálogo Examinar permite al usuario examinar el repositorio para seleccionar una ruta. Se suele usar a través de [BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.BrowseField)

  **Obsoleto: use [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.PathField) en su lugar**

* editor por lotes

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.BulkEditor)

  BulkEditor proporciona un motor de búsqueda y una cuadrícula para editar los resultados de búsqueda.

  El editor en bloque debe insertarse en un formulario de HTML (requerido por la funcionalidad de importación). Esto funciona perfectamente con [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

  BulkEditorForm proporciona [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.BulkEditor) rodeado por un formulario de HTML. Esta es la versión independiente de [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.BulkEditor), se requiere un formulario HTML para el botón Importar.

* button

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Button)

  Clase de botón simple

* buttongroup

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

  Contenedor de un grupo de botones.

* gráfico

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.chart.Chart)

  El paquete CQ.Ext.chart proporciona la capacidad de visualizar datos con gráficos basados en Flash. Cada gráfico se vincula directamente a un CQ.Ext.data.Store, lo que permite realizar actualizaciones automáticas del gráfico. Para cambiar el aspecto de un gráfico, vea las opciones de configuración [chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.chart.Chart) y [extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.chart.Chart).

* checkbox

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

  Campo de casilla de verificación único. Se puede utilizar como reemplazo directo de los campos de casilla de verificación tradicionales.

* checkboxgroup

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

  Un contenedor de agrupación para los controles [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Checkbox).

* clearcombo

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ClearableComboBox)

  ClearableComboBox es un cuadro combinado no editable con un déclencheur para borrar su valor.

* campo de color

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ColorField)

  ColorField permite al usuario introducir un valor hexadecimal de color directamente o mediante [CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ColorList)

  ColorList permite al usuario elegir un color de una lista editable.

* colormenu

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

  Menú que contiene un componente [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ColorPalette).

* paleta de colores

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ColorPalette)

  Clase de paleta de colores sencilla para elegir colores. La paleta se puede representar en cualquier contenedor.

* combinado

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

  Un control combobox con compatibilidad para autocompletar, carga remota, paginación y muchas otras características.

  Un ComboBox funciona de manera similar a un campo &lt;select> tradicional de HTML. La diferencia es que para enviar [valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox), debe especificar un [hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox) para crear una entrada oculta.

* componente

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Component)

  Clase base para todos los componentes de texto. Todas las subclases de Component pueden participar en el ciclo de vida automatizado del componente Ext de creación, representación y destrucción que proporciona la clase [Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container). Los componentes se pueden agregar a un contenedor mediante la opción de configuración [items](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container) en el momento en que se crea el contenedor.

* componentextractor

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

  ComponentExtractor permite al usuario extraer componentes de un sitio web o una página.

* selector de componente

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ComponentSelector)

  Una selección agrupada y ordenada de los componentes disponibles.

* componentstyles

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ComponentStyles)

* campo compuesto

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)

  Clase base para campos de formulario complejos basados en panel que incluyen un campo de formulario o un grupo de campos de formulario.

* contenedor

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container)

  Clase base para cualquier [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.BoxComponent) que pueda contener otros componentes. Los contenedores administran el comportamiento básico de los elementos contenedores, a saber, agregar, insertar y quitar elementos.

  Las clases de contenedor más utilizadas son [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window) y [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ContentFinder)

  ContentFinder es una [ventanilla](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Viewport) especializada de dos columnas que contiene el buscador de contenido real a la izquierda y el marco de contenido a la derecha.

* contentfindertab

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

  ContentFinderTab es un panel especializado que proporciona las características utilizadas en los paneles de pestañas de [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ContentFinder). Normalmente incluye un formulario de búsqueda (el Cuadro de consulta) y una vista de datos para mostrar la búsqueda.

* cq.workflow.model.combo

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

  WorkflowModelCombo es un [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox) personalizado que muestra una lista de modelos de flujo de trabajo disponibles.

* cq.workflow.model.selector

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

  WorkflowModelSelector combina WorkflowModelCombo con una imagen en miniatura del flujo de trabajo y botones para crear y editar modelos de flujo de trabajo.

* createsitewizard

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

  CreateSiteWizard es un asistente paso a paso para crear sitios (MSM).

* createversiondialog

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

  CreateVersionDialog es un cuadro de diálogo que permite crear una versión de una página.

* customcontentpanel

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.CustomContentPanel)

  CustomContentPanel es un panel especial para utilizarlo en [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog): su contenido se recupera y se envía a una dirección URL diferente de la de los demás campos del cuadro de diálogo.

* ciclo

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.CycleButton)

  SplitButton especializado que contiene un menú de [elementos CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.CheckItem). El botón recorre automáticamente cada elemento de menú al hacer clic, provocando el evento [change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.CycleButton) del botón (o llamando a la función [changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.CycleButton) del botón, si se proporciona) para el elemento de menú activo.

* dataview

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.DataView)

  Mecanismo para mostrar datos mediante plantillas de diseño y formato personalizados. DataView usa una [CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.XTemplate) como mecanismo de creación de plantillas interno y está enlazada a una [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store), de modo que a medida que los datos del almacén cambian, la vista se actualiza automáticamente para reflejar los cambios.

* datefield

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.DateField)

  Proporciona un campo de entrada de fecha con una lista desplegable de [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.DatePicker) y validación de fecha automática.

* datemenu

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

  Menú que contiene un componente [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.DatePicker).

* selector de fecha

  [Selector de fecha CQ.Ext.Date](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.DatePicker)

  Un selector de fechas emergente. La clase [DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.DateField) utiliza esta clase para permitir examinar y seleccionar fechas válidas.

* datetime

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.DateTime)

  DateTime permite al usuario escribir una fecha y una hora combinando [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.DateField) y [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* cuadro de diálogo

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog)

  El cuadro de diálogo es una ventana especial con un formulario en el cuerpo y un grupo de botones en el pie de página. Normalmente se utiliza para editar contenido, pero también puede mostrar solo información.

* dialogfieldset

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.DialogFieldSet)

  DialogFieldSet es un [FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.FieldSet) para su uso en [cuadros de diálogo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog).

* directstore

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

  Clase auxiliar pequeña para crear un [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store) configurado con un [CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) y [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader) para facilitar la interacción con un [proveedor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.direct.Provider) del lado del servidor [CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Direct).

* displayfield

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

  Campo de texto de solo visualización que no se valida ni se envía.

* barra de edición

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditBar)

  EditBar permite al usuario editar contenido mediante los botones de una barra.

  Aunque no aparece en la lista aquí, EditBar tiene todos los miembros de [CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Editor)

  Campo de editor base que controla la visualización y la ocultación bajo demanda y tiene lógica integrada de tamaño y de administración de eventos.

* rejilla del editor

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

  Esta clase amplía la clase [GridPanel Class](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) para proporcionar la edición de celdas en las [columnas](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.Column) seleccionadas. Las columnas editables se especifican proporcionando un [editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) en la [configuración de columna](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditRollover)

  EditRollover permite al usuario editar contenido mediante doble clic y proporciona más acciones de edición a través de un menú contextual. El área editable se indica con un marco cuando el ratón se desplaza sobre el contenido.

* importador de alimentos

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.FeedImporter)

  FeedImporter permite al usuario importar fuentes RSS o Atom y crear páginas para cada entrada de fuente.

* field

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Field)

  Clase base para campos de formulario que proporciona control de eventos, tamaño, control de valores y otras funcionalidades predeterminadas.

* fieldset

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

  Contenedor estándar utilizado para agrupar elementos en un [formulario](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.FormPanel).

* fileuploaddialogbutton

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

  FileUploadDialogButton crea un botón que abre un nuevo cuadro de diálogo para cargar un archivo a través de FileUploadField. Se puede utilizar dentro de cuadros de diálogo de edición, donde la carga debe realizarse en un formulario independiente.

* fileuploadfield

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.FileUploadField)

  FileUploadField permite al usuario seleccionar un solo archivo para cargar.

* findreplacedialog

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

  FindReplaceDialog es un cuadro de diálogo para buscar y reemplazar tokens en una página y sus páginas secundarias.

* destellar

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* cuadrícula

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

  Esta clase representa la interfaz principal de un control de cuadrícula basado en componentes para representar los datos en un formato tabular de filas y columnas.

* groupingstore

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

  Implementación de tienda especializada que permite agrupar registros por uno de los campos disponibles. Se usa con un [CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) para probar el modelo de datos de un GridPanel agrupado.

* heavy-movedialog

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

  HeavyMoveDialog es un cuadro de diálogo para mover una página y sus páginas secundarias, considerando también la reactivación de páginas activadas anteriormente (movimiento &quot;pesado&quot;).

* oculto

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Hidden)

  Campo oculto básico para almacenar valores ocultos en formularios que deben pasarse en el envío del formulario.

* historybutton

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.HistoryButton)

  HistoryButton es una pequeña clase de ayuda que proporciona fácilmente botones de atrás y adelante. Normalmente se requieren dos instancias relacionadas: La instancia del botón adelante es un botón simple vinculado a la instancia del botón atrás que administra el historial.

* htmleeditor

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

  Proporciona un componente ligero de HTML Editor. Safari no admite algunas funciones de la barra de herramientas, por lo que se ocultan automáticamente cuando es necesario. Se indican en las opciones de configuración cuando corresponde.

  Los botones de la barra de herramientas del editor tienen información sobre herramientas definida en la propiedad [buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor).

* iframedialog

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.IframeDialog)

  Cuadro de diálogo sin formato que muestra el contenido de un iframe y permite formularios en iframes.

* iframepanel

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.IframePanel)

  Panel que contiene un iframe. Proporciona una creación sencilla de iframes, un evento de carga de iframes y un acceso fácil al contenido del iframe.

* inlinetextfield

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.InlineTextField)

  InlineField es un campo de texto que se muestra como una etiqueta cuando no está enfocado.

* jsonstore

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

  Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos JSON. Se configura automáticamente un JsonStore con [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* etiqueta

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Label)

  Campo Etiqueta básico.

* languageCopyDialog

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

  LanguageCopyDialog es un cuadro de diálogo para copiar árboles de idioma.

* linkchecker

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.LinkChecker)

  LinkChecker es una herramienta para comprobar vínculos externos en un sitio.

* listview

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.ListView)

  CQ.Ext.list.ListView es una implementación rápida y ligera de una vista [similar a una cuadrícula](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel).

* livecopyproperties

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

  LiveCopyProperties proporciona un panel para ver y editar las propiedades de Live Copy ( herencia de relaciones, déclencheur de sincronización y acciones de sincronización ).

* lvbooleancolumn

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

  Una clase de definición de columna que procesa campos de datos booleanos. Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más información.

* lvcolumn

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column)

  Esta clase encapsula los datos de configuración de columna que se utilizarán en la inicialización de [ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

  Una clase de definición de columna que procesa una fecha pasada según la configuración regional predeterminada o un [formato](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.DateColumn) configurado. Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más información.

* lvnumbercolumn

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

  Una clase de definición de columna que procesa un campo de datos numéricos según una cadena [format](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.NumberColumn). Consulte la opción de configuración [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.list.Column) para obtener más información.

* mediabrowsedialog

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.MediaBrowseDialog)

  **Obsoleto: en su lugar, usa [Buscador de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ContentFinder) para examinar los medios.**

  MediaBrowseDialog es un cuadro de diálogo para examinar la biblioteca de medios.

* menú

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.Menu)

  Un objeto de menú. Este es el contenedor al que se pueden agregar elementos de menú. El menú también puede servir como clase base cuando desee un menú especializado basado en otro componente (como [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.DateMenu), por ejemplo).

  Los menús pueden contener [elementos de menú](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.Item) o [componentes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Component)s generales.

* menubaseitem

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

  La clase base para todos los elementos que se representan en menús. BaseItem proporciona opciones predeterminadas de procesamiento, administración de estado activada y configuración base compartidas por todos los componentes de menú.

* menucheckitem

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

  Agrega un elemento de menú que contiene una casilla de verificación de forma predeterminada, pero que también puede formar parte de un grupo de opciones.

* menuitem

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.Item)

  Una clase base para todos los elementos de menú que requieren funciones relacionadas con menús (como submenús) y no son elementos de visualización estáticos. El elemento amplía la funcionalidad base de [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) al agregar la activación específica del menú y el control de clics.

* menuseparator

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.Separator)

  Agrega una barra de separación a un menú, que se utiliza para dividir grupos lógicos de elementos de menú. Por lo general, se agrega uno de estos elementos utilizando &quot;-&quot; en la llamada a add() o en la configuración de elementos en lugar de crear uno directamente.

* menutextitem

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

  Agrega una cadena de texto estático a un menú, que se utiliza como separador de encabezado o de grupo.

* metadata

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.dam.form.Metadata)

  Los metadatos proporcionan un conjunto de campos para determinar la información necesaria para un campo de metadatos tal como se utiliza, por ejemplo, en las páginas del editor de recursos.

  Proporciona los siguientes campos:

* multicampo

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)

  MultiField es una lista editable de campos de formulario para editar propiedades de varios valores.

* mvt

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MVT)

  El componente Multivariate Testing se puede utilizar para definir y editar un conjunto de imágenes que se presentan como titulares alternativos. Las estadísticas de tasa de pulsaciones se recopilan por banner.

* notificationinbox

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

  La bandeja de entrada de notificaciones permite al usuario suscribirse a las acciones de WCM y administrar las notificaciones.

* campo numérico

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.NumberField)

  Campo de texto numérico que proporciona filtrado automático de pulsación de tecla y validación numérica.

* offlineimporter

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

  OfflineImporter es una herramienta para importar y convertir documentos de Microsoft® Word a páginas de AEM. Esta función permite editar contenido sin conexión mediante un procesador de textos.

* ownerdraw

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.OwnerDraw)

  OwnerDraw puede contener código HTML personalizado (introducido directamente o recuperado de una dirección URL).

* paginación

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

  A medida que aumenta el número de registros, aumenta el tiempo necesario para que el explorador los procese. La paginación se utiliza para reducir la cantidad de datos intercambiados con el cliente.

* panel

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Panel)

  El panel es un contenedor que tiene una funcionalidad específica y componentes estructurales que lo convierten en el bloque de creación perfecto para interfaces de usuario orientadas a la aplicación.

  Los paneles son, en virtud de su herencia de [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container).

* paragraphreference

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.ParagraphReference)

  El campo de referencia de párrafo permite examinar las páginas y seleccionar uno de sus párrafos. Consta de un campo de déclencheur y un cuadro de diálogo de exploración de párrafo asociado.

* contraseña

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Password)

  La contraseña es como [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField), pero mantiene su valor en privado, lo que permite a los usuarios introducir datos confidenciales.

* conclusión de ruta

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.PathCompletion)

  **Obsoleto: use [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.PathField) en su lugar**

* campo de trayectoria

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.PathField)

  PathField es un campo de entrada diseñado para rutas con finalización de ruta y un botón para abrir [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.BrowseDialog) para examinar el repositorio del servidor. También puede examinar los párrafos de la página para obtener información sobre la generación avanzada de vínculos.

* progreso

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ProgressBar)

  Un componente actualizable de la barra de progreso. La barra de progreso admite dos modos diferentes: manual y automático.

  En el modo manual, usted es responsable de mostrar, actualizar (a través de [updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ProgressBar)) y borrar la barra de progreso según sea necesario de su propio código. Este método es el más adecuado cuando desea mostrar el progreso.

* propertygrid

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

  Implementación de cuadrícula especializada diseñada para imitar la cuadrícula de propiedades tradicional, como se suele ver en los IDE de desarrollo. Cada fila de la cuadrícula representa una propiedad de algún objeto y los datos se almacenan como un conjunto de pares de nombre/valor en [CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.PropertyGrid)

  PropertyGrid es una cuadrícula genérica que se utiliza para mostrar y editar propiedades de objetos.

* información rápida

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.QuickTip)

  @xtype información rápida Clase de información sobre herramientas especializada que se puede especificar en el marcado y administrar automáticamente mediante la instancia global de [CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.QuickTips). Consulte el encabezado de clase QuickTips para obtener detalles y ejemplos de uso adicionales.

* radio

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Radio)

  Un solo campo de radio. Igual que la casilla de verificación, pero se proporciona como una comodidad para configurar automáticamente el tipo de entrada. El explorador gestiona automáticamente la agrupación de emisoras si asigna a cada emisora de radio de un grupo el mismo nombre.

* grupo radioeléctrico

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

  Un contenedor de agrupación para los controles [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.Radio).

* referencesdialog

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

  El cuadro de diálogo Referencias es un cuadro de diálogo para mostrar referencias en una página.

* restoretreedialog

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

  RestoreTreeDialog es un cuadro de diálogo para restaurar una versión anterior de un árbol.

* restoreversiondialog

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

  RestoreVersionDialog es un cuadro de diálogo para restaurar una versión anterior de una página.

* richtext

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText)

  RichText proporciona un campo de formulario para editar información de texto con estilo (texto enriquecido).

  Actualmente, el componente Texto enriquecido proporciona las siguientes funciones:

* plan de despliegue

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

  El plan de despliegue proporciona un cuadro de diálogo para ver el progreso de un despliegue de página. Un [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard) ha iniciado RolloutPlan.

* rolloutwizard

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

  El Asistente para despliegue proporciona un asistente para desplegar una página. RolloutWizard inicia un [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* campo de búsqueda

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SearchField)

  SearchField proporciona un campo de búsqueda que proporciona los resultados en una lista desplegable que se puede utilizar para buscar en el repositorio.

* selección

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection)

  Selection permite al usuario elegir entre varias opciones. Las opciones pueden formar parte de la configuración o cargarse desde una respuesta JSON. La selección se puede representar como un cuadro desplegable (seleccionar) o un cuadro combinado (seleccionar más la entrada de texto libre).

* compinche

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.Sidekick)

  Sidekick es un asistente flotante que proporciona al usuario herramientas comunes para la edición de páginas.

* siteadmin

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

  SiteAdmin es una consola que proporciona funciones de administración de WCM.

* importador de sitios

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteImporter)

  SiteImporter permite al usuario importar sitios web completos y crear proyectos iniciales.

* campo de tamaño

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SizeField)

  SizeField permite al usuario introducir el ancho y el alto (por ejemplo, para una imagen).

* regulador

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Slider)

  Regulador que admite orientación vertical u horizontal, ajustes de teclado, ajuste configurable, clic en el eje y animación. Se puede agregar como elemento a cualquier contenedor. Ejemplo de uso: ...

* presentación

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Slideshow)

  La presentación de diapositivas proporciona un componente que se puede utilizar para definir y editar un conjunto de imágenes y títulos de imágenes que pueden verse como una presentación de diapositivas.

  El componente Presentación de diapositivas se basa en el componente [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SmartImage).

* smartfile

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SmartFile)

  SmartFile es un cargador de archivos inteligente.

  Si hay instalado un complemento de Flash (versión >= 9), las cargas se ejecutan mediante la biblioteca de carga SWF, que proporciona una forma cómoda de gestionar las cargas.

* smartimage

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SmartImage)

  SmartImage es un cargador de imágenes inteligente. Proporciona herramientas para procesar una imagen cargada como, por ejemplo, una herramienta para definir mapas de imagen y un recortador de imágenes.

  El componente está diseñado para utilizarse en una pestaña de diálogo independiente.

* espaciador

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Spacer)

  Se utiliza para proporcionar un espacio considerable en un diseño.

* hilandero

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Spinner)

  El control de número es un campo de déclencheur para valores numéricos, de fecha u hora. El valor se puede aumentar y reducir utilizando los déclencheur arriba y abajo proporcionados, la rueda de desplazamiento o las teclas.

* splitbutton

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.SplitButton)

  Botón dividido que proporciona una flecha desplegable integrada que puede activar un evento independientemente del evento de clic predeterminado del botón. Normalmente, esto se utilizaría para mostrar un menú desplegable que proporciona opciones adicionales a la acción del botón principal, pero cualquier controlador personalizado puede proporcionar la implementación mediante flechas.

* estático

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Static)

  El elemento estático puede utilizarse para mostrar texto arbitrario o HTML.

* estadísticas

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.Statistics)

  Las Estadísticas muestran las impresiones de la página como un gráfico. El widget permite seleccionar un periodo para el cual se deben mostrar las estadísticas.

* almacenar

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store)

  La clase Store encapsula una caché del lado del cliente de objetos [Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Record) que proporcionan datos de entrada para componentes como [GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox) o [DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.DataView).

* sugerir campo

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.SuggestField)

  SuggestField proporciona al usuario sugerencias basadas en su entrada.

* cambiador

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Switcher)

  El conmutador proporciona un grupo de botones para la barra de encabezado de una consola para cambiar entre sitios web, Digital Assets, Herramientas, Flujo de trabajo y Seguridad.

* tableedit

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.TableEdit)

  **Obsoleto: use [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.TableEdit2) en su lugar.**

* tableedit2

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.TableEdit2)

  TableEdit2 proporciona un widget para crear tablas.

* tablero de fichas

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.TabPanel)

  Un contenedor de pestañas básico. Los TabPanels se pueden usar exactamente igual que un [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Panel) estándar con fines de diseño, pero también tienen compatibilidad especial para contener componentes secundarios ([`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container)).

* etiquetas

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.tagging.TagInputField)

  ```
  CQ.tagging.TagInputField
  ```

  es un widget de formulario para introducir etiquetas. Tiene un menú emergente para seleccionar entre las etiquetas existentes, incluye finalización automática y muchas otras funciones.

* área de texto

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextArea)

  Campo de texto multilínea. Se puede utilizar como reemplazo directo de los campos de área de texto tradicionales, además de añadir compatibilidad con el ajuste automático de tamaño.

* textbutton

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.TextButton)

  TextButton proporciona un vínculo de texto con las capacidades de [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)

  Campo de texto básico. Se puede usar como reemplazo directo de entradas de texto tradicionales o como clase base para controles de entrada más sofisticados (como [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextArea) y [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatura

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Thumbnail)

* campo de tiempo

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TimeField)

  Proporciona un campo de entrada de tiempo con un menú desplegable de tiempo y validación automática de la hora. Ejemplo de uso: ...

* propina

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Tip)

  @xtype sugerencia Esta es la clase base para [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.QuickTip) y [CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Tooltip) que proporciona el diseño y la posición básicos que todas las clases basadas en sugerencias requieren. Esta clase se puede utilizar directamente para sugerencias simples y con posición estática.

* titleseparator

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.menu.TitleSeparator)

  Agrega una barra de separación a un menú, que se utiliza para dividir grupos lógicos de elementos de menú. El separador también puede llevar un título.

* barra de herramientas

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Toolbar)

  Clase Basic Toolbar. Aunque [`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Container) para la barra de herramientas es [`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Button), los elementos de la barra de herramientas (elementos secundarios para el contenedor de la barra de herramientas) pueden ser prácticamente cualquier tipo de componente. Los elementos de la barra de herramientas se pueden crear explícitamente mediante sus constructores.

* información de objeto

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.ToolTip)

  Implementación de información sobre herramientas estándar para proporcionar información adicional al pasar el ratón por encima de un elemento de destino. @xtype información sobre herramientas.

* triglía

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.tree.TreeGrid)

  @xtype triglicérido

* panel de árbol

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

  TreePanel proporciona una representación de la interfaz de usuario con estructura de árbol de los datos con estructura de árbol.

  [TreeNode](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)s agregados al TreePanel pueden contener metadatos usados por su aplicación en su propiedad [attributes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreeNode).

* déclencheur

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

  Proporciona un contenedor cómodo para TextFields que agrega un botón de déclencheur en el que se puede hacer clic (de forma predeterminada, parece un cuadro combinado). El déclencheur no tiene una acción predeterminada, por lo que debe asignar una función para implementar el controlador de clics de déclencheur anulando [onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Puede crear un TriggerField directamente, ya que se representa exactamente como un cuadro combinado.

* uploaddialog

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.UploadDialog)

  UploadDialog permite al usuario cargar archivos en el repositorio. Crea un nuevo UploadDialog.

* userinfo

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.UserInfo)

  Elemento de la barra de herramientas para mostrar el nombre de usuario actual y permitir acciones del usuario como editar propiedades del usuario y suplantar.

* ventanilla

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Viewport)

  Un contenedor especializado que representa el área de aplicación visible (la ventanilla del explorador).

  La ventanilla se procesa en el cuerpo del documento y se ajusta automáticamente al tamaño de la ventanilla del explorador y administra el cambio de tamaño de la ventana. Solo puede haber una ventanilla creada.

* ventana

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)

  Panel especializado diseñado para utilizarse como ventana de aplicación. Las ventanas son flotantes, [modificables](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window) y [arrastrables](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window) de forma predeterminada. Las ventanas se pueden [maximizar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window) para llenar la ventanilla, restaurar a su tamaño anterior y se pueden [minimizar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

  Clase auxiliar pequeña para facilitar la creación de [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de datos XML. XmlStore se configura automáticamente con [CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

  **cqinclude** pseudotipo que incluye definiciones de widget de una ruta diferente en el repositorio. Se utiliza comúnmente en los cuadros de diálogo de página. No hay ninguna clase de widget de JavaScript real para este xtype. La función formatData() de la clase CQ.Util la procesa. Para obtener más información, consulte este artículo de la base de conocimiento.
