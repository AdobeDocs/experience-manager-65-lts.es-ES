---
title: Comprimir y descomprimir archivos con un AEM Forms en una DSC personalizada JEE
description: Aprenda a comprimir y descomprimir archivos mediante AEM Forms en una DSC personalizada JEE
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---

# Comprimir y descomprimir archivos mediante AEM Forms en una DSC personalizada JEE {#compressing-decompressing-files}

## Conocimientos previos requeridos {#prerequisites}

Experiencia con AEM Forms en la administración de procesos JEE, la programación básica de Java™ y la creación de componentes personalizados.

**Otros productos adicionales necesarios**

Editor Java™ como [Eclipse](https://www.eclipse.org/) o [Netbeans IDE](https://netbeans.apache.org/)

## Nivel de usuario {#user-level}

Intermedio

AEM Forms en JEE permite a los desarrolladores crear ASC (contenedor de servicios de Acrobat) personalizado para crear funciones enriquecidas listas para usar. La creación de estos componentes se puede conectar al entorno de tiempo de ejecución de AEM Forms en JEE y cumple el propósito deseado. Este artículo explica cómo crear un servicio ZIP personalizado que se puede utilizar para comprimir una lista de archivos en un archivo .zip y descomprimir un .zip en una lista de documentos.

## Crear un componente ASC personalizado {#create-custom-dsc-component}

Cree un componente ASC personalizado con dos operaciones de servicio para poder comprimir y descomprimir una lista de documentos. Este componente utiliza el paquete java.util.zip para la compresión y descompresión.

Para crear un componente ASC personalizado:

1. Añada el archivo adobe-livecycle-client.jar a la biblioteca
1. Añadir los iconos necesarios
1. Crear una clase pública
1. Cree dos métodos públicos denominados UnzipDocument y ZipDocuments
1. Escriba la lógica para Compresión y Descompresión

El código se puede encontrar aquí:

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## Crear un archivo Component.XML {#create-component-xml-file}

Se debe crear un archivo component.xml dentro de la carpeta raíz del paquete que definió las operaciones del servicio y sus parámetros.

El archivo component.xml se muestra aquí:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="https://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## Empaquetado e implementación del componente {#packaging-deploying-component}

1. Compile el proyecto Java™ y cree un archivo .JAR.
1. Implemente el componente (archivo .JAR) en el tiempo de ejecución de AEM Forms en JEE a través de Workbench.
1. Inicie el servicio desde Workbench (consulte la figura siguiente).

![Diseño de procesos](assets/process-design.jpg)

## Uso del servicio ZIP en flujos de trabajo {#using-zip-service-in-workflows}

La operación UnzipDocument del servicio personalizado ahora puede aceptar una variable de documento como entrada y devolver una lista de variables de documento como salida.

![Descomprimir documento](assets/unzip-doc.jpg)

Del mismo modo, la operación ZipDocuments del componente personalizado puede aceptar una lista de documentos como entrada, comprimirlos como archivo zip y devolver el documento comprimido.

![Documento Zip](assets/zip-doc.jpg)

La siguiente orquestación del flujo de trabajo muestra cómo descomprimir el archivo ZIP, comprimirlo de nuevo en otro archivo ZIP y devolver la salida (consulte la figura siguiente).

![Descomprimir flujo de trabajo ZIP](assets/unzip-zip-process.jpg)

## Algunos casos de uso empresariales {#business-use-cases}

Puede utilizar este servicio ZIP para los siguientes casos de uso:

* Busque todos los archivos de una carpeta determinada y devuélvalos como un documento comprimido.

* Proporcione un archivo ZIP que contenga varios documentos de PDF que se puedan leer y ampliar después de descomprimirlos. Esto requiere AEM Forms en el módulo de extensiones de Reader JEE.

* Suministre un archivo ZIP que contenga un tipo heterogéneo de documento que se pueda descomprimir y convertir como documento de PDF mediante el servicio Generate PDF.

* Política de proteger una lista de documentos y devolver como archivo ZIP.

* Permite a los usuarios descargar todos los archivos adjuntos de una instancia de proceso como un solo archivo ZIP.
