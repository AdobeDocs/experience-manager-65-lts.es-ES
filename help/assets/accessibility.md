---
title: Características e interfaces accesibles de  [!DNL Experience Manager Assets]
description: Obtenga información sobre cómo las características de accesibilidad de [!DNL Adobe Experience Manager] 6.5 LTS [!DNL Assets] ayudan a los usuarios con discapacidades.
feature: Asset Management
role: User, Architect, Leader
solution: Experience Manager, Experience Manager Assets
exl-id: f9540bfb-1c4f-41f0-9caa-ef9265225648
source-git-commit: 61a1bb55f4b8da8c421f51ee203ca8e433a73a64
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 1%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Características de accesibilidad en [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permite a los creadores y editores de contenido ofrecer experiencias increíbles en la web. Adobe se esfuerza por incluir a los creadores con discapacidades al mejorar la accesibilidad de [!DNL Experience Manager]. El software se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios y se adhiere a los estándares mundiales que incluyen personas con deficiencias visuales, auditivas, de movilidad u otras.

[!DNL Experience Manager] publica información de conformidad que describe los estándares a los que se adhiere, describe las características de accesibilidad del producto y describe el nivel de conformidad. Los informes de conformidad con la accesibilidad ayudan a los usuarios de [!DNL Experience Manager] a comprender el nivel de cumplimiento de varios estándares. Las mejoras realizadas en [!DNL Assets] permiten a todos los usuarios utilizar las interfaces fácilmente mediante el teclado, el lector de pantalla, los ampliadores y otras tecnologías de asistencia.

[!DNL Experience Manager] proporciona distintos niveles de compatibilidad con los siguientes estándares:

* [Directrices de accesibilidad de contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Se ha revisado la Sección 508 de la Ley de Rehabilitación](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Iniciativa de accesibilidad - Aplicaciones de Internet enriquecidas accesibles (WAI-ARIA) por W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para leer un informe con detalles del nivel de cumplimiento, consulte la página [Informe de conformidad de accesibilidad](https://www.adobe.com/accessibility/compliance.html) (ACR).

Para saber cómo se puede obtener acceso a [!DNL Dynamic Media], consulte [accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologías de asistencia {#at-support}

Los usuarios con discapacidades suelen depender del hardware y el software para acceder al contenido web y utilizar productos de software. Estas herramientas se conocen como tecnologías de asistencia. [!DNL Experience Manager Assets] puede trabajar con los siguientes tipos de tecnologías de asistencia (AT) al usar las funcionalidades principales del software:

* Lectores de pantalla y ampliador de pantalla.
* Software de reconocimiento de voz.
* Uso del teclado: navegación y métodos abreviados.
* Hardware de asistencia, incluidos controles de conmutador, pantallas de Braille actualizables y otros dispositivos de entrada de equipo.
* Herramientas de ampliación de IU.

## [!DNL Experience Manager Assets] casos de uso accesibles {#accessible-assets-use-cases}

En [!DNL Experience Manager], las características de accesibilidad satisfacen dos requisitos clave de [!DNL Experience Manager] usuarios y sus clientes.

* Para los diseñadores y creadores de contenido, hay funciones para crear y publicar contenido accesible que utilizan a su vez sus clientes y visitantes del sitio web. Las personas con discapacidad utilizan el contenido con la ayuda de tecnologías de asistencia. Para obtener más información, consulte [directrices de accesibilidad web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] también permite a los usuarios y administradores con discapacidades acceder a la interfaz de usuario y a los controles para crear y administrar contenido. Las personas con discapacidades pueden usar tecnologías de asistencia para navegar, usar y administrar la capacidad de [!DNL Assets].

Las características principales de [!DNL Assets] son más accesibles que antes y se actualizan con regularidad para mejorar el cumplimiento de los estándares globales. Las operaciones de CRUD en [!DNL Assets] tienen algún grado de accesibilidad integrado en ellas. Los flujos de trabajo de DAM, como la adición, administración, búsqueda y distribución de recursos, son accesibles con la ayuda de métodos abreviados de teclado, texto del lector de pantalla, contraste de color, etc.

## Compatibilidad con el uso del teclado {#keyboard-use}

Muchos elementos de la interfaz de usuario en los que se puede hacer clic o que se pueden llevar a cabo acciones con un puntero también se pueden utilizar con el teclado. Con un teclado, los usuarios pueden centrarse en los elementos de la interfaz de usuario y realizar las acciones adecuadas. Los usuarios pueden utilizar directamente los métodos abreviados de teclado para almacenar en déclencheur un comando o una acción sin tener que centrarse en los elementos de la interfaz de usuario y almacenarlos en déclencheur mediante el teclado. Por ejemplo, los usuarios pueden abrir la cronología de un recurso en el lado izquierdo de la interfaz de usuario navegando hasta el control de interfaz de usuario con un teclado, seleccionando `Return` y `Alt + 2` método abreviado de teclado.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Métodos abreviados de teclado en [!DNL Assets] {#keyboard-shortcuts}

Las siguientes acciones de [!DNL Assets] funcionan con los métodos abreviados de teclado enumerados. La mayoría de los métodos abreviados de teclado que se aplican a las consolas [!DNL Experience Manager] también se aplican a [!DNL Assets]. Consulte [métodos abreviados de teclado para consolas](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte cómo [habilitar o deshabilitar los métodos abreviados de teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaz de usuario o escenario | Métodos abreviados del teclado | Acción |
|---|---|---|
| Vista de columna en la interfaz de usuario [!DNL Assets] | Teclas de flecha arriba y abajo | Navegue hasta archivos y carpetas dentro de la misma jerarquía. |
| Vista de columna en la interfaz de usuario [!DNL Assets] | Teclas de flecha izquierda y derecha | Vaya a los archivos y carpetas que se encuentran por encima o por debajo de la carpeta actual. |
| Explorando carpetas en [!DNL Assets] | `/` | Invoque la búsqueda abriendo el cuadro Omnisearch. |
| Consola [!DNL Assets] | &grave; | Conmutar raíles laterales |
| Consola [!DNL Assets] | `Alt + 1` | Abra el árbol de contenido. |
| Consola [!DNL Assets] | `Alt + 2` | Abra el carril izquierdo de [!UICONTROL Navegación]. |
| Consola [!DNL Assets] | `Alt + 3` | Mostrar [!UICONTROL línea de tiempo] de un recurso seleccionado. |
| Consola [!DNL Assets] | `Alt + 4` | Abra las referencias de Live Copy del recurso seleccionado. |
| Consola [!DNL Assets] | `Alt + 5` | Inicie la búsqueda y busque dentro de la carpeta seleccionada. |
| Se ha seleccionado el recurso o la carpeta | Retroceso | Eliminar el recurso o la carpeta seleccionados. |
| Se ha seleccionado el recurso o la carpeta | `p` | Abra la página Propiedades del recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `e` | Editar el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `m` | Mover el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `Ctrl + c` | Copie el recurso seleccionado. |
| Se ha seleccionado el recurso o la carpeta | `Esc` | Cancelar la selección. |
| Se abre el cuadro de diálogo y está enfocado | `Esc` | Cerrar cuadro de diálogo. |
| Dentro de una carpeta en DAM | `Ctrl + v` | Pegue el recurso copiado. |
| Consola [!DNL Assets] | `Ctrl + A` | Seleccionar todos los recursos. |
| Páginas de propiedades de recursos | `Ctrl + S` | Guardar cambios. |
| Consola [!DNL Assets] | `?` | Consulte una lista de métodos abreviados de teclado. |

## Iniciar sesión y navegar por la interfaz de usuario de [!DNL Assets] {#login}

Los usuarios pueden utilizar el teclado para desplazarse a y rellenar el campo de inicio de sesión para iniciar sesión. Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión los anuncian los lectores de pantalla cada vez que se produce el error.

Después de iniciar sesión, los usuarios de DAM pueden navegar dentro de la interfaz de usuario [!DNL Assets] mediante el teclado. Los elementos de la interfaz de usuario, como el carril izquierdo, los menús, el perfil de usuario, la barra de búsqueda, los archivos y carpetas y las opciones de administración y configuración, se pueden navegar mediante el teclado. El orden de navegación del teclado es de izquierda a derecha y de arriba a abajo. Al navegar con un teclado, una opción procesable cuando está enfocado se resalta con mejor contraste de color y se narra mediante un lector de pantalla. Cuando corresponde, un lector de pantalla anuncia el estado (por ejemplo, expandido, contraído y de estado mixto) de las opciones enfocadas del menú. Además, el lector de pantalla anuncia el propósito de la opción procesable, en lugar de, por ejemplo, la apariencia o la ubicación de la interfaz.

Si un usuario expande la ayuda o la opción de perfil de usuario desde el menú, el lector de pantalla anuncia la opción o el estado correspondientes. Si un usuario amplía la opción de perfil de usuario, las opciones disponibles se pueden seleccionar mediante un teclado. Por ejemplo, un administrador puede suplantar a un usuario diferente. Si un usuario busca una cadena de la opción [!UICONTROL Ayuda], un narrador anuncia &quot;Buscando en la Ayuda&quot; para indicar que hay una búsqueda en curso.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Examinar recursos y ver información relacionada {#browse}

En la interfaz de usuario de [!DNL Assets], los usuarios pueden utilizar el teclado para examinar la lista de recursos digitales existentes en el repositorio de DAM, obtener una vista previa o descargar un recurso, ver representaciones generadas, cambiar vistas, ver las representaciones generadas, ver la cronología y el historial de versiones, ver comentarios y referencias, y ver y administrar metadatos.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Al examinar el repositorio de recursos, la siguiente funcionalidad mejora la accesibilidad:

* El lector de pantalla anuncia alternativas de texto que ilustran el propósito o la funcionalidad de los iconos en lugar de sus nombres.
* Los usuarios pueden acceder a las opciones interactivas de la interfaz de usuario y centrarlas en la lista de recursos Referencias mediante las teclas del teclado.
* Los lectores de pantalla anuncian los elementos de cada fila en la vista de lista como elementos de la misma fila.
* Al navegar con la tecla `Tab`, el enfoque puede moverse a la opción de cierre en la vista previa de la versión.
* Al utilizar el teclado para examinar, las opciones de interfaz de usuario procesables resaltadas tienen un enfoque visual más prominente con un contraste mejorado. Hace que el área enfocada sea más identificable para el usuario.
* El uso de la tecla `Esc` para eliminar los iconos de acción rápida de la vista de miniaturas no elimina el foco del teclado del último elemento centrado.
* Con un recurso seleccionado, al seleccionar `Alt + 4` se abre la lista [!UICONTROL Referencias] en el carril izquierdo. Con la clave `Tab`, los usuarios pueden navegar por las entradas de referencia distintas de cero. Al examinar sólo las entradas de referencia distintas de cero, se ahorra esfuerzo y también las pulsaciones de teclas.
* Los comentarios de un recurso están disponibles en la cronología del recurso. Es accesible si se accede al carril izquierdo mediante un teclado o un método abreviado de teclado.
* Se puede acceder a la [!UICONTROL configuración de vista] en [!DNL Experience Manager] mediante un teclado. Los usuarios pueden desplazarse por los tamaños de tarjeta disponibles mediante las teclas de dirección y seleccionar y tabular para desplazarse por otros elementos de la vista Configuración de vista existente y establecerlos.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Administrar los recursos digitales {#manage-assets}

Muchas tareas de administración de recursos, como las operaciones de CRUD, la descarga de un recurso y la adición de metadatos, son accesibles en varios grados. [!DNL Assets] le permite realizar las tareas utilizando diversas tecnologías de asistencia, como un lector de pantalla y un teclado.

Vea un vídeo de demostración sobre cómo usar un teclado para [examinar el repositorio y descargar un recurso](https://youtu.be/K3dgqMRQJys).

Para las operaciones de metadatos que suelen realizar funciones como especialistas en marketing y administradores, las siguientes funciones mejoran la accesibilidad:

* Ahora se puede acceder a la opción [!UICONTROL Guardar y cerrar] en la página del recurso [!UICONTROL Propiedades] mediante el teclado.
* Los lectores de pantalla anuncian las opciones para eliminar las etiquetas seleccionadas en la pestaña [!UICONTROL Básico] del recurso [!UICONTROL Propiedades].
* Los usuarios pueden utilizar el cuadro de diálogo emergente Selector de fecha con un teclado. El elemento de interfaz de usuario Selector de fecha se utiliza para establecer las horas de activación y desactivación, y seleccionar la fecha.
* La funcionalidad de arrastrar mediante el teclado funciona correctamente en [!UICONTROL Editor de esquemas de metadatos] en el modo de exploración del lector de pantalla.
* Un usuario puede mover el enfoque mediante el teclado al campo Agregar usuario o grupo bajo [!UICONTROL Grupo de usuarios cerrado] en la ficha [!UICONTROL Permisos] de la carpeta [!UICONTROL Propiedades].

## Búsqueda de recursos digitales {#search-assets}

Una experiencia de búsqueda de recursos rápida y perfecta aumenta la velocidad de contenido. Los casos de uso de velocidad de contenido forman parte de la funcionalidad principal [!DNL Assets]. Para iniciar una búsqueda desde la barra Omnisearch, los usuarios pueden usar el método abreviado de teclado `/` o utilizar `Tab` junto con lectores de pantalla para localizar rápidamente la opción de búsqueda. El lector de pantalla narra el nombre de la opción como &quot;Botón de búsqueda&quot; cuando el enfoque está en la opción de búsqueda ![opción de búsqueda](assets/do-not-localize/search_icon.png). Los usuarios pueden seleccionar `Return` para abrir el cuadro Omnisearch. El lector de pantalla no sólo narra la palabra clave escrita en el cuadro de búsqueda, sino también las sugerencias ofrecidas por [!DNL Experience Manager Assets]. Los usuarios pueden usar una combinación de teclas de dirección, `Return` y `Tab` para tener acceso a las distintas opciones para almacenar en déclencheur una búsqueda.

La funcionalidad de búsqueda se hace accesible mediante la siguiente funcionalidad:

* El título de página, disponible para un lector de pantalla, ayuda a identificar la página como página de búsqueda de recursos.
* Los usuarios buscan recursos desde el campo Omnisearch. Los usuarios pueden abrirlo mediante la navegación mediante el teclado o mediante el método abreviado de teclado `/`.
* Los usuarios pueden empezar a escribir la palabra clave de búsqueda y, a continuación, seleccionar las sugerencias automáticas utilizando las teclas de flecha. La sugerencia resaltada se puede seleccionar con la clave `Return` y se buscan los recursos para la sugerencia seleccionada.
* Los lectores de pantalla pueden identificar y anunciar las casillas de verificación de estado mixto (en las que, a menos que seleccione todos los predicados anidados, las casillas de verificación de primer nivel no están seleccionadas y se atraviesan) en el panel Filtros al filtrar los resultados de búsqueda.
* El enfoque del usuario se desplaza a las opciones de búsqueda una vez cerrado el cuadro Omnisearch.

Al filtrar los resultados de búsqueda:

* La página de resultados de búsqueda tiene un título informativo para comprender mejor a los usuarios del lector de pantalla.
* Un lector de pantalla anuncia las opciones en el filtro de búsqueda como acordeones expandibles.
* Los lectores de pantalla anuncian los predicados con opciones de estado mixto.

## Compartir recursos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Al compartir recursos, las siguientes funcionalidades mejoran la accesibilidad:

* Un usuario puede mover el enfoque con el teclado dentro del campo Buscar y agregar dirección de correo electrónico en el cuadro de diálogo de uso compartido de vínculos.

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, los lectores de pantalla,

   * No narre la información de la tabla cuando se carga el cuadro de diálogo.
   * Puede navegar a todas las sugerencias de la lista.
   * Narre las sugerencias mostradas para los campos Añadir dirección de correo electrónico y Buscar.

## Documentación accesible {#accessible-docs}

[!DNL Experience Manager] proporciona documentación accesible para su uso por personas con discapacidades. A continuación, se ayuda a que la oferta de contenido sea accesible por ahora, mientras que Adobe sigue mejorando la plantilla y el contenido:

* Los lectores de pantalla pueden leer el texto.
* Las imágenes e ilustraciones tienen texto alternativo disponible.
* Se puede navegar con el teclado.
* Las relaciones de contraste ayudan a resaltar algunas partes del sitio web de documentación.

## Proporcionar comentarios {#a11y-feedback}

Para proporcionar comentarios, formular preguntas y solicitar mejoras del producto, relacionadas con la accesibilidad, utilice los siguientes métodos:

* Rellene el formulario en [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envíenos un correo electrónico a access@adobe.com.

>[!MORELIKETHIS]
>
>* [Características de accesibilidad en [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de la versión de las mejoras realizadas en cada versión del Service Pack](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] guía de accesibilidad](/help/managing/web-accessibility.md).
>* [Informes de conformidad (ACR) y lista de VPAT para las soluciones de Adobe](https://www.adobe.com/accessibility/compliance.html).
