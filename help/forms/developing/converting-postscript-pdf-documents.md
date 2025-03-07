---
title: Convertir documentos Postscript a PDF
description: Utilice el servicio Distiller para convertir archivos PostScript®, PostScript encapsulado (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller convierte grandes volúmenes de documentos impresos en documentos electrónicos, como facturas e instrucciones, mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 39d793ca-5909-428e-9f6e-08d587f828c0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 2%

---

# Convertir documentos Postscript a PDF {#converting-postscript-to-pdf-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio Distiller {#about-the-distiller-service}

El servicio Distiller® convierte los archivos PostScript®, Encapsulated PostScript (EPS) y PRN en archivos PDF compactos, fiables y más seguros a través de una red. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas e instrucciones. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y otra electrónica de un documento.

>[!NOTE]
>
>Para obtener más información acerca del servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversión de documentos de PostScript a PDF {#converting-postscript-to-pdf-documents-inner}

En este tema se describe cómo puede utilizar la API del servicio Distiller (Java y servicio web) para convertir mediante programación archivos PostScript (PS), PostScript encapsulado (EPS) y PRN en documentos de PDF.

>[!NOTE]
>
>Para obtener más información acerca del servicio Distiller, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para convertir archivos de PostScript en documentos de PDF, es necesario instalar uno de los siguientes en el servidor que aloja AEM Forms: Acrobat 9 o paquete redistribuible de Microsoft Visual C++ 2005.

### Resumen de los pasos {#summary-of-steps}

Para convertir cualquiera de los tipos admitidos en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de servicio de Distiller.
1. Recupere el archivo que desea convertir.
1. Invoque la operación de creación de PDF.
1. Guarde el documento de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de servicio de Distiller**

Para poder realizar mediante programación una operación de servicio de Distiller, debe crear un cliente de servicio de Distiller. Si está usando la API de Java, cree un objeto `DistillerServiceClient`. Si está usando la API del servicio web, cree un objeto `DistillerServiceService`.

**Recuperar el archivo para convertir**

Recupere el archivo que desea convertir. Por ejemplo, para convertir un archivo PS en un documento de PDF, debe recuperar el archivo PS.

**Invocar la operación de creación de PDF**

Después de crear el cliente de servicios, puede invocar la operación de creación de PDF. Esta operación necesita información sobre el documento que se va a convertir, incluida la ruta al documento de destino.

**Guardar el documento de PDF**

Puede guardar el documento de PDF como archivo de PDF.

**Consulte también**

[Conversión de un archivo PostScript a PDF mediante la API de Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversión de un archivo PostScript a PDF mediante la API de servicio web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Conversión de un archivo PostScript a PDF mediante la API de Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertir un archivo PostScript en un documento de PDF mediante la API de servicio de Distiller (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-distiller-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de servicio de Distiller.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `DistillerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recupere el archivo que desea convertir.

   * Cree un objeto `java.io.FileInputStream` que represente el archivo que se va a convertir mediante su constructor y pasando un valor de cadena que especifique la ubicación del archivo.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Invoque la operación de creación de PDF.

   Invoque el método `createPDF` del objeto `DistillerServiceClient` y pase los siguientes valores:

   * El objeto `com.adobe.idp.Document` que representa el archivo PS, EPS o PRN que se va a convertir
   * Objeto `java.lang.String` que contiene el nombre del archivo que se va a convertir
   * Objeto `java.lang.String` que contiene el nombre de la configuración de Adobe PDF que se va a usar
   * Objeto `java.lang.String` que contiene el nombre de la configuración de seguridad que se va a utilizar
   * Un objeto `com.adobe.idp.Document` opcional que contiene la configuración que se aplicará durante la generación del documento de PDF
   * Un objeto `com.adobe.idp.Document` opcional que contiene información de metadatos que se aplicará al documento de PDF

   El método `createPDF` devuelve un objeto `CreatePDFResult` que contiene el nuevo documento de PDF y un archivo de registro que se puede generar. El archivo de registro suele contener mensajes de error o advertencia generados por la solicitud de conversión.

1. Guarde el documento de PDF.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el método `getCreatedDocument` del objeto `CreatePDFResult`. Devuelve un objeto `com.adobe.idp.Document`.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de PDF.

   Del mismo modo, para obtener el documento de registro, realice las siguientes acciones.

   * Invoque el método `getLogDocument` del objeto `CreatePDFResult`. Devuelve un objeto `com.adobe.idp.Document`.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de registro.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

[Inicio rápido (modo SOAP): Conversión de un archivo de PostScript a un documento de PDF mediante la API de Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversión de un archivo PostScript a PDF mediante la API de servicio web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertir un archivo PostScript en un documento de PDF mediante la API de servicio web de Distiller (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de servicio de Distiller.

   * Cree un objeto `DistillerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DistillerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, especifique `?blob=mtom` para utilizar MTOM.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DistillerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere el archivo que desea convertir.

   * Crear un objeto `BLOB` mediante su constructor. Este objeto `BLOB` se usa para almacenar el archivo que se convertirá en un documento de PDF.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo y el modo para abrirlo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Invoque la operación de creación de PDF.

   Invoque el método `CreatePDF2` del objeto `DistillerServiceService` y pase los siguientes valores necesarios:

   * El objeto `BLOB` que representa el archivo PS que se va a convertir
   * Cadena que contiene el nombre de ruta del archivo que se va a convertir
   * Objeto de cadena que contiene la configuración de Adobe PDF que se va a utilizar (por ejemplo, `Standard`)
   * Objeto de cadena que contiene la configuración de seguridad que se va a utilizar (por ejemplo, `No Securit`y)
   * Un objeto `BLOB` opcional que contiene la configuración que se aplicará durante la generación del documento de PDF
   * Un objeto `BLOB` opcional que contiene información de metadatos que se aplicará al documento de PDF
   * Un parámetro de salida `BLOB` utilizado para almacenar el documento de PDF
   * Un parámetro de salida `BLOB` utilizado para almacenar el registro

1. Guarde el documento de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF firmado y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `CreatePDF2` (el parámetro de salida). Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Resumen de los pasos](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
