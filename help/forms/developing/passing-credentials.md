---
title: Pasar credenciales mediante encabezados WS-security
description: Obtenga información sobre cómo pasar credenciales mediante encabezados WS-security
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 558d9b27-8734-4da2-b498-5bb2361ac65b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# Pasar credenciales mediante encabezados WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Al invocar un servicio de AEM Forms en JEE mediante servicios web, puede utilizar encabezados WS-Security para pasar la información de autenticación de cliente que AEM Forms requiere en JEE. WS-Security define las extensiones de SOAP para implementar la autenticación de clientes, la confidencialidad de mensajes y la integridad de mensajes. Como resultado, puede invocar AEM Forms en servicios JEE cuando AEM Forms en JEE se implementa como servidor independiente o dentro de un entorno agrupado.

La forma de pasar encabezados WS-Security a AEM Forms en JEE depende de si utiliza clases Java generadas por Axis o un ensamblado de cliente de .NET que consuma la pila nativa de SOAP de un servicio.

>[!NOTE]
>
>Como ejemplo de invocación de un servicio mediante encabezados WS-Security, en este tema se cifra un documento de PDF con una contraseña invocando el servicio Encryption.

Este documento abarca los siguientes temas:

* Pasar la autenticación de cliente mediante clases Java generadas por Axis

* Generando archivos de biblioteca de Axis necesarios para invocar el servicio Encryption

* Invocar el servicio Encryption mediante un encabezado WS-Security

* Pasar la autenticación de cliente mediante un ensamblado de cliente de .NET

* Invocar el servicio Encryption mediante un encabezado WS-Security


## Requisitos  {#requirements}

Para sacar el máximo partido a este documento, debe tener una comprensión sólida de AEM Forms en el software JEE.

>[!MORELIKETHIS]
>
>* [Pasar credenciales mediante encabezados WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
