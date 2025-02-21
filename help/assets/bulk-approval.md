---
title: Revisar recursos y colecciones de carpetas
description: Configure flujos de trabajo de revisión para los recursos de una carpeta o una colección y compártala con revisores o socios creativos para buscar comentarios.
contentOwner: AG
feature: Collaboration, Collections
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 6%

---

# Revisar recursos y colecciones de carpetas {#review-folder-assets-and-collections}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | Este artículo |

Configure flujos de trabajo de revisión para los recursos de una carpeta o una colección y compártala con revisores o socios creativos para buscar comentarios.

[!DNL Adobe Experience Manager Assets] le permite configurar un flujo de trabajo de revisión ad-hoc para los recursos de una carpeta o colección, así como compartirlo con revisores o socios creativos para buscar comentarios.

Puede asociar el flujo de trabajo de revisión con un proyecto o crear una tarea de revisión independiente.

Una vez compartidos los recursos, los revisores pueden aprobarlos o rechazarlos. Las notificaciones se envían en varias fases del flujo de trabajo para notificar a los destinatarios objetivo la finalización de diversas tareas. Por ejemplo, cuando comparte una carpeta o colección, el revisor recibe una notificación que le informa de que una carpeta o colección se ha compartido para su revisión.

Una vez que el revisor haya completado la revisión (aprueba o rechaza los recursos), recibirá una notificación de finalización de la revisión.

## Crear una tarea de revisión para carpetas {#creating-a-review-task-for-folders}

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta para la que desea crear una tarea de revisión.
1. En la barra de herramientas, haga clic en **[!UICONTROL Crear tarea de revisión]** ![crear tarea de revisión](assets/do-not-localize/create-review-task.png) para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver la opción en la barra de herramientas, haga clic en **[!UICONTROL Más]** y, a continuación, seleccione la opción.

1. (Opcional) En la lista **[!UICONTROL Proyecto]**, seleccione el proyecto al que desea asociar la tarea de revisión. De manera predeterminada, la opción **[!UICONTROL None]** está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la lista **[!UICONTROL Proyectos]**.

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]**.

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]**.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details](assets/task_details.png)

1. En la pestaña Advanced, introduzca una etiqueta para utilizar para crear el URI.

   ![nombre_revisión](assets/review_name.png)

1. Haga clic en **[!UICONTROL Enviar]** y, a continuación, haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en [!DNL Assets] como aprobador y navegue hasta la interfaz de usuario de [!DNL Assets]. Para aprobar los recursos, haga clic en **[!UICONTROL Notificaciones]** y seleccione la tarea de revisión en la lista.

   ![Notificación de Assets](assets/aemAssetsNotification.png)

1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, haga clic en **[!UICONTROL Revisar]**.
1. En la página **[!UICONTROL Revisar tarea]**, seleccione los recursos y haga clic en **[!UICONTROL Aprobar o rechazar]** para aprobarlos o rechazarlos, según corresponda.

   ![tarea_de_revisión](assets/review_task.png)

1. Haga clic en **[!UICONTROL Completar]** en la barra de herramientas. En el cuadro de diálogo, escriba un comentario y haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la interfaz de usuario [!DNL Assets] y abra la carpeta. Los iconos de estado de aprobación de los recursos aparecen en la vista de tarjeta y en la vista de lista.

   **Vista de tarjeta**

   ![Revisar el estado tal como se ve en la vista de tarjeta](assets/chlimage_1-404.png)

   **Vista de lista**

   ![Revisar el estado tal como se ve en la vista de lista](assets/review_status_listview.png)

## Crear una tarea de revisión para colecciones {#creating-a-review-task-for-collections}

1. En la página Colecciones, seleccione la colección para la que desea crear una tarea de revisión.
1. En la barra de herramientas, haga clic en **[!UICONTROL Crear tarea de revisión]** ![crear tarea de revisión](assets/do-not-localize/create-review-task.png) para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver la opción en la barra de herramientas, haga clic en **[!UICONTROL Más]** y, a continuación, seleccione la opción.

1. (Opcional) En la lista **[!UICONTROL Proyecto]**, seleccione el proyecto al que desea asociar la tarea de revisión. De manera predeterminada, la opción **[!UICONTROL None]** está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la lista **[!UICONTROL Proyectos]**.

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]**.

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]**.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details-collection](assets/task_details-collection.png)

1. Haga clic en **[!UICONTROL Enviar]** y, a continuación, haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en [!DNL Assets] como aprobador y vaya a la consola [!DNL Assets]. Para aprobar los recursos, haga clic en **[!UICONTROL Notificaciones]** y seleccione la tarea de revisión en la lista.
1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, haga clic en **[!UICONTROL Revisar]**.
1. Todos los recursos de la colección están visibles en la página de revisión. Seleccione los recursos y haga clic en **[!UICONTROL Aprobar/Rechazar]** para aprobar o rechazar recursos, según corresponda.

   ![review_task_collection](assets/review_task_collection.png)

1. Haga clic en **[!UICONTROL Completar]** en la barra de herramientas. En el cuadro de diálogo, escriba un comentario y haga clic en **[!UICONTROL Completar]** para confirmar.
1. Vaya a la consola Colecciones y abra la colección. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: Vista de tarjeta.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: vista de lista.*
