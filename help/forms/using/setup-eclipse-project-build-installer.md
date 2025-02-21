---
title: Crear la aplicación de AEM Forms para Android
description: Pasos para configurar el proyecto de Android Studio y crear el archivo .apk para la aplicación de AEM Forms para Android
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 887dc1d6d7e11672b62ef5ca5463ea6181ff0320
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 81%

---

# Crear la aplicación de AEM Forms para Android {#build-the-aem-forms-android-app}

Para crear la aplicación de Android para AEM Forms, realice los siguientes pasos en la secuencia recomendada.

1. [Descargar el paquete del AEM Forms App Source Code](#download-android-zip)
1. [Configurar las variables de entorno](#set-environment-variable-android)
1. [Creación de una aplicación estándar de AEM Forms](#set-up-the-xcode-project)

## Descargar el paquete del AEM Forms App Source Code {#download-android-zip}

El paquete del AEM Forms App Source Code hace referencia al archivo `adobe-lc-mobileworkspace-src-<version>.zip`. Este archivo incluye el código fuente necesario para crear una aplicación de AEM Forms personalizada. El archivo está incluido en el paquete `adobe-aemfd-forms-app-src-pkg-<version>.zip` disponible en la Distribución de software.

Para descargar el archivo de `adobe-aemfd-forms-app-src-pkg-<version>.zip`, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-2025/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.
1. Para descargar el archivo del código fuente, abra **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** en su explorador. El archivo .zip de la aplicación de Android se descargará en el dispositivo.
1. Extraiga el contenido del archivo .zip a una carpeta de su sistema de archivos local. Por ejemplo, *C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

La siguiente imagen muestra la estructura de la carpeta `adobe-lc-mobileworkspace-src-<version>.zip\android`.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Configurar las variables de entorno {#set-environment-variable-android}

Establezca las siguientes variables de entorno antes de iniciar el proceso de generación para la aplicación de AEM Forms:

* Establezca la variable de entorno JAVA_HOME en la ubicación del software JDK en el sistema de archivos local. Por ejemplo, C:\Program Files\Java\jdk1.8.0_181
* Configure la variable de entorno `ANDROID_SDK_ROOT` del sistema a la ubicación del SDK para Android. Por ejemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Configure la variable de entorno del sistema `Path` para incluir las ubicaciones de carpetas platform-tools y tools para Android. Por ejemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Creación de una aplicación estándar de AEM Forms {#set-up-the-xcode-project}

Después de guardar el archivo adobe-lc-mobileworkspace-src-&lt;version>.zip en el sistema de archivos local y establecer las variables de entorno, cree una aplicación estándar de AEM Forms para Android con cualquiera de las siguientes opciones:

* [Crear una aplicación de AEM Forms con Android Studio](#using-android-studio)
* [Generar archivos .apk con Android Studio](#generate-apk-android-studio)

### Crear una aplicación de AEM Forms con Android Studio {#using-android-studio}

Para crear una aplicación de AEM Forms con Android Studio, realice los siguientes pasos:

1. Inicie la aplicación Android Studio en su equipo.
1. Haga clic en **Abrir un proyecto existente de Android Studio**. Si el cuadro de diálogo para abrir un proyecto existente no aparece automáticamente, seleccione **Archivo** > **Abrir**.
1. Navegue hasta *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* en el sistema de archivos local y haga clic en **Aceptar**.

   La opción **android** se muestra en el panel izquierdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Seleccione **android** en el panel izquierdo y haga clic en **Ejecutar** > **Ejecutar “android”**.
1. Seleccione el dispositivo Android en la sección Dispositivos conectados del cuadro de diálogo Seleccionar destino de implementación y haga clic en Aceptar.

   Una vez que haya creado el entorno de desarrollo correctamente, ahora puede aplicar personalizaciones en la aplicación. Utilice los siguientes artículos para personalizar la aplicación:

   * [Personalizar la promoción de la marca](/help/forms/using/branding-customization.md)
   * [Personalizar temáticas](/help/forms/using/theme-customization.md)
   * [Personalizar gestos](/help/forms/using/gesture-customization.md)

   Después de aplicar las personalizaciones adecuadas a la aplicación, puede generar el archivo .apk para su distribución.

### Generar archivos .apk con Android Studio {#generate-apk-android-studio}

Para generar el archivo .apk con Android Studio, haga lo siguiente:

1. Inicie la aplicación Android Studio en su equipo.
1. Seleccione **Abrir un proyecto existente de Android Studio**. Si el cuadro de diálogo para abrir un proyecto existente no aparece automáticamente, seleccione **Archivo** > **Abrir**.
1. Navegue hasta *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* en el sistema de archivos local y haga clic en **Aceptar**.

   La opción android se muestra en el panel izquierdo.

1. Para generar el archivo .apk, seleccione **Generar** > **Generar APK**.

   De manera opcional, puede seleccionar **Generar** > **Generar APK firmado** para generar una [versión firmada](https://developer.android.com/studio/publish/app-signing) del archivo .apk.

## Usar Android Debug Bridge {#build-android-debug-bridge}

Una vez generado el archivo .apk, ejecute el siguiente comando para instalar la aplicación en un dispositivo Android mediante la función [Android Debug Bridge](https://developer.android.com/tools/adb).

**Usuarios de Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuarios de Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
