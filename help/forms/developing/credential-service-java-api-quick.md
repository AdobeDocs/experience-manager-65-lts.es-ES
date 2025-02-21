---
title: Inicio rápido (SOAP) de la API de Java&trade; servicio de credenciales
description: Obtenga información sobre cómo importar y eliminar credenciales en AEM Forms mediante el Inicio rápido de Java&trade; API (SOAP).
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Inicio rápido (SOAP) de la API de Java™ del servicio de credenciales {#credential-service-java-api-quickstart-soap}

El Inicio rápido (SOAP) de la API de Java™ está disponible para el servicio de credenciales.

[Inicio rápido (modo SOAP): Importación de credenciales con Java](credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inicio rápido (modo SOAP): Eliminación de credenciales mediante Java](credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

Las operaciones de AEM Forms se pueden realizar mediante la API de AEM Forms con establecimiento inflexible de tipos y el modo de conexión debe establecerse en SOAP.

>[!NOTE]
>
>Los inicios rápidos en la programación con formularios AEM Forms se basan en el servidor de Forms que se implementa en JBoss® y en el sistema operativo Windows. Sin embargo, si está utilizando otro sistema operativo, como UNIX®, reemplace las rutas específicas de Windows por rutas admitidas por el sistema operativo correspondiente. Del mismo modo, si está utilizando otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>No puede realizar operaciones de servicio de credenciales mediante servicios web.

## Inicio rápido (modo SOAP): Importación de credenciales mediante la API de Java™ {#quick-start-soap-mode-importing-credentials-using-the-java-api}

En el siguiente ejemplo de código se importa una credencial basada en un archivo denominado *cred.p12*. El valor de alias utilizado para importar la credencial es `Secure`. (Consulte [Importación de credenciales mediante la API del Administrador de confianza](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class ImportCredentialSoap {
 
     public static void main(String[] args) {
            try {
 
          //Set connection properties required to invoke AEM Forms using SOAP mode
              Properties connectionProps = new Properties();
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a CredentialServiceClient instance
             CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
             //Reference a credential based on a P12 file
             FileInputStream myCred = new FileInputStream("C:\\Adobe\cred.p12");
             Document credential = new Document(myCred);
 
             //Create a string array to store usage values
             String[] usage = new String[1];
             usage[0] = "truststore.usage.type.sign";
 
             //Import the credential
             certClient.importCredential("secure",credential,"password",usage);
             System.out.println("Credential was uploaded");
 
            }catch (Exception e) {
                e.printStackTrace();
            }
 
            }
 }
 
 
 
```

## Inicio rápido (modo SOAP): Eliminación de credenciales mediante la API de Java™ {#quick-start-soap-mode-deleting-credentials-using-the-java-api}

En el ejemplo de código siguiente se elimina una credencial basada en un valor de alias *secure*. (Consulte [Eliminación de credenciales mediante la API del Administrador de confianza](/help/forms/developing/credentials.md#deleting-credentials-by-using-the-trust-manager-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
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
 
 import java.util.Properties;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class DeleteCertificateSoap {
 
 
     public static void main(String[] args)
     {
     try {
 
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a CredentialServiceClient instance
         CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
         //Delete the certificate
         certClient.deleteCredential("secure");
         System.out.println("Credential was deleted");
 
        }catch (Exception e) {
            e.printStackTrace();
        }
 
        }
 
 }
 
```
