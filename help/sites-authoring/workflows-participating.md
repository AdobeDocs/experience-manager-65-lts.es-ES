---
title: Participación en flujo de trabajo
description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso.
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
exl-id: 2680e967-ec04-4ae6-b379-f1f0e7c6606b
source-git-commit: 21c5407d1153fa23a3e8b60487eb91f1c3101337
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 73%

---

# Participación en flujos de trabajo{#participating-in-workflows}

Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo. El usuario recibe una notificación y puede realizar las acciones adecuadas:

* [Visualización de notificaciones &#x200B;](#notifications-of-available-workflow-actions)
* [Finalización de una etapa de participante &#x200B;](#completing-a-participant-step)
* [Delegación de una etapa de participante &#x200B;](#delegating-a-participant-step)
* [Realización de una etapa hacia atrás en una etapa de participante &#x200B;](#performing-step-back-on-a-participant-step)
* [Apertura de un elemento de flujo de trabajo para ver los detalles (y tomar medidas) &#x200B;](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualización de la carga útil del flujo de trabajo (varios recursos) &#x200B;](#viewing-the-workflow-payload-multiple-resources)

## Notificaciones de acciones de flujo de trabajo disponibles {#notifications-of-available-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* Su indicador [notification](/help/sites-authoring/inbox.md) (barra de herramientas) se incrementará:

  ![Indicador de notificación](do-not-localize/wf-57.png)

* El elemento figurará en la [Bandeja de entrada](/help/sites-authoring/inbox.md) de notificaciones:

  ![wf-58](assets/wf-58.png)

* Cuando utilice el editor de páginas, la barra de estado mostrará lo siguiente:

   * Nombre de los flujos de trabajo que se están aplicando a la página; por ejemplo, Solicitud de activación.
   * Las acciones disponibles para el usuario actual para el paso actual del flujo de trabajo; por ejemplo, Completar, Delegar, Ver detalles.
   * El número de flujos de trabajo a los que está sujeta la página. Puede hacer lo siguiente:

      * utilice las flechas izquierda/derecha para navegar por la información de estado de los distintos flujos de trabajo.
      * haga clic en el número real para abrir una lista desplegable de todos los flujos de trabajo aplicables y, a continuación, seleccione el flujo de trabajo que desee mostrar en la barra de estado.

  ![wf-59](assets/wf-59.png)

  >[!NOTE]
  >
  >La barra de estado solo es visible para los usuarios con privilegios de flujo de trabajo; por ejemplo, los miembros del grupo `workflow-users`.
  >
  >
  >Las acciones se muestran cuando el usuario actual está directamente involucrado en el paso actual del flujo de trabajo.

* Cuando **Cronología** está abierta para el recurso, se muestra el paso del flujo de trabajo. Al hacer clic en el titular de la alerta, también se mostrarán las acciones disponibles:

  ![captura de pantalla_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Puede completar un elemento para permitir que el flujo de trabajo vaya al paso siguiente.

En esta acción puede indicar lo siguiente:

* **Etapa siguiente**: la etapa siguiente que se debe seguir; puede seleccionarla de la lista proporcionada
* **Comentario**: si es necesario

Puede completar un paso de participante desde:

* [la bandeja de entrada](#completing-a-participant-step-inbox)
* [el Editor de página](#completing-a-participant-step-page-editor)
* [Escala de cronología](#completing-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Finalización de una etapa de participante: bandeja de entrada {#completing-a-participant-step-inbox}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (haga clic en la miniatura).
1. Seleccione **Completar** en la barra de herramientas.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione **Siguiente paso** del selector desplegable y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Finalización de una etapa de participante: editor de la página {#completing-a-participant-step-page-editor}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Completar** de la barra de estado situada en la parte superior.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione **Siguiente paso** del selector desplegable y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Finalización de una etapa de participante: cronología {#completing-a-participant-step-timeline}

También puede utilizar la cronología para completar y avanzar un paso:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).

   ![captura de pantalla_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. Haga clic en el banner de alerta para mostrar las acciones disponibles. Seleccione **Avanzar**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. Según el flujo de trabajo, puede seleccionar la siguiente etapa:

   ![captura de pantalla_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. Seleccione **Asignar** para confirmar la acción.

### Delegación de una etapa de participante  {#delegating-a-participant-step}

Si se le ha asignado un paso, pero por cualquier motivo no puede realizar ninguna acción, puede delegar el paso a otro usuario o grupo.

Los usuarios que están disponibles para la delegación dependen de quién haya sido asignado el elemento de trabajo:

* Si el elemento de trabajo se asignó a un grupo, los miembros del grupo están disponibles.
* Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
* Si el elemento de trabajo se asignó a un único usuario, el elemento de trabajo no se puede delegar.

En esta acción puede indicar lo siguiente:

* **Usuario**: el usuario al que desea delegar; puede seleccionar de una lista proporcionada
* **Comentario**: si es necesario

Puede delegar una etapa de participante desde:

* [la bandeja de entrada](#delegating-a-participant-step-inbox)
* [el Editor de página](#delegating-a-participant-step-page-editor)
* [Escala de cronología](#delegating-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegación de una etapa de participante: bandeja de entrada {#delegating-a-participant-step-inbox}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (haga clic en la miniatura).
1. Seleccione **Delegar** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo. Especifique el **Usuario** del selector desplegable (también puede ser un grupo) y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Delegación de una etapa de participante: editor de páginas {#delegating-a-participant-step-page-editor}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Delegar** de la barra de estado situada en la parte superior.
1. Se abrirá el cuadro de diálogo. Especifique el **Usuario** del selector desplegable (también puede ser un grupo) y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Delegación de una etapa de participante: cronología {#delegating-a-participant-step-timeline}

También puede utilizar la cronología para delegar o asignar un paso:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).
1. Haga clic en el banner de alerta para mostrar las acciones disponibles. Seleccionar **Cambiar asignación**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. Especifique un nuevo usuario para la asignación:

   ![captura de pantalla_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. Seleccione **Asignar** para confirmar la acción.

### Realización de un paso hacia atrás durante el paso de participante {#performing-step-back-on-a-participant-step}

Si descubre que un paso o una serie de pasos debe repetirse, puede retroceder. Esto permite seleccionar un paso que se produjo anteriormente en el flujo de trabajo para volver a procesarlo. El flujo de trabajo vuelve al paso especificado y continúa desde ahí.

En esta acción puede indicar lo siguiente:

* **Paso anterior**: el paso al que se va a devolver; puede seleccionar de una lista proporcionada
* **Comentario**: si es necesario

Puede volver a un paso anterior en un paso de participante desde:

* [la bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [el Editor de página](#performing-step-back-on-a-participant-step-page-editor)
* [Escala de cronología](#performing-step-back-on-a-participant-step-timeline)
* al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Retroceder en un paso de participante: bandeja de entrada {#performing-step-back-on-a-participant-step-inbox}

Utilice el siguiente procedimiento para retroceder:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (haga clic en la miniatura).
1. Seleccione **Retroceder** para abrir el cuadro de diálogo. 

1. Especifique el **Paso anterior** y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Retroceder en un paso de participante: editor de la página {#performing-step-back-on-a-participant-step-page-editor}

Utilice el siguiente procedimiento para retroceder:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Retroceder** de la barra de estado situada en la parte superior.
1. Especifique el **Paso anterior** y agregue un **Comentario** si es necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Retroceder en un paso de participante: cronología {#performing-step-back-on-a-participant-step-timeline}

También puede utilizar la cronología para retroceder a un paso anterior:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).
1. Haga clic en el banner de alerta para mostrar las acciones disponibles. Seleccione **Restablecer**:

   ![captura de pantalla_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. Especifique la etapa a la que debe restablecerse el flujo de trabajo:

   ![captura de pantalla_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. Seleccione **Restablecer** para confirmar la acción.

### Apertura de un elemento de flujo de trabajo para ver los detalles (y tomar medidas)  {#opening-a-workflow-item-to-view-details-and-take-actions}

Vea los detalles del elemento de trabajo del flujo de trabajo y realice las acciones adecuadas.

Los detalles del flujo de trabajo se muestran en las pestañas, y las acciones adecuadas están disponibles en la barra de herramientas:

* Ficha **ELEMENTO DE TRABAJO:**

  ![wf-72](assets/wf-72.png)

* Pestaña **INFORMACIÓN DEL FLUJO DE TRABAJO**:

  ![wf-73](assets/wf-73.png)

  Si se han configurado [fases de flujo de trabajo](/help/sites-developing/workflows.md#workflow-stages) para el modelo, puede ver el progreso según los siguientes elementos:

  ![wf-107](assets/wf-107.png)

* Pestaña **COMENTARIOS**:

  ![wf-75](assets/wf-75.png)

Puede abrir los detalles del elemento de trabajo desde las ubicaciones siguientes:

* [la bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [el Editor de página](#performing-step-back-on-a-participant-step-page-editor)

#### Apertura de los detalles del flujo de trabajo: bandeja de entrada {#opening-workflow-details-inbox}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (haga clic en la miniatura).
1. Seleccione **Abrir** para abrir las pestañas de información. 

1. Si es necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice las opciones **Guardar** o **Cancelar** para salir.

#### Apertura de los detalles del flujo de trabajo: editor de página {#opening-workflow-details-page-editor}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la [página para editarla](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleccione **Ver detalles** de la barra de estado para abrir las pestañas de información. 

1. Si es necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice las opciones **Guardar** o **Cancelar** para salir.

### Visualización de la carga útil del flujo de trabajo (varios recursos)  {#viewing-the-workflow-payload-multiple-resources}

Puede ver los detalles de la carga útil asociada con la instancia de flujo de trabajo. Inicialmente, se muestran los recursos del paquete y luego puede explorar en profundidad para mostrar las páginas individuales.

Para ver la carga útil y los recursos de la instancia del flujo de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-authoring/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (haga clic en la miniatura).
1. Seleccione **Ver carga útil** de la barra de herramientas para abrir el cuadro de diálogo. 

   Dado que un paquete de flujo de trabajo es simplemente una colección de punteros a rutas dentro del repositorio, puede añadir, quitar o modificar las entradas aquí para ajustar los elementos a los que el paquete de flujo de trabajo hace referencia. Utilice el componente **Definición de recursos** para añadir nuevas entradas.

   ![wf-78](assets/wf-78.png)

1. Los vínculos se pueden utilizar para abrir las páginas individuales.
