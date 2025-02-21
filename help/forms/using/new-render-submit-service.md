---
title: Nuevo servicio de procesamiento y envío
description: Defina los servicios de procesamiento y envío en Workbench para procesar el formulario XDP como HTML o PDF según el dispositivo desde el que se accede a él.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 97%

---

# Nuevo servicio de procesamiento y envío{#new-render-and-submit-service}

## Introducción {#introduction}

Al definir una operación `AssignTask` en Workbench, especifique un formulario concreto (un formulario XDP o PDF). Especifique también un conjunto de servicios de procesamiento y envío mediante un perfil de acción.

Un XDP se puede procesar como un formulario PDF o HTML. Las nuevas funciones permiten hacer lo siguiente:

* Procesar y enviar un formulario XDP como HTML
* Procesar y enviar un formulario XDP como PDF en equipos de escritorio y como HTML en dispositivos móviles (por ejemplo, un iPad)

### Nuevo servicio de formularios HTML {#new-html-forms-service}

El nuevo servicio HTML Forms utiliza la nueva función de Forms para admitir el procesamiento de formularios XDP como HTML. El nuevo servicio de formularios HTML expone los siguientes métodos:

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Encontrará más información sobre los perfiles de formularios móviles en [Creación de un perfil personalizado](/help/forms/using/custom-profile.md).

## Nuevos procesos de procesamiento y envío de formularios HTML {#new-html-form-render-amp-submit-processes}

Especifique un proceso de procesamiento y envío con el formulario en cada operación &quot;AssignTask&quot;. Las API de TaskManager `renderForm` y `submitForm` llaman a estos procesos para permitir la administración personalizada. Semántica de estos procesos para el nuevo formulario HTML:

### Procesar un nuevo formulario HTML {#render-a-new-html-form}

Como todos los procesos de procesamiento, el nuevo proceso para procesar HTML incluye los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outFormDoc`

Este método simula el comportamiento exacto de la API `renderHTMLForm` de NewHTMLFormsService. Llama a la API `generateFormURL` para obtener la URL para la representación HTML del formulario. A continuación, rellena runtimeMap con las siguientes claves o valores:

new html form = true

newHTMLFormURL = la URL devuelta después de llamar a la API `generateFormURL`.

### Enviar un nuevo formulario HTML {#submit-a-new-html-form}

Este proceso para enviar un nuevo formulario HTML admite los siguientes parámetros de E/S:

Entrada - `taskContext`

Salida - `runtimeMap`

Salida - `outputDocument`

El proceso establece `outputDocument` en el `inputDocument` recuperado de `taskContext`.

## Procesos de procesamiento o envío predeterminados y perfiles de acción {#default-render-or-submit-processes-and-action-profiles}

Los servicios de procesamiento y envío predeterminados permiten procesar PDF en un equipo de escritorio y HTML en dispositivos móviles (iPad).

### Formulario de procesamiento predeterminado {#default-render-form}

Este proceso procesa fácilmente un formulario XDP en diferentes plataformas. El proceso recupera el agente de usuario de `taskContext` y utiliza los datos para llamar al proceso para procesar el HTML o el PDF.

![representación-de-formulario-predeterminada](assets/default-render-form.png)

### Formulario de envío predeterminado {#default-submit-form}

Este proceso envía fácilmente un formulario XDP en diferentes plataformas. Recupera el agente de usuario de `taskContext` y utiliza los datos para llamar al proceso y enviar el HTML o el PDF.

![formulario-envío-predeterminado](assets/default-submit-form.png)

## Cambiar el procesamiento de formularios móviles de PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Los exploradores están retirando gradualmente la compatibilidad con los complementos basados en NPAPI, incluidos los complementos de Adobe Acrobat y Adobe Acrobat Reader. Puede cambiar el procesamiento de los formularios móviles de PDF a HTML realizando los siguientes pasos:

1. Inicie sesión en Workbench como un usuario válido.
1. Seleccione **Archivo** > **Obtener aplicaciones**.

   Aparece el cuadro de diálogo Obtener aplicaciones.

1. Seleccione las aplicaciones para las que desea cambiar el procesamiento del formulario móvil y haga clic en **Aceptar**.
1. Abra el proceso para el que desea cambiar el procesamiento.
1. Abra el punto de inicio o la tarea de destino, vaya a la sección Presentación y datos y haga clic en **Administrar perfiles de acción**.

   Aparece el cuadro de diálogo Administrar perfiles de acción.
1. Cambie las configuraciones del perfil de procesamiento predeterminado de PDF a HTML y haga clic en **Aceptar**.
1. Compruebe el proceso.
1. Repita los pasos para cambiar el procesamiento de otros procesos.
1. Implemente la aplicación correspondiente a los procesos que ha cambiado.

### Perfil de acción predeterminado {#default-action-profile}

El perfil de acción predeterminado procesaba el formulario XDP como PDF. Este comportamiento se ha cambiado para utilizar los procesos Formulario de procesamiento predeterminado y Formulario de envío predeterminado.

A continuación, encontrará algunas de las preguntas más frecuentes sobre los perfiles de acción:

![gen_pregunta_b_20](assets/gen_question_b_20.png) **¿Qué procesos de procesamiento/envío estarán disponibles de forma predeterminada?**

* Guía de procesamiento (las guías están obsoletas)
* Guía de procesamiento de formularios
* Procesar un formulario PDF
* Procesar un formulario HTML
* Procesar un nuevo formulario HTML (nuevo)
* Formulario de procesamiento predeterminado (nuevo)

Y procesos de envío similares.

![gen_pregunta_b_20](assets/gen_question_b_20.png) **¿Qué perfiles de acción estarán disponibles de forma predeterminada?**

Para los formularios XDP:

* Predeterminado (procesar/enviar con los nuevos procesos &quot;Procesamiento/Envío&quot;)

![gen_pregunta_b_20](assets/gen_question_b_20.png) **¿Qué debe hacer el diseñador de procesos para que el formulario se procese en forma de HTML en un dispositivo y de PDF en un equipo de escritorio?**

Nada. El perfil de acción predeterminado se elige automáticamente, al igual que el modo de procesamiento.

![gen_pregunta_b_20](assets/gen_question_b_20.png) **¿Qué hay que hacer para que el formulario se procese en forma de HTML en un equipo de escritorio?**

El usuario debe seleccionar el botón de opción HTML del perfil predeterminado.

![gen_pregunta_b_20](assets/gen_question_b_20.png) **¿Cambiar el comportamiento predeterminado del perfil de acción puede tener algún impacto en la actualización?**

Sí. Dado que los servicios de procesamiento y envío asociados anteriormente al perfil de acción predeterminado eran diferentes, se consideran una personalización de los formularios existentes. Haga clic en **Restaurar valores predeterminados** para volver a establecer los servicios de procesamiento y envío predeterminados.

Si ha modificado los servicios de procesamiento o envío de formularios PDF existentes o ha creado servicios personalizados (por ejemplo, Personalizado1), y desea utilizar la misma funcionalidad para la representación HTML, debe replicar el nuevo servicio de procesamiento o envío (por ejemplo, como Personalizado2) y aplicarle las mismas personalizaciones que a estos. Ahora, modifique el perfil de acción para que el XDP empiece a utilizar los servicios Personalizado2 en lugar de Personalizado1 para procesar o enviar formularios.

¿Qué debe hacer el diseñador de procesos para que el formulario se procese en HTML en un dispositivo y en PDF en un equipo de escritorio?
¿Qué debe hacer el diseñador de procesos para que el formulario se procese en HTML en un dispositivo y en PDF en un equipo de escritorio?
