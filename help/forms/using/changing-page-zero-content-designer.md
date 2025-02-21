---
title: Cambiar el contenido de la página cero en Designer
description: ¿Sabe cómo puede cambiar el mensaje que se muestra en la página cero de un PDF XFA cuando se visualiza en un visor que no es Adobe PDF?
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 100%

---

# Cambiar el contenido de la página cero en Designer {#changing-page-zero-content-in-designer}

El contenido de la página cero se muestra de forma predeterminada cuando un visor que no es Adobe PDF, como el visor de PDF predeterminado de [!DNL Chrome] o [!DNL Firefox], no puede leer el contenido del formulario PDF/XFA. A continuación, se muestra el mensaje predeterminado de la página cero.

![defaultpage0message](assets/defaultpage0message.png)

La versión de Designer de [!DNL AEM Forms] permite cambiar el mensaje que se muestra en la página cero. Para cambiar el mensaje de la página cero, realice los siguientes pasos:

1. Asegúrese de que ha instalado la versión de Designer de [!DNL AEM Forms]. Puede comprobar la versión desde la pantalla Acerca de Designer.

1. Abra el formulario para el cual desea cambiar el contenido de la página cero.

1. Haga clic en **[!UICONTROL Archivo]** > **[!UICONTROL Propiedades del formulario]**.

1. En el cuadro de diálogo [!UICONTROL Propiedades del formulario], haga clic en ![plus](assets/plus.png) (icono + ) para añadir una propiedad personalizada.

1. Especifique **_pagezerocontent** como el nombre de la propiedad.
1. Agregue el nuevo mensaje de la página cero en formato de texto enriquecido como valor. Por ejemplo:


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader.</p></body>`

1. Guarde el formulario como PDF.

1. Vea el formulario PDF en el explorador para confirmar que el mensaje se ha actualizado. El valor del ejemplo anterior aparece de la siguiente forma:

   ![change.message](assets/changedmessage.png)

>[!NOTE]
>
>Es posible que la propiedad personalizada que has creado no aparezca correctamente en el cuadro de diálogo Propiedades del formulario cuando vuelvas a abrir el formulario. Sin embargo, funciona bien, y el formulario muestra el mensaje de la página cero actualizado.
