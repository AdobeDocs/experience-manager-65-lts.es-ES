---
title: Optimizar el rendimiento del servicio de Forms
description: Establezca opciones en tiempo de ejecución al procesar un formulario y almacenar archivos XDP en el repositorio para optimizar el rendimiento del servicio de Forms.
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
source-wordcount: '1424'
ht-degree: 1%

---

# Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-theforms-service}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Optimización del rendimiento del servicio de Forms {#optimizing-the-performance-of-the-forms-service}

Al procesar un formulario, puede establecer opciones en tiempo de ejecución que optimicen el rendimiento del servicio de Forms. Otra tarea que puede realizar para mejorar el rendimiento del servicio Forms es almacenar los archivos XDP en el repositorio. Sin embargo, esta sección no describe cómo realizar esta tarea. (Consulte [Invocar un servicio mediante una biblioteca de cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)).

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para optimizar el rendimiento del servicio Forms al procesar un formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer opciones de rendimiento en tiempo de ejecución.
1. Procese el formulario.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si está usando la API de Java, cree un objeto `FormsServiceClient`. Si está usando la API del servicio web de Forms, cree un objeto `FormsService`.

**Establecer opciones de tiempo de ejecución de rendimiento**

Puede establecer las siguientes opciones de tiempo de ejecución de rendimiento para mejorar el rendimiento del servicio de Forms:

* **Almacenamiento en caché de formularios**: puede almacenar en caché un formulario que se represente como PDF en la memoria caché del servidor. Cada formulario se almacena en caché después de generarse por primera vez. En un procesamiento posterior, si el formulario en caché es más reciente que la marca de tiempo del diseño de formulario, el formulario se recuperará de la caché. Al almacenar en caché los formularios, se mejora el rendimiento del servicio de Forms porque no tiene que recuperar el diseño de formulario de un repositorio.
* Las guías del formulario (obsoletas) pueden tardar más en procesarse que otros tipos de transformación. Se recomienda almacenar en caché las guías del formulario (obsoletas) para mejorar el rendimiento.
* **Opción independiente**: si no necesita que el servicio Forms realice cálculos del lado del servidor, puede establecer la opción Independiente en `true`, lo que hace que los formularios se representen sin información de estado. La información de estado es necesaria si desea procesar un formulario interactivo para un usuario final que luego introduzca información en el formulario y lo envíe de nuevo al servicio de Forms. A continuación, el servicio Forms realiza una operación de cálculo y devuelve el formulario al usuario con los resultados mostrados en el formulario. Si se devuelve un formulario sin información de estado al servicio Forms, solo estarán disponibles los datos XML y no se realizarán cálculos en el servidor.
* **PDF linearizado**: un archivo PDF linearizado está organizado para habilitar un acceso incremental eficiente en un entorno de red. El archivo PDF es válido en PDF en todos los aspectos y es compatible con todos los visores existentes y otras aplicaciones de PDF. Es decir, se puede ver una PDF linealizada mientras se sigue descargando.
* Esta opción no mejora el rendimiento cuando se procesa un formulario de PDF en el cliente.
* **Opción GuideRSL**: habilita la generación de guías de formulario (obsoleta) mediante bibliotecas compartidas en tiempo de ejecución. Esto significa que la primera solicitud descargará un archivo SWF más pequeño, además de bibliotecas compartidas más grandes almacenadas en la caché del explorador. Para obtener más información, consulte RSL en la documentación de Flex.
* También puede mejorar el rendimiento del servicio Forms al procesar un formulario en el cliente. (Consulte [Renderización de Forms en el cliente](/help/forms/developing/rendering-forms-client.md)).

**Procesar el formulario**

Para procesar el formulario después de establecer las opciones de rendimiento, utilice la misma lógica de aplicación que para procesar un formulario sin opciones de rendimiento.

**Escriba el flujo de datos del formulario en el explorador web del cliente**

Una vez que el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Optimizar el rendimiento mediante la API de Java {#optimize-the-performance-using-the-java-api}

Procese un formulario con un rendimiento optimizado mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establecer opciones de rendimiento en tiempo de ejecución

   * Crear un objeto `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de caché del formulario invocando el método `setCacheEnabled` del objeto `PDFFormRenderSpec` y pasando `true`.
   * Establezca la opción linealizada invocando el método `setLinearizedPDF` del objeto `PDFFormRenderSpec` y pasando `true.`

1. Procesar el formulario

   Invoque el método `renderPDFForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución para mejorar el rendimiento.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para enviar un flujo de datos de formulario al explorador web del cliente.
   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Optimización del rendimiento mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Optimizar el rendimiento mediante la API de servicio web {#optimize-the-performance-using-the-web-service-api}

Procese un formulario con un rendimiento optimizado mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de rendimiento en tiempo de ejecución

   * Crear un objeto `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de caché del formulario invocando el método `setCacheEnabled` del objeto `PDFFormRenderSpec` y pasando true.
   * Establezca la opción independiente invocando el método `setStandAlone` del objeto `PDFFormRenderSpec` y pasando true.
   * Establezca la opción linealizada invocando el método `setLinearizedPDF` del objeto `PDFFormRenderSpec` y pasando true.

1. Procesar el formulario

   Invoque el método `renderPDFForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Objeto `PDFFormRenderSpecc` que almacena opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que ha rellenado el método. Se utiliza para almacenar el formulario de PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que ha rellenado el método. (Este argumento almacenará el número de páginas en el formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que ha rellenado el método. (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `value` del objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para enviar un flujo de datos de formulario al explorador web del cliente.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
