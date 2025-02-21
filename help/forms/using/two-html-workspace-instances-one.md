---
title: Alojar dos instancias de espacio de trabajo de AEM Forms en un servidor
description: Cómo los administradores de LC pueden personalizar HTML WS para alojar dos instancias en un único servidor accesible mediante distintas URL.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 82%

---

# Alojar dos instancias de espacio de trabajo de AEM Forms en un servidor {#hosting-two-aem-forms-workspace-instances-on-one-server}

La instalación y configuración predeterminadas de AEM Forms permiten que solo haya un espacio de trabajo de AEM Forms disponible en el servidor. Sin embargo, es posible que necesite alojar dos instancias diferentes de AEM Forms Workspace en un único servidor de AEM Forms. Se puede acceder a las dos instancias desde direcciones URL diferentes.

Los administradores de AEM Forms personalizan el espacio de trabajo para crear dos direcciones URL diferentes y hacer que dos espacios de trabajo estén disponibles en el mismo servidor. En este artículo de personalización, puede suponer que se puede acceder a los dos espacios de trabajo en `https://'[server]:[port]'/lc/ws` y `https://'[server]:[port]':/lc/ws2`.

Siga estos pasos para configurar AEM Forms Workspace.

1. Instale el paquete dev de AEM Forms Workspace en su servidor. Consulte el [paquete dev](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) para obtener instrucciones sobre cómo crearlo.
1. Inicie sesión en CRXDE Lite como administrador al obtener acceso a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copie el nodo ws en /content y pegue en /content. Cambie el nombre del nodo a ws2. Haga clic en **[!UICONTROL Guardar todo]**. En las propiedades de este nodo, cambie el valor de `sling:resourceType` a ws2. Haga clic en **[!UICONTROL Guardar todo]**.

1. Copie la carpeta ws de /libs y péguela en /apps. Cambie el nombre de la carpeta a ws2. Haga clic en **[!UICONTROL Guardar todo]**.
1. En `GET.jsp`, en `/apps/ws2`, realice los siguientes cambios en el código. Sustituya lo siguiente

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   con el siguiente código

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. En `registry.js`, en `/apps/ws2/js`, cambie la ruta de las plantillas para hacer referencia a las plantillas en `/apps/ws2/js/runtime/templates`. Reemplace el siguiente código

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   con el siguiente código

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. En `userinfo.js`, en `/apps/ws2/js/runtime/models` y `/apps/ws2/js/runtime/views`, cambie la cadena `/lc/content/ws` a `lc/content/ws2`.

1. En `/apps/ws2/js/runtime/services/service.js`, cambie la ruta en la función `getLocalizationData` para que señale `/lc/apps/ws2/Locale.html`.

1. Para consultar `pdf.html` del nuevo espacio de trabajo, cambie la ruta de `pdf.html` en `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Para consultar `pdf.html` del nuevo espacio de trabajo, cambie las rutas de `pdf.html` y `WsNextAdapter.swf` en `startprocess.html`, `taskdetails.html` y `processinstancehistory.html`, en `/apps/ws2/js/runtime/templates`.

1. Copie la carpeta `/etc/map/ws` y péguela en `/etc/map`. Cambie el nombre de la nueva carpeta a ws2. Haga clic en Guardar todo.

1. En propiedades de `ws2`, cambie el valor de `sling:redirect` a `content/ws2`.

1. Cambie el valor de `sling:match` a `^[^/\||]/[^/\||]/ws2$`.
