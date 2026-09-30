---
title: Visualizar información en el panel Resumen de tareas
description: En AEM Forms Workspace, se puede configurar un panel Resumen de tareas para resumir la tarea o mostrar cualquier otra página web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 0ecca051-3ebc-4ace-b550-6e895c582e2c
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
source-wordcount: '266'
ht-degree: 92%
---
# Visualizar información en el panel Resumen de tareas {#displaying-information-in-the-task-summary-pane}

Cuando se abre una tarea en AEM Forms Workspace, el panel Resumen de tareas puede mostrar un resumen de la tarea. Esta información adicional y relevante para una tarea agrega más valor para el usuario final de AEM Forms Workspace.

El espacio de trabajo de AEM Forms le permite mostrar una página web de su elección en el panel Resumen de tareas. Se puede crear un proceso para mostrar un panel Resumen de tareas con Workbench.

1. Crear un proceso Asignar tarea en Workbench. Para obtener más información sobre la operación Asignar tarea, consulte el tema Referencia de servicio en [Ayuda de Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Si existe una URL de Resumen de tareas, la vista Resumen de tareas se abrirá de forma predeterminada en lugar de la vista Formulario. En este caso, incluso cuando un usuario habilite la opción “Abrir el formulario en modo maximizado” en Asignar tarea, el formulario no se abrirá en modo maximizado.

1. Configure el campo URL de resumen de tareas. Puede especificar un valor literal, una plantilla, una variable o una expresión XPath.
1. A continuación se muestra un ejemplo de visualización de la información en la página Resumen de tareas.

   * Inicie sesión en el entorno de CRXDE Lite en `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** bajo `/apps`. En la Lista de control de acceso de `/apps/SampleSummary`, agregue una entrada para `PERM_WORKSPACE_USER` y permita `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Establezca el valor de la URL del resumen de tareas como `/lc/content/SampleSummary.html` en el paso Asignar tarea.
   * Cuando la tarea asociada con el paso Asignar tarea se abra en AEM Forms Workspace, el `html.esp` en `/apps/SampleSummary` se representará en el panel Resumen de tareas.
