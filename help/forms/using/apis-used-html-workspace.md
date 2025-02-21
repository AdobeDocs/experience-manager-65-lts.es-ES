---
title: API utilizadas en AEM Forms Workspace
description: API de Java&trade; y JavaScript públicas y métodos de espacio de trabajo de LiveCycle AEM Forms, expuestos para la personalización y la automatización.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 44%

---

# API utilizadas en AEM Forms Workspace {#apis-used-in-aem-forms-workspace}

Las siguientes API se utilizan en AEM Forms Workspace.

<table>
 <tbody>
  <tr>
   <td><strong>Método JavaScript</strong></td>
   <td><strong>Nombre del servicio</strong></td>
   <td><strong>Nombre de la API</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Busca grupos. devuelve una lista de todos los grupos si no se ha especificado nada; si no, devuelve grupos con el nombre especificado.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Busca usuarios y grupos. Devuelve una lista de todos los usuarios y grupos si no se ha especificado nada; de lo contrario, devuelve usuarios y grupos con el nombre especificado.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>Se llama antes de enviar un formulario mediante DocumentSubmitServlet. Establece el ID de la tarea en una variable de sesión (junto con la hora de caducidad) que se recupera durante el envío real.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
   <td>Envía el objeto del documento asociado a una tarea (y el proceso de envío a su vez).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Obtiene todas las categorías raíz presentes en el servidor.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Obtiene todos los elementos secundarios directos de una categoría.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Obtiene todos los puntos de inicio presentes en el servidor en todas las categorías.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Esto invoca un punto de inicio y crea una tarea correspondiente a un punto de inicio</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>Obtiene todas las tareas que se crean, reenvían o consultan, guardan, asignan y guardan para el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>Obtiene una tarea específica.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>procesar</td>
   <td>Procesa una tarea y devuelve la información necesaria para procesar el formulario, como la dirección URL del formulario, el tipo de formulario o la dirección URL de datos, si es necesario.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>Devuelve el resultado de la API de envío de TaskManager mediante la clave de resultado.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>Envía los datos del formulario (pasados como cadena) asociados a la tarea mediante la API de envío de TaskManager. Se utiliza para formularios Flex que no llaman a la API de envío de TaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>save</td>
   <td>Guarda una tarea en el servidor.</td>
  </tr>
  <tr>
   <td>completar</td>
   <td>ProcessManagementTaskService</td>
   <td>completar</td>
   <td>Completa una tarea y esta se pasa al siguiente paso según el diseño del proceso.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>Devuelve la dirección URL de un archivo adjunto donde este está disponible.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>Obtiene todos los archivos adjuntos y notas de una tarea.</td>
  </tr>
  <tr>
   <td>compartir</td>
   <td>ProcessManagementTaskService</td>
   <td>compartir</td>
   <td>Comparte una tarea con otro usuario. Otro usuario puede reclamar la tarea y convertirse en su propietario.</td>
  </tr>
  <tr>
   <td>adelante</td>
   <td>ProcessManagementTaskService</td>
   <td>adelante</td>
   <td>Envía una tarea a otro usuario.</td>
  </tr>
  <tr>
   <td>consultar</td>
   <td>ProcessManagementTaskService</td>
   <td>consultar</td>
   <td>Consulta una tarea con otro usuario.</td>
  </tr>
  <tr>
   <td>solicitar</td>
   <td>ProcessManagementTaskService</td>
   <td>solicitar</td>
   <td>Afirma que una tarea está disponible en una cola compartida.</td>
  </tr>
  <tr>
   <td>desbloquear</td>
   <td>ProcessManagementTaskService</td>
   <td>desbloquear</td>
   <td>Desbloquea una tarea.</td>
  </tr>
  <tr>
   <td>bloquear</td>
   <td>ProcessManagementTaskService</td>
   <td>bloquear</td>
   <td>Bloquea una tarea y esta no puede solicitarla otro usuario si se comparte.</td>
  </tr>
  <tr>
   <td>rechazar</td>
   <td>ProcessManagementTaskService</td>
   <td>rechazar</td>
   <td>Devuelve una tarea al propietario anterior de la tarea.</td>
  </tr>
  <tr>
   <td>abandon</td>
   <td>ProcessManagementTaskService</td>
   <td>abandon</td>
   <td>Elimina una tarea.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>Establece la visibilidad de una tarea. Si la visibilidad se establece en false, el usuario no podrá ver la tarea posteriormente.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>Se utiliza para buscar usuarios. Devuelve todos los usuarios si no se especifica ningún nombre, o bien devuelve los usuarios con un nombre especificado.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Devuelve todos los usuarios de un grupo.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>Otorga acceso a la cola del usuario que ha iniciado sesión a un usuario especificado. Básicamente comparte su propia cola con otro usuario.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Realiza la solicitud de acceso de una cola de un usuario especificado para el usuario que ha iniciado sesión. Si el usuario aprueba la solicitud, su cola se compartirá con el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Devuelve todos los usuarios que tienen acceso a la cola del usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Devuelve todos los usuarios cuya cola es accesible para un usuario.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>Quita a un usuario de la lista de usuarios que tienen acceso a la cola del usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Quita a un usuario de la lista de usuarios a los que el usuario que ha iniciado sesión puede acceder desde su cola.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Obtiene todas las colas (propias, compartidas y grupales) accesibles para el usuario que ha iniciado sesión.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Obtiene la configuración de Fuera de la oficina de un usuario.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Guarda la configuración de Fuera de la oficina de un usuario.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>Devuelve una lista de todos los procesos.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>Devuelve una lista de todos los nombres de proceso participantes por el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Obtiene detalles de una instancia de proceso.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Obtiene todas las instancias de proceso de un proceso.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>Obtiene tareas pendientes para una instancia de proceso.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Obtiene todas las tareas de una instancia de proceso.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>Devuelve una lista de todas las plantillas de búsqueda.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>Devuelve el contenido de una plantilla de búsqueda.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>Busca y devuelve todas las tareas que cumplen todas las condiciones de una plantilla de búsqueda.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>Obtiene todas las asignaciones para una tarea. Por ejemplo, si un usuario reenvía o consulta una tarea con otro usuario, entonces es una asignación para una tarea.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>Elimina un archivo adjunto.</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>Se renueva la afirmación si es necesario. Autentica al usuario. Establece los parámetros de sesión para la información del servidor/cliente. Devuelve la información del usuario y el intervalo de sondeo.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Devuelve todas las tareas de los informes directos del administrador de la sesión.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Devuelve una tarea de un informe directo especificado del administrador de la sesión.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Reenvía una tarea de un informe directo a otro usuario.</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>Devuelve una tarea de un informe directo al usuario anterior.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>Obtiene una propiedad del espacio de trabajo para un usuario.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>eliminar</td>
   <td>Quita una propiedad del espacio de trabajo para un usuario.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Devuelve todas las propiedades del espacio de trabajo de un usuario.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>Establece una propiedad del espacio de trabajo para un usuario.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>Obtiene la dirección URL de la imagen del usuario para el usuario que ha iniciado sesión.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Obtiene la dirección URL de la imagen del usuario para el usuario especificado.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>Carga una nota en el servidor para una tarea.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer (también se llama directamente desde la plantilla html)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>Carga un archivo adjunto en el servidor para una tarea.</td>
  </tr>
  <tr>
   <td>getImageURL (también llamado directamente desde la plantilla de HTML)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Obtiene la imagen para un proceso.</td>
  </tr>
 </tbody>
</table>
