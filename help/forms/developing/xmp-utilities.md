---
title: Trabajar con utilidades XMP
description: Utilice las API de servicios web y Java de utilidades de XMP para importar mediante programación metadatos de XMP en un documento de PDF y recuperar y guardar metadatos de XMP de un documento de PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 6deed56a-2e87-4444-8fb5-1d06b0792a5e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# Trabajar con utilidades XMP {#working-with-xmp-utilities}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca del servicio de utilidades de XMP**

Los documentos de PDF contienen metadatos, que son información sobre el documento tal como se distingue del contenido del mismo, como texto y gráficos. Adobe Extensible Metadata Platform (XMP) es un estándar para administrar metadatos de documentos.

El servicio Utilidades de XMP puede recuperar y guardar metadatos de XMP de documentos de PDF e importar metadatos de XMP en documentos de PDF.

Puede realizar estas tareas mediante el servicio Utilidades de XMP:

* Importar metadatos en documentos de PDF. (Consulte [Importación de metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)).
* Exportar metadatos de documentos de PDF. (Consulte [Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de XMP, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importar metadatos en documentos de PDF {#importing-metadata-into-pdf-documents}

Puede utilizar las API de Java y de servicio web de Utilidades de XMP para importar mediante programación metadatos de XMP en un documento de PDF. Los metadatos proporcionan información sobre un documento de PDF, como el autor del documento y las palabras clave relacionadas con él. Los metadatos pueden encontrarse en el cuadro de diálogo Propiedades del documento, como se muestra en la siguiente ilustración.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Para importar metadatos mediante programación en un documento de PDF, puede utilizar un documento XML existente que especifique los valores de los metadatos o puede utilizar un objeto de tipo `XMPUtilityMetadata`. (Consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>En esta sección se explica cómo utilizar un documento XML para importar metadatos en un documento de PDF.

El siguiente código XML contiene valores de metadatos que corresponden a la ilustración anterior. Por ejemplo, observe los elementos en negrita, que especifican palabras clave.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de XMP, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para importar metadatos de XMP en un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de XMPUtilityService.
1. Invoque la operación de importación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de XMPUtilityService**

Para poder realizar mediante programación una operación de Utilidades de XMP, debe crear un cliente de XMPUtilityService. Con la API de Java, esto se logra creando un objeto `XMPUtilityServiceClient`. Con la API del servicio web, esto se logra mediante el uso de un objeto `XMPUtilityServiceService`.

**Invocar la operación de importación de metadatos de XMP**

Después de crear el cliente de servicios, puede invocar una de las operaciones de importación de metadatos de XMP para importar los metadatos de XMP en el documento de PDF especificado.

**Consulte también**

[Importar metadatos de XMP mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar metadatos de XMP mediante la API de Java {#import-xmp-metadata-using-the-java-api}

Importe metadatos de XMP mediante la API de utilidades de XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que permiten invocar mediante programación el servicio Utilidades de XMP.

1. Crear un cliente de XMPUtilityService

   Cree un objeto `XMPUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque el método `importMetadata` del objeto `XMPUtilityServiceClient` o su método `importXMP`.

   Si usa el método `importMetadata`, pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que representa el archivo PDF.
   * Un objeto `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si usa el método `importXMP`, pase los siguientes valores:

   * Objeto `com.adobe.idp.Document` que representa el archivo PDF.
   * Objeto `com.adobe.idp.Document` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un objeto `com.adobe.idp.Document` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importar metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importación de metadatos de XMP mediante la API de servicio web {#importing-xmp-metadata-using-the-web-service-api}

Para importar mediante programación metadatos de XMP mediante la API del servicio web de Utilidades de XMP, realice las siguientes tareas:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de XMP. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. (Vea [Crear un ensamblado de cliente .NET que utiliza codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Crear un cliente de XMPUtilityService

   Cree un objeto `XMPUtilityServiceService` con el constructor de clase de proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para modificar los metadatos de XMP, invoque el método `importMetadata` del objeto `XMPUtilityServiceService` o su método `importXMP`.

   Si usa el método `importMetadata`, pase los siguientes valores:

   * Objeto `BLOB` que representa el archivo PDF.
   * Un objeto `XMPUtilityMetadata` que contiene los metadatos que se van a importar.

   Si usa el método `importXMP`, pase los siguientes valores:

   * Objeto `BLOB` que representa el archivo PDF.
   * Objeto `BLOB` que representa un archivo XML que contiene los metadatos que se van a importar.

   En cualquier caso, el valor devuelto es un objeto `BLOB` que representa el archivo PDF con los metadatos recién importados. A continuación, puede guardar este objeto en el disco.

**Consulte también**

[Importar metadatos en documentos de PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Exportación de metadatos desde documentos de PDF {#exporting-metadata-from-pdf-documents}

Puede utilizar las API de Java y de servicio web de Utilidades de XMP para recuperar y guardar mediante programación metadatos de XMP de un documento de PDF.

>[!NOTE]
>
>Para obtener más información acerca del servicio Utilidades de XMP, vea [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para exportar metadatos de XMP desde un documento de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente de XMPUtilityService.
1. Invoque la operación de exportación de metadatos de XMP.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de XMPUtilityService**

Para poder realizar mediante programación una operación de Utilidades de XMP, debe crear un cliente de XMPUtilityService. Con la API de Java, esto se logra creando un objeto `XMPUtilityServiceClient`. Con la API del servicio web, esto se logra mediante un objeto `XMPUtilityServiceService`.

**Invocar la operación de exportación de metadatos de XMP**

Después de crear el cliente de servicios, puede invocar una de las operaciones de exportación de metadatos de XMP, que puede utilizarse para inspeccionar los metadatos de XMP o guardarlos en el disco.

**Consulte también**

[Importar metadatos de XMP mediante la API de Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importación de metadatos de XMP mediante la API de servicio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar metadatos de XMP mediante la API de Java {#export-xmp-metadata-using-the-java-api}

Exporte los metadatos de XMP mediante la API de utilidades de XMP (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-pdfutility-client.jar, en la ruta de clase del proyecto Java.

   >[!NOTE]
   >
   >El archivo adobe-pdfutility-client.jar contiene clases que permiten invocar mediante programación el servicio de utilidad de XMP.

1. Crear un cliente de XMPUtilityService

   Cree un objeto `XMPUtilityServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque el método `exportMetadata` del objeto `XMPUtilityServiceClient` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque el método `exportXMP` del objeto `XMPUtilityServiceClient` y pase un objeto `com.adobe.idp.Document` que represente el archivo PDF. El método devuelve un objeto `com.adobe.idp.Document` que contiene los metadatos recuperados, que posteriormente se pueden guardar en el disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportación de metadatos de XMP mediante la API de servicio web {#export-xmp-metadata-using-the-web-service-api}

Exportar metadatos de XMP mediante la API de utilidades de XMP (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el archivo WSDL del servicio Utilidades de XMP.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un cliente de XMPUtilityService

   Cree un objeto `XMPUtilityServiceService` con el constructor de clase de proxy.

1. Invocar la operación de importación de metadatos de XMP

   Para inspeccionar los metadatos de XMP, invoque el método `exportMetadata` del objeto `XMPUtilityServiceClient` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `XMPUtilityMetadata` que contiene los metadatos recuperados.

   Para recuperar y guardar los metadatos de XMP, invoque el método `exportXMP` del objeto `XMPUtilityServiceClient` y pase un objeto `BLOB` que represente el archivo PDF. El método devuelve un objeto `BLOB` que contiene los metadatos recuperados, que posteriormente se pueden guardar en el disco como archivo XML.

**Consulte también**

[Exportación de metadatos desde documentos de PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
