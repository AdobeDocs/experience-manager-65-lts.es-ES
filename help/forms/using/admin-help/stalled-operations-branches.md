---
title: Trabajar con operaciones y ramas estancadas
description: La página Operaciones paralizadas y la página Ramas paralizadas muestran los procesos que se han paralizado.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---

# Trabajar con operaciones y ramas estancadas {#working-with-stalled-operations-and-branches}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La página Operaciones paralizadas y la página Ramas paralizadas muestran los procesos que se han paralizado. Un proceso se puede detener cuando se produce un error durante o después de la ejecución de una operación o debido a una operación de detención deliberada en el proceso:

* Las operaciones pueden detenerse debido a un error imprevisto. Sin embargo, una operación de Rama de detención en un proceso detiene deliberadamente la ejecución de un proceso y requiere la intervención del administrador.
* Las ramas pueden detenerse entre operaciones durante una evaluación de regla.

Cuando se detiene un proceso, no se ejecutan más operaciones hasta que se soluciona el problema y se reinicia la operación o rama.

Para cada elemento parado, la lista muestra la siguiente información:

**Nombre de operación o nombre de rama:** Nombre de la operación o rama.

**Estado:** siempre en espera por elementos en espera.

**Error:** Breve descripción del problema.

**Id. de proceso:** El entero positivo que el flujo de trabajo de formularios asigna cuando se crea una instancia del proceso (es decir, cuando un usuario o un paso automatizado inicia un proceso). Puede utilizar este identificador para realizar un seguimiento de la instancia de proceso a lo largo de su ciclo de vida.

**Nombre del proceso - Versión:** El nombre del proceso asignado en Workbench.

**Fecha de detención:** La fecha y hora en que se detuvo la operación o rama.

Puede realizar las siguientes tareas en la página Operaciones paralizadas o Ramas paralizadas:

* Seleccione un error para ver los detalles al respecto. Cuando selecciona un error, aparece la página Detalles del Error.
* Finalizar o reintentar operaciones estancadas o reintentar ramas estancadas.

## Finalizar o reintentar operaciones o ramas estancadas {#terminating-or-retrying-stalled-operations-or-branches}

En la página Operaciones estancadas, puede finalizar las instancias de proceso mostradas.

Al finalizar una instancia de proceso, esta deja de ejecutarse y no se realizan más operaciones. Normalmente, un proceso solo se finaliza si se bloquea o deja de utilizarse debido a un error y no se puede corregir ni reiniciar.

En la página Operaciones bloqueadas o en la página Ramas bloqueadas, puede volver a intentar la operación o rama.

Al reintentar una operación, el flujo de trabajo de Forms se envía a una solicitud para reiniciar la operación. Si se ha corregido el error que provocó que el proceso se detuviera y la solicitud de reintento se realiza correctamente, el proceso vuelve a ejecutarse desde el punto en que se detuvo y su estado cambia a EN EJECUCIÓN. Si la operación no se puede reiniciar, permanece DETENIDA y es posible que tenga que finalizarla.

### Finalizar una operación detenida {#terminate-a-stalled-operation}

1. En la consola de administración, haga clic en Servicios > Forms workflow > Errores de operaciones detenidas.
1. En la página Operaciones interrumpidas, seleccione el elemento que desea finalizar y haga clic en Finalizar.

### Reintentar una operación o rama estancada {#retry-a-stalled-operation-or-branch}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios y, a continuación, haga clic en Errores de operaciones paralizadas o Errores de ramas paralizadas.
1. En la página Operaciones paralizadas o Ramas paralizadas, seleccione el elemento que desea reintentar y haga clic en Reintentar.

## Visualización de detalles de error sobre operaciones o ramas estancadas {#viewing-error-details-about-stalled-operations-or-branches}

Si selecciona un error de la lista de elementos paralizados en la página Operaciones paralizadas o Ramas paralizadas, aparecerá la página Detalles del error, que muestra detalles sobre el error que pueden ayudarle a solucionar el problema.

El cuadro de la parte inferior de la página contiene la información del error.

También puede finalizar o reintentar operaciones estancadas, y reintentar ramas estancadas, desde la página Detalles del error.

## El proceso no se detiene cuando el usuario de escalación no existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Se producen errores cuando la operación Asignar tarea del servicio de usuario de AEM Forms está configurada para escalar la tarea a otro usuario después de un período de tiempo específico y el usuario de escalación se elimina después de que se ejecute la operación Asignar tarea, pero antes de que se produzca la escalación.

Cuando se produce esta situación, el estado del proceso y la tarea no cambia en el momento de escalación configurado y la escalación no se produce, pero el proceso no se detiene. El siguiente mensaje aparece en el registro del servidor:

&quot;La entidad de seguridad especificada para la escalación no es válida, para taskID: *number*, cola especificada: *number*.&quot;

Si se elimina el usuario de escalación antes de que se genere la tarea (antes de que se ejecute la operación Asignar tarea), el proceso se detendrá o se producirá el evento de excepción InvalidPrincipal.

Para evitar este problema, cuando elimine un usuario, busque tareas que pertenezcan a ese usuario y haga frente a ellas en consecuencia. (Consulte [Trabajar con tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
