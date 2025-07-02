---
title: Habilitar AEM para buscar documentos PDF protegidos mediante Seguridad de documentos y documentos de Microsoft Office
description: Aprenda a habilitar la búsqueda nativa de AEM para realizar búsquedas de texto completo en documentos PDF protegidos por DRM.
noindex: true
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 5e9d3f3c-8fc4-4d01-9f1e-62d3c29ab9e5
source-git-commit: cd6caaf9de907488db14df2a6396fa60efa2d42c
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 98%

---

# Habilitar AEM para buscar documentos PDF protegidos mediante Seguridad de documentos y documentos de Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager proporciona una interfaz de usuario para buscar y localizar varios recursos almacenados en AEM. La búsqueda nativa permite buscar y localizar AEM Assets y realizar búsquedas de texto en varios formatos de documento de uso común, como archivos de texto sin formato, documentos de Microsoft Office y documentos PDF. También puede ampliar y habilitar la búsqueda nativa para realizar búsquedas de texto completo en documentos de Microsoft Office y PDF protegidos por DRM.

Realice los siguientes pasos para permitir que AEM busque documentos PDF y de Microsoft Office protegidos:

## Antes de comenzar {#before-you-start}

* Instale y configure la seguridad de documentos de AEM Forms.
* Agregue el paquete sun.util.calendar a la lista de permitidos de la **Configuración del firewall de deserialización.** La configuración se enumera en `https://'[server]:[port]'/system/console/configMgr`.
* Asegúrese de que todos los paquetes de AEM estén en funcionamiento. Los paquetes se enumeran en `https://'[server]:[port]'/system/console/bundles`. Si no todos los paquetes están activos, espere y compruebe el estado de los paquetes después de unos minutos.

## Establezca una conexión segura dentro del flujo de trabajo de AEM Forms (AEM Forms en JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una conexión segura permite un flujo de información fluido entre AEM Forms en JEE y los servicios OSGi que se ejecutan en el mismo servidor. Utilice uno de los siguientes métodos para establecer una conexión segura:

* Configurar el paquete del AEM Forms Client SDK con AEM Forms en credenciales de administrador de JEE
* Configurar el paquete del AEM Forms Client SDK mediante autenticación mutua

### Configurar el paquete del AEM Forms Client SDK con AEM Forms en credenciales de administrador de JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra el administrador de configuración de AEM e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del AEM Forms Client SDK. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** especifique la URL HTTP de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nombre del servicio**: agregue RightsManagementService a la lista de servicios especificados.
   * **Nombre de usuario:** especifique el nombre de usuario de AEM Forms en la cuenta JEE que se utilizará para iniciar llamadas desde AEM Forms en el servidor JEE. La cuenta especificada debe tener permisos para invocar servicios de documentos en AEM Forms en el servidor JEE.
   * **Contraseña**: especifique la contraseña de AEM Forms en la cuenta JEE mencionada en el campo Nombre de usuario.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF y de Microsoft Office protegidos.

### Configurar el paquete del AEM Forms Client SDK mediante autenticación mutua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Habilite la autenticación mutua para AEM Forms en JEE.
1. Abra el administrador de configuración de AEM e inicie sesión como administrador. La dirección URL predeterminada es https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Busque y abra el paquete del AEM Forms Client SDK. Especifique un valor para las siguientes propiedades:

   * **URL del servidor:** especifique la URL HTTPS de AEM Forms en el servidor JEE. Para habilitar la comunicación sobre https, reinicie AEM Forms en el servidor JEE con el parámetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Habilite SSL bidireccional**: active la opción Enable 2-way SSL.
   * **URL del archivo KeyStore**: especifique la dirección URL del archivo del repositorio de claves.
   * **URL de la interfaz de TrustStore**: especifique la dirección URL del archivo truststore.
   * **Contraseña de KeyStore**: especifique la contraseña del archivo keystore.
   * **TrustStorePassword**: especifique la contraseña del archivo truststore.
   * **Nombre del servicio**: agregue RightsManagementService a la lista de servicios especificados.

   Haga clic en **Guardar**. AEM está habilitado para buscar documentos PDF y de Microsoft Office protegidos

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

## Indexar un PDF de ejemplo o un documento de Microsoft Office protegidos mediante directivas {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Inicie sesión en AEM Assets como administrador.
1. Cree una carpeta en el administrador de recursos digitales de AEM y cargue un PDF protegido mediante directivas o un documento de Microsoft Office en la carpeta recién creada. Ahora, busque el contenido de los documentos protegidos con directivas mediante la búsqueda de AEM. Debe devolver el documento que contiene el texto buscado.
