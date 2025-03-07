---
title: Pasar documentos a FormsService
description: Pase un objeto com.adobe.idp.Document que contenga el diseño de formulario al servicio Forms. El servicio Forms procesa el diseño de formulario en el objeto com.adobe.idp.Document.
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
exl-id: 78d72100-b67b-48ac-9479-706fdccbd3cd
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Pasar documentos al servicio de Forms {#passing-documents-to-the-formsservice}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio AEM Forms procesa PDF forms interactivo en los dispositivos cliente, normalmente en los navegadores web, para recopilar información de los usuarios. Un formulario interactivo de PDF se basa en un diseño de formulario que normalmente se guarda como archivo XDP y se crea en Designer. A partir de AEM Forms, puede pasar un objeto `com.adobe.idp.Document` que contenga el diseño de formulario al servicio Forms. A continuación, el servicio Forms procesa el diseño de formulario en el objeto `com.adobe.idp.Document`.

Una ventaja de pasar un objeto `com.adobe.idp.Document` al servicio Forms es que otras operaciones del servicio devuelven una instancia `com.adobe.idp.Document`. Es decir, puede obtener una instancia de `com.adobe.idp.Document` de otra operación de servicio y procesarla. Por ejemplo, supongamos que un archivo XDP se almacena en un nodo de Content Services (obsoleto) denominado `/Company Home/Form Designs`, como se muestra en la siguiente ilustración.

Puede recuperar mediante programación Loan.xdp de Content Services (obsoleto) (obsoleto) y pasar el archivo XDP al servicio de Forms dentro de un objeto `com.adobe.idp.Document`.

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para pasar un documento obtenido de Content Services (obsoleto) (obsoleto) al servicio Forms, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms y de Administración de documentos.
1. Recupere el diseño de formulario de Content Services (obsoleto).
1. Procese el formulario interactivo de PDF.
1. Realice una acción con el flujo de datos del formulario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un Forms y un objeto de API de cliente de administración de documentos**

Para poder realizar mediante programación una operación de API de servicio de Forms, cree un objeto de API de cliente de Forms. Además, como este flujo de trabajo recupera un archivo XDP de los servicios de contenido (obsoleto), cree un objeto de API de administración de documentos.

**Recuperar el diseño de formulario de los servicios de contenido (obsoleto)**

Recupere el archivo XDP de los servicios de contenido (obsoleto) mediante Java o la API de servicio web. El archivo XDP se devuelve en una instancia `com.adobe.idp.Document` (o en una instancia `BLOB` si utiliza servicios web). A continuación, puede pasar la instancia `com.adobe.idp.Document` al servicio Forms.

**Procesar un formulario interactivo de PDF**

Para procesar un formulario interactivo, pase la instancia `com.adobe.idp.Document` devuelta por Content Services (obsoleta) al servicio Forms.

>[!NOTE]
>
>Puede pasar un(a) `com.adobe.idp.Document` que contenga el diseño de formulario al servicio Forms. Dos nuevos métodos denominados `renderPDFForm2` y `renderHTMLForm2` aceptan un objeto `com.adobe.idp.Document` que contiene un diseño de formulario.

**Realizar una acción con el flujo de datos del formulario**

Según el tipo de aplicación cliente, puede escribir el formulario en un explorador web de cliente o guardarlo como archivo PDF. Una aplicación basada en web suele escribir el formulario en el explorador web. Sin embargo, una aplicación de escritorio suele guardar el formulario como un archivo PDF.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Pasar documentos al servicio de Forms mediante la API de Java {#pass-documents-to-the-forms-service-using-the-java-api}

Pase un documento obtenido de Content Services (obsoleto) mediante el servicio Forms y la API de Content Services (obsoleto) (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar y adobe-contentservices-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms y Administración de documentos

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.
   * Cree un objeto `DocumentManagementServiceClientImpl` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Invoque el método `retrieveContent` del objeto `DocumentManagementServiceClientImpl` y pase los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Valor de cadena que especifica la ruta de acceso completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.

   El método `retrieveContent` devuelve un objeto `CRCResult` que contiene el archivo XDP. Obtenga una instancia `com.adobe.idp.Document` invocando el método `getDocument` del objeto `CRCResult`.

1. Procesar un formulario interactivo de PDF

   Invoque el método `renderPDFForm2` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un objeto `com.adobe.idp.Document` que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Objeto `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream`. Pase la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Pasar documentos al servicio Forms mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Pase documentos al servicio de Forms mediante la API de servicio web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Pase un documento obtenido de Content Services (obsoleto) mediante el servicio Forms y la API de Content Services (obsoleto) (servicio web):

1. Incluir archivos de proyecto

   Cree un proyecto de Microsoft .NET que utilice MTOM. Dado que esta aplicación cliente invoca dos servicios de AEM Forms, cree dos referencias de servicio. Utilice la siguiente definición WSDL para la referencia de servicio asociada al servicio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilice la siguiente definición de WSDL para la referencia de servicio asociada al servicio de administración de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Dado que el tipo de datos `BLOB` es común a ambas referencias de servicio, califique completamente el tipo de datos `BLOB` al utilizarlo. En el inicio rápido del servicio web correspondiente, todas las instancias de `BLOB` están completamente calificadas.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Crear un objeto de API de cliente de Forms y Administración de documentos

   * Cree un objeto `FormsServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `FormsServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio).
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `FormsServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estos pasos para el cliente de servicio `DocumentManagementServiceClient`.

1. Recuperar el diseño de formulario de Content Services (obsoleto)

   Recupere contenido invocando el método `retrieveContent` del objeto `DocumentManagementServiceClient` y pasando los siguientes valores:

   * Un valor de cadena que especifica el almacén donde se agrega el contenido. El almacén predeterminado es `SpacesStore`. Este valor es un parámetro obligatorio.
   * Valor de cadena que especifica la ruta de acceso completa del contenido que se va a recuperar (por ejemplo, `/Company Home/Form Designs/Loan.xdp`). Este valor es un parámetro obligatorio.
   * Un valor de cadena que especifica la versión. Este valor es un parámetro opcional y puede pasar una cadena vacía. En este caso, se recupera la versión más reciente.
   * Un parámetro de salida de cadena que almacena el valor del vínculo de exploración.
   * Parámetro de salida `BLOB` que almacena el contenido. Puede utilizar este parámetro de salida para recuperar el contenido.
   * Parámetro de salida `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` que almacena atributos de contenido.
   * Un parámetro de salida `CRCResult`. En lugar de usar este objeto, puede usar el parámetro de salida `BLOB` para obtener el contenido.

1. Procesar un formulario interactivo de PDF

   Invoque el método `renderPDFForm2` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un objeto `BLOB` que contiene el diseño de formulario recuperado de Content Services (obsoleto).
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `BLOB` vacío.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. Este valor es un parámetro opcional y puede especificar `null` si no desea especificar opciones en tiempo de ejecución.
   * Objeto `URLSpec` que contiene valores de URI. Este valor es un parámetro opcional y puede especificar `null`.
   * Objeto `Map` que almacena datos adjuntos de archivos. Este valor es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un parámetro de salida largo que se utiliza para almacenar el recuento de páginas.
   * Un parámetro de salida de cadena que se utiliza para almacenar el valor de configuración regional.
   * Un parámetro de salida `FormsResult` que se usa para almacenar el formulario PDF interactivo `.`

   El método `renderPDFForm2` devuelve un objeto `FormsResult` que contiene el formulario PDF interactivo.

1. Realizar una acción con el flujo de datos del formulario

   * Cree un objeto `BLOB` que contenga datos de formulario obteniendo el valor del campo `outputContent` del objeto `FormsResult`.
   * Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento interactivo de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `BLOB` recuperado del objeto `FormsResult`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
