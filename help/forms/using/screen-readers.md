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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 70%

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
