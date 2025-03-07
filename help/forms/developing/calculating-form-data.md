---
title: Calcular datos de formulario
description: Utilice el servicio Forms para calcular los valores que un usuario introduce en un formulario y mostrar los resultados. El servicio Forms calcula los valores mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 071a6ccb-8204-4cbc-a39b-143da52c16f7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Calcular datos de formulario {#calculating-form-data}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

El servicio Forms puede calcular los valores que un usuario introduce en un formulario y mostrar los resultados. Para calcular los datos del formulario, debe realizar dos tareas. En primer lugar, se crea un script de diseño de formulario que calcula los datos del formulario. Un diseño de formulario admite tres tipos de scripts. Un tipo de script se ejecuta en el cliente, otro se ejecuta en el servidor y el tercer tipo se ejecuta tanto en el servidor como en el cliente. El tipo de script que se describe en este tema se ejecuta en el servidor. Los cálculos del lado del servidor son compatibles con las transformaciones de HTML, PDF y la Guía de formularios (obsoletas).

Como parte del proceso de diseño del formulario, puede utilizar cálculos y scripts para proporcionar una experiencia de usuario más rica. Los cálculos y las secuencias de comandos se pueden agregar a la mayoría de los campos y objetos de formulario. Cree una secuencia de comandos de diseño de formulario para realizar operaciones de cálculo con los datos que un usuario introduce en un formulario interactivo.

El usuario introduce valores en el formulario y hace clic en el botón Calcular para ver los resultados. El siguiente proceso describe una aplicación de ejemplo que permite a un usuario calcular datos:

* El usuario accede a una página de HTML denominada StartLoan.html que actúa como página de inicio de la aplicación web. Esta página invoca un servlet Java denominado `GetLoanForm`.
* El servlet `GetLoanForm` procesa un formulario de préstamo. Este formulario contiene un script, campos interactivos, un botón de cálculo y un botón de envío.
* El usuario introduce valores en los campos del formulario y hace clic en el botón Calcular. El formulario se enviará al servlet Java `CalculateData` donde se ejecutará el script. El formulario se devuelve al usuario con los resultados del cálculo mostrados en el formulario.
* El usuario continúa introduciendo y calculando valores hasta que se muestra un resultado satisfactorio. Cuando esté satisfecho, el usuario hace clic en el botón Enviar para procesar el formulario. El formulario se enviará a otro servlet Java denominado `ProcessForm` responsable de recuperar los datos enviados. (Consulte [Gestión de Forms enviados](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


El diagrama siguiente muestra el flujo lógico de la aplicación.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

En la tabla siguiente se describen los pasos de este diagrama.

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>El servlet Java <code>GetLoanForm</code> se invoca desde la página de inicio de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>El servlet Java <code>GetLoanForm</code> utiliza la API de cliente del servicio Forms para procesar el formulario de préstamo en el explorador web del cliente. La diferencia entre procesar un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor y procesar un formulario que no contiene una secuencia de comandos es que debe especificar la ubicación de destino utilizada para ejecutar la secuencia de comandos. Si no se especifica una ubicación de destino, no se ejecuta ninguna secuencia de comandos configurada para ejecutarse en el servidor. Por ejemplo, considere la aplicación introducida en esta sección. El servlet Java <code>CalculateData</code> es la ubicación de destino donde se ejecuta el script.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El usuario introduce datos en campos interactivos y hace clic en el botón Calcular. El formulario se enviará al servlet Java <code>CalculateData</code>, donde se ejecutará el script. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El formulario se vuelve a procesar en el explorador web con los resultados del cálculo mostrados en el formulario. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>El usuario hace clic en el botón Enviar cuando los valores son satisfactorios. El formulario se enviará a otro servlet Java denominado <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

Normalmente, un formulario enviado como contenido de PDF contiene scripts que se ejecutan en el cliente. Sin embargo, también se pueden ejecutar cálculos del lado del servidor. No se puede utilizar un botón Enviar para calcular scripts. En este caso, los cálculos no se ejecutan porque el servicio Forms considera que la interacción ha finalizado.

Para ilustrar el uso de una secuencia de comandos de diseño de formulario, esta sección examina un formulario interactivo simple que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El diagrama siguiente muestra un diseño de formulario que contiene una secuencia de comandos que agrega valores que un usuario introduce en los dos primeros campos y muestra el resultado en el tercer campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Un campo denominado NumericField1 **B.** Un campo denominado NumericField2 **C.** Un campo denominado NumericField3

La sintaxis de la secuencia de comandos en este diseño de formulario es la siguiente:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

En este diseño de formulario, el botón Calcular es un botón de comando y el script se encuentra en el evento `Click` de este botón. Cuando un usuario introduce valores en los dos primeros campos (NumericField1 y NumericField2) y hace clic en el botón Calcular, el formulario se envía al servicio de Forms, donde se ejecuta la secuencia de comandos. El servicio Forms vuelve a procesar el formulario en el dispositivo cliente con los resultados del cálculo mostrados en el campo NumericField3.

>[!NOTE]
>
>Para obtener información sobre cómo crear un script de diseño de formulario, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumen de los pasos {#summary-of-steps}

Para calcular los datos del formulario, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Recupere un formulario que contenga un script de cálculo.
1. Escribir el flujo de datos de formulario en el explorador web del cliente

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms. Si está usando la API de Java, cree un objeto `FormsServiceClient`. Si está usando la API del servicio web de Forms, cree un objeto `FormsServiceService`.

**Recuperar un formulario que contiene un script de cálculo**

La API de cliente del servicio de Forms se utiliza para crear una lógica de aplicación que administra un formulario que contiene una secuencia de comandos configurada para ejecutarse en el servidor. El proceso es similar a la gestión de un formulario enviado. (Consulte [Gestión de Forms enviados](/help/forms/developing/handling-submitted-forms.md).)

Compruebe que el estado de procesamiento asociado con el formulario enviado es `1` `(Calculate)`, lo que significa que el servicio Forms está realizando una operación de cálculo en los datos del formulario y que los resultados se deben escribir en el usuario. En este caso, se ejecuta automáticamente un script configurado para ejecutarse en el servidor.

**Vuelva a escribir el flujo de datos de formulario en el explorador web del cliente**

Después de comprobar que el estado de procesamiento asociado a un formulario enviado es `1`, debe escribir los resultados en el explorador web del cliente. Cuando se muestra el formulario, el valor calculado aparece en los campos correspondientes.

**Consulte también**

[Incluyendo archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcular datos de formulario mediante la API de Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcular datos de formulario mediante la API de servicio web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Inicios rápidos de la API de servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Procesando PDF forms interactivo](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Creación de aplicaciones web que procesan Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcular datos de formulario mediante la API de Java {#calculate-form-data-using-the-java-api}

Calcular datos de formulario mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Recuperar un formulario que contiene un script de cálculo

   * Para recuperar datos de formulario que contengan un script de cálculo, cree un objeto `com.adobe.idp.Document` utilizando su constructor e invocando el método `getInputStream` del objeto `javax.servlet.http.HttpServletResponse` desde el constructor.
   * Invoque el método `processFormSubmission` del objeto `FormsServiceClient` y pase los siguientes valores:

      * El objeto `com.adobe.idp.Document` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno, incluidos todos los encabezados HTTP relevantes. Especifique el tipo de contenido que se va a administrar especificando uno o varios valores para la variable de entorno `CONTENT_TYPE`. Por ejemplo, para administrar datos XML y PDF, especifique el siguiente valor de cadena para este parámetro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objeto `RenderOptionsSpec` que almacena opciones en tiempo de ejecución.

     El método `processFormSubmission` devuelve un objeto `FormsResult` que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado con un formulario enviado es `1` invocando el método `getAction` del objeto `FormsResult`. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.

1. Escribir el flujo de datos de formulario en el explorador web del cliente

   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para enviar un flujo de datos de formulario al explorador web del cliente.
   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**


[Incluyendo archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcular datos de formulario mediante la API de servicio web {#calculate-form-data-using-the-web-service-api}

Calcular datos de formulario mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Recuperar un formulario que contiene un script de cálculo

   * Para recuperar datos de formulario publicados en un servlet Java, cree un objeto `BLOB` mediante su constructor.
   * Cree un objeto `java.io.InputStream` mediante el método `getInputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.ByteArrayOutputStream` utilizando su constructor y pasando la longitud del objeto `java.io.InputStream`.
   * Copie el contenido del objeto `java.io.InputStream` en el objeto `java.io.ByteArrayOutputStream`.
   * Cree una matriz de bytes invocando el método `toByteArray` del objeto `java.io.ByteArrayOutputStream`.
   * Rellene el objeto `BLOB` invocando su método `setBinaryData` y pasando la matriz de bytes como argumento.
   * Crear un objeto `RenderOptionsSpec` mediante su constructor. Establezca el valor de configuración regional invocando el método `setLocale` del objeto `RenderOptionsSpec` y pasando un valor de cadena que especifique el valor de configuración regional.
   * Invoque el método `processFormSubmission` del objeto `FormsServiceClient` y pase los siguientes valores:

      * El objeto `BLOB` que contiene los datos del formulario.
      * Un valor de cadena que especifica variables de entorno que incluyen todos los encabezados HTTP relevantes. Por ejemplo, puede especificar el siguiente valor de cadena: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`; por ejemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Objeto `RenderOptionsSpec` que almacena opciones en tiempo de ejecución. Para obtener más información, consulte .
      * Un objeto `BLOBHolder` vacío que ha rellenado el método.
      * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que ha rellenado el método.
      * Un objeto `BLOBHolder` vacío que ha rellenado el método.
      * Un objeto `BLOBHolder` vacío que ha rellenado el método.
      * Un objeto `javax.xml.rpc.holders.ShortHolder` vacío que ha rellenado el método.
      * Un objeto `MyArrayOf_xsd_anyTypeHolder` vacío que ha rellenado el método. Este parámetro se utiliza para almacenar los archivos adjuntos enviados junto con el formulario.
      * Un objeto `FormsResultHolder` vacío que el método rellena con el formulario enviado.

     El método `processFormSubmission` rellena el parámetro `FormsResultHolder` con los resultados del envío del formulario. El método `processFormSubmission` devuelve un objeto `FormsResult` que contiene los resultados del envío del formulario.

   * Compruebe que el estado de procesamiento asociado con un formulario enviado es `1` invocando el método `getAction` del objeto `FormsResult`. Si este método devuelve el valor `1`, se realizó el cálculo y los datos se pueden escribir de nuevo en el explorador web del cliente.

1. Escribir el flujo de datos de formulario en el explorador web del cliente

   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para enviar un flujo de datos de formulario al explorador web del cliente.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar la secuencia de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Ver también**
[Invocar AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
