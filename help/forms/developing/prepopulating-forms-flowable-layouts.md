---
title: Rellenado previo de Forms con diseños flexibles
description: Rellene previamente formularios con un diseño fluido para mostrar datos a los usuarios en un formulario procesado mediante la API de Java y la API de servicio web.
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 8de9682f-8332-4f6e-ac4b-295fca82a424
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 2%

---

# Rellenado previo de Forms con diseños flexibles {#prepopulating-forms-with-flowable-layouts1}

## Rellenado previo de Forms con diseños flexibles {#prepopulating-forms-with-flowable-layouts2}

Al rellenar previamente los formularios, se muestran datos a los usuarios dentro de un formulario procesado. Por ejemplo, supongamos que un usuario inicia sesión en un sitio web con un nombre de usuario y una contraseña. Si la autenticación se realiza correctamente, la aplicación cliente consulta una base de datos para obtener información del usuario. Los datos se combinan en el formulario y, a continuación, este se procesa para el usuario. Como resultado, el usuario puede ver datos personalizados dentro del formulario.

Rellenar previamente un formulario tiene las siguientes ventajas:

* Permite al usuario ver datos personalizados en un formulario.
* Reduce la cantidad de tiempo que el usuario escribe para rellenar un formulario.
* Garantiza la integridad de los datos al tener control sobre dónde se colocan.

Los dos orígenes de datos XML siguientes pueden rellenar previamente un formulario:

* Una fuente de datos XDP, que es XML que se ajusta a la sintaxis XFA (o datos XFDF para rellenar previamente un formulario creado con Acrobat).
* Fuente de datos XML arbitraria que contiene pares de nombre/valor que coinciden con los nombres de campo del formulario (los ejemplos de esta sección utilizan una fuente de datos XML arbitraria).

Debe existir un elemento XML para cada campo de formulario que desee rellenar previamente. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML, siempre y cuando se especifiquen todos los elementos XML.

Cuando se rellena previamente un formulario que ya contiene datos, se deben especificar los datos que ya se muestran en el origen de datos XML. Supongamos que un formulario que contiene 10 campos tiene datos en cuatro campos. A continuación, suponga que desea rellenar previamente los seis campos restantes. En este caso, debe especificar 10 elementos XML en la fuente de datos XML que se utiliza para rellenar previamente el formulario. Si especifica solo seis elementos, los cuatro campos originales están vacíos.

Por ejemplo, puede rellenar previamente un formulario como el formulario de confirmación de ejemplo. (Consulte &quot;Formulario de confirmación&quot; en [Procesamiento de PDF forms interactivo](/help/forms/developing/rendering-interactive-pdf-forms.md)).

Para rellenar previamente el formulario de confirmación de ejemplo, debe crear un origen de datos XML que contenga tres elementos XML que coincidan con los tres campos del formulario. Este formulario contiene los tres campos siguientes: `FirstName`, `LastName` y `Amount`. El primer paso es crear una fuente de datos XML que contenga elementos XML que coincidan con los campos del diseño de formulario. El siguiente paso es asignar valores de datos a los elementos XML, como se muestra en el siguiente código XML.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Después de rellenar previamente el formulario de confirmación con este origen de datos XML y, a continuación, procesar el formulario, se muestran los valores de datos asignados a los elementos XML, como se muestra en el diagrama siguiente.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Rellenado previo de formularios con diseños flexibles {#prepopulating_forms_with_flowable_layouts-1}

Los Forms con diseños flexibles son útiles para mostrar una cantidad indeterminada de datos a los usuarios. Dado que el diseño del formulario se ajusta automáticamente a la cantidad de datos que se combinan, no es necesario predeterminar un diseño fijo o un número de páginas para el formulario, como es necesario hacer con un formulario con un diseño fijo.

Un formulario se suele rellenar con datos que se obtienen durante el tiempo de ejecución. Como resultado, se puede rellenar previamente un formulario creando una fuente de datos XML en memoria y colocando los datos directamente en la fuente de datos XML en memoria.

Considere una aplicación basada en web, como una tienda en línea. Una vez que un comprador en línea termina de comprar artículos, todos los artículos comprados se colocan en una fuente de datos XML en memoria que se utiliza para rellenar previamente un formulario. El diagrama siguiente muestra este proceso, que se explica en la tabla siguiente.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un usuario compra artículos en una tienda en línea basada en web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Una vez que el usuario termina de comprar elementos y hace clic en el botón Enviar, se crea una fuente de datos XML en memoria. Los elementos adquiridos y la información de usuario se colocan en la fuente de datos XML en memoria. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>La fuente de datos XML se utiliza para rellenar previamente un formulario de pedido de compra (a continuación de esta tabla se muestra un ejemplo de este formulario). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario de pedido de compra se procesa en el explorador web del cliente. </p></td>
  </tr>
 </tbody>
</table>

El diagrama siguiente muestra un ejemplo de un formulario de pedido de compra. La información de la tabla se puede ajustar al número de registros de los datos XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Un formulario se puede rellenar previamente con datos de otras fuentes, como una base de datos empresarial o aplicaciones externas.

### Consideraciones del diseño del formulario {#form-design-considerations}

Forms con diseños flexibles se basan en diseños de formulario creados en Designer. Un diseño de formulario especifica un conjunto de reglas de diseño, presentación y captura de datos, incluido el cálculo de valores basado en los datos introducidos por el usuario. Las reglas se aplican cuando se introducen datos en un formulario. Los campos que se agregan a un formulario son subformularios que se encuentran dentro del diseño del formulario. Por ejemplo, en el formulario de pedido de compra que se muestra en el diagrama anterior, cada línea es un subformulario. Para obtener información acerca de cómo crear un diseño de formulario que contenga subformularios, vea [Crear un formulario de pedido de compra con un diseño variable](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9_es).

### Explicación de los subgrupos de datos {#understanding-data-subgroups}

Se utiliza una fuente de datos XML para rellenar previamente formularios con diseños fijos y diseños flexibles. Sin embargo, la diferencia radica en que un origen de datos XML que rellena previamente un formulario con un diseño variable contiene elementos XML repetidos que se utilizan para rellenar previamente subformularios que se repiten dentro del formulario. Estos elementos XML repetitivos se denominan subgrupos de datos.

Una fuente de datos XML que se utiliza para rellenar previamente el formulario de pedido de compra que se muestra en el diagrama anterior contiene cuatro subgrupos de datos repetidos. Cada subgrupo de datos corresponde a un artículo comprado. Los artículos adquiridos son un monitor, una lámpara de escritorio, un teléfono y una libreta de direcciones.

La siguiente fuente de datos XML se utiliza para rellenar previamente el formulario de pedido de compra.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Tenga en cuenta que cada subgrupo de datos contiene cuatro elementos XML que se corresponden con esta información:

* Número de pieza de artículos
* Descripción de elementos
* Cantidad de artículos
* Precio unitario

El nombre del elemento XML principal de un subgrupo de datos debe coincidir con el nombre del subformulario que se encuentra en el diseño de formulario. Por ejemplo, en el diagrama anterior, observe que el nombre del elemento XML principal del subgrupo de datos es `detail`. Corresponde al nombre del subformulario que se encuentra en el diseño de formulario en el que se basa el formulario de pedido de compra. Si el nombre del elemento XML principal del subgrupo de datos y el subformulario no coinciden, no se rellenará previamente un formulario del lado del servidor.

Cada subgrupo de datos debe contener elementos XML que coincidan con los nombres de campo del subformulario. El subformulario `detail` del diseño de formulario contiene los campos siguientes:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Si intenta rellenar previamente un formulario con un origen de datos que contiene elementos XML repetidos y establece la opción `RenderAtClient` en `No`, solo se combinará el primer registro de datos en el formulario. Para asegurarse de que todos los registros de datos se combinen en el formulario, establezca `RenderAtClient` en `Yes`. Para obtener información acerca de la opción `RenderAtClient`, consulte [Procesar Forms en el cliente](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para rellenar previamente un formulario con un diseño variable, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear una fuente de datos XML en memoria.
1. Convertir la fuente de datos XML.
1. Procesar un formulario rellenado previamente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un origen de datos XML en memoria**

Puede utilizar `org.w3c.dom` clases para crear un origen de datos XML en memoria para rellenar previamente un formulario con un diseño variable. Coloque los datos en una fuente de datos XML que se ajuste al formulario. Para obtener información acerca de la relación entre un formulario con un diseño fluido y el origen de datos XML, vea [Explicación de los subgrupos de datos](#understanding-data-subgroups).

**Convertir el origen de datos XML**

Un origen de datos XML en memoria creado mediante `org.w3c.dom` clases se puede convertir en un objeto `com.adobe.idp.Document` antes de poder utilizarlo para rellenar previamente un formulario. Una fuente de datos XML en memoria se puede convertir mediante clases de transformación XML de Java.

>[!NOTE]
>
>Si utiliza el WSDL del servicio Forms para rellenar previamente un formulario, debe convertir un objeto `org.w3c.dom.Document` en un objeto `BLOB`.

**Procesar un formulario previamente completado**

Puede procesar un formulario rellenado previamente como cualquier otro formulario. La única diferencia es que utiliza el objeto `com.adobe.idp.Document` que contiene el origen de datos XML para rellenar previamente el formulario.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rellenado previo de formularios con la API de Java {#prepopulating-forms-using-the-java-api}

Para rellenar previamente un formulario con un diseño variable mediante la API de Forms (Java), realice los siguientes pasos:

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crear una fuente de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `newInstance` de la clase `DocumentBuilderFactory`.
   * Cree un objeto Java `DocumentBuilder` llamando al método `newDocumentBuilder` del objeto `DocumentBuilderFactory`.
   * Llame al método `newDocument` del objeto `DocumentBuilder` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del origen de datos XML invocando el método `createElement` del objeto `org.w3c.dom.Document`. Esto crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, anexe el elemento raíz al documento llamando al método `appendChild` del objeto `Document` y pase el objeto del elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, agregue el elemento header al elemento raíz llamando al método `appendChild` del objeto `root` y pase el objeto header element como argumento. Los elementos XML que se anexan al elemento header corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento de encabezado llamando al método `createElement` del objeto `Document` y pase un valor de cadena que represente el nombre del elemento. Convertir el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pase el método `createTextNode` del objeto `Document` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Por último, agregue el elemento secundario al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Agregue todos los elementos restantes al elemento de encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de fuente de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups)).
   * Cree el elemento de detalle del origen de datos XML llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, anexe el elemento detail al elemento raíz llamando al método `appendChild` del objeto `root` y pase el objeto detail element como argumento. Los elementos XML anexados al elemento de detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando al método `createElement` del objeto `Document` y pase un valor de cadena que represente el nombre del elemento. Convertir el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pase el método `createTextNode` del objeto `Document` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Por último, agregue el elemento secundario al elemento de detalle llamando al método `appendChild` del elemento de detalle y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML para anexar al elemento de detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de pedido de compra, debe anexar los siguientes elementos XML al elemento de detalle: `txtDescription`, `numQty` y `numUnitPrice`.
   * Repita los dos últimos pasos secundarios para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Conversión de la fuente de datos XML

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método `newInstance` estático del objeto `javax.xml.transform.Transformer`.
   * Cree un objeto `Transformer` invocando el método `newTransformer` del objeto `TransformerFactory`.
   * Crear un objeto `ByteArrayOutputStream` mediante su constructor.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `org.w3c.dom.Document` creado en el paso 1.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `transform` del objeto `javax.xml.transform.Transformer` y pasando los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `toByteArray` del objeto `ByteArrayOutputStream`.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando la matriz de bytes.

1. Procesar un formulario rellenado previamente

   Invoque el método `renderPDFForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Asegúrese de utilizar el objeto `com.adobe.idp.Document` creado en los pasos uno y dos.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para enviar un flujo de datos de formulario al explorador web del cliente.
   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): rellenar previamente Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rellenado previo de formularios mediante la API de servicio web {#prepopulating-forms-using-the-web-service-api}

Para rellenar previamente un formulario con un diseño variable mediante la API de Forms (servicio web), realice los siguientes pasos:

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms. (Consulte [Creación de clases de proxy Java mediante Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)).
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear una fuente de datos XML en memoria

   * Cree un objeto Java `DocumentBuilderFactory` llamando al método `newInstance` de la clase `DocumentBuilderFactory`.
   * Cree un objeto Java `DocumentBuilder` llamando al método `newDocumentBuilder` del objeto `DocumentBuilderFactory`.
   * Llame al método `newDocument` del objeto `DocumentBuilder` para crear una instancia de un objeto `org.w3c.dom.Document`.
   * Cree el elemento raíz del origen de datos XML invocando el método `createElement` del objeto `org.w3c.dom.Document`. Esto crea un objeto `Element` que representa el elemento raíz. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, anexe el elemento raíz al documento llamando al método `appendChild` del objeto `Document` y pase el objeto del elemento raíz como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Cree el elemento de encabezado del origen de datos XML llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, agregue el elemento header al elemento raíz llamando al método `appendChild` del objeto `root` y pase el objeto header element como argumento. Los elementos XML que se anexan al elemento header corresponden a la parte estática del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Cree un elemento secundario que pertenezca al elemento de encabezado llamando al método `createElement` del objeto `Document` y pase un valor de cadena que represente el nombre del elemento. Convertir el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pase el método `createTextNode` del objeto `Document` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Por último, agregue el elemento secundario al elemento de encabezado llamando al método `appendChild` del elemento de encabezado y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Agregue todos los elementos restantes al elemento de encabezado repitiendo el último subpaso para cada campo que aparezca en la parte estática del formulario (en el diagrama de fuente de datos XML, estos campos se muestran en la sección A. (Consulte [Explicación de los subgrupos de datos](#understanding-data-subgroups)).
   * Cree el elemento de detalle del origen de datos XML llamando al método `createElement` del objeto `Document`. Pase un valor de cadena que represente el nombre del elemento al método `createElement`. Convertir el valor devuelto en `Element`. A continuación, anexe el elemento detail al elemento raíz llamando al método `appendChild` del objeto `root` y pase el objeto detail element como argumento. Los elementos XML anexados al elemento de detalle corresponden a la parte dinámica del formulario. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Cree un elemento secundario que pertenezca al elemento de detalle llamando al método `createElement` del objeto `Document` y pase un valor de cadena que represente el nombre del elemento. Convertir el valor devuelto en `Element`. A continuación, establezca un valor para el elemento secundario llamando a su método `appendChild` y pase el método `createTextNode` del objeto `Document` como argumento. Especifique un valor de cadena que aparezca como el valor del elemento secundario. Por último, agregue el elemento secundario al elemento de detalle llamando al método `appendChild` del elemento de detalle y pase el objeto de elemento secundario como argumento. Las siguientes líneas de código muestran esta lógica de aplicación:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita el último subpaso para todos los elementos XML para anexar al elemento de detalle. Para crear correctamente el origen de datos XML utilizado para rellenar el formulario de pedido de compra, debe anexar los siguientes elementos XML al elemento de detalle: `txtDescription`, `numQty` y `numUnitPrice`.
   * Repita los dos últimos pasos secundarios para todos los elementos de datos utilizados para rellenar previamente el formulario.

1. Conversión de la fuente de datos XML

   * Cree un objeto `javax.xml.transform.Transformer` invocando el método `newInstance` estático del objeto `javax.xml.transform.Transformer`.
   * Cree un objeto `Transformer` invocando el método `newTransformer` del objeto `TransformerFactory`.
   * Crear un objeto `ByteArrayOutputStream` mediante su constructor.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `org.w3c.dom.Document` creado en el paso 1.
   * Cree un objeto `javax.xml.transform.dom.DOMSource` utilizando su constructor y pasando el objeto `ByteArrayOutputStream`.
   * Rellene el objeto Java `ByteArrayOutputStream` invocando el método `transform` del objeto `javax.xml.transform.Transformer` y pasando los objetos `javax.xml.transform.dom.DOMSource` y `javax.xml.transform.stream.StreamResult`.
   * Cree una matriz de bytes y asigne el tamaño del objeto `ByteArrayOutputStream` a la matriz de bytes.
   * Rellene la matriz de bytes invocando el método `toByteArray` del objeto `ByteArrayOutputStream`.
   * Cree un objeto `BLOB` utilizando su constructor, invoque su método `setBinaryData` y pase la matriz de bytes.

1. Procesar un formulario rellenado previamente

   Invoque el método `renderPDFForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Asegúrese de utilizar el objeto `BLOB` creado en los pasos uno y dos.
   * Objeto `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que ha rellenado el método. Se utiliza para almacenar el formulario de PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que ha rellenado el método. (Este argumento almacenará el número de páginas en el formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que ha rellenado el método. (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `value` del objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

   >[!NOTE]
   >
   >El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
