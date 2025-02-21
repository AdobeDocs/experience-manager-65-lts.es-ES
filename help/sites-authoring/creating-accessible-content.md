---
title: Crear contenido accesible para Adobe Experience Manager (Conformidad con WCAG 2.1)
description: Utilice AEM para ayudar a que las personas con discapacidades puedan acceder al contenido web y utilizarlo
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '13636'
ht-degree: 82%

---

# Crear contenido accesible (Conformidad con WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Las [Directrices de accesibilidad al contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), elaboradas por [un grupo de trabajo del World Wide Web Consortium](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group), consisten en un conjunto de directrices y criterios de éxito independientes de la tecnología para ayudar a las personas con discapacidades a tener acceso al contenido web y utilizarlo.

Como introducción, el consorcio ofrece una serie de secciones y documentos de apoyo:

* [Nuevas funciones en WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Cómo cumplir con WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Comprender WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Técnicas para WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Los documentos WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Además, consulte:
* La [Guía rápida de WCAG 2.1](/help/managing/qg-wcag.md).
* Los [Informes de conformidad de accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility/compliance.html).
* [Configurar el Editor de texto enriquecido para producir contenido accesible](/help/sites-administering/rte-accessible-content.md)

Las directrices se clasifican según tres niveles de conformidad: Nivel A (el más bajo), Nivel AA y Nivel AAA (el más alto). Brevemente, los niveles se definen de la siguiente manera:

* **Nivel A:** El sitio alcanza un nivel básico y mínimo de accesibilidad. Para alcanzar este nivel, se cumplen todos los criterios de éxito del nivel A.
* **Nivel AA:** Se trata de un nivel ideal de accesibilidad al que se debe aspirar, en el que el sitio alcanza un nivel mejorado de accesibilidad, de modo que sea accesible a la mayoría de las personas en la mayoría de las situaciones y que usen la mayoría de las tecnologías. Para alcanzar este nivel, se cumplen todos los criterios de éxito de los niveles A y AA.
* **Nivel AAA:** Su sitio alcanza un nivel muy alto de accesibilidad. Para alcanzar este nivel, se deben cumplir todos los criterios de éxito de los niveles A, AA y AAA.

Al crear su sitio, debe determinar el nivel general en el que desea que se ajuste.

La siguiente sección presenta las [capas de las directrices WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) con los criterios de éxito vinculados a los [niveles de conformidad](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) de los niveles A y AA.

>[!NOTE]
>
>En este documento se utiliza lo siguiente:
>
>* Los [nombres abreviados para las directrices WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)
>* La [numeración utilizada en las directrices WCAG 2.1](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) para hacer referencias cruzadas con la página web de WCAG.

## Principio 1: perceptible     {#principle-perceivable}

[Principio 1: perceptible. Los componentes de la interfaz de usuario y de la información se deben presentar a los usuarios de forma perceptible.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternativas de texto (1.1)     {#text-alternatives}

[Directrices 1.1 Alternativas de texto: Proporcione alternativas de texto para cualquier contenido no textual y así poder cambiarlo por otras formas que la gente puede necesitar, como letras grandes, braille, voz, símbolos o lenguaje más sencillo.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenido no textual (1.1.1) {#non-text-content}

* Criterios de éxito 1.1.1
* Nivel A
* Contenido no textual: todo contenido no textual que se presenta al usuario tiene una alternativa de texto que cumple el objetivo equivalente, excepto para las situaciones que se detallan a continuación

#### Objetivo: Contenido no textual (1.1.1) {#purpose-non-text-content}

La información de una página web se puede proporcionar en muchos formatos no textuales diferentes, como imágenes, vídeos, animaciones, tablas y gráficos. Las personas ciegas o con deficiencias visuales graves no pueden ver el contenido no textual. Sin embargo, pueden acceder al contenido del texto si un lector de pantalla se lo lee en voz alta o si se presenta en un formato táctil a través de un dispositivo de visualización de Braille. Por lo tanto, al proporcionar alternativas textuales al contenido en formato gráfico, las personas que no pueden ver el contenido gráfico pueden acceder a una versión equivalente de la información que proporciona el contenido.

Una ventaja adicional útil es que las alternativas textuales permiten indexar el contenido no textual mediante la tecnología de motor de búsqueda.

#### Cómo cumplir: Contenido no textual (1.1.1) {#how-to-meet-non-text-content}

Para gráficos estáticos, el requisito principal es proporcionar una alternativa textual equivalente para el gráfico. Esto se puede hacer en el campo **Texto alternativo**. Vea, por ejemplo, el componente principal **[Image](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=es)**.

>[!NOTE]
>
>Algunos componentes principales listos para usar, como **[Carrusel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=es)**, no proporcionan un campo **Texto alternativo** para agregar descripciones de texto alternativas a imágenes individuales, aunque existe el campo **Etiqueta** (pestaña **[Accesibilidad](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=es#accessibility-tab)**) para todo el componente.
>
>Cuando se implementan versiones de estos componentes para su instancia de AEM, su equipo de desarrollo debe configurarlos para dar soporte al `alt` atributo y que así los autores puedan agregarlo al contenido (consulte [Añadir soporte para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

De forma predeterminada, AEM requiere que el campo **Texto alternativo** se rellene. Si la imagen es puramente decorativa y el texto alternativo sería innecesario, se puede marcar la opción **La imagen es decorativa**.

#### Crear buenas alternativas de texto {#creating-good-text-alternatives}

Existen varias formas de contenido no textual, por lo que el valor de la alternativa textual depende de la función del gráfico en la página web. Algunas reglas generales a seguir incluyen:

* Las alternativas textuales deben ser concisas, pero captar claramente la información esencial proporcionada por el contenido no textual.
* Deben evitarse las descripciones demasiado largas, que superen los 100 caracteres. Si una alternativa textual requiere más detalle, haga lo siguiente:
   * proporcione una breve descripción en el texto alternativo
   * y añada una descripción más larga en el texto en cualquier otra parte, en la misma página o en una página web aparte. Cree un vínculo a esta descripción separada poniendo un vínculo en la imagen o situando un vínculo de texto junto a la imagen.
* El texto alternativo no debe repetir el contenido proporcionado en el texto de la misma página. Recuerde que muchas imágenes son ilustraciones de puntos que ya están cubiertos en el texto de una página, por lo que puede existir una alternativa textual detallada.
* Si el contenido no textual es un vínculo a otra página o documento y no hay otro texto que forme parte del mismo vínculo, el texto alternativo para la imagen debe indicar el destino del vínculo. No debe describir la imagen.
* Si el contenido no textual está contenido en un elemento button y no hay texto que forme parte del mismo botón, el texto alternativo de la imagen debe indicar la funcionalidad del botón. No debe describir la imagen.
* Es perfectamente aceptable que una imagen tenga un texto alternativo vacío (nulo), pero solo si la imagen no necesita un texto alternativo. Por ejemplo, se trata de un gráfico puramente decorativo o si el texto equivalente existe en el texto de la página.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Los tipos específicos de contenido no textual que requieren alternativas textuales pueden incluir:

* Fotos ilustrativas: imágenes de personas, objetos o lugares. Es importante pensar en el papel de la foto en la página y describir el contenido de la imagen, ya que la tecnología de asistencia anunciará el tipo de elemento (por ejemplo, `graphic` o `image`); puede aumentar la claridad al usar `screenshot` o `illustration` en las descripciones de texto alternativas, pero esto depende del contexto. La coherencia es un factor importante, se debe tomar una decisión para todo el equipo de creación y esto se aplica en toda la experiencia del usuario.
* Iconos: Pequeños pictogramas (gráficos) que transmiten información específica. Se deben utilizar de manera consistente en una página o sitio. Todos los ejemplos del icono en una página o sitio deben contener el mismo texto alternativo, corto y preciso, a menos que se duplique innecesariamente el texto adyacente.
* Gráficos y diagramas: Normalmente representan datos numéricos. Por lo tanto, una opción para proporcionar una alternativa textual podría ser incluir un breve resumen de las principales tendencias que se muestran en el gráfico. Si es necesario, proporcione también una descripción más detallada en el texto con el campo **Descripción** en la pestaña de propiedades de imagen **Avanzadas**. Además, puede proporcionar los datos de origen en formato tabulado en cualquier otra parte de la página o sitio.
* Mapas, diagramas, diagramas de flujo: para los gráficos que proporcionan datos espaciales (por ejemplo, para admitir la descripción de relaciones entre objetos o un proceso), asegúrese de que el mensaje clave se proporcione en formato de texto y de que esta información de texto se coloque cerca de cada punto de datos asociado. En el caso de los mapas, es probable que no sea práctico suministrar un equivalente textual completo. No obstante, si el mapa se proporciona como una forma de ayudar a las personas a encontrar su camino a una ubicación determinada, el texto alternativo de la imagen del mapa puede indicar brevemente *Mapa de X* y, a continuación, ofrecer indicaciones para llegar a esa ubicación en texto en cualquier parte de la página o a través del campo **Descripción** en la pestaña **Avanzado** del componente **Imagen**.
* CAPTCHA: un CAPTCHA es una prueba de Turing pública *completamente automatizada para diferenciar equipos de humanos*. Se trata de una comprobación de seguridad que se utiliza en las páginas web para distinguir a los seres humanos del software malicioso, pero que puede causar barreras de accesibilidad. Son imágenes que requieren que se describa lo que se ve para pasar una prueba de seguridad. Como no es posible proporcionar una alternativa textual para la imagen, en lugar de ello tendrá que considerar una solución alternativa que no sea gráfica.‪ El W3C proporciona algunas sugerencias, como las siguientes:
   * Rompecabezas lógicos
   * El uso de sonido en lugar de imágenes
   * Cuentas de uso limitado y filtros de spam
* Imágenes de fondo: se consiguen utilizando hojas de estilo en cascada (CSS) en lugar de HTML. Esto quiere decir que no se puede especificar un valor de texto alternativo. Por ello, las imágenes de fondo no deben proporcionar información textual importante: si lo hacen, dicha información se debe proporcionar en el texto de la página. Sin embargo, es fundamental que se muestre un fondo alternativo cuando la imagen no se pueda mostrar.

>[!NOTE]
>
>Debe haber un nivel adecuado de contraste entre el fondo y el texto en primer plano; este es un tema que se analiza en detalle en [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Más información: Contenido no textual (1.1.1) {#more-information-non-text-content}

* [Entender los criterios de éxito 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Cumplir los criterios de éxito 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explicación de W3C y alternativas para CAPTCHA](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Medios basados en el tiempo (1.2)     {#time-based-media}

[Directriz 1.2 Medios basados en el tiempo: proporcionar alternativas para medios basados en el tiempo.](https://www.w3.org/TR/WCAG/#time-based-media)

Trata el contenido de la página web *basado en el tiempo*. Abarca el contenido que puede reproducir el usuario (como vídeos, audios y contenido animado) y puede ser pregrabado o reproducido en vivo.

### Solo audio y solo vídeo (pregrabado) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Criterios de éxito 1.2.1
* Nivel A
* Solo audio y Solo vídeo (pregrabado): para medios de solo audio y solo vídeo pregrabado, la siguiente información es cierta, excepto cuando el audio o el vídeo es una alternativa para texto y se etiqueta claramente como:
   * Solo audio pregrabado: se proporciona una alternativa para medios basados en el tiempo que presentan información equivalente para contenido solo audio pregrabado.
   * Solo vídeo pregrabado: se proporciona una alternativa para los medios basados en el tiempo o una pista de audio que presenta información equivalente para el contenido solo de vídeo pregrabado.

#### Objetivo: Solo audio y solo vídeo (pregrabado) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Los problemas de accesibilidad para vídeo y audio pueden experimentarse por parte de estos grupos:

* Personas con discapacidades visuales cuando no hay banda sonora o cuando la banda sonora no basta para informar de lo que está sucediendo en el vídeo o animación.
* Personas con discapacidades auditivas o sordera, que no pueden oír la banda sonora.
* Personas que pueden oír la banda sonora, pero que no entienden lo que se dice (por ejemplo, porque está en un idioma que no entienden).

También puede que el vídeo o el audio no se encuentre disponible para las personas que utilizan navegadores o dispositivos en los que no se puede reproducir contenido en formatos específicos, como Adobe Flash.

Proporcionar esta información en un formato diferente, como texto (o audio para vídeo sin audio) puede ser una manera accesible para las personas que no puedan entender el contenido original.

#### Cómo cumplir: Solo audio y solo vídeo (pregrabado) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Si el contenido es audio pregrabado sin vídeo (como podcast):
   * Proporcione un vínculo inmediatamente antes o después del contenido para obtener una transcripción textual del contenido del audio. La transcripción debe ser una página HTML con un texto equivalente a todo el contenido hablado o no hablado importante, además de una indicación de quién habla, una descripción del escenario, expresiones vocales y una descripción de cualquier otro audio significativo.
* Si el contenido es una animación o un vídeo pregrabado sin audio:
   * Proporcione un vínculo inmediatamente antes o después del contenido para una descripción textual equivalente a la información proporcionada por el vídeo.
   * O bien, una descripción de audio equivalente en un formato de audio utilizado comúnmente, como MP3.

>[!NOTE]
>
>Si el contenido de vídeo o audio se proporciona como una alternativa al contenido que ya existe en otro formato en la misma página web, es posible que no se requiera una alternativa adicional.
>
>Las directrices, [Comprender WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html), proporcionan más información.

Insertar contenido multimedia en sus páginas web de AEM es similar a insertar una imagen. Sin embargo, como el contenido multimedia es mucho más que una imagen fija, hay varios ajustes y opciones diferentes para controlar cómo se reproduce el contenido multimedia.

>[!NOTE]
>
>Al utilizar contenido multimedia con contenido informativo, también se deben crear vínculos a opciones alternativas. Por ejemplo, para incluir una transcripción textual, cree una página HTML para reproducir la transcripción y añada un vínculo debajo o junto al contenido del audio.

#### Más información: Solo audio y solo vídeo (pregrabado) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Entender los criterios de éxito 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Subtítulos (pregrabados) (1.2.2) {#captions-prerecorded}

* Criterios de éxito 1.2.2
* Nivel A
* Subtítulos (pregrabados): se proporcionan los subtítulos para todo el contenido de audio pregrabado en medios sincronizados, excepto cuando los medios son una alternativa para el texto y se etiquetan claramente como tal.

#### Objetivo: Subtítulos (pregrabados) (1.2.2) {#purpose-captions-prerecorded}

Las personas sordas o con dificultades auditivas no podrán acceder, o tendrán grandes dificultades para acceder, al contenido de audio. Los subtítulos son equivalentes textuales para audio verbal y no verbal que se muestran en la pantalla en el momento apropiado durante el vídeo. Permiten entender lo que está ocurriendo a las personas que no pueden oír el audio.

#### Cómo cumplir: Subtítulos (en vivo) (1.2.2) {#how-to-meet-captions-prerecorded}

Los subtítulos pueden ser:

* Abiertos: siempre visibles cuando se reproduce el vídeo
* Cerrados: el usuario puede activar o desactivar los subtítulos

Utilice subtítulos cerrados siempre que sea posible, ya que proporciona a los usuarios la opción de verlos o no.

Para los subtítulos cerrados, crea y proporciona un archivo de subtítulos sincronizados en un formato apropiado (como [SMIL](https://www.w3.org/AudioVideo/)) junto al archivo de vídeo (los detalles de cómo hacerlo exceden el alcance de esta guía, pero proporcionamos vínculos a varios tutoriales en [Más información: Subtítulos (pregrabados) (1.2.2)](#more-information-captions-prerecorded)). Asegúrese de proporcionar una nota o activar la función de subtítulo en el reproductor de vídeo para que los usuarios sepan que el vídeo tiene subtítulos disponibles.

Si necesita utilizar subtítulos abiertos, incorpore el texto en la pista de vídeo. Esto se puede conseguir con aplicaciones de edición de vídeo que permiten superponer títulos.

#### Más información: Subtítulos (pregrabados) (1.2.2) {#more-information-captions-prerecorded}

* [Entender los criterios de éxito 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Descripción del audio o medios alternativos (pregrabados) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Criterios de éxito 1.2.3
* Nivel A
* Descripción del audio o medios alternativos (pregrabados): se proporciona una alternativa para medios basados en el tiempo o descripción del audio del contenido de vídeo pregrabado para medios sincronizados, excepto cuando el medio es una alternativa para el texto y se etiqueta claramente como tal.

#### Objetivo: Descripción del audio o medios alternativos (pregrabados) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Las personas ciegas o con dificultades de visión experimentarán barreras de accesibilidad si la información en un vídeo o animación solo se proporciona de manera visual, o si la banda sonora no proporciona información suficiente para poder entender lo que está pasando visualmente.

#### Cómo cumplir: Descripción del audio o medios alternativos (pregrabados) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Se pueden adoptar dos enfoques para cumplir este criterio con éxito. Cualquiera es aceptable.

1. Incluir una descripción de audio adicional para el contenido del vídeo. Esto se puede lograr de una de las tres maneras siguientes:
   * Durante las pausas en el diálogo existente, se puede proporcionar información acerca de los cambios en la escena que no se presentan como parte de la pista de audio existente.
   * Proporcionando una pista de audio nueva, adicional y optativa, que contenga la banda sonora original, pero incluyendo también información de audio adicional acerca de los cambios en la escena.
      * Los usuarios pueden cambiar entre la pista de audio existente (que *no* contiene una descripción de audio) y la nueva pista de audio (que *sí* contiene una descripción de audio).
      * Esto evita interrupciones a los usuarios que no necesitan la descripción adicional.
   * Creando una segunda versión del contenido de vídeo que permita descripciones de audio extendidas. Reduce las dificultades que se asocian al proporcionar descripciones de audio detalladas en los huecos entre el diálogo existente, mediante pausas temporales en el audio y en el vídeo en puntos adecuados. El resultado es una descripción del audio mucho más larga antes de que se retome la acción. Como en el ejemplo anterior, esta opción resulta mejor como una pista de audio adicional y opcional para prevenir interrupciones a los usuarios que no necesitan la descripción adicional.
1. Proporcionar una transcripción del texto que sea adecuada al equivalente textual del audio y a los elementos visuales del vídeo o animación. Cuando sea adecuado, esto debe incluir una indicación de quién está hablando, una descripción del entorno, cualquier evento o información presentada visualmente y expresiones vocales. Según la longitud, se puede colocar la transcripción en la misma página del vídeo o de la animación o en una página aparte; si se elige esta última opción, se debe proporcionar un vínculo a la transcripción junto al vídeo o animación.

Los detalles exactos de cómo crear vídeos descritos por audio quedan fuera del alcance de esta guía. Crear descripciones de vídeo y audio puede llevar mucho tiempo, pero otros productos de Adobe pueden ayudarle a realizar estas tareas.

#### Más información: Descripción del audio o medios alternativos (pregrabados) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Comprender los criterios de éxito 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Subtítulos (en vivo) (1.2.4)          {#captions-live}

* Criterios de éxito 1.2.4
* Nivel AA
* Subtítulos (en vivo): se proporcionan subtítulos para todo el contenido de audio en vivo en medios sincronizados.

#### Objetivo: Subtítulos (en vivo) (1.2.4)     {#purpose-captions-live}

Este criterio de éxito es idéntico al de [Subtítulos (pregrabados)](#captions-prerecorded) ya que aborda las barreras de accesibilidad que experimentan las personas sordas o que sufren deficiencias auditivas, excepto por el hecho de que este criterio de éxito trata las presentaciones en vivo tales como retransmisiones vía Internet.

#### Cómo cumplir: Subtítulos (en vivo) (1.2.4) {#how-to-meet-captions-live}

Siga las directrices proporcionadas para [Subtítulos (pregrabados)](#captions-prerecorded) arriba. Sin embargo, debido a la naturaleza del medio, los subtítulos se deben crear lo antes posible y como respuesta a lo que está sucediendo. Por eso es necesario considerar la posibilidad de utilizar subtítulos a tiempo real o herramientas de función de voz a texto.

Las instrucciones detalladas van más allá del alcance de este documento, pero los siguientes recursos proporcionan información útil:

* [WebAIM: Subtítulos a tiempo real](https://webaim.org/techniques/captions/realtime)

* [Proyecto AccessComputing (Universidad de Washington): ¿Se pueden generar subtítulos de manera automática utilizando el reconocimiento de voz?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### Más información: Subtítulos (en vivo) (1.2.4)     {#more-information-captions-live}

* [Entender los criterios de éxito 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Cumplir los criterios de éxito 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Descripción del audio (pregrabado) (1.2.5)  {#audio-description-prerecorded}

* Criterios de éxito 1.2.5
* Nivel AA
* Descripción del audio (pregrabado): se proporciona una descripción del audio para todo el contenido de vídeo pregrabado en medios sincronizados.

#### Objetivo: Descripción del audio (pregrabado) (1.2.5) {#purpose-audio-description-prerecorded}

Este criterio de éxito es idéntico al de [Descripción del audio o medios alternativos (pregrabados)](#audio-description-or-media-alternative-prerecorded), excepto por el hecho de que los autores deben proporcionar una descripción del audio mucho más detallada para ajustarse al Nivel AA.

#### Cómo cumplir: Descripción del audio (pregrabado) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Siga las directrices que se proporcionan para la [Descripción del audio o medios alternativos (pregrabados)](#audio-description-or-media-alternative-prerecorded).

#### Más información: Descripción del audio (pregrabado) (1.2.5) {#more-information-audio-description-prerecorded}

* [Entender los criterios de éxito 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptable (1.3)     {#adaptable}

[Directriz 1.3 adaptable: cree contenido que se pueda presentar de diferentes maneras (por ejemplo, con un diseño más sencillo) sin perder información o estructura.](https://www.w3.org/TR/WCAG/#adaptable)

Esta directriz cubre los requisitos necesarios para apoyar a las siguientes personas:

* es posible que no puedan acceder a la información tal como la presenta un autor en la presentación predeterminada de dicho contenido (por ejemplo, un diseño de varias columnas o una página con un uso intensivo de colores o imágenes).

* pueden usar solo audio o una alternativa visual, como un texto largo o un gran contraste.

### Información y relaciones (1.3.1)          {#info-and-relationships}

* Criterios de éxito 1.3.1
* Nivel A
* Información y relaciones: la información, la estructura y las relaciones en presentaciones se pueden determinar mediante un programa o pueden estar disponibles en formato de texto.

#### Objetivo: Información y relaciones (1.3.1)     {#purpose-info-and-relationships}

Muchas tecnologías de asistencia que utilizan las personas con discapacidades cuentan con información estructural para que se pueda mostrar o *comprender* el contenido. Esta información estructural puede adoptar la forma de encabezados de página, encabezados de fila y columna de tabla y tipos de lista. Por ejemplo, un lector de pantalla podría permitir que un usuario navegue por una página de un encabezado a otro. Sin embargo, cuando el contenido de una página solo parece contener una estructura a través de un estilo visual, en lugar del formato HTML subyacente, quiere decir que no existe ninguna información estructural disponible para tecnologías de asistencia, lo que limita su capacidad de proporcionar una navegación más sencilla.

Este criterio de éxito existe para garantizar que esta información estructural se proporcione por programación a través de HTML u otras técnicas de codificación, para que los buscadores y las tecnologías de asistencia puedan acceder a la información y aprovecharla.

#### Cómo cumplir: Información y relaciones (1.3.1)     {#how-to-meet-info-and-relationships}

AEM facilita construir contenido web con sentido semántico utilizando los elementos HTML adecuados. Abra el contenido de su página en RTE (un componente Texto) y utilice el menú **Paraformato** (símbolo de párrafo) para especificar el elemento estructural adecuado (por ejemplo, párrafo y encabezado).

Puede garantizar que las páginas web tengan la estructura adecuada mediante los siguientes elementos, según corresponda:

* **Encabezados:** siempre y cuando tenga las funciones de accesibilidad del RTE activadas, AEM ofrece tres niveles de encabezado de página. Puede utilizarlas para identificar secciones y subsecciones de contenido. El encabezado 1 es el nivel más alto, mientras que el encabezado 3 es el más bajo. El administrador del sistema puede configurar el sistema para permitir el uso de más niveles de encabezado.

* **Listas**: Puede utilizar HTML para especificar tres tipos diferentes de listas:
   * El elemento `<ul>` se utiliza para listas *desordenadas* (o listas con viñetas). Los elementos de listas individuales se identifican utilizando el elemento `<li>`. En el RTE, utilice el icono **Lista con viñetas**.
   * El elemento `<ol>` se utiliza para listas *numeradas*. Los elementos de listas individuales se identifican utilizando el elemento `<li>`. En RTE, utilice el icono **Lista numerada**.

  Si desea cambiar contenido existente por un tipo de lista específico, resalte el texto correspondiente y seleccione el tipo de lista adecuado. Como en el ejemplo anterior, en el que se mostraba cómo se introducía texto en párrafos, los elementos de lista adecuada se agregan automáticamente al HTML.

  En el modo de pantalla completa, están visibles los iconos individuales **Lista con viñetas** y **Lista numerada**. Cuando no se encuentra en modo de pantalla completa, las dos opciones están disponibles detrás del icono de una **Listas**.

* **Tablas**: Las tablas de datos deben identificarse utilizando elementos de tablas HTML:
   * un elemento `<table>`
   * un elemento `<tr>` para cada fila de la tabla
   * un elemento `<th>` para cada titular de fila y columna
   * un elemento `<td>` para cada celda de datos

  Además, las tablas accesibles utilizan los siguientes elementos y atributos:

   * El elemento `<caption>` se utiliza para proporcionar un subtítulo visible para la tabla. Los subtítulos predeterminados aparecen centrados encima de la tabla, pero se pueden posicionar de cualquier otra manera adecuada utilizando CSS. El subtítulo está asociado programáticamente con la tabla, por lo que se trata de un método útil para proporcionar una introducción al contenido.
   * El elemento `<summary>` ayuda a los usuarios que carecen de visión para que entiendan con mayor facilidad la información que se presenta en la tabla mediante una sinopsis de lo que el usuario puede ver. Resulta útil cuando se utilizan diseños de tabla complejos o poco convencionales (este atributo no se muestra en el explorador, solo se lee en voz alta para tecnologías de asistencia).
   * El atributo `scope` del elemento `<th>` se utiliza para indicar si una celda representa el encabezado de una fila en concreto o de una columna en concreto. Un enfoque similar es el de utilizar el encabezado y los atributos de identificación en tablas complejas, donde las celdas de datos se pueden asociar con uno o más encabezados.

  >[!NOTE]
  >
  >De forma predeterminada, estos elementos y atributos no están disponibles directamente, aunque es posible que el administrador del sistema agregue compatibilidad con estos valores en el cuadro de diálogo **Propiedades de la tabla** (consulte [Agregar compatibilidad con elementos y atributos adicionales de HTML](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

  Para abrir el cuadro de diálogo **Tabla**, seleccione la pestaña **Propiedades de la tabla**:

   * Defina un **subtítulo** adecuado.
   * Idealmente, elimine los valores predeterminados de **anchura**, **altura**, **borde**, **relleno de celda** y **espaciado de celda**, ya que estas propiedades se pueden definir en una hoja de estilo global.

  Después, puede utilizar las **propiedades de la celda** para decidir si es de datos o de encabezado.

* **Énfasis**: Utilice el elemento `<strong>` o `<em>` para dar énfasis. No utilice encabezados o texto enfatizado en los párrafos.
   * Enfatice el texto que quiera remarcar;
   * Haga clic en el icono **B** (para `<strong>`) o en el icono **I** (para `<em>`) que se muestra en el panel **Propiedades** (asegúrese de que HTML está seleccionado).

     >[!NOTE]
     >
     >RTE en una instalación AEM estándar está configurada para utilizar:
     >
     >* `<b>` para `<strong>`
     >* `<i>` para `<em>`
     >
     >Aunque son igual de eficaces, `<strong>` y `<em>` son preferibles porque son HTML semánticamente correctos. Su equipo de desarrollo puede configurar el RTE para utilizar `<strong>` y `<em>` (en lugar de `<b>` y `<i>`) cuando desarrolle su proyecto.

* **Tablas de datos complejas**: A veces, cuando hay tablas complejas con dos o más niveles de encabezados, las propiedades de tabla básicas pueden no ser suficientes para proporcionar toda la información estructural necesaria. Para este tipo de tablas complejas, se deben crear relaciones directas entre los encabezados y sus celdas relacionadas mediante los atributos **header** e **id**.

  >[!NOTE]
  >
  >El atributo de identificación no se encuentra disponible en las instalaciones predeterminadas. Se puede activar configurando las normas HTML y el serializador en el RTE.

  Por ejemplo, en la tabla siguiente, los encabezados y las identificaciones se comparan para crear una asociación programática para los usuarios de tecnología de asistencia.

  ```xml
    <table>
      <tr>
        <th rowspan="2" id="h">Homework</th>
        <th colspan="3" id="e">Exams</th>
        <th colspan="3" id="p">Projects</th>
      </tr>
      <tr>
        <th id="e1" headers="e">1</th>
        <th id="e2" headers="e">2</th>
        <th id="ef" headers="e">Final</th>
        <th id="p1" headers="p">1</th>
        <th id="p2" headers="p">2</th>
        <th id="pf" headers="p">Final</th>
      </tr>
      <tr>
        <td headers="h">15%</td>
        <td headers="e e1">15%</td>
        <td headers="e e2">15%</td>
        <td headers="e ef">20%</td>
        <td headers="p p1">10%</td>
        <td headers="p p2">10%</td>
        <td headers="p pf">15%</td>
      </tr>
    </table>
  ```

  Para conseguirlo en AEM, añada las especificaciones directamente mediante el modo de edición de la fuente.

  >[!NOTE]
  >
  >Esta funcionalidad no se encuentra disponible de inmediato en las instalaciones estándar. Requiere la configuración del RTE, de las normas HTML y el serializador.

#### Más información: Información y relaciones (1.3.1) {#more-information-info-and-relationships}

* [Entender los criterios de éxito 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Cumplir los criterios de éxito 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Secuencia significativa (1.3.2)  {#meaningful-sequence}

* Criterios de éxito 1.3.2
* Nivel A
* Secuencia significativa: Cuando la secuencia en la que se presenta el contenido afecta su significado, se puede determinar una secuencia de lectura correcta mediante programación.

#### Objetivo: Secuencia significativa (1.3.2) {#purpose-meaningful-sequence}

La intención de este criterio de éxito es permitir que un agente de usuario proporcione una presentación alternativa del contenido, al tiempo que preserva el orden de lectura necesario para comprender el significado. Es importante que sea posible determinar al menos una secuencia del contenido que tenga sentido mediante programación. El contenido que no cumpla estos criterios de éxito puede confundir o desorientar a los usuarios si la tecnología de asistencia lee el contenido en un orden incorrecto, o si se aplican hojas de estilo alternativas u otros cambios de formato.

#### Cómo cumplir: Secuencia significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Siga las directrices de [Cómo cumplir los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Más información: Secuencia significativa (1.3.2) {#more-information-meaningful-sequence}

* [Entender los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Cumplir los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Características sensoriales (1.3.3)          {#sensory-characteristics}

* Criterios de éxito 1.3.3
* Nivel A
* Características sensoriales: las instrucciones que se proporcionan para entender el contenido y operar con él no se basan solo en características sensoriales de componentes como la forma, el tamaño, la ubicación visual, la orientación o el sonido

#### Objetivo: Características sensoriales (1.3.3)     {#purpose-sensory-characteristics}

Los diseñadores normalmente se centran en características de diseño visuales tales como el color, la forma, el estilo del texto o una parte de la ubicación absoluta o relativa del contenido a la hora de presentar la información. Estas pueden ser técnicas de diseño potentes para transmitir información (y pueden mejorar la accesibilidad general para usuarios videntes con necesidades de accesibilidad cognitiva), pero las personas ciegas o con dificultades visuales pueden no ser capaces de acceder a la información que requiera la identificación visual de atributos como posición, color o forma.

Del mismo modo, la información que requiere distinguir entre sonidos diferentes (por ejemplo, contenido cuya voz es masculina o femenina) presenta barreras de accesibilidad para las personas que sufren deficiencias auditivas si el contenido del audio no se refleja en un texto alternativo.

>[!NOTE]
>
>Para los requisitos relativos a las alternativas de color, consulte [Uso del color](#use-of-color).

#### Cómo cumplir: Características sensoriales (1.3.3)     {#how-to-meet-sensory-characteristics}

Asegúrese de que cualquier información relativa a las características visuales del contenido de una página también se presente en un formato alternativo.

* Es importante no basarse en la posición visual para dar información. Por ejemplo, si desea remitir a los usuarios a un menú situado en el lado derecho de la página para obtener acceso a información adicional, no haga referencia a *el menú de la derecha*; en su lugar, asigne un nombre al menú (por ejemplo, mediante un encabezado) y mencione ese nombre en el texto.
* También es importante no basarse en el estilo del texto (por ejemplo, si se trata de texto en negrita o en cursiva) como la única manera de transmitir la información.

>[!NOTE]
>
>El uso de términos descriptivos es aceptable si se entiende que tienen significado en un contexto no visual. Por ejemplo, usar *arriba* y *abajo* suele estar aceptado, porque implican (respectivamente) contenido antes y después de un elemento particular del contexto; tendría sentido si el contenido se lee en voz alta.

#### Más información: Características sensoriales (1.3.3)     {#more-information-sensory-characteristics}

* [Entender los criterios de éxito 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Cumplir los criterios de éxito 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Distinguible (1.4)     {#distinguishable}

[Directrices 1.4 Distinguible: Facilitar a los usuarios ver y oír el contenido incluyendo la posibilidad de separar el primer plano del fondo.](https://www.w3.org/TR/WCAG/#distinguishable)

### Uso del color (1.4.1)          {#use-of-color}

* Criterios de éxito 1.4.1
* Nivel A
* Uso del color: el color no es el único medio visual para transmitir información, indicar una acción, una respuesta o distinguir un elemento visual.

>[!NOTE]
>
>Este criterio de éxito se dirige específicamente a la percepción del color. Otras formas de percepción se tratan en [Adaptable (1.3)](#adaptable); incluyendo el acceso programático al color y otros códigos de presentación visual.

#### Objetivo: Uso del color (1.4.1)     {#purpose-use-of-color}

El color es una manera efectiva de resaltar el atractivo estético de las páginas web y también resulta útil para transmitir información. Sin embargo, existe una variedad de deficiencias visuales, desde la ceguera hasta la deficiencia en la percepción del color, que significa que algunas personas no pueden distinguir entre ciertos colores. Esto hace que la codificación de colores sea una manera poco fiable de transmitir información.

Por ejemplo, alguien con deficiencia de visión de color rojo-verde será incapaz de distinguir entre tonos de verde y tonos de rojo. Puede que esta persona vea ambos colores como un tercer color (por ejemplo, marrón), en cuyo caso no distingue entre el verde, el rojo y el marrón.

Además, las personas que utilizan exploradores de solo texto, dispositivos de pantallas monocromáticas o páginas en blanco y negro no pueden percibir el color.

Otra consideración es el estado *selected* de un elemento de interfaz (por ejemplo, pestañas, botones de alternar, entre otros), que debe transmitirse de alguna manera que no sea solo con el color y más allá de una presentación visual. Para estos elementos, el uso adicional de patrones, formas e información programática resulta útil a la hora de crear una experiencia de usuario totalmente inclusiva que no dependa de un sentido específico.

#### Cómo cumplir: Uso del color (1.4.1)     {#how-to-meet-use-of-color}

En todos los casos donde el color se utilice para transmitir información, es importante asegurarse de que la información se encuentra disponible sin necesidad de ver el color.

Por ejemplo, asegúrese de que la información que proporciona el color también esté explícita en el texto.

Si se utiliza el color como medio para transmitir información, se debería proporcionar una señal visual adicional, como cambiar el estilo (por ejemplo, usar negrita o cursiva) o la fuente. De esta manera, se ayuda a las personas con poca visión o que tienen una deficiencia de percepción de color a identificar la información. Sin embargo, no se puede confiar en esta medida totalmente puesto que no ayudaría a aquellos que no puedan ver la página. Por lo tanto, (a veces) resulta útil proporcionar texto oculto o utilizar soluciones programáticas, como el [grupo de estándares web de Aplicaciones de Internet enriquecidas accesibles (ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/), para transmitir esta información a usuarios sin visión.

#### Más información: Uso del color (1.4.1) {#more-information-use-of-color}

* [Entender los criterios de éxito 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Cumplir los criterios de éxito 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Control de audio (1.4.2)  {#audio-control}

* Criterios de éxito 1.4.2
* Nivel A
* Control de audio: Si el audio de una página web se reproduce automáticamente durante más de 3 segundos, o hay un mecanismo disponible para pausar o detener el audio, o hay un mecanismo para controlar el volumen del audio independientemente del nivel de volumen total del sistema.

#### Objetivo: Control de audio (1.4.2) {#purpose-audio-control}

A las personas que utilizan software de lectura de pantalla les resulta difícil escuchar la salida de voz si se reproduce otro audio al mismo tiempo. Esta dificultad se agrava cuando la salida de voz del lector de pantalla está basado en software (como la mayoría de los actuales) y se controla con el mismo control de volumen que el sonido. Además, algunas personas con discapacidades cognitivas y neurodivergentes pueden tener sensibilidad sonora. Para estas personas, no poder cambiar el nivel de volumen del contenido de audio es bastante perturbador.

Por lo tanto, es importante que el usuario pueda desactivar el sonido de fondo.

>[!NOTE]
>
>Tener el control del volumen incluye poder reducir el volumen a cero.

#### Cómo cumplir: Control de audio (1.4.2) {#how-to-meet-audio-control}

Siga las directrices de [Cómo cumplir los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Más información: Control de audio (1.4.2) {#more-information-audio-control}

* [Entender los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Cumplir los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (mínimo) (1.4.3)     {#contrast-minimum}

* Criterios de éxito 1.4.3
* Nivel AA
* Contraste (mínimo): la presentación visual del texto y las imágenes de texto tiene una relación de contraste de al menos 4.5:1, excepto en los siguientes casos:
   * Texto grande: el texto y las imágenes de texto a gran escala mantienen una relación de contraste de al menos 3:1.
   * Secundario: el texto o las imágenes de texto que forman parte de un componente de interfaz de usuario inactivo, [decoración pura](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), no son visibles para nadie o forman parte de una imagen que contiene otro contenido visual significativo, no tienen requisitos de contraste.
   * Logotipos: El texto que forma parte de un logotipo o del nombre de una marca no cuenta con un requisito mínimo de contraste.

  >[!NOTE]
  >
  >Para obtener más información, consulte [Comprensión del contraste no textual](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html), a fin de garantizar que los autores de contenido entiendan los requisitos adicionales relacionados con los elementos no textuales (incluidos los iconos y los elementos de interfaz, entre otros).

#### Objetivo: Contraste (mínimo) (1.4.3)     {#purpose-contrast-minimum}

Las personas con ciertas deficiencias visuales quizá no puedan distinguir entre ciertos pares de colores de poco contraste. Estas personas pueden tener problemas de accesibilidad si ocurre lo siguiente:

* El texto contrasta poco con el color del fondo.
* El código de color del texto (como el texto con vínculo y el texto sin vínculo) es importante para distinguir la información.

>[!NOTE]
>
>El texto que se utiliza con fines puramente decorativos se excluye de estos criterios de éxito.

#### Cómo cumplir: Cumplir los criterios de contraste (Mínimo) (1.4.3)     {#how-to-meet-contrast-minimum}

Asegúrese de que el texto contraste lo suficiente con el fondo. Las relaciones de contraste dependen del tamaño y del estilo del texto en cuestión:

* Para los textos cuyo tamaño es menor de 18 puntos (o 14 puntos en negrita), la relación de contraste entre el texto o las imágenes del texto y el fondo debería ser de al menos 4.5:1.
* Para los textos cuyo tamaño es de al menos 18 puntos (o 14 puntos en negrita), la relación de contraste debería ser de al menos 3:1.
* Ante un fondo estampado, el fondo alrededor de cualquier texto debería estar sombreado para que la relación 4.5:1 o 3:1 se mantenga.

>[!NOTE]
>
>Recuerde que las fuentes pueden diferir en la forma en que representan el tamaño equivalente de PT/PX/EM.
>
>Utilice el buen criterio y error en cuanto a la legibilidad y la facilidad de uso al seleccionar las fuentes adecuadas y el tamaño del contenido web.

>[!NOTE]
>
>Los siguientes sitios pueden ayudar con las conversiones a otras unidades:
>
>* Calculadora de [Px a Em - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* Consulte &quot;Conversión de tamaño de fuente: pixel-point-em-rem-percent&quot; en `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`
>* Consulte PMtoEM.com: Conversión de PX a EM simplificada en `http://pxtoem.com/`

Para comprobar los niveles de contraste, utilice una herramienta de contraste de color como el programa [Paciello Group Color Contrast Analyzer](https://www.paciellogroup.com/resources/contrast-analyser.html) o el [verificador de contraste de color WebAIM](https://webaim.org/resources/contrastchecker/). Estas herramientas permiten comprobar pares de colores e informar sobre cualquier problema de contraste.

Alternativamente, si no le preocupa especificar la apariencia de su página, puede optar por no especificar el color del fondo o del texto en primer plano. No es necesario comprobar el contraste, ya que el explorador del usuario determina los colores del texto y del fondo.

Si no es posible alcanzar los niveles de contraste recomendados, proporcione un vínculo a una versión alternativa y equivalente de la página (que no tenga problemas con el contraste de color). O bien, permita que el usuario ajuste el contraste de la combinación de colores de la página a sus propios requisitos.

#### Más información: Contraste (mínimo) (1.4.3)     {#more-information-contrast-minimum}

* [Entender los criterios de éxito 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Cumplir los criterios de éxito 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Cambiar el tamaño del texto (1.4.4)  {#resize-text}

* Criterios de éxito 1.4.4
* Nivel A
* Cambiar el tamaño del texto: Excepto para subtítulos e imágenes de texto, se puede cambiar el tamaño del texto sin tecnología de asistencia hasta un 200 % sin perder contenido o funcionalidad.

#### Objetivo: Cambiar el tamaño del texto (1.4.4) {#purpose-resize-text}

La intención de este criterio de éxito es garantizar que el texto procesado visualmente, incluidos los controles basados en texto (caracteres de texto que se han mostrado para que se puedan ver [frente a caracteres de texto que siguen en formato de datos como ASCII]), se pueda escalar correctamente para que personas con discapacidades visuales leves puedan leerlo directamente sin necesidad de utilizar tecnología de asistencia, como un ampliador de pantalla. Los usuarios pueden beneficiarse de escalar todo el contenido de la página web, pero el texto es lo fundamental.

#### Cómo cumplir: Cambiar el tamaño del texto (1.4.4) {#how-to-meet-resize-text}

Además de seguir las directrices de [Cómo cumplir los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text), puede recomendar a los autores de contenido que utilicen anchos y alturas flexibles en los diseños de página y tamaños de fuente (por ejemplo, diseño web adaptable) para permitir a los lectores cambiar el tamaño del texto.

#### Más información: Cambiar el tamaño del texto (1.4.4) {#more-information-resize-text}

* [Entender los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Cumplir los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Imágenes de texto (1.4.5)          {#images-of-text}

* Criterios de éxito 1.4.5
* Nivel AA
* Imágenes de texto: si las tecnologías que se utilizan consiguen la presentación visual, el texto se utiliza para proporcionar información (y no las imágenes de texto), excepto en los casos siguientes:
   * Personalizable: la imagen de texto se puede personalizar visualmente según los requisitos del usuario.
   * Esencial: una presentación de texto en concreto resulta esencial para que se transmita la información.

>[!NOTE]
>
>Los logotipos (texto que forma parte de un logotipo o de un nombre de marca) se consideran esenciales.

#### Objetivo: Imágenes de texto (1.4.5)          {#purpose-images-of-text}

Las imágenes de texto normalmente se utilizan cuando se prefiere un estilo de texto en particular; por ejemplo, un logotipo, o si un texto se ha generado desde otra fuente (por ejemplo, un documento físico escaneado). Sin embargo, comparadas con el texto presentado en HTML y cuyo estilo utiliza CSS, las imágenes de texto carecen de la flexibilidad de cambiar su tamaño o apariencia, lo que podría resultar necesario para las personas con deficiencias visuales o dificultades de lectura.

#### Cómo cumplir: Imágenes de texto (1.4.5)       {#how-to-meet-images-of-text}

Si es necesario utilizar imágenes de texto, utilice CSS para reemplazar las imágenes de texto con texto equivalente en HTML y así el texto estará disponible en un modo personalizable. Por ejemplo, vea [C30: usar CSS para reemplazar texto con imágenes de texto y proporcionar controles de interfaz de usuario para cambiar](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Más información: Imágenes de texto (1.4.5)          {#more-information-images-of-text}

* [Entender los criterios de éxito 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Cumplir los criterios de éxito 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principio 2: operable          {#principle-operable}

[Principio 2: operable. Los componentes y la navegación de interfaz de usuario deben ser operables.](https://www.w3.org/TR/WCAG/#operable)

### Teclado accesible (2.1) {#keyboard-accessible}

[Directriz 2.1 Teclado accesible: Haga que toda la funcionalidad esté disponible desde un teclado.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Se trata de garantizar que los usuarios puedan acceder a todas las funciones mediante un teclado.

### Teclado (2.1.1)  {#keyboard}

* Criterios de éxito 2.1.1
* Nivel A
* Teclado: Toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para presionar teclas individuales, excepto si la función subyacente requiere una entrada que depende de la ruta del movimiento del usuario y no solo de los extremos.

#### Objetivo: Teclado (2.1.1) {#purpose-keyboard}

La intención de este criterio de éxito es garantizar que, siempre que sea posible, el contenido se pueda utilizar mediante un teclado o una interfaz de teclado (de modo que se pueda utilizar un teclado alternativo). Si el contenido se puede utilizar mediante un teclado o un teclado alternativo, lo pueden utilizar personas sin visión (que no pueden utilizar dispositivos como ratones que requieran coordinación mano-ojo), así como personas que deben utilizar teclados alternativos o dispositivos de entrada que actúen como emuladores de teclado. Los emuladores de teclado incluyen software de entrada de voz, software de sorbo y soplo, teclados en pantalla, software de digitalización y una variedad de tecnologías de asistencia y teclados alternativos. Las personas con visión reducida también pueden tener problemas para seguir un puntero, y les resulta mucho más fácil (o lo único posible) el uso de software si pueden controlarlo desde el teclado.

#### Cómo cumplir: Teclado (2.1.1) {#how-to-meet-keyboard}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Más información: Teclado (2.1.1) {#more-information-keyboard}

* [Entender los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Cumplir los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Sin trampas para el foco del teclado (2.1.2)  {#no-keyboard-trap}

* Criterios de éxito 2.1.2
* Nivel A
* Sin trampas para el foco del teclado: Si es posible mover el foco a un componente de la página usando una interfaz de teclado, entonces el foco se puede quitar de ese componente usando solo la interfaz de teclado y, si se requiere algo más que las teclas de dirección o de tabulación, u otros métodos de salida estándar, se informa al usuario el método apropiado para mover el foco.

#### Objetivo: Sin trampas para el foco del teclado (2.1.2) {#purpose-no-keyboard-trap}

La intención de este criterio de éxito es garantizar que el contenido no *atrape* el foco del teclado dentro de subsecciones de contenido en una página web. Este es un problema común cuando se combinan múltiples formatos en una página y son procesados por complementos o aplicaciones incrustados.

Puede haber ocasiones en que la funcionalidad de la página web restrinja el enfoque a una subsección del contenido (por ejemplo, un cuadro de diálogo modal). En estos casos, debe proporcionar al usuario un método para que pueda salir de esa subsección de contenido (por ejemplo, la tecla ESC cierra el cuadro de diálogo modal o un botón Cerrar cierra el cuadro de diálogo modal).

#### Cómo cumplir: Sin trampas para el foco del teclado (2.1.2) {#how-to-meet-no-keyboard-trap}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Más información: Sin trampas para el foco del teclado (2.1.2) {#more-information-no-keyboard-trap}

* [Entender los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Cumplir los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Tiempo suficiente (2.2) {#enough-time}

[Directrices 2.2 Tiempo suficiente: Proporcione a los usuarios tiempo suficiente para leer y usar el contenido.](https://www.w3.org/TR/WCAG/#enough-time)

Esto trata de garantizar que los usuarios tengan tiempo suficiente para leer y realizar acciones.

### Tiempo ajustable (2.2.1)  {#timing-adjustable}

* Criterios de éxito 2.2.1
* Nivel A
* Teclado: Proporcionar a los usuarios tiempo suficiente para leer y utilizar el contenido.

#### Objetivo: Tiempo ajustable (2.2.1) {#purpose-timing-adjustable}

La intención de este criterio de éxito es garantizar que los usuarios con discapacidad tengan tiempo suficiente para interactuar con el contenido web siempre que sea posible. Las personas con discapacidades como ceguera, visión reducida, impedimentos de destreza y limitaciones cognitivas pueden requerir más tiempo para leer contenido o, por ejemplo, completar formularios en línea. Si las funciones web dependen del tiempo, será más difícil para algunos usuarios realizar las acciones requeridas antes de alcanzar el límite de tiempo. Esto puede impedirles el acceso al servicio. Diseñar funciones que no dependan del tiempo ayudará a las personas con discapacidad a completar estas funciones. Proporcionar opciones para deshabilitar los límites de tiempo, personalizar la duración de los límites de tiempo o solicitar más tiempo antes de alcanzar un límite de tiempo, ayuda a los usuarios que necesitan más tiempo del esperado a completar correctamente las tareas. Estas opciones se enumeran en el orden en que resulten más útil para el usuario. Deshabilitar los límites de tiempo es mejor que personalizar su duración, que es mejor que solicitar más tiempo antes de alcanzar el límite de tiempo.

#### Cómo cumplir: Calendario ajustable (2.2.1) {#how-to-meet-timing-adjustable}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Más información: Tiempo ajustable (2.2.1) {#more-information-timing-adjustable}

* [Entender los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Cumplir los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausar, parar, ocultar (2.2.2)          {#pause-stop-hide}

* Criterios de éxito 2.2.2
* Nivel A
* Pausar, parar, ocultar: Para mover, cerrar, desplazar o actualizar automáticamente la información, los siguientes criterios son verdaderos:  
   * Movimiento, parpadeo, desplazamiento: para cualquier información de movimiento, parpadeo o desplazamiento que
      * (a) se inicia automáticamente,
      * (b) dure más de cinco segundos, y
      * (C) se presente en paralelo con otros contenidos,
existe un mecanismo para que el usuario lo ponga en pausa, lo detenga o lo oculte a menos que el movimiento, el parpadeo o el desplazamiento formen parte de una actividad en la que sea esencial;
   * Actualización automática: para cualquier información de actualización automática que
      * (a) se inicie automáticamente, y
      * (b) se presente en paralelo con otros contenidos
existe un mecanismo para que el usuario lo ponga en pausa, lo detenga, lo oculte o controle la frecuencia de la actualización a menos que la actualización automática forme parte de una actividad en la que sea esencial.

Puntos que se deben tener en cuenta:

1. Para ver los requisitos relacionados con contenidos que parpadean, consulte No diseñar contenido de manera que cause parpadeos (2.3).
1. Ya que cualquier contenido que no cumpla estos criterios de éxito puede interferir en la capacidad de un usuario para utilizar toda una página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe obedecerlos. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG20/#cc5).
1. El contenido que se actualiza periódicamente a través del software o que se transmite al usuario no necesita preservar o presentar la información que se genera o se recibe entre la iniciación de la pausa y la reanudación de la presentación, puesto que puede no ser técnicamente posible y en muchas situaciones podría ser engañoso.
1. Una animación en una fase de precarga o en una situación similar se consideraría esencial si la interacción no se pudiera dar durante dicha fase para todos los usuarios, y si no indicara el progreso, podría confundirlos o llevarles a pensar que el contenido se ha congelado o estropeado.

#### Objetivo: Pausar, parar, ocultar (2.2.2)     {#purpose-pause-stop-hide}

Algunos usuarios pueden considerar que el contenido que se mueve distrae o dificulta la concentración en otras partes de la página. Además, dicho contenido puede ser difícil de leer para quienes tienen problemas para seguir un texto que se mueve.

#### Cómo cumplir: Pausar, parar, ocultar (2.2.2)     {#how-to-meet-pause-stop-hide}

Según la naturaleza del contenido, se puede aplicar una o varias de las siguientes sugerencias al crear páginas web con contenido que se mueve, que es intermitente o parpadea:

* Proporcionar la manera de pausar el movimiento del contenido y dar a los usuarios tiempo suficiente para leerlo. Por ejemplo, tableros de noticias, texto que se actualiza automáticamente y carruseles de imágenes que avanzan automáticamente.
* Asegúrese de que el contenido que parpadea deja de hacerlo tras cinco segundos.
* Use tecnologías adecuadas para mostrar el contenido parpadeante que se puede mostrar en el navegador. Por ejemplo, archivos de Formato de intercambio de gráficos (GIF) o Gráficos de red portátiles animados (APNG).
* Proporcione un control de formulario en la página web para permitir que el usuario desactive cualquier contenido que parpadee en la página.
* Si lo anterior no es posible, proporcione un vínculo a la página que contenga todo el contenido pero sin parpadeos.

#### Más información: Pausar, parar, ocultar (2.2.2)     {#more-information-pause-stop-hide}

* [Entender los criterios de éxito 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Cumplir los criterios de éxito 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Parpadeos y reacciones físicas (2.3) {#seizures-and-physcial-reactions}

[Directrices 2.3 Parpadeos: No diseñar contenido de manera que se conozca que cause parpadeos o reacciones físicas.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Tres parpadeos o por debajo del umbral (2.3.1)     {#three-flashes-or-below-threshold}

* Criterios de éxito 2.3.1
* Nivel A
* Tres parpadeos o Por debajo del umbral: las páginas web no contienen ningún elemento que parpadee más de tres veces en el intervalo de un segundo o que el parpadeo esté por debajo del umbral general de parpadeo y parpadeo en rojo.

>[!NOTE]
>
>Ya que cualquier contenido que no cumpla este criterio de éxito puede interferir en la capacidad de un usuario para utilizar toda la página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe cumplir este criterio de éxito. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG/#cc5).

#### Objetivo: Tres parpadeos o Por debajo de los límites (2.3.1) {#purpose-three-flashes-or-below-threshold}

En ciertos casos, el contenido intermitente puede causar convulsiones fotosensibles. Este criterio de éxito permite a los usuarios acceder y experimentar todo el contenido sin tener que preocuparse acerca del contenido intermitente.

#### Cómo cumplir: Tres parpadeos o por debajo del umbral (2.3.1)     {#how-to-meet-three-flashes-or-below-threshold}

Siga estos pasos para asegurarse de que se aplican las siguientes técnicas:

* Asegúrese de que los componentes no parpadean más de tres veces durante el intervalo de un segundo;
* Si no se cumple la condición anterior, muestre el contenido parpadeante en una *zona pequeña y segura* en píxeles en la pantalla. Esta área se calcula mediante una fórmula compleja, incluida en [G176: Mantener el área de parpadeo lo suficientemente pequeña](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), por lo que esta técnica solo se debe seguir si el contenido que parpadea es *necesario.

#### Más información: Tres parpadeos o por debajo de los límites (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Entender los criterios de éxito 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Cumplir los criterios de éxito 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navegable (2.4) {#navigable}

[Directriz 2.4 navegable: Proporcione formas de ayudar a los usuarios a navegar, buscar contenido y determinar dónde se encuentran.](https://www.w3.org/TR/WCAG/#navigable)

Esto garantiza que el contenido sea fácil y sencillo de navegar para los usuarios.

### Omitir bloques (2.4.1)  {#bypass-blocks}

* Criterios de éxito 2.4.1
* Nivel A
* Omitir bloques: Existe un mecanismo disponible para evitar bloques de contenido que se repiten en varias páginas web.

#### Objetivo: Omitir bloques (2.4.1) {#purpose-bypass-blocks}

La intención de este criterio de éxito es permitir que las personas que navegan secuencialmente a través del contenido tengan un acceso más directo al contenido principal de la página web. Las páginas web y las aplicaciones suelen tener contenido que aparece en otras páginas o pantallas. Entre otros, algunos ejemplos de bloques de contenido repetidos son los vínculos de navegación, los gráficos de encabezados y los marcos publicitarios. Las secciones pequeñas repetidas, como palabras individuales, frases o vínculos únicos, no se consideran bloques a efectos de esta disposición.

#### Cómo cumplir: Omitir bloques (2.4.1) {#how-to-meet-bypass-blocks}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Más información: Omitir bloques (2.4.1) {#more-information-bypass-blocks}

* [Entender los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Cumplir los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Página titulada (2.4.2)          {#page-titled}

* Criterios de éxito 2.4.2
* Nivel A
* Página con títulos: las páginas web tienen títulos que describen el tema o el objetivo.

#### Objetivo: Página titulada (2.4.2)     {#purpose-page-titled}

Este criterio de éxito ayuda a todo el mundo, independientemente de cualquier discapacidad en concreto, a identificar de manera rápida el contenido de una página web sin tener que leerla entera. Es particularmente útil cuando se abren varias páginas web en pestañas del explorador, ya que el título de la página se muestra en la pestaña y por eso se puede localizar rápidamente.

#### Cómo cumplir: Página con título (2.4.2)     {#how-to-meet-page-titled}

Al crear una página HTML nueva en AEM, se puede especificar el título de la página. Asegúrese de que el título describa adecuadamente el contenido de la página para que los usuarios puedan identificar rápidamente si el contenido es relevante o no para sus necesidades.

También puede editar el título de página al editarla. Se puede acceder a él mediante **Información de página** - **Propiedades.**

#### Más información: Página titulada (2.4.2) {#more-information-page-titled}

* [Entender los criterios de éxito 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Cumplir los criterios de éxito 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Orden de enfoque (2.4.3)  {#focus-order}

* Criterios de éxito 2.4.3
* Nivel A
* Orden de enfoque: Si una página web se puede navegar secuencialmente y las secuencias de navegación afectan al significado o al funcionamiento, los componentes enfocables reciben atención en un orden que preserva el significado y la operabilidad.

#### Objetivo: Orden de enfoque (2.4.3) {#purpose-focus-order}

La intención de este criterio de éxito es garantizar que, cuando los usuarios naveguen secuencialmente por el contenido, encuentren información en un orden que sea coherente con el significado del contenido y se pueda utilizar desde el teclado. Esto reduce la confusión al permitir que los usuarios formen un modelo mental coherente del contenido. Puede haber diferentes pedidos que reflejen las relaciones lógicas en el contenido. Por ejemplo, el desplazamiento por componentes en un formulario en línea compuesto de varios campos o pasos refleja las relaciones lógicas del contenido.

#### Cómo cumplir: Orden de enfoque (2.4.3) {#how-to-meet-focus-order}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Más información: Orden de enfoque (2.4.3) {#more-information-focus-order}

* [Entender los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Cumplir los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Objetivo del vínculo (en contexto) (2.4.4)                    {#link-purpose-in-context}

* Criterios de éxito 2.4.4
* Nivel A
* Objetivo del vínculo (en contexto): el objetivo de cada vínculo se puede determinar por el texto del vínculo en sí o por el texto junto al contexto del vínculo determinado programáticamente, excepto cuando sea ambiguo para los usuarios en general.

#### Objetivo: Objetivo del vínculo (en contexto) (2.4.4)          {#purpose-link-purpose-in-context}

Para todos los usuarios, independientemente de su discapacidad, es vital indicar claramente la dirección de un vínculo a través de un texto adecuado. Esto ayuda a los usuarios a decidir si quieren seguir el vínculo o no. Para los usuarios con visión normal, un texto para el vínculo con sentido es útil cuando hay varios vínculos en una página (particularmente si la página está muy cargada de texto), ya que el texto del vínculo con sentido proporciona una indicación más clara de la funcionalidad del destino de la página. Los usuarios de algunas tecnologías de asistencia, que pueden generar una lista de todos los vínculos en una sola página, pueden comprender más fácilmente el texto del vínculo fuera de contexto si el texto del vínculo es único e informativo. Sin embargo, los individuos con discapacidades cognitivas pueden confundirse si un vínculo no proporciona suficiente información para describir con precisión adónde los llevará.

#### Cómo cumplir: Objetivo del vínculo (en contexto) (2.4.4)       {#how-to-meet-link-purpose-in-context}

Sobre todo, es importante asegurarse de que el objetivo de un vínculo se describe con claridad en el texto del vínculo.

* Ejemplo incorrecto:
   * Texto: para obtener más información sobre las clases nocturnas de otoño de 2010, haga clic aquí.
   * Motivo: no indica el destino claramente y resulta ambiguo.
* Ejemplo correcto:
   * Texto: Clases nocturnas de otoño de 2010, más información.
   * Motivo: ajustando ligeramente el texto y la posición del vínculo se puede mejorar el texto del vínculo.

Los vínculos deben redactarse de forma coherente en todas las páginas, especialmente en las barras de navegación. Por ejemplo, si un vínculo a una página específica se denomina **Publicaciones** en una página, use ese texto en otras páginas para asegurar la coherencia.

En el momento de escribir este artículo, existen algunos problemas relacionados con el uso de atributos de título para garantizar que vínculos similares presentados en una página proporcionen información única sobre el destino (por ejemplo, &quot;leer más&quot; se referirá a menudo a un rango de destinos diferentes):

* El texto contenido en el atributo del título solo está disponible para los usuarios que utilizan el ratón como información del objeto emergente y no se puede acceder a él mediante el teclado, ni tampoco los usuarios de dispositivos móviles.
* Los lectores de pantalla pueden leer en voz alta los atributos de título, pero esta funcionalidad puede que no se permita de forma predeterminada, por lo que los usuarios quizá no están al tanto de que existe un atributo en el título.
* Es difícil cambiar la apariencia del texto del título, lo que quiere decir que puede resultar complicado o imposible de leer para algunas personas.

Por lo tanto, aunque el atributo del título se puede utilizar para proporcionar contexto adicional a un vínculo, tenga en cuenta sus limitaciones y no lo utilice como alternativa al vínculo de un texto.

Cuando el vínculo esté formado por una imagen, asegúrese de que el texto alternativo de la imagen describa el destino del vínculo. Por ejemplo, si la imagen de una estantería se establece como vínculo a las publicaciones de una persona, el texto alternativo debería ser **Publicaciones de John Smith** y no **Estantería**.

Alternativamente, si el anclaje del vínculo contiene texto que describe el objetivo del vínculo, además de la imagen (y por ello aparece junto a la imagen), utilice un atributo alternativo vacío para la imagen:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>El fragmento anterior representa una ilustración; es recomendable utilizar el componente **Imagen**.

Aunque se recomienda proporcionar un texto para el vínculo que identifique su objetivo sin necesidad de contexto adicional, no siempre es posible. Los vínculos de contexto libre se pueden utilizar en los casos siguientes, cuyos ejemplos HTML se pueden encontrar en [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* El texto del vínculo forma parte de una lista de vínculos relacionados y cuando el elemento de la lista que incluye el vínculo proporciona contexto suficiente.
* El propósito de un vínculo se puede identificar claramente a partir del párrafo *anterior* (no del siguiente).
* El vínculo está contenido en una tabla de datos y, por lo tanto, el propósito puede identificarse claramente desde los encabezados asociados.
* Una lista de vínculos está contenida dentro de un conjunto de encabezados y el propio encabezado proporciona un contexto adecuado.
* Una lista de vínculos está contenida dentro de un vínculo anidado y el elemento de lista principal encima del vínculo anidado proporciona un contexto adecuado.

En algunos casos en los que hay varios vínculos en una misma página (cada uno de los cuales proporciona la dirección de un vínculo con detalles complejos pero necesarios), puede resultar adecuado proporcionar una versión alternativa de la página web que muestre exactamente el mismo contenido pero donde el texto del vínculo no sea tan detallado.

También puede utilizar secuencias de comandos para proporcionar una cantidad mínima de texto en el vínculo. Al activar un control apropiado colocado hacia la parte superior de la página, el texto del vínculo se *expande* hacia más detalles. Un enfoque similar es usar CSS para *ocultar* el vínculo completo de los usuarios con visión, pero aun así imprimirlo en su totalidad para los usuarios del lector de pantalla. Esto queda fuera del ámbito de este documento, pero puede encontrar más información sobre cómo se puede lograr en la sección [Más información: objetivo del vínculo (en contexto) (2.4.4)](#more-information-link-purpose-in-context).

#### Más información: Objetivo del vínculo (en contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Entender los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Varias maneras (2.4.5)  {#multiple-ways}

* Criterios de éxito 2.4.5
* Nivel AA
* Múltiples maneras: Hay más de una manera de localizar una página web dentro de un conjunto de páginas web, excepto cuando la página web es el resultado de un proceso o un paso en él.

#### Objetivo: Varias maneras (2.4.5) {#purpose-multiple-ways}

La intención de este criterio de éxito es hacer posible que los usuarios localicen el contenido de la manera que mejor se adapte a sus necesidades. Los usuarios pueden encontrar una técnica más fácil o comprensible.

Incluso los sitios pequeños deben proporcionar a los usuarios algún medio de orientación. Para un sitio de tres o cuatro páginas, con todas las páginas vinculadas desde la página de inicio, puede ser suficiente simplemente proporcionar vínculos desde y hacia la página de inicio, donde los vínculos en la página de inicio también pueden servir como mapa del sitio.

#### Cómo cumplir: Múltiples formas (2.4.5) {#how-to-meet-multiple-ways}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Más información: Múltiples formas (2.4.5) {#more-information-multiple-ways}

* [Entender los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Cumplir los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Encabezados y etiquetas (2.4.6)  {#headings-and-labels}

* Criterios de éxito 2.4.6
* Nivel AA
* Encabezados y etiquetas: Los encabezados y las etiquetas describen el tema o el objetivo.

#### Objetivo: Encabezados y etiquetas (2.4.6) {#purpose-headings-and-labels}

La intención de este criterio de éxito es ayudar a los usuarios a comprender qué información se incluye en las páginas web y cómo se organiza dicha información. Si los encabezados son claros y descriptivos, los usuarios pueden encontrar la información que buscan más fácilmente y pueden comprender las relaciones entre las diferentes partes del contenido con mayor facilidad. Las etiquetas descriptivas ayudan a los usuarios a identificar componentes específicos dentro del contenido.

#### Cómo cumplir: Encabezados y etiquetas (2.4.6) {#how-to-meet-headings-and-labels}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Más información: Encabezados y etiquetas (2.4.6) {#more-information-headings-and-labels}

* [Entender los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Cumplir los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Enfoque visible (2.4.7)  {#focus-visible}

* Criterios de éxito 2.4.7
* Nivel AA
* Enfoque visible: Cualquier interfaz de usuario operable con el teclado tiene un modo de funcionamiento en el que el indicador de selección del teclado está visible.

#### Objetivo: Enfoque visible (2.4.7) {#purpose-focus-visible}

La intención de este criterio de éxito es ayudar a una persona a saber qué elemento tiene el enfoque del teclado.

Una persona debe saber cuál elemento de varios elementos tiene el enfoque del teclado. Si solo hay un control accionable por teclado en la pantalla, el criterio de éxito se cumpliría porque el diseño visual presenta solo un elemento procesable por teclado.

Si el criterio de éxito indica “modo de funcionamiento”, se tiene en cuenta para las plataformas que no siempre muestran un indicador de enfoque. Normalmente, solo hay un modo de funcionamiento, por lo que se aplican estos criterios de éxito.

#### Cómo cumplir: Enfoque visible (2.4.7) {#how-to-meet-focus-visible}

Siga las directrices de [Cómo cumplir los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Más información: Enfoque visible (2.4.7) {#more-information-focus-visible}

* [Entender los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Cumplir los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principio 3: comprensible          {#principle-understandable}

[Principio 3: Comprensible: la información y el funcionamiento de la interfaz del usuario deben ser comprensibles.](https://www.w3.org/TR/WCAG/#understandable)

### Hacer que el contenido del texto sea legible y comprensible (3.1)          {#make-text-content-readable-and-understandable}

[Directrices 3.1 Legible: hacer que el contenido del texto sea legible y comprensible.](https://www.w3.org/TR/WCAG/#readable)

### Idioma de la página (3.1.1)          {#language-of-page}

* Criterios de éxito 3.1.1
* Nivel A
* Idioma de la página: el lenguaje humano por defecto de cada página web se puede determinar programáticamente.

#### Objetivo: Idioma de la página (3.1.1)          {#purpose-language-of-page}

El objetivo de este criterio de éxito es asegurarse de que el texto y cualquier otro contenido lingüístico se introduce de manera correcta. Para los usuarios de lectores de pantalla, esto garantiza que el contenido se pronuncie correctamente, mientras que los navegadores visuales tienden a mostrar ciertos conjuntos de caracteres de manera adecuada.

#### Cómo cumplir: Idioma de la página (3.1.1)       {#how-to-meet-language-of-page}

Para cumplir este criterio de éxito, el idioma por defecto de una página web se puede identificar utilizando el atributo `lang` en el elemento `<html>` en la parte superior de la página. Por ejemplo:

* Si una página está escrita en inglés, el elemento `<html>` debería ser:
  `<html lang = "en">`

* Mientras que una página que se presentará en español debe adoptar el estándar siguiente:
  `<html lang = "es">`

En AEM, el idioma predeterminado de su página se configura cuando se crea la página, pero también se puede cambiar al editar [Propiedades de la página](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM ofrece un mayor perfeccionamiento para las variaciones de un idioma raíz. Por ejemplo, inglés estadounidense: en-us, inglés británico: en-gb e inglés canadiense: en-ca. Este nivel de detalle suele ser superfluo para la tecnología de asistencia, aunque puede utilizarse para variaciones regionales en el contenido de la página.

#### Más información: Idioma de la página (3.1.1) {#more-information-language-of-page}

* [Entender los criterios de éxito 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Cumplir los criterios de éxito 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Los códigos se basan en el código ISO 639-1. Encontrará una lista más extensa de códigos para cada idioma en el [sitio W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de las partes (3.1.2)      {#language-of-parts}

* Criterios de éxito 3.1.2
* Nivel AA
* Idioma de las partes: el lenguaje humano de cada pasaje o frase del contenido puede determinarse mediante programación. Las excepciones son nombres propios, términos técnicos, palabras de lenguaje indeterminado, y palabras o frases que se han convertido en parte de la lengua vernácula del texto inmediatamente circundante.

#### Objetivo: Idioma de las partes (3.1.2)   {#purpose-language-of-parts}

El propósito de este criterio de éxito es similar al del [Idioma de la página](#language-of-page), excepto que se aplica a páginas web que contienen contenido en varios idiomas en una sola página (por ejemplo, por las citas o préstamos poco frecuentes).

Las páginas que aplican este criterio de éxito permiten lo siguiente:

* Software de transición en braille para insertar caracteres acentuados.
* Los lectores de pantalla deben pronunciar las palabras que tienen caracteres especiales o que no están en el idioma predeterminado identificado en el nivel de página.
* Herramientas de traducción como Google Translate para traducir el contenido de manera correcta de un idioma a otro.

#### Cómo cumplir: Idioma de las partes (3.1.2)   {#how-to-meet-language-of-parts}

El atributo `lang` se puede utilizar para identificar los cambios en el idioma del contenido. Por ejemplo, una cita en alemán (ISO 639-1 código “de”) se puede mostrar de la manera siguiente:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Los bloques de citas no funcionan con las instancias listas para usarse. Se podría desarrollar un componente personalizado para admitir la función.

De manera similar, el navegador puede mostrar un préstamo poco común o una expresión correcta si el elemento `span` se utiliza de la manera siguiente:

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>No es necesario seguir este criterio de éxito al incluir nombres o ciudades en diferentes idiomas. O bien, cuando se usan préstamos o expresiones que ya son comunes en el idioma predeterminado, como *schadenfreude* en inglés.

Para añadir el elemento “span” (extensión), con un idioma adecuado, puede editar manualmente sus especificaciones HTML en el modo de edición de la fuente de RTE para que se lea como puede ver arriba. Alternativamente, el atributo `lang` se puede incluir en RTE a través de un administrador del sistema (consulte [Añadir ayuda para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Más información: Idioma de las partes (3.1.2) {#more-information-language-of-parts}

* [Entender los criterios de éxito 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Cumplir los criterios de éxito 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Predecible (3.2) {#predictable}

[Directriz 3.2 Predecible: Hacer que las páginas web aparezcan y funcionen de manera predecible.](https://www.w3.org/TR/WCAG/#predictable)

Esto trata de garantizar que las páginas web tengan un aspecto y un funcionamiento coherentes.

### Enfoque (3.2.1)  {#on-focus}

* Criterios de éxito 3.2.1
* Nivel A
* Enfoque: Cuando cualquier componente de interfaz de usuario recibe enfoque, no se inicia un cambio de contexto.

#### Objetivo: Enfoque (3.2.1) {#purpose-on-focus}

La intención de este criterio de éxito es garantizar que la funcionalidad sea predecible a medida que los visitantes navegan por un documento. Cualquier componente que pueda desencadenar un evento cuando se selecciona no debe cambiar el contexto. Algunos ejemplos de cambio de contexto cuando un componente recibe el enfoque son, entre otros:

* formularios enviados automáticamente cuando un componente recibe el enfoque;
* nuevas ventanas lanzadas cuando un componente recibe el enfoque;
* el enfoque se cambia a otro componente cuando ese componente recibe el enfoque;

El enfoque se puede mover a un control mediante el teclado (por ejemplo, presionando la tabulación hasta un control) o el ratón (por ejemplo, haciendo clic en un campo de texto). Mover el ratón sobre un control no desplaza el enfoque a menos que el script implemente este comportamiento. Para algunos tipos de controles, hacer clic en un control también puede activar el control (por ejemplo, botón), lo que a su vez puede iniciar un cambio en el contexto.

#### Cómo cumplir: Enfoque (3.2.1) {#how-to-meet-on-focus}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Más información: Enfoque (3.2.1) {#more-information-on-focus}

* [Entender los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Cumplir los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### Al recibir entradas (3.2.2)  {#on-input}

* Criterios de éxito 3.2.2
* Nivel A
* Al recibir entradas: Cambiar la configuración de cualquier componente de interfaz de usuario no provoca automáticamente un cambio de contexto a menos que se haya informado al usuario del comportamiento antes de utilizar el componente.

#### Objetivo: Al recibir entradas (3.2.2) {#purpose-on-input}

La intención de este criterio de éxito es garantizar que entrar datos o seleccionar un control de formulario tengan efectos predecibles. Cambiar la configuración de cualquier componente de interfaz de usuario cambia algún aspecto del control que persistirá cuando el usuario ya no interactúe con él. De este modo, activar una casilla de verificación, entrar texto en un campo de texto o cambiar la opción seleccionada en un control de lista, cambia su configuración, pero activar un vínculo o un botón no lo hace. Los cambios en el contexto pueden confundir a los usuarios que no perciben el cambio o que se distraen fácilmente con los cambios. Los cambios de contexto solo son adecuados cuando está claro que tal cambio se producirá en respuesta a la acción del usuario.

#### Cómo cumplir: Al recibir entradas (3.2.2) {#how-to-meet-on-input}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Más información: Al recibir entradas (3.2.2) {#more-information-on-input}

* [Entender los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Cumplir los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navegación coherente (3.2.3)  {#consistent-navigation}

* Criterios de éxito 3.2.3
* Nivel AA
* Navegación coherente: Los mecanismos de navegación que se repiten en varias páginas web dentro de un conjunto de páginas web se producen en el mismo orden relativo cada vez que se repiten, a menos que el usuario inicie un cambio.

#### Objetivo: Navegación coherente (3.2.3) {#purpose-consistent-navigation}

La intención de este criterio de éxito es fomentar el uso de una presentación y un diseño coherentes para los usuarios que interactúan con contenido repetido dentro de un conjunto de páginas web y deben localizar información o funcionalidad específicas más de una vez. Las personas con visión reducida que utilizan la ampliación de la pantalla para mostrar una pequeña parte de esta suelen usar indicaciones visuales y límites de página para localizar rápidamente el contenido repetido. La presentación de contenido repetido en el mismo orden también es importante para los usuarios visuales que usan la memoria espacial o las señales visuales en el diseño para localizar contenido repetido.

El uso de la frase &quot;el mismo orden&quot; en esta sección no implica que no se puedan usar los menús de subnavegación o que no se puedan usar bloques de navegación secundaria o de estructura de página. En su lugar, este criterio de éxito está diseñado para ayudar a los usuarios que interactúan con el contenido repetido en las páginas web, a poder predecir la ubicación del contenido que buscan. Y, para encontrarlo más rápido cuando lo encuentren de nuevo.

Los usuarios pueden iniciar un cambio en el orden utilizando agentes de usuario adaptables o estableciendo preferencias para que la información se presente de una manera que les resulte más útil.

#### Cómo cumplir: Navegación coherente (3.2.3) {#how-to-meet-consistent-navigation}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Más información: Navegación coherente (3.2.3) {#more-information-consistent-navigation}

* [Entender los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Cumplir los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identificación coherente (3.2.4)  {#consistent-identification}

* Criterios de éxito 3.2.4
* Nivel A
* Identificación coherente: Los componentes que tienen la misma funcionalidad dentro de un conjunto de páginas web se identifican de manera coherente.

#### Objetivo: Identificación coherente (3.2.4) {#purpose-consistent-identification}

La intención de este criterio de éxito es garantizar la identificación coherente de los componentes funcionales que aparecen repetidamente dentro de un conjunto de páginas web. Una estrategia que las personas que utilizan lectores de pantalla cuando administran un sitio web consiste en confiar en gran medida en su familiaridad con las funciones que pueden aparecer en diferentes páginas web. Si funciones idénticas tienen etiquetas diferentes (o, en términos más generales, un nombre accesible diferente) en páginas web diferentes, el sitio será considerablemente más difícil de usar. También puede ser confuso y aumentar la carga cognitiva para las personas con limitaciones cognitivas. Por lo tanto, un etiquetado coherente puede ser de gran ayuda.

Esta coherencia se extiende a las alternativas textuales. Si los íconos u otros elementos no textuales tienen la misma funcionalidad, las alternativas textuales también deben ser coherentes.

Si hay dos componentes en una página web que tienen la misma funcionalidad que un componente en otra página en un conjunto de páginas web, entonces los 3 deben ser coherentes. Por lo tanto, los dos en la misma página serán coherentes.

Aunque es deseable y es una práctica recomendada siempre ser coherente dentro de una sola página web, 3.2.4 solo aborda la coherencia dentro de un conjunto de páginas web en las que algo se repite en más de una página del conjunto.

#### Cómo cumplir: Identificación coherente (3.2.4) {#how-to-meet-consistent-identification}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Más información: Identificación coherente (3.2.4) {#more-information-consistent-identification}

* [Entender los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Cumplir los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Asistencia de entrada (3.3) {#input-assistance}

[Directrices 3.3 Asistencia de la entrada: ayudar a los usuarios a evitar y corregir errores.](https://www.w3.org/TR/WCAG/#input-assistance)

### Identificación de errores (3.3.1)  {#error-identification}

* Criterios de éxito 3.3.1
* Nivel A
* Identificación de errores: Si se detecta automáticamente un error de entrada, se identifica el elemento que está en error y el error se describe al usuario en el texto.

#### Objetivo: Identificación de errores (3.3.1) {#purpose-error-identification}

La intención de este criterio de éxito es garantizar que los usuarios sean conscientes de que se ha producido un error y puedan determinar lo que está mal. El mensaje de error debe ser lo más específico posible. Si el envío del formulario no se ha realizado correctamente, la visualización del formulario y la indicación de los campos en los que se ha producido un error no bastan para que algunos usuarios perciban que se ha producido un error. Los usuarios del lector de pantalla, por ejemplo, no sabrán que hubo un error hasta que encuentren uno de los indicadores. Es posible que abandonen el formulario por completo antes de encontrar el indicador de error, pensando que la página simplemente no funciona. Según la definición de WCAG, un [error de entrada](https://www.w3.org/TR/WCAG/#dfn-input-error) es información proporcionada por el usuario que no se acepta. Esto incluye lo siguiente.

Información requerida por la página web pero omitida por el usuario, o información proporcionada por el usuario pero que se encuentra fuera del formato de datos requerido o de los valores permitidos.
Por ejemplo:

* el usuario no puede introducir la abreviatura adecuada en el campo estado, provincia o región;
* el usuario introduce una abreviatura de estado que no es un estado válido;
* el usuario introduce un código postal inexistente;
* el usuario introduce una fecha de nacimiento 2 años en el futuro;
* el usuario introduce caracteres alfabéticos o paréntesis en su campo de número de teléfono que solo acepta números;
* el usuario introduce una oferta que está por debajo de la oferta anterior o del incremento mínimo de la oferta.

#### Cómo cumplir: Identificación de errores (3.3.1) {#how-to-meet-error-identification}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Más información: Identificación de error (3.3.1) {#more-information-error-identification}

* [Entender los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Cumplir los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etiquetas o instrucciones (3.3.2)   {#labels-or-instructions}

* Criterios de éxito 3.3.2
* Nivel A
* Etiquetas o instrucciones: se proporcionan cuando el contenido requiere la introducción de datos por parte del usuario.

#### Objetivo: Etiquetas o instrucciones (3.3.2)   {#purpose-labels-or-instructions}

Proporcionar instrucciones para ayudar a las personas a completar formularios es una parte fundamental de las prácticas recomendadas en el uso de la interfaz. Hacer esto es particularmente beneficioso para quienes sufren discapacidad visual o cognitiva, ya que de otra manera experimentarían dificultades para entender la estructura de un formulario y el tipo de datos que se proporcionan en un campo del formulario en concreto.

##### Forms

De manera predeterminada, en el proyecto de demostración AEM WKND, se añade una etiqueta al añadir un componente de formulario, como **Campo de texto**, a la página. Este título predeterminado depende del tipo de componente. Puede añadir su propio título en la pestaña **Título y texto** del cuadro de diálogo de edición de ese campo. Es importante asegurarse de que las etiquetas ayudan a los usuarios a entender los datos que se asocian con cada componente del formulario.

Este campo de **Título** debe utilizarse para elementos de campo, ya que proporciona una etiqueta disponible para la tecnología de asistencia. No basta con escribir una etiqueta en el texto junto al campo.

Para algunos componentes de formulario, también es posible ocultar visualmente las etiquetas mediante la casilla de verificación **Ocultar título**. Las etiquetas ocultas de esta forma siguen estando disponibles para la tecnología de asistencia, pero no se muestran en la pantalla. Aunque este enfoque puede ser bueno en algunas situaciones, es mejor incluir una etiqueta visual siempre que sea posible, ya que algunos usuarios pueden estar mirando una pequeña sección de la pantalla (un campo a la vez) y necesitan las etiquetas para identificar el campo correctamente.

###### Botones de imagen {#image-buttons}

Cuando se utilizan botones de imagen (por ejemplo, el componente **Botón de imagen** del proyecto WKND), el campo **Título** de la pestaña **Título y texto** del cuadro de diálogo de edición proporciona el texto alternativo de la imagen, en lugar de la etiqueta. Por eso, en el ejemplo siguiente, la imagen con el texto `Submit` contiene el texto alternativo `Submit`, que se ha añadido utilizando el campo **Título** en el diálogo de edición.

###### Grupos de campos de formulario {#groups-of-form-fields}

En el proyecto WKND, si hay un grupo de controles relacionados, como el **Grupo de radio**, puede ser necesario un título para el grupo, así como controles individuales. Al agregar un conjunto de botones de radio en AEM, el campo **Título** proporciona este título de grupo, mientras que los títulos individuales se especifican a medida que se crean los botones de radio (**Elementos**).

Sin embargo, no existe una asociación programática entre el título del grupo y los botones de opción. Los editores de plantillas deben envolver el título en las etiquetas `fieldset` y `legend` necesarias para crear esta asociación, que solo se puede hacer editando el código fuente de la página. Alternativamente, un administrador del sistema puede añadir soporte a estos elementos para que aparezcan en el diálogo **Propiedades del campo** (consulte [Añadir ayuda para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

###### Consideraciones adicionales para Formularios {#additional-considerations-for-forms}

Si se introducen datos en un formato concreto, especifíquelo en el texto de la etiqueta. Por ejemplo, si se tiene que introducir una fecha en formato `DD-MM-YYYY`, especifíquelo como parte de la etiqueta. Esto significa que cuando los usuarios de lectores de pantalla se encuentran con el campo, la etiqueta se anuncia automáticamente, junto con la información adicional sobre el formato.

Si es obligatorio introducir datos en un campo de formulario, especifíquelo utilizando la palabra obligatorio como parte de la etiqueta. AEM añade un asterisco cuando un campo es obligatorio, pero sería ideal incluir la palabra `required` en la etiqueta (en el campo **Título** del diálogo de edición).

La colocación de las etiquetas también es importante, ya que les ayuda a localizar los campos adecuados. Esto es de particular importancia cuando el usuario se enfrenta a un formulario complejo. Siga la convención siguiente:

* Casillas o botones de opciones: 
Las etiquetas se colocan inmediatamente a la derecha del campo.
* Otros componentes del formulario (por ejemplo, cuadros de texto o cuadros combinados): 
Las etiquetas se colocan inmediatamente encima o bien a la izquierda del campo.

En formularios simples con funcionalidad limitada, etiquetar correctamente un botón `Submit` puede actuar como una etiqueta para el campo adyacente (por ejemplo, `Search`). Resulta útil cuando puede ser difícil encontrar espacio para el texto de una etiqueta.

#### Más información: Etiquetas o instrucciones (3.3.2)   {#more-information-labels-or-instructions}

* [Entender los criterios de éxito 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Cumplir los criterios de éxito 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Sugerencias ante errores (3.3.3)  {#error-suggestion}

* Criterios de éxito 3.3.3
* Nivel AA
* Teclado: Si se detecta automáticamente un error de entrada y se conocen sugerencias para la corrección, estas se proporcionan al usuario, a menos que ello ponga en peligro la seguridad o el propósito del contenido.

#### Objetivo: Sugerencias ante errores (3.3.3) {#purpose-error-suggestion}

La intención de este criterio de éxito es garantizar que los usuarios reciban las sugerencias adecuadas para la corrección de un error de entrada, si es posible. La definición de WCAG de [error de entrada](https://www.w3.org/TR/WCAG/#dfn-input-error) indica que es &quot;información proporcionada por el usuario que no es aceptada&quot; por el sistema. Algunos ejemplos de información no aceptada incluyen la información que es necesaria pero que el usuario omite, y la información que el usuario proporciona pero que no corresponde al formato de datos requerido o a los valores permitidos.

Los criterios de éxito 3.3.1 permiten la notificación de errores. Sin embargo, a las personas con limitaciones cognitivas les puede resultar difícil entender cómo corregir errores. Es posible que las personas con discapacidad visual no puedan averiguar exactamente cómo corregir el error. Si el envío del formulario no se ha realizado correctamente, los usuarios pueden dejar el formulario al no estar seguros de cómo corregir el error aunque sepan que se ha producido.

El autor del contenido puede proporcionar la descripción del error, o el agente de usuario puede proporcionar la descripción del error en función de la información específica de la tecnología y determinada mediante programación.

#### Cómo cumplir: Sugerencias ante errores (3.3.3) {#how-to-meet-error-suggestion}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Más información: Sugerencias ante errores (3.3.3) {#more-information-error-suggestion}

* [Entender los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Cumplir los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prevención de errores (legal, financiero, de datos) (3.3.4)  {#error-prevention-legal-financial-data}

* Criterios de éxito 3.3.4
* Nivel AA
* Prevención de errores (legal, financiero, datos): Para las páginas web que provocan compromisos legales o transacciones financieras para el usuario, que modifican o eliminan datos controlables por el usuario en sistemas de almacenamiento de datos o que envían respuestas de prueba del usuario, al menos una de las siguientes opciones es verdadera:

   * Reversible
Los envíos son reversibles.
   * Comprobado
Se comprueba si los datos introducidos por el usuario tienen errores de entrada y se le ofrece al usuario la oportunidad de corregirlos.
   * Confirmado
Existe un mecanismo disponible para revisar, confirmar y corregir la información antes de finalizar la presentación.

#### Objetivo: Prevención de errores (legal, financiero, de datos) (3.3.4) {#purpose-error-prevention-legal-financial-data}

La intención de este criterio de éxito es ayudar a los usuarios con discapacidad a evitar consecuencias graves como resultado de un error al realizar una acción que no se puede revertir. Por ejemplo, la compra de pasajes aéreos no reembolsables o la presentación de una orden de compra de acciones en una cuenta de corretaje son transacciones financieras con graves consecuencias. Si un usuario comete un error en la fecha del vuelo, podría terminar con un billete para el día equivocado que no se puede cambiar. Si el usuario cometiera un error en el número de acciones que quiere comprar, podría terminar adquiriendo más acciones de lo que pretendía. Ambos tipos de errores costosos implican transacciones que ocurren de inmediato y no pueden modificarse posteriormente. Del mismo modo, puede ser un error irrecuperable que los usuarios modifiquen o eliminen de forma involuntaria los datos almacenados en una base de datos a la que posteriormente deban acceder, como todo su perfil de viajes en un sitio web de servicios de viajes. Al referirse a la modificación o eliminación de datos &#39;controlables por el usuario&#39;, la intención es evitar la pérdida masiva de datos, como eliminar un archivo o registro. No es la intención requerir una confirmación para cada comando de guardado ni la simple creación o edición de documentos, registros u otros datos.

Los usuarios con discapacidad pueden tener más probabilidades de cometer errores. Las personas con discapacidad de lectura pueden intercambiar números y letras, y las personas con discapacidad motriz pueden presionar teclas por error. Proporcionar la capacidad de revertir acciones permite a los usuarios corregir un error que podría tener consecuencias graves. La capacidad de revisar y corregir la información ofrece al usuario la oportunidad de detectar un error antes de realizar una acción que tenga graves consecuencias.

Los datos controlables por el usuario son datos que el usuario puede ver, cambiar o eliminar mediante una acción intencional. Algunos ejemplos de control de estos datos son la actualización del número de teléfono y la dirección de la cuenta del usuario o la eliminación de un registro de facturas anteriores de un sitio web. No se refiere a datos como registros de Internet y datos de supervisión de motores de búsqueda con los que el usuario no puede interactuar ni puede visualizar directamente.

#### Cómo cumplir: Prevención de errores (legal, financiero, de datos) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Siga las directrices de [Cómo cumplir los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Más información: Prevención de errores (legal, financiero, de datos) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Entender los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Cumplir los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principio 4: Sólido {#principle-robust}

[Principio 4: Sólido. El contenido debe ser lo suficientemente sólido como para que lo interpreten una amplia variedad de agentes de usuario, incluidas las tecnologías de asistencia.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Directrices 4.1 Compatible: Maximice la compatibilidad con los agentes de usuario actuales y futuros, incluidas las tecnologías de asistencia.](https://www.w3.org/TR/WCAG/#compatible)

Maximice la compatibilidad con los agentes de usuario actuales y futuros, incluidas las tecnologías de asistencia.

### Análisis (4.1.1)  {#parsing}

* Criterios de éxito 4.1.1
* Nivel A
* Análisis: En el contenido implementado con lenguajes de marcado, los elementos tienen etiquetas inicio y final completas, los elementos se anidan según sus especificaciones, los elementos no contienen atributos de duplicado y cualquier ID es único, excepto cuando las especificaciones permiten estas características.

#### Objetivo: Análisis (4.1.1) {#purpose-parsing}

La intención de este criterio de éxito es garantizar que los agentes de usuario, incluidas las tecnologías de asistencia, puedan interpretar y analizar el contenido con precisión. Si el contenido no puede descomponerse en una estructura de datos, los distintos agentes de usuario pueden presentarlo de forma diferente o ser incapaces de analizarlo. Algunos agentes de usuario utilizan &quot;técnicas de reparación&quot; para representar contenido mal codificado.

Dado que las técnicas de reparación varían entre los agentes de usuario, los autores no pueden suponer que el contenido se analiza con precisión en una estructura de datos o que los agentes de usuario especializados, incluidas las tecnologías de asistencia, lo procesarán correctamente, a menos que el contenido se cree según las reglas definidas en la gramática formal de esa tecnología. En los lenguajes de marcado, los errores en la sintaxis de elementos y atributos y no proporcionar las etiquetas de inicio/final anidadas correctamente, producen errores que impiden que los agentes de usuario analicen el contenido de forma fiable. Por lo tanto, el Criterio de éxito requiere que el contenido se pueda analizar usando solamente las reglas de la gramática formal.

#### Cómo cumplir: Análisis (4.1.1) {#how-to-meet-parsing}

Siga las directrices de [Cómo cumplir los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Más información: Análisis (4.1.1) {#more-information-parsing}

* [Entender los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Cumplir los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nombre, Función, Valor (4.1.2)  {#name-role-value}

* Criterios de éxito 4.1.2
* Nivel A
* Nombre, Función, Valor: para todos los componentes de la interfaz de usuario (incluidos, entre otros, elementos de formulario, vínculos y componentes generados por secuencias de comandos), el nombre y la función pueden determinarse mediante programación; los estados, las propiedades y los valores que el usuario puede establecer se pueden definir mediante programación, y la notificación de los cambios en estos artículos está disponible para los agentes de usuario, incluidas las tecnologías de asistencia.

#### Objetivo: Nombre, Función, Valor (4.1.2) {#purpose-ame-role-value}

La intención de este criterio de éxito es garantizar que las tecnologías de asistencia (AT) puedan recopilar información sobre, activar o establecer y mantener al día el estado de los controles de interfaz de usuario en el contenido.

Si se utilizan controles estándar de tecnologías accesibles, este proceso es sencillo. Si los elementos de la interfaz de usuario se utilizan de acuerdo con las especificaciones, se cumplen las condiciones de esta disposición. (Ver ejemplos de Criterios de éxito 4.1.2 más adelante)

Sin embargo, si se crean controles personalizados o si se programan elementos de interfaz (en código o secuencia de comandos) para que tengan una función o función distinta de la habitual, deben tomarse medidas adicionales para garantizar que los controles proporcionen información importante a las tecnologías de asistencia y permitan que se controlen mediante tecnologías de asistencia.

Un estado importante de un control de interfaz de usuario consiste en saber si tiene enfoque. El estado de enfoque de un control se puede determinar mediante programación, y las notificaciones sobre el cambio de enfoque se envían a los agentes de usuario y a la tecnología de asistencia. Otros ejemplos del estado de control de la interfaz de usuario son si se ha seleccionado una casilla de verificación o un botón de radio. O bien, si un árbol o nodo de lista contraíble está expandido o contraído.

#### Cómo cumplir: Nombre, función, valor (4.1.2) {#how-to-meet-ame-role-value}

Siga las directrices de [Cómo cumplir los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Más información: Nombre, Función, Valor (4.1.2)  {#more-information-ame-role-value}

* [Entender los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Cumplir los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
