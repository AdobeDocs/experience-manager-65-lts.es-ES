---
title: Configurar una solución de Administración de correspondencia
description: Aprenda a configurar una solución de Administración de correspondencia en un entorno de AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: da668935-9d16-49e1-8e7a-772fc4040c1d
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 84%
---
# Configurar una solución de Administración de correspondencia {#configuring-a-correspondence-management-solution}

## Definir la URL de instancia de autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Siga los siguientes pasos para definir un URL de instancia de autor para la restaurar la versión de la instancia de autor:

1. Vaya a *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Inicie sesión con las credenciales de usuario de la consola de administración OSGi. Las credenciales predeterminadas son admin/admin.
1. Busque y haga clic en el icono **[!UICONTROL Editar]** junto a la configuración **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**.
1. En el campo **[!UICONTROL URL del autor de VersionRestoreManager]** especifique la dirección URL de la instancia de autor de VersionRestoreManager.

   **Cadena de URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Si hay varias instancias de autor (agrupadas) delante de un equilibrador de carga, especifique la URL del equilibrador de carga en el campo **[!UICONTROL URL del autor de VersionRestoreManager]**.

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
