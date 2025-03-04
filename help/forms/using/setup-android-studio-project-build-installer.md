---
title: Configurar el proyecto Android&trade; studio y crear la aplicación Android&trade;
description: Pasos para configurar el proyecto Android&trade; Studio y crear el instalador para la aplicación Adobe Experience Manager (AEM) Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 65%

---

# Configurar el proyecto de Android™ Studio y crear la aplicación de Android™ {#set-up-the-android-studio-project-and-build-the-android-app}

Este artículo se utiliza para generar la aplicación de AEM Forms 6.3.1.1 y versiones posteriores. Para crear una aplicación a partir del código fuente de la aplicación AEM Forms 6.3, consulta [Configurar el proyecto Eclipse y crear la aplicación Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms proporciona el código fuente completo de la aplicación de AEM Forms. La fuente contiene todos los componentes para crear una aplicación de AEM Forms personalizada. El archivo del código fuente, `adobe-lc-mobileworkspace-src-<version>.zip` forma parte del paquete `adobe-aemfd-forms-app-src-pkg-<version>.zip` en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenido extraído de la fuente comprimida de Android™](assets/mws-content-1.png)

La siguiente imagen muestra la estructura de directorio de la carpeta `android` en la carpeta `src`.

![Estructura de directorio de la carpeta android en src](assets/android-folder.png)

## Generar aplicación de AEM Forms estándar {#set-up-the-xcode-project}

1. Siga los siguientes pasos para configurar un proyecto en Android™ Studio y proporcionar una identidad de firma:

   Inicie sesión en un equipo que tenga instalado y configurado Android™ Studio.

1. Copie el archivo descargado `adobe-lc-mobileworkspace-src-<version>.zip` en:

   **Para usuarios de Mac**: `[User_Home]/Projects`

   **Para usuarios de Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Para Windows®, se recomienda mantener el proyecto Android™ en la unidad del sistema.

1. Extraiga el archivo en el siguiente directorio:

   **Para usuarios de Mac**: `[User_Home]/Projects/[your-project]`

   **Para usuarios de Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Se recomienda mantener el proyecto de Android extraído en la unidad del sistema antes de importar el proyecto a Android™ Studio.

1. Inicie Android™ Studio.

   **Para usuarios de Mac**: Actualice el archivo `local.properties` presente en la carpeta `[User_Home]/Projects/[your-project]/android` y señale la variable `sdk.dir` a la ubicación `SDK` de su escritorio.

   **Para usuarios de Windows®**: actualice el archivo `local.properties` presente en la carpeta `%HOMEPATH%\Projects\[your-project]\android` y señale la variable `sdk.dir` a la `SDK` ubicación de su escritorio.

1. Haga clic en **[!UICONTROL Finalizar]** para generar el proyecto.

   El proyecto está disponible en el explorador de proyectos de ADT.

   ![proyecto Eclipse después de crear la aplicación](assets/eclipsebuildmws.png)

1. En Android™ Studio, seleccione **[!UICONTROL Importar Proyecto (Eclipse ADT, Gradle, etc.)]**.
1. En el explorador del proyecto, seleccione el directorio raíz del proyecto que desea crear en el cuadro de texto **Directorio raíz**:

   **Para usuarios Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **Para usuarios Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Una vez importado el proyecto, aparecerá una ventana emergente con la opción de actualizar el complemento Android™ Gradle. Haga clic en el botón correspondiente según sus necesidades.

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. Después de generar correctamente gradle, aparecerá la siguiente pantalla. Conecte el dispositivo o emulador apropiado con el sistema y haga clic en **[!UICONTROL Ejecutar Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio muestra los dispositivos conectados y los emuladores disponibles. Seleccione el dispositivo en el que desea ejecutar la aplicación y, a continuación, haga clic en **Aceptar**.

   ![connecteddevice](assets/connecteddevice.png)

Una vez creado el proyecto, puede elegir instalar la aplicación mediante Android™ Debug Bridge o Android™ Studio.

### Usar el puente de depuración de Android™ {#andriod-debug-bridge}

Puede instalar la aplicación en un dispositivo Android™ mediante [Android™ Debug Bridge](https://developer.android.com/tools/adb) con el siguiente comando:

**Para usuarios de Mac**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuarios de Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
