---
title: Trabajar con formularios con códigos de barras
description: Descodificar datos de un formulario PDF o una imagen que contenga un código de barras mediante la API de Java y la API de servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations, Barcoded Forms
hide: true
hidefromtoc: true
exl-id: 71dc8036-f9a3-4e00-bce1-3f162428053d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# Trabajar con formularios con códigos de barras {#working-with-barcoded-forms}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio de formularios con códigos de barras {#about-the-barcoded-forms-service}

El servicio de formularios con códigos de barras automatiza la captura de datos de los formularios de cumplimentación e impresión e integra la información capturada en los sistemas informáticos principales de una organización.

Con el servicio de formularios con códigos de barras, puede agregar códigos de barras unidimensionales y bidimensionales a PDF forms interactivo. A continuación, puede publicar los formularios con códigos de barras en un sitio web o distribuirlos por correo electrónico o CD. Cuando un usuario rellena un formulario con códigos de barras con Adobe Reader, Acrobat Professional o Acrobat Standard, el código de barras se actualiza automáticamente para codificar los datos del formulario proporcionados por el usuario. El usuario puede enviar el formulario electrónicamente o imprimirlo en papel y enviarlo por correo, fax o mano. Posteriormente, puede extraer los datos suministrados por el usuario como parte de un flujo de trabajo automatizado, y enrutar los datos entre procesos de aprobación y sistemas empresariales.

Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Descodificación de datos de formulario con códigos de barras {#decoding-barcoded-form-data}

Puede utilizar la API del servicio de formularios con códigos de barras para descodificar datos de un formulario de PDF o de una imagen que contenga un código de barras. Descodificar datos de formulario significa extraer datos que se encuentran en el código de barras. Para poder descodificar los datos de un formulario (o imagen) de PDF, un usuario debe rellenar el formulario con datos.

>[!NOTE]
>
>Para obtener más información sobre el servicio de formularios con códigos de barras, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para descodificar datos de un formulario de PDF, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de API formsClient con códigos de barras.
1. Obtenga un formulario de PDF que contenga datos con códigos de barras.
1. Descodificar los datos del formulario de PDF.
1. Convertir los datos en una fuente de datos XML.
1. Procese los datos descodificados.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)
* xercesImpl.jar (en &lt;directorio de instalación>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\third-party)

Si AEM Forms se implementa en un servidor de aplicaciones J2EE compatible que no sea JBOSS, debe reemplazar adobe-utilities.jar y jbossall-client.jar por archivos JAR específicos del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Para obtener información sobre la ubicación de todos los archivos JAR de AEM Forms, consulte [Incluyendo los archivos de la biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API de cliente de formularios con códigos de barras**

Para poder realizar mediante programación una operación de servicio de Forms con códigos de barras, debe crear un cliente de servicio de Forms con códigos de barras. Si está usando la API de Java, cree un objeto `BarcodedFormsServiceClient`. Si utiliza la API del servicio web de formularios con códigos de barras, cree un objeto `BarcodedFormsServiceService`.

**Obtener un formulario de PDF que contenga datos con códigos de barras**

Obtenga un formulario de PDF que contenga un código de barras que se haya rellenado con datos de usuario.

**Descodificar los datos del formulario de PDF**

Después de obtener un formulario (o una imagen) de PDF que contiene un código de barras, puede descodificar los datos. El servicio de Forms con códigos de barras es compatible con los siguientes tipos de códigos de barras:

* Códigos de barras PDF417.
* Códigos de barras de matriz de datos.
* Códigos de barras QR.
* Códigos de barras de Codabar.
* Código 128 códigos de barras.
* Código 39 códigos de barras.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

La entrada de conjunto de caracteres como hexadecimal en la API de descodificación implica que el contenido del código de barras se codifica como una cadena hexadecimal. Por ejemplo, si se especifica UTF-8 como codificación de caracteres en el formulario y Hex en la operación de descodificación, el contenido del código de barras se codifica como una cadena Hex en el elemento &lt; `xb:content`> de la salida descodificada. Puede convertir este valor hexadecimal para obtener el contenido original creando lógica de aplicación en la aplicación cliente.

**Convertir los datos en una fuente de datos XML**

Después de descodificar los datos del formulario, puede convertirlos en datos XDP o XFDF. Por ejemplo, supongamos que desea importar los datos en otro formulario. Para importar los datos en un formulario XFA, debe convertirlos en datos XDP. Para obtener más información, consulte [Importación de datos de formulario](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Procesar los datos descodificados**

Puede procesar los datos convertidos para satisfacer sus necesidades comerciales. Por ejemplo, después de descodificar y convertir los datos, puede guardarlos en un archivo, almacenarlos en una base de datos empresarial, rellenar otro formulario, etc. En esta sección se explica cómo guardar los datos convertidos como un archivo XML.

>[!NOTE]
>
>El servicio de Forms con códigos de barras no puede descodificar los datos de códigos de barras cuando los parámetros delimitador de línea y delimitador de campo tienen el mismo valor

**Consulte también**

[Descodificar datos de formulario con códigos de barras mediante la API de Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Descodificar datos de formulario con códigos de barras mediante la API de servicio web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario con códigos de barras mediante la API de Java {#decode-barcoded-form-data-using-the-java-api}

Descodificar datos de formulario mediante la API de formularios con códigos de barras (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de formularios con códigos de barras

   Cree un objeto `BarcodedFormsServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Obtenga un formulario de PDF que contenga datos con códigos de barras

   * Cree un objeto `java.io.FileInputStream` que represente el formulario de PDF que contiene datos con códigos de barras utilizando su constructor y pasando un valor de cadena que especifique la ubicación del documento de PDF.
   * Cree un objeto `com.adobe.idp.Document` utilizando su constructor y pasando el objeto `java.io.FileInputStream`.

1. Descodificar los datos del formulario de PDF

   Descodificar los datos del formulario invocando el método `decode` del objeto `BarcodedFormsServiceClient` y pasando los siguientes valores:

   * El objeto `com.adobe.idp.Document` que contiene el formulario de PDF.
   * Un objeto `java.lang.Boolean` que especifica si se va a descodificar un código de barras PDF417.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras de matriz de datos.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras de código QR.
   * Un objeto `java.lang.Boolean` que especifica si se va a descodificar un código de barras de la barra de códigos.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras 128.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras 39.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras EAN-13.
   * Un objeto `java.lang.Boolean` que especifica si se debe descodificar un código de barras EAN-8.
   * Valor de enumeración `com.adobe.livecycle.barcodedforms.CharSet` que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El método `decode` devuelve un objeto `org.w3c.dom.Document` que contiene datos de formulario descodificados.

1. Convertir los datos en una fuente de datos XML

   Convierta los datos descodificados en datos XDP o XFDF invocando el método `extractToXML` del objeto `BarcodedFormsServiceClient` y pasando los siguientes valores:

   * El objeto `org.w3c.dom.Document` que contiene datos descodificados (asegúrese de utilizar el valor devuelto del método `decode`).
   * Valor de enumeración `com.adobe.livecycle.barcodedforms.Delimiter` que especifica el delimitador de línea. Se recomienda especificar `Delimiter.Carriage_Return`.
   * Valor de enumeración `com.adobe.livecycle.barcodedforms.Delimiter` que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * Valor de enumeración `com.adobe.livecycle.barcodedforms.XMLFormat` que especifica si se convierten los datos de código de barras en datos XML XDP o XFDF. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros de delimitador de línea y delimitador de campo.

   El método `extractToXML` devuelve un objeto `java.util.List` donde cada elemento es un objeto `org.w3c.dom.Document`. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si el formulario tiene cuatro códigos de barras, el objeto `java.util.List` devuelto contiene cuatro elementos.

1. Procesamiento de los datos descodificados

   * Recorra en iteración el objeto `java.util.List` para obtener cada objeto `org.w3c.dom.Document` que se encuentra en la lista.
   * Para cada elemento de la lista, convierta el objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document`. (La lógica de la aplicación que convierte un objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document` se muestra en el ejemplo de la API de Java Descodificación de datos de formulario con códigos de barras).
   * Guarde los datos XML como un archivo XML invocando `copyToFile` del objeto `com.adobe.idp.Document` y pasando un objeto File que represente el archivo XML.

**Consulte también**

[Inicio rápido (modo SOAP): Descodificación de datos de formulario con códigos de barras mediante la API de Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Descodificar datos de formulario con códigos de barras mediante la API de servicio web {#decode-barcoded-form-data-using-the-web-service-api}

Descodificar datos de formulario mediante la API de formularios con códigos de barras (servicio web):

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del servicio de formularios con códigos de barras. Para obtener más información, vea [Invocar AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. Para obtener más información, vea &quot;Hacer referencia al ensamblado de cliente .NET&quot; en [Invocar AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Crear un objeto de API de cliente de formularios con códigos de barras

   Con el ensamblado de cliente de Microsoft .NET que consume el WSDL del servicio de formularios con códigos de barras, cree un objeto `BarcodedFormsServiceService` invocando su constructor predeterminado.

1. Obtenga un formulario de PDF que contenga datos con códigos de barras

   * Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF que contiene un código de barras.
   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF y el modo en que se abrirá el archivo.
   * Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
   * Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream` y pasando la matriz de bytes, la posición inicial y la longitud de secuencia para que se lea.
   * Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.

1. Descodificar los datos del formulario de PDF

   Descodificar los datos del formulario invocando el método `decode` del objeto `BarcodedFormsServiceService` y pasando los siguientes valores:

   * El objeto `BLOB` que contiene el formulario de PDF.
   * Un objeto `Boolean` que especifica si se va a descodificar un código de barras PDF417.
   * Un objeto `Boolean` que especifica si se debe descodificar un código de barras de matriz de datos.
   * Un objeto `Boolean` que especifica si se debe descodificar un código de barras de código QR.
   * Un objeto `Boolean` que especifica si se va a descodificar un código de barras de la barra de códigos.
   * Un objeto `Boolean` que especifica si se debe descodificar un código de barras 128.
   * Un objeto `Bolean` que especifica si se debe descodificar un código de barras 39.
   * Un objeto `Boolean` que especifica si se debe descodificar un código de barras EAN-13.
   * Un objeto `Boolean` que especifica si se debe descodificar un código de barras EAN-8.
   * Valor de enumeración `CharSet` que especifica el valor de codificación del conjunto de caracteres utilizado en el código de barras.

   El método `decode` devuelve un valor de cadena que contiene datos de formulario descodificados.

1. Convertir los datos en una fuente de datos XML

   Convierta los datos descodificados en datos XDP o XFDF invocando el método `extractToXML` del objeto `BarcodedFormsServiceService` y pasando los siguientes valores:

   * Valor de cadena que contiene datos descodificados (asegúrese de utilizar el valor devuelto del método `decode`).
   * Valor de enumeración `Delimiter` que especifica el delimitador de línea. Se recomienda especificar `Delimiter.Carriage_Return`.
   * Valor de enumeración `Delimiter` que especifica el delimitador de campo. Por ejemplo, especifique `Delimiter.Tab`.
   * Valor de enumeración `XMLFormat` que especifica si se convierten los datos de código de barras en datos XML XDP o XFDF. Por ejemplo, especifique `XMLFormat.XDP` para convertir los datos en datos XDP.

   >[!NOTE]
   >
   >No especifique los mismos valores para los parámetros de delimitador de línea y delimitador de campo.

   El método `extractToXML` devuelve una matriz `Object` donde cada elemento es una instancia `BLOB`. Hay un elemento independiente para cada código de barras ubicado en el formulario. Es decir, si hay cuatro códigos de barras en el formulario, hay cuatro elementos en la matriz `Object` devuelta.

1. Procesamiento de los datos descodificados

   * Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF protegido.
   * Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `encryptPDFUsingPassword`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `binaryData` del objeto `BLOB`.
   * Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
   * Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
