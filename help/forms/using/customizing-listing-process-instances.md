---
title: Personalizar la lista de instancias de proceso
description: Personalizar las propiedades mostradas en la instancia de proceso en AEM Forms Workspace.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# Personalizar la lista de instancias de proceso {#customizing-the-listing-of-process-instances}

La lista de instancias de proceso se muestra en la pestaña Seguimiento de AEM Forms Workspace.

En la lista de instancias de proceso, para cada instancia de proceso, AEM Forms Workspace muestra algunas propiedades. Las siguientes propiedades están disponibles para cada instancia de proceso. Estas propiedades se almacenan como atributos en el modelo de componentes de instancias de proceso y están disponibles para usarlas en su vista y plantilla.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>description</td>
   <td>Descripción de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>Nombre del iniciador de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID del iniciador de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Marca de hora de cuando se completó el proceso.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID de la instancia de proceso.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniciado<br /> 1 = En ejecución<br /> 2 = Completo<br /> 3 = Finalizado<br /> 4 = Terminado<br /> 5 = Finalización<br /> 6 = Suspendido<br /> 7 = Suspender<br /> 8 = Sin suspensión</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nombre del proceso.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Marca de tiempo de cuando se inició el proceso.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>La matriz de objetos de variables de proceso. Cada objeto de variable de proceso contiene <strong>name</strong> (el nombre de la variable de proceso), <strong>value</strong> (valor de la variable de proceso) y<strong> type</strong> (el tipo de variable de proceso).</td>
  </tr>
 </tbody>
</table>

**Ejemplo:**

Para mostrar la propiedad `description` de la instancia de proceso en la tarjeta Instancia de proceso, realice los siguientes pasos.

1. Siga los [Pasos genéricos para personalizar AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Haga lo siguiente:

   1. Copie /libs/ws/js/runtime/templates/processinstance.html a/apps/ws/js/runtime/templates/, si no existe. Haga clic en **Guardar todo**.
   1. Agregue un div de descripción del proceso con class = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Haga lo siguiente:

   1. Abra /apps/ws/js/registry.js para editarlo.
   1. Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/processinstance.html` con `text!/lc/`**apps**/ws/js/runtime/templates/processinstance.html.

1. Los cambios anteriores pueden requerir una actualización del archivo CSS al agregar una entrada en la hoja de estilo /apps/ws/css/newStyle.css de la siguiente manera:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
