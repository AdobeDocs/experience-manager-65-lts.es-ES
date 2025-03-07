---
title: Inicio rápido (SOAP) de la API de comercio; Java&amp del servicio de Forms con códigos de barras
description: Descubra cómo el servicio de Forms con códigos de barras Java& trade; API Quick Start (SOAP) en AEM Forms permite un procesamiento fluido de los códigos de barras.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: d1350be7-2204-4dc2-814b-4d9e3438a854
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Inicio rápido (SOAP) de la API de Java™ del servicio Forms con códigos de barras {#barcoded-forms-service-java-apiquick-start-soap}

El Inicio rápido (SOAP) de la API de Java™ está disponible para el servicio de Forms con códigos de barras:

[Inicio rápido (modo SOAP): Descodificación de datos de formulario con códigos de barras mediante Java](barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

Las operaciones de AEM Forms se pueden realizar mediante la API de AEM Forms con establecimiento inflexible de tipos y el modo de conexión debe establecerse en SOAP.

>[!NOTE]
>
>Los inicios rápidos en programación con AEM Forms se basan en el servidor de aplicaciones Forms Server que se implementa en el servidor de aplicaciones JBoss® y en el sistema operativo Microsoft® Windows. Sin embargo, si está utilizando otro sistema operativo, como UNIX®, reemplace las rutas específicas de Windows por rutas admitidas por el sistema operativo correspondiente. Del mismo modo, si está utilizando otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Inicio rápido (modo SOAP): Descodificación de datos de formulario con códigos de barras mediante la API de Java™ {#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api}

El siguiente código Java™ descodifica los datos del formulario que están en un formulario de PDF guardado como Loan.pdf. Los datos descodificados se guardan como un archivo XML denominado extractedData.xml. Este ejemplo de código convierte un objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document`. (Consulte [Descodificación de datos de formularios con códigos de barras](/help/forms/developing/barcoded-forms.md#decoding-barcoded-form-data)).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-barcodedforms-client.jar
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
 import java.io.*;
 import java.util.Iterator;
 import java.util.List;
 import java.util.Properties;
 import javax.xml.transform.*;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 import com.adobe.livecycle.barcodedforms.CharSet;
 import com.adobe.livecycle.barcodedforms.Delimiter ;
 import com.adobe.livecycle.barcodedforms.XMLFormat ;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.barcodedforms.client.*;
 
 public class DecodeFormDataSOAP {
 
     public static void main(String[] args) {
 
     try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         BarcodedFormsServiceClient barClient = new BarcodedFormsServiceClient(myFactory);
 
         //Specify a PDF document to convert to an XDP file
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanBarForms.pdf");
         Document inDoc = new Document (fileInputStream);
 
         java.lang.Boolean myFalse = new java.lang.Boolean(false);
         java.lang.Boolean myTrue = new java.lang.Boolean(true);
 
         //Decode barcoded form data
         org.w3c.dom.Document decodeXML = barClient.decode(
             inDoc,
             myTrue,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             CharSet.UTF_8);
 
         //Convert the decoded data to XDP data
         List extractedData = barClient.extractToXML(
             decodeXML,
             Delimiter.Carriage_Return,
             Delimiter.Tab,
             XMLFormat.XDP);
 
         //Create an Iterator object and iterate through
         //the List object
         Iterator iter = extractedData.iterator();
         int i = 0 ;
 
         while (iter.hasNext()) {
 
             //Get the org.w3c.dom.Document object in each element
             org.w3c.dom.Document myDom = (org.w3c.dom.Document)iter.next();
 
             //Convert the org.w3c.dom.Document object to a
             //com.adobe.idp.Document object
             com.adobe.idp.Document myDocument = convertDOM(decodeXML);
 
             //Save the XML data to extractedData.xml
             File myFile = new File("C:\\Adobe\extractedData"+i+".xml");
 
             myDocument.copyToFile(myFile);
             i++;
             }
         }
     catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 
 
     //This user-defined method converts an org.w3c.dom.Document to a
     //com.adobe.idp.Document object
     public static com.adobe.idp.Document convertDOM(org.w3c.dom.Document doc)
         {
 
             byte[] mybytes = null ;
         com.adobe.idp.Document myDocument = null;
         try
             {
 
             //Create a Java Transformer object
          TransformerFactory transFact = TransformerFactory.newInstance();
          Transformer transForm = transFact.newTransformer();
 
          //Create a Java ByteArrayOutputStream object
          ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
 
         //Create a Java Source object
          Source myInput = new DOMSource(doc);
 
         //Create a Java Result object
          Result myOutput = new StreamResult(myOutStream);
 
         //Populate the Java ByteArrayOutputStream object
          transForm.transform(myInput,myOutput);
 
         //Get the size of the ByteArrayOutputStream buffer
          int myByteSize = myOutStream.size();
 
         //Allocate myByteSize to the byte array
         mybytes = new byte[myByteSize];
 
         //Copy the content to the byte array
         mybytes = myOutStream.toByteArray();
         com.adobe.idp.Document myDoc = new com.adobe.idp.Document(mybytes);
 
          myDocument = myDoc ;
          }
 
         catch(Exception ee)
         {
             ee.printStackTrace();
         }
 
     return myDocument;
       }
 }
```

>[!NOTE]
>
>Al utilizar un objeto `org.w3c.dom.Document` y un objeto `com.adobe.idp.Document` en la misma lógica de aplicación, se recomienda calificar completamente ambos objetos.
