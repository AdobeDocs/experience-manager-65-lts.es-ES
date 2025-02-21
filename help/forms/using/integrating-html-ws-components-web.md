---
title: Integración de componentes de AEM Forms Workspace en aplicaciones web
description: Aprenda a reutilizar los componentes de AEM Forms Workspace en sus propias aplicaciones web para utilizar la funcionalidad y proporcionar una integración más estrecha.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 94%

---

# Integración de componentes de AEM Forms Workspace en aplicaciones web {#integrating-aem-forms-workspace-components-in-web-applications}

Puede utilizar los [componentes](/help/forms/using/description-reusable-components.md) de AEM Forms Workspace en su propia aplicación web. La siguiente implementación de ejemplo utiliza componentes de un paquete dev de AEM Forms Workspace instalado en una instancia CRX™ para crear una aplicación web. Personalice la siguiente solución para adaptarla a sus necesidades específicas. La implementación de ejemplo reutiliza los componentes `UserInfo`, `FilterList` y `TaskList` en un portal web.

1. Inicie sesión en el entorno de CRXDE Lite en `https://'[server]:[port]'/lc/crx/de/`. Asegúrese de tener instalado el paquete dev de AEM Forms Workspace.
1. Cree una ruta `/apps/sampleApplication/wscomponents`.
1. Copie css, imágenes, js/libs, js/runtime y js/registry.js

   * de `/libs/ws`
   * a `/apps/sampleApplication/wscomponents`.

1. Cree un archivo demomain.js en la carpeta /apps/sampleApplication/wscomponents/js. Copie el código de /libs/ws/js/main.js en demomain.js.
1. En demomain.js, elimine el código para inicializar Router y agregue el siguiente código:

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Cree un nodo en /content con el nombre `sampleApplication` y el tipo `nt:unstructured`. En las propiedades de este nodo, agregue `sling:resourceType` de tipo Cadena y valor `sampleApplication`. En la Lista de control de acceso de este nodo, agregue una entrada para `PERM_WORKSPACE_USER` para permitir privilegios jcr:read. Además, en la Lista de control de acceso de `/apps/sampleApplication`, agregar una entrada para `PERM_WORKSPACE_USER` para permitir privilegios jcr:read.
1. En `/apps/sampleApplication/wscomponents/js/registry.js`, actualice las rutas de `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` para los valores de plantilla.
1. En el archivo JSP de la página de inicio del portal, añada el siguiente código en `/apps/sampleApplication/GET.jsp` para incluir los componentes necesarios en el portal.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Incluya también los archivos CSS necesarios para los componentes de AEM Forms Workspace.

   >[!NOTE]
   >
   >Cada componente se añade a la etiqueta del componente (con la clase gcomponent) durante el procesamiento. Asegúrese de que la página de inicio contenga estas etiquetas. Consulte el archivo `html.jsp` de AEM Forms Workspace para obtener más información sobre estas etiquetas de control base.

1. Para personalizar los componentes, puede ampliar las vistas existentes para el componente requerido de la siguiente forma:

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Modifique el portal CSS para configurar el diseño, la posición y el estilo de los componentes necesarios en el portal. Por ejemplo, imagine que desea utilizar el color negro como color de fondo en el portal para ver bien el componente userInfo. Para ello, cambie el color de fondo en `/apps/sampleApplication/wscomponents/css/style.css` de la siguiente forma:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
