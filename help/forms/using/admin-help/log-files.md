---
title: Archivos de registro
description: Los eventos como los errores de tiempo de ejecución o de inicio se registran en los archivos de registro del servidor de aplicaciones, que se pueden abrir con cualquier editor de texto.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 3%

---

# Archivos de registro {#log-files}

Los eventos, como los errores en tiempo de ejecución o de inicio, se registran en los archivos de registro del servidor de aplicaciones. Si tiene algún problema al implementar en el servidor de aplicaciones, puede utilizar los archivos de registro para ayudarle a encontrar el problema. Puede abrir los archivos de registro con cualquier editor de texto.

(JBoss) Los siguientes archivos de registro se encuentran en el directorio `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[aaaa-mm-dd]*
* server.log

(WebLogic) Los archivos de registro del dominio se encuentran en el directorio `[appserverdomain]` y los archivos de registro del servidor se encuentran en el directorio `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Los siguientes archivos de registro se encuentran en el directorio `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log
