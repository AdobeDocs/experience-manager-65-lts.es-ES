---
title: Agrupar documentos mediante la numeración Bates
description: Utilice la numeración Bates para montar documentos de PDF mediante la API de Java y del servicio web.
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
exl-id: 310d0566-673a-4b78-9f0d-86f56c495105
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 3%

---

# Agrupar documentos mediante la numeración Bates {#assembling-documents-using-bates-numbering}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede combinar documentos de PDF que contengan identificadores de página únicos mediante la numeración Bates. *La numeración Bates* es un método para aplicar identificadores únicos a un lote de documentos relacionados. A cada página del documento (o conjunto de documentos) se le asigna un número Bates que identifica de forma exclusiva la página. Por ejemplo, los documentos de fabricación que contienen información de listas de materiales y están asociados con la producción de un conjunto pueden contener un identificador. Un número Bates contiene un valor numérico incrementado secuencialmente y un prefijo y sufijo opcionales. El prefijo + numérico + sufijo se denomina *patrón de fechas*.

La siguiente ilustración muestra un documento de PDF que contiene un identificador único en el encabezado del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

A los efectos de esta discusión, el identificador único de página se coloca en el encabezado de un documento. Supongamos que se utiliza el siguiente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Este documento DDX combina dos documentos de PDF llamados *map.pdf* y *direction.pdf* en un solo documento de PDF. El documento de PDF resultante contiene un encabezado que consta de un identificador de página único. Por ejemplo, el documento de la ilustración anterior muestra 000016.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con el ensamblado de documentos de PDF mediante el servicio Assembler. En esta sección no se analizan los conceptos, como crear un objeto de colección que contenga documentos de entrada o extraer los resultados del objeto de colección devuelto. (Consulte [Ensamblar documentos de PDF mediante programación](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Assembler, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener más información sobre un documento DDX, consulte [Servicio Assembler y referencia DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumen de los pasos {#summary-of-steps}

Para combinar un documento de PDF que contenga un identificador de página único (numeración Bates), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un cliente de PDF Assembler.
1. Hacer referencia a un documento DDX existente.
1. Hacer referencia a documentos de PDF de entrada.
1. Establezca el valor inicial del número Bates.
1. Montar los documentos de PDF de entrada.
1. Extraiga los resultados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requerido si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBoss, debe reemplazar los archivos adobe-utilities.jar y jbossall-client.jar con archivos JAR específicos del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluyendo los archivos de la biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de PDF Assembler**

Para poder realizar mediante programación una operación de Assembler, debe crear un cliente de servicio Assembler.

**Hacer referencia a un documento DDX existente**

Se debe hacer referencia a un documento DDX para combinar un documento PDF. Por ejemplo, considere el documento DDX que se introdujo en esta sección. Para combinar un documento de PDF que contenga identificadores de página únicos, el documento DDX debe contener el elemento `BatesNumber`.

**Documentos de PDF de entrada de referencia**

Se debe hacer referencia a los documentos de PDF de entrada para combinar un documento de PDF. Por ejemplo, se debe hacer referencia a los documentos map.pdf y direction.pdf para combinar estos documentos de PDF en un único documento de PDF.

**Establecer el valor inicial del número Bates**

Puede establecer el valor inicial del número Bates para satisfacer sus necesidades comerciales. Por ejemplo, supongamos que es un requisito establecer el valor inicial en 000100. Si no establece el valor inicial, se 000000 el valor de la primera página.

**Montar los documentos de PDF de entrada**

Después de crear el cliente del servicio Assembler, hacer referencia al documento DDX que contiene información del elemento `BatesNumber`, hacer referencia a un documento de PDF de entrada y establecer opciones en tiempo de ejecución, puede invocar la operación `invokeDDX` que resulta en el ensamblado del servicio Assembler de un documento de PDF que contiene identificadores de página únicos.

**Extraer los resultados**

El servicio Assembler devuelve un objeto de colección que contiene los resultados del trabajo. Puede extraer el documento de PDF resultante y las excepciones que se produzcan. En este caso, se encuentra un documento de PDF cifrado dentro del objeto de colección.

>[!NOTE]
>
>Se devuelve un objeto de colección si se invoca la operación `invokeDDX`. Esta operación se utiliza al pasar dos o más documentos de PDF de entrada al servicio Assembler. Sin embargo, si sólo pasa un documento de PDF de entrada al servicio Assembler, debe invocar la operación `invokeOneDocument`. Para obtener información acerca de cómo usar esta operación, vea [Agrupar documentos cifrados de PDF](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Configuración programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Combinar documentos con la numeración Bates mediante la API de Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Ensamble un documento de PDF que utilice identificadores de página únicos (numeración Bates) mediante la API del servicio Assembler (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-assembler-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de PDF Assembler.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `AssemblerServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un documento DDX existente.

   * Cree un objeto `java.io.FileInputStream` que represente el documento DDX utilizando su constructor y pasando un valor de cadena que especifique la ubicación del archivo DDX.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Hacer referencia a documentos de PDF de entrada.

   * Crear un objeto `java.util.Map` utilizado para almacenar documentos de PDF de entrada mediante un constructor `HashMap`.
   * Para cada documento de PDF de entrada, cree un objeto `java.io.FileInputStream` utilizando su constructor y pasando la ubicación del documento de PDF de entrada. En este caso, pase la ubicación de un documento de PDF no protegido.
   * Para cada documento de PDF de entrada, cree un objeto `com.adobe.idp.Document` y pase el objeto `java.io.FileInputStream` que contiene el documento de PDF.
   * Agregue una entrada al objeto `java.util.Map` invocando su método `put` y pasando los siguientes argumentos:

      * Valor de cadena que representa el nombre de clave. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. Por ejemplo, el nombre del archivo de origen de PDF especificado en el documento DDX que se presenta en esta sección es Loan.pdf.
      * Un objeto `com.adobe.idp.Document` que contiene el documento de PDF no protegido.

1. Establezca el valor inicial del número Bates.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial invocando `setFirstBatesNumber` del objeto `AssemblerOptionSpec` y pasando un valor numérico que especifique el valor inicial.

1. Montar los documentos de PDF de entrada.

   Invoque el método `invokeDDX` del objeto `AssemblerServiceClient` y pase los siguientes valores necesarios:

   * Un objeto `com.adobe.idp.Document` que representa el documento DDX.
   * Un objeto `java.util.Map` que contiene el archivo de PDF de entrada no protegido.
   * Un objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica las opciones en tiempo de ejecución, incluida la fuente predeterminada y el nivel de registro de trabajo.

   El método `invokeDDX` devuelve un objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contiene un documento de PDF cifrado con contraseña.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Invoque el método `getDocuments` del objeto `AssemblerResult`. Esta acción devuelve un objeto `java.util.Map`.
   * Recorra en iteración el objeto `java.util.Map` hasta encontrar el objeto `com.adobe.idp.Document`.
   * Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para extraer el documento de PDF.

**Consulte también**

[Inicio rápido (modo SOAP): Combinar un documento de PDF con la numeración Bates mediante la API de Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Combinar documentos con la numeración Bates mediante la API de servicio web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Ensamble un documento de PDF que utilice identificadores de página únicos (numeración Bates) mediante la API del servicio Assembler (servicio web):

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
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento DDX y el modo para abrir el archivo en.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su campo `MTOM` con el contenido de la matriz de bytes.

1. Hacer referencia a documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, cree un objeto `BLOB` utilizando su constructor. El objeto `BLOB` se usa para almacenar el documento de PDF de entrada.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF de entrada y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
   * Rellene el objeto `BLOB` asignando su propiedad `MTOM` con el contenido de la matriz de bytes.
   * Crear un objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de colección se utiliza para almacenar los documentos de PDF de entrada.
   * Para cada documento de PDF de entrada, cree un objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Por ejemplo, si se utilizan dos documentos de PDF de entrada, cree dos objetos `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Asigne un valor de cadena que represente el nombre de clave al campo `key` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor debe coincidir con el valor del elemento de origen PDF especificado en el documento DDX. (Realice esta tarea para cada documento de PDF de entrada).
   * Asigne el objeto `BLOB` que almacena el documento de PDF al campo `value` del objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Realice esta tarea para cada documento de PDF de entrada).
   * Agregue el objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` al objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque el método `Add` del objeto `MyMapOf_xsd_string_To_xsd_anyType` y pase el objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Realice esta tarea para cada documento de PDF de entrada).

1. Establezca el valor inicial del número Bates.

   * Cree un objeto `AssemblerOptionSpec` que almacene opciones en tiempo de ejecución mediante su constructor.
   * Establezca el número Bates inicial asignando un valor numérico al miembro de datos `firstBatesNumber` que pertenece al objeto `AssemblerOptionSpec`.

1. Montar los documentos de PDF de entrada.

   Invoque el método `invoke` del objeto `AssemblerServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que representa el documento DDX.
   * El objeto `MyMapOf_xsd_string_To_xsd_anyType` que contiene los documentos de PDF de entrada. Sus claves deben coincidir con los nombres de los archivos de origen de PDF y sus valores deben ser los objetos `BLOB` que corresponden a esos archivos.
   * Un objeto `AssemblerOptionSpec` que especifica opciones en tiempo de ejecución.

   El método `invoke` devuelve un objeto `AssemblerResult` que contiene los resultados del trabajo y las excepciones que se han producido.

1. Extraiga los resultados.

   Para obtener el documento de PDF recién creado, realice las siguientes acciones:

   * Obtenga acceso al campo `documents` del objeto `AssemblerResult`, que es un objeto `Map` que contiene los documentos de PDF resultantes.
   * Recorra en iteración el objeto `Map` hasta que encuentre la clave que coincida con el nombre del documento resultante. Luego convierta el `value` de ese miembro de la matriz en un `BLOB`.
   * Extraiga los datos binarios que representan el documento de PDF al tener acceso a la propiedad `MTOM` de su objeto `BLOB`. Devuelve una matriz de bytes que puede escribir en un archivo PDF.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
