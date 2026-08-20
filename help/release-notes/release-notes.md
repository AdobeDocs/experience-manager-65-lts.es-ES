---
title: Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP3
description: Busque la información actual de la versión de Adobe Experience Manager 6.5 LTS, Service Pack 3.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 0ce890503d43af340b6ee3c85b1b563613627c78
workflow-type: tm+mt
source-wordcount: '6749'
ht-degree: 26%

---


# Notas de la versión actuales de Adobe Experience Manager 6.5 LTS, SP3 {#release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versión | Paquete de servicio 3 (SP3) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 20 de agosto de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.3.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

<!-- **Mandatory Hotfix** – To avoid SNFE (SegmentNotFoundException) issues with offline compaction when installing SP2, install the hotfix described in [Known issues – Repository corruption during online compaction](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146). -->

## Qué se incluye en [!DNL Adobe Experience Manager] 6.5 LTS, SP3 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP3 incluye nuevas funciones, mejoras clave solicitadas por el cliente y correcciones de errores. Mejora el rendimiento, la seguridad y la localización en toda la plataforma desde la disponibilidad inicial de 6.5 LTS en marzo de 2025. [Instale este Service Pack](#install-update) en 6.5 LTS.

### Información general sobre problemas corregidos {#fixed-issues-overview}

[!DNL Adobe Experience Manager] 6.5 LTS, SP3 resuelve problemas en [!DNL Sites] y [!DNL Experience Manager Foundation]. Las correcciones mejoran la accesibilidad, la fiabilidad de la creación, la entrega de contenido sin encabezado, la administración de varios sitios y la estabilidad de la plataforma. Las secciones que siguen enumeran cada corrección con su número de referencia.

La mayoría de los cambios se aplican a [!DNL Sites]:

* Las mejoras de accesibilidad proceden del grupo más grande. Las actualizaciones refuerzan la navegación mediante el teclado, los comentarios de los lectores de pantalla, la administración del enfoque, el marcado semántico, el contraste del texto y el tamaño de destinatario táctil en el Editor de páginas, el carril lateral de Assets, los filtros y las interfaces de creación relacionadas.
* Las correcciones en [!DNL Content Fragments] abarcan el Editor de fragmentos, el Editor de modelos, la API de REST y la API de GraphQL. Las actualizaciones corrigen la localización, la validación de campos, el comportamiento de edición y la gestión de respuestas.
* Las correcciones de MSM Live Copies permiten a los autores implementar cambios de forma fiable desde páginas de modelo y conservar la configuración de despliegue existente.
* La compatibilidad con pasos cruzados está disponible en Adobe Managed Services, incluidos los paquetes, los usuarios del sistema y la configuración necesarios.
* Las correcciones adicionales se refieren a las interfaces admin y classic, los componentes principales, la consola de componentes, la integración de Campaign, los fragmentos de experiencias y los lanzamientos.

Los cambios restantes se aplican a [!DNL Experience Manager Foundation]:

* Las actualizaciones de localización traducen texto que antes solo estaba en inglés en los informes de estado, la consola Operaciones y varias interfaces de creación.
* Las correcciones de estabilidad restauran el extremo de supervisión de estado, mantienen el servicio de correo en ejecución después de errores de configuración intermitentes y corrigen la edición de variables de flujo de trabajo y paquetes de flujo de trabajo.
* La versión también agrega compatibilidad con el servicio de contexto de AEM y resuelve los problemas de seguridad, traducción e interfaz de usuario.

Para obtener la lista completa, consulte [Problemas corregidos en 6.5 LTS, Service Pack 3](#fixed-issues).


<!-- ## Key features and enhancements -->



<!-- UPDATE THE EACH RELEASE -->

## Se han corregido problemas en 6.5 LTS, Service Pack 3 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP3}

* AEM 6.5 LTS, Service Pack 3 incluye los paquetes Crosswalk, el paquete de contenido, los usuarios del sistema, las asignaciones de usuario de servicio, las alternancias de funciones y la configuración OSGi requerida. Las instalaciones nuevas proporcionan los requisitos previos de Crosswalk automáticamente y solo requieren una configuración de tiempo de ejecución específica del cliente. (SITES-41596)
* AEM 6.5 LTS, Service Pack 3 actualiza `cq-wcm-core` para admitir Crosswalk en Adobe Managed Services. La actualización añade la creación de plantillas y acceso al Editor universal, al tiempo que elimina los alternadores de funciones y código personalizados obsoletos. (SITES-37657)


#### Accesibilidad {#sites-accessibility-65-lts-sp3}

* El lienzo del editor de páginas ahora admite la administración de componentes solo de teclado. Los autores pueden utilizar Insertar componente, Cortar, Pegar y Eliminar para agregar, reordenar y quitar componentes. (SITES-25359) CRÍTICO
* Los usuarios de teclado ahora pueden reordenar las filas de la tabla en la vista de lista de sitios sin utilizar los gestos de arrastrar y soltar. Los controles de teclado permiten a los usuarios seleccionar una fila, moverla a otra posición y completar la colocación. (SITES-24946) CRÍTICO

* El editor de Propiedades personalizadas ahora admite la interacción mediante el teclado con sus controles de formato. Los autores pueden desplazar el enfoque entre las opciones de la barra de herramientas, seleccionar un estilo de texto y dar formato a los valores de las propiedades utilizando únicamente un teclado. (SITES-40333) PRINCIPAL

* Ahora, al enfocar el teclado se omite la lista Componentes del panel lateral cuando la interacción disponible requiere arrastrar y soltar. Este cambio evita que los usuarios del teclado introduzcan un flujo de trabajo de selección de componentes inutilizable. (SITES-40752)
* Al cerrar una superposición, ahora el enfoque se restablece a su control de activación. Los usuarios de teclado y lector de pantalla ya no vuelven a la superposición ni pierden su posición en la interfaz. (SITES-40819)
* La navegación mediante el teclado ya no desplaza el foco al contenido de página oculto. Este cambio mantiene una secuencia de enfoque predecible y evita interrupciones en la navegación. (SITES-41430)
* El botón Bloquear ahora proporciona comentarios precisos del lector de pantalla en función de su título. Los usuarios escuchan una etiqueta de acción clara en lugar de una descripción larga. (SITES-41431)
* Un indicador visual ahora identifica la opción seleccionada en el cuadro de lista Cambiar archivo o carpeta. El indicador ayuda a los usuarios a comprender la ruta de exploración y reconocer la carpeta actual. (SITES-25532)
* Los lectores de pantalla ahora anuncian una vez la dirección de clasificación ascendente o descendente. Una etiqueta descriptiva identifica claramente la acción del botón y elimina los comentarios duplicados. (SITES-25534)
* AEM Sites ahora proporciona una compatibilidad de accesibilidad más amplia en todos los flujos de trabajo de creación comunes. Las actualizaciones mejoran la interacción del teclado, las etiquetas de interfaz, la administración del enfoque y los comentarios sobre la tecnología de asistencia. (SITES-38239)
* Los elementos de la barra de herramientas ahora muestran etiquetas visibles cuando reciben el foco del teclado. Los usuarios del teclado pueden identificar cada control antes de activarlo. (SITES-40751)
* Los usuarios de teclado y lector de pantalla ahora pueden dejar el menú Bandeja de entrada sin dejarlo abierto. El menú se cierra automáticamente y conserva una ruta de navegación clara. (SITES-25518)
* Las muestras de color ahora muestran un icono de estado seleccionado con suficiente contraste. El indicador más claro ayuda a los usuarios a reconocer la muestra activa en diferentes colores de fondo. (SITES-25523)
* La barra de herramientas Editar diseño ahora informa del dispositivo actual con precisión a la tecnología de asistencia. Los botones del dispositivo ya no sugieren que los usuarios puedan activar y desactivar cada botón. (SITES-25524)
* El modal de búsqueda ahora muestra la etiqueta **Ordenar por** con suficiente contraste de texto. El estilo actualizado mejora la legibilidad para los usuarios con poca visión. (SITES-25531)
* Los botones de ordenación de Vista de lista de sitios ahora cumplen con los requisitos mínimos de contraste. Los usuarios pueden identificar más fácilmente cada control de ordenación y su estado en el fondo de la tabla. (SITES-25372)
* La lista Side Rail Assets ya no se vuelve a cargar cuando el campo Filter recibe el enfoque del teclado. Los usuarios pueden entrar en el campo sin movimientos de contenido inesperados ni anuncios repetidos del lector de pantalla. (SITES-25377)
* Las pestañas de la barra lateral del fragmento de contenido ahora proporcionan etiquetas accesibles coherentes. NVDA anuncia el nombre de la pestaña en lugar de anunciar el elemento de subnavegación seleccionado. (SITES-25509)
* El menú Ayuda ahora se cierra cuando el foco del teclado o del lector de pantalla se mueve fuera de él. Los usuarios pueden continuar navegando por los controles del encabezado o el contenido de la página sin dejar abierto el menú. (SITES-25517)
* El texto introducido en los campos de la barra de herramientas Demografía ahora cumple los requisitos mínimos de contraste. Los usuarios pueden leer más claramente los valores del perfil comparados con el fondo del campo de texto. (SITES-25318)
* El menú Información de página ahora muestra opciones enfocadas con suficiente contraste de texto. El estilo más claro ayuda a los usuarios a rastrear el enfoque del teclado a través del menú. (SITES-25321)
* Las casillas de verificación de los cuadros de diálogo Teaser, Imagen y Carrusel ahora exponen sus instrucciones relacionadas a los lectores de pantalla. Los usuarios escuchan la descripción de compatibilidad cuando el foco del teclado alcanza cada casilla de verificación. (SITES-25364)
* Los controles del editor de texto ahora comunican su estado actual a la tecnología de asistencia. Los lectores de pantalla identifican el formato de párrafo activo y la opción de destino de hipervínculo seleccionada. (SITES-25367)
* Los lectores de pantalla ahora anuncian claramente el botón **Rotar dispositivo** y la orientación actual del dispositivo. Al activar el control, se informa de la nueva orientación sin utilizar una etiqueta que describa la acción contraria. (SITES-25292)
* La navegación mediante el teclado ahora omite los controles ocultos dentro de la barra de herramientas Demografía contraída. Los usuarios pueden desplazarse por la Vista previa del diseño sin encontrar opciones de barra de herramientas no disponibles. (SITES-25304)
* Las etiquetas de texto de la barra de herramientas Demografía ahora cumplen los requisitos mínimos de contraste durante la Vista previa del diseño. Los usuarios pueden leer las etiquetas como Recomendado con mayor claridad en el fondo de la barra de herramientas. (SITES-25307)
* La barra de herramientas Demografía ahora muestra los indicadores de enfoque del botón con suficiente contraste. Los usuarios pueden identificar el control activo de Commerce, Persona o Dispositivo durante la navegación mediante el teclado. (SITES-25308)
* La barra de herramientas Editar diseño utiliza un indicador de enfoque agrupado para el selector de dispositivos. El esquema incluye los controles **Seleccionar dispositivo** y **Rotar dispositivo** relacionados como parte del comportamiento deseado de la barra de herramientas. (SITES-25283)
* La barra de herramientas Editar diseño ya no trunca la etiqueta **iPhone 8 Plus** cuando los usuarios seleccionan otro dispositivo. El nombre completo del dispositivo permanece visible en todos los estados de los botones. (SITES-25284)
* La regla Editar diseño ahora proporciona contexto de medición a los lectores de pantalla. Los usuarios escuchan una etiqueta descriptiva y el formato de medición en lugar de una serie de números inexplicable. (SITES-25287)
* La barra de herramientas Editar diseño ahora resalta el botón **Escritorio** cuando la vista de escritorio está activa. El indicador visual deja clara la selección del dispositivo actual. (SITES-25290)
* El foco del teclado ahora permanece visible en el botón de muestra en todos los colores disponibles. El espaciado añadido evita que el indicador de enfoque se fusione en la muestra seleccionada. (SITES-25253)
* Los lectores de pantalla ahora identifican correctamente el campo Fecha de deformación de tiempo. El campo ya no proporciona comentarios engañosos que sugieran que abre un cuadro de diálogo. (SITES-25263)
* La etiqueta del botón Anotación ahora cumple los requisitos mínimos de contraste en sus estados predeterminados y de desplazamiento. Los usuarios pueden leer la etiqueta claramente contra el fondo del botón. (SITES-25267)
* Los lectores de pantalla ahora anuncian etiquetas significativas para los controles en el cuadro de diálogo Anotación. Cada botón comunica su acción sin un prefijo de anotación innecesario. (SITES-25277)
* El botón Editar del carril lateral de Assets ahora proporciona un objetivo de contacto más grande. Los usuarios pueden activar el control de forma más fiable sin seleccionar un elemento cercano. (SITES-25221)
* El Editor de páginas ahora utiliza una jerarquía de encabezados lógica. Los lectores de pantalla identifican el título de página como el encabezado principal y los títulos de raíl lateral como encabezados subordinados. (SITES-25222)
* El cuadro de diálogo Anotación ahora expone su título como un encabezado semántico. Los usuarios del lector de pantalla pueden identificar el título y navegar por la estructura del cuadro de diálogo a través de los comandos de encabezado. (SITES-25248)
* Los usuarios del lector de pantalla ahora reciben comentarios cuando filtran la lista Insertar nuevo componente. El campo de búsqueda describe su comportamiento de filtrado y un mensaje de estado informa del recuento de resultados. (SITES-25251)
* El panel Componentes del raíl lateral ahora utiliza marcado de lista semántica. Los lectores de pantalla pueden anunciar el recuento de elementos y permitir una navegación eficiente por las listas. (SITES-25214)
* Los botones de información ahora utilizan iconos más grandes en el panel Componentes. Los usuarios pueden localizar y reconocer cada control con mayor facilidad. (SITES-25217)
* Los títulos de los componentes ahora permanecen visibles cuando los usuarios aumentan el espaciado del texto. Los títulos largos se ajustan en lugar de truncar o superponer el contenido cercano. (SITES-25219)
* El botón **Editar** del carril lateral de Assets ahora indica que se abre una nueva pestaña del explorador. Las señales visuales y de lector de pantalla preparan a los usuarios antes de la navegación. (SITES-25220)
* El modo de anotación ahora coloca el foco del teclado en la barra de herramientas de anotaciones cuando se abre la barra de herramientas. Los usuarios de teclado y lector de pantalla pueden desplazarse por los controles en una secuencia lógica sin tener que retroceder desde el botón **Cerrar**. (SITES-24996)
* Los botones de selección de los campos Ruta y Etiquetas ya no utilizan iconos de casilla de verificación. El icono actualizado muestra que el control abre un cuadro de diálogo de selección en lugar de cambiar un estado activado. (SITES-25210)
* El campo Filtro del panel Componentes del raíl lateral ahora tiene una etiqueta accesible válida. Los lectores de pantalla anuncian el propósito del campo en lugar de depender de un icono o texto de marcador de posición. (SITES-25212)
* El carril lateral de Assets ahora oculta miniaturas decorativas de los lectores de pantalla. Los usuarios ya no escuchan el nombre del recurso dos veces cuando navegan por la cuadrícula del recurso. (SITES-25213)
* Los botones de acordeón del carril Filtros ahora muestran los indicadores de enfoque con suficiente contraste. Los usuarios del teclado pueden rastrear el enfoque mientras navegan por las categorías de filtros. (SITES-24986)
* El carril Filtros ahora muestra un enfoque de teclado claro alrededor de los botones de opción. El aumento del contraste ayuda a los usuarios a realizar un seguimiento de su posición en las opciones de filtro. (SITES-24987)
* Ahora, la carga de mensajes de estado en la página Filtros cumple los requisitos mínimos de contraste de texto. Los usuarios pueden leer los comentarios del progreso al cambiar entre la vista de tarjeta y la vista de lista. (SITES-24991)
* El título de la página en el lienzo del editor ahora utiliza marcado de encabezado semántico. La tecnología de asistencia puede anunciar el título e incluirlo en la navegación del encabezado. (SITES-24993)
* Al expandir el menú Emulador, ahora el foco del teclado se mueve al primer elemento de menú. Al contraer el menú, el enfoque se mantiene dentro de la secuencia lógica de la barra de herramientas secundaria. (SITES-24954)
* El texto de la tabla de Live View ahora cumple los requisitos mínimos de contraste. Los usuarios pueden leer claramente los detalles de Live Copy durante los estados normal y de desplazamiento. (SITES-24956)
* El carril Referencias ahora utiliza marcado de encabezado semántico para su título. Los lectores de pantalla anuncian el encabezado durante la carga inicial y mientras los usuarios exploran las carpetas. (SITES-24967)
* Los vínculos de tarjeta ahora describen claramente sus destinos. Los usuarios del lector de pantalla pueden identificar cada vínculo sin escuchar los metadatos completos de la tarjeta. (SITES-24975)
* Los botones de menú Encabezado ya no indican a los lectores de pantalla que abran cuadros de diálogo. En su lugar, los lectores de pantalla anuncian el estado expandido o contraído de cada botón, que describe con precisión el comportamiento del menú. (SITES-24742)
* El texto del botón Eliminar ahora proporciona suficiente contraste con su fondo rojo. Los usuarios pueden identificar la acción con mayor facilidad antes de confirmar la eliminación. (SITES-24772)
* Las tarjetas de lienzo ya no exponen vínculos de imagen y encabezado independientes que llevan al mismo destino. Un solo vínculo reduce las interrupciones duplicadas del teclado y los anuncios repetidos del lector de pantalla. (SITES-24947)
* La vista de lista ahora muestra el botón de arrastrar y soltar con mayor prominencia visual. El tamaño, el peso y el contraste del icono actualizados facilitan la localización y el uso del control. (SITES-24951)
* Los botones de encabezado ahora proporcionan nombres accesibles concisos: Buscar, Aplicaciones, Ayuda, Bandeja de entrada y Usuario. Los lectores de pantalla ya no anuncian términos redundantes como &quot;en los que se puede hacer clic&quot; o &quot;gráfico&quot; durante la navegación mediante el teclado. (SITES-24715)
* Los vínculos en la navegación de la aplicación ahora muestran un énfasis visual más fuerte. El aumento del tamaño y el peso del texto mejora la legibilidad para los usuarios con poca visión o diferencias de visión de color. (SITES-24723)
* Los vínculos de la bandeja de entrada ahora utilizan marcado de lista semántica. Los lectores de pantalla pueden identificar los vínculos como un grupo relacionado, anunciar el recuento de elementos y ofrecer una navegación más eficaz. (SITES-24730)
* Los controles de información del objeto del cuadro de diálogo Preferencias de usuario ahora exponen nombres descriptivos accesibles. Los lectores de pantalla anuncian el propósito de cada control en lugar de decir &quot;en blanco&quot; antes de leer el contenido de la información sobre herramientas. (SITES-24732)
* Cada punto de referencia del carril del filtro ahora incluye una etiqueta accesible única. Los lectores de pantalla pueden distinguir el carril del filtro de otras regiones de la página e identificarlo durante la navegación. (SITES-24686)
* Los cuadros de diálogo del editor ahora separan los botones Ayuda y Alternar a pantalla completa del elemento de encabezado. Los lectores de pantalla identifican estos controles interactivos con precisión y ya no los anuncian como encabezados. (SITES-24696)
* El botón Informe CSV ahora advierte a los usuarios antes de abrir una nueva pestaña del explorador. Su etiqueta accesible comunica el comportamiento a los usuarios del lector de pantalla y del teclado antes de la activación. (SITES-24704)
* El carril de filtro ahora carga etiquetas para Búsquedas guardadas y Seleccionar directorio de búsqueda de forma coherente. El botón Filters ya no inserta elementos de etiqueta durante las interacciones de enfoque, teclado o ratón. (SITES-24706)
* Los botones Cerrar y Quitar ubicación ahora proporcionan destinos táctiles más grandes. Los usuarios pueden activar cualquiera de los controles de forma más fiable sin seleccionar elementos adyacentes. (SITES-24530)
* El botón Eliminar ubicación y su indicador de enfoque ahora cumplen los requisitos mínimos de contraste. Un contraste más fuerte ayuda a los usuarios a identificar el control y rastrear el enfoque del teclado. (SITES-24531)
* Los iFrames del editor ahora incluyen títulos descriptivos en el lienzo, los raíles laterales, los cuadros de diálogo de componentes y la vista previa del diseño. Los lectores de pantalla pueden identificar cada fotograma cuando el enfoque entra en él. (SITES-24650)
* El contraste de texto mejorado facilita la lectura de los mensajes del carril Referencias. El cambio aclara las solicitudes que solicitan una selección o informe de referencias no disponibles. (SITES-24666)
* El panel Componentes proporciona a cada icono de información una etiqueta accesible significativa. Los lectores de pantalla identifican de forma consistente el control que muestra la descripción de un componente. (SITES-24500)
* Ahora, el foco del teclado rodea todo el botón Mostrar descripción de Firma. El esquema visible ayuda a los usuarios a realizar un seguimiento de su posición y evitar activar otro control. (SITES-24503)
* El cuadro de diálogo del componente Teaser ya no expone los botones Ayuda y Alternar a pantalla completa como encabezados. Los lectores de pantalla anuncian ambos controles como botones y conservan la estructura de encabezado correcta. (SITES-24525)
* El control de encabezado de Adobe Experience Manager informa correctamente de su estado expandido o contraído. El control abre y cierra el contenido de navegación, por lo que los lectores de pantalla reciben información de estado válida. (SITES-24528)
* Los resultados del filtro marcan los iconos del globo como decorativos y eliminan sus nombres accesibles. Los lectores de pantalla ignoran los iconos en lugar de anunciar descripciones engañosas. (SITES-3057)
* El cuadro de diálogo Deformación de tiempo ahora asocia errores de entrada de tiempo con el campo correspondiente Horas o Minutos. Los lectores de pantalla anuncian el campo afectado junto con el mensaje de validación. (SITES-10980)
* El elemento de árbol de contenido seleccionado ya no forma parte de la etiqueta de control Cambiar archivo o carpeta. Los lectores de pantalla escuchan un nombre de control claro sin texto de estado adicional. (SITES-24496)
* Los puntos de referencia de región en el carril lateral de Assets ahora exponen nombres accesibles distintos. Los usuarios del lector de pantalla pueden identificar y navegar por cada región sin ambigüedad. (SITES-24497)
* Los lectores de pantalla ahora omiten la Ayuda decorativa y los iconos de pantalla completa del cuadro de diálogo Carrusel. La navegación por teclado ya no déclencheur anuncios de iconos innecesarios. (SITES-2912)
* Los lectores de pantalla ahora omiten los iconos decorativos de la barra de herramientas en el cuadro de diálogo Teaser. Los controles de Ayuda, Pantalla completa, Formato y Vínculo ya no producen anuncios redundantes. (SITES-2934)


#### Interfaz de usuario administrador{#sites-adminui-65-lts-sp3}

* AEM ahora permite a los miembros del grupo de administradores desbloquear páginas y suplantar a usuarios. Los miembros del grupo pueden completar ambas tareas administrativas a través de su acceso existente. (SITES-14732)
* La vista de administrador de Assets ahora actualiza una tarjeta de recursos después de que los autores seleccionen **Revertir a esta versión** en la cronología. La miniatura muestra la versión restaurada inmediatamente y ya no muestra contenido de vista previa obsoleto. (SITES-46590)


#### Interfaz de usuario clásica{#sites-classicui-65-lts-sp3}

Las propiedades de la copia de idioma indonesio muestran el código de idioma de ID correcto. El carril Referencias ya no sustituye IN cuando los autores crean o revisan una copia en idioma indonesio. (SITES-44918)


#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp3}

La consola de Assets ahora responde cuando los usuarios aplican filtros de búsqueda. Al cambiar un filtro de modelo de fragmento de contenido se actualizan los resultados en lugar de dejar sin cambios la lista de recursos actual. (SITES-38686) PRINCIPAL


#### [!DNL Content Fragments]: administración{#sites-admin-65-lts-sp3}

* La página Assets ahora localiza la información del objeto para un fragmento de contenido bloqueado. Los usuarios ven la etiqueta **Extraído por** traducida cuando pasan el ratón sobre el indicador de bloqueo. (SITES-42531) PRINCIPAL

* AEM localiza el mensaje de validación Nombre no válido proporcionado durante la creación del fragmento de contenido. Los caracteres de título no admitidos ya no almacenan en déclencheur el texto en inglés en las interfaces que no sean en inglés. (SITES-19796)
* AEM traduce la cadena Modelos de fragmento de contenido durante la creación del fragmento de contenido. La interfaz de Assets ya no muestra texto en inglés para esa etiqueta en entornos localizados. (SITES-22336)
* Los servicios de fragmento de contenido ya no dependen de la lógica de alternancia de funciones obsoletas. La implementación optimizada elimina las ramas que dependen de la alternancia y mantiene el comportamiento uniforme del Service Pack. (SITES-38688)
* AEM traduce la opción Más tarde durante la publicación programada del fragmento de contenido. El flujo de trabajo de publicación coincide con el idioma de la interfaz activa. (SITES-42532)
* AEM traduce la cadena Principal en el cuadro de diálogo de descarga de fragmentos de contenido. La sección Elementos coincide con el idioma de la interfaz activa. (SITES-42534)


#### [!DNL Content Fragments] - Editor de fragmentos{#sites-fragments-editor-65-lts-sp3}

* El Editor de fragmentos de contenido ahora coloca correctamente los menús desplegables del Editor de texto enriquecido. Cada menú permanece alineado con su control de barra de herramientas y mantiene visibles los controles de formato cercanos. (SITES-44005) CRÍTICO

* El botón Editar fragmento de contenido ahora aparece y funciona inmediatamente para las entradas de multicampo de referencia. Los autores ya no necesitan guardar, cerrar y volver a abrir el fragmento de contenido principal antes de editar un fragmento incrustado. (SITES-43733) PRINCIPAL

* El Editor de fragmentos de contenido muestra una descripción de enfoque cuando los autores seleccionan un campo de texto multilínea. El esquema ya no duplica ni superpone los controles cercanos. (SITES-39253)
* La creación de fragmentos de contenido muestra texto de marcador de posición CJK sin estilo en cursiva. Los caracteres japoneses, coreanos, chino simplificado y chino tradicional conservan el aspecto deseado. (SITES-43548)
* El Editor de fragmentos de contenido actualiza el banner de estado después de que los autores guarden o publiquen un fragmento. Los autores pueden confirmar los estados Modificado, Guardado o Publicado sin volver a cargar la pestaña del explorador. (SITES-45897)
* El Editor de fragmentos de contenido valida los campos de forma coherente después de realizar cambios en la IU de Granite. Las bibliotecas de cliente actualizadas restauran el comportamiento de validación esperado. (SITES-46650)


#### [!DNL Content Fragments]: API GraphQL {#sites-graphql-api-65-lts-sp3}

* Las respuestas JSON de GraphQL ahora incluyen referencias de imagen incrustadas cuando los nombres de archivo DAM contienen espacios o caracteres no ASCII. Las aplicaciones cliente pueden recuperar y procesar estas imágenes sin cambiar el nombre de los recursos. (SITES-42191) PRINCIPAL
* La API de GraphQL de fragmentos de contenido ahora incluye varias actualizaciones de procesamiento de consultas y de gestión de respuestas. Los cambios evitan valores y encabezados de caché duplicados, mejoran la codificación, conservan la información de estado de las consultas persistentes, administran encabezados vacíos y devuelven errores de extremo apropiados. (SITES-40159) PRINCIPAL
* PersistedQueryServlet ahora procesa variables codificadas en consultas persistentes válidas de GraphQL sin registrar errores o advertencias falsos. Las consultas siguen devolviendo respuestas correctas, mientras que los registros reflejan su estado de ejecución real. (SITES-39354) PRINCIPAL

* Al volver a cargar la página Puntos finales de GraphQL se conserva el mensaje de estado vacío localizado. La página ya no vuelve al inglés cuando no existen extremos. (SITES-43586)


<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp3}-->


#### [!DNL Content Fragments]: Editor de modelo{#sites-model-editor-65-lts-sp3}

* La consola Modelos de fragmentos de contenido ahora muestra miniaturas cargadas para configuraciones cuyos nombres contienen caracteres localizados. Los autores ya no pierden las vistas previas de miniaturas cuando los nombres de configuración utilizan texto que no esté en inglés. (SITES-39242) PRINCIPAL

* El Editor del modelo de fragmentos de contenido muestra texto **Etiqueta de campo** localizado en cuanto los autores agregan un componente al lienzo. Los autores ya no necesitan guardar y volver a abrir el modelo para ver la traducción. (SITES-45383)
* El Editor del modelo de fragmentos de contenido localiza el mensaje de validación que se muestra cuando los autores seleccionan un tipo de modelo no válido para un componente compuesto. El mensaje ahora coincide con la configuración regional activa en lugar de aparecer únicamente en inglés. (SITES-41117)
* El Editor del modelo de fragmentos de contenido localiza todo el texto del cuadro de diálogo El modelo está bloqueado. El cuadro de diálogo ya no mezcla etiquetas e instrucciones de botones en inglés con texto de interfaz traducido. (SITES-28592)



#### [!DNL Content Fragments]: API REST{#sites-restapi-65-lts-sp3}

El paquete de API de REST de fragmento de contenido sin encabezado elimina los alternadores de funciones obsoletas y el código condicional relacionado. El comportamiento de la API admitida permanece sin cambios, mientras que el paquete conserva solo las alternancias necesarias para las funciones activas. (SITES-39113)



#### Consola de componente{#sites-component-console-65-lts-sp3}

El Buscador de contenido ahora enumera los recursos cuyos nombres contienen caracteres no codificables sin provocar errores ni generar excepciones. La página Uso activo de componentes también carga grandes conjuntos de resultados de forma continua sin mostrar filas vacías durante el desplazamiento. (SITES-44672) PRINCIPAL

<!--
#### Content API{#sites-content-api-65-lts-sp3}

#### Core backend{#sites-core-backend-65-lts-sp3}
-->

#### Componentes principales{#sites-core-components-65-lts-sp3}

* Los componentes de varios campos ahora almacenan una selección remota de recursos independiente para cada entrada. Los autores pueden seleccionar, cambiar y guardar imágenes remotas sin duplicar una imagen en cada elemento de varios campos. (SITES-42376) PRINCIPAL
* ThumbnailServlet ahora deja de procesarse después de redirigir una solicitud de un recurso que falta. Este cambio evita repetidas excepciones de puntero nulo y un registro de errores excesivo durante la exploración de DAM y la consola. (SITES-41238) PRINCIPAL


#### Integración de Campaign{#sites-campaign-integration-65-lts-sp3}

El ContentServlet de Campaign ahora conserva el tipo de contenido de respuesta JSON durante las solicitudes de contenido. Este cambio detiene las entradas de registro repetidas `WARN` y `ERROR` que se produjeron después de una actualización de AEM 6.5.24. (SITES-46902) PRINCIPAL


#### Fragmentos de experiencias{#sites-experiencefragments-65-lts-sp3}

Los autores ahora pueden examinar más de 40 plantillas al crear una variación de fragmento de experiencia. Cada página adicional conserva el filtro de carpeta original y muestra las siguientes plantillas coincidentes. (SITES-41531) PRINCIPAL


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp3} -->


#### Lanzamientos{#sites-launches-65-lts-sp3}

El historial de promociones de Launch ahora muestra texto localizado en la cronología de Sites. La cronología traduce los mensajes &quot;Versión creada de&quot; y &quot;antes de promocionar el lanzamiento&quot; en las configuraciones regionales admitidas. (SITES-13389)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp3} -->



#### MSM: Live Copy{#sites-msm-live-copies-65-lts-sp3}

* Las carpetas de Live Copy de fragmentos de contenido ahora conservan cq:rolloutConfigs cuando los autores guardan las propiedades sin cambios. Los autores pueden actualizar posteriormente la configuración de despliegue sin perder la configuración existente. (SITES-43729) CRÍTICO

* Los autores ahora pueden implementar cambios de componentes desde la barra de herramientas editable en una página de modelo. El despliegue se completa sin un error de JavaScript y propaga los cambios a Live Copy. (SITES-46052) PRINCIPAL
* Los autores ahora pueden completar despliegues de MSM desde páginas de modelo después de una actualización. El cuadro de diálogo de despliegue carga las Live Copies disponibles y habilita sus controles de despliegue en lugar de permanecer en un estado de carga perpetua. (SITES-43116) PRINCIPAL

* La Información general de Live Copy ahora aplica formatos de fecha localizados en Estado de relación. Los campos **Última modificación de Live Copy en Source**, **Última modificación de Live Copy** y **Última implementación** coinciden con la configuración regional del usuario. (SITES-40756)
* Al desactivar un modelo principal y sus páginas secundarias en una solicitud, ahora se produce un evento de despliegue por ruta. El administrador de despliegue ya no ejecuta acciones duplicadas para la misma página secundaria. (SITES-44987)


#### Editor de páginas{#sites-pageeditor-65-lts-sp3}

* Los autores ahora pueden crear y aplicar etiquetas con letras mayúsculas o espacios durante un guardado de Propiedades de página. AEM almacena inmediatamente el valor de etiqueta normalizado y conserva la asignación de la página. (SITES-42550) CRÍTICO

* Al desplazarse por el menú Estilo, ya no se quita el resaltado del estilo seleccionado. Los autores pueden confirmar su selección actual mientras revisan otras opciones disponibles. (SITES-30874) PRINCIPAL

* El botón Vínculo del editor de texto enriquecido ahora se abre cuando los autores acceden a AEM a través de HTTP. La creación de vínculos ya no genera un déclencheur de error `crypto.randomUUID`. (SITES-39467)
* Los autores ahora pueden copiar y pegar los componentes de fragmento de contenido configurados en contenedores de diseño vacíos. El componente pegado conserva su referencia de fragmento de contenido original y ya no muestra el error *Elegir una variación de experiencia*. (SITES-41586)
* El Editor de imágenes ahora respeta las proporciones de recorte personalizadas durante la edición en línea híbrida. Cada destino de colocación de imagen utiliza su propia configuración, por lo que las selecciones de recorte se aplican de una manera correcta fuera del modo de pantalla completa. (SITES-45771)

<!--
#### Replication{#sites-replication-65-lts-sp3}

#### Rich Text Editor{#sites-rte-65-lts-sp3}

#### Template Editor{#sites-template-editor-65-lts-sp3}

#### Universal editor {#sites-universal-editor-65-lts-sp3}

### [!DNL Assets]{#assets-65-lts-sp3}

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp3}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp3}
-->



<!--
### [!DNL Forms]{#forms-65-lts-sp3}
-->



### Foundation {#foundation-65-lts-sp3}

#### AEM Context Service {#foundation-aem-context-service-65-lts-sp3}

AEM 6.5 LTS presenta compatibilidad con AEM Context Service. El despliegue agrega API de servicio, integración de agente, aprovisionamiento de AMS, integración de Experience Cloud, monitorización de la producción, runbooks operativos e informes de uso. (GRANITE-65148)

#### Apache Felix {#foundation-apachefelix-65-lts-sp3}

El servicio de correo de AEM ahora sigue enviando correos electrónicos cuando se producen errores de configuración intermitentes. Los administradores ya no necesitan reiniciar el paquete de Day Communicque 5 Mailer para restaurar la entrega de correo electrónico. (GRANITE-66817) PRINCIPAL

<!--
#### Campaign{#foundation-campaign-65-lts-sp3}

#### Cloud Services{#foundation-cloudservices-65-lts-sp3}

#### Communities {#foundation-communities-65-lts-sp3}

#### Content distribution{#foundation-content-distribution-65-lts-sp3}

#### CRX {#foundation-crx-65-lts-sp3}

#### Granite{#foundation-granite-65-lts-sp3}

#### HTL{#foundation-htl-5-lts-sp3}

#### Integrations{#foundation-integrations-65-lts-sp3}

#### Jetty{#foundation-jetty-65-lts-sp3}
-->

#### Localización{#foundation-localization-65-lts-sp3}

* La consola Operaciones ahora localiza el texto que no se ha traducido anteriormente en los informes de estado. Los usuarios ven mensajes de estado, advertencias, resultados de mantenimiento e información de rendimiento traducidos. (NPR-44280) PRINCIPAL

* La tarea de mantenimiento del registro de auditoría ahora muestra una exención de responsabilidad localizada. Los administradores ven la conformidad y la orientación legal en el idioma seleccionado antes de configurar la depuración automatizada de registros de auditoría. (NPR-44188)
* La página Editar Usuario ahora muestra un error localizado cuando los usuarios reordenan los perfiles modificados. El mensaje explica claramente que los perfiles modificados no se pueden mover hasta que los usuarios guarden sus cambios. (NPR-44282)
* AEM ahora localiza la información del objeto en las propiedades de la Lista de fragmentos de contenido. La guía traducida explica la selección del modelo, el filtrado de etiquetas, las rutas de contenido, los límites de elementos y la configuración de ordenación. (SITES-14969)
* Los vínculos de ayuda del componente del Editor de plantillas ahora abren la documentación localizada. Los autores obtienen directrices que coinciden con el idioma seleccionado en lugar de páginas de componentes solo en inglés. (SITES-15058)
* El editor de directivas de componentes ahora localiza los errores que informan sobre un recurso no modificable o sobre la creación fallida de un nodo. Los autores de plantillas reciben estos mensajes en el idioma seleccionado. (SITES-17475)

<!-- #### Omnisearch{#foundation-omnisearch-65-lts-sp3} -->

#### Tablero de operaciones{#foundation-operations-dashboard-65-lts-sp3}

El extremo `/system/health/systemalive.json` ahora permanece disponible después de que los clientes actualicen AEM LTS. Una configuración de contexto de servlet corregida evita las respuestas HTTP 404 y admite sistemas de supervisión de estado que dependen del extremo. (GRANITE-69457) CRÍTICO

#### Plataforma{#foundation-platform-65-lts-sp3}

La lista de permitidos de opción de expresión HTL predeterminada ahora reconoce `decorationTagName` y `cssClassName`. Al procesar la cuadrícula adaptable estándar, ya no se rellenarán `error.log` con advertencias repetidas de opciones desconocidas. (GRANITE-67152)

<!--
#### Projects{#foundation-projects-65-lts-sp3}

#### Oak {#foundation-oak-65-lts-sp3}

#### Quickstart{#foundation-quickstart-65-lts-sp3} 
-->


#### Seguridad{#foundation-security-65-lts-sp3}

La acción **Copiar grupo** ahora abre el formulario esperado en lugar de mostrar una página en blanco. Los administradores pueden introducir un nuevo ID de grupo y una descripción y luego duplicar un grupo de seguridad existente. (NPR-44302) PRINCIPAL


<!-- #### Sling{#foundation-sling-65-lts-sp3} -->


#### Traducción{#foundation-translation-65-lts-sp3}

Los proyectos de traducción ahora mantienen recuentos de estado precisos a medida que progresan los flujos de trabajo. La creación y propagación de estado de Launch siguen el comportamiento esperado del flujo de trabajo, eliminando los metadatos de proyecto incoherentes. (NPR-43420)


#### Interfaz de usuario{#foundation-ui-65-lts-sp3}

* La etiqueta País/Región aparece ahora en el idioma de interfaz seleccionado. Las interfaces localizadas ya no muestran la etiqueta en inglés. (NPR-43883)
* Al seleccionar una página del mismo nivel, ahora se activa **Select** en selectores de rutas de varios campos compuestos. Los autores pueden confirmar la nueva ruta sin agrandar la ventana del explorador ni repetir la selección. (GRANITE-69323)


<!-- #### WCM{#foundation-wcm-65-lts-sp3} -->


#### Flujo de trabajo{#foundation-workflow-65-lts-sp3}

* Las páginas de paquetes de flujos de trabajo ahora admiten los componentes Árbol de contenido y Definición de recurso editable en el Editor de páginas de IU táctil. Los autores pueden desplazarse por el contenido del paquete, así como inspeccionar o actualizar sus componentes sin utilizar la IU clásica. (GRANITE-67348) PRINCIPAL
* El editor de páginas de IU táctil ahora procesa el árbol de contenido para las páginas de paquete de flujo de trabajo. Los autores pueden inspeccionar la estructura del paquete y editar los componentes de definición de recursos a través del mismo editor. (GRANITE-67186) PRINCIPAL

* El cuadro de diálogo de variables de flujo de trabajo ahora muestra los controles correctos para las variables Modelo de datos de formulario, JSON, XML y Documento. Los autores ya no ven el marcado de HTML sin procesar cuando crean estas variables no primitivas. (GRANITE-67915)



## Acerca de [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 LTS se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x se utiliza como motor servlet para Quickstart.

### Compatibilidad con Java™  {#java-support}

* Compatibilidad con Java™ 17 y Java™ 21.
* Para obtener un rendimiento óptimo, reemplace los valores predeterminados de GC por otros valores. Para obtener más información, consulte la sección [Instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye actualizaciones de mantenimiento de Java™ 17 y Java™ 21 para que las utilicen los clientes en proyectos relacionados con AEM cuando no están disponibles para el público desde Oracle.

### Empaquetado de Uberjar {#uber-jar-packaging}

UberJar para AEM 6.5 LTS SP3 usa AEM 6.5 LTS UberJar versión 6.6.3. Puede recuperar los artefactos de UberJar correspondientes del repositorio de Maven Central. A diferencia de AEM 6.5, AEM 6.5 LTS separa las API públicas y las API obsoletas en dos artefactos diferentes.

Para compilar con las API públicas, utilice lo siguiente:

    &quot;xml
    &lt;dependencies>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;classifier>apis&lt;/classifier>
    &lt;scope>proporcionado&lt;/scope>
    &lt;/dependencies>
    &quot;

Si su código también depende de API obsoletas, agregue lo siguiente:

    &quot;xml
    &lt;dependencies>
    &lt;groupId>com.adobe.aem&lt;/groupId>
    &lt;artifactId>uber-jar&lt;/artifactId>
    &lt;version>6.6.3&lt;/version>
    &lt;classifier>deprecated-apis&lt;/classifier>
    &lt;scope>proporcionado&lt;/scope>
    &lt;/dependencies>
    &quot;

Consulte también [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Actualizar {#upgrade}

* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).
* Para obtener instrucciones de actualización detalladas, consulte [Guía de actualización de AEM Forms 6.5 LTS SP1 en JEE](https://experienceleague.adobe.com/es/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## Prácticas recomendadas para las actualizaciones del Service Pack de AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

Se aplica a: clientes de AEM 6.5 LTS (On-Premise) que instalan el Service Pack 3 (SP3). SP3 se entrega como un JAR de inicio rápido.

**Por qué es importante esta práctica de actualización**
SP2 for AEM 6.5 LTS se envía como un archivo JAR de inicio rápido en lugar de como un archivo ZIP para instalarlo a través del administrador de paquetes. Los clientes On-Premise actualizan reemplazando el JAR de Quickstart, desempaquetándolo y reiniciándolo. Este método es coherente con el procedimiento de actualización estándar de Adobe.


**Flujo de actualización recomendado (autor o publicación)**

1. Compruebe que la instancia de AEM 6.5 LTS esté en buen estado y sea accesible.
1. Descargue el archivo JAR de inicio rápido SP (por ejemplo, `cq-quickstart-6.6.x.jar`) desde Distribución de software.
1. Detenga la instancia en ejecución.
1. En el directorio de instalación de AEM (fuera de `crx-quickstart/`), reemplace el JAR de inicio rápido anterior por el JAR del SP3.
1. Descomprima el archivo JAR:

       &quot;java
     java -jar cq-quickstart-6.6.x.jar -unpack
     &quot;
   
   (Ajuste los indicadores de pila según sea necesario).

1. Cambie el nombre del JAR descomprimido para que coincida con la función y el puerto, por ejemplo `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Inicie AEM y confirme la actualización en la interfaz de usuario (Ayuda > Acerca de) y en los registros.

**Prácticas recomendadas**

* Ejecute la actualización en entornos de prueba o inferiores antes de la producción.
* Realice una copia de seguridad completa y restaurable (repositorio más cualquier almacén de datos externo) antes de empezar.
* Revise las directrices de actualización in situ y los requisitos técnicos de Adobe (se recomienda Java 17/21 para LTS).

>[!NOTE]
>
>Los nombres de archivo mostrados arriba (por ejemplo, `cq-quickstart-6.6.x.jar`) reflejan la nomenclatura de artefactos de inicio rápido detectada para esta versión de LTS; use siempre el nombre de archivo exacto que se descarga de Distribución de software.

## Instalación y actualización{#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

>[!NOTE]
>
> Si está actualizando directamente a LTS SP1 desde SP antiguos de 6.5, siga las instrucciones que se dan para la [actualización](/help/sites-deploying/upgrade.md) de 6.5 a 6.5 LTS GA.


Para obtener instrucciones detalladas, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md), ya que la misma documentación se aplica a las actualizaciones del Service Pack de LTS.

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

Adobe revisa y optimiza continuamente las funciones de los productos para ofrecer un mayor valor al cliente mediante la modernización o el reemplazo de funciones antiguas. Estos cambios se implementan teniendo en cuenta la compatibilidad con versiones anteriores.

Para garantizar la transparencia y permitir una planificación adecuada, Adobe sigue este proceso de desuso para Adobe Experience Manager (AEM):

* Primero se anuncia el desuso. Las funciones en desuso siguen estando disponibles, pero ya no se mejoran.
* La eliminación no se produce antes de la siguiente versión principal. La cronología de la eliminación planificada se comunica por separado.
* Se proporciona un mínimo de un ciclo de lanzamiento para que los clientes realicen la transición a alternativas admitidas antes de eliminar una capacidad.

### Funciones en desuso {#deprecated-features}

En esta sección se enumeran las características y funciones que Adobe ha dejado de utilizar en AEM 6.5 LTS. Normalmente, Adobe deja de utilizar las características antes de eliminarlas en una versión futura y proporciona una alternativa.

Se aconseja a los clientes que comprueben si utilizan la función o la capacidad en su implementación actual. Planifique el cambio de la implementación para utilizar la alternativa proporcionada.

| Área | Característica | Reemplazo | Versión (SP) |
| --- | --- | --- | --- |
| Sites | Resumen del texto del fragmento de contenido | No hay sustitución disponible. | |
| Guía de inicio rápido | API de Mongo | Las API de Mongo ya están en desuso y se planea eliminarlas en futuras versiones. | 6.5 TS SP2 |
| Sites | Compatibilidad con fragmentos de contenido en la API REST de AEM Assets | AEM 6.5 LTS SP2 proporciona OpenAPI modernas para la administración de modelos y fragmentos de contenido, por lo que los puntos finales de compatibilidad de fragmentos de contenido más antiguos en la API de REST de AEM Assets ya no se utilizan.<br>Adobe tiene la intención de mantener estos puntos finales más antiguos disponibles hasta que se anuncie el fin de la vida útil. Adobe no planea más mejoras para los puntos finales obsoletos. | 6.5 LTS SP2 |
| Sites | [Editor de SPA](/help/sites-developing/spa-overview.md) | Los editores preferidos para administrar el contenido headless en AEM son:<br>- [El Editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.<br>- [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios. | 6.5 LTS GA |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de IMS de Adobe | |

### Funciones eliminadas {#removed-features}

En esta sección se enumeran las características y funciones que se han eliminado de AEM 6.5 LTS. Las versiones anteriores tenían estas funciones marcadas como en desuso.

* Se ha eliminado la compatibilidad con RDBMK para la persistencia del repositorio de Adobe CRX.
* En entornos agrupados, MongoMK es ahora la única opción admitida para la persistencia del repositorio.

| Área | Característica | Reemplazo | Versión (SP) |
| --- | --- | --- | --- |
| Comercio | AEM CIF Classic no es compatible. | Migre a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluciones | Social/Communities no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Screens | Screens no se admiten. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `dam-pim` y `dam-rating` no se admiten porque los paquetes dependen de las redes sociales. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` se ha eliminado. | Utilice la API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` que se ha añadido. | 6.5 LTS GA |
| Portal | AEM Portal Director no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | Se ha eliminado el paquete `com.adobe.granite.socketio`. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `crx2oak` no es compatible. | Elija la versión pertinente de [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade). | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Guava | Todas las dependencias de Guava ahora se eliminan en AEM y, por lo tanto, el paquete `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` no forma parte de AEM. | Los clientes pueden agregar Guava por su cuenta si dependen de Guava o reemplazar el código de Guava con colecciones de Java u otras alternativas si es posible. | 6.5 LTS GA |
| `We.Retail` | El sitio de muestra `We-retail` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | El paquete `oak-solr-osgi` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` y `org.apache.sling.atom.taglib` no son compatibles. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.commons.io` paquetes se han exportado desde `org.apache.commons.commons-io`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | Se están exportando `javax.mail` paquetes desde el paquete `com.sun.javax.mail`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `org.apache.jackrabbit.api` paquetes se han exportado ahora desde el paquete `org.apache.jackrabbit.oak-jackrabbit-api`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `com.github.jknack.handlebars` no es compatible | Elija la [versión](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente. | 6.5 LTS GA |

## Problemas conocidos {#known-issues}

### AEM Forms

* En el Administrador de configuración, la inicialización de la base de datos falla durante Bootstrap en el modo personalizado llave en mano de AEM Forms 6.5 LTS JEE cuando no se selecciona ningún módulo o solo componentes limitados. El error se debe a que falta una dependencia (xalan-2.7.2.jar), lo que provoca un error. Añadir el archivo JAR a Adobe-livecycle-jboss.ear\lib resuelve el problema. (FORMS-24690)
* En implementaciones de Forms JEE LTS Service Pack 2 que se ejecutan en el perfil WebSphere® Liberty, la funcionalidad de correo electrónico falla. Al intentar utilizar las características de correo electrónico, el servidor registra un error: `Could not convert socket to TLS`. (FORMS-24692)
* En Forms JEE LTS que se ejecuta en JBoss®, la funcionalidad relacionada con el correo electrónico falla. Al intentar utilizar las características de correo electrónico, el servidor registra un error: `Error IMAPProvider not a subtype`. Para resolver este problema, instale la revisión de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear). (FORMS-24892)

### Corrupción del repositorio durante la compactación en línea después de la compactación sin conexión (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

Los usuarios pueden experimentar daños en el repositorio durante la compactación en línea si la compactación sin conexión se ejecutó antes en el repositorio JCR. Se puede producir un `SegmentNotFoundException` (SNFE) en este escenario y puede provocar daños en el repositorio.

Para resolver el problema, instale la revisión de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip). Dado que la revisión incluye un paquete `oak-segment-tar` de bajo nivel, la instancia se reinicia después de la instalación.

Planifique el tiempo de inactividad de la instancia al aplicarla. Para la compactación sin conexión, use el Jar [`oak-run` correspondiente](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar), también disponible en Distribución de software.

>[!NOTE]
>
> * Para cualquier operación de `oak-run`, use el Jar [`oak-run` 1.88.1-B006](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar).
>
> * Inicie AEM estableciendo la propiedad del sistema `oak.compaction.legacy=true`.

### Falta el paquete `com.adobe.granite.apicontroller` en AEM 6.5 LTS SP2 (GRANITE-67640) {#missing-apicontroller-bundle-granite-67640}

Falta el paquete `com.adobe.granite.apicontroller` en AEM 6.5 LTS SP2. Este paquete controla cómo se resuelven los paquetes OSGi y puede evitar que se resuelvan en otros paquetes, lo que resulta útil para limitar las API expuestas.

Para usar esta funcionalidad, instale la revisión de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip).

>[!NOTE]
>
> Para asegurarse de que la configuración predeterminada de `com.adobe.granite.apicontroller` no introduce restricciones de resolución no deseadas que afecten a las implementaciones personalizadas existentes, compruebe el estado del paquete de todos los paquetes instalados después de instalar la revisión.

### Los comentarios JSON ya no son compatibles con Sling-Initial-Content (SP2) {#json-comments-no-longer-supported-in-sling-initial-content}

Este problema afecta a los desarrolladores y administradores de paquetes OSGi que implementan paquetes que utilizan `Sling-Initial-Content` con archivos JSON.

A partir de AEM 6.5 LTS SP2, los archivos JSON utilizados en paquetes de `Sling-Initial-Content` ya no aceptan comentarios (`//` o `/* */`). En versiones anteriores de AEM se aceptaban comentarios porque el proveedor `javax.json` era flexible al respecto. AEM 6.5 LTS SP2 actualizó `org.apache.sling.jcr.contentloader` a la versión 2.6.0, lo que cambió el analizador JSON a `jakarta.json`. Aunque la especificación [JSON (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) no define una sintaxis para los comentarios, las versiones anteriores de AEM los aceptaban debido a la flexibilidad del proveedor `javax.json`. El proveedor `jakarta.json` no ofrece esta extensión.

El error es silencioso: los nodos de contenido no se cargan durante la activación del paquete sin que se muestre ningún error al instalador. Si falta contenido inesperadamente después de actualizar a SP2, compruebe los registros del instalador OSGi para ver si hay errores de análisis de JSON. Para identificar los paquetes afectados, busque `//` o `/* */` dentro de los archivos JSON enumerados en los encabezados de manifiesto de `Sling-Initial-Content`.

>[!CAUTION]
>
> Para evitar errores en la carga de contenido después de actualizar a AEM 6.5 LTS SP2, quite todos los comentarios de los archivos JSON en los paquetes de `Sling-Initial-Content`.

### La actualización del paquete Jackson afecta al conector GlobalLink {#jackson-upgrade-globallink-connector}

AEM 6.5 LTS SP3 actualiza el paquete `jackson`. Este cambio afecta a las implementaciones que utilizan el conector de traducción GlobalLink.

Si utiliza el paquete `gs4tr-globallink-adaptors-aem.core` en una versión anterior a la 3.4.0, actualice el paquete a una versión compatible. La versión 3.4.0 o posterior funciona con el paquete `jackson` actualizado en SP3.

>[!NOTE]
>
> Actualice el paquete `gs4tr-globallink-adaptors-aem.core` a la versión 3.4.0 o posterior antes o durante la actualización del SP3 para evitar problemas de compatibilidad con el conector GlobalLink.


### Instale los índices Oak necesarios para las API headless de Sites{#site-headless-api}

Algunas API que se trasladaron a Sites headless requieren índices Oak adicionales para una funcionalidad completa.

Para utilizar las siguientes características, instale el paquete `cq-dam-cfm-indices`:

* Lista de modelos de fragmento de contenido
* Lista de fragmentos de contenido
* API de búsqueda
* Flujos de trabajo

Descargue el paquete de índice [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fcq-dam-cfm-indices-1.1.5.zip) del portal de distribución de software de Adobe.

### Error de conexión de Dispatcher con la función solo SSL (corregido en AEM 6.5 LTS SP1 y posterior){#ssl-only-feature}

>[!NOTE]
>
> Este problema solo está presente en la versión de AEM 6.5 LTS GA.

Al habilitar la función Solo SSL en las implementaciones de AEM, existe un problema conocido que afecta a la conectividad entre las instancias de Dispatcher y AEM. Después de habilitar esta función, las comprobaciones de estado fallan y la comunicación entre las instancias de Dispatcher y AEM se interrumpe. Este problema se produce específicamente cuando los clientes intentan conectarse a través de `https + IP` desde Dispatcher a instancias de AEM. Está relacionado con problemas de validación de SNI (Indicación de nombre de servidor).

**Impacto**

* Errores de comprobación de estado con códigos de respuesta HTTP 400.
* Tráfico interrumpido entre instancias de Dispatcher y AEM.
* El contenido no se puede proporcionar correctamente a través de Dispatcher.
* Errores de conexión al utilizar HTTPS con direcciones IP en la configuración de Dispatcher.
* Errores HTTP 400 del tipo “SNI no válido” al conectarse mediante HTTPS + IP.

**Entornos afectados**

* Implementaciones de AEM con configuraciones de Dispatcher.
* Sistemas en los que se ha habilitado la función Solo SSL.
* Configuraciones de Dispatcher que utilizan el método de conexión `https + IP` a instancias de AEM.

**Solución**

Si tiene este problema, póngase en contacto con el servicio de atención al cliente de Adobe. Hay disponible una revisión [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) para resolver este problema. No intente habilitar las funciones Solo SSL hasta que aplique la revisión necesaria.

## Paquetes OSGI y paquetes de contenido incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes archivos zip contienen los documentos de texto que enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio LTS de Experience Manager 6.5:

* [paquetes OSGi](/help/release-notes/assets/65lts_sp3_bundles.zip)
* [Paquetes de contenido](/help/release-notes/assets/65lts_sp3_packages.zip)

## Sitios web restringidos{#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga del producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/es/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience).

