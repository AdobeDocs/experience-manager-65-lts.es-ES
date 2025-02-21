---
title: Tareas de mantenimiento previas a la actualización
description: Obtenga información acerca de las tareas previas a la actualización recomendadas para AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 108e1b3d840287e3d694242d934d0fbe4606801c
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Tareas de mantenimiento previas a la actualización{#pre-upgrade-maintenance-tasks}

Antes de comenzar la actualización, es importante realizar estas tareas de mantenimiento para asegurarse de que el sistema está listo y se puede revertir en caso de que se produzcan problemas:

* [Definiciones de índice](#index-definitions)
* [Garantizar suficiente espacio en disco](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Copia de seguridad completa de AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Generar el archivo quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurar depuración de flujo de trabajo y registro de auditoría](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Instalar, configurar y ejecutar las tareas previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Deshabilitar módulos de inicio de sesión personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Quitar Actualizaciones Del Directorio /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Detener Cualquier Instancia De Espera En Frío](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Deshabilitar trabajos programados personalizados](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Ejecutar limpieza de revisión sin conexión](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Ejecutar recolección de basura del almacén de datos](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Actualizar el esquema de base de datos si es necesario](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Eliminar usuarios que puedan obstaculizar la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Rotar archivos de registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Definiciones de índice {#index-definitions}

Asegúrese de que ha instalado las definiciones de índice necesarias publicadas con los paquetes de servicio de AEM 6.5 proporcionados con el paquete de servicio 22 de AEM como mínimo (consulte las [notas de la versión del paquete de servicio de AEM 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/release-notes/release-notes) para obtener más información).

## Garantizar suficiente espacio en disco {#ensure-sufficient-disk-space}

Al ejecutar la actualización, además de las actividades de actualización de contenido y código, se debe realizar una migración del repositorio. La migración crea una copia del repositorio en el nuevo formato de Segment TAR. Como resultado, necesita suficiente espacio en disco para conservar una segunda versión, potencialmente más grande, del repositorio.

## Copia de seguridad completa de AEM {#fully-back-up-aem}

Se debe realizar una copia de seguridad completa de AEM antes de comenzar la actualización. Asegúrese de realizar una copia de seguridad del repositorio, la instalación de la aplicación, el almacén de datos y las instancias de Mongo si corresponde. Para obtener más información sobre cómo hacer copias de seguridad y restaurar una instancia de AEM, consulte [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md).

## Generar el archivo quickstart.properties {#generate-quickstart-properties}

Al iniciar AEM desde el archivo jar, se genera un archivo `quickstart.properties` en `crx-quickstart/conf`. Si AEM solo se ha iniciado con la secuencia de comandos de inicio en el pasado, este archivo no está presente y la actualización falla. Asegúrese de comprobar la existencia de este archivo y reinicie AEM desde el archivo jar si no está presente.

## Configurar depuración de flujo de trabajo y registro de auditoría {#configure-wf-audit-purging}

Las tareas `WorkflowPurgeTask` y `com.day.cq.audit.impl.AuditLogMaintenanceTask` requieren configuraciones OSGi independientes y no pueden funcionar sin ellas. Si fallan durante la ejecución de la tarea previa a la actualización, la razón más probable es que falten configuraciones. Por lo tanto, asegúrese de agregar configuraciones de OSGi para estas tareas o eliminarlas por completo de la lista de tareas de optimización previas a la actualización si no desea ejecutarlas. Encontrará documentación para configurar las tareas de depuración del flujo de trabajo en [Administrar instancias del flujo de trabajo](/help/sites-administering/workflows-administering.md) y la configuración de las tareas de mantenimiento del registro de auditoría en [Mantenimiento del registro de auditoría en AEM 6](/help/sites-administering/operations-audit-log.md).

Para la depuración de registros de auditoría y flujo de trabajo en CQ 5.6 y depuración de registros de auditoría en AEM 6.0, consulte [Purgar flujo de trabajo y nodos de auditoría](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Instalar, configurar y ejecutar las tareas previas a la actualización {#install-configure-run-pre-upgrade-tasks}

Las tareas de mantenimiento previas a la actualización que antes se tenían que realizar manualmente se están optimizando y automatizando. La optimización del mantenimiento previo a la actualización permite una forma unificada de almacenar en déclencheur estas tareas y poder inspeccionar sus resultados bajo demanda.

### Cómo se usa {#how-to-use-it}

El componente OSGI `PreUpgradeTasksMBean` viene preconfigurado con una lista de tareas de mantenimiento previas a la actualización que se pueden ejecutar todas a la vez. Puede configurar las tareas siguiendo el siguiente procedimiento:

1. Vaya a la consola web explorando *https://serveraddress:serverport/system/console/configMgr*

1. Busque &quot;**preupgradetasks**&quot; y, a continuación, haga clic en el primer componente que coincida. El nombre completo del componente es `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modifique la lista de tareas de mantenimiento que deben ejecutarse como se muestra a continuación:

   ![1487758925984](assets/1487758925984.png)

A continuación se describe el modo de ejecución para el que está diseñada cada tarea de mantenimiento.

| Tarea | Notas |
|---|---|
| WorkflowPurgeTask | Debe configurar la configuración OSGi de depuración del flujo de trabajo de Adobe Granite antes de ejecutar. |
| GenerateBundlesListFileTask |   |
| RevisionCleanupTask |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | Debe configurar el programador de purga de registros de auditoría OSGi antes de ejecutar. |

### Configuración predeterminada de las comprobaciones de estado previas a la actualización {#default-configuration-of-the-pre-upgrade-health-checks}

El componente OSGI `PreUpgradeTasksMBeanImpl` viene preconfigurado con una lista de etiquetas de comprobación de estado previas a la actualización para ejecutarse cuando se llame al método `runAllPreUpgradeHealthChecks`:

* **system**: la etiqueta utilizada por las comprobaciones de estado de mantenimiento de granite

* **actualización previa**: una etiqueta personalizada que se podría agregar a todas las comprobaciones de estado que se pueden configurar para que se ejecuten antes de una actualización

**Métodos MBean**

Se puede acceder a la funcionalidad de bean administrada mediante la [consola JMX](/help/sites-administering/jmx-console.md).

Puede acceder a los MBeans mediante las siguientes opciones:

1. Ir a la consola JMX en *https://serveraddress:serverport/system/console/jmx*
1. Busque **PreUpgradeTasks** y haga clic en el resultado

1. Seleccione cualquier método de la sección **Operations** y seleccione **Invoke** en la siguiente ventana.

A continuación se muestra una lista de todos los métodos disponibles que expone `PreUpgradeTasksMBeanImpl`:

| Nombre del método | Tipo | Descripción |
|---|---|---|
| runAllPreUpgradeTasks() | ACCIÓN | Ejecuta todas las tareas de mantenimiento previas a la actualización de la lista. |
| runPreUpgradeTask(preUpgradeTaskName) | ACCIÓN | Ejecuta la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro. |
| getPreUpgradeTaskLastRunTime(preUpgradeTaskName) | ACCIÓN | Muestra el tiempo de ejecución exacto de la tarea de mantenimiento anterior a la actualización con el nombre dado como parámetro. |
| getPreUpgradeTaskLastRunState(preUpgradeTaskName) | ACCIÓN | Muestra el último estado de ejecución de la tarea de mantenimiento previa a la actualización con el nombre dado como parámetro. |
| runAllPreUpgradeHealthChecks(shutdownOnSuccess) | ACCIÓN | Ejecuta todas las comprobaciones de estado anteriores a la actualización y guarda su estado en un archivo denominado preUpgradeHCStatus.properties en la ruta de inicio de sling. Si shutdownOnSuccess se establece en true, la instancia de AEM se cierra, pero solo si todas las comprobaciones de estado anteriores a la actualización tienen el estado OK. El archivo de propiedades se utiliza como condición previa para cualquier actualización futura y el proceso de actualización se detiene si falla la ejecución de la comprobación de estado previa a la actualización. Si desea omitir el resultado de las comprobaciones de estado anteriores a la actualización e iniciar la actualización de todos modos, puede eliminar el archivo. |
| detectUsageOfUnavailableAPI(aemVersion) | ACCIÓN | Enumera todos los paquetes importados que ya no se satisfacen al actualizar a la versión de AEM especificada. La versión de AEM de destino debe proporcionarse como parámetro. |

>[!NOTE]
>
>Los métodos MBean se pueden invocar mediante:
>
>* La consola JMX
>* Cualquier aplicación externa que se conecte a JMX
>* cURL
>

## Quitar Actualizaciones Del Directorio /install {#remove-updates-install-directory}

>[!NOTE]
>
>Solo elimine paquetes del directorio crx-quickstart/install DESPUÉS de cerrar la instancia de AEM. Este paso es uno de los últimos antes de iniciar el procedimiento de actualización in situ.

Quite los Service Packs, paquetes de características o revisiones que se hayan implementado a través del directorio `crx-quickstart/install` en el sistema de archivos local. Al hacerlo, se evita la instalación involuntaria de revisiones y Service Packs antiguos además de la nueva versión de AEM una vez completada la actualización.

## Detener Cualquier Instancia De Espera En Frío {#stop-tarmk-coldstandby-instance}

Si utiliza TarMK modo de espera en frío, detenga cualquier instancia de espera en frío. Al hacerlo, se garantiza una forma eficaz de volver a estar en línea si hay problemas en la actualización. Una vez que la actualización se haya completado correctamente, las instancias de espera en frío deben volver a crearse a partir de las instancias principales actualizadas.

## Deshabilitar trabajos programados personalizados {#disable-custom-scheduled-jobs}

Deshabilite los trabajos programados de OSGi que se incluyan en el código de la aplicación.

## Ejecutar limpieza de revisión sin conexión {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Este paso solo es necesario para instalaciones de TarMK

Si utiliza TarMK, debe ejecutar Offline Revision Cleanup antes de actualizar. Al hacerlo, el paso de migración del repositorio y las tareas de actualización subsiguientes se ejecutan mucho más rápido y ayuda a garantizar que Limpieza de revisiones en línea se pueda ejecutar correctamente una vez completada la actualización. Para obtener información sobre cómo ejecutar la limpieza de revisión sin conexión, consulte [Realización de la limpieza de revisión sin conexión](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Rotar archivos de registro {#rotate-log-files}

Adobe recomienda archivar los archivos de registro actuales antes de comenzar la actualización. Al hacerlo, resulta más fácil supervisar y analizar los archivos de registro durante y después de la actualización para identificar y resolver los problemas que se puedan producir.
