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
exl-id: e99f1cbd-492e-4cc2-9975-8f17c885dd8c
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '142'
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
