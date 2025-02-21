---
title: Descripción de los objetos JSON de AEM Forms Workspace
description: Información conceptual sobre los objetos JavaScript de JSON utilizados en LiveCycle AEM Forms Workspace para tareas de personalización, extensión, modificación y reutilización.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 96%

---

# Descripción de los objetos JSON de AEM Forms Workspace {#aem-forms-workspace-json-object-description}

A continuación, se describen los objetos JSON utilizados en AEM Forms Workspace.

1. Categoría

   Las categorías se encuentran en la pestaña Iniciar proceso del espacio de trabajo. Estas categorías se utilizan para clasificar los puntos de inicio.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>Nombre de categoría</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>ID de categoría<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>Descripción de la categoría<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene el OID de la categoría principal.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de todos los puntos de inicio presentes en una categoría.</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contiene la lista de categorías secundarias directas de una categoría.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Todos los puntos de inicio y Favoritos son categorías que se definen en el lado del cliente. La categoría Favorito contiene todos los puntos de inicio que el usuario ha marcado como favoritos. La categoría Todos los puntos de inicio contiene todos los puntos de inicio.

1. Punto de inicio

   Un punto de inicio se utiliza para iniciar un proceso desde el espacio de trabajo cuando se invoca.

   | **Propiedad** | **Solo cliente** | **Comentarios** |
   |---|---|---|
   | categoryId | F | Contiene el ID de la categoría a la que pertenece el punto de inicio. |
   | description | F | Contiene la descripción de un punto de inicio. |
   | name | F | Contiene el nombre del punto de inicio. |
   | serializedImageTicket | F | Contiene un ticket de imagen correspondiente al punto de inicio. Este ticket de imagen se utiliza en el campo imageUrl del punto de inicio para obtener la imagen del punto de inicio desde el servidor. |
   | serviceName | F | Contiene el nombre del servicio del punto de inicio. |
   | startpointId | F | Contiene el ID del punto de inicio. |
   | isFavorite | T | Indica si el punto de inicio ha sido agregado a Favoritos o no. El valor es True si el punto de inicio ha sido agregado a Favoritos; en caso contrario, es False. |
   | isDefaultImage | T | Indica si hay una imagen especificada para el proceso o no. El valor es True si no hay ninguna imagen asociada con el proceso; en caso contrario, es False. |
   | task | T | Contiene la tarea creada cuando se invoca el punto de inicio. |
   | imageUrl | T | Contiene la URL de la imagen correspondiente al punto de inicio. |

1. Tarea

   Las tareas se asignan a usuarios o grupos e incluyen una interfaz de usuario (un formulario o una guía [obsoleta]) que se puede cumplimentar con datos. Cuando a los usuarios se les asigna una tarea, se les proporciona el formulario o la guía para que los cumplimenten y los envíen.

<table>
 <tbody>
  <tr>
   <td>Propiedad<br /> </td>
   <td>Solo cliente<br /> </td>
   <td>Comentarios<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>La clase de tarea es "LC8" cuando la tarea es "lc8 task"; en caso contrario, es "Standard".<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca de tiempo del momento en el que se completa la tarea.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>Contiene el ID del grupo al que se puede consultar la tarea. Se configura durante el diseño del proceso.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca de tiempo del momento en el que se crea la tarea.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>Contiene el ID del usuario que creó la tarea.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Contiene detalles sobre la asignación actual de tareas.<br /> </td>
  </tr>
  <tr>
   <td>deadline<br /> </td>
   <td>F</td>
   <td>Contiene la marca de tiempo del momento en el que una tarea alcanzará su fecha límite.<br /> </td>
  </tr>
  <tr>
   <td>description<br /> </td>
   <td>F</td>
   <td>Contiene la descripción de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre para mostrar de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Contiene el ID del grupo al que se puede reenviar la tarea. Se configura durante el diseño del proceso.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>Contiene las instrucciones de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>El valor es True si la tarea está bloqueada.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>El valor es True si se debe abrir el formulario de la tarea para completar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Si el valor es True, al abrir la tarea, el formulario se muestra en pantalla completa la primera vez.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Si el valor es True, se debe seleccionar una ruta para completar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Los archivos adjuntos se muestran si el valor es True.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Si el valor es True, la tarea se crea desde el punto de inicio.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>El valor es True si la tarea es visible en Workspace.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>La marca de tiempo del siguiente recordatorio.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contiene la prioridad de la tarea.<br /> 1 = Prioridad más alta<br /> 2 = Prioridad alta<br /> 3 = Prioridad Normal<br /> 4 = Prioridad baja<br /> 5 = Prioridad más baja<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>El ID de la instancia de proceso de la que forma parte la tarea.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>El estado de la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>Contiene un recuento de los recordatorios de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contiene la lista de rutas asociadas con la tarea. El usuario puede completar la tarea seleccionando cualquiera de las rutas de la lista de rutas.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Contiene el nombre de la ruta seleccionada cuando se completó la tarea.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contiene el ticket de imagen correspondiente a la tarea. Este ticket de imagen se utiliza en el campo de tarea imageUrl para obtener la imagen de la tarea del servidor.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre del servicio de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Contiene el título del servicio de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Creada (la tarea se ha creado desde el punto de inicio).<br /> 2 = Creada y guardada (la tarea se ha creado desde el punto de inicio y se ha guardado).<br /> 3 = Asignada (la tarea se ha asignado al usuario una vez iniciado el proceso).<br /> 4 = Asignada y guardada (la tarea se ha asignado y guardado).<br /> 100 = Completada (la tarea se ha completado).<br /> 101 = Con fecha límite (la tarea ha alcanzado la fecha límite).<br /> 102 = Terminada<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Contiene el nombre del conjunto de tareas durante el diseño del proceso.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contiene la URL de resumen de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>Es la lista de control de acceso de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>El ID de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se actualizó la tarea por última vez.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Contiene la URL del formulario de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contiene el tipo de formulario de la tarea. Con este campo, la tarea se representa en el cliente como un formulario pdf, swf, etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Si el valor es True, las acciones de ruta son visibles en Workspace.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Si el valor es True, las acciones como Reenviar, Consultar y Compartir son visibles en Workspace.<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>Si el valor es True, el formulario se puede cumplimentar sin conexión. Disponible únicamente para formularios pdf.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>Si el valor es True, el usuario puede guardar la tarea.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Este objeto contiene opciones que se utilizan para enviar formularios pdf a través de Reader cuando el formulario no contiene un botón de envío.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica si hay una imagen especificada para el proceso o no. El valor es True si no hay ninguna imagen asociada con el proceso; en caso contrario, es False.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Contiene la lista de tareas que se utilizan en la pestaña del historial de detalles de las tareas.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>El valor es True si el usuario que ha iniciado sesión es el propietario de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Contiene todas las acciones que se pueden realizar en una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Contiene todas las acciones de ruta disponibles para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandos como Reenviar, Compartir y Consultar si están disponibles para una tarea.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandos como Bloquear, Desbloquear, Abandonar, Devolver, Reclamar, etc., según estén disponibles.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Contiene información sobre la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contiene una matriz de objetos de variables de proceso, si los hay.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contiene la lista de tareas pendientes de la instancia de proceso de la tarea.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>Es una matriz de objetos. Cada objeto contiene detalles sobre la ruta y el mensaje de confirmación correspondiente, si lo hay.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>Es la URL de los datos del formulario de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Se trata de la configuración de los formularios de aplicaciones de terceros.<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>El valor es True si se envía la tarea.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>La lista de archivos adjuntos de una tarea.<br /> </td>
  </tr>
  <tr>
   <td>assignments<br /> </td>
   <td>T</td>
   <td>La lista de asignaciones de una tarea.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filter

   Filter es básicamente la cola de un usuario o grupo. Cuando se asigna una tarea al usuario o grupo, esta se agrega a la cola correspondiente.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>El valor es True si la cola es la cola predeterminada del usuario que ha iniciado sesión; en caso contrario, es False.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del propietario de la cola.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>El ID de la cola.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type</td>
   <td>F</td>
   <td>Contiene el tipo de la cola.<br /> 0 - Cola de usuario<br /> 1. Cola compartida<br /> 2. Cola de grupo<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contiene una consulta asociada a un filtro. Esta consulta se utiliza para buscar tareas de la lista de tareas completa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasks</td>
   <td>T</td>
   <td>Contiene una lista de todas las tareas que pertenecen a un filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fuera de la oficina

   Puede administrar la programación de Fuera de la oficina y controlar el flujo de tareas que le han sido asignadas en su ausencia.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong><br type="_moz" /> </td>
   <td><strong>Solo cliente</strong><br type="_moz" /> </td>
   <td><strong>Comentarios</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene los objetos de matriz de programación de Fuera de la oficina de un usuario. En cada objeto de programación, el campo startDate contiene la fecha de inicio de la programación y el campo endDate contiene la fecha de finalización. Si endDate es nulo en la programación, significa que el usuario no ha programado la fecha de finalización de la programación de Fuera de la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>El valor es True si no hay ningún designado principal en el caso de que el usuario esté fuera de la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>El valor es True si el usuario está fuera de la oficina.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene detalles del usuario que el usuario asigna como designado principal.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene una matriz de objetos para las designaciones Fuera de la oficina específicas del proceso. En cada objeto designado específico del proceso, processName contiene el nombre del proceso, isNotDesignated es True si no se asigna ningún usuario al proceso correspondiente y userDesignated es Null si no se asigna ningún otro detalle al usuario asignado al proceso correspondiente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de todos los procesos disponibles para el usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene la configuración inicial de Fuera de la oficina del usuario que se recuperó inicialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene configuraciones de Fuera de la oficina modificadas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene una lista de usuarios que han buscado los usuarios que han iniciado sesión hasta la fecha.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instancia de proceso

   Se crea una instancia de proceso cuando se invoca un proceso mediante Workspace o Workbench.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>La descripción de la instancia de proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>F</td>
   <td>El nombre del iniciador de la instancia de proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>El ID del iniciador de la instancia de proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se completó el proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID de la instancia de proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Iniciado<br /> 1 = En ejecución<br /> 2 = Completo<br /> 3 = Finalizado<br /> 4 = Terminado<br /> 5 = Finalización<br /> 6 = Suspendido<br /> 7 = Suspender<br /> 8 = Sin suspensión<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se inició el proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>La matriz de objetos de variables de proceso. Cada objeto de variable de proceso contiene un nombre, que es el nombre de la variable de proceso; un valor, que es el valor de la variable de proceso, y un tipo, que es el tipo de variable de proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasklist<br type="_moz" /> </td>
   <td>T</td>
   <td>Las tareas generadas por esta instancia de proceso<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nombre del proceso

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>La versión principal de un proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>La versión menor de un proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del proceso.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>El título del proceso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>La lista de instancias de proceso de este proceso<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto Task Assignment

   El objeto Task Assignment contiene información sobre la asignación de la tarea. A continuación, se muestran las propiedades de la asignación de la tarea.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se crea la asignación de una tarea<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Asignación inicial<br /> 1 = Reenviada (la tarea se ha reenviado al propietario actual de la tarea)<br /> 2 = Devuelta (el propietario anterior de la tarea ha devuelto la tarea a su propietario actual)<br /> 3 = Reclamada (la tarea ha sido reclamada por el propietario actual de la tarea)<br /> 4 = Escalación (la tarea se ha asignado al propietario actual de la tarea después de la escalación)<br /> 5 = Administrador asignado (el administrador ha asignado la tarea a su propietario actual)<br /> 6 = Consultada (Se ha consultado la tarea a su propietario actual)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se actualiza la asignación de una tarea<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID de cola del propietario actual de la tarea<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del propietario actual de la tarea<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID del propietario actual de la tarea<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto Task ACL

   El objeto Task ACL contiene información sobre los permisos de una tarea, como reenviar, compartir, consultar, etc. A continuación se muestran las propiedades del ACL de la tarea.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible agregar archivos adjuntos a la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible agregar notas a la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible reclamar la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible consultar la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible reenviar la tarea.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, es posible compartir la tarea.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Archivo adjunto de tarea

   Es posible agregar archivos adjuntos a una tarea. El archivo adjunto puede ser de tipo adjunto y nota. A continuación, se muestran las propiedades del objeto attachment.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que se creó el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID del usuario que agregó el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del usuario que agregó el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>Descripción<br type="_moz" /> </td>
   <td>F</td>
   <td>La descripción del archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID del archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>La marca de tiempo del momento en el que el archivo adjunto se modificó por última vez.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Si el valor es True, la nota es una nota ampliada (larga).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissions<br type="_moz" /> </td>
   <td>F</td>
   <td>Los permisos asociados a un archivo adjunto. allowRead es para el permiso de lectura, allowWrite es para el permiso de escritura y allowDelete es para el permiso de eliminación.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> </td>
   <td>F</td>
   <td>El tamaño del archivo adjunto en bytes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID de la tarea a la que se agrega el archivo adjunto.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>El tipo es un archivo adjunto para archivos y una nota para notas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene la fecha de creación del archivo adjunto según la configuración de la interfaz de usuario del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>La descripción formateada del archivo adjunto. Se utiliza para mostrar los caracteres especiales presentes en la descripción del archivo adjunto en AEM Forms Workspace.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>El nombre formateado del archivo adjunto. Se utiliza para mostrar los caracteres especiales presentes en el nombre del archivo adjunto en AEM Forms Workspace. Disponible únicamente para notas.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Usuario

   A continuación, se muestran las propiedades del objeto user.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Solo cliente</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>La dirección del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre común del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>La descripción del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>Lista del grupo del usuario.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre para mostrar del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID de correo electrónico del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>El valor es True si el usuario está fuera de la oficina<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>El apellido del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>El nombre de la organización del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>La dirección postal del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>El número de contacto del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>El número de contacto del usuario<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>El ID de inicio de sesión del usuario<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
