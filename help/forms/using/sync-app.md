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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 84%

---

# Sincronizar la aplicación{#synchronizing-the-app}

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
* En el .js, la llamada a la función processOfflineSubmittedSavedTasks(...) envía las tareas guardadas/enviadas al servidor. También controla cualquier error o conflicto en el proceso de sincronización. Si falla el envío de una tarea, la tarea en la aplicación se marca como fallida. Además, la tarea permanece en su Bandeja de salida.
* Las funciones syncSubmittedTask() y syncSavedTask() realizan operaciones en tareas individuales.
* La llamada a la función processOfflineSubmittedSavedTasks() se inicia mediante el componente de lista de tareas después de que un usuario selecciona sincronizar el estado sin conexión con el servidor o una sincronización automática por el hilo en segundo plano.
