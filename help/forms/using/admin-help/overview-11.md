---
title: Resumen del monitor de estado
description: Este documento proporciona información general sobre el monitor de estado y detalles sobre cómo puede acceder a él.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f187d4e4-7fe6-4f58-a2df-9d415dcff4aa
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Resumen del monitor de estado {#overview-of-health-monitor}

El monitor de estado proporciona información crítica sobre el sistema de formularios de AEM, como información del servidor, uso de la memoria y uso del procesador. También están disponibles las estadísticas de Work Manager, como el número de elementos de trabajo o trabajos en cola y sus estados. Puede realizar las siguientes tareas con el Monitor de estado:

* Compruebe que el sistema funciona correctamente
* Ver información para ayudar a diagnosticar los problemas del sistema a medida que se producen
* Realizar operaciones en elementos de trabajo o trabajos que muestren problemas
* Purgar registros obsoletos de la base de datos de Job Manager

La página Monitor de estado de la consola de administración tiene tres pestañas:

* La pestaña System muestra gráficos de monitorización de recursos e información sobre Forms Server (o el nodo en un entorno agrupado). (Consulte [Ver información del sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* La ficha Administrador de trabajo muestra datos relacionados con el Administrador de trabajo, como el número de elementos de trabajo de la cola Administrador de trabajos. Puede filtrar la información utilizando varios criterios o administrar elementos de trabajo individuales utilizando las herramientas de operación. (Consulte [Ver estadísticas relacionadas con Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La pestaña Programador de Depuración de Trabajos permite depurar registros obsoletos de la base de datos Administrador de trabajos. (Consulte [Purgar registros de la base de datos de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La página web Monitor de estado se rellena con estadísticas recopiladas mediante una API de Gemfire. Esta API detecta automáticamente todos los nodos de un clúster. También resuelve los problemas de seguridad que se producen al recopilar estadísticas desde servidores proxy o equilibradores de carga. Las opciones de Java están disponibles para ajustar el Monitor de estado y reducir el impacto en el rendimiento del entorno de los formularios AEM Forms. (Consulte [Ajustar el rendimiento del Monitor de estado](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Monitor de estado de acceso**

1. En la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página.
