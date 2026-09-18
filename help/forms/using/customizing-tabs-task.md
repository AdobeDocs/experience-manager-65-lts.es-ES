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
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
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
