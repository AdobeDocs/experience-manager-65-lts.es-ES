---
title: No se puede abrir PDF forms basado en XFA en Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
description: No se puede abrir PDF forms basado en XFA en Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
feature: Adaptive Forms,Document Services
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: a28b084e-ec74-4c05-a90c-d447792faa41
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
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%
---
# No se puede abrir PDF forms basado en XFA en Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muchas versiones recientes de exploradores han incluido su propia compatibilidad limitada con PDF forms basado en XFA. Aunque estos exploradores pueden abrir PDF forms basado en XFA, las capacidades proporcionadas son limitadas. Si no puede abrir o enviar un formulario PDF basado en XFA en un explorador moderno, utilice uno de los siguientes métodos:

* Use [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) o [Adobe® Adobe® Reader®](https://get.adobe.com/es/reader/), versión 8 o posterior para abrir y enviar PDF forms basado en XFA.
* Acrobat y Reader, en Microsoft® Windows®, le permiten configurar para abrir archivos PDF en modo de Vista protegida, lo que evita que se abra PDF forms basado en XFA. Asegúrese de que el modo Vista protegida de su Acrobat o Reader esté deshabilitado. Para obtener más información, consulte [Vista protegida (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Para desarrolladores de Forms) Adobe Experience Manager Forms también proporciona asistencia para lo siguiente:

  * [procese formularios basados en XFA en HTML5 Forms](/help/forms/using/introduction.md#key-capabilities-of-html-forms-br) de forma que se puedan abrir en exploradores compatibles con HTML5, incluidos los que se ejecuten en dispositivos móviles como iPad. La representación HTML5 de los formularios mantiene la presentación del diseño de formulario y admite la mayoría de las lógicas de formulario (como JavaScript, cálculo de formulario y validaciones de formulario) incrustadas en la plantilla de formulario XFA.
  * [convertir formularios basados en XFA a Forms adaptable con capacidad de respuesta móvil](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template). Estos formularios proporcionan un diseño interactivo, funciones de personalización y se adaptan de forma dinámica a las respuestas del usuario añadiendo o eliminando campos o secciones según sea necesario. También proporcionan conectores predeterminados para varias fuentes de datos, funciones de documento de registro y una conexión sencilla a Adobe Analytics para evaluar el rendimiento. Para obtener más información, vea [Características y características clave](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=es)
    De este modo, sus inversiones en tecnología en formularios XFA están protegidas y siguen proporcionando una experiencia óptima a los usuarios finales. Para obtener más información, consulte [Documentación del producto de Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=es).
