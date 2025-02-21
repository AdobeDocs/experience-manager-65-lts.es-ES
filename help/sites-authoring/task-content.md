---
title: Uso de tareas
description: Las tareas representan elementos de trabajo por realizar en el contenido y se utilizan en los proyectos para determinar el nivel de compleción de las tareas actuales
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 41%

---


# Uso de tareas {#working-with-tasks}

Las tareas representan elementos de trabajo que deben realizarse con respecto al contenido. Cuando se le asigna una tarea, esta aparece en la bandeja de entrada del flujo de trabajo. Los elementos de tarea se pueden distinguir de los elementos de flujo de trabajo por el valor de la columna **Type**.

Las tareas también se utilizan en los proyectos para determinar el nivel de integridad del proyecto.

## Seguimiento del progreso del proyecto {#tracking-project-progress}

Puede realizar un seguimiento del progreso del proyecto si observa las tareas activas o completadas dentro de un proyecto representado por el mosaico **Tareas**. El progreso del proyecto puede determinarse por lo siguiente:

* **Mosaico de tareas:** En el mosaico de tareas, disponible en la página de detalles del proyecto, se muestra un progreso general del proyecto.

* **Lista de tareas:** Al hacer clic en el mosaico de tareas, se muestra una lista de tareas. Esta lista contiene información detallada sobre todas las tareas relacionadas con el proyecto.

Ambas opciones enumeran las tareas de flujo de trabajo y las tareas que cree directamente en el mosaico de tareas.

### Mosaico Tarea {#task-tile}

Si un proyecto tiene tareas relacionadas, se muestra un mosaico de tareas dentro del proyecto. El mosaico de tareas muestra el estado actual del proyecto. Esto se basa en las tareas existentes dentro del flujo de trabajo y no incluye ninguna tarea que se genere en el futuro a medida que este avance. La siguiente información está visible en el mosaico de la tarea:

* Porcentaje de tareas completadas
* Porcentaje de tareas activas
* Porcentaje de tareas vencidas

![Mosaico de tareas](assets/project-tile-tasks.png)

### Ver o modificar las tareas de un proyecto {#viewing-or-modifying-the-tasks-in-a-project}

Además de realizar el seguimiento del progreso, es posible que también desee ver más información sobre el proyecto o modificarlo.

#### Lista de tareas {#task-list}

Haga clic en el botón de los tres puntos de la parte inferior derecha del mosaico de tareas para mostrar la bandeja de entrada filtrada en las tareas relacionadas con el proyecto. Los detalles de la tarea se muestran junto con los metadatos como la fecha de vencimiento, el usuario asignado, la prioridad y el estado.

![Bandeja de entrada de tarea de proyecto](assets/project-tasks.png)

#### Detalles de la tarea {#task-details}

Para obtener más información sobre una tarea en particular, en la bandeja de entrada, haz clic en la tarea para seleccionarla y luego haz clic en **Abrir** en la barra de herramientas.

![Detalle de la tarea](assets/project-task-detail.png)

Puede ver, editar o agregar detalles a la tarea a través de diferentes pestañas.

* **Tarea** - Información general de la tarea
* **Información del proyecto** - Resumen del proyecto con el que está asociada la tarea
* **Información de flujo de trabajo**: resumen del flujo de trabajo al que está asociada la tarea (si corresponde)
* **Comentarios**: comentarios generales sobre la propia tarea

### Adición de tareas {#adding-tasks}

Puede agregar nuevas tareas a los proyectos. A continuación, estas tareas aparecen en el mosaico de tareas y están disponibles en la bandeja de entrada de notificaciones para que tenga en cuenta las tareas pendientes.

Para añadir una tarea, haga lo siguiente:

1. En el proyecto, busque el mosaico **Tareas**
1. Haga clic en las comillas angulares hacia abajo en la parte superior derecha del mosaico y seleccione **Crear tarea**.
1. En la ventana **Agregar tarea**, proporcione detalles de la tarea, como la prioridad, el usuario asignado y la fecha de vencimiento.

   ![Agregando una tarea](assets/project-add-task.png)

1. Haga clic en **Enviar**.

## Trabajar con tareas en la bandeja de entrada {#working-with-tasks-in-the-inbox}

En lugar de tener acceso a las tareas del proyecto desde el propio proyecto, puede tener acceso a ellas directamente desde la bandeja de entrada. La bandeja de entrada le ofrece una descripción general de las tareas de los distintos proyectos para que pueda comprender todo el flujo de trabajo.

Desde la bandeja de entrada, puede abrir las tareas y establecer su estado. Las tareas también aparecen en la bandeja de entrada cuando se asignan a un grupo de usuarios al que pertenece. En este caso, cualquier miembro del grupo puede realizar el trabajo y completar la tarea.

![Bandeja de entrada](assets/project-inbox.png)

Para completar una tarea, selecciónela y haga clic en **Completar** en la barra de herramientas. Añada información a la tarea y, a continuación, haga clic en **Hecho**. Consulte la [bandeja de entrada](/help/sites-authoring/inbox.md) para obtener más información.
