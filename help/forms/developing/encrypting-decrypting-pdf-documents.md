---
title: Codificar y descifrar documentos PDF
description: Utilice el servicio Encryption para cifrar y descifrar documentos. Las tareas del servicio Encryption incluyen el cifrado de un documento de PDF con una contraseña, el cifrado de un documento de PDF con un certificado, la eliminación del cifrado basado en contraseña de un documento de PDF, la eliminación del cifrado basado en certificados de un documento de PDF, el desbloqueo del documento de PDF para que se puedan realizar otras operaciones de servicio y la determinación del tipo de cifrado de un documento de PDF protegido.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 9f694358-e502-4fc0-8352-4c5119573756
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 3%

---

# Codificar y descifrar documentos PDF {#encrypting-and-decrypting-pdf-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de cifrado**

El servicio Encryption permite cifrar y descifrar documentos. Cuando se encripta un documento, su contenido se vuelve ilegible. Un usuario autorizado puede desencriptar el documento para obtener acceso a su contenido. Si un documento PDF está encriptado con una contraseña, el usuario debe escribir la contraseña para abrir y visualizar el documento en Adobe Reader o Adobe Acrobat. Del mismo modo, si un documento PDF está encriptado con un certificado, el usuario debe desencriptar el documento PDF con la clave pública que corresponde al certificado (clave privada) que se utilizó para encriptarlo.

Puede realizar estas tareas mediante el servicio Encryption:

* Cifrar un documento de PDF con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Cifrar un documento de PDF con un certificado. (Consulte [Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Quitar el cifrado basado en contraseña de un documento de PDF. (Consulte [Quitar el cifrado de contraseña](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Quite el cifrado basado en certificados de un documento de PDF. (Consulte [Quitar el cifrado basado en certificados](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloquee el documento de PDF para que se puedan realizar otras operaciones de servicio. Por ejemplo, después de desbloquear un documento de PDF cifrado con contraseña, puede aplicarle una firma digital. (Consulte [Desbloquear documentos cifrados de PDF](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine el tipo de cifrado de un documento de PDF protegido. (Consulte [Determinación del tipo de cifrado](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Cifrar documentos de PDF con una contraseña {#encrypting-pdf-documents-with-a-password}

Cuando se cifra un documento PDF con una contraseña, cualquier usuario deberá especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que se pueda realizar otra operación de AEM Forms, como firmar digitalmente el documento de PDF, se debe desbloquear un documento de PDF cifrado con contraseña.

>[!NOTE]
>
>Si carga un documento de PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Recursos de escritura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para cifrar un documento de PDF con una contraseña, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento de PDF para cifrar.
1. Establecer opciones de cifrado en tiempo de ejecución.
1. Añada la contraseña.
1. Guarde el documento de PDF cifrado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un objeto de API de cliente de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption.

**Obtener un documento de PDF para cifrar**

Obtenga un documento de PDF sin cifrar para cifrar el documento con una contraseña. Si intenta proteger un documento de PDF que ya está cifrado, se producirá una excepción.

**Establecer opciones de cifrado en tiempo de ejecución**

Para cifrar un documento de PDF con una contraseña, debe especificar cuatro valores, incluidos dos valores de contraseña. El primer valor de contraseña se utiliza para cifrar el documento de PDF y debe especificarse al abrir el documento de PDF. El segundo valor de contraseña, denominado valor de contraseña maestra, se utiliza para quitar el cifrado del documento de PDF. Los valores de contraseña distinguen entre mayúsculas y minúsculas y estos dos valores de contraseña no pueden ser iguales.

Especifique los recursos de documentos de PDF que desea cifrar. Puede cifrar todo el documento de PDF, todo excepto los metadatos del documento o solo los archivos adjuntos. Si cifra únicamente los datos adjuntos del documento, se pedirá al usuario una contraseña cuando intente obtener acceso a los datos adjuntos del archivo.

Al cifrar un documento de PDF, puede especificar los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que puede realizar un usuario que abre un documento de PDF cifrado con contraseña. Por ejemplo, para extraer correctamente datos de formulario, debe establecer los siguientes permisos:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Los permisos se especifican como `PasswordEncryptionPermission` valores de enumeración.

**Agregar la contraseña**

Después de recuperar un documento de PDF no protegido y establecer los valores de cifrado en tiempo de ejecución, puede agregar una contraseña al documento de PDF.

**Guardar el documento de PDF cifrado como archivo de PDF**

Puede guardar el documento de PDF cifrado con contraseña como archivo de PDF.

**Consulte también**

[Cifrar un documento de PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifrado de un documento de PDF mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Cifrar un documento de PDF mediante la API de Java {#encrypt-a-pdf-document-using-the-java-api}

Cifrar un documento de PDF con una contraseña mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Crear una API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento de PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Cree un objeto `PasswordEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documentos de PDF que se van a cifrar invocando el método `setEncryptOption` del objeto `PasswordEncryptionOptionSpec` y pasando un valor de enumeración `PasswordEncryptionOption` que especifica los recursos de documentos que se van a cifrar. Por ejemplo, para cifrar todo el documento de PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `PasswordEncryptionOption.ALL`.
   * Cree un objeto `java.util.List` que almacene los permisos de cifrado mediante el constructor `ArrayList`.
   * Especifique un permiso invocando el método `add` del objeto `java.util.List` y pasando un valor de enumeración que corresponda al permiso que desea establecer. Por ejemplo, para establecer el permiso que permite a un usuario copiar datos en el documento de PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita este paso para cada permiso que desee establecer).
   * Especifique la opción de compatibilidad de Acrobat invocando el método `setCompatability` del objeto `PasswordEncryptionOptionSpec` y pasando un valor de enumeración que especifique el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique el valor de contraseña que permite a un usuario abrir el documento cifrado de PDF invocando el método `setDocumentOpenPassword` del objeto `PasswordEncryptionOptionSpec` y pasando un valor de cadena que representa la contraseña de apertura.
   * Especifique el valor de la contraseña maestra que permite a un usuario quitar el cifrado del documento de PDF invocando el método `setPermissionPassword` del objeto `PasswordEncryptionOptionSpec` y pasando un valor de cadena que representa la contraseña maestra.

1. Añada la contraseña.

   Cifre el documento de PDF invocando el método `encryptPDFUsingPassword` del objeto `EncryptionServiceClient` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento de PDF que se va a cifrar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El método `encryptPDFUsingPassword` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `encryptPDFUsingPassword`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): cifrado de un documento de PDF mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)


[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrado de un documento de PDF mediante la API de servicio web {#encrypting-a-pdf-document-using-the-web-service-api}

Cifrar un documento de PDF con una contraseña mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF para cifrar.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF cifrado con una contraseña.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que se va a cifrar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un objeto `PasswordEncryptionOptionSpec` mediante su constructor.
   * Especifique los recursos de documentos de PDF que desea cifrar asignando un valor de enumeración `PasswordEncryptionOption` al miembro de datos `encryptOption` del objeto `PasswordEncryptionOptionSpec`. Para cifrar todo el PDF, incluidos sus metadatos y sus datos adjuntos, asigne `PasswordEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un valor de enumeración `PasswordEncryptionCompatability` al miembro de datos `compatability` del objeto `PasswordEncryptionOptionSpec`. Por ejemplo, asigne `PasswordEncryptionCompatability.ACRO_7` a este miembro de datos.
   * Especifique el valor de contraseña que permite a un usuario abrir el documento cifrado de PDF asignando un valor de cadena que representa la contraseña de apertura al miembro de datos `documentOpenPassword` del objeto `PasswordEncryptionOptionSpec`.
   * Especifique el valor de contraseña que permite a un usuario quitar el cifrado del documento de PDF asignando un valor de cadena que represente la contraseña maestra al miembro de datos `permissionPassword` del objeto `PasswordEncryptionOptionSpec`.

1. Añada la contraseña.

   Cifre el documento de PDF invocando el método `encryptPDFUsingPassword` del objeto `EncryptionServiceClient` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento de PDF que se va a cifrar con la contraseña.
   * El objeto `PasswordEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El método `encryptPDFUsingPassword` devuelve un objeto `BLOB` que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingPassword`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifrar documentos de PDF con certificados {#encrypting-pdf-documents-with-certificates}

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública. Se pueden otorgar permisos a varios destinatarios diferentes para el documento. Muchos aspectos del cifrado son posibles gracias a la tecnología de claves públicas. Se usa un algoritmo para generar dos números grandes, conocidos como *claves*, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, solo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.

Una de las claves actúa como clave privada de un usuario. Es importante que solo el usuario tenga acceso a esta clave. La otra clave es la clave pública del usuario, que se puede compartir con otros.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. Se utiliza el formato X.509 para almacenar certificados. Los certificados los suele emitir y firmar digitalmente una autoridad de certificación (CA), que es una entidad reconocida que proporciona confianza en la validez del certificado. Los certificados tienen una fecha de caducidad tras la cual ya no son válidos. Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL las publican periódicamente las autoridades certificadoras. El estado de revocación de un certificado también se puede recuperar mediante el Protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Si carga un documento de PDF cifrado en el repositorio de AEM Forms, no podrá descifrar el documento de PDF ni extraer el contenido XDP. Se recomienda no cifrar un documento antes de cargarlo en el repositorio de AEM Forms. (Consulte [Recursos de escritura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para poder cifrar un documento de PDF con un certificado, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API de Administrador de confianza. (Consulte [Importación de credenciales mediante la API del Administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para cifrar un documento de PDF con un certificado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de cifrado.
1. Obtenga un documento de PDF para cifrar.
1. Haga referencia al certificado.
1. Establecer opciones de cifrado en tiempo de ejecución.
1. Cree un documento de PDF cifrado mediante certificado.
1. Guarde el documento de PDF cifrado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un objeto de API de cliente de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si está usando la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si está usando la API del servicio de cifrado del servicio web, cree un objeto `EncryptionServiceService`.

**Obtener un documento de PDF para cifrar**

Obtenga un documento de PDF sin cifrar para cifrar. Si intenta proteger un documento de PDF que ya está cifrado, se generará una excepción.

**Hacer referencia al certificado**

Para cifrar un documento de PDF con un certificado, haga referencia a un certificado que se utiliza para cifrar un documento de PDF. El certificado es un archivo .cer, .crt o .pem. Se utiliza un archivo PKCS#12 para almacenar claves privadas con los certificados correspondientes.

Al cifrar un documento de PDF con un certificado, especifique los permisos asociados al documento protegido. Al especificar permisos, puede controlar las acciones que puede realizar un usuario que abre un documento de PDF cifrado mediante certificado.

**Establecer opciones de cifrado en tiempo de ejecución**

Especifique los recursos de documentos de PDF que desea cifrar. Puede cifrar todo el documento de PDF, todo excepto los metadatos del documento o solo los archivos adjuntos.

**Crear un documento de PDF cifrado mediante certificado**

Después de recuperar un documento de PDF no protegido, hacer referencia al certificado y establecer las opciones en tiempo de ejecución, puede crear un documento de PDF cifrado mediante certificado. Una vez cifrado el documento de PDF, se necesita la clave pública correspondiente para descifrarlo.

**Guardar el documento de PDF cifrado como archivo de PDF**

Puede guardar el documento cifrado de PDF como archivo de PDF.

**Consulte también**

[Cifrar un documento de PDF con un certificado mediante la API de Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Cifrar un documento de PDF con un certificado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Cifrar un documento de PDF con un certificado mediante la API de Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Cifrar un documento de PDF con un certificado mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga un documento de PDF para cifrar.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a cifrar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Haga referencia al certificado.

   * Cree un objeto `java.util.List` que almacene información de permisos mediante su constructor.
   * Especifique el permiso asociado con el documento cifrado invocando el método `add` del objeto `java.util.List` y pasando un valor de enumeración `CertificateEncryptionPermissions` que representa los permisos concedidos al usuario que abre el documento protegido de PDF. Por ejemplo, para especificar todos los permisos, pase `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Crear un objeto `Recipient` mediante su constructor.
   * Cree un objeto `java.io.FileInputStream` que represente el certificado que se usa para cifrar el documento de PDF usando su constructor y pasando un valor de cadena que especifique la ubicación del certificado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream` que representa el certificado.
   * Invoque el método `setX509Cert` del objeto `Recipient` y pase el objeto `com.adobe.idp.Document` que contiene el certificado. (Además, el objeto `Recipient` puede tener un alias de certificado de Truststore o una URL LDAP como origen de certificado).
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de permisos y certificados mediante su constructor.
   * Invoque el método `setPerms` del objeto `CertificateEncryptionIdentity` y pase el objeto `java.util.List` que almacena la información de permisos.
   * Invoque el método `setRecipient` del objeto `CertificateEncryptionIdentity` y pase el objeto `Recipient` que almacena información de certificado.
   * Cree un objeto `java.util.List` que almacene información de certificado mediante su constructor.
   * Invoque el método add del objeto `java.util.List` y pase el objeto `CertificateEncryptionIdentity`. (Este objeto `java.util.List` se pasa como parámetro al método `encryptPDFUsingCertificates`.)

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Cree un objeto `CertificateEncryptionOptionSpec` invocando su constructor.
   * Especifique los recursos de documentos de PDF que se van a cifrar invocando el método `setOption` del objeto `CertificateEncryptionOptionSpec` y pasando un valor de enumeración `CertificateEncryptionOption` que especifica los recursos de documentos que se van a cifrar. Por ejemplo, para cifrar todo el documento de PDF, incluidos sus metadatos y sus archivos adjuntos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique la opción de compatibilidad de Acrobat invocando el método `setCompat` del objeto `CertificateEncryptionOptionSpec` y pasando un valor de enumeración `CertificateEncryptionCompatibility` que especifica el nivel de compatibilidad de Acrobat. Por ejemplo, puede especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Cree un documento de PDF cifrado mediante certificado.

   Cifre el documento de PDF con un certificado invocando el método `encryptPDFUsingCertificates` del objeto `EncryptionServiceClient` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento de PDF que se va a cifrar.
   * El objeto `java.util.List` que almacena información de certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El método `encryptPDFUsingCertificates` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF cifrado mediante certificado.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `encryptPDFUsingCertificates`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): cifrado de un documento de PDF con un certificado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifrar un documento de PDF con un certificado mediante la API de servicio web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Cifrar un documento de PDF con un certificado mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un objeto de API de cliente de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF para cifrar.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF cifrado con un certificado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que se va a cifrar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al certificado.

   * Crear un objeto `Recipient` mediante su constructor. Este objeto almacenará información de certificado.
   * Crear un objeto `BLOB` mediante su constructor. Este objeto `BLOB` almacenará el certificado que cifra el documento de PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del certificado y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.
   * Asigne el objeto `BLOB` que almacena el certificado al miembro de datos `x509Cert` del objeto `Recipient`.
   * Cree un objeto `CertificateEncryptionIdentity` que almacene información de certificado mediante su constructor.
   * Asigne el objeto `Recipient` que almacena el certificado al miembro de datos de destinatario del objeto `CertificateEncryptionIdentity`.
   * Cree una matriz `Object` y asigne el objeto `CertificateEncryptionIdentity` al primer elemento de la matriz `Object`. Esta matriz `Object` se pasa como parámetro al método `encryptPDFUsingCertificates`.

1. Establecer opciones de cifrado en tiempo de ejecución.

   * Crear un objeto `CertificateEncryptionOptionSpec` mediante su constructor.
   * Especifique los recursos de documentos de PDF que desea cifrar asignando un valor de enumeración `CertificateEncryptionOption` al miembro de datos `option` del objeto `CertificateEncryptionOptionSpec`. Para cifrar todo el documento de PDF, incluidos los metadatos y los datos adjuntos, asigne `CertificateEncryptionOption.ALL` a este miembro de datos.
   * Especifique la opción de compatibilidad de Acrobat asignando un valor de enumeración `CertificateEncryptionCompatibility` al miembro de datos `compat` del objeto `CertificateEncryptionOptionSpec`. Por ejemplo, asigne `CertificateEncryptionCompatibility.ACRO_7` a este miembro de datos.

1. Cree un documento de PDF cifrado mediante certificado.

   Cifre el documento de PDF con un certificado invocando el método `encryptPDFUsingCertificates` del objeto `EncryptionServiceService` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento de PDF que se va a cifrar.
   * Matriz `Object` que almacena información de certificado.
   * El objeto `CertificateEncryptionOptionSpec` que contiene opciones de cifrado en tiempo de ejecución.

   El método `encryptPDFUsingCertificates` devuelve un objeto `BLOB` que contiene un documento de PDF cifrado mediante certificado.

1. Guarde el documento de PDF cifrado como archivo de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingCertificates`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `binaryData` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar el cifrado basado en certificados {#removing-certificate-based-encryption}

El cifrado basado en certificados se puede quitar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat. Para quitar el cifrado de un documento de PDF cifrado con un certificado, se debe hacer referencia a una clave pública. Una vez eliminado el cifrado de un documento de PDF, ya no es seguro.

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para quitar el cifrado basado en certificados de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado de PDF.
1. Elimine el cifrado.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si está usando la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si está usando la API del servicio de cifrado del servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento cifrado de PDF**

Obtenga un documento de PDF cifrado para quitar el cifrado basado en certificados. Si intenta quitar el cifrado de un documento de PDF que no está cifrado, se generará una excepción. Del mismo modo, si intenta quitar el cifrado basado en certificados de un documento cifrado con contraseña, se generará una excepción.

**Quitar cifrado**

Para quitar el cifrado basado en certificados de un documento de PDF cifrado, necesita un documento de PDF cifrado y la clave privada que corresponde a la clave utilizada para cifrar el documento de PDF. El valor de alias de la clave privada se especifica al eliminar el cifrado basado en certificados de un documento de PDF cifrado. Para obtener información acerca de la clave pública, vea [Cifrar documentos de PDF con certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una clave privada se almacena en el Almacén de confianza de AEM Forms. Cuando se coloca un certificado, se especifica un valor de alias.

**Guardar el documento de PDF**

Una vez eliminado el cifrado basado en certificados de un documento cifrado de PDF, puede guardar el documento de PDF como archivo de PDF. Los usuarios pueden abrir el documento de PDF en Adobe Reader o Acrobat.

**Consulte también**

[Quite el cifrado basado en certificados mediante la API de Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Quitar el cifrado basado en certificados mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Quite el cifrado basado en certificados mediante la API de Java {#remove-certificate-based-encryption-using-the-java-api}

Elimine el cifrado basado en certificados de un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento cifrado de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine el cifrado.

   Quite el cifrado basado en certificados del documento de PDF invocando el método `removePDFCertificateSecurity` del objeto `EncryptionServiceClient` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento de PDF cifrado.
   * Valor de cadena que especifica el nombre de alias de la clave privada que corresponde a la clave utilizada para cifrar el documento PDFf.

   El método `removePDFCertificateSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `removePDFCredentialSecurity`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Quitar el cifrado basado en certificados mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Quitar el cifrado basado en certificados mediante la API de servicio web {#remove-certificate-based-encryption-using-the-web-service-api}

Quite el cifrado basado en certificados mediante la API Encryption (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento cifrado de PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF cifrado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Elimine el cifrado.

   Invoque el método `removePDFCertificateSecurity` del objeto `EncryptionServiceClient` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de secuencia de archivos que representa un documento de PDF cifrado.
   * Valor de cadena que especifica el nombre de alias de la clave pública correspondiente a la clave privada utilizada para cifrar el documento PDFf.

   El método `removePDFCredentialSecurity` devuelve un objeto `BLOB` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `removePDFPasswordSecurity`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar el cifrado de contraseña {#removing-password-encryption}

El cifrado basado en contraseña se puede eliminar de un documento de PDF para que los usuarios puedan abrir el documento de PDF en Adobe Reader o Acrobat sin tener que especificar una contraseña. Una vez eliminado el cifrado basado en contraseña de un documento de PDF, el documento deja de ser seguro.

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para quitar el cifrado basado en contraseña de un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado de PDF.
1. Elimine la contraseña.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si está usando la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si está usando la API del servicio de cifrado del servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento cifrado de PDF**

Obtenga un documento de PDF cifrado para quitar el cifrado basado en contraseña. Si intenta quitar el cifrado de un documento de PDF que no está cifrado, se generará una excepción.

**Quitar la contraseña**

Para quitar el cifrado basado en contraseña de un documento cifrado de PDF, necesita un documento cifrado de PDF y un valor de contraseña maestra que se utilice para quitar el cifrado del documento de PDF. La contraseña utilizada para abrir un documento de PDF cifrado con contraseña no se puede usar para quitar el cifrado. Se especifica una contraseña maestra cuando el documento de PDF se cifra con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Guardar el documento de PDF**

Una vez que el servicio Encryption quita el cifrado basado en contraseña de un documento de PDF, puede guardar el documento de PDF como archivo de PDF. Los usuarios pueden abrir el documento de PDF en Adobe Reader o Acrobat sin especificar una contraseña.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Eliminación del cifrado basado en contraseña mediante la API de Java {#remove-password-based-encryption-using-the-java-api}

Elimine el cifrado basado en contraseña de un documento de PDF mediante la API Encryption (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento cifrado de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Elimine la contraseña.

   Quite el cifrado basado en contraseña del documento de PDF invocando el método `removePDFPasswordSecurity` del objeto `EncryptionServiceClient` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF cifrado.
   * Valor de cadena que especifica el valor de la contraseña maestra que se utiliza para quitar el cifrado del documento de PDF.

   El método `removePDFPasswordSecurity` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` devuelto por el método `removePDFPasswordSecurity`.

**Consulte también**

[Inicio rápido (modo SOAP): Eliminación del cifrado basado en contraseña mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Quitar el cifrado basado en contraseña mediante la API de servicio web {#remove-password-based-encryption-using-the-web-service-api}

Quite el cifrado basado en contraseña utilizando la API Encryption (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF cifrado con contraseña.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF cifrado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Elimine la contraseña.

   Invoque el método `removePDFPasswordSecurity` del objeto `EncryptionServiceService` y pase los siguientes valores:

   * El objeto `BLOB` que contiene datos de secuencia de archivos que representa un documento de PDF cifrado.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para quitar el cifrado del documento de PDF. Este valor se especifica al cifrar el documento de PDF con una contraseña.

   El método `removePDFPasswordSecurity` devuelve un objeto `BLOB` que contiene un documento de PDF no protegido.

1. Guarde el documento de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF no protegido.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `removePDFPasswordSecurity`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos cifrados de PDF {#unlocking-encrypted-pdf-documents}

Un documento de PDF cifrado con contraseña o con certificado debe estar desbloqueado para que se pueda realizar otra operación de AEM Forms en él. Si intenta realizar una operación en un documento cifrado de PDF, generará una excepción. Después de desbloquear un documento cifrado de PDF, puede realizar una o varias operaciones en él. Estas operaciones pueden pertenecer a otros servicios, como el servicio de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para desbloquear un documento cifrado de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado de PDF.
1. Desbloquee el documento.
1. Realice una operación de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio de cifrado**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si está usando la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si está usando la API del servicio de cifrado del servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento cifrado de PDF**

Obtenga un documento de PDF cifrado para desbloquearlo. Si intenta desbloquear un documento de PDF que no esté cifrado, se generará una excepción.

**Desbloquear el documento**

Para desbloquear un documento de PDF cifrado con contraseña, necesita un documento de PDF cifrado y un valor de contraseña que se utilice para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento de PDF con una contraseña. (Consulte [Cifrar documentos de PDF con una contraseña](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Para desbloquear un documento de PDF cifrado mediante certificado, se necesita un documento de PDF cifrado y el valor de alias de la clave pública que corresponde a la clave privada que se utilizó para cifrar el documento de PDF.

**Realizar una operación de AEM Forms**

Una vez desbloqueado un documento cifrado de PDF, puede realizar otra operación de servicio en él, como aplicarle derechos de uso. Esta operación pertenece al servicio Acrobat Reader DC Extensions.

**Consulte también**

[Desbloquear un documento cifrado de PDF mediante la API de Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear un documento cifrado de PDF mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear un documento cifrado de PDF mediante la API de Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloquee un documento cifrado de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento cifrado de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF cifrado utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF cifrado.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando el método `unlockPDFUsingPassword` o `unlockPDFUsingCredential` del objeto `EncryptionServiceClient`.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento de PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF cifrado mediante certificado.
   * Valor de cadena que especifica el nombre de alias de la clave pública que corresponde a la clave privada utilizada para cifrar el documento de PDF.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que se pasa a otro método Java de AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento de PDF desbloqueado para satisfacer sus necesidades empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso a un documento de PDF desbloqueado, pase el objeto `com.adobe.idp.Document` devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `applyUsageRights` del objeto `ReaderExtensionsServiceClient`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): desbloquear un documento de PDF cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modo SOAP)

[Aplicar derechos de uso a documentos de PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear un documento cifrado de PDF mediante la API de servicio web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloquee un documento cifrado de PDF mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de cifrado.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga un documento de PDF cifrado.

   * Crear un objeto `BLOB` mediante su constructor.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF cifrado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Desbloquee el documento.

   Desbloquee un documento de PDF cifrado invocando el método `unlockPDFUsingPassword` o `unlockPDFUsingCredential` del objeto `EncryptionServiceClient`.

   Para desbloquear un documento de PDF cifrado con una contraseña, invoque el método `unlockPDFUsingPassword` y pase los siguientes valores:

   * Un objeto `BLOB` que contiene el documento de PDF cifrado con contraseña.
   * Valor de cadena que especifica el valor de contraseña que se utiliza para abrir un documento de PDF cifrado con contraseña. Este valor se especifica al cifrar el documento de PDF con una contraseña.

   Para desbloquear un documento de PDF cifrado con un certificado, invoque el método `unlockPDFUsingCredential` y pase los siguientes valores:

   * Un objeto `BLOB` que contiene el documento de PDF cifrado mediante certificado.
   * Valor de cadena que especifica el nombre de alias de la clave pública correspondiente a la clave privada utilizada para cifrar el documento PDFf.

   Los métodos `unlockPDFUsingPassword` y `unlockPDFUsingCredential` devuelven un objeto `com.adobe.idp.Document` que se pasa a otro método AEM Forms para realizar una operación.

1. Realice una operación de AEM Forms.

   Realice una operación de AEM Forms en el documento de PDF desbloqueado para satisfacer sus necesidades empresariales. Por ejemplo, suponiendo que desea aplicar derechos de uso al documento de PDF desbloqueado, pase el objeto `BLOB` devuelto por los métodos `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al método `applyUsageRights` del objeto `ReaderExtensionsServiceClient`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinar el tipo de cifrado {#determining-encryption-type}

Puede determinar mediante programación el tipo de cifrado que protege un documento de PDF mediante la API del servicio de cifrado de Java o la API del servicio de cifrado del servicio web. A veces es necesario determinar dinámicamente si un documento de PDF está cifrado y, si es así, el tipo de cifrado. Por ejemplo, puede determinar si un documento de PDF está protegido con cifrado basado en contraseña o con una directiva de Rights Management.

Un documento de PDF puede protegerse con los siguientes tipos de cifrado:

* Cifrado basado en contraseña
* Cifrado basado en certificados
* Una directiva creada por el servicio Rights Management
* Otro tipo de cifrado

>[!NOTE]
>
>Para obtener más información acerca del servicio Encryption, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para determinar el tipo de cifrado que protege un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de cifrado.
1. Obtenga el documento cifrado de PDF.
1. Determine el tipo de cifrado.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

**Crear un cliente de servicio**

Para realizar mediante programación una operación de servicio Encryption, debe crear un cliente de servicio Encryption. Si está usando la API del servicio de cifrado de Java, cree un objeto `EncrytionServiceClient`. Si está usando la API del servicio de cifrado del servicio web, cree un objeto `EncryptionServiceService`.

**Obtener el documento cifrado de PDF**

Obtenga un documento de PDF para determinar el tipo de cifrado que lo protege.

**Determinar el tipo de cifrado**

Puede determinar el tipo de cifrado que protege un documento de PDF. Si el documento de PDF no está protegido, el servicio Encryption le informa de que el documento de PDF no está protegido.

**Consulte también**

[Determine el tipo de cifrado mediante la API de Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinar el tipo de cifrado mediante la API de servicio web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de API de servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Proteger documentos mediante directivas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determine el tipo de cifrado mediante la API de Java {#determine-the-encryption-type-using-the-java-api}

Determine el tipo de cifrado que protege un documento de PDF mediante la API de cifrado (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-encryption-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicios.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `EncryptionServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento cifrado de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Determine el tipo de cifrado.

   * Determine el tipo de cifrado invocando el método `getPDFEncryption` del objeto `EncryptionServiceClient` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Invoque el método `getEncryptionType` del objeto `EncryptionTypeResult`. Este método devuelve un valor de enumeración `EncryptionType` que especifica el tipo de cifrado. Por ejemplo, si el documento de PDF está protegido con cifrado basado en contraseña, este método devuelve `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Determinación del tipo de cifrado mediante la API de Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar el tipo de cifrado mediante la API de servicio web {#determine-the-encryption-type-using-the-web-service-api}

Determine el tipo de cifrado que protege un documento de PDF mediante la API de cifrado (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicios.

   * Cree un objeto `EncryptionServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `EncryptionServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `EncryptionServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento cifrado de PDF.

   * Crear un objeto `BLOB` mediante su constructor.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF cifrado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando el contenido de la matriz de bytes al miembro de datos `MTOM` del objeto `BLOB`.

1. Determine el tipo de cifrado.

   * Invoque el método `getPDFEncryption` del objeto `EncryptionServiceClient` y pase el objeto `BLOB` que contiene el documento de PDF. Este método devuelve un objeto `EncryptionTypeResult`.
   * Obtenga el valor del método de datos `encryptionType` del objeto `EncryptionTypeResult`. Por ejemplo, si el documento de PDF está protegido con cifrado basado en contraseña, el valor de este miembro de datos es `EncryptionType.PASSWORD`.

**Consulte también**

[Resumen de los pasos](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
