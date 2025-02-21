---
title: Configurar el entorno para la aplicación de AEM Forms
description: Hardware, software y licencias para crear e implementar la aplicación de AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 51%

---

# Configurar el entorno para la aplicación de AEM Forms{#set-up-environment-for-aem-forms-app}

Para crear e implementar la aplicación de AEM Forms necesita el hardware, el software y las licencias siguientes:

## Para dispositivos Windows {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools para Apache Cordova

## Para dispositivos iOS {#for-ios-devices}

* Apple Mac basado en Intel con macOS X 10.9.5 o superior
* iOS SDK 8.4 o superior
* Versión de Xcode: Xcode 6.4 para OS X o superior
* Pertenencia al programa iOS Developer Enterprise
* Certificado empresarial para la distribución de aplicaciones internas de iOS 
* Apple iPad con iOS 8.4 o posterior

## Para dispositivos Android™ {#for-android-devices}

* Android™ Development Toolkit (paquete ADT) que se puede descargar de [https://developer.android.com/studio](https://developer.android.com/studio)
* Si el entorno está configurado en un sistema Mac, el ADT debe instalarse en la carpeta Aplicaciones.
* Si el ADT está instalado en cualquier otra ubicación de Mac o si el entorno está configurado en un sistema Windows, la ruta de acceso del ADT SDK debe actualizarse en el archivo `local.properties`. Este archivo está disponible en la carpeta `src\android` del archivo de origen extraído `mobileworkspace-src.zip`. En este archivo, señale la variable `sdk.dir` a la ubicación del SDK de ADT en su escritorio.

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip contiene PhoneGap SDK 5.0. Asegúrese de que el SDK de PhoneGap no esté preinstalado.
