---
title: Especificar la configuración de seguridad
description: Obtenga información sobre cómo especificar la configuración de seguridad para proteger archivos de datos XML. La función de configuración de seguridad controla las entidades externas en las entradas XML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: ccda0b61-f22a-4ae3-95e6-74d545d6d890
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '101'
ht-degree: 7%
---
# Especificar la configuración de seguridad {#specify-security-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Output permite controlar si se resuelven las entidades externas en las entradas XML. De forma predeterminada, se resuelven, pero puede cambiar este comportamiento para aumentar la seguridad del sistema de formularios de AEM.

**Impedir el procesamiento de archivos de datos XML que contengan referencias a entidades externas**

1. En la consola de administración, haga clic en Servicios > Resultados.
1. Desactive la casilla Resolver entidades externas.
1. Haga clic en Guardar.
