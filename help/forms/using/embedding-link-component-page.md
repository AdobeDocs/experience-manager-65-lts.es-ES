---
title: Incrustar un componente de vínculo en una página
description: Puede utilizar el componente de vínculo para vincular un documento adaptable o un formulario adaptable desde cualquier página.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 97%

---

# Incrustar un componente de vínculo en una página{#embedding-link-component-in-a-page}

## Requisitos previos {#prerequisites}

El componente de vínculo es miembro de la categoría Servicios de documento. Asegúrese de que la categoría Servicios de documentos esté visible en el explorador de componentes de AEM. Si la categoría no aparece en la lista, siga los pasos que se indican en [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md).

## Componente Vínculo {#link-component}

El componente Vínculo permite a los autores del portal de formularios crear un vínculo a un formulario adaptable desde cualquier lugar de una página. El componente Vínculo está disponible en la sección Servicios de documentos del explorador de componentes.

Siga estos pasos para agregar un componente Vínculo a la página:

1. Arrastre el **Vínculo** en la página. Seleccione el componente y seleccione ![cmppr](assets/cmppr.png). Se abrirá el cuadro de diálogo Editar el componente Vínculo.

   ![edit-link-component](assets/edit-link-component.png)

1. En la pestaña **Mostrar**, configure lo siguiente:

   * **Pie de ilustración del vínculo**: Texto o rótulo del vínculo.
   * **Información del objeto del vínculo**: Información del objeto para el vínculo.
   * **Plantilla de diseño**: Plantilla para el diseño del componente Vínculo.

1. Abra la pestaña **Información del recurso** y especifique el tipo de recurso. Un recurso puede ser un **formulario**. Según el tipo de recurso seleccionado, se mostrarán las siguientes opciones:

   * **Ruta de recursos**: Ruta del repositorio en la que se almacena el recurso.

   * **Tipo de procesamiento**: El formato de procesamiento: PDF, HTML o Automático. El tipo de procesamiento automático detecta el entorno del usuario y, en consecuencia, procesa el formulario como HTML o como PDF. Por ejemplo, si se accede al formulario desde un dispositivo móvil, el tipo de procesamiento automático procesará el formulario en HTML.
   * **Enviar URL:** URL del servlet donde se envían los datos del formulario.
   * **Perfil del HTML**: Perfil para procesar el formulario como HTML.
   * **Perfil del PDF**: Perfil para procesar el formulario como documento PDF.

1. Abra la pestaña **Avanzado**. Puede especificar los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

   Seleccione **Listo** para guardar la configuración.

## Prácticas recomendadas para usar el componente Vínculo {#best-practices-for-using-link-component-br}

* Asegúrese de seleccionar PDF como tipo de procesamiento si la ruta especificada en Ruta de formulario apunta a un documento que tiene PDF como formato de procesamiento permitido.
* La dirección URL de envío de un formulario se puede especificar en varios lugares y su orden de prioridad es el siguiente:

   1. La dirección URL de envío incrustada en el formulario (en el botón de envío) tiene la prioridad más alta.
   1. La dirección URL de envío que se menciona en el Administrador de Forms tiene la prioridad media.
   1. Enviar URL mencionada en el portal de formularios tiene la prioridad más baja.
