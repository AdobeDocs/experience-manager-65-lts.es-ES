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
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# Actualización a Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>La actualización a AEM 6.5 LTS es compatible con los últimos 6 Service Packs.

Esta sección cubre la actualización de una instalación de AEM a AEM 6.5:

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

A continuación se indican algunos cambios importantes que se han producido en las últimas versiones de AEM:

1. La capa Foundation se ha actualizado para admitir Java 17 (que incluye capas de código abierto de paquetes de Apache Sling, Apache Felix y Apache Jackrabbit Oak)

1. El paquete jar de AEM 6.5 LTS ahora es compatible con las especificaciones 5 de las API del servlet Jarkarta y el paquete war se puede implementar en contenedores de servlet que implementen las especificaciones 5/6 de la API del servlet Jakarta

1. El empaquetado de AEM 6.5 LTS uber-jar ha cambiado. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) para obtener más información.

### Se han eliminado los artefactos y las funciones heredadas {#removed-legacy-features-artifacts}

Las siguientes soluciones heredadas se han eliminado de AEM 6.5 LTS. Para obtener más información, consulte TBD: vínculo a las notas de la versión y [Lista de paquetes obsoletos desinstalados después de la actualización](/help/sites-deploying/obsolete-bundles.md)

1. Social
1. Comercio
1. Screens
1. We-retail
1. Integración de búsqueda y promoción

**Artefactos eliminados**

1. CRX-explorer
1. Crx2oak
1. Google guava (eliminado debido a vulnerabilidades de seguridad)
1. Abdera-parser (eliminado debido a vulnerabilidades de seguridad)
1. jdom (`org.apache.servicemix.bundles.jdom`) (eliminado debido a vulnerabilidades de seguridad)
1. `com.github.jknack.handlebars` (eliminado debido a vulnerabilidades de seguridad)

AEM 6.5 LTS tiene un fuerte enfoque en la compatibilidad con versiones anteriores de las características y viene con una herramienta de análisis. Consulte [Evaluación de la complejidad de la actualización con AEM Analyzer](/help/sites-deploying/pattern-detector.md) para evaluar la complejidad a medida que planifica la actualización. Para obtener más información sobre qué más ha cambiado, consulte las notas de la versión completas aquí. TBD: vínculo a las notas de la versión de AEM 6.5 LTS