---
title: Asignar derechos de uso
description: Utilice las extensiones de Acrobat Reader DC API de cliente Java y API de servicio web para aplicar y quitar derechos de uso de documentos de PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3897'
ht-degree: 2%

---

# Asignar derechos de uso {#assigning-usage-rights}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio de extensiones de Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

El servicio de extensiones de Acrobat Reader DC permite a su organización compartir fácilmente documentos interactivos de PDF ampliando la funcionalidad de Adobe Reader. El servicio de extensiones de Acrobat Reader DC es totalmente compatible con cualquier documento de PDF, hasta PDF 1.7 incluido. Funciona con Adobe Reader 7.0 y versiones posteriores. El servicio añade derechos de uso a un documento de PDF, activando funciones que normalmente no están disponibles cuando se abre un documento de PDF con Adobe Reader. Los usuarios de terceros no requieren software ni complementos adicionales para trabajar con los documentos con derechos activados.

Puede realizar estas tareas mediante el servicio de extensiones de Acrobat Reader DC:

* Aplicar derechos de uso a documentos de PDF. Para obtener más información, vea [Aplicar derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Quitar derechos de uso de documentos de PDF. Para obtener más información, consulte [Quitar derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperar detalles de credenciales. Para obtener más información, consulte [Recuperación de información de credenciales](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aplicar derechos de uso a documentos de PDF {#applying-usage-rights-to-pdf-documents}

Puede aplicar derechos de uso a documentos de PDF mediante la API de cliente Java y el servicio web de extensiones de Acrobat Reader DC. Los derechos de uso pertenecen a una funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o rellenar los campos del formulario y guardarlo. Los documentos PDF a los que se les han aplicado derechos de uso se denominan “documentos con derechos activados”. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese documento específico.

>[!NOTE]
>
>Al aplicar derechos de uso a documentos de PDF mediante el método `applyUsageRights`, que forma parte de la API de Java, puede establecer el parámetro `isModeFinal` del objeto `ReaderExtensionsOptionSpec` en `false`. Esto hace que el contador de formularios procesados no se actualice y mejore el rendimiento. Si no le preocupa actualizar el contador de formularios procesados, se recomienda establecer el parámetro `isModeFinal` en `false`.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para aplicar derechos de uso a un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento de PDF.
1. Especifique los derechos de uso que desea aplicar.
1. Aplicar derechos de uso al documento de PDF.
1. Guarde el documento de PDF con los derechos activados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto cliente de extensiones de Acrobat Reader DC**

Para realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto de cliente de servicio de extensiones de Acrobat Reader DC. Si utiliza la API de Java de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento de PDF**

Recupere un documento de PDF para aplicar derechos de uso. Los documentos de PDF con derechos activados contienen un diccionario de derechos de uso. Cuando Adobe Reader abre un documento que contiene dicho diccionario, solo habilita los derechos de uso especificados en el diccionario para ese documento. Si el documento no contiene un diccionario de derechos de uso, el servicio de extensiones de Acrobat Reader DC crea uno. Si ya contiene un diccionario, el servicio de extensiones de Acrobat Reader DC sobrescribe los derechos de uso existentes con los especificados. El diccionario especifica qué derechos de uso están habilitados. Cuando un usuario abre el documento en Adobe Reader, solo se permiten los derechos de uso especificados en el diccionario.

**Especifique los derechos de uso que desea aplicar**

Los derechos de uso que puede establecer están determinados por una credencial que adquiere de Adobe Systems Incorporated. Las credenciales suelen proporcionar permiso para establecer un grupo de derechos de uso relacionados, como los que pertenecen a los formularios interactivos. Cada credencial proporciona el derecho a crear un determinado número de documentos de PDF con derechos activados. Una credencial de evaluación le da derecho a crear un número ilimitado de borradores de documentos.

>[!NOTE]
>
>Si intenta asignar un derecho de uso que no está permitido por sus credenciales, causará una excepción.

**Aplicar derechos de uso al documento de PDF**

Para aplicar derechos de uso a un documento de PDF, debe hacer referencia al alias de la credencial que está utilizando para aplicar derechos de uso (una credencial suele instalarse durante la instalación de AEM Forms). Además, debe especificar el documento de PDF al que se aplican los derechos de uso. Para obtener información sobre cómo configurar una credencial, consulte la guía de instalación e implementación para su servidor de aplicaciones.

**Guardar el documento de PDF con derechos habilitados**

Una vez que el servicio de extensiones de Acrobat Reader DC aplique los derechos de uso a un documento de PDF, puede guardar el documento de PDF con los derechos activados como archivo de PDF.

**Consulte también**

[Aplicar derechos de uso mediante la API de Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Aplicar derechos de uso mediante la API de servicio web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Aplicar derechos de uso mediante la API de Java {#apply-usage-rights-using-the-java-api}

Aplique derechos de uso a un documento de PDF mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere un documento de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso mediante su constructor.
   * Para aplicar cada derecho de uso, invoque un método correspondiente que pertenezca al objeto `UsageRights`. Por ejemplo, para agregar el derecho de uso de `enableFormFillIn`, invoque el método `enableFormFillIn` del objeto `UsageRights` y pase `true`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplicar derechos de uso al documento de PDF.

   * Crear un objeto `ReaderExtensionsOptionSpec` mediante su constructor. Este objeto contiene opciones en tiempo de ejecución requeridas por el servicio de extensiones de Acrobat Reader DC. Al invocar este constructor, debe especificar los siguientes valores:

      * El objeto `UsageRights` que contiene los derechos de uso que se aplicarán al documento.
      * Valor de cadena que especifica un mensaje que ve un usuario cuando se abre el documento de PDF con derechos habilitados en Adobe Reader 7.x. Este mensaje no se muestra en Adobe Reader 8.0.

   * Aplique derechos de uso al documento de PDF invocando el método `applyUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene el documento de PDF al que se aplican los derechos de uso.
      * Valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente este parámetro se ignora. Puede pasar `null`.)

   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `com.adobe.idp.Document` que contiene el documento de PDF con derechos habilitados.

1. Guarde el documento de PDF con los derechos activados.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo (asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `applyUsageRights`).

**Consulte también**

[Aplicar derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inicio rápido (modo SOAP):Aplicar derechos de uso mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar derechos de uso mediante la API de servicio web {#apply-usage-rights-using-the-web-service-api}

Aplicar derechos de uso a un documento de PDF mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF al que se aplican derechos de uso.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Especifique los derechos de uso que desea aplicar.

   * Cree un objeto `UsageRights` que represente los derechos de uso mediante su constructor.
   * Para que se aplique cada derecho de uso, asigne el valor `true` al miembro de datos correspondiente que pertenezca al objeto `UsageRights`. Por ejemplo, para agregar el derecho de uso de `enableFormFillIn`, asigne `true` al miembro de datos `enableFormFillIn` del objeto `UsageRights`. (Repita este paso para cada derecho de uso que desee aplicar).

1. Aplicar derechos de uso al documento de PDF.

   * Crear un objeto `ReaderExtensionsOptionSpec` mediante su constructor. Este objeto contiene opciones en tiempo de ejecución requeridas por el servicio de extensiones de Acrobat Reader DC.
   * Asigne el objeto `UsageRights` al miembro de datos `usageRights` del objeto `ReaderExtensionsOptionSpec`.
   * Asigne un valor de cadena que especifique el mensaje que ve un usuario cuando se abre el documento de PDF con derechos habilitados en Adobe Reader al miembro de datos `message` del objeto `ReaderExtensionsOptionSpec`.
   * Aplique derechos de uso al documento de PDF invocando el método `applyUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando los siguientes valores:

      * El objeto `BLOB` que contiene el documento de PDF al que se aplican los derechos de uso.
      * Valor de cadena que especifica el alias de la credencial que le permite aplicar derechos de uso.
      * Un valor de cadena que especifica el valor de contraseña correspondiente. (Actualmente este parámetro se ignora. Puede pasar `null`.)

   * El objeto `ReaderExtensionsOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `applyUsageRights` devuelve un objeto `BLOB` que contiene el documento de PDF con derechos habilitados.

1. Guarde el documento de PDF con los derechos activados.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF con derechos activados.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `applyUsageRights`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Aplicar derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Quitar derechos de uso de documentos de PDF {#removing-usage-rights-from-pdf-documents}

Puede quitar los derechos de uso de un documento con derechos activados. La eliminación de los derechos de uso de un documento de PDF con derechos activados también es necesaria para realizar otras operaciones de AEM Forms en él. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de establecer los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento con derechos activados, debe quitar los derechos de uso del documento de PDF, realizar el resto de operaciones, como firmar digitalmente el documento y, a continuación, volver a aplicar los derechos de uso al documento.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para quitar los derechos de uso de un documento de PDF con derechos activados, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento de PDF con los derechos activados.
1. Quite los derechos de uso del documento de PDF.
1. Guarde el documento de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto de cliente de servicio de extensiones de Acrobat Reader DC. Si está usando la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento de PDF con derechos habilitados**

Recupere un documento de PDF con los derechos activados para eliminar los derechos de uso.

**Quitar derechos de uso del documento de PDF**

Después de recuperar un documento de PDF con los derechos activados, puede quitar los derechos de uso. Después de eliminar los derechos de uso, el documento de PDF no tendrá ninguna funcionalidad adicional cuando se visualice en Adobe Reader.

**Guardar el documento de PDF**

Puede guardar el documento de PDF que ya no contiene derechos de uso como archivo de PDF. Una vez guardado como archivo de PDF, el documento de PDF se puede ver en Adobe Reader o Acrobat.

**Consulte también**

[Eliminación de derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminación de derechos de uso mediante la API de servicio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Aplicar derechos de uso a documentos de PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Eliminación de derechos de uso mediante la API de Java {#remove-usage-rights-using-the-java-api}

Quite los derechos de uso de un documento de PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF con derechos habilitados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quite los derechos de uso del documento de PDF.

   Quite los derechos de uso del documento de PDF invocando el método `removeUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de PDF con derechos habilitados. Este método devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF que no tiene derechos de uso.

1. Aplicar derechos de uso al documento de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .PDF.
   * Invoque el método `copyToFile` del objeto `Document` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` devuelto por el método `removeUsageRights`).

**Consulte también**

[Quitar derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Inicio rápido (modo SOAP): Eliminación de los derechos de uso de un documento de PDF mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminación de derechos de uso mediante la API de servicio web {#remove-usage-rights-using-the-web-service-api}

Quite los derechos de uso de un documento de PDF con derechos activados mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF con los derechos habilitados del que se quitan los derechos de uso.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Quite los derechos de uso del documento de PDF.

   Quite los derechos de uso del documento de PDF invocando el método `removeUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando el objeto `BLOB` que contiene el documento de PDF con derechos habilitados. Este método devuelve un objeto `BLOB` que contiene un documento de PDF que no tiene derechos de uso.

1. Aplicar derechos de uso al documento de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo PDF.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `removeUsageRights`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.

**Consulte también**

[Quitar derechos de uso de documentos de PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando información de credenciales {#retrieving-credential-information}

Puede recuperar información sobre las credenciales que se utilizaron para aplicar derechos de uso a un documento de PDF con derechos activados. Al recuperar información sobre una credencial, puede obtener información como la fecha después de la cual el certificado ya no es válido.

>[!NOTE]
>
>Para obtener más información sobre el servicio de extensiones de Acrobat Reader DC, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar información sobre la credencial que se utilizó para aplicar derechos de uso a un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un objeto cliente de extensiones de Acrobat Reader DC.
1. Recupere un documento de PDF con los derechos activados.
1. Recupere información sobre la credencial.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto cliente de extensiones de Acrobat Reader DC**

Para poder realizar mediante programación una operación de servicio de extensiones de Acrobat Reader DC, debe crear un objeto de cliente de servicio de extensiones de Acrobat Reader DC. Si está usando la API de Java, cree un objeto `ReaderExtensionsServiceClient`. Si utiliza la API del servicio web de extensiones de Acrobat Reader DC, cree un objeto `ReaderExtensionsServiceService`.

**Recuperar un documento de PDF con derechos habilitados**

Recupere un documento de PDF con derechos habilitados para recuperar información sobre la credencial. También puede recuperar información sobre una credencial especificando su alias; sin embargo, si desea recuperar información sobre una credencial que se utilizó para aplicar derechos de uso a un documento de PDF con derechos específicos habilitados, deberá recuperar el documento.

**Recuperar información sobre la credencial**

Después de recuperar un documento de PDF con derechos habilitados, puede obtener información sobre la credencial que se utilizó para aplicarle derechos de uso. Puede obtener la siguiente información sobre la credencial:

* El mensaje que se muestra en Adobe Reader cuando se abre el documento de PDF con los derechos activados.
* La fecha a partir de la cual la credencial deja de ser válida.
* La fecha antes de la cual la credencial no es válida.
* Los derechos de uso establecidos para este documento de PDF con derechos activados.
* El número de veces que se ha utilizado la credencial.

**Consulte también**

[Eliminación de derechos de uso mediante la API de Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Eliminación de derechos de uso mediante la API de servicio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperar información de credenciales mediante la API de Java {#retrieve-credential-information-using-the-java-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-reader-extensions-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Recupere un documento de PDF.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF con derechos habilitados mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF con derechos habilitados.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Quite los derechos de uso del documento de PDF.

   * Recupere información sobre la credencial utilizada para aplicar derechos de uso al documento de PDF invocando el método `getDocumentUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de PDF con derechos habilitados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha a partir de la cual la credencial deja de ser válida invocando el método `getNotAfter` del objeto `GetUsageRightsResult`. Este método devuelve un objeto `java.util.Date` que representa la fecha después de la cual la credencial ya no es válida.
   * Recupere el mensaje que se muestra en Adobe Reader cuando se abre el documento de PDF con derechos habilitados invocando el método `getMessage` del objeto `GetUsageRightsResult`. Este método devuelve un valor de cadena que representa el mensaje.

**Consulte también**

[Recuperando información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Inicio rápido (modo SOAP): Recuperación de información de credenciales mediante la API de Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar información de credenciales mediante la API de servicio web {#retrieve-credential-information-using-the-web-service-api}

Recupere información de credenciales mediante la API de extensiones de Acrobat Reader DC (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto cliente de extensiones de Acrobat Reader DC.

   * Cree un objeto `ReaderExtensionsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ReaderExtensionsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Asegúrese de especificar `?blob=mtom`.)
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere un documento de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF con derechos habilitados.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF con derechos habilitados y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Quite los derechos de uso del documento de PDF.

   * Recupere información sobre la credencial utilizada para aplicar derechos de uso al documento de PDF invocando el método `getDocumentUsageRights` del objeto `ReaderExtensionsServiceClient` y pasando el objeto `com.adobe.idp.Document` que contiene el documento de PDF con derechos habilitados. Este método devuelve un objeto `GetUsageRightsResult` que contiene información de credenciales.
   * Recupere la fecha a partir de la cual la credencial deja de ser válida obteniendo el valor del miembro de datos `notAfter` del objeto `GetUsageRightsResult`. El tipo de datos de este miembro de datos es `System.DateTime`.
   * Recupere el mensaje que se muestra cuando se abre el documento de PDF con derechos habilitados en Adobe Reader obteniendo el valor del miembro de datos `message` del objeto `GetUsageRightsResult`. El tipo de datos de este miembro de datos es una cadena.
   * Recupere el número de veces que se usa la credencial obteniendo el valor del miembro de datos `useCount` del objeto `GetUsageRightsResult`. El tipo de datos de este miembro de datos es un número entero.

**Consulte también**

[Recuperando información de credenciales](assigning-usage-rights.md#retrieving-credential-information)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
