---
title: 'Creación: el entorno y las herramientas en AEM'
description: El entorno de creación AEM ofrece varios mecanismos para organizar y editar el contenido.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 2a406ca2870e241539819ae62c6a14904ee71211
workflow-type: tm+mt
source-wordcount: '2211'
ht-degree: 47%

---

# Creación: el entorno y las herramientas{#authoring-the-environment-and-tools}

El entorno de creación AEM ofrece varios mecanismos para organizar y editar el contenido. Se puede acceder a las herramientas desde varios editores de páginas y distintas consolas.

## Administración del sitio {#managing-your-site}

La consola **Sites** le permite navegar y administrar su sitio web mediante la barra de encabezado, la barra de herramientas, los iconos de acción (aplicables al recurso seleccionado), las rutas de exploración y, cuando se seleccionan, los carriles secundarios (por ejemplo, referencias y cronología).

Por ejemplo, la vista de columna:

![ateat-01](assets/ateat-01.png)

## Edición del contenido de una página {#editing-page-content}

Puede editar una página con el editor de páginas. Por ejemplo:

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>La primera vez que abre una página para editarla, una serie de diapositivas le ofrecen un recorrido por las características.
>
>Si lo desea, puede omitir el recorrido y repetirlo en cualquier momento seleccionando una de las opciones del menú **Información de página**.

## Acceso a la Ayuda   {#accessing-help}

Al editar una página, se puede acceder a la **Ayuda** desde los siguientes puntos:

* el selector [**Información de la página**](/help/sites-authoring/editing-page-properties.md#page-properties); muestra las diapositivas introductorias (tal y como se muestran la primera vez que se accede al editor).
* el diálogo [configuración](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) para componentes específicos (usando el signo de interrogación (?) en la barra de herramientas del cuadro de diálogo); esto muestra la Ayuda contextual.

Encontrará [más recursos relacionados con la ayuda en las consolas](/help/sites-authoring/basic-handling.md#accessing-help).

## Navegador de componentes   {#components-browser}

El navegador de componentes muestra todos los componentes que se pueden utilizar en la página actual. Se pueden arrastrar a la ubicación adecuada y editarse para añadir contenido.

El navegador de componentes es una pestaña del panel lateral (junto con el [explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser) y el [árbol de contenido](/help/sites-authoring/author-environment-tools.md#content-tree)). Para abrir (o cerrar) el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![ateat-03](assets/ateat-03.png)

Cuando abra el panel lateral, se deslizará para abrirse de izquierda a derecha (seleccione la pestaña **Componentes** si es necesario). Al abrirla, puede examinar todos los componentes disponibles para su página.

El aspecto y el control dependerán del tipo de dispositivo que utilice:

>[!NOTE]
>
>Se detectará un dispositivo móvil si la anchura es inferior a 1024 píxeles. Este también puede ser el caso de una pequeña ventana de escritorio.

* **Dispositivo móvil (por ejemplo, iPad)**

  El explorador de componentes cubre completamente la página que se está editando.

  Para añadir un componente a la página, pulse y mantenga pulsado el componente necesario y muévalo hacia la derecha (el navegador de componentes se cierra para volver a mostrar la página), donde podrá colocar el componente.

  ![ateat-04](assets/ateat-04.png)

* **Dispositivo de escritorio**

  El explorador de componentes se abre en la parte izquierda de la ventana.

  Para añadir un componente a la página, haga clic en el componente necesario y arrástrelo a la ubicación que desee.

  ![ateat-05](assets/ateat-05.png)

  Los componentes se representan mediante los siguientes elementos:

   * Nombre del componente
   * Grupo de componentes (en gris)
   * Icono o abreviatura

      * Los iconos de los componentes estándar son monocromos.
      * Las abreviaturas siempre están formadas por los dos primeros caracteres del nombre del componente.

  Desde la barra de herramientas superior del explorador **Components**, puede hacer lo siguiente:

   * Filtrar componentes por su nombre.
   * Restringir la visualización a un grupo específico mediante la selección desplegable.

  Para obtener una descripción más detallada del componente, puede hacer clic en el icono de información situado junto al componente en el explorador **Componentes** (si está disponible). Por ejemplo, para el **contenedor de diseños**:

  ![ateat-06](assets/ateat-06.png)

  Para obtener más información sobre los componentes disponibles, consulte [Consola de componentes](/help/sites-authoring/default-components-console.md).

## Navegador de recursos {#assets-browser}

El explorador de recursos muestra todos los [recursos](/help/assets/assets.md) que se pueden utilizar directamente en la página actual.

El navegador de recursos es una pestaña del panel lateral junto con [el navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser)r y el [árbol de contenido](/help/sites-authoring/author-environment-tools.md#content-tree). Para abrir o cerrar el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![ateat-03-1](assets/ateat-03-1.png)

Cuando abra el panel lateral, se deslizará para abrirse de izquierda a derecha. Seleccione la ficha **Assets** si es necesario.

![ateat-07](assets/ateat-07.png)

Cuando se abre el explorador de recursos, puede examinar todos los recursos disponibles para la página. Si es necesario, puede utilizar el desplazamiento indefinido para ampliar la lista.

![ateat-08](assets/ateat-08.png)

Para añadir un recurso a la página, selecciónelo y arrástrelo a la ubicación deseada. Esto puede ser lo siguiente:

* Un componente existente del tipo adecuado.

   * Por ejemplo, puede arrastrar un recurso de tipo imagen hacia un componente de imagen.

* Un [marcador de posición](/help/sites-authoring/editing-content.md#component-placeholder) en el sistema de párrafos para crear un componente del tipo apropiado.

   * Por ejemplo, puede arrastrar un recurso de tipo imagen al sistema de párrafos para crear un componente de imagen.

>[!NOTE]
>
>Esta opción está disponible para determinados tipos de recursos y componentes. Consulte [Inserción de un componente con el explorador de recursos](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser) para obtener más información.

Desde la barra de herramientas superior del explorador de recursos, puede filtrar los recursos por lo siguiente:

* Nombre
* Ruta
* Tipo de recurso, como imágenes, manuscritos, documentos, vídeos, páginas, párrafos y productos
* Características del recurso como Orientación (vertical, horizontal, cuadrado) y Estilo (color, monocromo, escala de grises)

   * Disponible solo para determinados tipos de recursos

El aspecto y el control dependerán del tipo de dispositivo que utilice:

>[!NOTE]
>
>Se detecta un dispositivo móvil cuando la anchura sea menor a 1024 píxeles; es decir, también cuando la ventana de escritorio sea pequeña.

* **Dispositivo móvil como iPad**

  El explorador de recursos cubre completamente la página que se está editando.

  Para añadir un recurso a su página, toque y mantenga presionado el recurso necesario y, a continuación, muévalo hacia la derecha: el explorador de recursos se cerrará para mostrar de nuevo la página, donde puede añadir el recurso al componente requerido.

  ![ateat-09](assets/ateat-09.png)

* **Dispositivo de escritorio**

  El explorador de recursos se abre en la parte izquierda de la ventana.

  Para agregar un recurso a su página, haga clic en el recurso y arrástrelo a la ubicación o componente necesarios.

  ![ateat-10](assets/ateat-10.png)

Si debe cambiar rápidamente un recurso, puede iniciar [Editor de recursos](/help/assets/manage-assets.md) directamente desde el explorador de recursos haciendo clic en el icono de edición que se muestra al lado del nombre del recurso.

![Dispositivo de escritorio para navegador Assets](do-not-localize/screen_shot_2018-03-22at142448.png)

## Árbol de contenido {#content-tree}

El **Árbol de contenido** proporciona una descripción general de todos los componentes de la página en una jerarquía para que pueda ver de un vistazo cómo está compuesta la página.

El árbol de contenido es una pestaña del panel lateral (junto con el explorador de recursos y componentes). Para abrir o cerrar el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![Árbol de contenido](do-not-localize/screen_shot_2018-03-22at142042.png)

Cuando abra el panel lateral, se deslizará para abrirse (de izquierda a derecha). Seleccione la pestaña **Árbol de contenido** si es necesario. Cuando se abre, puede ver una representación de vista de árbol de la página o plantilla, de modo que sea más fácil comprender cómo se estructura jerárquicamente su contenido. Además, en una página compleja, resulta más fácil saltar entre los componentes de la página.

![ateat-11](assets/ateat-11.png)

Una página puede estar compuesta fácilmente por muchos componentes del mismo tipo, por lo que el árbol de contenido (componentes) muestra un texto descriptivo (en gris) después del nombre del tipo de componente (en negro). El texto descriptivo viene de las propiedades comunes del componente, como el título o el texto.

Los tipos de componente se muestran en el idioma del usuario, mientras que el texto de descripción del componente proviene del idioma de la página.

Al hacer clic en las comillas angulares junto a un componente, se contrae o se expande ese nivel.

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>Si edita una página en un dispositivo móvil, el árbol de contenido no está disponible (si el valor de la anchura del explorador es inferior a 1024 píxeles).

Al hacer clic en el componente, se resalta el componente en el editor de páginas. Las acciones disponibles dependen del estado de la página:

* Por ejemplo, una página básica:

  `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

  ![ateat-12](assets/ateat-12.png)

  Si el componente en el que hace clic en el árbol es editable, aparece un icono de llave inglesa a la derecha del nombre. Al hacer clic en este icono, se abre el cuadro de diálogo de edición del componente.

  ![Icono de llave inglesa - Editar](do-not-localize/screen_shot_2018-03-22at142725.png)

* O una página que forma parte de [livecopy](/help/sites-administering/msm.md), donde los componentes se heredan de otra página; por ejemplo:

  `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

  ![ateat-13](assets/ateat-13.png)

## Fragmentos: navegador de contenido asociado {#fragments-associated-content-browser}

Si su página contiene fragmentos de contenido, tendrá acceso al [explorador de contenido asociado](/help/sites-authoring/content-fragments.md#using-associated-content).

## Referencias {#references}

**Referencias** muestran conexiones a la página seleccionada:

* Planes
* Lanzamientos
* Live Copies
* Copias de idioma
* Vínculos entrantes
* Utilización del componente de referencia: contenido prestado

Abra la consola en cuestión, desplácese hasta el recurso y abra **Referencias** con el procedimiento siguiente:

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[Seleccione el recurso necesario](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) muestra una lista de tipos de referencias relevantes para ese recurso:

![ateat-22](assets/ateat-22.png)

Seleccione el tipo de referencia adecuado para obtener más información. En determinadas situaciones, hay disponibles más acciones al seleccionar una referencia específica, como:

* **Vínculos entrantes** proporciona una lista de páginas que hacen referencia a la página, así como acceso directo a **Editar** una de esas páginas cuando selecciona un vínculo específico.

   * Esto solo puede mostrar vínculos estáticos, no vínculos generados dinámicamente; por ejemplo, desde el componente Lista.

* Instancias de contenido prestado mediante el componente de **referencia**; desde aquí puede navegar hasta la página de referencia o a la que se hace referencia

* [Lanzamientos](/help/sites-authoring/launches.md) proporciona acceso a lanzamientos relacionados.
* [Live Copies](/help/sites-administering/msm.md) muestra las rutas de todas las Live Copies que se basan en el recurso seleccionado.
* [Modelo](/help/sites-administering/msm-best-practices.md) proporciona detalles y diversas acciones.
* [Copias de idiomas](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel) proporciona detalles y diversas acciones.

Por ejemplo, se puede corregir una referencia rota dentro de un componente Referencia:

![ateat-14](assets/ateat-14.png)

## Eventos: línea de tiempo {#events-timeline}

Para obtener los recursos adecuados (por ejemplo, páginas de la consola **Sitios** o activos de la consola **Activos**) se [puede utilizar la cronología para mostrar la actividad reciente de cualquier elemento seleccionado](/help/sites-authoring/basic-handling.md#timeline).

Abra la consola en cuestión, desplácese hasta el recurso y abra **Cronología** con el procedimiento siguiente:

![ateat-15](assets/ateat-15.png)

[Seleccione el recurso en cuestión](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) mediante **Mostrar todo** o **Actividades** para enumerar las acciones recientes en los recursos seleccionados:

![ateat-16](assets/ateat-16.png)

## Información de la página {#page-information}

El botón Información de página (icono de ecualizador) abre un menú que también proporciona detalles sobre la última edición y la última publicación. En función de las características de la página, del sitio y de su instancia, habrá más o menos opciones disponibles:

![ateat-17](assets/ateat-17.png)

* [Abrir propiedades](/help/sites-authoring/editing-page-properties.md)
* [Desplegar página](/help/sites-administering/msm.md#msm-from-the-ui)
* [Iniciar flujo de trabajo](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [Bloquear página](/help/sites-authoring/editing-content.md#locking-a-page)
* [Publicar página](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [Cancelar la publicación de la página](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [Editar plantilla](/help/sites-authoring/templates.md); cuando la página está basada en una [plantilla editable](/help/sites-authoring/templates.md#editable-and-static-templates)

* [Ver como aparece publicado](/help/sites-authoring/editing-content.md#view-as-published)
* Ver en Administración; abre la página en la [consola Sitios](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [Ayuda](/help/sites-authoring/basic-handling.md#accessing-help)

Por ejemplo, cuando sea apropiado, **Información de la página** también tiene las opciones:

* [Promocionar lanzamiento](/help/sites-authoring/launches-promoting.md) si la página es un lanzamiento
* [Abrir en la interfaz de usuario clásica](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) si un administrador habilitó esta opción [3&rbrace;](/help/sites-administering/enable-classic-ui-editor.md)

Además, **Información de página** puede proporcionar acceso a análisis y recomendaciones, cuando proceda.

## Modos de página   {#page-modes}

Al editar una página existen varios modos que permiten realizar diferentes acciones:

* [Editar](/help/sites-authoring/editing-content.md): utilice este modo al editar el contenido de la página.
* [Diseño](/help/sites-authoring/responsive-layout.md): permite crear y editar su diseño interactivo en función del dispositivo (si la página está basada en un contenedor de diseños)

* [Desarrollador](/help/sites-developing/developer-mode.md): permite realizar diversas acciones (requiere privilegios). Estos incluyen la inspección de los detalles técnicos de una página y sus componentes.

* [Diseño](/help/sites-authoring/default-components-designmode.md): permite habilitar o deshabilitar componentes para usarlos en una página y configurar el diseño del componente (si la página está basada en una [plantilla estática](/help/sites-authoring/templates.md#editable-and-static-templates)).

* [Segmentación:](/help/sites-authoring/content-targeting-touch.md) aumente la relevancia del contenido mediante la segmentación y efectuando mediciones en todos los canales.
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor): muestra datos de Analytics para la página.

* [Deformación de tiempo](/help/sites-authoring/working-with-page-versions.md#timewarp): le permite ver el estado de una página en un momento determinado.
* [Estado de Live Copy](/help/sites-authoring/editing-content.md#live-copy-status): permite echar un vistazo rápido al estado de la Live Copy y de los componentes que se han heredado o no.
* [Vista previa](/help/sites-authoring/editing-content.md#previewing-pages): se utiliza para ver la página tal como se muestra en el entorno de publicación o para navegar mediante vínculos en el contenido. 

* [Anotar:](/help/sites-authoring/annotations.md) se utiliza para añadir o ver anotaciones en la página.

Puede acceder a ellas mediante los iconos de la esquina superior derecha. El icono cambia para reflejar el modo que está utilizando actualmente:

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* Según las características de la página, es posible que algunos modos no estén disponibles.
>* El acceso a algunos modos requiere los permisos o privilegios adecuados.
>* El modo de desarrollador no está disponible en dispositivos móviles debido a las restricciones de espacio.
>* Hay un [método abreviado de teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) (`Ctrl-Shift-M`) para alternar entre **Vista previa** y el modo seleccionado actualmente (por ejemplo, **Editar** y **Diseño**).
>

## Selección de la ruta {#path-selection}

A menudo, durante la creación es necesario seleccionar otro recurso, como al definir un vínculo a otra página o recurso o al seleccionar una imagen. Para poder seleccionar una ruta con facilidad, los [campos de ruta](/help/sites-authoring/author-environment-tools.md#path-fields) ofrecen la opción de completado automático y el [explorador de rutas](/help/sites-authoring/author-environment-tools.md#path-browser) permite una selección más sólida.

### Campos de rutas   {#path-fields}

El ejemplo que se utiliza aquí a modo de ilustración se corresponde con el componente de imagen. Para obtener más información acerca de cómo usar y editar componentes, vea [Componentes para la creación de páginas](/help/sites-authoring/default-components.md).

Los campos de rutas de acceso disponen de las funciones de completado automático y de predicción de texto para que la localización de recursos resulte más sencilla.

Al hacer clic en el botón **Abrir cuadro de diálogo de selección**, en el campo de rutas de acceso se abrirá el cuadro de diálogo del [navegador de rutas de acceso](/help/sites-authoring/author-environment-tools.md#path-browser), en el que dispondrá de opciones de selección más detalladas.

![Abrir cuadro de diálogo de selección](do-not-localize/screen_shot_2018-03-22at154427.png)

También puede empezar a escribir en el campo de ruta y AEM ofrece rutas coincidentes a medida que escribe.

![ateat-19](assets/ateat-19.png)

### Navegador de rutas {#path-browser}

El navegador de rutas está organizado como la [vista de columna](/help/sites-authoring/basic-handling.md#column-view) de la consola Sitios, lo que permite efectuar una selección más detallada de los recursos.

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* Una vez seleccionado un recurso, el botón **Seleccionar** en la parte superior derecha del cuadro de diálogo se activa. Haga clic para confirmar la selección o en **Cancelar** para cancelar.
* Si el contexto permite la selección de varios recursos, al seleccionar un recurso también se activa el botón **Seleccionar**, pero también se agrega un recuento del número de recursos seleccionados a la esquina superior derecha de la ventana. Haga clic en **X** junto al número para anular toda la selección.
* Al navegar por el árbol, su ubicación se refleja en las rutas de exploración en la parte superior del cuadro de diálogo. Estas rutas de exploración también se pueden utilizar para saltar rápidamente dentro de la jerarquía de recursos.
* En cualquier momento, puede utilizar el campo de búsqueda en la parte superior del cuadro de diálogo. Haga clic en **X** en el campo de búsqueda para borrar la búsqueda.
* Para limitar la búsqueda, puede mostrar las opciones de filtro y filtrar los resultados en función de una ruta determinada.

  ![ateat-21](assets/ateat-21.png)

## Métodos abreviados de teclado {#keyboard-shortcuts}

Hay varios [métodos abreviados del teclado](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) disponibles.
