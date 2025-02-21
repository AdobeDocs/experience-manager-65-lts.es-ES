---
title: Proteger un documento en nombre de otro usuario
description: Descubra cómo AEM Forms Document Security Java& trade; SDK ofrece API para una cuenta de usuario a fin de proteger un documento en nombre de otro usuario.
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 53%

---

# Proteger un documento en nombre de otro usuario {#protect-a-document-on-behalf-of-another-user}

AEM Forms Document Security Java™ SDK proporciona API que permiten a una cuenta de usuario proteger un documento en nombre de otro usuario sin obtener permisos para editar el documento. Puede utilizar las API en un proceso de flujo de trabajo o programáticamente como un servicio de documentos. Las nuevas API son:

* **protectDocumentUse** usa la API ProtectDocument para que pueda aplicar una directiva a un documento en nombre de

  otra cuenta de usuario. Los permisos de la cuenta de usuario utilizada para aplicar la política siguen estando limitados a la protección del documento. No obtiene el derecho de abrir y ver el documento. RMSecureDocumentResult protectDocument(Document inDoc, String documentName, String policySetName, String policyName, RMLocale locale, boolean bExactMatchForNames)

* **createLicenseUse** usa la API CreateLicense para poder crear una licencia para una directiva en nombre de otra cuenta de usuario. PublishLicenseDTO createLicense(String policyId, String documentName, boolean logSecureDocEvent)
* **protectDocumentWithCoverPageUse** usa la API ProtectDocumentWithCoverPage para que pueda aplicar una directiva y agregar una portada a un documento en nombre de otro usuario. Los permisos de la cuenta de usuario utilizada para aplicar la política siguen estando limitados a la protección del documento. No obtiene el derecho de abrir y ver el documento. RMSecureDocumentResult protectDocumentWithCoverPage(Document inDoc, String documentName, String policySetName, String policyName, Document coverDoc, boolean bExactMatchForNames)

## Uso de API para proteger un documento en nombre de otro usuario {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

Haga lo siguiente para poder proteger un documento en nombre de otro usuario y sin obtener permisos para editar el documento:

1. Cree un conjunto de políticas. Por ejemplo, el ConjuntodePolíticas1.
1. Cree una política en el conjunto de políticas que acaba de crear. Por ejemplo, la Política1 en ConjuntodePolíticas1.
1. Cree un usuario con la función Rights Management End User; por ejemplo, el Usuario1. Proporcione permisos para ver los documentos protegidos con la Política1 al usuario que acaba de crear.
1. Cree una función. por ejemplo, la Función1. Proporcione el permiso Invocar servicio a la función recién creada. Cree un usuario con la función que acaba de crear; Por ejemplo, Usuario2. Puede utilizar el Usuario2 o un administrador para crear una conexión de SDK e invocar el servicio protectDocument.

   Ahora, puede ejecutar el siguiente código de ejemplo para proteger un documento sin proporcionar permisos para editarlo al usuario que lo protege:

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```
