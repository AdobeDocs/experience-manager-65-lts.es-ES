---
title: Consultas ad hoc en informes de procesos
description: Cree consultas personalizadas para buscar AEM Forms en los detalles de procesos y tareas de JEE en la Creación de informes de procesos
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 7380be9a-7f5c-46df-97f8-6309daa2a566
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 96%

---

# Consultas ad hoc en informes de procesos{#ad-hoc-queries-in-process-reporting}

## Crear informes de consultas Ad hoc en proceso {#ad-hoc-queries-in-process-reporting-1}

Las consultas Ad hoc en los informes de procesos le permiten crear consultas personalizadas que puede utilizar para buscar detalles de procesos y tareas de las instancias de procesos de AEM Forms definidas en su entorno de AEM Forms.

Además, las consultas Ad hoc se pueden definir mediante filtros de propiedades de procesos y tareas. Estos filtros se pueden guardar y utilizar para ejecutar los informes más adelante.

[**Buscar el proceso**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p): busque instancias de proceso con un filtro de búsqueda definido por el usuario basado en atributos de proceso.

[**Detalles del proceso**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p): consulte los detalles de una instancia de proceso al especificar el ID de proceso.

**Buscar tareas**: busque instancias de tareas con un filtro de búsqueda definido por el usuario basado en atributos de tareas.

**Detalles de la tarea**: para ver los detalles de una instancia de tarea, especifique el ID de la tarea.

### Procesos y tareas {#processes-and-tasks}

Los pasos que sigue para crear filtros y ejecutar consultas para detalles del proceso son los mismos que para las tareas.

Esto significa que las interfaces de usuario para la búsqueda de procesos y la búsqueda de tareas difieren únicamente en los campos por los que puede buscar y en los devueltos en los resultados de búsqueda. Esto se debe simplemente a que, aunque muchos de los campos son idénticos, algunos son específicos de los procesos y otros son específicos de las tareas.

Este artículo detalla las descripciones de las secciones Proceso/Búsqueda de tareas y Detalles de procesos/tareas. En los lugares apropiados, se indicarán específicamente las diferencias.

## Búsqueda de procesos/tareas {#process-task-search}

La búsqueda de procesos/tareas se utiliza para definir filtros para consultar instancias de proceso/tarea.

### Crear una consulta de búsqueda de proceso/tarea {#to-create-a-process-task-search-query}

1. Para ver las consultas guardadas sobre Búsqueda de procesos/tareas o para crear una consulta, haga clic en **Consultas Ad hoc** y haga clic en **Búsqueda de procesos/tareas**.

   ![search_nodes](assets/search_nodes.png)

   El panel **Mis filtros** se muestra a la derecha de la vista de árbol.

   En el panel **Mis filtros**, puede crear nuevas consultas Ad hoc y hacer clic en para ejecutar consultas guardadas anteriormente.

   ![my_filters_panel](assets/my_filters_panel.png)

1. Para ejecutar una consulta existente, simplemente haga clic sobre la consulta en el panel **Mis filtros**.
1. Para crear una consulta, haga clic en **Agregar** (+).

   Se mostrará el panel **Crear filtro**.

   ![create_filter_panel](assets/create_filter_panel.png)

   Una consulta consta de uno o más filtros de consulta. Para crear un filtro, agregue una fila de filtro a la consulta. De forma predeterminada, se agregará una fila de filtro a la consulta.

   **Definir un filtro**

   1. Seleccione un campo.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >La lista de campos contiene los campos específicos del proceso o la tarea de AEM Forms.

   1. Seleccione una condición.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >Las condiciones enumeradas dependen del atributo seleccionado para el filtrado.

   1. Escriba un valor.

      ![filter_value](assets/filter_value.png)

   1. Para agregar otro filtro a la consulta, haga clic en **Agregar (+)** a la derecha de la fila de filtro.

      Para quitar un filtro de la consulta, haga clic en **Eliminar (-)** a la derecha de la fila de filtro.

      ![filter_add_del](assets/filter_add_del.png)

Después de crear una consulta, utilice las opciones de la esquina superior derecha del panel **Crear filtro** para lo siguiente:

* **Cancelar**: cancelar los cambios y volver al panel **Mis filtros**.
* **Ejecutar**: ejecute la consulta actual para ver y / o comprobar los resultados. En este caso, no es necesario guardar la consulta antes de ejecutarla. Puede comprobar los resultados, realizar cambios si es necesario y, a continuación, guardar la consulta cuando esté satisfecho con el resultado.
* **Guardar**: guarde el filtro. El filtro se puede ver y ejecutar desde el panel **Mis filtros**.

### Opciones en el panel Mis filtros {#options-in-my-filters-panel}

Utilice las opciones del panel **Mis filtros** para **Agregar** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Editar** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png) o **Eliminar** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png) una consulta Ad hoc.

![my_filters_options](assets/my_filters_options.png)

### Ejecutar una consulta de búsqueda {#to-execute-a-search-query}

1. Para ejecutar una consulta, haga clic en el filtro en el panel **Mis filtros** o haga clic en el botón **Ejecutar** si crea o edita un filtro.
1. Los resultados de la consulta se muestran en el panel **Informe** de la ventana **Informes de procesos**.

   ![process_search_result](assets/process_search_result.png)

   Puede paginar los resultados de la búsqueda con la ayuda del panel de paginación que se muestra en la parte inferior del informe.

   ![process_result_pgn](assets/process_result_pgn.png)

   En la lista desplegable **Mostrar**, elija el número de resultados que desea mostrar por página.

   En el cuadro de texto **Página**, escriba un número de página para ir directamente a ella.

1. Los siguientes campos se muestran en un resultado de búsqueda de proceso:

   * **ID de proceso**: ID del proceso. El campo contiene un hipervínculo. Si hace clic en un ID de proceso en este campo, se le redirigirá al panel **[!UICONTROL Detalles del proceso]** para el proceso.
   * **Iniciador**: el usuario de AEM Forms que inició la instancia de proceso
   * **Hora de creación**: la fecha y la hora en que se inició la instancia de proceso
   * **Hora de finalización**: la fecha y la hora en que se completó la instancia de proceso
   * **Duración**: duración desde el inicio hasta que finalizó la instancia de proceso
   * **Estado**: estado actual de la instancia de proceso.

   De forma predeterminada, el resultado se ordenará por ID de proceso. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo.

   Como el orden es una operación de alternancia, haga clic en un encabezado de columna para ordenar el resultado en orden ascendente y vuelva a hacer clic en él para ordenarlo en orden descendente.

   Del mismo modo, los siguientes campos se mostrarán en el resultado de Búsqueda de tareas:

   * **ID de tarea**: el ID de la tarea. El campo contiene un hipervínculo. Si hace clic en un ID de tarea en este campo, se le redirigirá al panel **[!UICONTROL Detalles de la tarea]** para la tarea.
   * **Iniciador**: el usuario de AEM Forms que inició la instancia de proceso
   * **Hora de creación**: la fecha y la hora en que se inició la instancia de proceso
   * **Hora de finalización**: la fecha y la hora en que se completó la instancia de proceso
   * **Duración**: duración desde el inicio hasta que finalizó la instancia de proceso
   * **Estado**: estado actual de la instancia de proceso.

   De forma predeterminada, el resultado se ordenará por ID de tarea. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo. El resultado se ordenará por la columna que se indica con una flecha oscura junto al encabezado de la columna.

   Como el orden es una operación de alternancia, haga clic en un encabezado de campo para ordenar el resultado en orden ascendente y vuelva a hacer clic en él para ordenarlo en orden descendente. El orden de clasificación actual (ascendente/descendente) se indica mediante la dirección de la flecha oscurecida situada junto al encabezado de la columna.

   ![task_search_result](assets/task_search_result.png)

1. Haga clic en el botón del carril ![lc_pr_carril_button](assets/lc_pr_rail_button.png) en la esquina superior izquierda para contraer el panel **Mis filtros** y expanda el espacio disponible para el panel **Informe**.
1. Utilice las opciones de la esquina superior derecha del panel **Informe** para realizar operaciones en el resultado de la consulta.

   * **Actualizar**: actualiza el informe con los datos más recientes disponibles en el almacenamiento.

   * **Exportar a CSV**: exporte los datos del informe a un archivo separado por comas.

   >[!NOTE]
   >
   >Al exportar un informe, el resultado de la búsqueda se exportará a un archivo CSV y no solo a la página actual

## Detalles del proceso/tarea {#process-task-details}

Utilice el panel **Detalles del proceso** para ver los detalles de un proceso específico.

Del mismo modo, se usa el panel **Detalles de la tarea** para ver los detalles de una tarea específica.

### Ver los detalles del proceso/tarea {#to-view-process-task-details}

Puede ver los detalles de un proceso o tarea específico de AEM Forms:

* **A partir de un resultado de búsqueda de proceso/tarea**
* **Al escribir el ID de proceso/tarea en el panel Detalles del proceso/tarea**

#### A partir de un resultado de búsqueda de proceso/tarea {#from-a-process-task-search-result}

1. Ejecute una búsqueda de procesos/tareas. Para obtener más información, consulte [Ejecutar una consulta de búsqueda de procesos](#to-execute-a-search-query).

   Observe que los ID de proceso mostrados devueltos en el resultado contienen hipervínculos.

   ![process_id_list](assets/process_id_list.png)

1. Haga clic en un ID de proceso de la lista para ver los detalles de este proceso en el panel **Detalles del proceso**.

   El resultado de la consulta **Detalles del proceso/tarea** muestra detalles de las tareas/formularios contenidos en el proceso/tarea.

   De forma predeterminada, el resultado se ordenará por el ID de las Tareas/Formularios. Sin embargo, para ordenar el resultado por cualquiera de los campos, haga clic en el título del campo. La columna por la que se ordena el resultado se indicará mediante una flecha oscura junto al encabezado de la columna.

   Como el orden es una operación de alternancia, haga clic en un encabezado de campo para ordenar el resultado en orden ascendente y vuelva a hacer clic en él para ordenarlo en orden descendente. El orden de clasificación actual (ascendente/descendente) se indica mediante la dirección de la flecha oscurecida situada junto al encabezado de la columna.

   **Resultado de los detalles del proceso**

   ![process_details](assets/process_details.png)

   **Panel izquierdo:** muestra los siguientes detalles del proceso seleccionado:

   * Nombre del proceso
   * Hora de la fecha de creación del proceso
   * Hora de finalización del proceso
   * Duración del proceso
   * Estado del proceso
   * Iniciador del proceso

   **Panel superior derecho:** muestra los siguientes detalles de las tareas que componen el proceso seleccionado:

   * ID de tarea
   * Nombre de la tarea
   * Propietario de la tarea
   * Hora de la creación de la tarea
   * Hora de la actualización de la tarea
   * Fecha de finalización de la tarea
   * Duración de la tarea
   * Estado de la tarea

   **Panel inferior derecho:** muestra los siguientes detalles del historial de procesos del proceso seleccionado:

   * Nombre del proceso
   * Iniciador del proceso
   * Hora de actualización del proceso
   * Hora de finalización del proceso
   * Estado del proceso

   **Resultado de los detalles de la tarea**

   ![task_details](assets/task_details.png)

   **Panel izquierdo:** muestra los siguientes detalles de la tarea seleccionada:

   * Nombre de la tarea
   * ID del proceso al que pertenece esta tarea
   * Descripción de la tarea
   * Hora de la creación de la tarea
   * Fecha de finalización de la tarea
   * Duración de la tarea
   * Estado de la tarea
   * Ruta de tarea seleccionada

   **Panel superior derecho:** muestra los siguientes detalles de los formularios que componen la tarea seleccionada:

   * ID de formulario
   * Fecha de creación del formulario
   * Hora de la actualización del formulario
   * URL de la plantilla del formulario

   **Panel inferior derecho:** muestra los siguientes detalles del historial de procesos de la tarea seleccionada:

   * Tipo de asignación de tarea
   * Propietario de la tarea
   * Hora de creación de la asignación de tareas
   * Hora de la actualización de la tarea

1. Haga clic en **Volver a la búsqueda de procesos/tareas** para volver al resultado de la búsqueda desde el que se profundizaron los detalles del proceso/tarea.

   ![back_to_search](assets/back_to_search.png)

   Sin embargo, si los detalles del proceso/tarea se encontraron al escribir un ID de proceso/tarea específico, si hace clic en Volver a búsqueda de procesos/tareas volverá a **Búsqueda de procesos/tareas**, sin mostrar ningún resultado de búsqueda.

#### Al escribir el ID de proceso/tarea en el panel Detalles del proceso/tarea {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vaya a el panel **Detalles del proceso/tarea**.

   ![details_nodes](assets/details_nodes.png)

1. En el cuadro de texto ID de proceso/tarea, escriba el ID de proceso/tarea.

   ![process_details-1](assets/process_details-1.png)

   Los campos del resultado de la consulta **Detalles del proceso/tarea** son campos específicos de un proceso/tarea de AEM Forms.

   Para un proceso, el resultado de la consulta muestra los detalles de las tareas contenidas en el proceso.

   Para una tarea, el resultado de la consulta muestra los detalles de los formularios contenidos en la tarea.
