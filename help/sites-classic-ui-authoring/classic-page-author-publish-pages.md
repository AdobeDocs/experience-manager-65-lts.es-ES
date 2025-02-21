---
title: Publicación de páginas
description: Después de crear y revisar el contenido en el entorno de creación, haga que esté disponible en el sitio web público.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 9%

---

# Publicar páginas{#publishing-pages}

Después de crear y revisar el contenido en el entorno de creación, debe publicarlo en su sitio web público (el entorno de publicación).

Es lo que se denomina publicar una página. Quitar una página del entorno de publicación, se denomina cancelar la publicación. Al publicar y cancelar la publicación, la página permanece disponible en el entorno de creación para realizar más cambios hasta que se elimine.

También puede publicar una página (o cancelar su publicación) inmediatamente o en un momento posterior predefinido.

>[!NOTE]
>
>Algunos términos relacionados con la publicación pueden confundirse:
>
>* **Publicar o cancelar la publicación**
>  Estos son los términos principales de las acciones que harán que el contenido esté disponible o no para los visitantes en su entorno de publicación.
>
>* **Activar o desactivar**
>  Estos términos son sinónimos de publicar y cancelar la publicación.
>
>* **Replicar o replicación**
>  Son los términos técnicos que describen el movimiento de datos (por ejemplo, contenido de página, archivos, código, comentarios del usuario) de un entorno a otro, como al publicar o replicar de forma inversa comentarios del usuario.
>

>[!NOTE]
>
>Si no dispone de los privilegios necesarios para publicar una página específica:
>
>* Se activará un flujo de trabajo para notificar a la persona adecuada su solicitud de publicación.
>* Se mostrará un mensaje (durante un corto periodo de tiempo) para notificarle esto.
>

## Publicación de una página {#publishing-a-page}

Existen dos métodos para activar una página:

* [desde la consola Sitios web](#activating-a-page-from-the-websites-console)
* [de la barra de tareas en la propia página](#activating-a-page-from-sidekick)

>[!NOTE]
>
>También puede activar un subárbol de varias páginas con [Activar árbol](#howtoactivateacompletesectiontreeofyourwebsite) en la consola Herramientas.

### Activación de una página desde la consola Sitios web {#activating-a-page-from-the-websites-console}

Puede activar páginas en la consola Sitios web. Después de abrir una página y modificar su contenido, vuelve a la consola Sitios web:

1. En la consola Sitios web, seleccione la página que desea activar.
1. Seleccione **Activar**, ya sea en el menú superior o en el menú desplegable del elemento de página seleccionado.

   Para activar el contenido de la página y todas sus páginas secundarias, usa la consola [**Herramientas**](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >Si es necesario, AEM solicita que active o reactive cualquier recurso vinculado a la página. Puede activar o desactivar las casillas de verificación para activar esos recursos.
   >
   >

1. Si es necesario, AEM solicita que active o reactive cualquier recurso vinculado a la página. Puede activar o desactivar las casillas de verificación para activar esos recursos.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM activa el contenido seleccionado. La página o páginas publicadas aparecen en la [consola Sitios web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) (marcada como verde) con información sobre quién activó el contenido y la fecha y hora de activación.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Activación de una página desde Sidekick {#activating-a-page-from-sidekick}

También puede activar una página cuando la tenga abierta para editarla.

Después de abrir la página y modificar su contenido, debe hacer lo siguiente:

1. Seleccione la ficha **Página** en Sidekick.
1. Haga clic en **Activar página**.
Aparece un mensaje en la parte superior derecha de la ventana que confirma que la página se ha activado.

## Cancelar la publicación de una página {#unpublishing-a-page}

Para quitar una página del entorno de publicación, se desactiva el contenido.

Para desactivar una página:

1. En la consola Sitios web, seleccione la página que desea desactivar.
1. Seleccione **Desactivar**, ya sea en el menú superior o en el menú desplegable del elemento de página seleccionado. Se le pedirá que confirme la eliminación.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. Actualice la consola [Sitios web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) y el contenido se marcará en rojo para indicar que ya no se publicará.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## Activar/desactivar más tarde {#activate-deactivate-later}

### Activar más tarde {#activate-later}

Para programar la activación para un momento posterior:

1. En la consola Sitios web, ve al menú **Activar** y selecciona **Activar más tarde**.
1. En el cuadro de diálogo que se abre, proporcione la fecha y la hora de activación y haga clic en **Aceptar**. Esto crea una versión de la página que se activa a la hora especificada.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

La activación posterior inicia un flujo de trabajo para activar esta versión de la página a la hora especificada. Por el contrario, la desactivación posterior inicia un flujo de trabajo para desactivar esta versión de la página en un momento específico.

Si desea cancelar esta activación/desactivación, vaya a la [Consola de flujo de trabajo](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para finalizar el flujo de trabajo correspondiente.

### Desactivar más tarde {#deactivate-later}

Para programar la desactivación para un momento posterior:

1. En la consola del sitio web, ve al menú **Desactivar** y selecciona **Desactivar más tarde**.

1. En el cuadro de diálogo que se abre, proporcione la fecha y la hora de desactivación y haga clic en **Aceptar**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**Al desactivar más tarde** r se inicia un flujo de trabajo para desactivar esta versión de la página en un momento específico.

Si desea cancelar esta desactivación, vaya a la [Consola de flujo de trabajo](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para finalizar el flujo de trabajo correspondiente.

## Activación/Desactivación Programadas (Tiempo De Activación/Desactivación) {#scheduled-activation-deactivation-on-off-time}

Puede programar tiempos de publicación/cancelación de publicación de una página usando los valores de **Tiempo de activación** y **Tiempo de inactividad** que se pueden definir en [Propiedades de la página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### Determinar el estado de publicación de la página {#determining-page-publication-status-classic-ui}

El estado se puede ver desde la [consola Sitios web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). Los colores indican el estado de publicación.

## Activar una sección completa (árbol) del sitio web {#activating-a-complete-section-tree-of-your-website}

Desde la ficha **Sitios web** puede activar las páginas individuales. Cuando ha introducido o actualizado un número considerable de páginas de contenido (todas ellas residentes en la misma página raíz), puede resultar más fácil activar todo el árbol en una acción. También puede realizar una Ejecución en seco para emular una activación y resaltar qué páginas se activarían.

1. Abra la consola **Herramientas** seleccionándola en la página **Bienvenido** y luego haga doble clic en **Replicación** para abrir la consola (`https://localhost:4502/etc/replication.html`).

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. En la consola **Replicación**, haga clic en **Activar árbol**.

   Se mostrará la siguiente ventana ( `https://localhost:4502/etc/replication/treeactivation.html`).

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. Escriba la **ruta de inicio**. Esto especifica la ruta a la raíz de la sección que desea activar (publicar). Esta página y todas las páginas por debajo se consideran para su activación (o se utilizan en la emulación si se selecciona una Ejecución en seco).
1. Active los criterios de selección según sea necesario:

   * **Solo modificadas**: activar solo las páginas modificadas.
   * **Solo activadas**: activar solo las páginas que (ya) se han activado. Actúa como una forma de reactivación.
   * **Ignorar desactivadas**: ignore todas las páginas que se hayan desactivado.

1. Seleccione la acción que desea realizar:

   1. Seleccione **Ejecución en seco** si desea comprobar qué páginas *se activarían*. Esto es solo una emulación, no se activará ninguna página.

   1. Seleccione **Activar** si desea activar las páginas.
