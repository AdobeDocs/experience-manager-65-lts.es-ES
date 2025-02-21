---
title: Directrices y prácticas de accesibilidad recomendadas para crear formularios en Forms Designer
description: Prácticas recomendadas y directrices para la accesibilidad al desarrollar formularios en Forms Designer.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# Asignación entre directrices y prácticas recomendadas

Las siguientes secciones asignan las directrices Section 508 y WCAG a las prácticas recomendadas descritas en esta guía.

## § 1194.21 Descripción de la directriz y prácticas recomendadas

### Sección 508 §1194.21: Aplicaciones de software y sistemas operativos

| § 1194.21 Directriz | Descripción de directriz | Prácticas recomendadas necesarias de LiveCycle Designer para el cumplimiento | Notas |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | Cuando el software esté diseñado para ejecutarse en un sistema que tenga un teclado, las funciones del producto serán ejecutables desde un teclado en el que la función en sí o el resultado de realizar una función puedan discernirse textualmente. | <li> 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado </li><li> 2.6 Asegúrese de que la lectura y el orden de tabulación sean correctos</li> | |
| (b) | Las aplicaciones no alterarán ni desactivarán las características activadas de otros productos que se identifiquen como características de accesibilidad, cuando dichas características se desarrollen y documenten de conformidad con las normas del sector. Las aplicaciones tampoco alterarán ni desactivarán las funciones activadas de ningún sistema operativo que se identifiquen como funciones de accesibilidad cuando el fabricante del sistema operativo haya documentado la interfaz de programación de aplicaciones para dichas funciones de accesibilidad y esté disponible para el desarrollador del producto. | No hay técnicas específicas de LiveCycle Designer: esta guía la gestiona Adobe Reader for PDF forms. | |
| (c) | Se proporcionará una indicación en pantalla bien definida del enfoque actual que se desplaza entre los elementos interactivos de la interfaz a medida que cambia el enfoque de entrada. El objetivo se expondrá mediante programación de modo que la tecnología de asistencia pueda rastrear el enfoque y los cambios de enfoque. | 2.3 Elegir los controles adecuados Para garantizar que el enfoque se expone tanto de forma programada como visual, utilice siempre los controles estándar. | |
| (d) | La tecnología de asistencia dispondrá de información suficiente sobre un elemento de interfaz de usuario, incluidos la identidad, el funcionamiento y el estado del elemento. Cuando una imagen representa un elemento de programa, la información transmitida por la imagen también debe estar disponible en texto. | <ul><li>2.1 Mantener los formularios simples y fáciles de usar</li> <li>2.1.1 Evitar mover, parpadear o parpadear contenido</li> <li>2.2 Configurar las propiedades del formulario para generar información de accesibilidad</li> <li>2.5 Proporcionar etiquetas adecuadas para los controles del formulario</li></ul> | |
| (e) | Cuando las imágenes de mapa de bits se utilizan para identificar controles, indicadores de estado u otros elementos programáticos, el significado asignado a esas imágenes deberá ser coherente en todo el funcionamiento de la aplicación. | <ul><li>2.4 Proporcionar equivalentes de texto para las imágenes</li><li> 2.5 Proporcionar etiquetas adecuadas para los controles del formulario Este estándar solo se aplica si utiliza la misma imagen en varios lugares de un formulario. No se recomienda el uso de controles personalizados basados en imágenes. En su lugar, utilice únicamente los controles estándar proporcionados por LiveCycle Designer. Si utiliza imágenes en los controles, asegúrese siempre de que se utilizan de forma coherente.</li> | |
| (f) | La información textual se facilitará a través de las funciones del sistema operativo para la visualización del texto. La información mínima que estará disponible es el contenido de texto, la ubicación del símbolo de intercalación de entrada de texto y los atributos de texto. | 2.3 Elegir los controles adecuados Evitar utilizar imágenes para transmitir información textual. En lugar de utilizar componentes de entrada personalizados que podrían no exponer correctamente las propiedades de texto al sistema operativo, utilice siempre los controles estándar. | |
| (g) | Las aplicaciones no sustituirán las selecciones de contraste y color seleccionadas por el usuario ni otros atributos de visualización individuales. | No hay técnicas específicas de LiveCycle Designer | Si es posible, utilice los colores básicos predeterminados del sistema. |
| (h) | Cuando se visualice la animación, la información se podrá visualizar al menos en un modo de presentación no animado a opción del usuario. | 2.1 Mantenga los formularios simples y fáciles de usar Evite utilizar animaciones en sus formularios o proporcione versiones independientes en las que las animaciones se sustituyan por imágenes estáticas. | |
| (i) | La codificación por colores no se utilizará como único medio para transmitir información, indicar una acción, provocar una respuesta o distinguir un elemento visual. | 2.8 Usar el color de forma responsable | |
| (j) | Cuando un producto permita al usuario ajustar la configuración del color y del contraste, deberá ofrecerse una variedad de selecciones de colores capaces de producir una gama de niveles de contraste. | No aplicable | Esta funcionalidad la proporciona generalmente Adobe Reader, no el desarrollador de formularios. |
| (k) | El software no debe utilizar texto parpadeante o intermitente, objetos u otros elementos que tengan una frecuencia de parpadeo mayor de 2 Hz e inferior a 55 Hz. | 2.1.1 Evitar mover, parpadear o parpadear contenido | |
| (l) | Cuando se utilicen formularios electrónicos, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales. | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |

### Sección 508 §11942: Información y aplicaciones de Internet e intranet basadas en la Web

| §11942 Directriz | Descripción de directriz | Prácticas recomendadas necesarias de LiveCycle Designer para el cumplimiento | Notas |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | Se proporcionará un equivalente textual para cada elemento no textual (por ejemplo, mediante &quot;alt&quot;, &quot;longdesc&quot; o en el contenido del elemento). | 2.4 Proporcionar equivalentes de texto para las imágenes | |
| (b) | Las alternativas equivalentes para cualquier presentación multimedia se sincronizarán con la presentación. | 2.12 Garantizar el acceso a todo el contenido multimedia | |
| (c) | Las páginas web se diseñarán de manera que toda la información transmitida en color también esté disponible sin color, por ejemplo, a partir del contexto o del marcado. | 2.8 Usar el color de forma responsable | |
| (d) | Los documentos se organizarán de manera que sean legibles sin necesidad de una hoja de estilo asociada. | No aplicable | |
| (e) | Se proporcionarán enlaces de texto redundantes para cada región activa de un mapa de imagen del lado del servidor. | No aplicable | |
| (f) | Se facilitarán mapas de imágenes del lado del cliente en lugar de mapas de imágenes del lado del servidor, excepto cuando las regiones no puedan definirse con una forma geométrica disponible. | No aplicable | |
| (g) | Los encabezados de fila y columna se identificarán para las tablas de datos. | 2.9 Proporcionar celdas de encabezado para las tablas | |
| (h) | El marcado se utilizará para asociar celdas de datos y celdas de encabezado para tablas de datos que tengan dos o más niveles lógicos de encabezados de fila o columna. | 2.9 Proporcionar celdas de encabezado para las tablas | |
| (i) | Los marcos tendrán un título con texto que facilite la identificación y navegación del marco. | No aplicable | |
| (j) | Las páginas se diseñarán para evitar que la pantalla parpadee con una frecuencia superior a 2 Hz e inferior a 55 Hz. | 2.1 Mantener los formularios simples y fáciles de usar | |
| (k) | Se proporcionará una página de solo texto, con información o funcionalidad equivalente, para hacer que un sitio web cumpla con las disposiciones de esta parte, cuando el cumplimiento no se pueda lograr de ninguna otra manera. El contenido de la página de solo texto se actualizará cada vez que cambie la página principal. | No aplicable | |
| (l) | Cuando las páginas utilicen lenguajes de secuencias de comandos para mostrar contenido o crear elementos de interfaz, la información proporcionada por la secuencia de comandos se identificará con texto funcional que pueda ser leído por la tecnología de asistencia. | 2.11 Evitar scripts disruptivos | |
| (m) | Cuando una página web requiere que haya un applet, un complemento u otra aplicación en el sistema cliente para interpretar el contenido de la página, la página debe proporcionar un vínculo a un complemento o applet que cumpla con §1194.21(a) a (l). | No aplicable | Las páginas web vinculadas a PDF forms deben proporcionar un vínculo a Adobe Reader. |
| (n) | Cuando los formularios electrónicos estén diseñados para cumplimentarse en línea, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las indicaciones y indicaciones. | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |
| (o) | Se facilitará un método que permita a los usuarios omitir los enlaces de navegación repetitivos. | 2.10 Proporcionar una estructura de formulario navegable | |
| (p) | Cuando se requiera una respuesta temporizada, se alertará al usuario y se le dará tiempo suficiente para indicar que se requiere más tiempo. | 2.11 Evitar scripts disruptivos | |

### Puntos de comprobación de prioridad 1 de WCAG 1.0

| Punto de comprobación | Descripción del punto de comprobación | Prácticas recomendadas necesarias de LiveCycle Designer para el cumplimiento | Notas |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | Proporcione un equivalente textual para cada elemento no textual (por ejemplo, a través de &quot;alt&quot;, &quot;longdesc&quot; o en el contenido del elemento). Esto incluye: imágenes, representaciones gráficas de texto (incluidos símbolos), regiones de mapa de imagen, animaciones (por ejemplo, GIF animados), applets y objetos programáticos, arte ASCII, fotogramas, scripts, imágenes utilizadas como viñetas de lista, espaciadores, botones gráficos, sonidos (reproducidos con o sin interacción del usuario), archivos de audio independientes, pistas de audio de vídeo y vídeo. | <ul><li>2.4 Proporcionar equivalentes de texto para las imágenes</li> <li>2.12 Garantizar el acceso a todo el contenido multimedia</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | Proporcione vínculos de texto redundantes para cada región activa de un mapa de imagen del lado del servidor. | No aplicable | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | Hasta que los agentes de usuario puedan leer automáticamente en voz alta el texto equivalente a una pista visual, proporcione una descripción auditiva de la información importante de la pista visual de una presentación multimedia. | 2.12 Garantizar el acceso a todo el contenido multimedia | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | Para cualquier presentación multimedia basada en el tiempo (por ejemplo, una película o una animación), sincronice alternativas equivalentes (por ejemplo, subtítulos o descripciones auditivas de la pista visual) con la presentación. | 2.12 Garantizar el acceso a todo el contenido multimedia | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | Asegúrese de que toda la información transmitida con el color también esté disponible sin color, por ejemplo, desde el contexto o el marcado. | 2.8 Usar el color de forma responsable | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | Identifique claramente los cambios en el idioma natural del texto de un documento y cualquier equivalente textual (por ejemplo, subtítulos). | 2.13 Identificar cambios en el idioma | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | Para las tablas de datos, identifique los encabezados de fila y columna. | 2.9 Proporcionar celdas de encabezado para las tablas | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | Para las tablas de datos que tienen dos o más niveles lógicos de encabezados de fila o columna, utilice el marcado para asociar celdas de datos y celdas de encabezado. | 2.9 Proporcionar celdas de encabezado para las tablas | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | Organice los documentos para que se puedan leer sin hojas de estilo. Por ejemplo, cuando se procesa un documento de HTML sin hojas de estilo asociadas, aún debe ser posible leer el documento. | No aplicable | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | Asegúrese de que los equivalentes del contenido dinámico se actualicen cuando cambie el contenido dinámico. | 2.11 Evitar scripts disruptivos | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | Asegúrese de que las páginas se puedan utilizar cuando los scripts, applets u otros objetos de programación estén desactivados o no sean compatibles. Si no es posible, proporcione información equivalente en una página alternativa accesible. | 2.11 Evitar scripts disruptivos | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | Hasta que los agentes de usuario permitan a los usuarios controlar los parpadeos, evite que la pantalla parpadee. | 2.1 Mantener los formularios simples y fáciles de usar | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | Proporcione mapas de imagen del lado del cliente en lugar de mapas de imagen del lado del servidor, excepto cuando las regiones no se puedan definir con una forma geométrica disponible. | No aplicable | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | Si, después de realizar los mejores esfuerzos, no puede crear una página accesible, proporcionar un vínculo a una página alternativa que utilice tecnologías W3C, sea accesible, tenga información (o funcionalidad) equivalente y se actualice con tanta frecuencia como la página inaccesible (original). | No aplicable | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | Asigne un título a cada fotograma para facilitar su identificación y navegación. | No aplicable | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | Utilice el lenguaje más claro y sencillo adecuado para el contenido de un sitio. | 2.1 Mantener los formularios simples y fáciles de usar | |

### Puntos de comprobación de prioridad 2 de WCAG 1.0

| Punto de comprobación de prioridad 2 | Descripción del punto de comprobación | Prácticas recomendadas necesarias de LiveCycle para el cumplimiento | Notas |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | Asegúrese de que las combinaciones de colores de primer plano y de fondo ofrezcan suficiente contraste cuando las vea alguien con deficiencias de color o cuando las vea en una pantalla en blanco y negro. [Prioridad 2 para imágenes, Prioridad 3 para texto]. | 2.8 Usar el color de forma responsable | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | Cuando exista un lenguaje de marcado adecuado, utilice marcado en lugar de imágenes para transmitir información. | <ul><li>2.1 Mantener los formularios simples y fáciles de usar</li><li> 2.1.1 Evitar mover, parpadear o parpadear contenido</li> <li>2.2 Configurar las propiedades del formulario para generar información de accesibilidad Utilice siempre texto real en lugar de imágenes de texto.</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | Crear documentos que validen gramáticas formales publicadas. | | PDF forms debe coincidir con la especificación de PDF publicada para poder procesarse en Adobe Reader. |
| [3,3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | Utilice hojas de estilo para controlar el diseño y la presentación. | No aplicable | |
| [3,4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | Utilice unidades relativas en lugar de absolutas en los valores de atributo del lenguaje de marcado y en los valores de propiedad de la hoja de estilos. | No aplicable | |
| [3,5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | Utilice elementos de encabezado para transmitir la estructura del documento y utilizarlos según las especificaciones. | 2.10 Proporcionar una estructura de formulario navegable | |
| [3,6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | Marcar listas y elementos de lista correctamente. | 2.10.3 Listas de marcado Marcar contenido basado en listas como listas utilizando las funciones Lista y Elemento de lista. | |
| [3,7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | Marcar las comillas. No utilice comillas dobles para efectos de formato como la sangría. | No aplicable | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | No utilice tablas para el diseño a menos que la tabla tenga sentido cuando esté linealizada. De lo contrario, si la tabla no tiene sentido, proporcione un equivalente alternativo (que puede ser una versión linealizada). | No hay técnicas específicas de LiveCycle | No hay razón para utilizar tablas para el diseño en formularios de LiveCycle. En su lugar, utilice la paleta Diseño para colocar los campos del formulario en un patrón de cuadrícula. Utilice una tabla únicamente cuando utilice funciones específicas de la tabla, como encabezados de tabla. |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | Si se utiliza una tabla para el diseño, no utilice ningún marcado estructural con el fin de aplicar formato visual. | No hay técnicas específicas de LiveCycle | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | Para scripts y applets, asegúrese de que los controladores de eventos son independientes del dispositivo de entrada. | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | Asegúrese de que el contenido dinámico sea accesible o proporcione una presentación o página alternativa. | 2.11 Evitar scripts disruptivos | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | Hasta que los agentes de usuario permitan a los usuarios controlar los parpadeos, evite que el contenido parpadee (es decir, cambie la presentación a una velocidad normal, como activar y desactivar). | 2.1 Mantener los formularios simples y fáciles de usar | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | Hasta que los agentes de usuario permitan a los usuarios congelar el contenido en movimiento, evite el movimiento en las páginas. | 2.1 Mantener los formularios simples y fáciles de usar | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | Hasta que los agentes de usuario permitan detener la actualización, no cree páginas de actualización automática de forma periódica. | No aplicable | |
| [7,5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | Hasta que los agentes de usuario permitan detener el redireccionamiento automático, no utilice el marcado para redireccionar las páginas automáticamente. En su lugar, configure el servidor para realizar redirecciones. | No aplicable | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | Hacer que los elementos programáticos, como scripts y applets, sean accesibles directamente o compatibles con las tecnologías de asistencia [Prioridad 1 si la funcionalidad es importante y no se presenta en ninguna otra parte; de lo contrario, Prioridad 2.] | 2.11 Evitar scripts disruptivos | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | Asegúrese de que cualquier elemento que tenga su propia interfaz pueda funcionar de forma independiente del dispositivo. | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | Para los scripts, especifique controladores de eventos lógicos en lugar de controladores de eventos dependientes del dispositivo. | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | Hasta que los agentes de usuario permitan a los usuarios desactivar las ventanas generadas, no haga que aparezcan ventanas emergentes u otras ventanas y no cambie la ventana actual sin informar al usuario. | 2.11 Evitar scripts disruptivos | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | Hasta que los agentes de usuario admitan asociaciones explícitas entre etiquetas y controles de formulario, asegúrese de que la etiqueta esté colocada correctamente en todos los controles de formulario con etiquetas asociadas implícitamente. | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | Utilice las tecnologías W3C cuando estén disponibles y sean adecuadas para una tarea, y utilice las versiones más recientes cuando sean compatibles. | No aplicable | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | Evite las funciones obsoletas de las tecnologías W3C. | No aplicable | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | Describa el propósito de los marcos y cómo se relacionan entre sí los marcos si no es obvio solo por los títulos de los marcos. | No aplicable | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | Divida grandes bloques de información en grupos más manejables donde sea natural y apropiado. | 2.10 Proporcionar una estructura de formulario navegable | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | Asociar etiquetas explícitamente con sus controles. | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | Identifique claramente el destinatario de cada vínculo. | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario 2.5.6 Proporcionar texto del vínculo | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | Proporcionar metadatos para agregar información semántica a páginas y sitios. | No aplicable | |
| [13.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | Proporcionar información sobre el diseño general de un sitio (por ejemplo, un mapa del sitio o un índice). | 2.10 Proporcionar una estructura de formulario navegable | |
| [13.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | Utilice los mecanismos de navegación de forma coherente. | 2.10 Proporcionar una estructura de formulario navegable | Utilice las páginas maestras para crear contenido de navegación coherente. |

### Criterios de éxito de WCAG 2.0

| Prioridad 1 G 2 Puntos de control | Prácticas recomendadas necesarias de LiveCycle para el cumplimiento | Notas |
| --- | --- | --- |
| 1.1 [Alternativas de texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [Contenido no textual](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 Proporcionar equivalentes de texto para las imágenes | |
| | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |
| 1.2 [Medios basados en el tiempo](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [Solo audio y solo vídeo (pregrabado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.2 [Subtítulos (pregrabados)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.3 [Descripción del audio o medios alternativos (pregrabados)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.4 [Subtítulos (en vivo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.5 [Descripción del audio (pregrabado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.6 [Lenguaje de señas (pregrabado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.7 [Descripción de audio extendido (pregrabado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.8 [Medios alternativos (pregrabados)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.2.9 [Solo audio (activo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 Asegurarse de que todo el contenido de audio y vídeo es accesible | |
| 1.3 [Adaptable](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [Información y relaciones](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 Proporcionar celdas de encabezado para las tablas | |
| 1.3.2 [Secuencia significativa](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 Asegúrese de que la lectura y el orden de tabulación sean correctos | |
| | 2.10 Proporcionar una estructura de formulario navegable | |
| 1.3.3 [Características sensoriales](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 Usar el color de forma responsable | |
| 1.4 [Distinguible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [Uso del color](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 Usar el color de forma responsable | |
| 1.4.2 [Control de audio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | No hay técnicas específicas de LiveCycle | |
| 1.4.3 [Contraste (mínimo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 Usar el color de forma responsable | |
| 1.4.4 [Cambiar el tamaño del texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | No hay técnicas específicas de LiveCycle | |
| 1.4.5 [Imágenes de texto](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | No hay técnicas específicas de LiveCycle | |
| 1.4.6 [Contraste (mejorado)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 Usar el color de forma responsable | |
| 1.4.7 [Audio de fondo bajo o sin audio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | No hay técnicas específicas de LiveCycle | |
| 1.4.9 [Imágenes de texto (sin excepción)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | No hay técnicas específicas de LiveCycle | |
| 2.1 [Teclado accesible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [Teclado](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 Asegúrese de que la lectura y el orden de tabulación sean correctos | |
| | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| 2.1.2 [Sin trampas para el foco del teclado](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| 2.1.3 [Teclado (sin excepción)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 Asegúrese de que la lectura y el orden de tabulación sean correctos | |
| | 2.7 Garantizar que los controles del formulario sean accesibles mediante el teclado | |
| 2.2 [Tiempo suficiente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [Tiempo ajustable](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | No hay técnicas específicas de LiveCycle | |
| 2.2.2 [Pausar, parar, ocultar](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 Mantener los formularios simples y fáciles de usar | |
| 2.2.3 [Sin tiempo](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | No hay técnicas específicas de LiveCycle | |
| 2.2.4 [Interrupciones](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | No hay técnicas específicas de LiveCycle | |
| 2.2.5 [Volver a autenticar](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | No hay técnicas específicas de LiveCycle | |
| 2.3 [Parpadeos] | | |
| 2.3.1 [Tres parpadeos o por debajo de los límites](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 Mantener los formularios simples y fáciles de usar | |
| 2.3.2 [Tres parpadeos](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 Mantener los formularios simples y fáciles de usar | |
| 2.4 [Navegable](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [Omitir bloques](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 Proporcionar una estructura de formulario navegable | |
| 2.4.2 [Página titulada](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | No hay técnicas específicas de LiveCycle | |
| 2.4.3 [Orden de enfoque](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 Asegúrese de que la lectura y el orden de tabulación sean correctos | |
| 2.4.4 [Objetivo del vínculo (en contexto)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | No hay técnicas específicas de LiveCycle | El propósito del vínculo depende de que los autores elijan un texto significativo para los elementos vinculados. |
| 2.4.5 [Múltiples maneras](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 Proporcionar una estructura de formulario navegable | |
| 2.4.6 [Encabezados y etiquetas](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 Proporcionar etiquetas adecuadas para los controles del formulario</li><li>2.10 Proporcionar una estructura de formulario navegable</li> | |
| 2.4.7 [Enfoque visible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | No hay técnicas específicas de LiveCycle | El enfoque predeterminado de los formularios de LiveCycle es visible. |
| 2.4.8 [Ubicación](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | No hay técnicas específicas de LiveCycle | No aplicable: los formularios de LiveCycle no requieren sistemas de navegación. |
| 2.4.9 [Objetivo del vínculo (solo vínculo)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | No hay técnicas específicas de LiveCycle | El propósito del vínculo depende de que los autores elijan un texto significativo para los elementos vinculados. |
| 2.4.10 [Encabezados de sección](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 Proporcionar una estructura de formulario navegable | |
| 3.1 [Legible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [Idioma de la página](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 Identificar el lenguaje natural y cualquier cambio en el lenguaje | |
| 3.1.2 [Idioma de las partes](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 Identificar el lenguaje natural y cualquier cambio en el lenguaje | |
| 3.1.3 [Palabras inusuales](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | No hay técnicas específicas de LiveCycle | |
| 3.1.4 [Abreviaciones](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | No hay técnicas específicas de LiveCycle | |
| 3.1.5 [Nivel de lectura](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | No hay técnicas específicas de LiveCycle | |
| 3.1.6 [Pronunciación](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | No hay técnicas específicas de LiveCycle | |
| 3.2 [Predecible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [Enfoque](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 Evitar scripts disruptivos | |
| 3.2.2 [Al recibir entradas](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 Evitar scripts disruptivos | |
| 3.2.3 [Navegación coherente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 Proporcionar una estructura de formulario navegable | |
| 3.2.4 [Identificación coherente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 Elija los controles adecuados</li><li>2.5 Proporcionar etiquetas adecuadas para los controles del formulario</li> | |
| 3.2.5 [Cambio en la solicitud](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 Evitar scripts disruptivos | |
| 3.3 [Asistencia de entrada](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [Identificación de error](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycle Designer proporciona herramientas para marcar los campos de formulario como obligatorios y para validar la entrada del formulario. |
| 3.3.2 [Etiquetas o instrucciones](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 Proporcionar etiquetas adecuadas para los controles del formulario | |
| 3.3.3 [Sugerencias ante errores](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycle Designer proporciona herramientas para marcar los campos de formulario como obligatorios y para validar la entrada del formulario. |
| 3.3.4 [Prevención de errores (legal, financiero, de datos)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | No hay técnicas específicas de LiveCycle | |
| 3.3.5 [Ayuda](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | No hay técnicas específicas de LiveCycle | |
| 3.3.6 [Prevención de errores (todos)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | No hay técnicas específicas de LiveCycle | |
| 4.1 [Compatible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [Análisis](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | No hay técnicas específicas de LiveCycle | |
| 4.1.2 [Nombre, función, valor](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 Elija los controles adecuados</li> <li>2.5 Proporcionar etiquetas adecuadas para los controles del formulario</li> | |
