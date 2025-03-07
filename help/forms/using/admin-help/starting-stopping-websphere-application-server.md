---
title: Iniciar y detener del servidor de aplicaciones WebSphere
description: Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios AEM Forms. Este documento describe cómo iniciar y detener el servidor de aplicaciones WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 20cd6efb-edcf-4c87-b0f5-bdec5a0f6280
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# Iniciar y detener del servidor de aplicaciones WebSphere {#starting-and-stopping-websphere-application-server}

Varios procedimientos requieren que detenga o inicie la instancia de WebSphere en la que desea implementar productos de formularios AEM Forms. Si no está seguro de si el servidor de aplicaciones se ha iniciado, puede ver primero el estado del servidor de aplicaciones de WebSphere.

## Ver el estado del servidor de aplicaciones WebSphere {#view-the-status-of-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `serverStatus.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `serverStatus.sh`*nombre_servidor*

## Iniciar el servidor de aplicaciones WebSphere {#start-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `startServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `startServer.sh`*nombre_servidor*

## Detener el servidor de aplicaciones WebSphere {#stop-websphere-application-server}

1. Desde un símbolo del sistema, vaya al directorio `[appserver root]/bin`.
1. Introduzca el siguiente comando y reemplace *server_name* por el nombre de su servidor de aplicaciones de WebSphere:

   * (Windows) `stopServer.bat`*nombre_servidor*
   * (Linux, UNIX) ./ `stopServer.sh`*nombre_servidor*
