---
title: Lectores de pantalla para formularios HTML5
description: Enumera los lectores de pantalla compatibles con los formularios HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: cf652b91-ee92-4d54-8a29-2653d882d5f2
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 66%
---
# Lectores de pantalla para formularios HTML5 {#screen-readers-for-html-forms}

Los componentes de formularios HTML5 representan la plantilla de formulario XFA en formato HTML5. Todos los exploradores estándar compatibles con HTML5 pueden procesar estos formularios. Para admitir una experiencia de captura de datos similar en los formularios PDF y HTML5, la presentación de los PDF se conserva en los formularios HTML5.

Los formularios HTML5 utilizan construcciones estándar HTML que permiten utilizar herramientas de accesibilidad regulares para que el HTML se utilice con estos formularios. Si un formulario está diseñado según las prácticas recomendadas para formularios accesibles, funcionará con cualquier lector de pantalla admitido. Además, estos formularios están habilitados para la navegación mediante el teclado.

## Estándares de accesibilidad {#accessibility-standards}

Los formularios HTML5 cumplen con la sección 508 para accesibilidad con excepciones conocidas. Consulte [VPAT para formularios HTML5](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) para obtener más información.

## Lectores de pantalla certificados para formularios HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 en Microsoft® Windows
* VoiceOver en macOS X y iPad

### JAWS {#jaws}

Todos los accesos directos y las pulsaciones de teclas predeterminados funcionan en los formularios HTML5. Para obtener más información sobre el uso de JAWS, visite [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

Los formularios HTML5 son compatibles con todas las pulsaciones de teclas y gestos predeterminados de Voice Over. Para obtener más información sobre cómo configurar y usar VoiceOver, consulte [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## Problemas conocidos {#known-issues}

* **(Solo el explorador interno 9)** En los formularios HTML5, las páginas se cargan bajo demanda (de forma dinámica). La carga de páginas bajo demanda causa problemas con el funcionamiento de los lectores de pantalla. Cuando el foco del lector de pantalla está en el último campo de la página y el usuario pulsa la pestaña, el lector de pantalla vuelve a centrarse en el primer campo de la primera página del formulario.
* **(solo Explorador interno 9)** El control Selector de fecha de los formularios HTML5 no es totalmente accesible con el teclado. En el control Selector de fecha, si pulsa las teclas Subir/Bajar varias veces, se cerrará el control Selector de fecha y el enfoque pasará al campo siguiente/último.

* VoiceOver no puede detectar las teclas de flecha en el widget de fecha en iPad Safari.
