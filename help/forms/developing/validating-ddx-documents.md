---
title: Validar documentos DDX
description: Valide un documento DDX mediante programación utilizando la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 4efc6e82-f577-4881-9c9d-30e1fe2cdb9d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 2%

---

# Validar documentos DDX {#validating-ddx-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede validar mediante programación un documento DDX que utilice el servicio Assembler. Es decir, mediante la API del servicio Assembler, puede determinar si un documento DDX es válido o no. Por ejemplo, si ha actualizado desde una versión anterior de AEM Forms y desea asegurarse de que el documento DDX sea válido, puede validarlo mediante la API del servicio Assembler.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para validar un documento DDX, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de Assembler.
1. Hacer referencia a un documento DDX existente.
1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.
1. Realice la validación.
1. Guarde los resultados de validación en un archivo de registro.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Para validar un documento DDX, debe hacer referencia a un documento DDX existente.

**Establecer opciones en tiempo de ejecución para validar el documento DDX**

Al validar un documento DDX, debe establecer opciones específicas en tiempo de ejecución que indiquen al servicio Assembler que valide el documento DDX en lugar de ejecutarlo. Además, puede aumentar la cantidad de información que el servicio Assembler escribe en el archivo de registro.

**Realizar la validación**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX y establecer las opciones en tiempo de ejecución, puede invocar la operación `invokeDDX` para validar el documento DDX. Al validar el documento DDX, puede pasar `null` como el parámetro de asignación (este parámetro generalmente almacena documentos de PDF que el ensamblador requiere para realizar las operaciones especificadas en el documento DDX).

Si la validación falla, se genera una excepción y el archivo de registro contiene detalles que explican por qué el documento DDX no es válido y que se pueden obtener de la instancia `OperationException`. Una vez pasado el análisis XML básico y la comprobación de esquema, se realiza la validación con respecto a la especificación DDX. Todos los errores que se encuentran en el documento DDX se especifican en el registro.

**Guardar los resultados de validación en un archivo de registro**

El servicio Assembler devuelve los resultados de validación que se pueden escribir en un archivo de registro XML. La cantidad de detalles que el servicio Assembler escribe en el archivo de registro depende de la opción de tiempo de ejecución que se establezca.

**Consulte también**

[Validar un documento DDX mediante la API de Java](#validate-a-ddx-document-using-the-java-api)

[Validar un documento DDX mediante la API de servicio web](#validate-a-ddx-document-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar un documento DDX mediante la API de Java {#validate-a-ddx-document-using-the-java-api}

Valide un documento DDX mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX invocando el método setValidateOnly del objeto `AssemblerOptionSpec` y pasando `true`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro invocando el método `getLogLevel` del objeto `AssemblerOptionSpec` y pasando un valor de cadena que cumpla con sus requisitos. Al validar un documento DDX, desea escribir más información en el archivo de registro que ayude en el proceso de validación. Como resultado, puede pasar el valor `FINE` o `FINER`.

1. Realice la validación.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX.
   * Valor `null` para el objeto java.io.Map que generalmente almacena documentos de PDF.
   * Objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución.

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .xml.
   * Invoque el método `getJobLog` del objeto `AssemblerResult`. Este método devuelve una instancia `com.adobe.idp.Document` que contiene información de validación.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, se generará un `OperationException`. En la instrucción catch, puede invocar el método `getJobLog` del objeto `OperationException`.

**Consulte también**

[Validar documentos DDX](#validating-ddx-documents)

[Inicio rápido (modo SOAP): Validación de documentos DDX mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modo SOAP)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar un documento DDX mediante la API de servicio web {#validate-a-ddx-document-using-the-web-service-api}

Valide un documento DDX mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace localhost por la dirección IP del servidor de Forms.

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando a leer la matriz de bytes, la posición inicial y la longitud de secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Establezca las opciones en tiempo de ejecución para validar el documento DDX.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca la opción en tiempo de ejecución que indica al servicio Assembler que valide el documento DDX asignando el valor true al miembro de datos `validateOnly` del objeto `AssemblerOptionSpec`.
   * Establezca la cantidad de información que el servicio Assembler escribe en el archivo de registro asignando un valor de cadena al miembro de datos `logLevel` del objeto `AssemblerOptionSpec`. método Al validar un documento DDX, desea obtener más información escrita en el archivo de registro que le ayudará en el proceso de validación. Como resultado, puede especificar el valor `FINE` o `FINER`. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la referencia de clase `AssemblerOptionSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Realice la validación.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * Valor `null` para el objeto `Map` que generalmente almacena documentos de PDF.
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene información que especifica si el documento DDX es válido.

1. Guarde los resultados de validación en un archivo de registro.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de registro y el modo para abrir el archivo en. Asegúrese de que la extensión del nombre de archivo sea .xml.
   * Cree un objeto `BLOB` que almacene información de registro obteniendo el valor del miembro de datos `jobLog` del objeto `AssemblerResult`.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB`. Rellene la matriz de bytes obteniendo el valor del campo `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

   >[!NOTE]
   >
   >Si el documento DDX no es válido, se generará un `OperationException`. En la instrucción catch, puede obtener el valor del miembro `jobLog` del objeto `OperationException`.

**Consulte también**

[Validar documentos DDX](#validating-ddx-documents)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
