---
title: Usar AEM Document Services mediante programación
description: Aprenda a utilizar las API de servicios de documentos para firmar, cifrar, etiquetar y generar digitalmente documentos de PDF.
feature: Document Services,APIs & Integrations
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '6439'
ht-degree: 93%

---

# Usar AEM Document Services mediante programación  {#using-aem-document-services-programmatically}

Los ejemplos de este documento le ayudarán a comprender y utilizar Servicios de documentos de AEM en AEM Forms en un entorno OSGi. Para obtener ejemplos de AEM Forms en un entorno JEE, consulte

* [Inicio rápido de la API de Java del servicio Signature](/help/forms/developing/signature-service-java-api-quick.md#programming-aem-forms-jee)

* [Inicio rápido de la API de Java del servicio de cifrado](/help/forms/developing/encryption-service-java-api-quick.md#developer-reference)

* [Inicio rápido de la API de Java del servicio Extensiones de Acrobat Reader](/help/forms/developing/acrobat-reader-dc-extensions-service.md#developer-reference)

## Requisitos previos {#prerequisite}

* Antes de usar las API del servicio DocAssurance, [configure el servicio DocAssurance](/help/forms/using/install-configure-document-services.md).

* Descargue y configure el [AEM Forms Client SDK](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) con su proyecto Maven de AEM. Las clases de cliente necesarias para crear proyectos Maven mediante AEM Document Services están disponibles allí.

* Más información sobre [cómo crear su proyecto de AEM con Maven](/help/sites-developing/ht-projects-maven.md)

## Servicio DocAssurance {#docassurance-service}

El servicio DocAssurance incluye los siguientes servicios:

* Servicio de firmas
* Servicio de cifrado
* Servicio de ampliación de Reader

Puede realizar las siguientes operaciones con el servicio DocAssurance:

* [Agregar una firma invisible](/help/forms/using/aem-document-services-programmatically.md#p-adding-an-invisible-signature-field-p)

* [Agregar un campo de firma](/help/forms/using/aem-document-services-programmatically.md#p-adding-a-signature-field-nbsp-p)
* [Aplicar marca de fecha y hora al documento](/help/forms/using/aem-document-services-programmatically.md#apply-document-timestamp)

* [Obtener firma](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-p)
* [Obtener lista de campos de firma](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-field-list-nbsp-p)
* [Modificar campos de firma](/help/forms/using/aem-document-services-programmatically.md#p-modifying-signature-fields-nbsp-p)

* [Proteger documento](/help/forms/using/aem-document-services-programmatically.md#p-securing-documents-p)

* [Obtener derechos de uso de las credenciales](/help/forms/using/aem-document-services-programmatically.md#p-getting-credential-usage-rights-p)

* [Obtener derechos de uso del documento](/help/forms/using/aem-document-services-programmatically.md#p-getting-document-usage-rights-p)

* [Quitar derechos de uso](/help/forms/using/aem-document-services-programmatically.md#p-removing-usage-rights-p)
* [Verificar firmas digitales](/help/forms/using/aem-document-services-programmatically.md#p-verifying-digital-signatures-p)
* [Verificar varias firmas digitales](/help/forms/using/aem-document-services-programmatically.md#p-verifying-multiple-digital-signatures-p)
* [Quitar firmas digitales](/help/forms/using/aem-document-services-programmatically.md#p-removing-digital-signatures-p)

* [Obtener certificación del campo de firma](/help/forms/using/aem-document-services-programmatically.md#p-getting-certifying-signature-field-p)
* [Obtener tipo de cifrado de PDF](/help/forms/using/aem-document-services-programmatically.md#p-getting-pdf-encryption-type-p)
* [Quitar cifrado de contraseña](/help/forms/using/aem-document-services-programmatically.md#p-removing-password-encryption-from-pdf-p)

* [Quitar cifrado de certificado](/help/forms/using/aem-document-services-programmatically.md#p-removing-certificate-encryption-p)

>[!NOTE]
>
>Todos estos servicios utilizan el objeto Document como parámetro de entrada para el que se puede encontrar el Javadoc en la dirección URL [https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/index.html](https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/index.html)

### Agregar un campo de firma invisible {#adding-an-invisible-signature-field}

Las firmas digitales aparecen en los campos de firma, que son campos de formulario que contienen una representación gráfica de la firma. Los campos de firma pueden ser visibles o invisibles. Los firmantes pueden utilizar un campo de firma preexistente o se puede agregar un campo de firma mediante programación. En cualquier caso, el campo de firma debe existir antes de que se pueda firmar un documento PDF. Puede agregar mediante programación un campo de firma mediante la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar más de un campo de firma a un documento PDF. Sin embargo, cada nombre de campo de firma debe ser único.

**Sintaxis**: `addInvisibleSignatureField(Document inDoc, String signatureFieldName, FieldMDPOptionSpec fieldMDPOptionsSpec, PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Objeto de documento que contiene el PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code><br /> </td>
   <td>Nombre del campo de firma. Este parámetro es obligatorio y no puede tener nulo como valor.<br /> </td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>Un objeto <code>FieldMDPOptionSpec</code> que especifica los campos de documento PDF que están bloqueados después de firmar en el campo de firma. Este parámetro es opcional y puede aceptar un valor nulo.</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>Un objeto <code>SeedValueOptions</code> que especifica los distintos valores semilla del campo. T Este parámetro es opcional y puede aceptar un valor nulo.<span class="acrolinxCursorMarker"></span></td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Este parámetro solo es necesario para los archivos cifrados.</td>
  </tr>
 </tbody>
</table>

Este es un ejemplo de código Java que agrega un campo de firma invisible a un documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds an invisible signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddInvisibleSignatureField.class)
public class AddInvisibleSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addInvisibleSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addInvisibleSignatureField(
       inDoc,
       fieldName,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

También puede utilizar la especificación [CAdES](https://es.wikipedia.org/wiki/CAdES_(inform%C3%A1tica)) para firmar documentos. Utilice el siguiente código de ejemplo para configurar el formato de firma para [CAdES.](https://es.wikipedia.org/wiki/CAdES_(inform%C3%A1tica))

```java
SigningFormat signingFormat = SigningFormat.CAdES;
sigAppearence.setSigningFormat(signingFormat);
signOptions.setSigAppearence(sigAppearence);
```

### Agregar un campo de firma  {#adding-a-signature-field-nbsp}

Puede agregar mediante programación un campo de firma mediante la API de Java del servicio de firma o la API del servicio web de firma. Puede agregar varios campos de firma a un documento PDF. Sin embargo, cada nombre de campo de firma debe ser único.

**Sintaxis**:

```java
public Document addSignatureField(Document inDoc,
 String signatureFieldName,
 Integer pageNo,
 PositionRectangle positionRectangle,
 FieldMDPOptionSpec fieldMDPOptionsSpec,
 PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)
```

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Objeto de documento que contiene el PDF</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nombre del campo de firma. Este parámetro es obligatorio y no puede aceptar un valor nulo.</td>
  </tr>
  <tr>
   <td><code>pageNumber</code></td>
   <td>Número de página en el que se agrega el campo de firma. Los valores válidos son del 1 al número de páginas que contenga el documento. Este parámetro es obligatorio y no puede aceptar un valor nulo.<br /> </td>
  </tr>
  <tr>
   <td><code>positionRectangle</code></td>
   <td>Un <code>PositionRectangle object</code> que especifica la posición del campo de firma. Este parámetro es obligatorio y no puede aceptar un valor nulo. Si el rectángulo especificado no se encuentra al menos parcialmente en el cuadro de recorte de la página especificada, se lanzará un <code>InvalidArgumentException</code>. Además, ni la altura ni la anchura del rectángulo especificado pueden ser 0 ni negativas. Las coordenadas por debajo de X izquierda o Y izquierda pueden ser 0 o mayor pero no negativas y están relacionadas con el cuadro de recorte de la página.</td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>Un objeto <code>FieldMDPOptionSpec</code> que especifica los campos de documento PDF que están bloqueados después de firmar en el campo de firma. Es un parámetro opcional y puede ser nulo.</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>Un objeto <code>SeedValueOptions</code> que especifica los distintos valores semilla del campo. Es un parámetro opcional y puede ser nulo.</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Este parámetro solo es necesario para los archivos cifrados.</td>
  </tr>
 </tbody>
</table>

Este es un ejemplo de código Java que agrega un campo de firma a un documento PDF.

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds a signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddSignatureField.class)
public class AddSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addSignatureField(
       inDoc,
       fieldName,
       pageNum,
       post,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Aplicar marca de fecha y hora al documento {#apply-document-timestamp}

La marca de tiempo de un documento se puede programar según las especificaciones de [PAdES 4](https://es.wikipedia.org/wiki/PAdES). También puede utilizar las especificaciones de [CAdES](https://es.wikipedia.org/wiki/CAdES_(inform%C3%A1tica)) para documentos relacionados con transacciones.

**Sintaxis**: `applyDocumentTimeStamp(Document doc, VerificationTime verificationTime, ValidationPreferences dssPrefs, ResourceResolver resourceResolver, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>VerificationTime</code></td>
   <td>El momento en que debe validarse la firma<br /> </td>
  </tr>
  <tr>
   <td><code>ValidationPreferences</code> </td>
   <td>Preferencias para controlar las configuraciones de validación.</td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>Resolución de recursos en el repositorio de Granite Trust.</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.</td>
  </tr>
 </tbody>
</table>

Los siguientes ejemplos de código agregan una marca de tiempo a un documento según [PAdES 4](https://es.wikipedia.org/wiki/PAdES).

```java
package com.adobe.signatures.test;

import java.io.File;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

 @Component
 @Service(value=Test.class)
 public class Test {

     @Reference
     private DocAssuranceService docAssuranceService;

     @Reference
     private SlingRepository slingRepository;

     @Reference
     private JcrResourceResolverFactory jcrResourceResolverFactory ;

     /**
      *
      * @param inputFile - path to the pdf document stored at disk
      * @param outputFile - path to the pdf document where the output needs to be stored
      * @throws Exception
      */
     public void TimeStamp(String inputFile, String outputFile) throws Exception{

         File inFile = new File(inputFile);
         Document inDoc = new Document(inFile);

         File outFile = new File(outputFile);
         Document outDoc = null;

         Session adminSession = null;
         ResourceResolver resourceResolver = null;
         try {

              /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
              the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
              the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
              here we are using the same resource resolver
              */
              adminSession = slingRepository.loginAdministrative(null);
              resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

              VerificationTime verificationTime = getVerificationTimeForPades();
              ValidationPreferences dssPrefs = getValidationPreferences();

              //retrieve specifications for each of the services, you may pass null if you do not want to use that service
              //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
               outDoc = docAssuranceService.applyDocumentTimeStamp(inDoc, verificationTime, dssPrefs, resourceResolver, null);
         }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

         outDoc.copyToFile(outFile);

     }

  public  VerificationTime getVerificationTimeForPades(){

         return VerificationTime.SECURE_TIME_ELSE_CURRENT_TIME;

     }

 /**
       * sets ValidationPreferences
       */
      private static ValidationPreferences getValidationPreferences(){

         ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
         prefs.setPKIPreferences(getPKIPreferences());

         //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected

         return prefs;

     }

   /**
       * sets PKIPreferences
       */
     private static PKIPreferences getPKIPreferences(){
         PKIPreferences pkiPref = new PKIPreferencesImpl();
         pkiPref.setCRLPreferences(getCRLPreferences());
         pkiPref.setPathPreferences(getPathValidationPreferences());
         pkiPref.setOCSPPreferences(getOCSPPref());
         pkiPref.setTSPPreferences(getTspPref());
         return pkiPref;
     }

   /**
      * sets CRL Preferences
      */
     private static CRLPreferences getCRLPreferences(){

         CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
         crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
         crlPrefs.setGoOnline(true);
         return crlPrefs;
     }

     /**
      *
      * sets PathValidationPreferences
      */
     private static PathValidationPreferences getPathValidationPreferences(){
         PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
         pathPref.setDoValidation(true);
         return pathPref;

     }

   public static TSPPreferences getTspPref(){
   TSPPreferencesImpl tspPrefs=new TSPPreferencesImpl();
   char pass[]=new char[9];

   tspPrefs.setTspServerURL("TSPPrefs_ServerURL");
   tspPrefs.setUsername("TSPPrefs_Username");
   tspPrefs.setPassword(pass);
   tspPrefs.setSize(10240);
   return tspPrefs;
   }

     private static OCSPPreferencesImpl getOCSPPref(){
         OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
         ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
         return ocsp;
     }

}
```

### Conseguir firma {#getting-signature}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma en un documento de PDF o para comprobar los nombres, recupere los nombres mediante programación. El servicio Firma devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintaxis**: `getSignature(Document doc, String signatureFieldName, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nombre del campo de firma que contiene una firma. Especifique el nombre completo del campo de firma. Cuando se utiliza un documento PDF basado en un formulario XFA, se puede utilizar el nombre parcial del campo de firma. Por ejemplo, <code>form1[0].#subform[1].SignatureField3[3]</code> se puede especificar como <code>SignatureField3[3]</code>.</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java recupera la información de firma del campo de firma dado en un documento de PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.client.types.PDFSignature;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetSignature.class)
public class GetSignature {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void GetSignature(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignature pdfSignature = docAssuranceService.getSignature(inDoc,"fieldName",null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Conseguir una lista de campos de firma  {#getting-signature-field-list-nbsp}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma en un documento de PDF, puede recuperarlos y verificarlos mediante programación. El servicio Firma devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintaxis**: `public List <PDFSignatureField> getSignatureFieldList (Document inDoc, UnlockOptions unlockOptions)`

**Parámetros de entrada**

| Parámetros | Descripción |
|---|---|
| `inDoc` | Objeto de documento que contiene el PDF |
| `unlockOptions` | Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado. |

El siguiente ejemplo de código Java recupera los nombres de los campos de firma de un documento de PDF.

```java
/*************************************************************************
 *
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------
**************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the names of signature fields in a PDF document.
 */

@Component
@Service(value=GetSignatureFields.class)
public class GetSignatureFields {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getSignatureFields(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve the name of the document's signature fields
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        List fieldNames = docAssuranceService.getSignatureFieldList(inDoc,null);

        //Obtain the name of each signature field by iterating through the
        //List object
        Iterator iter = fieldNames.iterator();
        int i = 0 ;
        String fieldName="";
        while (iter.hasNext()) {
            PDFSignatureField signatureField = (PDFSignatureField)iter.next();
            fieldName = signatureField.getName();
            System.out.println("The name of the signature field is " +fieldName);
            i++;
        }
   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Modificar campos de firma  {#modifying-signature-fields-nbsp}

Puede modificar los campos de firma que se encuentran en un documento de PDF. La modificación de un campo de firma implica la manipulación de sus valores del diccionario de bloqueo de campos de firma o valores del diccionario de valores de semillas.

Un diccionario de bloqueo de campos especifica una lista de campos que se bloquearán cuando se firme en el campo de firma. Un campo bloqueado impedirá que los usuarios lo editen. Un diccionario de valores semillas contiene información de la restricción que se utilizará en el momento en que se aplique la firma. Por ejemplo, puede cambiar los permisos que controlan las acciones que se pueden producir sin invalidar una firma.

Si modifica un campo de firma existente, podrá editar el documento PDF para reflejar los cambios en los requisitos empresariales. Por ejemplo, un requisito empresarial nuevo requiere bloquear todos los campos del documento después de firmarlo.

**Sintaxis**: `public Document modifySignatureField(Document inDoc, String signatureFieldName, PDFSignatureFieldProperties pdfSignatureFieldProperties, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Objeto de documento que contiene el PDF</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nombre del campo de firma. Este parámetro es obligatorio y no puede aceptar un valor nulo.<br /> </td>
  </tr>
  <tr>
   <td><code>pdfSignatureFieldProperties</code></td>
   <td>Objeto que especifica información sobre los valores <code>PDFSeedValueOptionSpec</code> y <code>FieldMDPOptionSpec</code> del campo de firma.</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java modifica un campo de firma al bloquear todos los campos del formulario cuando se firme en el campo de firma.

```java
/*************************************************************************
 *

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.FieldMDPAction;
import com.adobe.fd.signatures.client.types.FieldMDPOptionSpec;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.PDFSeedValueOptionSpec;
import com.adobe.fd.signatures.client.types.PDFSignatureFieldProperties;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.MissingSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignatureFieldSignedException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can modify signature fields that are in a PDF document by using the Java API and web service API. Modifying a signature field involves
 * manipulating its signature field lock dictionary values or seed value dictionary values.
 * A field lock dictionary specifies a list of fields that are locked when the signature field is signed. A locked field prevents users from making
 * changes to the field. A seed value dictionary contains constraining information that is used at the time the signature is applied.
 * For example, you can change permissions that control the actions that can occur without invalidating a signature.
 * By modifying an existing signature field, you can change the PDF document to reflect changing business requirements. For example,
 * a new business requirement may require locking all document fields after the document is signed.
 * This section explains how to modify a signature field by amending both field lock dictionary and seed value dictionary values.
 * Changes made to the signature field lock dictionary result in all fields in the PDF document being locked when a signature field is signed.
 * Changes made to the seed value dictionary prohibit specific types of changes to the document.
 *
 * The following Java code example modifies a signature field named SignatureField1 by locking all fields in the form when a signature is applied to the signature field and ensuring that no changes are allowed.
 * After the Signature service returns the PDF document that contains the modified signature field
 */

@Component
@Service(value=ModifySignatureField.class)
public class ModifySignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  *
  *
  */
 public void modifySignatureField(String inputFile, String outFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a PDFSignatureFieldProperties
        PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();

         //Create a PDFSeedValueOptionSpec object that stores
         //seed value dictionary information.
         PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();

         //Disallow changes to the PDF document. Any change to the document invalidates
         //the signature
         seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);

         //Create a FieldMDPOptionSpec object that stores
         //signature field lock dictionary information.
         FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();

         //Lock all fields in the PDF document
         fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);

         //Set dictionary information
         fieldProperties.setSeedValue(seedOptionsSpec);
         fieldProperties.setFieldMDP(fieldMDPOptionsSpec);

         //Modify the signature field
         //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
         Document modSignatureField =  docAssuranceService.modifySignatureField(inDoc,fieldName,fieldProperties,null);

        //save the modSignatureField
         modSignatureField.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Certificar documentos PDF  {#certifying-pdf-documents-nbsp}

Puede proteger un documento PDF certificándolo con un tipo de firma concreto denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes maneras:

* Debe ser la primera firma aplicada al documento PDF. Es decir, cuando se aplica la firma certificada, los demás campos de firma del documento deben estar sin firmar. Solo se permite una firma certificada en un documento PDF. Para firmar y certificar un documento PDF, debe certificarlo antes de firmarlo. Después de certificar un documento PDF, puede firmar digitalmente en los campos de firma adicionales.
* El autor o el creador del documento pueden especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada. Por ejemplo, el documento puede permitir rellenar formularios o realizar comentarios. Si el autor especifica que no se permite una modificación determinada, Acrobat impedirá que los usuarios modifiquen el documento de esa manera. Si se realizan estas modificaciones, la firma certificada no será válida. Además, Acrobat emitirá una advertencia cuando cualquier usuario abra el documento. (Con las firmas no certificadas no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).
* En el momento de la firma, el documento se analizará para detectar tipos de contenido específicos que puedan hacer que el contenido de un documento sea ambiguo o engañoso. Por ejemplo, una anotación podría complicar algún texto de una página que sea importante para comprender qué se certifica. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

**Sintaxis**:

```java
secureDocument(Document inDoc, EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions, ReaderExtensionOptions readerExtensionOptions, UnlockOptions unlockOptions)
```

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento PDF de entrada de documento<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>Incluye los argumentos necesarios para codificar un documento PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>Incluye las opciones necesarias para firmar/certificar un documento PDF</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>Incluye las opciones necesarias para que Reader amplíe un documento PDF</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código certifica un documento PDF basado en un archivo PDF.

```java
/*************************************************************************

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * You can secure a PDF document by certifying it with a particular type of signature called a certified signature.
 * A certified signature is distinguished from a digital signature in these ways:
 *
 * It must be the first signature applied to the PDF document; that is, at the time the certified signature is applied, any other signature fields in the document must be unsigned.
 * Only one certified signature is permitted in a PDF document. If you want to sign and certify a PDF document, you must certify it before signing it.
 * After you certify a PDF document, you can digitally sign additional signature fields.
 *
 * The author or originator of the document can specify that the document can be modified in certain ways without invalidating the certified signature. For example,
 * the document may permit filling in forms or commenting. If the author specifies that a certain modification is not permitted, Acrobat restricts users from modifying the document
 * in that way. If such modifications are made, such as by using another application, the certified signature is invalid and Acrobat issues a warning when a user opens the document.
 * (With non-certified signatures, modifications are not prevented, and normal editing operations do not invalidate the original signature.)
 *
 * At the time of signing, the document is scanned for specific types of content that could make the contents of a document ambiguous or misleading. For example, an annotation could
 * obscure some text on a page that is important for understanding what is being certified. An explanation (legal attestation) can be provided about such content.
 * You can programmatically certify PDF documents by using the Signature service Java API or the Signature web service API. When certifying a PDF document, you must reference a security
 * credential that exists in the Credential service.
 *
 * Note: When certifying and signing the same PDF document, if the certify signature is not trusted, a yellow triangle appears next to the first sign signature when you open the PDF document in Acrobat or Adobe Reader.
 * The certifying signature must be trusted to avoid this situation.
 *
 * The following Java code example certifies a PDF document that is based on a PDF file.
 *
 * PreRequisites - Digital certificate for certifying the document has to be uploaded on AEM Key Store.
 *
 */

@Component
@Service(value=Certify.class)
public class Certify {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void certify(String inputFile, String outputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //we are not extending the reader in this case, so passing null
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    try {
    outDoc = docAssuranceService.secureDocument(inDoc, null, getCertificationOptions(resourceResolver), null,null);
   } catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }

        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA256;

        //Reason for signing/certifying
        String reason = "Reason";

        //location of the signer
        String location = "Location";

        //contact info of the signer
        String contactInfo = "Contact Info";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, false, true, true, TextDirection.AUTO);
        signatureOptions.setLockCertifyingField(true);
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Proteger documentos {#securing-documents}

secureDocument le permite cifrar, firmar/certificar y leer un documento PDF, ya sea de forma individual o en cualquier combinación en un orden determinado. Para acceder a cualquiera de estas funcionalidades, apruebe el argumento correspondiente. Si es nulo, se supondría que el procesamiento en particular no es necesario.

**Cifrar documentos PDF con contraseña**

Cuando se cifra un documento PDF con una contraseña, cualquier usuario deberá especificar la contraseña para abrir el documento PDF en Adobe Reader o Acrobat. Además, antes de que otra operación de los servicios de documentos de AEM Forms utilice el documento, se deberá desbloquear un documento PDF cifrado con contraseña.

**Cifrar documentos PDF con certificados**

El cifrado basado en certificados permite cifrar un documento para destinatarios específicos mediante tecnología de clave pública.

Se pueden otorgar permisos a varios destinatarios diferentes para el documento. Muchos aspectos del cifrado son posibles gracias a la tecnología de claves públicas.

Se utiliza un algoritmo para generar dos números grandes, conocidos como claves, que tienen las siguientes propiedades:

* Se utiliza una clave para cifrar un conjunto de datos. Posteriormente, solo se puede utilizar la otra clave para descifrar los datos.
* Es imposible distinguir una clave de la otra.
* Una de las claves actúa como clave privada de un usuario. Es importante que solo el usuario tenga acceso a esta clave.
* La otra clave es la clave pública del usuario, que se puede compartir con otros.

Un certificado de clave pública contiene la clave pública y la información de identificación del usuario. Se utiliza el formato X.509 para almacenar certificados. Los certificados los suele emitir y firmar digitalmente una autoridad de certificación (CA), que es una entidad reconocida que proporciona confianza en la validez del certificado. Los certificados tienen una fecha de caducidad tras la cual ya no son válidos.

Además, las listas de revocación de certificados (CRL) proporcionan información sobre los certificados revocados antes de su fecha de caducidad. Las listas CRL las publican periódicamente las autoridades certificadoras. El estado de revocación de un certificado también se puede recuperar mediante el Protocolo de estado de certificado en línea (OCSP) a través de la red.

>[!NOTE]
>
>Para poder cifrar un documento PDF con un certificado, debe asegurarse de agregar el certificado al repositorio de confianza de AEM.

**Aplicar derechos de uso a documentos PDF**

Puede aplicar derechos de uso a documentos PDF mediante la API de cliente Java y el servicio web de ampliación de Reader. Los derechos de uso pertenecen a una funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o rellenar los campos del formulario y guardarlo. Los documentos PDF a los que se les han aplicado derechos de uso se denominan “documentos con derechos activados”. Un usuario que abre un documento con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese documento específico.

Antes de poder ampliar un documento PDF con un certificado, Reader debe asegurarse de agregar el certificado al repositorio de claves de AEM.

**Firma digital de documentos PDF**

Las firmas digitales se pueden aplicar a documentos PDF para proporcionar cierto nivel de seguridad. Las firmas digitales, como las firmas manuscritas, proporcionan un medio para que los firmantes se identifiquen y hagan declaraciones sobre un documento.

La tecnología utilizada para firmar documentos digitalmente ayuda a garantizar que tanto el firmante como los destinatarios tengan una idea clara de lo que se firmó y estén seguros de que el documento no se ha alterado desde que se firmó.

Los documentos PDF se firman mediante tecnología de clave pública. Un firmante tiene dos claves: una clave pública y una clave privada. La clave privada se almacenará en las credenciales del usuario, que deberán estar disponibles a la hora de realizar la firma.

La clave pública se almacenará en el certificado del usuario, que deberá estar disponible para que los destinatarios validen la firma. La información sobre los certificados revocados se encuentra en las listas de revocación de certificados (CRL) y en las respuestas del Protocolo de estado de certificado en línea (OCSP) distribuidas por las autoridades de certificación (CA). La hora de la firma se puede obtener de una fuente de confianza conocida como Autoridad de marca de tiempo.

>[!NOTE]
>
>Para poder firmar digitalmente un documento PDF, debe asegurarse de agregar la credencial al repositorio de claves de AEM. La credencial es la clave privada que se utiliza para la firma.

>[!NOTE]
>
>AEM Forms también es compatible con la especificación *[CAdES](https://es.wikipedia.org/wiki/CAdES_(inform%C3%A1tica))* para firmar digitalmente documentos PDF.

**Certificar documentos PDF**

Puede proteger un documento PDF certificándolo con un tipo de firma concreto denominada firma certificada. Una firma certificada se distingue de una firma digital de las siguientes maneras:

Debe ser la primera firma aplicada al documento PDF; es decir, en el momento en que se aplique la firma certificada, cualquier otro campo de firma del documento debe estar sin firmar.

Solo se permite una firma certificada en un documento PDF. Si desea firmar y certificar un documento PDF, deberá certificarlo antes de firmarlo.

Después de certificar un documento PDF, puede firmar digitalmente en los campos de firma adicionales.

El autor o el creador del documento pueden especificar que el documento se puede modificar de determinadas formas sin invalidar la firma certificada.

Por ejemplo, el documento puede permitir rellenar formularios o hacer comentarios. Si el autor especifica que no se permite una modificación determinada,

Acrobat impedirá que los usuarios modifiquen el documento de esta manera. Si se realizan dichas modificaciones, como por ejemplo utilizar otra aplicación, la firma certificada no será válida y Acrobat emitirá una advertencia cuando cualquier usuario abra el documento. (Con las firmas no certificadas no se evitan las modificaciones y las operaciones de edición normales no invalidan la firma original).

En el momento de la firma, el documento se analizará para detectar tipos de contenido específicos que puedan hacer que el contenido de un documento sea ambiguo o engañoso.

Por ejemplo, una anotación podría complicar algún texto de una página que sea importante para comprender qué se certifica. Se puede proporcionar una explicación (autenticación legal) sobre dicho contenido.

>[!NOTE]
>
>Para poder firmar digitalmente un documento PDF, debe asegurarse de agregar la credencial al repositorio de claves de AEM. La credencial es la clave privada que se utiliza para la firma.

**Sintaxis**:

```java
secureDocument(Document inDoc,
 EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions,
 ReaderExtensionOptions readerExtensionOptions,
 UnlockOptions unlockOptions)
```

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento PDF de entrada de documento<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>Incluye los argumentos necesarios para codificar un documento PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>Incluye las opciones necesarias para firmar o certificar un documento PDF</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>Incluye las opciones necesarias para que Reader amplíe un documento PDF</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.<br /> </td>
  </tr>
 </tbody>
</table>

**Ejemplo 1**: este ejemplo se utiliza para realizar el cifrado de contraseña, para certificar un campo de firma y ampliar con Reader el documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.PasswordEncryptionCompatability;
import com.adobe.fd.encryption.client.PasswordEncryptionOption;
import com.adobe.fd.encryption.client.PasswordEncryptionOptionSpec;
import com.adobe.fd.encryption.client.PasswordEncryptionPermission;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * password encryption, certifying a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptCertifyExtend.class)
public class PassEncryptCertifyExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void SecureDocument(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getPassEncryptionOptions(), getCertificationOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getPassEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

  //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
        PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();

        //Specify the PDF document resource to encrypt
        passSpec.setEncryptOption(PasswordEncryptionOption.ALL);

        //Specify the permission associated with the password
        //These permissions enable data to be extracted from a password
        //protected PDF form
        List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
        passSpec.setPermissionsRequested(encrypPermissions);

        //Specify the Acrobat version
        passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);

        //Specify the password values
        passSpec.setDocumentOpenPassword("OpenPassword");
        passSpec.setPermissionPassword("PermissionPassword");

        //Set the encryption type to Password Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_PASSWORD);
        encryptionOptions.setPasswordEncryptionOptionSpec(passSpec);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

**Ejemplo 2**: este ejemplo se utiliza para realizar el cifrado PKI, firmar un campo de firma y el ampliar con Reader el documento PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.CertificateEncryptionCompatibility;
import com.adobe.fd.encryption.client.CertificateEncryptionIdentity;
import com.adobe.fd.encryption.client.CertificateEncryptionOption;
import com.adobe.fd.encryption.client.CertificateEncryptionOptionSpec;
import com.adobe.fd.encryption.client.CertificateEncryptionPermissions;
import com.adobe.fd.encryption.client.Recipient;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * certificate encryption, signing a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for encrypting the document has to be uploaded on Granite Trust Store
       Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptSignExtend.class)
public class PassEncryptSignExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void CertEncryptSignReaderExtend(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getCertEncryptionOptions(), getSignatureOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getCertEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

        //Set the encryption type to Certificate Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_CERTIFCATE);

  //Set the List that stores PKI information
  List<CertificateEncryptionIdentity> pkiIdentities = new ArrayList<CertificateEncryptionIdentity>();

  //Set the Permission List
  List<CertificateEncryptionPermissions> permList = new ArrayList<CertificateEncryptionPermissions>();
  permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;

  //Create a Recipient object to store certificate information
  Recipient recipient = new Recipient();

  //Specify the alias of the public certificate present in the trust store that is used to encrypt the document
  recipient.setX509Cert("alias");
  /*
   * An alternative to add a certificate is by providing the alias
   * of the certificate stored in AEM trust store.
   * recipient.setAlias(alias);
   */

  //Create an EncryptionIdentity object
  CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
  encryptionId.setPerms(permList);
  encryptionId.setRecipient(recipient);

  //Add the EncryptionIdentity to the list
  pkiIdentities.add(encryptionId);

  //Set encryption run-time options
  CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
  certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
  certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_9);

  //Set the certificate encryption option
  encryptionOptions.setCertOptionSpec(certOptionsSpec)

  //Set the PKI Identities in encryption Options
        encryptionOptions.setPkiIdentities(pkiIdentities);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

Si aparece el siguiente mensaje de error mientras el lector amplía un documento PDF:

```javascript
org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.ThreadDeath: null at com.adobe.internal.pdftoolkit.services.javascript.GibsonContextFactory.observeInstructionCount(GibsonContextFactory.java:138)
```

Significa que el servicio de ampliación de Reader no puede ejecutar los JavaScript utilizados en el documento dentro del intervalo de tiempo de espera definido.

Administre el intervalo de tiempo de espera definido para JavaScript en el documento PDF mediante:

```javascript
ReaderExtensionsOptionSpec optionSpec = new ReaderExtensionsOptionSpec(usageRights, message);
optionSpec.setJsScriptExecutionTimeoutInterval(100);
```

donde 100 hace referencia al intervalo de tiempo de espera definido para la ejecución de JavaScript (en segundos). Establezca un valor apropiado para el intervalo de tiempo de espera.

### Obtener derechos de uso de credenciales {#getting-credential-usage-rights}

Para recuperar la información de derechos de uso de la credencial especificada por el `credentialAlias`, llame a esta API desde la API `SecureDocument`.

**Sintaxis**: `getCredentialUsageRights(String credentialAlias, ResourceResolver resourceResolver)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>credentialAlias</code><br /> </td>
   <td>El <code>credentialAlias</code> que especifica la credencial.<br /> </td>
  </tr>
  <tr>
   <td><code>credentialPassword</code><br /> </td>
   <td>Para la contraseña de la credencial, si esta está cifrada, se debe utilizar nulo si la credencial no está cifrada.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo obtiene información de derechos de uso para las credenciales especificadas.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 *
 */
@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
 private ResourceResolverFactory resourceResolverFactory;
public void getCredentialUsageRights() {
  try {

   GetUsageRightsResult usageRightsResult = docAssuranceService.getCredentialUsageRights("production",
     resourceResolverFactory.getAdministrativeResourceResolver(null));

   System.out.println("Credential usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  }
 }
}
```

### Obtener derechos de uso de documentos {#getting-document-usage-rights}

Para recuperar la información de derechos de uso de un documento determinado, llame a esta API desde la API `docAssuranceService`.

**Sintaxis**: `getDocumentUsageRights(Document inDocument, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>Documento desde el que se obtiene la información de derechos de uso<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente código de ejemplo devuelve la información de derechos de uso de un documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void getDocumentUsageRights() {
  Document inputDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/GetUsageRightsInfo/02_fromAcrobat7.0.8_Acro700_UB8_BS_signed_commenting.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   GetUsageRightsResult usageRightsResult = docAssuranceService.getDocumentUsageRights(inputDocument, unlockOptions);

   System.out.println("Document usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  } finally {
//   if (inputDocument != null) {
//    inputDocument.dispose(); //dispose off the document.
//   }
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

### Quitar derechos de uso {#removing-usage-rights}

Puede quitar los derechos de uso de un documento llamando a la API `removeUsageRights` desde la API `docAssuranceService`.

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>Documento desde el que se quitan los derechos de uso.<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo quita los derechos de uso de un documento determinado.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void removeDocumentUsageRights() {
  Document inputDocument = null;
  Document outDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/RemoveUsageRights/01_Ubiquitized_50-267_PDF1.5_UB2_Rights.pdf";

   //Name of the output file where result will be saved.
   String outputFileName = "C:/RETest/output/samples/removeUsageRightsOutput.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   //Specify null encryption options and signatures options.
   //If requirement is also to encrypt and sign the document then, corresponding options can also be specified.
   outDocument = docAssuranceService.removeUsageRights(inputDocument, unlockOptions);

   File outputdir = new File("C:/RETest/output/samples");
   outputdir.mkdirs();

   outDocument.copyToFile(new File(outputFileName));
  } catch (Exception e) {
   e.printStackTrace();
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

#### Verificar firmas digitales {#verifying-digital-signatures}

Las firmas digitales se pueden verificar para garantizar que no se haya modificado un documento PDF firmado y que la firma digital sea válida. Al verificar una firma digital, puede comprobar el estado y las propiedades de la firma, como la identidad del firmante. Antes de confiar en una firma digital, se recomienda verificarla. Al verificar una firma digital, haga referencia a un documento de PDF que contenga una firma digital.

**Sintaxis**: `verify( inDoc, signatureFieldName, revocationCheckStyle, verificationTime, dssPrefs, ResourceResolver resourceResolver)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF<br /> </td>
  </tr>
  <tr>
   <td><code class="code">signatureField
      Name</code><br /> </td>
   <td>Nombre del campo de firma que se debe validar. se puede dar un nombre completo o parcial<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>Opción para regular la comprobación de revocación de los certificados encontrados durante la validación</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>El momento en que debe validarse la firma</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>Preferencias para controlar distintas configuraciones de validación. Para un documento cifrado, defina las opciones de desbloqueo mediante <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Resolución de recursos en el repositorio de Granite Trust</td>
  </tr>
 </tbody>
</table>

Este código de ejemplo utiliza `DocAssuranceService` para comprobar un campo de firma en un documento PDF cifrado.

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.IdentityInformation;
import com.adobe.fd.signatures.client.types.IdentityStatus;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of a signature field in an already Encrypted PDF Document
 *
 * Digital signatures can be verified to ensure that a signed PDF document was not modified and that the digital signature is valid.
 * When verifying a digital signature, you can check the signature's status and the signature's properties, such as the signer's identity.
 * Before trusting a digital signature, it is recommended that you verify it. When verifying a digital signature, reference a PDF document
 * that contains a digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyFieldEncryptedPDF.class)
public class VerifyFieldEncryptedPDF {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyFieldEncryptedPDF(String inputFile,String fieldName) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

         //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

           //Specify the name of the signature field

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.AlwaysCheck;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFSignatureVerificationInfo  signInfo = docAssuranceService.verify(
                 inDoc,
                 fieldName,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get the Signature Status
             SignatureStatus sigStatus = signInfo.getStatus();
             String myStatus="";

             //Determine the status of the signature
             if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                 myStatus = "The signatures in the dynamic PDF form are unknown";
             else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                 myStatus = "The signatures in the PDF document are unknown";
             else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a certified PDF form are valid";
             else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a signed dynamic PDF form are valid";
             else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                 myStatus = "The signatures in a certified PDF document are valid";
             else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                 myStatus = "The signatures in a signed PDF document are valid";
             else if (sigStatus == SignatureStatus.SignatureFormatError)
                 myStatus = "The format of a signature in a signed document is invalid";
             else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                 myStatus = "No changes were made to the signed dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                 myStatus = "No changes were made to the signed PDF document";
             else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified PDF document";
             else if (sigStatus == SignatureStatus.DocSigWithChanges)
                 myStatus = "There were changes to a signed PDF document";
            else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                 myStatus = "There were changes made to the PDF document.";

             //Get the signature type
             SignatureType sigType = signInfo.getSignatureType();
             String myType = "";

             if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                    myType="Certification";
             else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                    myType="Recipient";

             //Get the identity of the signer
             IdentityInformation signerId = signInfo.getSigner();
             String signerMsg = "";

            if (signerId.getStatus() == IdentityStatus.UNKNOWN)
                signerMsg = "Identity Unknown";
            else if (signerId.getStatus() == IdentityStatus.TRUSTED)
                signerMsg = "Identity Trusted";
            else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
                signerMsg = "Identity Not Trusted";

            //Get the Signature properties returned by the Signature service
            SignatureProperties sigProps = signInfo.getSignatureProps();
            String signerName =  sigProps.getSignerName();

           System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        pkiPref.setOCSPPreferences(getOCSPPref());
        pkiPref.setTSPPreferences(getTspPref());
        return pkiPref;
    }

    private static TSPPreferences getTspPref(){
     TSPPreferencesImpl tsp = new TSPPreferencesImpl();
     tsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return tsp;
    }
    private static OCSPPreferencesImpl getOCSPPref(){
     OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
     ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return ocsp;
    }
    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(true);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Verificar varias firmas digitales {#verifying-multiple-digital-signatures}

AEM permite verificar las firmas digitales en los documentos PDF. Un documento PDF puede contener varias firmas digitales si está sujeto a un proceso empresarial que requiera firmas de varios firmantes. Por ejemplo, una transacción financiera requiere las firmas del responsable del préstamo y del administrador. Puede utilizar la API del servicio de firma para comprobar todas las firmas del documento PDF. Al comprobar varias firmas digitales, puede comprobar el estado y las propiedades de cada firma. Antes de confiar en una firma digital, Adobe recomienda verificarla.

**Sintaxis**: `verifyDocument(Document doc, RevocationCheckStyle revocationCheckStyle, VerificationTime verificationTime, ValidationPreferences prefStore, ResourceResolver resourceResolver)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>Opción para regular la comprobación de revocación de los certificados encontrados durante la validación</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>El momento en que debe validarse la firma</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>Preferencias para controlar distintas configuraciones de validación. Para un documento cifrado, defina las opciones de desbloqueo mediante <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Resolución de recursos en el repositorio de Granite Trust</td>
  </tr>
 </tbody>
</table>

El siguiente código de ejemplo utiliza DocAssuranceService para verificar los campos de firma de un documento PDF ya cifrado.

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.List;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFDocumentVerificationInfo;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of all the signature fields in an already Encrypted PDF Document
 *
 * Assume that a PDF document contains multiple digital signatures as a result of a business process that requires signatures from multiple
 * signers. For example, consider a financial transaction that requires both a loan officer's and a manager's signature. You can use the
 * Signature service Java API or web service API to verify all signatures within the PDF document. When verifying multiple digital signatures,
 * you can check the status and properties of each signature. Before you trust a digital signature, it is recommended that you verify it. It
 * is recommended that you are familiar with verifying a single digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyEncryptedPDFDoc.class)
public class VerifyEncryptedPDFDoc {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyEncryptedPDFDoc(String inputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.CheckIfAvailable;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFDocumentVerificationInfo  docInfo = docAssuranceService.verifyDocument(
                 inDoc,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get a list of all signatures that are in the PDF document
             List allSignatures = docInfo.getVerificationInfos();

           //Create an Iterator object and iterate through
           //the List object
           Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();

           while (iter.hasNext()) {
                  PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();

                  //Get the Signature Status
                     SignatureStatus sigStatus = signInfo.getStatus();
                     String myStatus="";

                   //Determine the status of the signature
                     if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                         myStatus = "The signatures in the dynamic PDF form are unknown";
                     else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                         myStatus = "The signatures in the PDF document are unknown";
                     else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a certified PDF form are valid";
                     else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a signed dynamic PDF form are valid";
                     else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                         myStatus = "The signatures in a certified PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                         myStatus = "The signatures in a signed PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignatureFormatError)
                         myStatus = "The format of a signature in a signed document is invalid";
                     else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                         myStatus = "No changes were made to the signed dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                         myStatus = "No changes were made to the signed PDF document";
                     else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified PDF document";
                     else if (sigStatus == SignatureStatus.DocSigWithChanges)
                         myStatus = "There were changes to a signed PDF document";
                    else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                         myStatus = "There were changes made to the PDF document.";

                     //Get the signature type
                    SignatureType sigType = signInfo.getSignatureType();
                    String myType = "";

                    if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                        myType="Certification";
                    else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                        myType="Recipient";

                    //Get the Signature properties returned by the Signature service
                    SignatureProperties sigProps = signInfo.getSignatureProps();
                    String signerName =  sigProps.getSignerName();

                   System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
               }
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the document is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### Quitar firmas digitales {#removing-digital-signatures}

Solo se puede aplicar una firma digital nueva a un campo de firma después de quitar la anterior. No se puede sobrescribir una firma digital. Si intenta aplicar una firma digital a un campo de firma que ya contiene otra firma, se producirá una excepción.

**Sintaxis**: `clearSignatureField(Document inDoc, String signatureFieldName, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>Nombre del campo de firma<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>Incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java quita una firma digital de un campo de firma.

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file
*from a source other than Adobe, then your use, modification, or distribution of it requires
*the prior written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures must be removed from a signature field before a newer digital signature can be applied.
 * A digital signature cannot be overwritten.
 * If you attempt to apply a digital signature to a signature field that contains a signature, an exception occurs
 *
 *The following Java code example removes a digital signature from a signature field named SignatureField1.
 *The name of the PDF file that contain the signature field is LoanSigned.pdf
 */

@Component
@Service(value=ClearSignatureField.class)
public class ClearSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;
 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  * @throws Exception
  */
 public void clearSignatureField(String inputFile, String outFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Clear the signature field
        //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        Document outPDF = docAssuranceService.clearSignatureField(inDoc,fieldName,null);

        //save the outPDF
        outPDF.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Obtener certificados de campo de firma {#getting-certifying-signature-field}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que están en un documento de PDF o desea verificarlos, puede recuperarlos mediante programación. El servicio Firma devuelve el nombre completo del campo de firma, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintaxis**: `getCertifyingSignatureField(Document inDoc, UnlockOptions unlockOptions)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Objeto de documento que contiene el PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>UnlockOptions incluye los parámetros necesarios para desbloquear un archivo cifrado. Esto solo es necesario si el archivo está cifrado.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java recupera el campo de firma que se utilizó para certificar el documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the ignature field that was used to certify the document.
 */

@Component
@Service(value=GetCertifyingSignatureField.class)
public class GetCertifyingSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getCertifyingSignatureField(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignatureField pdfSignature = docAssuranceService.getCertifyingSignatureField(inDoc,null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Obtener el tipo de cifrado del PDF {#getting-pdf-encryption-type}

Puede recuperar los nombres de todos los campos de firma que se encuentran en un documento de PDF que desee firmar o certificar. Si no está seguro de los nombres de los campos de firma que están en un documento de PDF o desea verificarlos, puede recuperarlos mediante programación. El servicio de firma devuelve el nombre completo del campo de firma, como `asform1[0].grantApplication[0].page1[0].SignatureField1[0]`.

**Sintaxis**: `void getPDFEncryption(Document inDoc)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento proporcionado como entrada. Puede o no cifrarse.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java recupera la información de la firma del campo de firma dado en un documento de PDF.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.encryption.client.EncryptionTypeResult;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetPDFEncryption.class)
public class GetPDFEncryption {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getPDFEncryption(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        EncryptionTypeResult encryptionTypeResult = docAssuranceService.getPDFEncryption(inDoc);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### Quitar el cifrado mediante contraseña del PDF {#removing-password-encryption-from-pdf}

Quite el cifrado basado en contraseña de un documento PDF para permitir a los usuarios abrir el documento en Adobe Reader o Acrobat sin tener que especificar una contraseña. Después de quitar el cifrado basado en contraseña de un documento PDF, el documento ya no será seguro.

**Sintaxis**: `Document removePDFPasswordSecurity (Document inDoc,String password)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Documento suministrado como entrada. Debe estar protegido con una contraseña.<br /> </td>
  </tr>
  <tr>
   <td><code>password</code><br /> </td>
   <td>Abra un documento o use una contraseña de permiso para quitar la seguridad del documento.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código quita el cifrado basado en contraseña de un documento PDF.

```java
    package com.adobe.docassurance.samples;

    import java.io.File;
    import java.io.FileNotFoundException;
    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.jcr.api.SlingRepository;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes password-based encryption from a PDF document.
    * The master password value used to remove password-based encryption is PermissionPassword
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePasswordEncryption.class)
    public class RemovePasswordEncryption {

    // Create reference for DocAssuranceService
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    /**
    * The below sample code demonstrates removing password encryption from a PDF using AEM EncryptionService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_out.pdf"
    * @throws Exception
    */
    public void removePasswordEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

        try{

        String password = "PermissionPassword"; //master password with which the pdf was encrypted
                    //in case if the pdf is encrypted only with user password, specify the
                    //user password
        //Remove password-based encryption from the PDF document
        outDoc = docAssuranceService.removePDFPasswordSecurity(inDoc,password);

        }finally{
                    /**
                    * always close the PDFDocument object after your processing is done.
                    */
                    if(inDoc != null){
                        inDoc.close();
                    }

            }

            outDoc.copyToFile(outFile);

    }

    }
```

### Quitar el cifrado de certificados {#removing-certificate-encryption}

Puede quitar el cifrado basado en certificados de un documento PDF para que los usuarios puedan abrirlo en Adobe Reader o Acrobat. Para quitar el cifrado de un documento PDF cifrado mediante un certificado, haga referencia a una clave privada. Después de quitar el cifrado de un documento PDF, este ya no será seguro.

**Sintaxis**: `removePDFCertificateSecurity(Document inDoc, String alias, ResourceResolver resourceResolver)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>Objeto Document que representa el documento PDF cifrado mediante certificado.<br /> </td>
  </tr>
  <tr>
   <td><code>alias</code><br /> </td>
   <td>El alias que corresponde a la clave del repositorio de Granite Trust que se utiliza para quitar el cifrado basado en certificados del documento PDF.<br /> </td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>ResourceResolver permite acceder al repositorio de claves de un usuario en particular para recuperar la credencial.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java quita el cifrado basado en certificados de un documento PDF.

```java
    package com.adobe.docassurance.samples;

    import java.io.File;

    import javax.jcr.Session;

    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.api.resource.ResourceResolver;
    import org.apache.sling.jcr.api.SlingRepository;
    import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes certificate-based encryption from a PDF document
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePKIEncryption.class)
    public class RemovePKIEncryption {

    // Create reference for docAssuranceServiceInterface
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    @Reference
        private JcrResourceResolverFactory jcrResourceResolverFactory ;

    /**
    * The below sample code demonstrates encrypting PDF with Password using AEM docAssuranceService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_Encrypted.pdf"
    *
    * @throws Exception
    */
    public void removePKIEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

            Session adminSession = null;
            ResourceResolver resourceResolver = null;
            try{
        adminSession = slingRepository.loginAdministrative(null);
        resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

        //Remove certificate-based encryption from the PDF document
        /**
        * Here the alias("encryption") of the private credential stored in the keystore of the
        * user has been provided with the user's resource resolver
        */
        outDoc = docAssuranceService.removePDFCertificateSecurity(inDoc, "encryption",resourceResolver);

            }catch(Exception e){

            // TODO Auto-generated catch block
            }finally{
                /**
                * always close the PDFDocument object after your processing is done.
                */
                if(inDoc != null){
                    inDoc.close();
                }
                if(adminSession != null && adminSession.isLive()){
                    if(resourceResolver != null){
                        resourceResolver.close();
                    }
                    adminSession.logout();
                }
            }

            outDoc.copyToFile(outFile);
    }

    }
```

## Servicio de salida {#output-service}

El servicio Output proporciona varias API para procesar un archivo XDP en los formatos .pdf, .pcl, .zpl y .ps. El servicio admite las siguientes API:

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** genera un documento PDF al combinar un diseño de formulario con datos almacenados en una ubicación de red, un sistema de archivos local o una ubicación HTTP como valores literales.

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p):** genera un documento PDF al combinar un diseño de formulario con datos almacenados en una aplicación.
* **[generatePDFOutputBatch](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutputbatch-p):** combina un diseño de formulario con datos para crear un documento PDF. Opcionalmente, genera un archivo de metadatos para cada registro o guarda la salida en un archivo PDF.
* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** genera una salida PCL, PostScript o ZPL a partir de un diseño de formulario y un archivo de datos almacenados en una ubicación de red, un sistema de archivos local o una ubicación HTTP como valores literales.

* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p):** genera una salida PCL, PostScript y ZPL a partir de un diseño de formulario y un archivo de datos que se almacenan en una aplicación.

### generatePDFOutput {#generatepdfoutput}

La API generatePDFOutput genera un documento PDF al combinar un diseño de formulario con datos. Opcionalmente, genera un archivo de metadatos para cada registro o guarda la salida en un archivo PDF. Utilice la API generatePDFOutput para los diseños de formulario o los datos almacenados en una ubicación de red, un sistema de archivos local o una ubicación HTTP como valores literales. Si el diseño de formulario y los datos XML se almacenan en una aplicación, utilice la API [generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p).

**Sintaxis:** `Document generatePDFOutput(String uriOrFileName, Document data, PDFOutputOptions options);`

#### Parámetros de entrada {#input-parameters}

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>uriOrFileName</td>
   <td>Especifica la ruta y el nombre del archivo de entrada. El archivo puede ser de tipo PDF o XDP. Si solo se especifica el nombre de archivo, el archivo se leerá en relación con el contentRoot especificado en las opciones.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Archivo XML que contiene los datos combinados con el documento PDF.<br /> </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Especifica valores de las variables contentRoot, locale, AcrobatVersion, linearizedPDF y taggedPDF. El parámetro de opciones acepta un objeto del tipo PDFOutputOptions. <br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera un documento PDF al combinar un diseño de formulario con datos almacenados en un archivo XML.

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput(String contentRoot,File inputXML,String templateStr,String acrobatVersion,String tagged,String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

    try {

            PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);         if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

            {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {             option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

            }

            if (tagged.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if (linearized.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if(locale!=null)

            {

                option.setLocale(locale);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePDFOutput(templateStr,new Document(in),option);         File toSave = new File(outputFolder+"Output.pdf");

            doc.copyToFile(toSave);

            return toSave;

        } catch (OutputServiceException e) {

            e.printStackTrace();

        }catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }finally{

                    doc.dispose();

        }

        return null;

    }
```

### generatePDFOutput {#generatepdfoutput-1}

La API generatePDFOutput genera un documento PDF al combinar un diseño de formulario con datos. De forma opcional, genere un archivo de metadatos para cada registro o guarde la salida en un archivo PDF. Utilice la API generatePrintedOutput para los diseños de formulario o los datos almacenados en una aplicación. Si el diseño de formulario y los datos XML se almacenan en una ubicación de red, localmente o en una ubicación HTTP como valores literales, utilice la API [generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p).

**Sintaxis:** `Document generatePDFOutput(Document inputdocument, Document data, PDFOutputOptions options)`

#### Parámetro de entrada {#input-parameter}

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>Especifica la ruta y el nombre del archivo de entrada. El archivo puede ser de tipo PDF o XDP. Si solo se especifica el nombre de archivo, el archivo se leerá en relación con el contentRoot especificado en las opciones. <br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>Archivo XML que contiene los datos combinados con el documento PDF.<br /> </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Especifica valores de las variables contentRoot, locale, AcrobatVersion, linearizedPDF y taggedPDF. El parámetro options acepta un objeto del tipo PDFOutputOptions.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera un documento PDF al combinar un diseño de formulario con datos almacenados en un archivo XML.

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput2(String contentRoot, File inputXML, File templateStr, String acrobatVersion, String tagged, String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

        try {

                PDFOutputOptions option = new PDFOutputOptions();             option.setContentRoot(contentRoot);
                if(locale!=null)

                {

                    option.setLocale(locale);

                }

                if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

                {

                    option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

                }

                if (tagged.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                if (linearized.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                InputStream inputXMLStream = new FileInputStream(inputXML);

                InputStream templateStream = new FileInputStream(templateStr);;

                doc = outputService.generatePDFOutput(new Document(templateStream),new             Document(inputXMLStream),option);

                        File toSave = new File(outputFolder,"Output.pdf");

                        doc.copyToFile(toSave);

                        return toSave;

                    } catch (OutputServiceException e) {

                            e.printStackTrace();

                }catch (FileNotFoundException e) {

                            e.printStackTrace();

                } catch (IOException e) {

                            e.printStackTrace();

                }finally{

                                doc.dispose();

                }

                    return null;

    }
```

### generatePDFOutputBatch {#generatepdfoutputbatch}

Combina un diseño de formulario con datos para crear un documento PDF. Opcionalmente, genera un archivo de metadatos para cada registro o guarda la salida en un archivo PDF. Utilice la API generatePDFOutputBatch para diseños de formulario o datos almacenados en una ubicación de red, un sistema de archivos local o una ubicación HTTP como valores literales.

**Sintaxis:** `BatchResult generatePDFOutputBatch(Map templates, Map data, PDFOutputOptions options, BatchOptions batchOptions);`

#### Parámetros de entrada {#input-parameters-1}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>templates<br /> </td>
   <td>Especifica el mapa de la clave y el nombre del archivo de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>Especifica el mapa de la clave y del documento de datos. Si la clave no es nula, el documento de datos se procesará con la plantilla para la clave correspondiente especificada en el mapa de plantillas. </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Especifica valores de las variables contentRoot, locale, AcrobatVersion, linearizedPDF y taggedPDF. El parámetro options acepta un objeto del tipo PDFOutputOptions.</td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>Especifica el valor de la variable <code>generateManyFiles</code>. Establezca el indicador generateManyFiles para generar varios archivos. El parámetro options acepta un objeto del tipo BatchOptions.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera documentos PDF al combinar diseños de formulario con datos almacenados en un archivo XML.

```java
private ArrayList generatePDFBatch(String contentRoot,String multipleFiles) {

String outputFolder="C:/Output";

    try {

        PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);

        Map templates = new LinkedHashMap();

        Map data = new LinkedHashMap();

        String template1 = "PurchaseOrder.xdp"; String template2 = "CardApp.xdp";         templates.put(template1.substring(0, template1.indexOf(".xdp")),template1);         templates.put(template1.substring(0, template2.indexOf(".xdp")),template2);

        File inputXML1 = new File("c:/InputFolder/PurchaseOrder.xml");

        File inputXML2 = new File("c:/InputFolder/CardApp.xml");

        InputStream in1 = new FileInputStream(inputXML1);

        InputStream in2 = new FileInputStream(inputXML2);

        data.put(template1.substring(0, template1.indexOf(".xdp")),new         Document((in1))); data.put(template1.substring(0,         template1.indexOf(".xdp")),new Document((in2))); BatchOptions bo = new         BatchOptions(); BatchResult ret=null;         if(multipleFiles.equalsIgnoreCase("true"))

        {

            bo.setGenerateManyFiles(true);

            ret = outputService.generatePDFOutputBatch(templates, data, option, bo);

        } else {

            ret = outputService.generatePDFOutputBatch(templates, data, option, new             BatchOptions());

        }

        ArrayList outputs = new ArrayList();

        int counter=0;

        if(ret.getMetaDataDoc() !=null ){

        File toSave = new File(outputFolder+"Output.xml");

        ret.getMetaDataDoc().copyToFile(toSave);

        outputs.add(toSave);

        List<Document> list = ret.getGeneratedDocs();

        for(Document doc:list){

        File toSave = new File(outputFolder,"Output"+"_"+counter+".pdf");         doc.copyToFile(toSave);                    outputs.add(toSave);

        counter++;

        doc.dispose();

        }

        return outputs;

       } catch (OutputServiceException e) {

            e.printStackTrace();

       }catch (FileNotFoundException e) {

            e.printStackTrace();

       }catch (IOException e) {

            e.printStackTrace();

       }

       return null;

}
```

### generatePrintedOutput {#generateprintedoutput}

Genera una salida PCL, PostScript y ZPL a partir de un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le aplica un formato para imprimirlo. Puede enviar la salida directamente a una impresora o guardarla como archivo. Utilice la API generatePrintedOutput para los diseños de formulario o los datos almacenados en una aplicación.

**Sintaxis:** `Document generatePrintedOutput(String uriOrFileName, Document data, PrintedOutputOptions);`

#### Parámetros de entrada {#input-parameters-2}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>uriOrFileName<br /> </td>
   <td>Especifica la ruta y el nombre del archivo de entrada. Si solo se especifica el nombre de archivo, el archivo se leerá en relación con el contentRoot especificado en las opciones. El archivo puede ser de tipo PDF o XDP.<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>Archivo XML que contiene datos combinados con documentos PDF.<br /> </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Especifica valores de las variables contentRoot, locale, AcrobatVersion, linearizedPDF y taggedPDF. El parámetro options acepta un objeto del tipo PrintedOutputOptions.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera una salida PCL, PostScript y ZPL a partir de un diseño de formulario y datos. El tipo de salida depende del valor aprobado en el parámetro `printConfig`.

```java
@Reference private OutputService outputService;

private File generatePrintedOutput(String contentRoot,File inputXML,String templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

    try {

            PrintedOutputOptions options = new PrintedOutputOptions();                           options.setContentRoot(contentRoot);

            if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {

                            options.setPrintConfig(PrintConfig.HP_PCL_5e);

                     }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePrintedOutput(templateStr,new             Document(in),options);

            in.close();

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return  toSave;

        } catch (OutputServiceException e) {

             e.printStackTrace();

        }catch (FileNotFoundException e) {

             e.printStackTrace();

        }catch (IOException e) {

             e.printStackTrace();

        }finally{

             doc.dispose();

        }

        return null;

}
```

### generatePrintedOutput {#generateprintedoutput-1}

Genera una salida PCL, PostScript y ZPL a partir de un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le aplica un formato para imprimirlo. La salida se puede enviar directamente a una impresora o guardarse como archivo. Utilice la API generatePrintedOutput para los diseños de formulario o los datos almacenados en una aplicación.

**Sintaxis:** `Document generatePrintedOutput(Document inputdocument, Document data, PrintedOutputOptions);`

#### Parámetros de entrada {#input-parameters-3}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>Especifica la ruta y el nombre del archivo de entrada. Si solo se especifica el nombre de archivo, el archivo se leerá en relación con el contentRoot especificado en las opciones. El archivo puede ser de tipo XDP. </td>
  </tr>
  <tr>
   <td>data</td>
   <td>Archivo XML que contiene datos combinados con documentos PDF.<br /> </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Este objeto se utiliza para establecer los valores de contentRoot, locale, printConfig, copies y paginationOverride. El parámetro options acepta un objeto del tipo PrintedOutputOptions.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera una salida PCL, PostScript y ZPL a partir de un diseño de formulario y datos. El tipo de salida depende del valor aprobado en el parámetro `printConfig`.

```java
@Reference private OutputService outputService;

private File generatePrintedOutput2(File  inputXML,File templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

       try {

            PrintedOutputOptions options = new PrintedOutputOptions();             if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {                                   options.setPrintConfig(PrintConfig.HP_PCL_5e);

            }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

                             }

            InputStream inputXMlStream = new FileInputStream(inputXML);

            InputStream templateStream = new FileInputStream(templateStr); doc =             outputService.generatePrintedOutput(new Document(templateStream),new             Document(inputXMlStream),options);

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return toSave;

            } catch (OutputServiceException e) {

                e.printStackTrace();

            }catch (FileNotFoundException e) {

                e.printStackTrace();

            } catch (IOException e) {

                e.printStackTrace();

            }finally{

                doc.dispose();

            }

            return null;

}
```

### generatePrintedOutputBatch {#generateprintedoutputbatch}

Genera un documento en formato PS, PCL y ZPL al combinar un diseño de formulario con datos. De forma opcional, genere un archivo de metadatos para cada registro o guarde la salida en un archivo PDF. Utilice la API generatePrintedOutputBatch para los diseños de formulario o los datos almacenados en una ubicación de red, un sistema de archivos local o una ubicación HTTP como valores literales.

**Sintaxis`:`** `BatchResult generatePrintedOutputBatch(Map templates, Map data, PrintedOutputOptions options, BatchOptions batchOptions);`

#### Parámetros de entrada {#input-parameters-4}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>templates<br /> </td>
   <td>Especifica el mapa de la clave y el nombre de archivo de la plantilla.<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>Especifica el mapa de la clave y el documento de datos. Si la clave no es nula, el documento de datos se procesará con la plantilla para la clave correspondiente en el mapa de plantillas.<br /> </td>
  </tr>
  <tr>
   <td>opciones</td>
   <td>Especifica el objeto del tipo PrintedOutputOptions. Este objeto se utiliza para establecer los valores de contentRoot, locale, printConfig, copies, paginationOverride.<br /> </td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>Especifica el valor de la variable generateManyFiles. Establezca el indicador generateManyFiles para generar varios archivos. El parámetro options acepta un objeto del tipo BatchOptions.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java genera la salida PCL, PostScript y ZPL por lotes a partir de varias plantillas de diseño de formulario y archivos de datos. El tipo de salida depende del valor aprobado en el parámetro `printConfig`.

```java
@Reference private OutputService outputService;

private ArrayList generatePrintedOutputBatch(String contentRoot,String multipleFiles,String printConfig) {

String outputFolder="C:/Output";

        try {

                PrintedOutputOptions option = new PrintedOutputOptions();                 option.setContentRoot(contentRoot);

                Map templates = new LinkedHashMap();

                Map data = new LinkedHashMap();

                String template1 = "PurchaseOrder.xdp";

                String template2 = "CardApp.xdp";

                templates.put(template1.substring(0,                 template1.indexOf(".xdp")),template1);                 templates.put(template1.substring(0,                 template2.indexOf(".xdp")),template2);

                File inputXML1 = new                                   File("c:/InputFolder/PurchaseOrder.xml");

                File inputXML2 = new File("c:/InputFolder/CardApp.xml");

                InputStream in1 = new FileInputStream(inputXML1);

                InputStream in2 = new FileInputStream(inputXML2);                  data.put(template1.substring(0,                     template1.indexOf(".xdp")),new Document((in1)));

                 data.put(template2.substring(0,                     template2.indexOf(".xdp")),new Document((in2)));

                 if(printConfig.equalsIgnoreCase("ps"))

                 {

                    option.setPrintConfig(PrintConfig.PS_PLAIN);

                 } else if(printConfig.equalsIgnoreCase("pcl"))

                 {

                    option.setPrintConfig(PrintConfig.HP_PCL_5e);

                 } else if(printConfig.equalsIgnoreCase("zpl")){

                                         option.setPrintConfig(PrintConfig.ZPL300);

                 }

                 option.setContentRoot(contentRoot);

                 BatchOptions bo = new BatchOptions();

                 BatchResult ret =                             outputService.generatePrintedOutputBatch(temp                                    lates, data, option, new                                                     BatchOptions());

                 ArrayList outputs = new ArrayList();

                 int counter=0;

                 if(ret.getMetaDataDoc() !=null ){

                 File toSave = new File(outputFolder,"Output"+".xml");                    ret.getMetaDataDoc().copyToFile(toSave);

                 outputs.add(toSave);

                 List<Document> list = ret.getGeneratedDocs();

                 for(Document doc:list){

                 File toSave = new                                                               File(outputFolder,"Output"+"_"+counter+".                                        "+printConfig);                                    doc.copyToFile(toSave);

                 outputs.add(toSave);

                 counter++;

                 doc.dispose();

                 }

                 return outputs;

          }

            catch (OutputServiceException e) {

                e.printStackTrace();

          }catch (FileNotFoundException e) {

                e.printStackTrace();

          } catch (IOException e) {

                e.printStackTrace();

          }

            return null;

  }
```

## Servicio de Forms {#forms-service}

El servicio Forms proporciona API para importar y exportar datos desde y hacia un formulario PDF interactivo. Un formulario PDF interactivo es un documento PDF que contiene uno o más campos utilizados para mostrar y recopilar información de los usuarios. El servicio admite las siguientes API:

* **[exportData](/help/forms/using/aem-document-services-programmatically.md#p-exportdata-p):** exporta datos desde un formulario PDF.
* **[importData](/help/forms/using/aem-document-services-programmatically.md#p-importdata-p):** importa datos en un formulario PDF interactivo.

### exportData {#exportdata}

Exporta datos de formulario desde un formulario PDF interactivo en los formatos XML y XDP.

**Sintaxis:** `Document exportData(Document xdpOrPdf, DataFormat dataFormat)`

#### Parámetros de entrada {#input-parameters-5}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>xdpOrPdf<br /> </td>
   <td>Especifica un objeto de documento que contiene un archivo XDP o PDF. </td>
  </tr>
  <tr>
   <td>dataFormat<br /> </td>
   <td>Especifica el formato en el que se exportan los datos. Acepta variable de tipo enum(XDP, XmlData, Auto).<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java exporta datos de formulario desde un formulario de PDF interactivo en los formatos XML y XDP.

#### Muestra {#sample}

```java
@Reference private FormsService formsService;
private File exportData(String  dataFormat, File  inDoc) {

String outputFolder="C:/Output";

InputStream in; Document doc=null;

try {

        in = new FileInputStream(inDoc);

        if(dataFormat.equalsIgnoreCase("xml"))

        {

          doc=formsService.exportData(new Document(in),                                       DataFormat.XmlData);

        }

        else if(dataFormat.equalsIgnoreCase("xdp")) {

        doc =formsService.exportData(new Document(in),                       DataFormat.XDP);

        }

        File toSave = new File(outputFolder,"Output"+"."+dataFormat);

        doc.copyToFile(toSave);

        return toSave;

    } catch (FormsServiceException e) {

       e.printStackTrace();

    }catch (FileNotFoundException e) {

       e.printStackTrace();

    } catch (IOException e) {

       e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

 }
```

### importData {#importdata}

Importa datos de formulario a un formulario PDF interactivo.

**Sintaxis:** `Document importData(Document PDF, Document data)`

#### Parámetros de entrada {#input-parameters-6}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>PDF<br /> </td>
   <td>Especifica un objeto de documento que contiene archivos PDF. </td>
  </tr>
  <tr>
   <td>Datos<br /> </td>
   <td>Archivo XML que contiene datos en formato XML.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java importa datos de formulario en un formulario PDF interactivo.

#### Muestra {#sample-1}

```java
@Reference private FormsService formsService

private File importData(File inDoc, File inXML)

{

 String outputFolder="C:/Output";

 Document doc=null;

 try {

        InputStream in = new FileInputStream(inDoc);

        InputStream in2 = new FileInputStream(inXML);

        doc=formsService.importData(new Document(in), new Document(in2));

        File toSave = new File(outputFolder,"Output.pdf");

        doc.copyToFile(toSave);

    } catch (FormsServiceException e) {

         e.printStackTrace();

    }catch (FileNotFoundException e) {

         e.printStackTrace();

    } catch (IOException e) {

         e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

}
```

## Servicio Generador de PDF {#pdfgeneratorservice}

El servicio Generador de PDF proporciona API para convertir formatos de archivo nativos a PDF. También convierte PDF a otros formatos de archivo y optimiza el tamaño de los documentos PDF.

### GeneratePDFService {#generatepdfservice}

GeneratePDFService proporciona API para convertir varios formatos de archivo como .doc, .docx, .ppt, .pptx, .xls, .xlsx, .odp, .odt, .ods, .swf (obsoleto), .jpg, .bmp, .tif, .png, .html y muchos otros formatos a PDF. También proporciona API para exportar el PDF a varios formatos de archivo y optimizar los PDF. El servicio admite las siguientes API:

* **createPDF**: convierte un archivo compatible en un documento PDF. Admite formatos de archivo como Microsoft Word, Microsoft PowerPoint, Microsoft Excel y Microsoft Project. Además de estas aplicaciones, cualquier PDF genérico de terceros que genere un tipo de aplicación también puede conectarse a la API.
* **exportPDF**: convierte un documento PDF en un archivo compatible. El método acepta un PDF como entrada y exporta el contenido de este en el formato de archivo especificado. Puede exportar un documento PDF en los formatos: Encapsulated PostScript( eps), HTML 3.2( htm, html), HTML 4.01 with CSS 1.0( htm, html), JPEG( jpg, jpeg, jpe), JPEG2000( jpf, jpx, jp2, j2k, j2c, jpc), Documento de Microsoft Word ( doc, docx) Hoja de cálculo de Microsoft Excel ( xlsx), Presentación de Microsoft PowerPoint ( pptx), PNG( png), PostScript( ps), Formato de texto enriquecido ( rtf), Texto (Accesible)( txt), Text(Sin formato)( txt) TIFF( tif, tiff), XML 1.0( xml), PDF/A-1a(sRGB), PDF/A-1b, PDF/A-2a(sRGB), PDF/A-2b(sRGB), PDF/A-3a(sRGB), PDF/A-3b(sRGB). También puede especificar [perfiles de comprobación previa personalizados](https://helpx.adobe.com/es/acrobat/using/preflight-profiles-acrobat-pro.html) para las salidas PDF.

* **optimizePDF**: optimiza el documento PDF y también convierte un documento PDF de un tipo a otro. El método acepta un documento PDF como entrada.
* **htmlToPdf2**: convierte una página HTML en un documento PDF. Acepta la dirección URL de la página HTML como entrada.

>[!NOTE]
>
>La API HTMLtoPDF está obsoleta para el servidor de AEM Forms que se ejecuta en el sistema operativo AIX.

#### La API Generador de PDF está disponible en Microsoft Windows y Linux {#pdf-generator-api-available-on-microsoft-windows-and-linux}

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><p><strong>Microsoft Windows </strong></p> </td>
   <td><strong>Linux </strong></td>
  </tr>
  <tr>
   <td>createPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
  <tr>
   <td>htmlToPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
   <td>optimizePDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>exportPDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>PDF OCR (PDF en el que se pueden realizar búsquedas)</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
 </tbody>
</table>

#### createPDF {#createpdf}

La API createPDF convierte un archivo compatible en un documento PDF. Admite varios formatos de archivo, como Microsoft Word, Microsoft PowerPoint, Microsoft Excel y Microsoft Project. Además de estas aplicaciones, cualquier PDF genérico de terceros que genere un tipo de aplicación también puede conectarse a la API.

Para la conversión, solo son obligatorios unos pocos parámetros. Un documento de entrada es un parámetro obligatorio. Puede aplicar los permisos de seguridad, la configuración de salida del PDF y la información de metadatos más adelante al documento PDF de salida.

El servicio createPDF devuelve un archivo java.util.Map con resultados. Las claves del mapa son las siguientes:

* Documento convertido: contiene el documento PDF recién creado.
* LogDoc: contiene el archivo de registro.

El servicio createPDF presenta las siguientes excepciones:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintaxis:** `Map createPDF(Document inputDoc, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws InvalidParameterException, ConversionException, FileFormatNotSupportedException;`

#### Parámetros de entrada {#input-parameters-7}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Especifica un objeto de documento. El objeto document contiene el archivo de entrada. Cree un objeto com.adobe.aemfd.docmanager.Document sobre el documento de entrada. Es un parámetro obligatorio.</td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>Nombre del archivo de entrada junto con la extensión. Es un parámetro obligatorio.<br /> </td>
  </tr>
  <tr>
   <td>fileTypeSettings</td>
   <td>Es un parámetro opcional.</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>Salida PDF para el documento convertido. Solo puede aplicar las siguientes configuraciones:</p>
    <ul>
     <li>High_Quality_Print<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Smallest_File_Size</li>
    </ul> <p>Es un parámetro opcional.<br /> </p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>Configuración de seguridad del documento convertido. Puede aplicar la siguiente configuración:</p>
    <ul>
     <li>Sin seguridad</li>
     <li>Seguridad de las contraseñas<br /> </li>
     <li>Seguridad del certificado<br /> </li>
     <li>Servidor de directivas de Adobe</li>
    </ul> <p>Es un parámetro opcional.</p> </td>
  </tr>
  <tr>
   <td>settingsDoc</td>
   <td>El archivo contiene la configuración aplicada al generar el documento PDF (como el documento PDF de optimización para la visualización de la web) y la configuración aplicada después de crear el documento PDF (como la vista inicial y la seguridad). Es un parámetro opcional.<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>El archivo contiene información de metadatos aplicada al documento PDF generado. Este parámetro es opcional.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente código Java convierte un documento compatible en un documento PDF.

```java
@Reference GeneratePDFService generatePdfService;
File createPDF(File inputFile, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = generatePdfService.createPDF(inDoc, inputFilename, fileTypeSettings, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

#### exportPDF {#exportpdf}

Convierte un documento PDF en un archivo compatible. El método acepta un PDF como entrada y exporta el contenido de este en el formato de archivo especificado.

El servicio createPDF devuelve un archivo java.util.Map con resultados. Las claves del mapa son las siguientes:

* Documento convertido: contiene el documento de salida.

El servicio createPDF presenta las siguientes excepciones:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintaxis:**

```java
Map exportPDF(Document inputDoc, String inputFileName, String formatType, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parámetros de entrada {#input-parameters-8}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Especifica el documento que se va a convertir. </td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>Nombre del archivo junto con la extensión.<br /> </td>
  </tr>
  <tr>
   <td>formatType</td>
   <td>Formato del archivo de salida para la API exportPDF.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>El archivo contiene las configuraciones que se deben aplicar durante la generación del documento de salida. Generalmente, es un archivo XML.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java convierte un documento PDF en el tipo de archivo especificado.

```java
(tx == null)
OSGiUtils.getTransactionManager().begin();
String outputFolder="C:/Output"
Document convertedDoc = null;
Document inDoc = null;
Document settingsDoc = null;
try
{
 inDoc = new Document(inputFile);
 if(inputFileName == null || inputFileName.trim().equals("")) {
  throw new Exception("Input file name cannot be null");
 }
 if(inputFileExtension.lastIndexOf('.') == -1) {
  throw new Exception("Input file should have an extension");
 }
 if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
 settingsDoc = new Document(settingsFile);
 Map result = generatePdfService.exportPDF(inDoc, inputFileName, formatType, settingsDoc);
 convertedDoc = (Document)result.get("ConvertedDoc");
 OSGiUtils.getTransactionManager().commit();
 File outputFile = new File(outputFolder,"OutputFile");
 doc.copyToFile(outputFile);
 return outputFile;
}
catch (Exception e)
{
 if (OSGiUtils.getTransactionManager().getTransaction() != null)
 OSGiUtils.getTransactionManager().rollback();
 throw e;
}
finally {
 if (convertedDoc != null) {
  convertedDoc.dispose();
  convertedDoc = null;
 }
 if (inDoc != null) {
  inDoc.dispose();
  inDoc = null;
 }
 if (settingsDoc != null) {
  settingsDoc.dispose();
  settingsDoc = null;
 }
}
}
```

#### optimizePDF {#optimizepdf}

La API OptimizePDF optimiza los archivos PDF al reducir su tamaño. El resultado de esta conversión son archivos PDF que pueden ser más pequeños que sus versiones originales. Esta operación también convierte los documentos PDF a la versión PDF especificada en los parámetros de optimización. Devuelve el objeto OptimizePDFResult que contiene el PDF optimizado.

El servicio createPDF presenta las siguientes excepciones:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintaxis:**

```java
OptimizePDFResult optimizePDF(Document inputDoc, String fileTypeSettings, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parámetros de entrada {#input-parameters-9}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Especifica el documento de entrada. Es un parámetro obligatorio.</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>Es un parámetro opcional.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>El archivo contiene la configuración aplicada al generar el documento PDF (como el documento PDF de optimización para la visualización de la web) y la configuración aplicada después de crear el documento PDF (como la vista inicial y la seguridad). Es un parámetro opcional.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java optimiza el archivo PDF de entrada al reducir su tamaño.

```java
@Reference GeneratePDFService generatePdfService;
File optimizePDF(File inputFile, String fileTypeSettings, File settingsFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  OptimizePDFResult result = generatePdfService.optimizePDF(inDoc, fileTypeSettings, settingsDoc);
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

#### htmlToPdf2 {#htmltopdf}

Convierte una página HTML en un documento PDF. Acepta la dirección URL de la página HTML como entrada.

El servicio htmlToPdf2 devuelve un objeto HtmlToPdfResult. Puede obtener el PDF convertido mediante result.getConvertedDocument().

El servicio htmlToPdf2 genera las siguientes excepciones:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**Sintaxis:**

```java
HtmlToPdfResult htmlToPdf2(String inputUrl, String fileTypeSettingsName, String securitySettingsName, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parámetros de entrada {#input-parameters-10}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Especifica el documento de entrada. Es un parámetro obligatorio.</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>Es un parámetro opcional.<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>El archivo contiene la configuración aplicada al generar el documento PDF (como el documento PDF de optimización para la visualización de la web) y la configuración aplicada después de crear el documento PDF (como la vista inicial y la seguridad). Es un parámetro opcional.<br /> </td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java convierte una página HTML en un documento PDF.

```java
Reference GeneratePDFService generatePdfService;
File htmlToPdf(String inputUrl, String fileTypeSettingsName, String securitySettingsName, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  HtmlToPdfResult result = generatePdfService.htmlToPdf2(inputURL, fileTypeSettingsName, securitySettingsName, settingsDoc, xmpDoc);;
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

### DistillerService {#distillerservice}

El servicio Distiller convierte PostScript, PostScript encapsulado (EPS) y archivos de texto de impresora (PRN) en archivos PDF. El servicio Distiller se utiliza con frecuencia para convertir grandes volúmenes de documentos impresos en documentos electrónicos, como facturas e instrucciones. La conversión de documentos a PDF también permite a las empresas enviar a sus clientes una versión en papel y otra electrónica de un documento. Los formatos de archivo admitidos son .ps, .eps y .prn. El servicio admite la siguiente API:

El servicio createPDF devuelve un archivo java.util.Map con resultados. Las claves del mapa son las siguientes:

* ConvertedDoc : contiene el documento PDF recién creado.
* LogDoc : contiene el archivo de registro.

El servicio createPDF presenta las siguientes excepciones:

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

#### createPDF {#createpdf-1}

Convierte los formatos admitidos en documentos PDF. El método acepta archivos de formato .ps, .eps y .prn como entrada. Puede aplicar permisos de seguridad, configuración de salida e información de metadatos específicos al documento PDF de salida.

**Sintaxis:**

```java
Map createPDF(Document inputDoc, String inputFileName, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### Parámetros de entrada {#input-parameters-11}

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>Especifica el documento de entrada. Es un parámetro obligatorio.</td>
  </tr>
  <tr>
   <td>inputFileName</td>
   <td>Especifica el nombre completo del archivo de entrada junto con su extensión. Es un parámetro obligatorio.</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>Configuración de salida del PDF para el documento convertido. Solo puede aplicar las siguientes configuraciones:</p>
    <ul>
     <li>High_Quality_Print<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Smallest_File_Size</li>
    </ul> <p>Es un parámetro opcional.</p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>Configuración de seguridad del documento convertido. Puede aplicar la siguiente configuración:</p>
    <ul>
     <li>Sin seguridad</li>
     <li>Seguridad de las contraseñas<br /> </li>
     <li>Seguridad del certificado<br /> </li>
     <li>Servidor de directivas de Adobe</li>
    </ul> <p>Es un parámetro opcional.</p> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>El archivo contiene la configuración aplicada al generar el documento PDF (como el documento PDF de optimización para la visualización de la web) y la configuración aplicada después de crear el documento PDF (como la vista inicial y la seguridad). Es un parámetro opcional.<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>El archivo contiene información de metadatos del documento PDF generado. Es un parámetro opcional.</td>
  </tr>
 </tbody>
</table>

El siguiente ejemplo de código Java convierte los archivos de entrada del tipo PostScript (PS), PostScript encapsulado (EPS) y archivos de texto de impresora (PRN) a archivos PDF.

```java
@Reference DistillerService distillerService;
File createPDF(File inputFile, String inputFilename, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = distillerService.createPDF(inDoc, inputFilename, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

### Servicios de utilidad Doc {#doc-utility-services}

<!-- Document utilities with synchronous APIs help you <!--convert documents from PDF to XDP file format, Clone a PDF, Retrieve PDF properties (Redact), Multiclone PDF, Sanitise PDF for retrieving uninteneded hidden information, and tag PDF documents with lists and paragraphs. Details of each APIs are given below: -->

#### Etiquetado automático de documentos de PDF {#auto-tag-api}

La API de PDF de etiqueta automática mejora la accesibilidad de PDF al añadir etiquetas a los documentos, lo que garantiza el cumplimiento de los estándares de accesibilidad. Esto no solo mejora la experiencia del usuario, sino que también mantiene la precisión y la coherencia en todos los documentos. La API de etiqueta automática admite el etiquetado de los siguientes elementos:

* Bloques de texto (párrafos)
* Listas con viñetas en un operador
* Tabla de contenido (TOC)

![Documento de PDF etiquetado automáticamente](assets/auto-tag-api.png)

El siguiente ejemplo de código Java muestra cómo convertir un archivo PDF en un documento de PDF etiquetado.

**Sintaxis**: `Document tag(final Document inDoc)`

**Parámetros de entrada**

<table>
 <tbody>
  <tr>
   <th>Parámetros</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>Documento proporcionado como entrada para etiquetar. Es un parámetro obligatorio.<br /> </td>
  </tr>
 </tbody>
</table>

```java
@Reference
private PDFUtilityService pdfutilityService;
private static final File outputFolder = new File("C:/Output/");
void tag(File inputFile) throws Exception
{
    Document inDoc = null;
    try
    {
        inDoc = new Document(inputFile);
        if(inputFile.getName().trim().isEmpty()) {
            throw new Exception("Input file name cannot be null");
        }
        String inputFileExtension = "";
        int dotIndex = inputFile.getName().lastIndexOf('.');
        if (dotIndex > 0 && dotIndex < inputFile.getName().length() - 1) {
            inputFileExtension = inputFile.getName().substring(dotIndex + 1);
        }
        if(inputFileExtension.isEmpty()) {
            throw new Exception("Input file should have an extension");
        }
        Document taggedDoc;
        taggedDoc = pdfutilityService.tag(inDoc);
        File outputFile = new File(outputFolder,"Output.pdf");
        taggedDoc.copyToFile(outputFile);
        taggedDoc.close();
    } 
    finally {
        if (inDoc != null) {
            inDoc.dispose();
            inDoc = null;
        }
    }
}
```


