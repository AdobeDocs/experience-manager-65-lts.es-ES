---
title: Mantenimiento del registro de auditoría en AEM 6
description: Obtenga información sobre el mantenimiento del registro de auditoría en Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Mantenimiento del registro de auditoría en AEM 6{#audit-log-maintenance-in-aem}

Los eventos de AEM que cumplen los requisitos para el registro de auditoría generan muchos datos archivados. Estos datos pueden crecer rápidamente con el tiempo debido a las replicaciones, las cargas de recursos y otras actividades del sistema.

El mantenimiento del registro de auditoría incluye varias partes de funcionalidad que permiten automatizar el mantenimiento del registro de auditoría en directivas específicas.

Se implementa como una tarea de mantenimiento semanal configurable y se puede acceder a ella a través de la consola de monitorización del tablero de operaciones.

Para obtener más información, consulte la [Documentación del tablero de operaciones](/help/sites-administering/operations-dashboard.md).

Existen tres tipos de opciones de depuración de registros de auditoría:

1. [Purga del registro de auditoría de página](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Depuración del registro de auditoría DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Purga del registro de auditoría de replicación](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Cada una se puede configurar creando reglas en la consola web de AEM. Una vez configurados, puede almacenarlos en déclencheur en **Herramientas - Operaciones - Mantenimiento - Ventana de mantenimiento semanal** y ejecutando **Tarea de mantenimiento de AuditLog**.

## Configurar depuración del registro de auditoría de página {#configure-page-audit-log-purging}

Siga estos pasos para configurar la depuración del registro de auditoría:

1. Vaya al administrador de la consola web señalando el explorador a `http://localhost:4502/system/console/configMgr/`

1. Busque un elemento llamado **Regla de purga de registros de auditoría de páginas** y haga clic en él.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. A continuación, configure el planificador de depuración según sus necesidades. Las opciones disponibles son:

   * **Nombre de regla:** nombre de la regla de directiva de auditoría;
   * **Ruta de acceso de contenido:** la ruta de acceso del contenido al que se aplicará la regla;
   * **Edad mínima:** el tiempo en días que se deben guardar los registros de auditoría;
   * **Tipo de registro de auditoría:** el tipo de registro de auditoría que se debe purgar.

   >[!NOTE]
   >
   >La ruta de contenido solo se aplica a los elementos secundarios del nodo `/var/audit/com.day.cq.wcm.core.page` en el repositorio.

1. Guarde la regla.
1. La regla que ha creado debe exponerse en el tablero de operaciones para que se ejecute. Para ello, vaya a **Herramientas - Operaciones - Mantenimiento** desde la pantalla de bienvenida de AEM.

1. Presione la tarjeta **Ventana de mantenimiento semanal**.

1. Encontrará la tarea de mantenimiento ya presente en la tarjeta **Tarea de mantenimiento de AuditLog**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Puede inspeccionar la fecha de la siguiente ejecución, configurarla o ejecutarla manualmente pulsando el botón de reproducción.

En AEM 6.3, si la ventana de mantenimiento programado se cierra antes de que se complete la tarea Purga del registro de auditoría, la tarea se detiene automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.

**Con AEM 6.5**, puede detener manualmente una tarea de purga del registro de auditoría en ejecución si hace clic en el icono **Detener**. En la siguiente ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder el seguimiento del trabajo ya en curso.

## Configurar depuración del registro de auditoría DAM {#configure-dam-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque la regla **Depuración del registro de auditoría DAM** y haga clic en el resultado.
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de regla:** nombre de la regla de directiva de auditoría;
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** el tiempo en días que se deben conservar los registros de auditoría
   * **Tipos de eventos DAM de registro de auditoría:** los tipos de eventos de auditoría DAM que se deben purgar.

1. Haga clic en **Guardar** para guardar la configuración

## Configurar depuración del registro de auditoría de replicación  {#configure-replication-audit-log-purging}

1. Vaya a la consola del sistema en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Busque **Planificador de purga del registro de auditoría de replicación** y haga clic en el resultado
1. En la siguiente ventana, configure la regla en consecuencia. Las opciones son:

   * **Nombre de regla:** el nombre de la regla de directiva de auditoría
   * **Ruta de contenido:** la ruta del contenido al que se aplicará la regla
   * **Edad mínima:** el tiempo en días que se deben conservar los registros de auditoría
   * **Tipos de eventos de replicación de registros de auditoría:** los tipos de eventos de auditoría de replicación que deben purgarse

1. Haga clic en **Guardar** para guardar la configuración.
