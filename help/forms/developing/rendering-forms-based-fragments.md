---
title: Procesar formularios basados en fragmentos
description: Utilice el servicio Forms para procesar formularios basados en fragmentos creados con Designer.
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
exl-id: 3af4361d-ff30-46db-ac88-64bfae8f63a4
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 3%

---

# Procesar formularios basados en fragmentos {#rendering-forms-based-on-fragments}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Procesar formularios basados en fragmentos {#rendering-forms-based-on-fragments-inner}

El servicio Forms puede procesar formularios basados en fragmentos creados con Designer. Un *fragmento* es una parte reutilizable de un formulario y se guarda como un archivo XDP independiente que se puede insertar en varios diseños de formulario. Por ejemplo, un fragmento puede incluir un bloque de direcciones o texto legal.

El uso de fragmentos simplifica y acelera la creación y el mantenimiento de una gran cantidad de formularios. Al crear un formulario, inserte una referencia al fragmento requerido y este aparecerá en el formulario. La referencia de fragmento contiene un subformulario que señala al archivo XDP físico. Para obtener información sobre la creación de diseños de formulario basados en fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un fragmento puede incluir varios subformularios envueltos en un conjunto de subformularios de opción. Los conjuntos de subformularios de opción controlan la visualización de subformularios en función del flujo de datos desde una conexión de datos. Las sentencias condicionales se utilizan para determinar qué subformulario del conjunto aparece en el formulario enviado. Por ejemplo, cada subformulario de un conjunto puede incluir información de una ubicación geográfica determinada y el subformulario que se muestra se puede determinar en función de la ubicación del usuario.

Un *fragmento de script* contiene funciones o valores de JavaScript reutilizables que se almacenan por separado de cualquier objeto en particular, como un analizador de fechas o una invocación de servicio web. Estos fragmentos incluyen un solo objeto de script que aparece como un elemento secundario de variables en la paleta Jerarquía. Los fragmentos no se pueden crear a partir de scripts que sean propiedades de otros objetos, como scripts de evento como validate, calculate o initialize.

Estas son las ventajas de utilizar fragmentos:

* **Reutilización de contenido**: puede utilizar fragmentos para reutilizar contenido en varios diseños de formulario. Cuando necesita utilizar parte del mismo contenido en varios formularios, es más rápido y sencillo utilizar un fragmento que copiar o volver a crear el contenido. El uso de fragmentos también garantiza que el contenido y el aspecto de las partes de un diseño de formulario que se utilizan con frecuencia sean coherentes en todos los formularios de referencia.
* **Actualizaciones globales**: puede usar fragmentos para realizar cambios globales en varios formularios solo una vez, en un archivo. Puede cambiar el contenido, los objetos de script, los enlaces de datos, el diseño o los estilos de un fragmento, y todos los formularios XDP que hagan referencia a él reflejarán los cambios.
* Por ejemplo, un elemento común en muchos formularios podría ser un bloque de direcciones que incluya un objeto de lista desplegable para el país. Si necesita actualizar los valores del objeto de lista desplegable, debe abrir muchos formularios para realizar los cambios. Si incluye el bloque de direcciones en un fragmento, solo necesita abrir un archivo de fragmento para realizar los cambios.
* Para actualizar un fragmento en un formulario de PDF, debe volver a guardar el formulario en Designer.
* **Creación de formularios compartidos**: puede utilizar fragmentos para compartir la creación de formularios entre varios recursos. Los desarrolladores de formularios con experiencia en scripts u otras funciones avanzadas de Designer pueden desarrollar y compartir fragmentos que aprovechan los scripts y las propiedades dinámicas. Los diseñadores de formularios pueden utilizar esos fragmentos para diseñar diseños de formulario y para asegurarse de que todas las partes de un formulario tienen un aspecto y una funcionalidad coherentes en todos los formularios diseñados por varias personas.

### Combinar un diseño de formulario ensamblado mediante fragmentos {#assembling-a-form-design-assembled-using-fragments}

Puede combinar un diseño de formulario para pasarlo al servicio de Forms en función de varios fragmentos. Para ensamblar varios fragmentos, utilice el servicio Assembler. Para ver un ejemplo de cómo usar el servicio Assembler para crear un diseño de formulario usado por otros servicios de Forms (el servicio Output), vea [Crear documentos de PDF mediante fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). En lugar de utilizar el servicio Output, puede realizar el mismo flujo de trabajo mediante el servicio Forms.

Al utilizar el servicio Assembler, pasa un diseño de formulario que se ensambló mediante fragmentos. El diseño de formulario creado no hace referencia a otros fragmentos. Por el contrario, este tema trata sobre cómo pasar un diseño de formulario que hace referencia a otros fragmentos al servicio de Forms. Sin embargo, Assembler no ensambló el diseño de formulario. Se creó en Designer.

>[!NOTE]
>
>Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obtener información acerca de cómo crear una aplicación basada en Web que procese formularios basados en fragmentos, vea [Crear aplicaciones Web que procese Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario basado en fragmentos, realice las siguientes tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de cliente de Forms.
1. Especifique los valores de URI.
1. Procese el formulario.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un objeto de API de cliente de Forms**

Para poder realizar mediante programación una operación de API de cliente de servicio de Forms, debe crear un cliente de servicio de Forms.

**Especificar valores de URI**

Para procesar correctamente un formulario basado en fragmentos, debe asegurarse de que el servicio Forms pueda localizar el formulario y los fragmentos (los archivos XDP) a los que hace referencia el diseño de formulario. Por ejemplo, supongamos que el formulario se denomina PO.xdp y que utiliza dos fragmentos llamados FooterUS.xdp y FooterCanada.xdp. En este caso, el servicio Forms debe poder localizar los tres archivos XDP.

Puede organizar un formulario y sus fragmentos colocándolo en una ubicación y los fragmentos en otra ubicación, o bien puede colocar todos los archivos XDP en la misma ubicación. A los efectos de esta sección, supongamos que todos los archivos XDP están en el repositorio de AEM Forms. Para obtener información sobre cómo colocar archivos XDP en el repositorio de AEM Forms, consulte [Recursos de escritura](/help/forms/developing/aem-forms-repository.md#writing-resources).

Al procesar un formulario basado en fragmentos, solo debe hacer referencia al propio formulario y no a los fragmentos. Por ejemplo, debe hacer referencia a PO.xdp y no a FooterUS.xdp o FooterCanada.xdp. Asegúrese de colocar los fragmentos en una ubicación en la que el servicio Forms pueda localizarlos.

**Procesar el formulario**

Un formulario basado en fragmentos se puede procesar del mismo modo que los formularios no fragmentados. Es decir, puede procesar el formulario como PDF, HTML o guías del formulario (obsoleto). El ejemplo de esta sección procesa un formulario basado en fragmentos como un formulario interactivo de PDF. (Consulte [Procesamiento de PDF forms interactivo](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Escriba el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente. Cuando se escribe en el explorador web del cliente, el formulario es visible para el usuario.

**Consulte también**

[Procesar formularios basados en fragmentos mediante la API de Java](#render-forms-based-on-fragments-using-the-java-api)

[Procesar formularios basados en fragmentos mediante la API de servicio web](#render-forms-based-on-fragments-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar formularios basados en fragmentos mediante la API de Java {#render-forms-based-on-fragments-using-the-java-api}

Procesar un formulario basado en fragmentos mediante la API de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Crear un objeto de API de cliente de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores de URI mediante su constructor.
   * Invoque el método `setApplicationWebRoot` del objeto `URLSpec` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `setContentRootURI` del objeto `URLSpec` y pase un valor de cadena que especifique el valor del URI de raíz de contenido. Asegúrese de que el diseño de formulario y los fragmentos estén en el URI raíz de contenido. Si no es así, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el método `setTargetURL` del objeto `URLSpec` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Procesar el formulario

   Invoque el método `renderPDFForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms para procesar un formulario basado en fragmentos.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderPDFForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` utilizado para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes para rellenarla con el flujo de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Procesar formularios basados en fragmentos](#rendering-forms-based-on-fragments)

[Inicio rápido (modo SOAP): Procesamiento de un formulario basado en fragmentos mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Procesar formularios basados en fragmentos mediante la API de servicio web {#render-forms-based-on-fragments-using-the-web-service-api}

Procesar un formulario basado en fragmentos mediante la API de Forms (servicio web):

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Crear un objeto de API de cliente de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Especificar valores de URI

   * Cree un objeto `URLSpec` que almacene valores de URI mediante su constructor.
   * Invoque el método `setApplicationWebRoot` del objeto `URLSpec` y pase un valor de cadena que represente la raíz web de la aplicación.
   * Invoque el método `setContentRootURI` del objeto `URLSpec` y pase un valor de cadena que especifique el valor del URI de raíz de contenido. Asegúrese de que el diseño del formulario esté en el URI raíz del contenido. Si no es así, el servicio Forms genera una excepción. Para hacer referencia al repositorio, especifique `repository://`.
   * Invoque el método `setTargetURL` del objeto `URLSpec` y pase un valor de cadena que especifique el valor de la dirección URL de destino donde se publican los datos del formulario. Si define la dirección URL de destino en el diseño de formulario, puede pasar una cadena vacía. También puede especificar la dirección URL a la que se envía un formulario para realizar cálculos.

1. Procesar el formulario

   Invoque el método `renderPDFForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * Objeto `PDFFormRenderSpec` que almacena opciones en tiempo de ejecución. La opción PDF etiquetada no se puede establecer si el documento de entrada es un documento de PDF. Si el archivo de entrada es un archivo XDP, se puede establecer la opción PDF etiquetado.
   * Un objeto `URLSpec` que contiene valores de URI requeridos por el servicio Forms.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que ha rellenado el método. Este parámetro se utiliza para almacenar el formulario procesado.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que ha rellenado el método. Este argumento almacenará el número de páginas en el formulario.
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que ha rellenado el método. Este argumento almacenará el valor de configuración regional.
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

[Procesar formularios basados en fragmentos](#rendering-forms-based-on-fragments)

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
