---
title: Procesar formularios HTML mediante archivos CSS personalizados
description: Utilice el servicio Forms para hacer referencia a archivos CSS personalizados y procesar formularios HTML en respuesta a una solicitud HTTP de un explorador web. Puede procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: b70404ee-21dc-4c0b-a66f-c37a6f29f98e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---

# Procesar formularios HTML mediante archivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms procesa los formularios HTML en respuesta a una solicitud HTTP de un explorador web. Al procesar un formulario HTML, el servicio Forms puede hacer referencia a un archivo CSS personalizado. Puede crear un archivo CSS personalizado para satisfacer los requisitos empresariales y hacer referencia a ese archivo CSS al utilizar el servicio Forms para procesar formularios HTML.

El servicio Forms analiza de forma silenciosa el archivo CSS personalizado. Es decir, el servicio Forms no informa de los errores que se pueden encontrar si el archivo CSS personalizado no cumple con los estándares CSS. En este caso, el servicio Forms ignora el estilo y continúa con los estilos restantes del archivo CSS.

La siguiente lista especifica los estilos compatibles con un archivo CSS personalizado:

* **Pares de estilo selector de nivel de clase**: si están presentes en un archivo CSS personalizado, se utilizan selectores utilizados en el formulario de HTML como estilos de clase. Se omiten los estilos de clase no utilizados.
* **Pares de estilo selector de nivel de identificador**: todos los estilos de identificador se utilizan si están en el formulario de HTML.
* **Pares de estilo selector de nivel de elemento**: todos los estilos de elemento se utilizan si están en el formulario de HTML.
* **Prioridad de estilo**: la prioridad de estilo (como importante) es compatible y se puede usar en un archivo CSS personalizado.
* **Tipo de medio**: uno o más pares de estilo selector se pueden ajustar en @media estilo para definir el tipo de medio. El servicio Forms no comprueba si se admite el tipo de medio especificado. El tipo de medios especificado en el archivo CSS personalizado se combina en el formulario de HTML.

Puede recuperar un archivo CSS de ejemplo utilizando la aplicación FormsIVS. Cargue el formulario, selecciónelo en la página Diseño del formulario de prueba y haga clic en Generar CSS. No es necesario que establezca el tipo de transformación de HTML antes de hacer clic en el botón. A continuación, seleccione guardar. Puede editar este archivo CSS para satisfacer sus necesidades comerciales.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice un archivo CSS personalizado, es importante que tenga una comprensión sólida del procesamiento de formularios de HTML. (Consulte [Procesar Forms como HTML](/help/forms/developing/rendering-forms-html.md)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que utilice un archivo CSS, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Haga referencia al archivo CSS.
1. Procesar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API Java de Forms**

Para poder realizar mediante programación una operación admitida por el servicio Forms, debe crear un objeto de cliente de Forms.

**Hacer referencia al archivo CSS**

Para procesar un formulario HTML que utilice un archivo CSS personalizado, asegúrese de hacer referencia a un archivo CSS existente.

**Procesar un formulario de HTML**

Para procesar un formulario de HTML, especifique un diseño de formulario que se haya creado en Designer y guardado como archivo XDP. Seleccione un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación de HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario de HTML también requiere valores, como los valores URI necesarios para procesar otros tipos de formulario.

**Escriba el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que el formulario de HTML sea visible para el usuario.

**Consulte también**

[Procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Procesar un formulario de HTML que utilice un archivo CSS mediante la API de Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Procesar un formulario de HTML que utilice un archivo CSS personalizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia al archivo CSS

   * Crear un objeto `HTMLRenderSpec` mediante su constructor.
   * Para procesar el formulario de HTML que usa un archivo CSS personalizado, invoque el método `setCustomCSSURI` del objeto `HTMLRenderSpec` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Procesar un formulario de HTML

   Invoque el método `(Deprecated) (Deprecated) renderHTMLForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valor de enumeración `TransformTo` que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con Dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objeto `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `(Deprecated) renderHTMLForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.h\ttp.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Procesar formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Inicio rápido (modo SOAP): procesar un formulario de HTML que utiliza un archivo CSS mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Procesar un formulario de HTML que utilice un archivo CSS mediante la API de servicio web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Procesar un formulario de HTML que utilice un archivo CSS personalizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Creación de un objeto de API de Java de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Hacer referencia al archivo CSS

   * Crear un objeto `HTMLRenderSpec` mediante su constructor.
   * Para procesar el formulario de HTML que usa un archivo CSS personalizado, invoque el método `setCustomCSSURI` del objeto `HTMLRenderSpec` y pase un valor de cadena que especifique la ubicación y el nombre del archivo CSS.

1. Procesar un formulario de HTML

   Invoque el método `(Deprecated) renderHTMLForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valor de enumeración `TransformTo` que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con Dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Puede pasar una cadena vacía si no desea establecer este valor.
   * Un objeto `URLSpec` que almacena los valores de URI necesarios para procesar un formulario de HTML.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método `(Deprecated) renderHTMLForm`. Este valor de parámetro almacena el formulario procesado.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método `(Deprecated) renderHTMLForm`. Este parámetro almacena los datos XML de salida.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el número de páginas del formulario.
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el valor de configuración regional.
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método `(Deprecated) renderHTMLForm`. Este argumento almacena el valor de procesamiento de HTML que se utiliza.
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `(Deprecated) renderHTMLForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `value` del objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Procesar formularios HTML mediante archivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
