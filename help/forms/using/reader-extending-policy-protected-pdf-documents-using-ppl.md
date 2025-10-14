---
title: Ampliar documentos PDF protegidos por políticas utilizando la Biblioteca de Protección Portátil mediante Reader
description: Extensiones de Reader habilita funciones interactivas en documentos de Adobe PDF a través de Acrobat Reader. Puede utilizar la Biblioteca de Protección Portátil (PPL) para que Reader amplíe los documentos PDF protegidos por DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security,Reader Extensions
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 97%

---

# Ampliar documentos PDF protegidos por políticas utilizando la Biblioteca de Protección Portátil mediante Reader {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Familiarícese con los conceptos de Document Security, Extensiones de Reader y el lenguaje de programación Java para ampliar los documentos de PDF protegidos por directivas de Document Security mediante Reader.

Puede utilizar Document Security para restringir el acceso de documentos PDF específicos únicamente a usuarios autorizados. También puede determinar cómo un destinatario puede utilizar un documento protegido. Por ejemplo, puede especificar si los destinatarios pueden imprimir, copiar o editar el texto de un documento protegido por políticas de Document Security. Para obtener más información sobre Document Security, consulte [Acerca de la seguridad de los documentos](/help/forms/using/admin-help/document-security.md).

Puede utilizar Extensiones de Reader para habilitar funciones interactivas en documentos de Adobe PDF mediante Acrobat Reader. Normalmente, estas funciones interactivas solo están disponibles mediante Adobe Acrobat Professional y Standard. Para obtener más información sobre las funciones interactivas que puede habilitar Extensiones de Reader, consulte [Servicio DocAssurance de Adobe Experience Manager Forms &#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

Puede utilizar la Biblioteca de Protección Portátil para aplicar políticas en el documento sin necesidad de enviarlo por la red. A través de ella solo se transmiten las credenciales de seguridad y los detalles de la política de protección. El documento real nunca sale del cliente, y las políticas de protección se aplican en él de forma local.

## Ampliar documentos PDF protegidos por políticas de Document Security {#reader-extending-document-security-policy-protected-pdf-documents}

Los documentos protegidos por políticas se denominan documentos cifrados. No puede utilizar API estándares de Extensiones de Reader para aplicar, quitar y recuperar derechos de uso de documentos PDF protegidos por políticas. Solo el servicio Extensiones de Reader de la Biblioteca de Protección Portátil proporciona API para aplicar, quitar y recuperar derechos de uso de documentos PDF protegidos por políticas de Document Security.

### Servicio Extensiones de Reader {#reader-extensions-service}

El servicio Extensiones de Reader agrega derechos de uso a un documento PDF protegido por políticas, activando funciones que normalmente no están disponibles cuando se abre un documento PDF con Adobe Acrobat Reader. También incluye API para eliminar y recuperar derechos de uso de un documento protegido por políticas.

El servicio Extensiones de Reader es totalmente compatible con documentos PDF basados en el estándar PDF 1.6 y versiones posteriores. Aparte de Acrobat Reader, los usuarios de terceros no necesitan ningún software o complemento adicional para utilizar los documentos PDF protegidos por políticas.

Puede realizar las siguientes tareas con el servicio Extensiones de Reader:

* Aplicar derechos de uso a un documento PDF protegido por políticas
* Eliminar derechos de uso de un documento PDF protegido por políticas
* Recuperar los derechos de uso aplicados a un documento PDF protegido por políticas

### Aplicar derechos de uso a un documento PDF protegido por políticas de Document Security {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Puede usar la API de Java `applyUsageRights` para aplicar derechos de uso a documentos PDF protegidos por políticas. Los derechos de uso pertenecen a una funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o rellenar los campos del formulario y guardarlo. Los documentos PDF a los que se les han aplicado derechos de uso se denominan “documentos con derechos activados”. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese documento específico.

**Sintaxis:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Especifique InputStream, que representa el documento PDF al que se deben aplicar los derechos de uso. Puede utilizar documentos protegidos mediante LiveCycle Rights Management o AEM Forms Document Security.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Especifique el objeto File que representa un archivo .jks. El archivo .jks es un archivo de almacén de claves. Señala a un certificado que concede derechos de uso.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Especifique la contraseña del almacén de claves. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Especifica un objeto de tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. El objeto usageRights representa derechos individuales que pueden aplicarse a un documento PDF protegido por políticas.</p> </td>
  </tr>
 </tbody>
</table>

### Recuperar los derechos de uso aplicados a un documento PDF protegido por políticas.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Puede usar la API de Java `getDocumentUsageRights` para recuperar los derechos de uso de Extensiones de Reader aplicados a un documento PDF protegido por políticas. Al recuperar información sobre los derechos de uso, puede obtener información sobre las funciones que Extensiones de Reader ha habilitado para el documento PDF protegido por políticas.

**Sintaxis:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Especifique InputStream, que representa el documento PDF desde el que se van a recuperar los derechos de uso. Puede utilizar documentos protegidos mediante LiveCycle Rights Management o AEM Forms Document Security.</p> </td>
  </tr>
 </tbody>
</table>

#### Ejemplo de código {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ");
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Eliminación de los derechos de uso de un documento PDF protegido por políticas {#remove-usage-rights-of-a-policy-protected-pdf-document}

Puede usar la API de Java `removeUsageRights` para eliminar los derechos de uso de un documento protegido por políticas. La eliminación de los derechos de uso de un documento PDF protegido por políticas es necesaria para realizar otras operaciones de AEM Forms en el documento. Por ejemplo, debe firmar digitalmente (o certificar) un documento PDF antes de establecer los derechos de uso. Por lo tanto, si desea realizar operaciones en un documento protegido por políticas, debe eliminar los derechos de uso del documento PDF, realizar el resto de operaciones —como firmar digitalmente el documento— y, a continuación, volver a aplicarle los derechos.

**Sintaxis:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Especifique InputStream, que representa el documento PDF en el que se eliminarán los derechos.<br />. Puede utilizar documentos protegidos mediante LiveCycle Rights Management o AEM Forms Document Security.</td>
  </tr>
 </tbody>
</table>

#### Ejemplo de código {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
