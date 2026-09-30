---
title: Personalizar pestañas para una tarea
description: Personalizar los nombres de las pestañas de las tareas, en AEM Forms Workspace de LiveCycle.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 88f5093c-f249-4e4b-900a-5897f47e513c
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
source-wordcount: '104'
ht-degree: 100%
---
# Personalizar pestañas para una tarea {#customizing-tabs-for-a-task}

Puede personalizar los nombres de las pestañas para el componente `Start Process` en la `Start Process` vista Uber y el componente `Task Details` en la `ToDo` vista Uber.

1. Siga los [Pasos genéricos para personalizar AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Cambiar el valor de `tabname` en el archivo `translation.json`.

   Por ejemplo, cambie `/apps/ws/locales/en-US/translation.json` al inglés para lo siguiente.

   * Para las tareas iniciadas en el proceso de inicio, utilice el siguiente fragmento del bloque `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Para las tareas en Tareas pendientes, use el siguiente fragmento del bloque `"todo" : {}`.

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Agregue el par clave-valor correspondiente a todos los idiomas compatibles.
