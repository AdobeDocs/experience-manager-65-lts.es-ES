---
title: Trabajar en modo sin conexión
description: Desconecte el dispositivo móvil fuera del intervalo de red de AEM Forms o en modo completamente sin conexión y trabaje en la aplicación de AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 100%

---

# Trabajar en modo sin conexión {#working-in-the-offline-mode}

El modo sin conexión de la aplicación de AEM Forms le permite trabajar sin problemas aunque la aplicación esté sin conexión. Puede abrir, actualizar y enviar un formulario sin necesidad de conectividad de red.

Empiece a trabajar en la aplicación de AEM Forms sincronizando la aplicación con el servidor de AEM Forms. Todos los formularios asignados a usted se descargan en la aplicación. Para AEM Forms en JEE, las tareas se recuperan en la pestaña tareas y los puntos de inicio se recuperan en los formularios asociados y otros formularios en la pestaña Formularios. Para AEM Forms en OSGi, solo se cargan formularios en la pestaña Formularios.

Para obtener más información sobre cómo sincronizar la aplicación, consulte [Sincronizar la aplicación](/help/forms/using/sync-app.md).

## Disponibilidad de Forms sin conexión {#making-forms-available-offline}

Al sincronizar la aplicación con el servidor de AEM Forms, los formularios se descargan en el dispositivo móvil. Sin embargo, de forma predeterminada, los archivos adjuntos asociados al formulario no se descargan. Esto implica que si está en línea, puede ver los archivos adjuntos. Sin embargo, para asegurarse de que puede ver los archivos adjuntos en el modo sin conexión, cambie la configuración predeterminada en su aplicación.

Para asegurarse de que los archivos adjuntos asociados se descargan con cada formulario, establezca Recuperar archivos adjuntos en Activado. Para obtener más información, consulte [Actualizar la configuración general](/help/forms/using/update-general-settings.md).

Dado que la descarga de datos en el dispositivo móvil puede afectar al rendimiento del dispositivo, de forma predeterminada, la configuración Recuperar archivos adjuntos está Desactivada. Los archivos adjuntos se recuperan en el dispositivo para cualquier tarea que se descargue del servidor después de actualizar la configuración a Activado. En el modo sin conexión, un usuario puede trabajar en todas las tareas que se descarguen en el dispositivo después de establecer la opción **Recuperar archivos adjuntos** en Activado.

## Configurar el servicio sin conexión para la aplicación de AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

El servicio sin conexión de la aplicación de AEM Forms identifica los recursos utilizados en un formulario. La aplicación de AEM Forms se basa en este servicio para obtener información sobre las dependencias del formulario. Se necesita información sobre las dependencias del formulario para habilitar las funcionalidades sin conexión. El servicio sin conexión de la aplicación de AEM Forms almacena en caché las rutas o direcciones URL de los recursos utilizados en un formulario. La caché se actualiza en función de los cambios del formulario y del periodo de validez configurado para el servicio sin conexión. El almacenamiento en caché de rutas o direcciones URL de los recursos utilizados en un formulario mejora el rendimiento del lado del servidor.

Para configurar el componente sin conexión del lado del servidor de la aplicación de AEM Forms:

1. En la instancia de autor, vaya a **Adobe Experience Manager** > **Herramientas** > **Formularios** > **Configurar el servicio sin conexión de la aplicación de Forms**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. En Configuración general, puede realizar lo siguiente:

   * **Borrar caché**: Borra la caché del lado del servidor de las dependencias del formulario.
   * **Restablecer configuración**: Restablece la configuración sin conexión de la aplicación de AEM Forms.
   * **Validez de caché**: Especifica el período de validez de la caché sin conexión del lado del servidor.
   * **Rutas de observación de recursos**: Especifica las rutas en las que el servicio sin conexión monitoriza los cambios de recursos. Si se producen cambios en las rutas especificadas, se actualiza la caché sin conexión de todos los formularios dependientes. Por ejemplo, `/etc/clientlibs/fd,/content/dam/images`.

1. En la pestaña **Caché de recursos manual**, especifique las dependencias del formulario que el servicio sin conexión no puede identificar. Puede especificar recursos, como imágenes cargadas desde JavaScript. La aplicación de AEM Forms también descargará estos recursos para el modo sin conexión.
