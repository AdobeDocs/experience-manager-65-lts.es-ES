---
title: Uso y ampliación de widgets (IU clásica)
description: La interfaz basada en web de Adobe Experience Manager utiliza AJAX y otras tecnologías modernas de explorador para permitir que los autores editen y apliquen formato al contenido desde WYSIWYG directamente en la página web
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# Uso y ampliación de widgets (IU clásica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página describe el uso de widgets dentro de la IU clásica, que estaba en desuso en AEM 6.4.
>
>Adobe recomienda usar la moderna [IU táctil](/help/sites-developing/touch-ui-concepts.md) basada en [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) y [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

La interfaz basada en web de Adobe Experience Manager (AEM) utiliza AJAX y otras tecnologías modernas de explorador para permitir que los autores editen y apliquen formato al contenido directamente en la página web desde WYSIWYG.

AEM usa la biblioteca de widgets [ExtJS](https://www.sencha.com/), que proporciona los elementos de interfaz de usuario altamente refinados que funcionan en todos los exploradores más importantes y permiten crear experiencias de interfaz de usuario de nivel de escritorio.

Estos widgets se incluyen en AEM y, además de ser utilizados por el propio AEM, pueden utilizarse en cualquier sitio web creado con AEM.

Para obtener una referencia completa de todos los widgets disponibles en AEM, consulte la [documentación de la API de widgets](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o la [lista de xtypes existentes](/help/sites-developing/xtypes.md). Además, hay muchos ejemplos que muestran cómo usar el marco de ExtJS disponibles en el sitio [Sencha](https://examples.sencha.com/extjs/7.6.0/), el propietario del marco de trabajo.

Esta página ofrece información sobre cómo utilizar y ampliar widgets. Primero describe cómo [incluir código del lado del cliente en una página](#including-the-client-sided-code-in-a-page). A continuación, se describen algunos componentes de muestra que se han creado para ilustrar algunos usos y extensiones básicos. Estos componentes están disponibles en el paquete **Uso de widgets de ExtJS** en **Uso compartido de paquetes**.

El paquete incluye ejemplos de lo siguiente:

* [Cuadros de diálogo básicos](#basic-dialogs) creados con widgets predeterminados.
* [Cuadros de diálogo dinámicos](#dynamic-dialogs) creados con widgets predeterminados y lógica de JavaScript personalizada.
* Diálogos basados en [widgets personalizados](#custom-widgets).
* Un [panel de árbol](#tree-overview) que muestra un árbol JCR bajo una ruta determinada.
* Un [panel de cuadrícula](#grid-overview) que muestra datos en formato de tabla.

>[!NOTE]
>
>La IU clásica de Adobe Experience Manager se basa en [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusión del código del lado del cliente en una página {#including-the-client-sided-code-in-a-page}

El JavaScript del lado del cliente y el código de la hoja de estilo deben colocarse en una biblioteca de cliente.

Para crear una biblioteca de cliente:

1. Cree un nodo por debajo de `/apps/<project>` con las siguientes propiedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. Debajo de `clientlib` se crean las carpetas `css` y `js` (nt:folder).

1. Debajo de `clientlib` se crean los archivos `css.txt` y `js.txt` (nt:files). Estos archivos .txt enumeran los archivos que se incluyen en la biblioteca.

1. Editar `js.txt`: debe comenzar con &#39; `#base=js`&#39; seguido de la lista de los archivos agregados por el servicio de biblioteca del cliente de CQ, por ejemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: debe comenzar con &#39; `#base=css`&#39; seguido de la lista de los archivos agregados por el servicio de biblioteca del cliente de CQ, por ejemplo:

   ```
   #base=css
    components.css
   ```

1. Debajo de la carpeta `js`, coloque los archivos JavaScript que pertenecen a la biblioteca.

1. Debajo de la carpeta `css`, coloque los archivos `.css` y los recursos utilizados por los archivos css (por ejemplo, `my_icon.png`).

>[!NOTE]
>
>El manejo de las hojas de estilo descritas anteriormente es opcional.

Para incluir la biblioteca de cliente en el jsp del componente de página:

* para incluir hojas de estilos y código JavaScript:
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
donde `<category-nameX>` es el nombre de la biblioteca del cliente.

* para incluir solo código JavaScript:
  `<ui:includeClientLib js="<category-name>"/>`

Para obtener más información, consulte la descripción del [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) etiqueta.&lt;/ui:includeClientLib>

A veces, un biblioteca cliente solo debe estar disponible en modo de autor y debe excluirse en modo publicar. Se puede lograr de la siguiente manera:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introducción con las muestras {#getting-started-with-the-samples}

Para seguir los tutoriales de esta página, instale el paquete **Utilizando widgets de ExtJS** en una instancia local de AEM y cree una página de muestra en la que se incluyan los componentes. Para ello, haga lo siguiente:

1. En su instancia de AEM, descargue el paquete llamado **Utilizando widgets de ExtJS (v01)** desde Package Share e instale el paquete. Crea el proyecto `extjstraining` por debajo de `/apps` en el repositorio.
1. Incluya la biblioteca de cliente que contiene los scripts (js) y la hoja de estilo (css) en la etiqueta head del jsp de la página de Geometrixx. Va a incluir los componentes de ejemplo en una nueva página de la rama **Geometrixx**:
en **CRXDE Lite**, abra el archivo `/apps/geometrixx/components/page/headlibs.jsp` y agregue la categoría `cq.extjstraining` a la etiqueta `<ui:includeClientLib>` existente de la siguiente manera:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Cree una página en la rama **Geometrixx** debajo de `/content/geometrixx/en/products` y llámela **con widgets de ExtJS**.
1. Vaya en modo de diseño y agregue todos los componentes del grupo denominado **Uso de widgets de ExtJS** al diseño de Geometrixx
1. Volver en modo de edición: los componentes del grupo **Uso de widgets de ExtJS** están disponibles en Sidekick.

>[!NOTE]
>
>Los ejemplos de esta página se basan en el contenido de muestra de Geometrixx, que ya no se envía con AEM y que se ha sustituido por We.Retail. Consulte la [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

### Cuadros de diálogo básicos {#basic-dialogs}

Los cuadros de diálogo suelen utilizarse para editar contenido, pero también pueden mostrar información. Una manera fácil de ver un cuadro de diálogo completo es acceder a su representación en formato json. Para ello, dirija su explorador a:

`https://localhost:4502/<path-to-dialog>.-1.json`

El primer componente del grupo **Uso de widgets de ExtJS** en Sidekick se llama **1. Conceptos básicos del cuadro de diálogo** e incluye cuatro cuadros de diálogo básicos que se crean con widgets predeterminados y sin lógica de JavaScript personalizada. Los cuadros de diálogo se almacenan debajo de `/apps/extjstraining/components/dialogbasics`. Los cuadros de diálogo básicos son:

* Haga clic en el cuadro de diálogo Completo (nodo `full` ): muestra una ventana con tres pestañas, cada una de las cuales tiene dos campos de texto.
* Cuadro de diálogo Panel único (nodo `singlepanel`): muestra una ventana con una pestaña que tiene dos campos de texto.
* el cuadro de diálogo Varios paneles (nodo `multipanel`): su visualización es la misma que el cuadro de diálogo Completo, pero se crea de forma diferente.
* el cuadro de diálogo Diseño (nodo `design`): muestra una ventana con dos pestañas. La primera pestaña tiene un campo de texto, un menú desplegable y un área de texto contraíble. La segunda pestaña tiene un conjunto de campos con cuatro campos de texto y un conjunto de campos contraíbles con dos campos de texto.

Incluir **1. Conceptos básicos del cuadro de diálogo** componente de la página de muestra:

1. Agregar **1. Conceptos básicos del diálogo** a la página de muestra desde la ficha **Uso de widgets de ExtJS** en **Sidekick**.
1. El componente muestra un título, texto y un vínculo **PROPERTIES**. Al seleccionar el vínculo, se muestran las propiedades del párrafo almacenado en el repositorio. Vuelva a seleccionar el vínculo para ocultar las propiedades.

El componente se muestra de la siguiente manera:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Ejemplo 1: Cuadro de diálogo completo {#example-full-dialog}

El cuadro de diálogo **Completo** muestra una ventana con tres fichas, cada una con dos campos de texto. Es el cuadro de diálogo predeterminado del componente **Conceptos básicos del diálogo**. Sus características son:

* Se define mediante un nodo: node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Muestra tres fichas (tipo de nodo = `cq:Panel`).
* Cada ficha tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Se define mediante el nodo:
  `/apps/extjstraining/components/dialogbasics/full`
* Se representa en formato JSON al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

El cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Ejemplo 2: Cuadro de diálogo de panel único {#example-single-panel-dialog}

El cuadro de diálogo **Panel único** muestra una ventana con una pestaña que tiene dos campos de texto. Sus características son:

* Muestra una ficha (tipo de nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* La ficha tiene dos campos de texto (tipo de nodo = `cq:Widget`, tipo de archivo x = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* Se define mediante el nodo:
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Una ventaja con respecto al **cuadro de diálogo completo** es que se necesita menos configuración.
* Uso recomendado: para cuadros de diálogo sencillos que muestran información o solo tienen unos pocos campos.

Para usar el cuadro de diálogo Panel único:

1. Reemplace el cuadro de diálogo del componente **Conceptos básicos del cuadro de diálogo** por el cuadro de diálogo **Un solo panel**:
   1. En **CRXDE Lite**, elimine el nodo: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Haga clic en **Guardar todo** para guardar los cambios.
   1. Copie el nodo: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Pegue el nodo copiado a continuación: `/apps/extjstraining/components/dialogbasics`
   1. Seleccione el nodo: `/apps/extjstraining/components/dialogbasics/Copy of singlepanel` y renómbrelo `dialog`.
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Ejemplo 3: Cuadro de diálogo de varios paneles {#example-multi-panel-dialog}

El cuadro de diálogo **Panel múltiple** tiene la misma visualización que el cuadro de diálogo **Completo**, pero se ha creado de forma diferente. Sus características son:

* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Muestra tres fichas (tipo de nodo = `cq:Panel`).
* Cada pestaña tiene dos campos de texto (nodo type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Se define mediante la nodo:
  `/apps/extjstraining/components/dialogbasics/multipanel`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Una ventaja sobre **Full Dialog** es que tiene una estructura simplificada.
* Uso recomendado: para cuadros de diálogo de varias pestañas.

Para usar el cuadro de diálogo Varios paneles:

1. Reemplace el cuadro de diálogo del componente **Conceptos básicos del cuadro de diálogo** por el cuadro de diálogo **Panel múltiple**:
siga los pasos descritos para [Ejemplo 2: Diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Ejemplo 4: Cuadro de diálogo enriquecido {#example-rich-dialog}

El cuadro de diálogo **Enriquecido** muestra una ventana con dos fichas. La primera pestaña tiene un campo de texto, un menú desplegable y un área de texto contraíble. La segunda pestaña tiene un conjunto de campos con cuatro campos de texto y un conjunto de campos contraíbles con dos campos de texto. Sus características son:

* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra dos fichas (tipo de nodo = `cq:Panel`).
* La primera pestaña tiene un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con un widget ` [textfield](/help/sites-developing/xtypes.md#textfield)` y un widget ` [selection](/help/sites-developing/xtypes.md#selection)` con tres opciones, y un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` contraíble con un widget ` [textarea](/help/sites-developing/xtypes.md#textarea)`.
* La segunda ficha tiene un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con cuatro widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)` y un widget `dialogfieldset` contraíble con dos widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)`.
* Se define mediante el nodo:
  `/apps/extjstraining/components/dialogbasics/rich`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar el cuadro de diálogo **Rich**:

1. Reemplace el cuadro de diálogo del componente **Conceptos básicos del cuadro de diálogo** por el cuadro de diálogo **Enriquecido**:
siga los pasos descritos para [Ejemplo 2: Diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Cuadros de diálogo dinámicos {#dynamic-dialogs}

El segundo componente del grupo **Uso de widgets de ExtJS** en Sidekick se llama **2. Diálogos dinámicos** e incluye tres cuadros de diálogo dinámicos creados con widgets predeterminados y **con lógica de JavaScript personalizada**. Los cuadros de diálogo se almacenan debajo de `/apps/extjstraining/components/dynamicdialogs`. Los cuadros de diálogo dinámicos son:

* el cuadro de diálogo Cambiar fichas (nodo `switchtabs` ): muestra una ventana con dos fichas. La primera pestaña tiene una selección de opción con tres opciones: cuando se selecciona una opción, se muestra una pestaña relacionada con la opción. La segunda pestaña tiene dos campos de texto.
* el cuadro de diálogo Arbitrary (nodo `arbitrary`): muestra una ventana con una pestaña. La pestaña tiene un campo para soltar o cargar un recurso y un campo que muestra información sobre la página contenedora y sobre el recurso si se hace referencia a uno.
* Cuadro de diálogo Alternar campos (nodo `togglefield` ): muestra una ventana con una pestaña. La pestaña tiene una casilla de verificación: cuando se activa, se muestra un conjunto de campos con dos campos de texto.

Para incluir **2. Componente de cuadros de diálogo dinámicos** en la página de muestra:

1. Agregar **2. Componente de cuadros de diálogo dinámicos** a la página de muestra desde la ficha **Uso de widgets de ExtJS** en **Sidekick**.
1. El componente muestra un título, texto y un vínculo **PROPERTIES**. Al seleccionar el vínculo, se muestran las propiedades del párrafo almacenado en el repositorio. Vuelva a seleccionar el vínculo para ocultar las propiedades.

El componente se muestra de la siguiente manera:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Ejemplo 1: Cuadro de diálogo Cambiar fichas {#example-switch-tabs-dialog}

El cuadro de diálogo **Cambiar fichas** muestra una ventana con dos fichas. La primera pestaña tiene una selección de opción con tres opciones: cuando se selecciona una opción, se muestra una pestaña relacionada con la opción. La segunda pestaña tiene dos campos de texto.

Sus principales características son:

* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra dos fichas (tipo de nodo = `cq:Panel`): una ficha de selección y la segunda ficha depende de la selección de la primera ficha (tres opciones).
* Tiene tres fichas opcionales (tipo de nodo = `cq:Panel`), cada una tiene dos campos de texto (tipo de nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Solo se muestra una pestaña opcional a la vez.
* Definido por el nodo `switchtabs` en:
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* El nodo de diálogo tiene un detector &quot; `beforeshow`&quot; que oculta todas las pestañas opcionales antes de que se muestre el cuadro de diálogo:
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` obtiene `tabpanel` que contiene el panel de selección y los tres paneles opcionales.
* El objeto `Ejst.x2` se define en el archivo `exercises.js` en:
  `/apps/extjstraining/clientlib/js/exercises.js`
* En el método `Ejst.x2.manageTabs()`, como el valor de `index` es -1, todas las fichas opcionales están ocultas (va del 1 al 3).
* La ficha de selección tiene dos agentes de escucha: uno que muestra la ficha seleccionada cuando se carga el cuadro de diálogo (evento &quot; `loadcontent`&quot;) y otro que muestra la ficha seleccionada cuando se cambia la selección (evento &quot; `selectionchanged`&quot;):
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Para el método `Ejst.x2.showTab()`,
  `field.findParentByType('tabpanel')` obtiene `tabpanel` que contiene todas las fichas ( `field` representa el widget de selección)
  `field.getValue()` obtiene el valor de la selección, por ejemplo, tab2
  `Ejst.x2.manageTabs()` muestra la ficha seleccionada.
* Cada ficha opcional tiene un agente de escucha que oculta la ficha en el evento &quot; `render`&quot;:
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Para el método `Ejst.x2.hideTab()`,
  `tabPanel` es el `tabpanel` que contiene todas las fichas
  `index` es el índice del pestaña opcional
  `tabPanel.hideTabStripItem(index)` oculta el pestaña

Se muestra de la siguiente manera:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Ejemplo 2: Diálogo arbitrario {#example-arbitrary-dialog}

A menudo, un cuadro de diálogo muestra el contenido del componente subyacente. El cuadro de diálogo que se describe aquí, denominado **Cuadro de diálogo arbitrario**, extrae contenido de un componente diferente.

El cuadro de diálogo **Arbitrario** muestra una ventana con una pestaña. La pestaña tiene dos campos: uno para soltar o cargar un recurso y otro que muestra información sobre la página contenedora y sobre el recurso si se ha hecho referencia a uno.

Sus principales características son:

* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra un widget `tabpanel` (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) con un panel (tipo de nodo = `cq:Panel`)
* El panel tiene un widget de archivo inteligente (tipo de nodo = `cq:Widget`, tipo de archivo x = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) y un widget de dibujo propietario (tipo de nodo = `cq:Widget`, tipo de archivo x = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* Definido por el nodo `arbitrary` en:
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* El widget `ownerdraw` tiene un detector &quot;`loadcontent`&quot; que muestra información sobre la página que contiene el componente. Es decir, el recurso al que hace referencia el widget smartfile cuando se carga el contenido:
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` se ha establecido con el objeto `ownerdraw`
  `path` se ha establecido con la ruta de contenido del componente (por ejemplo, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* El objeto `Ejst.x2` se define en el archivo `exercises.js` en:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Para el método `Ejst.x2.showInfo()`,
  `pagePath` es la ruta de acceso de la página que contiene el componente;
  `pageInfo` representa las propiedades de la página en formato json;
  `reference` es la ruta del recurso al que se hace referencia;
  `metadata` representa los metadatos del recurso en formato json;
  `ownerdraw.getEl().update(html);` muestra el html creado en el cuadro de diálogo

Para usar el cuadro de diálogo **Arbitrario**:

1. Reemplazar el cuadro de diálogo del componente Diálogo **dinámico con el** cuadro de **diálogo arbitrario**:
seguir los pasos descritos para el Ejemplo 2: Cuadro de [diálogo de panel único](#example-single-panel-dialog)
1. Editar el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Ejemplo 3: Cuadro de diálogo Alternar campos {#example-toggle-fields-dialog}

El cuadro de diálogo **Alternar campos** muestra una ventana con una pestaña. El pestaña tiene una casilla de verificación: cuando está marcada, se muestra un conjunto de campos con dos campos de texto.

Sus principales características son:

* Se define mediante una nodo (nodo type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra un `tabpanel` widget (nodo type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) con un panel (nodo type = `cq:Panel`).
* El panel tiene un widget de selección/casilla de verificación (nodo type = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) y un widget dialogfieldset plegable (nodo type = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que se oculta de forma predeterminada, con dos widgets de campo de texto (nodo type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Definido por el nodo `togglefields` en:
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

La lógica se implementa mediante detectores de eventos y código JavaScript de la siguiente manera:

* la ficha selección tiene dos agentes de escucha: uno que muestra el conjunto de campos de diálogo cuando se carga el contenido (evento &quot; `loadcontent`&quot;) y otro que muestra el conjunto de campos de diálogo cuando se cambia la selección (evento &quot; `selectionchanged`&quot;):
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* El objeto `Ejst.x2` se define en el archivo `exercises.js` en:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Para el método `Ejst.x2.toggleFieldSet()`,
  `box` es el objeto de selección;
  `panel` es el panel que contiene la selección y los widgets dialogfieldset;
  `fieldSet` es el objeto dialogfieldset;
  `show` es el valor de la selección (verdadero o falso);
basado en &#39; `show`&#39;, el conjunto de campos de diálogo se muestra o no

Para usar el cuadro de diálogo **Alternar campos**, haga lo siguiente:

1. Reemplace el cuadro de diálogo del componente **Diálogo dinámico** por el cuadro de diálogo **Alternar campos**:
siga los pasos descritos para [Ejemplo 2: Diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Los widgets listos para usar que se envían con AEM deben cubrir la mayoría de los casos de uso. Sin embargo, a veces puede ser necesario crear un widget personalizado para cubrir un requisito específico de un proyecto. Se pueden crear widgets personalizados ampliando los existentes. Para ayudarle a empezar con esta personalización, el paquete **`Using ExtJS Widgets`** incluye tres cuadros de diálogo que utilizan tres widgets personalizados diferentes:

* el cuadro de diálogo Varios campos (nodo `multifield` ) muestra una ventana con una pestaña. La pestaña tiene un widget de varios campos personalizado que tiene dos campos: un menú desplegable con dos opciones y un campo de texto. Como se basa en el widget `multifield` incorporado (que solo tiene un campo de texto), tiene todas las características del widget `multifield`.
* el cuadro de diálogo Examinar árbol (nodo `treebrowse` ) muestra una ventana con una pestaña que contiene un widget de exploración de rutas: al hacer clic en la flecha, se abre una ventana en la que puede examinar una jerarquía y seleccionar un elemento. A continuación, la ruta del elemento se agrega al campo de ruta y se mantiene cuando se cierra el cuadro de diálogo.
* un cuadro de diálogo basado en el complemento Editor de texto enriquecido (nodo `rteplugin` ) que agrega un botón personalizado al Editor de texto enriquecido para insertar texto personalizado en el texto principal. Consiste en un widget `richtext` (RTE) y una característica personalizada que se agrega a través del mecanismo de complemento RTE.

Los widgets personalizados y el complemento están incluidos en el componente denominado **3. Widgets personalizados del** paquete Using ExtJS Widgets.**&#x200B;** Para incluir este componente en la Página de ejemplo:

1. añadir el **3. Componente Widgets** personalizados al Página de muestra de la **pestaña Uso de widgets de** ExtJS en la **barra de tareas**.
1. El componente muestra un título, texto y, al hacer clic en el **vincular PROPIEDADES** , las propiedades del párrafo almacenadas en el repositorio. Al volver a hacer clic en se ocultan las propiedades.
El componente se muestra de la siguiente manera:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Ejemplo 1: Widget multicampo personalizado {#example-custom-multifield-widget}

El cuadro de diálogo **Multicampo personalizado** basado en widgets muestra una ventana con una pestaña. La pestaña tiene un widget de varios campos personalizado que, a diferencia del estándar que tiene un campo, tiene dos campos: un menú desplegable con dos opciones y un campo de texto.

El cuadro de diálogo **Multicampo personalizado** basado en widgets:

* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra un widget `tabpanel` (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) que contiene un panel (tipo de nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un widget `multifield` (tipo de nodo = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* El widget `multifield` tiene un elemento fieldconfig (tipo de nodo = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) basado en el elemento xtype personalizado &#39; `ejstcustom`&#39;:
   * `fieldconfig` es una opción de configuración del objeto ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)`.
   * &#39; `optionsProvider`&#39; es una configuración del widget `ejstcustom`. Se configura con el método `Ejst.x3.provideOptions` que se define en `exercises.js` en:

     `/apps/extjstraining/clientlib/js/exercises.js`
y devuelve dos opciones.
* Definido por el nodo `multifield` en:
  `/apps/extjstraining/components/customwidgets/multifield`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

El widget personalizado `multifield` (xtype = `ejstcustom`):

* Es un objeto de JavaScript llamado `Ejst.CustomWidget`
* Se define en el archivo JavaScript `CustomWidget.js` en:
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Amplía el widget ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)`.
* Tiene tres campos: `hiddenField` (Campo de texto), `allowField` (Cuadro combinado) y `otherField` (Campo de texto)
* Anula `CQ.Ext.Component#initComponent` para agregar los tres campos:
   * `allowField` es un objeto [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) de tipo &#39;select&#39;. optionsProvider es una configuración del objeto Selection que se crea una instancia con la configuración optionsProvider del CustomWidget definido en el cuadro de diálogo
   * `otherField` es un objeto [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)
* Anula los métodos `setValue`, `getValue`, y `getRawValue` de [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) para establecer y recuperar el valor de CustomWidget con el formato:
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* Se registra como &#39;`ejstcustom`&#39; xtype:
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

El cuadro de diálogo **Multicampo personalizado** basado en widgets se muestra de la siguiente manera:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Ejemplo 2: Widget personalizada `Treebrowse` {#example-custom-treebrowse-widget}

El cuadro de diálogo basado en widgets personalizados **`Treebrowse`** muestra una ventana con una pestaña que contiene un widget de exploración de ruta personalizado. Cuando selecciona la flecha, se abre una ventana en la que puede examinar un jerarquía y seleccionar un elemento. La ruta del elemento se agrega entonces al campo de ruta y se mantiene cuando se cierra el cuadro de diálogo.

El cuadro de diálogo personalizado `treebrowse` :

* Se define mediante una nodo (nodo type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Muestra un widget `tabpanel` (tipo de nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) que contiene un panel (tipo de nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un widget personalizado (tipo de nodo = `cq:Widget`, xtype = `ejstbrowse`)
* Definido por el nodo `treebrowse` en:
  `/apps/extjstraining/components/customwidgets/treebrowse`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

El widget de exploración del árbol personalizado (xtype = `ejstbrowse`):

* Es un objeto de JavaScript llamado `Ejst.CustomWidget`
* Se define en el archivo JavaScript `CustomBrowseField.js` en:
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Extiende ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define una ventana de exploración llamada `browseWindow`.
* Invalida ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar la ventana de exploración cuando se hace clic en la flecha.
* Define un objeto [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel):
   * Obtiene sus datos llamando al servlet registrado en `/bin/wcm/siteadmin/tree.json`.
   * Su raíz es &quot; `apps/extjstraining`&quot;.
* Define un objeto `window` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Basado en el panel predefinido.
   * Tiene un botón **Aceptar** que establece el valor de la ruta seleccionada y oculta el panel.
* La ventana está anclada debajo del campo **Ruta**.
* La ruta seleccionada se pasa del campo de exploración a la ventana en el evento `show`.
* Se registra como &#39;`ejstbrowse`&#39; xtype:
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar el cuadro de diálogo **Examen de árbol personalizado** basado en widgets:

1. Reemplace el cuadro de diálogo del componente **Widgets personalizados** por el cuadro de diálogo **Examen de árbol personalizado**:
siga los pasos descritos para [Ejemplo 2: Diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente: el cuadro de diálogo se muestra de la siguiente manera:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Ejemplo 3: Complemento del editor de texto enriquecido (RTE) {#example-rich-text-editor-rte-plug-in}

El **cuadro de diálogo basado en el complemento Editor de texto enriquecido (RTE) es un cuadro de diálogo basado en** el editor de texto enriquecido que tiene un botón personalizado para insertar texto personalizado entre corchetes. El texto personalizado puede analizarse mediante alguna lógica del lado del servidor (no implementada en este ejemplo), por ejemplo, para agregar texto definido en la ruta dada:

El **cuadro de diálogo basado en plug-in** RTE:

* Se define mediante el nodo reteplugin en:
  `/apps/extjstraining/components/customwidgets/rteplugin`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* El nodo `rtePlugins` tiene un nodo secundario `inserttext` (tipo de nodo = `nt:unstructured`) con el nombre del complemento. Tiene una propiedad denominada `features` que define qué características del complemento están disponibles para RTE.

El complemento RTE:

* Es un objeto de JavaScript llamado `Ejst.InsertTextPlugin`
* Se define en el archivo JavaScript `InsertTextPlugin.js` en:
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Extiende el objeto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`.
* Los siguientes métodos definen el objeto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` y se anulan en el complemento de implementación:
   * `getFeatures()` devuelve una matriz de todas las características que el complemento pone a disposición.
   * `initializeUI()` agrega el nuevo botón a la barra de herramientas RTE.
   * `notifyPluginConfig()` muestra título y texto cuando se pasa el ratón por encima del botón.
   * Se llama a `execute()` cuando se hace clic en el botón y realiza la acción del complemento: muestra una ventana que se utiliza para definir el texto que se va a incluir.
* `insertText()` inserta un texto usando el objeto de diálogo correspondiente `Ejst.InsertTextPlugin.Dialog` (ver más adelante).
* El método `apply()` del cuadro de diálogo llama a `executeInsertText()`, que se activa cuando se hace clic en el botón **Aceptar**.
* Se registra como complemento &#39; `inserttext`&#39;:
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* el objeto `Ejst.InsertTextPlugin.Dialog` define el cuadro de diálogo que se abre cuando se hace clic en el botón del complemento. El cuadro de diálogo consta de un panel, un formulario, un campo de texto y dos botones (**Aceptar** y **Cancelar**).

Para usar el cuadro de diálogo basado en el complemento **Editor de texto enriquecido (RTE)**:

1. Reemplace el cuadro de diálogo del componente **Widgets personalizados** por el cuadro de diálogo basado en el complemento **Editor de texto enriquecido (RTE)**:
siga los pasos descritos para [Ejemplo 2: Diálogo de panel único](#example-single-panel-dialog)
1. Edite el componente.
1. Haga clic en el último icono de la derecha (el que tiene cuatro flechas). Escriba una ruta y haga clic en **Aceptar**:
La ruta se muestra entre corchetes ([ ]).
1. Haz clic en **Aceptar** para cerrar el Editor de texto enriquecido.

El **cuadro de diálogo basado en** el complemento Editor de texto enriquecido (RTE) muestra lo siguiente:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este ejemplo solo muestra cómo implementar la parte lado del cliente de la lógica: los marcadores de posición (*[texto]*) deben analizarse en el del lado del servidor explícitamente (por ejemplo, en el componente JSP).

### Resumen de árbol {#tree-overview}

El objeto ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` predeterminado proporciona una representación de la interfaz de usuario estructurada por árbol de los datos estructurados por árbol. El componente Descripción general del árbol incluido en el **paquete Using ExtJS Widgets muestra cómo utilizar el `TreePanel` objeto para mostrar un árbol JCR debajo de** una ruta determinada. La ventana en sí se puede acoplar / desacoplar. En este ejemplo, la lógica de ventana está incrustada en el componente jsp entre &lt;script> etiquetas.

Para incluir el componente Información general **de**&#x200B;árbol en la Página de muestra:

1. añadir el **4. Componente Información general** del árbol a la Página de muestra de la **pestaña Uso de widgets de** ExtJS en la **barra de tareas**.
1. El componente muestra:
   * un título, con texto
   * un vínculo **PROPERTIES**: haga clic en para mostrar las propiedades del párrafo almacenado en el repositorio. Haga clic en de nuevo para ocultar las propiedades.
   * una ventana flotante con una representación en árbol del repositorio que se puede expandir.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

El componente Información general de árbol:

* Se define en:
  `/apps/extjstraining/components/treeoverview`

* El cuadro de diálogo le permite establecer el tamaño de la ventana y acoplarla o desacoplarla (consulte los detalles a continuación).

El componente jsp:

* Recupera las propiedades de anchura, altura y acoplamiento del repositorio.
* Muestra texto sobre el formato de datos de información general de árbol.
* Incrusta la lógica de ventana en el componente jsp entre las etiquetas de JavaScript.
* Se define en:
  `apps/extjstraining/components/treeoverview/content.jsp`

El código JavaScript incrustado en el componente jsp:

* Define un objeto `tree` al intentar recuperar una ventana de árbol de la página.
* Si la ventana que muestra el árbol no existe, se crea `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` contiene los datos utilizados para crear la ventana.
   * Los datos se recuperan llamando al servlet registrado en:

     `/bin/wcm/siteadmin/tree.json`
* El agente de escucha `beforeload` se asegura de que se ha cargado el nodo seleccionado.
* El objeto `root` establece la ruta de acceso `apps/extjstraining` como raíz de árbol.
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) se ha establecido en función del valor predefinido `treePanel` y se muestra con:
  `tree.show();`
* Si la ventana existe, se muestra en función de las propiedades de anchura, altura y acoplamiento recuperadas del repositorio.

El cuadro de diálogo de componentes:

* Muestra una pestaña con dos campos para establecer el tamaño (ancho y alto) de la ventana de información general del árbol y un campo para acoplar/desacoplar la ventana
* Se define mediante un nodo (tipo de nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* El panel tiene un widget de campo de tamaño (tipo de nodo = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) y un widget de selección (tipo de nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`) con dos opciones (true/false)
* Se define mediante el nodo de diálogo en:
  `/apps/extjstraining/components/treeoverview/dialog`
* Se representa en formato json al solicitar:
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Se muestra de la siguiente manera:

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Resumen de cuadrícula {#grid-overview}

Un panel Cuadrícula representa los datos en un formato tabular de filas y columnas. Se compone de lo siguiente:

* Almacén: el modelo que contiene los registros de datos (filas).
* Modelo de columna : el diseño de la columna.
* Vista : encapsula la interfaz de usuario.
* Modelo de selección : el comportamiento de selección.

El componente Información general de cuadrícula incluido en el paquete **Uso de widgets de ExtJS** muestra cómo mostrar datos en formato de tabla:

* El ejemplo 1 utiliza datos estáticos.
* El ejemplo 2 utiliza datos recuperados del repositorio.

Para incluir el componente Información general de cuadrícula en la página de muestra:

1. Agregar **5. Componente Información general de cuadrícula** a la página de muestra desde la ficha **Uso de widgets de ExtJS** en **Sidekick**.
1. El componente muestra:
   * un título con texto
   * un vínculo **PROPERTIES**: haga clic en para mostrar las propiedades del párrafo almacenado en el repositorio. Haga clic en de nuevo para ocultar las propiedades.
   * ventana flotante que contiene datos en formato tabular.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Ejemplo 1: Cuadrícula predeterminada {#example-default-grid}

En su versión predeterminada, el **componente Información general** de cuadrícula muestra una ventana con datos estáticos en un formato tabular. En este ejemplo, la lógica está integrada en el componente jsp de dos maneras:

* La lógica genérica se define entre &lt;script> etiquetas
* la lógica específica está disponible en un archivo .js independiente y se vincula a en el jsp. Esta configuración le permite alternar entre las dos lógicas (estáticas y dinámicas) comentando las etiquetas &lt;script> que desee.

El componente Información general de cuadrícula:

* Se define en:
  `/apps/extjstraining/components/gridoverview`
* El cuadro de diálogo permite establecer el tamaño de la ventana y acoplar o desacoplar la ventana.

El componente jsp:

* Recupera las propiedades de anchura, altura y acoplamiento del repositorio.
* Muestra texto como introducción al formato de datos generales de la cuadrícula.
* Hace referencia al código JavaScript que define el objeto GridPanel:
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` define algunos datos estáticos como base para el objeto GridPanel.
* Incrusta código JavaScript entre etiquetas JavaScript que define el objeto Window que consume el objeto GridPanel.
* Se define en:
  `apps/extjstraining/components/gridoverview/content.jsp`

El código JavaScript incrustado en el componente jsp:

* Define el objeto `grid` al intentar recuperar el componente de ventana de la página:
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Si `grid` no existe, se define un objeto [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) llamando al método `getGridPanel()` (ver a continuación). Este método está definido en `defaultgrid.js`.
* `grid` es un objeto ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`, basado en el GridPanel predefinido, y se muestra: `grid.show();`
* Si `grid` existe, se muestra en función de la anchura, la altura y las propiedades de acoplamiento recuperadas del repositorio.

El archivo JavaScript (`defaultgrid.js`) al que se hace referencia en el componente jsp define el método `getGridPanel()` al que llama el script incrustado en el JSP y devuelve un objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, basado en datos estáticos. La lógica es la siguiente:

* `myData` es una matriz de datos estáticos formateados como una tabla de cinco columnas y cuatro filas.
* `store` es un objeto `CQ.Ext.data.Store` que consume `myData`.
* `store` se ha cargado en la memoria:
  `store.load();`
* `gridPanel` es un objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` que consume `store`:
   * las anchuras de columna siempre se redimensionan:

     `forceFit: true`
   * solo se puede seleccionar una fila a la vez:

     `singleSelect:true`

#### Ejemplo 2: Cuadrícula de búsqueda de referencia {#example-reference-search-grid}

Al instalar el paquete, `content.jsp` del componente **Información general de cuadrícula** muestra una cuadrícula basada en datos estáticos. Es posible modificar el componente para mostrar una cuadrícula con las siguientes características:

* Tiene tres columnas.
* Se basa en los datos recuperados del repositorio mediante una llamada a un servlet.
* Las celdas de la última columna se pueden editar. El valor se mantiene en una propiedad `test` debajo del nodo definido por la ruta mostrada en la primera columna.

Como se explica en la sección anterior, el objeto window obtiene su objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` llamando al método `getGridPanel()` definido en el archivo `defaultgrid.js` en `/apps/extjstraining/components/gridoverview/defaultgrid.js`. El componente **Información general de cuadrícula &#x200B;** proporciona una implementación diferente para el método `getGridPanel()`, definido en el archivo `referencesearch.js` en `/apps/extjstraining/components/gridoverview/referencesearch.js`. Al cambiar el archivo .js al que se hace referencia en el componente jsp, la cuadrícula se basa en los datos recuperados del repositorio.

Cambie el archivo .js al que se hace referencia en el componente jsp:

1. En **CRXDE Lite**, en el archivo `content.jsp` del componente, comente la línea que incluye el archivo `defaultgrid.js`, de modo que tenga el siguiente aspecto:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Quite el comentario de la línea que incluye el archivo `referencesearch.js`, de modo que tenga el siguiente aspecto:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Guarde los cambios.
1. Actualice la página de muestra.

El componente se muestra de la siguiente manera:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

El código JavaScript al que se hace referencia en el jsp del componente (`referencesearch.js`) define el método `getGridPanel()` al que se llama desde el jsp del componente y devuelve un objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, basado en los datos que se recuperan dinámicamente del repositorio. La lógica de `referencesearch.js` define algunos datos dinámicos como base para GridPanel:

* `reader` es un objeto ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`que lee la respuesta del servlet en formato json para tres columnas.
* `cm` es un objeto ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` para tres columnas.
Las celdas de la columna &quot;Prueba&quot; se pueden editar tal como se definen con un editor:
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* las columnas se pueden ordenar:
  `cm.defaultSortable = true;`
* `store` es un objeto ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)`:
   * obtiene sus datos llamando al servlet registrado en &quot;`/bin/querybuilder.json`&quot; con algunos parámetros utilizados para filtrar la consulta
   * se basa en `reader`, definido previamente
   * la tabla se ordena de acuerdo con la columna &#39;**jcr:path**&#39; en orden ascendente
* `gridPanel` es un objeto ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` que se puede editar:
   * se basa en el `store` predefinido y en el modelo de columna `cm`
   * solo se puede seleccionar una fila a la vez:

     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * el agente de escucha `afteredit` se asegura de que después de editar una celda de la columna &quot;**Test**&quot;:
      * la propiedad &#39;`test`&#39; del nodo en la ruta definida por la columna &quot;**jcr:path**&quot; se establece en el repositorio con el valor de la celda
      * si el POST se realiza correctamente, el valor se agrega al objeto `store`; de lo contrario, se rechaza
