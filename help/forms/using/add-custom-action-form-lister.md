---
title: Agregar acciones personalizadas a elementos de lista de formularios
description: Los desarrolladores de formularios pueden agregar más acciones a la lista de formularios de la página del portal de formularios. De forma predeterminada, la lista de formularios le permite acceder al formulario, rellenarlo y enviarlo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
exl-id: 4678557b-904d-43c4-b53c-5710ab081f0f
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
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
source-wordcount: '265'
ht-degree: 94%
---
# Agregar acciones personalizadas a elementos de lista de formularios{#adding-custom-action-on-form-lister-items}

En AEM Forms, puede crear una página del portal que enumere los formularios disponibles. De forma predeterminada, puede buscar y mostrar formularios en una página del portal. Puede abrir formularios para rellenar y enviar la información. Solo se proporcionan las acciones de procesamiento predeterminadas para los formularios enumerados en una página del portal. Para obtener más información sobre las acciones disponibles en una página del portal, consulte [Crear una página de portal de formularios](../../forms/using/creating-form-portal-page.md).

Puede agregar otras opciones a la página del portal. Estas opciones o acciones se pueden personalizar si personaliza la plantilla del portal de formularios.

Este artículo muestra cómo crear un botón para enviar el vínculo de un formulario, directamente desde una página del portal de formularios. Esta personalización requiere la actualización de la plantilla para el componente Buscar y listar.

El código requerido para agregar la acción a la plantilla está disponible a continuación. El atributo `onclick` del fragmento de código tiene un script para enviar un vínculo de un formulario por correo electrónico.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

Puede agregar acciones similares en la plantilla personalizada. Para definir una función de JavaScript, agregue la función en un script de nivel de página y vincúlelo con el elemento HTML requerido. En el ejemplo anterior, la expresión `onclick` es la función vinculada.

Después de realizar las ediciones en la plantilla, la página del portal de muestra contiene un botón para enviar el vínculo del formulario por correo electrónico, como se muestra a continuación.

![correo electrónico](assets/email.png)
