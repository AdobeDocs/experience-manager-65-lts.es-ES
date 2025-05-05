---
title: Invocar AEM Forms mediante Remoting
description: Utilice la comunicación remota para invocar un proceso de AEM Forms e invocar procesos creados en Workbench. Puede invocar un proceso de AEM Forms desde una aplicación cliente creada con Flex.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Workbench
hide: true
hidefromtoc: true
exl-id: 37f5efaa-db0b-4035-987d-4140fc5a97be
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '4604'
ht-degree: 1%

---

# Invocar AEM Forms mediante Remoting {#invoking-aem-forms-using-remoting}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Los procesos creados en Workbench se pueden invocar mediante Remoting. Es decir, puede invocar un proceso de AEM Forms desde una aplicación cliente creada con Flex. Esta función se basa en los servicios de datos.

>[!NOTE]
>
>Al utilizar la comunicación remota, se recomienda invocar procesos creados en Workbench en lugar de servicios de AEM Forms. Sin embargo, es posible invocar los servicios de AEM Forms directamente. (Consulte Cifrado de documentos de PDF mediante Remoting, ubicado en AEM Forms Developer Center).

>[!NOTE]
>
>Si un servicio de AEM Forms no está configurado para permitir el acceso anónimo, las solicitudes de un cliente de Flex resultan en un desafío para el explorador web. El usuario debe introducir las credenciales de nombre de usuario y contraseña.

El siguiente proceso de corta duración de AEM Forms, denominado `MyApplication/EncryptDocument`, se puede invocar mediante Remoting. (Para obtener información acerca de este proceso, como sus valores de entrada y salida, vea [Ejemplo de proceso de corta duración](/help/forms/developing/aem-forms-processes.md)).

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Para invocar un proceso de AEM Forms mediante una aplicación de Flex, asegúrese de que esté habilitado un extremo remoto. De forma predeterminada, se habilita un extremo remoto al implementar un proceso.

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa como valor de entrada. Esta acción se basa en la operación `SetValue`. El nombre del parámetro de entrada es `inDoc` y su tipo de datos es `document`. (El tipo de datos `document` es un tipo de datos disponible desde Workbench).
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El nombre del valor de salida de este proceso es `outDoc` y representa el documento de PDF cifrado con contraseña. El tipo de datos de outDoc es `document`.
1. Guarda el documento de PDF cifrado con contraseña como un archivo PDF en el sistema de archivos local. Esta acción se basa en la operación `WriteDocument`.

>[!NOTE]
>
>El proceso `MyApplication/EncryptDocument` no se basa en un proceso de AEM Forms existente. Para continuar con los ejemplos de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench.

>[!NOTE]
>
>Para obtener información acerca del uso de Remoting para invocar un proceso de larga duración, vea [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**Consulte también**

[Inclusión del archivo de biblioteca Flex de AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Administrar documentos con (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticación de aplicaciones cliente creadas con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Invocar servicios de componentes personalizados mediante Remoting](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Creación de una aplicación cliente creada con Flex que invoca un proceso de larga duración centrado en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Crear aplicaciones de Flash Builder que realizan autenticación SSO mediante tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*Asegúrese de colocar el archivo cross-domain.xml en el lugar adecuado. Por ejemplo, suponiendo que ha implementado AEM Forms en JBoss, coloque este archivo en la siguiente ubicación: &lt;directorio_instalación>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Inclusión del archivo de biblioteca Flex de AEM Forms {#including-the-aem-forms-flex-library-file}

Para invocar mediante programación los procesos de AEM Forms mediante Remoting, agregue el archivo adobe-remoting-provider.swc a la ruta de clase del proyecto de Flex. Este archivo SWC se encuentra en la siguiente ubicación:

* *&lt;directorio_instalación>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

  donde &lt;*install_directory*> es el directorio donde está instalado AEM Forms.

**Consulte también**

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Administrar documentos con (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticación de aplicaciones cliente creadas con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Administrar documentos con Remoting {#handling-documents-with-remoting}

Uno de los tipos Java™ no primitivos más importantes que se utiliza en AEM Forms es la clase `com.adobe.idp.Document`. Normalmente, se requiere un documento para invocar una operación de AEM Forms. Es principalmente un documento de PDF, pero puede contener otros tipos de documento como SWF, HTML, XML o un archivo DOC. (Consulte [Pasar datos a servicios de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Una aplicación cliente creada con Flex no puede solicitar directamente un documento. Por ejemplo, no se puede iniciar Adobe Reader para solicitar una dirección URL que produzca un archivo PDF. Las solicitudes de tipos de documento, como los documentos de PDF y Microsoft® Word, devuelven un resultado que es una dirección URL. Es responsabilidad del cliente mostrar el contenido de la dirección URL. El servicio Administración de documentos ayuda a generar la dirección URL y la información de tipo de contenido. Las solicitudes de documentos XML devuelven el documento XML completo en el resultado.

### Pasar un documento como parámetro de entrada {#passing-a-document-as-an-input-parameter}

Una aplicación cliente creada con Flex no puede pasar un documento directamente a un proceso de AEM Forms. En su lugar, la aplicación cliente utiliza una instancia de la clase ActionScript `mx.rpc.livecycle.DocumentReference` para pasar parámetros de entrada a una operación que espera una instancia `com.adobe.idp.Document`. Una aplicación cliente de Flex tiene varias opciones para configurar un objeto `DocumentReference`:

* Cuando el documento esté en el servidor y se conozca su ubicación de archivo, establezca la propiedad referenceType del objeto DocumentReference en REF_TYPE_FILE. Establezca la propiedad fileRef en la ubicación del archivo, como se muestra en el siguiente ejemplo:

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Cuando el documento se encuentra en el servidor y conoce su dirección URL, establezca la propiedad referenceType del objeto DocumentReference en REF_TYPE_URL. Establezca la propiedad url en la dirección URL, como se muestra en el siguiente ejemplo:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Para crear un objeto DocumentReference a partir de una cadena de texto en la aplicación cliente, establezca la propiedad referenceType del objeto DocumentReference en REF_TYPE_INLINE. Establezca la propiedad text en el texto que desea incluir en el objeto, como se muestra en el siguiente ejemplo:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Cuando el documento no esté en el servidor, utilice el servlet de carga remota para cargar un documento en AEM Forms. Una novedad en AEM Forms es la capacidad de cargar documentos seguros. Al cargar un documento seguro, debe utilizar un usuario que tenga la función *Usuario de aplicación de carga de documentos*. Sin esta función, el usuario no puede cargar un documento seguro. Se recomienda utilizar el inicio de sesión único para cargar un documento seguro. (Consulte [Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)).

>[!NOTE]
>
>si AEM Forms está configurado para permitir la carga de documentos no seguros, puede utilizar un usuario que no tenga la función de usuario de la aplicación Document Upload para cargar un documento. Un usuario también puede tener el permiso de carga de documento. Sin embargo, si AEM Forms está configurado para permitir solo documentos seguros, asegúrese de que el usuario tenga la función de usuario de la aplicación de carga de documentos o el permiso de carga de documentos. (Consulte [Configuración de AEM Forms para aceptar documentos seguros y no seguros](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

Utiliza las funciones de carga estándar de Flash para la dirección URL de carga designada: `https://SERVER:PORT/remoting/lcfileupload`. Puede usar el objeto `DocumentReference` siempre que se espere un parámetro de entrada de tipo `Document`
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`El Inicio rápido de Remoting usa el servlet de carga Remoting para pasar un archivo PDF al proceso `MyApplication/EncryptDocument`. (Consulte [Invocar un proceso de corta duración al pasar un documento no seguro mediante (Obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

Inicio rápido Remoting usa el servlet de carga Remoting para pasar un archivo PDF al proceso `MyApplication/EncryptDocument`. (Consulte [Invocar un proceso de corta duración al pasar un documento no seguro mediante (Obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)).)

### Volver a pasar un documento a una aplicación cliente {#passing-a-document-back-to-a-client-application}

Una aplicación cliente recibe un objeto de tipo `mx.rpc.livecycle.DocumentReference` para una operación de servicio que devuelve una instancia `com.adobe.idp.Document` como parámetro de salida. Dado que una aplicación cliente trata de objetos ActionScript y no de Java, no puede devolver un objeto Document basado en Java a un cliente de Flex. En su lugar, el servidor genera una dirección URL para el documento y la devuelve al cliente. La propiedad `referenceType` del objeto `DocumentReference` especifica si el contenido se encuentra en el objeto `DocumentReference` o si debe recuperarse de una dirección URL de la propiedad `DocumentReference.url`. La propiedad `DocumentReference.contentType` especifica el tipo de documento.

**Consulte también**

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Inclusión del archivo de biblioteca Flex de AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticación de aplicaciones cliente creadas con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Invocar un proceso de corta duración pasando un documento no seguro mediante Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Para invocar un proceso de AEM Forms desde una aplicación creada con Flex, realice las siguientes tareas:

1. Crear una instancia de `mx:RemoteObject`.
1. Crear una instancia de `ChannelSet`.
1. Pasar los valores de entrada necesarios.
1. Gestionar valores devueltos.

>[!NOTE]
>
>En esta sección se explica cómo invocar un proceso de AEM Forms y cargar un documento cuando AEM Forms está configurado para cargar documentos no seguros. Para obtener información sobre cómo invocar procesos de AEM Forms y cargar documentos seguros, y cómo configurar AEM Forms para que acepte documentos seguros y no seguros, vea [Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**Creando una instancia mx:RemoteObject**

Cree una instancia de `mx:RemoteObject` para invocar un proceso de AEM Forms creado en Workbench. Para crear una instancia de `mx:RemoteObject`, especifique los siguientes valores:

* **id:** El nombre de la instancia de `mx:RemoteObject` que representa el proceso que se va a invocar.
* **destino:** Nombre del proceso de AEM Forms que se va a invocar. Por ejemplo, para invocar el proceso `MyApplication/EncryptDocument`, especifique `MyApplication/EncryptDocument`.
* **resultado:** Nombre del método Flex que administra el resultado.

En la etiqueta `mx:RemoteObject`, especifique una etiqueta `<mx:method>` que especifique el nombre del método de invocación del proceso. Normalmente, el nombre de un método de invocación de Forms es `invoke`.

En el ejemplo de código siguiente se crea una instancia de `mx:RemoteObject` que invoca el proceso `MyApplication/EncryptDocument`.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Crear un canal con AEM Forms**

Una aplicación cliente puede invocar AEM Forms especificando un Channel en MXML o ActionScript, como se muestra en el siguiente ejemplo de ActionScript. El canal debe ser un `AMFChannel`, `SecureAMFChannel`, `HTTPChannel` o `SecureHTTPChannel`.

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

Asigne la instancia `ChannelSet` al campo `channelSet` de la instancia `mx:RemoteObject` (como se muestra en el ejemplo de código anterior). Por lo general, se importa la clase channel en una instrucción import en lugar de especificar el nombre completo cuando se invoca el método `ChannelSet.addChannel`.

**Pasar valores de entrada**

Un proceso creado en Workbench puede tener cero o más parámetros de entrada y devolver un valor de salida. Una aplicación cliente pasa parámetros de entrada dentro de un objeto `ActionScript` con campos que corresponden a parámetros que pertenecen al proceso de AEM Forms. El proceso de corta duración denominado `MyApplication/EncryptDocument` requiere un parámetro de entrada denominado `inDoc`. El nombre de la operación expuesta por el proceso es `invoke` (el nombre predeterminado para un proceso de corta duración). (Consulte [Invocación de AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)).

En el ejemplo de código siguiente se pasa un documento de PDF al proceso `MyApplication/EncryptDocument`:

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

En este ejemplo de código, `pdfDocument` es una instancia de `DocumentReference` que contiene un documento de PDF no protegido. Para obtener información sobre un(a) `DocumentReference`, consulte [Administración de documentos con (obsoleto para formularios AEM) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**Invocando una versión específica de un servicio**

Puede invocar una versión específica de un servicio de Forms utilizando un parámetro `_version` en la asignación de parámetros de la invocación. Por ejemplo, para invocar la versión 1.2 del servicio `MyApplication/EncryptDocument`:

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

El parámetro `version` debe ser una cadena que contenga un solo punto. Los valores a la izquierda, versión principal y derecha, versión secundaria, del punto deben ser enteros. Si no se especifica este parámetro, se invoca la versión activa del encabezado.

**Administrar valores devueltos**

Los parámetros de salida de proceso de AEM Forms se deserializan en objetos ActionScript de los que la aplicación cliente extrae parámetros específicos por nombre, como se muestra en el ejemplo siguiente. (El valor de salida del proceso `MyApplication/EncryptDocument` se denomina `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Invocando el proceso MyApplication/EncryptDocument**

Puede invocar el proceso `MyApplication/EncryptDocument` realizando los siguientes pasos:

1. Cree una instancia de `mx:RemoteObject` mediante ActionScript o MXML. Consulte Creación de una instancia mx:RemoteObject.
1. Configure una instancia de `ChannelSet` para comunicarse con AEM Forms y asóciela a la instancia `mx:RemoteObject`. Consulte Creación de un canal a AEM Forms.
1. Llame al método `login` del ChannelSet o al método `setCredentials` del servicio para especificar el valor del identificador de usuario y la contraseña. (Consulte [Uso del inicio de sesión único](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Rellene una instancia de `mx.rpc.livecycle.DocumentReference` con un documento de PDF no protegido para pasarlo al proceso `MyApplication/EncryptDocument`. (Vea [Pasar un documento como parámetro de entrada](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. Cifre el documento de PDF llamando al método `invoke` de la instancia `mx:RemoteObject`. Pase el `Object` que contiene el parámetro de entrada (que es el documento de PDF no protegido). Consulte Pasar valores de entrada.
1. Recupere el documento de PDF cifrado con contraseña que devuelve el proceso. Consulte Gestión de valores devueltos.

[Inicio rápido: invocar un proceso de corta duración al pasar un documento no seguro mediante (obsoleto para formularios AEM) AEM Forms Remoting](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Autenticación de aplicaciones cliente creadas con Flex {#authenticating-client-applications-built-with-flex}

Existen varias formas en las que el administrador de usuarios de formularios AEM Forms puede autenticar una solicitud de Remoting desde una aplicación de Flex, incluido el inicio de sesión único de AEM Forms a través del servicio de inicio de sesión central, la autenticación básica y la autenticación personalizada. Cuando no se habilita el inicio de sesión único ni el acceso anónimo, una solicitud de Remoting genera autenticación básica (predeterminada) o personalizada.

La autenticación básica se basa en la autenticación básica J2EE estándar del contenedor de aplicaciones web. Para la autenticación básica, un error HTTP 401 provoca un desafío del explorador. Esto significa que cuando intenta conectarse a una aplicación de Forms mediante RemoteObject y aún no ha iniciado sesión desde la aplicación de Flex, el explorador le pide un nombre de usuario y una contraseña.

Para la autenticación personalizada, el servidor envía un error al cliente para indicar que se requiere autenticación.

>[!NOTE]
>
>Para obtener información sobre cómo realizar la autenticación mediante tokens HTTP, consulte [Creación de aplicaciones de Flash Builder que realizan autenticación SSO mediante tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### Uso de la autenticación personalizada {#using-custom-authentication}

Para habilitar la autenticación personalizada en la consola de administración, cambie el método de autenticación de Básico a Personalizado en el extremo remoto. Si usa autenticación personalizada, la aplicación cliente llama al método `ChannelSet.login` para iniciar sesión y al método `ChannelSet.logout` para cerrar sesión.

>[!NOTE]
>
>En la versión anterior de AEM Forms, enviaba credenciales a un destino llamando al método `RemoteObject.setCredentials`. El método `setCredentials` no pasó realmente las credenciales al servidor hasta el primer intento del componente de conectarse al servidor. Por lo tanto, si el componente emite un evento de error, no puede estar seguro de si el error se produjo debido a un error de autenticación o por otro motivo. El método `ChannelSet.login` se conecta al servidor cuando lo llama para que pueda controlar un problema de autenticación inmediatamente. Aunque puede seguir utilizando el método `setCredentials`, se recomienda utilizar el método `ChannelSet.login`.

Dado que varios destinos pueden utilizar los mismos canales y el objeto ChannelSet correspondiente, al iniciar sesión en un destino, el usuario inicia sesión en cualquier otro destino que utilice el mismo canal o canales. Si dos componentes aplican credenciales diferentes al mismo objeto ChannelSet, se utilizan las últimas credenciales aplicadas. Si varios componentes utilizan el mismo objeto ChannelSet autenticado, al llamar al método `logout` se cierra la sesión de todos los componentes de los destinos.

El ejemplo siguiente utiliza los métodos `ChannelSet.login` y `ChannelSet.logout` con un control RemoteObject. Esta aplicación realiza las siguientes acciones:

* Crea un objeto `ChannelSet` en el controlador `creationComplete` que representa los canales utilizados por el componente `RemoteObject`
* Pasa credenciales al servidor llamando a la función `ROLogin` en respuesta a un evento de clic en botón
* Utiliza el componente RemoteObject para enviar un objeto String al servidor en respuesta a un evento Button click. El servidor devuelve el mismo valor String al componente RemoteObject
* Utiliza el evento result del componente RemoteObject para mostrar el valor String en un control TextArea
* Cierra la sesión del servidor llamando a la función `ROLogout` en respuesta a un evento de clic en botón

```java
 <?xml version="1.0"?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx="https://www.adobe.com/2006/mxml" width="100%"
     height="100%" creationComplete="creationCompleteHandler();">
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login("sampleuser", "samplepassword");
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case "success":
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case "Client.Authentication":
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show("Login failure: " + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case "success":
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show("Logout failure: " + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += "Server responded: "+ event.result + "\n";
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += "Received fault: " + event.fault + "\n";
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text="Enter a text for the server to echo"/>
         <mx:TextInput id="ti" text="Hello World!"/>
         <mx:Button label="Login"
             click="ROLogin();"/>
         <mx:Button label="Echo"
             enabled="{authenticatedCB.selected}"
             click="remoteObject.echo(ti.text);"/>
         <mx:Button label="Logout"
             click="ROLogout();"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
     <mx:TextArea id="ta" width="100%" height="100%"/>
 
     <mx:RemoteObject id="remoteObject"
         destination="myDest"
         result="resultHandler(event);"
         fault="faultHandler(event);"/>
 </mx:Application>
```

Los métodos `login` y `logout` devuelven un objeto AsyncToken. Asigne controladores de eventos al objeto AsyncToken para que el evento de resultado controle una llamada correcta y para que el evento de error controle un error.

### Usar el inicio de sesión único {#using-single-sign-on}

Los usuarios de formularios AEM Forms pueden conectarse a varias aplicaciones web de AEM Forms para realizar una tarea. A medida que los usuarios pasan de una aplicación web a otra, no es eficiente pedirles que inicien sesión por separado en cada aplicación web. El mecanismo de inicio de sesión único de AEM Forms permite a los usuarios iniciar sesión una vez y, a continuación, acceder a cualquier aplicación web de AEM Forms. Dado que los desarrolladores de AEM Forms pueden crear aplicaciones cliente para utilizarlas con AEM Forms, también deben poder aprovechar el mecanismo de inicio de sesión único.

Cada aplicación web de AEM Forms está empaquetada en su propio archivo web (WAR), que a continuación se empaqueta como parte de un archivo Enterprise Archive (EAR). Dado que un servidor de aplicaciones no permite compartir datos de sesión entre distintas aplicaciones web, AEM Forms utiliza cookies HTTP para almacenar información de autenticación. Las cookies de autenticación permiten al usuario iniciar sesión en una aplicación de Forms y, a continuación, conectarse a otras aplicaciones web de AEM Forms. Esta técnica se conoce como inicio de sesión único.

Los desarrolladores de AEM Forms escriben aplicaciones cliente para ampliar la funcionalidad de las guías del formulario (obsoletas) y personalizar Workspace. Por ejemplo, una aplicación de Workspace puede iniciar un proceso. A continuación, la aplicación cliente utiliza un extremo remoto para recuperar datos del servicio de Forms.

Cuando se invoca un servicio de AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting, la aplicación cliente pasa la cookie de autenticación como parte de la solicitud. Como el usuario ya se ha autenticado, no se requiere ningún inicio de sesión adicional para establecer una conexión desde la aplicación cliente al servicio de AEM Forms.

>[!NOTE]
>
>Si una cookie no es válida o falta, no hay ninguna redirección implícita a una página de inicio de sesión. Por lo tanto, aún puede llamar a un servicio anónimo.

Puede evitar el mecanismo de inicio de sesión único de AEM Forms escribiendo una aplicación cliente que inicie y cierre la sesión por su cuenta. Si omite el mecanismo de inicio de sesión único, puede utilizar la autenticación básica o personalizada con la aplicación.

Dado que este mecanismo no utiliza el mecanismo de inicio de sesión único de AEM Forms, no se escribe ninguna cookie de autenticación en el cliente. Las credenciales de inicio de sesión se almacenan en el objeto `ChannelSet` para el canal remoto. Por lo tanto, cualquier llamada de `RemoteObject` que realice sobre el mismo `ChannelSet` se realizará en el contexto de esas credenciales.

### Configuración del inicio de sesión único en AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Para utilizar el inicio de sesión único en AEM Forms, instale el componente de flujo de trabajo de Forms, que incluye el servicio de inicio de sesión centralizado. Cuando un usuario inicia sesión correctamente, el servicio de inicio de sesión centralizado devuelve una cookie de autenticación al usuario. Cada solicitud posterior a una aplicación web de Forms contiene la cookie. Si la cookie es válida, se considera que el usuario está autenticado y no tiene que volver a iniciar sesión.

### Escribir una aplicación cliente que utilice el inicio de sesión único {#writing-a-client-application-that-uses-single-sign-on}

Cuando se aprovecha el mecanismo de inicio de sesión único, se espera que los usuarios inicien sesión utilizando el servicio de inicio de sesión centralizado antes de iniciar una aplicación cliente. Es decir, una aplicación cliente no inicia sesión a través del explorador o llamando al método `ChannelSet.login`.

Si utiliza el mecanismo de inicio de sesión único de AEM Forms, configure el extremo remoto para que utilice autenticación personalizada, no básica. De lo contrario, cuando se utiliza la autenticación básica, un error de autenticación provoca un desafío del explorador, que no desea que el usuario vea. En su lugar, la aplicación detecta el error de autenticación y, a continuación, muestra un mensaje que indica al usuario que inicie sesión mediante el servicio de inicio de sesión centralizado.

Una aplicación cliente tiene acceso a AEM Forms a través de un extremo remoto mediante el componente `RemoteObject`, como se muestra en el ejemplo siguiente.

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Iniciando sesión como un nuevo usuario mientras la aplicación Flex aún se está ejecutando**

Una aplicación creada con Flex incluye la cookie de autenticación con cada solicitud a un servicio de AEM Forms. Por motivos de rendimiento, AEM Forms no valida la cookie en cada solicitud. Sin embargo, AEM Forms detecta cuándo se sustituye una cookie de autenticación por otra cookie de autenticación.

Por ejemplo, inicia una aplicación cliente y mientras la aplicación está activa, utiliza el servicio de inicio de sesión centralizado para cerrar la sesión. A continuación, puede iniciar sesión como un usuario diferente. Al iniciar sesión como un usuario diferente, se sustituye la cookie de autenticación existente por una cookie de autenticación para el nuevo usuario.

En la siguiente solicitud de la aplicación cliente, AEM Forms detecta que la cookie ha cambiado y cierra la sesión del usuario. Por lo tanto, falla la primera solicitud después de un cambio de cookie. Todas las solicitudes posteriores se realizan en el contexto de la nueva cookie y se procesan correctamente.

**Cerrando sesión**

Para cerrar la sesión de AEM Forms e invalidar una sesión, la cookie de autenticación debe eliminarse del equipo del cliente. Dado que el propósito del inicio de sesión único es permitir que un usuario inicie sesión una vez, no desea que una aplicación cliente elimine la cookie. Esta acción cierra la sesión del usuario de forma efectiva.

Por lo tanto, llamar al método `RemoteObject.logout` en una aplicación cliente genera un mensaje de error en el cliente especificando que la sesión no se ha cerrado. En su lugar, el usuario puede utilizar el servicio de inicio de sesión centralizado para cerrar la sesión y eliminar la cookie de autenticación.

**Se está cerrando la sesión mientras la aplicación Flex aún se está ejecutando**

Puede iniciar una aplicación cliente creada con Flex y utilizar el servicio de inicio de sesión centralizado para cerrar la sesión. Como parte del proceso de cierre de sesión, se elimina la cookie de autenticación. Si se realiza una solicitud remota sin una cookie o con una cookie no válida, la sesión del usuario se invalida. Esta acción es, en efecto, un cierre de sesión. La próxima vez que la aplicación cliente intente conectarse a un servicio de AEM Forms, se solicitará al usuario que inicie sesión.

**Consulte también**

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Administrar documentos con (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusión del archivo de biblioteca Flex de AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Pasar documentos seguros para invocar procesos mediante Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}

Puede pasar documentos seguros a AEM Forms al invocar un proceso que requiere uno o más documentos. Al pasar un documento seguro, protege la información comercial y los documentos confidenciales. En este caso, un documento puede hacer referencia a un documento de PDF, a un documento XML, a un documento de Word, etc. La transferencia de un documento seguro a AEM Forms desde una aplicación de cliente escrita en Flex es necesaria cuando AEM Forms está configurado para permitir documentos seguros. (Consulte [Configuración de AEM Forms para aceptar documentos seguros y no seguros](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)).

Al pasar un documento seguro, utilice el inicio de sesión único y especifique un usuario de formularios AEM Forms que tenga la función *Usuario de aplicación de carga de documentos*. Sin esta función, el usuario no puede cargar un documento seguro. Puede asignar mediante programación una función a un usuario. (Consulte [Administración de roles y permisos](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
>
>Cuando cree una función y desee que sus miembros carguen documentos seguros, asegúrese de especificar el permiso de carga de documentos.

AEM Forms admite una operación denominada `getFileUploadToken` que devuelve un token que se pasa al servlet de carga. El método `DocumentReference.constructRequestForUpload` requiere una dirección URL para AEM Forms junto con el token devuelto por el método `LC.FileUploadAuthenticator.getFileUploadToken`. Este método devuelve un objeto `URLRequest` que se usa en la invocación al servlet de carga. El código siguiente muestra esta lógica de aplicación.

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### Configuración de AEM Forms para aceptar documentos seguros y no seguros {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

Puede utilizar la consola de administración para especificar si los documentos son seguros al pasar un documento de una aplicación cliente de Flex a un proceso de AEM Forms. De forma predeterminada, AEM Forms está configurado para aceptar documentos seguros. Puede configurar AEM Forms para que acepte documentos seguros realizando los siguientes pasos:

1. Inicie sesión en la consola de administración.
1. Haga clic en **Configuración**.
1. Haga clic en **Configuración del sistema principal.**
1. Haga clic en Configuraciones.
1. Asegúrese de que la opción Permitir la carga de documentos no seguros desde aplicaciones de Flex no esté seleccionada.

>[!NOTE]
>
>* Para configurar AEM Forms para que acepte documentos no seguros, seleccione la opción Permitir la carga de documentos no seguros desde aplicaciones de Flex. A continuación, reinicie una aplicación o servicio para asegurarse de que la configuración surta efecto.
>* Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.


### Inicio rápido: invocar un proceso de corta duración pasando un documento seguro mediante Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

El siguiente ejemplo de código invoca el `MyApplication/EncryptDocument.`Un usuario debe iniciar sesión para hacer clic en el botón Seleccionar archivo que se utiliza para cargar un archivo PDF e invocar el proceso. Es decir, una vez que el usuario está autenticado, el botón Seleccionar archivo está habilitado. La siguiente ilustración muestra la aplicación cliente de Flex después de que un usuario se autentique. Observe que la casilla de verificación Autenticado está habilitada.

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

si AEM Forms está configurado para permitir que solo se carguen documentos seguros y el usuario no tiene el rol *Usuario de aplicación de carga de documentos*, se generará una excepción. Si el usuario tiene esta función, el archivo se carga y se invoca el proceso.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef's url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**Consulte también**

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Administrar documentos con (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusión del archivo de biblioteca Flex de AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticación de aplicaciones cliente creadas con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Invocar servicios de componentes personalizados mediante Remoting {#invoking-custom-component-services-using-remoting}

Puede invocar servicios en un componente personalizado mediante Remoting. Por ejemplo, considere el componente Banco que contiene el Servicio de atención al cliente. Puede invocar operaciones que pertenecen al servicio de atención al cliente mediante una aplicación cliente escrita en Flex. Para poder ejecutar el inicio rápido asociado a esta sección, debe crear el componente personalizado Banco.

El servicio de atención al cliente expone una operación denominada `createCustomer`. En esta discusión se describe cómo crear una aplicación cliente de Flex que invoque el servicio de atención al cliente y cree un cliente. Esta operación requiere un objeto complejo de tipo `com.adobe.livecycle.sample.customer.Customer` que representa al nuevo cliente. La siguiente ilustración muestra la aplicación cliente que invoca el servicio de atención al cliente y crea un cliente nuevo. La operación `createCustomer` devuelve un valor de identificador de cliente. El valor del identificador se muestra en el cuadro de texto Identificador de cliente.

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

En la tabla siguiente se enumeran los controles que forman parte de esta aplicación cliente.

<table>
 <thead>
  <tr>
   <th><p>Nombre del control</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>Especifica el nombre del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>Especifica el apellido del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>Especifica el número de teléfono del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>Especifica el nombre de la calle del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>Especifica el estado del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>Especifica el código postal del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>Especifica la ciudad del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtCustomerId</p></td>
   <td><p>Especifica el valor del identificador de cliente al que pertenece la nueva cuenta. Este cuadro de texto se completa con el valor devuelto por la operación <code>createCustomer</code> del servicio de atención al cliente. </p></td>
  </tr>
 </tbody>
</table>

### Asignación de tipos de datos complejos de AEM Forms {#mapping-aem-forms-complex-data-types}

Algunas operaciones de AEM Forms requieren tipos de datos complejos como valores de entrada. Estos tipos de datos complejos definen los valores en tiempo de ejecución utilizados por la operación. Por ejemplo, la operación `createCustomer` del servicio de atención al cliente requiere una instancia de `Customer` que contiene los valores de tiempo de ejecución requeridos por el servicio. Sin el tipo complejo, el servicio de atención al cliente genera una excepción y no realiza la operación.

Al invocar un servicio de AEM Forms, cree objetos ActionScript que se asignen a tipos complejos AEM Forms necesarios. Para cada tipo de datos complejo que requiera una operación, cree un objeto ActionScript independiente.

En la clase ActionScript, utilice la etiqueta de metadatos `RemoteClass` para asignarla al tipo complejo de AEM Forms. Por ejemplo, al invocar la operación `createCustomer` del servicio de atención al cliente, cree una clase ActionScript que se asigne a `com.adobe.livecycle.sample.customer.Customer` tipo de datos.

La siguiente clase de ActionScript denominada Customer muestra cómo asignar al tipo de datos de AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

El tipo de datos completo del tipo complejo de AEM Forms se asigna a la etiqueta de alias.

Los campos de la clase ActionScript coinciden con los campos que pertenecen al tipo complejo de AEM Forms. Los seis campos de la clase Customer ActionScript coinciden con los campos que pertenecen a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
>Una buena manera de determinar los nombres de campo que pertenecen a un tipo complejo de Forms es ver el WSDL de un servicio en un explorador web. Un WSDL especifica los tipos complejos de un servicio y los miembros de datos correspondientes. Se utiliza el siguiente WSDL para el servicio de atención al cliente: `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

La clase Customer ActionScript pertenece a un paquete denominado Customer. Se recomienda colocar todas las clases de ActionScript que se asignan a tipos de datos de AEM Forms complejos en su propio paquete. Cree una carpeta en la carpeta src del proyecto Flex y coloque el archivo ActionScript en ella, como se muestra en la siguiente ilustración.

![iu_iu_customeras](assets/iu_iu_customeras.png)

### Inicio rápido: Invocar el servicio personalizado del cliente mediante Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}

En el ejemplo de código siguiente se invoca el servicio Customer y se crea un cliente. Cuando ejecute este ejemplo de código, asegúrese de rellenar todos los cuadros de texto. Además, asegúrese de crear el archivo Customer.as que se asigna a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
>Para poder ejecutar este inicio rápido, debe crear e implementar el componente personalizado Banco.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**Hoja de estilo**

Este inicio rápido contiene una hoja de estilo denominada *bank.css*. El siguiente código representa la hoja de estilos que se utiliza.

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**Consulte también**

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Administrar documentos con (obsoleto para formularios AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusión del archivo de biblioteca Flex de AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar un proceso de corta duración pasando un documento no seguro mediante (obsoleto para formularios AEM Forms) Remoting de AEM Forms](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticación de aplicaciones cliente creadas con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Pasar documentos seguros para invocar procesos mediante Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
