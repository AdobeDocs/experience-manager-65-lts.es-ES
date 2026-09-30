---
title: Iniciar un nuevo proceso con datos de proceso existentes en AEM Forms Workspace
description: Consulte cómo puede iniciar un proceso nuevo con datos de proceso existentes en AEM Forms Workspace.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 4a2a06c2-a4fa-463c-9375-bebda426a14c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 94%
---
# Iniciar un nuevo proceso con datos de proceso existentes en AEM Forms Workspace{#initiating-a-new-process-with-existing-process-data-in-aem-forms-workspace}

Puede iniciar un nuevo proceso utilizando los datos de un proceso existente. La necesidad de iniciar un nuevo proceso a partir de los datos de proceso existentes surge cuando tenemos que usar el mismo formulario con frecuencia con pocos cambios en el contenido, como en el caso de los formularios de las vacaciones retribuidas. Esta función ahorra tiempo y esfuerzo a los usuarios, especialmente cuando el formulario del proceso es muy extenso.

A continuación se indican los pasos para iniciar un nuevo proceso a partir de los datos de proceso existentes:

1. Realice alguna de las siguientes acciones:

   * En Seguimiento, haga clic en la instancia de proceso cuyos datos desee utilizar. En la vista Historial de procesos del panel derecho, haga clic en la fila de tareas que corresponda al punto de inicio.
   * En Seguimiento, seleccione una plantilla de búsqueda para mostrar una lista de instancias de proceso. Seleccione la instancia cuyos datos desee utilizar.
   * En la pestaña **[!UICONTROL Tareas pendientes]**, seleccione la tarea. Haga clic en la pestaña **[!UICONTROL Historial]** y seleccione la tarea que inició la instancia de proceso.

   ![Seleccionar la tarea](assets/start3_new.png) ![Seleccionar la tarea](assets/start1_new.png)

1. En la barra de herramientas Acciones de tarea, haga clic en **[!UICONTROL Inicio]**. Se muestra un formulario adaptable para la nueva instancia de proceso con datos rellenados previamente.

1. Actualice los datos según sea necesario y haga clic en **[!UICONTROL Completar]** o en el botón apropiado del formulario.
