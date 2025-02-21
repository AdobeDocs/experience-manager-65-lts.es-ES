---
title: Agrupar documentos PDF cifrados
description: Ensamble documentos de PDF cifrados mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 4%

---

# Agrupar documentos PDF cifrados {#assembling-encrypted-pdf-documents}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede cifrar un documento de PDF con una contraseña utilizando el servicio Assembler. Una vez que un documento PDF esté cifrado con una contraseña, los usuarios deberán especificar la contraseña para ver el documento PDF en Adobe Reader o Acrobat. Para cifrar un documento PDF con una contraseña, el documento DDX debe contener valores de elementos de cifrado necesarios para cifrar un documento PDF.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

Dentro de este documento DDX, observe que el atributo de origen tiene asignado el valor `inDoc`. En situaciones en las que solo se pase un documento de PDF de entrada al servicio Assembler y se devuelva un documento de PDF y se invoque la operación `invokeOneDocument`, asigne el valor `inDoc` al atributo de origen de PDF. Al invocar la operación `invokeOneDocument`, el valor `inDoc` es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos de PDF de entrada al servicio Assembler, puede invocar la operación `invokeDDX`. En este caso, asigne el nombre de archivo del documento de PDF de entrada al atributo `source`.

El servicio Encryption no tiene que formar parte de la instalación de AEM Forms para cifrar un documento de PDF con una contraseña. Consulte [Cifrar y descifrar documentos de PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF cifrado, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF no seguro.
1. Establecer opciones en tiempo de ejecución.
1. Cifre el documento.
1. Guarde el documento cifrado de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluyendo los archivos de la biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para cifrar un documento de PDF, el documento DDX debe contener el elemento `PasswordEncryptionProfile`.

**Hacer referencia a un documento de PDF no protegido**

Se debe hacer referencia a un documento de PDF no protegido y pasarlo al servicio Assembler para cifrarlo. Si hace referencia a un documento de PDF que ya está cifrado, se produce una excepción.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la referencia de clase `AssemblerOptionSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Cifrar el documento**

Después de crear el cliente de servicio Assembler, hacer referencia al documento DDX que contiene información de cifrado, hacer referencia a un documento de PDF no protegido y establecer opciones en tiempo de ejecución, puede invocar la operación `invokeOneDocument`. Dado que solo se pasa un documento de entrada de PDF al servicio Assembler (y se devuelve un documento), puede utilizar la operación `invokeOneDocument` en lugar de la operación `invokeDDX`.

**Guardar el documento cifrado de PDF**

Si solo se pasa un documento de PDF al servicio Assembler, el servicio Assembler devuelve un solo documento en lugar de un objeto de colección. Es decir, al invocar la operación `invokeOneDocument`, se devuelve un solo documento. Dado que el documento DDX al que se hace referencia en esta sección contiene información de cifrado, el servicio Assembler devuelve un documento de PDF cifrado con una contraseña.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar un documento de PDF cifrado mediante la API de Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a un documento de PDF no seguro.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación de un documento de PDF no protegido.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF. Este objeto `com.adobe.idp.Document` se ha pasado al método `invokeOneDocument`.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Cifre el documento.

   Invoque el método `invokeOneDocument` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` para el elemento de origen PDF.
   * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF no protegido.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo.

   El método `invokeOneDocument` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF cifrado con contraseña.

1. Guarde el documento cifrado de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `Document` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` que devolvió el método `invokeOneDocument`.

**Consulte también**

[Inicio rápido (modo SOAP): Combinar un documento de PDF cifrado mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Montar un documento de PDF cifrado mediante la API de servicio web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al establecer una referencia de servicio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de Assembler.

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
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF no seguro.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada. Este objeto `BLOB` se pasó a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Cifre el documento.

   Invoque el método `invokeOneDocument` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * Un objeto `BLOB` que representa el documento de PDF no protegido
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeOneDocument` devuelve un objeto `BLOB` que contiene un documento de PDF cifrado.

1. Guarde el documento cifrado de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF cifrado y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `invokeOneDocument`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
