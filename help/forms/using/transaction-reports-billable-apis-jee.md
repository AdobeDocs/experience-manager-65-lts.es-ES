---
title: API facturables de informes de transacciones para AEM Forms en JEE.
description: Lista de todas las API que se contabilizan como transacciones para AEM Forms en JEE.
topic-tags: forms-manager
feature: Transaction Reports
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: 2bcd650f-c729-43b1-b7a7-9463a47ae25e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 53%

---

# API facturables de informes de transacciones para AEM Forms en JEE {#transaction-reports-billable-apis}

AEM Forms en JEE proporciona varias API para enviar, procesar y procesar documentos. Algunas API se contabilizan como transacciones y otras se pueden usar libremente. Este documento proporciona una lista de todas las API que se contabilizan como transacciones. Estos son algunos escenarios comunes en los que se utiliza un API facturable:

* Convertir un documento de un formato a otro
* Acoplar un documento PDF dinámico
* Combinar un documento PDF interactivo con otro PDF

Las API de facturación no tienen en cuenta el número de páginas, la longitud de un documento o formulario o el formato final del documento representado.
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

A continuación se muestra la lista de las API facturables de JEE. Encuentra la lista de [API facturables para AEM Forms en OSGi](/help/forms/using/transaction-reports-billable-apis.md).

## API de servicios de documentos facturables {#billable-document-services-apis}

### Generar un servicio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
   <tr>
   <td><a>Crear PDF</a></td>
   <td>Crea Adobe PDF para crear tipos de archivo compatibles.</td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>Crea Adobe PDF para crear tipos de archivo compatibles. </td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>Convierte el archivo HTML a Adobe PDF. </td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>Exporta PDF a tipos de archivo compatibles. </td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>EXPORTPDF2</a></td>
   <td><p>Exporta PDF a tipos de archivo compatibles.</p> </td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>EXPORTPDF3</a></td>
   <td>Exporta PDF a tipos de archivo compatibles.</td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>Convierte el archivo HTML a PDF.</td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>Convierte el archivo HTML a PDF.</td>
   <td>Conversión<br /> </td>
  </tr>
  <tr>
   <td><a>OptimizePDF</a></td>
   <td>Optimiza al PDF para reducir el tamaño del archivo eliminando metadatos innecesarios sin afectar a la calidad.</td>
   <td>Conversión<br /> </td>
  </tr>
 </tbody>
</table>

### Servicio DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td><a>Firmar/Certificar</a><br /> </td>
   <td>Esta API le permite proteger su documento. Puede utilizar la API para firmar y certificar un documento de PDF.</td>
   <td>Conversión</td>
  </tr>
 </tbody>
</table>


### Servicio Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
  <tr>
   <td><a>Crear PDF</a></td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Conversión</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Conversión</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Servicio de salida {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos representados</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos representados</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos representados</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos representados</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos representados</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>Convierte un conjunto de documentos XDP y PDF a un conjunto de formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Conversión de documentos</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Servicio ConvertPDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>Convierte un documento PDF en una lista de documentos de imagen. Los formatos de imagen compatibles son JPEG, JPEG2K, PNG y TIFF.</td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>Convierte un archivo de PDF plano al formato PostScript mediante las opciones especificadas en la especificación de opciones.</td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>Convierte un archivo de Flat PDF al formato SWF mediante las opciones especificadas en la especificación de opciones.</td>
   <td>Conversión de documentos</td>
  </tr>
 </tbody>
</table>

### Servicio de Forms con códigos de barras {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td><a>decode</a></td>
   <td>Descodifica todos los códigos de barras en un objeto de documento y devuelve un objeto de documento org.w3c.dom. que contiene datos recuperados del código de barras.</td>
   <td>Conversión de documentos</td>
  </tr>
 </tbody>
</table>

### Servicio Assembler {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td><a>invoke</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto AssemblerResult que contiene los documentos resultantes. </td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto AssemblerResult que contiene los documentos resultantes. </td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>Convertir un documento especificado en PDF/A utilizando las opciones especificadas.</td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>invokeDXOneDocument</a></td>
   <td>Convertir un documento especificado en PDF/A utilizando las opciones especificadas.</td>
   <td>Conversión de documentos</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>Convertir un documento especificado en PDF/A utilizando las opciones especificadas.</td>
   <td>Conversión de documentos</td>
  </tr>
 </tbody>
</table>

El uso de la API de invocación se cuenta como una transacción cuando realiza una o más de las siguientes operaciones:
1. Conversión de formatos que no son PDF a formatos PDF. Por ejemplo, la conversión de formato XDP al formato PDF.<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversión de formato PDF a formato PDF/A.
1. Conversión de formato PDF a formatos no PDF. Algunos ejemplos son la transformación de PDF a formato de imagen o la conversión de PDF a formato de texto.

>[!NOTE]
>
>* El API de invocación del servicio de ensamblador puede llamar internamente a un API facturable de otro servicio en función de la entrada. Por lo tanto, `invoke API` puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende de la entrada y las API internas invocadas.
>* Un solo documento de PDF producido mediante un servicio de ensamblador como `invoke` y `invokeDDX` puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende del código <!--DDX--> proporcionado.

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## API de captura de datos facturables {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Formularios {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>Envía el formulario.</td>
   <td>Formularios enviados</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>Envía el formulario.</td>
   <td>Formularios enviados</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>Envía el formulario.</td>
   <td>Forms Renderizado</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## Artículos relacionados

* [Activación y visualización del informe de transacciones para AEM Forms en JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Registre una transacción para las API de componentes personalizadas para AEM Forms en JEE](/help/forms/using/record-transaction-custom-component-jee.md)
