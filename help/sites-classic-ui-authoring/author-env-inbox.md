---
title: Su bandeja de entrada
description: Puede recibir notificaciones de varias áreas de AEM, como notificaciones sobre elementos de trabajo o tareas que representan acciones que debe realizar en el contenido de la página.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Su bandeja de entrada{#your-inbox}

Puede recibir notificaciones de varias áreas de AEM, como notificaciones sobre elementos de trabajo o tareas que representan acciones que debe realizar en el contenido de la página.

Estas notificaciones se reciben en dos bandejas de entrada, separadas por el tipo de notificaciones:

* En la siguiente sección se describe una bandeja de entrada en la que puede ver las notificaciones que recibe como resultado de las suscripciones.
* En el documento [Participar en flujos de trabajo](/help/sites-classic-ui-authoring/classic-workflows-participating.md) se describe una bandeja de entrada especializada para elementos de flujo de trabajo.

## Visualización de las notificaciones {#viewing-your-notifications}

Para ver las notificaciones:

1. Abra la bandeja de entrada de notificaciones: en la consola **Sitios web**, haga clic en el botón de usuario en la esquina superior derecha y seleccione **Bandeja de entrada de notificaciones**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >También puede acceder a la consola directamente en el explorador; por ejemplo:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Se muestran sus notificaciones. Puede realizar las acciones necesarias:

   * [Suscripción a notificaciones](#subscribing-to-notifications)
   * [Procesamiento de notificaciones](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Suscripción a notificaciones {#subscribing-to-notifications}

Para suscribirse a las notificaciones:

1. Abra la bandeja de entrada de notificaciones: en la consola **Sitios web**, haga clic en el botón de usuario en la esquina superior derecha y seleccione **Bandeja de entrada de notificaciones**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >También puede acceder a la consola directamente en el explorador; por ejemplo:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Haga clic en **Configurar...** en la esquina superior izquierda para abrir el cuadro de diálogo de configuración.

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. Seleccione el canal de notificación:

   * **Bandeja de entrada**: las notificaciones se muestran en la Bandeja de entrada AEM.
   * **Correo electrónico**: las notificaciones se envían por correo electrónico a la dirección de correo electrónico definida en el perfil de usuario.

   >[!NOTE]
   >
   >Se deben configurar algunos ajustes para recibir notificaciones por correo electrónico. También es posible personalizar la plantilla de correo electrónico o añadir una plantilla de correo electrónico para un nuevo idioma. Consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification) para configurar notificaciones por correo electrónico en AEM.

1. Seleccione las acciones de página para las que desea recibir notificaciones:

   * Activated: cuando se activa una página.
   * Desactivado: cuando se desactiva una página.
   * Deleted (syndication): cuando una página se ha eliminado o replicado, es decir, cuando se replica una acción de eliminación realizada en una página.
Cuando se elimina o mueve una página, se replica automáticamente una acción de eliminación: la página se elimina en la instancia de origen en la que se realizó la acción de eliminación y en la instancia de destino definida por los agentes de replicación.

   * Modificado: cuando se modifica una página.
   * Creado: cuando se crea una página.
   * Eliminado: cuando se elimina una página mediante la acción de eliminación de página.
   * Desplegado: cuando se ha desplegado una página.

1. Defina las rutas de las páginas para las que se le notificará:

   * Haga clic en **Agregar** para agregar una fila nueva a la tabla.
   * Haga clic en la celda de tabla **Path** e introduzca la ruta de acceso, por ejemplo, `/content/docs`.

   * Para recibir notificaciones de todas las páginas que pertenecen al subárbol, establezca **¿Exacto?** a **No**.
Para que solo se le notifique por las acciones en la página definida por la ruta, establezca **¿Exacto?** a **Sí**.

   * Para permitir la regla, establezca **Rule** en **Allow**. Si se establece en **Denegar**, la regla se deniega, pero no se elimina y se puede permitir más adelante.

   Para quitar una definición, seleccione la fila haciendo clic en una celda de tabla y haga clic en **Eliminar**.

1. Haga clic en **Aceptar** para guardar la configuración.

## Procesamiento de notificaciones {#processing-your-notifications}

Si ha elegido recibir notificaciones en la bandeja de entrada AEM, esta se rellenará con notificaciones. Puedes [ver tus notificaciones](#viewing-your-notifications) y luego seleccionar las notificaciones necesarias para:

* Acéptelo haciendo clic en **Aprobar**: el valor de la columna **Leer** está establecido en **verdadero**.

* Elimínelo haciendo clic en **Eliminar**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
