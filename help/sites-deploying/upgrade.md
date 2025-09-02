---
title: Actualización a Adobe Experience Manager 6.5
description: Obtenga información acerca de los conceptos básicos para actualizar una instalación de Adobe Experience Manager (AEM) anterior a AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: ebc34847-dc3d-41ed-b0d6-f004c3debcd9
source-git-commit: e9fc4a6294588b527a3b19d64101c81f0eb7bf55
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Actualización a Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>La actualización a AEM 6.5 LTS está disponible para todos los paquetes de servicio 6.5 admitidos.

>[!NOTE]
>
>Desde un punto de vista técnico, el proceso de actualización de AEM 6.5 LTS a AEM 6.5 LTS Service Packs está diseñado para ser una [actualización in situ sin problemas](/help/sites-deploying/in-place-upgrade.md). Este proceso generalmente no requiere ningún cambio de código por parte de los clientes, a menos que se indique específicamente en las notas de la versión.

Esta sección cubre la actualización de una instalación de AEM a AEM 6.5 LTS:

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

Para facilitar la referencia a las instancias de AEM involucradas en estos procedimientos, se utilizan los siguientes términos en estos artículos:

* La instancia *source* es la instancia de AEM desde la que está actualizando.
* La instancia *target* es a la que está actualizando.

## ¿Qué ha cambiado? {#what-has-changed}

### Actualizaciones {#updates}

La capa de base ahora es compatible con Java 17 y Java 21, e incorpora los últimos paquetes de código abierto de Apache Sling, Felix y Jackrabbit Oak. Además, el empaquetado de AEM 6.5 LTS uber-jar ha cambiado. Además, se han eliminado algunas funciones heredadas de AEM 6.5 LTS. Para obtener más información, consulte [Notas de la versión](/help/release-notes/release-notes.md#whats-new-what-s-new) y [Lista de paquetes obsoletos desinstalados después de la actualización](/help/sites-deploying/obsolete-bundles.md)

AEM 6.5 LTS tiene un fuerte enfoque en la compatibilidad con versiones anteriores de las características y viene con una herramienta de análisis. Consulte [Evaluación de la complejidad de la actualización con AEM Analyzer](/help/sites-deploying/aem-analyzer.md) para evaluar la complejidad al comenzar a [planificar la actualización](/help/sites-deploying/upgrade-planning.md).
