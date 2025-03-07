---
title: Ver estadísticas relacionadas con Work Manager
description: La pestaña Administrador de trabajo muestra estadísticas relacionadas con los elementos de Administrador de trabajo. Descubra cómo puede ver y filtrar los elementos de trabajo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 7c1023ac-9d52-49f8-8e92-20e2d9d7079b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 1%

---

# Ver estadísticas relacionadas con Work Manager {#view-statistics-related-to-work-manager}

La pestaña Administrador de trabajo muestra estadísticas relacionadas con los elementos de Administrador de trabajo. Estos elementos de trabajo se encuentran en diferentes estados según su ubicación en proceso. (Vea [Estado (sólo para las categorías Predeterminado, Flujo de trabajo o Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Puede filtrar la información para ver sólo un subconjunto de los elementos mediante las distintas opciones disponibles (por ejemplo, Estado o Categoría). Puede ordenar los elementos de trabajo o trabajo resultantes (en orden ascendente o descendente) haciendo clic en uno de los encabezados de columna. Además, puede administrar los elementos de trabajo mediante las herramientas de operación que se muestran encima de la lista de elementos de trabajo.

## Filtrar los elementos de trabajo {#filter-the-work-items}

1. Haga clic en la ficha Administrador de trabajo.
1. Seleccione los criterios para uno o varios de los filtros descritos a continuación y, a continuación, haga clic en Ir.

### Categoría {#category}

**Valor predeterminado:** Todos los elementos de trabajo a los que el cliente no asignó una categoría cuando se enviaron. Work Manager administra estos elementos, por lo que los estados pertenecen a Work Manager.

**Administrador de trabajos:** Todos los trabajos que pertenecen al Administrador de trabajos. El Gestor de trabajos gestiona sus propios trabajos y tiene sus propios estados de trabajo. Consulte los estados de trabajo específicos que se describen a continuación.

**Flujo de trabajo:** Todos los elementos de trabajo que pertenecen a la ejecución del flujo de trabajo. El flujo de trabajo no administra sus propios elementos de trabajo sino que depende de Work Manager; por lo tanto, los estados pertenecen a Work Manager.

**Eventos:** Todos los elementos de trabajo que pertenecen a la Administración de eventos. La administración de eventos no administra sus propios elementos de trabajo sino que depende de Work Manager; por lo tanto, los estados pertenecen a Work Manager.

### Estado (solo para las categorías Predeterminado, Flujo de trabajo o Eventos) {#status-for-default-workflow-or-events-categories-only}

**Mostrar todo:** Muestra todos los elementos de trabajo actuales.

**Programado:** Muestra todos los elementos de trabajo listos para su ejecución por el servidor de aplicaciones, pero aún no iniciados.

**En pausa:** Muestra todos los elementos de trabajo programados que la aplicación cliente ha pausado. Estos elementos se pueden ejecutar o eliminar. (Consulte Administrar los elementos de trabajo o los trabajos.)

**En curso:** muestra todos los elementos de trabajo que el administrador de trabajo del servidor de aplicaciones recopiló y que se completarán o suspenderán. No se pueden utilizar operaciones en estos elementos de trabajo.

**Completado:** Muestra todos los elementos de trabajo que se ejecutaron correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al finalizar las devoluciones de llamada a los controladores de devolución de llamada. Puede eliminar estos elementos mediante la operación Eliminar elementos. (Consulte Administrar los elementos de trabajo o los trabajos.)

**Error:** muestra todos los elementos de trabajo que no se completaron correctamente debido a una condición de error. Estos elementos de trabajo se pueden volver a intentar varias veces mediante la operación Reintentar elementos. (Consulte Administrar los elementos de trabajo o los trabajos.) Un vínculo Error en la columna Estado le permite acceder a los detalles del error.

**Desconocido:** Muestra todos los elementos de trabajo cuyo estado es desconocido.

### Estado (solo para la categoría Administrador de trabajos) {#status-for-job-manager-category-only}

**Completados:** Muestra todos los trabajos que se han ejecutado correctamente. Los elementos de trabajo persistentes permanecen en este estado y los elementos no persistentes se eliminan al finalizar las devoluciones de llamada a los controladores de devolución de llamada.

**Solicitud completa:** muestra los trabajos para los que se realizó una solicitud completa.

**Error solicitado:** muestra los trabajos para los que se realizó una solicitud de error.

**Error:** muestra trabajos que no se completaron correctamente debido a una condición de error. Un vínculo Failure en la columna Status permite acceder a los detalles del error.

**Finalización solicitada:** muestra los trabajos para los que se realizó una solicitud de finalización.

**Finalizados:** muestra los trabajos que finalizaron sin completarse.

**Suspender solicitado:** Muestra los trabajos para los que se realizó una solicitud de suspensión.

**Suspendidos:** Muestra los trabajos que están suspendidos.

**Solicitud de reanudación:** Muestra los trabajos para los que se realizó una solicitud de reanudación.

**En cola:** muestra los trabajos que están en cola.

**En ejecución:** muestra los trabajos que se están ejecutando.

### Nombre del servidor {#server-name}

Solo para servidores agrupados, seleccione el nombre del nodo para mostrar solo los elementos de trabajo o los elementos de trabajo creados en ese servidor. Si se selecciona Mostrar todo, se muestran todos los elementos de trabajo de todos los nodos de un clúster.

### Hora de creación {#create-time}

Seleccione una opción de este filtro para mostrar solo los elementos de trabajo creados dentro del periodo de tiempo seleccionado. Por ejemplo, si selecciona 1 día, se muestran todos los elementos de trabajo que se crearon en las 24 horas anteriores a la hora establecida en el filtro Antes de.

### Antes de {#prior-to}

Establece la fecha y la hora que utiliza el filtro Crear hora como fecha de finalización. Mantenga la opción Usar fecha y hora actuales seleccionada para filtrar desde la fecha y hora actuales, o anule la selección de la opción e introduzca los valores adecuados. Haga clic en los iconos del calendario o en los iconos del reloj para seleccionar valores mediante esas herramientas.

Por ejemplo, si selecciona Hora de creación = 1 día y Antes de = Usar fecha y hora actuales, se devuelven todos los elementos de trabajo creados en las últimas 24 horas.

>[!NOTE]
>
>En implementaciones de bases de datos de Oracle, los filtros de intervalo de fechas (es decir, Crear hora y Antes de la configuración) no funcionan con precisión. Utilice otro filtro para recuperar los elementos de trabajo.

## Interfaz de la ficha Administrador de trabajo {#about-the-work-manager-tab-interface}

Cuando se ejecuta una consulta de Work Manager o se realiza una operación en un elemento de trabajo o trabajo, aparece un mensaje sobre la lista. Este mensaje proporciona comentarios sobre la acción que ha iniciado y, en algunos casos, un vínculo Más información para proporcionar detalles. Por ejemplo, si la operación que ha iniciado falla, el mensaje lo indica y proporciona un vínculo para obtener detalles sobre el error.

Al hacer clic en Más información, el cuadro de diálogo Detalles de la operación muestra una lista de los elementos de trabajo o trabajos seleccionados durante la operación. Puede hacer clic en cada elemento de la lista para ver los detalles del error en la parte inferior del cuadro de diálogo.

### Administrar los elementos de trabajo o trabajos {#manage-the-work-items-or-jobs}

1. Utilice las herramientas de operación que se describen a continuación para administrar los elementos de trabajo o los trabajos de la lista.

   >[!NOTE]
   >
   >Las operaciones están disponibles según el estado del elemento.

   **Eliminar elementos:** Elimina el elemento de trabajo o trabajo seleccionado.

   **Pausar elementos:** Pausa el elemento de trabajo o trabajo seleccionado.

   **Reanudar elementos:** Reanuda el trabajo o elemento de trabajo seleccionado desde su estado pausado.

   **Elementos de reintento:** intenta volver a ejecutar el trabajo o elemento de trabajo seleccionado desde su estado actual.

   Puede comprobar si una operación se ha realizado correctamente haciendo clic en Más información encima de la lista. Se muestra un cuadro de diálogo que contiene los elementos de trabajo o trabajos seleccionados y sus estados.

## Información adicional sobre los estados de elementos de trabajo {#additional-information-about-work-item-statuses}

Una transición de estado típica para un elemento de trabajo es Nuevo > Programado > En curso > Completado o Error.

El estado Paused interrumpe este flujo normal. La aplicación cliente o el administrador del sistema pueden iniciar esta interrupción (por ejemplo, para mantenimiento o actualización). Puede invertir esta acción mediante la operación Reanudar para volver a mover el elemento de trabajo a un estado Programado.

Un elemento de trabajo en un estado Programado se pone en cola para su ejecución que aún no ha comenzado. Estos elementos se pueden pausar o eliminar, o pasarán al estado En curso cuando Work Manager los extraiga de la cola. Los elementos de trabajo en curso no se pueden modificar. Se completarán o no.

El estado Error se produce como resultado de una condición de error que se produce durante la ejecución del elemento de trabajo. Si sospecha que los errores son circunstanciales (debido al contexto en el momento de la ejecución), puede volver a intentar la ejecución y volver a colocar el elemento de trabajo en la cola. Solo se permite un número limitado de reintentos.
