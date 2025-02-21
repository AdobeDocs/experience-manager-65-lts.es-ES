---
title: Actualizar el vínculo a la documentación
description: Actualizar el destino del vínculo de ayuda del espacio de trabajo en el espacio de AEM Forms para que señale al vínculo de documentación personalizado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 100%

---

# Actualizar el vínculo a la documentación {#updating-the-link-to-the-documentation}

Puede acceder al contenido de ayuda predeterminado de AEM Forms Workspace al seleccionar **Ayuda > Ayuda del espacio de trabajo**. Señala a la documentación en línea del sitio web de Adobe. Sin embargo, puede actualizarlo para que señale cualquier otra dirección URL.

Tenga en cuenta los siguientes casos de uso en los que puede que desee cambiar la dirección URL de ayuda predeterminada:

* Para proporcionar ayuda localizada en un idioma de su elección.
* Para ofrecer contenido de ayuda personalizado para su espacio de trabajo personalizado.

Para actualizar la URL de la documentación en línea, siga los [Pasos genéricos de personalización](/help/forms/using/generic-steps-html-workspace-customization.md) y luego los siguientes pasos.

1. Copie el archivo `userinfo.html` de `/libs/ws/js/runtime/templates` a `/apps/ws/js/runtime/templates`.
1. Cambiar:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   hasta

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Haga lo siguiente:

   1. Abra /apps/ws/js/registry.js para editarlo.
   1. Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/userinfo.html` con `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
