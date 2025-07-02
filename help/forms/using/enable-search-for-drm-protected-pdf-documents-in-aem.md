---
title: Habilitar AEM para buscar documentos PDF protegidos mediante Seguridad de documentos
description: Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: ad86398d-0dc9-4168-b409-4d231b8d586b
source-git-commit: 757c26274b39f5fb37a090f320493abd1af44c42
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 98%

---

# Habilitar AEM para buscar documentos PDF protegidos mediante Seguridad de documentos{#enable-aem-to-search-document-security-protected-pdf-documents}

La búsqueda de AEM puede buscar y localizar AEM Assets y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar la búsqueda nativa para realizar búsquedas de texto completo en [documentos PDF protegidos con seguridad de documentos de AEM](../../forms/using/admin-help/document-security.md). Para permitir que AEM realice búsquedas de texto completo en dichos documentos, realice los siguientes pasos:

1. Establezca una conexión segura
1. Indexe un documento PDF de ejemplo protegido por directivas

## Requisitos previos {#prerequisites}

* Si utiliza AEM Forms en OSGi:

   * Instale el [Paquete del indexador de seguridad de documentos de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) en el servidor de AEM Forms.

   * Asegúrese de que haya AEM Forms en el servidor JEE en funcionamiento y de que la seguridad de los documentos esté instalada en AEM Forms correspondiente del servidor JEE. Necesita AEM Forms del servidor JEE para indexar el documento protegido.

* Si solo utiliza AEM Forms en el servidor JEE, el paquete del indexador ya estará instalado.
* Asegúrese de que todos los paquetes estén en funcionamiento. Si no todos los paquetes están activos, espere hasta que todos los paquetes estén en funcionamiento.

   * Para AEM Forms en OSGi, los paquetes se enumeran en https://&#39;[servidor]:[puerto]&#39;/system/console/bundles.
   * Para AEM Forms en JEE, los paquetes se enumeran en https://&#39;[servidor]:[puerto]&#39;/[context-path]/system/console/bundles. Por ejemplo, https://localhost:8080/lc/system/console/bundles.

* Agregue el paquete *sun.util.calendar* a la lista de permitidos. Para agregar el paquete a la lista de permitidos, realice los siguientes pasos:

   1. Abra la consola web de AEM. La dirección URL es https://&#39;[servidor]:[puerto]&#39;/system/console/configMgr.
   1. Localice y abra **Configuración del firewall de deserialización**.

   1. Agregue el paquete sun.util.calendar al campo Allowlisted classes o Paquete de prefijos y haga clic en **Guardar**.

### Establezca una conexión segura entre las pilas de AEM Forms JEE y OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Puede utilizar uno de los siguientes métodos para establecer la conexión segura:

* Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE
* Configurar el paquete del SDK del cliente de LiveCycle de Adobe mediante la autenticación mutua

#### Configurar el paquete del SDK del cliente de LiveCycle de Adobe con AEM Forms en las credenciales de administrador de JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra la consola web de AEM. La dirección URL es https://&#39;[servidor]:[puerto]&#39;/system/console/configMgr.
1. Busque y abra el paquete **SDK de cliente de LiveCycle de Adobe**. Especifique un valor para los siguientes campos:

   * **URL del servidor:** especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nombre del servicio**: agregue RightsManagementService a la lista de servicios especificados.
   * **Nombre de usuario:** especifique el nombre de usuario de AEM Forms en la cuenta JEE que se utilizará para iniciar llamadas desde el servidor de AEM. La cuenta especificada debe tener permisos para iniciar los servicios de documentos en AEM Forms en el servidor JEE.
   * **Contraseña**: especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos.

#### Configurar el paquete del SDK del cliente de LiveCycle de Adobe mediante la autenticación mutua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE.
1. Abra la consola web de AEM. La dirección URL es https://&#39;[servidor]:[puerto]&#39;/system/console/configMgr.
1. Busque y abra el paquete **SDK de cliente de LiveCycle de Adobe**. Especifique un valor para las siguientes propiedades:

   * **URL del servidor**: especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie el servidor AEM con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Habilite SSL bidireccional**: active la opción Enable 2-way SSL.
   * **URL del archivo KeyStore**: especifique la dirección URL del archivo keystore.
   * **URL de la interfaz de TrustStore**: especifique la dirección URL del archivo truststore.
   * **Contraseña de KeyStore**: especifique la contraseña del archivo keystore.
   * **TrustStorePassword**: especifique la contraseña del archivo truststore.
   * **Nombre del servicio**: agregue RightsManagementService a la lista de servicios especificados.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF protegidos

### Indexe un documento PDF de ejemplo protegido por directivas {#index-a-sample-policy-protected-pdf-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en el administrador de recursos digitales de AEM y cargue los documentos PDF protegidos por directivas en la carpeta recién creada.

   Ahora puede buscar los documentos protegidos por directivas mediante la búsqueda de AEM.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.
