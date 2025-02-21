---
title: Informes predefinidos en informes de proceso
description: Consulte datos de proceso de AEM Forms en JEE para crear informes sobre los procesos de larga duración, la duración de los procesos y el volumen del flujo de trabajo.
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 100%

---

# Informes predefinidos en informes de proceso {#pre-defined-reports-in-process-reporting}

## Informes predefinidos en informes de proceso {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting incluye los siguientes informes *predeterminados*:

* **[Procesos de larga duración](#long-running-processes)**: un informe de todos los procesos de AEM Forms que han tardado más tiempo del especificado en completarse.
* **[Gráfico de duración del proceso](#process-duration-report)**: un informe de un proceso de AEM Forms especificado en función de su duración.
* **[Volumen del flujo de trabajo](#workflow-volume-report)**: un informe de las instancias en ejecución y las instancias completadas del proceso especificado por fecha.

## Procesos de larga duración {#long-running-processes}

El informe Procesos de larga duración muestra los procesos de AEM Forms que han tardado más tiempo del especificado en completarse.

### Ejecutar un informe Procesos de larga duración {#to-execute-a-long-running-process-report}

1. Para ver la lista de informes predefinidos en informes de proceso, haga clic en el nodo **Informes** en la vista de árbol de **Process Reporting**.
1. Haga clic en el nodo de informes **Procesos de larga duración**.

   ![nodo_larga_duración](assets/long_running_node.png)

   Al seleccionar un informe, el panel **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![Panel Parámetros de informe de Procesos de larga ejecución](assets/report_parameters_panel.png)

   Parámetros:

   * **Duración** (*obligatorio*): especifique una duración y una unidad de tiempo. Muestre todos los procesos de AEM Forms que se han ejecutado durante más tiempo del especificado.
   * **Se inició después de** (*opcional*): seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que se han iniciado después de la fecha especificada.
   * **Se inició antes de** (*opcional*): seleccione una fecha. Filtre el informe para mostrar las instancias de proceso que se iniciaron antes de la fecha especificada.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en el panel **Informe** que aparece en la parte derecha de la ventana **Process Reporting**.

   ![procesos_larga_duración](assets/long_running_processes.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: actualiza el informe con los datos más recientes disponibles en el almacenamiento.
   * **Cambiar el color de la leyenda**: seleccione y cambie el color de la leyenda del informe.
   * **Exportar a CSV**: exporte y descargue los datos del informe en un archivo separado por comas.

## Informe Duración del proceso  {#process-duration-report}

El informe Duración del proceso muestra el número de instancias de un proceso de Forms en función del número de días que se ha ejecutado cada instancia.

### Ejecutar un informe Duración del proceso {#to-execute-a-process-duration-report}

1. Para ver los informes predefinidos en informes de proceso, haga clic en el nodo **Informes** de la vista de árbol de **Process Reporting**.
1. Haga clic en el nodo de informes **Duración de los procesos**.

   ![nodo_duración_proceso](assets/process_duration_node.png)

   Al seleccionar un informe, el panel **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![Panel Parámetros de informe de Procesos de larga ejecución](assets/process_duration_params.png)

   Parámetros:

   * **Seleccionar proceso** (*obligatorio*): seleccione un proceso de AEM Forms.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en el panel **Informe** que aparece en la parte derecha de la ventana Process Reporting.

   ![process_duration_report](assets/process_duration_report.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: actualiza el informe con los datos más recientes disponibles en el almacenamiento.
   * **Cambiar el color de la leyenda**: seleccione y cambie el color de la leyenda del informe.
   * **Exportar a CSV**: exporte y descargue los datos del informe en un archivo separado por comas.

## Informe Volumen del flujo de trabajo {#workflow-volume-report}

El informe Volumen del flujo de trabajo muestra el número de instancias de un proceso de AEM Forms que se ejecutan actualmente y las que se han completado en función del día del calendario.

### Para ejecutar un informe Volumen del flujo de trabajo {#to-execute-a-workflow-volume-report}

1. Para ver los informes predefinidos en informes de proceso, haga clic en el nodo **Informes** de la vista de árbol de **Process Reporting**.
1. Haga clic en el nodo de informes **Volumen del flujo de trabajo**.

   ![nodo_volumen_flujo_trabajo](assets/workflow_volume_node.png)

   Al seleccionar un informe, el panel **Parámetros de informe** se muestra a la derecha de la vista de árbol.

   ![Panel Parámetros de informe de Procesos de larga ejecución](assets/workflow_volume_params.png)

   Parámetros:

   * **Seleccionar proceso** (*obligatorio*): seleccione un proceso de AEM Forms.

   * **Se inició después de** (*opcional*): seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que se iniciaron después de la fecha especificada.

   * **Se inició antes de** (*opcional*): seleccione una fecha. Filtra el informe para mostrar las instancias de proceso que se iniciaron antes de la fecha especificada.

1. Haga clic en **Ir** para ejecutar el informe.

   El informe se muestra en el panel **Informe** que aparece en la parte derecha de la ventana **Process Reporting**.

   ![informe_volumen_flujo_trabajo](assets/workflow_volume_report.png)

   Utilice las opciones de la esquina superior derecha del panel **Informe** para realizar las siguientes operaciones en el informe.

   * **Actualizar**: actualiza el informe con los datos más recientes disponibles en el almacenamiento.
   * **Cambiar el color de la leyenda**: seleccione y cambie el color de la leyenda del informe.
   * **Exportar a CSV**: exporte y descargue los datos del informe en un archivo separado por comas.
