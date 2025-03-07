---
title: Agrupar documentos PDF con marcadores
description: Utilice el servicio Assembler para modificar un documento de PDF que no contenga marcadores para incluirlos mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services
hide: true
hidefromtoc: true
exl-id: 40fbbef6-3a2e-455d-81a3-23c7e322c0fb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# Agrupar documentos PDF con marcadores {#assembling-pdf-documents-with-bookmarks}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede combinar un documento de PDF que contenga marcadores. Por ejemplo, suponga que tiene un documento de PDF que no contiene marcadores y que desea modificarlo proporcionando marcadores. Con el servicio Assembler, puede pasarle un documento de PDF que no contenga marcadores y recuperar un documento de PDF que los contenga.

Los marcadores contienen las siguientes propiedades:

* Título que aparece como texto en la pantalla.
* Una acción que especifica lo que sucede cuando un usuario hace clic en el marcador. La acción típica de un marcador es moverse a otra ubicación en el documento actual o abrir otro documento de PDF, aunque se pueden especificar otras acciones.

A los efectos de este análisis, supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Dentro de este documento DDX, observe que el atributo de origen tiene asignado el valor `Loan.pdf`. Este documento DDX especifica que se pasa un solo documento de PDF al servicio Assembler. Al combinar un documento de PDF con marcadores, debe especificar un documento XML de marcador que describa los marcadores en el documento resultante. Para especificar un documento XML de marcador, asegúrese de que el elemento `Bookmarks` se especifica en el documento DDX.

En este documento DDX de ejemplo, el elemento `Bookmarks` especifica `doc2` como valor. Este valor indica que el mapa de entrada pasado al servicio Assembler contiene una clave denominada `doc2`. El valor de la clave `doc2` es un valor `com.adobe.idp.Document` que representa el documento XML de marcador. (Consulte &quot;Idioma de marcadores&quot; en [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63)).

En este tema se utiliza el siguiente lenguaje de marcadores XML para combinar un documento de PDF que contenga marcadores.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Dentro de este documento XML de marcador, observe el elemento Action que define la acción que se realiza cuando un usuario hace clic en el marcador. Debajo del elemento Action está el elemento Launch que inicia aplicaciones, como NotePad y abre archivos, como archivos PDF. Para abrir un archivo PDF, debe utilizar el elemento File que especifica el archivo que se va a abrir. Por ejemplo, en el archivo XML de marcador especificado en esta sección, el nombre del archivo que se abre es LoanDetails.pdf.

>[!NOTE]
>
>Para obtener información detallada sobre las acciones compatibles, consulte &quot;`Action` elemento&quot; en [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado el documento DDX especificado en esta sección y el archivo XML de marcador como entrada, el servicio Assembler monta un documento de PDF que contiene los siguientes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Cuando un usuario hace clic en el marcador *Abrir los detalles del préstamo*, se abre LoanDetails.pdf. Del mismo modo, cuando el usuario hace clic en el marcador *Launch NotePad*, se inicia NotePad.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. En esta sección no se tratan conceptos como, por ejemplo, la creación de un objeto de colección que contenga documentos de entrada o el aprendizaje de cómo extraer los resultados del objeto de colección devuelto. (Consulte [Ensamblar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF que contenga marcadores, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a un documento de PDF al que se agregan marcadores.
1. Haga referencia al documento XML de marcador.
1. Agregue el documento de PDF y el documento XML de marcador a una colección Map.
1. Establecer opciones en tiempo de ejecución.
1. Monte el documento de PDF.
1. Guarde el documento de PDF que contiene marcadores.

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

Se debe hacer referencia a un documento DDX para combinar un documento PDF. Este documento DDX debe contener el elemento `Bookmarks`, que indica al servicio Assembler que combine un PDF que contenga marcadores. (Consulte el documento DDX mostrado anteriormente en esta sección para ver un ejemplo).

**Hacer referencia a un documento de PDF al que se agregan marcadores**

Hacer referencia a un documento de PDF al que se agregan marcadores. No importa si el documento de PDF al que se hace referencia ya contiene marcadores. Si el elemento `Bookmarks` es secundario del elemento de origen PDF, los marcadores reemplazarán a los que ya existen en el origen PDF. Sin embargo, si desea conservar los marcadores existentes, asegúrese de que `Bookmarks` sea secundario del elemento de origen de PDF. Veamos el siguiente ejemplo:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Hacer referencia al documento XML de marcador**

Para combinar un PDF que contenga marcadores nuevos, debe hacer referencia a un documento XML de marcador. El documento XML de marcador se pasa al servicio Assembler dentro del objeto de la colección Map. (Consulte el documento XML de marcadores que se muestra anteriormente en esta sección para ver un ejemplo).

>[!NOTE]
>
>Consulte &quot;Idioma de marcadores&quot; en [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Agregue el documento de PDF y el documento XML de marcador a una colección Map**

Agregue el documento de PDF al que se agregan los marcadores y el documento XML de marcador a la colección Map. Por lo tanto, el objeto de colección Map contiene dos elementos: un documento de PDF y el documento XML de marcador.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error. Para obtener información acerca de las opciones en tiempo de ejecución que puede establecer, vea la referencia de clase `AssemblerOptionSpec` en [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar el documento de PDF**

Para combinar un documento de PDF que contenga nuevos marcadores, utilice la operación `invokeDDX` del servicio Assembler. El motivo por el que debe utilizar la operación `invokeDDX` en lugar de otras operaciones del servicio Assembler como `invokeOneDocument` es porque el servicio Assembler requiere un documento XML de marcador que se pasa dentro del objeto de colección Map. Este objeto es un parámetro de la operación `invokeDDX`.

**Guarde el documento de PDF que contiene marcadores**

Extraiga los resultados del objeto de asignación devuelto y guarde el documento de PDF correspondiente. (Consulte &quot;Extraer los resultados&quot; en [Agrupar documentos PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Combinar documentos de PDF con marcadores mediante la API de Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a un documento de PDF al que se agregan marcadores.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF.

1. Haga referencia al documento XML de marcador.

   * Cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del archivo XML que representa el documento XML de marcador.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF.

1. Agregue el documento de PDF y el documento XML de marcador a una colección Map.

   * Cree un objeto `java.util.Map` que se use para almacenar tanto el documento de PDF de entrada como el documento XML de marcador.
   * Agregue el documento de PDF de entrada invocando el método `put` del objeto `java.util.Map` y pasando los argumentos siguientes:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
      * Un objeto `com.adobe.idp.Document` que contiene el documento de entrada de PDF.

   * Agregue el documento XML de marcador invocando el método `put` del objeto `java.util.Map` y pasando los argumentos siguientes:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen Bookmarks especificado en el documento DDX.
      * Un objeto `com.adobe.idp.Document` que contiene el documento XML de marcador.

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Monte el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a usar
   * Un objeto `java.util.Map` que contiene el documento de entrada de PDF y el documento XML de marcador.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde el documento de PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante. (Puede utilizar el elemento de resultado de PDF especificado en el documento DDX para obtener el documento).
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Agrupar documentos de PDF con marcadores mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Combinar documentos de PDF con marcadores mediante la API de servicio web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Ensamble un documento de PDF con marcadores mediante la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento DDX y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a un documento de PDF al que se agregan marcadores.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Haga referencia al documento XML de marcador.

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el documento XML de marcador.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Agregue el documento de PDF y el documento XML de marcador a una colección Map.

   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los documentos de PDF de entrada y el documento XML de marcador.
   * Para cada documento de PDF de entrada y el documento XML de marcador , cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX.
   * Asigne el objeto `BLOB` que almacena el documento de PDF al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento de PDF de entrada y para el documento XML de marcador).

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Monte el documento de PDF.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * La matriz `MyMapOf_xsd_string_To_xsd_anyType` que contiene los documentos de entrada
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que puedan haberse producido.

1. Guarde el documento de PDF que contiene marcadores.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF resultantes.
   * Recorra en iteración el objeto `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. Luego convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al obtener acceso al campo `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
