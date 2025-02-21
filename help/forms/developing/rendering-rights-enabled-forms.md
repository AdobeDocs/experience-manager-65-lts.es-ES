---
title: Procesar formularios con derechos activados
description: Utilice el servicio Forms para procesar formularios a los que se les han aplicado derechos de uso. Puede procesar formularios con derechos activados mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 4%

---

# Procesar formularios con derechos activados {#rendering-rights-enabled-forms}

El servicio Forms puede procesar formularios a los que se les han aplicado derechos de uso. Los derechos de uso pertenecen a una funcionalidad que está disponible de forma predeterminada en Acrobat pero no en Adobe Reader, como la capacidad de agregar comentarios a un formulario o rellenar los campos del formulario y guardarlo. Las Forms a las que se les han aplicado derechos de uso se denominan formularios con derechos activados. Un usuario que abre un formulario con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese formulario.

Para aplicar derechos de uso a un formulario, el servicio de extensiones de Acrobat Reader DC debe formar parte de la instalación de formularios AEM Forms. Además, debe tener una credencial válida que le permita aplicar derechos de uso a documentos de PDF. Es decir, debe configurar correctamente el servicio de extensiones de Acrobat Reader DC para poder procesar un formulario con los derechos activados. (Consulte [Acerca del servicio de extensiones de Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)).

>[!NOTE]
>
>Para procesar un formulario que contenga derechos de uso, debe utilizar un archivo XDP como entrada, no un archivo PDF. Si utiliza un archivo PDF como entrada, el formulario se seguirá representando; sin embargo, no será un formulario con derechos habilitados.

>[!NOTE]
>
>No se puede rellenar previamente un formulario con datos XML cuando se especifican los siguientes derechos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` o `enableDigitalSignatures`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario con derechos activados, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer opciones de tiempo de ejecución de derechos de uso.
1. Procesar un formulario con los derechos activados.
1. Escriba el formulario con los derechos activados en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Establecer opciones en tiempo de ejecución de derechos de uso**

Establezca opciones de tiempo de ejecución de derechos de uso para procesar un formulario con derechos activados. Especifique el alias de la credencial que se utiliza para aplicar derechos de uso a un formulario. Después de especificar el valor del alias, debe especificar cada derecho de uso que se aplicará al formulario.

**Procesar un formulario con derechos activados**

Para procesar un formulario con derechos activados, se utiliza la misma lógica de aplicación que para procesar un formulario sin derechos de uso. La única diferencia es que debe asegurarse de que las opciones de derechos de uso en tiempo de ejecución estén incluidas en la lógica de la aplicación.

>[!NOTE]
>
>Al procesar un formulario con derechos activados mediante la API del servicio web de Forms, no se pueden adjuntar archivos al formulario.

**Escriba el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario con derechos habilitados, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Una vez escrito en el explorador web del cliente, el formulario es visible para el usuario. Un usuario que ve el formulario con derechos activados en Adobe Reader puede realizar las operaciones que están habilitadas para ese formulario.

**Consulte también**

[Procesar formularios con derechos activados mediante la API de Java](#render-rights-enabled-forms-using-the-java-api)

[Procesar formularios con derechos activados mediante la API de servicio web](#render-rights-enabled-forms-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar formularios con derechos activados mediante la API de Java {#render-rights-enabled-forms-using-the-java-api}

Procesar un formulario con derechos activados mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establecer opciones de tiempo de ejecución de derechos de uso

   * Crear un objeto `ReaderExtensionSpec` mediante su constructor.
   * Especifique el alias de la credencial invocando el método `setReCredentialAlias` del objeto `ReaderExtensionSpec` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al objeto `ReaderExtensionSpec`. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Por ejemplo. para establecer el derecho de uso que permite a un usuario rellenar campos de formulario y guardar el formulario, invoque el método `setReFillIn` del objeto `ReaderExtensionSpec` y pase `true`.

   >[!NOTE]
   >
   >No es necesario invocar el método `setReCredentialPassword` del objeto `ReaderExtensionSpec`. El servicio Forms no utiliza este método.

1. Procesar un formulario con derechos activados

   Invoque el método `renderPDFFormWithUsageRights` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `ReaderExtensionSpec` que almacena opciones de derechos de uso en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.

   El método `renderPDFFormWithUsageRights` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Procesamiento de un formulario con derechos activados mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar formularios con derechos activados mediante la API de servicio web {#render-rights-enabled-forms-using-the-web-service-api}

Procesar un formulario con derechos activados mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución de derechos de uso

   * Crear un objeto `ReaderExtensionSpec` mediante su constructor.
   * Especifique el alias de la credencial invocando el método `setReCredentialAlias` del objeto `ReaderExtensionSpec` y especifique un valor de cadena que represente el valor del alias.
   * Establezca cada derecho de uso invocando el método correspondiente que pertenece al objeto `ReaderExtensionSpec`. Sin embargo, solo puede establecer un derecho de uso si la credencial a la que hace referencia le permite hacerlo. Es decir, no puede establecer un derecho de uso si la credencial no le permite establecerlo. Para establecer el derecho de uso que permite a un usuario rellenar campos de formulario y guardar el formulario, invoque el método `setReFillIn` del objeto `ReaderExtensionSpec` y pase `true`.

1. Procesar un formulario con derechos activados

   Invoque el método `renderPDFFormWithUsageRights` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos con el formulario, debe pasar un objeto `BLOB` basado en un origen de datos XML vacío. No puede pasar un objeto `BLOB` que sea nulo; de lo contrario, se generará una excepción.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `ReaderExtensionSpec` que almacena opciones de derechos de uso en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.

   El método `renderPDFFormWithUsageRights` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Procesar formularios con derechos activados](#rendering-rights-enabled-forms)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
