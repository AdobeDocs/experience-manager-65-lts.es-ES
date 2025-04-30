---
title: Desarrollo de componentes de AEM
description: Los componentes de AEM se utilizan para mantener, dar formato y representar el contenido disponible en las páginas web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: ff9c9e25-13a8-4ca7-a347-1da1352ef223
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '3200'
ht-degree: 0%

---

# Desarrollo de componentes de AEM{#developing-aem-components}

Los componentes de AEM se utilizan para mantener, dar formato y representar el contenido disponible en las páginas web.

* Al [crear páginas](/help/sites-authoring/default-components.md), los componentes permiten a los autores editar y configurar el contenido.

* En la instancia de publicación, los componentes procesan el contenido y lo presentan a los visitantes del sitio web según sea necesario.

>[!NOTE]
>
>Esta página es una continuación del documento [Componentes de AEM - Conceptos básicos](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Los componentes por debajo de `/libs/cq/gui/components/authoring/dialog` están pensados para utilizarse solamente en el Editor (cuadros de diálogo de componentes en Creación). Si se utilizan en otra parte (por ejemplo, en un cuadro de diálogo del asistente), es posible que no se comporten según lo esperado.

## Ejemplos de código {#code-samples}

Esta página proporciona la documentación de referencia (o vínculos a la documentación de referencia) necesaria para desarrollar nuevos componentes para AEM. Consulte [Desarrollo de componentes de AEM: ejemplos de código](/help/sites-developing/developing-components-samples.md) para ver algunos ejemplos prácticos.

## Estructura {#structure}

La estructura básica de un componente se explica en la página [Componentes de AEM: conceptos básicos](/help/sites-developing/components-basics.md#structure). Ese documento abarca tanto las IU táctiles como las clásicas. Aunque no necesite utilizar la configuración clásica en el nuevo componente, puede resultar útil tenerlos en cuenta al heredar de componentes existentes.

## Ampliación de componentes y cuadros de diálogo existentes {#extending-existing-components-and-dialogs}

Según el componente que desee implementar, podría ser posible extender o personalizar una instancia existente, en lugar de definir y desarrollar toda la [estructura](#structure) desde cero.

Al ampliar o personalizar un componente o cuadro de diálogo existente, puede copiar o replicar toda la estructura o la estructura necesaria para el cuadro de diálogo antes de realizar los cambios.

### Ampliación de un componente existente {#extending-an-existing-component}

Se puede ampliar un componente existente con [Jerarquía de tipos de recursos](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) y los mecanismos de herencia relacionados.

>[!NOTE]
>
>Los componentes también se pueden redefinir con una superposición basada en la lógica de ruta de búsqueda. Sin embargo, en tal caso, la [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) no se activa y `/apps` debe definir toda la superposición.

>[!NOTE]
>
>El [componente de fragmento de contenido](/help/sites-developing/customizing-content-fragments.md) también se puede personalizar y ampliar, aunque se deben tener en cuenta la estructura completa y las relaciones con Assets.

### Cuadro de diálogo Personalizar un componente existente {#customizing-a-existing-component-dialog}

También es posible anular un *cuadro de diálogo de componentes* mediante la [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y la definición de la propiedad `sling:resourceSuperType`.

Esto significa que solo necesita redefinir las diferencias necesarias, en lugar de redefinir todo el cuadro de diálogo (con `sling:resourceSuperType`). Este método se recomienda ahora para ampliar el cuadro de diálogo de un componente

Consulte la [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) para obtener más información.

## Definición del marcado {#defining-the-markup}

El componente se procesará con [HTML](https://www.w3schools.com/htmL/html_intro.asp). El componente debe definir el HTML necesario para tomar el contenido necesario y luego procesarlo según sea necesario, en los entornos de creación y publicación.

### Uso del lenguaje de plantilla de HTML {#using-the-html-template-language}

El [lenguaje de plantilla HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es), introducido con AEM 6.0, sustituye a JSP (JavaServer Pages) como sistema de plantillas preferido y recomendado en el lado del servidor para HTML. Para los desarrolladores web que necesitan crear sitios web empresariales sólidos, HTL les ayuda a lograr una mayor seguridad y eficacia en el desarrollo.

>[!NOTE]
>
>Aunque HTL y JSP se pueden utilizar para desarrollar componentes, ilustraremos el desarrollo con HTL en esta página, ya que es el lenguaje de script recomendado para AEM.

## Desarrollo de la lógica de contenido {#developing-the-content-logic}

Esta lógica opcional selecciona o calcula el contenido que se procesará. Se invoca desde expresiones HTL con el patrón de API de uso adecuado.

El mecanismo para separar la lógica de la apariencia ayuda a aclarar lo que se necesita para una vista determinada. También permite una lógica diferente para diferentes vistas del mismo recurso.

### Uso de Java {#using-java}

[La API de uso de Java de HTL permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). Esto permite utilizar código Java para implementar la lógica de selección y configuración del contenido del componente.

### Uso de JavaScript {#using-javascript}

[La API de uso de JavaScript de HTL permite que un archivo HTL acceda al código de ayuda escrito en JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). Esto permite utilizar código JavaScript para implementar la lógica de selección y configuración del contenido del componente.

### Uso de bibliotecas HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Lea [Uso de bibliotecas HTML del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente, incluidos atributos como las acciones disponibles para el componente, las características del editor local y los oyentes relacionados con los eventos del componente. La configuración es común tanto a la IU táctil como a la clásica, aunque con ciertas diferencias específicas.

El comportamiento de edición [de un componente se ha configurado](/help/sites-developing/components-basics.md#edit-behavior) agregando un nodo `cq:editConfig` de tipo `cq:EditConfig` debajo del nodo de componente (de tipo `cq:Component`) y agregando propiedades específicas y nodos secundarios.

## Configuración del comportamiento de vista previa {#configuring-the-preview-behavior}

La cookie [WCM Mode](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/WCMMode.html) se establece al cambiar al modo **Preview** aunque la página no se haya actualizado.

Para los componentes con una renderización sensible al modo WCM, deben definirse para actualizarse específicamente y, a continuación, basarse en el valor de la cookie.

>[!NOTE]
>
>En la IU táctil, solo se usan los valores `EDIT` y `PREVIEW` para la cookie [Modo WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Creación y configuración de un cuadro de diálogo {#creating-and-configuring-a-dialog}

Los cuadros de diálogo se utilizan para permitir que el autor interactúe con el componente. El uso de un cuadro de diálogo permite a los autores o administradores editar contenido, configurar el componente o definir parámetros de diseño (mediante un [Cuadro de diálogo de diseño](#creating-and-configuring-a-design-dialog))

### IU de Coral e IU de Granite {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) y [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) definen la apariencia moderna de AEM.

[Granite UI proporciona una amplia gama de componentes básicos (widgets)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) necesarios para crear el cuadro de diálogo en el entorno de creación. Si es necesario, puede ampliar esta selección y [crear su propio widget](#creatinganewwidget).

Para obtener información detallada, consulte:

* IU de Coral

   * Proporciona una IU coherente en todas las soluciones de nube
   * [Conceptos de la IU táctil de AEM: interfaz de usuario de Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guía de Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite UI

   * Proporciona marcado de la IU de Coral envuelto en componentes de Sling para crear consolas y cuadros de diálogo de IU
   * [Conceptos de la interfaz de usuario táctil de AEM: Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>Debido a la naturaleza de los componentes de Granite UI (y a las diferencias con los widgets de ExtJS), existen algunas diferencias entre la forma en que los componentes interactúan con la interfaz de usuario táctil y [Classic UI](/help/sites-developing/developing-components-classic.md).

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Cuadros de diálogo para la IU táctil:

* se denominan `cq:dialog`.
* se definen como un nodo `nt:unstructured` con la propiedad `sling:resourceType` establecida.

* se encuentran bajo su nodo `cq:Component` y junto a su definición de componente.
* se representan en el servidor (como componentes de Sling), según su estructura de contenido y la propiedad `sling:resourceType`.
* Utilice el marco de trabajo de Granite UI.
* contiene una estructura de nodos que describe los campos del cuadro de diálogo.

   * estos nodos son `nt:unstructured` con la propiedad `sling:resourceType` requerida.

Un ejemplo de estructura de nodos puede ser:

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

La personalización de un cuadro de diálogo es similar a desarrollar un componente, ya que el cuadro de diálogo es en sí mismo un componente (es decir, marcado procesado por un script de componente junto con el comportamiento/estilo proporcionado por una biblioteca de cliente).

Para ver ejemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Si un componente no tiene ningún cuadro de diálogo definido para la IU táctil, el cuadro de diálogo de la IU clásica se utiliza como alternativa dentro de una capa de compatibilidad. Para personalizar un cuadro de diálogo de este tipo, debe personalizar el cuadro de diálogo IU clásica. Consulte [Componentes de AEM para la IU clásica](/help/sites-developing/developing-components-classic.md).

### Personalización de campos de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* la sesión de AEM Gems en [Personalizar campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
>* el código de ejemplo relacionado que se cubre en [Ejemplo de código: Cómo personalizar los campos de diálogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Creación de un nuevo campo {#creating-a-new-field}

Los widgets para la interfaz de usuario táctil se implementan como componentes de la interfaz de usuario de Granite.

Para crear un widget para utilizarlo en un cuadro de diálogo de componentes para la IU táctil, es necesario que [cree un componente de campo de Granite UI](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Para obtener información detallada acerca de Granite UI, consulte la [documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Si considera el cuadro de diálogo como un contenedor simple para un elemento de formulario, también puede ver el contenido principal del cuadro de diálogo como campos de formulario. La creación de un campo de formulario requiere la creación de un tipo de recurso; esto equivale a la creación de un componente. Para ayudarle en esa tarea, la interfaz de usuario de Granite ofrece un componente de campo genérico del que heredar (con `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Más específicamente, la interfaz de usuario de Granite proporciona una amplia gama de componentes de campo que son adecuados para su uso en cuadros de diálogo (o, más generalmente, en [formularios](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Esto difiere de la IU clásica, donde los widgets están representados por `cq:Widgets` nodos, cada uno con un `xtype` en particular para establecer la relación con su widget ExtJS correspondiente. Desde el punto de vista de la implementación, el marco de ExtJS representó estos widgets del lado del cliente.

Una vez creado el tipo de recurso, puede crear una instancia del campo agregando un nuevo nodo en el cuadro de diálogo, con la propiedad `sling:resourceType` que hace referencia al tipo de recurso que acaba de introducir.

#### Crear una biblioteca de cliente para el estilo y el comportamiento {#creating-a-client-library-for-style-and-behavior}

Si desea definir el estilo y el comportamiento del componente, puede crear una [biblioteca de cliente](/help/sites-developing/clientlibs.md) dedicada que defina CSS/LESS y JS personalizados.

Para que la biblioteca de cliente se cargue únicamente para el cuadro de diálogo de componentes (es decir, no se cargará para otro componente), debe establecer la propiedad `extraClientlibs` del cuadro de diálogo en el nombre de categoría de la biblioteca de cliente que ha creado. Esto es aconsejable si la biblioteca de cliente es bastante grande o si el campo es específico de ese cuadro de diálogo y no es necesario en otros cuadros de diálogo.

Para que se cargue la biblioteca de cliente para todos los cuadros de diálogo, establezca la propiedad category de la biblioteca de cliente en `cq.authoring.dialog`. Es el nombre de categoría de la biblioteca de cliente que se incluye de forma predeterminada al procesar todos los cuadros de diálogo. Desea hacerlo si la biblioteca de cliente es pequeña o si el campo es genérico y se puede reutilizar en otros cuadros de diálogo.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * proporcionado por [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ampliación (herencia) de un campo {#extending-inheriting-from-a-field}

Según sus necesidades, puede hacer lo siguiente:

* Ampliar un campo de IU de Granite determinado mediante la herencia de componentes ( `sling:resourceSuperType`)
* Amplíe un widget determinado desde la biblioteca de widgets subyacente (si hay una interfaz de usuario de Granite, es la interfaz de usuario de Coral), siguiendo la API de biblioteca de widgets (herencia JS/CSS)

#### Acceso a campos de diálogo {#access-to-dialog-fields}

También puede utilizar condiciones de procesamiento (`rendercondition`) para controlar quién tiene acceso a fichas/campos específicos del cuadro de diálogo; por ejemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestión de eventos de campo {#handling-field-events}

El método de administrar eventos en campos de diálogo ahora se realiza con [oyentes en una biblioteca de cliente personalizada](#listeners-in-a-custom-client-library). Esto supone un cambio con respecto al método anterior de tener [oyentes en la estructura de contenido](#listenersinthecontentstructureclassicui).

#### Escuchadores en una biblioteca de cliente personalizada {#listeners-in-a-custom-client-library}

Para introducir lógica en el campo, debe:

1. Marque su campo con una clase CSS determinada (el *vínculo*).
1. Defina en la biblioteca de cliente un oyente JS conectado a ese nombre de clase CSS (esto garantiza que la lógica personalizada solo está vinculada al campo y no afecta a otros campos del mismo tipo).

Para conseguirlo, debe conocer la biblioteca de widgets subyacente con la que desea interactuar. Consulte la [documentación de la interfaz de usuario de Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) para identificar a qué evento desea reaccionar. Esto es muy similar al proceso que tuvo que realizar con ExtJS en el pasado: busque la página de documentación de un widget determinado y, a continuación, compruebe los detalles de su API de evento.

Para ver un ejemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * proporcionado por [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Oyentes en la estructura de contenido {#listeners-in-the-content-structure}

En la IU clásica con ExtJS, era habitual tener oyentes para un widget determinado en la estructura de contenido. Lograr lo mismo en la IU táctil es diferente, ya que el código de escucha JS (o cualquier código) ya no está definido en el contenido.

La estructura de contenido describe la estructura semántica; no debe implicar la naturaleza del widget subyacente. Al no tener código JS en la estructura de contenido, puede cambiar los detalles de implementación sin tener que cambiar la estructura de contenido. En otras palabras, puede cambiar la biblioteca de widgets sin necesidad de tocar la estructura de contenido.

#### Detectar la disponibilidad del cuadro de diálogo {#dialog-ready}

Si tiene un JavaScript personalizado que necesita ejecutarse solo cuando el cuadro de diálogo esté disponible y listo, debe escuchar el evento `dialog-ready`.

Este evento se activa cada vez que se carga el cuadro de diálogo (o se vuelve a cargar) y está listo para usarse, lo que significa que siempre que haya un cambio (crear/actualizar) en el DOM del cuadro de diálogo.

`dialog-ready` se puede usar para vincular código personalizado de JavaScript que realice personalizaciones en los campos de un cuadro de diálogo o tareas similares.

### Validación de campos {#field-validation}

#### Campo obligatorio {#mandatory-field}

Para marcar un campo determinado como obligatorio, establezca la siguiente propiedad en el nodo de contenido del campo:

* Nombre: `required`
* Tipo: `Boolean`

Para ver un ejemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validación de campos (IU de Granite) {#field-validation-granite-ui}

La validación de campos en la interfaz de usuario de Granite y en los componentes de la interfaz de usuario de Granite (equivalentes a widgets) se realiza mediante la API `foundation-validation`. [Consulte la documentación de `foundation-valdiation` Granite para obtener más información.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * proporcionado por [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creación y configuración de un cuadro de diálogo de diseño {#creating-and-configuring-a-design-dialog}

El cuadro de diálogo Diseño se proporciona cuando un componente tiene detalles de diseño que se pueden editar en [Modo de diseño](/help/sites-authoring/default-components-designmode.md).

La definición es muy similar a la de un [cuadro de diálogo utilizado para editar contenido](#creating-a-new-dialog), con la diferencia de que se define como un nodo:

* Nombre de nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creación y configuración de un editor local {#creating-and-configuring-an-inplace-editor}

Un editor in situ permite al usuario editar contenido directamente en el flujo del párrafo, sin necesidad de abrir un cuadro de diálogo. Por ejemplo, los componentes estándar Texto y Título tienen un editor local.

Un editor local no es necesario ni significativo para cada tipo de componente.

Consulte [Ampliación de la creación de páginas - Agregar nuevo editor local](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) para obtener más información.

## Personalizar la barra de herramientas de componentes {#customizing-the-component-toolbar}

La [Barra de herramientas de componentes](/help/sites-developing/touch-ui-structure.md#component-toolbar) proporciona al usuario acceso a una serie de acciones para el componente, como editar, configurar, copiar y eliminar.

Consulte [Ampliación de la creación de páginas - Agregar nueva acción a una barra de herramientas de componentes](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) para obtener más información.

## Configuración de un componente para el carril de referencias (prestado/prestado) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Si el nuevo componente hace referencia a contenido de otras páginas, puede considerar si desea que afecte a las secciones **Contenido prestado** y **Contenido prestado** del carril de [**Referencias**](/help/sites-authoring/basic-handling.md#references).

AEM solo comprueba el componente de referencia de forma predeterminada. Para agregar el componente, debe configurar el paquete OSGi **WCM Authoring Content Reference Configuration**.

Cree una entrada en la definición para especificar el componente, junto con la propiedad que se va a comprobar. Por ejemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de dichos servicios. Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Activación y adición del componente al sistema de párrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Una vez desarrollado el componente, debe habilitarse para utilizarlo en un sistema de párrafos adecuado, de modo que se pueda utilizar en las páginas requeridas.

Esto se puede hacer mediante:

* usando [Modo de diseño](/help/sites-authoring/default-components-designmode.md) al editar una página específica.
* [definiendo la propiedad `components` en el sistema de párrafos de una plantilla](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configuración de un sistema de párrafos para que, al arrastrar un recurso, se cree una instancia de componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM ofrece la posibilidad de configurar un sistema de párrafos en su página para que [se cree automáticamente una instancia de su nuevo componente cuando un usuario arrastre un recurso (apropiado) a una instancia de esa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (en lugar de tener que arrastrar siempre un componente vacío a la página).

Se puede configurar este comportamiento y la relación de recurso a componente necesaria:

1. En la definición de párrafo del diseño de página. Por ejemplo:

   * `/etc/designs/<myApp>/page/par`

   Cree un nodo:

   * Nombre: `cq:authoring`
   * Tipo: `nt:unstructured`

1. En esta sección, cree un nodo que contenga todas las asignaciones de recursos a componentes:

   * Nombre: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Para cada asignación de recursos a componentes, cree un nodo:

   * Nombre: texto. Se recomienda que el nombre indique el recurso y el tipo de componente relacionado; por ejemplo, imagen
   * Tipo: `nt:unstructured`

   Cada uno con las siguientes propiedades:

   * `assetGroup`:

      * Tipo: `String`
      * Valor: el grupo al que pertenece el recurso relacionado; por ejemplo, `media`

   * `assetMimetype`:

      * Tipo: `String`
      * Valor: el tipo MIME del recurso relacionado; por ejemplo, `image/*`

   * `droptarget`:

      * Tipo: `String`
      * Valor: el destino de colocación; por ejemplo, `image`

   * `resourceType`:

      * Tipo: `String`
      * Valor: el recurso de componente relacionado; por ejemplo, `foundation/components/image`

   * `type`:

      * Tipo: `String`
      * Valor: el tipo, por ejemplo, `Images`

Para ver ejemplos, consulte:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto aem-project-archetype en GitHub](https://github.com/adobe/aem-project-archetype)
* Descargar el proyecto como [archivo ZIP](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creación automática de instancias de componentes ahora se puede configurar fácilmente dentro de la interfaz de usuario al usar [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y Plantillas editables. Consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) para obtener más información sobre cómo definir qué componentes se asocian automáticamente con determinados tipos de medios.

## Uso de la extensión AEM Brackets {#using-the-aem-brackets-extension}

La [extensión de AEM Brackets](/help/sites-developing/aem-brackets.md) proporciona un flujo de trabajo suave para editar los componentes de AEM y las bibliotecas de cliente. Se basa en el editor de código [Brackets](https://brackets.io/).

La extensión es la siguiente:

* Facilita la sincronización (no se requiere Maven ni File Vault) para aumentar la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos limitados de AEM a participar en proyectos.
* Proporciona compatibilidad con [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es), el lenguaje de plantilla diseñado para simplificar el desarrollo de componentes y aumentar la seguridad.

>[!NOTE]
>
>Los corchetes son el mecanismo recomendado para crear componentes. Reemplaza la funcionalidad CRXDE Lite: Crear componente, que se diseñó para la interfaz de usuario clásica.

## Migración desde un componente clásico {#migrating-from-a-classic-component}

Al migrar un componente diseñado para utilizarlo con la IU clásica a un componente que se pueda utilizar con la IU táctil (única o conjuntamente), se deben tener en cuenta los siguientes problemas:

* HTL

   * El uso de [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) no es obligatorio, pero si el componente necesita actualizarse, es un momento ideal para considerar la [migración de JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar código [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) que use funciones específicas de la IU clásica
   * Complemento RTE; para obtener más información, consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md).
   * [Migrar `cq:listener` código](#migrating-cq-listener-code) que usa funciones específicas de la IU clásica

* Cuadros de diálogo

   * Cree un cuadro de diálogo para utilizarlo en la interfaz de usuario táctil. Sin embargo, por motivos de compatibilidad, la IU táctil puede utilizar la definición de un cuadro de diálogo de IU clásico cuando no se ha definido ningún cuadro de diálogo para la IU táctil.
   * Se proporcionan [herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md) para ayudarle a ampliar los componentes existentes.
   * [Asignar ExtJS a componentes de Granite UI](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) proporciona una visión general conveniente de los xtype y tipos de nodo de ExtJS con sus tipos de recursos de Granite UI equivalentes.
   * Personalizando campos, para obtener más información, consulte la sesión de AEM Gems en [Personalización de campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
   * Migrar de vtypes a [Validación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Con oyentes JS, para obtener más información, consulte [Gestión de eventos de campo](#handling-field-events) y la sesión de AEM Gems en [Personalización de campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).

### Migrando código cq:listener {#migrating-cq-listener-code}

Si migra un proyecto diseñado para la interfaz de usuario clásica, el código `cq:listener` (y los clientlibs relacionados con componentes) podrían utilizar funciones específicas de la interfaz de usuario clásica (como `CQ.wcm.*`). Para la migración, debe actualizar dicho código utilizando los objetos o funciones equivalentes en la IU táctil.

Si el proyecto se está migrando completamente a la interfaz de usuario táctil, debe reemplazar dicho código para utilizar los objetos y las funciones relevantes para la interfaz de usuario táctil.

Sin embargo, si el proyecto debe adaptarse tanto a la IU clásica como a la IU táctil durante el período de migración (el escenario habitual), debe implementar un conmutador para diferenciar el código independiente que hace referencia a los objetos adecuados.

Este mecanismo de conmutación se puede implementar de la siguiente manera:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentar el componente {#documenting-your-component}

Como desarrollador, desea acceder fácilmente a la documentación de los componentes para comprender rápidamente lo siguiente:

* Descripción
* Uso previsto
* Estructura y propiedades del contenido
* API y puntos de extensión expuestos
* Y así sucesivamente

Por este motivo, es fácil hacer que cualquier Markdown de documentación existente que tenga disponible dentro del propio componente.

Coloque un archivo de `README.md` en la estructura del componente. Esta marca se muestra en la [consola de componentes](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

El marcado admitido es el mismo que para [fragmentos de contenido](/help/assets/content-fragments/content-fragments-markdown.md).
