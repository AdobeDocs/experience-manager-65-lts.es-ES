---
title: Trabajar con credenciales
description: Importe credenciales en AEM Forms mediante la API de Trust Manager y la API de Java. Además, aprenda a eliminar credenciales mediante la API de Trust Manager y la API de Java.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: b3a0eb20-5b85-45a3-a416-a16a9f44acc5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 1%

---

# Trabajar con credenciales {#working-with-credentials}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de credenciales**

Una credencial contiene la información de clave privada necesaria para firmar o identificar documentos. Un certificado es información de clave pública que se configura para la confianza. AEM Forms utiliza certificados y credenciales para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Aplicar derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* El servicio Signature accede a los certificados y las credenciales mientras realiza operaciones como firmar digitalmente documentos de PDF. (Consulte [Firmar digitalmente documentos de PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Puede interactuar mediante programación con el servicio de credenciales mediante la API de Java de Administrador de confianza. Puede realizar las siguientes tareas:

* [Importación de credenciales mediante la API de Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>También puede importar y eliminar certificados mediante la consola de administración. (Consulte la [ayuda de administración.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importación de credenciales mediante la API de Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Puede importar mediante programación una credencial en AEM Forms mediante la API de Administrador de confianza. Por ejemplo, puede importar una credencial utilizada para firmar un documento de PDF. (Consulte [Firmar digitalmente documentos de PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Al importar una credencial, se especifica un alias para la credencial. El alias se utiliza para realizar una operación de Forms que requiere credenciales. Una vez importadas, las credenciales se pueden ver en la consola de administración, como se muestra en la siguiente ilustración. Observe que el alias de la credencial es *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>No puede importar una credencial en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary-of-steps}

Para importar una credencial en AEM Forms, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Haga referencia a la credencial.
1. Realice la operación de importación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben añadirse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Para poder importar mediante programación una credencial en AEM Forms, cree un cliente de servicio de credenciales. Para obtener más información, vea [Configurar propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Hacer referencia a la credencial**

Haga referencia a una credencial que desee importar en AEM Forms. El inicio rápido asociado a esta sección hace referencia a un archivo P12 en el sistema de archivos.

**Realizar la operación de importación**

Después de hacer referencia a la credencial, impórtela a AEM Forms. Si la credencial no se importa correctamente, se produce una excepción. Al importar una credencial, se especifica un alias para la credencial.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de servicio de credenciales](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciales mediante la API de Java {#import-credentials-using-the-java-api}

Importe una credencial en AEM Forms mediante la API de Trust Manager (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-truststore-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `CredentialServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a la credencial

   * Crear un objeto `java.io.FileInputStream` mediante su constructor. Pase un valor de cadena que especifique la ubicación de la credencial.
   * Cree un objeto `com.adobe.idp.Document` que almacene la credencial mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene la credencial al constructor.

1. Realice la operación de importación

   * Cree una matriz de cadenas que contenga un elemento. Asigne el valor `truststore.usage.type.sign` al elemento.
   * Invoque el método `importCredential` del objeto `CredentialServiceClient` y pase los siguientes valores:

      * Valor de cadena que especifica el valor de alias de la credencial.
      * La instancia `com.adobe.idp.Document` que almacena la credencial.
      * Valor de cadena que especifica la contraseña asociada a la credencial.
      * Matriz de cadenas que contiene el valor de uso. Por ejemplo, puede especificar este valor `truststore.usage.type.sign`. Para importar una credencial de extensión de Reader, especifique `truststore.usage.type.lcre`.

**Consulte también**

[Importación de credenciales mediante la API de Trust Manager](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eliminación de credenciales mediante la API de Administrador de confianza {#deleting-credentials-by-using-the-trust-manager-api}

Puede eliminar una credencial mediante programación utilizando la API de Administrador de confianza. Al eliminar una credencial, debe especificar un alias que corresponda a la credencial. Una vez eliminada, no se puede utilizar una credencial para realizar una operación.

>[!NOTE]
>
>No puede eliminar una credencial en AEM Forms mediante servicios web.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar una credencial, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de credenciales.
1. Realice la operación de eliminación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Los siguientes archivos JAR deben añadirse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de servicio de credenciales**

Para poder eliminar una credencial mediante programación, cree un cliente del servicio de integración de datos. Al crear un cliente de servicios, define la configuración de conexión necesaria para invocar un servicio. Para obtener más información, vea [Configurar propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Realizar la operación de eliminación**

Para eliminar una credencial, especifique el alias que corresponda a la credencial. Si especifica un alias que no existe, se produce una excepción.

**Consulte también**

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciales mediante la API de Java](credentials.md#import-credentials-using-the-java-api)

### Eliminación de credenciales mediante la API de Java {#deleting-credentials-using-the-java-api}

Eliminar una credencial de AEM Forms mediante la API de Administrador de confianza (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-truststore-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de servicio de credenciales

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `CredentialServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Realice la operación de eliminación

   Invoque el método `deleteCredential` del objeto `CredentialServiceClient` y pase un valor de cadena que especifique el valor del alias.

**Consulte también**

[Eliminación de credenciales mediante la API de Administrador de confianza](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
