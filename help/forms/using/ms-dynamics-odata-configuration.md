---
title: Configuración de OData de Microsoft Dynamics
description: Aprenda a utilizar, integrar y trabajar con servicios de Microsoft Dynamics en línea y locales a través del modelo de datos de formulario.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 93%

---

# Configuración de OData de Microsoft Dynamics{#microsoft-dynamics-odata-configuration}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html?lang=es) |
| AEM 6.5 | Este artículo |

![integración de datos](assets/data-integeration.png)

Microsoft Dynamics es un software de gestión de relaciones con el cliente (CRM) y planificación de recursos empresariales (ERP) que proporciona soluciones empresariales para crear y administrar cuentas de cliente, contactos, posibles clientes, oportunidades y casos. La [integración de datos de AEM Forms](../../forms/using/data-integration.md) proporciona una configuración de servicio en la nube de OData para integrar Forms con servidores de Microsoft Dynamics en línea y locales. Esto permite crear el modelo de datos de formulario en función de las entidades, atributos y servicios definidos en el servicio de Microsoft Dynamics. El modelo de datos de formulario se puede utilizar para crear formularios adaptables que interactúen con el servidor de Microsoft Dynamics para habilitar los flujos de trabajo empresariales. Por ejemplo:

* Consultar el servidor de Microsoft Dynamics para obtener datos y rellenar previamente formularios adaptables
* Escribir datos en Microsoft Dynamics durante el envío de formularios adaptables
* escribir datos en Microsoft Dynamics mediante entidades personalizadas definidas en el modelo de datos de formulario y a la inversa;

El paquete de complementos de AEM Forms también incluye la configuración de OData de referencia, que puede utilizar para integrar rápidamente Microsoft Dynamics con AEM Forms.

Cuando se instala el paquete, las siguientes entidades y servicios están disponibles en la instancia de AEM Forms:

* El servicio en la nube de OData de Microsoft Dynamics (servicio OData)
* El modelo de datos de formulario con entidades y servicios preconfigurados de Microsoft Dynamics

Las entidades y servicios preconfigurados de Microsoft Dynamics de un modelo de datos de formulario solo están disponibles en la instancia de AEM Forms si el modo de ejecución de la instancia de AEM se ha definido como `samplecontent` (predeterminado). El servicio en la nube de OData de MS Dynamics (servicio OData) también está disponible con otros modos de ejecución. Para obtener más información sobre la configuración de los modos de ejecución de una instancia de AEM, consulte [Modos de ejecución](/help/sites-deploying/configure-runmodes.md).

## Requisitos previos {#prerequisites}

Antes de comenzar a configurar Microsoft Dynamics, asegúrese de que dispone de lo siguiente:

* Se ha instalado el [paquete de complementos de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
* Se ha configurado Microsoft Dynamics 365 en línea o se ha instalado una instancia de una de las siguientes versiones de Microsoft Dynamics:

   * Microsoft Dynamics 365 local
   * Microsoft Dynamics 2016 local

* [Se ha registrado la aplicación del servicio en línea de Microsoft Dynamics con Microsoft Azure Active Directory](https://docs.microsoft.com/es-es/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Tome nota de los valores del ID de cliente (también denominado ID de aplicación) y del secreto de cliente del servicio registrado. Estos valores se utilizan para [configurar el servicio en la nube del servicio de Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Establecer la URL de respuesta para la aplicación registrada de Microsoft Dynamics {#set-reply-url-for-registered-microsoft-dynamics-application}

Haga lo siguiente para establecer la URL de respuesta para la aplicación registrada de Microsoft Dynamics:

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor en línea de Microsoft Dynamics.

1. Vaya a su cuenta de Microsoft Active Directory y agregue la siguiente URL de configuración del servicio en la nube en la opción **URL de respuesta** de la aplicación registrada:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure Directory](assets/azure_directory_new.png)

1. Guarde la configuración.

## Configuración de Microsoft Dynamics para IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics utiliza la autenticación basada en notificaciones para proporcionar acceso a los datos del servidor de Microsoft Dynamics CRM a los usuarios externos. Para ello, realice los siguientes pasos para configurar Microsoft Dynamics para la implementación con conexión a Internet y las opciones de notificación.

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor local de Microsoft Dynamics.

1. Configure la instancia local de Microsoft Dynamics para IFD como se describe en [Configurar IFD para Microsoft Dynamics](https://technet.microsoft.com/es-es/library/dn609803.aspx).
1. Ejecute los siguientes comandos utilizando Windows PowerShell para configurar las opciones de notificación en Microsoft Dynamics para IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro de aplicaciones para CRM local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obtener más información.

## Configurar el cliente OAuth en el equipo AD FS {#configure-oauth-client-on-ad-fs-machine}

Haga lo siguiente para registrar un cliente de OAuth en el equipo de los Servicios de federación de Active Directory (AD FS) y conceder acceso desde él:

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor local de Microsoft Dynamics.

1. Ejecute el siguiente comando:

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Donde:

   * `Client-ID` es un ID de cliente que puede generar con cualquier generador GUID.
   * `redirect-uri` es la dirección URL del servicio en la nube de OData de Microsoft Dynamics en AEM Forms. El servicio en la nube predeterminado instalado con el paquete de AEM Forms se implementa en la siguiente URL:

     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Ejecute el siguiente comando para conceder acceso desde el equipo AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Donde:

   * `resource` es la URL de la organización de Microsoft Dynamics.

1. Microsoft Dynamics utiliza el protocolo HTTPS. Para invocar los extremos de AD FS desde el servidor de Forms, instale el certificado del sitio de Microsoft Dynamics en el almacén de certificados de Java mediante el comando `keytool` en el equipo en el que se ejecuta AEM Forms.

## Configurar el servicio en la nube para el servicio de Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

La configuración del **servicio en la nube de OData de MS Dynamics (servicio OData)** viene con las opciones de configuración predeterminadas de OData. Para configurarlo para que se conecte con el servicio de Microsoft Dynamics, siga los siguientes pasos.

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]** y seleccione la carpeta de configuración `global`.
1. Seleccione la configuración **MS Dynamics OData Cloud Service (servicio OData)** y seleccione **[!UICONTROL Propiedades]**. Se abre el cuadro de diálogo de las propiedades de configuración del servicio en la nube.

   En la pestaña **Configuración de autenticación**:

   1. Introduzca el valor del campo **Raíz del servicio**. Vaya a la instancia de Dynamics y luego a **Recursos para desarrolladores** para ver el valor del campo Raíz del servicio. por ejemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Reemplace los valores predeterminados en los campos **ID de cliente** (también denominado **ID de aplicación**), **Secreto de cliente**, **URL de OAuth**, **Actualizar URL del token**, **URL del token de acceso** y **Recurso** con los valores de la configuración del servicio de Microsoft Dynamics. Es obligatorio especificar la URL de la instancia de Dynamics en el campo **Recurso** para configurar Microsoft Dynamics con un modelo de datos de formulario. Utilice la URL raíz del servicio para derivar la URL de la instancia de Dynamics. Por ejemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especifique **openid** en el campo **Ámbito de autorización** para el proceso de autorización en Microsoft Dynamics.

   ![Configuración de autenticación](assets/dynamics_authentication_settings_new.png)

1. Haga clic en **[!UICONTROL Conectarse a OAuth]**. Se le redirigirá a la página de inicio de sesión de Microsoft Dynamics.
1. Inicie sesión con sus credenciales de Microsoft Dynamics y haga clic en Aceptar para permitir que la configuración del servicio en la nube se conecte al servicio de Microsoft Dynamics. Únicamente es necesario completar una vez el proceso para establecer una conexión entre el servicio en la nube y el servicio.

   A continuación, se le redirigirá a la página de configuración del servicio en la nube, la cual muestra un mensaje que indica que la configuración de OData se ha guardado correctamente.

El servicio en la nube OData Cloud Service de MS Dynamics (servicio OData) está configurado y conectado con el servicio de Dynamics.

## Crear un modelo de datos de formulario {#create-form-data-model}

Al instalar el paquete de AEM Forms, se implementa un modelo de datos de formulario (**Microsoft Dynamics FDM**) en la instancia de AEM. De forma predeterminada, el modelo de datos de formulario utiliza el servicio de Microsoft Dynamics configurado en el servicio en la nube de OData de MS Dynamics (servicio OData) como fuente de datos.

Al abrir el modelo de datos de formulario por primera vez, se conecta al servicio configurado de Microsoft Dynamics y recupera entidades de la instancia de Microsoft Dynamics. Las entidades &quot;Contacto&quot; y &quot;Posible cliente&quot; de Microsoft Dynamics ya se han agregado al modelo de datos de formulario.

Para revisar el modelo de datos de formulario, vaya a **[!UICONTROL Forms > Integraciones de datos]**. Seleccione **FDM de Microsoft Dynamics** y haga clic en **Editar** para abrir el modelo de datos de formulario en el modo Edición. También puede abrir el modelo de datos de formulario directamente desde la siguiente URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![fdm-predeterminado-1](assets/default-fdm-1.png)

A continuación, puede crear un formulario adaptable basado en el modelo de datos de formulario y utilizarlo en varios casos de uso de formularios adaptables, como los siguientes:

* Rellenar previamente formularios adaptables consultando información en las entidades y los servicios de Microsoft Dynamics
* Invocar las operaciones del servidor de Microsoft Dynamics definidas en un modelo de datos de formulario mediante las reglas de los formularios adaptables
* Escribir los datos de los formularios enviados en las entidades de Microsoft Dynamics

Se recomienda crear una copia del modelo de datos de formulario que se proporciona con el paquete de AEM Forms y configurar los modelos y los servicios de datos para adaptarlos a sus necesidades. Esto le permitirá asegurarse de que las futuras actualizaciones del paquete no reemplacen el modelo de datos de formulario.

Para obtener más información sobre la creación y el uso de modelos de datos de formulario en flujos de trabajo empresariales, consulte [Integración de datos](../../forms/using/data-integration.md).
