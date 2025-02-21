---
title: Desmontaje programático de documentos PDF
description: Utilice el servicio Assembler para desmontar un solo documento de PDF en varios documentos de PDF mediante la API de Java y la API de servicio web.
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 2%

---

# Desmontaje programático de documentos PDF {#programmatically-disassembling-pdf-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede desmontar un documento de PDF pasándolo al servicio Assembler. Normalmente, esta tarea resulta útil cuando el documento de PDF se creó originalmente a partir de numerosos documentos individuales, como una colección de declaraciones. En la siguiente ilustración, el DocA se divide en varios documentos resultantes, donde el primer marcador de nivel 1 de una página identifica el inicio de un nuevo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar un documento de PDF, asegúrese de que el elemento `PDFsFromBookmarks` esté en el documento DDX. El elemento `PDFsFromBookmarks` es un elemento resultante y sólo puede ser un elemento secundario del elemento `DDX`. No tiene un atributo `result` porque puede generar varios documentos.

El elemento `PDFsFromBookmarks` hace que se genere un solo documento para cada marcador de nivel 1 en el documento de origen.

A los efectos de esta discusión, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. (Consulte [Ensamblar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Al pasar un solo documento de PDF al servicio Assembler y recuperar un solo documento, puede invocar la operación `invokeOneDocument`. Sin embargo, para desmontar un documento de PDF, utilice la operación `invokeDDX` porque, aunque se pasa un documento de entrada de PDF al servicio Assembler, este devuelve un objeto de colección que contiene uno o varios documentos.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para desmontar un documento de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF para desmontar.
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

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para desmontar un documento PDF. Este documento DDX debe contener el elemento `PDFsFromBookmarks`.

**Hacer referencia a un documento de PDF para desmontar**

Para desmontar un documento de PDF, haga referencia a un archivo de PDF que represente el documento de PDF que desea desmontar. Cuando se pasa al servicio Assembler, se devuelve un documento de PDF independiente para cada marcador de nivel 1 del documento.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Desmontar el documento de PDF**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento de PDF para desmontar y establecer opciones en tiempo de ejecución, puede desmontar un documento de PDF invocando el método `invokeDDX`. Siempre que el documento DDX contenga instrucciones para desmontar el documento PDF, el servicio Assembler devolverá documentos PDF desensamblados dentro de un objeto de colección.

**Guardar los documentos de PDF desensamblados**

Todos los documentos de PDF desensamblados se devuelven dentro de un objeto de colección. Recorra en iteración el objeto de colección y guarde cada documento de PDF como un archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontar un documento de PDF mediante la API de Java {#disassemble-a-pdf-document-using-the-java-api}

Desmontar un documento de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a un documento de PDF para desmontar.

   * Cree un objeto `java.util.Map` que se use para almacenar documentos de PDF de entrada mediante un constructor `HashMap`.
   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF que desea desmontar.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF que desea desmontar.
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Objeto `com.adobe.idp.Document` que contiene el documento de PDF que se va a desmontar.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Desmontar el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Objeto `java.util.Map` que contiene el documento de PDF que se va a desmontar
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluidas la fuente predeterminada y el nivel de registro del trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los documentos de PDF desensamblados y las excepciones que se han producido.

1. Guarde los documentos de PDF desensamblados.

   Para obtener los documentos de PDF desensamblados, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de PDF.

**Consulte también**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Inicio rápido (modo SOAP): Desmontaje de un documento de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desagrupar de un documento PDF mediante la API de servicio web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmontar un documento de PDF mediante la API del servicio Assembler (servicio web):

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

1. Hacer referencia a un documento DDX existente.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación de archivo del documento DDX y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF para desmontar.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada. Este objeto `BLOB` se pasó a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` al contenido de la matriz de bytes.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar el PDF que se va a desmontar.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento de PDF al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al campo `failOnError` del objeto `AssemblerOptionSpec`.

1. Desmontar el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX que desmonta el documento de PDF
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento de PDF que se va a desmontar
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde los documentos de PDF desensamblados.

   Para obtener los documentos de PDF recién creados, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF desensamblados.
   * Recorra en iteración el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al tener acceso a la propiedad `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Desmontaje programático de documentos PDF](#programmatically-disassembling-pdf-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
