---
title: Determinar si los documentos cumplen los criterios de PDF/A
description: Utilice el servicio Assembler para determinar si un documento de PDF es compatible con PDF/A mediante la API de Java y la API de servicio web.
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
source-wordcount: '2065'
ht-degree: 2%

---

# Determinar si los documentos cumplen los criterios de PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Puede determinar si un documento de PDF es compatible con PDF/A mediante el servicio Assembler. Existe un documento PDF/A como formato de archivo diseñado para la preservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

La especificación PDF/A-1 consta de dos niveles de conformidad, a saber, A y B. La principal diferencia entre los dos niveles es la compatibilidad con la estructura lógica (accesibilidad), que no es necesaria para el nivel de conformidad B. Independientemente del nivel de conformidad, PDF/A-1 dicta que todas las fuentes estén incrustadas dentro del documento PDF/A generado. En este momento, solo se admite PDF/A-1b en la validación (y conversión).

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dentro de este documento DDX, el elemento `DocumentInformation` indica al servicio Assembler que devuelva información sobre el documento PDF de entrada. Dentro del elemento `DocumentInformation`, el elemento `PDFAValidation` indica al servicio Assembler si el documento de entrada de PDF es compatible con PDF/A.

El servicio Assembler devuelve información que especifica si el documento de PDF de entrada es compatible con PDF/A en un documento XML que contiene un elemento `PDFAConformance`. Si el documento de PDF de entrada es compatible con PDF/A, el valor del atributo `isCompliant` del elemento `PDFAConformance` es `true`. Si el documento de PDF no es compatible con PDF/A, el valor del atributo `isCompliant` del elemento `PDFAConformance` es `false`.

>[!NOTE]
>
>Dado que el documento DDX especificado en esta sección contiene un elemento `DocumentInformation`, el servicio Assembler devuelve datos XML en lugar de un documento PDF. Es decir, el servicio Assembler no monta ni desmonta un documento de PDF; devuelve información sobre el documento de PDF de entrada dentro de un documento XML.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para determinar si un documento de PDF es compatible con PDF/A, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A.
1. Establecer opciones en tiempo de ejecución.
1. Recupere información sobre el documento de PDF.
1. Guarde el documento XML devuelto.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluyendo los archivos de la biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para realizar una operación del servicio Assembler. Para determinar si un documento de PDF de entrada es compatible con PDF/A, asegúrese de que el documento DDX contenga el elemento `PDFAValidation` dentro de un elemento `DocumentInformation`. El elemento `PDFAValidation` indica al servicio Assembler que devuelva un documento XML que especifica si el documento de PDF de entrada es compatible con PDF/A.

**Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A**

Se debe hacer referencia a un documento de PDF y pasarlo al servicio Assembler para determinar si el documento de PDF es compatible con PDF/A.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la referencia de clase `AssemblerOptionSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar información acerca del documento de PDF**

Después de crear el cliente del servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento interactivo de PDF y establecer las opciones en tiempo de ejecución, puede invocar la operación `invokeDDX`. Dado que el documento DDX contiene el elemento `DocumentInformation`, el servicio Assembler devuelve datos XML en lugar de un documento de PDF.

**Guardar el documento XML devuelto**

El documento XML que devuelve el servicio Assembler especifica si el documento de PDF de entrada es compatible con PDF/A. Por ejemplo, si el documento de PDF de entrada no es compatible con PDF/A, el servicio Assembler devuelve un documento XML que contiene el siguiente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Guarde el documento XML como archivo XML para poder abrir el archivo y ver los resultados.

**Consulte también**

[Determine si un documento es compatible con PDF/A mediante la API de Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine si un documento es compatible con PDF/A mediante la API de servicio web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine si un documento es compatible con PDF/A mediante la API de Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine si un documento de PDF es compatible con PDF/A mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX. Para determinar si el documento de PDF es compatible con PDF/A, asegúrese de que el documento DDX contenga el elemento `PDFAValidation` que está contenido en un elemento `DocumentInformation`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación de un documento de PDF que se utiliza para determinar la compatibilidad con PDF/A.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream` que contiene el documento de PDF.
   * Cree un objeto `java.util.Map` que se use para almacenar el documento de PDF de entrada mediante un constructor `HashMap`.
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. Por ejemplo, el valor del elemento de origen en el documento DDX que se introduce en esta sección es Loan.pdf.
      * Un objeto `com.adobe.idp.Document` que contiene el documento de entrada de PDF.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Recupere información sobre el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene el archivo PDF de entrada que se usa para determinar la conformidad con PDF/A
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene datos XML que especifican si el documento de PDF de entrada es compatible con PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento de PDF de entrada es un documento de PDF/A, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento XML. Asegúrese de guardar los datos XML como un archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Determinando si un documento es compatible con PDF/A mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modo SOAP)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine si un documento es compatible con PDF/A mediante la API de servicio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine si un documento de PDF es compatible con PDF/A mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AssemblerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Hacer referencia a un documento DDX existente.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento DDX.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF utilizado para determinar la conformidad con PDF/A.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar el documento de PDF.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento de PDF al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Recupere información sobre el documento de PDF.

   Invoque el método `invoke` del objeto `AssemblerServiceService` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene el documento de entrada de PDF. Sus claves deben coincidir con los nombres de los archivos de origen de PDF y sus valores deben ser el objeto `BLOB` que corresponde al archivo PDF de entrada.
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `invoke` devuelve un objeto `AssemblerResult` que contiene datos XML que especifican si el documento de PDF de entrada es un documento de PDF/A.

1. Guarde el documento XML devuelto.

   Para obtener datos XML que especifiquen si el documento de PDF de entrada es un documento de PDF/A, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los datos XML que especifican si el documento de PDF de entrada es un documento de PDF/A.
   * Recorra en iteración el objeto `Map` para obtener cada documento resultante. A continuación, convierta el valor de ese miembro de la matriz a `BLOB`.
   * Extraiga los datos binarios que representan los datos XML al tener acceso al campo `MTOM` de su objeto `BLOB`. Este campo almacena una matriz de bytes en la que puede escribir como archivo XML.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
