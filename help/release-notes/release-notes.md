---
title: Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP1
description: Busque la información actual de la versión de Adobe Experience Manager 6.5 LTS, Service Pack 1.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: b6a5e6bacfee72e162ce3bc035f909c02fbbf6db
workflow-type: tm+mt
source-wordcount: '4935'
ht-degree: 14%

---

# Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP1 {#release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versión | Paquete de servicio 1 (SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | 21 de agosto de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://artifactory.corp.adobe.com/artifactory/maven-aem-release-local/com/adobe/aem/cq-quickstart/6.6.1/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## Qué se incluye en [!DNL Adobe Experience Manager] 6.5 LTS, SP1 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad inicial de 6.5 LTS en marzo de 2025. [Instalar este Service Pack](#install-update) en 6.5 LTS.

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## Se han corregido problemas en 6.5 LTS, Service Pack 1 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### Accesibilidad {#sites-accessibility-65-lts-sp1}

* Se ha corregido un problema en el cual el elemento editor de texto de Fragmentos de contenido se truncaba de forma predeterminada. El editor de texto ahora muestra el contenido completo sin truncamiento. (SITES-33005)
* Se ha corregido un problema en el cual al hacer clic en las rutas URL se abría la página principal de Indigo en lugar de la dirección URL de destino correcta. (SITES-33004)
* Se ha corregido un problema de accesibilidad en un componente personalizado de AEM que provocaba errores de conformidad con ADA durante las pruebas automatizadas. (SITES-30660)
* Se han corregido problemas de cumplimiento de ADA en el cuadro de diálogo Alerta y Mensajes de flujo de trabajo al garantizar que el texto se muestre en negro sobre fondos claros y cumpla los requisitos de contraste de WCAG 2.0. (SITES-30138)
* Se ha corregido un problema de accesibilidad en el que el botón &quot;Categoría&quot; del editor de AEM Sites carecía de una etiqueta específica, lo que provocaba que JAWS la anunciara como &quot;Menú de botón de imágenes&quot; en lugar de proporcionar una etiqueta descriptiva. (SITES-27497)
* Se ha corregido un problema de accesibilidad en el que los iconos de marca de verificación de la pantalla Permisos efectivos carecían de texto alternativo, lo que impedía que JAWS leyera y transmitiera su significado. (SITES-27272)
* Se ha corregido un problema de accesibilidad en el que la página Permisos no mostraba un anuncio claro de JAWS para eliminar permisos de usuarios o grupos, lo que causaba confusión a los usuarios del lector de pantalla. (SITES-27238)
* Se ha corregido un problema de accesibilidad en el que los mensajes de error solo se mostraban como iconos sin texto descriptivo, lo que impedía que JAWS anunciara los errores cuando se producían. (SITES-27155)
* Se ha corregido un problema de accesibilidad en el que JAWS leía descripciones de botones incorrectas y poco claras en el entorno local de AEM, incluido el texto de nivel 2 de encabezado que faltaba para la sección de módulos. (SITES-27152)
* Se ha corregido un problema de accesibilidad en el cual JAWS no anunciaba el número de resultados después de filtrar los valores en la pestaña AEM Assets. (SITES-27150)
* Se ha corregido un problema de accesibilidad en el cual al crear una carpeta no se mostraba una confirmación y JAWS no lo anunciaba en la interfaz de usuario de Assets. (SITES-27141)
* Se ha corregido un problema de accesibilidad en AEM Sites. JAWS no anunció errores de formulario, el enfoque se movió a elementos de error no interactivos y los errores de campo obligatorio no se mostraron en la pestaña de salida. (SITES-27138)
* Se ha corregido un problema de accesibilidad en el que el menú del botón Líneas de tiempo carecía de una etiqueta específica, lo que provocaba que JAWS solo leyera &quot;Menú del botón Actividades&quot; sin proporcionar una descripción clara. (SITES-27134)
* Se ha corregido un problema de accesibilidad en el que JAWS no anunciaba la acción o la función para los elementos de contenedor, que solo leían &quot;Ruta de exploración v1&quot; y &quot;Botón v2&quot; en lugar de etiquetas descriptivas. (SITES-27131)
* Se ha corregido un problema de accesibilidad en el que la ventana emergente de publicación rápida no mostraba un mensaje de éxito adecuado, lo que impedía a los lectores de pantalla anunciar comentarios de finalización. (SITES-26912)
* Se ha corregido un problema de accesibilidad en la vista de columna coral en el que los elementos con funciones ARIA que requerían funciones secundarias no las contenían, lo que provocaba un incumplimiento de los estándares de accesibilidad. (SITES-26898)
* Se ha corregido un problema de accesibilidad en el que los textos &quot;plantilla&quot; y &quot;propiedades&quot; de la navegación superior de la página de creación no eran visibles en el modo Reflow, lo que impedía el acceso a los usuarios del teclado y del lector de pantalla. (SITES-26895)
* Se ha corregido un problema de accesibilidad en el que no se podía acceder a la información de herramientas de los iconos &quot;búsqueda&quot;, &quot;solución&quot;, &quot;ayuda&quot;, &quot;bandeja de entrada&quot; y &quot;usuario&quot; de la navegación superior mediante la navegación con el teclado. (SITES-26889)
* Se ha corregido un problema de accesibilidad en el que los campos de formulario de pestaña Básico no proporcionaban sugerencias de error, lo que impedía a los usuarios recibir orientación cuando los campos de entrada obligatorios estaban vacíos. (SITES-26885)
* Se ha corregido un problema de accesibilidad en el que los lectores de pantalla de NVDA y Narrador no anunciaban detalles de archivo de plantilla en la página Crear, lo que impedía a los usuarios recibir información completa mediante programación. (SITES-26884)
* Se ha corregido un problema de accesibilidad que utilizaba un nombre incorrecto para el &quot;Cuadro de texto de título de página&quot; en la pestaña Básico, lo que impedía que los lectores de pantalla proporcionaran información precisa a los usuarios. (SITES-26879)
* Se han actualizado los colores de primer plano y de fondo del botón para cumplir los requisitos de relación de contraste mínima de WCAG 2.2 AA, lo que mejora la legibilidad y accesibilidad para todos los usuarios. (SITES-26877)
* Se ha resuelto un problema que provocaba que los textos &quot;plantilla&quot; y &quot;propiedades&quot; de la navegación superior de la página de creación desaparecieran tras cambiar de tamaño, lo que garantizaba la visibilidad y accesibilidad para los usuarios con problemas de visión. (SITES-26872)
* Se ha corregido un problema que hacía que aparecieran varias barras de desplazamiento horizontales en la página principal después de aplicar un Reflujo, lo que garantizaba que se mostrara una sola barra de desplazamiento para una accesibilidad y visibilidad del contenido adecuadas. (SITES-26800)
* Se ha corregido un problema de accesibilidad en el Editor de páginas de AEM por el que el foco del teclado se restablece inesperadamente al principio de la barra de herramientas demográfica después de activar botones como Persona, Carro de compras o Abandonado. Ahora, el enfoque permanece en el botón activado para admitir flujos de trabajo coherentes de navegación mediante el teclado y lector de pantalla. (SITES-25306)
* Se ha corregido un problema de asociación de etiquetas de accesibilidad para el título de página y los campos de etiquetas. La interfaz de AEM ahora asocia correctamente las etiquetas de accesibilidad con los campos &quot;Título&quot; y &quot;Título de página&quot; al utilizar lectores de pantalla como JAWS. La corrección garantiza una lectura de etiquetas adecuada y mejora el cumplimiento de la ADA en la creación de páginas, las propiedades y los flujos de trabajo de movimiento. (SITES-27149)
* Se ha corregido la falta de una etiqueta visual para los campos de entrada de comentarios en la cronología. Se han corregido las etiquetas visuales que faltaban para los campos de entrada de &quot;comentario&quot; en la sección de cronología para mejorar la accesibilidad. La actualización garantiza que los lectores de pantalla puedan anunciar con precisión las etiquetas de campo. Esta experiencia mejora la navegación y el envío de formularios para todos los usuarios, especialmente las personas que dependen de las tecnologías de asistencia. (SITES-26903)
* Se ha corregido la accesibilidad del teclado para el botón de puntos suspensivos en comentarios de cronología. Se ha habilitado la navegación mediante el teclado para el botón de puntos suspensivos (tres puntos) junto a los comentarios en la sección de cronología. Los usuarios ahora pueden acceder al botón e interactuar con él mediante la tecla de tabulación, lo que mejora la accesibilidad para los usuarios que dependen de la navegación solo mediante teclado. (SITES-26891)
* Se han mejorado los anuncios de NVDA/Narrador para resultados de búsqueda en cuadros de diálogo de selección. Se ha actualizado el cuadro de diálogo Abrir selección para anunciar si se encuentran o no resultados de búsqueda al utilizar lectores de pantalla, como NVDA o Narrador. Esta mejora ayuda a los usuarios que dependen de tecnologías de asistencia a comprender el resultado de sus acciones de búsqueda sin necesidad de confirmación visual. (SITES-26883)
* Se ha corregido la función ARIA del icono de puntos suspensivos junto al campo de entrada de comentarios. Se ha actualizado el icono de puntos suspensivos (tres puntos) junto al campo de entrada del comentario para utilizar la función ARIA correcta, lo que garantiza que los lectores de pantalla puedan identificar el elemento con precisión. Esta mejora mejora mejora el cumplimiento de la accesibilidad y la experiencia de los usuarios que dependen de las tecnologías de asistencia. (SITES-26881)
* Se han corregido atributos ARIA no válidos en los componentes de Coral UI. Se han actualizado los componentes de la interfaz de usuario de Coral para garantizar que todos los atributos ARIA utilicen valores válidos, mejorando la accesibilidad y el cumplimiento. En particular, se abordaron casos en los que valores no válidos como `aria-modal="dialog"` se asignaron incorrectamente. Esta mejora permite a los lectores de pantalla interpretar correctamente los elementos del cuadro de diálogo, lo que mejora la accesibilidad para los usuarios que dependen de tecnologías de asistencia. (SITES-26873)
* Visibilidad mejorada e información sobre herramientas para iconos en escenarios de reflujo. Se ha mejorado el comportamiento de reflujo para garantizar que la información sobre herramientas se muestre correctamente en los iconos **Descargar**, **Volver a procesar recursos** y **Finalizar compra**. Se centró en un problema de accesibilidad en el que los iconos y sus etiquetas se volvían invisibles cuando cambiaba el tamaño de la ventanilla móvil o la configuración de zoom del explorador. Esta corrección admite usuarios con visión reducida al mantener la visibilidad y proporcionar descripciones de iconos adecuadas durante el reflujo. (SITES-26871)


#### Interfaz de usuario de administrador{#sites-adminui-65-lts-sp1}

* Se ha corregido un problema de accesibilidad en el cual JAWS no anunciaba funciones de lista ni proporcionaba instrucciones de navegación y activación en el cuadro de diálogo Crear sitio. (SITES-30661)
* La compatibilidad del lector de pantalla con los mensajes de estado en la vista de filtro de Sitios funciona según lo esperado, lo que garantiza que los usuarios reciban comentarios claros y oportunos al cambiar entre vistas. (SITES-24992)
* El selector de fechas del carril de los filtros se muestra completamente dentro de su contenedor, lo que proporciona un tamaño de destino táctil adecuado y elimina los problemas de recorte. (SITES-24988)
* Las etiquetas de filtro seleccionadas ahora utilizan etiquetas HTML semánticas y aria que coinciden con la presentación visual, lo que garantiza una compatibilidad de funciones precisa y acciones claras para las tecnologías de asistencia. (SITES-24980)
* Se ha añadido un atributo aria-label a la región Carril de referencias para proporcionar una etiqueta única y descriptiva a los usuarios del lector de pantalla y garantizar una identificación uniforme de los puntos de referencia en toda la página. (SITES-24973)
* Se ha actualizado el carril referencias para que utilice unidades relativas para el tamaño y la posición, lo que permite que el contenido se escale y siga funcionando completamente al ampliarse al 400 % en una ventanilla de 1280 x 1024. (SITES-24972)
* Los elementos de tabla confirmados en la vista de lista de la página de inicio de Sites contienen las funciones de encabezado de columna adecuadas, lo que permite a los lectores de pantalla anunciar encabezados para cada celda de datos. (SITES-24942)
* Ahora, NVDA anuncia la fecha de modificación en el directorio de árbol, lo que garantiza que los usuarios del lector de pantalla reciban información detallada completa sobre los recursos. (SITES-24782)
* Se ha corregido un problema en el cual el lector de pantalla NVDA anunciaba texto incompleto para elementos en el componente Directorio de árbol en AEM Sites. NVDA ahora lee texto completo para cada elemento, mejorando la accesibilidad y el cumplimiento normativo. (SITES-24780)
* Se ha agregado accesibilidad de teclado al divisor de ventanas en el directorio de árbol, lo que permite a los usuarios cambiar el tamaño de la barra lateral izquierda utilizando únicamente un teclado. (SITES-24779)
* Se han actualizado los resultados de búsqueda del menú Ayuda para incluir funciones ARIA correctas para los elementos de lista, lo que garantiza que los lectores de pantalla anuncien los vínculos correctamente para mejorar la accesibilidad. (SITES-24729)
* Se ha corregido un problema en el cual los lectores de pantalla no anunciaban el mensaje de estado &quot;X de Y resultados&quot;. O bien, el mensaje &quot;no se encontraron resultados&quot; después de aplicar los filtros en el panel Filtro de sitios, lo que garantiza que los usuarios reciban la confirmación adecuada de los resultados. (SITES-24720)
* Se han corregido las asignaciones de funciones que faltaban para los vínculos de navegación en la navegación de la aplicación. Se han añadido las funciones ARIA adecuadas para garantizar que los lectores de pantalla identifiquen y anuncien correctamente los elementos de navegación. (SITES-24719)
* Se ha reemplazado el marcado de función de cuadrícula incorrecto para las etiquetas de filtro seleccionadas con elementos de botón y nombres accesibles añadidos, lo que garantiza que los lectores de pantalla anuncien e identifiquen correctamente las etiquetas. (SITES-24717)
* Se han añadido anuncios de lector de pantalla para el mensaje de estado Carril de referencias al realizar varias selecciones, lo que garantiza que los usuarios reciban confirmación de los cambios. (SITES-24678)
* Se ha corregido el comportamiento del campo de búsqueda para que el primer resultado no se anuncie automáticamente. Los lectores de pantalla ahora anuncian la cantidad de resultados que se encuentran, lo que permite a los usuarios navegar por la lista sin anuncios de enfoque incorrectos. (SITES-24658)
* Se eliminaron atributos `aria-label` incorrectos de elementos estáticos no interactivos en la vista de lista para evitar que los lectores de pantalla anuncien información engañosa o irrelevante. (SITES-24515)
* Se ha actualizado la casilla de verificación de la primera columna de la vista de lista para utilizar el texto de la columna Título para su nombre accesible, lo que garantiza que los lectores de pantalla transmitan con precisión el propósito del campo de formulario. (SITES-24514)
* Se han agregado atributos ARIA adecuados y compatibilidad con regiones activas para anunciar mensajes de estado de carga a los usuarios del lector de pantalla al navegar por el contenido. (SITES-24481)
* Se ha actualizado el diseño interactivo para eliminar el desplazamiento horizontal cuando el contenido se amplía al 400 % con una anchura de ventanilla de 1280×1024, lo que garantiza una visibilidad completa sin desplazamiento lateral. (SITES-24308)
* Se ha corregido la navegación de enfoque en la IU de administración de Sites para seguir un orden lógico, se vuelve a enfocar en el botón &quot;Seleccionar todo&quot; después de pulsar Esc y se mueve el enfoque al siguiente elemento interactivo después de pulsar la pestaña. (SITES-24307)
* Se ha actualizado el orden de enfoque en la IU de administración de sitios para que el botón de rutas de exploración del elemento `<betty-titlebar-title>` se centre en la secuencia correcta durante la navegación mediante el teclado. (SITES-24305)
* Se ha verificado la funcionalidad de omisión de vínculos para garantizar que mueve el foco del teclado al área de contenido principal, lo que permite a los usuarios del teclado evitar los elementos del encabezado y acceder al contenido de forma eficaz. (SITES-24061)


#### IU clásica{#sites-classicui-65-lts-sp1}

Se ha corregido un problema en la IU clásica por el que faltaban etiquetas de casilla de verificación y HTML se mostraba como texto codificado en varios elementos de la interfaz de usuario, incluida la búsqueda por fecha y las interfaces no estándar. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM ahora evita la degradación del rendimiento causada por el formato incorrecto de los metadatos de XMP en los recursos de imagen. Los Assets que contienen nombres de propiedad de XMP no válidos o no compatibles, como los que tienen segmentos numéricos o estructuras no calificadas, ya no almacenan en déclencheur los registros de advertencia repetidos durante el procesamiento. El sistema filtra los metadatos problemáticos para garantizar que la ingesta y validación de recursos se complete sin errores. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-65-lts-sp1}

Otros autores aún pueden publicar fragmentos de contenido incluso cuando otro autor los desproteja, lo que es contrario al comportamiento deseado de la función de cierre de compra. Esta corrección evita que otros usuarios vean o utilicen los botones de publicación en la interfaz de creación cuando se retira un fragmento de contenido. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### Consola de componente{#sites-component-console-65-lts-sp1}

Se ha corregido un problema en el componente Lista de productos en el cual la casilla Seleccionar todo añadía solo los 20 primeros SKU de la página inicial en lugar de todos los SKU en los resultados de búsqueda. (SITES-29191)

#### Servidor principal{#sites-core-backend-65-lts-sp1}

Los metadatos de XMP con formato incorrecto desencadenaron un error durante el procesamiento de los recursos de imagen en `ValidationDataServlet`. La corrección garantiza la administración de metadatos compatible y evita el análisis repetido de propiedades no válidas. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM: Live Copies{#sites-msm-live-copies-65-lts-sp1}

* Se corrigió un error de JavaScript `ns.ui.alert is not a function` que se producía al volver a habilitar la herencia de componentes fantasma en AEM 6.5 local. (SITES-31993)
* Se ha corregido un problema en el cual la opción Despliegue &quot;Más tarde&quot; permitía continuar sin seleccionar una fecha en AEM 6.5. (SITES-31374)

#### Editor de páginas{#sites-pageeditor-65-lts-sp1}

* Se ha resuelto un problema en el modo Teaser en el que la pestaña Vínculo y acciones seguía mostrando el estilo de error, los iconos y el atributo no válido para aria después de una entrada de datos y una resolución de error válidas. (SITES-25527)
* Se ha corregido un problema en el editor de texto Modo teaser en el que los botones Listas y Párrafos no transmitían su estado expandido o contraído a los lectores de pantalla, lo que garantizaba actualizaciones de atributos expandidas por aria precisas. (SITES-25365)
* Se ha corregido un problema en la barra de herramientas de datos demográficos por el que, al ajustar el deslizador del carro de compras con la entrada de teclado, se desplazaba el enfoque al botón del carro de compras en lugar de mantenerlo, lo que mejoraba la eficacia de navegación de los usuarios del teclado. (SITES-25324)
* Se ha agregado un nombre accesible al control deslizante del carro de compras en la barra de herramientas demográficas al asignar un valor a su elemento `<label>` asociado. Esto corrigió la compatibilidad mejorada con las tecnologías de asistencia y mejoró la capacidad de uso de los usuarios de lectores de pantalla. (SITES-25322)
* Se han agregado funciones ARIA y nombres accesibles a los botones de la lista desplegable Barra de herramientas demográfica. Esta corrección habilitó la identificación adecuada mediante tecnologías de asistencia y mejoró la navegación para los usuarios del teclado y del lector de pantalla. (SITES-25315)
* Se ha ajustado el diseño de la barra de herramientas demográfica para evitar el desbordamiento del contenido más allá de la ventanilla con un zoom del explorador del 200 %, lo que garantiza que todos los controles permanezcan accesibles sin desplazamiento horizontal. (SITES-25309)
* Se ha corregido la administración de enfoque en la barra de herramientas demográfica para mantener el enfoque del teclado en el botón activado en lugar de restablecer el enfoque en la posición inicial de la barra de herramientas. (SITES-25306)
* La superposición de etiquetas de botón funciona según lo diseñado, con información del objeto para mostrar la etiqueta cuando los modos con anchos de pantalla similares están activos. (SITES-25285)
* El modal de anotación incluye un botón de envío visible, que permite a los usuarios enviar anotaciones sin depender de la tecla Escape ni hacer clic fuera del modal. (SITES-25281)
* El modal de anotación incluye un botón de icono de lápiz que permite a los usuarios enviar anotaciones, lo que proporciona un método de envío claro y accesible. (SITES-25269)
* Se han corregido los anuncios del lector de pantalla para los botones Anotar y Cerrar anotación a fin de proporcionar comentarios precisos y relevantes y eliminar información no relacionada o confusa. (SITES-25268)
* Las secciones de lienzo de las páginas del Editor de AEM ahora admiten la accesibilidad total del teclado. Los usuarios pueden activar los títulos de sección y los botones de edición utilizando únicamente el teclado, sin depender del desplazamiento del ratón. Esta actualización garantiza el cumplimiento de WCAG 2.1.1 y mejora la capacidad de uso entre componentes (como Teaser, Imagen, Carrusel, Diseño, Deformación de tiempo y Modelos de anotación). (SITES-25256)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal de carrusel a una anchura de 320 píxeles para garantizar que todo el contenido se muestre dentro de la ventanilla sin requerir navegación de lado a lado. (SITES-25254)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal de imagen a 320 píxeles de anchura para garantizar que todo el contenido se muestre dentro de la ventanilla sin necesidad de navegación de lado a lado. (SITES-25244)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal Teaser a 320 píxeles de anchura para garantizar que todo el contenido se muestre dentro de la ventanilla sin requerir navegación de lado a lado. (SITES-25242)
* Se habilitó la navegación mediante el teclado para el menú emergente `List` y `Paragraph Format`, ambos en el modo Teaser. Esta corrección permite a los usuarios acceder y navegar por estos menús con las teclas de flecha. (SITES-25235)
* Se han corregido los anuncios del lector de pantalla para los botones Anotar y Cerrar anotación para proporcionar comentarios precisos y relevantes alineados con las acciones asociadas. (SITES-25234)
* Se ha mejorado la etiqueta del botón Ayuda en el modo Teaser para describir claramente su propósito y proporcionar un contexto significativo para todos los usuarios, incluidos los usuarios de tecnología de asistencia. (SITES-25224)
* Se ha mejorado la regla del emulador para los usuarios del lector de pantalla al asociar las mediciones de la regla con sus respectivos dispositivos. Además, reemplace la información del objeto por un elemento aria-described by. (SITES-24955)
* No se ha implementado ninguna corrección porque el botón Editar funciona según lo previsto y proporciona un contexto informativo en lugar de realizar una acción. (SITES-24950)
* El orden de enfoque confirmado en la página del editor sigue una secuencia lógica, lo que permite a los usuarios navegar por todos los elementos interactivos sin saltar ni volver a crear bucles de forma inesperada. (SITES-24937)
* El lienzo del modo de vista previa confirmado actualiza correctamente el espaciado del texto cuando los usuarios aplican la configuración personalizada de espaciado del texto, lo que garantiza un formato coherente en todas las áreas de contenido. (SITES-24936)
* El botón Vista previa ya no almacena en déclencheur los cambios de contexto o estado de enfoque, lo que garantiza que los usuarios activen el botón intencionadamente antes de que se actualice la vista de página. (SITES-24784)
* Se han añadido asignaciones de funciones ARIA correctas a los vínculos de navegación de la aplicación, lo que permite a los lectores de pantalla identificarse con precisión y anunciar elementos de navegación para mejorar la accesibilidad. (SITES-24718)
* Se ha actualizado el botón Cambiar filtros para anunciar estados expandidos y contraídos a los lectores de pantalla, se han eliminado atributos ARIA redundantes y se ha ajustado el etiquetado para proporcionar descripciones claras y no duplicadas. (SITES-24713)
* Se han añadido anuncios de lector de pantalla para los mensajes de estado de los resultados de búsqueda en el cuadro de diálogo Selección de vínculos, lo que garantiza que los usuarios reciban confirmación cuando se carguen los resultados o no se encuentren coincidencias. (SITES-24700)
* Se han añadido anuncios de lector de pantalla para el estado de carga del modal de imagen, lo que garantiza que los usuarios reciban comentarios cuando el modal se carga y está listo para la interacción. (SITES-24697)
* Se ha resuelto un problema de accesibilidad en el que el encabezado adhesivo oscurecía el contenido modal de teaser al 200 % y al 400 % de zoom, lo que garantiza una visibilidad y una facilidad de uso completas al utilizar la ampliación de la página. (SITES-24523)
* Se ha agregado un mensaje de estado con el número de resultados de búsqueda al campo Buscar/filtrar, lo que permite a los lectores de pantalla anunciar resultados a los usuarios. (SITES-24506)
* Se han añadido anuncios de lector de pantalla para la cantidad de resultados de búsqueda en el campo Buscar/filtrar, lo que garantiza que los usuarios reciban comentarios inmediatos cuando se carguen los resultados. (SITES-24505)
* Se ha añadido un nombre accesible a la lista de pestañas del panel Carril lateral, lo que permite a los lectores de pantalla anunciar su propósito de acuerdo con las directrices WAI-ARIA. (SITES-24492)
* Se han añadido etiquetas descriptivas a los iconos ambiguos del editor, lo que garantiza que todos los usuarios entiendan claramente la función de cada botón. (SITES-24480)
* Se ha habilitado la accesibilidad completa del teclado para los títulos de sección y los botones de acción en la vista Lienzo, lo que garantiza un funcionamiento coherente para los usuarios del ratón y el teclado. (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Editor universal {#sites-universal-editor-65-lts-sp1}

* Se ha corregido una condición de carrera en QueryTokenService que provocaba inicios de sesión incorrectos cuando varias solicitudes con parámetros de consulta activados antes de que el servicio de token de inicio de sesión devolviera un resultado. (SITES-30659)
* Se ha corregido un problema en UniversalEditorURLService por el cual al guardar una matriz de rutas asignadas en Felix ConfigMgr solo se guardaba el primer elemento. (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

Se ha corregido un problema en el cual la sincronización de recursos de DAM remoto a AEM local de Sites eliminaba el estado publicado y las propiedades relacionadas con la replicación de los recursos. (Assets-48958)

<!--
#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp1}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp1}



### [!DNL Forms]{#forms-65-lts-sp1}


#### Forms Designer 

#### Forms

#### Forms JEE 
 
#### Forms Captcha {#forms-captcha-65-lts-sp1} 

#### XMLFM {#forms-xmlfm-65-lts-sp1}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp1}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp1} -->



### Foundation {#foundation-65-lts-sp1}

<!--
#### Apache Felix {#foundation-apachefelix-65-lts-sp1}

#### Campaign{#foundation-campaign-65-lts-sp1}

#### Cloud Services{#foundation-cloudservices-65-lts-sp1}



#### Communities {#foundation-communities-65-lts-sp1}

#### Content distribution{#foundation-content-distribution-65-lts-sp1}

#### CRX {#foundation-crx-65-lts-sp1}

#### Granite{#foundation-granite-65-lts-sp1} -->

#### HTL{#foundatoin-htl-5-lts-sp1}

Se han resuelto ciclos de dependencia de OSGi que bloqueaban el funcionamiento de la fábrica del motor de scripts HTL, lo que garantizaba la resolución adecuada del servicio y la ejecución de scripts. (Granite-58275)

#### Integraciones{#foundation-integrations-65-lts-sp1}

* Se ha eliminado el uso de commons-httpclient 3.x del paquete `com.adobe.cq.cq-analytics-integration` y se ha reemplazado por `org.apache.httpcomponents.httpclient` 4.5.13.B0001 para que se ajuste a los estándares AEM 6.5 LTS más recientes. (CQ-4360586)
* Se ha eliminado el paquete de integración de Search&amp;Promote obsoleto de AEM para eliminar los componentes no utilizados y reducir la sobrecarga de mantenimiento. (CQ-4358030)
* Se han añadido nuevos casos de prueba back-end para la integración de SiteCatalyst con el fin de mejorar la validación de análisis y garantizar una cobertura más completa. (CQ-4359991)
* Se ha corregido un problema en la sección Propiedades de la configuración de Launch en el que no aparecían los menús desplegables Compañía y Propiedad. Además, Guardar y cerrar activó errores a pesar de que se rellenaban todos los campos obligatorios y se mostraban mensajes de error incorrectos para Empresa y Propiedad cuando solo el campo Título estaba vacío. (CQ-4359853)
* Se ha eliminado la entrada de ruta de acceso al servlet `searchpromote` de la versión 6.6 para alinearla con la eliminación del paquete de Search&amp;Promote. (CQ-4359523)
* Se han corregido casos de prueba HTTP para el repositorio de Target a fin de garantizar una validación precisa y una fiabilidad de prueba mejorada. (CQ-4359022)
* Se ha eliminado el uso de almacenamiento en caché de Guava del módulo integration-adobeims-console para eliminar las dependencias de la biblioteca de Guava. (CQ-4358710)
* Se han validado los flujos de trabajo de integración de DTM, las tareas de la bandeja de entrada y la funcionalidad del proyecto en AEM 6.6 para garantizar un funcionamiento adecuado en AEM 6.5. (CQ-4358151)
* Se ha validado la funcionalidad de Insight de contenido en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357774)
* Se ha validado la funcionalidad de Cloud Services en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357773)
* Se ha validado la integración de la consola de Adobe IMS en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357772)
* Se ha actualizado la canalización de Jenkins para que la integración de Test&amp;Target se ejecute en Java 17, resuelva las pruebas de Selenium que fallan, mueva las pruebas seleccionadas a Playwright y garantice que todas las pruebas unitarias pasen. (CQ-4357770)
* Integraciones, flujo de trabajo, bandeja de entrada y proyectos DX alineados con la rama 6.6.0 mediante la actualización de canalizaciones de compilación y prueba. Además, resuelva los problemas de compatibilidad de actualización y valide todos los servicios afectados para mantener la estabilidad y la funcionalidad. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### Localización{#foundation-localization-65-lts-sp1}

* Se han localizado las cadenas en el cuadro de diálogo &quot;Quitar control de acceso&quot; de la lista &quot;Permisos&quot; para mostrar las traducciones correctas. (GRANITE-59427)
* Se ha corregido un problema en el cuadro de diálogo Añadir regla de propiedades de división &quot;O&quot; del Editor del modelo en el que aparecían sin localizar varias cadenas de interfaz de usuario, incluidos operadores y etiquetas de campo. Ahora todas las cadenas se muestran con la localización correcta. (CQ-4354014)
* Se ha añadido la traducción que falta para la información sobre herramientas Mostrar descripción de en el cuadro de diálogo Editar modelos de flujo de trabajo. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

Se ha resuelto un problema en el cual AEM volvía a crear o cambiar el nombre de los archivos de configuración existentes en `/apps/system/config` durante las actualizaciones y reemplazaba `.cfg.json` archivos por `.config` archivos. (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

Se ha corregido un problema de accesibilidad en el que los marcadores de posición aparecían incorrectamente como etiquetas para los campos de entrada. Este problema provocaba la falta de etiquetas de campo en la búsqueda, en los fragmentos de experiencias de AEM, en los fragmentos de contenido y en los modelos de fragmentos de contenido. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### Proyectos{#foundation-projects-65-lts-sp1}

* Se ha resuelto un problema que mostraba una ventana emergente de error incorrecto al eliminar un proyecto en la vista Calendario, a pesar de que la eliminación del proyecto se había realizado correctamente. (CQ-4358890)
* Se ha corregido un problema en Firefox por el que el pie de página de la tarjeta &quot;Recopilación de recursos&quot; en la vista Proyecto se superponía al borde de la tarjeta. El pie de página ahora se alinea correctamente sin superponerse. (CQ-4353317)

#### Guía de inicio rápido{#foundation-quickstart-65-lts-sp1}

* Se ha actualizado el script de desinstalación para ajustar el intervalo de versiones del paquete Guava, lo que evita que se vea incluido en la lista de bloqueados cuando se instala mediante el Administrador de paquetes. (GRANITE-59559)
* Se ha corregido un error de configuración de varias partes que se producía durante las cargas de paquetes de AEMFD en Tomcat 11 con JDK 17 al actualizar la configuración del servidor para admitir instalaciones de paquetes grandes sin activar errores de análisis. (GRANITE-58327)
* Se ha corregido un problema en la interfaz de usuario de replicación que mostraba un error (`#1660`) al editar los agentes de replicación al corregir la administración de las casillas de verificación clásicas en la interfaz. (GRANITE-58302)
* Se han resuelto varios errores de inicio del almacén de datos S3 al ejecutar AEM 6.5 LTS con JDK 21. Para ello, se han de corregir los permisos de servicio que faltaban, actualizar la administración de la configuración y garantizar que los servicios necesarios se inicialicen correctamente. (GRANITE-57082)
* Se ha definido la estrategia de mantenimiento y mantenimiento para AEM 6.5. Esta corrección incluye lo siguiente:
   * Cadencia del paquete de servicio.
   * Cadencia de revisión.
   * Compatibilidad paralela con AEM 6.6.
   * Matriz de soporte actualizada.
   * Responsabilidades de propiedad del complemento. (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* Se ha actualizado Sling ResourceAccessSecurity a la versión 1.1.2 para resolver un problema `ClassCastException` que se producía cuando se inicializaban varias referencias de `ResourceAccessGate` `ResourceAccessSecurityImpl`. (NPR-42750)
* Se ha corregido un problema en la integración de Adobe Stock por el que el cuadro de diálogo Licencia aparecía atenuado. Este problema se debió a la eliminación de los campos de entrada requeridos por la función `sunt:initList`. La función se ha encontrado en las bibliotecas de cliente de Coral Foundation. Se han actualizado las bibliotecas de cliente para conservar los campos necesarios, lo que permite la correcta funcionalidad del cuadro de diálogo de licencias. (NPR-42748)
* Se antepuso la corrección de un problema de scripts de Sling que causaba `DataTimeParseException` y `String.length()` excepciones de puntero nulo durante la instalación del paquete. Se ha actualizado Sling Scripting a la versión 2.8.3-1.0.10.6 para reducir los errores de instalación y mejorar la estabilidad. (NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### Interfaz de usuario{#foundation-ui-65-lts-sp1}

* Se ha resuelto un problema en la interfaz de usuario de Autor de AEM que limitaba la visualización de grupos de usuarios a 41. Este problema se debía a un límite de lotes predeterminado en el componente selector de grupos de Granite UI. Se ha actualizado el componente para mostrar todos los grupos sin truncamiento. (NPR-42749)
* Se ha resuelto un problema en el asistente de creación de página local en el que los campos obligatorios en los componentes de varios campos no se volvían a validar al editar las propiedades de página. Este problema, a su vez, permitía a los autores omitir la validación y continuar con los datos incompletos. (GRANITE-58826)
* Se han corregido los atributos ARIA del botón de ayuda de AEM para garantizar que los lectores de pantalla de JAWS anuncien una etiqueta clara y fácil de usar en lugar de mostrar iconos y metadatos de texto sin traducir. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* Se ha agregado compatibilidad con Java 17 para las traducciones de AEM mediante la actualización de paquetes de traducción, la verificación de la compatibilidad de paquetes Java, la eliminación de dependencias obsoletas y la garantía de funcionalidad completa mediante pruebas exhaustivas. (CQ-4357525)
* Se eliminó la prueba Evergreen en descomposición `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater` para evitar errores falsos durante las pruebas automatizadas. (CQ-4298376)

#### Flujo de trabajo{#foundation-workflow-65-lts-sp1}

* Se ha agregado el atributo `data-detailsurl` que falta en los elementos de la bandeja de entrada para evitar que valores indefinidos aparezcan en las direcciones URL al usar AEM 6.5 LTS con Java 21. (GRANITE-60158)
* Se corrigió una NullPointerException en el método `deactivate` del paquete `WorkflowToPublishEventService` al ejecutar AEM 6.5 LTS con Java 21, lo que garantiza el cierre correcto del servicio de flujo de trabajo sin errores. (GRANITE-58151)
* Se ha actualizado el índice del flujo de trabajo para admitir el uso compartido, la personalización fuera de la oficina y la resolución de problemas de consultas de cronología. (GRANITE-52640)
* Se ha actualizado el índice del flujo de trabajo para admitir el uso compartido de, las funciones de personalización fuera de la oficina y la resolución de problemas de consultas de cronología. (GRANITE-52294)
* Se han resuelto mayores errores de registro durante la validación de comparación de registros para una actualización de programa a la versión 10912 de AEM, lo que garantiza una ejecución estable del flujo de trabajo. (GRANITE-44268)
* Se ha actualizado el método de saneamiento de URL en los repositorios de flujo de trabajo para reemplazar `url.searchParams` por `url.search`, lo que mejora la protección XSS para las direcciones URL vulnerables. (CQ-4359585)
* Se ha validado la funcionalidad de flujo de trabajo, bandeja de entrada y proyectos en AEM 6.6 Forms para garantizar un funcionamiento e integración adecuados. (CQ-4358777)
* Se ha implementado la automatización para liberar artefactos de contenido de flujo de trabajo a través de Jenkins, lo que permite procesos de implementación optimizados y coherentes en AEM 6.5. (CQ-4358472)
* Se ha corregido un problema en el flujo de trabajo Crear tarea de la Bandeja de entrada en el que el cuadro de diálogo &quot;Agregar tarea&quot; no se cerraba después de hacer clic en Enviar, a pesar de la tarea que se estaba creando, debido a un error de sintaxis de JavaScript. (CQ-4355336)
* Se ha corregido un problema que impedía guardar la configuración de vista de la Bandeja de entrada debido a que faltaba una definición de propiedad para `isEndUserConfigurationEnabled`. (CQ-4287757)




## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 LTS se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x se utiliza como motor servlet para Quickstart.

### Compatibilidad con Java™  {#java-support}

* Compatibilidad con Java™ 17 y Java™ 21.
* Para obtener un rendimiento óptimo, reemplace los valores predeterminados de GC por otros valores. Para obtener más información, consulte la sección [Instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye actualizaciones de mantenimiento de Java™ 17 y Java™ 21 para que las utilicen los clientes en proyectos relacionados con AEM cuando no están disponibles para el público desde Oracle.

### Embalaje Uberjar {#uber-jar-packaging}

* Hay una ligera diferencia en el empaquetado de Uberjar de AEM 6.5 LTS. Para obtener más información, consulte [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Actualizar {#upgrade}

* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

## Instalación y actualización {#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Para instalaciones nuevas de AEM 6.5 LTS, las definiciones de índice deben instalarse por separado. Para obtener más información, vea [este artículo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas compatibles, incluido el nivel de compatibilidad, en [Requisitos técnicos de AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Java™ 17 y Java™ 21 son las versiones recomendadas para usar con AEM 6.5 LTS.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe revisa continuamente las funciones de los productos para mejorar el valor para los clientes mediante la modernización o el reemplazo de funciones antiguas. Estos cambios se realizan prestando especial atención a la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las funciones de Adobe Experience Manager (AEM), se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las funciones siguen estando disponibles, pero no se siguen mejorando.
1. La eliminación de las funciones en desuso se produce en la siguiente versión principal como pronto. La fecha objetivo real para la eliminación está planeada para su anuncio más adelante.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.


### Funciones en desuso {#deprecated-features}

En esta sección se enumeran las características y funciones que Adobe ha dejado de utilizar en AEM 6.5 LTS. Normalmente, Adobe deja de utilizar las características antes de eliminarlas en una versión futura y proporciona una alternativa.


Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|---|---|---|---|


### Funciones eliminadas {#removed-features}

En esta sección se enumeran las características y funciones que se han eliminado de AEM 6.5 LTS. Las versiones anteriores tenían estas funciones marcadas como en desuso.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|--- |--- |--- |--- |



## Problemas conocidos {#known-issues}

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

### Problema con el paquete de scripts JSP en AEM 6.5.21-6.5.23 y AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23 y AEM 6.5 LTS GA se envían con el paquete `org.apache.sling.scripting.jsp:2.6.0`, que contiene un problema conocido. El problema suele producirse con una carga alta cuando la instancia de AEM administra muchas solicitudes simultáneas.

Cuando se produce este problema, puede aparecer una de las siguientes excepciones en los registros de errores junto con las referencias a `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

Hay disponible una revisión [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) para resolver este problema.

### Error de conexión de Dispatcher con función solo SSL {#ssl-only-feature}

Al habilitar la función Solo SSL en las implementaciones de AEM, existe un problema conocido que afecta a la conectividad entre las instancias de Dispatcher y AEM. Después de habilitar esta función, las comprobaciones de estado pueden fallar y la comunicación entre las instancias de Dispatcher y AEM puede verse interrumpida. Este problema se produce específicamente cuando los clientes intentan conectarse a través de `https + IP` desde Dispatcher a instancias de AEM. Está relacionado con problemas de validación de SNI (Server Name Indication).

**Impacto:**

* Errores de comprobación de estado con códigos de respuesta HTTP 400
* Tráfico interrumpido entre instancias de Dispatcher y AEM
* El contenido no se puede proporcionar correctamente a través de Dispatcher
* Errores de conexión al utilizar HTTPS con direcciones IP en la configuración de Dispatcher
* Errores HTTP 400 del tipo &quot;SNI no válido&quot; al conectarse mediante HTTPS + IP

**Entornos afectados:**

* Implementaciones de AEM con configuraciones de Dispatcher
* Sistemas en los que se ha habilitado la función Solo SSL
* Configuraciones de Dispatcher que utilizan el método de conexión `https + IP` a instancias de AEM

**Solución:**
Si tiene este problema, póngase en contacto con Atención al cliente de Adobe. Hay disponible una revisión [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) para resolver este problema. No intente habilitar las funciones Solo SSL hasta que aplique la revisión necesaria.

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión de [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el Administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

