---
title: Notas de la versión actual de Adobe Experience Manager 6.5 LTS, SP1
description: Busque la información de la versión actual de Adobe Experience Manager 6.5 LTS, Service Pack 1.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 6023c211220bb500814ecd511b8787d107c3c6cd
workflow-type: tm+mt
source-wordcount: '7381'
ht-degree: 99%

---

# Notas de la versión actual de Adobe Experience Manager 6.5 LTS, SP1 {#release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versión | Service Pack 1 (SP1), revisión para GRANITE-61551 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 9 de septiembre de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fcq-6.5.lts.1-hotfix-GRANITE-61551-1.2.zip) |

<!-- OLD URL TO JAR
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) | -->


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## ¿Qué incluye [!DNL Adobe Experience Manager] 6.5 LTS, SP1? {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad inicial de 6.5 LTS en marzo de 2025. [Instale este Service Pack](#install-update) en 6.5 LTS.

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## Se han corregido problemas en 6.5 LTS, Service Pack 1 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### Accesibilidad {#sites-accessibility-65-lts-sp1}

* Se ha corregido un problema por el que el elemento del editor de texto de fragmentos de contenido se truncaba de forma predeterminada. El editor de texto ahora muestra el contenido completo sin truncarse. (SITES-33005)
* Se ha corregido un problema por el que al hacer clic en las rutas URL se abría la página principal de Indigo en lugar de la dirección URL de destino correcta. (SITES-33004)
* Se ha corregido un problema de accesibilidad en un componente personalizado de AEM que provocaba errores de conformidad con ADA durante las pruebas automatizadas. (SITES-30660)
* Se han corregido problemas de cumplimiento de ADA en el cuadro de diálogo Alerta y Mensajes de flujo de trabajo, garantizando que el texto se muestre en negro sobre fondos claros y cumpla los requisitos de contraste WCAG 2.0. (SITES-30138)
* Se ha corregido un problema de accesibilidad por el que el botón “Categoría” del editor de AEM Sites carecía de una etiqueta específica, lo que provocaba que JAWS la anunciara como “Menú del botón de imágenes” en lugar de proporcionar una etiqueta descriptiva. (SITES-27497)
* Se ha corregido un problema de accesibilidad por el que los iconos de marca de verificación de la pantalla Permisos efectivos carecían de texto alternativo, lo que impedía que JAWS leyera y transmitiera su significado. (SITES-27272)
* Se ha corregido un problema de accesibilidad por el que la página Permisos no mostraba un anuncio claro de JAWS para eliminar permisos de usuarios o grupos, lo que causaba confusión a los usuarios del lector de pantalla. (SITES-27238)
* Se ha corregido un problema de accesibilidad por el que los mensajes de error solo se mostraban como iconos sin texto descriptivo, lo que impedía que JAWS anunciara los errores cuando se producían. (SITES-27155)
* Se ha corregido un problema de accesibilidad por el que JAWS leía descripciones de botones incorrectas y poco claras en el entorno On-Premise de AEM, incluido el texto de nivel 2 del encabezado que faltaba para la sección de módulos. (SITES-27152)
* Se ha corregido un problema de accesibilidad por el que JAWS no anunciaba el número de resultados después de filtrar los valores en la pestaña AEM Assets. (SITES-27150)
* Se ha corregido un problema de accesibilidad por el que al crear una carpeta no se mostraba una confirmación y JAWS no la anunciaba en la interfaz de usuario de Assets. (SITES-27141)
* Se ha corregido un problema de accesibilidad en AEM Sites. JAWS no anunció errores de formulario, el enfoque se movió a elementos de error no interactivos y los errores de campo obligatorio no se mostraron en la pestaña de salida. (SITES-27138)
* Se ha corregido un problema de accesibilidad por el que el menú del botón Cronologías carecía de una etiqueta específica, lo que provocaba que JAWS solo leyera “Menú del botón Actividades” sin proporcionar una descripción clara. (SITES-27134)
* Se ha corregido un problema de accesibilidad por el que JAWS no anunciaba la acción o la función de los elementos de contenedor, que solo leían “Ruta de exploración v1” y “Botón v2” en lugar de las etiquetas descriptivas. (SITES-27131)
* Se ha corregido un problema de accesibilidad por el que el elemento emergente de publicación rápida no mostraba un mensaje de éxito adecuado, lo que impedía a los lectores de pantalla anunciar comentarios de finalización. (SITES-26912)
* Se ha corregido un problema de accesibilidad en la vista de columna coral en el que los elementos con funciones ARIA que requerían funciones secundarias no las contenían, lo que provocaba un incumplimiento de los estándares de accesibilidad. (SITES-26898)
* Se ha corregido un problema de accesibilidad por el que los textos “plantilla” y “propiedades” en la navegación superior de la página de creación no eran visibles en el modo Reflow, lo que impedía el acceso a los usuarios del teclado y del lector de pantalla. (SITES-26895)
* Se ha corregido un problema de accesibilidad por el que no se podía acceder a la ayuda contextual de los iconos “búsqueda”, “solución”, “ayuda”, “bandeja de entrada” y “usuario” de la navegación superior mediante la navegación con el teclado. (SITES-26889)
* Se ha corregido un problema de accesibilidad por el que los campos de formulario de pestaña Básico no proporcionaban sugerencias de error, lo que impedía a los usuarios recibir ayuda cuando los campos de entrada obligatorios estaban vacíos. (SITES-26885)
* Se ha corregido un problema de accesibilidad por el que los lectores de pantalla de NVDA y Narrador no anunciaban detalles de archivo de plantilla en la página Crear, lo que impedía a los usuarios recibir información completa mediante programación. (SITES-26884)
* Se ha corregido un problema de accesibilidad que utilizaba un nombre incorrecto para el “Cuadro de texto de título de página” en la pestaña Básico, lo que impedía que los lectores de pantalla proporcionaran información precisa a los usuarios. (SITES-26879)
* Se han actualizado los colores de primer plano y de fondo del botón para cumplir los requisitos de relación de contraste mínima WCAG 2.2 AA, lo que mejora la legibilidad y accesibilidad para todos los usuarios. (SITES-26877)
* Se ha resuelto un problema que provocaba que los textos “plantilla” y “propiedades” en la navegación superior de la página de creación desaparecieran tras cambiar de tamaño, lo que garantiza la visibilidad y accesibilidad para los usuarios con problemas de visión. (SITES-26872)
* Se ha corregido un problema que hacía que aparecieran varias barras de desplazamiento horizontales en la página principal después de aplicar un Reflow, lo que garantiza que se muestre una sola barra de desplazamiento para una accesibilidad y visibilidad del contenido adecuadas. (SITES-26800)
* Se ha corregido un problema de accesibilidad en el editor de páginas de AEM por el que el enfoque del teclado se restablece inesperadamente al principio de la barra de herramientas demográficas después de activar botones como Persona, Carro de compras o Abandonado. Ahora, el enfoque permanece en el botón activado para admitir flujos de trabajo coherentes de navegación mediante el teclado y lector de pantalla. (SITES-25306)
* Se ha corregido un problema de asociación de etiquetas de accesibilidad para el título de página y los campos de etiquetas. La interfaz de AEM ahora asocia correctamente las etiquetas de accesibilidad con los campos “Título” y “Título de página” al utilizar lectores de pantalla como JAWS. La corrección garantiza una lectura de etiquetas adecuada y mejora el cumplimiento de la ADA en la creación de páginas, las propiedades y los flujos de trabajo de movimiento. (SITES-27149)
* Se ha corregido la falta de etiqueta visual para los campos de entrada de comentarios en la cronología. Se han corregido las etiquetas visuales que faltaban para los campos de entrada de “comentario” en la sección de cronología para mejorar la accesibilidad. La actualización garantiza que los lectores de pantalla puedan anunciar con precisión las etiquetas de campo. Esta experiencia mejora la navegación y el envío de formularios para todos los usuarios, y sobre todo para las personas que dependen de las tecnologías de asistencia. (SITES-26903)
* Se ha corregido la accesibilidad del teclado para el botón de puntos suspensivos en comentarios de la cronología. Se ha habilitado la navegación mediante el teclado para el botón de puntos suspensivos (tres puntos) junto a los comentarios en la sección de cronología. Los usuarios ahora pueden acceder al botón e interactuar con él mediante la tecla de tabulación, lo que mejora la accesibilidad para los usuarios que dependen de la navegación solo mediante teclado. (SITES-26891)
* Se han mejorado los anuncios de NVDA/Narrator para resultados de búsqueda en los cuadros de diálogo de selección. Se ha actualizado el cuadro de diálogo Abrir selección para anunciar si se encuentran o no resultados de búsqueda al utilizar lectores de pantalla, como NVDA o Narrator. Esta mejora ayuda a los usuarios que dependen de las tecnologías de asistencia a comprender el resultado de sus acciones de búsqueda sin necesidad de confirmación visual. (SITES-26883)
* Se ha corregido la función ARIA del icono de puntos suspensivos junto al campo de entrada de comentarios. Se ha actualizado el icono de puntos suspensivos (tres puntos) junto al campo de entrada del comentario para utilizar la función ARIA correcta, lo que garantiza que los lectores de pantalla puedan identificar el elemento con precisión. Esta mejora optimiza el cumplimiento de la accesibilidad y la experiencia de los usuarios que dependen de las tecnologías de asistencia. (SITES-26881)
* Se han corregido atributos ARIA no válidos en los componentes de Coral UI. Se han actualizado los componentes de Coral UI para garantizar que todos los atributos ARIA utilicen valores válidos, lo que mejora la accesibilidad y el cumplimiento. En particular, se han abordado los casos en los que valores no válidos como `aria-modal="dialog"` se asignaban de forma incorrecta. Esta mejora permite a los lectores de pantalla interpretar correctamente los elementos del cuadro de diálogo, lo que mejora la accesibilidad para los usuarios que dependen de las tecnologías de asistencia. (SITES-26873)
* Visibilidad mejorada e información sobre herramientas para iconos en escenarios de reflujo. Se ha mejorado el comportamiento de reflujo para garantizar que la información sobre herramientas se muestre correctamente en los iconos **Descargar**, **Volver a procesar recursos** y **Finalizar compra**. Se centró en un problema de accesibilidad en el que los iconos y sus etiquetas se volvían invisibles cuando cambiaba el tamaño de la ventanilla móvil o la configuración de zoom del explorador. Esta corrección admite usuarios con visión reducida al mantener la visibilidad y proporcionar descripciones de iconos adecuadas durante el reflujo. (SITES-26871)


#### Interfaz de usuario administrador{#sites-adminui-65-lts-sp1}

* Se ha corregido un problema de accesibilidad por el que JAWS no anunciaba funciones de lista ni proporcionaba instrucciones de navegación y activación en el cuadro de diálogo Crear sitio. (SITES-30661)
* La compatibilidad del lector de pantalla con los mensajes de estado en la vista de filtro Sitios funciona según lo previsto, lo que garantiza que los usuarios reciban comentarios claros y oportunos al cambiar entre vistas. (SITES-24992)
* El selector de fechas del carril de los filtros se muestra completamente dentro de su contenedor, lo que proporciona un tamaño de destino táctil adecuado y elimina los problemas de recorte. (SITES-24988)
* Las etiquetas de filtro seleccionadas ahora utilizan HTML semántico y aria-labels que coinciden con la presentación visual, lo que garantiza una compatibilidad de funciones precisa y acciones claras para las tecnologías de asistencia. (SITES-24980)
* Se ha añadido un atributo aria-label a la región Carril de referencias para proporcionar una etiqueta única y descriptiva a los usuarios del lector de pantalla y garantizar una identificación uniforme de los puntos de referencia en toda la página. (SITES-24973)
* Se ha actualizado el carril de referencias para que utilice unidades relativas para el tamaño y la posición, lo que permite que el contenido se escale y siga funcionando completamente al ampliarse al 400 % en una ventanilla de 1280 x 1024. (SITES-24972)
* Los elementos de tabla confirmados en la vista de lista de la página principal de Sites contienen las funciones de encabezado de columna adecuadas, lo que permite a los lectores de pantalla anunciar encabezados para cada celda de datos. (SITES-24942)
* Ahora, NVDA anuncia la fecha de modificación en el directorio de árbol, lo que garantiza que los usuarios del lector de pantalla reciban información detallada completa sobre los recursos. (SITES-24782)
* Se ha corregido un problema por el que el lector de pantalla NVDA anunciaba texto incompleto para elementos en el componente Directorio de árbol en AEM Sites. NVDA ahora lee el texto completo para cada elemento, mejorando la accesibilidad y el cumplimiento normativo. (SITES-24780)
* Se ha añadido accesibilidad del teclado al divisor de ventanas en el directorio de árbol, lo que permite a los usuarios cambiar el tamaño de la barra lateral izquierda utilizando únicamente un teclado. (SITES-24779)
* Se han actualizado los resultados de búsqueda del menú Ayuda para incluir funciones ARIA correctas para los elementos de lista, lo que garantiza que los lectores de pantalla anuncien los vínculos correctamente para mejorar la accesibilidad. (SITES-24729)
* Se ha corregido un problema por el que los lectores de pantalla no anunciaban el mensaje de estado “X de Y resultados”. O bien, el mensaje “no se han encontrado resultados” después de aplicar los filtros en el panel Filtro de sitios, lo que garantiza que los usuarios reciban la confirmación adecuada de los resultados. (SITES-24720)
* Se han corregido las asignaciones de funciones que faltaban para los vínculos de navegación en la navegación de la aplicación. Se han añadido las funciones ARIA adecuadas para garantizar que los lectores de pantalla identifiquen y anuncien correctamente los elementos de navegación. (SITES-24719)
* Se ha reemplazado el marcado de función de cuadrícula incorrecto para las etiquetas de filtro seleccionadas con elementos de botón y se han añadido nombres accesibles, lo que garantiza que los lectores de pantalla anuncien e identifiquen correctamente las etiquetas. (SITES-24717)
* Se han añadido anuncios de lector de pantalla para el mensaje de estado Carril de referencias al realizar varias selecciones, lo que garantiza que los usuarios reciban confirmación de los cambios. (SITES-24678)
* Se ha corregido el comportamiento del campo de búsqueda para que el primer resultado no se anuncie automáticamente. Los lectores de pantalla ahora anuncian la cantidad de resultados que se encuentran, lo que permite a los usuarios navegar por la lista sin anuncios de enfoque incorrectos. (SITES-24658)
* Se han quitado atributos `aria-label` incorrectos de elementos estáticos no interactivos en la vista de lista para evitar que los lectores de pantalla anuncien información engañosa o irrelevante. (SITES-24515)
* Se ha actualizado la casilla de verificación de la primera columna de la vista de lista para utilizar el texto de la columna Título para su nombre accesible, lo que garantiza que los lectores de pantalla transmitan con precisión el propósito del campo de formulario. (SITES-24514)
* Se han añadido los atributos ARIA adecuados y compatibilidad con las regiones activas para anunciar mensajes de estado de carga a los usuarios del lector de pantalla al navegar por el contenido. (SITES-24481)
* Se ha actualizado el diseño interactivo para eliminar el desplazamiento horizontal cuando el contenido se amplía al 400 % con una anchura de ventanilla de 1280 x 1024, lo que garantiza una visibilidad completa sin desplazamiento lateral. (SITES-24308)
* Se ha corregido la navegación del enfoque en la IU del administrador de Sites para seguir un orden lógico, devolviendo el enfoque al botón “Seleccionar todo” después de pulsar Esc y moviendo el enfoque al siguiente elemento interactivo después de pulsar la pestaña. (SITES-24307)
* Se ha actualizado el orden de enfoque en la IU del administrador de Sites para que el botón de rutas de exploración del elemento `<betty-titlebar-title>` se centre en la secuencia correcta durante la navegación mediante el teclado. (SITES-24305)
* Se ha verificado la funcionalidad de omisión de vínculos para garantizar que mueva el enfoque del teclado al área de contenido principal, lo que permite a los usuarios del teclado omitir los elementos del encabezado y acceder al contenido de forma eficaz. (SITES-24061)


#### Interfaz de usuario clásica{#sites-classicui-65-lts-sp1}

Se ha corregido un problema en la IU clásica por el que faltaban etiquetas de la casilla de verificación y el HTML se mostraba como texto codificado en varios elementos de la interfaz de usuario, incluida la búsqueda por fecha y las interfaces no estándar. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM ahora evita la degradación del rendimiento causada por el formato incorrecto de los metadatos de XMP en los recursos de imagen. Los recursos que contienen nombres de propiedad de XMP no válidos o no compatibles, como los que tienen segmentos numéricos o estructuras no calificadas, ya no activan los registros de advertencia repetidos durante el procesamiento. El sistema filtra los metadatos problemáticos para garantizar que la ingesta y validación de recursos se complete sin errores. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-65-lts-sp1}

Otros autores aún pueden publicar fragmentos de contenido incluso cuando otro autor los desprotege lo que es contrario al comportamiento deseado de la función de desprotección. Esta corrección evita que otros usuarios vean o utilicen los botones de publicación en la interfaz de creación cuando se desprotege un fragmento de contenido. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### Consola de componente{#sites-component-console-65-lts-sp1}

Se ha corregido un problema en el componente Lista de productos por el que la casilla “Seleccionar todo” añadía solo las 20 primeras SKU de la página inicial en lugar de todas las SKU en los resultados de búsqueda. (SITES-29191)

#### Back-end principal{#sites-core-backend-65-lts-sp1}

Los metadatos de XMP con formato incorrecto activaron un error durante el procesamiento de los recursos de imagen en `ValidationDataServlet`. La corrección garantiza la administración de metadatos compatible y evita el análisis repetido de propiedades no válidas. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM: Live Copy{#sites-msm-live-copies-65-lts-sp1}

* Se ha corregido un error de JavaScript `ns.ui.alert is not a function` que se producía al volver a habilitar la herencia de componentes fantasma en AEM 6.5 local. (SITES-31993)
* Se ha corregido un problema por el que la opción Despliegue “Más tarde” permitía continuar sin seleccionar una fecha en AEM 6.5. (SITES-31374)

#### Editor de página{#sites-pageeditor-65-lts-sp1}

* Se ha resuelto un problema en el modal Teaser por el que la pestaña Vínculo y acciones seguía mostrando el estilo de error, los iconos y el atributo aria-invalid después de una entrada de datos y una resolución de error válidas. (SITES-25527)
* Se ha corregido un problema en el editor de texto del modal Teaser por el que los botones Listas y Párrafos no transmitían su estado expandido o contraído a los lectores de pantalla, lo que garantiza actualizaciones de atributos expandidas por aria precisas. (SITES-25365)
* Se ha corregido un problema en la barra de herramientas de demografía por el que, al ajustar el regulador del carro de compras con la entrada del teclado, el enfoque se desplazaba al botón del carro de compras en lugar de permanecer en el regulador, mejorando la eficacia de navegación de los usuarios del teclado. (SITES-25324)
* Se ha añadido un nombre accesible al regulador del carro de compras en la barra de herramientas de demografía al asignar un valor a su elemento `<label>` asociado. Esta corrección mejoró la compatibilidad con las tecnologías de asistencia y mejoró la capacidad de uso de los usuarios de lectores de pantalla. (SITES-25322)
* Se han añadido funciones ARIA y nombres accesibles a los botones de la lista desplegable Barra de herramientas de demografía. Esta corrección permitió la identificación adecuada mediante tecnologías de asistencia y mejoró la navegación para los usuarios del teclado y del lector de pantalla. (SITES-25315)
* Se ha ajustado el diseño de la barra de herramientas demográficas para evitar el desbordamiento del contenido más allá de la ventanilla con un zoom del explorador del 200 %, lo que garantiza que todos los controles permanezcan accesibles sin desplazamiento horizontal. (SITES-25309)
* Se ha corregido la administración del enfoque en la barra de herramientas demográficas para mantener el enfoque del teclado en el botón activado en lugar de restablecer el enfoque en la posición inicial de la barra de herramientas. (SITES-25306)
* El solapamiento de etiquetas del botón funciona según lo diseñado, mediante ayuda contextual para mostrar la etiqueta cuando los modos con anchuras de pantalla similares están activos. (SITES-25285)
* El modal de anotación incluye un botón de envío visible, que permite a los usuarios enviar anotaciones sin depender de la tecla Escape ni hacer clic fuera del modal. (SITES-25281)
* El modal de anotación incluye un botón de icono de lápiz que permite a los usuarios enviar anotaciones, lo que proporciona un método de envío claro y accesible. (SITES-25269)
* Se han corregido los anuncios del lector de pantalla para los botones Anotar y Cerrar anotación a fin de proporcionar comentarios precisos y relevantes y eliminar información no relacionada o confusa. (SITES-25268)
* Las secciones de lienzo de las páginas del Editor de AEM ahora admiten la accesibilidad total del teclado. Los usuarios pueden activar los títulos de sección y los botones de edición utilizando únicamente el teclado, sin depender del desplazamiento del ratón. Esta actualización garantiza el cumplimiento de WCAG 2.1.1 y mejora la capacidad de uso entre componentes (como los modales Teaser, Imagen, Carrusel, Diseño, Deformación de tiempo y Anotación). (SITES-25256)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal Carrusel a una anchura de 320 píxeles para garantizar que todo el contenido se muestre dentro de la ventanilla sin que se requiera la navegación de lado a lado. (SITES-25254)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal Imagen a 320 píxeles de anchura para garantizar que todo el contenido se muestre dentro de la ventanilla sin necesidad de navegación de lado a lado. (SITES-25244)
* Se ha eliminado el desplazamiento horizontal innecesario en el modal Teaser a 320 píxeles de anchura para garantizar que todo el contenido se muestre dentro de la ventanilla sin que se requiera la navegación de lado a lado. (SITES-25242)
* Se ha habilitado la navegación mediante el teclado para el menú emergente `List` y `Paragraph Format`, ambos en el modal Teaser. Esta corrección permite a los usuarios acceder y navegar por estos menús con las teclas de flecha. (SITES-25235)
* Se han corregido los anuncios del lector de pantalla para los botones Anotar y Cerrar anotación para proporcionar comentarios precisos y relevantes alineados con las acciones asociadas. (SITES-25234)
* Se ha mejorado la etiqueta del botón Ayuda en el modal Teaser para describir claramente su propósito y proporcionar un contexto significativo para todos los usuarios, incluidos los usuarios de tecnología de asistencia. (SITES-25224)
* Se ha mejorado la regla del emulador para los usuarios del lector de pantalla al asociar las mediciones de la regla con sus respectivos dispositivos. Además, se ha reemplazado la ayuda contextual por un elemento aria-describedby. (SITES-24955)
* No se ha implementado ninguna corrección porque el botón Editar funciona según lo previsto y proporciona un contexto informativo en lugar de realizar una acción. (SITES-24950)
* El orden de enfoque confirmado en la página del editor sigue una secuencia lógica, lo que permite a los usuarios navegar por todos los elementos interactivos sin omitir ni volver a crear bucles de forma inesperada. (SITES-24937)
* El lienzo del modo de vista previa confirmado actualiza correctamente el espaciado del texto cuando los usuarios aplican la configuración personalizada de espaciado de texto, lo que garantiza un formato coherente en todas las áreas de contenido. (SITES-24936)
* El botón Vista previa verificado ya no activa los cambios de contexto o estado en el enfoque, lo que garantiza que los usuarios activen el botón de manera intencionada antes de que se actualice la vista de página. (SITES-24784)
* Se han añadido asignaciones de funciones ARIA correctas a los vínculos de navegación de la aplicación, lo que permite a los lectores de pantalla identificarse con precisión y anunciar elementos de navegación para mejorar la accesibilidad. (SITES-24718)
* Se ha actualizado el botón Cambiar filtros para anunciar estados expandidos y contraídos en los lectores de pantalla, se han eliminado atributos ARIA redundantes y se ha ajustado el etiquetado para proporcionar descripciones claras y no duplicadas. (SITES-24713)
* Se han añadido anuncios de lector de pantalla para los mensajes de estado de los resultados de búsqueda en el cuadro de diálogo Selección de vínculos, lo que garantiza que los usuarios reciban confirmación cuando se carguen los resultados o no se encuentren coincidencias. (SITES-24700)
* Se han añadido anuncios de lector de pantalla para el estado de carga del modal Imagen, lo que garantiza que los usuarios reciban comentarios cuando el modal se carga y está listo para la interacción. (SITES-24697)
* Se ha resuelto un problema de accesibilidad por el que el encabezado fijo ocultaba el contenido del modal Teaser al 200 % y al 400 % de zoom, lo que garantiza una visibilidad y una facilidad de uso completas al utilizar la ampliación de la página. (SITES-24523)
* Se ha añadido un mensaje de estado con el número de resultados de búsqueda en el campo Buscar/Filtrar, lo que permite que los lectores de pantalla anuncien los resultados a los usuarios. (SITES-24506)
* Se han añadido anuncios de lector de pantalla para la cantidad de resultados de búsqueda en el campo Buscar/Filtrar, lo que garantiza que los usuarios reciban comentarios inmediatos cuando se cargan los resultados. (SITES-24505)
* Se ha añadido un nombre accesible a la lista de pestañas del panel Carril lateral, lo que permite a los lectores de pantalla anunciar su propósito de acuerdo con las directrices WAI-ARIA. (SITES-24492)
* Se han añadido etiquetas descriptivas a los iconos ambiguos del editor, lo que garantiza que todos los usuarios entiendan claramente la función de cada botón. (SITES-24480)
* Se ha habilitado la accesibilidad completa del teclado para los títulos de sección y los botones de acción en la vista Lienzo, lo que garantiza un funcionamiento coherente para los usuarios del ratón y el teclado. (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Editor universal {#sites-universal-editor-65-lts-sp1}

* Se ha corregido una condición de carrera en QueryTokenService que provocaba inicios de sesión incorrectos cuando varias solicitudes con parámetros de consulta se activaban antes de que el servicio de tokens de inicio de sesión devolviera un resultado. (SITES-30659)
* Se ha corregido un problema en UniversalEditorURLService por el que al guardar una matriz de rutas asignadas en Felix ConfigMgr solo se guardaba el primer elemento. (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

Se ha corregido un problema por el que la sincronización de recursos de DAM remota con AEM local de Sites eliminaba el estado publicado y las propiedades relacionadas con la replicación de los activos. (Assets-48958)

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

Se han resuelto ciclos de dependencia de OSGi que bloqueaban el funcionamiento de la fábrica del motor de scripts HTL, lo que garantiza la resolución adecuada del servicio y la ejecución de scripts. (Granite-58275)

#### Integraciones{#foundation-integrations-65-lts-sp1}

* Se ha eliminado el uso de commons-httpclient 3.x del paquete `com.adobe.cq.cq-analytics-integration` y se ha reemplazado por `org.apache.httpcomponents.httpclient` 4.5.13.B0001 para que se ajuste a los estándares más recientes de AEM 6.5 LTS. (CQ-4360586)
* Se ha eliminado el paquete de integración de Search&amp;Promote obsoleto de AEM para eliminar los componentes no utilizados y reducir la sobrecarga en el mantenimiento. (CQ-4358030)
* Se han añadido nuevos casos de prueba back-end para la integración de SiteCatalyst con el fin de mejorar la validación de análisis y garantizar una cobertura más completa. (CQ-4359991)
* Se ha corregido un problema en la sección Propiedades de Launch Config por el que no aparecían los menús desplegables Compañía y Propiedad. Además, Guardar y cerrar activaba errores a pesar de que se rellenaban todos los campos obligatorios y se mostraban mensajes de error incorrectos para Compañía y Propiedad cuando solo el campo Título estaba vacío. (CQ-4359853)
* Se ha eliminado la entrada de ruta de acceso al servlet `searchpromote` de la versión 6.6 para alinearla con la eliminación del paquete de Search&amp;Promote. (CQ-4359523)
* Se han corregido casos de prueba HTTP para el repositorio de Target a fin de garantizar una validación precisa y una fiabilidad de las pruebas mejorada. (CQ-4359022)
* Se ha eliminado el uso de almacenamiento en caché de Guava del módulo integration-adobeims-console para eliminar las dependencias de la biblioteca de Guava. (CQ-4358710)
* Se han validado los flujos de trabajo de integración de DTM, las tareas de la bandeja de entrada y la funcionalidad del proyecto en AEM 6.6 para garantizar un funcionamiento adecuado en AEM 6.5. (CQ-4358151)
* Se ha validado la funcionalidad de datos de contenido en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357774)
* Se ha validado la funcionalidad de Cloud Services en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357773)
* Se ha validado la integración de la consola de Adobe IMS en AEM 6.6 para garantizar la compatibilidad y el funcionamiento adecuado en AEM 6.5. (CQ-4357772)
* Se ha actualizado la canalización de Jenkins para que la integración de Test&amp;Target se ejecute en Java 17, resuelva las pruebas de Selenium que fallan, mueva las pruebas seleccionadas a Playwright y garantice que todas las pruebas unitarias se realicen correctamente. (CQ-4357770)
* Se han alineado integraciones, flujo de trabajo, bandeja de entrada y proyectos DX con la rama 6.6.0 mediante la actualización de canalizaciones de compilación y prueba. Además, se han resueltos los problemas de compatibilidad de actualización y se han validado todos los servicios afectados para mantener la estabilidad y la funcionalidad. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### Localización{#foundation-localization-65-lts-sp1}

* Se han localizado las cadenas en el cuadro de diálogo “Quitar control de acceso” de la lista “Permisos” para mostrar las traducciones correctas. (GRANITE-59427)
* Se ha corregido un problema en el cuadro de diálogo Añadir regla de “Propiedades de división O” del editor del modelo en el que aparecían sin localizar varias cadenas de interfaz de usuario, incluidos operadores y etiquetas de campo. Ahora todas las cadenas se muestran con la localización correcta. (CQ-4354014)
* Se ha añadido la traducción que falta para la ayuda contextual “Mostrar descripción para” en el cuadro de diálogo Editar modelos de flujo de trabajo. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

Se ha resuelto un problema por el que AEM volvía a crear o cambiar el nombre de los archivos de configuración existentes en `/apps/system/config` durante las actualizaciones, sustituyendo los archivos `.cfg.json` por los archivos `.config`. (GRANITE-58899)

#### OmniSearch{#foundation-omnisearch-65-lts-sp1}

Se ha corregido un problema de accesibilidad por el que los marcadores de posición aparecían incorrectamente como etiquetas para los campos de entrada. Este problema provocaba la falta de etiquetas de campo en la búsqueda, en los fragmentos de experiencias de AEM, en los fragmentos de contenido y en los modelos de fragmentos de contenido. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### Proyectos{#foundation-projects-65-lts-sp1}

* Se ha resuelto un problema que mostraba un elemento emergente de error incorrecto al eliminar un proyecto en la vista Calendario, a pesar de que la eliminación del proyecto se había realizado correctamente. (CQ-4358890)
* Se ha corregido un problema en Firefox por el que el pie de página de la tarjeta “Colección de recursos” en la vista Proyecto se solapaba con el borde de la tarjeta. El pie de página ahora se alinea correctamente sin solaparse. (CQ-4353317)

#### Guía de inicio rápido{#foundation-quickstart-65-lts-sp1}

* Se ha actualizado el script de desinstalación para ajustar el intervalo de versiones del paquete Guava, lo que evita que se bloquee al instalarlo mediante el Administrador de paquetes. (GRANITE-59559)
* Se ha corregido un problema en la IU de replicación que mostraba un error (`#1660`) al editar los agentes de replicación al corregir la administración de las casillas de verificación clásicas en la interfaz. (GRANITE-58302)
* Se han resuelto varios errores de inicio del almacén de datos S3 al ejecutar AEM 6.5 LTS con JDK 21 al solucionar los permisos de servicio que faltaban, actualizar la gestión de la configuración y garantizar que los servicios necesarios se inicialicen correctamente. (GRANITE-57082)
* Se ha definido la estrategia de mantenimiento y soporte para AEM 6.5. Esta corrección incluía lo siguiente:
   * Cadencia de Service Pack.
   * Cadencia de revisión.
   * Compatibilidad paralela con AEM 6.6.
   * Matriz de compatibilidad actualizada.
   * Responsabilidades de propiedad complementarias. (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* Se ha actualizado Sling ResourceAccessSecurity a la versión 1.1.2 para resolver un problema de tipo `ClassCastException` que se producía cuando múltiples referencias `ResourceAccessGate` inicializaban `ResourceAccessSecurityImpl`. (NPR-42750)
* Se ha corregido un problema en la integración de Adobe Stock por el que el cuadro de diálogo Licencia aparecía atenuado. Este problema se debió a que la función `sunt:initList` quitó los campos de entrada necesarios. La función se ha encontrado en las bibliotecas de cliente de Coral Foundation. Se han actualizado las bibliotecas de cliente para conservar los campos necesarios, lo que permite la correcta funcionalidad del cuadro de diálogo de licencia. (NPR-42748)
* Se corrigió un error inesperado de compilación de JSP con `org.apache.sling.scripting.jsp 2.6.0`. (NPR-42640)

<!--
* Backported the fix for Sling Scripting issue that caused `DataTimeParseException` and `String.length()` null pointer exceptions during package installation. Updated Sling Scripting to version 2.8.3-1.0.10.6 to reduce installation errors and improve stability. (NPR-42640) -->

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### Interfaz de usuario{#foundation-ui-65-lts-sp1}

* Se ha resuelto un problema en la interfaz de usuario de AEM Author que limitaba la visualización de grupos de usuarios a 41. Este problema se debía a un límite de lotes predeterminado en el componente de selector de grupos de Granite UI. Se ha actualizado el componente para mostrar todos los grupos sin truncarse. (NPR-42749)
* Se ha resuelto un problema en el asistente de creación de la página local en el que los campos obligatorios de los componentes de varios campos no se volvían a validar al editar propiedades de la página. Este problema, a su vez, permitía a los autores omitir la validación y continuar con los datos incompletos. (GRANITE-58826)
* Se han corregido los atributos ARIA del botón de ayuda de AEM para garantizar que los lectores de pantalla de JAWS anuncien una etiqueta clara y fácil de usar en lugar de mostrar el icono sin traducir y los metadatos de texto. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* Se ha añadido compatibilidad con Java 17 para AEM Translations mediante la actualización de paquetes de traducción, la verificación de la compatibilidad de paquetes Java, la eliminación de dependencias obsoletas y la garantía de una funcionalidad completa mediante pruebas completas. (CQ-4357525)
* Se ha eliminado la prueba Evergreen inestable `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater` para evitar errores falsos durante las pruebas automatizadas. (CQ-4298376)

#### Flujo de trabajo{#foundation-workflow-65-lts-sp1}

* Se ha añadido el atributo `data-detailsurl` que falta en los elementos de la bandeja de entrada para evitar que aparezcan valores no definidos en las direcciones URL al usar AEM 6.5 LTS con Java 21. (GRANITE-60158)
* Se corrigió una excepción NullPointerException en el método `deactivate` del paquete `WorkflowToPublishEventService` al ejecutar AEM 6.5 LTS con Java 21, lo que garantiza el cierre correcto del servicio de flujo de trabajo sin errores. (GRANITE-58151)
* Se ha actualizado el índice del flujo de trabajo para admitir el uso compartido, la personalización fuera de la oficina y la resolución de problemas de consulta de cronología. (GRANITE-52640)
* Se ha actualizado el índice del flujo de trabajo para admitir el uso compartido, las funciones de personalización fuera de la oficina y la resolución de problemas de consulta de cronología. (GRANITE-52294)
* Se han resuelto más errores de registro durante la validación de la comparación de registros para una actualización de programa a AEM versión 10912, lo que garantiza una ejecución estable del flujo de trabajo. (GRANITE-44268)
* Se ha actualizado el método de limpieza de URL en las repositorios de flujo de trabajo para reemplazar `url.searchParams` por `url.search`, lo que mejora la protección XSS para las URL vulnerables. (CQ-4359585)
* Se ha validado la funcionalidad de flujo de trabajo, bandeja de entrada y proyectos en AEM 6.6 Forms para garantizar un funcionamiento y una integración adecuados. (CQ-4358777)
* Se ha implementado la automatización para lanzar artefactos de contenido de flujo de trabajo a través de Jenkins, lo que permite procesos de implementación optimizados y coherentes en AEM 6.5. (CQ-4358472)
* Se ha corregido un problema en el flujo de trabajo Crear tarea de la bandeja de entrada por el que el cuadro de diálogo “Añadir tarea” no se cerraba después de hacer clic en Enviar, a pesar de que la tarea se estaba creando, debido a un error de sintaxis de JavaScript. (CQ-4355336)
* Se ha corregido un problema que impedía guardar la configuración de la vista Bandeja de entrada porque faltaba una definición de propiedad para `isEndUserConfigurationEnabled`. (CQ-4287757)

## Formularios

### Forms Designer

* Cuando un usuario exporta los datos de un PDF basado en XFA mediante exportDataAPI, el XML resultante muestra discrepancias cuando se compara con los datos XML exportados manualmente mediante Acrobat Reader. Faltaban valores de algunos campos en la salida en comparación con la salida generada desde Acrobat Reader. (LC-3922791)
* La generación de una etiqueta de PDF con el servicio Output en Workbench añade una etiqueta inesperada bajo la etiqueta de referencia en un elemento de tabla de contenido. (LC-3922756)
* Al acoplar archivos PDF dinámicos y rellenables al formato PDF/A mediante el servicio Output, no se conserva el estado dinámico. Este problema provoca la pérdida de datos y posibles problemas de cumplimiento, especialmente cuando el etiquetado está habilitado. (LC-3922708)
* Cuando un usuario coloca pies de ilustración de campo con alineación inferior o derecha en AEM Forms Designer, el árbol de etiquetas incluye solo el pie de ilustración sin el valor correspondiente, lo que provoca un etiquetado de accesibilidad incompleto. (LC-3922619)
* Los códigos QR de los PDF generados no se pueden leer. El texto alternativo para los códigos QR también falla en las pruebas de accesibilidad, lo que afecta a la compatibilidad con los lectores de pantalla. (LC-3922551)
* Cuando un usuario procesa una carta en la interfaz de usuario del agente, el contenido no se muestra correctamente debido a la API render() de FormService. (LC-3922461)
* Cuando un usuario intenta crear archivos PDF/A a partir de XDP con estilo de cuadrado hundido en AEM Forms, se producen problemas de procesamiento de bordes. (LC-3922180)
* Acoplar formularios dinámicos enlazados a un esquema XSD provoca la pérdida parcial de datos, ya que algunos datos de formulario enlazados no se retienen en el PDF final. (LC-3922008)
* Cuando un usuario intenta exportar datos de archivos PDF interactivos mediante la API extractData en AEM Forms 6.5.13 y versiones posteriores, se producen datos que faltan en comparación con la exportación manual. (LC-3921983)
* Convertir formularios XDP en PDF estáticos con AEM Forms Designer o el servicio Output crea varias etiquetas `Link-OBJR`. Los problemas causan un problema de cumplimiento de la accesibilidad porque se espera una sola etiqueta de vínculo unificado. (LC-3921977)

### Formularios adaptables

* En AEM Forms, la habilitación de “Permitir texto enriquecido para el título” en el panel raíz hará que “Excluir título del documento de registro” en un panel anidado oculte el título del panel raíz de forma incorrecta. Lo hace así en el documento de registro generado. (FORMS-19696)
* El sistema ignora el `sling:resourceType` personalizado asignado a través de `aem:afProperties` en un esquema JSON. El tipo de recurso personalizado se omite durante el procesamiento. (FORMS-19691)
* Cuando un usuario envía un formulario adaptable con archivos adjuntos rellenados previamente mediante URI, el envío del formulario falla con una NullPointerException debido a la falta de datos binarios. (FORMS-19371) (FORMS-19486)
* Cuando un usuario carga un PDF en la sección “Formularios y documentos”, la función de cronología deja de funcionar. (FORMS-19407)(FORMS-19234)
* Cuando un usuario carga archivos mediante el componente de archivos adjuntos listo para usar (OOTB) en AEM Forms, se identifican vulnerabilidades de seguridad. El problema lleva a una posible interceptación del proceso de envío por entidades no autorizadas. (FORMS-19271)
* Cuando un usuario configura un formulario adaptable listo para usar en AEM Forms para generar un documento de registro (DoR) automáticamente, el campo “Título” de las propiedades del documento de Acrobat Reader no muestra el título del documento de registro capturado. De forma predeterminada, el título del formulario no aparece en lugar del nombre del archivo. (FORMS-19263)
* Cuando un usuario abre una comunicación interactiva en la interfaz de usuario de Agent, los datos rellenados previamente no se pueden borrar por completo; al eliminarlos, se rellenan automáticamente con los mismos datos. (FORMS-19151)
* Cuando un usuario previsualiza un campo de fecha en la interfaz de usuario de Agent, la fecha cambia inesperadamente. El problema se produce debido a discrepancias de las zonas horarias entre la configuración UTC de VM y la interpretación de la fecha por parte del sistema. (FORMS-19115)
* Cuando un usuario envía un formulario, los archivos adjuntos pueden duplicarse, lo que provoca varias cargas del mismo archivo. (FORMS-19045)(FORMS-19051)
* La adición de coordinadores a los conjuntos de políticas en Document Security falla tanto en los entornos de producción como en los entornos inferiores. (FORMS-18603, FORMS-18212, FORMS-19697)
* Cuando un usuario hace clic en el “datepicker-calendar-icon” en modo de escritorio con un campo vacío, se produce un error debido a la variable indefinida _$focusedDate, lo que interrumpe los scripts personalizados asociados. (FORMS-18483)(FORMS-18268)
* Cuando un cliente obtiene una vista previa de una carta, el campo “Cantidad en palabras” no muestra o actualiza los valores numéricos incorrectamente, lo que provoca desalineación y falta de espacios en el contenido. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004)
* Cuando un cliente previsualiza una carta guardada en RHEL, el contenido no se alinea correctamente, faltan espacios y aparecen caracteres inesperados como “x”. (FORMS-18422)(FORMS-17641)
* Cuando un usuario navega entre las pestañas de AEM Forms, la selección de componentes en la primera pestaña deja de responder. (FORMS-18345)
* Cuando un usuario convierte un archivo HTML a PDF mediante la opción WebToPDF, el PDF de salida no muestra la sección de encabezado, incluidas las etiquetas de metadatos y título. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)
* En AEM JEE Process Manager SDK, cuando un usuario invoca el método retryAction(long actionOid), el sistema reintenta incorrectamente la primera acción encontrada en la tabla tb_action_instance. Este flujo de trabajo se produce incluso cuando se proporciona un ID de acción específico o cuando el ID es nulo, lo que da lugar a un comportamiento no deseado. (FORMS-18187)
* Un usuario encuentra problemas en los que las funcionalidades de borrador y envío guardadas fallan sin mostrar ningún mensaje de error. (FORMS-18069)
* La transición de componentes de base basados en XSD a componentes principales evita la implementación de referencias entre archivos en esquemas JSON, lo que afecta a la migración de Formularios adaptables. (FORMS-18065)
* Cuando un usuario obtiene una vista previa de una carta en la IU del agente, el campo de fecha muestra un valor incorrecto debido a problemas de conversión de tiempo CI. Estas discrepancias surgen de las diferencias de huso horario entre el entorno de la VM y la interpretación del tiempo por parte del sistema (horario UTC frente a hora local). (FORMS-17988) (FORMS-17248)
* Cuando un usuario obtiene una vista previa de las cartas mediante plantillas de notificación CI en AEM Forms, los tiempos de generación del PDF varían significativamente, de 1,5 segundos a más de 10 segundos, incluso en el mismo servidor. Esta incoherencia afecta a los flujos de trabajo críticos para el negocio. (FORMS-17951)
* Cuando un usuario enlaza un objeto de firma manuscrita en un formulario adaptable a un XDP mediante la opción “Fuentes de datos”, los cambios no se pueden guardar. El motivo se debe a errores persistentes de validación de la relación de aspecto, incluso cuando se utilizan valores válidos. (FORMS-17587)
* Cuando un usuario utiliza un XDP específico con muchos campos ocultos para fragmentos de documento, AEM crea nodos de CRX con la propiedad `cm:optional` establecida en falso, lo que provoca que falle el envío de la comunicación interactiva (CI). (FORMS-17538)
* Cuando un cliente obtiene una vista previa de una carta, el campo del cuadro numérico no gestiona correctamente los valores negativos cuando se definen los límites de dígitos para el posible cliente potencial y el valor de fragmento. Este problema se produce debido al uso de parseFloat, que trata el signo menos como parte del número. (FORMS-17451)
* Cuando se obtiene una vista previa de una carta, se advierte el uso del comodín “*” en el archivo Adobe.json, lo que plantea una preocupación sobre su finalidad y su posible modificación. (FORMS-17317)
* Cuando un usuario utiliza un lector de pantalla en la cuenta conjunta Solicitar un ahorro de tasa fija, los encabezados se anuncian incorrectamente como elementos en los que se puede hacer clic, lo que provoca problemas de accesibilidad. (FORMS-17038)
* Cuando se incrusta un formulario, al iframe generado le falta un atributo de título, lo que provoca un problema de cumplimiento de la accesibilidad. (FORMS-17010)
* La descarga de un formulario mediante la IU del administrador de Forms siempre incluye dependencias asociadas, como temáticas y fragmentos. (FORMS-15811)
* Cuando un usuario accede al formulario en dispositivos móviles (iOS y Android™), los botones “siguiente” y “anterior” de la primera página están desactivados. Sin embargo, el lector de pantalla no los identifica como deshabilitados. (FORMS-15773)
* Cuando un usuario guarda un formulario grande con fragmentos y carga diferida habilitados, no puede recuperar borradores, lo que interrumpe el flujo de trabajo. (FORMS-19890, FORMS-19808)
* Los usuarios han experimentado problemas al guardar las propiedades del formulario para el formulario adaptable basado en los componentes principales. Esto se producía porque se incluyen scripts redundantes del formulario adaptable basados en el editor de componentes de base, lo que provocaba conflictos en el formulario adaptable basado en los componentes principales. editor. (FORMS-17474)
* Los usuarios han tenido problemas con la página de firma de Adobe Sign GovCloud que no se representaba en un iframe. (FORMS-16803)
* Los usuarios experimentan errores al seleccionar referencias para fragmentos de formularios adaptables (AF) de componentes principales. Aparecía el mensaje de error “No se puede procesar la referencia: no es una ruta absoluta”, lo que impedía el renderizado de referencias adecuado. (FORMS-19678)
* Se ha añadido compatibilidad con la conversión multiproceso con Acrobat DC, lo que permite a los usuarios realizar conversiones simultáneas de documentos de Word, Excel y PowerPoint en documentos PDF de forma más eficaz. (FORMS-21310)
* Se ha añadido la inclusión del paquete `com.adobe.granite.toggle.impl.dev` en el Service Pack 24 de AEM, lo que permite procesos de desarrollo más optimizados al eliminarlo del complemento de Forms. (FORMS-20139)
* Se ha eliminado FeatureToggleRenderConditionServlet del paquete forms-foundation y com.adobe.granite.toggle.impl.dev del complemento Forms. Esta actualización garantiza que, después de la instalación del complemento de Forms, la condición de procesamiento se resuelva correctamente, lo que mejora la funcionalidad del componente para los clientes. (FORMS-20138)
* Los usuarios experimentaron un rendimiento lento debido a consultas de larga ejecución en formularios adaptables. Esta actualización respalda los cambios de consulta para mejorar la eficacia. Los clientes ahora pueden crear un índice con el nombre de etiqueta aemformsAFRereferences. (FORMS-21411)
* Los usuarios experimentaban desalineación en las posiciones de los encabezados al convertir HTML a formato de documento portátil (PDF,Portable Document Format) mediante WebtoPDF. Este problema afectaba a la coherencia del diseño del documento y a la legibilidad de la salida. (FORMS-21502, FORMS-21540)
* Los usuarios experimentaban errores de validación de PDF/A-1b a pesar de la verificación correcta de PreFlight. Este problema afectaba a las comprobaciones de conformidad de documentos para clientes empresariales que utilizan las herramientas de validación de PDF. (FORMS-20196)
* Los usuarios experimentaban cadenas sin traducir en la interfaz de usuario, lo que causaba confusión y dificultades para comprender la interfaz. (FORMS-6542)
* Los usuarios han experimentado problemas con las notificaciones por correo electrónico. El paso Enviar flujo de trabajo de correo electrónico no pudo enviar correos electrónicos, lo que afectó a los procesos de comunicación automatizados. (FORMS-17961)
* Los usuarios experimentaron errores en las pruebas de los flujos de trabajo de formularios, lo que afectó a su capacidad para completar procesos de flujo de trabajo de forma eficaz. (FORMS-16231)
* Los usuarios no pudieron utilizar la función de cronología de los PDF en los formularios de AEM. Este problema afectaba a la capacidad de los usuarios para rastrear los cambios y revisiones de los documentos de forma eficaz. Al cargar cualquier PDF en la sección “Formularios y documentos&quot; del área de AEM Forms, la vista de cronología deja de funcionar. (FORMS-19408)
* Los usuarios experimentan una excepción de puntero nulo al interactuar con OData. Esto causa interrupciones en los procesos de recuperación de datos. (FORMS-20348)
* Se ha eliminado la biblioteca google.common.collect tras la eliminación de Guava, una biblioteca Java de código abierto. Esta actualización garantiza una mejor compatibilidad y rendimiento para los clientes empresariales que utilizan Formularios adaptables. (FORMS-17031)

### Captcha de Forms

* Se ha añadido compatibilidad con `Hcaptcha` y `Turnstile` para Formularios adaptables basados en componentes de base. (FORMS-16562)
* Los usuarios experimentaron problemas de superposición de iconos en el cuadro de diálogo `Create hCaptcha Configuration`. Al rellenar los campos obligatorios, el icono de información se solapaba con el icono de error, lo que provocaba confusión durante la configuración. (FORMS-16916)
* Los usuarios experimentaron una configuración incorrecta al ser recogida para reCAPTCHA en Formularios adaptables en función de los componentes de base. Cuando no se seleccionó el contenedor de configuración para un formulario, el problema se debió a varias configuraciones en la carpeta `conf/global`. (FORMS-19237)
* Los usuarios experimentaron problemas con reCAPTCHA, que no se procesaba. Esto afectaba a los envíos de formularios y a la validación de seguridad para clientes empresariales. (FORMS-17136, FORMS-19596)
* Los usuarios experimentan un problema en el cual el tamaño de la empresa reCAPTCHA no se refleja en la interfaz de usuario (IU). (FORMS-16574)
* Los usuarios experimentaron problemas con la funcionalidad ReCaptcha debido a un ResourceResolver no cerrado en `ReCaptchaConfigurationServiceImpl`, lo que provocó errores de validación intermitentes durante los envíos del formulario. (FORMS-19241)
* Los usuarios experimentaban problemas con la validación de reCAPTCHA cuando los formularios se creaban en Sites. Los formularios AEM no reconocían correctamente el nombre del formulario, lo que provocaba errores de validación. (FORMS-20486)
* Los usuarios experimentaron envíos de formularios incluso cuando la puntuación de reCAPTCHA empresarial era 1,0, lo que producía posibles riesgos de seguridad. (FORMS-16766){{$include }}
* Se han mejorado las alertas reCAPTCHA en Formularios adaptables al actualizar los códigos de error de envío a 400. Además, se han refinado las alertas de registro para distinguir entre tiempos de espera, caducidades y errores de detección de bots, lo que mejora la precisión de la resolución de problemas y la observabilidad del sistema. (FORMS-19240)
* Se ha cerrado una instancia ResourceResolver no cerrada en ReCaptchaConfigurationServiceImpl para evitar posibles fugas de recursos y mejorar la estabilidad del sistema al utilizar integraciones de reCAPTCHA en AEM Forms. (FORMS-19242)
* Se ha mejorado la administración de la configuración de CAPTCHA para AEM Forms, al garantizar que la configuración correcta se vincula a cada formulario cuando existen varias entradas en la carpeta /conf/global. Evita el uso no intencionado de configuraciones de CAPTCHA incorrectas cuando el contenedor de configuración no está seleccionado explícitamente. (FORMS-19239)

### IU de administración de formularios

* Los usuarios experimentaron cadenas no localizadas en el proceso de creación de `Forms` > `Create Watchfolder` >` Watchfolder`. Al crear una carpeta inspeccionada, no se encontraron cadenas como `Watchfolder creation` y `Watchfolder created successfully`, lo que afectó a la experiencia de la interfaz de usuario. (FORMS-15234)

## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 LTS se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x se utiliza como motor servlet para Quickstart.

### Compatibilidad con Java™  {#java-support}

* Compatibilidad con Java™ 17 y Java™ 21.
* Para obtener un rendimiento óptimo, reemplace los valores predeterminados de GC por otros valores. Para obtener más información, consulte la sección [Instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye actualizaciones de mantenimiento de Java™ 17 y Java™ 21 para que las utilicen los clientes en proyectos relacionados con AEM cuando no están disponibles para el público desde Oracle.

### Empaquetado de Uberjar {#uber-jar-packaging}

* Hay una ligera diferencia en el empaquetado de Uberjar de AEM 6.5 LTS. Para obtener más información, consulte [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Actualizar {#upgrade}

* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

#### Prácticas recomendadas para las actualizaciones del Service Pack de AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**Entorno**
Se aplica a: clientes de AEM 6.5 LTS (locales) que instalan el Service Pack 1 (SP1). SP1 se suministra como un archivo JAR de inicio rápido.

**Por qué es importante**
SP1 para AEM 6.5 LTS se envía como un archivo JAR de inicio rápido en lugar de como un archivo ZIP para instalarlo a través del administrador de paquetes. Los clientes locales se actualizan reemplazando el JAR de Quickstart, descomprimiéndolo y reiniciándolo. Este método es coherente con el procedimiento de actualización in situ de Adobe.

**Flujo de actualización recomendado (autor o publicación)**

1. Compruebe que la instancia de AEM 6.5 LTS esté en buen estado y sea accesible.
1. Descargue el archivo JAR de inicio rápido SP1 (por ejemplo, `cq-quickstart-6.6.x.jar`) desde Distribución de software.
1. Detenga la instancia en ejecución.
1. En el directorio de instalación de AEM (fuera de `crx-quickstart/`), reemplace el JAR de inicio rápido anterior por el JAR SP1.
1. Descomprima el archivo JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Ajuste los indicadores de pila según sea necesario).

1. Cambie el nombre del JAR descomprimido para que coincida con la función y el puerto, por ejemplo `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Inicie AEM y confirme la actualización en la interfaz de usuario (Ayuda > Acerca de) y en los registros.

**Buena higiene**

* Ejecute la actualización en entornos de prueba o inferiores antes de la producción.
* Realice copias de seguridad completas y restaurables (repositorio más cualquier almacén de datos externo) antes de empezar.
* Revise las directrices de actualización in situ y los requisitos técnicos de Adobe (se recomienda Java 17/21 para LTS).

>[!NOTE]
>
>Los nombres de archivo mostrados arriba (por ejemplo, `cq-quickstart-6.6.x.jar`) reflejan la nomenclatura de artefactos de inicio rápido de SP1 detectada para esta versión de LTS; use siempre el nombre de archivo exacto que se descarga de Distribución de software.

## Instalación y actualización {#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

>[!NOTE]
>
> Si está actualizando directamente a LTS SP1 desde SPs antiguos de 6.5, siga las instrucciones que se dan para la [actualización](/help/sites-deploying/upgrade.md) de 6.5 a 6.5 LTS GA.


Para obtener instrucciones detalladas, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Para instalaciones nuevas de AEM 6.5 LTS, las definiciones de índice deben instalarse por separado. Para obtener más información, consulte este [artículo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Instalación y actualización del complemento de Formularios de AEM {#install-update-aem-forms-add-on}

Para obtener instrucciones detalladas, consulte [Realización de una actualización in situ](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions).



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

| Área | Característica | Reemplazo | Versión (SP) |
| --- | --- | --- | --- |
| Sites | [Editor de SPA](/help/sites-developing/spa-overview.md) | Los editores preferidos para administrar el contenido sin encabezado en AEM son: <br> el [Editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.<br>- [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios. | 6.5 LTS GA |

### Funciones eliminadas  {#removed-features}

En esta sección se enumeran las características y funciones que se han eliminado de AEM 6.5 LTS. Las versiones anteriores tenían estas funciones marcadas como en desuso.

| Área | Característica | Reemplazo | Versión (SP) |
| --- | --- | --- | --- |
| Comercio | AEM CIF Classic no es compatible. | Migre a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluciones | Social/Communities no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Screens | Screens no se admiten. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `dam-pim` y `dam-rating` no se admiten porque los paquetes dependen de las redes sociales. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` se ha eliminado. | Utilice la API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` que se ha añadido. | 6.5 LTS GA |
| Portal | AEM Portal Director no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | Se ha eliminado el paquete `com.adobe.granite.socketio`. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` no es compatible.  | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `crx2oak` no es compatible.  | Elija la versión pertinente de [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade). | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` no es compatible.  | No hay sustitución disponible. | 6.5 LTS GA |
| Guava | Todas las dependencias de Guava ahora se eliminan en AEM y, por lo tanto, el paquete `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` no forma parte de AEM. | Los clientes pueden agregar Guava por su cuenta si dependen de Guava o reemplazar el código de Guava con colecciones de Java u otras alternativas si es posible. | 6.5 LTS GA |
| `We.Retail` | El sitio de muestra `We-retail` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | El paquete `oak-solr-osgi` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` y `org.apache.sling.atom.taglib` no son compatibles. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.commons.io` paquetes se han exportado desde `org.apache.commons.commons-io`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | Se están exportando `javax.mail` paquetes desde el paquete `com.sun.javax.mail`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `org.apache.jackrabbit.api` paquetes se han exportado ahora desde el paquete `org.apache.jackrabbit.oak-jackrabbit-api`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `com.github.jknack.handlebars` no es compatible | Elija la [versión](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente. | 6.5 LTS GA |


## Problemas conocidos {#known-issues}

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

<!-- REMOVED THIS SECTION AS PER CQDOC-23046
### Issue with JSP scripting bundle in AEM 6.5.21-6.5.23 and AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23, and AEM 6.5 LTS GA ship with the `org.apache.sling.scripting.jsp:2.6.0` bundle, which contains a known issue. The issue typically occurs under high load when the AEM instance handles many concurrent requests.

When this issue occurs, one of the following exceptions may appear in the error logs alongside references to `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

A hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) is available to resolve this problem. -->

### Error de conexión de Dispatcher con la función solo SSL (corregido en AEM 6.5 LTS SP1 y posterior){#ssl-only-feature}

>[!NOTE]
>
> Este problema solo está presente en la versión de AEM 6.5 LTS GA.

Al habilitar la función Solo SSL en las implementaciones de AEM, existe un problema conocido que afecta a la conectividad entre las instancias de Dispatcher y AEM. Después de habilitar esta función, las comprobaciones de estado pueden fallar y la comunicación entre las instancias de Dispatcher y AEM puede verse interrumpida. Este problema se produce específicamente cuando los clientes intentan conectarse a través de `https + IP` desde Dispatcher a instancias de AEM. Está relacionado con problemas de validación de SNI (Indicación de nombre de servidor).

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

### Página de permisos vacía en la interfaz de usuario de seguridad del SP1 de AEM 6.5 LTS

>[!NOTE]
>
> Este problema solo está presente en la versión AEM 6.5 LTS SP1.

Al acceder a la página Permisos en Herramientas -> Seguridad en AEM 6.5 LTS SP1, proporciona una página en blanco en lugar de mostrar permisos para un usuario o grupo.

**Solución:**
Hay disponible una revisión [cq-6.5.lts.1-hotfix-GRANITE-62993-1.0.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.1-hotfix-GRANITE-62993-1.0.zip) para resolver este problema.


## Paquetes OSGI y paquetes de contenido incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión de [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/es/docs/customer-one/using/home).

