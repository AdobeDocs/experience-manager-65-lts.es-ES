---
title: Configuración de las fuentes de datos
description: Aprenda a configurar diferentes tipos de fuentes de datos para poder crear modelos de datos de formulario.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 82%

---

# Configuración de las fuentes de datos{#configure-data-sources}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | Este artículo |


![Integración de datos](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms le permite configurar y conectarse a fuentes de datos diferentes. Los siguientes tipos son compatibles de forma predeterminada. Sin embargo, con poca personalización, también puede integrar otras fuentes de datos.

* Bases de datos relacionales: MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS, postgreSQL y Sybase
* Perfil de usuario de AEM
* Servicios web RESTful
* Servicios web basados en SOAP
* Servicios OData

La integración de datos es compatible con los tipos de autenticación OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica y clave de la API predeterminados, y permite implementar la autenticación personalizada para acceder a servicios web. Mientras que los servicios RESTful, SOAP y OData están configurados en AEM Cloud Services, JDBC para bases de datos relacionales y conector para el perfil de usuario de AEM están configurados en la consola web de AEM.

## Configuración de la base de datos relacional {#configure-relational-database}

Puede configurar bases de datos relacionales mediante la configuración de la consola web de AEM. Haga lo siguiente:

1. Vaya a la consola web de AEM en `https://server:host/system/console/configMgr`.
1. Busque la configuración **[!UICONTROL Fuente de datos obtenida de una conexión Apache Sling]**. Seleccione esta opción para abrir la configuración en modo de edición.
1. En el cuadro de diálogo de configuración, especifique los detalles de la base de datos que desea configurar, como:

   * Nombre de la fuente de datos
   * Propiedad del servicio de la fuente de datos que almacena el nombre de la fuente de datos
   * Nombre de clase Java para el controlador JDBC
   * URI de conexión JDBC
   * Nombre de usuario y contraseña para establecer conexión con el controlador JDBC

   >[!NOTE]
   >
   >Asegúrese de cifrar información confidencial como contraseñas antes de configurar la fuente de datos. Para cifrarla, haga lo siguiente:
   >
   > 1. Vaya a https://&#39;[server]:[port]&#39;/system/console/crypto.
   > 1. En el campo **[!UICONTROL Texto sin formato]**, especifique la contraseña o cualquier cadena que desee cifrar y seleccione **[!UICONTROL Proteger]**.
   >
   >El texto cifrado aparece en el campo Texto protegido que puede especificar en la configuración.

1. Habilite **[!UICONTROL Probar en el préstamo]** o **[!UICONTROL Probar en la devolución]** para especificar que los objetos se validan antes de ser prestados o devueltos al grupo, respectivamente.
1. Especifique una consulta SQL SELECT en el campo **[!UICONTROL Consulta de validación]** para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. En función de la base de datos, especifique una de las siguientes opciones:

   * SELECT 1 (MySQL y MS SQL)
   * SELECT 1 desde dual (Oracle)

1. Seleccione **[!UICONTROL Guardar]** para salvar la configuración.

   >[!NOTE]
   >
   > Si el modelo de datos de Forms contiene un objeto que es una palabra clave reservada para la base de datos relacional, puede provocar problemas de adición, actualización o recuperación de datos. Por lo tanto, evite utilizar estos objetos en el modelo de datos de formulario.

## Configurar el perfil de usuario de AEM {#configure-aem-user-profile}

Puede configurar el perfil de usuario de AEM mediante la configuración del conector de perfil de usuario en la consola web de AEM. Haga lo siguiente:

1. Vaya a la consola web de AEM en https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Busque **[!UICONTROL Integraciones de datos de AEM Forms - Configuración del conector de perfil de usuario]** y seleccione para abrir la configuración en modo de edición.
1. En el cuadro de diálogo Configuración del conector de perfil de usuario, puede agregar, quitar o actualizar las propiedades del perfil de usuario. Las propiedades especificadas están disponibles para su uso en el modelo de datos de formulario. Utilice el siguiente formato para especificar las propiedades del perfil del usuario:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Ejemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >El **&#42;** en el ejemplo anterior indica todos los nodos bajo el nodo `profile/empLocation/` en el perfil de usuario de AEM en la estructura CRXDE. Significa que el modelo de datos de formulario puede acceder a la propiedad `city` de tipo `string` presente en cualquier nodo bajo el nodo `profile/empLocation/`. Sin embargo, los nodos que contienen la propiedad especificada deben seguir una estructura coherente.

1. Seleccione **[!UICONTROL Guardar]** para salvar la configuración.

## Configurar carpetas para configuraciones de servicios en la nube {#cloud-folder}

>[!NOTE]
>
>La configuración de la carpeta de servicios en la nube es necesaria para configurar los servicios en la nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube de AEM se consolidan en la carpeta `/conf`, en el repositorio de AEM. De forma predeterminada, la carpeta `conf` contiene la carpeta `global`, donde puede crear configuraciones de servicios en la nube. Debe habilitarla manualmente para las configuraciones en la nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicios en la nube.

Para configurar la carpeta para las configuraciones de servicios en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube u omita este paso para crear y configurar otra carpeta para configuraciones de servicios en la nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione la carpeta `global` y **[!UICONTROL Propiedades]**.

   1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

   1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Seleccione **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.

## Configurar servicios web de RESTful {#configure-restful-web-services}

El servicio web RESTful se puede describir con las [especificaciones de Swagger](https://swagger.io/specification/) en formato JSON o YAML en un archivo de definición. Para configurar el servicio web RESTful en AEM Cloud Service, asegúrese de que dispone del archivo Swagger en su sistema de archivos o de la URL donde se hospeda el archivo.

Haga lo siguiente para configurar los servicios RESTful:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione la URL o el archivo en la lista desplegable Fuente Swagger y especifique la URL Swagger al archivo de definición Swagger o cargue el archivo Swagger de su sistema de archivos local.
   * En función de la entrada Fuente Swagger, los siguientes campos están rellenados previamente con valores:

      * Esquema: Los protocolos de transferencia utilizados por la API REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en la fuente Swagger.
      * Host: El nombre de dominio o la dirección IP del host que sirve la API de REST. Es un campo obligatorio.
      * Ruta base: El prefijo URL de todas las rutas de API. Es un campo opcional.\
        Si es necesario, edite los valores rellenados previamente para estos campos.

   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica, Clave de API, Autenticación personalizada o Autenticación mutua) para acceder al servicio RESTful y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios web RESTful y SOAP](#mutual-authentication).

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

### Configuración del cliente HTTP del modelo de datos del formulario para optimizar el rendimiento {#fdm-http-client-configuration}

Modelo de datos del formulario [!DNL Experience Manager Forms] al integrarse con los servicios web RESTful, ya que la fuente de datos incluye configuraciones de cliente HTTP para la optimización del rendimiento.
Realice los siguientes pasos para configurar el cliente HTTP del modelo de datos de formulario:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms] como administrador y vaya a los paquetes de la consola web de [!DNL Experience Manager]. La URL predeterminada es [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Seleccione **[!UICONTROL Configuración del cliente Http del modelo de datos del formulario para la fuente de datos REST]**.

1. En el cuadro de diálogo [!UICONTROL Configuración del cliente Http del modelo de datos del formulario para fuente de datos REST: &#x200B;]

   * Especifique el número máximo de conexiones permitidas entre el modelo de datos de formulario y los servicios web RESTful en el campo **[!UICONTROL Límite de conexión en total]**. El valor predeterminado es 20 conexiones.

   * Especifique el número máximo de conexiones permitidas para cada ruta en el campo **[!UICONTROL Límite de conexión por ruta]**. El valor predeterminado es 2 conexiones.

   * Especifique la duración, durante la cual se mantiene activa una conexión HTTP persistente, en el campo **[!UICONTROL Mantener activa]**. El valor predeterminado es 15 segundos.

   * Especifique la duración durante la que el servidor [!DNL Experience Manager Forms] espera a que se establezca una conexión, en el campo **[!UICONTROL Suspensión de la conexión]**. El valor predeterminado es 10 segundos.

   * Especifique el período de tiempo máximo de inactividad entre dos paquetes de datos en el campo **[!UICONTROL Suspensión de la toma]**. El valor predeterminado es 30 segundos.

## Configurar servicios web SOAP {#configure-soap-web-services}

Los servicios web basados en SOAP se describen utilizando [Especificaciones del lenguaje de descripción de servicios web (WSDL)](https://www.w3.org/TR/wsdl). Para configurar el servicio web basado en SOAP en AEM Cloud Services, asegúrese de que cuenta con la URL de WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear las fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio web SOAP]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL de WSDL para el servicio web.
   * Punto final de servicio. Especifique un valor en este campo para anular el punto final de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica, Autenticación personalizada, Token X509 o Autenticación mutua) para acceder al servicio SOAP y facilitar los detalles correspondientes para la autenticación.

     Si selecciona **[!UICONTROL Token X509]** como tipo de autenticación, configure el certificado X509. Para obtener más información, consulte [Configurar certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique el alias de KeyStore para el certificado X509 en el campo **[!UICONTROL Alias de la clave]**. Especifique el tiempo, en segundos, durante los que la solicitud de autenticación será válida en el campo **[!UICONTROL Tiempo de vida]**. De forma opcional, seleccione para firmar el cuerpo del mensaje, el encabezado de la marca de tiempo o ambos.

     Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios web RESTful y SOAP](#mutual-authentication).

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio web SOAP.

## Configurar servicios OData {#config-odata}

Un servicio OData se identifica mediante su URL raíz de servicio. Para configurar un servicio OData en AEM Cloud Service, asegúrese de que tiene una URL raíz de servicio para el servicio y haga lo siguiente:

>[!NOTE]
>
>El modelo de datos de formulario admite [OData versión 4](https://www.odata.org/documentation/).
>Para obtener una guía paso a paso sobre la configuración de Microsoft Dynamics 365, en línea o local, consulte [Configuración de OData de Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL raíz del servicio para configurar el servicio OData.
   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica o Autenticación personalizada) para acceder al servicio OData y facilitar los detalles correspondientes para la autenticación.

   >[!NOTE]
   >
   >Seleccione el tipo de autenticación OAuth 2.0 para conectarse a los servicios de Microsoft Dynamics que utilizan el punto final OData como raíz del servicio.

1. Seleccione **Crear** para crear la configuración de nube para el servicio OData.

## Autenticación mutua basada en certificados para servicios web RESTful y SOAP {#mutual-authentication}

Cuando se habilita la autenticación mutua para el modelo de datos de formulario, tanto la fuente de datos como el servidor de AEM que ejecuta el modelo de datos de formulario se autentican entre sí antes de compartir cualquier dato. Puede utilizar la autenticación mutua para conexiones basadas en REST y SOAP (fuentes de datos). Para configurar la autenticación mutua para un modelo de datos de formulario en su entorno de AEM Forms haga lo siguiente:

1. Cargue la clave privada (certificado) en el servidor [!DNL AEM Forms]. Para cargar la clave privada haga lo siguiente:
   1. Inicie sesión en su servidor [!DNL AEM Forms] como administrador.
   1. Navegue hasta **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el usuario `fd-cloudservice` y seleccione **[!UICONTROL Propiedades]**.
   1. Abra la pestaña **[!UICONTROL Keystore]**, expanda la opción **[!UICONTROL Agregar clave privada desde el archivo KeyStore]**, cargue el archivo KeyStore, especifique los alias, las contraseñas y seleccione **[!UICONTROL Enviar]**. El certificado se ha cargado.  El alias de la clave privada se menciona en el certificado y se establece al crearlo.
1. Cargar certificado de confianza al repositorio de confianza global. Para cargar el certificado haga lo siguiente:
   1. Navegue hasta **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL repositorio de confianza]**.
   1. Expanda la opción **[!UICONTROL Agregar certificado del archivo CER]**, seleccione **[!UICONTROL Seleccionar archivo de certificado]**, cargue el certificado y seleccione **[!UICONTROL Enviar]**.
1. Configure los servicios web [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) como fuente de datos y seleccione **[!UICONTROL Autenticación mutua]** como tipo de autenticación. Si configura varios certificados autofirmados para el usuario `fd-cloudservice`, especifique el nombre del alias de la clave para el certificado.

## Pasos siguientes {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un modelo de datos de formulario o, si ya ha creado uno sin una fuente de datos, puede asociarlo a las fuentes de datos configuradas. Consulte [Crear un modelo de datos de formulario](/help/forms/using/create-form-data-models.md) para obtener más información.
