---
title: Administrar procesos
description: La página Lista de procesos muestra los procesos que un usuario ha iniciado o que se han iniciado automáticamente. Más información sobre la administración de los procesos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# Administrar procesos {#managing-processes}

La página Lista de procesos muestra los procesos que un usuario ha iniciado o que se han iniciado automáticamente.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Flujo de trabajo de Forms. La lista de procesos muestra la siguiente información:

   **Nombre del proceso - Versión:** El nombre del proceso, tal como se define en Workbench.

   **Aplicación:** La aplicación a la que pertenece el proceso, tal como se define en Workbench.

   **Estado:** Activo significa que el proceso es el activado para la versión del proceso. Inactivo significa que el proceso es una versión antigua que aún tiene instancias de proceso.

   **Fecha de creación:** Fecha y hora en que se implementó el proceso.

1. Haga clic en un nombre de proceso para ver sus instancias de proceso en la página Instancia de Proceso.

## Uso de instancias de proceso {#working-with-process-instances}

Si accede a la página Instancia de Proceso desde la página Lista de Procesos, se muestran todas las instancias de proceso del proceso seleccionado. Si accede a la página Instancia de proceso después de realizar una búsqueda, solo se muestran las instancias de proceso encontradas.

Para cada instancia de proceso, la lista muestra la siguiente información:

**Id. de proceso:** Identificador que asigna el flujo de trabajo de formularios cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia un proceso). Puede utilizar este identificador para realizar un seguimiento de la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso - Versión:** El nombre del proceso, tal como se define en Workbench.

**Estado:** Indica si la instancia de proceso se está ejecutando con normalidad, si cambia de estado o si se ha detenido. (Consulte Acerca de los estados de instancias de proceso.)

**Fecha de creación:** Fecha y hora en que se creó la instancia de proceso.

**Fecha de actualización:** Fecha y hora en que se cambió por última vez el estado de la instancia de proceso.

Puede realizar las siguientes tareas en la página Instancia de Proceso:

* Seleccione una instancia de proceso para ver los detalles sobre ella, como sus operaciones y subprocesos. Al seleccionar una instancia de proceso, aparecerá la página Detalles de la instancia de proceso.
* Suspender, cancelar la suspensión o finalizar instancias de proceso.
* Busque una instancia de proceso. Para comenzar una búsqueda, haga clic en Buscar.

### Acerca de los estados de instancias de proceso {#about-process-instance-statuses}

Una instancia de proceso, incluidos los subprocesos, puede tener los siguientes estados:

**COMPLETADO:** Se han completado todas las ramas y operaciones de la instancia de proceso. COMPLETADO es el estado final de una instancia de proceso.

**FINALIZANDO:** El estado de la instancia de proceso está a punto de cambiar a COMPLETADO.

**INICIADA:** La instancia de proceso se ha creado pero aún no se está ejecutando. INICIADO es el primer estado de una instancia de proceso.

**EN EJECUCIÓN:** La instancia de proceso se está ejecutando normalmente. Puede que haya un paso automatizado en curso o que la instancia de proceso esté recibiendo los datos del usuario o esperando su interacción.

**SUSPENDIDA:** La instancia de proceso ha sido suspendida por un administrador o por un paso en el proceso. No se producirán más operaciones hasta que se cambie el estado.

**SUSPENDIENDO:** El estado está a punto de cambiar a SUSPENDIDO. Si una operación se ha diseñado para omitir las solicitudes de suspensión y aún no se ha completado, esa operación debe completarse antes de que se suspenda la instancia de proceso.

**TERMINADA:** Un administrador ha finalizado la instancia de proceso.

**TERMINANDO:** El estado está a punto de cambiar a TERMINADO. Si se ha diseñado una operación para omitir las solicitudes de finalización y aún no se ha completado, esa operación debe completarse antes de que finalice la instancia de proceso.

**SIN SUSPENDER:** El estado está a punto de cambiar a EN EJECUCIÓN después de haber sido SUSPENDIDO.

>[!NOTE]
>
>Cuando se realiza una solicitud para cambiar el estado de una instancia de proceso (como suspender o finalizar), la solicitud entra en la cola de comandos del flujo de trabajo de formularios. Según el tamaño de la cola y la velocidad de procesamiento general, el estado mostrado puede no cambiar hasta que la página se vuelva a cargar una o más veces.

### Suspender o anular la suspensión de instancias de proceso {#suspend-or-unsuspend-process-instances}

Si necesita solucionar un problema o si sabe que una instancia de proceso se encontrará con un problema en un paso posterior debido a alguna condición externa, puede suspender la instancia de proceso temporalmente.

Puede suspender las instancias de proceso que tengan el estado EN EJECUCIÓN.

Después de suspender una instancia de proceso, su estado cambia a SUSPENDING y, a continuación, a SUSPENDED, y el proceso se detiene en su operación actual. La instancia de proceso permanece en este estado hasta que el estado se cambie a NO SUSPENDIDO.

Solo las instancias de proceso que tienen un estado de SUSPENDIDO pueden cambiarse a NO SUSPENDIDO.

Al anular la suspensión de una instancia de proceso, su estado cambia a EN EJECUCIÓN y continúa con la operación en la que se había suspendido.

Al suspender una instancia de proceso que ha invocado otros procesos (procesos secundarios) mediante su operación de invocación, los procesos secundarios también se suspenden.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Flujo de trabajo de Forms.
1. En la página Instancia de proceso, seleccione el proceso y haga clic en Suspender o en Cancelar la suspensión.

### Finalización de instancias de proceso {#terminate-a-process-instances}

Si una operación de una instancia de proceso se ha detenido o ha encontrado alguna otra condición de error, o si necesita forzar una instancia de proceso para que deje de ejecutarse, puede finalizar la instancia de proceso.

Puede finalizar instancias de proceso que tengan cualquier estado.

Al finalizar una instancia de proceso, su estado cambia a TERMINATING y, a continuación, TERMINATED, y el proceso se detiene en su operación actual. No se ejecutan más operaciones y se finalizan todas las operaciones y tareas asociadas.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Flujo de trabajo de Forms.
1. En la página Instancia de proceso, seleccione el proceso y haga clic en Finalizar.

## Trabajar con detalles de instancia de proceso {#working-with-process-instance-details}

La página Detalles de Instancia de Proceso muestra el historial de una instancia de proceso.

El área Resumen muestra información básica sobre la instancia de proceso.

En la pestaña Operaciones, cada operación de la instancia de proceso se muestra en orden de finalización del primero al último con la siguiente información:

**Nombre de operación:** El nombre de la operación, tal como se define en Workbench.

**Estado:** Indica si la operación se está ejecutando con normalidad o si se ha detenido. (Consulte Acerca de los estados de instancias de proceso.)

**Nombre de rama:** El nombre de la rama, tal como se define en Workbench.

**Fecha de inicio:** Fecha y hora en que se inició la operación.

**Fecha de finalización:** Fecha y hora en que se completó la operación.

Un subproceso es una instancia de proceso iniciada por otro proceso y que se ejecuta independientemente de ese otro proceso. Los subprocesos solo se muestran si se diseñaron como parte del proceso en Workbench. En la ficha Subprocesos, cada subproceso se muestra con la siguiente información:

**Id. de proceso:** Este entero positivo que el flujo de trabajo de formularios asigna cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia el proceso). Puede utilizar este identificador para realizar un seguimiento de la instancia de proceso a través de su ciclo de vida.

**Nombre del proceso - Versión:** El nombre del proceso, tal como se define en Designer.

**Estado:** Indica si la instancia de proceso se está ejecutando con normalidad, si cambia de estado o si está detenida. (Consulte Acerca de los estados de instancias de proceso.)

**Fecha de creación:** Fecha y hora en que se creó el subproceso.

**Fecha de actualización:** La fecha y hora en que se cambió por última vez el estado del subproceso.

Puede realizar las siguientes tareas en la página Detalles de la instancia de proceso:

* Seleccione una operación para ver los detalles al respecto. Al seleccionar una operación, aparecerá la página Detalles de Operación.
* Seleccione un subproceso para ver detalles al respecto. Al seleccionar un subproceso, aparecerá la página Detalle de Instancia de Proceso.
* Finalizar o reintentar operaciones o subprocesos, según su estado.

### Acerca de los estados operativos {#about-operation-statuses}

Una operación (un paso en un proceso) puede tener los siguientes estados:

**COMPLETADA:** La operación se completó.

**EN EJECUCIÓN:** La operación se está ejecutando normalmente. Puede estar recibiendo entradas del usuario o esperando la interacción del usuario, o puede que haya un paso automatizado en curso.

**DETENIDO:** Se produjo un problema mientras se procesaba la operación. Compruebe el error o la excepción en la página Operaciones paralizadas.

**TERMINADA:** Un administrador finalizó la operación.

### Finalizar operaciones o subprocesos {#terminate-operations-or-subprocesses}

Si una operación o subproceso se ha detenido o ha encontrado alguna otra condición de error, o si necesita forzar una operación o subproceso para que deje de ejecutarse, puede finalizarlo.

Puede finalizar una operación que se esté EJECUTANDO.

Cuando finaliza una operación, su estado cambia a TERMINATED. La operación no se completa y la instancia de proceso deja de ejecutarse.

Puede finalizar un subproceso que tenga cualquier estado.

Al finalizar un subproceso, su estado cambia a TERMINATING y, a continuación, TERMINATED, y la instancia de proceso se detiene en sus operaciones actuales. No se ejecutan más operaciones en el subproceso, aunque la instancia de proceso principal sigue ejecutándose.

No se pueden finalizar procesos que tengan elementos de puerta de enlace en el diagrama de procesos. Si intenta finalizar estos tipos de procesos, las operaciones dentro de los elementos de puerta de enlace no se ven afectadas. Para finalizar operaciones que se encuentran dentro de un elemento de puerta de enlace, debe finalizar las operaciones directamente.

1. En la página Detalles de la instancia de proceso, haga clic en la pestaña Operaciones o en la pestaña Subprocesos.
1. Seleccione la operación o subproceso y haga clic en Finalizar.

### Reintentar una operación {#retry-an-operation}

Puede reintentar la operación que tenga el estado DETENIDO.

Al reintentar una operación, el flujo de trabajo de Forms se envía a una solicitud para reiniciar la operación. Si la solicitud se realiza correctamente, el estado cambia a EN EJECUCIÓN. Si la operación no se puede reiniciar, permanece DETENIDA y es posible que tenga que finalizarla.

1. En la página Detalles de la instancia de proceso, haga clic en la pestaña Operaciones.
1. Seleccione la operación y haga clic en Reintentar.

## Uso de operaciones {#working-with-operations}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La página Detalles de Operación muestra un resumen de una operación de un proceso y sus asignaciones de usuario actuales.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Flujo de trabajo de Forms.
1. Haga clic en un nombre de proceso para mostrar sus instancias de proceso. Haga clic en una instancia de proceso para mostrar la página Detalles de Instancia de Proceso y, a continuación, seleccione una operación para mostrar la página Detalles de Operación.

   Para cada tarea, la lista muestra la siguiente información:

   **Nombre del proceso - Versión:** El nombre del proceso, tal como se define en Workbench.

   **Aplicación:** La aplicación a la que pertenece el proceso, tal como se define en Workbench.

   **Estado:** Activo significa que el proceso es el activado para la versión del proceso. Inactivo significa que el proceso es una versión antigua que aún tiene instancias de proceso.

   **Fecha de creación:** Fecha y hora en que se implementó el proceso.
