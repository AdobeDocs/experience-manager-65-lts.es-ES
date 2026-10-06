---
title: Sincronizar la aplicación
description: Sincronizar la aplicación de AEM Forms en su dispositivo móvil con el servidor de AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: c1c4ab9c-7950-41f8-a493-11e11ebcaa95
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
source-wordcount: '431'
ht-degree: 68%
---
# Sincronizar la aplicación{#synchronizing-the-app}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

## Sincronizar la aplicación {#synchronizing-the-app-1}

Los formularios de su aplicación se descargan del servidor de AEM Forms. Los formularios se descargan en las pestañas Tareas y Formularios. Los borradores creados a partir de los formularios se descargan en la pestaña de borradores y los borradores creados a partir de las tareas se descargan en la pestaña de tareas. Para un formulario independiente en el servidor OSGi, los formularios y borradores se descargan en las pestañas Formularios y Borrador respectivamente.

Cuando completa y envía un formulario, este se vuelve a cargar en el servidor de AEM Forms al instante si la aplicación está en línea. Los formularios se recuperan del servidor cuando la aplicación se sincroniza. Sin embargo, los borradores se sincronizan con el servidor instantáneamente si la aplicación está en línea.

Cuando está en línea con el servidor de AEM Forms, de forma predeterminada, la aplicación se sincroniza cada 15 minutos. Con todo, tiene la opción de cambiar la frecuencia de sincronización. Como alternativa, puede sincronizar manualmente la aplicación en cualquier momento.

**Para sincronizar la aplicación manualmente**

Seleccione el botón Sincronizar ![sync-app](assets/sync-app.png) en la esquina inferior derecha de la pantalla principal.

**Para modificar la frecuencia de sincronización**

1. Para ir a la pantalla Configuración, selecciona el botón de menú en la esquina superior izquierda de la pantalla Inicio y, a continuación, selecciona **Configuración**.
1. En la pantalla Configuración, seleccione la pestaña General.

   ![Configuración de frecuencia de sincronización en la ventana Configuración general](assets/gen-settings-2.png)

1. En la opción Frecuencia de sincronización, seleccione el valor a la derecha de Frecuencia de sincronización.
1. En la lista desplegable, seleccione la nueva frecuencia de sincronización.

### Especificaciones técnicas {#technical-specifications}

* La lógica principal del envío de datos de aplicaciones sin conexión al servidor de AEM Forms se incluye en runtime/offline/util/offline.js.
* En el .js, la llamada a processOfflineSubmittedSavedTasks(...) función, envía las tareas guardadas/enviadas al servidor. También controla cualquier error o conflicto en el proceso de sincronización. Si falla el envío de una tarea, la tarea en la aplicación se marca como fallida. Además, la tarea permanece en su Bandeja de salida.
* Las funciones syncSubmittedTask() y syncSavedTask() realizan operaciones en tareas individuales.
* La llamada a la función processOfflineSubmittedSavedTasks() se inicia mediante el componente de lista de tareas después de que un usuario selecciona sincronizar el estado sin conexión con el servidor o una sincronización automática por el hilo en segundo plano.
