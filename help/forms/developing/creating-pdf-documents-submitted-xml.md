---
title: Crear documentos PDF con datos XML enviados
description: Utilice el servicio Forms para recuperar los datos de formulario introducidos por el usuario en un formulario interactivo. Pase los datos del formulario a otra operación del servicio AEM Forms y cree un documento de PDF con los datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Services, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 66736a58-b2ef-404e-b94c-9bc407828359
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 1%

---

# Crear documentos PDF con datos XML enviados {#creating-pdf-documents-with-submittedxml-data}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Crear documentos PDF con datos XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Las aplicaciones basadas en Web que permiten a los usuarios rellenar formularios interactivos requieren que los datos se devuelvan al servidor. Con el servicio Forms, puede recuperar los datos de formulario introducidos por el usuario en un formulario interactivo. A continuación, puede pasar los datos del formulario a otra operación del servicio AEM Forms y crear un documento de PDF utilizando los datos.

>[!NOTE]
>
>Antes de leer este contenido, se recomienda tener una comprensión sólida de la gestión de los formularios enviados. Los conceptos como la relación entre un diseño de formulario y los datos XML enviados se tratan en Gestión de Forms enviados.

Tenga en cuenta el siguiente flujo de trabajo que implica tres servicios de AEM Forms:

* Un usuario envía datos XML al servicio Forms desde una aplicación basada en web.
* El servicio Forms se utiliza para procesar el formulario enviado y extraer los campos del formulario. Se pueden procesar los datos del formulario. Por ejemplo, los datos se pueden enviar a una base de datos empresarial.
* Los datos de formulario se envían al servicio Output para crear un documento de PDF no interactivo.
* El documento no interactivo de PDF se almacena en Content Services (obsoleto).

El diagrama siguiente proporciona una representación visual de este flujo de trabajo.

![cd_cd_finsrv_Architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Una vez que el usuario envía el formulario desde el explorador web del cliente, el documento no interactivo de PDF se almacena en Content Services (obsoleto). La siguiente ilustración muestra un documento de PDF almacenado en Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Resumen de los pasos {#summary-of-steps}

Para crear un documento no interactivo de PDF con datos XML enviados y almacenarlos en el documento de PDF en Content Services (obsoleto), realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Crear objetos de Forms, Output y Document Management.
1. Recupere datos de formulario mediante el servicio de Forms.
1. Cree un documento de PDF no interactivo con el servicio Output.
1. Almacene el formulario de PDF en Content Services (obsoleto) mediante el servicio Document Management.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear objetos de Forms, Output y Document Management**

Para poder realizar mediante programación una operación de API de servicio de Forms, cree un objeto de API de cliente de Forms. Del mismo modo, dado que este flujo de trabajo invoca los servicios Output y Document Management, cree un objeto de API de cliente de salida y un objeto de API de cliente de Document Management.

**Recuperar datos de formulario mediante el servicio Forms**

Recupere los datos de formulario enviados al servicio Forms. Puede procesar los datos enviados para satisfacer sus necesidades comerciales. Por ejemplo, puede almacenar datos de formulario en una base de datos empresarial. Sin embargo, para crear un documento de PDF no interactivo, los datos del formulario se pasan al servicio Output.

**Crear un documento no interactivo de PDF mediante el servicio Output.**

Utilice el servicio Output para crear un documento de PDF no interactivo basado en un diseño de formulario y datos de formulario XML. En el flujo de trabajo, los datos del formulario se recuperan del servicio de Forms.

**Almacenar el formulario de PDF en Content Services (obsoleto) mediante el servicio Document Management**

Utilice la API del servicio Administración de documentos para almacenar un documento de PDF en Content Services (obsoleto).

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Crear un documento de PDF con datos XML enviados mediante la API de Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Cree un documento de PDF con datos XML enviados mediante la API de Forms, Output y Document Management (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, adobe-output-client.jar y adobe-contentservices-client.jar en la ruta de clase de su proyecto Java.

1. Creación de objetos de Forms, Output y Document Management

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `OutputClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `DocumentManagementServiceClientImpl` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperación de datos de formulario mediante el servicio de Forms

   * Invoque el método `processFormSubmission` del objeto `FormsServiceClient` y pase los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a administrar especificando uno o varios valores para la variable de entorno `CONTENT_TYPE`. Por ejemplo, para administrar datos XML, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=text/xml`.
      * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objeto `RenderOptionsSpec` que almacena opciones en tiempo de ejecución.

     El método `processFormSubmission` devuelve un objeto `FormsResult` que contiene los resultados del envío del formulario.

   * Determine si el servicio Forms terminó de procesar los datos del formulario invocando el método `getAction` del objeto `FormsResult`. Si este método devuelve el valor `0`, los datos están listos para procesarse.
   * Recupere datos de formulario creando un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`. (Este objeto contiene datos de formulario que se pueden enviar al servicio Output).
   * Cree un objeto `java.io.InputStream` invocando el constructor `java.io.DataInputStream` y pasando el objeto `com.adobe.idp.Document`.
   * Cree un objeto `org.w3c.dom.DocumentBuilderFactory` llamando al método `newInstance` del objeto `org.w3c.dom.DocumentBuilderFactory` estático.
   * Cree un objeto `org.w3c.dom.DocumentBuilder` invocando el método `newDocumentBuilder` del objeto `org.w3c.dom.DocumentBuilderFactory`.
   * Cree un objeto `org.w3c.dom.Document` invocando el método `parse` del objeto `org.w3c.dom.DocumentBuilder` y pasando el objeto `java.io.InputStream`.
   * Recupere el valor de cada nodo dentro del documento XML. Una manera de realizar esta tarea es crear un método personalizado que acepte dos parámetros: el objeto `org.w3c.dom.Document` y el nombre del nodo cuyo valor desee recuperar. Este método devuelve un valor de cadena que representa el valor del nodo. En el ejemplo de código que sigue este proceso, este método personalizado se llama `getNodeText`. Se muestra el cuerpo de este método.

1. Cree un documento de PDF no interactivo con el servicio Output.

   Cree un documento de PDF invocando el método `generatePDFOutput` del objeto `OutputClient` y pasando los siguientes valores:

   * Un valor de enumeración `TransformationFormat`. Para generar un documento de PDF, especifique `TransformationFormat.PDF`.
   * Un valor de cadena que especifica el nombre del diseño de formulario. Asegúrese de que el diseño de formulario sea compatible con los datos de formulario recuperados del servicio de Forms.
   * Valor de cadena que especifica la raíz de contenido donde se encuentra el diseño de formulario.
   * Un objeto `PDFOutputOptionsSpec` que contiene opciones en tiempo de ejecución de PDF.
   * Objeto `RenderOptionsSpec` que contiene opciones de procesamiento en tiempo de ejecución.
   * El objeto `com.adobe.idp.Document` que contiene el origen de datos XML que contiene los datos que se van a combinar con el diseño de formulario. Asegúrese de que el método `getOutputContent` del objeto `FormsResult` devolvió este objeto.
   * El método `generatePDFOutput` devuelve un objeto `OutputResult` que contiene los resultados de la operación.
   * Recupere el documento no interactivo de PDF invocando el método `getGeneratedDoc` del objeto `OutputResult`. Este método devuelve una instancia `com.adobe.idp.Document` que representa el documento no interactivo de PDF.

1. Almacenar el formulario de PDF en Content Services (obsoleto) mediante el servicio Document Management

   Agregue el contenido invocando el método `storeContent` del objeto `DocumentManagementServiceClientImpl` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Valor de cadena que especifica la ruta de acceso completa del espacio donde se agrega el contenido (por ejemplo, `/Company Home/Test Directory`). Este valor es un parámetro obligatorio.
   * Nombre del nodo que representa el nuevo contenido (por ejemplo, `MortgageForm.pdf`). Este valor es un parámetro obligatorio.
   * Valor de cadena que especifica el tipo de nodo. Para agregar contenido nuevo, como un archivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Este valor es un parámetro obligatorio.
   * Un objeto `com.adobe.idp.Document` que representa el contenido. Este valor es un parámetro obligatorio.
   * Valor de cadena que especifica el valor de codificación (por ejemplo, `UTF-8`). Este valor es un parámetro obligatorio.
   * Valor de enumeración `UpdateVersionType` que especifica cómo controlar la información de versión (por ejemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar la versión del contenido. ) Este valor es un parámetro obligatorio.
   * Una instancia de `java.util.List` que especifica aspectos relacionados con el contenido. Este valor es un parámetro opcional y puede especificar `null`.
   * Objeto `java.util.Map` que almacena atributos de contenido.

   El método `storeContent` devuelve un objeto `CRCResult` que describe el contenido. Con un objeto `CRCResult`, por ejemplo, puede obtener el valor de identificador único del contenido. Para realizar esta tarea, invoque el método `getNodeUuid` del objeto `CRCResult`.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
