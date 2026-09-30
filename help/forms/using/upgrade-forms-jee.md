---
title: Actualizar a AEM 6.5 Forms en JEE
description: Puede realizar una actualización directa de AEM 6.1 Forms, AEM 6.2 Forms y LiveCycle ES4 SP1 a AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
hide: true
hidefromtoc: 'yes'
removedfrom6.5.2025: 'yes'
exl-id: 643bc966-b2d8-4626-8c25-b63c8909287e
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: b9cdd520-e7a7-4af9-a95f-296f28882b69
    internal-label: AEM Forms upgrade
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 66%
---
# Actualizar a AEM 6.5 Forms en JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.18.0 Forms en JEE proporciona dos tipos de instaladores: Programa de instalación completo y Programa de instalación de parches.

**Programa de instalación completo**: Puede usar [AEM 6.5.18.0 en el programa de instalación completo de JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para configurar nuevas instancias de AEM Forms o realizar actualizaciones de AEM 6.5.x.x Forms en JEE a AEM 6.5.18.0 Forms en JEE.

**Programa de instalación de parches**: [AEM 6.5.18.0 en el programa de instalación de parches JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) es para clientes que ya utilizan versiones de AEM 6.5.x.x. Puede utilizar el programa de instalación de parches para actualizar a la versión más reciente de AEM Forms.

La siguiente tabla muestra los escenarios para utilizar el programa de instalación completo y de parches.

![Escenario del instalador completo y de parches](assets/full-and-patch-installer.png)

Realice el siguiente procedimiento para utilizar el programa de instalación completo para actualizar el AEM Forms 6.5.x.x existente en JEE a AEM 6.5.18.0 Forms en JEE:

1. Descargue el programa de instalación AEM 6.5 Forms en JEE desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Necesita un contrato de mantenimiento y soporte válido para utilizar el programa de instalación.
1. Consulte [Planificación y lista de comprobación de la actualización](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65_es) para obtener más información sobre las comprobaciones que se deben realizar para garantizar una actualización correcta.
1. Consulte [Prepararse para actualizar a AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65_es) para aprender y realizar las tareas que garantizan que la actualización se ejecute correctamente con un tiempo de inactividad mínimo en el servidor.
1. Según el entorno y el servidor de aplicaciones existentes, elija uno de los siguientes documentos y siga las instrucciones.

   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65_es)
   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65_es)
   * [Actualización de AEM 6.3 o AEM 6.4 Forms a AEM 6.5 Forms para JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65_es)

La actualización directa desde LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms a AEM 6.5 Forms no está disponible. Puede realizar una actualización intermedia a una o más versiones de LiveCycle o AEM Forms y, a continuación, actualizar a AEM 6.5 Forms. Para obtener la lista de versiones intermedias y las instrucciones de actualización correspondientes, consulte [Elegir una ruta de actualización](upgrade.md).
