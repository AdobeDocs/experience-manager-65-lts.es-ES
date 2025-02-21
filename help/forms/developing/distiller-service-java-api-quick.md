---
title: Inicio rápido (SOAP) de la API de Distiller Service Java& trade
description: Descubra cómo el servicio Distiller transforma los archivos PostScript, EPS y PRN en PDF, comúnmente empleados para conversiones de documentos de impresión a electrónicos de gran volumen.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Inicio rápido (SOAP) de la API de Java™ del servicio Distiller {#distiller-service-java-api-quickstart-soap}

El Inicio rápido de la API de Java™ (SOAP) está disponible para el servicio Distiller®:

[Inicio rápido (modo SOAP): Conversión de un archivo de PostScript a un documento de PDF mediante Java](distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

Las operaciones de AEM Forms se pueden realizar mediante la API de AEM Forms con establecimiento inflexible de tipos y el modo de conexión debe establecerse en SOAP.

>[!NOTE]
>
>Los inicios rápidos en la programación con formularios AEM Forms se basan en el servidor de Forms que se implementa en el servidor de aplicaciones JBoss® y en el sistema operativo Microsoft® Windows. Sin embargo, si está utilizando otro sistema operativo, como UNIX®, reemplace las rutas específicas de Windows por rutas admitidas por el sistema operativo correspondiente. Del mismo modo, si está utilizando otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Inicio rápido (modo SOAP): Conversión de un archivo de PostScript a un documento de PDF mediante la API de Java™ {#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api}

El siguiente ejemplo de código convierte un archivo PostScript llamado *Loan.ps* en un archivo PDF llamado *Loan.pdf*. (Consulte [Conversión de documentos de PostScript a PDF](/help/forms/developing/converting-postscript-pdf-documents.md#converting-postscript-to-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-distiller-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */

 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.distiller.client.DistillerServiceClient;

 public class JavaAPICreatePDFSoap {

     public static void main(String[] args)
     {
         try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

         // Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

         DistillerServiceClient disClient = new DistillerServiceClient(factory );

         // Get a PS file document to convert to a PDF document and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.ps";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);

         //Set run-time options
         String adobePDFSettings = "Standard";
          String securitySettings = "No Security";

          //Convert a PS  file into a PDF file
         CreatePDFResult result = new CreatePDFResult();
         result = disClient.createPDF(
                 inDoc,
                 inputFileName,
                      adobePDFSettings,
                 securitySettings,
                 null,
                 null
             );

          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();

          //Save the PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.pdf"));
         }
         catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```
