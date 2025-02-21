---
title: Detalles del documento para el procesador
description: Información conceptual sobre cómo funcionan los procesamientos en AEM Forms Workspace para procesar los distintos tipos de formularios y archivos admitidos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 62%

---

# Detalles del documento para el procesador {#document-details-for-renderer}

## Introducción {#introduction}

En AEM Forms Workspace, se admiten varios tipos de formularios. Entre estas características se incluyen:

* Formularios PDF (XDP/Acroform/PDF aplanados)
* Nuevos formularios HTML
* Imágenes
* Aplicaciones de terceros (por ejemplo, Administración de correspondencia)

Este documento explica el trabajo de estos procesadores desde la perspectiva de la personalización semántica / reutilización de componentes, de modo que los requisitos del cliente se cumplan sin romper ninguna representación. Aunque AEM Forms Workspace permite cualquier cambio semántico/de interfaz de usuario, se recomienda que no se cambie la lógica de procesamiento de distintos tipos de formulario; de lo contrario, los resultados pueden ser impredecibles. El propósito de este documento es para orientación / conocimiento para admitir el procesamiento del mismo formulario, utilizando los mismos componentes de espacio de trabajo en diferentes portales y no para modificar la propia lógica de procesamiento.

## Formularios PDF {#pdf-forms}

Los formularios PDF son procesados por `PdfTaskForm View`.

Cuando se procesa un formulario XDP como PDF, el servicio FormsAugmenter agrega un `FormBridge` JavaScript™. Este JavaScript™ (dentro del formulario PDF) ayuda a realizar acciones como enviar, guardar o quitar formularios sin conexión.

En AEM Forms Workspace, la vista PDFTaskForm se comunica con `FormBridge`JavaScript mediante un HTML intermedio presente en `/lc/libs/ws/libs/ws/pdf.html`. El flujo es:

**Vista de PDFTaskForm: pdf.html**

Se comunica mediante `window.postMessage` / `window.attachEvent('message')`

Este método es la forma estándar de comunicación entre un marco principal y un iframe. Los oyentes de eventos existentes de los formularios PDF abiertos anteriormente se quitan antes de agregar uno nuevo. Esta depuración también tiene en cuenta el cambio entre la pestaña del formulario y la del historial en la vista de detalles de la tarea.

**pdf.html - `FormBridge`JavaScript dentro del PDF procesado**

Se comunica mediante `pdfObject.postMessage` / `pdfObject.messageHandler`

Este método es la forma estándar de comunicación con un PDFJavaScript de un HTML. La vista PdfTaskForm también se encarga de una PDF plana y la procesa sin formato.

>[!NOTE]
>
>No se recomienda editar el pdf.html / contenido de la vista PdfTaskForm.

## Nuevos formularios HTML {#new-html-forms}

La vista de NewHTMLTaskForm representa los nuevos formularios HTML.

Cuando un formulario XDP se procesa como HTML mediante el paquete de formularios móviles implementado en CRX, también agrega `FormBridge` JavaScript para el formulario, que expone diferentes métodos para guardar y enviar datos de formulario.

Esta JavaScript es diferente de la mencionada en PDF forms anterior, pero tiene un propósito similar.

>[!NOTE]
>
>Adobe no recomienda editar el contenido de la vista de NewHTMLTaskForm.

## Formularios Flex y guías {#flex-forms-and-guides}

SwfTaskForm procesa los formularios Flex, y las vistas de HtmlTaskFormlas procesan las guías, respectivamente.

En AEM Forms Workspace, estas vistas se comunican con el SWF real que conforma el formulario o la guía de Flex® mediante un SWF intermedio presente en `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicación se produce mediante `swfObject.postMessage` / `window.flexMessageHandler`.

Este protocolo se define mediante `WsNextAdapter.swf`. Los `flexMessageHandlers` existentes en el objeto window, de los formularios SWF abiertos previamente se quitan antes de agregar uno nuevo. La lógica también tiene en cuenta el cambio entre la pestaña del formulario y la del historial en la vista de detalles de la tarea. `WsNextAdapter.swf` se usa para realizar diversas acciones de formulario, como guardar o enviar.

>[!NOTE]
>
>No se recomienda modificar `WSNextAdapter.swf` o el contenido de la vista de SwfTaskForm / HtmlTaskForm.

## Aplicaciones de terceros (por ejemplo, Administración de correspondencia) {#third-party-applications-for-example-correspondence-management}

Las aplicaciones de terceros se representan mediante la vista de ExtAppTaskForm.

**Comunicación de la aplicación de terceros con AEM Forms Workspace**

El espacio de trabajo de AEM Forms escucha en `window.global.postMessage([Message],[Payload])`

[El mensaje] puede ser una cadena especificada como `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`en el `runtimeMap`. Las aplicaciones de terceros deben utilizar esta interfaz para notificar al espacio de trabajo de AEM Forms según sea necesario. El uso de esta interfaz es obligatorio, ya que AEM Forms Workspace debe saber que, cuando se envía la tarea, puede limpiar la ventana de tareas.

**Comunicación de AEM Forms Workspace con aplicaciones de terceros**

Si los botones de acción directa de AEM Forms Workspace están visibles, llama a `window.[External-App-Name].getMessage([Action])`, donde `[Action]` se lee desde el `routeActionMap`. La aplicación de terceros debe escuchar en esta interfaz y, a continuación, notificar al espacio de trabajo de AEM Forms a través de la API `postMessage ()`.

Por ejemplo, una aplicación de Flex puede definir `ExternalInterface.addCallback('getMessage', listener)` para apoyar esta comunicación. Si la aplicación de terceros desea administrar el envío de formularios mediante sus propios botones, debe especificar `hideDirectActions = true() in the runtimeMap` y puede omitir este oyente. Por lo tanto, esta construcción es opcional.

Puede leer más sobre la integración de aplicaciones de terceros con respecto a Administración de correspondencia en [Integración de Administración de correspondencia en el espacio de trabajo de AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
