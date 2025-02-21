---
title: Crear una aplicación segura de AEM Forms para iOS
description: Obtenga información sobre cómo crear una aplicación segura de AEM Forms para iOS archivando el proyecto Xcode. Esto crea un instalador (un archivo .ipa) y un archivo de lista de propiedades (un archivo .plist).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 87%

---

# Crear una aplicación segura de AEM Forms para iOS {#building-a-secure-aem-forms-app-for-ios}

Debe archivar el proyecto Xcode para la aplicación de AEM Forms para crear el programa de instalación (un archivo .ipa) y un archivo de lista de propiedades (un archivo .plist). El archivo de lista de propiedades contiene información de configuración de la aplicación interna alojada, como el nombre y la ubicación de alojamiento de la aplicación. Para obtener más información sobre el archivo de la lista de propiedades, consulte [Acerca de los archivos de la lista de propiedades de información](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Inicie sesión en el siguiente sitio web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Crear un ID de aplicación. Para ver los pasos detallados para crear un ID de aplicación, consulte [Crear y configurar un ID de aplicación](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Para configurar el identificador del paquete para la aplicación iOS de su aplicación, haga clic en **[!UICONTROL Configurar ID de aplicación]**.
1. En la parte inferior de la página web, seleccione **[!UICONTROL Habilitar para la protección de datos]**. Especifique las opciones de protección de datos.

   Haga clic en **[!UICONTROL Listo]**.

1. Vaya a Aprovisionamiento>Distribución y cree un nuevo perfil con el ID de aplicación configurado en el paso 3.
1. Descargue y agregue el perfil de aprovisionamiento al Xcode y al iPad.
1. Inicie sesión en el equipo Mac que tenga Xcode y iOS SDK instalados y configurados.
1. Abra el proyecto `AEM Forms.xcodeproj` en Xcode.
1. Haga clic en **[!UICONTROL AEM Forms]**, en **[!UICONTROL OBJETIVOS]**, seleccione **[!UICONTROL AEM Forms]**. Seleccione la pestaña **[!UICONTROL Generar configuración]**, busque la sección **[!UICONTROL Derecho de firma de código]** y, en la lista desplegable Derechos, seleccione la opción **[!UICONTROL LC Enterprise]**.
1. Busque y abra el archivo `LC Enterprise.entitlements` en el Xcode para editarlo. En **Derechos XCode**, agregue el mismo par clave-valor que está presente en el perfil de aprovisionamiento.
1. En la pestaña **[!UICONTROL Configurar generación]**, haga clic en **[!UICONTROL Todo]** y haga clic en **[!UICONTROL Combinado]**.
1. En la lista **[!UICONTROL Configuración]**, expanda **[!UICONTROL Firma de código]**.
1. Para **[!UICONTROL Identidad de firma de código]**, seleccione la firma adecuada. Asegúrese de que se ha seleccionado la misma firma para **[!UICONTROL Depurar]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK de iOS]**.
1. En **[!UICONTROL PROYECTO]**, seleccione **[!UICONTROL AEM Forms]** y asegúrese de que la firma adecuada esté seleccionada para **[!UICONTROL Identidad de firma de código]**, **[!UICONTROL Depurar]**, **[!UICONTROL Versión]** y **[!UICONTROL Cualquier SDK de iOS]**.
1. Generar y distribuir la aplicación de AEM Forms. Para obtener instrucciones detalladas sobre la compilación y distribución de la aplicación de AEM Forms, consulte [Crear el programa de instalación de la aplicación de AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
