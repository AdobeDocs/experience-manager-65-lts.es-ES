---
title: Usar el modelo de datos de formulario
description: Aprender a utilizar el modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 90%

---

# Usar el modelo de datos de formulario{#use-form-data-model}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model.html?lang=es) |
| AEM 6.5 | Este artículo |


![imagen a pantalla completa](do-not-localize/data-integration.png)

La integración de datos de AEM Forms permite utilizar fuentes de datos de diferentes back-end para crear un modelo de datos de formulario que se puede utilizar como esquema en varios flujos de trabajo de formularios adaptables y comunicaciones interactivas. Para ello, es necesario configurar las fuentes de datos y crear un modelo de datos de formulario basado en los objetos y servicios de modelo de datos disponibles en las fuentes de datos. Para obtener más información, consulte:

* [Integración de datos de AEM Forms](../../forms/using/data-integration.md)
* [Configurar fuentes de datos](../../forms/using/configure-data-sources.md)
* [Crear un modelo de datos de formulario](../../forms/using/create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md)

Un modelo de datos de formulario es una extensión del esquema JSON que puede utilizar para lo siguiente:

* [Crear formularios adaptables y fragmentos](#create-af)
* [Crear comunicaciones interactivas y componentes básicos como fragmentos de texto, lista y condición](#create-ic)
* [Previsualizar comunicaciones interactivas con datos de ejemplo](#preview-ic)
* [Prerrellenar formularios adaptables y comunicaciones interactivas](#prefill)
* [Escribir en diferido datos de formulario adaptable en fuentes de datos](#write-af)
* [Invocar servicios mediante reglas de formulario adaptable](#invoke-services)

## Crear formularios adaptables y fragmentos {#create-af}

Puede crear [formularios adaptables](../../forms/using/creating-adaptive-form.md) y [fragmentos de formulario adaptables](../../forms/using/adaptive-form-fragments.md) a partir de un modelo de datos de formulario. Para utilizar un modelo de datos de formulario al crear un formulario adaptable o un fragmento de formulario adaptable, haga lo siguiente:

1. En la pestaña Modelo de formulario de la pantalla Agregar propiedades, seleccione **[!UICONTROL Modelo de datos de formulario]** en la lista desplegable **[!UICONTROL Seleccionar desde]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Seleccione para expandir **[!UICONTROL Seleccionar modelo de datos de formulario]**. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de formulario.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Solo fragmentos de formulario adaptable**) Puede crear un fragmento de formulario adaptable basado en un único objeto de modelo de datos en un modelo de datos de formulario. Expanda la lista desplegable **[!UICONTROL Definiciones del modelo de datos de formulario]**. Esta lista enumera todos los objetos de modelo de datos del modelo de datos de formulario especificado. Seleccione un objeto de modelo de datos de la lista.

   ![create-af-3](assets/create-af-3.png)

Una vez creado el formulario adaptable o el fragmento de formulario adaptable basado en un modelo de datos de formulario, los objetos de modelo de datos de formulario aparecen en la pestaña **[!UICONTROL Objetos del modelo de datos]** del Explorador de contenido en el Editor de formularios adaptables.

>[!NOTE]
>
>En el caso de los fragmentos de formulario adaptable, solo el objeto de modelo de datos seleccionado en el momento de la creación y los objetos de modelo de datos asociados aparecen en la pestaña Objetos del modelo de datos.

![data-model-objects-tab](assets/data-model-objects-tab.png)

Puede arrastrar y soltar objetos de modelo de datos en el formulario adaptable o en el fragmento para agregar campos de formulario. Los campos de formulario agregados conservan las propiedades de metadatos y el enlace con las propiedades del objeto de modelo de datos. El enlace garantiza que los valores de los campos se actualicen en las fuentes de datos correspondientes al enviar el formulario y se prerrellenen cuando se representa el formulario.

## Crear comunicaciones interactivas {#create-ic}

Puede crear una comunicación interactiva basada en un modelo de datos de formulario que puede utilizar para prerrellenar la comunicación interactiva con datos de fuentes de datos configuradas. Además, los componentes básicos de una comunicación interactiva, como los fragmentos de documento de texto, lista y condición, pueden basarse en un modelo de datos de formulario.

Puede elegir un modelo de datos de formulario al crear una comunicación interactiva o un fragmento de documento. La siguiente imagen muestra la pestaña General del cuadro de diálogo Crear comunicación interactiva.

![create-ic](assets/create-ic.png)

Pestaña General del cuadro de diálogo Crear comunicación interactiva

Para obtener más información, consulte:

[Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)

[Texto en comunicaciones interactivas](/help/forms/using/texts-interactive-communications.md)

[Condiciones de las comunicaciones interactivas](/help/forms/using/conditions-interactive-communications.md)

[Enumerar fragmentos](/help/forms/using/lists.md)

## Usar una vista previa con datos de ejemplo {#preview-ic}

El editor del modelo de datos de formulario permite generar y editar datos de ejemplo para objetos de modelo de datos en el modelo de datos de formulario. Puede utilizar estos datos para previsualizar y probar comunicaciones interactivas y formularios adaptables. Genere los datos de ejemplo antes de obtener la vista previa como se describe en [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md#sample).

Para previsualizar una comunicación interactiva con datos del modelo de datos de formulario de ejemplo:

1. En la instancia de autor de AEM, vaya a **[!UICONTROL Formularios > Formularios y documentos]**.
1. Seleccione una comunicación interactiva y seleccione **[!UICONTROL Vista previa]** en la barra de herramientas para seleccionar **[!UICONTROL Canal web]**, **[!UICONTROL Canal de impresión]** o **[!UICONTROL Ambos canales]** para previsualizar la comunicación interactiva.
1. En el cuadro de diálogo Vista previa de [*canal*], asegúrese de que está seleccionado **[!UICONTROL Probar datos del modelo de datos de formulario]** y seleccione **[!UICONTROL Vista previa]**.

La comunicación interactiva se abre con datos de ejemplo prerrellenados.

![web-preview](assets/web-preview.png)

Del mismo modo, para obtener una vista previa de un formulario adaptable con datos de ejemplo, ábralo en el modo Autor y seleccione **[!UICONTROL Vista previa]**.

## Prerrellenar mediante el servicio del modelo de datos de formulario {#prefill}

AEM Forms proporciona de forma predeterminada un servicio de prerrellenado del modelo de datos de formulario que puede habilitar para formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario. El servicio de prerrellenado consulta las fuentes de datos de los objetos de modelo de datos del formulario adaptable y la comunicación interactiva y prerrellena los datos de la forma correspondiente al representar el formulario o la comunicación.

Para habilitar el servicio de prerrellenado del modelo de datos de formulario de un formulario adaptable, abra las propiedades del contenedor de formulario adaptable y seleccione **[!UICONTROL Servicio de prerrellenado del modelo de datos de formulario]** en la lista desplegable **[!UICONTROL Servicio de prerrellenado]** en el acordeón Básico. A continuación, guarde las propiedades.

![prefill-service](assets/prefill-service.png)

Para configurar el servicio de prerrellenado del modelo de datos de formulario en una comunicación interactiva, puede seleccionar Servicio de prerrellenado del modelo de datos de formulario en la lista desplegable Servicio de prerrellenado al crearlo o posteriormente al modificar las propiedades.

![edit-ic-props](assets/edit-ic-props.png)

Cuadro de diálogo Editar propiedades para una comunicación interactiva

## Escribir los datos de los formularios adaptables enviados en fuentes de datos {#write-af}

Cuando un usuario envía un formulario basado en un modelo de datos de formulario, se puede configurar el formulario para que escriba los datos enviados de un objeto de modelo de datos en sus fuentes de datos. Para aplicar este caso de uso, AEM Forms proporciona la [Acción de envío del modelo de datos de formulario](../../forms/using/configuring-submit-actions.md), disponible de forma predeterminada solo para formularios adaptables basados en un modelo de datos de formulario. Escribe los datos enviados de un objeto de modelo de datos en su fuente de datos.

Para configurar la acción de envío del modelo de datos de formulario, abra las propiedades del contenedor de formulario adaptable y seleccione **[!UICONTROL Enviar mediante el modelo de datos de formulario]** en la lista desplegable Acción de envío, en el acordeón Envío. A continuación, examine y seleccione un objeto de modelo de datos en la lista desplegable **[!UICONTROL Nombre del objeto de modelo de datos que se va a enviar]**. Guarde las propiedades.

Al enviar el formulario, los datos del objeto de modelo de datos configurado se escriben en la fuente de datos correspondiente.

![data-submission](assets/data-submission.png)

También puede enviar los archivos adjuntos del formulario a una fuente de datos mediante la propiedad de objeto del modelo de datos binaria. Haga lo siguiente para enviar archivos adjuntos a una fuente de datos JDBC:

1. Agregue un objeto de modelo de datos que incluya una propiedad binaria al modelo de datos de formulario.
1. En el formulario adaptable, arrastre y coloque el componente **[!UICONTROL Archivo adjunto]** desde el Explorador de componente al formulario adaptable.
1. Seleccione para seleccionar el componente agregado y seleccione ![settings_icon](assets/settings_icon.png) para abrir el Explorador de propiedades del componente.
1. En el campo Referencia de enlace, seleccione ![foldersearch_18](assets/foldersearch_18.png) y desplácese hasta seleccionar la propiedad binaria añadida en el modelo de datos de formulario. Configure otras propiedades según corresponda.

   Seleccione ![check-button](assets/check-button.png) para guardar las propiedades. El campo Datos adjuntos ahora está enlazado a la propiedad binaria del modelo de datos de formulario.

1. En la sección Envío de las propiedades del contenedor de formulario adaptable, active **[!UICONTROL Enviar archivos adjuntos del formulario]**. Esto envía el archivo adjunto del campo de propiedad binaria a la fuente de datos al enviar el formulario.

## Invocar servicios desde formularios adaptables mediante reglas {#invoke-services}

En un formulario adaptable basado en un modelo de datos de formulario, puede [crear reglas](../../forms/using/rule-editor.md) para invocar servicios configurados en el modelo de datos de formulario. La operación **[!UICONTROL Invocar servicios]** en una regla enumera todos los servicios disponibles en el modelo de datos de formulario y permite seleccionar campos de entrada y salida para el servicio. También puede usar el tipo de regla **Set Value** para invocar un servicio del modelo de datos de formulario y establecer el valor de un campo en la salida de vuelta por el servicio.

Por ejemplo, la siguiente regla invoca un servicio de obtención que toma el ID de empleado como entrada, y los valores devueltos se rellenan en los campos correspondientes ID de la persona dependiente, Apellidos, Nombre y Género del formulario.

![invoke-service](assets/invoke-service.png)

Además, puede usar la API `guidelib.dataIntegrationUtils.executeOperation` para escribir un JavaScript en el Editor de código del Editor de reglas. Para obtener más información sobre las API, consulte [API para invocar el servicio del modelo de datos de formulario](/help/forms/using/invoke-form-data-model-services.md).
