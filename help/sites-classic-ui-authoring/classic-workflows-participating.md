---
title: Participación en flujos de trabajo
description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 39%

---

# Participación en flujos de trabajo{#participating-in-workflows}

Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo.

## Procesamiento de elementos de trabajo {#processing-your-work-items}

Puede realizar las siguientes acciones para procesar un elemento de trabajo:

* **Completar**

  Puede completar un elemento para permitir que el flujo de trabajo vaya al paso siguiente.

* **Delegar**

  Si se le ha asignado un paso, pero por cualquier motivo no puede realizar ninguna acción, puede delegar el paso a otro usuario o grupo.

  Los usuarios que están disponibles para la delegación dependen de quién haya sido asignado el elemento de trabajo:

   * Si el elemento de trabajo se asignó a un grupo, los miembros del grupo están disponibles.
   * Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
   * Si el elemento de trabajo se asignó a un único usuario, el elemento de trabajo no se puede delegar.

* **Retroceder**

  Si descubre que un paso o una serie de pasos debe repetirse, puede retroceder. Esto permite seleccionar un paso que se produjo anteriormente en el flujo de trabajo para volver a procesarlo. El flujo de trabajo vuelve al paso especificado y continúa desde ahí.

## Participar en un flujo de trabajo {#participating-in-a-workflow}

### Notificaciones de acciones de flujo de trabajo asignadas {#notifications-of-assigned-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* La columna **Estado** de la consola Sitios web indica cuándo una página está en un flujo de trabajo:

  ![workflowstatus-1](assets/workflowstatus-1.png)

* Cuando a usted o a un grupo al que pertenece se le asigna un elemento de trabajo como parte de un flujo de trabajo, este aparece en la bandeja de entrada del flujo de trabajo de AEM.

  ![workflowinbox](assets/workflowinbox.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Después de realizar la acción indicada, puede completar el elemento de trabajo, lo que permite que el flujo de trabajo continúe. Utilice el siguiente procedimiento para completar el elemento de trabajo.

1. Seleccione el paso del flujo de trabajo y haga clic en el botón **Completar** de la barra de navegación superior.
1. En el cuadro de diálogo resultante, seleccione **Siguiente paso**; es decir, el paso que se ejecutará a continuación. Una lista desplegable muestra todos los destinos adecuados. **También se puede escribir un comentario**.

   ![flujo de trabajo completado](assets/workflowcomplete.png)

   El número de pasos enumerados depende del diseño del modelo del flujo de trabajo.

1. Haga clic en **Aceptar** para confirmar la acción.

### Delegación de una etapa de participante  {#delegating-a-participant-step}

Utilice el siguiente procedimiento para delegar un elemento de trabajo.

1. Haga clic en el botón **Delegar** de la barra de navegación superior.
1. En el cuadro de diálogo, utilice la lista desplegable para seleccionar el **Usuario** al que delegar el elemento de trabajo. También puede agregar un **comentario**.

   ![delegado de flujo de trabajo](assets/workflowdelegate.png)

1. Haga clic en **Aceptar** para confirmar la acción.

### Realización de un paso hacia atrás durante el paso de participante {#performing-step-back-on-a-participant-step}

Utilice el siguiente procedimiento para retroceder.

1. Haga clic en el botón Retroceder de la barra de navegación superior.
1. En el cuadro de diálogo resultante, seleccione el Paso anterior; es decir, el paso que se ejecutará a continuación, aunque sea un paso que se produzca anteriormente en el flujo de trabajo. Una lista desplegable muestra todos los destinos adecuados.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Haga clic en OK para confirmar la acción.
