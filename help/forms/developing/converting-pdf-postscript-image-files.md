---
title: Convertir archivos PDF a Postscript andImage
description: Utilice el servicio ConvertPDF para convertir documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF) mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 509b9e53-9af4-4916-afba-2db358ec0764
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 2%

---

# Conversión de PDF a archivos Postscript y de imagen {#converting-pdf-to-postscript-andimage-files}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio Convert PDF**

El servicio ConvertPDF convierte los documentos de PDF a PostScript y a varios formatos de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento PDF en un archivo TIFF de varias páginas es práctico cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos PDF.

Puede realizar estas tareas mediante el servicio ConvertPDF:

* Convertir documentos de PDF a PostScript.
* Convertir documentos de PDF a formatos de imagen.

>[!NOTE]
>
>Para obtener más información acerca del servicio ConvertPDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertir documentos de PDF a PostScript {#converting-pdf-documents-to-postscript}

En este tema se describe cómo se puede utilizar la API Convert PDF Service (Java y servicio web) para convertir mediante programación documentos de PDF en archivos de PostScript. El documento de PDF convertido en un archivo de PostScript debe ser un documento no interactivo de PDF. Es decir, si intenta convertir un documento interactivo de PDF en un archivo de PostScript, se genera una excepción.

>[!NOTE]
>
>Para obtener más información acerca del servicio ConvertPDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un archivo de PostScript, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio ConvertPDF.
1. Haga referencia al documento de PDF para convertirlo en un archivo de PostScript.
1. Establecer las opciones de tiempo de ejecución de conversión.
1. Convierta el documento de PDF en un archivo de PostScript.
1. Guarde el archivo PostScript.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de Convert PDF**

Para poder realizar mediante programación una operación de servicio ConvertPDF, debe crear un cliente de servicio ConvertPDF. Si está usando la API de Java, cree un objeto `ConvertPdfServiceClient`. Si está usando la API del servicio web, cree un objeto `ConvertPDFServiceService`.

Esta sección utiliza la funcionalidad de servicio web que se introduce en AEM Forms. Para acceder a la nueva funcionalidad, debe construir el objeto proxy con el atributo `lc_version`. (Consulte &quot;Acceso a la nueva funcionalidad mediante servicios web&quot; en [Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)).

**Hacer referencia al documento de PDF para convertirlo en un archivo de PostScript**

Haga referencia al documento de PDF que desea convertir en un archivo de PostScript. Como se ha indicado anteriormente en este tema, el documento de PDF debe ser un documento no interactivo de PDF. Si intenta convertir un documento interactivo de PDF en un archivo de PostScript, se producirá una excepción.

**Establecer opciones de tiempo de ejecución de conversión**

Al convertir un documento de PDF en un archivo de PostScript, puede definir opciones en tiempo de ejecución que especifiquen el tipo de PostScript que se crea. Por ejemplo, puede definir un archivo PostScript de nivel 3.

Normalmente, el archivo de PostScript generado reflejará el tamaño del documento de PDF de entrada. Si selecciona la opción `ShrinkToFit` (que reduce la salida del archivo PostScript para que se ajuste a la página), no verá una diferencia entre el documento de PDF de entrada y el archivo de PostScript generado. La opción `ShrinkToFit` sólo tiene efecto si selecciona imprimir en un tamaño de página menor que el documento de PDF de entrada. Para seleccionar un tamaño de página menor, defina la opción `PageSize`. Además, se recomienda establecer la opción `RotateAndCenter` en `true` para obtener el resultado de PostScript correcto.

Del mismo modo, si selecciona la opción `ExpandToFit` (que expande la salida del archivo PostScript para que se ajuste a la página), solo tendrá efecto si selecciona imprimir en un tamaño de página mayor que el documento de PDF de entrada. Para seleccionar un tamaño de página mayor, defina la opción `PageSize`. Además, se recomienda establecer la opción `RotateAndCenter` en `true` para obtener el resultado de PostScript correcto.

>[!NOTE]
>
>Para obtener información acerca de los valores en tiempo de ejecución que puede establecer, vea la referencia de clase `ToPSOptionsSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el documento de PDF en un archivo de PostScript**

Después de crear el cliente de servicios y establecer las opciones en tiempo de ejecución, puede invocar la operación de conversión de PostScript. Esta operación necesitará información sobre el documento que desea convertir, incluido el nivel de PostScript preferido para el documento de destino.

**Guardar el archivo de PostScript**

Después de convertir el documento de PDF a PostScript, puede guardar la salida como un archivo de PostScript.

**Consulte también**

[Conversión de un documento de PDF a PS mediante la API de Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Conversión de un documento de PDF en PS mediante la API de servicio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio ConvertPDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento de PDF a PS mediante la API de Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Conversión de un documento de PDF a PostScript mediante la API de servicio de ConvertPDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de ConvertPDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Haga referencia al documento de PDF para convertirlo en un archivo de PostScript.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pase un valor de cadena que especifique la ubicación del documento de PDF que desea convertir.
   * Cree un objeto `com.adobe.idp.Document` que almacene el documento de PDF mediante el constructor `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el documento de PDF.

1. Establecer las opciones de tiempo de ejecución de conversión.

   * Cree un objeto `ToPSOptionsSpec` invocando su constructor.
   * Establezca las opciones en tiempo de ejecución invocando un método apropiado que pertenezca al objeto `ToPSOptionsSpec`. Por ejemplo, para definir el nivel de PostScript que se crea, invoque el método `setPsLevel` del objeto `ToPSOptionsSpec` y pase un valor de enumeración `PSLevel` que especifique el nivel de PostScript. Para obtener información acerca de todos los valores en tiempo de ejecución que puede establecer, vea la referencia de clase `ToPSOptionsSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convierta el documento de PDF en un archivo de PostScript.

   Invoque el método `toPS2` del objeto `ConvertPdfServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF que se va a convertir en un archivo de PostScript.
   * Un objeto `ToPSOptionsSpec` que especifica las opciones de tiempo de ejecución de PostScript.

   El método `toPS2` devuelve un objeto `Document` que contiene el nuevo documento de PostScript.

1. Guarde el archivo PostScript.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .ps.
   * Invoque el método `copyToFile` del objeto `Document` para copiar el contenido del objeto `Document` en el archivo (asegúrese de utilizar el objeto `Document` devuelto por el método `toPS2`).

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Inicio rápido (modo SOAP): Convertir un documento de PDF a PostScript mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un documento de PDF en PS mediante la API de servicio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Conversión de un documento de PDF a PostScript mediante la API de conversión de servicios de PDF (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de ConvertPDF.

   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ConvertPdfServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). No necesita utilizar el atributo `lc_version`. Sin embargo, especifique `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ConvertPdfServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Haga referencia al documento de PDF para convertirlo en un archivo de PostScript.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF convertido en un archivo de PostScript.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo del documento de PDF que se va a convertir y el modo en que se va a abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establecer las opciones de tiempo de ejecución de conversión.

   * Cree un objeto `ToPSOptionsSpec` invocando su constructor.
   * Establezca las opciones en tiempo de ejecución asignando un valor al miembro de datos del objeto `ToPSOptionsSpec`. Por ejemplo, para definir el nivel de PostScript que se crea, asigne un valor de enumeración `PSLevel` al miembro de datos `psLevel` del objeto `ToPSOptionsSpec`.

1. Convierta el documento de PDF en un archivo de PostScript.

   Invoque el método `toPS2` del objeto `GeneratePDFServiceService` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento de PDF que se va a convertir en un archivo de PostScript
   * Un objeto `ToPSOptionsSpec` que especifica las opciones en tiempo de ejecución

   Una vez completada la conversión, extraiga los datos binarios que representan el documento de PostScript teniendo acceso a la propiedad `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PostScript.

1. Guarde el archivo PostScript.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo PS.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingPassword`. Rellene la matriz de bytes obteniendo el valor del campo `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en el archivo PostScript invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversión de documentos de PDF a formatos de imagen {#converting-pdf-documents-to-image-formats}

Puede utilizar el servicio Convert PDF para convertir documentos de PDF a formatos de imagen mediante programación, que incluyen JPEG, JPEG 2000, TIFF y PNG. Al convertir un documento de PDF en un archivo de imagen, puede utilizar el documento de PDF como archivo de imagen. Por ejemplo, puede colocar la imagen en un sistema de administración de contenido empresarial para su almacenamiento.

Al convertir un documento de PDF en una imagen, el servicio ConvertPDF crea una imagen independiente para cada página del documento. Es decir, si el documento tiene 20 páginas, el servicio Convert PDF crea 20 archivos de imagen. Al convertir un documento de PDF a un formato de imagen, puede crear imágenes individuales para cada página dentro del documento de PDF o un solo archivo de imagen para todo el documento de PDF.

>[!NOTE]
>
>Para obtener más información acerca del servicio ConvertPDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento de PDF en cualquiera de los tipos compatibles, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio ConvertPDF.
1. Recupere el documento de PDF que desea convertir.
1. Establecer opciones en tiempo de ejecución.
1. Convierta PDF en una imagen.
1. Recupere los archivos de imagen de una colección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de Convert PDF**

Para poder realizar mediante programación una operación de servicio ConvertPDF, debe crear un cliente de servicio ConvertPDF. Si está usando la API de Java, cree un objeto `ConvertPdfServiceClient`. Si está usando la API del servicio web, cree un objeto `ConvertPDFServiceService`.

**Recuperar el documento de PDF para convertirlo**

Recupere el documento de PDF para convertirlo en una imagen. No puede convertir un documento interactivo de PDF en una imagen. Si intenta hacerlo, se produce una excepción. Para convertir un documento interactivo de PDF en un archivo de imagen, debe acoplar el documento de PDF antes de convertirlo. (Consulte [Acoplar documentos de PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Establecer opciones en tiempo de ejecución**

Establezca opciones en tiempo de ejecución como el formato de imagen y los valores de resolución. Para obtener información acerca de los valores en tiempo de ejecución, vea la referencia de clase `ToImageOptionsSpec` en [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir el PDF en imagen**

Después de crear el cliente de servicios y establecer las opciones en tiempo de ejecución, puede convertir el documento de PDF en una imagen. Se devuelve un objeto de colección que contiene las imágenes.

**Recuperar los archivos de imagen de una colección**

Puede recuperar archivos de imagen de un objeto de colección que devuelva el servicio ConvertPDF. Cada elemento de la colección es una instancia de `com.adobe.idp.Document` (o una instancia de `BLOB` si utiliza servicios web) que puede guardar como archivo de imagen, como un archivo JPG.

El formato del archivo de imagen depende de la opción de tiempo de ejecución `ImageConvertFormat`. Es decir, si establece la opción de tiempo de ejecución `ImageConvertFormat` en `ImageConvertFormat.JPEG`, puede guardar archivos de imagen como archivos de JPG.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de la API del servicio ConvertPDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversión de un documento de PDF en archivos de imagen mediante la API de Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Conversión de un documento de PDF a un formato de imagen mediante la API del servicio ConvertPDF (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-convertpdf-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de ConvertPDF.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el documento de PDF que desea convertir.

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a convertir mediante su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones en tiempo de ejecución.

   * Crear un objeto `ToImageOptionsSpec` mediante su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, establezca el tipo de imagen invocando el método `setImageConvertFormat` y pasando un valor de enumeración `ImageConvertFormat` que especifique el tipo de formato.

   >[!NOTE]
   >
   >Es obligatorio establecer el valor de enumeración `ImageConvertFormat`.

1. Convierta PDF en una imagen.

   Invoque el método `toImage2` del objeto `ConvertPdfServiceClient` y pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que representa el archivo PDF que se va a convertir.
   * Un objeto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino.

   El método `toImage2` devuelve un objeto `java.util.List` que contiene imágenes. Cada elemento de la colección es una instancia de `com.adobe.idp.Document`.

1. Recupere los archivos de imagen de una colección.

   Recorra en iteración el objeto `java.util.List` para determinar si las imágenes están presentes. Cada elemento es una instancia de `com.adobe.idp.Document`. Guarde la imagen invocando el método `copyToFile` del objeto `com.adobe.idp.Document` y pasando un objeto `java.io.File`.

**Consulte también**

[Inicio rápido (modo SOAP): Conversión de un documento de PDF a archivos JPEG mediante la API de Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversión de un documento de PDF en archivos de imagen mediante la API de servicio web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Conversión de un documento de PDF a un formato de imagen mediante la API de PDF Service (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de PDF convertido.

   * Cree un objeto `ConvertPdfServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `ConvertPdfServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). No necesita utilizar el atributo `lc_version`. Sin embargo, especifique `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `ConvertPdfServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el documento de PDF que desea convertir.

   * Crear un objeto `BLOB` mediante su constructor. Este objeto `BLOB` se usa para almacenar el formulario de PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que especifique la ubicación del formulario de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Determine el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Crear un objeto `ToImageOptionsSpec` mediante su constructor.
   * Invoque los métodos que pertenezcan a este objeto según sea necesario. Por ejemplo, establezca el tipo de imagen invocando el método `setImageConvertFormat` y pasando un valor de enumeración `ImageConvertFormat` que especifique el tipo de formato.

   >[!NOTE]
   >
   >Es obligatorio establecer el valor de enumeración `ImageConvertFormat`.

1. Convierta PDF en una imagen.

   Invoque el método `toImage2` del objeto `ConvertPDFServiceService` y pase los siguientes valores:

   * Objeto `BLOB` que representa el archivo que se va a convertir
   * Un objeto `ToImageOptionsSpec` que contiene las distintas preferencias sobre el formato de imagen de destino

   El método `toImage2` devuelve un objeto `MyArrayOfBLOB` que contiene los archivos de imagen recién creados.

1. Recupere los archivos de imagen de una colección.

   * Determine el número de elementos en el objeto `MyArrayOfBLOB` obteniendo el valor de su campo `Count`. Cada elemento es un objeto `BLOB` que contiene la imagen.
   * Recorra en iteración el objeto `MyArrayOfBLOB` y guarde cada archivo de imagen.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
