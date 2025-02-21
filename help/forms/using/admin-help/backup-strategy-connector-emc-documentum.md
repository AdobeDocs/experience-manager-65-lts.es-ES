---
title: Estrategia de copia de seguridad para usuarios de Connector para EMC Documentum&reg;
description: Consulte cómo crear una estrategia de copia de seguridad para los usuarios de Connector for EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
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
