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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 93%

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
