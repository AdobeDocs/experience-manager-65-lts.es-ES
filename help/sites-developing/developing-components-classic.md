---
title: Desarrollo de componentes de Adobe Experience Manager (IU clásica)
description: La IU clásica utiliza ExtJS para crear widgets que proporcionen el aspecto de los componentes. HTL no es el lenguaje de script recomendado para Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d44e6ea8-b4e5-4ed7-a6d0-de1da2709e18
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 0%

---

# Desarrollo de componentes de Adobe Experience Manager (AEM) (IU clásica){#developing-aem-components-classic-ui}

La IU clásica utiliza ExtJS para crear widgets que proporcionen el aspecto de los componentes. Debido a la naturaleza de estos widgets, existen algunas diferencias entre la forma en que los componentes interactúan con la IU clásica y la [IU táctil](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Muchos aspectos del desarrollo de componentes son comunes tanto a la IU clásica como a la IU táctil, por lo que **debe leer [Componentes de AEM - Conceptos básicos](/help/sites-developing/components-basics.md) antes de** mediante esta página, que trata los aspectos específicos de la IU clásica.

>[!NOTE]
>
>Aunque el lenguaje de plantilla HTML (HTL) y JSP se pueden utilizar para desarrollar componentes para la IU clásica, esta página ilustra el desarrollo con JSP. Esto se debe únicamente al historial de uso de JSP en la IU clásica.
>
>HTL es ahora el lenguaje de script recomendado para AEM. Consulte [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) y [Desarrollo de componentes de AEM](/help/sites-developing/developing-components.md) para comparar métodos.

## Estructura {#structure}

La estructura básica de un componente se explica en la página [Componentes de AEM: conceptos básicos](/help/sites-developing/components-basics.md#structure), que aplica tanto las IU táctiles como las clásicas. Aunque no necesite utilizar la configuración de la IU táctil en el nuevo componente, puede resultar útil tenerla en cuenta al heredar de los componentes existentes.

## Scripts JSP {#jsp-scripts}

Los scripts JSP o los servlets se pueden utilizar para procesar componentes. Según las reglas de procesamiento de solicitudes de Sling, el nombre del script predeterminado es:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

El archivo de script JSP `global.jsp` se utiliza para proporcionar acceso rápido a objetos específicos (es decir, para acceder al contenido) a cualquier archivo de script JSP utilizado para procesar un componente.

Por lo tanto, `global.jsp` debe incluirse en cada script JSP de procesamiento de componentes donde se utilicen uno o más de los objetos proporcionados en `global.jsp`.

La ubicación del valor predeterminado `global.jsp` es:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>La ruta de acceso `/libs/wcm/global.jsp`, utilizada por las versiones CQ 5.3 y anteriores, ya está obsoleta.

### Función de global.jsp, API utilizadas y Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

A continuación se enumeran los objetos más importantes proporcionados a partir del valor predeterminado `global.jsp`:

Resumen:

* `<cq:defineObjects />`

   * `slingRequest` - El objeto de solicitud ajustado ( `SlingHttpServletRequest`).
   * `slingResponse`: el objeto de respuesta ajustado ( `SlingHttpServletResponse`).
   * `resource` - El objeto de recursos de Sling ( `slingRequest.getResource();`).
   * `resourceResolver` - El objeto Resource Resolver de Sling ( `slingRequest.getResoucreResolver();`).
   * `currentNode`: el nodo JCR resuelto para la solicitud.
   * `log` - El registrador predeterminado ().
   * `sling`: el asistente de scripts de Sling.
   * `properties` - Las propiedades del recurso al que se dirige ( `resource.adaptTo(ValueMap.class);`).
   * `pageProperties`: propiedades de la página del recurso al que se dirige.
   * `pageManager`: administrador de páginas para acceder a las páginas de contenido de AEM ( `resourceResolver.adaptTo(PageManager.class);`).
   * `component`: objeto de componente del componente de AEM actual.
   * `designer`: objeto de Designer para recuperar información de diseño ( `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign`: diseño del recurso al que se dirige.
   * `currentStyle`: estilo del recurso al que se dirige.

### Acceso al contenido {#accessing-content}

Existen tres métodos para acceder al contenido en AEM WCM:

* Mediante el objeto de propiedades introducido en `global.jsp`:

  El objeto properties es una instancia de ValueMap (consulte [API de Sling](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) y contiene todas las propiedades del recurso actual.

  Ejemplo: `String pageTitle = properties.get("jcr:title", "no title");` utilizado en el script de procesamiento de un componente de página.

  Ejemplo: `String paragraphTitle = properties.get("jcr:title", "no title");` utilizado en el script de procesamiento de un componente de párrafo estándar.

* Mediante el objeto `currentPage` introducido en `global.jsp`:

  El objeto `currentPage` es una instancia de una página (consulte [API de AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html)). La clase de página proporciona algunos métodos para tener acceso al contenido.

  Ejemplo: `String pageTitle = currentPage.getTitle();`

* A través del objeto `currentNode` introducido en `global.jsp`:

  El objeto `currentNode` es una instancia de un nodo (consulte [API JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). Se puede obtener acceso a las propiedades de un nodo mediante el método `getProperty()`.

  Ejemplo: `String pageTitle = currentNode.getProperty("jcr:title");`

## Bibliotecas de etiquetas JSP {#jsp-tag-libraries}

Las bibliotecas de etiquetas CQ y Sling le proporcionan acceso a funciones específicas para utilizarlas en el script JSP de sus plantillas y componentes.

Para obtener más información, consulte el documento [Bibliotecas de etiquetas](/help/sites-developing/taglib.md).

## Uso de bibliotecas HTML del lado del cliente {#using-client-side-html-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permite almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

Consulte el documento [Uso de bibliotecas HTML del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Cuadro de diálogo {#dialog}

El componente necesita un cuadro de diálogo para que los autores añadan y configuren el contenido.

Consulte [Componentes de AEM: conceptos básicos](/help/sites-developing/components-basics.md#dialogs) para obtener más información.

## Configuración del comportamiento de edición {#configuring-the-edit-behavior}

Puede configurar el comportamiento de edición de un componente. Esto incluye atributos como las acciones disponibles para el componente, las características del editor local y los oyentes relacionados con los eventos del componente. La configuración es común a las IU táctiles y a las clásicas, aunque con ciertas diferencias específicas.

El comportamiento de edición [de un componente se ha configurado](/help/sites-developing/components-basics.md#edit-behavior) agregando un nodo `cq:editConfig` de tipo `cq:EditConfig` debajo del nodo de componente (de tipo `cq:Component`) y agregando propiedades específicas y nodos secundarios.

## Uso y ampliación de widgets de ExtJS {#using-and-extending-extjs-widgets}

Consulte [Uso y ampliación de widgets de ExtJS](/help/sites-developing/widgets.md) para obtener más información.

## Uso de xtype para widgets de ExtJS {#using-xtypes-for-extjs-widgets}

Consulte [Uso de xtypes](/help/sites-developing/xtypes.md) para obtener más información.

## Desarrollo de componentes nuevos {#developing-new-components}

En esta sección se describe cómo crear sus propios componentes y añadirlos al sistema de párrafos.

Una forma rápida de empezar es copiar un componente existente y luego realizar los cambios que desee.

Un ejemplo de cómo desarrollar un componente se describe en detalle en [Ampliación del componente Texto e Imagen: un ejemplo.](#extending-the-text-and-image-component-an-example)

### Desarrollar un componente nuevo (adaptar componente existente) {#develop-a-new-component-adapt-existing-component}

Para desarrollar nuevos componentes para AEM basados en componentes existentes, puede copiar el componente, crear un archivo JavaScript para el nuevo componente y almacenarlo en una ubicación accesible para AEM (consulte también [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Con CRXDE Lite, cree una carpeta de componentes en:

   / `apps/<myProject>/components/<myComponent>`

   Vuelva a crear la estructura del nodo como en las bibliotecas y, a continuación, copie la definición de un componente existente, como el componente Texto. Por ejemplo, para personalizar la copia del componente Texto:

   * de `/libs/foundation/components/text`
   * hasta `/apps/myProject/components/text`

1. Modifique `jcr:title` para reflejar su nuevo nombre.
1. Abra la nueva carpeta de componentes y realice los cambios necesarios. Elimine también la información superflua de la carpeta.

   Puede realizar cambios como los siguientes:

   * adición de un campo en el cuadro de diálogo

      * `cq:dialog` - cuadro de diálogo para la IU táctil
      * `dialog` - cuadro de diálogo para la IU clásica

   * reemplazando el archivo `.jsp` (asígnele el nombre después del nuevo componente)
   * o reprocesamiento completo de todo el componente si lo desea

   Por ejemplo, si toma una copia del componente Texto estándar, puede agregar un campo adicional al cuadro de diálogo y, a continuación, actualizar `.jsp` para procesar la entrada realizada allí.

   >[!NOTE]
   >
   >Un componente para:
   >
   >* La IU táctil usa componentes de [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
   >* La IU clásica utiliza [widgets de ExtJS](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

   >[!NOTE]
   >
   >Un cuadro de diálogo definido para la IU clásica funciona dentro de la IU táctil.
   >
   >Un cuadro de diálogo definido para la IU táctil no funcionará dentro de la IU clásica.
   >
   >Según la instancia y el entorno de creación, es posible que desee definir ambos tipos de cuadro de diálogo para el componente.

1. Uno de los siguientes nodos debe estar presente e inicializarse correctamente para que aparezca el nuevo componente:

   * `cq:dialog` - cuadro de diálogo para la IU táctil
   * `dialog` - cuadro de diálogo para la IU clásica
   * `cq:editConfig`: comportamiento de los componentes en el entorno de edición (por ejemplo, arrastrar y soltar)
   * `design_dialog`: cuadro de diálogo para el modo de diseño (solo IU clásica)

1. Active el nuevo componente en el sistema de párrafos mediante:

   * uso de CRXDE Lite para agregar el valor `<path-to-component>` (por ejemplo, `/apps/geometrixx/components/myComponent`) a los componentes de propiedad del nodo `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * siguiendo las instrucciones de [Agregar nuevos componentes a los sistemas de párrafos](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. En AEM WCM, abra una página del sitio web e inserte un párrafo del tipo que ha creado para asegurarse de que el componente funciona correctamente.

>[!NOTE]
>
>Para ver las estadísticas de tiempo de carga de la página, puede usar Ctrl-Mayús-U - con `?debugClientLibs=true` establecido en la dirección URL.

### Adición de un nuevo componente al sistema de párrafos (modo de diseño) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Una vez desarrollado el componente, se añade al sistema de párrafos, que permite a los autores seleccionar y utilizar el componente al editar una página.

1. Obtenga acceso a una página del entorno de creación que usa el sistema de párrafos, por ejemplo, `<contentPath>/Test.html`.
1. Cambie al modo Diseño mediante una de las siguientes opciones:

   * agregando `?wcmmode=design` al final de la dirección URL y obteniendo acceso de nuevo, por ejemplo:

     `<contextPath>/ Test.html?wcmmode=design`

   * hacer clic en Diseño en Sidekick

   Ahora se encuentra en modo de diseño y puede editar el sistema de párrafos.

1. Haga clic en Editar.

   Se mostrará una lista de los componentes que pertenecen al sistema de párrafos. El nuevo componente también aparece en la lista.

   Los componentes se pueden activar (o desactivar) para determinar qué se ofrecen al autor al editar una página.

1. Active el componente y vuelva al modo de edición normal para confirmar que está disponible para su uso.

### Ampliación del componente Texto e imagen: un ejemplo {#extending-the-text-and-image-component-an-example}

Esta sección proporciona un ejemplo de cómo ampliar el ampliamente utilizado componente estándar de texto e imagen con una función de colocación de imágenes configurable.

La extensión del componente de texto e imagen permite a los editores utilizar todas las funcionalidades existentes del componente, además de tener una opción adicional para especificar la ubicación de la imagen:

* En el lado izquierdo del texto (comportamiento actual y el nuevo valor predeterminado)
* Y en el lado derecho

Después de ampliar este componente, puede configurar la ubicación de la imagen a través del cuadro de diálogo del componente.

En este ejercicio se describen las siguientes técnicas:

* Copiar el nodo de componente existente y modificar sus metadatos
* Modificar el cuadro de diálogo del componente, incluida la herencia de widgets de cuadros de diálogo principales
* Modificación del script del componente para implementar la nueva funcionalidad

>[!NOTE]
>
>Este ejemplo está dirigido a la IU clásica.

>[!NOTE]
>
>Este ejemplo se basa en el contenido de muestra de Geometrixx, que ya no se envía con AEM y que ha sido reemplazado por We.Retail. Consulte el documento [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para obtener información sobre cómo descargar e instalar Geometrixx.

#### Ampliación del componente textimage existente {#extending-the-existing-textimage-component}

Para crear el componente, utilice el componente textimage estándar como base y modifíquelo. El nuevo componente se almacena en la aplicación de ejemplo WCM de Geometrixx AEM.

1. Copie el componente textimage estándar de `/libs/foundation/components/textimage` en la carpeta de componentes de Geometrixx, `/apps/geometrixx/components`, con textimage como nombre de nodo de destino. (Copie el componente navegando hasta el componente, haciendo clic con el botón derecho y seleccionando Copiar y explorando el directorio de destino).

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Para que este ejemplo sea sencillo, vaya al componente que ha copiado y elimine todos los subnodos del nuevo nodo textimage, excepto los siguientes:

   * definición del cuadro de diálogo: `textimage/dialog`
   * script de componente: `textimage/textimage.jsp`
   * editar el nodo de configuración (permitiendo arrastrar y soltar recursos): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >La definición del cuadro de diálogo depende de la interfaz de usuario:
   >
   >* IU táctil: `textimage/cq:dialog`
   >* IU clásica: `textimage/dialog`

1. Edite los metadatos del componente:

   * Nombre del componente

      * Establecer `jcr:description` en `Text Image Component (Extended)`
      * Establecer `jcr:title` en `Text Image (Extended)`

   * Grupo, donde el componente aparece en la barra de tareas (dejar tal cual)

      * Dejar `componentGroup` establecido en `General`

   * Componente principal para el nuevo componente (el componente estándar textimage)

      * Establecer `sling:resourceSuperType` en `foundation/components/textimage`

   Después de este paso, el nodo de componente tiene este aspecto:

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. Cambie la propiedad `sling:resourceType` del nodo de configuración de edición de la imagen (propiedad: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) a `geometrixx/components/textimage.`

   De este modo, cuando se coloque una imagen en el componente de la página, la propiedad `sling:resourceType` del componente textimage extendido se establecerá en: `geometrixx/components/textimage.`

1. Modifique el cuadro de diálogo del componente para incluir la nueva opción. El nuevo componente hereda las partes del cuadro de diálogo que son las mismas que en el original. La única adición que hace es ampliar la ficha **Avanzado**, agregando una lista desplegable de **Posición de la imagen**, con las opciones **Izquierda** y **Derecha**:

   * No modifique las propiedades `textimage/dialog`.

   Observe cómo `textimage/dialog/items` tiene cuatro subnodos, tab1 a tab4, que representan las cuatro fichas del cuadro de diálogo textimage.

   * Para las dos primeras pestañas (tab1 y tab2):

      * Cambie xtype a cqinclude (para heredar del componente estándar).
      * Agregue una propiedad path con los valores `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json` y `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`, respectivamente.
      * Elimine todas las demás propiedades o subnodos.

   * Para la pestaña 3:

      * Deje las propiedades y los subnodos sin cambios
      * Agregar una definición de campo a `tab3/items`, posición de nodo de tipo `cq:Widget`
      * Establezca las siguientes propiedades (de tipo cadena) para el nuevo nodo `tab3/items/position`:

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`

      * Agregue el subnodo `position/options` de tipo `cq:WidgetCollection` para representar las dos opciones de colocación de la imagen y, debajo de él, cree dos nodos, o1 y o2 de tipo `nt:unstructured`.
      * Para el nodo `position/options/o1` establezca las propiedades: `text` en `Left` y `value` en `left.`
      * Para el nodo `position/options/o2` establezca las propiedades: `text` en `Right` y `value` en `right`.

   * Eliminar ficha4.

   La posición de la imagen se mantiene en el contenido como la propiedad `imagePosition` del nodo que representa el párrafo `textimage`. Después de estos pasos, el cuadro de diálogo del componente tiene este aspecto:

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. Amplíe el script del componente `textimage.jsp` con un control adicional del nuevo parámetro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Va a reemplazar el fragmento de código enfatizado *%>&lt;div class=&quot;image&quot;>&lt;%* con código nuevo que genera un estilo personalizado para esta etiqueta.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. Guarde el componente en el repositorio. El componente está listo para probarse.

#### Comprobación del nuevo componente {#checking-the-new-component}

Una vez desarrollado el componente, puede agregarlo al sistema de párrafos, que permite a los autores seleccionar y utilizar el componente al editar una página. Estos pasos le permiten probar el componente.

1. Abra una página en Geometrixx como, por ejemplo, Inglés/Compañía.
1. Cambie al modo de diseño haciendo clic en Diseño en Sidekick.
1. Edite el diseño del sistema de párrafos haciendo clic en Editar en el sistema de párrafos situado en medio de la página. Se muestra una lista de componentes que se pueden colocar en el sistema de párrafos y que deben incluir el componente recién desarrollado, Imagen de texto (ampliada) . Actívelo para el sistema de párrafos seleccionándolo y haciendo clic en Aceptar
1. Vuelva al modo de edición.
1. Agregue el párrafo Imagen de texto (ampliado) al sistema de párrafos e inicialice el texto y la imagen con contenido de ejemplo. Guarde los cambios.
1. Abra el cuadro de diálogo del texto y del párrafo de imagen, cambie la Posición de la imagen en la pestaña Avanzado a Derecha y haga clic en Aceptar para guardar los cambios.
1. El párrafo se procesa con la imagen a la derecha.
1. El componente ya está listo para usarse.

El componente almacena su contenido en un párrafo de la página Compañía.

### Deshabilitar la capacidad de carga del componente de imagen {#disable-upload-capability-of-the-image-component}

Para deshabilitar esta capacidad, utilice el componente de imagen estándar como base y modifíquelo. El componente nuevo se almacena en la aplicación de ejemplo de Geometrixx.

1. Copie el componente de imagen estándar de `/libs/foundation/components/image` en la carpeta de componentes de Geometrixx, `/apps/geometrixx/components`, utilizando la imagen como nombre de nodo de destino.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. Edite los metadatos del componente:

   * Definir **jcr:title** en `Image (Extended)`

1. Navegue hasta `/apps/geometrixx/components/image/dialog/items/image`.
1. Añada una propiedad:

   * **Nombre**: `allowUpload`
   * **Tipo**: `String`
   * **Valor**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. Haga clic en **Guardar todo**. El componente está listo para probarse.
1. Abra una página en Geometrixx como, por ejemplo, Inglés/Compañía.
1. Cambie al modo de diseño y active Imagen (ampliada).
1. Vuelva al modo de edición y agréguelo al sistema de párrafos. En las siguientes imágenes, puede ver las diferencias entre el componente de imagen original y el que ha creado.

   Componente de imagen original:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   El nuevo componente de imagen:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. El componente ya está listo para usarse.
