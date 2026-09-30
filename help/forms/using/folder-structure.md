---
title: Explicación de la estructura de carpetas
description: Obtenga más información sobre la estructura de carpetas del código fuente de AEM Forms Workspace que se va a personalizar.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
exl-id: 08e6b25c-eef5-4f29-99fa-524f563e7f25
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%
---
# Explicación de la estructura de carpetas {#understanding-the-folder-structure}

Los componentes de AEM Forms Workspace han sido diseñados sobre arquitectura MVC mediante Backbone. Cada componente tiene un archivo para:

* El modelo, que contiene lógica empresarial.
* La plantilla, es decir, un archivo HTML que contiene controles de interfaz.
* La vista, que actúa como una clase de controlador para la plantilla.

Los archivos de todos los componentes se colocan en la estructura de carpetas que se describe a continuación. Para acceder a los archivos, inicie sesión en CRXDE Lite y desplácese hasta `/libs/ws/js/runtime/`.

**models** Contiene modelos de Backbone.

**views** Contiene vistas de Backbone.

**templates** Contiene únicamente las plantillas HTML de los componentes.

**routes** Contiene rutas universales. La carpeta templates dentro de routes contiene el código HTML y las referencias a los componentes.

**services** Contiene la interfaz de servicio para llamar a las API del servidor de Adobe Experience Manager en el extremo REST.

**util** Contiene utilidades genéricas que se pueden utilizar en varios componentes.
