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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 89%

---

# Personalizar temáticas {#theme-customization}

Puede personalizar el código HTML y el archivo CSS para ofrecer a la aplicación AEM Forms una apariencia específica de la organización. Por ejemplo, puede cambiar el color de fondo y la altura de las tareas o puntos de inicio. El ejemplo siguiente indica las instrucciones para cambiar:

* Las instrucciones de visualización en lugar de la descripción.
* Número de rutas de visualización.
* Color de degradado de fondo.

## Etapas {#steps}

1. Abra su proyecto.

   * Si utiliza un dispositivo iOS, abra `Capture.xcodeproj` en Xcode.
   * Si utiliza un dispositivo Android, abra el proyecto de Android en Eclipse.
   * Para Windows, abra `MWSWindows.sln` en Visual Studio.

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
