---
title: Cambiar la fuente en la interfaz
description: Cómo cambiar las fuentes en la interfaz de usuario de forma selectiva.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 100%

---

# Cambiar la fuente en la interfaz{#changing-the-font-on-the-interface}

Puede cambiar la fuente que se muestra en AEM Forms Workspace. Las fuentes utilizadas en una sección específica de la interfaz de usuario se definen en la sección correspondiente de la hoja de estilo. Puede cambiar las fuentes de la interfaz de usuario de forma selectiva.

Siga los [Pasos genéricos para personalizar AEM Forms Workspace](../../forms/using/generic-steps-html-workspace-customization.md) y según sus necesidades, siga los pasos para personalizar CSS, HTML o ambos.

1. Cambie o agregue la familia de fuentes en un estilo existente.
1. Cambie o agregue la familia de fuentes en línea para el elemento HTML.
1. Agregue un estilo y utilícelo para el elemento HTML.

Por ejemplo, para cambiar la fuente del texto de anclaje de la barra de navegación superior a Courier New, siga los siguientes pasos:

1. Inicie sesión en CRXDE Lite accediendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Realice una de las siguientes acciones:

   1. Para cambiar la familia de fuentes en un estilo existente, agregue lo siguiente en el archivo newStyle.css en /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Para agregar la familia de fuentes en línea para el elemento HTML, copie el archivo `/libs/ws/js/runtime/templates/appnavigation.html` en `/apps/ws/js/runtime/templates/appnavigation.html`.

      Actualice el archivo /apps/ws/js/runtime/templates/appnavigation.html de la siguiente manera:

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Abra el archivo /apps/ws/js/registry.js para editarlo y reemplace `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` con `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Para agregar un estilo que defina la familia de fuentes, agregue lo siguiente en el archivo newStyle.css en /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Para agregar la familia de fuentes en línea para el elemento HTML, agregue lo siguiente en el archivo appnavigation.html en /apps/ws/js/runtime/templates.

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Vuelva a iniciar el espacio de trabajo y borre la memoria caché del explorador para que los cambios sean visibles.

![change_font_before](assets/change_font_before.png)

Barra de navegación superior antes de personalizar la fuente

![change_font_after](assets/change_font_after.png)

Barra de navegación superior después de personalizar la fuente de la primera pestaña
