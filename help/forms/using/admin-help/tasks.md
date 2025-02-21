---
title: Trabajar con tareas
description: Utilice la página Búsqueda de Tareas para buscar tareas por nombre de usuario o ID de tarea. Más información sobre cómo trabajar con tareas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Trabajar con tareas {#working-with-tasks}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Utilice la página Búsqueda de Tareas para buscar tareas por nombre de usuario o ID de tarea. Los resultados de la búsqueda se muestran en la página Lista de tareas, donde puede acceder al historial de una tarea. También puede reasignar una tarea si un usuario tiene demasiadas tareas o si un usuario ha recibido una asignación de tarea por error.

>[!NOTE]
>
>Al realizar búsquedas de tareas, no se obtienen resultados para los nombres de usuario que comienzan con un signo de número (#). Si es posible, evite crear nombres de usuario que comiencen con un signo de número.

## Buscar tareas asociadas a un usuario {#search-for-tasks-associated-with-a-user}

1. En la consola de administración, haga clic en Servicios > Forms workflow > Búsqueda de tareas.
1. En Buscar por, seleccione Nombre de usuario. Si conoce parte del nombre de usuario que está buscando, escríbalo en el cuadro. Haga clic en Buscar usuario.
1. Aparecerá la página Buscar Usuario. Puede restringir aún más la búsqueda, buscando por nombre de usuario o correo electrónico. Cuando encuentre el usuario que está buscando, seleccione el botón de opción situado junto al nombre y haga clic en Aceptar.
1. De forma predeterminada, la búsqueda de tareas busca las tareas que están asignadas actualmente al usuario. Para buscar también tareas que se hayan asignado anteriormente al usuario, seleccione Mostrar tarea no asignada. Para buscar también tareas que haya completado el usuario, seleccione Mostrar tarea completada.
1. Haga clic en Buscar. Aparecerá la página Lista de tareas con el resultado de la búsqueda.

## Busque una tarea cuando conozca su ID de tarea {#search-for-a-task-when-you-know-its-task-id}

1. En la consola de administración, haga clic en Servicios > Forms workflow > Búsqueda de tareas.
1. En Buscar por, seleccione ID de tarea y escriba el ID de tarea en el cuadro.
1. Haga clic en Buscar. Aparecerá la página Lista de tareas con el resultado de la búsqueda.

## Trabajar con la lista de tareas {#working-with-the-task-list}

Los resultados de una búsqueda de tareas se muestran en la página Lista de tareas. Puede seleccionar una tarea para abrir la página Historial de tareas. Desde allí, puede asignar la tarea a otro usuario.

Las tareas se muestran con la siguiente información:

**Id. de tarea:** El entero positivo que el flujo de trabajo de formularios asigna cuando se crea una instancia de la tarea (iniciada por un usuario). Puede utilizar este identificador para realizar un seguimiento de la tarea a lo largo de su ciclo de vida. Haga clic en un ID de tarea para ver los detalles sobre el historial de tareas o para reasignar la tarea a otro usuario.

**Estado:** Asignado significa que la tarea está actualmente asignada al usuario. Sin asignar significa que la tarea se asignó anteriormente al usuario. El estado también puede ser Completado.

**Actividad:** Muestra el formulario y el nombre de una operación inicial o de la operación de proceso que generó la tarea.

**ID. de proceso:** Este entero positivo que el flujo de trabajo de formularios asigna cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia un proceso). Puede utilizar este identificador para realizar un seguimiento de la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso - Versión:** El nombre del proceso, tal como se define en Workbench.

**Aplicación:** Nombre de la aplicación a la que pertenece el proceso, tal como se define en Workbench.

**Fecha de creación:** Fecha y hora en que se creó la tarea.

## Ver el historial de tareas y reasignar tareas {#viewing-task-history-and-reassigning-tasks}

La página Historial de tareas muestra una lista de los usuarios y grupos que se han asignado a una tarea determinada.

Para cada asignación de tarea, la lista muestra la siguiente información:

**Nombre:** El nombre del usuario.

**Estado:** asignado significa que la tarea está asignada actualmente al usuario. Sin asignar significa que la tarea se asignó anteriormente al usuario.

**Id. de lista de trabajo:** Identificador numérico de la cola de usuario a la que pertenece la tarea. Un proceso se puede compartir entre varios usuarios.

**Tipo:** Indica cómo se asignó la tarea:

**Inicial:** Al usuario se le asignó originalmente la tarea.

**Reenviar:** El propietario original de la tarea asignó la tarea a otro usuario.

**Rechazar:** Se rechazó una tarea reenviada o se devolvió una tarea a una lista de trabajo sin haberse completado.

**Notificación:** El usuario reclamó la tarea en una lista de trabajo compartida.

**Escalación:** Transcurrió un tiempo predeterminado (tal como se establece en la acción del usuario en Workbench) sin la interacción del usuario y se asignó la tarea a otro usuario.

**Consultar:** El propietario de la tarea ha reenviado esta tarea a otro usuario para su consulta, que puede abrir el formulario, guardar datos, modificar los archivos adjuntos y las notas, pero no puede completar el paso. El usuario debe devolver la tarea al propietario de la tarea que consultó con el usuario.

**Reasignación de administrador:** Un administrador reasignó la tarea.

**Fecha de asignación:** Fecha y hora en que se asignó la tarea al usuario.

### Asignar un nuevo usuario a una tarea {#assigning-a-new-user-to-a-task}

La página Asignar usuario enumera los usuarios que pueden asignarse a una tarea. Para acceder a la página Asignar usuario, haga clic en Asignar nuevo usuario en la página Historial de tareas.

1. En el cuadro Buscar de la página Asignar usuario, escriba parte o toda la dirección de correo electrónico o nombre de usuario necesarios.
1. En Utilizando, seleccione Nombre o Dirección de correo electrónico y, a continuación, haga clic en Buscar. Se muestran los usuarios que coinciden con la búsqueda.
1. Seleccione el usuario de la lista y haga clic en Aceptar. Aparecerá la página Historial de tareas con la nueva asignación de usuario.
