---
title: Configurar el servicio de información del sistema
description: Obtenga información sobre cómo configurar el servicio de información del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: e31614a9-d670-4d22-88ba-8953797f6e14
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
source-wordcount: '114'
ht-degree: 10%
---
# Configurar el servicio de información del sistema {#set-up-the-system-information-service}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El servicio de información del sistema proporciona API de REST para recuperar información. Para utilizar el servicio de información del sistema, habilite el extremo REST desde la consola de administración. Realice los siguientes pasos para habilitar el extremo REST:

1. Inicie sesión en la consola de administración. La dirección URL predeterminada de la consola de administración es `https://[hostname]:'port'/adminui.`
1. Vaya a Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio **SystemInfo**.
1. En la lista de la ficha Extremos, seleccione REST y haga clic en **Agregar**.
1. En la pantalla Agregar extremo REST, haga clic en **Agregar**.
