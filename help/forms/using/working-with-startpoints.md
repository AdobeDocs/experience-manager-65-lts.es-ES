---
title: Trabajar con puntos de inicio
description: Pasos para trabajar con un proceso de Adobe Experience Manager Forms desde su dispositivo móvil definido en Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 45%

---


# Trabajar con puntos de inicio{#working-with-startpoints}

Un punto de inicio invoca un proceso creado en Workbench. Está asociado a un formulario que invoca el proceso cuando se envía el formulario.

>[!NOTE]
>
>Los puntos de inicio, el proceso de inicio y el formulario de los términos se utilizan de forma intercambiable al hacer referencia a este concepto.

Para iniciar un proceso desde la aplicación Forms de Adobe Experience Manager (AEM), debe tener un punto de inicio de tipo **Workspace** en su proceso. Además, debe seleccionar la opción **[!UICONTROL Visible en Workspace móvil]** para el punto de inicio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Para iniciar un proceso definido en Workbench**

1. Para ver los puntos de inicio disponibles en la aplicación de AEM Forms, vaya a la [Pantalla de inicio](../../forms/using/home-screen.md).
1. En la pantalla **[!UICONTROL Inicio]**, de forma predeterminada, se muestra la lista **[!UICONTROL Todos los formularios]**.

   El punto de inicio está asociado a un formulario. Seleccione el formulario asociado al punto de inicio en la lista para abrirlo.

   Se abre el formulario asociado al punto de inicio.

1. Introduzca los detalles en el formulario **[!UICONTROL Punto de inicio]**.

   Puede agregar anotaciones a esta tarea con el botón [Archivo adjunto](../../forms/using/add-attachments.md).

1. Después de rellenar el formulario, selecciona el botón **[!UICONTROL Enviar]**.

Si la aplicación está sin conexión, el formulario y sus datos se guardan en la carpeta Bandeja de salida.

Si la aplicación está en línea, la tarea se sincroniza con el servidor de AEM Forms y se asigna al usuario especificado en el proceso.

Para trabajar con la tarea en la lista de tareas, consulte [Abrir una tarea](/help/forms/using/open-task.md).
