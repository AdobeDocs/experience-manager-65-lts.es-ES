---
title: Controlador de autenticación SAML 2.0
description: Obtenga información acerca del Controlador de autenticación SAML 2.0 en AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM se envía con un controlador de autenticación [SAML](https://saml.xml.org/saml-specifications). Este controlador admite el protocolo de solicitud de autenticación [SAML](https://saml.xml.org/saml-specifications) 2.0 (perfil Web-SSO) mediante el enlace `HTTP POST`.

Admite lo siguiente:

* firma y cifrado de mensajes
* creación automática de usuarios
* sincronización de grupos con los existentes en AEM
* Autenticación iniciada por el proveedor de servicios y el proveedor de identidad

Este controlador almacena el mensaje de respuesta SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un proveedor de servicios de terceros.

>[!NOTE]
>
>Ver [una demostración de la integración de AEM y SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## Configuración del controlador de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

La [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso a la configuración del Controlador de autenticación [SAML](https://saml.xml.org/saml-specifications) 2.0 llamada **Controlador de autenticación Adobe Granite SAML 2.0**. Se pueden configurar las siguientes propiedades.

>[!NOTE]
>
>El Controlador de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Establezca al menos una de las siguientes propiedades para habilitar el controlador:
>
>* La URL POST del proveedor de identidad o la URL de IDP.
>* El ID de entidad de Service Provider.
>

>[!NOTE]
>
>Las afirmaciones de SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en el almacén de confianza. Consulte [Agregar el certificado IdP a TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**Ruta** de acceso al repositorio para el cual Sling debe usar este controlador de autenticación. Si está vacío, el controlador de autenticación se deshabilitará.

**Clasificación del servicio** Valor de clasificación del servicio del marco OSGi para indicar el orden en que se debe llamar a este servicio. Es un valor entero en el que los valores más altos designan una prioridad mayor.

**Alias de certificado IDP** El alias del certificado del IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. Consulte el capítulo &quot;Añadir el certificado IdP al almacén de confianza de AEM&quot; a continuación sobre cómo configurarlo.

**URL de IDP** URL del IDP al que se debe enviar la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse a la configuración OSGi **Filtro de referente de Apache Sling**. Consulte la sección [Consola web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

**ID de entidad de proveedor de servicios** que identifica de forma exclusiva a este proveedor de servicios con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redirección predeterminada**: La ubicación predeterminada a la que se redirigirá tras la autenticación correcta.

>[!NOTE]
>
>Esta ubicación solo se usa si no se ha establecido la cookie `request-path`. Si solicita cualquier página por debajo de la ruta configurada sin un token de inicio de sesión válido, la ruta solicitada se almacenará en una cookie
>y el explorador se redirigirá a esta ubicación de nuevo después de la autenticación correcta.

**Atributo de Id. de usuario** El nombre del atributo que contiene el Id. de usuario usado para autenticar y crear al usuario en el repositorio de CRX.

>[!NOTE]
>
>El identificador de usuario no se tomará del nodo `saml:Subject` de la afirmación de SAML, sino de este `saml:Attribute`.

**Usar cifrado** Indica si este controlador de autenticación espera o no afirmaciones SAML cifradas.

**Crear automáticamente usuarios de CRX** Indica si se crearán o no automáticamente usuarios no existentes en el repositorio después de la autenticación correcta.

>[!CAUTION]
>
>Si la creación automática de usuarios de CRX está desactivada, estos deben crearse manualmente.

**Agregar a grupos** Indica si un usuario debe agregarse automáticamente a los grupos de CRX después de la autenticación correcta.

**Pertenencia a grupo** El nombre del saml:Atributo que contiene una lista de grupos de CRX a los que este usuario debe agregarse.

## Agregar el certificado IdP al almacén de confianza de AEM {#add-the-idp-certificate-to-the-aem-truststore}

Las afirmaciones de SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe:

1. Ir a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Presione el vínculo **[!UICONTROL Crear TrustStore]**
1. Escriba la contraseña de TrustStore y presione **[!UICONTROL Guardar]**.
1. Haz clic en **[!UICONTROL Administrar almacén de confianza]**.
1. Cargue el certificado IdP.
1. Tome nota del alias del certificado. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Agregue la cadena de certificado y clave de Service Provider al repositorio de claves de AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se generará la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Editar el usuario `authentication-service`.
1. Para crear un almacén de claves, haga clic en **Crear almacén de claves** en **Configuración de la cuenta**.

>[!NOTE]
>
>Los siguientes pasos solo son necesarios si el controlador debe poder firmar o descifrar mensajes.

1. Cree el certificado/par de claves para AEM. El comando para generarlo mediante openssl debe ser similar al ejemplo siguiente:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Convertir la clave al formato PKCS#8 con codificación DER. Este es el formato que requiere el almacén de claves de AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Cargue el archivo de clave privada haciendo clic en **Seleccionar archivo de clave privada**.
1. Cargue el archivo de certificado haciendo clic en **Seleccionar archivos de cadena de certificados**.
1. Asigne un alias, como se muestra a continuación:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configuración de un registrador para SAML {#configure-a-logger-for-saml}

Puede configurar un registrador para depurar cualquier problema que pueda surgir por una configuración incorrecta de SAML. Para ello:

1. Va a la consola web, en *http://localhost:4502/system/console/configMgr*
1. Busque y haga clic en la entrada **Configuración del registrador de Apache Sling**
1. Cree un registrador con la siguiente configuración:

   * **Nivel de registro:** depuración
   * **Archivo de registro:** logs/saml.log
   * **Registrador:** com.adobe.granite.auth.saml
