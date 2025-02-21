---
title: Agregar archivos adjuntos
description: Agregue fotografías y notas garabateadas como anotaciones a su tarea en la aplicación de AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 76%

---

# Agregar archivos adjuntos{#adding-attachments}

## Agregar archivos adjuntos en formularios sincronizados con el servidor de flujo de trabajo de AEM Forms (AEM Forms en JEE) {#adding-annotations}

La aplicación de AEM Forms permite adjuntar imágenes, notas garabateadas y notas de texto al formulario sincronizado con el servidor JEE de AEM Forms. Si el formulario se carga desde un servidor del flujo de trabajo de AEM Forms, los archivos adjuntos se agregan al formulario. Puede seleccionar el botón de datos adjuntos ![attachments-app](assets/attachments-app.png) para ver todos los archivos adjuntos de un formulario juntos. La notificación roja especifica el número de archivos adjuntos en el formulario. Si no hay datos adjuntos en el formulario, no verá el botón de notificaciones rojo. Si no hay datos adjuntos en el formulario, al seleccionar el botón de datos adjuntos ![adjuntar](assets/attch.png), obtendrá opciones para adjuntar fotos o garabatos.

Las opciones son las siguientes:

* **Galería**: permite agregar una imagen de las imágenes guardadas en el dispositivo.

* **Cámara**: permite tomar una imagen y agregarla al formulario.

* **Notas**: permite agregar un garabato o una nota de texto. Use ![garabato](assets/scribble.png) para agregar un garabato y el ![teclado](assets/keyboard.png) para agregar una nota de texto.

>[!NOTE]
>
>Los archivos adjuntos agregados por un usuario son visibles para otros usuarios de aplicaciones de AEM Forms. Otros usuarios no pueden eliminar los archivos adjuntos que haya agregado un usuario.
>

### Pantalla de archivos adjuntos {#the-attachments-screen}

Para ver todos los archivos adjuntos en un lugar, seleccione ![attachments-app](assets/attachments-app.png). Aquí puede agregar, cambiar el nombre y eliminar archivos adjuntos.

![Todos los archivos adjuntos en un lugar](assets/attachments-screen.png)

Puede usar el botón **+** de la pantalla de archivos adjuntos para adjuntar otra imagen, garabato o texto.

### Agregar una fotografía {#adding-a-photograph}

Puede utilizar la cámara del dispositivo móvil o guardar imágenes en el dispositivo para adjuntar una imagen en el formulario.

1. Seleccione el botón de datos adjuntos ![attch](assets/attch.png) en la parte inferior de la ventana.
1. Seleccione **Galería** o **Cámara** en la ventana emergente que aparece.
1. En función de la opción seleccionada, realice lo siguiente:

   1. Si selecciona **Cámara**.

      Tome una foto. A continuación, seleccione el botón **Usar** ![use-pic](assets/use-pic.png).

      O bien, selecciona el botón **Repetir** ![repetir](assets/retake.png) para volver a tomar la fotografía.

   1. Si selecciona **Galería**.

      Aparecerá el explorador de imágenes del dispositivo. En el explorador de imágenes del dispositivo, seleccione la imagen que desea adjuntar.

### Agregar una nota {#adding-a-note}

La opción **Notas** permite agregar garabatos hechos a mano alzada y archivos adjuntos de texto en el formulario.

1. Seleccione el botón de datos adjuntos ![attch](assets/attch.png) en la parte inferior de la ventana.
1. Seleccione **Notas** en la ventana emergente que aparece.
1. En la interfaz de usuario de Notas que se inicia, realice un garabato a mano alzada.

   ![Interfaz de Garabatos](assets/scribble-ui.png)

   Garabato

   Puede utilizar las siguientes opciones en la interfaz de garabatos:

   * **Borrar**: borra la pantalla.
   * **Botón Listo**: adjunta el garabato actual.
   * **Botón Cancelar**: descarta el garabato actual y sale de la interfaz de usuario de Garabatos.
   * ![teclado](assets/keyboard.png): borra el garabato y permite agregar una nota de texto.

   ![Teclado en los garabatos de la aplicación de AEM Forms](assets/keyboard-inapp.png)

## Archivos adjuntos en formularios sincronizados con los servidores de AEM Forms sin flujo de trabajo de AEM Forms (AEM Forms en OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Los archivos adjuntos para formularios móviles sincronizados con servidores OSGi de AEM Forms funcionan de forma similar a los servidores JEE de AEM Forms.

Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables cargados en la aplicación desde un servidor OSGi de AEM Forms. Para adjuntar imágenes o notas de texto, active los archivos adjuntos de nivel de campo en el formulario cuando lo cree. Arrastre y suelte el componente de archivo adjunto desde el explorador de componentes del campo.

Si hay formularios adaptables, puede ver los archivos adjuntos en el documento de registro (DoR). Consulte, [Generar un documento de registro para formularios adaptables que no sean XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
