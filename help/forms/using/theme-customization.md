---
title: Personalizar temáticas
description: Aprenda a personalizar la temática de la aplicación de AEM Forms. Puede personalizar el código HTML y el archivo CSS para proporcionar una apariencia y un funcionamiento específicos de la organización.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 5765b456-c6e8-4498-ade0-b36c95aadd71
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2b710c6ef8d291a42b4a7658bf84f5e764422d5c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 72%
---
# Personalizar temáticas {#theme-customization}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Puede personalizar el código HTML y el archivo CSS para ofrecer a la aplicación AEM Forms una apariencia específica de la organización. Por ejemplo, puede cambiar el color de fondo y la altura de las tareas o puntos de inicio. El ejemplo siguiente indica las instrucciones para cambiar:

* Las instrucciones de visualización en lugar de la descripción.
* Número de rutas de visualización.
* Color de degradado de fondo.

## Etapas {#steps}

1. Abra su proyecto.

   * Si utiliza un dispositivo iOS, abra `Capture.xcodeproj` en Xcode.
   * Si utiliza un dispositivo Android, abra el proyecto de Android en Eclipse.
   * Si utiliza un dispositivo Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta de plantillas.

   * En Xcode, vaya a la carpeta **Captura > www > wsmobile > js > runtime > plantillas**.
   * En Eclipse, vaya a la carpeta **Recursos > www > wsmobile > js > runtime > plantillas**.
   * En Visual Studio, vaya a la carpeta **MWSWindows > www > wsmobile > js > runtime > plantillas**.

1. Abra el archivo `template.html` para editarlo.
1. Localice la siguiente cadena:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sustitúyala por `<%`.

1. Localice el código siguiente en el archivo `template.html`:

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Comente la siguiente línea y guarde el archivo.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Vaya a la carpeta css.

   * En Xcode, vaya a **Captura > www > wsmobile > css**.
   * En Eclipse, vaya a **recursos > www > wsmobile > css**.
   * En Visual Studio, vaya a **MWSWindows > www > wsmobile > css**.

1. Abra el archivo `_style.css` para editarlo.
1. Para la imagen de fondo, cambie `#323232` a `#fff`.
1. Guarde los cambios y cierre el archivo `_style.css`.
1. Abra la aplicación de AEM Forms.

   La aplicación de AEM Forms ahora muestra instrucciones en lugar de la descripción.
