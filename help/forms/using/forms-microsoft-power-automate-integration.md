---
title: Conexión y envío de datos de formularios adaptables a Microsoft&reg; Power Automate
description: Una guía paso a paso para conectar y enviar datos de formulario adaptable a Microsoft&reg; Power Automate.
keywords: Forms Microsoft Power Automate adaptable, enviar datos de Forms adaptables a Microsoft Power Automate
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 85%

---

# Conexión y envío de datos de formulario adaptable a Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

Puede configurar un formulario adaptable para ejecutar un flujo de nube de Microsoft® Power Automate en el envío. El formulario adaptable configurado envía los datos capturados, los archivos adjuntos y el documento de registro al flujo de nube de Power Automate para su procesamiento. Le ayuda a crear una experiencia de captura de datos personalizados mientras aprovecha el poder de Microsoft® Power Automate para crear lógicas empresariales en torno a los datos capturados y automatizar los flujos de trabajo de los clientes. A continuación se muestran algunos ejemplos de lo que puede hacer después de integrar un formulario adaptable con Microsoft® Power Automate:

* Usar datos de formularios adaptables en procesos empresariales de Power Automate
* Utilice Power Automate para enviar datos capturados a más de 500 fuentes de datos o a cualquier API disponible públicamente
* Realizar cálculos complejos en los datos capturados
* Guardar datos de formularios adaptables en sistemas de almacenamiento con una programación predefinida

El editor de formularios adaptables ofrece la acción de envío **Invocar un flujo de Microsoft® Power Automate** para enviar una acción y enviar datos de formularios adaptables, archivos adjuntos y documentos de registro a flujos de nube de Power Automate. Para usar la acción Enviar para enviar los datos capturados a Microsoft® Power Automate, [Conecte la instancia de autor de AEM Forms con Microsoft® Power Automate] (#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)

## Requisitos previos

Para conectar un formulario adaptable con Microsoft® Power Automate, es necesario lo siguiente:

* Licencia de Microsoft® Power Automate Premium
* Flujo de Microsoft® [Power Automate](https://docs.microsoft.com/es-es/power-automate/create-flow-solution) con el déclencheur `When an HTTP request is received` para aceptar los datos de envío del formulario adaptable
* Un usuario de Experience Manager con privilegios de [autor de formularios](/help/forms/using/forms-groups-privileges-tasks.md) y [administrador de formularios](/help/forms/using/forms-groups-privileges-tasks.md)
* La cuenta utilizada para conectarse a Microsoft® Power Automate es la propietaria del flujo de Power Automate configurada para recibir datos del formulario adaptable


## Conecte su instancia de AEM Forms con Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Realice las siguientes acciones para conectar la instancia de autor de AEM Forms con Microsoft® Power Automate:

1. [Crear un Microsoft](#ms-power-automate-application)
1. [Crear Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Crear Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publicar Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Crear una aplicación de Microsoft® Azure Active Directory {#ms-power-automate-application}

1. Iniciar sesión en [Azure Portal](https://portal.azure.com/).
1. Seleccione [!UICONTROL Azure Active Directory] en el panel de navegación izquierdo.
1. En la página de directorio predeterminada, seleccione [!UICONTROL Registros de aplicaciones] en el panel izquierdo.
1. En la página Registros de aplicaciones, haga clic en Nuevos registros.
1. Especifique el nombre, tipos de cuenta compatibles y URI de redireccionamiento en la página. En el URI de redireccionamiento, especifique lo siguiente y haga clic en Guardar.
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrar una aplicación de Azure Active Directory](assets/power-automate-application.png)

   >[!NOTE]
   >También puede especificar los URI de redireccionamiento adicionales, si es necesario, desde la página Autenticación.
   > Para los tipos de cuenta compatibles, seleccione un inquilino o varios o una cuenta personal de Microsoft®, según su caso de uso


1. En la página Autenticación, habilite las siguientes opciones y haga clic en Guardar.


   * Tokens de acceso (utilizados para flujos implícitos)
   * Tokens de ID (utilizados para flujos implícitos e híbridos)

1. En la página Permisos de API, haga clic en Añadir un permiso.
1. En las API de Microsoft®, seleccione el servicio de flujo y los siguientes permisos.
   * Flows.Manage.All
   * Flows.Read.All

   Haga clic en Añadir permisos para guardar los permisos.
1. En la página Permisos de API, haga clic en Añadir un permiso. Seleccione las API que utiliza mi organización y busque `DataVerse`.
1. Habilite user_impersonation y haga clic en Añadir permisos.
1. (Opcional) En la página Certificados y secretos, haga clic en Nuevo secreto de cliente. En la pantalla Añadir un secreto de cliente, aporte una descripción y un período de tiempo para que el secreto caduque y haga clic en Añadir. Se genera una cadena secreta.
1. Tenga en cuenta la [URL del entorno de Dynamics](https://docs.microsoft.com/es-es/power-automate/web-api#compose-http-requests) específica de su organización.

### Crear la configuración de nube de Microsoft® Power Automate Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.
1. En la página **[!UICONTROL Explorador de configuración]**, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y seleccione **[!UICONTROL Crear]**. Crea un contenedor de configuración para almacenar servicios en la nube. Asegúrese de que el nombre de la carpeta no contenga ningún espacio.
1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** y abra el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Cuando cree un formulario adaptable, especifique el nombre del contenedor en el campo **[!UICONTROL Contenedor de configuración]**.

1. En la página de configuración, seleccione **[!UICONTROL Crear]** para crear una configuración de [!DNL Microsoft®® Power Automate Flow Service] en AEM Forms.
1. En la página **[!UICONTROL Configurar el servicio Dataverse para Microsoft® Power Automate]**, especifique el **[!UICONTROL ID del cliente]** (también denominado ID de aplicación), el **[!UICONTROL secreto del cliente]**, la **[!UICONTROL URL de OAuth]** y la **[!UICONTROL URL del entorno de Dynamics]**. Utilice el ID del cliente, el secreto del cliente, la URL de OAuth y la URL del entorno de Dynamics de la [Aplicación de Microsoft® Azure Active Directory](#ms-power-automate-application) creada en la sección anterior. Utilice la opción Puntos finales en la interfaz de usuario de la aplicación de Microsoft® Azure Active Directory para encontrar la URL de OAuth

   ![Utilice la opción de puntos finales en la IU de la aplicación de Microsoft Power Automate para encontrar la URL de OAuth](assets/endpoints.png)

1. Seleccione **[!UICONTROL Conectar]**. Si se le solicita, inicie sesión en su cuenta de Microsoft® Azure. Seleccione **[!UICONTROL Guardar]**.

### Crear la configuración de nube de Microsoft® Power Automate Flow Service. {#create-microsoft-power-automate-flow-cloud-configuration}

1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Flow Service]** y abra el contenedor de configuración que creó en la sección anterior.

   >[!NOTE]
   >
   >Cuando cree un formulario adaptable, especifique el nombre del contenedor en el campo **[!UICONTROL Contenedor de configuración]**.
1. En la página de configuración, seleccione **[!UICONTROL Crear]** para crear una configuración de [!DNL Microsoft®® Power Automate Flow Service] en AEM Forms.
1. En la página **[!UICONTROL Configurar Dataverse para Microsoft® Power Automate]**, especifique el **[!UICONTROL ID del cliente]** (también denominado ID de aplicación), el **[!UICONTROL Secreto del cliente]**, la **[!UICONTROL URL de OAuth]** y la **[!UICONTROL URL del entorno de Dynamics]**. Utilice el ID del cliente, el secreto del cliente, la URL de OAuth y el ID del entorno de Dynamics. Utilice la opción Puntos finales en la interfaz de usuario de la aplicación de Microsoft® Azure Active Directory para encontrar la URL de OAuth. Abra el vínculo [Mis flujos](https://us.flow.microsoft.com) y seleccione Mis flujos para usar el ID indicado en la URL como ID del entorno de Dynamics.
1. Seleccione **[!UICONTROL Conectar]**. Si se le solicita, inicie sesión en su cuenta de Microsoft® Azure. Seleccione **[!UICONTROL Guardar]**.

### Publicar las configuraciones de nube de Microsoft® Power Automate Dataverse y Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** y abra el contenedor de configuración que creó en la sección anterior [Crear la configuración de la nube de Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration).
1. Seleccione la configuración de `dataverse` y seleccione **[!UICONTROL Publicar]**.
1. En la página Publicar, seleccione **[!UICONTROL Todas las configuraciones]** y seleccione **[!UICONTROL Publicar]**. Publicar las configuraciones de nube de Power Automate Dataverse y Power Automate Flow Service.

La instancia de autor de AEM Forms ahora está conectada con Microsoft® Power Automate. Ahora puede enviar datos de formularios adaptables a un flujo de Power Automate.

## Utilizar la acción de envío Invocar un flujo de Microsoft® Power Automate para enviar datos a un flujo de Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Después de [conectar la instancia de autor de AEM Forms con Microsoft® Power Automate](#connect-forms-server-with-power-automate), realice la siguiente acción para configurar el formulario adaptable y enviar los datos capturados a un flujo de Microsoft® al enviar el formulario.

1. Inicie sesión en la instancia de autor, seleccione su formulario adaptable y haga clic en **[!UICONTROL Propiedades]**.
1. En el contenedor de configuración, examine y seleccione el contenedor creado en la sección [Crear la configuración de nube de Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration) y seleccione **[!UICONTROL Guardar y cerrar]**.
1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En el contenedor de propiedades, para **[!UICONTROL Acciones de envío]**, seleccione la opción **[!UICONTROL Invocar un flujo de Power Automate]**. Hay una lista de flujos de Power Automate disponibles en la opción **[!UICONTROL Flujo de Power Automate]**. Seleccione el flujo necesario y los datos de formularios adaptables se envían en el momento del envío.

   ![Configurar la acción de envío](assets/submission.png)

>[!NOTE]
>
> Antes de enviar el formulario adaptable, asegúrese de que se añada el activador `When an HTTP Request is received` con el esquema JSON a continuación a su flujo de Power Automate.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

## Consulte también lo siguiente:

* [Crear un formulario adaptable](create-an-adaptive-form-core-components.md)
* [Configurar la acción de envío](configuring-submit-actions.md)
* [Conector de Adobe Experience Manager para Microsoft® Power Automate](https://learn.microsoft.com/es-es/connectors/adobeexperiencemanag/)
