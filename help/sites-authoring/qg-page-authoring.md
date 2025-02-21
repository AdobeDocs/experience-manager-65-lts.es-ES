---
title: Guía rápida para la creación de páginas
description: Una guía rápida y de alto nivel sobre las acciones clave para crear contenido de página
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 61%

---

# Guía rápida para la creación de páginas{#quick-guide-to-authoring-pages}

Estos procedimientos están pensados como una guía rápida (de alto nivel) para las acciones clave de la creación de contenido de página en AEM.

Estos procedimientos:

* No están pensados como una cobertura completa.
* Proporcione vínculos a la documentación detallada.

Para obtener más información sobre la creación con AEM, consulte:

* [Primeros pasos para los autores](/help/sites-authoring/first-steps.md)
* [Creación de páginas](/help/sites-authoring/page-authoring.md)

## Algunas sugerencias rápidas {#a-few-quick-hints}

Antes de dar la descripción general de los detalles específicos, aquí hay una pequeña colección de sugerencias generales que vale la pena tener en cuenta.

### Consola Sites {#sites-console}

* **Crear**

   * Este botón está disponible en muchas consolas. Las opciones presentadas son sensibles al contexto, por lo que pueden variar en función del escenario.

* Reordenación de páginas en una carpeta

   * Esto se puede hacer en [Vista de lista](/help/sites-authoring/basic-handling.md#list-view). Los cambios se aplican y son visibles en otras vistas.

#### Creación de páginas {#page-authoring}

* Vínculos de navegación 

   * ***Los vínculos no están disponibles para la navegación*** cuando esté en el modo **Editar**. Para navegar con vínculos, debe [obtener una vista previa de la página](/help/sites-authoring/editing-content.md#previewing-pages) mediante:

      * [Modo de vista previa](/help/sites-authoring/editing-content.md#preview-mode)
      * [Ver como aparece publicado](/help/sites-authoring/editing-content.md#view-as-published)

* Las versiones no se inician ni se crean desde el editor de páginas; ahora se realiza desde la consola Sitios (a través de **Crear** o [Cronología](/help/sites-authoring/basic-handling.md#timeline) para un recurso seleccionado).

>[!NOTE]
>
>Existen varios métodos abreviados del teclado que pueden facilitar la experiencia de creación.
>
>* [Métodos abreviados del teclado al editar páginas](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Métodos abreviados del teclado para las consolas](/help/sites-authoring/keyboard-shortcuts.md)
>

### Encontrar su página {#finding-your-page}

Existen varios aspectos para encontrar una página; puede navegar o buscar:

1. Abra la consola **Sitios** (con la opción **Sitios** en [Navegación global](/help/sites-authoring/basic-handling.md#global-navigation)); esto se activa (menú desplegable) al seleccionar el vínculo de Adobe Experience Manager (parte superior izquierda).

1. Desplácese hacia abajo en el árbol tocando o haciendo clic en la página correspondiente. La manera en que se representan los recursos de la página depende de la vista que utilice: [Tarjeta, Lista o Columna](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Desplácese hacia arriba del árbol mediante [la ruta de exploración del encabezado](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs), que le permite volver a la ubicación seleccionada:

   ![qgtap-01](assets/qgtap-01.png)

1. También puede [buscar](/help/sites-authoring/search.md) una página. Puede seleccionar la página en los resultados que se muestran.

   ![qgtap-03](assets/qgtap-03.png)

### Creación de una nueva página {#creating-a-new-page}

Para [crear una página](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Vaya a la ubicación](#finding-your-page) donde desea crear la página.
1. Utilice el icono **Crear** y luego seleccione **Página** en la lista:

   ![qgtap-02](assets/qgtap-02.png)

1. Se abre el asistente que le guiará a través de la recopilación de la información necesaria cuando [cree su nueva página](/help/sites-authoring/managing-pages.md#creating-a-new-page). Siga las instrucciones que aparecen en pantalla.

### Seleccionar su página para ejecutar acciones adicionales   {#selecting-your-page-for-further-action}

Puede seleccionar una página para poder realizar acciones en ella. Si se selecciona una página, se actualizará automáticamente la barra de herramientas para que se muestren las acciones relevantes para ese recurso.

La forma de seleccionar una página depende de la vista que utilice en la consola:

1. Vista de columna:

   * Haga clic en la miniatura del recurso en cuestión: la miniatura mostrará una marca de verificación para indicar que se ha seleccionado.

1. Vista en lista:

   * Haga clic en la miniatura del recurso en cuestión: la miniatura mostrará una marca de verificación para indicar que se ha seleccionado.

1. Vista de tarjeta:

   * Especifique el modo de selección [seleccionando el recurso necesario](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) con:

      * Dispositivo móvil: seleccionar y mantener presionado
      * Escritorio: [acción rápida](/help/sites-authoring/basic-handling.md#quick-actions) - icono de marcar:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * En la tarjeta se superpondrá una marca de verificación que indica que se ha seleccionado la página.

   >[!NOTE]
   >
   >Una vez en el modo de selección, el icono **Seleccionar** (una marca de verificación) cambiará al icono **Anular la selección** (una cruz).

### Acciones rápidas (solo vista de tarjeta y escritorio) {#quick-actions-card-view-desktop-only}

Hay [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions) disponibles:

1. [Desplácese hasta la página](#finding-your-page) sobre la que quiera llevar a cabo una acción.
1. Pase el puntero del ratón sobre la tarjeta que representa el recurso necesario; se muestran las acciones rápidas:

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Edición del contenido de la página {#editing-your-page-content}

1. [Desplácese hasta la página](#finding-your-page) que quiera editar.
1. [Abra la página que quiera editar](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) con el icono Editar (lápiz):

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   Puede acceder desde:

   * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
   * La barra de herramientas cuando [su página se haya seleccionado](#selectiingyourpageforfurtheraction).

1. Cuando se abre el editor, puede:

   * [Añadir un componente nuevo a su página](/help/sites-authoring/editing-content.md#inserting-a-component) mediante las siguientes opciones:

      * apertura del panel lateral
      * seleccionar la ficha componentes (el [explorador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser))
      * arrastre el componente requerido a la página.

     El panel lateral se puede abrir (y cerrar) con:

     ![Abrir panel lateral](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Editar el contenido de un componente existente](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) en la página:

      * Abra la barra de herramientas de componentes haciendo clic en. Utilice el icono **Editar** (lápiz) para abrir el cuadro de diálogo.
      * Abra el editor en contexto del componente con las funciones Seleccionar y mantener presionadas o Hacer doble clic con el botón lento. Se muestran las acciones disponibles (para algunos componentes se trata de una selección limitada).
      * Para ver todas las acciones disponibles, acceda al modo de pantalla completa mediante:

     ![Modo de pantalla completa](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Configurar las propiedades de un componente existente](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Abra la barra de herramientas de componentes haciendo clic en. Utilice el icono **Configurar** (llave inglesa) para abrir el cuadro de diálogo.

   * [Desplazar un componente](/help/sites-authoring/editing-content.md#moving-a-component) mediante las siguientes opciones:

      * Arrastre el componente en cuestión a la ubicación nueva.
      * Abra la barra de herramientas de componentes haciendo clic en. Use los iconos **Cortar** y **Pegar** donde sea necesario.

   * [Copiar (y pegar)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Abra la barra de herramientas de componentes haciendo clic en. Use los iconos **Copiar** y **Pegar** según sea necesario.

   >[!NOTE]
   >
   >Puede **pegar** componentes en la misma página o en otra página. Si pega el componente en una página diferente que ya estaba abierta antes de la operación de cortar o copiar, tendrá que actualizase la página. 

   * [Eliminar](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Abra la barra de herramientas de componentes haciendo clic en y, a continuación, utilice el icono **Eliminar**.

   * [Añadir anotaciones](/help/sites-authoring/annotations.md#annotations) a la página:

      * Seleccione el modo **Anotar** (icono de burbuja de voz). Añada anotaciones utilizando el icono **Añadir anotación** (signo más). Salga del modo Anotar utilizando la X en la parte superior derecha.

     ![Anotar](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Vista previa de una página](/help/sites-authoring/editing-content.md#preview-mode) (para ver cómo aparecerá en el entorno de publicación)

      * Seleccione **Vista previa** en la barra de herramientas.

   * Vuelva al modo de edición (o seleccione otro modo) utilizando **Editar** en el selector desplegable.

   >[!NOTE]
   >
   >Para navegar usando vínculos en el contenido, debe usar [Modo de vista previa](/help/sites-authoring/editing-content.md#preview-mode).

### Editar las Propiedades de la página   {#editing-the-page-properties}

Existen dos métodos (principales) para [editar las propiedades de la página](/help/sites-authoring/editing-page-properties.md):

* Desde la consola **Sitios**:

   1. [Desplácese hasta la página](#finding-your-page) que quiera publicar.
   1. Seleccione el icono **Propiedades** desde:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando [su página se haya seleccionado](#selectiingyourpageforfurtheraction).

  ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. Se muestran las propiedades de la página. Puede aplicar actualizaciones según sea necesario y, a continuación, seleccionar Guardar para preservarlas.

* Cuando [edite su página](#editing-your-page-content):

   1. Abra el menú **Información de página**.
   1. Seleccione **Abrir propiedades** para abrir el cuadro de diálogo y editar las propiedades.

  ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Publicar su página (o eliminar la publicación) {#publishing-your-page-or-unpublishing}

Existen dos métodos principales para [publicar la página](/help/sites-authoring/publishing-pages.md) (y también para eliminar la publicación):

* Desde la consola **Sitios**:

   1. [Desplácese hasta la página](#finding-your-page) que quiera editar.
   1. Seleccione el icono **Publicación rápida** desde:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando su [página se haya seleccionado](#selectiingyourpageforfurtheraction) (también permite el acceso a [Publicar posteriormente](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* Cuando [edite su página](#editing-your-page-content):

   1. Abra el menú **Información de página**.
   1. Seleccione **Publicar página**.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* La cancelación de la publicación de una página desde la consola solo se puede realizar mediante la opción **Administrar publicación**, que solo está disponible en la barra de herramientas (no a través de las acciones rápidas).

  La opción **Cancelar la publicación de páginas** todavía está disponible en el menú **Información de página** en el editor.

  ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  Consulte [Publicación de páginas](/help/sites-authoring/publishing-pages.md#unpublishing-pages) para obtener más información.

### Mover, copiar y pegar o eliminar su página   {#move-copy-and-paste-or-delete-your-page}

Todas estas acciones pueden activarse del siguiente modo:

1. [Desplácese hasta la página](#finding-your-page) que desea mover, copiar y pegar o eliminar.
1. Seleccione el icono de copiar (y luego pegar), mover o eliminar según sea necesario mediante:

   * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso requerido.
   * La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).

   A continuación, depende de la acción:

   * Copiar:

      * Vaya a la nueva ubicación y pegue.

   * Mover:

      * El asistente se abre para recopilar la información necesaria para mover la página. Siga las instrucciones que aparecen en pantalla.

   * Eliminar:

      * Se le solicitará que confirme la acción.

   >[!NOTE]
   >
   >La opción Eliminar no se encuentra disponible como Acción rápida.

### Bloquear y desbloquear su página  {#locking-your-page-then-unlocking}

[Bloquear una página](/help/sites-authoring/editing-content.md#locking-a-page) impide que otros autores trabajen en ella al mismo tiempo que usted. El icono/botón Bloquear (y Desbloquear) se encuentra en:

* La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).
* El menú desplegable [Información de página](#editing-the-page-properties) cuando edita la página.
* Barra de herramientas de la página cuando edita la página (cuando está bloqueada).

Por ejemplo, el icono de bloqueo presenta el siguiente aspecto:

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Acceder a las referencias de la página {#accessing-page-references}

[El acceso rápido a las referencias](/help/sites-authoring/author-environment-tools.md#references) a una página o desde una página está disponible en el carril Referencias.

1. Seleccione **Referencias** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   Se muestra una lista de tipos de referencias:

   ![captura de pantalla_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Haga clic en el tipo de referencia necesario para mostrar más detalles y (cuando corresponda) realizar más acciones.

### Crear una versión de su página   {#creating-a-version-of-your-page}

Para crear una [versión](/help/sites-authoring/working-with-page-versions.md) de la página:

1. Para abrir el raíl de cronología, seleccione **[Cronología](/help/sites-authoring/basic-handling.md#timeline)** con el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Haga clic en la flecha hacia arriba situada en la parte inferior derecha de la columna Cronología para mostrar botones adicionales, como **Guardar como versión**.

   ![captura de pantalla_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Seleccione **Guardar como versión**, y después seleccione **Crear**.

### Restablecer o comparar una versión de su página {#restoring-comparing-a-version-of-your-page}

Se utiliza el mismo mecanismo básico cuando se restablecen y/o se comparan versiones de su página:

1. Seleccione **[Línea de tiempo](/help/sites-authoring/basic-handling.md#timeline)** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Si ya se ha guardado una versión de su página, se indica en la cronología.

1. Haga clic en la versión que desee restaurar. Esto mostrará botones de acción adicionales:

   * **Volver a esta versión**

      * Se restaura la versión.

   * **Mostrar diferencias**

      * La página se abre con las diferencias (entre las dos versiones) resaltadas.
