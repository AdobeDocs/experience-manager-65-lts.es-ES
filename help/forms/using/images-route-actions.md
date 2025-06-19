---
title: Personalizar imágenes utilizadas en acciones de ruta
description: Personalización de las imágenes utilizadas en las acciones de ruta de LiveCycle AEM Forms Workspace.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 782043c0-79f8-42a4-ae1b-4743b480e523
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 97%

---

# Personalizar imágenes utilizadas en acciones de ruta {#customize-images-used-in-route-actions}

Para personalizar las imágenes utilizadas en las acciones de ruta, siga los pasos que se describen en [Pasos genéricos para la personalización](/help/forms/using/generic-steps-html-workspace-customization.md) y, a continuación, los pasos descritos en este artículo.

## Imágenes de acciones de ruta {#images-for-route-actions}

1. Agregue los estilos que definen las imágenes en CSS en la siguiente ubicación para las nuevas acciones de ruta:

   `/apps/ws/css/newStyle.css`

   Por ejemplo: añada un nuevo estilo llamado `myStyle1` como se muestra a continuación y cargue el archivo de imagen `myStyleIcon1.png` en la carpeta `/apps/ws/image`s utilizando un cliente de WebDAV.

   >[!NOTE]
   >
   >Para obtener más información, consulte [Acceso a WebDAV](/help/sites-administering/webdav-access.md).

   >[!NOTE]
   >
   >Especifique que el nombre del estilo sea el mismo que el nombre de la acción de ruta en las preferencias.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Elemento emergente de acción de tarea Lista de tareas {#task-list-task-action-popup}

1. Cree un elemento emergente de acción de la lista de tareas. Consulte [Creación del código de espacio de trabajo de AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code). Requiere utilizar el paquete dev.

1. Copie `/libs/ws/js/runtime/templates/task.html` en `/apps/ws/js/runtime/templates/task.html`.

1. Si el nombre del estilo CSS es el mismo que el nombre de la acción de ruta proveniente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/task.html`:

   ```jsp
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. Si el nombre del estilo CSS es diferente del nombre de la acción de ruta proveniente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/task.html`. Esto agrega una pila de las condiciones del servlet `if-else` para asignar el estilo con el nombre de la acción de ruta.

```jsp
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Elemento emergente de acción de tarea Detalles de tarea {#task-details-task-action-popup}

1. Copie `/libs/ws/js/runtime/templates/taskdetails.html` en `/apps/ws/js/runtime/templates/taskdetails.html`.

1. Si el nombre del estilo CSS es el mismo que el nombre de la acción de ruta proveniente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. Si el nombre del estilo CSS es diferente del nombre de la acción de ruta proveniente del servidor, modifique el siguiente código en `/apps/ws/js/runtime/templates/taskdetails.html`. Agrega una pila de las condiciones del servlet `if-else` para asignar el estilo con el nombre de la acción de ruta.

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Abra el archivo `/apps/ws/js/registry.js` para editarlo y busque el siguiente texto :
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Reemplace el texto con lo siguiente:
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
