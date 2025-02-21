---
title: Servicio de Forms con códigos de barras
description: Utilice el servicio de Forms con códigos de barras de AEM Forms para extraer datos de imágenes electrónicas de códigos de barras.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Assembler,Barcoded Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 97%

---

# Servicio de Forms con códigos de barras{#barcoded-forms-service}

## Información general {#overview}

El servicio de Forms con códigos de barras extrae datos de imágenes electrónicas de códigos de barras. El servicio acepta archivos TIFF y PDF que incluyen uno o más códigos de barras como entrada y extrae los datos del código de barras. Los datos de código de barras se pueden formatear de varias formas, incluso XML, cadenas delimitadas o cualquier formato personalizado creado con JavaScript.

El servicio de Forms con códigos de barras es compatible con las siguientes simbologías **bidimensionales (2D)** suministradas como documentos TIFF o PDF escaneados:

* PDF417
* Matriz de datos
* Código QR

El servicio también es compatible con las siguientes simbologías **unidimensionales** suministradas como documentos TIFF o PDF escaneados:

* Codabar
* Código 128
* Código 3 de 9
* EAN13
* EAN8

Puede utilizar el servicio de Forms con códigos de barras para realizar las siguientes tareas:

* Extraer datos de códigos de barras de imágenes (TIFF o PDF). Los datos se almacenan como texto delimitado.
* Convierta datos de texto delimitados a XML (XDP o XFDF). Los datos XML son más fáciles de analizar que el texto delimitado. Además, los datos en formato XDP o XFDF pueden utilizarse como entrada para otros servicios en AEM Forms.

Para cada código de barras de una imagen, el servicio de Forms con códigos de barras localiza el código de barras, lo descodifica y extrae los datos. El servicio devuelve los datos del código de barras (mediante la codificación de entidad donde sea necesario) en un elemento de contenido de un documento XML. Por ejemplo, la siguiente imagen de TIFF escaneado de un formulario contiene dos códigos de barras:

![ejemplo](assets/example.png)

El servicio de Forms con códigos de barras devuelve el siguiente documento XML después de descodificar los códigos de barras:

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## Consideraciones sobre el servicio {#considerations}

### Flujos de trabajo que utilizan formularios con códigos de barras {#workflows-that-use-barcoded-forms}

Los autores de formularios crean formularios interactivos con códigos de barras mediante Designer. (Consulte [Ayuda de Designer](https://www.adobe.com/go/learn_aemforms_designer_63).) Cuando un usuario rellena un formulario con códigos de barras con Adobe Reader o Acrobat, el código de barras se actualiza automáticamente para codificar los datos del formulario.

El servicio de Forms con códigos de barras es útil para convertir los datos que existen en papel a formato electrónico. Por ejemplo, cuando se rellena e imprime un formulario con códigos de barras, la copia impresa se puede escanear y utilizar como entrada en el servicio de Forms con códigos de barras.

Los extremos de carpeta observados generalmente se utilizan para iniciar aplicaciones que utilizan el servicio de Forms con códigos de barras. Por ejemplo, los escáneres de documentos pueden guardar imágenes de TIFF o PDF de formularios con códigos de barras en una carpeta inspeccionada. El punto final de la carpeta inspeccionada pasa las imágenes al servicio para su descodificación.

### Formatos de codificación y descodificación recomendados {#recommended-encoding-and-decoding-formats}

Se recomienda a los autores de formularios con códigos de barras utilizar un formato simple y delimitado (como delimitado por tabulaciones) al codificar datos en códigos de barras. Además, evite utilizar un salto de línea como delimitador de campo. Designer proporciona una selección de codificaciones delimitadas que generan automáticamente scripts de JavaScript para codificar códigos de barras. Los datos descodificados tienen los nombres de campo en la primera línea y sus valores en la segunda línea, con pestañas entre cada campo.

Al descodificar códigos de barras, especifique el carácter que se utiliza para delimitar los campos. El carácter especificado para la descodificación debe ser el mismo que se utilizó para codificar el código de barras. Por ejemplo, al utilizar el formato delimitado por tabulaciones recomendado, la operación Extraer a XML debe utilizar el valor predeterminado de Tabulador como delimitador de campo.

### Conjuntos de caracteres especificados por el usuario {#user-specified-character-sets}

Cuando los autores de formularios agregan objetos de código de barras a sus formularios utilizando Designer, pueden especificar una codificación de caracteres. Las codificaciones reconocidas son UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16. De forma predeterminada, todos los datos se codifican en códigos de barras como UTF-8.

Al descodificar códigos de barras, puede especificar la codificación del conjunto de caracteres que va a utilizar. Para garantizar que todos los datos se descodifican correctamente, especifique el mismo conjunto de caracteres que el autor del formulario especificó cuando se diseñó el formulario.

### Limitaciones de la API {#api-limitations}

Cuando utilice las API de BCF, tenga en cuenta las siguientes limitaciones:

* Los formularios dinámicos no se admiten.
* Los formularios interactivos no se descodifican correctamente, a menos que se acoplen.
* Los códigos de barras 1D solo deben contener valores alfanuméricos (si se admiten). Los códigos de barras 1D que contienen símbolos especiales no se descodifican.

### Otras limitaciones {#other-limitations}

Además, tenga en cuenta las siguientes limitaciones al utilizar el servicio de Forms con códigos de barras:

* El servicio es totalmente compatible con AcroForms y formularios estáticos que contienen códigos de barras 2D guardados con Adobe Reader o Acrobat. Sin embargo, para los códigos de barras 1D, acople el formulario o suministre el formulario como documento PDF o TIFF escaneado.
* Los formularios XFA dinámicos no son totalmente compatibles. Para descodificar correctamente los códigos de barras 1D y 2D en un formulario dinámico, acople el formulario o suministre el formulario como documento PDF o TIFF escaneado.

Además, el servicio puede descodificar cualquier código de barras que utilice simbología admitida si se observan las limitaciones anteriores. Para obtener más información sobre cómo crear formularios interactivos con códigos de barras, consulte [Ayuda de Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Configurar propiedades del servicio   {#configureproperties}

Puede usar el **Servicio de Forms con códigos de barras de AEMFD** en la consola de AEM para configurar las propiedades de este servicio. La dirección URL predeterminada de la consola AEM es `https://[host]:'port'/system/console/configMgr`.

## Usar el servicio {#using}

El servicio de Forms con códigos de barras proporciona las dos API siguientes:

* **[decode](https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Descodifica todos los códigos de barras disponibles en un documento de PDF de entrada o en una imagen tiff. Devuelve otro documento XML que contiene datos recuperados de todos los códigos de barras disponibles en el documento de entrada o la imagen.

* **[extractToXML](https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Convierte datos descodificados mediante la API de descodificación a datos XML. Estos datos XML se pueden combinar con un formulario XFA. Devuelve una lista de documentos XML, uno para cada código de barras.

### Usar un servicio BCF con un JSP o Servlets {#using-bcf-service-with-a-jsp-or-servlets}

El siguiente código de ejemplo descodifica un código de barras en un documento y guarda el XML de salida en el disco.

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // See Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // See javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### Usar el servicio BCF con flujos de trabajo de AEM {#using-the-bcf-service-with-aem-workflows}

La ejecución del servicio Forms con códigos de barras desde un flujo de trabajo es similar a la ejecución del servicio desde JSP/Servlet. La única diferencia es que al ejecutar el servicio desde JSP/Servlet el objeto de documento recupera automáticamente una instancia del objeto ResourceResolver del objeto ResourceResolverHelper. Este mecanismo automático no funciona cuando se llama al código desde un flujo de trabajo.

Para un flujo de trabajo, pase explícitamente una instancia del objeto ResourceResolver al constructor de la clase Documento. A continuación, el objeto Documento utiliza el objeto ResourceResolver proporcionado para leer el contenido del repositorio.

El siguiente proceso de flujo de trabajo de ejemplo descodifica un código de barras en un documento y guarda el resultado en el disco. El código se escribe en ECMAScript y el documento se pasa como carga útil de flujo de trabajo:

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```
