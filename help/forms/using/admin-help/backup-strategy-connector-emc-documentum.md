---
title: Estrategia de copia de seguridad para usuarios de Connector para Documentum&reg; de EMC
description: Consulte cómo crear una estrategia de copia de seguridad para los usuarios de Connector for EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 019e1a9b-c26c-429f-8153-fceeb85f7096
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%
---
# Estrategia de copia de seguridad para usuarios de Connector para Documentum® de EMC {#backup-strategy-for-connector-for-emc-documentum-users}

Si tiene instalado Connector para EMC Documentum®, además de las instrucciones de este capítulo, la estrategia de copia de seguridad y recuperación debe incluir la copia de seguridad (o recuperación) del equipo en el que está instalado el sistema ECM. (Consulte la documentación de ECM Documentum®).

Haga una copia de seguridad del entorno de AEM Forms utilizando el repositorio de ECM y realizando las siguientes tareas:

* Haga una copia de seguridad de los formularios AEM siguiendo las instrucciones que se describen en este documento.
* Realice una copia de seguridad del sistema ECM Documentum® siguiendo las instrucciones de [Copia de seguridad de EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Restaure el entorno de AEM Forms utilizando el repositorio de ECM y realizando las siguientes tareas:

* Restaure su sistema ECM respectivo siguiendo las instrucciones de [Restaurar EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Restaure los formularios de AEM siguiendo las instrucciones descritas en este documento.
