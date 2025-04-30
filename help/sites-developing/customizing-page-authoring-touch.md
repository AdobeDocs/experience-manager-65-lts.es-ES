---
title: Personalización de la creación de páginas
description: Adobe Experience Manager (AEM) proporciona varios mecanismos para permitirle personalizar la funcionalidad de creación de páginas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 8d53072b-826d-4ff4-843b-09204fb5a455
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 2%

---

# Personalización de la creación de páginas{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento describe cómo personalizar la creación de páginas en la IU moderna y táctil, y no se aplica a la IU clásica.

Adobe Experience Manager (AEM) proporciona varios mecanismos para permitirle personalizar la funcionalidad de creación de páginas (y las [consolas](/help/sites-developing/customizing-consoles-touch.md)) de su instancia de creación.

* Clientlibs

  Clientlibs le permite ampliar la implementación predeterminada para obtener nuevas funcionalidades, mientras reutiliza las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.`. La nueva clientlib debe:

   * dependen de la clientlib de creación `cq.authoring.editor.sites.page`
   * formar parte de la categoría `cq.authoring.editor.sites.page.hook` apropiada

* Superposiciones

  Las superposiciones se basan en definiciones de nodo y le permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no es necesaria una copia 1:1 del original, ya que la [fusión de recursos de sling](/help/sites-developing/sling-resource-merger.md) permite la herencia.

>[!NOTE]
>
>Para obtener más información, consulte [Conjunto de documentación de JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Se pueden utilizar de muchas maneras para ampliar la funcionalidad de creación de páginas en la instancia de AEM. A continuación se cubre una selección (en un nivel superior).

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Usando y creando [clientlibs](/help/sites-developing/clientlibs.md).
>* Usando y creando [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estructura de la IU táctil de AEM](/help/sites-developing/touch-ui-structure.md) para obtener detalles de las áreas estructurales utilizadas para la creación de páginas.
>


>[!CAUTION]
>
>***No*** cambie nada en la ruta de acceso `/libs`.
>
>El motivo es que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
>1. Realizar cambios en `/apps`

## Añadir nueva capa (modo) {#add-new-layer-mode}

Cuando está editando una página, hay varios [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponibles. Estos modos se implementaron usando [layers](/help/sites-developing/touch-ui-structure.md#layer). Permiten acceder a diferentes tipos de funcionalidades para el mismo contenido de página. Las capas estándar son: editar, previsualizar, anotar, desarrollador y segmentación.

### Ejemplo de capa: estado de Live Copy {#layer-example-live-copy-status}

Una instancia estándar de AEM proporciona la capa MSM. Esto accede a los datos relacionados con la [administración de varios sitios](/help/sites-administering/msm.md) y los resalta en la capa.

Para verlo en acción, puede editar cualquier página de [Copia de idioma de We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (o cualquier otra página de Live Copy) y seleccionar el modo **Estado de Live Copy**.

Puede encontrar la definición de capa de MSM (para referencia) en:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Ejemplo de código {#code-sample}

Este es un paquete de muestra que muestra cómo crear una capa (modo), que es una nueva capa para la vista MSM.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto aem-authoring-new-layer-mode en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Añadir nueva categoría de selección al navegador de recursos {#add-new-selection-category-to-asset-browser}

El explorador de recursos muestra recursos de varios tipos o categorías (por ejemplo, imágenes y documentos). Los recursos también se pueden filtrar por estas categorías de recursos.

### Ejemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` es un paquete de muestra que muestra cómo agregar un grupo al buscador de recursos. Este ejemplo se conecta al flujo público de [Flickr](https://www.flickr.com) y los muestra en el panel lateral.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-authoring-extension-assetfinder-flickr en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrado de recursos {#filtering-resources}

Al crear páginas, el usuario debe seleccionar a menudo entre recursos (por ejemplo, páginas, componentes y recursos). Esto puede adoptar la forma de una lista, por ejemplo, desde la que el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Por ejemplo, si se usa el componente [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) para permitir que el usuario seleccione la ruta de acceso a un recurso concreto, las rutas presentadas se pueden filtrar de la siguiente manera:

* Implemente el predicado personalizado implementando la interfaz [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Especifique un nombre para el predicado y haga referencia a ese nombre cuando use `pathbrowser`.

Para obtener más información sobre la creación de un predicado personalizado, consulte [Implementación de un evaluador de predicados personalizado para el Generador de consultas](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>La implementación de un predicado personalizado mediante la implementación de la interfaz `com.day.cq.commons.predicate.AbstractNodePredicate` también funciona en la IU clásica.
>
>Consulte [este artículo de la base de conocimiento](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) para ver un ejemplo de implementación de un predicado personalizado en la IU clásica.

## Agregar una nueva acción a una barra de herramientas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente (normalmente) tiene una barra de herramientas que proporciona acceso a una serie de acciones que se pueden realizar en ese componente.

### Ejemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de herramientas para procesar componentes.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-authoring-extension-toolbar-screenshot en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Añadir nuevo editor en contexto {#add-new-in-place-editor}

### Editor in situ estándar {#standard-in-place-editor}

En una instalación estándar de AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contiene definiciones de los distintos editores disponibles.

1. Existe una conexión entre el editor y cada tipo de recurso (como en el componente ) que puede utilizarlo:

   * `cq:inplaceEditing`

     por ejemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propiedad: `editorType`

           Define el tipo de editor en línea que se utiliza cuando se activa la edición in situ para ese componente; por ejemplo, `text`, `textimage`, `image`, `title`.

1. Se pueden configurar detalles de configuración adicionales del editor mediante un nodo `config` que contenga configuraciones y un nodo `plugin` que contenga los detalles de configuración del complemento necesarios.

   A continuación se muestra un ejemplo de definición de relaciones de aspecto para el complemento de recorte de imágenes del componente de imagen. Debido al potencial del tamaño de pantalla limitado, las relaciones de aspecto de recorte se trasladaron al editor de pantalla completa y solo se pueden ver allí.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >Las proporciones de recorte de AEM establecidas por la propiedad `ratio` se definen como **altura/anchura**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios autores no notarán ninguna diferencia siempre que defina claramente la propiedad `name`, ya que esto es lo que se muestra en la interfaz de usuario.

#### Creación de un nuevo editor in situ {#creating-a-new-in-place-editor}

Para implementar un nuevo editor in situ (dentro de la clientlib):

>[!NOTE]
>
>Por ejemplo, consulte:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre el editor (incluye el constructor):

   * `editor.register`

1. Proporcione la conexión entre el editor y cada tipo de recurso (como en el componente) que pueda utilizarlo.

#### Ejemplo de código para crear un nuevo editor en contexto {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` es un paquete de muestra que muestra cómo crear un editor local en AEM.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-authoring-extension-inplace-editor en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuración de varios editores locales {#configuring-multiple-in-place-editors}

Es posible configurar un componente para que tenga varios editores in situ. Cuando se configuran varios editores locales, puede seleccionar el contenido adecuado y abrir el editor correspondiente. Consulte la documentación de [Configuración de varios editores locales](/help/sites-developing/multiple-inplace-editors.md) para obtener más información.

## Añadir una acción de nueva página {#add-a-new-page-action}

Para agregar una nueva acción de página a la barra de herramientas de la página, por ejemplo, una acción **Volver a sitios** (consola).

### Ejemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de encabezado para volver a la consola Sitios.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-authoring-extension-header-backtosites en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizar el flujo de trabajo de solicitud de activación {#customizing-the-request-for-activation-workflow}

El flujo de trabajo predeterminado, **Solicitud de activación**:

* Aparecerá automáticamente en el menú apropiado cuando un autor de contenido **no tenga** los derechos de replicación adecuados, pero **sí tiene** miembros de Usuarios y autores DAM.

* De lo contrario, no se muestra nada, ya que se han eliminado los derechos de replicación.

Para tener un comportamiento personalizado en dicha activación, puede superponer el flujo de trabajo **Solicitud de activación**:

1. En la superposición `/apps`, el asistente **Sitios**:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Esto en sí, anula la instancia común de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Actualice el [modelo de flujo de trabajo](/help/sites-developing/workflows-models.md) y las configuraciones/scripts relacionados según sea necesario.
1. Elimine el derecho a la acción [`replicate`](/help/sites-administering/security.md#actions) de todos los usuarios adecuados para todas las páginas relevantes; para que este flujo de trabajo se active como una acción predeterminada cuando cualquiera de los usuarios intente publicar (o replicar) una página.
