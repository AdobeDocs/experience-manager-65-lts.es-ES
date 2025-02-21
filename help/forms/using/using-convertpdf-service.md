---
title: Servicio ConvertPDF
description: Utilice el servicio ConvertPDF de Adobe Experience Manager Forms para convertir documentos de PDF en archivos de PostScript o de imagen.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Assembler
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 95%

---

# Servicio ConvertPDF {#convertpdf-service}

## Información general {#overview}

El servicio ConvertPDF convierte los documentos PDF en archivos PostScript o de imagen (JPEG, JPEG 2000, PNG y TIFF). Convertir un documento PDF a PostScript es útil para la impresión desatendida basada en servidor en cualquier impresora PostScript. Convertir un documento PDF en un archivo TIFF de varias páginas es práctico cuando se archivan documentos en sistemas de administración de contenido que no admiten documentos PDF.

Puede realizar lo siguiente con el servicio ConvertPDF:

* Convertir documentos PDF a PostScript. Al convertir a PostScript, puede utilizar la operación de conversión para especificar el documento de origen y si desea convertir a PostScript de nivel 2 o 3. El documento PDF que convierta a un archivo PostScript no debe ser interactivo.
* Convierta documentos PDF a los formatos de imagen JPEG, JPEG 2000, PNG y TIFF. Al convertir a cualquiera de estos formatos de imagen, puede utilizar la operación de conversión para especificar el documento de origen y una especificación de opciones de imagen. La especificación contiene varias preferencias, como formato de conversión de imagen, resolución de imagen y conversión de color.

## Configurar propiedades del servicio   {#properties}

Puede usar el **Servicio ConvertPDF de AEMFD** en la consola de AEM para configurar las propiedades de este servicio. La dirección URL predeterminada de la consola AEM es `https://[host]:'port'/system/console/configMgr`.

## Usar el servicio {#using-the-service}

El servicio ConvertPDF proporciona las dos API siguientes:

* **[toPS](https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**: Convierte un documento PDF en un archivo PostScript.

* **[toImage](https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**: Convierte un documento PDF en un archivo de imagen. Los formatos de imagen compatibles son JPEG, JPEG2000, PNG y TIFF.

### Usar la API toPS con un JSP o Servlets {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### Usar la API toImage con un JSP o Servlets {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### Usar el servicio ConvertPDF con flujos de trabajo de AEM {#using-convertpdf-service-with-aem-workflows}

La ejecución del servicio ConvertPDF desde un flujo de trabajo es similar a la ejecución desde JSP/Servlet.

La única diferencia es que al ejecutar el servicio desde JSP/Servlet el objeto de documento recupera automáticamente una instancia del objeto ResourceResolver del objeto ResourceResolverHelper. Este mecanismo automático
no funciona cuando se llama al código desde un flujo de trabajo. Para un flujo de trabajo, pase explícitamente una instancia del objeto ResourceResolver al constructor de la clase Documento. A continuación, el objeto Documento utiliza
el objeto ResourceResolver proporcionado para leer el contenido del repositorio.

El siguiente proceso de flujo de trabajo de ejemplo convierte el documento de entrada en un documento PostScript. El código se escribe en ECMAScript y el documento se pasa como carga útil de flujo de trabajo:

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

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

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
