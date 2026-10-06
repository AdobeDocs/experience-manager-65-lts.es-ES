---
title: Distribuir la aplicación de AEM Forms
description: Utilice la administración de dispositivos móviles (MDM) para implementar a gran escala aplicaciones en dispositivos móviles.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 840dadca-6691-4244-9383-7dbc8e14f0a0
source-git-commit: d8150dc7cb8ec161b875263ecfaaca6424ff629f
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 42%
---
# Distribuir la aplicación de AEM Forms {#distribute-aem-forms-app}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

La administración de dispositivos móviles (MDM) permite implementar a gran escala aplicaciones en dispositivos móviles.

>[!NOTE]
>
>Esta distribución solo es aplicable a dispositivos iOS y Android™.

## Características principales que ofrecen las soluciones de MDM: {#main-features-generally-provided-by-mdm-solutions}

* Habilitar la inscripción de dispositivos en su entorno empresarial
* Permitir la configuración y actualización de la configuración del dispositivo
* Aplicar el cumplimiento de seguridad.
* Acceso móvil seguro a los recursos corporativos

Una solución de MDM junto con la administración de aplicaciones móviles, le permite administrar aplicaciones internas, públicas y compradas en todos los dispositivos móviles de su empresa.

El administrador de MDM puede cargar archivos ipa y apk al servidor de MDM y controlar a los usuarios que pueden acceder a los archivos ipa o apk. El administrador también puede controlar la configuración de perfil que corresponde a cada aplicación.

## Configuración del perfil que afecta a la aplicación de AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

La siguiente configuración del perfil de su dispositivo afecta al funcionamiento de la aplicación AEM Forms en su dispositivo:

* **Permitir el uso de la cámara** en la sección **Funcionalidad del dispositivo**

Si deshabilita **Permitir el uso de la cámara**, la característica de cámara de [Anotación fotográfica](/help/forms/using/add-attachments.md) no funcionará. Active esta opción para utilizar la cámara en la aplicación.

* **Requerir contraseña en el dispositivo** en la sección directivas de contraseñas

Para habilitar el **cifrado de datos de la aplicación**, se recomienda habilitar la **contraseña** en su dispositivo. Si la contraseña no está establecida en el dispositivo, los datos de la aplicación almacenados en el dispositivo no se cifrarán.
