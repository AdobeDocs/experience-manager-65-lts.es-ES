---
title: Edición del contenido de página
description: El contenido se añade mediante componentes que se pueden arrastrar hasta la página. Después estos se pueden editar local, mover o eliminar.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 1a942dc471cde14fa3b811b31e54644e199f8738
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 16%

---

# Edición del contenido de una página{#editing-page-content}

Después de crear una página (nueva o como parte de un lanzamiento o Live Copy), puede editar el contenido para realizar las actualizaciones que requiera.

El contenido se añade empleando los [componentes](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) (según el tipo de contenido) que pueden arrastrarse a la página. Después estos se pueden editar local, mover o eliminar.

>[!NOTE]
>
>Su cuenta necesita los [derechos de acceso apropiados](/help/sites-administering/security.md) y [permisos](/help/sites-administering/security.md#permissions) para editar páginas; por ejemplo, agregar, editar o eliminar componentes, anotar o desbloquear.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

## Sidekick {#sidekick}

La barra de tareas es una herramienta clave al crear páginas. Flota al crear una página, por lo que siempre es visible.

Hay varias pestañas e iconos disponibles, entre ellos:

* Componentes
* Página
* Información
* Versiones
* Flujo de trabajo
* Modos
* Andamiaje
* Client Context
* Sitios web

![chlimage_1-71](assets/chlimage_1-71.png)

Estos proporcionan acceso a una amplia selección de funcionalidades, entre las que se incluyen:

* [selección de componentes](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [mostrar referencias](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [acceso al registro de auditoría](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [modos de conmutación](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [creando](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), [restaurando](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) y [comparando](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) versiones

* [publicando](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page), [cancelando la publicación](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) de una página

* [editar propiedades de página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [andamiaje](classic-feature-scaffolding.md)

* [Client Context](/help/sites-administering/client-context.md)

## Insertar un componente {#inserting-a-component}

### Insertar un componente {#inserting-a-component-1}

Después de abrir la página, puede empezar a agregar contenido. Para ello, agregue componentes (también denominados párrafos).

Para insertar un componente nuevo:

1. Existen varios métodos para seleccionar el tipo de párrafo que desea insertar:

   * Haga doble clic en el área denominada **Arrastre componentes o recursos aquí...**: se abre la barra de herramientas **Insertar nuevo componente**. Seleccione un componente y haga clic en **Aceptar**.

   * Arrastre un componente desde la barra de herramientas flotante (denominada barra de tareas) para insertar un nuevo párrafo.
   * Haga clic con el botón derecho en un párrafo existente y seleccione **Nuevo...**: se abrirá la barra de herramientas Insertar nuevo componente. Seleccione un componente y haga clic en **Aceptar**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. Tanto en la barra de tareas como en la barra de herramientas **Insertar nuevo componente**, verá una lista de los componentes disponibles (tipos de párrafo). Se pueden dividir en varias secciones (por ejemplo, General, Columnas, etc.), que se pueden expandir según sea necesario.

   Según el entorno de producción, estas opciones pueden diferir. Para obtener información detallada sobre los componentes, consulte [Componentes predeterminados](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. Inserte el componente que desee en la página. A continuación, haga doble clic en el párrafo y se abrirá una ventana que le permitirá configurar el párrafo y añadir contenido.

### Inserción de un componente mediante el buscador de contenido {#inserting-a-component-using-the-content-finder}

También puede agregar un componente nuevo a la página arrastrando un recurso desde el [Buscador de contenido](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). Esto crea automáticamente un componente del tipo adecuado que contiene el recurso.

Esto es válido para los siguientes tipos de recursos (algunos dependerán del sistema de páginas o párrafos):

| Tipo de recurso | Tipo de componente resultante |
|---|---|
| Imagen | Imagen |
| Documento | Descargar |
| Producto | Producto |
| Vídeo | Flash |

>[!NOTE]
>
>Puede configurar este comportamiento en su instalación. Consulte [Configuración de un sistema de párrafos para que, al arrastrar un recurso, se cree una instancia de componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) para obtener más información.

Para crear un componente arrastrando uno de los tipos de activo anteriores:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
1. Abra [Buscador de contenido](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. Arrastre el recurso en cuestión hasta la posición deseada. El [marcador de posición de componente](#componentplaceholder) le muestra dónde se colocará el componente.

   Se creará un componente, adecuado para el tipo de recurso, en la ubicación requerida; contendrá el recurso seleccionado.

1. [Editar](#editmovecopypastedelete) el componente si es necesario.

## Edición de un componente (contenido y propiedades) {#editing-a-component-content-and-properties}

Para editar un párrafo existente, realice una de las siguientes acciones:

* **Haga doble clic** en el párrafo para abrirlo. Verá la misma ventana que cuando creó el párrafo con el contenido existente. Realice los cambios y haga clic en **Aceptar**.

* **Haga clic con el botón derecho** en el párrafo y haga clic en **Editar**.

* **Haga clic** dos veces en el párrafo (un doble clic lento) para entrar al modo de edición local. Podrá editar directamente el texto de la página, en lugar de hacerlo desde una ventana de diálogo. En este modo, se le proporcionará una barra de herramientas en la parte superior de la página. Simplemente realice los cambios y se guardarán automáticamente.

## Mover un componente {#moving-a-component}

Para mover un párrafo:

>[!NOTE]
>
>También puede utilizar [Cortar y pegar](#cut-copy-paste-a-component) para mover un componente.

1. Seleccione el párrafo que desea mover:

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. Arrastre el párrafo a la nueva ubicación: AEM indica a dónde se puede mover el párrafo con una marca de verificación verde. Colóquelo en la ubicación que desee.
1. Se mueve el párrafo:

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## Eliminación de un componente {#deleting-a-component}

Para eliminar un párrafo:

1. Seleccione el párrafo y **haga clic con el botón secundario**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. Seleccione **Eliminar** en el menú. AEM WCM solicita confirmación para eliminar el párrafo, ya que esta acción no se puede deshacer.
1. Haga clic en **OK**.

>[!NOTE]
>
>Si ha configurado las propiedades de [usuario para que muestren la barra de herramientas de edición global](/help/sites-classic-ui-authoring/author-env-user-props.md), también puede realizar ciertas acciones en los párrafos usando los botones **Copiar**, **Cortar**, **Pegar**, **Eliminar** disponibles.
>
>También hay varios [métodos abreviados de teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) disponibles.

## Cortar/copiar/pegar un componente {#cut-copy-paste-a-component}

Al igual que cuando [Eliminando un componente](#deleting-a-component), puede utilizar el menú contextual para copiar, cortar o pegar un componente

>[!NOTE]
>
>Si ha configurado las propiedades de [usuario para que muestren la barra de herramientas de edición global](/help/sites-classic-ui-authoring/author-env-user-props.md), también puede realizar ciertas acciones en los párrafos usando los botones **Copiar**, **Cortar**, **Pegar**, **Eliminar** disponibles.
>
>También hay varios [métodos abreviados de teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) disponibles.

>[!NOTE]
>
>Cortar, copiar y pegar contenido solo es compatible dentro de la misma página.

## Componentes heredados {#inherited-components}

Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios](/help/sites-administering/msm.md); también en combinación con [andamiaje](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [Inicios](/help/sites-classic-ui-authoring/classic-launches.md) (cuando se basan en Live Copy).
* Componentes específicos; por ejemplo, el sistema de párrafos heredado en Geometrixx.

Puede cancelar (y volver a habilitar) la herencia. Según el componente, esto puede estar disponible en:

1. **Live Copy**

   Si un componente forma parte de una Live Copy o un lanzamiento, se indica mediante un icono de candado. Puede hacer clic en el candado para cancelar la herencia.

   * El icono de candado se muestra cuando se selecciona el componente; por ejemplo:

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * El candado también se muestra en el cuadro de diálogo de componentes; por ejemplo:

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **Un Sistema De Párrafos Heredado**

   El cuadro de diálogo Configuración. Por ejemplo, como con el sistema de párrafos heredados en Geometrixx:

   ![chlimage_1-74](assets/chlimage_1-74.png)

## Agregar anotaciones {#adding-annotations}

[Anotaciones](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) permiten que otros autores proporcionen comentarios sobre tu contenido. Esto se utiliza a menudo con fines de revisión y validación.

## Previsualizar páginas {#previewing-pages}

Hay dos iconos en el borde inferior de la barra de tareas que son importantes para obtener una vista previa de las páginas:

![Borde inferior de la barra de tareas con una fila horizontal de siete iconos. Dos de los iconos al principio de la fila, el icono de edición y el icono de modo de vista previa, se indican mediante un símbolo de lápiz y un símbolo de lupa, respectivamente.](do-not-localize/chlimage_1-5.png)

* El icono de lápiz le muestra que está actualmente en modo de edición, donde puede agregar, modificar, mover o eliminar contenido.

  ![Editar icono indicado por un símbolo de lápiz.](do-not-localize/chlimage_1-6.png)

* El icono de lupa le permite seleccionar el modo de vista previa en el que la página se muestra tal y como se verá en el entorno de publicación (a veces también es necesario actualizar la página):

  ![Icono de modo de vista previa indicado por un símbolo de lupa.](do-not-localize/chlimage_1-7.png)

  En el modo de vista previa, se reducirá la barra de tareas y haga clic en el icono de flecha abajo para volver al modo de edición:

  ![Barra con AEM como título y un icono de modo de edición a la derecha del título indicado por un símbolo de flecha hacia abajo.](do-not-localize/chlimage_1-8.png)

## Buscar y reemplazar {#find-replace}

Para ediciones a mayor escala de la misma frase, una opción de menú **[Buscar y reemplazar](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** le permite buscar y reemplazar varias instancias de una cadena, dentro de una sección del sitio web.

## Bloquear una página   {#locking-a-page}

AEM le permite bloquear páginas para que nadie más pueda cambiar su contenido. Esto resulta útil cuando realiza varias ediciones en una página específica o cuando necesita congelar una página durante un corto tiempo.

>[!CAUTION]
>
>El bloqueo de páginas debe utilizarse con cuidado, ya que la única persona que puede desbloquear una página es la persona que la bloqueó (o una cuenta con privilegios de administrador).

Para bloquear una página:

1. En la ficha **Sitios web**, seleccione la página que desee bloquear.
1. Haga doble clic en la página para abrirla y editarla.
1. En la ficha **Página** de la barra de tareas, seleccione **Bloquear página**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   Aparece un mensaje que indica que la página está bloqueada para otros usuarios. Además, en el panel derecho de la consola **Sitios web**, AEM WCM muestra la página como bloqueada e indica qué usuario la ha bloqueado.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## Desbloquear una página {#unlocking-a-page}

Para desbloquear una página:

1. En la ficha **Sitios web**, seleccione la página que desee desbloquear.
1. Haga doble clic en la página para abrirla.
1. En la ficha **Página** de la barra de tareas, seleccione **Desbloquear página**.

## Deshacer y rehacer modificaciones de páginas {#undoing-and-redoing-page-edits}

Utilice los siguientes métodos abreviados del teclado mientras el marco de contenido de la página está seleccionado:

* Deshacer: Ctrl+Z (Windows) o Cmd+Z (Mac)
* Rehacer: Ctrl+Y (Windows) o Cmd+Y (Mac)

Al deshacer o rehacer la eliminación, adición o reubicación de uno o más párrafos, los resaltados parpadeantes (comportamiento predeterminado) indican los párrafos afectados.

>[!NOTE]
>
>Consulte [Deshacer y rehacer ediciones de página: la teoría](#undoing-and-redoing-page-edits-the-theory) para ver toda la información sobre las posibilidades de deshacer y rehacer ediciones de página.

## Deshacer y rehacer ediciones de página: la teoría {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>El administrador del sistema puede [configurar varios aspectos de las características Deshacer/Rehacer](/help/sites-administering/config-undo.md) según los requisitos de la instancia.

AEM almacena un historial de las acciones que realiza y la secuencia en que las realizó. Por lo tanto, deshace varias acciones en el orden en que las realizó. A continuación, puede utilizar rehacer para volver a aplicar una o varias acciones.

Si hay un elemento seleccionado en la página de contenido, el comando Deshacer y Rehacer se aplica al elemento seleccionado, como un componente de texto.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas de software. Utilice los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si, a continuación, decide volver a mover el párrafo, utilice el comando Rehacer.

>[!NOTE]
>
>Puede hacer lo siguiente:
>
>* rehacer acciones siempre que no haya realizado una edición de página desde que utilizó deshacer.
>* deshacer un máximo de 20 acciones de edición (configuración predeterminada).
>* use también [métodos abreviados de teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) para deshacer y rehacer.
>

Puede usar los comandos Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Añadir, editar, quitar y mover párrafos
* Editar contenido de párrafos in-situ
* Copiar, cortar y pegar elementos en una página
* Copiar, cortar y pegar elementos en las páginas
* Agregar, quitar y cambiar archivos e imágenes
* Adición, eliminación y cambio de anotaciones y bocetos
* Cambios en el andamiaje
* Adición y eliminación de referencias
* Cambiar valores de propiedad en cuadros de diálogo de componentes.

Los campos de formulario que representan los componentes de formulario no están pensados para tener valores especificados durante la creación de páginas. Por lo tanto, los comandos Deshacer y Rehacer no afectan a los cambios realizados en los valores de esos tipos de componentes. Por ejemplo, no se puede deshacer la selección de un valor en una lista desplegable.

>[!NOTE]
>
>Se requieren permisos especiales para deshacer y rehacer cambios en archivos e imágenes. Además, el historial de deshacer para cambios en archivos e imágenes dura un mínimo de horas. No obstante, pasado ese tiempo, no se garantiza que se puedan deshacer los cambios. El administrador puede proporcionar permisos y cambiar el tiempo predeterminado de diez horas.
