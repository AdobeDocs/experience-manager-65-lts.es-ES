---
title: Distribuir la aplicación de AEM Forms
description: Utilice la administración de dispositivos móviles (MDM) para implementar a gran escala aplicaciones en dispositivos móviles.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 51%

---

# Distribuir la aplicación de AEM Forms {#distribute-aem-forms-app}

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
