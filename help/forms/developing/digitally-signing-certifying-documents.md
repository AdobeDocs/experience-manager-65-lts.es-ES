---
title: 'Firmar y certificar documentos digitalmente '
description: Utilice el servicio Signature para agregar y eliminar campos de firma digital en un documento de PDF, recuperar los nombres de los campos de firma en un documento de PDF, modificar los campos de firma, firmar digitalmente documentos de PDF, certificar documentos de PDF, validar firmas digitales en un documento de PDF, validar todas las firmas digitales de un documento de PDF y quitar una firma digital de un campo de firma.
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 30ed51ad-4f69-41eb-9fca-d29d644aa4ba
source-git-commit: 9a11887b6bb8446772e5a41246da1023f40ce507
workflow-type: tm+mt
source-wordcount: '16909'
ht-degree: 3%

---

# Firmar y certificar documentos digitalmente  {#digitally-signing-and-certifying-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Signature**

El servicio Signature permite a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos. Dado que las características de seguridad se aplican al propio documento, este permanece seguro y controlado durante todo su ciclo de vida. Un documento permanece seguro más allá del cortafuegos, cuando se descarga sin conexión y cuando se devuelve a su organización.

>[!NOTE]
>
>Puede crear un controlador de firma personalizado para el servicio Signature que se invoca cuando se invocan determinadas operaciones, como firmar un documento de PDF.

**Nombres de campos de firma**

Algunas operaciones del servicio Signature requieren que especifique el nombre del campo de firma en el que se realiza una operación. Por ejemplo, al firmar un documento de PDF, especifique el nombre del campo de firma que desea firmar. Supongamos que el nombre completo de un campo de firma es `form1[0].Form1[0].SignatureField1[0]`. Puede especificar `SignatureField1[0]` en lugar de `form1[0].Form1[0].SignatureField1[0]`.

A veces, un conflicto hace que el servicio de firma firme (o realice otra operación que requiera el nombre del campo de firma) el campo incorrecto. Este conflicto se debe a que el nombre `SignatureField1[0]` aparece en dos o más lugares del mismo documento de PDF. Por ejemplo, considere un documento de PDF que contiene dos campos de firma denominados `form1[0].Form1[0].SignatureField1[0]` y `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` y especifique `SignatureField1[0]`. En este caso, el servicio de firma firma el primer campo de firma que encuentra al repetir todos los campos de firma del documento.

Si hay varios campos de firma ubicados dentro de un documento de PDF, se recomienda especificar los nombres completos de los campos de firma. Es decir, especifique `form1[0].Form1[0].SignatureField1[0]` en lugar de `SignatureField1[0]`.

Puede realizar estas tareas utilizando el servicio Signature:

* Agregar y eliminar campos de firma digital en un documento de PDF. (Consulte [Agregar campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupere los nombres de los campos de firma en un documento de PDF. (Consulte [Recuperación de nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modificar campos de firma. (Consulte [Modificar campos de firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Firmar digitalmente documentos de PDF. (Consulte [Firmar digitalmente documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certificar documentos de PDF. (Consulte [Certificar documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Validar firmas digitales en un documento de PDF. (Consulte [Verificación de firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Validar todas las firmas digitales de un documento de PDF. (Consulte [Verificar varias firmas digitales](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Quitar una firma digital de un campo de firma. (Consulte [Quitar firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Adición de campos de firma {#adding-signature-fields}

Las firmas digitales aparecen en los campos de firma, que son campos de formulario que contienen una representación gráfica de la firma. Los campos de firma pueden ser visibles o invisibles. Los firmantes pueden utilizar un campo de firma preexistente o se puede agregar un campo de firma mediante programación. En cualquier caso, el campo de firma debe existir antes de que se pueda firmar un documento de PDF.

Puede agregar mediante programación un campo de firma mediante la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar más de un campo de firma a un documento de PDF; sin embargo, cada nombre de campo de firma debe ser único.

>[!NOTE]
>
>Algunos tipos de documento de PDF no permiten agregar mediante programación un campo de firma. Para obtener más información acerca del servicio Signature y la adición de campos de firma, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para agregar un campo de firma a un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga un documento de PDF al que se agregue un campo de firma.
1. Agregue un campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de firma**

Para poder realizar mediante programación una operación del servicio Signature, debe crear un cliente del servicio Signature.

**Obtener un documento de PDF al que se agrega un campo de firma**

Obtenga un documento de PDF al que se agregue un campo de firma.

**Agregar un campo de firma**

Para agregar correctamente un campo de firma a un documento de PDF, especifique valores de coordenadas que identifiquen la ubicación del campo de firma. (Si agrega un campo de firma invisible, estos valores no son obligatorios). Además, puede especificar qué campos del documento de PDF están bloqueados después de aplicar una firma al campo de firma.

**Guardar el documento de PDF como archivo de PDF**

Una vez que el servicio Signature agrega un campo de firma al documento de PDF, puede guardar el documento como un archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Añadir campos de firma mediante la API de Java {#add-signature-fields-using-the-java-api}

Agregar un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtener un documento de PDF al que se agregue un campo de firma

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF al que se agrega un campo de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Agregar un campo de firma

   * Cree un objeto `PositionRectangle` que especifique la ubicación del campo de firma mediante su constructor. En el constructor, especifique los valores de coordenadas.
   * Si lo desea, cree un objeto `FieldMDPOptions` que especifique los campos que se bloquearán cuando se aplique una firma digital al campo de firma.
   * Agregue un campo de firma a un documento de PDF invocando el método `SignatureServiceClient` del objeto `addSignatureField` y pasando los siguientes valores:

      * A `com.adobe.idp`. `Document` objeto que representa el documento de PDF al que se agrega un campo de firma.
      * Valor de cadena que especifica el nombre del campo de firma.
      * Valor `java.lang.Integer` que representa el número de página al que se agrega un campo de firma.
      * Un objeto `PositionRectangle` que especifica la ubicación del campo de firma.
      * Un objeto `FieldMDPOptions` que especifica campos en el documento de PDF que están bloqueados después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y puede pasar `null`.

   * Un objeto `PDFSeedValueOptions` que especifica varios valores en tiempo de ejecución. Este valor de parámetro es opcional y puede pasar `null`.

     El método `addSignatureField` devuelve un `com.adobe.idp`. `Document` objeto que representa un documento de PDF que contiene un campo de firma.

   >[!NOTE]
   >
   >Puede invocar el método `SignatureServiceClient` del objeto `addInvisibleSignatureField` para agregar un campo de firma invisible.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el `com.adobe.idp`. El método `Document` del objeto `copyToFile` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar `com.adobe.idp`. Objeto `Document` devuelto por el método `addSignatureField`.

**Consulte también**

[Inicios rápidos de API de Signature Service](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Agregar campos de firma mediante la API de servicio web {#add-signature-fields-using-the-web-service-api}

Para agregar un campo de firma mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtener un documento de PDF al que se agregue un campo de firma

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF que contendrá un campo de firma.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Agregar un campo de firma

   Agregue un campo de firma al documento de PDF invocando el método `SignatureServiceClient` del objeto `addSignatureField` y pasando los siguientes valores:

   * Un objeto `BLOB` que representa el documento de PDF al que se agrega un campo de firma.
   * Valor de cadena que especifica el nombre del campo de firma.
   * Valor entero que representa el número de página al que se agrega un campo de firma.
   * Un objeto `PositionRect` que especifica la ubicación del campo de firma.
   * Un objeto `FieldMDPOptions` que especifica campos en el documento de PDF que están bloqueados después de aplicar una firma digital al campo de firma. Este valor de parámetro es opcional y puede pasar `null`.
   * Un objeto `PDFSeedValueOptions` que especifica varios valores en tiempo de ejecución. Este valor de parámetro es opcional y puede pasar `null`.

   El método `addSignatureField` devuelve un objeto `BLOB` que representa un documento de PDF que contiene un campo de firma.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `addSignatureField`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando nombres de campos de firma {#retrieving-signature-field-names}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que están en un documento de PDF o desea verificarlos, puede recuperarlos mediante programación. El servicio Firma devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-1}

Para recuperar los nombres de los campos de firma, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que contiene campos de firma.
1. Recupere los nombres de los campos de firma.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar mediante programación una operación del servicio Signature, debe crear un cliente del servicio Signature.

**Obtener el documento de PDF que contiene campos de firma**

Recupere un documento de PDF que contenga campos de firma.

**Recuperar los nombres de los campos de firma**

Puede recuperar los nombres de los campos de firma después de recuperar un documento de PDF que contenga uno o varios campos de firma.

**Consulte también**

[Recuperar nombres de campos de firma mediante la API de Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar el campo de firma mediante la API de servicio web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nombres de campos de firma mediante la API de Java {#retrieve-signature-field-names-using-the-java-api}

Recupere los nombres de los campos de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que contiene campos de firma

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que contiene campos de firma utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Recuperar los nombres de los campos de firma

   * Recupere los nombres de los campos de firma invocando el método `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de PDF que contiene los campos de firma. Este método devuelve un objeto `java.util.List`, en el que cada elemento contiene un objeto `PDFSignatureField`. Con este objeto, puede obtener información adicional sobre un campo de firma, como si está visible.
   * Recorra en iteración el objeto `java.util.List` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento de PDF, puede obtener un objeto `PDFSignatureField` independiente. Para obtener el nombre del campo de firma, invoque el método `PDFSignatureField` del objeto `getName`. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperando nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Inicio rápido (modo SOAP): Recuperación de nombres de campos de firma mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar el campo de firma mediante la API de servicio web {#retrieve-signature-field-using-the-web-service-api}

Recupere los nombres de los campos de firma mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que contiene campos de firma

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF que contiene campos de firma.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` al contenido de la matriz de bytes.

1. Recuperar los nombres de los campos de firma

   * Recupere los nombres de los campos de firma invocando el método `SignatureServiceClient` del objeto `getSignatureFieldList` y pasando el objeto `BLOB` que contiene el documento de PDF que contiene los campos de firma. Este método devuelve un objeto de colección `MyArrayOfPDFSignatureField` donde cada elemento contiene un objeto `PDFSignatureField`.
   * Recorra en iteración el objeto `MyArrayOfPDFSignatureField` para determinar si hay nombres de campo de firma. Para cada campo de firma del documento de PDF, puede obtener un objeto `PDFSignatureField`. Para obtener el nombre del campo de firma, invoque el método `PDFSignatureField` del objeto `getName`. Este método devuelve un valor de cadena que especifica el nombre del campo de firma.

**Consulte también**

[Recuperando nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificación de campos de firma {#modifying-signature-fields}

Puede modificar los campos de firma que se encuentran en un documento de PDF mediante la API de Java y la API del servicio web. La modificación de un campo de firma implica la manipulación de sus valores del diccionario de bloqueo de campos de firma o valores del diccionario de valores de semillas.

Un *diccionario de bloqueo de campos* especifica una lista de campos que se bloquearán cuando se firme en el campo de firma. Un campo bloqueado impedirá que los usuarios realicen cambios en el campo. Un *diccionario de valores de inicialización* contiene información de restricción que se usa en el momento en que se aplica la firma. Por ejemplo, puede cambiar los permisos que controlan las acciones que se pueden producir sin invalidar una firma.

Si modifica un campo de firma existente, podrá cambiar el documento de PDF para reflejar los cambios en los requisitos empresariales. Por ejemplo, un requisito empresarial nuevo puede requerir bloquear todos los campos del documento después de firmarlo.

En esta sección se explica cómo modificar un campo de firma mediante la modificación de los valores del diccionario de bloqueo de campos y del diccionario de valores semilla. Los cambios realizados en el diccionario de bloqueo de campos de firma hacen que todos los campos del documento de PDF se bloqueen cuando se firma un campo de firma. Los cambios realizados en el diccionario de valores semilla prohíben tipos específicos de cambios en el documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio Signature y la modificación de los campos de firma, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para modificar los campos de firma en un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que contiene el campo de firma que desea modificar.
1. Establecer valores de diccionario.
1. Modifique el campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar mediante programación una operación del servicio Signature, debe crear un cliente del servicio Signature.

**Obtenga el documento de PDF que contiene el campo de firma que desea modificar**

Recupere un documento de PDF que contenga el campo de firma que desea modificar.

**Establecer valores de diccionario**

Para modificar un campo de firma, asigne valores a su diccionario de bloqueo de campos o diccionario de valores semilla. Especificar los valores del diccionario de bloqueo de campos de firma implica especificar los campos de documento de PDF que están bloqueados cuando se firma el campo de firma. (En esta sección se explica cómo bloquear todos los campos.)

Se pueden configurar los siguientes valores de diccionario de valores semilla:

* **Comprobación de revisión**: Especifica si se realiza una comprobación de revocación cuando se aplica una firma al campo de firma.
* **Opciones de certificado**: asigna valores al diccionario de valores de inicialización del certificado. Antes de especificar opciones de certificado, se recomienda familiarizarse con un diccionario de valores semilla de certificado.
* **Opciones de resumen**: Asigna los algoritmos de resumen que se usan para firmar. Los valores válidos son SHA1, SHA256, SHA384, SHA512 y RIPEMD160.
* **Filtro**: especifica el filtro que se usa con el campo de firma. Por ejemplo, puede utilizar el filtro Adobe.PPKLite.
* **Opciones de marca**: especifica los valores de marca asociados con este campo de firma. Un valor de 1 significa que un firmante solo debe utilizar los valores especificados para la entrada. Un valor de 0 significa que se permiten otros valores. Estas son las posiciones de bits:

   * **1(Filtro):** Controlador de firma que se utilizará para firmar el campo de firma
   * **2 (subfiltro):** Matriz de nombres que indica codificaciones aceptables para usar al firmar
   * **3 (V)**: El número de versión mínimo requerido del controlador de firma que se utilizará para firmar el campo de firma
   * **4 (Motivos):** Matriz de cadenas que especifica posibles motivos para firmar un documento
   * **5 (PDFLegalWarnings):** Una matriz de cadenas que especifica posibles autenticaciones legales

* **Autenticaciones legales**: cuando se certifica un documento, se analiza automáticamente para detectar tipos de contenido específicos que pueden hacer que el contenido visible de un documento sea ambiguo o engañoso. Por ejemplo, una anotación puede oscurecer el texto que es importante para comprender qué se certifica. El proceso de digitalización genera advertencias que indican la presencia de este tipo de contenido. También proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Permisos**: especifica los permisos que se pueden usar en un documento de PDF sin invalidar la firma.
* **Motivos**: especifica los motivos por los que se debe firmar este documento.
* **Marca de tiempo**: Especifica las opciones de marca de tiempo. Por ejemplo, puede establecer la dirección URL del servidor de marca de tiempo que se utiliza.
* **Versión**: especifica el número mínimo de versión del controlador de firma que se utilizará para firmar el campo de firma.

**Modificar el campo de firma**

Después de crear un cliente de servicio de firma, recuperar el documento de PDF que contiene el campo de firma que desea modificar y establecer los valores del diccionario, puede indicar al servicio de firma que modifique el campo de firma. A continuación, el servicio Signature devolverá un documento de PDF que contiene el campo de firma modificado. El documento original de PDF no se ve afectado.

**Guardar el documento de PDF como archivo de PDF**

Guarde el documento de PDF que contiene el campo de firma modificado como archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de Signature Service](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digital de documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificación de los campos de firma mediante la API de Java {#modify-signature-fields-using-the-java-api}

Modificar un campo de firma mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que contiene el campo de firma que desea modificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que contiene el campo de firma que se va a modificar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer valores de diccionario

   * Crear un objeto `PDFSignatureFieldProperties` mediante su constructor. Un objeto `PDFSignatureFieldProperties` almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla.
   * Crear un objeto `PDFSeedValueOptionSpec` mediante su constructor. Este objeto permite definir los valores del diccionario de valores semilla.
   * No permitir cambios en el documento de PDF invocando el método `PDFSeedValueOptionSpec` del objeto `setMdpValue` y pasando el valor de enumeración `MDPPermissions.NoChanges`.
   * Crear un objeto `FieldMDPOptionSpec` mediante su constructor. Este objeto permite establecer los valores del diccionario de bloqueo de campos de firma.
   * Bloquee todos los campos del documento de PDF invocando el método `FieldMDPOptionSpec` del objeto `setMdpValue` y pasando el valor de enumeración `FieldMDPAction.ALL`.
   * Para establecer la información del diccionario de valores de inicialización, invoque el método `PDFSignatureFieldProperties` del objeto `setSeedValue` y pase el objeto `PDFSeedValueOptionSpec`.
   * Establezca la información del diccionario de bloqueo de campos de firma invocando el método `PDFSignatureFieldProperties` del objeto `setFieldMDP` y pasando el objeto `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Para ver todos los valores de diccionario de valores semilla que puede establecer, consulte la referencia de clase `PDFSeedValueOptionSpec`. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificación del campo de firma

   Modifique el campo de firma invocando el método `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que almacena el documento de PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El objeto `PDFSignatureFieldProperties` que almacena la información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla

   El método `modifySignatureField` devuelve un objeto `com.adobe.idp.Document` que almacena un documento de PDF que contiene el campo de firma modificado.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que devolvió el método `modifySignatureField`.

### Modificación de los campos de firma mediante la API de servicio web {#modify-signature-fields-using-the-web-service-api}

Modificar un campo de firma mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que contiene el campo de firma que desea modificar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF que contiene el campo de firma que se va a modificar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.

1. Establecer valores de diccionario

   * Crear un objeto `PDFSignatureFieldProperties` mediante su constructor. Este objeto almacena información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla.
   * Crear un objeto `PDFSeedValueOptionSpec` mediante su constructor. Este objeto permite definir los valores del diccionario de valores semilla.
   * No permitir cambios en el documento de PDF asignando el valor de enumeración `MDPPermissions.NoChanges` al miembro de datos `PDFSeedValueOptionSpec` del objeto `mdpValue`.
   * Crear un objeto `FieldMDPOptionSpec` mediante su constructor. Este objeto permite establecer los valores del diccionario de bloqueo de campos de firma.
   * Bloquee todos los campos del documento de PDF asignando el valor de enumeración `FieldMDPAction.ALL` al miembro de datos `FieldMDPOptionSpec` del objeto `mdpValue`.
   * Para establecer la información del diccionario de valores semilla, asigne el objeto `PDFSeedValueOptionSpec` al miembro de datos `PDFSignatureFieldProperties` del objeto `seedValue`.
   * Establezca la información del diccionario de bloqueo de campos de firma asignando el objeto `FieldMDPOptionSpec` al miembro de datos `PDFSignatureFieldProperties` del objeto `fieldMDP`.

   >[!NOTE]
   >
   >Para ver todos los valores de diccionario de valores semilla que puede establecer, consulte la referencia de clase `PDFSeedValueOptionSpec`. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificación del campo de firma

   Modifique el campo de firma invocando el método `SignatureServiceClient` del objeto `modifySignatureField` y pasando los siguientes valores:

   * El objeto `BLOB` que almacena el documento de PDF que contiene el campo de firma que se va a modificar
   * Un valor de cadena que especifica el nombre del campo de firma
   * El objeto `PDFSignatureFieldProperties` que almacena la información del diccionario de bloqueo de campos de firma y del diccionario de valores semilla

   El método `modifySignatureField` devuelve un objeto `BLOB` que almacena un documento de PDF que contiene el campo de firma modificado.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que contendrá el campo de firma y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` que devuelve el método `addSignatureField`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de documentos de PDF {#digitally-signing-pdf-documents}

Las firmas digitales se pueden aplicar a documentos PDF para proporcionar cierto nivel de seguridad. Las firmas digitales, como las firmas manuscritas, proporcionan un medio para que los firmantes se identifiquen y hagan declaraciones sobre un documento. La tecnología utilizada para firmar documentos digitalmente ayuda a garantizar que tanto el firmante como los destinatarios tengan una idea clara de lo que se firmó y estén seguros de que el documento no se ha alterado desde que se firmó.

Los documentos PDF se firman mediante tecnología de clave pública. Un firmante tiene dos claves: una clave pública y una clave privada. La clave privada se almacena en las credenciales de un usuario, que deben estar disponibles en el momento de la firma. La clave pública se almacenará en el certificado del usuario, que deberá estar disponible para que los destinatarios validen la firma. La información sobre los certificados revocados se encuentra en las listas de revocación de certificados (CRL) y en las respuestas del Protocolo de estado de certificado en línea (OCSP) distribuidas por las autoridades de certificación (CA). La hora de la firma se puede obtener de una fuente de confianza conocida como Autoridad de marca de tiempo.

>[!NOTE]
>
>Para poder firmar digitalmente un documento de PDF, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API de Administrador de confianza. (Consulte [Importación de credenciales mediante la API del Administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Mediante programación, puede firmar digitalmente documentos de PDF. Al firmar digitalmente un documento de PDF, debe hacer referencia a una credencial de seguridad que exista en AEM Forms. La credencial es la clave privada que se utiliza para la firma.

El servicio Signature realiza los siguientes pasos cuando se firma un documento de PDF:

1. El servicio Signature recupera la credencial del almacén de confianza pasando el alias especificado en la solicitud.
1. Truststore busca las credenciales especificadas.
1. La credencial se devuelve al servicio Signature y se utiliza para firmar el documento. La credencial también se almacena en caché con el alias para solicitudes futuras.

Para obtener información sobre cómo administrar las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Existen diferencias entre firmar y certificar documentos. (Consulte [Certificar documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>No todos los documentos de PDF admiten la firma. Para obtener más información acerca del servicio Signature y los documentos de firma digital, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>El servicio Signature no admite archivos XDP con datos de PDF incrustados como entrada para una operación, como la certificación de un documento. Esta acción provoca que el servicio Signature emita un `PDFOperationException`. Para resolver este problema, convierta el archivo XDP en un archivo PDF mediante el servicio Utilidades de PDF y, a continuación, pase el archivo PDF convertido a una operación del servicio Signature. (Consulte [Uso de utilidades PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credencial HSM de Cipher nShield**

Cuando se utiliza una credencial HSM de Cipher nShield para firmar o certificar un documento de PDF, la nueva credencial no se puede utilizar hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede definir un valor de configuración, lo que hace que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede añadir el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de añadir este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

    >[!NOTE]
    >
    > Se recomienda usar el comando &#39;Ctrl + C&#39; para reiniciar SDK. El reinicio de AEM SDK mediante métodos alternativos, como detener los procesos Java, puede generar incoherencias en el entorno de desarrollo de AEM.

**La firma no es de confianza**

Al certificar y firmar el mismo documento de PDF, si la firma certificadora no es de confianza, aparece un triángulo amarillo frente a la primera firma al abrir el documento de PDF en Acrobat o Adobe Reader. La firma certificadora debe ser de confianza para evitar esta situación.

**Firmar documentos basados en XFA**

Si intenta firmar un formulario basado en XFA utilizando la API del servicio de firma, es posible que falten los datos de `View` `Signed` `Version` en Acrobat. Por ejemplo, considere el siguiente flujo de trabajo:

* Al utilizar un archivo XDP creado con Designer, se combina un diseño de formulario que contiene un campo de firma y datos XML que contienen datos de formulario. El servicio Forms se utiliza para generar un documento interactivo de PDF.
* El documento de PDF se firma mediante la API del servicio de firma.

### Resumen de los pasos {#summary_of_steps-3}

Para firmar digitalmente un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Signature service.
1. Obtenga el documento de PDF para firmar.
1. Firme el documento de PDF.
1. Guarde el documento de PDF firmado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de firmas**

Para poder realizar mediante programación una operación del servicio Signature, debe crear un cliente del servicio Signature.

**Consiga el documento de PDF para firmar**

Para firmar un documento de PDF, debe obtener un documento de PDF que contenga un campo de firma. Si un documento de PDF no contiene un campo de firma, no se puede firmar. Se puede agregar un campo de firma mediante Designer o mediante programación.

**Firmar el documento de PDF**

Al firmar un documento de PDF, puede establecer las opciones en tiempo de ejecución que utiliza el servicio Signature. Puede establecer las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de tiempo

Las opciones de apariencia se establecen mediante un objeto `PDFSignatureAppearanceOptionSpec`. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el método `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` y pasando `true`.

También puede especificar si desea realizar o no una comprobación de revocación que determine si se ha revocado el certificado que se utiliza para firmar digitalmente un documento de PDF. Para realizar la comprobación de revocación, puede especificar uno de los siguientes valores:

* **NoCheck**: no realizar comprobación de revocación.
* **BestEffort**: Intente siempre comprobar la revocación de todos los certificados de la cadena. Si se produce algún problema en la comprobación, se asume que la revocación es válida. Si se produce algún error, suponga que el certificado no se ha revocado.
* **CheckIfAvailable:** Comprobar la revocación de todos los certificados de la cadena si la información de revocación está disponible. Si se produce algún problema en la comprobación, se asume que la revocación no es válida. Si se produce algún error, suponga que el certificado se ha revocado y no es válido. (Este es el valor predeterminado).
* **AlwaysCheck**: comprobar la revocación de todos los certificados de la cadena. Si la información de revocación no está presente en ningún certificado, se supone que la revocación no es válida.

Para realizar la comprobación de revocación en un certificado, puede especificar una dirección URL a un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si desea realizar la comprobación de revocación y no especifica una dirección URL a un servidor CRL, el servicio Signature obtiene la dirección URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de Protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte &quot;Protocolo de estado de certificado en línea&quot; en [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor de CRL y OCSP que utiliza el servicio Signature mediante Aplicaciones y servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL. (Consulte &quot;Administración de certificados y credenciales mediante el Almacén de confianza&quot; en la Ayuda de AAC).

Si especifica no realizar la comprobación de revocación, el servicio Signature no comprueba si se ha revocado el certificado utilizado para firmar o certificar un documento. Es decir, se omite la información del servidor CRL y OCSP.

>[!NOTE]
>
>Aunque se puede especificar una CRL o un servidor OCSP en el certificado, puede anular la URL especificada en el certificado mediante un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para invalidar el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de tiempo hace referencia al proceso de seguimiento de la hora en que se modificó un documento firmado o certificado. Una vez firmado un documento, no debe modificarse, ni siquiera por el propietario del documento. La marca de tiempo ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer opciones de marca de tiempo mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de tiempo (TSP).

>[!NOTE]
>
>En las secciones Paseo por Java y servicio web y los inicios rápidos correspondientes, se utiliza la comprobación de revocación. Dado que no se especifica ninguna información del servidor CRL u OCSP, la información del servidor se obtiene del certificado utilizado para firmar digitalmente el documento de PDF.

Para firmar correctamente un documento de PDF, puede especificar el nombre completo del campo de firma que contendrá la firma digital, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`.

También debe hacer referencia a una credencial de seguridad para firmar digitalmente un documento de PDF. Para hacer referencia a una credencial de seguridad, especifique un alias. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con extensión .pfx) o un módulo de seguridad de hardware (HSM). Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

**Guardar el documento de PDF firmado**

Una vez que el servicio Signature haya firmado digitalmente el documento de PDF, puede guardarlo como archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Firmar digitalmente documentos de PDF mediante la API de Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digital de documentos de PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperando nombres de campos de firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firmar digitalmente documentos de PDF mediante la API de Java {#digitally-sign-pdf-documents-using-the-java-api}

Firmar digitalmente un documento de PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firmas

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF para firmar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF para firmar digitalmente utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Firmar el documento de PDF

   Firme el documento de PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF que se va a firmar.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un objeto `Credential` que representa la credencial que se usa para firmar digitalmente el documento de PDF. Cree un objeto `Credential` invocando el método `Credential` estático del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash que se utilizará para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor de cadena que representa el motivo por el que el documento de PDF se firmó digitalmente.
   * Valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `java.lang.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante.
   * Un objeto `OCSPOptionSpec` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   El método `sign` devuelve un objeto `com.adobe.idp.Document` que representa el documento de PDF firmado.

1. Guardar el documento de PDF firmado

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` y pase `java.io.File` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `sign`.

**Consulte también**

[Firma digital de documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Inicio rápido (modo SOAP): firmar digitalmente un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digital de documentos de PDF mediante la API de servicio web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para firmar digitalmente un documento de PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firmas

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF para firmar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF firmado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que se va a firmar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.

1. Firmar el documento de PDF

   Firme el documento de PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * Un objeto `BLOB` que representa el documento de PDF que se va a firmar.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma digital.
   * Un objeto `Credential` que representa la credencial que se usa para firmar digitalmente el documento de PDF. Cree un objeto `Credential` mediante su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash que se utilizará para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor booleano que especifica si se utiliza el algoritmo hash.
   * Valor de cadena que representa el motivo por el que el documento de PDF se firmó digitalmente.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `System.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si se realiza esta comprobación de revocación, está incrustada en la firma. El valor predeterminado es `false`.
   * Un objeto `OCSPOptionSpec` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información acerca de este objeto, vea [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `BLOB` que representa el documento de PDF firmado.

1. Guardar el documento de PDF firmado

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Firma digital de documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digital de Forms interactivo {#digitally-signing-interactive-forms}

Puede firmar un formulario interactivo que crea el servicio de Forms. Por ejemplo, considere el siguiente flujo de trabajo:

* Puede combinar un formulario PDF basado en XFA creado mediante Designer y datos de formulario en un documento XML utilizando el servicio Forms. El servidor de Forms procesa un formulario interactivo.
* El formulario interactivo se firma mediante la API del servicio de firma.

El resultado es un formulario PDF interactivo firmado digitalmente. Al firmar un formulario de PDF basado en un formulario XFA, asegúrese de guardar el archivo de PDF como un formulario de PDF estático de Adobe. Si intenta firmar un formulario de PDF guardado como formulario de Adobe Dynamic PDF, se producirá una excepción. Dado que está firmando el formulario devuelto por el servicio Forms, asegúrese de que el formulario contenga un campo de firma.

>[!NOTE]
>
>Para poder firmar digitalmente un formulario interactivo, debe asegurarse de agregar el certificado a AEM Forms. Se agrega un certificado mediante la consola de administración o mediante programación mediante la API de Administrador de confianza. (Consulte [Importación de credenciales mediante la API del Administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Al usar la API del servicio Forms, establezca la opción de tiempo de ejecución `GenerateServerAppearance` en `true`. Esta opción en tiempo de ejecución garantiza que el aspecto del formulario generado en el servidor siga siendo válido cuando se abra en Acrobat o Adobe Reader. Se recomienda establecer esta opción en tiempo de ejecución al generar un formulario interactivo para firmar mediante la API de Forms.

>[!NOTE]
>
>Antes de leer Firma digital interactiva de Forms, se recomienda estar familiarizado con la firma de documentos de PDF. (Consulte [Firmar digitalmente documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Resumen de los pasos {#summary_of_steps-4}

Para firmar digitalmente un formulario interactivo que devuelve el servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Forms y firmas.
1. Obtenga el formulario interactivo mediante el servicio de Forms.
1. Firme el formulario interactivo.
1. Guarde el documento de PDF firmado como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de Forms y firmas**

Dado que este flujo de trabajo invoca tanto Forms como Signature services, cree un cliente de servicio de Forms y un cliente de servicio de Signature.

**Obtenga el formulario interactivo mediante el servicio de Forms**

Puede utilizar el servicio Forms para obtener el formulario interactivo de PDF que desea firmar. A partir de AEM Forms, puede pasar un objeto `com.adobe.idp.Document` al servicio Forms que contiene el formulario que se va a procesar. El nombre de este método es `renderPDFForm2`. Este método devuelve un objeto `com.adobe.idp.Document` que contiene el formulario que se va a firmar. Puede pasar esta instancia de `com.adobe.idp.Document` al servicio Signature.

Del mismo modo, si utiliza servicios web, puede pasar la instancia `BLOB` que el servicio Forms devuelve al servicio Signature.

>[!NOTE]
>
>El inicio rápido asociado a la sección Firma digital de Forms interactivo invoca el método `renderPDFForm2`.

**Firmar el formulario interactivo**

Al firmar un documento de PDF, puede establecer las opciones en tiempo de ejecución que utiliza el servicio Signature. Puede establecer las siguientes opciones:

* Opciones de aspecto
* Comprobación de revocación
* Valores de marca de tiempo

Las opciones de apariencia se establecen mediante un objeto `PDFSignatureAppearanceOptionSpec`. Por ejemplo, puede mostrar la fecha dentro de una firma invocando el método `PDFSignatureAppearanceOptionSpec` del objeto `setShowDate` y pasando `true`.

**Guardar el documento de PDF firmado**

Una vez que el servicio Signature haya firmado digitalmente el documento de PDF, puede guardarlo como archivo de PDF. El archivo PDF se puede abrir en Acrobat o Adobe Reader.

**Consulte también**

[Firmar digitalmente un formulario interactivo con la API de Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firmar digitalmente un formulario interactivo mediante la API de servicio web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digital de documentos de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firmar digitalmente un formulario interactivo con la API de Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firme digitalmente un formulario interactivo con Forms y la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar y adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un cliente de Forms y firmas

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtención del formulario interactivo mediante el servicio de Forms

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a pasar al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.
   * Cree un objeto `java.io.FileInputStream` que represente el documento XML que contiene los datos de formulario para pasarlos al servicio Forms mediante su constructor. Pase un valor de cadena que especifique la ubicación del archivo XML.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.
   * Cree un objeto `PDFFormRenderSpec` que se use para establecer opciones en tiempo de ejecución. Invoque el método `PDFFormRenderSpec` del objeto `setGenerateServerAppearance` y pase `true`.
   * Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * Objeto `com.adobe.idp.Document` que contiene el formulario de PDF que se va a procesar.
      * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario.
      * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
      * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

     El método `renderPDFForm2` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario

   * Recupere el formulario de PDF invocando el método `FormsResult` del objeto `getOutputContent`. Este método devuelve un objeto `com.adobe.idp.Document` que representa el formulario interactivo.

1. Firma del formulario interactivo

   Firme el documento de PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF que se va a firmar. Asegúrese de que este objeto sea el objeto `com.adobe.idp.Document` obtenido del servicio Forms.
   * Valor de cadena que representa el nombre del campo de firma firmado.
   * Un objeto `Credential` que representa la credencial que se usa para firmar digitalmente el documento de PDF. Cree un objeto `Credential` invocando el método `Credential` estático del objeto `getInstance`. Pase un valor de cadena que especifique el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash que se utilizará para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor de cadena que representa el motivo por el que el documento de PDF se firmó digitalmente.
   * Valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `java.lang.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante.
   * Un objeto `OCSPPreferences` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `com.adobe.idp.Document` que representa el documento de PDF firmado.

1. Guardar el documento de PDF firmado

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del nombre del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` y pase `java.io.File` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` que devolvió el método `sign`.

**Consulte también**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Inicio rápido (modo SOAP): firmar digitalmente un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firmar digitalmente un formulario interactivo mediante la API de servicio web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firme digitalmente un formulario interactivo con Forms y la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición de WSDL para la referencia de servicio asociada al servicio Signature: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Dado que el tipo de datos `BLOB` es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` al utilizarlo. En el inicio rápido del servicio web correspondiente, todas las instancias de `BLOB` están completamente calificadas.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Creación de un cliente de Forms y firmas

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el cliente de servicio de Forms.

1. Obtención del formulario interactivo mediante el servicio de Forms

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF firmado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que se va a firmar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.
   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar datos de formulario.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo XML que contiene los datos del formulario y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.
   * Cree un objeto `PDFFormRenderSpec` que se use para establecer opciones en tiempo de ejecución. Asigne el valor `true` al campo `PDFFormRenderSpec` del objeto `generateServerAppearance`.
   * Invoque el método `FormsServiceClient` del objeto `renderPDFForm2` y pase los siguientes valores:

      * Objeto `BLOB` que contiene el formulario de PDF que se va a procesar.
      * Objeto `BLOB` que contiene datos para combinar con el formulario.
      * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
      * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms. Puede especificar `null` para este valor de parámetro.
      * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
      * Un parámetro de salida largo utilizado para almacenar el número de páginas en el formulario.
      * Un parámetro de salida de cadena que se utiliza para el valor de configuración regional.
      * Un valor `FormResult` que es un parámetro de salida que se usa para almacenar el formulario interactivo.

   * Recupere el formulario de PDF invocando el campo `FormsResult` del objeto `outputContent`. Este campo almacena un objeto `BLOB` que representa el formulario interactivo.

1. Firma del formulario interactivo

   Firme el documento de PDF invocando el método `SignatureServiceClient` del objeto `sign` y pasando los siguientes valores:

   * Un objeto `BLOB` que representa el documento de PDF que se va a firmar. Utilice la instancia `BLOB` devuelta por el servicio Forms.
   * Valor de cadena que representa el nombre del campo de firma firmado.
   * Un objeto `Credential` que representa la credencial que se usa para firmar digitalmente el documento de PDF. Cree un objeto `Credential` mediante su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash que se utilizará para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor booleano que especifica si se utiliza el algoritmo hash.
   * Valor de cadena que representa el motivo por el que el documento de PDF se firmó digitalmente.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma digital. Por ejemplo, puede utilizar este objeto para agregar un logotipo personalizado a una firma digital.
   * Un objeto `System.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si se realiza esta comprobación de revocación, está incrustada en la firma. El valor predeterminado es `false`.
   * Un objeto `OCSPPreferences` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información acerca de este objeto, vea [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Este parámetro es opcional y puede ser `null`.

   El método `sign` devuelve un objeto `BLOB` que representa el documento de PDF firmado.

1. Guardar el documento de PDF firmado

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Firma digital de Forms interactivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificar documentos de PDF {#certifying-pdf-documents}

Puede proteger un documento PDF certificándolo con un tipo de firma concreto denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes maneras:

* Debe ser la primera firma aplicada al documento de PDF; es decir, en el momento en que se aplique la firma certificada, cualquier otro campo de firma del documento debe estar sin firmar. Solo se permite una firma certificada en un documento PDF. Si desea firmar y certificar un documento de PDF, debe certificarlo antes de firmarlo. Después de certificar un documento PDF, puede firmar digitalmente en los campos de firma adicionales.
* El autor o el creador del documento pueden especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada. Por ejemplo, el documento puede permitir rellenar formularios o hacer comentarios. Si el autor especifica que no se permite una modificación determinada, Acrobat impedirá que los usuarios modifiquen el documento de esa manera. Si se realizan dichas modificaciones, como por ejemplo utilizar otra aplicación, la firma certificada no será válida y Acrobat emitirá una advertencia cuando cualquier usuario abra el documento. (Con las firmas no certificadas no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).
* En el momento de la firma, el documento se analizará para detectar tipos de contenido específicos que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría complicar algún texto de una página que sea importante para comprender qué se certifica. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

Puede certificar documentos de PDF mediante programación utilizando la API de Java del servicio de firma o la API del servicio web de firma. Al certificar un documento de PDF, debe hacer referencia a una credencial de seguridad que exista en el servicio de credenciales. Para obtener información sobre las credenciales de seguridad, consulte la guía *Instalación e implementación de AEM Forms* para su servidor de aplicaciones.

>[!NOTE]
>
>Al certificar y firmar el mismo documento de PDF, si la firma de certificado no es de confianza, aparece un triángulo amarillo junto a la primera firma de firma al abrir el documento de PDF en Acrobat o Adobe Reader. La firma certificadora debe ser de confianza para evitar esta situación.

>[!NOTE]
>
>Cuando se utiliza una credencial HSM de Cipher nShield para firmar o certificar un documento de PDF, la nueva credencial no se puede utilizar hasta que se reinicie el servidor de aplicaciones J2EE en el que se implementa AEM Forms. Sin embargo, puede definir un valor de configuración, lo que hace que la operación de firma o certificación funcione sin reiniciar el servidor de aplicaciones J2EE.

Puede añadir el siguiente valor de configuración en el archivo cknfastrc, que se encuentra en /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Después de añadir este valor de configuración al archivo cknfastrc, la nueva credencial se puede utilizar sin reiniciar el servidor de aplicaciones J2EE.

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature y la certificación de un documento, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-5}

Para certificar un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que desea certificar.
1. Certifique el documento de PDF.
1. Guarde el documento certificado de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar mediante programación una operación Signature, debe crear un cliente Signature.

**Obtenga el documento de PDF para certificar**

Para certificar un documento de PDF, debe obtener un documento de PDF que contenga un campo de firma. Si un documento de PDF no contiene un campo de firma, no se puede certificar. Se puede agregar un campo de firma mediante Designer o mediante programación. Para obtener información acerca de cómo agregar mediante programación un campo de firma, vea [Agregar campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar el documento de PDF**

Para certificar correctamente un documento de PDF, necesita los siguientes valores de entrada que utiliza el servicio Signature para certificar un documento de PDF:

* **documento de PDF**: documento de PDF que contiene un campo de firma, que es un campo de formulario que contiene una representación gráfica de la firma certificada. Un documento de PDF debe contener un campo de firma para poder certificarse. Se puede agregar un campo de firma mediante Designer o mediante programación. (Consulte [Agregar campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nombre de campo de firma**: el nombre completo del campo de firma certificado. El siguiente valor es un ejemplo: `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también se puede utilizar el nombre parcial del campo de firma: `SignatureField3[3]`. Si se pasa un valor nulo para el nombre del campo, se crea y certifica dinámicamente un campo de firma invisible.
* **Credencial de seguridad**: Una credencial que se usa para certificar el documento de PDF. Esta credencial de seguridad contiene una contraseña y un alias, que deben coincidir con un alias que aparezca en la credencial que se encuentra dentro del servicio de credenciales. El alias es una referencia a una credencial real que puede estar en un archivo PKCS#12 (con extensión .pfx) o un módulo de seguridad de hardware (HSM).
* **Algoritmo hash**: Algoritmo hash que se utilizará para asimilar el documento de PDF.
* **Motivo de la firma**: Valor que se muestra en Acrobat o Adobe Reader para que otros usuarios conozcan el motivo por el que se certificó el documento de PDF.
* **Ubicación del firmante**: La ubicación del firmante especificada por la credencial.
* **Información de contacto**: Información de contacto, como la dirección y el número de teléfono del firmante.
* **Información de permisos**: permisos que controlan las acciones que un usuario final puede realizar en un documento sin que la firma certificada no sea válida. Por ejemplo, puede establecer el permiso para que cualquier cambio en el documento de PDF haga que la firma certificada no sea válida.
* **Explicación legal**: cuando se certifica un documento, se analiza automáticamente en busca de tipos de contenido específicos que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría complicar algún texto de una página que sea importante para comprender qué se certifica. El proceso de digitalización genera advertencias sobre estos tipos de contenido. Este valor proporciona una explicación adicional del contenido que puede haber generado advertencias.
* **Opciones de apariencia**: opciones que controlan el aspecto de la firma certificada. Por ejemplo, la firma certificada puede mostrar información de fecha.
* **Comprobación de revocación**: Este valor especifica si se realiza la comprobación de revocación para el certificado del firmante. La configuración predeterminada de `false` significa que no se ha completado la comprobación de revocación.
* **Configuración de OCSP**: Configuración de la compatibilidad con el Protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se usa para certificar el documento de PDF. Por ejemplo, puede especificar la dirección URL del servidor que proporciona información sobre las credenciales que está utilizando para iniciar sesión en el documento de PDF.
* **Configuración de CRL**: Configuración de las preferencias de la lista de revocación de certificados (CRL) si se ha realizado la comprobación de revocación. Por ejemplo, puede especificar para comprobar siempre si se ha revocado una credencial.
* **Marca de tiempo**: Configuración que define la información de marca de tiempo aplicada a la firma certificada. Una marca de tiempo indica que se establecieron datos específicos antes de una hora determinada. Este conocimiento ayuda a crear una relación de confianza entre el firmante y el verificador.

**Guardar el documento certificado de PDF como archivo de PDF**

Una vez que el servicio Signature haya certificado el documento de PDF, puede guardarlo como archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Certificar documentos de PDF mediante la API de Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos de PDF mediante la API de servicio web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos de PDF mediante la API de Java {#certify-pdf-documents-using-the-java-api}

Certificar un documento de PDF mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que certificar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que desea certificar mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Certificar el documento de PDF

   Certifique el documento de PDF invocando el método `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que representa el documento de PDF que se certificará.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un objeto `Credential` que representa la credencial que se usa para certificar el documento de PDF. Cree un objeto `Credential` invocando el método `Credential` estático del objeto `getInstance` y pasando un valor de cadena que especifica el valor de alias que corresponde a la credencial de seguridad.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash utilizado para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor de cadena que representa el motivo por el que se certificó el documento de PDF.
   * Valor de cadena que representa la información de contacto del firmante.
   * Un objeto `MDPPermissions` que especifica las acciones que se pueden realizar en el documento de PDF que invalida la firma.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Si lo desea, modifique el aspecto de la firma invocando un método, como `setShowDate`.
   * Valor de cadena que proporciona una explicación de qué acciones invalidan la firma.
   * Un objeto `java.lang.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si se realiza esta comprobación de revocación, está incrustada en la firma. El valor predeterminado es `false`.
   * Un objeto `java.lang.Boolean` que especifica si el campo de firma que se certifica está bloqueado. Si el campo está bloqueado, el campo de firma está marcado como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios puede borrarlo. El valor predeterminado es `false`.
   * Un objeto `OCSPPreferences` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`. Para obtener información acerca de este objeto, vea [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Por ejemplo, después de crear un objeto `TSPPreferences`, puede establecer la dirección URL del servidor TSP invocando el método `TSPPreferences` del objeto `setTspServerURL`. Este parámetro es opcional y puede ser `null`. Para obtener más información, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   El método `certify` devuelve un objeto `com.adobe.idp.Document` que representa el documento certificado de PDF.

1. Guarde el documento certificado de PDF como archivo de PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo.

**Consulte también**

[Certificar documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Inicio rápido (modo SOAP): Certificación de un documento de PDF mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos de PDF mediante la API de servicio web {#certify-pdf-documents-using-the-web-service-api}

Certificar un documento de PDF mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que certificar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF certificado.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que se va a certificar y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su miembro de datos `MTOM` al contenido de la matriz de bytes.

1. Certificar el documento de PDF

   Certifique el documento de PDF invocando el método `SignatureServiceClient` del objeto `certify` y pasando los siguientes valores:

   * El objeto `BLOB` que representa el documento de PDF que se certificará.
   * Valor de cadena que representa el nombre del campo de firma que contendrá la firma.
   * Un objeto `Credential` que representa la credencial que se usa para certificar el documento de PDF. Cree un objeto `Credential` mediante su constructor y especifique el alias asignando un valor a la propiedad `Credential` del objeto `alias`.
   * Un objeto `HashAlgorithm` que especifica un miembro de datos estáticos que representa el algoritmo hash utilizado para asimilar el documento de PDF. Por ejemplo, puede especificar `HashAlgorithm.SHA1` para que use el algoritmo SHA1.
   * Valor booleano que especifica si se utiliza el algoritmo hash.
   * Valor de cadena que representa el motivo por el que se certificó el documento de PDF.
   * Valor de cadena que representa la ubicación del firmante.
   * Valor de cadena que representa la información de contacto del firmante.
   * Miembro de datos estáticos de un objeto `MDPPermissions` que especifica las acciones que se pueden realizar en el documento de PDF que invalidan la firma.
   * Valor booleano que especifica si se debe utilizar el objeto `MDPPermissions` pasado como valor de parámetro anterior.
   * Valor de cadena que explica qué acciones invalidan la firma.
   * Objeto `PDFSignatureAppearanceOptions` que controla el aspecto de la firma certificada. Crear un objeto `PDFSignatureAppearanceOptions` mediante su constructor. Puede modificar el aspecto de la firma estableciendo uno de sus miembros de datos.
   * Un objeto `System.Boolean` que especifica si se va a realizar la comprobación de revocación en el certificado del firmante. Si se realiza esta comprobación de revocación, está incrustada en la firma. El valor predeterminado es `false`.
   * Un objeto `System.Boolean` que especifica si el campo de firma que se certifica está bloqueado. Si el campo está bloqueado, el campo de firma está marcado como de solo lectura, sus propiedades no se pueden modificar y nadie que no tenga los permisos necesarios puede borrarlo. El valor predeterminado es `false`.
   * Un objeto `System.Boolean` que especifica si el campo de firma está bloqueado. Es decir, si pasa `true` al parámetro anterior, pase `true` a este parámetro.
   * Un objeto `OCSPPreferences` que almacena las preferencias de compatibilidad con el Protocolo de estado de certificado en línea (OCSP), que proporciona información sobre el estado de la credencial que se usa para certificar el documento de PDF. Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `CRLPreferences` que almacena las preferencias de la lista de revocación de certificados (CRL). Si no se realiza la comprobación de revocación, no se usa este parámetro y puede especificar `null`.
   * Objeto `TSPPreferences` que almacena las preferencias de compatibilidad con el proveedor de marcas de hora (TSP). Por ejemplo, después de crear un objeto `TSPPreferences`, puede establecer la dirección URL del TSP estableciendo el miembro de datos `TSPPreferences` del objeto `tspServerURL`. Este parámetro es opcional y puede ser `null`.

   El método `certify` devuelve un objeto `BLOB` que representa el documento certificado de PDF.

1. Guarde el documento certificado de PDF como archivo de PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que contendrá el documento de PDF certificado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `certify`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `binaryData`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Certificar documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificar firmas digitales {#verifying-digital-signatures}

Las firmas digitales se pueden verificar para garantizar que no se haya modificado un documento PDF firmado y que la firma digital sea válida. Al verificar una firma digital, puede comprobar el estado y las propiedades de la firma, como la identidad del firmante. Antes de confiar en una firma digital, se recomienda verificarla. Al verificar una firma digital, haga referencia a un documento de PDF que contenga una firma digital.

Supongamos que se desconoce la identidad del firmante. Cuando se abre el documento de PDF en Acrobat, un mensaje de advertencia indica que la identidad del firmante es desconocida, como se muestra en la siguiente ilustración.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Del mismo modo, cuando se comprueba una firma digital mediante programación, se puede determinar el estado de la identidad del firmante. Por ejemplo, si comprueba la firma digital en el documento mostrado en la ilustración anterior, el resultado sería que se desconoce la identidad del firmante.

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature y la comprobación de firmas digitales, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-6}

Para comprobar una firma digital, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que contiene la firma que desea comprobar.
1. Establecer las opciones de tiempo de ejecución de PKI.
1. Compruebe la firma digital.
1. Determine el estado de la firma.
1. Determine la identidad del firmante.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar mediante programación una operación del servicio Signature, cree un cliente del servicio Signature.

**Obtenga el documento de PDF que contiene la firma que desea comprobar**

Para comprobar una firma utilizada para firmar o certificar digitalmente un documento de PDF, obtenga un documento de PDF que contenga una firma.

**Establecer opciones de tiempo de ejecución de PKI**

Establezca estas opciones de tiempo de ejecución de PKI que utiliza el servicio Signature al comprobar firmas en un documento de PDF:

* Tiempo de verificación
* Comprobación de revocación
* Valores de marca de tiempo

Al configurar estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora del equipo del validador), lo que indica que se debe utilizar la hora actual. Para obtener información acerca de los distintos valores de tiempo, vea el valor de enumeración `VerificationTime` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información acerca de las opciones de comprobación de revocación, vea el valor de enumeración `RevocationCheckStyle` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una dirección URL a un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si no especifica una dirección URL al servidor CRL, el servicio de firma obtiene la dirección URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de Protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor de CRL y OCSP que utiliza el servicio Signature mediante Aplicaciones y servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se omite la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado usando un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para invalidar el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de tiempo es el proceso de rastrear la hora en que se modificó un documento firmado o certificado. Una vez firmado un documento, nadie puede modificarlo. La marca de tiempo ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer opciones de marca de tiempo mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de tiempo (TSP).

>[!NOTE]
>
>En los inicios rápidos de Java y el servicio web, la hora de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna información del servidor CRL u OCSP, la información del servidor se obtiene del certificado.

**Verificar la firma digital**

Para comprobar correctamente una firma, especifique el nombre completo del campo de firma que contiene la firma, como `form1[0].#subform[1].SignatureField3[3]`. Al utilizar un campo de formulario XFA, también puede utilizar el nombre parcial del campo de firma: `SignatureField3`.

De forma predeterminada, el servicio Signature limita el tiempo que se puede firmar un documento después del tiempo de validación a 65 minutos. Si un usuario intenta verificar una firma en el momento actual y el tiempo de firma es posterior al tiempo actual y se encuentra dentro de los 65 minutos, el servicio de firma no crea un error de verificación.

>[!NOTE]
>
>Para ver otros valores que necesita al comprobar una firma, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinar el estado de la firma**

Como parte de la verificación de una firma digital, puede comprobar el estado de la firma.

**Determinar la identidad del firmante**

Puede determinar la identidad del firmante, que puede ser uno de los siguientes valores:

* **Desconocido**: este firmante es desconocido porque no se puede realizar la verificación del firmante.
* **De confianza**: este firmante es de confianza.
* **No es de confianza**: este firmante no es de confianza.

**Consulte también**

[Verificar firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificar firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar firmas digitales mediante la API de Java {#verify-digital-signatures-using-the-java-api}

Verificar una firma digital mediante la API del servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que contiene la firma que desea comprobar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que contiene la firma que se va a comprobar utilizando su constructor. Pase un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones de tiempo de ejecución de PKI

   * Crear un objeto `PKIOptions` mediante su constructor.
   * Establezca el tiempo de comprobación invocando el método `PKIOptions` del objeto `setVerificationTime` y pasando un valor de enumeración `VerificationTime` que especifica el tiempo de comprobación.
   * Establezca la opción de comprobación de revocación invocando el método `PKIOptions` del objeto `setRevocationCheckStyle` y pasando un valor de enumeración `RevocationCheckStyle` que especifica si se va a realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el método `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene un documento de PDF certificado o firmado digitalmente.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Objeto `PKIOptions` que contiene opciones de tiempo de ejecución de PKI.
   * Instancia de `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verify2` devuelve un objeto `PDFSignatureVerificationInfo` que contiene información que se puede utilizar para comprobar la firma digital.

1. Determinar el estado de la firma

   * Determine el estado de la firma invocando el método `PDFSignatureVerificationInfo` del objeto `getStatus`. Este método devuelve un objeto `SignatureStatus` que especifica el estado de la firma. Por ejemplo, si no se modifica un documento de PDF firmado, este método devuelve `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante invocando el método `PDFSignatureVerificationInfo` del objeto `getSigner`. Este método devuelve un objeto `IdentityInformation`.
   * Invoque el método `IdentityInformation` del objeto `getStatus` para determinar la identidad del firmante. Este método devuelve un valor de enumeración `IdentityStatus` que especifica la identidad. Por ejemplo, si el firmante es de confianza, este método devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificar firmas digitales](#verify-digital-signatures-using-the-java-api)

[Inicio rápido (modo SOAP): Verificación de una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar firmas digitales mediante la API de servicio web {#verify-digital-signatures-using-the-web-service-api}

Verificar una firma digital mediante la API del servicio de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que contiene la firma que desea comprobar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF que contiene una firma digital o certificada que se va a comprobar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución de PKI

   * Crear un objeto `PKIOptions` mediante su constructor.
   * Establezca el tiempo de comprobación asignando el miembro de datos `PKIOptions` del objeto `verificationTime` a un valor de enumeración `VerificationTime` que especifique el tiempo de comprobación.
   * Establezca la opción de comprobación de revocación asignando el miembro de datos `PKIOptions` del objeto `revocationCheckStyle` a un valor de enumeración `RevocationCheckStyle` que especifique si se va a realizar la comprobación de revocación.

1. Verificar la firma digital

   Compruebe la firma invocando el método `SignatureServiceClient` del objeto `verify2` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene un documento de PDF certificado o firmado digitalmente.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma que se va a comprobar.
   * Objeto `PKIOptions` que contiene opciones de tiempo de ejecución de PKI.
   * Instancia de `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verify2` devuelve un objeto `PDFSignatureVerificationInfo` que contiene información que se puede utilizar para comprobar la firma digital.

1. Determinar el estado de la firma

   Determine el estado de la firma obteniendo el valor del miembro de datos `PDFSignatureVerificationInfo` del objeto `status`. Este miembro de datos almacena un objeto `SignatureStatus` que especifica el estado de la firma. Por ejemplo, si se modifica un documento de PDF firmado, el miembro de datos `status` almacena el valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar la identidad del firmante

   * Determine la identidad del firmante recuperando el valor del miembro de datos `PDFSignatureVerificationInfo` del objeto `signer`. Este miembro devuelve un objeto `IdentityInformation`.
   * Recupere el miembro de datos `IdentityInformation` del objeto `status` para determinar la identidad del firmante. Este miembro de datos devuelve un valor de enumeración `IdentityStatus` que especifica la identidad. Por ejemplo, si el firmante es de confianza, este miembro devuelve `IdentityStatus.TRUSTED`.

**Consulte también**

[Verificar firmas digitales](#verify-digital-signatures-using-the-java-api)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificar varias firmas digitales {#verifying-multiple-digital-signatures}

AEM Forms proporciona los medios para comprobar todas las firmas digitales incluidas en un documento de PDF. Supongamos que un documento de PDF contiene varias firmas digitales como resultado de un proceso empresarial que requiere firmas de varios firmantes. Por ejemplo, considere una transacción financiera que requiera la firma de un responsable de préstamo y de un administrador. Puede utilizar la API de Java o la API del servicio web de Signature para comprobar todas las firmas del documento de PDF. Al comprobar varias firmas digitales, puede comprobar el estado y las propiedades de cada firma. Antes de confiar en una firma digital, se recomienda verificarla. Se recomienda que esté familiarizado con la comprobación de una firma digital única.

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature y la comprobación de firmas digitales, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-7}

Para comprobar varias firmas digitales, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que contiene las firmas que desea comprobar.
1. Establecer las opciones de tiempo de ejecución de PKI.
1. Recupere todas las firmas digitales.
1. Iterar en todas las firmas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Antes de realizar mediante programación una operación del servicio Signature, cree un cliente del servicio Signature.

**Obtenga el documento de PDF que contiene las firmas que se van a comprobar**

Para comprobar una firma utilizada para firmar o certificar digitalmente un documento de PDF, obtenga un documento de PDF que contenga una firma.

**Establecer opciones de tiempo de ejecución de PKI**

Establezca estas opciones de tiempo de ejecución de PKI que utiliza el servicio Signature al comprobar todas las firmas de un documento de PDF:

* Tiempo de verificación
* Comprobación de revocación
* Valores de marca de tiempo

Al configurar estas opciones, puede especificar el tiempo de verificación. Por ejemplo, puede seleccionar la hora actual (la hora del equipo del validador), lo que indica que se debe utilizar la hora actual. Para obtener información acerca de los distintos valores de tiempo, vea el valor de enumeración `VerificationTime` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

También puede especificar si desea realizar la comprobación de revocación como parte del proceso de verificación. Por ejemplo, puede realizar una comprobación de revocación para determinar si el certificado está revocado. Para obtener información acerca de las opciones de comprobación de revocación, vea el valor de enumeración `RevocationCheckStyle` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para realizar la comprobación de revocación en un certificado, especifique una dirección URL a un servidor de lista de revocación de certificados (CRL) mediante un objeto `CRLOptionSpec`. Sin embargo, si no especifica una dirección URL a un servidor CRL, el servicio de firma obtiene la dirección URL del certificado.

En lugar de utilizar un servidor CRL, puede utilizar un servidor de Protocolo de estado de certificado en línea (OCSP) al realizar la comprobación de revocación. Normalmente, cuando se utiliza un servidor OCSP en lugar de un servidor CRL, la comprobación de revocación se realiza más rápido. (Consulte [Protocolo de estado de certificado en línea](https://tools.ietf.org/html/rfc2560).)

Puede establecer el orden del servidor de CRL y OCSP que utiliza el servicio Signature mediante Aplicaciones y servicios de Adobe. Por ejemplo, si el servidor OCSP se establece primero en Aplicaciones y servicios de Adobe, se comprueba el servidor OCSP, seguido del servidor CRL.

Si no realiza la comprobación de revocación, el servicio Signature no comprueba si el certificado está revocado. Es decir, se omite la información del servidor CRL y OCSP.

>[!NOTE]
>
>Puede anular la dirección URL especificada en el certificado usando un objeto `CRLOptionSpec` y un objeto `OCSPOptionSpec`. Por ejemplo, para invalidar el servidor CRL, puede invocar el método `CRLOptionSpec` del objeto `setLocalURI`.

La marca de tiempo es el proceso de rastrear la hora en que se modificó un documento firmado o certificado. Una vez firmado un documento, nadie puede modificarlo. La marca de tiempo ayuda a hacer cumplir la validez de un documento firmado o certificado. Puede establecer las opciones de marca de tiempo mediante un objeto `TSPOptionSpec`. Por ejemplo, puede especificar la dirección URL de un servidor de proveedor de marca de tiempo (TSP).

>[!NOTE]
>
>En los inicios rápidos de Java y el servicio web, la hora de verificación se establece en `VerificationTime.CURRENT_TIME` y la comprobación de revocación en `RevocationCheckStyle.BestEffort`. Dado que no se especifica ninguna información del servidor CRL u OCSP, la información del servidor se obtiene del certificado.

**Recuperar todas las firmas digitales**

Para comprobar todas las firmas digitales de un documento de PDF, recupere las firmas digitales del documento de PDF. Todas las firmas se devuelven en una lista. Como parte de la verificación de una firma digital, compruebe el estado de la firma.

>[!NOTE]
>
>A diferencia de cuando se comprueba una sola firma digital, cuando se verifican varias firmas, no es necesario especificar el nombre del campo de firma.

**Recorrer en iteración todas las firmas**

Iterar en cada firma. Es decir, para cada firma, compruebe la firma digital y la identidad del firmante y el estado de cada firma. (Consulte [Verificación de firmas digitales](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>No es necesario repetir todas las firmas si el requisito es todo el documento.

**Consulte también**

[Verificar varias firmas digitales mediante la API de Java](#verify-digital-signatures-using-the-java-api)

[Verificar varias firmas digitales mediante la API de servicio web](#verify-digital-signatures-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar varias firmas digitales mediante la API de Java {#verify-multiple-digital-signatures-using-the-java-api}

Compruebe varias firmas digitales mediante la API del servicio de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de firma

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que contiene las firmas que desea comprobar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que contiene varias firmas digitales para comprobar mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones de tiempo de ejecución de PKI

   * Crear un objeto `PKIOptions` mediante su constructor.
   * Establezca el tiempo de comprobación invocando el método `PKIOptions` del objeto `setVerificationTime` y pasando un valor de enumeración `VerificationTime` que especifica el tiempo de comprobación.
   * Establezca la opción de comprobación de revocación invocando el método `PKIOptions` del objeto `setRevocationCheckStyle` y pasando un valor de enumeración `RevocationCheckStyle` que especifica si se va a realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el método `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que contiene un documento de PDF con varias firmas digitales.
   * Objeto `PKIOptions` que contiene opciones de tiempo de ejecución de PKI.
   * Instancia de `VerifySPIOptions` que contiene información de SPI. Puede especificar `null` para este parámetro.

   El método `verifyPDFDocument` devuelve un objeto `PDFDocumentVerificationInfo` que contiene información sobre todas las firmas digitales del documento de PDF.

1. Iterar en todas las firmas

   * Recorra todas las firmas invocando el método `PDFDocumentVerificationInfo` del objeto `getVerificationInfos`. Este método devuelve un objeto `java.util.List` donde cada elemento es un objeto `PDFSignatureVerificationInfo`. Utilice un objeto `java.util.Iterator` para recorrer en iteración la lista de firmas.
   * Con el objeto `PDFSignatureVerificationInfo`, puede realizar tareas como determinar el estado de la firma invocando el método `PDFSignatureVerificationInfo` del objeto `getStatus`. Este método devuelve un objeto `SignatureStatus` cuyo miembro de datos estáticos le informa sobre el estado de la firma. Por ejemplo, si se desconoce la firma, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificar varias firmas digitales](#verifying-multiple-digital-signatures)

[Inicio rápido (modo SOAP): Verificación de varias firmas digitales mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificar firmas digitales](#verify-digital-signatures-using-the-java-api)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar varias firmas digitales mediante la API de servicio web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Compruebe varias firmas digitales mediante la API del servicio de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que contiene las firmas que desea comprobar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` almacena un documento de PDF que contiene varias firmas digitales para comprobar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.

1. Establecer opciones de tiempo de ejecución de PKI

   * Crear un objeto `PKIOptions` mediante su constructor.
   * Establezca el tiempo de comprobación asignando el miembro de datos `PKIOptions` del objeto `verificationTime` a un valor de enumeración `VerificationTime` que especifique el tiempo de comprobación.
   * Establezca la opción de comprobación de revocación asignando el miembro de datos `PKIOptions` del objeto `revocationCheckStyle` a un valor de enumeración `RevocationCheckStyle` que especifique si se va a realizar la comprobación de revocación.

1. Recuperar todas las firmas digitales

   Invoque el método `SignatureServiceClient` del objeto `verifyPDFDocument` y pase los siguientes valores:

   * Objeto `BLOB` que contiene un documento de PDF con varias firmas digitales.
   * Objeto `PKIOptions` que contiene opciones de tiempo de ejecución de PKI.
   * Instancia de `VerifySPIOptions` que contiene información de SPI. Puede especificar null para este parámetro.

   El método `verifyPDFDocument` devuelve un objeto `PDFDocumentVerificationInfo` que contiene información sobre todas las firmas digitales del documento de PDF.

1. Iterar en todas las firmas

   * Recorra todas las firmas obteniendo el miembro de datos `PDFDocumentVerificationInfo` del objeto `verificationInfos`. Este miembro de datos devuelve una matriz `Object` donde cada elemento es un objeto `PDFSignatureVerificationInfo`.
   * Con el objeto `PDFSignatureVerificationInfo`, puede realizar tareas como determinar el estado de la firma obteniendo el miembro de datos `PDFSignatureVerificationInfo` del objeto `status`. Este miembro de datos devuelve un objeto `SignatureStatus` cuyo miembro de datos estático le informa sobre el estado de la firma. Por ejemplo, si se desconoce la firma, este método devuelve `SignatureStatus.DocumentSignatureUnknown`.

**Consulte también**

[Verificar varias firmas digitales](#verifying-multiple-digital-signatures)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar firmas digitales {#removing-digital-signatures}

Las firmas digitales deben eliminarse de un campo de firma para poder aplicar una firma digital más reciente. No se puede sobrescribir una firma digital. Si intenta aplicar una firma digital a un campo de firma que contiene una firma, se produce una excepción.

>[!NOTE]
>
>Para obtener más información acerca del servicio Signature, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-8}

Para quitar una firma digital de un campo de firma, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de firma.
1. Obtenga el documento de PDF que contiene una firma que quitar.
1. Quite la firma digital del campo de firma.
1. Guarde el documento de PDF como archivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de firma**

Para poder realizar mediante programación una operación del servicio Signature, debe crear un cliente del servicio Signature.

**Obtenga el documento de PDF que contiene una firma que quitar**

Para quitar una firma de un documento de PDF, debe obtener un documento de PDF que la contenga.

**Quitar la firma digital del campo de firma**

Para quitar correctamente una firma digital de un documento de PDF, debe especificar el nombre del campo de firma que la contiene. Además, debe tener permiso para quitar la firma digital; de lo contrario, se produce una excepción.

**Guardar el documento de PDF como archivo de PDF**

Una vez que el servicio Signature quita una firma digital de un campo de firma, puede guardar el documento de PDF como un archivo de PDF para que los usuarios puedan abrirlo en Acrobat o Adobe Reader.

**Consulte también**

[Eliminación de firmas digitales mediante la API de Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Quitar firmas digitales mediante la API de servicio web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de campos de firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Eliminación de firmas digitales mediante la API de Java {#remove-digital-signatures-using-the-java-api}

Quitar una firma digital mediante la API de firma (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-signatures-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de firma.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `SignatureServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Obtenga el documento de PDF que contiene una firma que quitar

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que contiene la firma que se va a quitar utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quitar la firma digital del campo de firma

   Quite una firma digital de un campo de firma invocando el método `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF que contiene la firma que se va a quitar.
   * Valor de cadena que especifica el nombre del campo de firma que contiene la firma digital.

   El método `clearSignatureField` devuelve un objeto `com.adobe.idp.Document` que representa el documento de PDF del que se quitó la firma digital.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `com.adobe.idp.Document` del objeto `copyToFile`. Pase el objeto `java.io.File` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `Document` devuelto por el método `clearSignatureField`.

**Consulte también**

[Quitar firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Inicio rápido (modo SOAP): Quitar una firma digital mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Quitar firmas digitales mediante la API de servicio web {#remove-digital-signatures-using-the-web-service-api}

Quitar una firma digital mediante la API de firma (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un cliente de firma

   * Cree un objeto `SignatureServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `SignatureServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `SignatureServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `System.ServiceModel.BasicHttpBinding` del objeto `MessageEncoding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenga el documento de PDF que contiene una firma que quitar

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF que contiene una firma digital que se va a quitar.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `System.IO.FileStream` del objeto `Length`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `System.IO.FileStream` del objeto `Read`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Quitar la firma digital del campo de firma

   Quite la firma digital invocando el método `SignatureServiceClient` del objeto `clearSignatureField` y pasando los siguientes valores:

   * Un objeto `BLOB` que contiene el documento de PDF firmado.
   * Valor de cadena que representa el nombre del campo de firma que contiene la firma digital que se va a quitar.

   El método `clearSignatureField` devuelve un objeto `BLOB` que representa el documento de PDF del que se quitó la firma digital.

1. Guarde el documento de PDF como archivo de PDF

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF que contiene un campo de firma vacío y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `sign`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `BLOB` del objeto `MTOM`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en el archivo PDF invocando el método `System.IO.BinaryWriter` del objeto `Write` y pasando la matriz de bytes.

**Consulte también**

[Quitar firmas digitales](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
