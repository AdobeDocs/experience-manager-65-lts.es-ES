---
title: Diseñar plantillas de formulario para formularios HTML5
description: AEM Forms puede procesar plantillas de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario con Designer y utilizar la capacidad de representación de HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 90%

---

# Diseñar plantillas de formulario para formularios HTML5{#designing-form-templates-for-html-forms}

El componente de formularios HTML5 de AEM puede procesar plantillas de formulario XFA en formato HTML5. Los diseñadores de formularios pueden diseñar plantillas de formulario mediante [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) y utilizar la capacidad de representación de HTML5. Estas plantillas de formulario, junto con sus recursos, pueden residir en el repositorio de AEM, el sistema de archivos o exponerse a través de http. Sin embargo, si planea administrar los formularios con Forms Manager, las plantillas y los recursos deben residir en el repositorio de AEM.

Aunque los formularios HTML5 coinciden en buena medida con el comportamiento de los formularios PDF, hay algunas características en ambos formatos que no se pueden aplicar al otro. Por ejemplo, la forma en que se aplican los códigos de barras en un formulario PDF en Adobe Reader varía según el formulario de Mobile o la forma en que el formulario se firma digitalmente también varía según el formato. Para obtener más información sobre estas variaciones, consulte [Diferenciar las características entre formularios HTML5 y los formularios PDF](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para ver las características comunes de XFA, consulte las siguientes prácticas recomendadas y directrices para diseñar un formulario que funcione en ambos formatos.

## Prácticas recomendadas {#best-practices}

La mayoría de los pasos para diseñar una plantilla de formulario, como enlaces de esquema o escribir lógica de formulario, son los mismos. Sin embargo, debido a las diferencias inherentes entre el procesamiento y el motor de script de un cliente grande como Adobe Reader y los formularios basados en el explorador, hay algunas recomendaciones que se describen en el artículo [Prácticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Estas prácticas recomendadas le ayudan a diseñar plantillas de formulario para que funcionen según lo esperado en ambos formatos.

### Funciones en AEM Forms Designer para formularios HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Previsualizar HTML {#preview-html}

La pestaña Previsualizar HTML se agrega en el modo Diseño para que los diseñadores de formularios obtengan una vista previa de los formularios en formato HTML5 durante el proceso de diseño. Para obtener más información sobre cómo habilitar y configurar esta capacidad en AEM Forms Designer, consulte [Previsualizar HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma manuscrita {#scribble-signature}

El objetivo principal de los formularios HTML5 son los dispositivos táctiles. Por lo tanto, se agrega un nuevo control de firma de anotaciones en AEM Forms Designer. Puede hacer clic o arrastrar y soltar el control de firma de anotaciones en la plantilla de formulario y configurarlo. Se representa como un campo de anotaciones en la representación HTML5 y se puede utilizar para garabatear la firma en dispositivos táctiles. En equipos de escritorio, se puede utilizar como campo de garabato mediante el control del ratón. Para obtener más información sobre cómo utilizar esta función, consulte [Campo de garabato XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato de texto enriquecido {#rich-text-format}

Puede convertir un campo de texto en un campo de texto enriquecido. Agregar una lista de opciones de formato al campo de texto. Para convertirlo, abra Forms Designer y seleccione el campo de texto en **[!UICONTROL Vista de diseño]**. En la pestaña **[!UICONTROL Campo]**, seleccione **[!UICONTROL Texto enriquecido]** de la lista desplegable **[!UICONTROL Formato de campo]**. Ahora, cuando el formulario XFA se represente como un formulario HTML5, el campo se procesará como un campo de texto enriquecido. Seleccione ![Maximizar](assets/maximize_icon.svg) para ver opciones de formato adicionales.
