---
title: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento.
description: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento en el servidor JEE y en el servidor OSGi.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 22dd8daa-b8c6-4e7d-bca3-3958a79fb4b5
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
source-wordcount: '110'
ht-degree: 3%
---
# AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Antes de que el servidor de AEM Forms esté completamente activo y todas las aplicaciones estén en funcionamiento, AEM Forms Server comienza a procesar los documentos.


## Se aplica a {#applies-to}

La solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.

## Solución {#solution}

Para resolver el problema, agregue un argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` al [archivo por lotes](/help/sites-deploying/command-line-start-and-stop.md#windows-platform-start-bat-script-example) durante el inicio del servidor.
