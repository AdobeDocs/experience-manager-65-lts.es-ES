---
title: Trabajar con utilidades PDF
description: Utilice el servicio Utilidades de PDF para realizar conversiones entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular los metadatos de XMP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# Trabajar con utilidades PDF {#working-with-pdf-utilities}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de utilidades de PDF**

El servicio Utilidades de PDF puede realizar conversiones entre los formatos de archivo PDF y XDP, establecer y recuperar propiedades de documento de PDF y manipular metadatos de XMP. Por ejemplo, antes de convertir un documento de PDF a otro formato, es útil inspeccionar sus propiedades para determinar qué operación de servicio invocar para la conversión.

Puede realizar estas tareas mediante el servicio Utilidades de PDF:

* Convertir documentos de PDF en documentos XDP.
* Convertir documentos XDP en documentos de PDF. (Consulte [Conversión de documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)).
* Recupere las propiedades del documento PDF. (Consulte [Recuperando propiedades de documentos de PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Guarde un documento de PDF y optimícelo para una visualización web rápida. (Consulte [Configuración de los modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertir documentos de PDF en documentos XDP {#converting-pdf-documents-into-xdp-documents}

Puede utilizar las API de Java y de servicios web de Utilidades de PDF para convertir mediante programación documentos de PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para convertir un documento de PDF en un documento XDP, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de conversión de PDF a XDP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente de PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API del servicio web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión de PDF a XDP**

Después de crear el cliente de servicio, puede invocar la operación de conversión de PDF a XDP.

**Consulte también**

[Convertir documentos de PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos de PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos de PDF en documentos XDP mediante la API de Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convierta documentos de PDF en documentos XDP mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de PDF a XDP

   Para realizar la conversión, invoque el método `convertPDFtoXDP` del objeto `PDFUtilityServiceClient` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Convertir documentos de PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos de PDF en documentos XDP mediante la API de servicio web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convierta documentos de PDF en documentos XDP mediante la API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` con el constructor de clase de proxy.

1. Invocar la operación de conversión de PDF a XDP

   Invoque el método `convertPDFtoXDP` del objeto `PDFUtilityServiceService` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `BLOB` que representa el archivo XDP recién creado.

**Consulte también**

[Convertir documentos de PDF en documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Convertir documentos XDP en documentos de PDF {#converting-xdp-documents-into-pdf-documents}

Puede utilizar las API de Java y de servicios web de Utilidades de PDF para convertir mediante programación documentos XDP en documentos de PDF.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para convertir un documento XDP en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de conversión de XDP a PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente de PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API del servicio web, esto se logra mediante el uso de un objeto `PDFUtilityServiceService`.

**Invocar la operación de conversión de XDP a PDF**

Después de crear el cliente de servicio, puede invocar la operación de conversión de XDP a PDF.

**Consulte también**

[Convertir documentos XDP en documentos de PDF mediante la API de Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversión de documentos XDP en documentos de PDF mediante la API de servicio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir documentos XDP en documentos de PDF mediante la API de Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque el método `convertXDPtoPDF` del objeto `PDFUtilityServiceClient` y pase un objeto `com.adobe.idp.Document` que represente el archivo XDP. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo PDF recién creado.

**Consulte también**

[Convertir documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de documentos XDP en documentos de PDF mediante la API de servicio web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convierta documentos XDP en documentos de PDF mediante la API de utilidades de PDF (API de servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` con el constructor de clase de proxy.

1. Invocar la operación de conversión de XDP a PDF

   Para realizar la conversión, invoque el método `convertXDPtoPDF` del objeto `PDFUtilityServiceService` y pase un objeto `BLOB` que represente el archivo XDP. El método devuelve un objeto `BLOB` que representa el archivo PDF recién creado.

**Consulte también**

[Convertir documentos XDP en documentos de PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando propiedades de documento de PDF {#retrieving-pdf-document-properties}

Puede utilizar las API de Java y de servicio web de Utilidades de PDF para recuperar mediante programación las propiedades de documento de PDF, como si el documento es un formulario rellenable o la versión mínima de Acrobat necesaria para leer el documento.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumen de los pasos {#summary_of_steps-2}

Para recuperar las propiedades del documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de recuperación de propiedades.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente de PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API del servicio web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Invocar la operación de recuperación de propiedades**

Después de crear el cliente de servicios, puede invocar la operación de recuperación de propiedades.

**Consulte también**

[Recuperar propiedades de documentos de PDF mediante la API de Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propiedades de documento de PDF mediante la API de servicio web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documentos de PDF mediante la API de Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere las propiedades del documento de PDF mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `getPDFProperties` del objeto `PDFUtilityServiceClient` y pase lo siguiente:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF.
   * Objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperando propiedades de documento de PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propiedades de documento de PDF mediante la API de servicio web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere las propiedades del documento de PDF mediante la API del servicio web Utilidades de PDF:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` con el constructor de clase de proxy.

1. Invocar la operación de recuperación de propiedades

   Para realizar la conversión, invoque el método `getPDFProperties` del objeto `PDFUtilityServiceService` y pase lo siguiente:

   * Un objeto `BLOB` que representa el documento de PDF.
   * Objeto `PDFPropertiesOptionSpec` que contiene las propiedades que se van a evaluar.

   El método devuelve un objeto `PDFPropertiesResult` que contiene los resultados de la consulta.

**Consulte también**

[Recuperando propiedades de documento de PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Estableciendo modos de guardado de documentos de PDF {#setting-pdf-document-save-modes}

Puede utilizar las API de Java y del servicio web de Utilidades de PDF para establecer mediante programación un modo de guardado para un documento de PDF. Al utilizar el servicio Utilidades de PDF para establecer un modo de guardado, el servicio Utilidades de PDF solo establece el modo de guardado y no guarda realmente el documento de PDF. El documento de PDF se guarda cuando se pasa a otra operación de servicio. Por ejemplo, puede utilizar el servicio Utilidades de PDF para establecer un modo de guardado específico y pasarlo al servicio Encryption, donde el documento de PDF se guarda y se cifra.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-3}

Para definir la opción de guardado para documentos de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Configure el modo de guardado.
1. Invoque la operación de guardado.
1. Pase el documento de PDF a otra operación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de Utilidades de PDF, debe crear un cliente de PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`. Con la API del servicio web, esto se logra mediante un objeto `PDFUtilityServiceService`.

**Establecer el modo de guardado**

Puede elegir una de las siguientes opciones de guardado:

* `INCREMENTAL`: para guardar de forma incremental a fin de reducir el tiempo necesario para guardar
* `FAST_WEB_VIEW`: guardar para visualización web rápida
* `FULL`: para guardar usando un guardado completo (sin optimizaciones)

**Invocar la operación de guardar estilo**

Después de crear el cliente de servicios, puede invocar la operación de recuperación de propiedades.

**Pase el documento de PDF a otra operación de AEM Forms**

Una vez que el servicio Utilidades de PDF haya establecido el modo Guardar especificado, pase el documento de PDF a otra operación de AEM Forms. Una vez devuelto por esa operación, el documento de PDF se guarda en el modo especificado. Por ejemplo, si utiliza el servicio Utilidades de PDF para establecer el modo `FAST_WEB_VIEW` y, a continuación, pasa el documento de PDF a la operación `encryptUsingPassword` del servicio Encryption, el documento de PDF devuelto se cifra con una contraseña y se guarda en el modo `FAST_WEB_VIEW`.

>[!NOTE]
>
>El Inicio rápido asociado a esta sección establece el modo `FAST_WEB_VIEW` y, a continuación, pasa el documento de PDF a la operación `encryptUsingPassword` del servicio Encryption.

**Consulte también**

[Definir opciones de guardado de documentos de PDF mediante la API de Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir opciones de guardado de documentos de PDF mediante la API de servicio web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Cifrar documentos de PDF con una contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Definir opciones de guardado de documentos de PDF mediante la API de Java {#set-pdf-document-save-options-using-the-java-api}

Defina las opciones de guardado de documentos de PDF mediante la API de Utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Configuración del modo Guardar

   * Crear un objeto `PDFUtilitySaveMode` mediante su constructor.
   * Establezca el modo de guardado invocando el método `setSaveStyle` del objeto `PDFUtilitySaveMode` y pasando un valor de cadena que especifica el modo de guardado. Por ejemplo, para guardar para ver rápidamente en la web, pase `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el método `setSaveMode` del objeto `PDFUtilityServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento de PDF.
   * Objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Valor booleano que se utiliza para determinar si se debe anular la configuración anterior.

   El método devuelve un objeto `com.adobe.idp.Document` al que se ha dado formato utilizando el estilo de guardado especificado.

1. Pase el documento de PDF a otra operación de AEM Forms

   * Pase el objeto `com.adobe.idp.Document` devuelto a otra operación de AEM Forms.

**Consulte también**

[Estableciendo modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Definir opciones de guardado de documentos de PDF mediante la API de servicio web {#set-pdf-document-save-options-using-the-web-service-api}

Establezca las opciones de guardado de documentos de PDF mediante la API de utilidades de PDF (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de PDF.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceService` con el constructor de clase de proxy.

1. Configuración del modo Guardar

   * Crear un objeto `PDFUtilitySaveMode` mediante su constructor.
   * Establezca el modo de guardado asignando un valor de cadena al método `saveStyle` del objeto `PDFUtilitySaveMode` que especifica el modo de guardado. Por ejemplo, para guardar para la visualización rápida en la web, especifique `FAST_WEB_VIEW`.

1. Invocar la operación de guardar estilo

   Invoque el método `setSaveMode` del objeto `PDFUtilityServiceService` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento de PDF.
   * Objeto `PDFUtilitySaveMode` que contiene el estilo de guardado que se va a utilizar.
   * Valor booleano que se utiliza para determinar si se debe anular la configuración anterior.

   El método devuelve un objeto `BLOB` al que se ha dado formato utilizando el estilo de guardado especificado. A continuación, puede guardar ese objeto como un documento de PDF.

1. Pase el documento de PDF a otra operación de Forms

   * Pase el objeto `BLOB` devuelto a otra operación de AEM Forms.

**Consulte también**

[Estableciendo modos de guardado de documentos de PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanear documentos de PDF {#sanitizing-pdf-documents}

Puede utilizar las API de Java de Utilidades de PDF para convertir mediante programación documentos de PDF en documentos XDP.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de PDF, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-4}

Para sanear el documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDFUtilityService.
1. Invoque la operación de desinfección.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Para crear una aplicación cliente con Java, incluya los archivos JAR necesarios.

**Crear un cliente de PDFUtilityService**

Para poder realizar mediante programación una operación de saneamiento, debe crear un cliente PDFUtilityService. Con la API de Java, esto se logra creando un objeto `PDFUtilityServiceClient`.

**Invocar la operación de conversión de PDF a XDP**

Después de crear el cliente de servicios, puede invocar la operación de saneamiento.

**Consulte también**

[Convertir documentos de PDF en documentos XDP mediante la API de Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversión de documentos de PDF en documentos XDP mediante la API de servicio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Limpieza de documentos de PDF mediante la API de Java {#sanitize-pdf-documents-using-the-java-api}

Limpieza de documentos mediante la API de utilidades de PDF (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

1. Crear un cliente de PDFUtilityService

   Cree un objeto `PDFUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de conversión de PDF a XDP

   Para realizar la conversión, invoque el método `convertPDFtoXDP` del objeto `PDFUtilityServiceClient` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que representa el archivo XDP recién creado.

**Consulte también**

[Sanear documentos de PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
