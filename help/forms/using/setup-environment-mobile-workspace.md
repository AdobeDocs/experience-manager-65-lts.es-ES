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
exl-id: 41799183-ef5a-4990-bd7b-7b58cafe3960
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2b710c6ef8d291a42b4a7658bf84f5e764422d5c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 35%
---
# Configurar el entorno para la aplicación de AEM Forms{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

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
>adobe-lc-mobileworkspace-src.zip contiene PhoneGap SDK 5.0. Asegúrese de que PhoneGap SDK no esté preinstalado.
