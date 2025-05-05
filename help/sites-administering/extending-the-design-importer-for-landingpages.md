---
title: Ampliación y configuración del importador de diseños para páginas de destino
description: Obtenga información sobre cómo configurar el Importador de diseños para páginas de aterrizaje.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: baf8bbbf4d3c27117a620d0ee0c799b8cc37582f
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 0%

---

# Ampliación y configuración del importador de diseños para páginas de destino{#extending-and-configuring-the-design-importer-for-landing-pages}

En esta sección se describe cómo configurar y, si lo desea, ampliar el importador de diseños para páginas de aterrizaje. El trabajo con páginas de aterrizaje después de la importación se cubre en [páginas de aterrizaje.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Haciendo que el importador de diseños extraiga el componente personalizado**

Estos son los pasos lógicos para que el importador de diseños reconozca el componente personalizado

1. Crear un TagHandler

   * Un controlador de etiquetas es un POJO que administra etiquetas de HTML de un tipo específico. El &quot;tipo&quot; de etiquetas de HTML que puede gestionar TagHandler se define mediante la propiedad OSGi de TagHandlerFactory &quot;tagpattern.name&quot;. Esta propiedad OSGi es esencialmente una regex que debe coincidir con la etiqueta html de entrada que desee administrar. Todas las etiquetas anidadas se lanzarán al controlador de etiquetas para su gestión. Por ejemplo, si se registra en un div que contiene una etiqueta &lt;p> anidada, la etiqueta &lt;p> también se lanzará a su TagHandler y depende de usted cómo desee encargarse de ella.
   * La interfaz del controlador de etiquetas es similar a una interfaz del controlador de contenido SAX. Recibe eventos SAX para cada etiqueta html. Como proveedor de controladores de etiquetas, debe implementar ciertos métodos del ciclo vital a los que llama automáticamente el marco de trabajo del importador de diseños.

1. Cree su TagHandlerFactory correspondiente.

   * El generador del controlador de etiquetas es un componente OSGi (singleton) responsable de generar instancias de su controlador de etiquetas.
   * el generador del controlador de etiquetas debe exponer una propiedad OSGi llamada &quot;tagpattern.name&quot; cuyo valor coincida con la etiqueta html de entrada.
   * Si hay varios controladores de etiquetas que coinciden con la etiqueta html de entrada, se selecciona la que tenga una clasificación más alta. La propia clasificación se expone como una propiedad OSGi **service.ranking**.
   * TagHandlerFactory es un componente OSGi. Cualquier referencia que desee proporcionar a TagHandler debe realizarse a través de esta fábrica.

1. Asegúrese de que TagHandlerFactory tenga una mejor clasificación si desea anular el valor predeterminado.

>[!CAUTION]
>
>El importador de diseños, utilizado para importar páginas de aterrizaje, ha quedado obsoleto con AEM 6.5.

## Preparación de HTML para su importación {#preparing-the-html-for-import}

Después de crear una página de importador, puede importar la página de aterrizaje completa de HTML. Para importar la página de aterrizaje de HTML, primero debe comprimir su contenido en un paquete de diseño. El paquete de diseño contiene la página de aterrizaje de HTML junto con los recursos a los que se hace referencia (imágenes, css, iconos, secuencias de comandos, etc.).

La siguiente hoja de trucos proporciona un ejemplo de cómo preparar HTML para la importación:

Hoja de características clave de página de aterrizaje

[Obtener archivo](assets/cheatsheet.zip)

### Diseño y requisitos del archivo zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>En este punto, los archivos ZIP solo pueden contener una página de HTML o una parte de una página.

A continuación se muestra un ejemplo de diseño del zip:

* /index.html > archivo HTML de página de aterrizaje
* /css > para agregar a la clientlib de CSS
* /img > todas las imágenes y recursos
* /js > para agregarlo a la clientlib de JS

El diseño se basa en el diseño de prácticas recomendadas de HTML5 Boilerplate. Más información en [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>Como mínimo, el paquete de diseño **debe** contener un archivo **index.html** en el nivel raíz. Si la página de aterrizaje que se va a importar también tiene una versión móvil, el zip debe contener **mobile.index.html** junto con **index.html** en el nivel raíz.

### Preparación de la página de aterrizaje en HTML {#preparing-the-landing-page-html}

Para poder importar HTML, debe añadir un div de lienzo a la página de aterrizaje de HTML.

El div lienzo es un html **div** con `id="cqcanvas"` que debe insertarse dentro de la etiqueta HTML `<body>` y debe envolver el contenido que se va a convertir.

A continuación se muestra un fragmento de ejemplo de la página de aterrizaje de HTML después de agregar el div de lienzo:

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### Preparación de HTML para incluir componentes editables de AEM {#preparing-the-html-to-include-editable-aem-components}

Al importar una página de aterrizaje, tiene la opción de importar la página tal cual, lo que significa que después de importar la página de aterrizaje no puede editar ninguno de los elementos importados en AEM (aún puede agregar componentes de AEM adicionales en la página).

Antes de importar la página de aterrizaje, es posible que desee convertir algunas partes de la página de aterrizaje para que sean componentes editables de AEM. Esto permite editar rápidamente partes de la página de aterrizaje incluso después de importar el diseño de esta.

Para ello, agregue `data-cq-component` al componente apropiado en el archivo HTML que importa.

En la siguiente sección se describe cómo editar el archivo HTML para convertir determinadas partes de las páginas de aterrizaje en diferentes componentes editables de AEM. Los componentes se describen en detalle en [Componentes de páginas de aterrizaje](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>El marcado de HTML para convertir partes de la página de aterrizaje en componentes de AEM tiene una declaración de etiqueta de formato largo y otra de forma abreviada. Ambos se describen para cada componente.

### Limitaciones {#limitations}

Antes de realizar la importación, tenga en cuenta las siguientes limitaciones:

### No se conserva ningún atributo como class o id aplicado en la etiqueta &lt;body> {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Si se aplica algún atributo como id o class en la etiqueta body por ejemplo, `<body id="container">`, no se conservará después de la importación. Por lo tanto, el diseño que se esté importando no debería tener dependencias en los atributos aplicados en la etiqueta `<body>`.

### Arrastrar y soltar zip {#drag-and-drop-zip}

La carga ZIP de arrastrar y soltar no es compatible con Internet Explorer y Firefox versiones 3.6 y anteriores. Para cargar un diseño al utilizar estos exploradores, haga clic en la zona de colocación de archivos para abrir un cuadro de diálogo de carga de archivos y cargar el diseño mediante ese cuadro de diálogo.

Los navegadores que admiten &quot;arrastrar y soltar&quot; del zip de diseño son Chrome, Safari5.x, Firefox 4 y superiores.

### El moderador no es compatible {#modernizr-is-not-supported}

`Modernizr.js` es una herramienta basada en JavaScript que detecta las capacidades nativas de los navegadores y si son adecuadas para elementos html5 o no. Los diseños que utilizan Modernizador para mejorar la compatibilidad con versiones anteriores de distintos exploradores pueden causar problemas de importación en la solución de página de aterrizaje. No se admiten scripts de `Modernizr.js` con el importador de diseños.

### Las propiedades de página no se conservan al importar el paquete de diseño {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Cualquier propiedad de página (por ejemplo, Dominio personalizado, Aplicación de HTTPS, etc.) establecida para una página (que utiliza la plantilla Página de aterrizaje en blanco) antes de importar el paquete de diseño se pierde después de importar el diseño. Por lo tanto, la práctica recomendada es establecer las propiedades de la página después de importar el paquete de diseño.

### Se supone solo marcado de HTML {#html-only-markup-assumed}

En la importación, el marcado se sanea por motivos de seguridad y para evitar la importación y publicación de marcado no válido. Esto supone que solo hay marcado de HTML y que se filtrarán todas las demás formas de elementos, como SVG en línea o componentes web.

### Texto {#text}

Marcado de HTML para insertar un componente de texto (`foundation/components/text`) en HTML en el paquete de diseño:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Si se incluye el marcado anterior en HTML, se hace lo siguiente:

* Crea un componente de texto de AEM editable ( `sling:resourceType=foundation/components/text`) en la página de aterrizaje creada después de importar el paquete de diseño.
* Establece la propiedad `text` del componente de texto creado en el HTML incluido dentro de `div`.

**Declaración de etiqueta de componente abreviada**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texto con una lista**

Para añadir un texto con una lista:

* 1st
* 2nd

que se pueden editar en el editor RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texto con color**

Para añadir un texto con color (rosa) que se pueda editar en el editor RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Título {#title}

Marcado de HTML para insertar un componente de título (`wcm/landingpage/components/title`) en HTML en el paquete de diseño:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Si se incluye el marcado anterior en HTML, se hace lo siguiente:

* Crea un componente de título de AEM editable ( `sling:resourceType=wcm/landingpage/components/title`) en la página de aterrizaje creada después de importar el paquete de diseño.
* Establece la propiedad `jcr:title` del componente de título creado en el texto de la etiqueta de encabezado incluida en div.
* Establece la propiedad `type` en la etiqueta de encabezado, en este caso `h1`.

El componente de título admite siete tipos: `h1, h2, h3, h4, h5, h6` y `default`.

**Declaración de etiqueta de componente abreviada**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Imagen {#image}

Marcado de HTML para insertar un componente de imagen (base/componentes/imagen) en HTML en el paquete de diseño:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

Si se incluye el marcado anterior en HTML, se hace lo siguiente:

* Crea un componente de imagen de AEM editable ( `sling:resourceType=foundation/components/image`) en la página de aterrizaje creada después de importar el paquete de diseño.
* Establece la propiedad `fileReference` del componente de imagen creado en la ruta a la que se importa la imagen especificada en el atributo src.
* Establece la propiedad `alt` en el valor del atributo alt de la etiqueta img.
* Establece la propiedad `title` al valor del atributo title en la etiqueta img.
* Establece la propiedad `width` al valor del atributo width en la etiqueta img.
* Establece la propiedad `height` al valor del atributo height en la etiqueta img.

**Declaración de etiqueta de componente abreviada:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### No se admite el origen img de URL absoluta dentro del div de componente de imagen {#absolute-url-img-src-not-supported-within-image-component-div}

Si se intenta la conversión de un componente con una etiqueta `<img>` con un src de dirección URL absoluta, se generará una **excepción UnsupportedTagContentException** adecuada. Por ejemplo, lo siguiente no es compatible:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Sin embargo, en caso contrario, las imágenes de URL absolutas son compatibles con las etiquetas img que no forman parte del div Componente de imagen.

### Componentes de llamada a la acción {#call-to-action-components}

Puede marcar parte de la página de aterrizaje para importarla como un &quot;componente editable de llamada a la acción&quot;; estos componentes importados se pueden editar después de importar la página de aterrizaje. AEM incluye los siguientes componentes de CTA:

* Vínculo de pulsación: Permite añadir un vínculo de texto que, cuando se hace clic, lleva al visitante a una URL de destino.
* Vínculo gráfico: le permite añadir una imagen que, cuando se hace clic, lleva al visitante a una dirección URL de destino.

#### Vínculo de pulsación {#click-through-link}

Este componente de CTA se puede utilizar para agregar un vínculo de texto en la página de aterrizaje.

Propiedades compatibles

* Etiquetar con negrita, cursiva y opciones de subrayado
* URL de destino, admite URL de terceros y de AEM
* Opciones de procesamiento de páginas (misma ventana, nueva ventana, etc.)

Etiqueta de HTML para incluir el componente de pulsaciones en el zip importado. Aquí href se asigna a la dirección URL de destino, &quot;Ver detalles del producto&quot; se asigna a la etiqueta, etc.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

Este componente se puede utilizar en cualquier aplicación independiente o se puede importar desde zip.

**Declaración de etiqueta de componente abreviada**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Vínculo gráfico {#graphical-link}

Este componente de CTA se puede utilizar para añadir cualquier imagen gráfica con vínculo en la página de aterrizaje. La imagen puede ser un botón simple o cualquier imagen gráfica como fondo. Al hacer clic en la imagen, el usuario se dirige a la URL de destino especificada en las propiedades del componente. Forma parte del grupo &quot;Llamada a la acción&quot;.

Propiedades compatibles

* Recorte, rotación de imágenes
* Texto, descripción y tamaño de desplazamiento en píxeles
* URL de destino, admite URL de terceros y de AEM
* Opciones de procesamiento de páginas (misma ventana, nueva ventana, etc.)

Etiqueta de HTML para incluir el componente de vínculo gráfico en el zip importado. Aquí href se asigna a la dirección URL de destino, img src es la imagen de renderización, &quot;título&quot; se toma como texto de desplazamiento, etc.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Declaración de etiqueta de componente abreviada**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Para crear un vínculo gráfico de pulsaciones, debe envolver una etiqueta de anclaje y la etiqueta de imagen dentro de un div con el atributo `data-cq-component="clickthroughgraphicallink"`.
>
>Por ejemplo, `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>No se admiten otras formas de asociar una imagen con una etiqueta de anclaje mediante CSS. Por ejemplo, el marcado siguiente no funciona:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>con un `css .hasbackground { background-image: pathtoimage }` asociado
>

### Formulario de posibles clientes {#lead-form}

Un formulario de posible cliente es un formulario que se utiliza para recopilar información del perfil de un visitante o posible cliente. Esta información se puede almacenar y utilizar más adelante para realizar un marketing eficaz basado en la información. Esta información generalmente incluye título, nombre, correo electrónico, fecha de nacimiento, dirección, interés, etc. Forma parte del grupo &quot;Formulario de posible cliente de CTA&quot;.

**Funciones compatibles**

* Campos de posibles clientes predefinidos: nombre, apellido, dirección, dob, sexo, acerca de, userId, emailId, botón de envío están disponibles en la barra de tareas. Basta con arrastrar y soltar el componente necesario en el formulario de posible cliente.
* Con la ayuda de estos componentes, el autor puede diseñar un formulario de posible cliente independiente, estos campos corresponden a campos de formulario de posible cliente. En la aplicación zip independiente o importada, el usuario puede añadir campos adicionales utilizando los campos cq:form o cta del formulario de posibles clientes, asignarles un nombre y diseñarlos según los requisitos.
* Asigne campos de formulario de posibles clientes con nombres predefinidos específicos de formularios de posibles clientes de CTA, por ejemplo, - firstName para el nombre en el formulario de posibles clientes, etc.
* Los campos que no están asignados al formulario principal se asignan a los componentes cq:form: texto, radio, casilla de verificación, lista desplegable, oculto, contraseña.
* El usuario puede proporcionar el título con la etiqueta &quot;label&quot; y puede proporcionar estilo utilizando el atributo de estilo &quot;class&quot; (solo disponible para componentes de formulario de posibles clientes de CTA).
* La página de agradecimiento y la lista de suscripción se pueden proporcionar como un parámetro oculto del formulario (presente en el index.htm) o se pueden agregar o editar desde la barra de edición de Inicio del formulario de posibles clientes

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Las restricciones como - obligatorio se pueden proporcionar desde la configuración de edición de cada uno de los componentes.

Etiqueta de HTML para incluir el componente de vínculo gráfico en el zip importado. Aquí, &quot;firstName&quot; está asignado al nombre del formulario principal, y así sucesivamente, excepto para las casillas de verificación: estas dos casillas de verificación se asignan al componente desplegable cq:form.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

El componente Parsys de AEM es un componente contenedor que puede contener otros componentes de AEM. Es posible añadir un componente Parsys en el HTML importado. Esto permite al usuario añadir o eliminar componentes editables de AEM en la página de aterrizaje incluso después de importarlos.

El sistema de párrafos permite a los usuarios añadir componentes mediante la barra de tareas.

Marcado de HTML para insertar un componente Parsys (`foundation/components/parsys`) en HTML dentro del paquete de diseño:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

Incluir el marcado anterior en HTML hace lo siguiente:

* Inserta un componente Parsys de AEM (foundation/components/parsys) en la página de aterrizaje creada después de importar el paquete de diseño.
* Inicializa la barra de tareas con componentes predeterminados. Se pueden añadir nuevos componentes a la página de aterrizaje arrastrando componentes de la barra de tareas al componente Parsys.
* Dos componentes de título también forman parte de Parsys.

### Público destinatario {#target}

El componente de destino muestra el contenido de una experiencia en la página. Se pueden crear muchas experiencias en una campaña y el componente de destino puede mostrar dinámicamente contenido de diferentes experiencias a varios usuarios que visitan la página.

El marcado html para insertar un componente de destinatario y también crear diferentes experiencias en una campaña:

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## Opciones de importación adicionales {#additional-importing-options}

Además de especificar si los componentes importados son componentes editables de AEM, también puede configurar lo siguiente antes de importar el paquete de diseño:

* Configurar las propiedades de la página extrayendo los metadatos definidos en la HTML importada.
* Especificar la codificación charset en HTML.
* Superponiendo la plantilla de página del importador.

### Configuración de propiedades de página mediante la extracción de metadatos definidos en HTML importado {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

El importador de diseños extraerá y conservará los metadatos siguientes declarados en el encabezado de la HTML importada como propiedad &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

El importador de diseños extraerá y conservará el atributo de idioma establecido en la etiqueta HTML como la propiedad &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Especificar la codificación charset en el html {#specifying-the-charset-encoding-in-the-html}

El importador de diseño lee la codificación especificada en la HTML importada. La codificación se puede especificar de la siguiente manera:

`<meta charset="UTF-8">`

*O*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si no se especifica ninguna codificación en la HTML importada, la predeterminada establecida por el importador de diseño es UTF-8.

### Plantilla superpuesta {#overlaying-template}

La plantilla Página de aterrizaje en blanco se puede reproducir creando una en: `/apps/<appName>/designimporter/templates/<templateName>`

Los pasos para crear una plantilla en AEM se explican en [Plantillas](/help/sites-developing/templates.md).

### Referencia a un componente desde la página de aterrizaje {#referring-a-component-from-landing-page}

Supongamos que tiene un componente al que desea hacer referencia en HTML mediante el atributo data-cq-component y que el importador de diseños procesa un componente incluido en este lugar. Por ejemplo, desea hacer referencia al componente de tabla ( `resourceType = /libs/foundation/components/table`). Se debe añadir lo siguiente en HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

La ruta en el componente data-cq debe ser el resourceType del componente.

### Prácticas recomendadas {#best-practices}

No se recomienda el uso de selectores CSS similares a los siguientes para elementos marcados para conversión de componentes en la importación.

| E > F | un elemento F secundario de un elemento E | [Combinador secundario](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | un elemento F precedido inmediatamente por un elemento E | [Combinador adyacente del mismo nivel](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un elemento F precedido de un elemento E | [Combinador general del mismo nivel](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:raíz | un elemento E, raíz del documento | [pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un elemento E, el número n secundario de su elemento principal | [pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un elemento E, el número n secundario de su elemento principal, contando desde el último | [pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un elemento E, el número n del mismo nivel de su tipo | [pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un elemento E, el número n del mismo nivel de su tipo, contando desde el último | [pseudoclases estructurales](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Esto se debe a que elementos html adicionales como la etiqueta &lt;div> se añaden al HTML generado después de la importación.

* Tampoco se recomiendan los scripts que dependen de una estructura similar a la anterior para su uso con elementos marcados para su conversión a componentes de AEM.
* No se recomienda el uso de estilos en las etiquetas de marcado para la conversión de componentes como &lt;div data-cq-component=&quot;&ast;&quot;>.
* El diseño debe seguir las prácticas recomendadas de las plantillas HTML5. Más información sobre: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuración de módulos OSGI {#configuring-osgi-modules}

Los componentes que exponen propiedades configurables mediante la consola OSGI son los siguientes:

* Importador de diseños de página de aterrizaje
* Generador de páginas de aterrizaje
* Generador de páginas de aterrizaje móviles
* Preprocesador de entrada de página de aterrizaje

En la tabla siguiente se describen brevemente las propiedades:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nombre de la propiedad</strong></td>
   <td><strong>Descripción de la propiedad </strong></td>
  </tr>
  <tr>
   <td>Importador de diseños de página de aterrizaje</td>
   <td>Extraer filtro</td>
   <td>La lista de expresiones regulares que se utilizarán para filtrar archivos de extracción. <br />: se excluyen de la extracción las entradas zip que coincidan con cualquiera de los patrones especificados</td>
  </tr>
  <tr>
   <td>Generador de páginas de aterrizaje</td>
   <td>Patrón de archivos</td>
   <td>El Generador de páginas de aterrizaje se puede configurar para que gestione los archivos HTML que coinciden con una expresión regular según se define en el patrón de archivo.</td>
  </tr>
  <tr>
   <td>Generador de páginas de aterrizaje móviles</td>
   <td>Patrón de archivos</td>
   <td>El Generador de páginas de aterrizaje se puede configurar para que gestione los archivos HTML que coinciden con una expresión regular según se define en el patrón de archivo.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Grupos de dispositivos</td>
   <td>La lista de grupos de dispositivos que se admitirán.</td>
  </tr>
  <tr>
   <td>Preprocesador de entrada de página de aterrizaje</td>
   <td>Patrón de búsqueda </td>
   <td>El patrón que se va a buscar en el contenido de la entrada del archivo. Esta expresión regular coincide con la entrada de contenido línea a línea. Tras la coincidencia, el texto coincidente se reemplaza con el patrón de reemplazo especificado.<br /> <br /> Consulte la nota siguiente con respecto a las limitaciones actuales del preprocesador de entrada de página de aterrizaje.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Reemplazar motivo</td>
   <td>Patrón que reemplaza a las coincidencias encontradas. Puede usar referencias de grupo regex como $1 o $2. Además, este patrón admite palabras clave como {designPath} que se resuelven con el valor real durante la importación.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Límite actual del preprocesador de entrada de página de aterrizaje:**
>Si necesita realizar cambios en el patrón de búsqueda, al abrir el editor de propiedades felix, debe agregar manualmente caracteres de barra invertida para escapar de los metacaracteres regex. Si no agrega manualmente caracteres de barra invertida, la regex se considera no válida y no reemplazará a la anterior.
>
>Por ejemplo, si la configuración predeterminada es
>
>&#x200B;>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>Y necesita reemplazar `CQ_DESIGN_PATH` con `VIPURL` en el patrón de búsqueda, entonces el patrón de búsqueda debería tener este aspecto:
>
>`/\* *VIPURL *\*/ *(['"])`

## Solución de problemas {#troubleshooting}

Al importar el paquete de diseño, pueden producirse varios errores, que se describen en esta sección.

### Inicialización de la barra de tareas con componentes relevantes de la página de aterrizaje {#initialization-of-sidekick-with-landing-page-relevant-components}

Si el paquete de diseño contiene un marcado de componente Parsys, después de la importación, la barra de tareas comienza a mostrar los componentes relevantes de la página de aterrizaje. Puede arrastrar y soltar nuevos componentes en el componente Parsys de la página de aterrizaje. También puede ir al modo de diseño y agregar nuevos componentes a la barra de tareas.

### Mensajes de error mostrados durante la importación {#error-messages-displayed-during-import}

Si hay algún error (por ejemplo, el paquete importado no es un zip válido), la importación de diseño no importa el paquete. En su lugar, se muestra un mensaje de error en la parte superior de la página justo encima del cuadro de arrastrar y soltar. Aquí se indican ejemplos de escenarios de error. Después de corregir el error, puede volver a importar el zip actualizado en la misma página de aterrizaje en blanco. Los diferentes escenarios en los que se generan errores son los siguientes:

* El paquete de diseño importado no es un archivo zip válido.
* El paquete de diseño importado no contiene un index.html en el nivel superior.

### Advertencias mostradas tras la importación {#warnings-displayed-after-import}

Si hay advertencias (por ejemplo, HTML se refiere a imágenes que no existen dentro del paquete), el importador de diseños importa el zip pero al mismo tiempo muestra una lista de problemas/advertencias en el panel de resultados. Al hacer clic en el vínculo de problemas, se muestra una lista de advertencias que señalan cualquier problema dentro del paquete de diseño. Los distintos escenarios en los que el importador de diseños captura y muestra advertencias son los siguientes:

* HTML se refiere a imágenes que no existen dentro del paquete.
* HTML hace referencia a scripts que no existen dentro del paquete.
* HTML hace referencia a estilos que no existen dentro del paquete.

### ¿Dónde se almacenan los archivos del archivo ZIP en AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Una vez importada la página de aterrizaje, los archivos (imágenes, css, js, etc.) del paquete de diseño se almacenan en la siguiente ubicación de AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supongamos que la página de aterrizaje se crea bajo la campaña `We.Retail` y el nombre de la página de aterrizaje es **myBlankLandingPage**, y la ubicación donde se almacenan los archivos Zip es la siguiente:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Formato no conservado {#formatting-not-preserved}

Al crear su CSS, tenga en cuenta las siguientes limitaciones:

Si un texto y una imagen (editable) son como los siguientes:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

con un archivo CSS aplicado en la clase `box` de la siguiente manera:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Entonces `box img` se usa en el importador de diseño, la página de aterrizaje resultante parece no haber conservado el formato. Para evitarlo, AEM agrega etiquetas div en CSS y reescribe el código en consecuencia. De lo contrario, algunas reglas CSS no serán válidas.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>Los diseñadores sólo deben codificar dentro de la etiqueta **id=cqcanvas** reconocida por el importador; de lo contrario, el diseño no se conserva.
