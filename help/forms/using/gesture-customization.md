---
title: Personalizar gestos
description: Aprenda a personalizar los gestos en la aplicación AEM Forms. Puede personalizar los gestos para proporcionar un método distinto de interactuar con la aplicación.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: d89005b3-8478-4b74-b28b-200c121eea3a
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
source-git-commit: 711891ad88f25baaedffb46ec9441c120af3eed4
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 70%
---
# Personalizar gestos {#gesture-customization}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Puede personalizar los gestos de la aplicación AEM Forms para proporcionar un método distinto de interactuar con la aplicación. Por ejemplo, puede añadir nuevos gestos para abrir o cerrar una tarea o un punto de inicio.

## Personalizar los gestos en la aplicación AEM Forms {#to-customize-gestures-in-aem-forms-app}

En la aplicación AEM Forms, el gesto de deslizar el dedo hacia la izquierda abre una nueva tarea o un punto de inicio, mientras que el gesto de deslizar el dado hacia la derecha no realiza ninguna acción. En el siguiente ejemplo se proporcionan los pasos para abrir una nueva tarea o un punto de inicio deslizando el dedo hacia la derecha en la aplicación AEM Forms.

1. Abra su proyecto.

   * Si utiliza un dispositivo iOS, abra `Capture.xcodeproj` en Xcode.
   * Si utiliza un dispositivo Android, abra el proyecto de Android en Eclipse.
   * Si utiliza un dispositivo Windows, abra `MWSWindows.sln` en Visual Studio.

1. Vaya a la carpeta views y abra el archivo `task.js` para editarlo.

   * En Xcode, vaya a la carpeta **Capture > www > wsmobile > js > runtime > views**.
   * En Eclipse, vaya a la carpeta **assets > www > wsmobile > js > runtime > views**.
   * En Visual Studio, vaya a la carpeta **MWSWindows > www > wsmobile > js > runtime > views**.

>[!NOTE]
>
>El archivo task.js contiene la vista de Backbone asociada a todas las tareas o puntos de inicio que aparecen en las listas de tareas o puntos de inicio.

1. Busque la propiedad events de la vista en el archivo `task.js`.

   La propiedad events es un mapa que contiene todas las entradas con el formato:

   `"EventName Selector": "Function"`

   Cuando se almacena en déclencheur un evento de JavaScript denominado `EventName` en un elemento HTML especificado por `Selector`, se llama al `Function`.

1. Busque

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   y reemplácelo por

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Guarde y cierre el archivo `task.js`.
1. Genere y ejecute la aplicación AEM Forms. Ahora puede realizar la acción Abrir deslizando el dedo a la izquierda y a la derecha.

Del mismo modo, puede realizar cambios en otras vistas para utilizar diversas combinaciones de gestos, elementos HTML y funciones.
