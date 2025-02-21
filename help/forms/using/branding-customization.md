---
title: Personalizar la promoción de la marca
description: Personalice el icono y el nombre de la aplicación, las imágenes de inicio y la página de inicio de sesión para proporcionar a la aplicación de AEM Forms un aspecto diferente y específico de la organización.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 97%

---

# Personalizar la promoción de la marca {#branding-customization}

Puede personalizar el icono y el nombre de la aplicación, las imágenes de inicio y la página de inicio de sesión para proporcionar a la aplicación de AEM Forms un aspecto específico de la organización. Por ejemplo, puede cambiar las imágenes para usar logotipos de su organización. La aplicación de AEM Forms admite las siguientes personalizaciones:

* Personalizar el icono de la aplicación y las imágenes de inicio
* Personalizar el nombre de la aplicación
* Personalizar imágenes en la página de inicio de sesión
* Personalizar el logotipo en el menú de la aplicación

## Personalizar imágenes de icono e inicio {#customizing-icon-and-launch-images}

Siga estos pasos para personalizar el icono predeterminado de la aplicación y la imagen de inicio de la aplicación de AEM Forms:

>[!NOTE]
>
>Para todos los iconos e imágenes, utilice un formato PNG no entrelazado.

### Personalizar iconos e imágenes de lanzamiento {#to-customize-icon-and-launch-images}

#### Para iOS {#for-ios}

1. Abra el proyecto `Capture.xcodeproj` en Xcode.
1. (***Para personalizar el icono***) En la vista del explorador de Capture, navegue hasta **[!UICONTROL Capture > Capture > Archivos compatibles > Capture-info.plist]**. Haga clic en la lista desplegable junto a los archivos de icono. Especifique el nombre del archivo de icono (.png) y cargue el archivo en **[!UICONTROL Capture > Capture > Recursos > Iconos]**. Las dimensiones admitidas actualmente son: 29 x 29, 50 x 50, 58 x 58, 72 x 72, 100 x 100 y 144 x 144.
1. (***Para personalizar imágenes de lanzamiento***) Asegúrese de que los nombres de archivo de las imágenes sean:

   * Para vertical: `Default-Portrait~ipad.png` y `Default-Portrait@2x~ipad.png`
   * Para horizontal: `Default-Landscape~ipad.png` y `Default-Landscape@2x~ipad.png`

   Cargue los archivos en el proyecto de Capture para reemplazar los archivos existentes en el proyecto.

   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coincidan con la imagen que reemplaza en el proyecto.

1. Cree y ejecute la aplicación de AEM Forms en el dispositivo o el simulador de iOS.

#### Para Android {#for-android}

1. Asigne un nombre a los archivos de icono de la aplicación como:

   `ic_launcher.png`

1. Coloque los archivos de icono correspondientes en los siguientes directorios:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coincidan con la imagen que reemplaza en el proyecto.

1. Vuelva a compilar la aplicación de AEM Forms.

### Para Windows {#for-windows}

1. Reemplace los iconos en la ruta:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Reemplace la imagen del lanzador en la ruta:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Asegúrese de que el nombre y la resolución de la imagen coincidan con la imagen que reemplaza en el proyecto.

1. Vuelva a compilar la aplicación de AEM Forms.

## Personalizar el nombre de la aplicación {#customize-the-app-name}

### Para iOS {#for-ios-1}

1. Abra el proyecto `Capture.xcodeproj` en Xcode.
1. En la vista del explorador de Capture, navegue hasta **[!UICONTROL Capture > Capture > Archivos compatibles > InfoPlist.strings]**.

   Actualice el valor del atributo `CFBundleDisplayName` al nombre que desee para la aplicación.

1. Cree y ejecute la aplicación de AEM Forms en el dispositivo o el simulador de iOS.

   Para obtener más información sobre crear la aplicación para iOS, consulte [Configurar el proyecto Xcode y compilar la aplicación fr iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Para Android {#for-android-1}

1. Abra el siguiente XML en cualquier editor de texto o XML:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Actualice el valor de la clave `app_name`.
1. Vuelva a compilar la aplicación de AEM Forms.

   Para obtener más información sobre la creación de la aplicación para Android, consulte [Configurar el proyecto Eclipse y crear la aplicación de Android.](/help/forms/using/setup-eclipse-project-build-installer.md).

### Para Windows {#for-windows-1}

1. Abra el siguiente XML en cualquier editor de texto:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Actualice el valor en la etiqueta `<name>...</name>`.
1. Vuelva a compilar la aplicación de AEM Forms.

   Para obtener más información sobre la creación de la aplicación para Windows, consulte [Configurar el proyecto de Visual Studio y crear la aplicación de Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalizar imágenes en la página de inicio de sesión {#customizing-images-on-the-login-page}

La página de inicio de sesión de la aplicación de AEM Forms tiene un logotipo y unas imágenes de fondo. El logotipo se encuentra encima del cuadro de diálogo de inicio de sesión y la imagen de fondo se encuentra debajo del cuadro de diálogo de inicio de sesión. Siga estos pasos para personalizar la imagen predeterminada en la página de inicio de sesión:

**Antes de comenzar**

Asegúrese de que tiene las siguientes imágenes:

<table>
 <tbody>
  <tr>
   <th><p>Descripción</p> </th>
   <th><p>Tamaño</p> </th>
   <th><p>Nombre de archivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 píxeles</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Imagen de fondo (vertical)</p> </td>
   <td><p>1280 x 989 píxeles</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Para personalizar imágenes en la página de inicio de sesión mediante Xcode**

1. Abra el proyecto `Capture.xcodeproj` en Xcode.

1. Navegue hasta la carpeta `www/wsmobile/images`.
1. Para cambiar el logotipo, sustituya el archivo `LC-logo.png` por el archivo personalizado `LC-logo.png`.
1. Para cambiar el fondo, reemplace el archivo predeterminado `Landing_bg.jpeg` por el archivo personalizado `Landing_bg.jpeg`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo o el simulador de iOS.

### Para personalizar imágenes en las páginas de inicio de sesión con Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Abra el proyecto de Android en Eclipse.

1. Navegue hasta la carpeta `assets/www/wsmobile/images`.
1. Para cambiar el logotipo, sustituya el archivo `LC-logo.png` por el archivo personalizado `LC-logo.png`.
1. Para cambiar el fondo, reemplace el archivo predeterminado `Landing_bg.jpeg` por el archivo personalizado `Landing_bg.jpeg`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Android.

### Para personalizar imágenes en las páginas de inicio de sesión mediante Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Abra el `MWSWindows.sln` en Visual Studio.

1. Navegue hasta la carpeta `MWSWindows\www\wsmobile\images`.
1. Para cambiar el logotipo, sustituya el archivo `LC-logo.png` por el archivo personalizado `LC-logo.png`.
1. Para cambiar el fondo, reemplace el archivo predeterminado `Landing_bg.jpeg` por el archivo personalizado `Landing_bg.jpeg`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Windows.

## Personalizar el logotipo en el menú de la aplicación {#customizing_images_on_the_login_page-1}

Después de iniciar sesión en la aplicación de AEM Forms y seleccionar el botón de menú, puede ver el logotipo encima del menú. Siga estos pasos para personalizar el logotipo predeterminado:

**Antes de comenzar**

Asegúrese de que tiene la siguiente imagen:

<table>
 <tbody>
  <tr>
   <th><p>Descripción</p> </th>
   <th><p>Tamaño</p> </th>
   <th><p>Nombre de archivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 píxeles</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Para personalizar imágenes en la página de inicio de sesión mediante Xcode**

1. Abra el proyecto `Capture.xcodeproj` en Xcode.

1. Navegue hasta la carpeta `www/wsmobile/images`.
1. Para cambiar el logotipo, sustituya el archivo predeterminado `aem_icon.png` por el archivo personalizado `aem_icon.png`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo o el simulador de iOS.

### Para personalizar imágenes en las páginas de inicio de sesión con Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Abra el proyecto de Android en Eclipse.

1. Navegue hasta la carpeta `assets/www/wsmobile/images`.
1. Para cambiar el logotipo, sustituya el archivo predeterminado `aem_icon.png` por el archivo personalizado `aem_icon.png`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Android.

### Para personalizar imágenes en las páginas de inicio de sesión mediante Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Abra el `MWSWindows.sln` en Visual Studio.

1. Navegue hasta la carpeta `MWSWindows\www\wsmobile\images`.
1. Para cambiar el logotipo, sustituya el archivo predeterminado `aem_icon.png` por el archivo personalizado `aem_icon.png`.
1. Cree y ejecute la aplicación de AEM Forms en el dispositivo Windows.
