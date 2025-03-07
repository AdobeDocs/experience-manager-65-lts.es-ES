---
title: Agrupar documentos PDF no interactivos
description: Utilice un formulario PDF no interactivo como entrada para combinar un documento de PDF no interactivo mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: fc5ea2a6-79b4-436e-b5bc-c4beaf3619ee
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Agrupar documentos PDF no interactivos {#assembling-non-interactive-pdf-documents}

Puede combinar un documento de PDF no interactivo al utilizar un formulario interactivo de PDF como entrada. Es decir, supongamos que tiene un formulario que los usuarios pueden utilizar para introducir datos en sus campos. Puede pasar ese formulario al servicio Assembler, lo que hace que el servicio Assembler devuelva un documento de PDF que impide que los usuarios introduzcan datos en sus campos. Este documento es un formulario no interactivo de PDF. Por ejemplo, la siguiente ilustración muestra una solicitud hipotecaria que representa un formulario interactivo.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Dentro de este documento DDX, observe que el atributo de origen tiene asignado el valor `inDoc`. En situaciones en las que solo se pase un documento de PDF de entrada al servicio Assembler y se devuelva un documento de PDF y se invoque la operación `invokeOneDocument`, asigne el valor `inDoc` al atributo de origen de PDF. Al invocar la operación `invokeOneDocument`, el valor `inDoc` es una clave predefinida que debe especificarse en el documento DDX.

Por el contrario, al pasar dos o más documentos de PDF de entrada al servicio Assembler, puede invocar la operación `invokeDDX`. En este caso, asigne el nombre de archivo del documento de PDF de entrada al atributo `source`.

Este documento DDX contiene el elemento `NoXFA`, que indica al servicio Assembler que devuelva un documento de PDF no interactivo.

El servicio Assembler puede ensamblar documentos de PDF no interactivos sin que el servicio Output forme parte de la instalación de formularios de AEM si el documento de PDF de entrada se basa en un formulario de Acrobat o en un formulario XFA estático. Sin embargo, si el documento de PDF de entrada es un formulario XFA dinámico, el servicio Output debe formar parte de la instalación de formularios AEM. Si el servicio Output no forma parte de la instalación de AEM Forms cuando se monta un formulario XFA dinámico, se genera una excepción. Consulte [Creación de flujos de salida de documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como, por ejemplo, la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Ensamblar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF no interactivo, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento interactivo de PDF.
1. Establecer opciones en tiempo de ejecución.
1. Monte el documento de PDF.
1. Guarde el documento no interactivo de PDF.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

**Crear un cliente Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento PDF. Este documento DDX debe contener el elemento `NoXFA`, que indica al servicio Assembler que devuelva un documento de PDF no interactivo.

**Hacer referencia a un documento interactivo de PDF**

Se debe hacer referencia a un documento interactivo de PDF y pasarlo al servicio Assembler para recuperar un documento no interactivo de PDF.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar el documento de PDF**

Después de crear el cliente del servicio Assembler, hacer referencia al documento DDX, hacer referencia a un documento interactivo de PDF y establecer las opciones en tiempo de ejecución, puede invocar la operación `invokeOneDocument`. Dado que solo se pasa un documento de PDF de entrada al servicio Assembler y se devuelve un solo documento, puede utilizar la operación `invokeOneDocument` en lugar de la operación `invokeDDX`.

**Guardar el documento no interactivo de PDF**

Si solo se pasa un documento de PDF al servicio Assembler, el servicio Assembler devuelve un solo documento en lugar de un objeto de colección. Es decir, al invocar la operación `invokeOneDocument`, se devuelve un solo documento. Dado que el documento DDX al que se hace referencia en esta sección contiene instrucciones para crear un documento de PDF no interactivo, el servicio Assembler devuelve un documento de PDF no interactivo que se puede guardar como archivo de PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar un documento no interactivo de PDF mediante la API de Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Ensamble un documento no interactivo de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a un documento interactivo de PDF.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación de un documento interactivo de PDF.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF. Este objeto `com.adobe.idp.Document` se ha pasado al método `invokeOneDocument`.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Monte el documento de PDF.

   Invoque el método `invokeOneDocument` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX. Asegúrese de que este documento DDX contenga el valor `inDoc` para el elemento de origen PDF.
   * Un objeto `com.adobe.idp.Document` que contiene el documento interactivo de PDF.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo.

   El método `invokeOneDocument` devuelve un objeto `com.adobe.idp.Document` que contiene un documento de PDF no interactivo.

1. Guarde el documento no interactivo de PDF.

   * Cree un objeto `java.io.File` y asegúrese de que la extensión de nombre de archivo sea .pdf.
   * Invoque el método `copyToFile` del objeto `Document` para copiar el contenido del objeto `Document` en el archivo. Asegúrese de utilizar el objeto `Document` que devolvió el método `invokeOneDocument`.

* &quot;Inicio rápido (modo SOAP): Combinar un documento de PDF no interactivo con la API de Java&quot;

## Montar un documento no interactivo de PDF mediante la API de servicio web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Ensamble un documento no interactivo de PDF mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento interactivo de PDF.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada. Este objeto `BLOB` se pasó a `invokeOneDocument` como argumento.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Monte el documento de PDF.

   Invoque el método `invokeOneDocument` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * Un objeto `BLOB` que representa el documento interactivo de PDF
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeOneDocument` devuelve un objeto `BLOB` que contiene un documento de PDF no interactivo.

1. Guarde el documento no interactivo de PDF.

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento no interactivo de PDF y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` devuelto por el método `invokeOneDocument`. Rellene la matriz de bytes obteniendo el valor del campo `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

* &quot;Inicio rápido (MTOM): Combinar un documento de PDF no interactivo mediante la API de servicio web&quot;.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
