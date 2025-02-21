---
title: Configurar una solución de Administración de correspondencia
description: Aprenda a configurar una solución de Administración de correspondencia en un entorno de AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 83%

---

# Configurar una solución de Administración de correspondencia {#configuring-a-correspondence-management-solution}

## Definir la URL de instancia de autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Siga los siguientes pasos para definir un URL de instancia de autor para la restaurar la versión de la instancia de autor:

1. Vaya a *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Inicie sesión con las credenciales de usuario de la consola de administración OSGi. Las credenciales predeterminadas son admin/admin.
1. Busque y haga clic en el icono **[!UICONTROL Editar]** junto a la configuración **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**.
1. En el campo **[!UICONTROL URL de autor de VersionRestoreManager]** especifique la dirección URL de la instancia de autor de VersionRestoreManager.

   **Cadena de URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Si hay varias instancias de autor (agrupadas) delante de un equilibrador de carga, especifique la URL del equilibrador de carga en el campo **[!UICONTROL URL de autor de VersionRestoreManager]**.

1. Haga clic en **[!UICONTROL Guardar]**.

## Definir la URL de instancia de publicación para ActivationManagerImpl (administrador de activación de instancias públicas) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estos pasos para poder definir la URL de instancia de publicación para el administrador de activación de instancias públicas:

1. Vaya a *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Inicie sesión con las credenciales de usuario de la consola de administración OSGi. Las credenciales predeterminadas son admin/admin.
1. Busque y haga clic en el icono **[!UICONTROL Editar]** junto a la configuración **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**.
1. En el campo **[!UICONTROL URL de publicación de ActivationManager]** especifique la URL para acceder a la instancia de publicación ActivationManager. Puede proporcionar las siguientes URL.

   * **URL del equilibrador de carga (recomendado)**: proporcione la URL del equilibrador de carga si tiene un servidor web que actúa como tal frente a la granja de servidores de publicación (varias instancias de publicación no agrupadas).
   * **URL de instancia de publicación**: proporcione cualquier URL de instancia de publicación, si tiene una sola instancia de publicación o el servidor web que enlaza la granja de servidores de publicación no es accesible desde el entorno de creación debido a restricciones. En caso de que la instancia de publicación especificada no funcione, existe un mecanismo de reserva para el autor.
   * **Cadena de URL**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Haga clic en **[!UICONTROL Guardar]**.

Para obtener más información sobre configurar Administración de correspondencia, consulte [Propiedades de configuración de Administración de correspondencia](https://helpx.adobe.com/es/aem-forms/6-2/cm-configuration-properties.html).
