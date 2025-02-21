---
title: Descripción de los componentes reutilizables
description: Una lista completa de componentes reutilizables con nombres de archivo y dependencias para ayudarle a integrar el componente de espacio de trabajo de AEM Forms en sus aplicaciones web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 100%

---

# Descripción de los componentes reutilizables {#description-of-reusable-components}

El espacio de trabajo de AEM Forms está compuesto por componentes [reutilizables](/help/forms/using/integrating-html-ws-components-web.md) organizados en una [estructura de carpetas](/help/forms/using/folder-structure.md) en CRX™. Cada componente tiene un modelo, una vista y una plantilla en la ubicación especificada en la estructura de carpetas, dependencias JavaScript™ de otros archivos de componentes, eventos escuchados por el componente y objetos JavaScript que activan estos eventos en AEM Forms Workspace. La lista completa de componentes reutilizables con nombres de archivo y dependencias constituyentes se proporciona aquí.

## TaskList {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>Tarea</p></li>
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>filterSelected: modelo tasklist</p></li>
     <li><p>quitar: modelo tasklist</p></li>
     <li><p>updateQueue: modelo tasklist</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente se puede utilizar de forma independiente de AEM Forms Workspace, siempre que active el evento filterSelected para este componente desde la aplicación personalizada.

## Tarea {#task}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo tasklist</p></li>
     <li><p>utilidad taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>submitComplete: modelo de tareas</p></li>
     <li><p>Rechazar: modelo de tareas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El espacio de trabajo llama a la función fetchTasks del modelo TaskList para crear modelos de tareas para este componente.

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>fetched: modelo tasklist </p></li>
     <li><p>quitar: modelo tasklist </p></li>
     <li><p>updateQueue: modelo tasklist </p></li>
     <li><p>refreshedQueue: modelo tasklist </p></li>
     <li><p>filterSelected: modelo tasklist</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## Filtro {#filter}

<table>
 <tbody>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>Field: queue: { name, qid, isDefault, type}</p> </li>
     <li><p>Field: query: string</p> </li>
     <li><p>Field: parentView: filterlist view</p> </li>
     <li><p>Field: parentModel: tasklist model</p> </li>
     <li><p>Field: utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>teamqueue.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>teamqueue.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>fetched: modelo tasklist </p></li>
     <li><p>quitar: modelo tasklist </p></li>
     <li><p>updateQueue: modelo tasklist </p></li>
     <li><p>teamQueuesFetched: modelo tasklist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>Extends : filter view</p> </li>
     <li><p>Field : queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>Field : query : string</p> </li>
     <li><p>Field : parentView : filterlist view</p> </li>
     <li><p>Field : parentModel : tasklist model</p> </li>
     <li><p>Field : utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter obtiene el evento que indica qué tarea se ha seleccionado del componente TaskList. Aunque estos componentes comparten la clase de modelo, no hay otra dependencia.

## TaskDetails {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>La mayoría de las clases de utilidades</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utilidad formrendering</p> </li>
     <li><p>utilidad notas</p> </li>
     <li><p>utilidad archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
     <li><p>utilidad historial</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li><p>reenviado: modelo de tareas</p> </li>
     <li><p>compartido: modelo de tareas</p> </li>
     <li><p>consultado: modelo de tareas</p> </li>
     <li><p>rechazado: modelo de tareas</p> </li>
     <li><p>abandonado: modelo de tarea</p> </li>
     <li><p>desbloqueado: modelo de tareas</p> </li>
     <li><p>bloqueado: modelo de tareas</p> </li>
     <li><p>reclamado: modelo de tarea</p> </li>
     <li><p>Change:taskselected: modelo tasklist</p> </li>
     <li><p>change:formUrl: modelo de tareas</p> </li>
     <li>attachmentURLFetched: modelo de tareas</li>
    </ul>
    <ul>
     <li>newAttachment: modelo de tareas</li>
     <li><p>taskHistoryFetched: modelo de tareas</p> </li>
     <li>prepareForSubmitComplete: modelo de tareas</li>
     <li><p>submitComplete: modelo de tareas</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startProcess.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>Categoría</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo favoritecategoryfactory</p></li>
     <li><p>modelo allcategoryfactory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched: modelo tasklist </p></li>
     <li><p>agregar: modelo categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente utiliza clases de modelo de otros componentes, como StartPointList, StartPoint y Task. Además de esta dependencia, CategoryList puede utilizarse de forma independiente.

## Categoría {#category}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo categorylist</p></li>
     <li><p>modelo startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>changed: modelo category </p></li>
     <li><p>childrenFetched: modelo category </p></li>
     <li><p>category:selected: modelo categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startProcess.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de categoría</p></li>
     <li><p>modelo favoritecategoryfactory</p></li>
     <li><p>modelo allcategoryfactory</p></li>
     <li><p>vista startpoint</p></li>
     <li><p>modelo startpointlist</p></li>
     <li><p>modelo startpoint</p></li>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo de tareas</p></li>
     <li><p>modelo tasklist</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>category:selected: modelo categorylist </p></li>
     <li><p>allStartpointsFetched: modelo tasklist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartPointList y CategoryList comparten la clase de modelo, por lo que la primera depende de la segunda. CategoryList accede a la información sobre los puntos de inicio de la categoría que se muestran. Para utilizar StartPointList de forma independiente, simule el activador de evento de CategoryList.

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo de tarea</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td><p>cambiar: modelo startpoint </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>startProcess.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>startProcess.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td>
    <ul>
     <li><p>La mayoría de las clases de utilidades</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>
    <ul>
     <li><p>modelo de categoría</p> </li>
     <li><p>modelo favoritecategoryfactory</p> </li>
     <li><p>modelo allcategoryfactory</p> </li>
     <li><p>utilidad formrendering</p> </li>
     <li><p>utilidad notas</p> </li>
     <li><p>utilidad archivos adjuntos</p> </li>
     <li><p>utilidad taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li><p>category:selected: modelo categorylist</p> </li>
     <li><p>change:invokedTask: modelo startpointlist</p> </li>
     <li><p>change:formUrl: modelo de tareas</p> </li>
     <li><p>Startpoint:selected: modelo startpointlist</p> </li>
     <li><p>reenviado: modelo de tareas</p> </li>
     <li><p>abandonado: modelo de tarea</p> </li>
     <li><p>desbloqueado: modelo de tareas</p> </li>
     <li><p>bloqueado: modelo de tareas</p> </li>
     <li>attachmentURLFetched: modelo de tareas</li>
     <li>newAttachment: modelo de tareas</li>
     <li>prepareForSubmitComplete: modelo de tareas </li>
     <li><p>submitComplete: modelo de tareas</p> </li>
     <li><p>allStartpointsFetched: modelo tasklist</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los componentes StartProcess y StartPointList comparten la clase de modelo. Este componente se vuelve relevante si selecciona un punto de inicio de StartPointList.

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tracking.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>agregar: modelo processnamelist </p></li>
     <li><p>Fetched:processnames: modelo processnamelist </p></li>
     <li><p>cambiar: modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList no depende de otros componentes. Sin embargo, depende internamente de la clase del modelo ProcessInstanceList que a su vez depende de otros componentes. Por lo tanto, ProcessNameList utiliza muchas clases de modelo como ProcessInstanceList, ProcessInstance, TaskList, Teamtask y Task. Además de estas dependencias, ProcessNameList puede utilizarse de forma independiente.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processname (en processnamelist.js)</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td><p>cambiar: modelo processname  </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>tracking.html (en la carpeta de ruta)</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>Processname:selected: modelo processnamelist </p></li>
     <li><p>Processname:instancesfetched: modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera un evento de ProcessNameList que indica el nombre del proceso para recuperar y mostrar instancias. Para utilizar ProcessInstanceList de forma independiente, simule el activador de eventos por separado.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processname dentro de processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>modelo tasklist</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td><p>cambiar: modelo processinstance  </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td>
    <ul>
     <li><p>modelo processname</p></li>
     <li><p>utilidad historial</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>Processname:selected: modelo processnamelist </p></li>
     <li><p>Processinstance:selected: modelo processinstancelist </p></li>
     <li><p>tasksFetched: modelo processinstance  </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera un evento de ProcessInstanceList que indique qué historial de instancias de proceso se va a mostrar. Además de esta dependencia, el componente se puede utilizar de forma independiente.

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched: modelo outofoffice</p> </li>
     <li><p>outOfOfficeSettingsSaved: modelo outofoffice </p> </li>
     <li><p>processesFetched: modelo outofoffice </p> </li>
     <li><p>principalSelected: vista principalsearch </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice puede utilizarse de forma independiente.

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted: modelo sharequeue</p> </li>
     <li><p>queueAccessRequested: modelo sharequeue</p> </li>
     <li><p>grantedUsersFetched: modelo sharequeue</p> </li>
     <li>accessibleUsersFetched: modelo sharequeue</li>
     <li><p>queueAccessRevoked: modelo sharequeue</p> </li>
     <li><p>queueAccessRemoved: modelo sharequeue</p> </li>
     <li><p>principalSelected: vista principalsearch</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue se puede usar de forma independiente.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched: modelo uisettings </p></li>
     <li><p>settingUpdated: modelo uisettings  </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings se puede usar de forma independiente.

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados</p></td>
   <td><p>ND</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation puede utilizarse de forma independiente.

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched: modelo userinfo</li>
     <li>sessionRenewed: modelo userinfo <br /> </li>
     <li>sessionExpired: modelo userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo se puede utilizar de forma independiente.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Ver</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Plantilla</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p></td>
   <td><p>newWsError: modelo wserror </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td>
    <ul>
     <li>principalSearched: modelo principalsearch </li>
     <li>outOfOfficeInfoFetched: modelo usersearch </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplate (en searchtemplatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td><p>templateFetched: modelo searchtemplate </p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>tracking.html (en la carpeta de ruta)</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td><p>modelo searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td><p>Cambiar: modelo searchtemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Ver</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Plantilla</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requiere componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependencias de JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventos escuchados (Nombre del evento: Activador)</p> </td>
   <td><p>searchTemplate:selected: modelo searchtemplate</p> </td>
  </tr>
 </tbody>
</table>
