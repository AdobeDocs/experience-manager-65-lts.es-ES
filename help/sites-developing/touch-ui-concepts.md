---
title: Conceptos de la IU táctil de Adobe Experience Manager
description: Con Adobe Experience Manager 5.6, Adobe introdujo una nueva interfaz de usuario táctil optimizada con diseño interactivo para el entorno de creación
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: e12f12862c31cef81b2808897fab5cf8e19dfa86
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 0%

---

# Conceptos de la IU táctil de Adobe Experience Manager{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM) cuenta con una interfaz de usuario táctil con [diseño interactivo](/help/sites-authoring/responsive-layout.md) para el entorno de creación, que está diseñada para funcionar tanto en dispositivos táctiles como de escritorio.

>[!NOTE]
>
>La IU táctil es la IU estándar de AEM. La IU clásica ya no se utiliza en AEM 6.4.

La IU táctil incluye lo siguiente:

* El encabezado de grupo indica que:
   * Muestra el logotipo
   * Proporciona un vínculo a la navegación global
   * Proporciona un vínculo a otras acciones genéricas, como Buscar, Ayuda, Soluciones de Experience Cloud, Notificaciones y Configuración de usuario.
* El carril izquierdo (se muestra cuando es necesario y se puede ocultar), que puede mostrar:
   * Escala de cronología
   * Referencias
   * Filtros
* El encabezado de navegación, que de nuevo distingue entre contextos y puede mostrar:
   * Indica la consola que está utilizando actualmente, su ubicación o ambas dentro de esa consola
   * Selección para el carril izquierdo
   * Rutas de exploración
   * Acceso a **Crear** acciones apropiadas
   * Ver selecciones
* El área de contenido que:
   * Enumera los elementos de contenido (ya sean páginas, recursos, publicaciones en foros, etc.)
   * Puede tener el formato solicitado, por ejemplo, columna, tarjeta o lista
   * Utiliza un diseño interactivo (la pantalla cambia de tamaño automáticamente según el tamaño del dispositivo o la ventana)
   * Utiliza desplazamiento infinito (no más paginación, todos los elementos se muestran en una ventana)

![chlimage_1-79](assets/chlimage_1-79.png)

Adobe ha diseñado la interfaz de usuario táctil para proporcionar coherencia en la experiencia del usuario en varios productos. Se basa en:

* **IU de Coral** (CUI) es una implementación del estilo visual de Adobe para la IU táctil. La interfaz de usuario de Coral proporciona todo lo que necesita su producto, proyecto o aplicación web para adoptar el estilo visual de la interfaz de usuario.
* Los componentes de **Granite UI** se han creado con Coral UI.

Los principios básicos de la IU táctil son los siguientes:

* Móvil primero (con el escritorio en mente)
* Diseño interactivo
* Visualización relevante por contexto
* Reutilizable
* Incluir documentación de referencia incrustada
* Incluir pruebas incrustadas
* Diseño ascendente para garantizar que estos principios se apliquen a cada elemento y componente

Para obtener más información general sobre la estructura de la IU táctil, consulte [Estructura de la IU táctil de AEM](/help/sites-developing/touch-ui-structure.md).

## Pila de tecnología AEM {#aem-technology-stack}

AEM utiliza la plataforma Granite como base y la plataforma Granite incluye, entre otras cosas, el repositorio de contenido Java™.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite es la pila web abierta de Adobe, que proporciona varios componentes, incluidos:

* Un lanzador de aplicaciones
* Un marco OSGi en el que se implementa todo
* Varios servicios de compendio de OSGi para admitir la creación de aplicaciones
* Un marco de trabajo de registro completo que proporciona varias API de registro
* Implementación del repositorio de CRX de la especificación de la API de JCR
* El marco web de Apache Sling
* Partes adicionales del producto actual de CRX

>[!NOTE]
>
>Granite se ejecuta como un proyecto de desarrollo abierto dentro de Adobe: las contribuciones al código, las discusiones y los problemas se realizan desde toda la compañía.
>
>Sin embargo, Granite es **no** un proyecto de código abierto. Se basa principalmente en varios proyectos de código abierto (Apache Sling, Felix, Jackrabbit y Lucene en particular), pero Adobe traza una línea clara entre lo que es público y lo que es interno.

## Granite UI {#granite-ui}

La plataforma de ingeniería de Granite también proporciona un marco de trabajo de base de interfaz de usuario. Los principales objetivos de esto son:

* Proporcionar widgets de IU granulares
* Implemente los conceptos de la interfaz de usuario e ilustre las prácticas recomendadas (procesamiento de listas largas, filtrado de listas, CRUD de objetos, asistentes para CUD...)
* Proporcionar una IU de administración ampliable y basada en complementos

Estos cumplen con los requisitos:

* Respeto &quot;primero el móvil&quot;
* Ser extensible
* Sea fácil de anular

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[Obtener archivo](assets/graniteui.pdf)
La IU de Granite:

* Utiliza la arquitectura RESTful de Sling
* Implementa bibliotecas de componentes destinadas a crear aplicaciones web centradas en el contenido
* Proporciona widgets de IU granulares
* Proporciona una interfaz de usuario predeterminada y estandarizada
* Es extensible
* Está diseñado tanto para dispositivos móviles como de escritorio (respeta primero el móvil)
* Se puede utilizar en cualquier plataforma/producto/proyecto basado en Granite; por ejemplo, AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Componentes de Granite UI Foundation](#granite-ui-foundation-components)
Otras bibliotecas pueden utilizar o ampliar esta biblioteca de componentes de base.
* [Componentes de administración de Granite UI](#granite-ui-administration-components)

### Lado del cliente frente al lado del servidor {#client-side-vs-server-side}

La comunicación cliente-servidor en la interfaz de usuario de Granite consiste en hipertexto, no en objetos, por lo que no es necesario que el cliente comprenda la lógica empresarial

* El servidor enriquece HTML con datos semánticos
* El cliente enriquece el hipertexto con hipermedia (interacción)

![chlimage_1-83](assets/chlimage_1-83.png)

#### Lado del cliente {#client-side}

Utiliza una extensión del vocabulario de HTML, siempre que el autor pueda expresar su intención de crear una aplicación web interactiva. Este es un enfoque similar para [WAI-ARIA](https://www.w3.org/TR/wai-aria/) y [microformatos](https://microformats.org/).

Consiste principalmente en una colección de patrones de interacción (por ejemplo, el envío asincrónico de un formulario) que interpretan los códigos JS y CSS y que se ejecutan del lado del cliente. La función del lado del cliente es mejorar el marcado (dado que el servidor permite el uso de hipermedios) para la interactividad.

El lado del cliente es independiente de cualquier tecnología de servidor. Siempre que el servidor proporcione el marcado adecuado, el lado del cliente puede cumplir su función.

Actualmente, los códigos JS y CSS se entregan como Granite [clientlibs](/help/sites-developing/clientlibs.md) en la categoría:

`granite.ui.foundation and granite.ui.foundation.admin`

Se entregan como parte del paquete de contenido:

`granite.ui.content`

#### Del Lado Del Servidor {#server-side}

Esto está formado por una colección de componentes de sling que permiten al autor *componer* una aplicación web rápidamente. Cuando el desarrollador desarrolla componentes, el autor los monta para que sean una aplicación web. La función del lado del servidor es proporcionar la asequibilidad de los hipermedios (marcado) al cliente.

Actualmente, los componentes están en el repositorio de Granite en:

`/libs/granite/ui/components/foundation`

Esto se entrega como parte del paquete de contenido:

`granite.ui.content`

### Diferencias con la IU clásica {#differences-with-the-classic-ui}

Las diferencias entre la interfaz de usuario de Granite y ExtJS (utilizadas para la IU clásica) también son de interés:

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>Llamada a procedimiento remoto <br /> </td>
   <td>Transiciones de estado</td>
  </tr>
  <tr>
   <td>Objetos de transferencia de datos</td>
   <td>Hipermedia</td>
  </tr>
  <tr>
   <td>El cliente conoce los internos del servidor</td>
   <td>El cliente no conoce los datos internos</td>
  </tr>
  <tr>
   <td>"Cliente gordo"</td>
   <td>"Cliente ligero"</td>
  </tr>
  <tr>
   <td>Bibliotecas de cliente especializadas</td>
   <td>Bibliotecas de cliente universales</td>
  </tr>
 </tbody>
</table>

### Componentes de Granite UI Foundation {#granite-ui-foundation-components}

Los [componentes básicos de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) proporcionan los componentes básicos necesarios para crear cualquier interfaz de usuario. Entre ellos se incluyen:

* Botón
* Hipervínculo
* Avatar del usuario

Los componentes de base se encuentran en:

`/libs/granite/ui/components/foundation`

Esta biblioteca contiene un componente de la interfaz de usuario de Granite para cada elemento de Coral. Un componente depende del contenido y su configuración reside en el repositorio. Esto permite crear una aplicación de Granite UI sin tener que escribir el marcado de HTML a mano.

Objetivo:

* Modelo de componente para elementos de HTML
* Composición de componentes
* Pruebas automáticas de unidad y funcionalidad

Implementación:

* Composición y configuración basadas en repositorios
* Uso de las instalaciones de prueba proporcionadas por la plataforma Granite
* Creación de plantillas JSP

Otras bibliotecas pueden utilizar o ampliar esta biblioteca de componentes de base.

### ExtJS y los componentes correspondientes de la interfaz de usuario de Granite {#extjs-and-corresponding-granite-ui-components}

Al actualizar el código ExtJS para utilizar la interfaz de usuario de Granite, la siguiente lista proporciona una descripción general práctica de los xtype de ExtJS y los tipos de nodo con sus tipos de recursos de interfaz de usuario de Granite equivalentes.

| **ExtJS xtype** | **Tipo de recurso de IU de Granite** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **Tipo de nodo** | **Tipo de recurso de IU de Granite** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Componentes de administración de Granite UI {#granite-ui-administration-components}

Los [componentes de administración de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) se basan en los componentes básicos para proporcionar bloques de creación genéricos que cualquier aplicación de administración pueda implementar. Estas incluyen, entre otras:

* Barra de navegación global
* Carril (esqueleto)
* Panel Buscar

Objetivo:

* Aspecto unificado para las aplicaciones de administración
* RAD para aplicaciones de administración

Implementación:

* Componentes predefinidos que utilizan los componentes de base
* Los componentes se pueden personalizar

## IU de Coral {#coral-ui}

CoralUI.pdf

[Obtener archivo](assets/coralui.pdf)
La IU de Coral (CUI) es una implementación del estilo visual de Adobe para la IU táctil diseñada para proporcionar coherencia en la experiencia del usuario en varios productos. La interfaz de usuario de Coral proporciona todo lo necesario para adoptar el estilo visual utilizado en el entorno de creación.

>[!CAUTION]
>
>Coral UI es una biblioteca de IU que está disponible para los clientes de AEM para crear aplicaciones e interfaces web dentro de los límites de su uso con licencia del producto.
>
>Solo se permite el uso de la interfaz de usuario de Coral:
>
>
>* Cuando se ha enviado y empaquetado con AEM.
>* Para su uso al ampliar la IU existente del entorno de creación.
>* Material promocional, anuncios y presentaciones corporativos de Adobe.
>* La interfaz de usuario de las aplicaciones de marca Adobe (la fuente no debe estar disponible para otros usos).
>* Con personalizaciones menores.
>
>El uso de la interfaz de usuario de Coral debe evitarse en:
>
>* Documentos y otros elementos no relacionados con Adobe.
>* Entornos de creación de contenido (donde otros podrían generar los elementos anteriores).
>* Aplicaciones, componentes o páginas web que no están claramente conectadas a Adobe.
>

La interfaz de usuario de Coral es una colección de componentes básicos para el desarrollo de aplicaciones web.

![chlimage_1-84](assets/chlimage_1-84.png)

Diseñado para ser modular desde el principio, cada módulo forma una capa distinta en función de su función principal. Aunque las capas se han diseñado para que se admitan entre sí, también se pueden utilizar de forma independiente si es necesario. Esto permite implementar la experiencia del usuario de Coral en cualquier entorno compatible con HTML.

Con la interfaz de usuario de Coral, no es obligatorio utilizar un modelo o una plataforma de desarrollo en particular. El objetivo principal de Coral es proporcionar un marcado de HTML5 unificado y limpio, independiente del método real utilizado para emitir este marcado. Esto puede utilizarse para el procesamiento en el lado del cliente o del servidor, plantillas, JSP, PHP o incluso aplicaciones de RIA Flash de Adobe, por nombrar solo algunas.

### Elementos de HTML: la capa de marcado {#html-elements-the-markup-layer}

Los elementos de HTML proporcionan una apariencia común para todos los elementos de la interfaz de usuario base (incluida la barra de navegación, el botón, el menú, el carril, etc.).

En el nivel más básico, un elemento HTML es una etiqueta HTML con un nombre de clase específico. Los elementos más complejos pueden estar compuestos por varias etiquetas, anidadas entre sí (de una manera específica).

El CSS se utiliza para proporcionar la apariencia real. Para que sea posible personalizar fácilmente el aspecto (por ejemplo, en el caso de la promoción de la marca), los valores de estilo reales se declaran como variables que el preprocesador [LESS](https://lesscss.org/) expande durante el tiempo de ejecución.

Objetivo:

* Proporcionar elementos básicos de la interfaz de usuario con un aspecto y una sensación comunes
* Proporcionar el sistema de cuadrícula predeterminado

Implementación:

* Etiquetas HTML con estilos inspirados en [Bootstrap](https://twitter.github.com/bootstrap/)
* Las clases se definen en archivos LESS
* Los iconos se definen como sprites de fuente

Por ejemplo, el marcado:

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

Se muestra como:

![chlimage_1-85](assets/chlimage_1-85.png)

El aspecto se define en LESS, vinculado a un elemento por el nombre de clase dedicado (el siguiente extracto se ha abreviado en aras de la brevedad):

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

Los valores reales se definen en un archivo de variables LESS (el siguiente extracto se ha abreviado en aras de la brevedad):

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### Complementos de elementos {#element-plugins}

Muchos de los elementos de HTML deben mostrar algún tipo de comportamiento dinámico, como abrir y cerrar menús emergentes. Esta es la función de los complementos de elemento, que realizan estas tareas manipulando el DOM mediante JavaScript.

Un complemento puede ser:

* Diseñado para funcionar en un elemento DOM específico. Por ejemplo, un complemento de diálogo espera encontrar `DIV class=dialog`
* De naturaleza genérica. Por ejemplo, un administrador de diseño proporciona diseño para cualquier lista de `DIV` o `LI` elementos

El comportamiento del complemento se puede personalizar con parámetros mediante lo siguiente:

* Pasar los parámetros con una llamada de JavaScript
* Utilizando atributos específicos de `data-*` vinculados al marcado de HTML

Aunque el desarrollador puede seleccionar el mejor enfoque para cualquier complemento, la regla general es utilizar:

* `data-*` atributos para opciones relacionadas con el diseño de HTML. Por ejemplo, para especificar el número de columnas
* Opciones/clases de API para la funcionalidad relacionada con los datos. Por ejemplo, construir la lista de elementos para mostrar

El mismo concepto se utiliza para implementar la validación del formulario. Para un elemento que desea validar, debe especificar el formulario de entrada requerido como un atributo `data-*` personalizado. A continuación, este atributo se utiliza como opción para un complemento de validación.

>[!NOTE]
>
>La validación de formularios nativos de HTML5 se debe utilizar siempre que sea posible o se debe expandir.

Objetivo:

* Proporcionar un comportamiento dinámico para los elementos de HTML
* Proporcionar diseños personalizados no es posible con CSS puro
* Realizar validación de formulario
* Realizar manipulación avanzada de DOM

Implementación:

* Complemento jQuery, vinculado a elementos DOM específicos
* Usar atributos de `data-*` para personalizar el comportamiento

Un extracto de marcado de ejemplo (observe las opciones especificadas como atributos data-&#42;):

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

La llamada al complemento jQuery:

```
$('.cards').cardlayout ();
```

Esto se muestra como:

![chlimage_1-86](assets/chlimage_1-86.png)

El complemento `cardLayout` presenta los elementos `UL` incluidos en función de sus alturas respectivas y teniendo en cuenta también la anchura del elemento principal.

### Widgets de elementos HTML {#html-elements-widgets}

Un widget combina uno o más elementos básicos con un complemento de JavaScript para formar elementos de IU de &quot;nivel superior&quot;. Estos pueden implementar un comportamiento más complejo y también una apariencia más compleja de lo que un solo elemento podría ofrecer. Buenos ejemplos son el selector de etiquetas o los widgets de carril.

Un widget puede almacenar en déclencheur y escuchar eventos personalizados para cooperar con otros widgets de la página. Algunos widgets son widgets nativos de jQuery que utilizan los elementos de Coral HTML.

Objetivo:

* Implementar elementos de IU de nivel superior que muestren un comportamiento complejo
* Activación y gestión de eventos

Implementación:

* Complemento jQuery + marcado HTML
* Puede utilizar plantillas de cliente/servidor

Ejemplo de marcado es:

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

La llamada al complemento jQuery (con opciones):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

El complemento emite un marcado de HTML (este marcado utiliza elementos básicos, que pueden utilizar otros complementos internamente):

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

Esto se muestra como:

![chlimage_1-87](assets/chlimage_1-87.png)

### Biblioteca de utilidades {#utility-library}

Esta biblioteca es una colección de complementos o funciones de ayuda de JavaScript que son:

* Independiente de IU
* Sin embargo, es crucial para crear aplicaciones web completas

Estos incluyen la gestión de XSS y el bus de eventos.

Aunque los complementos y widgets de elementos de HTML pueden depender de la funcionalidad proporcionada por la biblioteca de utilidades, esta no puede depender en gran medida de los elementos ni de los widgets en sí.

Objetivo:

* Proporcionar funcionalidad común
* Implementación del bus de eventos
* Plantillas del lado del cliente
* XSS

Implementación:

* Complementos de jQuery o módulos JavaScript compatibles con AMD
