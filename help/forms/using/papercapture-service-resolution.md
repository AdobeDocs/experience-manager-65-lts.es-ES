---
title: Artículo de solución de problemas para resolver el problema cuando el servicio PaperCapture no realiza operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF.
description: Conozca los pasos para resolver el problema en el que el servicio PaperCapture no realiza operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 19%

---


# El servicio PaperCapture no puede realizar la operación de OCR en archivos PDF

## Problema

Después de actualizar a AEM Forms Service Pack 6.5.21.0, el servicio `PaperCapture` no puede realizar operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF. El servicio no genera resultados en forma de PDF o de archivo de registro.

## Se aplica a

Esta solución se aplica a:
* AEM Forms en todos los servidores JEE de (JBoss, Weblogic, Websphere)
* AEM Forms en servidores OSGi

## Solución

1. Descargue la [revisión](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0) del Portal de distribución de software.
1. Extraiga y copie el contenido de la carpeta descargada.
1. Vaya a las rutas siguientes para los servidores de aplicaciones correspondientes:
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **esfera web**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configuración de OSGi**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Detenga el servidor de aplicaciones de AEM.
1. Reemplace el contenido existente de la carpeta `PaperCaptureSvc` con el contenido copiado.
1. Reinicie el servidor de aplicaciones de AEM.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.
