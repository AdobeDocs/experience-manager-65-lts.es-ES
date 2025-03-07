---
title: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento.
description: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento en el servidor JEE y en el servidor OSGi.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 22dd8daa-b8c6-4e7d-bca3-3958a79fb4b5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Antes de que el servidor de AEM Forms esté completamente activo y todas las aplicaciones estén en funcionamiento, AEM Forms Server comienza a procesar los documentos.


## Se aplica a {#applies-to}

La solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.

## Solución {#solution}

Para resolver el problema, agregue un argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` al [archivo por lotes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante el inicio del servidor.
