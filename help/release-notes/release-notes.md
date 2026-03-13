---
title: Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP2
description: Busque la información de la versión actual de Adobe Experience Manager 6.5 LTS, Service Pack 2.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 0268920d3c4895a1c52fbc36f537a02d1424c2a4
workflow-type: tm+mt
source-wordcount: '6243'
ht-degree: 20%

---

# Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP2 {#release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versión | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 19 de febrero de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **Revisión obligatoria**: para evitar problemas de SNFE (SegmentNotFoundException) con la compactación sin conexión al instalar el SP2, instale la revisión descrita en [Problemas conocidos: corrupción del repositorio durante la compactación en línea](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146).

## Qué se incluye en [!DNL Adobe Experience Manager] 6.5 LTS, SP2 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP2 incluye nuevas características, mejoras clave solicitadas por los clientes y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde la disponibilidad inicial de 6.5 LTS en marzo de 2025. [Instale este Service Pack](#install-update) en 6.5 LTS.

## Función clave y mejora

**AEM Sites**

AEM 6.5 LTS SP2 ahora incluye OpenAPI para [administración de modelos y fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/) y [lanzamientos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/). Estas API proporcionan acceso a los fragmentos de contenido y a los lanzamientos para la creación y programación. Utilizan las mismas OpenAPI modernas que AEM as a Cloud Service.


<!-- UPDATE THE EACH RELEASE -->

## Se han corregido problemas en 6.5 LTS, Service Pack 2 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### Accesibilidad {#sites-accessibility-65-lts-sp2}

* El componente Texto perdía el enfoque del teclado cuando los autores pasaban el ratón por los elementos del Explorador de componentes durante la edición. Esto interrumpió la escritura y activó un error de accesibilidad en WCAG 3.2.1. La corrección evita que el estilo de desplazamiento desplace el enfoque y mantiene el componente Texto enfocado durante la interacción del Explorador de componentes. (SITES-35370)
* Se ha corregido la administración de enfoque en el campo de texto enriquecido Descripción que bloqueaba la navegación hacia delante con el tabulador. Los usuarios se quedaron atascados en el RTE porque el componente dependía de un comando de teclado no estándar para cambiar el enfoque, lo que rompía la navegación esperada en el cuadro de diálogo. El cambio exige la interacción estándar del teclado y conserva la secuenciación lógica de tabulación en todo el cuadro de diálogo. (SITES-35228)
* Se ha corregido un problema en el editor de sitios que afectaba el comportamiento esperado durante la creación de la página y provocaba una interacción incoherente del componente. Los autores experimentaron respuestas de IU poco fiables que interferían con las tareas de edición estándar y reducían la eficacia del flujo de trabajo. La actualización perfecciona la lógica del editor subyacente y restaura una interacción estable y predecible entre los componentes afectados. (SITES-35227)
* una regresión que rompió el selector de recursos en el editor de páginas e impidió que se cargara en escenarios de edición de páginas específicos. Ahora, los autores pueden abrir y utilizar el selector de recursos con normalidad al elegir o examinar recursos mientras editan una página. Este cambio restablece el acceso coherente a los flujos de trabajo de selección de recursos que interrumpen los errores de carga. (SITES-35226)
* Se ha eliminado un problema en el Editor de sitios que provocaba un comportamiento incoherente durante la interacción de la página e interrumpía los flujos de trabajo de creación estándar. El defecto provocaba respuestas de interfaz de usuario inesperadas que interferían con la configuración del componente y las actualizaciones de contenido. La actualización estabiliza la funcionalidad afectada y restaura la ejecución fiable de las acciones de edición en todas las páginas. (SITES-35225)
* Se ha eliminado un defecto en la interfaz de creación de Sites que provocaba un comportamiento incoherente durante la edición de la página y afectaba a los flujos de trabajo normales. Los autores encontraron respuestas de interfaz de usuario inesperadas que interferían con la interacción de los componentes y las actualizaciones de contenido. La actualización estabiliza la funcionalidad afectada y restaura un comportamiento fiable y predecible en todos los escenarios de edición. (SITES-35224)
* AEM Sites ahora incluye compatibilidad de texto de `alt` en las imágenes para cumplir los requisitos de ADA y WCAG. La salida de página ya no omite los atributos `alt`, por lo que los lectores de pantalla recibirán el texto alternativo correcto. (SITES-27153)
* Se ha corregido el diseño de la barra de herramientas `Note Add` de modo que el botón Agregar ya no se superponga con el título a una anchura de ventanilla de 320 píxeles. Reflow de pantalla pequeña mejorado para que los controles puedan leerse y utilizarse durante el zoom del 400 %. (SITES-25376)
* Se han corregido los anuncios del lector de pantalla que faltaban para los errores del cuadro de diálogo Selección de vínculos. La interfaz de usuario ahora publica el texto de error a través de un contenedor de mensajes de estado, por lo que NVDA lee el mensaje en cuanto aparece. (SITES-25368)
* Se han eliminado los roles de cuadrícula ARIA y celda de cuadrícula de la lista de activos de la barra lateral. Se ha restaurado la semántica de lista estándar y el orden de enfoque de teclado, lo que ha mejorado la navegación del lector de pantalla y reducido las tabulaciones adicionales. (SITES-25361)
* Se ha corregido la secuencia de enfoque en los activos de la barra lateral. Los usuarios del teclado ahora pueden acceder a todas las acciones de recursos, incluida la edición, a través de una ruta de tabulación coherente. (SITES-25360)
* Se ha corregido el desbordamiento de diseño en el modo Buscar activos con una anchura de ventanilla de 320 px. El contenido modal ahora se reorganiza y se mantiene legible, por lo que los controles ya no se superponen ni se desbordan en el cuadro de diálogo. (SITES-25330)
* Salida NVDA corregida para el botón Editar. Ahora, NVDA anuncia la acción Editar, no &quot;Previsualizar botón pulsado&quot;. (SITES-25320)
* Se corrigieron entradas de texto de la barra de herramientas Demográficas sin nombre que provocaban una salida de lector de pantalla silenciosa o genérica. Cada entrada ahora expone un nombre accesible claro basado en etiquetas, que mejora el teclado y la navegación con tecnología de asistencia. (SITES-25316)
* Se ha corregido el orden de enfoque del teclado de la barra de herramientas Demográfica durante la navegación de previsualización de maquetación. La navegación por pestañas ahora se mueve directamente desde el botón Demográfico a los controles de la barra de herramientas, sin pasar a la barra de herramientas secundaria. (SITES-25305)
* Se ha corregido el orden de anuncio incorrecto de las etiquetas &quot;Pantallas más pequeñas&quot; y &quot;Tablet&quot; en la regla Editar diseño. Los lectores de pantalla ahora anuncian estas etiquetas en los marcadores de regla correctos, que coinciden con el diseño de página. (SITES-25291)
* Se ha corregido el desbordamiento de la barra de herramientas Editar diseño con un zoom del 200 %. El contenido ahora permanece dentro de la ventanilla móvil y permanece accesible mediante el desplazamiento. (SITES-25288)
* Se ha resuelto un orden de enfoque incorrecto en la superposición Anotaciones. La tabulación de teclado ahora recorre los controles de superposición y los elementos de anotación. La página principal ya no se centra desde detrás de la superposición. (SITES-25282)
* Muestras fijas en el control de enfoque. El cuadro de diálogo ahora mueve el enfoque a un encabezado claro e inicia la salida del lector de pantalla en ese punto de entrada. NVDA ya no lee el contenido completo del cuadro de diálogo fuera de la secuencia. (SITES-25275)
* Se ha corregido el control de enfoque modal de Deformación de tiempo después de cerrar el Selector de fecha. `Escape` ahora devuelve el foco al botón Selector de fecha. La selección de fecha ahora coloca el foco en el campo de entrada situado junto al control Selector de fecha, lo que evita la pérdida del foco y el acceso a la página en segundo plano. (SITES-25264)
* Se ha corregido el control de enfoque del teclado para el cuadro de diálogo Eliminar anotación. Cancelar ahora devuelve el foco al control `Delete` que abrió el cuadro de diálogo, no al control de valor hexadecimal Confirm. Los lectores de pantalla ya no anuncian el contenido de cuadros de diálogo no relacionados después de Cancelar. (SITES-25258)
* Tratamiento de enfoque fijo para el cuadro de diálogo modal Anotación. Al abrir el cuadro de diálogo, ahora se establece el enfoque en el encabezado del cuadro de diálogo y se impide que NVDA lea contenido de lienzo y texto de cuadro de diálogo no relacionado. La navegación con teclado ahora permanece dentro del cuadro de diálogo hasta que se cierra. (SITES-25257)
* Se han corregido problemas de diseño modal de búsqueda con una anchura de 320 px. El contenido modal ahora se reorganiza de forma limpia y evita la superposición con el directorio de árbol. Los usuarios pueden ver los resultados y navegar por el directorio sin controles ocultos. (SITES-25246)
* El texto modal de búsqueda ya no recorta después de aumentar el espaciado del texto. El diseño del directorio de árbol ahora mantiene una separación clara, por lo que las etiquetas y las entradas se pueden leer. Ahora los usuarios pueden completar la búsqueda y la navegación sin superposición ni texto cortado. (SITES-25245)
* Al activar Anotar, ahora se mueve el foco del teclado al contenido de la anotación, no al botón Salir de anotación. El orden de tabulación sigue una secuencia lógica y mantiene accesibles los controles relacionados sin navegación inversa. (SITES-25241)
* A los vínculos Configurar fecha y Deformación de tiempo de salida les faltaba un indicador de enfoque visible durante la navegación con teclado. La interfaz de usuario ahora representa un estilo de enfoque distinto y de alto contraste para que los usuarios puedan identificar el vínculo activo de un vistazo. (SITES-25232)
* El encabezado Teaser Modal ya no impide que los usuarios del teclado muevan el cuadro de diálogo. Los controles de teclado ahora permiten las acciones de recoger, mover y soltar, lo que mejora la facilidad de uso del lector de pantalla y la operabilidad general. (SITES-25226)
* AEM ahora utiliza una etiqueta accesible significativa para el botón Información modal del teaser. Los lectores de pantalla anuncian un nombre de acción claro en lugar del icono predeterminado cadena de texto alternativo. (SITES-25223)
* Los lectores de pantalla anuncian ahora la acción correcta cuando los usuarios activan el botón Editar. NVDA ya no informa &quot;Botón de previsualización presionado&quot;, lo que provocó comentarios engañosos y confusión durante la navegación mediante el teclado. (SITES-25208)
* Al expandir el carril izquierdo, ahora se mueve el foco del teclado al primer control del carril izquierdo. La secuencia Tab ya no salta a la barra de herramientas secundaria o llega a la lista intermedia, por lo que los usuarios del teclado pueden alcanzar el contenido de la línea izquierda sin navegación inversa. (SITES-24998)
* El contenido de la barra de emulador de dispositivos ahora permanece totalmente visible a 320 px de ancho de puerto de visualización. El texto de la barra de herramientas y los controles se ajustan en lugar de truncar, reduciendo la superposición y mejorando la legibilidad. (SITES-24953)
* AEM ahora muestra la etiqueta de dispositivo iPhone completa en la barra de herramientas del emulador. El texto ya no se trunca con la anchura predeterminada, lo que mejora la legibilidad y la claridad de selección del dispositivo. (SITES-24952)
* Los encabezados de tabla de Vista de lista ahora exponen el estado de ordenación a través de ARIA. Los lectores de pantalla anuncian el orden ascendente o descendente después de una acción de ordenación de columnas. (SITES-24943)
* AEM ahora conserva la visibilidad de la etiqueta del menú Más acciones en la Vista de tarjetas durante los cambios de espaciado del texto. Las opciones del menú mantienen el texto completo, incluida la Publicación rápida, y el menú permanece legible durante cualquier configuración de espaciado de texto WCAG. (SITES-24941)
* La barra de menús Acciones de tarjeta ahora muestra un nombre accesible en la Vista de tarjetas. Los lectores de pantalla anuncian claramente el propósito de la barra de menús y el control por voz puede dirigirse al control por nombre. (SITES-24938)
* La vista de tarjeta ya no depende de la semántica de cuadrícula ARIA que causó un comportamiento confuso del lector de pantalla. La interfaz de usuario ahora proporciona funciones y etiquetas significativas para el contenido de la tarjeta y la barra de acciones de la tarjeta, lo que reduce los controles perdidos durante el uso del teclado. (SITES-24933)
* La información sobre herramientas de `Delete Modal` aparece ahora cada vez que los usuarios colocan el puntero sobre el icono de información sobre herramientas. Las acciones de enfoque ahora muestran el mismo texto de información del objeto, lo que mejora el acceso repetido para los usuarios de ratón y teclado. (SITES-24778)
* La navegación del carril izquierdo ahora sigue el orden de enfoque de teclado esperado después de que los usuarios configuren el carril. El enfoque de tabulación aterriza en el área del carril izquierdo seleccionada en lugar de Cambiar pantalla, lo que mejora la claridad de navegación del lector de pantalla. (SITES-24754)
* Se han corregido los comentarios incorrectos del NVDA durante la navegación por muestras de color en el modo Preferencias de usuario. Ahora, el NVDA lee la etiqueta de la muestra que recibe el foco, lo que elimina la salida de color engañosa. El conjunto de muestras ahora admite una navegación de teclado coherente y un conocimiento claro de la selección. (SITES-24739)
* Resultado NVDA detallado reducido para el control `Spin`. Se ha eliminado el etiquetado de grupo redundante que duplicaba la etiqueta de entrada, por lo que NVDA anuncia el nombre del control una vez. El teclado y la navegación del lector de pantalla ahora ofrecen un único anuncio claro. (SITES-24725)
* El cuadro de diálogo Carrusel ahora coloca el foco en el encabezado del cuadro de diálogo en lugar de en la ficha Elementos. Cancel y Esc restauran el foco al control que inició el cuadro de diálogo, lo que reduce la salida de NVDA detallada. (SITES-24716)
* El cuadro de diálogo de selección de vínculos ahora alinea la etiqueta programática con la etiqueta en pantalla para los elementos del árbol de último nivel. Los déclencheur de navegación con teclas de flecha proporcionan un anuncio fiable para cada elemento y eliminan la salida de etiquetas engañosas. (SITES-24710)
* El cuadro de diálogo Vincular selección abierta ahora se reorganiza correctamente en una ventana gráfica de 320 px. El contenido ya no se excede en el modal ni se trunca, y el modal ya no muestra una barra de desplazamiento horizontal. (SITES-24709)
* El cuadro de diálogo Vincular selección abierta ahora restaura el foco del teclado al activador del cuadro de diálogo después de Cerrar o Cancelar. El enfoque ya no salta a la entrada Link, lo que mantiene estable el contexto del lector de pantalla y reduce la navegación adicional. (SITES-24707)
* El cuadro de diálogo modal de imagen ahora sigue una secuencia de enfoque lógico. El enfoque ya no omite los controles anteriores ni suelta el marcador de posición de la página después de Cancelar y los usuarios vuelven a centrarse en el botón Configurar después de salir. (SITES-24693)
* El cuadro de diálogo modal Carril de referencias ahora intercepta el foco del teclado. Tab y Mayús+Tab permanecen dentro de los controles del cuadro de diálogo y el enfoque ya no se escapa al contenido de la página. Los lectores de pantalla solo anuncian el contenido del cuadro de diálogo. (SITES-24683)
* El modo Selección de ruta de hipervínculo ahora establece el foco en el encabezado del cuadro de diálogo al abrir. Cancelar cierra el cuadro de diálogo y restaura el foco en el botón Abrir cuadro de diálogo de selección, lo que evita la pérdida de foco y la salida redundante del lector de pantalla. (SITES-24672)
* El campo de búsqueda utiliza ahora una etiqueta persistente en pantalla en lugar de texto falso. La etiqueta permanece visible durante la entrada, lo que mejora la claridad para los usuarios de teclado, lector de pantalla y voz. (SITES-24529)
* El cuadro de diálogo modal de borrador ahora establece el foco en el encabezado del cuadro de diálogo al abrirlo. Al cerrar el cuadro de diálogo, se devuelve el enfoque al control `Configure`, lo que evita la pérdida de enfoque y el exceso de resultados del lector de pantalla. (SITES-24522)
* El panel Assets del raíl lateral ahora incluye un control Cerrar. Cerrar devuelve el foco del teclado al conmutador Carril lateral y evita la tabulación forzada en el contenido del panel. (SITES-24489)
* La tabulación de teclado ahora alcanza los botones y vínculos dentro de las tablas de administración. Los usuarios ya no dependen de la navegación con teclas de dirección para encontrar los controles interactivos. (SITES-24285)
* El cuadro de diálogo Componente de imagen ya no muestra los iconos de Ayuda decorativa y Pantalla completa como imágenes. Los lectores de pantalla ahora omiten estos iconos, manteniendo el enfoque en los controles procesables y el contenido de campo. (SITES-2940)
* El administrador de sitios ahora elimina la función de imagen de los iconos de miniatura de la carpeta. La tecnología de asistencia omite estos elementos decorativos y mantiene el enfoque en los nombres y las acciones de las carpetas. (SITES-2852)
* El árbol de contenido ahora enruta el foco del teclado al elemento de árbol activo o al primer elemento de árbol. El contenedor de árbol ya no actúa como una tabulación vacía, lo que evita que Mayús + Tabulación revente el enfoque. (SITES-1577)

#### Interfaz de usuario administrador{#sites-adminui-65-lts-sp2}

La configuración de la vista de lista de la consola Sitios no reflejaba las columnas mostradas en la vista de lista. El cuadro de diálogo se abrió con casillas de verificación desactivadas y un recuento incorrecto de columnas seleccionadas. El estado del cuadro de diálogo Corregir sincroniza con las columnas de la cuadrícula activa y actualiza el contador para que coincida con la visibilidad real de las columnas. (SITES-38576)

#### Interfaz de usuario clásica{#sites-classicui-65-lts-sp2}

La edición de componentes de texto de la IU clásica mostraba etiquetas de HTML sin procesar en lugar de texto enriquecido después de una actualización. Service Pack 2 corrige el procesamiento RTE (Editor de texto enriquecido) de la IU clásica para que el editor muestre el contenido con formato y conserve el marcado almacenado. La corrección también detiene la expansión del marcado durante las ediciones y los guardados repetidos. (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

El soporte para eventos sin cabeza carecía de eventos OSGi requeridos para fragmentos de contenido y modelos en 6.5 LTS. La actualización agrega el paquete de eventos más las dependencias requeridas e incluye una versión 6.5 LTS. Los eventos Fragmento de contenido y Modelo ahora se activan correctamente y admiten inicia flujos de trabajo de API. (SITES-35329)

#### [!DNL Content Fragments]: administración{#sites-admin-65-lts-sp2}

* El control de componentes ajustado en la interfaz de creación de sitios para detener el comportamiento irregular durante las actualizaciones de página. El defecto llevó a respuestas impredecibles del editor que interfirieron con las modificaciones rutinarias del contenido y redujeron la eficiencia del flujo de trabajo. La actualización alinea la lógica del editor con los patrones de interacción esperados y ofrece un rendimiento fiable durante las actividades de creación. (SITES-35078) CRÍTICO

* Una regresión interrumpió la vista de lista de la consola de Assets para los fragmentos de contenido y activó un error durante la representación de la lista. La actualización corrige la lógica de vista de lista después de la eliminación de información de previsualización y restaura una salida de lista estable. La consola ahora muestra los fragmentos de contenido sin errores y mantiene las interacciones de lista utilizables. (SITES-38683)
* El Editor de fragmentos de contenido ahora localiza la etiqueta Etiquetas. El editor también localiza la etiqueta Colecciones, de modo que el texto de la interfaz de usuario coincide con la configuración regional seleccionada. (SITES-977)


#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-65-lts-sp2}

* Las etiquetas de variación de fragmentos de contenido desaparecían cuando el botón deslizante de la función permanecía desactivado tras la refactorización. La corrección restaura la compatibilidad con la etiqueta de variación incluso cuando el conmutador permanece desactivado. Los autores pueden añadir y ver de nuevo las etiquetas de variación en el Editor de fragmentos de contenido. (SITES-38682) CRÍTICO
* Los fragmentos de contenido editados desaparecieron de la lista de la consola de Assets después de que los autores regresaran del Editor de fragmentos de contenido. El almacenamiento en caché del explorador devolvió una lista obsoleta y ocultó el fragmento actualizado hasta una actualización manual. La corrección agrega control de caché para la ruta de retorno del editor, de modo que la lista se vuelva a cargar correctamente y se mantenga visible el fragmento editado. (SITES-35374) CRÍTICO

* El RTE de fragmento de contenido mostraba problemas visuales y de diseño después de cambios recientes en el estilo de la interfaz de usuario. Service Pack 2 mejora el estilo RTE para que la barra de herramientas y el área editable se representen correctamente y sean legibles. El Editor de fragmentos de contenido ahora se alinea con la apariencia y el comportamiento del Editor de páginas. (SITES-38684)
* Al quitar ámbitos de IMS del selector de recursos Polaris, se rompió la integración de fragmentos de contenido con el punto final de entrega. Los autores obtienen errores al abrir el selector de recursos remoto y seleccionar recursos. La actualización vuelve a agregar los ámbitos de IMS necesarios y restaura el acceso estable en el nivel de entrega. (SITES-35837)
* El panel Contenido asociado ya no representa un marcador de posición &quot;indefinido&quot; codificado. El Editor de fragmentos de contenido ahora resuelve ese texto mediante recursos de localización, de modo que los editores ven el texto de la interfaz de usuario traducido. (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* El Editor de fragmentos de contenido ahora muestra una etiqueta de pestaña General traducida en todas las configuraciones regionales. El editor reemplaza el texto de tabulación no localizado y elimina los identificadores internos de los títulos de tabulación. (SITES-30715)
* El Editor de fragmentos de contenido ahora muestra los nombres traducidos para los tipos de recursos permitidos. La lista de selección ya no combina cadenas internas y etiquetas de solo inglés cuando los autores configuran restricciones de referencia de contenido. (SITES-29699)

#### [!DNL Content Fragments]: API GraphQL {#sites-graphql-api-65-lts-sp2}

* Control perfeccionado de la validación de consultas de GraphQL para detener los errores de implementación causados por errores de ejecución de filtros. El defecto generó excepciones durante el inicio de la aplicación y bloqueó el despliegue correcto en los entornos afectados. La revisión garantiza un comportamiento de validación coherente y permite una implementación fluida sin interrupciones de validación de consultas en tiempo de ejecución. (SITES-34301) CRÍTICO

* El cuadro de diálogo Editar extremo de GraphQL ahora muestra cadenas de IU traducidas. El cuadro de diálogo ya no muestra texto solo en inglés como &quot;GraphQL schema is take from configuration&quot; (El esquema de se toma de la configuración) y las etiquetas relacionadas se procesan correctamente en las configuraciones regionales. (SITES-34018)

#### [!DNL Content Fragments] - Editor de consultas de GraphQL{#sites-graphql-query-editor-65-lts-sp2}

* Se ha refinado el control de validación de consultas de GraphQL para detener los errores de implementación causados por errores de ejecución de filtros. El defecto generaba excepciones durante el inicio de la aplicación y bloqueaba el despliegue correcto en los entornos afectados. La revisión garantiza un comportamiento de validación coherente y permite una implementación sin problemas sin interrupciones de validación de consultas en tiempo de ejecución. (SITES-35529)
* El Explorador de GraphQL ya no falla cuando un nombre de Explorador de configuración contiene caracteres CJK. La creación de extremos y el acceso a consultas guardadas funcionan normalmente y la página del Editor de consultas de GraphQL permanece sin errores. (SITES-31616)

#### [!DNL Content Fragments] - Editor de modelo{#sites-model-editor-65-lts-sp2}

* Los modelos de fragmento de contenido anidado dejaron de funcionar al refactorizar la función vinculada a una opción deshabilitada. La corrección restaura la compatibilidad con modelos anidados sin requerir cambios de alternancia. Los autores pueden volver a crear y utilizar modelos anidados en el Editor de modelos. (SITES-38681) CRÍTICO

* El panel de filtro de modelos de fragmento de contenido ya no muestra cadenas no localizadas. AEM muestra ahora etiquetas de filtro localizadas y valores de estado localizados en todas las configuraciones regionales. (SITES-30863)
* El Editor del modelo de fragmentos de contenido ahora procesa cadenas localizadas para el cuadro de diálogo de advertencia de bloqueo. La IU reemplaza los mensajes en inglés no localizados con recursos de configuración regional en todos los idiomas admitidos. (SITES-28592)

#### [!DNL Content Fragments]: API REST{#sites-restapi-65-lts-sp2}

AEM Headless necesitaba una rama de versión dedicada para evitar la dependencia y los conflictos de versión del paquete con las compilaciones de línea principal. La actualización añade una rama sin encabezado versión/6.5lts y alinea los conjuntos de dependencias y las versiones de paquetes. Jenkins ahora construye la base de código sin encabezado de forma limpia sin conflictos de versiones. (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### API de contenido{#sites-content-api-65-lts-sp2}

Error al informar del estado de la API de administración de páginas al cambiar entre funciones. La actualización agrega un indicador de habilitación dedicado y lo evalúa junto con la opción existente. La API de administración de páginas ahora muestra el estado estable. La API de administración del sitio sigue siendo experimental. (SITES-39284)

#### Back-end principal{#sites-core-backend-65-lts-sp2}

* Cambio en la experiencia de creación de sitios para resolver comportamientos incoherentes que interrumpen los flujos de trabajo de edición de páginas estándar. Los autores encontraron resultados inesperados durante la interacción de los componentes, lo que interfirió con las actualizaciones de contenido y redujo la confiabilidad. El cambio restaura el comportamiento estable del editor y garantiza la ejecución coherente de las acciones de creación en los escenarios afectados. (SITES-35162) CRÍTICO

* Comportamiento de creación de sitios refinado para resolver un problema que perturbaba la edición de la página y provocaba resultados incoherentes durante la interacción del componente. Los autores experimentaron respuestas de interfaz de usuario inesperadas que interferían con las actualizaciones de contenido y reducían la fiabilidad del flujo de trabajo. El cambio restaura la administración estable del estado del editor y garantiza la ejecución predecible de las acciones de creación en los escenarios afectados. (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### Lanzamientos{#sites-launches-65-lts-sp2}

* La línea de tiempo de sitios mostró texto en inglés codificado durante la promoción de lanzamiento: &quot;Versión creada ... antes de promocionar el lanzamiento&quot;. La actualización reemplaza la cadena codificada por un control de mensajes localizado. La línea de tiempo ahora muestra texto localizado y alinea la entrada con el comportamiento de localización estándar de AEM. (SITES-39157)
* El ámbito de promoción de lanzamiento se desvió cuando los autores promovieron una subsección mediante la promoción de páginas y subpáginas actuales. AEM también promovió páginas no relacionadas y causó modificaciones inesperadas en el sitio. La corrección corrige el cálculo del ámbito de lanzamiento, de modo que sólo el subárbol elegido promueva. (SITES-38315)
* Los fragmentos de contenido dentro de los lanzamientos no participaron en el índice `damAssetLucene` y los resultados de búsqueda limitados y la eficiencia de la consulta. Este cambio añade las rutas de fragmentos de contenido de Launch a la definición del índice. Las consultas personalizadas y de búsqueda ahora encuentran fragmentos de contenido en `/content/launches`. (SITES-35634)
* La interfaz de usuario Lanzamientos mostraba controles de Lanzamiento de fragmentos de contenido aunque el producto no exponga Lanzamientos de fragmentos de contenido en la IU táctil. Este cambio elimina las rutas de código de Launch de los fragmentos de contenido de cq-launches-content y ajusta el filtrado de listas de Launch. Los autores ahora ven opciones de Launch de página coherentes sin entradas de Launch de fragmentos de contenido. (SITES-35633)
* AEM 6.5 LTS Quickstart carecía de paquetes y requisitos previos de Launch requeridos, que bloqueaban la habilitación de OpenAPI de Launch. La actualización añade paquetes de inicio y dependencias necesarias, como soporte de métricas, actualizaciones de DAM-cfm y configuración de colas. Inicia las API que ahora se ejecutan en 6.5 LTS Quickstart con los componentes de tiempo de ejecución necesarios presentes. (SITES-35297)
* CF Lanza empaquetado extrae nuevas versiones de dependencias y bibliotecas de GraphQL innecesarias, lo que complica AEM integración 6.5 LTS. Este cambio alinea las versiones de dependencia con la línea de base de AEM 6.5 LTS y elimina las dependencias de GraphQL no utilizadas. La resolución del paquete ahora permanece coherente y el inicio de los lanzamientos de CF permanece estable. (SITES-35295)
* AEM Launches ahora ejecuta una canalización Jenkins dedicada para la rama 6.5 LTS. La canalización se ejecuta todas las noches y genera y envía alertas de error por correo electrónico. Esta configuración aumenta la cobertura de las pruebas y detecta las regresiones antes de tiempo. (SITES-35293)
* AEM 6.5 LTS ahora envía un paquete de API de Launch actualizado con versiones de artefactos alineadas. El paquete rastrea la línea de código principal mientras mantiene la versión correcta de la versión 6.5 LTS. Esta actualización estabiliza el consumo de la API de lanzamientos en la pila de 6.5 LTS. (SITES-35292)
* AEM 6.5 LTS ahora incluye un paquete de lanzamientos-core actualizado con versiones de dependencia alineadas. La actualización añade el control de inicio de núcleo para los tipos de datos UUID de fragmento y UUID de referencia. El procesamiento de inicio ahora mantiene un comportamiento uniforme en los flujos de trabajo de inicios y fragmentos de contenido. (SITES-35290)
* Se ha perfeccionado el editor de sitios para resolver comportamientos incoherentes que interrumpían los flujos de trabajo normales de creación de páginas. Los autores encontraron interacciones de componentes inesperadas que interferían con las actualizaciones de contenido y reducían la fiabilidad de la edición. El cambio restaura la administración coherente del estado de la interfaz de usuario y garantiza la ejecución predecible de las acciones de creación en los escenarios afectados. (SITES-35138)
* Inicia Editar ahora muestra texto de error localizado en lugar de la cadena codificada `Provided path is not a launch`. La interfaz de usuario ahora procesa los mensajes traducidos en varios idiomas cuando Edit recibe una ruta de inicio no válida. (SITES-33360)
* AEM 6.5 LTS ahora incluye el trabajo de puerto lateral de Launch OpenAPI. La actualización pone en paridad los paquetes de API de lanzamientos, los paquetes de contenido y los artefactos de inicio rápido necesarios, y habilita los escenarios de API abierta de lanzamientos de fragmentos de contenido con validación de CI estable. (SITES-32050)
* La interfaz de usuario de Lanzamientos ahora localiza la etiqueta de plantilla Anulada. Los detalles de anulación de plantilla ahora muestran el texto traducido en lugar de una cadena solo en inglés. (SITES-29525)
* AEM ha resuelto la clave de localización que faltaba en **Sitios** > **Inicios** > **Editar**. Los usuarios ahora ven un mensaje de error traducido en lugar de la cadena sin procesar &quot;No se puede actualizar la lista de fuentes de lanzamiento&quot;. (SITES-21499)
* La interfaz de usuario de lanzamiento de promoción ahora muestra etiquetas de estado y acciones localizadas. El área de vista previa muestra texto traducido para **Eliminado**, **Nuevo** y **Ver**, en lugar de cadenas en inglés sin formato. (SITES-13540)
* La creación de Launch ahora muestra mensajes de error localizados. La interfaz de usuario ya no muestra cadenas en inglés sin procesar como `Unable to create launch page`, `Source root resource is not a page` o `Mandatory parameter is missing`. (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM: Live Copy{#sites-msm-live-copies-65-lts-sp2}

* Los administradores tenían una visibilidad limitada del procesamiento push-on-modify de MSM durante los cambios de contenido. La corrección agrega un registro detallado de la recepción de eventos MSM y la ejecución del despliegue. El resultado de la depuración ahora muestra qué eventos se activaron, qué rutas de contenido cambiaron y quién activó el cambio. (SITES-38029)
* AEM solucionado un problema de diseño de localización en el campo de fecha Despliegue del modelo. El mensaje de fecha ahora se ajusta al control y se puede leer en todos los idiomas admitidos, incluido `fr_FR`. (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### Replicación{#sites-replication-65-lts-sp2}

La publicación del Editor de páginas ahora gestiona las direcciones URL que contienen selectores o sufijos. La solicitud publicada ahora envía la ruta de la página JCR, no un selector o una cadena de URL de sufijo, por lo que la activación se completa y el contenido se activa. La replicación ahora devuelve un estado de error en caso de error, lo que evita los mensajes falsos de &quot;inicio de la publicación&quot;. (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### Editor de plantillas{#sites-template-editor-65-lts-sp2}

El texto de estado de la plantilla se muestra verticalmente en **Herramientas** > **General** > **Plantillas** para algunas configuraciones regionales. La etiqueta &quot;obsoleta&quot; rompió el diseño y se leyó como una columna de caracteres. La corrección corrige el estilo del estado de la plantilla de modo que la etiqueta se procese en una sola línea horizontal. (SITES-36797)

#### Editor universal {#sites-universal-editor-65-lts-sp2}

* Se estableció una configuración predeterminada de OSGi como `preview=true` y se forzó el inicio del Editor universal en el modo de vista previa. Esta actualización corrige el valor predeterminado y restaura el comportamiento de entrada de producción estándar. El Editor Universal se abre ahora en modo Producción a menos que un administrador habilite explícitamente el modo Vista previa. (SITES-37193)
* El comando Abrir editor universal ahora tiene como valor predeterminado el modo de vista previa en los entornos de desarrollo y escenario. El comando agrega preview=true, que mantiene las comprobaciones de autor alineadas con el contexto de previsualización y evita que se abra la producción de forma accidental. (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Ahora, la opción Relacionar activos funciona con nombres de archivo que incluyen espacios. La lógica del cliente Relate actualizada ahora gestiona correctamente las rutas que contienen espacio y evita `undefined` errores de origen durante la selección de relaciones. El cuadro de diálogo Relacionar ahora se abre y guarda las relaciones sin bloqueos de interfaz de usuario ni giros. Los usuarios de DAM pueden relacionar, derivar y desrelacionar activos sin cambiar el nombre de los archivos. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* Nueva integración del reproductor de vídeo Dynamic Media (implementación limitada): Una nueva experiencia del reproductor de vídeo Dynamic Media ya está disponible en Quickstart de AEM 6.6. Actualmente, esta mejora solo está habilitada para clientes iniciales como parte de un despliegue controlado. (ASSETS-60165)
* Se ha resuelto un problema en el cual la opción Seleccionar miniatura del cuadro de diálogo de propiedades de vídeo no abría el selector de recursos, lo que restauraba la capacidad de los usuarios de elegir miniaturas personalizadas para los recursos de vídeo. (Activo-58926)
* En el video de Dynamic Media, se agregó soporte para seleccionar árabe en la lista desplegable Idioma de Subtítulos y pistas de audio, permitiendo a los autores administrar subtítulos en árabe directamente en AEM. (Assets-61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->


<!--
### [!DNL Forms]{#forms-65-lts-sp2}

#### Forms Designer

#### Forms

#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### Foundation {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* La seguridad de acceso a recursos de Sling ahora se ejecuta en la versión 1.1.2. ResourceAccessSecurityImpl ya no produce una ClassCastException durante la inicialización cuando se registran varios servicios ResourceAccessGateHandler. La inicialización se completa ahora de forma fiable y evita los errores de inicio en entornos con varios controladores. (NPR-42750)
* La consola JMX y la consola web ahora envían un `Content-Type: text/css header` para los recursos CSS de la consola. La comprobación MIME estricta ya no bloquea la carga de la hoja de estilos, por lo que la IU `/system/console/jmx` se procesa con un estilo normal. (GRANITE-63677)
* AEM ahora evita entradas ACL duplicadas para el grupo `contributor` en el `WEB-INF/resources/provisioning/model.txt` generado. La salida WAR ahora contiene un bloque ACL coherente, que evita confundir las diferencias de permisos durante la revisión. (GRANITE-63269)
* AEM borra la configuración de la lista de bloques y de la lista de permitidos del Firewall de deserialización durante las operaciones de actualización de paquetes. La lógica de registro de filtros actualizada mantiene la instancia del firewall activo alineada con la configuración guardada, por lo que la protección permanece habilitada sin reiniciar. (GRANITE-61382)
* Felix Web Console ya no emite `NullPointerException` errores intermitentes durante el acceso a `/system/console`. El control actualizado de ServiceTracker evita un estado de rastreador nulo. El inicio de sesión y la navegación en la consola permanecen estables durante las solicitudes repetidas y la validación automatizada. (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

CRXDE Lite ya no muestra una pestaña en blanco al abrir un archivo JSP después de una actualización del Service Pack. AEM envía ahora código básico y de complemento de CodeMirror coincidentes, lo que evita el error fatal del explorador y mantiene el editor utilizable. (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

El validador de seguridad de expresión ahora administra valores de configuración OSGi vacíos o nulos. Aplica valores predeterminados seguros, omite matrices vacías y registra registros de borrado, lo que evita NullPointerException y resultados de validación impredecibles. (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### Integraciones{#foundation-integrations-65-lts-sp2}

AEM sincroniza las actividades de Adobe Target incluso cuando existen fechas de inicio y finalización. La carga útil de Target ahora formatea las fechas de actividad como marcas de tiempo completas ISO 8601, incluidos segundos, milisegundos y zona horaria. El destino ya no rechaza la solicitud con `InvalidJson.Json`. Las actividades programadas ahora pasan a un estado sincronizado en lugar de permanecer sin sincronizar. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 



#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM Service Pack 2 de 6.5 LTS requiere el conector S3 1.60.10 o posterior. La configuración del almacén de datos de S3 ahora incluye `crossRegionAccess` y `mode`, de modo que los administradores pueden habilitar el acceso de bloque entre regiones y cambiar el almacenamiento a GCP cuando sea necesario. El `s3EndPoint` espera ahora una región alineada con `s3Region` o permanece vacía para que el controlador genere el extremo. (GRANITE-64873)


#### Guía de inicio rápido{#foundation-quickstart-65-lts-sp2}

* Sling actualiza la lista de permitidos de inicio de sesión administrativo para utilizar una terminología inclusiva y nuevos PID de configuración. Este cambio se ajusta a Sling JCR Base 3.2.0. (GRANITE-63756)

  **Impacto**

   * Sling deja en desuso estos PID y debe eliminarlos de sus configuraciones:
      * PID de fábrica: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * PID global: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
Estas configuraciones antiguas utilizan propiedades como `whitelist.name` y `whitelist.bundles`.

   * Sling sigue proporcionando compatibilidad con versiones anteriores parciales para los PID obsoletos, pero no los utiliza para nuevas configuraciones. En su lugar, utilice los `LoginAdminAllowList.*` PID más recientes.
   * No ejecute configuraciones de lista de permitidos obsoletas y nuevas al mismo tiempo. Las configuraciones mixtas pueden crear ambigüedad y producir un comportamiento no deseado. Cuando migre a AEM 6.5 LTS SP2, elimine por completo los PID obsoletos.

  **Lo que debe hacer**

   1. Busque configuraciones de lista de permitidos que utilicen `LoginAdminWhitelist*` PID.
   1. Sustitúyalos por los nuevos PID apropiados:

      * PID de fábrica: `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * PID global: `org.apache.sling.jcr.base.LoginAdminAllowList`

      Para obtener más información, consulte [Enfoque obsoleto de los paquetes de lista de permitidos para el inicio de sesión administrativo](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login).

* AEM 6.5 LTS SP2 actualiza el paquete de capas base establecido para Sling, Oak y Felix. Estas actualizaciones refuerzan la estabilidad del tiempo de ejecución principal y alinean las versiones de dependencia en toda la plataforma. (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311) -->

#### Sling{#foundation-sling-65-lts-sp2}

AEM ahora incluye Sling Engine 2.16.6. Este cambio elimina las infracciones XSS marcadas por las herramientas de seguridad y mejora la seguridad y estabilidad del procesamiento principal. (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

AEM Translations ya no falla en Java 17 o Java 21 debido a problemas de formato XLIFF. La canalización de exportación ahora produce XLIFF compatible con estándares que los proveedores de traducción aceptan. Este cambio elimina las interrupciones del trabajo de traducción y restaura el traspaso predecible entre AEM y los servicios de traducción. Los flujos de trabajo de traducción ahora permanecen estables en los tiempos de ejecución de Java compatibles. (CQ-4360217)

#### Flujo de trabajo{#foundation-workflow-65-lts-sp2}

EmailNotificationService-Processor ya no activa repetidos errores de tipo &quot;Segmento no encontrado&quot; durante la gestión de notificaciones del flujo de trabajo. El control de excepciones actualizado detecta SegmentNotFoundException y detiene el bucle de procesamiento en lugar de continuar con lecturas no válidas. La ejecución del flujo de trabajo permanece estable y el ruido de registro disminuye durante el acceso a la bandeja de entrada y al elemento de trabajo. (GRANITE-62635)




## Acerca de [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 LTS se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x se utiliza como motor servlet para Quickstart.

### Compatibilidad con Java™  {#java-support}

* Compatibilidad con Java™ 17 y Java™ 21.
* Para obtener un rendimiento óptimo, reemplace los valores predeterminados de GC por otros valores. Para obtener más información, consulte la sección [Instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye actualizaciones de mantenimiento de Java™ 17 y Java™ 21 para que las utilicen los clientes en proyectos relacionados con AEM cuando no están disponibles para el público desde Oracle.

### Empaquetado de Uberjar {#uber-jar-packaging}

UberJar para AEM 6.5 LTS SP2 utiliza la versión 6.6.0 de AEM 6.5 LTS UberJar. Puede recuperar los artefactos UberJar correspondientes del repositorio central de Maven. A diferencia de AEM 6.5, AEM 6.5 LTS separa las API públicas y las API obsoletas en dos artefactos diferentes.

Para compilar con las API públicas, utilice lo siguiente:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

Si su código también depende de API obsoletas, agregue lo siguiente:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

Consulte también [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Actualizar {#upgrade}

* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).
* Para obtener instrucciones detalladas sobre la actualización, consulte la [Guía de actualización de AEM Forms 6.5 LTS SP1 en JEE](https://experienceleague.adobe.com/es/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### Prácticas recomendadas para las actualizaciones del Service Pack de AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**Entorno**
Se aplica a: AEM 6.5 LTS (local) clientes que instalen Service Pack 2 (SP2). El SP2 se entrega como un JAR de inicio rápido.

**Por qué es importante**
SP2 para AEM 6.5 LTS se envía como un JAR de inicio rápido en lugar de un ZIP para instalar a través del Administrador de paquetes. Los clientes locales se actualizan reemplazando el JAR de Quickstart, descomprimiéndolo y reiniciándolo. Este método es coherente con el procedimiento de actualización in situ de Adobe.

**Flujo de actualización recomendado (autor o publicación)**

1. Compruebe que la instancia de AEM 6.5 LTS está sana y es accesible.
1. Descargue Quickstart JAR (por ejemplo, `cq-quickstart-6.6.x.jar`) desde Distribución de software.
1. Detenga la instancia en ejecución.
1. En el directorio de instalación de AEM (fuera de `crx-quickstart/`), reemplace el JAR de inicio rápido anterior por el JAR de SP2.
1. Descomprima el archivo JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Ajuste los indicadores de pila según sea necesario).

1. Cambie el nombre del JAR descomprimido para que coincida con la función y el puerto, por ejemplo `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Inicie AEM y confirme la actualización en la interfaz de usuario (Ayuda > Acerca de) y en los registros.

**Buena higiene**

* Ejecute la actualización en entornos de prueba o inferiores antes de la producción.
* Realice una copia de seguridad completa y restaurable (repositorio más cualquier almacén de datos externo) antes de empezar.
* Revise las directrices de actualización in situ y los requisitos técnicos de Adobe (se recomienda Java 17/21 para LTS).

>[!NOTE]
>
>Los nombres de archivo que se muestran arriba (por ejemplo, `cq-quickstart-6.6.x.jar`) reflejan la nomenclatura de artefactos de Quickstart observada para esta versión de LTS; use siempre el nombre de archivo exacto que descargue de Distribución de software.

## Instalación y actualización{#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

>[!NOTE]
>
> Si está actualizando directamente a LTS SP1 desde SPs antiguos de 6.5, siga las instrucciones dadas para 6.5 a 6.5 LTS GA [actualizar](/help/sites-deploying/upgrade.md).


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

Adobe revisa y desarrolla continuamente las capacidades de los productos para ofrecer un mayor valor al cliente modernizando o sustituyendo las funciones heredadas. Estos cambios se implementan teniendo en cuenta la compatibilidad con versiones anteriores.

Para garantizar la transparencia y permitir una planificación adecuada, Adobe sigue este proceso de desaprobación de Adobe Experience Manager (AEM):

* Primero se anuncia el desuso. Las funciones obsoletas siguen estando disponibles, pero ya no se mejoran.
* La eliminación no se produce antes de la siguiente versión principal. La cronología de eliminación planificada se comunica por separado.
* Se proporciona un mínimo de un ciclo de versión para que los clientes realicen la transición a alternativas admitidas antes de eliminar una capacidad.

### Funciones en desuso {#deprecated-features}

En esta sección se enumeran las características y funciones que Adobe ha dejado de utilizar en AEM 6.5 LTS. Normalmente, Adobe deja de utilizar las características antes de eliminarlas en una versión futura y proporciona una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Característica | Reemplazo | Versión (SP) |
| --- | --- | --- | --- |
| Guía de inicio rápido | API de Mongo | Las API de Mongo ya no se usan y se prevé eliminarlas en futuras versiones. | 6.5 TS SP2 |
| Sites | Compatibilidad con fragmentos de contenido en la API REST de AEM Assets | AEM 6.5 LTS SP2 proporciona OpenAPI modernas para la administración de modelos y fragmentos de contenido, por lo que los antiguos puntos finales de compatibilidad con fragmentos de contenido de la AEM Assets REST API ya no se usan.<br>Adobe tiene la intención de mantener estos puntos finales más antiguos disponibles hasta que se anuncie el final de su vida útil. Adobe no planea nuevas mejoras para los puntos finales obsoletos. | SP2 DE 6,5 LTS |
| Sites | [Editor de SPA](/help/sites-developing/spa-overview.md) | Los editores preferidos para administrar el contenido sin encabezado en AEM son: <br> el [Editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.<br>- [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios. | 6.5 LTS GA |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de IMS de Adobe |  |

### Funciones eliminadas  {#removed-features}

En esta sección se enumeran las características y funciones que se han eliminado de AEM 6.5 LTS. Las versiones anteriores tenían estas funciones marcadas como en desuso.

* Se ha eliminado la compatibilidad con RDBMK para la persistencia del repositorio CRX.
* En entornos agrupados, MongoMK es ahora la única opción admitida para la persistencia de repositorios.

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

### Corrupción del repositorio durante la compactación en línea después de la compactación sin conexión (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

Los usuarios pueden experimentar daños en el repositorio durante la compactación en línea si la compactación sin conexión se ejecutó anteriormente en el repositorio JCR. Se puede producir un `SegmentNotFoundException` (SNFE) en este escenario y puede provocar daños en el repositorio.

Para resolver el problema, instale la revisión de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip). Dado que la revisión incluye un paquete `oak-segment-tar` de bajo nivel, la instancia se reinicia después de la instalación.

Planifique el tiempo de inactividad de la instancia al aplicarla. Para la compactación sin conexión, use el [jar oak-run](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar) correspondiente, también disponible en Distribución de software.

>[!NOTE]
>
> * Para cualquier operación de oak-run, use el [jar oak-run 1.88.1-B006](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar).
>
> * Inicie AEM estableciendo la propiedad del sistema `oak.compaction.legacy=true`.

### Instalar los índices de Oak necesarios para las API descentralizadas de sitios{#site-headless-api}

Algunas API que se han trasladado a Sites Headless requieren índices de Oak adicionales para una funcionalidad completa.

Instale el paquete `cq-dam-cfm-indices` para usar las siguientes características:

* Mostrar modelos de fragmentos de contenido
* Listar fragmentos de contenido
* API de búsqueda
* Flujos de trabajo

Descargue el paquete de índice [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip) del portal de distribución de software de Adobe.

### Error de conexión de Dispatcher con la función solo SSL (corregido en AEM 6.5 LTS SP1 y posterior){#ssl-only-feature}

>[!NOTE]
>
> Este problema solo está presente en la versión de AEM 6.5 LTS GA.

Al habilitar la función Solo SSL en las implementaciones de AEM, existe un problema conocido que afecta a la conectividad entre las instancias de Dispatcher y AEM. Después de habilitar esta función, las comprobaciones de estado pueden fallar y la comunicación entre las instancias de Dispatcher y AEM puede verse interrumpida. Este problema se produce específicamente cuando los clientes intentan conectarse a través de `https + IP` desde Dispatcher a instancias de AEM. Está relacionado con problemas de validación de SNI (Indicación de nombre de servidor).

**Impacto**

* Errores de comprobación de estado con códigos de respuesta HTTP 400
* Tráfico interrumpido entre instancias de Dispatcher y AEM
* El contenido no se puede proporcionar correctamente a través de Dispatcher
* Errores de conexión al utilizar HTTPS con direcciones IP en la configuración de Dispatcher
* Errores HTTP 400 del tipo &quot;SNI no válido&quot; al conectarse mediante HTTPS + IP

**Entornos afectados**

* Implementaciones de AEM con configuraciones de Dispatcher
* Sistemas en los que se ha habilitado la función Solo SSL
* Configuraciones de Dispatcher que utilizan el método de conexión `https + IP` a instancias de AEM

**Solución**

Si tiene este problema, póngase en contacto con el servicio de atención al cliente de Adobe. Hay disponible una revisión [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) para resolver este problema. No intente habilitar las funciones Solo SSL hasta que aplique la revisión necesaria.

## Paquetes OSGI y paquetes de contenido incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión de [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/es/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience).

