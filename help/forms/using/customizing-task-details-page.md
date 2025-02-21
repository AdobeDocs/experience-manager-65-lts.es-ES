---
title: Personalizar la página de detalles de la tarea
description: Personalizar la página de detalles de tareas en AEM Forms Workspace para modificar la información predeterminada que se muestra sobre una tarea.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 83%

---

# Personalizar la página de detalles de la tarea {#customizing-the-task-details-page}

La página de detalles de la tarea contiene información sobre una tarea y sus procesos. Puede personalizar la página de detalles de la tarea para agregar o eliminar información.

Puede agregar la siguiente información a la página de detalles de la tarea:

* Información disponible en el objeto JSON de una tarea (sección Tarea de la [Descripción del objeto JSON de AEM Forms Workspace](/help/forms/using/html-workspace-json-object-description.md))
* Información disponible en el objeto JSON de una instancia de proceso (sección Instancia de proceso en la [Descripción del objeto JSON de AEM Forms Workspace](/help/forms/using/html-workspace-json-object-description.md))

Para personalizar la página de detalles de la tarea, haga lo siguiente:

1. Siga los [Pasos genéricos para personalizar AEM Forms Workspace.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Para mostrar información adicional, agregue los pares de clave-valor correspondientes al archivo `translation.json` en `todo`bloque > `details`bloque > `app`bloque > [`required`bloque].

   El [`required`bloque] hace referencia a bloques disponibles, como el bloque de tareas para la información de tareas, el bloque de procesos para la información de procesos y el bloque de tareas pendientes para la información de tareas pendientes.

   Por ejemplo, para agregar información sobre la selección de la ruta requerida en la página de detalles de la tarea, puede agregar el siguiente par clave-valor en el bloque de tareas:

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >Agregue los pares de clave-valor correspondientes para todos los idiomas compatibles.

1. Copie `/libs/ws/js/runtime/templates/taskdetails.html` en `/apps/ws/js/runtime/templates/taskdetails.html`.

   Agregue la nueva información a `/apps/ws/js/runtime/templates/taskdetails.html`. Por ejemplo:

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. Abra /apps/ws/js/registry.js para editarlo.

   Buscar y reemplazar `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` con `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Para personalizar la página de detalles de la tarea con las tareas creadas en la pestaña **Iniciar proceso** en AEM Forms Workspace, agregue la nueva información a `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Para agregar estilos nuevos a la información agregada en la página de detalles, modifique el archivo CSS mediante la variable *Cambios en la interfaz de usuario* en [Personalizar el espacio de trabajo](changing-locale-user-interface.md).
