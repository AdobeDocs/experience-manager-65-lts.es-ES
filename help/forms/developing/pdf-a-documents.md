---
title: Trabajar con documentos PDF/A
description: Utilice el servicio DocConverter para determinar si un documento de PDF es un documento de PDF/A y convertir documentos de PDF en documentos de PDF/A.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 387f917c-eae3-4326-88f4-3b77cb9e4d46
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 2%

---

# Trabajar con documentos PDF/A {#working-with-pdf-a-documents}

**Acerca del servicio DocConverter**

El servicio DocConverter puede convertir documentos de PDF en documentos PDA/A. Puede realizar estas tareas con este servicio:

* Convierta documentos de PDF en documentos de PDF/A. (Consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine si los documentos de PDF son documentos de PDF/A. (Consulte [Determinación Programática De La Conformidad Con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obtener más información acerca del servicio DocConverter, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos a documentos de PDF/A {#converting-documents-to-pdf-a-documents}

Puede utilizar el servicio DocConverter para convertir un documento de PDF en un documento de PDF/A. Dado que PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.  Antes de convertir un documento de PDF en un documento de PDF/A, asegúrese de que el documento de PDF no sea un documento de PDF/A.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes estén incrustadas en el documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

Aunque PDF/A es el estándar para archivar documentos de PDF, no es obligatorio que PDF/A se utilice para archivar si un documento estándar de PDF cumple los requisitos de su empresa. El propósito del estándar PDF/A es crear un archivo PDF diseñado para las necesidades de archivado y conservación de documentos a largo plazo.

>[!NOTE]
>
>Para obtener más información acerca del servicio DocConverter, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un documento de PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A.
1. Configure la información de seguimiento.
1. Convertir el documento.
1. Guarde el documento de PDF/A.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar mediante programación una operación DocConverter, debe crear un cliente DocConverter. Si está usando la API de Java, cree un objeto `DocConverterServiceClient`. Si está usando la API del servicio web DocConverter, cree un objeto `DocConverterServiceService`.

**Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A**

Recupere un documento de PDF para convertirlo en un documento de PDF/A. Si intenta convertir un documento de PDF, como un formulario de Acrobat, en un documento de PDF/A, se producirá una excepción.

**Establecer información de seguimiento**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen la cantidad de información que el servicio DocConverter rastrea cuando convierte un documento de PDF en un documento de PDF/A.

**Convertir el documento**

Después de crear el cliente del servicio DocConverter, haga referencia al documento de PDF para convertir y establezca la opción en tiempo de ejecución que especifica la cantidad de información de la que se realiza el seguimiento, puede convertir el documento de PDF en un documento de PDF/A.

**Guardar el documento de PDF/A**

Puede guardar el documento de PDF/A como archivo de PDF.

**Consulte también**

[Conversión de documentos en documentos de PDF/A mediante la API de Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversión de documentos en documentos de PDF/A mediante la API de servicio web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinación programática de la compatibilidad con PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Conversión de documentos en documentos de PDF/A mediante la API de Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Conversión de un documento de PDF en un documento de PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente DocConvert

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a convertir mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer información de seguimiento

   * Crear un objeto `PDFAConversionOptionSpec` mediante su constructor.
   * Establezca el nivel de seguimiento de la información invocando el método `setLogLevel` del objeto `PDFAConversionOptionSpec` y pasando un valor de cadena que especifique el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información acerca de los distintos valores, vea el método `setLogLevel` en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir el documento

   Convierta el documento de PDF en un documento de PDF/A invocando el método `toPDFA` del objeto `DocConverterServiceClient` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento de PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento de PDF/A

   * Recupere el documento PDF/A invocando el método `getPDFA` del objeto `PDFAConversionResult`. Este método devuelve un objeto `com.adobe.idp.Document` que representa el documento de PDF/A.
   * Cree un objeto `java.io.File` que represente el archivo PDF/A. Asegúrese de que la extensión del nombre de archivo sea .pdf.
   * Rellene el archivo con datos de PDF/A invocando el método `copyToFile` del objeto `com.adobe.idp.Document` y pasando el objeto `java.io.File`.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Conversión de un documento a un documento de PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos en documentos de PDF/A mediante la API de servicio web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Conversión de un documento de PDF en un documento de PDF/A mediante la API de DocConverter (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de DocConverter.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `Credentials` del objeto `DocConverterServiceService` con un valor `System.Net.NetworkCredential` que especifique el valor de nombre de usuario y contraseña.

1. Hacer referencia a un documento de PDF para convertirlo en un documento de PDF/A

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF convertido en un documento de PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Establecer información de seguimiento

   * Crear un objeto `PDFAConversionOptionSpec` mediante su constructor.
   * Establezca el nivel de seguimiento de la información asignando un valor que especifique el nivel de seguimiento al miembro de datos `logLevel` del objeto `PDFAConversionOptionSpec`. Por ejemplo, asigne el valor `FINE` a este miembro de datos.

1. Convertir el documento

   Convierta el documento de PDF en un documento de PDF/A invocando el método `toPDFA` del objeto `DocConverterServiceService` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el documento de PDF que se va a convertir
   * El objeto `PDFAConversionOptionSpec` que especifica la información de seguimiento

   El método `toPDFA` devuelve un objeto `PDFAConversionResult` que contiene el documento PDF/A.

1. Guardar el documento de PDF/A

   * Cree un objeto `BLOB` que almacene el documento PDF/A obteniendo el valor del miembro de datos `PDFADocument` del objeto `PDFAConversionResult`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto mediante el objeto `PDFAConversionResult`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `binaryData` del objeto `BLOB`.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF/A.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinación programática de la compatibilidad con PDF/A {#programmatically-determining-pdf-a-compliancy}

Puede utilizar el servicio DocConverter para determinar si un documento de PDF es compatible con PDF/A. Para obtener información sobre un documento de PDF/A y cómo convertir un documento de PDF en un documento de PDF/A, consulte [Conversión de documentos a documentos de PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obtener más información acerca del servicio DocConverter, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para determinar la conformidad con PDF/A, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente DocConvert
1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A.
1. Establecer opciones en tiempo de ejecución.
1. Recupere información sobre el documento de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente DocConvert**

Para poder realizar mediante programación una operación DocConverter, debe crear un cliente DocConverter. Si está usando la API de Java, cree un objeto `DocConverterServiceClient`. Si está usando la API del servicio web DocConverter, cree un objeto `DocConverterServiceService`.

**Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento de PDF y pasarlo al servicio DocConverter para determinar si el documento de PDF es compatible con PDF/A.

**Establecer opciones en tiempo de ejecución**

Puede establecer una opción en tiempo de ejecución que determine la cantidad de información que se rastreará durante el proceso de conversión. Es decir, puede establecer nueve niveles diferentes que especifiquen cuánta información rastrea el servicio DocConverter cuando convierte un documento de PDF en un documento de PDF/A.

**Recuperar información acerca del documento de PDF**

Después de crear el cliente de servicio DocConverter, hacer referencia al documento de PDF y establecer las opciones en tiempo de ejecución, puede determinar si el documento de PDF es un documento compatible con PDF/A.

**Consulte también**

[Determinar la conformidad de PDF/A mediante la API de Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinar la conformidad de PDF/A mediante la API del servicio web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad de PDF/A mediante la API de Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine la conformidad con PDF/A mediante la API de Java:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-docconverter-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente DocConvert

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DocConverterServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A

   * Cree un objeto `java.io.FileInputStream` que represente el documento de PDF que se va a convertir mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establecer opciones en tiempo de ejecución

   * Crear un objeto `PDFAValidationOptionSpec` mediante su constructor.
   * Defina el nivel de cumplimiento invocando el método `setCompliance` del objeto `PDFAValidationOptionSpec` y pasando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información invocando el método `setLogLevel` del objeto `PDFAValidationOptionSpec` y pasando un valor de cadena que especifique el nivel de seguimiento. Por ejemplo, pase el valor `FINE`. Para obtener información acerca de los distintos valores, vea el método `setLogLevel` en la [Referencia de API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar información sobre el documento de PDF

   Para determinar la compatibilidad con PDF/A, invoque el método `isPDFA` del objeto `DocConverterServiceClient` y pase los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el documento de PDF.
   * El objeto `PDFAValidationOptionSpec` que especifica las opciones en tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Inicio rápido (modo SOAP): Determinación del cumplimiento de PDF/A mediante la API de Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar la conformidad de PDF/A mediante la API del servicio web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine la conformidad de PDF/A mediante la API del servicio web:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de DocConverter.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente DocConvert

   * Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `DocConverterServiceService` invocando su constructor predeterminado.
   * Establezca el miembro de datos `Credentials` del objeto `DocConverterServiceService` con un valor `System.Net.NetworkCredential` que especifique el valor de nombre de usuario y contraseña.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF convertido en un documento de PDF/A.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución

   * Crear un objeto `PDFAValidationOptionSpec` mediante su constructor.
   * Establezca el nivel de cumplimiento asignando el miembro de datos `compliance` del objeto `PDFAValidationOptionSpec` con el valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Establezca el nivel de seguimiento de la información asignando el miembro de datos `resultLevel` del objeto `PDFAValidationOptionSpec` con el valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar información sobre el documento de PDF

   Para determinar la compatibilidad con PDF/A, invoque el método `isPDFA` del objeto `DocConverterServiceService` y pase los siguientes valores:

   * El objeto `BLOB` que contiene el documento de PDF.
   * El objeto `PDFAValidationOptionSpec` que contiene opciones en tiempo de ejecución.

   El método `isPDFA` devuelve un objeto `PDFAValidationResult` que contiene los resultados de esta operación.

**Consulte también**

[Trabajar con documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
