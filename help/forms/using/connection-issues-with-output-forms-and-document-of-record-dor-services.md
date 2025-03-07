---
title: Problemas de conexión con los servicios de salida, Forms y DoR (documento de registro)
description: Resuelva los errores de conexión de AEM Forms posteriores al SP19. Detenga, instale Microsoft Visual C++ y reinicie el servidor para obtener una solución perfecta. Solución de problemas de los servicios Output, Forms y DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: c84ba536-a78d-4cf9-a480-59cb18e41076
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 21%

---

# No se puede usar el servicio Output, el servicio Forms o el servicio Documento de registro (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problema

Después de instalar el paquete de servicio 19 de AEM Forms 6.5, al intentar usar el servicio Output, el servicio Forms o el servicio de documento de registro (DoR), puede producirse un error de `Connection to failed service`.

## Solución

Para resolver el problema:

1. Detenga la instancia de AEM 6.5 Forms.
1. Descargue e instale la versión de [64 bits de los paquetes redistribuibles de Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 y 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) en el equipo donde esté instalado AEM 6.5 Forms.
1. Reinicie el servidor de AEM Forms.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.


>[!NOTE]
>
>
> Asegúrese de instalar el Redistribuible, incluso si hay una versión anterior instalada.
