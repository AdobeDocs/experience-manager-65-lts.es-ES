---
title: Creación dinámica de documentos DDX
description: Cree un documento DDX de forma dinámica mediante la API de Java y la API de servicio web. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX que se obtienen durante el tiempo de ejecución.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# Creación dinámica de documentos DDX {#dynamically-creating-ddx-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede crear dinámicamente un documento DDX que se pueda utilizar para realizar una operación de Assembler. La creación dinámica de un documento DDX permite utilizar valores en el documento DDX que se obtienen durante el tiempo de ejecución. Para crear dinámicamente un documento DDX, utilice clases que pertenezcan al lenguaje de programación que esté utilizando. Por ejemplo, si está desarrollando la aplicación cliente mediante Java, utilice clases que pertenezcan al paquete `org.w3c.dom.*`. Del mismo modo, si utiliza Microsoft .NET, utilice clases que pertenezcan al espacio de nombres `System.Xml`.

Antes de pasar el documento DDX al servicio Assembler, convierta el XML de una instancia de `org.w3c.dom.Document` a una instancia de `com.adobe.idp.Document`. Si utiliza servicios web, convierta el XML del tipo de datos utilizado para crear el XML (por ejemplo, `XmlDocument`) a una instancia de `BLOB`.

Para esta discusión, suponga que el siguiente documento DDX se crea dinámicamente.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta un documento de PDF. Se recomienda estar familiarizado con el desmontaje de documentos de PDF.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento de PDF mediante un documento DDX creado dinámicamente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Cree el documento DDX.
1. Convierta el documento DDX.
1. Establecer opciones en tiempo de ejecución.
1. Desmontar el documento de PDF.
1. Guarde los documentos de PDF desensamblados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, cree un cliente de servicio Assembler.

**Crear el documento DDX**

Cree un documento DDX utilizando el lenguaje de programación que está utilizando. Para crear un documento DDX que desensamble un documento de PDF, asegúrese de que contenga el elemento `PDFsFromBookmarks`. Convierta el tipo de datos utilizado para crear el documento DDX a una instancia de `com.adobe.idp.Document` si utiliza la API de Java. Si utiliza servicios web, convierta el tipo de datos a una instancia de `BLOB`.

**Convertir el documento DDX**

Un documento DDX creado con `org.w3c.dom` clases debe convertirse en un objeto `com.adobe.idp.Document`. Para realizar esta tarea al utilizar la API de Java, utilice las clases de transformación XML de Java. Si utiliza servicios web, convierta el documento DDX en un objeto `BLOB`.

**Hacer referencia a un documento de PDF para desmontar**

Para desmontar un documento de PDF, haga referencia a un archivo de PDF que represente el documento de PDF que desea desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento de PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para establecer las opciones en tiempo de ejecución, se usa un objeto `AssemblerOptionSpec`.

**Desmontar el documento de PDF**

Quite el documento de PDF invocando la operación `invokeDDX`. Pase el documento DDX creado dinámicamente. El servicio Assembler devuelve documentos de PDF desensamblados dentro de un objeto de colección.

**Guardar los documentos de PDF desensamblados**

Todos los documentos de PDF desensamblados se devuelven dentro de un objeto de colección. Recorra en iteración el objeto de colección y guarde cada documento de PDF como un archivo de PDF.

**Consulte también**

[Crear dinámicamente un documento DDX mediante la API de Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Crear dinámicamente un documento DDX mediante la API de servicio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontaje programático de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Crear dinámicamente un documento DDX mediante la API de Java {#dynamically-create-a-ddx-document-using-the-java-api}

Cree de forma dinámica un documento DDX y desmonte un documento de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Cree el documento DDX.

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `newInstance` de la clase `DocumentBuilderFactory`.
   * Cree un objeto Java `DocumentBuilder` llamando al método `newDocumentBuilder` del objeto `DocumentBuilderFactory`.
   * Llame al método `newDocument` del objeto `DocumentBuilder` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del documento DDX invocando el método `createElement` del objeto `org.w3c.dom.Document`. Este método crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `setAttribute`. Finalmente, agregue el elemento al elemento header llamando al método `appendChild` del elemento header y pase el objeto del elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Cree el elemento `PDFsFromBookmarks` llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. Establezca un valor para el elemento `PDFsFromBookmarks` llamando a su método `setAttribute`. Anexe el elemento `PDFsFromBookmarks` al elemento `DDX` llamando al método `appendChild` del elemento DDX. Pase el objeto de elemento `PDFsFromBookmarks` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Cree un elemento `PDF` llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento. Convertir el valor devuelto en `Element`. Establezca un valor para el elemento `PDF` llamando a su método `setAttribute`. Anexe el elemento `PDF` al elemento `PDFsFromBookmarks` llamando al método `appendChild` del elemento `PDFsFromBookmarks`. Pase el objeto de elemento `PDF` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convierta el documento DDX.

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método `newInstance` estático del objeto `javax.xml.transform.Transformer`.
   * Cree un objeto `Transformer` invocando el método `newTransformer` del objeto `TransformerFactory`.
   * Crear un objeto `ByteArrayOutputStream` mediante su constructor.
   * Crear un objeto `javax.xml.transform.dom.DOMSource` mediante su constructor. Pase el objeto `org.w3c.dom.Document` que representa el documento DDX.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `transform` del objeto `javax.xml.transform.Transformer`. Pase los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `toByteArray` del objeto `ByteArrayOutputStream`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando la matriz de bytes.

1. Hacer referencia a un documento de PDF para desmontar.

   * Cree un objeto `java.util.Map` que se use para almacenar documentos de PDF de entrada mediante un constructor `HashMap`.
   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF que desea desmontar.
   * Crear un objeto `com.adobe.idp.Document`. Pase el objeto `java.io.FileInputStream` que contiene el documento de PDF que se va a desmontar.
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (En el documento DDX creado dinámicamente, el valor es `AssemblerResultPDF.pdf`).
      * Objeto `com.adobe.idp.Document` que contiene el documento de PDF que se va a desmontar.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Desmontar el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX creado dinámicamente
   * Objeto `java.util.Map` que contiene el documento de PDF que se va a desmontar
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluidas la fuente predeterminada y el nivel de registro del trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desensamblados y las excepciones que se han producido.

1. Guarde los documentos de PDF desensamblados.

   Para obtener los documentos de PDF desensamblados, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Este método devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Creación dinámica de un documento DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Crear dinámicamente un documento DDX mediante la API de servicio web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Cree de forma dinámica un documento DDX y descombine un documento de PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al establecer una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Cree el documento DDX.

   * Crear un objeto `System.Xml.XmlElement` mediante su constructor.
   * Cree el elemento raíz del documento DDX invocando el método `CreateElement` del objeto `XmlElement`. Este método crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. Establezca un valor para el elemento DDX llamando a su método `SetAttribute`. Finalmente, anexe el elemento al documento DDX llamando al método `AppendChild` del objeto `XmlElement`. Pase el objeto DDX como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Cree el elemento `PDFsFromBookmarks` del documento DDX llamando al método `CreateElement` del objeto `XmlElement`. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. A continuación, establezca un valor para el elemento llamando a su método `SetAttribute`. Anexe el elemento `PDFsFromBookmarks` al elemento raíz llamando al método `AppendChild` del elemento `DDX`. Pase el objeto de elemento `PDFsFromBookmarks` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Cree el elemento `PDF` del documento DDX llamando al método `CreateElement` del objeto `XmlElement`. Pase un valor de cadena que represente el nombre del elemento al método `CreateElement`. A continuación, establezca un valor para el elemento secundario llamando a su método `SetAttribute`. Anexe el elemento `PDF` al elemento `PDFsFromBookmarks` llamando al método `AppendChild` del elemento `PDFsFromBookmarks`. Pase el objeto de elemento `PDF` como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convierta el documento DDX.

   * Crear un objeto `System.IO.MemoryStream` mediante su constructor.
   * Rellene el objeto `MemoryStream` con el documento DDX mediante el objeto `XmlElement` que representa el documento DDX. Invoque el método `Save` del objeto `XmlElement` y pase el objeto `MemoryStream`.
   * Cree una matriz de bytes y rellénela con datos en el objeto `MemoryStream`. El siguiente código muestra esta lógica de aplicación:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crear un objeto `BLOB`. Asigne la matriz de bytes al campo `MTOM` del objeto `BLOB`.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada. Este objeto `BLOB` se pasó a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF de entrada y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` al contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Desmontar el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX creado dinámicamente
   * La matriz `mapItem` que contiene el documento de PDF de entrada
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos de PDF desensamblados.

   Para obtener los documentos de PDF recién creados, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF desensamblados.
   * Recorra en iteración el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al tener acceso a la propiedad `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
