---
title: Configurar el proyecto de Visual Studio y crear la aplicación de Windows
description: Obtenga información sobre cómo configurar un proyecto de Visual Studio para generar la aplicación de AEM Forms para dispositivos móviles Windows.
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 95%

---

# Configurar el proyecto de Visual Studio y crear la aplicación de Windows{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms proporciona el código fuente completo de la aplicación de AEM Forms. El origen contiene todos los componentes para generar una aplicación de espacio de trabajo personalizada. El archivo del código fuente, `adobe-lc-mobileworkspace-src-<version>.zip` forma parte del paquete `adobe-aemfd-forms-app-src-pkg-<version>.zip` en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para descargar el archivo del código fuente, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` en su explorador.\
   El paquete de fuente se descargará en el dispositivo.

La siguiente imagen muestra el contenido extraído del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

La siguiente imagen muestra la estructura de directorio de la carpeta `windows` en la carpeta `src`.

![win-dir](assets/win-dir.png)

## Configurar el entorno {#setting-up-the-environment}

Para dispositivos Windows, necesita:

* Microsoft Windows 8.1 o Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools para Apache Cordova

## Configurar el proyecto de Visual Studio para la aplicación de AEM Forms {#setting-up-visual-studio-project-for-aem-forms-app}

Siga estos pasos para configurar el proyecto de aplicación de AEM Forms en Visual Studio.

1. Copie el archivo `adobe-lc-mobileworkspace-src-<version>.zip` en la carpeta `%HOMEPATH%\Projects` en el dispositivo Windows 8.1 o Windows 10 con Visual Studio 2015 instalado y configurado.
1. Extraiga el archivo en el directorio `%HOMEPATH%\Projects\MobileWorkspace`.
1. Navegue hasta el directorio `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`
1. Abra el archivo `CordovaApp.sln` con Visual Studio 2015 y continúe con la generación de la aplicación de AEM Forms.

## Generar aplicación de AEM Forms {#build-aem-forms-app}

Siga estos pasos para crear e implementar la aplicación de AEM Forms.

>[!NOTE]
>
>Los datos almacenados en el sistema de archivos de Windows para la aplicación de AEM Forms no están cifrados. Se recomienda usar una herramienta de terceros como el Cifrado de unidad BitLocker de Windows para cifrar datos del disco.

1. En la barra de herramientas de Visual Studio Standard, seleccione **Versión** de la lista desplegable del modo de generación.

1. Seleccione Windows-AnyCPU, Windows-x64 o Windows-x86 según su plataforma. Se recomienda Windows-AnyCPU.
1. En el explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto **CordovaApp.Windows** y seleccione **Almacenar > Crear paquetes de aplicaciones**.

   ![createapppackages](assets/createapppackages.png)

   Aparecerá el asistente Crear paquetes de aplicaciones.

   El archivo del instalador CordovaApp.Windows_3.0.2.0_anycpu.appx se creará en el directorio platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test.

   Si aparece el error `Retarget to windows 8.1 required`, haga clic con el botón derecho en el error y, en el menú emergente, seleccione **Redestinar A Windows 8.1**.

   ![retarget-solution](assets/retarget-solution.png)

1. En el asistente Crear paquetes de aplicaciones, seleccione si desea o no cargar la aplicación en el almacén de Windows y, a continuación, haga clic en **Siguiente**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. Realice los cambios necesarios en los parámetros, como la versión y la ubicación de salida de la generación de la aplicación.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. Una vez creado el proyecto, puede instalar la aplicación mediante lo siguiente:

   * Windows PowerShell
   * Visual Studio

   El paquete `.appx` requiere que los siguientes elementos se instalen correctamente:

   1. Biblioteca WinJS
   1. Asegúrese de que el paquete incluye un certificado autofirmado o un certificado público firmado por una autoridad de confianza, como VeriSign.
   1. Licencia para desarrolladores

   El directorio Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test contiene los cuatro componentes principales:

   1. El archivo `.appx` 
   1. El certificado (actualmente es un certificado firmado automátiamente por Apache Cordova)
   1. La carpeta de dependencias
   1. El archivo PowerShell (extensión .ps1)

## Implementar una aplicación mediante Windows PowerShell {#deploying-an-app-using-windows-powershell}

Existen dos maneras de instalar la aplicación en un dispositivo Windows.

### Al adquirir la licencia de desarrollador {#by-acquiring-the-developer-license}

1. Haga clic con el botón secundario en el archivo de PowerShell ( `Add-AppDevPackage.ps1)` y elija **Ejecutar con PowerShell**.

1. La configuración le solicitará una licencia para desarrolladores. Utilice las credenciales de la cuenta de Microsoft para adquirir una licencia de desarrollador.\
   Esta licencia es válida durante 30 días y puede renovarla gratis.
1. Cuando adquiere la licencia de desarrollador, el programa de instalación instala el certificado firmado automáticamente en el sistema y la aplicación se instalará correctamente.

### Mediante dispositivos de propiedad empresarial {#by-using-enterprise-owned-devices}

Para los dispositivos de propiedad empresarial unidos al dominio de la empresa, no es necesario adquirir una licencia de desarrollador.

Los dispositivos de propiedad empresarial utilizan las ediciones Professional y Enterprise de Windows.

Microsoft recomienda instalar un certificado público emitido por una autoridad de confianza, como VeriSign.

Para implementar la aplicación, haga lo siguiente:

* Asegúrese de que el dispositivo esté unido al dominio de la empresa.
* Habilite la configuración de la directiva de grupo.

**Para habilitar la configuración de la directiva de grupo, haga lo siguiente:**

1. En el dispositivo, ejecute `gpedit.msc`.
1. Navegue hasta **Configuración del equipo > Plantillas administrativas > Componente de Windows > Implementar el paquete de aplicaciones**.
1. Haga clic con el botón derecho en **Permitir que todas las aplicaciones de confianza instalen**.
1. Haga clic en **Editar** y seleccione **Habilitado**.

1. Haga clic en **Aceptar**.

Edite el script de PowerShell generado por Visual Studio para evitar que adquiera una licencia de desarrollador.

En el script de PowerShell, establezca la variable: `$NeedDeveloperLicense = $false`.

Para los dispositivos que no están unidos al dominio, se requiere una clave de activación de producto de carga secundaria. Puede comprarlo a un distribuidor de Windows.

Para Windows 8.1 Home Edition, no hay directiva de grupo, no se permite la carga secundaria de empresa y no se puede unir con el dominio de empresa. Implemente la aplicación en un dispositivo Windows 8.1 Home Edition con licencia de desarrollador.

Para obtener más información, haga clic [aquí](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Implementar una aplicación mediante Visual Studio {#deploying-an-app-using-visual-studio}

Para instalar la aplicación en Windows mediante Visual Studio, haga lo siguiente:

1. Conecte el dispositivo con el depurador remoto.\
   Para obtener más información, consulte [Ejecutar aplicaciones de Windows Store en un equipo remoto](https://docs.microsoft.com/es-es/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Con la aplicación abierta en Visual Studio, elija Windows-x64, Windows-x86 o Windows-AnyCPU en la lista de Plataformas de solución y seleccione **Equipo remoto**.
1. La aplicación se implementará en el equipo remoto.
