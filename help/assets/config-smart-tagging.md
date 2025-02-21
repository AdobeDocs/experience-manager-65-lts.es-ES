---
title: Configuración del etiquetado de recursos mediante el servicio de contenido inteligente
description: Aprenda a configurar el etiquetado inteligente y el etiquetado inteligente mejorado en  [!DNL Adobe Experience Manager] mediante el servicio de contenido inteligente.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 17%

---

# Preparar [!DNL Assets] para el etiquetado inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de empezar a etiquetar recursos usando Smart Content Services, integre [!DNL Experience Manager Assets] con Adobe Developer Console para usar el servicio inteligente de [!DNL Adobe Sensei]. Una vez configurado, entrene el servicio con algunas imágenes y una etiqueta.

<!--
>[!NOTE]
>
>* Smart Content Services is no longer available to new [!DNL Experience Manager Assets] On-Premise customers. Existing On-Premise customers, who already have this capability enabled, can continue using Smart Content Services.
>* Smart Content Services is available for existing [!DNL Experience Manager Assets] Managed Services customers, who already have this capability enabled.
>* New Experience Manager Assets Managed Services customers can follow the instructions mentioned in this article to set up Smart Content Services.
>* For Service Pack 20 and older, you need to perform the workaround steps for SCS to support Oauth integration. See [Troubleshooting smart tags for OAuth credentials](config-oauth.md).
>* To support the Oauth integration on Service Pack 21, you need to install the [Hotfix for SP 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip). 
>* For Existing SCS configuration, the process is the same as setting up a new OAuth integration. Any legacy configuration will be automatically cleaned up.
-->

Antes de usar el servicio de contenido inteligente, asegúrese de lo siguiente:

* [Integrar con Adobe Developer Console](#integrate-adobe-io).
* [Entrenar el servicio de contenido inteligente](#training-the-smart-content-service).

* Instale el [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es) más reciente.

## Actualización de SCS para admitir Oauth para Adobe Managed Services {#scs-upgrade-oauth-managed-services}

**Nuevos usuarios**

Instale el paquete de servicio 21. Para admitir la integración de Oauth en el Service Pack 21, debe instalar [Revisión para el Service Pack 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip).

Siga las instrucciones mencionadas en este artículo para configurar Smart Content Services.

**Usuarios existentes**

Si ha actualizado a Service Pack 21, instale la revisión [para SP 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip) para admitir la integración con Oauth. Cualquier configuración existente se elimina automáticamente. Siga las instrucciones mencionadas en este artículo para configurar Smart Content Services.

Para Service Pack 20 y versiones anteriores, debe realizar los pasos de la solución para que SCS admita la integración con Oauth. Consulte [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](config-oauth.md).

## Actualización de SCS para admitir Oauth para usuarios On-Premise {#scs-upgrade-oauth-on-premise}

**Nuevos usuarios**

Smart Content Services ya no está disponible para los nuevos usuarios locales de [!DNL Experience Manager Assets].

**Usuarios existentes**

Los usuarios locales existentes, que ya tienen esta capacidad habilitada, pueden seguir utilizando Smart Content Services.

Si ha actualizado a Service Pack 21, instale la revisión [para SP 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip) para admitir la integración con Oauth. Cualquier configuración existente se elimina automáticamente. Siga las instrucciones mencionadas en este artículo para configurar Smart Content Services.

Para Service Pack 20 y versiones anteriores, debe realizar los pasos de la solución para que SCS admita la integración con Oauth. Consulte [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](config-oauth.md).


## Integración con Adobe Developer Console {#integrate-adobe-io}

Al integrarse con Adobe Developer Console, el servidor [!DNL Experience Manager] autentica las credenciales del servicio con la puerta de enlace de Adobe Developer Console antes de reenviar la solicitud al servicio de contenido inteligente. Para integrarse, necesita una cuenta de Adobe ID que tenga privilegios de administrador para la organización y la licencia de Smart Content Service comprada y habilitada para su organización.

Para configurar el servicio de contenido inteligente, siga estos pasos de nivel superior:

1. Cree una integración en [Adobe Developer Console](#create-adobe-io-integration).

1. Cree [la configuración de la cuenta técnica de IMS](#create-ims-account-config) mediante la clave de API y otras credenciales de Adobe Developer Console.

1. [Configurar el servicio de contenido inteligente](#configure-smart-content-service).

1. [Compruebe la configuración](#validate-the-configuration).

<!--
To configure the Smart Content Service, follow these top-level steps:

1. To generate a public key, [Create a Smart Content Service] (#obtain-public-certificate) configuration in [!DNL Experience Manager]. 

1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

   <!--1. [Obtain public certificate](#obtain-public-certificate) for OAuth integration.
   1. [Create an integration in Adobe Developer Console](#create-adobe-i-o-integration) and upload the generated public key.

   1. [Configure your deployment](#configure-smart-content-service) using the API key and other credentials from Adobe Developer Console.

   1. [Test the configuration](#validate-the-configuration).-->

### Creación de la integración con Adobe Developer Console {#create-adobe-io-integration}

Para usar las API del servicio de contenido inteligente, cree una integración en Adobe Developer Console para obtener [!UICONTROL clave de API] (generada en el campo [!UICONTROL ID de cliente] de la integración de Adobe Developer Console), [!UICONTROL ID de organización] y [!UICONTROL SECRETO DE CLIENTE] para la [!UICONTROL configuración del servicio de etiquetado inteligente de Assets] de la configuración en la nube en [!DNL Experience Manager].

1. Acceda a [https://developer.adobe.com](https://developer.adobe.com/) en un explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea **administrador** del sistema.

1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.

1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y **[!UICONTROL Contenido inteligente]**. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione **[!UICONTROL OAuth Server-to-Server]**. Haga clic en **[!UICONTROL Siguiente]**.
Para obtener más información sobre cómo realizar esta configuración, consulte la documentación de Developer Console, según sus necesidades:

   * Información general:
      * [Autenticación de servidor a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

   * Creación de una nueva credencial de OAuth:
      * [Guía de implementación de credenciales de servidor a servidor de OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

   * Migración de una credencial JWT existente a una credencial de OAuth:
      * [Migración de una credencial de cuenta de servicio (JWT) a una credencial de servidor a servidor de OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)


1. En la página **[!UICONTROL Seleccionar perfiles de producto]**, seleccione **[!UICONTROL Servicios de contenido inteligente]**. Haga clic en **[!UICONTROL Guardar API configurada]**.

   La página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y agregar estos valores en [!UICONTROL Configuración del servicio de etiquetado inteligente de Assets] de la configuración de la nube en [!DNL Experience Manager] para configurar las etiquetas inteligentes.

   ![Credencial de OAuth en Developer Console](assets/ims-configuration-developer-console.png)

### Crear la configuración de cuenta técnica de IMS {#create-ims-account-config}

Debe crear la configuración de cuenta técnica de IMS siguiendo los pasos a continuación:

1. En la [!DNL Experience Manager] interfaz de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. Haga clic en **[!UICONTROL Crear]**.

1. En el cuadro de diálogo Configuración de cuenta técnica de IMS, utilice los siguientes valores:

   ![Ventana de configuración de Adobe IMS](assets/adobe-ims-config.png)

   | Campo | Descripción |
   | -------- | ---------------------------- |
   | Solución en la nube | Elija **[!UICONTROL Etiquetas inteligentes]** en la lista desplegable. |
   | Título | Añada el título de la cuenta de IMS que configura. |
   | Servidor de autorización | Agregar `https://ims-na1.adobelogin.com` |
   | ID del cliente | Se proporcionará a través de [Adobe Developer console](https://developer.adobe.com/console/). |
   | Secreto de cliente | Se proporcionará a través de [Adobe Developer console](https://developer.adobe.com/console/). |
   | Ámbito | Se proporcionará a través de [Adobe Developer console](https://developer.adobe.com/console/). |
   | ID de organización | Se proporcionará a través de [Adobe Developer console](https://developer.adobe.com/console/). |

1. Seleccione la configuración que ha creado y haga clic en **[!UICONTROL Comprobar estado]**.

1. Confirme el cuadro de diálogo Comprobar estado y haga clic en Cerrar cuando la configuración esté en buen estado.

### Crear una nueva configuración {#configure-smart-content-service}

<!--
>[!CAUTION]
>
>Previously, configurations that were made with JWT Credentials are now subject to deprecation in the Adobe Developer Console. You cannot create new JWT credentials after June 3, 2024. Such configurations can no longer be created or updated, but can be migrated to OAuth configurations.
> See [Setting up IMS integrations for AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>See [Steps to configure OAuth for on-premise users](#config-oauth-onprem)
> See [Troubleshooting smart tags for OAuth credentials](#config-smart-tagging.md)
-->

Para configurar la integración, use los valores de los campos [!UICONTROL ID. DE CUENTA TÉCNICA], [!UICONTROL ID. DE ORGANIZACIÓN], [!UICONTROL SECRETO DE CLIENTE] e [!UICONTROL ID. DE CLIENTE] de la integración de Adobe Developer Console. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la implementación de [!DNL Experience Manager].

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Etiqueta inteligente]** para abrir las [!UICONTROL Configuraciones de etiquetas inteligentes].

1. Haga clic en **[!UICONTROL Crear]** para crear una nueva configuración. De lo contrario, haga clic en **[!UICONTROL Propiedades]** para actualizar la configuración existente.

1. Rellene los campos siguientes:

   ![Configuración de etiquetas inteligentes](assets/smart-tags-config.png)

   | Campo | Descripción |
   | -------- | ---------------------------- |
   | Título | Añada el título de la cuenta de IMS que configura. |
   | Configuración de Adobe IMS asociada | Elija la configuración en la lista desplegable. |
   | URL del servicio | `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`. Por ejemplo, `https://smartcontent.adobe.io/apac`. Puede especificar `na`, `emea` o `apac` como las regiones en las que está alojada la instancia de autor de Experience Manager. |

   >[!NOTE]
   >
   >Si el servicio administrado de Experience Manager se aprovisiona antes del 1 de septiembre de 2022, utilice la siguiente URL de servicio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

### Validar la configuración {#validate-the-configuration}

Una vez completada la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Obtenga acceso a su servidor [!DNL Experience Manager] en `https://[aem_server]:[port]`.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal] > [!UICONTROL JMX]**.

<!--
1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.-->

1. Haga clic en `com.day.cq.dam.similaritysearch.internal.impl (SCS)`.

   ![Ventana Mbean](assets/mbean.png)

1. Haga clic en `validateConfigs()`. En el diálogo **[!UICONTROL Validar configuraciones]**, haga clic en **[!UICONTROL Invocar]**.

Los resultados de validación se muestran en el mismo cuadro de diálogo.

<!--
### Obtain public certificate by creating Smart Content Service configuration {#obtain-public-certificate}

A public certificate lets you authenticate your profile on Adobe Developer Console.

1. In the [!DNL Experience Manager] user interface, access **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. In the **[!UICONTROL Create Configuration]** dialog, specify a title and name for the Smart Tags configuration. Click **[!UICONTROL Create]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the following values:

   **[!UICONTROL Service URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   For example, `https://smartcontent.adobe.io/apac`. You can specify `na`, `emea`, or, `apac` as the regions where your Experience Manager author instance is hosted. 

   >[!NOTE]
   >
   >If the Experience Manager Managed Service is provisioned before September 01, 2022, use the following Service URL:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Authorization Server]**: `https://ims-na1.adobelogin.com`

   Leave the other fields blank for now (to be provided later). Click **[!UICONTROL OK]**.

   ![Experience Manager Smart Content Service dialog to provide content service URL](assets/aem_scs.png)


   *Figure: Smart Content Service dialog to provide content service URL*

   >[!NOTE]
   >
   >The URL provided as [!UICONTROL Service URL] is not accessible via browser and generates a 404 error. The configuration works OK with the same value of the [!UICONTROL Service URL] parameter. For the overall service status and maintenance schedule, see [https://status.adobe.com](https://status.adobe.com).

1. Click **[!UICONTROL Download Public Certificate for OAuth Integration]**, and download the public certificate file `AEM-SmartTags.crt`.

   ![A representation of the settings created for the smart tagging service](assets/smart-tags-download-public-cert.png)


   *Figure: Settings for smart tagging service.*

#### Reconfigure when a certificate expires {#certrenew}

After a certificate expires, it is no longer trusted. You cannot renew an expired certificate. To add a certificate, follow these steps.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Click **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Locate and click **[!UICONTROL dam-update-service]** user. Click **[!UICONTROL Keystore]** tab.

1. Delete the existing **[!UICONTROL similaritysearch]** keystore with the expired certificate. Click **[!UICONTROL Save & Close]**.

   ![Delete the existing similarity search entry in Keystore to add a security certificate](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figure: Delete the existing `similaritysearch` entry in Keystore to add a security certificate.*

1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Click **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Click the required configuration.  

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Access [https://console.adobe.io](https://console.adobe.io) and navigate to the existing Smart Content Services on the **[!UICONTROL Integrations]** page. Upload the new certificate. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### Create Adobe Developer Console integration {#create-adobe-i-o-integration}

To use Smart Content Service APIs, create an integration in Adobe Developer Console to obtain [!UICONTROL API Key] (generated in [!UICONTROL CLIENT ID] field of Adobe Developer Console integration), [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], and [!UICONTROL CLIENT SECRET] for [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager].

1. Access [https://console.adobe.io](https://console.adobe.io/) in a browser. Select the appropriate account and verify that the associated organization role is system administrator.

1. Create a project with any desired name. Click **[!UICONTROL Add API]**.

1. On the **[!UICONTROL Add an API]** page, select **[!UICONTROL Experience Cloud]** and select **[!UICONTROL Smart Content]**. Click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Upload your public key]**. Provide the certificate file downloaded from [!DNL Experience Manager]. A message [!UICONTROL Public key(s) uploaded successfully] is displayed. Click **[!UICONTROL Next]**.

   [!UICONTROL Create a new Service Account (JWT) credential] page displays the public key for the service account.

1. Click **[!UICONTROL Next]**.

1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*

### Configure Smart Content Service {#configure-smart-content-service}

>[!CAUTION]
>
>Previously, configurations that were made with JWT Credentials are now subject to deprecation in the Adobe Developer Console. You cannot create new JWT credentials after June 3, 2024. Such configurations can no longer be created or updated, but can be migrated to OAuth configurations.
> See [Setting up IMS integrations for AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>See [Steps to configure OAuth for on-premise users](#config-oauth-onprem)
> See [Troubleshooting smart tags for OAuth credentials](#config-smart-tagging.md)

To configure the integration, use the values of [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], [!UICONTROL CLIENT SECRET], and [!UICONTROL CLIENT ID] fields from the Adobe Developer Console integration. Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] deployment.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.

1. Under the **[!UICONTROL Assets Smart Tags]**, open the configuration created above. On the service settings page, click **[!UICONTROL Edit]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the pre-populated values for the **[!UICONTROL Service URL]** and **[!UICONTROL Authorization Server]** fields.

1. For the fields [!UICONTROL Api Key], [!UICONTROL Technical Account ID], [!UICONTROL Organization ID], and [!UICONTROL Client Secret], copy and use the following values generated in [Adobe Developer Console integration](#create-adobe-i-o-integration).

   | [!UICONTROL Assets Smart Tagging Service Settings] | [!DNL Adobe Developer Console] integration fields |
   |--- |--- |
   | [!UICONTROL Api Key] | [!UICONTROL CLIENT ID] |
   | [!UICONTROL Technical Account ID] | [!UICONTROL TECHNICAL ACCOUNT ID] |
   | [!UICONTROL Organization ID] | [!UICONTROL ORGANIZATION ID] |
   | [!UICONTROL Client Secret] | [!UICONTROL CLIENT SECRET] |

### Configure OAuth for on-premise users {#config-oauth-onprem}

#### Prerequisites {#prereqs-config-oauth-onprem}

An authorization scope is an OAuth string that contains the following prerequisites:

* Create a new OAuth integration in the [Developer Console](https://developer.adobe.com/console/user/servicesandapis) using `ClientID`, `ClientSecretID`, and `OrgID`.
* Add the following files at this path `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configure OAuth for on-premise users {#steps-config-oauth-onprem}

1. Add or update the below properties in `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Update the `auth.token.provider.client.id` with the Client ID of the new OAuth configuration.
   * Update `auth.access.token.request` to `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Rename the file to `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Perform the steps below in `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Update the property auth.ims.client.secret with the Client Secret from the new OAuth integration.
   * Rename the file to `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Save all the changes in content repository development console, for example, CRXDE.
5. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
6. Delete the old configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
7. Restart the console.

### Validate the configuration {#validate-the-configuration}

After you have completed the configuration, you can use a JMX MBean to validate the configuration. To validate, follow these steps.

1. Access your [!DNL Experience Manager] server at `https://[aem_server]:[port]`.

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** to open the OSGi console. Click **[!UICONTROL Main] > [!UICONTROL JMX]**.

1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.

1. Click `validateConfigs()`. In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**.

The validation results are displayed in the same dialog.
-->

### Habilitar el etiquetado inteligente en el flujo de trabajo [!UICONTROL Recurso de actualización DAM] (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.

1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

1. Abra las propiedades del paso para modificar los detalles. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configurar el flujo de trabajo de recursos de actualización DAM y agregar el paso de etiquetas inteligentes](assets/smart-tag-step-properties-workflow1.png)

1. En la pestaña **[!UICONTROL Argumentos]**, seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo se complete aunque falle el paso de etiquetado automático.

   Además, para etiquetar recursos cuando se carguen, independientemente de si el etiquetado inteligente está habilitado en las carpetas, seleccione **[!UICONTROL Omitir indicador de etiqueta inteligente]**.

   ![Configure el flujo de trabajo del recurso de actualización DAM para agregar el paso de la etiqueta inteligente y seleccionar el avance del controlador](assets/smart-tag-step-properties-workflow2.png)

1. Haga clic en hecho ![icono hecho](assets/do-not-localize/check-ok-done-icon.png) para cerrar el paso del proceso.

1. Haga clic en **[!UICONTROL Sincronizar]** para guardar el flujo de trabajo.

## Formación del servicio de contenido inteligente {#training-the-smart-content-service}

Para que el servicio de contenido inteligente reconozca su taxonomía empresarial, ejecútela en un conjunto de recursos que ya incluyan etiquetas relevantes para su negocio. Para etiquetar de forma eficaz las imágenes de marca, el servicio de contenido inteligente requiere que las imágenes de formación se ajusten a determinadas directrices. Después de la formación, el servicio puede aplicar la misma taxonomía a un conjunto similar de recursos.

Puede entrenar el servicio varias veces para mejorar su capacidad de aplicar etiquetas relevantes. Después de cada ciclo de formación, ejecute un flujo de trabajo de etiquetado y compruebe si los recursos están etiquetados correctamente.

Puede entrenar el Servicio de contenido inteligente periódicamente o según sea necesario.

>[!NOTE]
>
>El flujo de trabajo de formación se ejecuta únicamente en carpetas.

### Directrices para la formación {#guidelines-for-training}

Para obtener los mejores resultados, las imágenes del conjunto de formación se ajustan a las siguientes directrices:

**Cantidad y tamaño:** Mínimo de 30 imágenes por etiqueta. Mínimo de 500 píxeles en el lado más largo.

**Coherencia**: las imágenes utilizadas para una etiqueta específica son visualmente similares.

Por ejemplo, no es aconsejable etiquetar todas estas imágenes como `my-party` (para aprendizaje) porque no son visualmente similares.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Use suficiente variedad en las imágenes del curso de formación. La idea es ofrecer algunos ejemplos, pero razonablemente diversos, para que Experience Manager aprenda a centrarse en lo correcto. Si aplica la misma etiqueta a imágenes visualmente distintas, incluya al menos cinco ejemplos de cada tipo.

Por ejemplo, para la etiqueta *model-down-pose*, incluya más imágenes de aprendizaje similares a la imagen resaltada a continuación para que el servicio identifique las imágenes similares con mayor precisión durante el etiquetado.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/coverage_1.png)

**Distracción/obstrucción**: El servicio se entrena mejor con las imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el asunto principal).

Por ejemplo, para la etiqueta *casual-shoe*, la segunda imagen no es una buena candidata para entrenamiento.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/distraction.png)

**Complejidad:** Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para etiquetas, como `raincoat` y `model-side-view`, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacidad del servicio de contenido inteligente para aprender sobre sus etiquetas y aplicarlas a otras imágenes depende de la calidad de las imágenes que utilice para la formación. Para obtener los mejores resultados, Adobe recomienda utilizar imágenes visualmente similares para entrenar el servicio para cada etiqueta.

### Formación periódica {#periodic-training}

Puede habilitar el Servicio de contenido inteligente para que se imparta formación periódicamente sobre los recursos y las etiquetas asociadas dentro de una carpeta. Abra la página [!UICONTROL Propiedades] de la carpeta de recursos, seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en la pestaña **[!UICONTROL Detalles]** y guarde los cambios.

![enable_smart_tags](assets/enable_smart_tags.png)

Una vez seleccionada esta opción para una carpeta, [!DNL Experience Manager] ejecuta un flujo de trabajo de formación automáticamente para entrenar el servicio de contenido inteligente en los recursos de la carpeta y sus etiquetas. De forma predeterminada, el flujo de trabajo de formación se ejecuta semanalmente a las 12:30 los sábados.

### Formación a la carta {#on-demand-training}

Puede entrenar el servicio de contenido inteligente siempre que sea necesario desde la consola Flujo de trabajo.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que incluye los recursos etiquetados para entrenar el servicio.
1. Especifique un título para el flujo de trabajo y añada un comentario. A continuación, haga clic en **[!UICONTROL Ejecutar]**. Los recursos y las etiquetas se envían para su formación.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una vez que los recursos de una carpeta se procesan para formación, solo los modificados se procesan en ciclos de formación posteriores.

### Ver informes de formación {#viewing-training-reports}

Para comprobar si el servicio de contenido inteligente ha recibido formación sobre las etiquetas del conjunto de recursos de formación, consulte el informe de flujo de trabajo de formación desde la consola Informes.

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.
1. En la página **[!UICONTROL Informes de recursos]**, haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. A continuación, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. Para ver el informe, haz clic en **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe.

   El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna **[!UICONTROL Estado de formación]** indica que el servicio de contenido inteligente ha recibido formación para la etiqueta. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta.

   Si no ve las etiquetas en este informe, ejecute de nuevo el flujo de trabajo de formación para estas etiquetas.

1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como una hoja de cálculo de Microsoft Excel.

## Limitaciones {#limitations}

* Las etiquetas inteligentes mejoradas se basan en modelos de aprendizaje de imágenes y sus etiquetas. Estos modelos no siempre son perfectos para identificar etiquetas. La versión actual del servicio de contenido inteligente tiene las siguientes limitaciones:

   * Incapacidad para reconocer diferencias sutiles en las imágenes. Por ejemplo, camisetas ajustadas delgadas versus regulares.
   * Incapacidad para identificar etiquetas en función de patrones o partes diminutos de una imagen. Por ejemplo, logotipos en camisetas.
   * El etiquetado es compatible con las configuraciones regionales que admiten [!DNL Experience Manager].

* Para buscar recursos con etiquetas inteligentes (regulares o mejoradas), use el Omnisearch [!DNL Assets] (búsqueda de texto completo). No hay ningún predicado de búsqueda independiente para las etiquetas inteligentes.

>[!MORELIKETHIS]
>
>* [Información general y cómo entrenar etiquetas inteligentes](enhanced-smart-tags.md)
>* [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](config-oauth.md)
>* [Tutorial de vídeo sobre etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
