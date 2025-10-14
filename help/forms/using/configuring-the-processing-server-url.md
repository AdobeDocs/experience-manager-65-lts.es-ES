---
title: Configurar AEM DS
description: Obtenga información sobre cómo especificar la URL del servidor de procesamiento antes de enviar un formulario.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 62%

---

# Configurar AEM DS{#configuring-aem-ds-settings}

Este artículo describe cómo configurar el **Servicio de configuración de AEM DS**. Esta configuración se puede utilizar en varios escenarios, por ejemplo:

* En Administración de correspondencia

   * Para configurar el flujo de trabajo de AEM Forms
   * Al utilizar el portal de Forms para el guardado remoto del borrador/envío

* En formularios adaptables, para casos en los que se envía un formulario adaptable desde una instancia de publicación

A continuación se indican los pasos para establecer la **[!UICONTROL Configuración de AEM DS]**:

1. Abra el Administrador de configuración en la instancia de publicación mediante la URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configuración de la consola web AEM &#x200B;](assets/web_configuration_console_new.png)

1. En la **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]**, busque y haga clic en la opción **[!UICONTROL Configuración de AEM DS]**.

   ![Configuración de DS](assets/ds_settings_new.png)

1. El **[!UICONTROL Servicio de configuración de AEM DS]** muestra los ajustes de configuración comunes de los Componentes de AEM DS.

   ![Servicio de configuración de DS](assets/ds_settings_service_new.png)

1. Agregue la siguiente información en los campos respectivos:

   **[!UICONTROL URL del servidor de procesamiento]**: el servidor de procesamiento es el servidor donde se debe activar el flujo de trabajo de Forms o AEM. Puede ser la misma URL que la de la instancia de autor de AEM o que la otra URL del servidor (es decir, https://localhost:port/).

   **[!UICONTROL Nombre de usuario del servidor de procesamiento]**: nombre de usuario del usuario del flujo de trabajo [en función de la URL del servidor que se utilice]

   **[!UICONTROL Contraseña del servidor de procesamiento]**: contraseña del usuario del flujo de trabajo

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Al utilizar Forms o flujos de trabajo de AEM, antes de realizar cualquier envío desde el servidor de publicación, es necesario configurar el servicio de configuración de DS. De lo contrario, el envío del formulario fallará.
   >    
   >
