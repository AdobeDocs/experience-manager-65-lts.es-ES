---
title: API facturables de informes de transacciones
description: Lista de todas las API que se contabilizan como transacciones
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1754'
ht-degree: 92%

---

# API facturables de informes de transacciones para AEM Forms en OSGi {#transaction-reports-billable-apis}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/transaction-reports-billable-apis) |
| AEM 6.5 | Este artículo |

AEM Forms ofrece varias API para enviar formularios, procesar documentos y representar documentos. Algunas API se contabilizan como transacciones y otras se pueden usar libremente. Este documento proporciona una lista de todas las API que se contabilizan como transacciones en un informe de transacciones. Estos son algunos escenarios comunes en los que se utiliza un API facturable:

* Enviar un formulario adaptable, un formulario HTML5 y un conjunto de formularios
* Representar una versión impresa o web de una comunicación interactiva
* Convertir un documento de un formato a otro
* Acoplar un documento PDF dinámico
* Generar un documento de registro
* Combinar un documento PDF interactivo con otro documento PDF
* Usar los pasos asignar tarea y servicios doc de flujos de trabajo de AEM
* Usar formularios adaptables en un formulario adaptable

Las API de facturación no tienen en cuenta el número de páginas, la longitud de un documento o formulario o el formato final del documento representado. Un informe de transacciones divide las transacciones en dos categorías: documentos representados y formularios enviados.

* **Formularios enviados:** Cuando los datos se envían desde cualquier tipo de formulario creado con AEM Forms y los datos se envían a cualquier repositorio de almacenamiento de datos o base de datos, se considera envío de formulario. Por ejemplo, el envío de un formulario adaptable, un formulario HTML5, PDF Forms y un conjunto de formularios se contabilizan como formularios enviados. Cada formulario de un conjunto de formularios se considera un envío. Por ejemplo, si un conjunto de formularios tiene 5 formularios, cuando se envía el conjunto de formularios, el servicio de informes de transacciones lo contabiliza como 5 envíos.

* **Documentos representados:** La generación de un documento mediante la combinación de una plantilla y datos, la firma o certificación digitalmente de un documento, el uso de una API de servicios de documentos facturables para servicios de documentos o la conversión de un documento de un formato a otro se contabilizan como documentos representados.

>[!NOTE]
>
>La interfaz de usuario Informes de transacciones muestra tres categorías: formularios enviados, documentos representados y documentos procesados. Tanto los documentos representados como los documentos procesados se contabilizan como documentos representados.

## API de servicios de documentos facturables {#billable-document-services-apis}

### Generar un servicio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Convierte un Adobe PDF en tipos de archivo compatibles. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Convierte un Adobe PDF en tipos de archivo compatibles. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Convierte un Adobe PDF en tipos de archivo compatibles. </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crea un PDF a partir de páginas HTML.</p> </td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crea un PDF a partir de direcciones URL que señalan una página HTML.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crea un PDF a partir de direcciones URL que señalan una página HTML.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimiza al PDF para reducir el tamaño del archivo eliminando metadatos innecesarios sin afectar a la calidad.</td>
   <td>Documentos procesados<br /> </td>
   <td> </td>
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
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>Esta API le permite proteger su documento. Puede utilizar la API para firmar, certificar, leer, extender o cifrar un documento PDF.</td>
   <td>Documentos procesados</td>
   <td>Solo se factura la operación firmar y certificar de secureDocument.</td>
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
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea un Adobe PDF a partir de tipos de archivo compatibles.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Documento de servicio de registro (Servicio DoR) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invoca el método de representación especificado para generar un documento de registro utilizando los parámetros proporcionados.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servicio de salida {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Combina datos y plantillas para crear un conjunto de documentos PDF.</td>
   <td>Documentos procesados</td>
   <td> El API generatePDFOutputBatch combina una plantilla de formulario con un registro y genera un PDF. Al procesar un lote de registros, el servicio de informes de transacciones contabiliza cada registro como una representación de PDF independiente. <br> Puede usar el indicador <a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> para combinar varias representaciones en un solo archivo PDF. Independientemente del estado del indicador, el servicio cuenta cada registro como una representación de PDF independiente. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Convierte un conjunto de documentos XDP y PDF a un conjunto de formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> El API generatePDFOutputBatch combina una plantilla de formulario con un registro y genera un PDF. Al procesar un lote de registros, el servicio de informes de transacciones contabiliza cada registro como una representación de PDF independiente. <br> Puede usar el indicador <a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> para combinar varias representaciones en un solo archivo PDF. Independientemente del estado del indicador, el servicio cuenta cada registro como una representación de PDF independiente. </td>
  </tr>
 </tbody>
</table>

### Servicio de Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Representa el formulario PDF a partir de plantillas XDP. Las plantillas XP se crean en Forms Designer.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extrae datos de un formulario PDF o de plantillas XDP</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servicio ConvertPDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Convierte un documento PDF en una lista de documentos de imagen. Los formatos de imagen compatibles son JPEG, JPEG2K, PNG y TIFF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Convierte un archivo de PDF plano al formato PostScript mediante las opciones especificadas en la especificación de opciones.</td>
   <td>Documentos procesados</td>
   <td> </td>
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
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Descodifica todos los códigos de barras en un objeto de documento y devuelve un objeto de documento org.w3c.dom. que contiene datos recuperados del código de barras.</td>
   <td>Documentos procesados</td>
   <td> </td>
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
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invoke</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto <a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> que contiene los documentos resultantes. </td>
   <td>Documentos procesados</td>
   <td>Las siguientes operaciones no se contabilizan como transacciones:
    <ul>
     <li>Crear paquetes o portafolios</li>
     <li>Configurar varios XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invoke</a></td>
   <td>Ejecuta el documento DDX especificado y devuelve un objeto <a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> que contiene los documentos resultantes. </td>
   <td>Documentos procesados</td>
   <td>Todos los formatos de archivo de entrada compatibles con Generador de PDF, Formularios y Servicios de salida; el servicio Ensamblador admite todos esos formatos como formatos de archivo de salida. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convertir un documento especificado en PDF/A utilizando las opciones especificadas.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

El uso de la API de invocación se cuenta como una transacción cuando realiza una o más de las siguientes operaciones:
1. Conversión de formatos que no son PDF a formatos PDF. Por ejemplo, la conversión de formato XDP a formato PDF, que abarca tanto las formas de comunicación interactivas como las no interactivas, y la conversión de Word a PDF.
1. Conversión de formato PDF a formato PDF/A.
1. Conversión de formato PDF a formatos no PDF. Algunos ejemplos son la transformación de PDF a formato de imagen o la conversión de PDF a formato de texto.

>[!NOTE]
>
>* El API de invocación del servicio de ensamblador puede llamar internamente a un API facturable de otro servicio en función de la entrada. Por lo tanto, la API de invocación puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende de la entrada y las API internas invocadas.
>* Un documento PDF único producido mediante el servicio de ensamblador puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende del código DDX proporcionado.

### Servicio de utilidad de PDF  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Convierte un documento PDF en un archivo XDP. Para que un documento de PDF se convierta correctamente en un archivo XDP, el documento de PDF debe contener una secuencia XFA en el diccionario de AcroForm.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API de captura de datos facturables {#billable-data-capture-apis}

Todos los eventos de envío de formularios adaptables, formularios HTML5 y conjuntos de formularios se contabilizan como transacciones. De forma predeterminada, el envío de un formulario PDF no se contabiliza como una transacción. Utilice la [API de registro de transacciones](record-transaction-custom-implementation.md) proporcionada para registrar un envío de PDF Forms como una transacción.

### Formularios adaptables {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso práctico</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un formulario adaptable</td>
   <td>Envía un formulario adaptable a la acción de envío configurada. </td>
   <td>Formularios enviados</td>
   <td>
    <ul>
     <li>Cuenta de envíos correcta para una o dos transacciones. El número de transacciones contabilizadas depende del tipo de acción de envío utilizada para el envío. Por ejemplo, enviar al PDF mediante cuentas de acción de envío por correo electrónico para dos recuentos de transacciones. Una transacción para el envío de formularios y otra para el PDF generado mediante el servicio documento de registro (DOR). </li>
     <li>El uso del formulario adaptable en un formulario adaptable (conjunto de formularios de formulario adaptable) contabiliza solo una transacción. Puede tener cualquier número de formularios adaptables dentro de un formulario adaptable.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Formularios HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso práctico</p> </td>
   <td>Descripción </td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un formulario HTML5</td>
   <td>Envía un formulario HTML5 para enviar la dirección URL configurada en el formulario.</td>
   <td>Formularios enviados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Conjunto de formularios {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un conjunto de formularios</td>
   <td>Envía el conjunto de formularios a la dirección URL de envío configurada en el conjunto de formularios.</td>
   <td>Formularios enviados</td>
   <td>
    <ul>
     <li>El uso del formulario adaptable en un formulario adaptable (conjunto de formularios de formulario adaptable) contabiliza solo una transacción. Puede tener cualquier número de formularios adaptables dentro de un formulario adaptable.</li>
     <li>Todos los formularios de un conjunto de formularios de Formularios HTML5 se contabilizan como una transacción independiente. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de comunicación interactiva facturables y AEM centrados en formularios en las API de OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Asignar pasos de tareas y servicios de documentos de flujos de trabajo AEM centrados en formularios en OSGi y todas las representaciones de comunicación interactiva y se contabilizan como transacciones. La vista previa de una comunicación interactiva en la instancia de autor y la vista previa en la instancia de publicación mediante la interfaz de usuario del agente no se contabilizan como transacciones. Si un paso de flujo de trabajo cuenta una transacción y el flujo de trabajo no se completa, el recuento de transacciones no se invierte.

### Comunicación interactiva - Canal web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Representar un canal web</td>
   <td>Abre la versión web de una comunicación interactiva.</td>
   <td>Documentos representados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Comunicación interactiva - Canal de impresión {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">representar</a> (convertir en PDF)</td>
   <td>Genera la versión PDF de una comunicación interactiva.</td>
   <td>Documentos representados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Flujos de trabajo AEM centrados en formularios en OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un paso Asignar tarea</td>
   <td>Formularios enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Enviar un punto de inicio de aplicación de flujo de trabajo </td>
   <td>Formularios enviados</td>
   <td> </td>
  </tr>
  <tr>
   <td>Enviar una comunicación interactiva (canal de impresión) desde la interfaz de usuario del agente a un flujo de trabajo</td>
   <td>Documentos representados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrar API facturables como transacciones para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Las acciones como enviar un formulario PDF, utilizar la interfaz de usuario del agente para obtener una vista previa de una comunicación interactiva, usar el envío de formulario no estándar y las implementaciones personalizadas no se contabilizan como transacciones. AEM Forms proporciona un API para registrar esas acciones como transacciones. Puede llamar al API desde sus implementaciones personalizadas para [registrar una transacción](/help/forms/using/record-transaction-custom-implementation.md).

## Artículos relacionados {#related-articles}

* [Información general de informes de transacciones para AEM Forms en OSGi](../../forms/using/transaction-reports-overview.md)
* [Ver y comprender los informes de transacciones de AEM Forms en OSGi](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrar una transacción para implementaciones personalizadas para AEM Forms en OSGi](/help/forms/using/record-transaction-custom-implementation.md)
