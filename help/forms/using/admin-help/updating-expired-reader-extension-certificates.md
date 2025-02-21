---
title: Caducidad de los certificados de extensiones de Reader y su impacto
description: Caducidad de los certificados de extensiones de Reader y su impacto
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 887dc1d6d7e11672b62ef5ca5463ea6181ff0320
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---


# Caducidad de los certificados de extensiones de Reader y su impacto {#expiration-of-reader-extensions-certificates-and-its-impact}

Los clientes de Adobe Experience Manager Forms (AEM Forms) con licencias de Adobe Managed Services o On-premise Enterprise Base pueden utilizar el servicio de extensiones de Acrobat Reader DC. El servicio permite a una organización compartir fácilmente documentos interactivos de PDF ampliando la funcionalidad de Acrobat Reader con derechos de uso adicionales. El servicio agrega derechos de uso a un documento de PDF y activa funciones que no están disponibles cuando se abre un documento de PDF con Adobe Acrobat Reader, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Los usuarios de terceros no requieren software ni complementos adicionales para trabajar con documentos con derechos activados. Los documentos de PDF que tienen derechos de uso añadidos se denominan documentos con derechos activados. Un usuario que abre un documento de PDF con derechos activados en Acrobat Reader puede realizar las operaciones que están habilitadas para ese documento.

Adobe utiliza una infraestructura de clave pública (PKI) para emitir certificados digitales para su uso en licencias y habilitación de funciones. Adobe ha estado emitiendo certificados en la entidad emisora de certificados **Adobe Root CA**, que caducará el 7 de enero de 2023. La caducidad del certificado no afecta a los documentos de PDF extendidos mediante certificados de producción emitidos desde los certificados basados en **Adobe Root CA** (certificados antiguos). Todos los documentos de PDF, Reader extendidos con los certificados antiguos antes del 7 de enero de 2023, incluidos los descargados por sus clientes, seguirían funcionando con todos los derechos de uso que se les aplican y no requieren ninguna actualización.

Ya están disponibles una nueva entidad emisora de certificados, **Adobe Root CA G2**, y certificados basados en la nueva entidad emisora de certificados. A partir del 7 de enero de 2023, empiece a usar los nuevos certificados (basados en **Adobe Root CA G2**) para Reader y ampliar sus nuevos documentos de PDF.  Puede [obtener nuevos certificados del Sitio web de licencias de Adobe](https://licensing.adobe.com/) o del Soporte técnico de Adobe.

## Preguntas frecuentes

**Q. ¿Cuál es la diferencia entre un certificado raíz de Adobe y un certificado de extensiones de Acrobat Reader? ¿El certificado raíz de Adobe depende de un certificado de extensiones de Acrobat Reader? ¿Vencen ambos certificados en enero de 2023?**

A. La CA raíz de Adobe es la autoridad de certificación desde la que se emite un certificado de extensiones de Acrobat Reader. El 7 de enero de 2023 caducará &quot;CA raíz de Adobe&quot; y todos los certificados emitidos a partir de ella.

**Q. Había una comunicación previa de Adobe sobre la caducidad de los certificados y el impacto en el uso o la apertura de documentos de PDF. ¿Se debe omitir esa comunicación?**

A. En función de la reevaluación de la situación, todos los documentos de PDF extendidos mediante certificados de producción emitidos desde la antigua &quot;CA raíz de Adobe&quot; antes del 7 de enero de 2023 siguen funcionando sin ningún cambio después del 7 de enero de 2023. Si ya ha actualizado los documentos de PDF, no hay cambios en la experiencia.

**Q. ¿Con quién debo ponerme en contacto si tengo más preguntas?**

R. Puedes ponerte en contacto con el [Soporte técnico de Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=es#support) o enviar un ticket de asistencia.

**Q. ¿Qué sucede si no se actualiza el certificado antes del 7 de enero de 2023?**

R. Todos los documentos de PDF extendidos mediante certificados de producción emitidos desde la antigua &quot;CA raíz de Adobe&quot; antes del 7 de enero de 2023 siguen funcionando sin ningún cambio después del 7 de enero de 2023. Los PDF extendidos con certificados de evaluación no funcionan después de la fecha de caducidad.

**Q. ¿Es diferente la descripción de los nuevos certificados de los antiguos?**

R. La descripción de los nuevos certificados de Acrobat Reader Extensions menciona **G3-P24** como nombre del programa. En la descripción de los certificados antiguos (certificados basados en &quot;Adobe Root CA&quot;), **P24** se menciona como el nombre del programa.

**Q. ¿Cómo obtengo los certificados más recientes?**

R. Todos los clientes de Forms autorizados (con licencia activa) pueden descargar los nuevos certificados (certificados basados en &quot;Adobe Root CA G2&quot;) desde el [Sitio web de licencias de Adobe](https://licensing.adobe.com/). Si no puede encontrar el certificado en el sitio web de licencias de Adobe, póngase en contacto con el [Soporte técnico de Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) o genere un ticket de asistencia.

**Q. ¿Siguen funcionando después del 7 de enero de 2023 mis documentos de PDF extendidos mediante certificados emitidos desde la &quot;CA raíz de Adobe&quot; (la antigua autoridad de certificación)?**

R. Sí, todos los documentos de PDF extendidos mediante certificados de producción emitidos desde la &quot;CA raíz de Adobe&quot; (la antigua autoridad de certificación) antes del 7 de enero de 2023 siguen funcionando sin ningún cambio después del 7 de enero de 2023. Los documentos de PDF extendidos con certificados de evaluación dejan de funcionar después de la fecha de caducidad.

**Q. ¿Qué versión de Adobe Acrobat Reader es necesaria para seguir utilizando documentos de PDF extendidos con certificados emitidos desde la &quot;CA raíz de Adobe&quot; (la autoridad de certificación anterior)?**

A. Se requiere Adobe Acrobat Reader 2020 o posterior para utilizar documentos de PDF ampliados con &quot;Adobe Root CA&quot; (la autoridad de certificación antigua). Es la versión compatible de Acrobat Reader en el momento de publicar este documento. Si usa una [versión no compatible de Adobe Acrobat](https://helpx.adobe.com/es/support/programs/eol-matrix.html), Adobe recomienda [descargar e instalar la versión más reciente de Adobe Acrobat Reader](https://get.adobe.com/es/reader/).

**Q. ¿Qué versión de Adobe Acrobat Reader es necesaria para seguir utilizando documentos de PDF extendidos con certificados emitidos desde &quot;Adobe Root CA 2&quot; (la nueva entidad emisora de certificados)?**

A. Se requiere Adobe Acrobat Reader 2020 o posterior para utilizar documentos de PDF ampliados con &quot;Adobe Root CA 2&quot; (la nueva autoridad de certificación). Si usa una [versión no compatible de Adobe Acrobat Reader](https://helpx.adobe.com/es/support/programs/eol-matrix.html), Adobe recomienda [descargar e instalar la versión más reciente de Adobe Acrobat Reader](https://get.adobe.com/es/reader/).

**Q. ¿Puedo eliminar un certificado antiguo de Extensiones de Acrobat Reader y agregar uno nuevo en un servidor de Adobe Experience Manager Forms mientras sigo usando el alias existente?**

R. Sí, puede eliminar un certificado antiguo de Extensiones de Acrobat Reader y agregar uno nuevo con el alias existente a un servidor de Adobe Experience Manager Forms.

**Q. ¿Puedo mantener certificados de extensiones de Acrobat Reader nuevos y antiguos en un servidor de Adobe Experience Manager Forms?**

R. Sí, puede mantener ambos certificados, pero con diferentes alias en un servidor de Adobe Experience Manager Forms. Después del 7 de enero de 2023, solo puede utilizar el nuevo certificado para ampliar un documento de PDF con Reader.

**Q. ¿Puedo importar el mismo certificado de extensiones de Acrobat Reader a todos los entornos de Adobe Experience Manager Forms?**

A. Sí, se puede utilizar el mismo certificado de extensiones de Acrobat Reader en varios entornos.

**Q. ¿Cómo puedo comprobar los derechos de uso aplicados a un documento de PDF?**

R. Puede usar la API [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65-2025/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) para recuperar la información sobre los derechos de uso aplicados a un documento de PDF.

**Q. ¿Cómo cambio la contraseña de un archivo de certificado de extensiones de Acrobat Reader?**

A. En Microsoft Windows, para cambiar la contraseña del certificado, instale el certificado mediante Microsoft Management Console (MMC) y seleccione **Marcar la clave como exportable**. Una vez instalado, exporte el certificado con una clave privada y utilice otra contraseña para el archivo PFX.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65-2025/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
