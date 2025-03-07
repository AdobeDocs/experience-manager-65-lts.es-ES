---
title: Configurar el conector para Microsoft SharePoint
description: Configure el conector para Microsoft SharePoint para habilitar la comunicación entre los formularios de AEM y Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: d1575576-3a05-496c-b683-bb5badc02711
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 7%

---

# Configurar el conector para Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El conector para Microsoft SharePoint permite la comunicación entre los formularios de AEM y Microsoft SharePoint. Para obtener información adicional, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

1. En la consola de administración, haga clic en Servicios > Conector para Microsoft SharePoint.
1. Especifique la siguiente configuración para el servidor de SharePoint:

   **Nombre de host de SharePoint Server:** El número de puerto del nombre de host de la aplicación web en el servidor de SharePoint, con el formato `[hostname]:'port'`.

   **Nombre de usuario:** Cuenta de usuario utilizada para conectarse al servidor de SharePoint.

   **Contraseña:** Contraseña de la cuenta de usuario utilizada para conectarse al servidor de SharePoint

   **Nombre de dominio:** Dominio donde se encuentra el servidor de SharePoint.

1. Haga clic en Guardar.

## Servicio de configuración de Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

El servicio de configuración de Microsoft SharePoint `(MSSharePointConfigService)` le permite especificar credenciales para el usuario de formularios AEM que tiene permisos de suplantación. Para obtener información acerca de los permisos de suplantación, consulte [Configuración del conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estos pasos para especificar la configuración de `MSSharePointConfigService`:

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. Navegue por la lista de servicios y haga clic en `MSSharePointConfigService`.
1. Especifique las siguientes opciones en la página Configuración:

   * Nombre De Usuario Para Un Usuario Con Permisos De Suplantación
   * Contraseña Del Usuario Anterior

1. Haga clic en Guardar.
