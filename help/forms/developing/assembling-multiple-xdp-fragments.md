---
title: Agrupar varios fragmentos XDP
description: Ensamble varios fragmentos XDP en un único documento XDP mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
docset: aem65
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# Agrupar varios fragmentos XDP{#assembling-multiple-xdp-fragments}

Puede combinar varios fragmentos XDP en un único documento XDP. Por ejemplo, considere los fragmentos XDP en los que cada archivo XDP contiene uno o más subformularios utilizados para crear un formulario de mantenimiento. La siguiente ilustración muestra la vista de esquema (representa el archivo tuc018_template_flowed.xdp utilizado en el inicio rápido *Agrupar varios fragmentos XDP*):

![am_am_formato](assets/am_am_forma.png)

La siguiente ilustración muestra la sección del paciente (representa el archivo tuc018_contact.xdp utilizado en el *inicio rápido Ensamblando varios fragmentos XDP*):

![am_am_form](assets/am_am_formb.png)

La siguiente ilustración muestra la sección de mantenimiento del paciente (representa el archivo tuc018_paciente.xdp utilizado en el *inicio rápido del ensamblado de varios fragmentos XDP*):

![am_am_formc](assets/am_am_formc.png)

Este fragmento contiene dos subformularios llamados *subPatientPhysical* y *subPatientHealth*. Se hace referencia a ambos subformularios en el documento DDX que se pasa al servicio Assembler. Con el servicio Assembler, puede combinar todos estos fragmentos XDP en un único documento XDP, como se muestra en la siguiente ilustración.

![am_am_form](assets/am_am_formd.png)

El siguiente documento DDX combina varios fragmentos XDP en un documento XDP.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

El documento DDX contiene una etiqueta XDP `result` que especifica el nombre del resultado. En este caso, el valor es `tuc018result.xdp`. Se hace referencia a este valor en la lógica de la aplicación que se utiliza para recuperar el documento XDP después de que el servicio Assembler devuelva el resultado. Por ejemplo, considere la siguiente lógica de aplicación Java que se utiliza para recuperar el documento XDP ensamblado (observe que el valor está en negrita):

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

La etiqueta `XDP source` especifica el archivo XDP que representa un documento XDP completo que se puede utilizar como contenedor para agregar fragmentos XDP o como uno de varios documentos que se anexan juntos en orden. En este caso, el documento XDP solo se utiliza como contenedor (la primera ilustración que se muestra en *Agrupar varios fragmentos XDP*). Es decir, los demás archivos XDP se colocan dentro del contenedor XDP.

Para cada subformulario, puede agregar un elemento `XDPContent` (este elemento es opcional). En el ejemplo anterior, observe que hay tres subformularios: `subPatientContact`, `subPatientPhysical` y `subPatientHealth`. Tanto el subformulario `subPatientPhysical` como el subformulario `subPatientHealth` se encuentran en el mismo archivo XDP, tuc018_paciente.xdp. El elemento de fragmento especifica el nombre del subformulario, tal como se define en Designer.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para montar varios fragmentos XDP, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a los documentos XDP.
1. Establecer opciones en tiempo de ejecución.
1. Monte los distintos documentos XDP.
1. Recupere el documento XDP ensamblado.

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

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar varios documentos XDP. Este documento DDX debe contener `XDP result`, `XDP source` y `XDPContent` elementos.

**Hacer referencia a los documentos XDP**

Para montar varios documentos XDP, haga referencia a todos los archivos XDP que se utilizan para montar el documento XDP resultante. Asegúrese de que el nombre del subformulario contenido en el documento XDP al que hace referencia el atributo `source` se especifica en el atributo `fragment`. Se define un subformulario en Designer. Por ejemplo, considere el siguiente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

El subformulario denominado *subPatientContact* debe estar en el archivo XDP denominado *tuc018_contact.xdp*.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar los múltiples documentos XDP**

Para ensamblar varios archivos XDP, llame a la operación `invokeDDX`. El servicio Assembler devuelve el documento XDP ensamblado dentro de un objeto de colección.

**Recuperar el documento XDP ensamblado**

Se devuelve un documento XDP ensamblado dentro de un objeto de colección. Itere por el objeto de colección y guarde el documento XDP como un archivo XDP. También puede pasar el documento XDP a otro servicio de AEM Forms, como Output.

**Consulte también**

[Combinar varios fragmentos XDP mediante la API de Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Combinar varios fragmentos XDP mediante la API de servicio web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Crear documentos de PDF mediante fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Combinar varios fragmentos XDP mediante la API de Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a los documentos XDP.

   * Cree un objeto `java.util.Map` que se use para almacenar documentos XDP de entrada mediante un constructor `HashMap`.
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el archivo XDP de entrada (repita esta tarea para cada archivo XDP).
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento `source` especificado en el documento DDX (repita esta tarea para cada archivo XDP).
      * Un objeto `com.adobe.idp.Document` que contiene el documento XDP que corresponde al elemento `source` (repita esta tarea para cada archivo XDP).

1. Establecer las opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Monte los distintos documentos XDP.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene los archivos XDP de entrada
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluidas la fuente predeterminada y el nivel de registro del trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el documento XDP ensamblado.

1. Recupere el documento XDP ensamblado.

   Para obtener el documento XDP ensamblado, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Este método devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento XDP ensamblado.

**Consulte también**

[Agrupar varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Inicio rápido (modo SOAP): ensamblar varios fragmentos XDP mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Incluyendo archivos de la biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Combinar varios fragmentos XDP mediante la API de servicio web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Ensamble varios fragmentos XDP utilizando la API del servicio Assembler (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL al configurar una referencia de servicio:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `AssemblerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AssemblerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio de AEM Forms (por ejemplo, `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
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
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase la matriz de bytes, la posición inicial y la longitud de la secuencia a leer.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a los documentos XDP.

   * Para cada archivo XDP de entrada, cree un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar el archivo de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase la matriz de bytes, la posición inicial y la longitud de la secuencia a leer.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un documento XDP ensamblado.
   * Para cada archivo de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo XDP de entrada).
   * Asigne el objeto `BLOB` que almacena el archivo de entrada al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Realice esta tarea para cada archivo XDP de entrada).
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento XDP de entrada).

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Monte los distintos documentos XDP.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Recupere el documento XDP ensamblado.

   Para obtener el documento XDP recién creado, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF resultantes.
   * Recorra en iteración el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al tener acceso a la propiedad `MTOM` de su objeto `BLOB`. Esto devuelve una matriz de bytes que puede escribir en un archivo XDP.

**Consulte también**

[Agrupar varios fragmentos XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Invocando AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
