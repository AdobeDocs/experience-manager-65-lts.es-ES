---
title: Usar la firma manuscrita en formularios HTML5
description: Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es ser compatibles con firmas. La firma de documentos en dispositivos móviles es una forma aceptada de firmar formularios en dispositivos móviles.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 96%

---

# Usar la firma manuscrita en formularios HTML5{#using-scribble-signature-in-html-forms}

Los formularios HTML5 se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es ser compatibles con firmas. Garabatear (escribir con un lápiz o un dedo) se está convirtiendo en una forma aceptada de firmar formularios en dispositivos móviles. Los formularios HTML5 y Forms Designer ahora habilitan la opción de tener un campo de firma de anotaciones en el formulario. Cuando el formulario se procesa en el explorador, se puede iniciar sesión en estos campos con un lápiz, ratón o contacto.

## Cómo diseñar un formulario mediante el campo Firma manuscrita {#how-to-design-a-form-using-scribble-signature-field}

1. Abra un formulario en Forms Designer.
1. Arrastre y suelte el campo Firma manuscrita en la página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Las dimensiones del campo seleccionado en Forms Designer se reflejan cuando se procesa el campo. Sin embargo, la dimensión del cuadro de firma procesada se calcula en función de la relación de aspecto del campo y no de la dimensión especificada en Forms Designer.

1. Configurar el campo Firma manuscrita

   El campo Firma manuscrita, de forma predeterminada, marca la información de geolocalización como obligatoria durante el proceso de firma en iPad (y es opcional para otros dispositivos). Este comportamiento predeterminado se puede anular cambiando el valor de la propiedad `geoLocMandatoryOnIpad`. Esta propiedad se expone como extras en el campo Firma manuscrita. Los pasos para modificarla son los siguientes:

   1. En el formulario, seleccione el campo Firma manuscrita.
   1. Seleccione la pestaña **Fuente XML**.

      >[!NOTE]
      >
      >Para abrir la pestaña Fuente XML, haga clic en **Ver** > **Fuente XML**.

   1. Busque la etiqueta `<ui>` en la etiqueta `<field>` y modifique el código fuente para que tenga la siguiente apariencia:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Seleccione la pestaña **Vista de diseño**. En el cuadro de confirmación, haga clic en **Sí**.
   1. Guarde el formulario.

1. Representar el formulario en un explorador de escritorio o dispositivo compatible.

## Interrelación con las firmas manuscritas {#interfacing-with-the-scribble-signatures}

### Firmar {#signing}

Una vez que se ha agregado un campo de Firma manuscrita al formulario y se ha procesado, al pulsar o hacer clic en el campo se abre un cuadro de diálogo. El usuario puede garabatear una firma en el área de dibujo designada por un rectángulo de puntos con un ratón, un dedo o un lápiz.

![geolocation](assets/geolocation.png)

**A.** Pincel **B.** Borrador **C.** Geolocalización **D.** Información de geolocalización

### Geo-tagging {#geo-tagging}

Al hacer clic en el icono de geolocalización mientras se crea la firma manuscrita, la ubicación geográfica y la información horaria se incrustarán en el campo.

>[!NOTE]
>
De forma predeterminada, en iPad es obligatorio incrustar información de geolocalización.

En iPad, el icono de geolocalización no se muestra de forma predeterminada y la información de geolocalización se incrusta automáticamente al hacer clic en **Aceptar**.

Para los iPads, esta configuración se puede modificar al cambiar el valor del parámetro `geoLocManadatoryOnIpad` a `0`, en los parámetros init del campo.

* Cuando la información de geolocalización es obligatoria, al usuario se le presenta un área de dibujo reducida. El texto de geolocalización se agrega cuando el usuario hace clic en **Aceptar** en el área restante.
* En otros casos, el usuario se presenta con un área de cajón completa. Si el usuario decide incrustar la información de geolocalización, esta área cambia de tamaño para ajustarse al texto de geolocalización.

### Borrar una firma {#clearing-a-signature}

Al utilizar esta función, un usuario puede hacer clic en el botón **Borrador** para borrar el campo y volver a empezar. Si se agregó información de geolocalización, también se borrará.

### Guardar una firma {#saving-a-signature}

Al hacer clic en **Aceptar** se guarda el garabato como una imagen en el campo. La imagen y los valores se pueden enviar al servidor para un procesamiento posterior. Una vez que el usuario ha hecho clic en **Aceptar**, el campo de garabatos quedará bloqueado. La firma no se podrá volver a editar con el widget de garabatos.

Al pulsar o hacer clic en el campo Firma manuscrita se abre el cuadro de diálogo en modo de solo lectura.

![3](assets/3.png)

### Seleccionar el tamaño de la pluma {#selecting-pen-size}

Haga clic en el icono **Pinceles** para mostrar una lista de los tamaños de pluma disponibles. Haga clic en un tamaño de pluma para utilizar la pluma correspondiente.

### Eliminar firmas del formulario {#delete-signatures-from-the-form}

Para eliminar las firmas del formulario, haga lo siguiente:

* (Dispositivos móviles) Presione durante mucho tiempo el campo de firma y, en el cuadro de diálogo de confirmación, seleccione **Sí**.
* (Escritorio) Pase el ratón sobre el campo de firma y haga clic en el botón **Cancelar** y, en el cuadro de diálogo de confirmación, haga clic en **Sí**.
