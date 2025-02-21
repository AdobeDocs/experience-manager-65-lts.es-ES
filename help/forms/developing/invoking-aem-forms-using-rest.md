---
title: Invocar AEM Forms mediante solicitudes REST
description: Invocar procesos creados en Workbench mediante solicitudes REST.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 0%

---

# Invocar AEM Forms mediante solicitudes REST {#invoking-aem-forms-using-rest-requests}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Los procesos creados en Workbench se pueden configurar para que se puedan invocar a través de solicitudes de transferencia de estado representacional (REST). Las solicitudes REST se envían desde páginas de HTML. Es decir, puede invocar un proceso de Forms directamente desde una página web mediante una solicitud REST. Por ejemplo, puede abrir una nueva instancia de una página web. A continuación, puede invocar un proceso de Forms y cargar un documento de PDF procesado con datos enviados en una solicitud HTTP POST.

Existen dos tipos de clientes de HTML. El primer cliente de HTML es un cliente de AJAX escrito en JavaScript. El segundo cliente es un formulario de HTML que contiene un botón de envío. Una aplicación cliente basada en HTML no es el único cliente REST posible. Cualquier aplicación cliente que admita solicitudes HTTP puede invocar un servicio mediante una invocación de REST. Por ejemplo, puede invocar un servicio utilizando una invocación de REST desde un formulario de PDF. (Consulte [Invocación del proceso MyApplication/EncryptDocument desde Acrobat](#rest-invocation-examples)).

Al utilizar solicitudes REST, se recomienda no invocar los servicios de Forms directamente. En su lugar, invoque los procesos creados en Workbench. Cuando cree un proceso diseñado para invocar a REST, utilice un punto de inicio programático. En este caso, el punto final REST se agrega automáticamente. Para obtener información sobre cómo crear procesos en Workbench, consulte [Usar Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Cuando invoca un servicio mediante REST, se le solicita un nombre de usuario y una contraseña de formularios AEM Forms. Sin embargo, si no desea especificar un nombre de usuario y una contraseña, puede deshabilitar la seguridad del servicio.

Para invocar un servicio de Forms (un proceso se convierte en servicio cuando se activa el proceso) mediante REST, configure un extremo REST. (Consulte &quot;Administración de extremos&quot; en la [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63)).

Una vez configurado un extremo REST, puede invocar un servicio de Forms mediante un método HTTP GET o un método POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

El valor `ServiceName` obligatorio es el nombre del servicio Forms que se va a invocar. El valor `OperationName` opcional es el nombre de la operación del servicio. Si no se especifica este valor, el valor predeterminado de este nombre es `invoke`, que es el nombre de la operación que inicia el proceso. El valor `ServiceVersion` opcional es la versión codificada en formato X.Y. Si no se especifica este valor, se utiliza la versión más actual. El valor `enctype` también puede ser `application/x-www-form-urlencoded`.

## Tipos de datos admitidos {#supported-data-types}

Se admiten los siguientes tipos de datos al invocar servicios de AEM Forms mediante solicitudes REST:

* Tipos de datos primitivos de Java, como cadenas y números enteros
* `com.adobe.idp.Document` tipo de datos
* Tipos de datos XML como `org.w3c.Document` y `org.w3c.Element`
* Objetos de colección como `java.util.List` y `java.util.Map`

  Estos tipos de datos se aceptan comúnmente como valores de entrada para los procesos creados en Workbench.

  Si se invoca un servicio Forms con el método HTTP POST, los argumentos se pasan dentro del cuerpo de la solicitud HTTP. Si la firma del servicio AEM Forms tiene un parámetro de entrada de cadena, el cuerpo de la solicitud puede contener el valor de texto del parámetro de entrada. Si la firma del servicio define varios parámetros de cadena, la solicitud puede seguir la notación `application/x-www-form-urlencoded` de HTTP con los nombres de parámetro utilizados como nombres de campo del formulario.

  Si un servicio de Forms devuelve un parámetro de cadena, el resultado es una representación textual del parámetro de salida. Si un servicio devuelve varios parámetros de cadena, el resultado es un documento XML que codifica los parámetros de salida en el siguiente formato:
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >El valor `output-paramater1` representa el nombre del parámetro de salida.

  Si un servicio de Forms requiere un parámetro `com.adobe.idp.Document`, el servicio sólo se puede invocar mediante el método HTTP POST. Si el servicio requiere un parámetro `com.adobe.idp.Document`, el cuerpo de la solicitud HTTP se convierte en el contenido del objeto de documento de entrada.

  Si un servicio de AEM Forms requiere varios parámetros de entrada, el cuerpo de la solicitud HTTP debe ser un mensaje MIME de varias partes, tal como se define en RFC 1867. (RFC 1867 es un estándar que utilizan los exploradores web para cargar archivos en sitios web). Cada parámetro de entrada debe enviarse como una parte independiente del mensaje multipart y codificarse en el formato `multipart/form-data`. El nombre de cada artículo debe coincidir con el nombre del parámetro.

  Las listas y los mapas también se utilizan como valores de entrada para los procesos de AEM Forms creados en Workbench. Como resultado, puede utilizar estos tipos de datos cuando utilice una solicitud REST. No se admiten matrices Java porque no se utilizan como valor de entrada para un proceso de AEM Forms.

  Si un parámetro de entrada es una lista, un cliente REST puede enviarla especificando el parámetro varias veces (una vez para cada elemento de la lista). Por ejemplo, si A es una lista de documentos, la entrada debe ser un mensaje de varias partes formado por varias partes denominadas A. En este caso, cada pieza denominada A se convierte en un elemento de la lista de entrada. Si B es una lista de cadenas, la entrada puede ser un mensaje `application/x-www-form-urlencoded` que consta de varios campos llamados B. En este caso, cada campo de formulario denominado B se convierte en un elemento de la lista de entrada.

  Si un parámetro de entrada es un mapa y es el parámetro de entrada solo de servicios, cada parte o campo del mensaje de entrada se convierte en un registro de clave o valor en el mapa. El nombre de cada parte/campo se convierte en la clave del registro. El contenido de cada parte/campo se convierte en el valor del registro.

  Si un mapa de entrada no es el parámetro de entrada solo de servicios, cada registro de clave/valor que pertenece al mapa se puede enviar utilizando un parámetro denominado como concatenación del nombre del parámetro y la clave del registro. Por ejemplo, se puede enviar un mapa de entrada denominado `attributes` con una lista de los siguientes pares clave/valores:

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  Esto se traduce en un mapa de tres registros: `Color=red`, `Shape=box` y `Width=5`.

  Los parámetros de salida de los tipos de lista y asignación pasan a formar parte del mensaje XML resultante. La lista de resultados se representa en XML como una serie de elementos XML con un elemento para cada elemento de la lista. A cada elemento se le asigna el mismo nombre que al parámetro de lista de salida. El valor de cada elemento XML es una de dos cosas:

* Una representación de texto del elemento de la lista (si la lista consta de tipos de cadena)
* Dirección URL que señala al contenido del documento (si la lista consta de `com.adobe.idp.Document` objetos)

  El siguiente ejemplo es un mensaje XML devuelto por un servicio que tiene un único parámetro de salida denominado *list*, que es una lista de enteros.
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`En el mensaje XML resultante se representa un parámetro de mapa de salida como una serie de elementos XML con un elemento para cada registro del mapa. A cada elemento se le asigna el mismo nombre que a la clave del registro de mapa. El valor de cada elemento es una representación textual del valor del registro del mapa (si el mapa consiste en registros con un valor de cadena) o una dirección URL que señala al contenido del documento (si el mapa consiste en registros con el valor `com.adobe.idp.Document`). A continuación se muestra un ejemplo de un mensaje XML devuelto por un servicio que tiene un único parámetro de salida denominado `map`. Este valor de parámetro es un mapa que consta de registros que asocian letras con `com.adobe.idp.Document` objetos.
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Invocaciones asincrónicas {#asynchronous-invocations}

Algunos servicios de AEM Forms, como los procesos de larga duración centrados en el ser humano, requieren mucho tiempo para completarse. Estos servicios se pueden invocar asincrónicamente de forma no bloqueante. (Consulte [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Se puede invocar un servicio de AEM Forms asincrónicamente reemplazando `services` con `async_invoke` en la dirección URL de invocación, como se muestra en el ejemplo siguiente.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Esta URL devuelve el valor del identificador (en formato &quot;text/plain&quot;) del trabajo responsable de esta invocación.

El estado de la invocación asincrónica se puede recuperar usando una URL de invocación con `services` sustituido por `async_status`. La dirección URL debe contener un parámetro `job_id` que especifique el valor del identificador del trabajo asociado con esta invocación. Por ejemplo:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Esta URL devuelve un valor entero (en formato &quot;texto/sin formato&quot;) que codifica el estado del trabajo según la especificación del Administrador de trabajos (por ejemplo, 2 significa en ejecución, 3 significa completado, 4 significa fallido, etc.).

Si se completa el trabajo, la dirección URL devuelve el mismo resultado que si el servicio se hubiera invocado sincrónicamente.

Una vez completado el trabajo y recuperado el resultado, el trabajo se puede eliminar usando una URL de invocación con `services` y se sustituye por `async_dispose`. La dirección URL también debe contener un parámetro `job_id` que especifique el valor del identificador del trabajo. Por ejemplo:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Si el trabajo se elimina correctamente, esta dirección URL devuelve un mensaje vacío.

## Informes de errores {#error-reporting}

Si no se puede completar una solicitud de invocación sincrónica o asincrónica debido a que se está iniciando una excepción en el servidor, la excepción se comunica como parte del mensaje de respuesta HTTP. Si la dirección URL de invocación (o la dirección URL `async_result` si hay una invocación asincrónica) no tiene un sufijo .xml, el proveedor REST devuelve el código HTTP `500 Internal Server Error` seguido de un mensaje de excepción.

Si la dirección URL de invocación (o la dirección URL `async_result` si hay una invocación asincrónica) tiene un sufijo .xml, el proveedor de REST devuelve el código HTTP `200 OK` seguido de un documento XML que describe la excepción en el siguiente formato.

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

El elemento `DSCError` es opcional y está presente solamente si la excepción es una instancia de `com.adobe.idp.dsc.DSCException`.

## Seguridad y autenticación {#security-and-authentication}

Para proporcionar a las invocaciones de REST un transporte seguro, un administrador de formularios de AEM puede habilitar el protocolo HTTPS en el servidor de aplicaciones J2EE que aloja AEM Forms. Esta configuración es específica del servidor de aplicaciones J2EE; no forma parte de la configuración del servidor de Forms.

>[!NOTE]
>
>Como desarrollador de Workbench que desea exponer sus procesos a través de un extremo REST, tenga en cuenta el problema de vulnerabilidad XSS. Las vulnerabilidades XSS se pueden utilizar para robar o manipular cookies, modificar la presentación del contenido y comprometer la información confidencial. Se recomienda ampliar la lógica de proceso con las reglas de validación de datos de entrada y salida adicionales si la vulnerabilidad XSS es un problema.

## Servicios de AEM Forms compatibles con la invocación de REST {#aem-forms-services-that-support-rest-invocation}

Aunque se recomienda invocar directamente los procesos creados con Workbench en lugar de los servicios de, hay algunos servicios de AEM Forms que no admiten la invocación de REST. El motivo por el que se recomienda invocar un proceso directamente en lugar de un servicio es porque es más eficiente invocar un proceso. Considere el siguiente escenario. Supongamos que desea crear una directiva a partir de un cliente REST. Es decir, desea que el cliente REST defina valores como el nombre de la directiva o el período de concesión sin conexión.

Para crear una directiva, debe definir tipos de datos complejos como un objeto `PolicyEntry`. Un objeto `PolicyEntry` define atributos como permisos asociados a la directiva. (Consulte [Creación de directivas](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

En lugar de enviar una solicitud REST para crear una directiva (que incluiría la definición de tipos de datos complejos como un objeto `PolicyEntry`), cree un proceso que cree una directiva mediante Workbench. Defina el proceso para aceptar variables de entrada primitivas, como un valor de cadena que defina el nombre del proceso o un entero que defina el período de concesión sin conexión.

De este modo, no es necesario crear una solicitud de invocación de REST que incluya tipos de datos complejos que requiere la operación. El proceso define los tipos de datos complejos y todo lo que hace desde el cliente REST es invocar el proceso y pasar tipos de datos primitivos. Para obtener información acerca de cómo invocar un proceso mediante REST, vea [Invocar el proceso MyApplication/EncryptDocument mediante REST](#rest-invocation-examples).

Las siguientes listas especifican los servicios de AEM Forms que admiten la invocación directa de REST.

* servicio de Distiller
* servicio de Rights Management
* Servicio GeneratePDF
* Servicio Generate3dPDF
* FormDataIntegration

## Ejemplos de invocación de REST {#rest-invocation-examples}

Se proporcionan los siguientes ejemplos de invocación de REST:

* Pasar valores booleanos a un proceso de AEM Forms
* Pasar valores de fecha a un proceso de AEM Forms
* Pasar documentos a un proceso de AEM Forms
* Pasar valores de documento y texto a un proceso de AEM Forms
* Pasar valores de enumeración a un proceso de AEM Forms
* Invocar el proceso MyApplication/EncryptDocument mediante REST
* Invocar el proceso MyApplication/EncryptDocument desde Acrobat

  En cada ejemplo se muestra cómo pasar distintos tipos de datos a un proceso de AEM Forms

**Pasar valores booleanos a un proceso**

El siguiente ejemplo de HTML pasa dos valores `Boolean` a un proceso de AEM Forms denominado `RestTest2`. El nombre del método de invocación es `invoke` y la versión es 1.0. Observe que se utiliza el método HTML Post.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de fecha a un proceso**

El siguiente ejemplo de HTML pasa un valor de fecha a un proceso de AEM Forms denominado `SOAPEchoService`. El nombre del método de invocación es `echoCalendar`. Observe que se utiliza el método HTML `Post`.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Pasar documentos a un proceso**

El siguiente ejemplo de HTML invoca un proceso de AEM Forms denominado `MyApplication/EncryptDocument` que requiere un documento de PDF. Para obtener información acerca de este proceso, vea [Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de documento y texto a un proceso**

En el siguiente ejemplo de HTML se invoca un proceso de AEM Forms denominado `RestTest3` que requiere un documento y dos valores de texto. Observe que se utiliza el método HTML Post.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Pasar valores de enumeración a un proceso**

El siguiente ejemplo de HTML invoca un proceso de AEM Forms denominado `SOAPEchoService` que requiere un valor de enumeración. Observe que se utiliza el método HTML Post.

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Invocando el proceso MyApplication/EncryptDocument mediante REST**

Puede invocar un proceso de corta duración de AEM Forms denominado *MyApplication/EncryptDocument* mediante REST.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

   Cuando se invoca este proceso mediante una solicitud REST, el documento PDF cifrado se muestra en el explorador web. Antes de ver el documento de PDF, especifique la contraseña (a menos que la seguridad esté deshabilitada). El siguiente código HTML representa una solicitud de invocación de REST para el proceso `MyApplication/EncryptDocument`.

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Invocando el proceso MyApplication/EncryptDocument desde Acrobat** {#invoke-process-acrobat}

Puede invocar un proceso de Forms desde Acrobat mediante una solicitud REST. Por ejemplo, puede invocar el proceso *MyApplication/EncryptDocument*. Para invocar un proceso de Forms desde Acrobat, coloque un botón de envío en un archivo XDP dentro de Designer. (Consulte [Ayuda de Designer](https://www.adobe.com/go/learn_aemforms_designer_63)).

Especifique la URL para invocar el proceso en el campo *Enviar a la URL* del botón, como se muestra en la siguiente ilustración.

La dirección URL completa para invocar el proceso es https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Si el proceso requiere un documento de PDF como valor de entrada, asegúrese de enviar el formulario como PDF, como se muestra en la ilustración anterior. Además, para invocar correctamente un proceso, el proceso debe devolver un documento de PDF. De lo contrario, Acrobat no podrá controlar el valor devuelto y se producirá un error. No es necesario especificar el nombre de la variable del proceso de entrada. Por ejemplo, el proceso *MyApplication/EncryptDocument* tiene una variable de entrada denominada `inDoc`. No es necesario especificar inDoc, siempre y cuando el formulario se envíe como PDF.

También puede enviar datos de formulario como XML a un proceso de Forms. Para enviar datos XML, asegúrese de que la lista desplegable `Submit As` especifique XML. Dado que el valor devuelto del proceso debe ser un documento de PDF, el documento de PDF se muestra en Acrobat.
