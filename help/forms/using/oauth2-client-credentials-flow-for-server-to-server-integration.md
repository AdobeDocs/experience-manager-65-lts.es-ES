---
title: Flujo de integración de Salesforce con AEM Forms mediante credenciales de cliente de OAuth 2.0
description: Pasos para integrar la integración de Salesforce con AEM Forms mediante el flujo de credenciales de cliente de OAuth 2.0
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: 887dc1d6d7e11672b62ef5ca5463ea6181ff0320
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 76%

---

# Integración de Salesforce mediante el flujo de credenciales de cliente de OAuth 2.0 {#configure-salesforce-with-ouath-2.0-client-credential}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=es) |
| AEM 6.5 | Este artículo |

Puede utilizar las credenciales de cliente de OAuth 2.0 para integrar AEM Forms con la aplicación Salesforce. Las credenciales de cliente de OAuth 2.0 son un método estándar y seguro para la comunicación directa sin la participación del usuario.

![Flujo de trabajo al establecer la comunicación entre AEM Forms y la aplicación Salesforce](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms intercambia las credenciales del cliente (clave del cliente y secreto de cliente), definidas en la aplicación conectada de Salesforce, para obtener un token de acceso.

El uso de credenciales del cliente OAuth 2.0 para la autenticación a través de la autenticación de flujo de código de autorización ofrece varias ventajas:

* La autenticación de credenciales de cliente de OAuth 2.0 permite más de cinco conexiones por usuario.
* La configuración de la fuente de datos de AEM sigue funcionando en la desactivación, los cambios de acceso y la actualización de la contraseña de un usuario de AEM.

## Requisitos previos {#prerequisites}

Antes de establecer la comunicación entre una aplicación de Salesforce y un entorno de AEM, haga lo siguiente:

* Cree una [Aplicación conectada de Salesforce con flujo de credenciales de cliente de OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) y un único usuario de API para su organización y obtenga la clave y el secreto de consumidor para la aplicación.

* Asegúrese de que el archivo Swagger esté configurado correctamente para que coincida con las API de su organización. También puede optar por [crear un archivo Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=es) desde cero, adaptado para su utilización en el entorno de AEM.
>[!NOTE]
>
> AEM 6.5 solo admite especificaciones de archivo de Swagger 2.0.

+++

## Pasos para configurar Salesforce con el flujo de credenciales del cliente {#steps-to-create-aem-datasource-configuration}

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**.
1. Seleccione la carpeta de configuración.
1. Haga clic en **[!UICONTROL Crear]** y aparece **[!UICONTROL Crear configuración de fuente de datos]**.
1. Especifique el **[!UICONTROL Título]** y seleccione el **[!UICONTROL Tipo de servicio]** como **[!UICONTROL Servicio RESTful]**.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione el **[!UICONTROL Origen de Swagger]** como **[!UICONTROL Archivo].**
   >[!NOTE]
   >
   > En cuanto se selecciona el archivo swagger, el esquema, el nombre del host y la ruta base se rellenan automáticamente.

1. Cargue el archivo Swagger creado desde el equipo local haciendo clic en **[!UICONTROL Examinar]**.
1. Seleccione el **[!UICONTROL Tipo de autenticación]** como **[!UICONTROL OAuth 2.0]** y aparecerá el panel **[!UICONTROL Configuración de autenticación]**.
1. Seleccione **[!UICONTROL Tipo de concesión]** como **[!UICONTROL Credenciales de cliente]**.
1. Especifique el **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** obtenido de la aplicación conectada de Salesforce.
1. Especifique la **[!UICONTROL URL de token de acceso]** con el formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organización tiene su propio nombre de dominio específico.

1. Haga clic en **[!UICONTROL Probar conexión]**.
1. Si la conexión se realiza correctamente, haga clic en el botón **[!UICONTROL Crear]**.

Ahora, puede [crear el modelo de datos de formulario](https://experienceleague.adobe.com/docs/experience-manager-65-2025/forms/form-data-model/create-form-data-models.html?lang=en) para integrar la fuente de datos configurada con su Forms adaptable.
