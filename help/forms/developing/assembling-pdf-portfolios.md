---
title: Agrupar portfolios PDF
description: Montar un portafolio de PDF para combinar varios documentos de varios tipos, incluidos archivos de Word, archivos de imagen y documentos de PDF. Puede combinar un portafolio de PDF mediante una API de Java y una API de servicio web.
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
exl-id: 43460ac1-a152-4a0d-943f-1b3ed007f089
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# Agrupar portfolios PDF {#assembling-pdf-portfolios}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede combinar un Portfolio de PDF mediante el Java del ensamblador y la API de servicio web. Un portafolio puede combinar varios documentos de varios tipos, incluidos archivos de Word, archivos de imagen (por ejemplo, un archivo JPEG) y documentos de PDF. El diseño del portafolio se puede establecer en diferentes estilos, como el diseño de *cuadrícula con vista previa*, el diseño de *en una imagen* o incluso *revolución*.

La siguiente ilustración es una captura de pantalla de un portafolio con diseño de estilo *En una imagen*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creación de una Portfolio de PDF sirve como alternativa sin papel a pasar una colección de documentos. Con AEM Forms puede crear portafolios invocando el servicio Assembler con un documento DDX estructurado. El siguiente documento DDX es un ejemplo de documento DDX que crea un PDF Portfolio.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

El documento DXX debe contener una etiqueta `Portfolio` con una etiqueta `Navigator` anidada. Tenga en cuenta que la etiqueta `<Resource name="navigator/image.xxx" source="myImage.png"/>` solo es necesaria si `myNavigator` se asigna como el navegador de diseño onImage: `AdobeOnImage.nav`. Esta etiqueta permite al servicio Assembler seleccionar la imagen que se utilizará como fondo del portafolio. Incluya las etiquetas `PackageFiles` y `File` para definir el nombre de archivo y el tipo MIME del archivo empaquetado.

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para crear un Portfolio de PDF, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Consulte los documentos necesarios.
1. Establecer opciones en tiempo de ejecución.
1. Organice el portafolio.
1. Guarde el portafolio ensamblado.

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

Se debe hacer referencia a un documento DDX para ensamblar un Portfolio de PDF. Este documento DDX debe contener los elementos `Portfolio`, `Navigator` y `PackageFiles`.

**Hacer referencia a los documentos necesarios**

Para montar un Portfolio de PDF, haga referencia a todos los archivos que representan los documentos que se van a montar. Por ejemplo, pase todos los archivos de imagen especificados en el documento DDX al servicio Assembler. Observe que se hace referencia a estos archivos en el documento DDX especificado en esta sección: *myImage.png* y *saint_bernard.jpg*.

Al combinar una Portfolio de PDF, pase un archivo NAV (un archivo del navegador) al servicio Assembler. El archivo NAV que pasa al servicio Assembler depende del tipo de PDF Portfolio que se va a crear. Por ejemplo, para crear un diseño de *On an Image*, pase el archivo AdobeOnImage.nav. Puede localizar archivos NAV en la siguiente carpeta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie el archivo NAV del directorio de instalación de Acrobat 9 (o posterior). Coloque el archivo NAV en una ubicación donde la aplicación cliente pueda acceder a él. Todos los archivos se pasan al servicio Assembler dentro de un objeto de la colección Map.

>[!NOTE]
>
>Los inicios rápidos asociados con el ensamblado de portafolios de PDF utilizan AdobeOnImage.nav.

**Establecer opciones en tiempo de ejecución**

Puede establecer opciones en tiempo de ejecución que controlen el comportamiento del servicio Assembler mientras realiza un trabajo. Por ejemplo, puede establecer una opción que indique al servicio Assembler que continúe procesando un trabajo si se produce un error.

**Montar el portafolio**

Para ensamblar un Portfolio de PDF, llame a la operación `invokeDDX`. El servicio Assembler devuelve el Portfolio de PDF dentro de un objeto de colección.

**Guardar el portafolio ensamblado**

Se devuelve un Portfolio de PDF dentro de un objeto de colección. Itere por el objeto de colección y guarde PDF Portfolio como archivo de PDF.

**Consulte también**

[Montar un Portfolio de PDF mediante la API de Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Montar un Portfolio de PDF mediante la API de servicio web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar un Portfolio de PDF mediante la API de Java {#assemble-a-pdf-portfolio-using-the-java-api}

Montar un Portfolio de PDF mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Consulte los documentos necesarios.

   * Cree un objeto `java.util.Map` que se use para almacenar documentos de PDF de entrada mediante un constructor `HashMap`.
   * Crear un objeto `java.io.FileInputStream` mediante su constructor. Pase la ubicación del archivo NAV requerido (repita esta tarea con cada archivo necesario para crear un portafolio).
   * Cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el archivo NAV (repita esta tarea para cada archivo necesario para crear un portafolio).
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen especificado en el documento DDX. (repita esta tarea para cada archivo necesario para crear un portafolio).
      * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF. (repita esta tarea para cada archivo necesario para crear un portafolio).

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca opciones en tiempo de ejecución para satisfacer sus necesidades empresariales invocando un método que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, invoque el método `setFailOnError` del objeto `AssemblerOptionSpec` y pase `false`.

1. Organice el portafolio.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX que se va a utilizar
   * Un objeto `java.util.Map` que contiene los archivos necesarios para generar un Portfolio de PDF.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones de tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro del trabajo

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene el PDF Portfolio ensamblado y las excepciones que se han producido.

1. Guarde el portafolio ensamblado.

   Para obtener PDF Portfolio, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Este método devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document` resultante.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer PDF Portfolio.

**Consulte también**

[Inicio rápido (modo SOAP): Agrupar portafolios de PDF mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar un Portfolio de PDF mediante la API de servicio web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Montar un Portfolio de PDF mediante la API del servicio Assembler (servicio web):

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento DDX y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.

1. Consulte los documentos necesarios.

   * Para cada archivo de entrada, cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se usa para almacenar el archivo de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación del archivo de entrada y el modo en que se debe abrir el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los archivos de entrada necesarios para crear un Portfolio de PDF.
   * Para cada archivo de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento especificado en el documento DDX. (Realice esta tarea para cada archivo de entrada).
   * Asigne el objeto `BLOB` que almacena el archivo de entrada al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Realice esta tarea para cada documento de PDF de entrada).
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento de PDF de entrada).

1. Establecer opciones en tiempo de ejecución.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca las opciones en tiempo de ejecución para satisfacer sus necesidades comerciales asignando un valor a un miembro de datos que pertenezca al objeto `AssemblerOptionSpec`. Por ejemplo, para indicar al servicio Assembler que continúe procesando un trabajo cuando se produzca un error, asigne `false` al miembro de datos `failOnError` del objeto `AssemblerOptionSpec`.

1. Organice el portafolio.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los archivos necesarios
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución

   El método `invokeDDX` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Guarde el portafolio ensamblado.

   Para obtener el PDF Portfolio recién creado, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF resultantes.
   * Recorra en iteración el objeto `Map` para obtener cada documento resultante. A continuación, convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al tener acceso a la propiedad `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
