---
title: Trabajar con un formulario
description: Ver y actualizar el formulario asociado a una tarea o punto de inicio en la aplicación de AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 7c9d2407-4255-4d04-a413-edf428b7564b
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
source-wordcount: '471'
ht-degree: 76%
---
# Trabajar con un formulario {#working-with-a-form}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Si un formulario está habilitado para la sincronización en la aplicación de Forms, este se descarga y puede trabajar con él directamente.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo, ejecuta una empresa bancaria y un cliente rellena una solicitud en su sitio. La solicitud es un formulario adaptable que acepta información de sus clientes y la almacena para revisarla. El administrador revisa el formulario y crea un formulario de verificación en la instancia de autor de AEM. El administrador habilita la sincronización del formulario con la aplicación de AEM Forms. Si el formulario de verificación está disponible en la aplicación de AEM Forms, su agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. Su agente de campo puede visitar a su cliente, comprobar los detalles, guardar datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor cada vez que la aplicación está en línea.

Para sincronizar su formulario en la aplicación de AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en **Ver propiedades**.
1. En la página Propiedades, haga clic en **Avanzadas**.
1. En Avanzadas, habilita la opción: **Sincronizar con la aplicación de AEM Forms** y selecciona **Guardar**.

Para sincronizar varios formularios, en la instancia de autor, selecciona varios formularios en el administrador de formularios y selecciona **Sincronizar con la aplicación de AEM Forms**. Cuando se publica el formulario, la aplicación de AEM Forms puede conectarse al servidor de publicación y recuperar los formularios.

Si su aplicación AFA Android (aplicación de AEM Forms) no se puede sincronizar, realice los siguientes pasos para solucionar el problema de sincronización:

1. Vaya a **https://[server]:[port]/system/console/configMgr**.
1. Busque el **[!UICONTROL Controlador de autenticación de token de Adobe Granite]** y haga clic en **[!UICONTROL Editar]**.
1. Seleccione la opción **[!UICONTROL Ninguno]** en el menú desplegable del atributo **[!UICONTROL Atributo SameSite para la cookie del token de inicio de sesión]**.
1. Haga clic en **[!UICONTROL Guardar]**.

![Sincronizar imagen con la aplicación de AFA Android](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Formularios admitidos:
>
>* Formularios adaptables (sin carga diferida)
>* Mobile Forms
>
>Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables recuperados en la aplicación de AEM Forms sincronizados con el servidor OSGi de AEM Forms. Los usuarios pueden adjuntar archivos en un campo si el autor ha habilitado los archivos adjuntos de nivel de campo en el momento de crear el formulario.


**Para abrir y actualizar un formulario**

1. Para abrir un formulario, selecciona **[!UICONTROL Formulario]** en la pantalla de inicio.
1. Puede actualizar los campos del formulario, agregar archivos adjuntos, guardar como borrador y enviarlo.
