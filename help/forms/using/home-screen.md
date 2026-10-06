---
title: Pantalla principal
description: Descripción de los componentes de la pantalla Inicio de la aplicación AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: b8e413e0-1387-46c7-891a-85d5fc61288b
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
source-wordcount: '397'
ht-degree: 44%
---
# Pantalla principal{#home-screen}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Al iniciar sesión en la aplicación AEM Forms, se le redirige a la pantalla Inicio.

## Pantalla Inicio predeterminada {#default-home-screen}

De forma predeterminada, la pantalla Inicio muestra todos los formularios, incluidos los puntos de inicio y las tareas (si el servidor conectado está habilitado para AEM Forms Workflow), junto con las miniaturas asociadas. Puede especificar las miniaturas en AEM Forms Server.

La siguiente figura muestra anotaciones con llamadas a los componentes esenciales en la pantalla Inicio predeterminada.

![Pantalla Inicio de la aplicación Forms](assets/home-screen-1.png)

<!--
Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)
-->

1. **Botón de menú**: selecciona el botón **Menú** para ir a Tareas, Forms, Bandeja de salida y Configuración. Si la aplicación AEM Forms está conectada a un servidor de AEM Forms JEE, puede ver la opción Tareas. La opción Tareas también almacena los borradores creados a partir de las tareas de un proceso. En los servidores OSGi de AEM Forms, la opción Tareas está oculta. La Bandeja de salida almacena los formularios y los borradores guardados antes de sincronizarse con el servidor. Todos los formularios y borradores guardados en la Bandeja de salida se cargan en el servidor de AEM Forms cuando la aplicación está [sincronizada con el servidor](../../forms/using/sync-app.md). Para obtener información sobre la configuración, consulte [Actualización de la configuración general](../../forms/using/update-general-settings.md).
1. **Tarea o formulario**: seleccione la tarea o el formulario de la lista con los que desea trabajar.
1. **Puntos suspensivos horizontales**: indican que hay acciones disponibles en el formulario. Al pulsar los puntos suspensivos, se muestran las acciones y la descripción que ha proporcionado el autor. Las opciones **Eliminar borrador** y **Completar** están visibles al seleccionar los puntos suspensivos.
1. **Icono de actualización**: Seleccione el icono de actualización para sincronizar su aplicación con el servidor de AEM Forms.

### Personalización de la pantalla Inicio {#customizing-the-home-screen}

![Configuración general](assets/gen-settings.png)

Puede cambiar la pantalla Inicio predeterminada de la aplicación desde la **[Configuración general](../../forms/using/update-general-settings.md)** de la aplicación o desde la pestaña **Preferencia** de HTML Workspace.

Los cambios realizados en la configuración de la pantalla Inicio de la aplicación afectan a la pantalla Inicio del usuario que ha iniciado sesión o del usuario que utiliza el dispositivo móvil actual.

Sin embargo, los cambios realizados en HTML Workspace afectan a todos los usuarios de la aplicación de AEM Forms que han iniciado sesión en el servidor de AEM Forms.
