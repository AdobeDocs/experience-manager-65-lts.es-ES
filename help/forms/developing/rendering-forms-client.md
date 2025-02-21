---
title: Procesar formularios en el cliente
description: Optimizar la entrega de contenido de PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de procesamiento del lado del cliente de Acrobat o Adobe Reader
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
source-wordcount: '1690'
ht-degree: 1%

---

# Procesar formularios en el cliente {#rendering-forms-at-the-client}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Procesar formularios en el cliente {#rendering-forms-at-the-client-inner}

Puede optimizar la entrega de contenido de PDF y mejorar la capacidad del servicio Forms para gestionar la carga de red mediante la capacidad de procesamiento del lado del cliente de Acrobat o Adobe Reader. Este proceso se conoce como procesar un formulario en el cliente. Para procesar un formulario en el cliente, el dispositivo cliente (normalmente un explorador web) debe utilizar Acrobat 7.0 o Adobe Reader 7.0 o posterior.

Los cambios realizados en un formulario como resultado de la ejecución de scripts del lado del servidor no se reflejan en un formulario que se procese en el cliente a menos que el subformulario raíz contenga el atributo `restoreState` establecido en `auto`. Para obtener más información acerca de este atributo, vea [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario en el cliente, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Establecer las opciones de tiempo de ejecución de procesamiento de cliente.
1. Procesar un formulario en el cliente.
1. Escriba el formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si está usando la API de Java, cree un objeto `FormsServiceClient`. Si está usando la API del servicio web de Forms, cree un objeto `FormsService`.

**Establecer opciones de tiempo de ejecución de procesamiento de cliente**

Establezca la opción de tiempo de ejecución de representación de cliente para procesar un formulario en el cliente estableciendo la opción de tiempo de ejecución `RenderAtClient` en `true`. Esto hace que el formulario se envíe al dispositivo cliente donde se representa. Si `RenderAtClient` es `auto` (el valor predeterminado), el diseño de formulario determina si el formulario se procesará en el cliente. El diseño de formulario debe ser un diseño de formulario con un diseño fluido.

Una opción de tiempo de ejecución opcional que puede establecer es la opción `SeedPDF`. La opción `SeedPDF` combina el contenedor de PDF (documento PDF semilla) con el diseño de formulario y los datos XML. Tanto el diseño de formulario como los datos XML se envían a Acrobat o Adobe Reader, donde se procesa el formulario. La opción `SeedPDF` se puede usar cuando el equipo cliente no tiene fuentes que se usen en el formulario, como cuando un usuario final no tiene licencia para usar una fuente para la que el propietario del formulario tiene licencia.

Puede utilizar Designer para crear un archivo PDF dinámico simple para utilizarlo como archivo PDF semilla. Se requieren los siguientes pasos para realizar esta tarea:

1. Determine si necesita incrustar alguna fuente dentro del archivo PDF semilla. El archivo PDF semilla debe contener las fuentes adicionales que requiere el formulario que se está procesando. Al incrustar fuentes en el archivo PDF semilla, asegúrese de que no infringe ningún acuerdo de licencia de fuentes. En Designer, puede determinar si puede incrustar fuentes legalmente. Al guardar, si hay fuentes que no se pueden incrustar en el formulario, Designer muestra un mensaje con las fuentes que no se pueden incrustar. Este mensaje no se muestra en Designer para documentos estáticos de PDF.
1. Si está creando el archivo de PDF semilla en Designer, se recomienda que, como mínimo, añada un campo de texto que contenga un mensaje. El mensaje debe dirigirse a los usuarios de versiones anteriores de Adobe Reader para informarles de que necesitan Acrobat 7.0 o posterior, o Adobe Reader 7.0 o posterior, para ver el documento.
1. Guarde el archivo PDF semilla como un archivo PDF dinámico con la extensión de nombre de archivo PDF.

>[!NOTE]
>
>No es necesario definir la opción de tiempo de ejecución de PDF semilla para procesar un formulario en el cliente. Si no especifica un PDF semilla, el servicio Forms crea un PDF de shell que no contendrá objetos COS, pero sí un envoltorio PDF con el contenido XDP real incrustado en él. Los pasos de esta sección no establecen la opción del tiempo de ejecución de PDF semilla. Para obtener información sobre los objetos COS, consulte la Guía de referencia de Adobe PDF.

**Procesar un formulario en el cliente**

Para procesar un formulario en el cliente, debe asegurarse de que las opciones de tiempo de ejecución de procesamiento del cliente estén incluidas en la lógica de la aplicación para procesar un formulario.

**Escriba el flujo de datos del formulario en el explorador web del cliente**

El servicio Forms crea un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario se procesa mediante Acrobat 7.0 o Adobe Reader 7.0 o posterior y es visible para el usuario.

**Consulte también**

[Procesar un formulario en el cliente mediante la API de Java](#render-a-form-at-the-client-using-the-java-api)

[Procesar un formulario en el cliente mediante la API de servicio web](#render-a-form-at-the-client-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Pasar documentos al servicio de Forms](/help/forms/developing/passing-documents-forms-service.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar un formulario en el cliente mediante la API de Java {#render-a-form-at-the-client-using-the-java-api}

Procesar un formulario en el cliente mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Establecer opciones de tiempo de ejecución de procesamiento de cliente

   * Crear un objeto `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de tiempo de ejecución `RenderAtClient` invocando el método `setRenderAtClient` del objeto `PDFFormRenderSpec` y pasando el valor de enumeración `RenderAtClient.Yes`.

1. Procesar un formulario en el cliente

   Invoque el método `renderPDFForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de AEM Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Un objeto `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms para procesar un formulario.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Procesar un formulario en el cliente mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Procesar un formulario en el cliente mediante la API de servicio web {#render-a-form-at-the-client-using-the-web-service-api}

Procesar un formulario en el cliente mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Establecer opciones de tiempo de ejecución de procesamiento de cliente

   * Crear un objeto `PDFFormRenderSpec` mediante su constructor.
   * Establezca la opción de tiempo de ejecución `RenderAtClient` invocando el método `setRenderAtClient` del objeto `PDFFormRenderSpec` y pasando el valor de cadena `RenderAtClient.Yes`.

1. Procesar un formulario en el cliente

   Invoque el método `renderPDFForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`. (Consulte [Rellenado previo de Forms con diseños flexibles](/help/forms/developing/prepopulating-forms-flowable-layouts.md)).
   * Un objeto `PDFFormRenderSpec` que almacena las opciones en tiempo de ejecución necesarias para procesar un formulario en el cliente.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que ha rellenado el método. Este parámetro se utiliza para almacenar el formulario de PDF procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que ha rellenado el método. (Este argumento almacenará el número de páginas en el formulario).
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que ha rellenado el método. (Este argumento almacenará el valor de configuración regional).
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderPDFForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `value` del objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Procesar formularios en el cliente](#rendering-forms-at-the-client)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
