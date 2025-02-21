---
title: Creación de aplicaciones de Flash Builder que realizan autenticación SSO mediante tokens HTTP
description: Cree una aplicación cliente mediante Flash Builder que realice la autenticación de inicio de sesión único (SSO) mediante tokens HTTP. Autentique un usuario para una operación una vez y utilice esa autenticación para realizar varias operaciones de AEM Forms.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 0%

---

# Crear aplicaciones de Flash Builder que realizan autenticación SSO mediante tokens HTTP {#creating-flash-builder-applicationsthat-perform-sso-authentication-using-http-tokens}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Puede crear una aplicación cliente mediante Flash Builder que realice la autenticación de inicio de sesión único (SSO) mediante tokens HTTP. Supongamos, por ejemplo, que crea una aplicación basada en web mediante Flash Builder. A continuación, supongamos que la aplicación contiene vistas diferentes, donde cada vista invoca una operación de AEM Forms diferente. En lugar de autenticar a un usuario para cada operación de Forms, puede crear una página de inicio de sesión que permita a un usuario autenticarse una vez. Una vez autenticado, un usuario puede invocar varias operaciones sin tener que autenticarse de nuevo. Por ejemplo, si un usuario ha iniciado sesión en Workspace (u otra aplicación de Forms), no es necesario que vuelva a autenticarse.

Aunque la aplicación cliente contiene la lógica de aplicación necesaria para realizar la autenticación SSO, AEM Forms User Management realiza la autenticación de usuario real. Para autenticar a un usuario mediante tokens HTTP, la aplicación cliente invoca la operación `authenticateWithHTTPToken` del servicio Administrador de autenticación. Administración de usuarios puede autenticar usuarios mediante un token HTTP. Para las llamadas posteriores de servicios remotos o web a AEM Forms, no es necesario pasar las credenciales para la autenticación.

>[!NOTE]
>
>Antes de leer esta sección, se recomienda que esté familiarizado con la invocación de AEM Forms mediante Remoting. (Consulte [Invocación de AEM Forms mediante Remoting en AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)).

El siguiente proceso de corta duración de AEM Forms, denominado `MyApplication/EncryptDocument`, se invoca después de que un usuario se autentique usando SSO. (Para obtener información acerca de este proceso, como sus valores de entrada y salida, vea [Ejemplo de proceso de corta duración](/help/forms/developing/aem-forms-processes.md)).

![cf_cf_encryptdocumentprocess2](assets/cf_cf_encryptdocumentprocess2.png)

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con los ejemplos de código que describen cómo invocar este proceso, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

La aplicación cliente creada con Flash Builder interactúa con el servlet de seguridad del Administrador de usuarios configurado en `/um/login` y `/um/logout`. Es decir, la aplicación cliente envía una solicitud a la dirección URL `/um/login` durante el inicio para determinar el estado del usuario. A continuación, el administrador de usuarios responde con el estado del usuario. La aplicación cliente y el servlet de seguridad del Administrador de usuarios se comunican mediante HTTP.

**Formato de solicitud**

El servlet de seguridad requiere las siguientes variables de entrada:

* `um_no_redirect` - Este valor debe ser `true`. Esta variable acompaña todas las solicitudes realizadas al servlet de seguridad del Administrador de usuarios. También ayuda al servlet de seguridad a diferenciar la solicitud entrante proveniente de un cliente flexible u otras aplicaciones web.
* `j_username`: este valor es el valor del identificador de inicio de sesión del usuario tal como se proporciona en el formulario de inicio de sesión.
* `j_password`: este valor es la contraseña correspondiente del usuario, tal como se indica en el formulario de inicio de sesión.

El valor `j_password` solo es necesario para solicitudes de credenciales. Si no se especifica el valor de la contraseña, el servlet de seguridad comprueba si la cuenta que está utilizando ya está autenticada. Si es así, puede continuar; sin embargo, el servlet de seguridad no vuelve a autenticarle.

>[!NOTE]
>
>Para gestionar correctamente i18n, asegúrese de que estos valores estén en formato POST.

**Formato de respuesta**

El servlet de seguridad configurado en `/um/login` responde con el formato `URLVariables`. En este formato, la salida del tipo de contenido es texto/sin formato. La salida contiene pares de nombre-valor separados por un carácter ampersand (&amp;). La respuesta contiene las siguientes variables:

* `authenticated` - El valor es `true` o `false`.
* `authstate` - Este valor puede contener uno de los siguientes valores:

   * `CREDENTIAL_CHALLENGE`: este estado indica que el Administrador de usuarios no puede determinar la identidad del usuario por ningún medio. Para que se realice la autenticación, se requiere el nombre de usuario y la contraseña del usuario.
   * `SPNEGO_CHALLENGE`: este estado se trata igual que `CREDENTIAL_CHALLENGE`.
   * `COMPLETE`: este estado indica que el administrador de usuarios puede autenticar al usuario.
   * `FAILED`: este estado indica que el administrador de usuarios no pudo autenticar al usuario. Como respuesta a este estado, el cliente Flex puede mostrar un mensaje de error al usuario.
   * `LOGGED_OUT`: este estado indica que el usuario cerró sesión correctamente.

* `assertionid`: si el estado era `COMPLETE`, entonces contiene el valor `assertionId` del usuario. Una aplicación cliente puede obtener `AuthResult` para el usuario.

**Proceso de inicio de sesión**

Cuando se inicia una aplicación cliente, puede realizar una petición POST al servlet de seguridad `/um/login`. Por ejemplo, `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true`. Cuando la solicitud llega al servlet de seguridad del Administrador de usuarios, realiza los siguientes pasos:

1. Busca una cookie denominada `lcAuthToken`. Si el usuario ya ha iniciado sesión en otra aplicación de Forms, esta cookie está presente. Si se encuentra la cookie, se valida su contenido.
1. Si el SSO basado en encabezado está activado, el servlet busca encabezados configurados para determinar la identidad del usuario.
1. Si SPNEGO está habilitado, el servlet intenta iniciar SPNEGO e intenta determinar la identidad del usuario.

Si el servlet de seguridad encuentra un token válido que coincida con un usuario, el servlet de seguridad le permite continuar y responder con `authstate=COMPLETE`. De lo contrario, el servlet de seguridad responde con `authstate=CREDENTIAL_CHALLENGE`. La siguiente lista explica estos valores:

* `Case authstate=COMPLETE`: indica que el usuario está autenticado y que el valor `assertionid` contiene el identificador de afirmación del usuario. En esta fase, la aplicación cliente puede conectarse a AEM Forms. El servlet configurado para esa dirección URL puede obtener `AuthResult` para el usuario invocando el método `AuthenticationManager.authenticate(HttpRequestToken)`. La instancia `AuthResult` puede crear el contexto del administrador de usuarios y almacenarlo en la sesión.
* `Case authstate=CREDENTIAL_CHALLENGE`: indica que el servlet de seguridad requiere las credenciales del usuario. Como respuesta, la aplicación cliente puede mostrar la pantalla de inicio de sesión al usuario y enviar la credencial obtenida al servlet de seguridad (por ejemplo, `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true&j_username=administrator&j_password=password)`. Si la autenticación se realiza correctamente, el servlet de seguridad responde con `authstate=COMPLETE`.

Si la autenticación aún no se realiza correctamente, el servlet de seguridad responderá con `authstate=FAILED`. Para responder a este valor, la aplicación cliente puede mostrar un mensaje para obtener las credenciales de nuevo.

>[!NOTE]
>
>Mientras esté `authstate=CREDENTIAL_CHALLENGE`, se recomienda que el cliente envíe la credencial obtenida al servlet de seguridad en un formulario POST.

**Proceso de cierre de sesión**

Cuando una aplicación cliente cierra la sesión, puede enviar una solicitud a la siguiente URL:

`https://<your_serverhost>:<your_port>/um/logout?um_no_redirect=true`

Al recibir esta solicitud, el servlet de seguridad del Administrador de usuarios elimina la cookie `lcAuthToken` y responde con `authstate=LOGGED_OUT`. Una vez que la aplicación cliente recibe este valor, la aplicación puede realizar tareas de limpieza.

## Crear una aplicación cliente que autentique usuarios de formularios AEM Forms mediante SSO {#creating-a-client-application-that-authenticates-aem-forms-users-using-sso}

Para mostrar cómo crear una aplicación cliente que realice la autenticación SSO, se crea una aplicación cliente de ejemplo. La siguiente ilustración muestra los pasos que la aplicación cliente realiza para autenticar a un usuario mediante SSO.

![cf_cf_flexsso](assets/cf_cf_flexsso.png)

En la ilustración anterior se describe el flujo de aplicación que se produce cuando se inicia la aplicación cliente.

1. La aplicación cliente déclencheur el evento `applicationComplete`.
1. Se realiza la llamada a `ISSOManager.singleSignOn`. La aplicación cliente envía una solicitud al servlet de seguridad del Administrador de usuarios.
1. Si el servlet de seguridad autentica al usuario, `ISSOManager` envía `SSOEvent.AUTHENTICATION_SUCCESS`. Como respuesta, la aplicación cliente muestra la página principal. En este ejemplo, la página principal invoca el proceso de corta duración de AEM Forms denominado MyApplication/EncryptDocument.
1. Si el servlet de seguridad no puede determinar si el usuario es válido, la aplicación vuelve a solicitar las credenciales de usuario. La clase `ISSOManager` distribuye el evento `SSOEvent.AUTHENTICATION_REQUIRED`. La aplicación cliente muestra la página de inicio de sesión.
1. Las credenciales proporcionadas en la página de inicio de sesión se envían al método `ISSOManager.login`. Si la autenticación se realiza correctamente, siga con el paso 3. De lo contrario, se activa el evento `SSOEvent.AUTHENTICATION_FAILED`. La aplicación cliente muestra la página de inicio de sesión y un mensaje de error correspondiente.

### Creación de la aplicación cliente {#creating-the-client-application}

La aplicación cliente consta de los siguientes archivos:

* `SSOStandalone.mxml`: archivo MXML principal que representa la aplicación cliente. (Consulte [Creación del archivo SSOStandalone.xml](creating-flash-builder-applications-perform.md#creating-the-ssostandalone-mxml-file)).
* `um/ISSOManager.as`: exponer operaciones relacionadas con el inicio de sesión único (SSO). (Consulte [Creación del archivo ISSOManager.as](creating-flash-builder-applications-perform.md#creating-the-issomanager-as-file).)
* `um/SSOEvent.as`: `SSOEvent` se ha enviado para eventos relacionados con SSO. (Consulte [Creación del archivo SSOEvent.as](creating-flash-builder-applications-perform.md#creating-the-ssoevent-as-file)).
* `um/SSOManager.as`: administra las operaciones relacionadas con el SSO y envía los eventos correspondientes. (Consulte [Creación del archivo SSOManager.as](creating-flash-builder-applications-perform.md#creating-the-ssomanager-as-file)).
* `um/UserManager.as`: contiene lógica de aplicación que invoca el servicio Administrador de autenticación mediante su WSDL. (Consulte [Creación del archivo UserManager.as](creating-flash-builder-applications-perform.md#creating-the-usermanager-as-file)).
* `views/login.mxml`: representa la pantalla de inicio de sesión. (Consulte [Creación del archivo login.xml](creating-flash-builder-applications-perform.md#creating-the-login-mxml-file)).
* `views/logout.mxml`: representa la pantalla de cierre de sesión. (Consulte [Creación del archivo logout.xml](creating-flash-builder-applications-perform.md#creating-the-logout-mxml-file)).
* `views/progress.mxml`: representa una vista de progreso. (Consulte [Creación del archivo progress.xml](creating-flash-builder-applications-perform.md#creating-the-progress-mxml-file)).
* `views/remoting.mxml`: representa la vista que invoca un proceso de corta duración de AEM Forms denominado MyApplication/EncryptDocument mediante comunicación remota. (Consulte [Creación del archivo remoting.xml](creating-flash-builder-applications-perform.md#creating-the-remoting-mxml-file)).

La siguiente ilustración proporciona una representación visual de la aplicación cliente.

![cf_cf_sso_project](assets/cf_cf_sso_project.png)

>[!NOTE]
>
>Observe que hay dos paquetes llamados um y views. Al crear la aplicación cliente, asegúrese de colocar los archivos en los paquetes adecuados. Además, asegúrese de agregar el archivo adobe-remoting-provider.swc a la ruta de clase del proyecto. (Consulte [Inclusión del archivo de biblioteca Flex de AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)).

### Creación del archivo SSOStandalone.xml {#creating-the-ssostandalone-mxml-file}

El siguiente código representa el archivo SSOStandalone.xml.

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application
                 layout="absolute"
                 applicationComplete="initApp()"
                 height="400" width="550"
                 xmlns:v="views.*"
                 backgroundColor="#EDE8F0" viewSourceURL="srcview/index.html">
     <mx:Script>
         <![CDATA[
             import mx.utils.URLUtil;
             import um.SSOEvent;
             import mx.core.UIComponent;
             import um.SSOManager;
             import mx.rpc.events.ResultEvent;
             import mx.utils.ObjectUtil;
             import mx.controls.Alert;
 
             [Bindable]
             private var _serverURL:String;
 
             private var _ssoManager:SSOManager;
 
             private var _progress:UIComponent;
 
             private var _loginPage:UIComponent;
 
             private function initApp():void{
                 _serverURL = determineServerUrl();
                 _ssoManager = new SSOManager(_serverURL);
 
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAILED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_SUCCESS,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_REQUIRED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.LOGOUT_COMPLETE,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAULT,loginHandler);
 
                 trace("[Main] Add the required event handlers for authentication");
                 _ssoManager.singleSignOn();
 
                 showBusy();
             }
 
             private function determineServerUrl():String
             {
                 var s:String ;
                 var appUrl:String = Application.application.url;
                 var givenUrl:String  = ExternalInterface.call("serverUrl.toString");
                 trace("[Main] Application url ["+appUrl+"] Given url ["+givenUrl+"]");
                 if(appUrl != null && appUrl.search("^http") != -1){
                     s = appUrl;
                 }
                 if(s == null){
                     s = givenUrl;
                 }
                 if(s== null){
                     s = "https://hiro-xp:8080/";
                 }
                 s = URLUtil.getFullURL(s,"/");
                 trace("[Main] Would be using ["+s+"] as serverUrl");
                 return s;
             }
 
             private function loginHandler(event:SSOEvent):void
             {
                 trace("[Main] Handling event "+event.type);
                 switch(event.type)
                 {
                     case SSOEvent.AUTHENTICATION_FAILED:
                         viewContent.selectedChild = login;
                         login.showLoginFailed();
                         break;
                     case SSOEvent.AUTHENTICATION_SUCCESS:
                         viewContent.selectedChild = remoting;
                         break;
                     case SSOEvent.AUTHENTICATION_REQUIRED:
                         viewContent.selectedChild = login;
                         break;
                     case SSOEvent.LOGOUT_COMPLETE:
                         viewContent.selectedChild = logout;
                         break;
                     case SSOEvent.AUTHENTICATION_FAULT:
                         Alert.show("Error doing authentication. Root error ["+event.rootEvent+"]","Authentication Fault",Alert.OK);
                 }
             }
 
             public function get ssoManager():SSOManager
             {
                 return _ssoManager;
             }
 
             public function showBusy():void
             {
                 viewContent.selectedChild = progress;
             }
 
             public function get serverUrl():String
             {
                 return _serverURL;
             }
 
         ]]>
     </mx:Script>
     <mx:ViewStack x="0" y="0" id="viewContent" >
         <v:login id="login" />
         <v:remoting id="remoting"  />
         <v:progress id="progress" />
         <v:logout id="logout"/>
     </mx:ViewStack>
 </mx:Application>
 
```

### Creación del archivo ISSOManager.as {#creating-the-issomanager-as-file}

El siguiente código representa el archivo ISSOManager.as.

```java
 package um
 {
     import flash.events.IEventDispatcher;
 
     /**
      * The <code>ISSOManager</code> expose operations related to Single Sign On (SSO) in AEM Forms
      * environment. The application should register appropriate <code>SSOEvent</code> handlers prior
      * to calling any of the following operations
      */
     public interface ISSOManager extends IEventDispatcher
     {
         /**
          * Tries to validate whether the user has an already existing session or not (SSO Scenarios). The application
          * may call this method during the initialization. In general this call would lead to one of the
          * following events getting dispatched
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - If a SSO session was found and valid
          * <li>SSOEvent.AUTHENTICATION_REQUIRED - No SSO session was found and as such authentication is required in
          * the form of username and password.
          * <li>SSOEvent.AUTHENTICATION_FAULT - Some error has occured while connecting to the server
          * </ul>
          */
         function singleSignOn():void;
 
         /**
          * Authenticates the user using username and password. It may lead to one of the following events
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - The authentication is successful and a session is established
          * <li>SSOEvent.AUTHENTICATION_FAILED - Authentication has failed
          * </ul>
          */
         function login(username:String, password:String):void;
 
         /**
          * Terminates the current session and logs out the user.
          */
         function logout():void;
 
         /**
          * Get the assertionId for the logged in user
          */
         function get assertionId():String;
     }
 }
```

### Creación del archivo SSOEvent.as {#creating-the-ssoevent-as-file}

El siguiente código representa el archivo SSOEvent.as.

```java
 package um
 {
     import flash.events.Event;
 
     /**
      * The <code>SSOEvent</code> is dispatched for SSO related events
      */
     public class SSOEvent extends Event
     {
         /**
          * This type of event would be dispatched when the Authentication process is successful. Authentication
          * might have been done with SSO or username and password. As a response to this event the application
          * can show the welcome page to the user
          * The application may want to perform specific check for permission/role so as to verify the user is allowed.
          * So as a response to this event the application would do those checks and then only show the welcome page
          */
         public static const AUTHENTICATION_SUCCESS:String = "authenticationSuccess";
 
         /**
          * This type of event would be dispatched when authentication fails using the username, password.
          * As a response to this type of event an application can show an error message to the user.
          * This event would only happen when authentication is done using username and password and NOT in
          * SSO case.
          */
         public static const AUTHENTICATION_FAILED:String = "authenticationFailed";
 
         /**
          * This type of event would be dispatched when authentication using SSO is not achieved. And due to
          * that we require the user's username and password for authentication. As a response to this event
          * the application can show the login page to the user.
          */
         public static const AUTHENTICATION_REQUIRED:String = "authenticationRequired";
 
         /**
          * This type of event would be dispatched when logout is complete. As a response to this event the
          * application may show a logout page informing the user that he has been logged out. Or the application
          * can take the user back to login page
          */
         public static const LOGOUT_COMPLETE:String = "logoutComplete";
 
         /**
          * This type of event would be dispatched when ever there is a problem in doing Authentication. The root cause
          * can be obtained from the <code>rootEvent</code>.
          */
         public static const AUTHENTICATION_FAULT:String = "authenticationFault";
 
         private var _rootEvent:Event;
 
         public function SSOEvent(type:String, rootEvent:Event=null)
         {
             super(type,true,false);
             _rootEvent = rootEvent;
         }
 
         /**
          * The root event. If current event type is <code>AUTHENTICATION_FAULT</code> then it would be an
          * <code>IOErrorEvent</code> in other cases it would be complete event. Its basic use is to extract the root
          * cause if there is an authentication fault.
          */
         public function get rootEvent():Event
         {
             return _rootEvent;
         }
     }
 }
```

### Creación del archivo SOManager.as {#creating-the-ssomanager-as-file}

El siguiente código representa el archivo SOManager.as.

```java
 package um
 {
     import flash.events.Event;
     import flash.events.EventDispatcher;
     import flash.events.IOErrorEvent;
     import flash.external.ExternalInterface;
     import flash.net.URLLoader;
     import flash.net.URLLoaderDataFormat;
     import flash.net.URLRequest;
     import flash.net.URLVariables;
 
     import mx.utils.ObjectUtil;
 
     /**
      * Manages the SSO related operations and dispatches appropriate events. It would connect to the UM Filter/Servlet
      * at <code>um/login</code> The UM response would be of form of url encoded variables. It would look for
      * <code>authstate</code> value in the response and depending on that it would proceed.
      *
      * <p>If there is an IO_Error while initial attempt to UM then it would assume it as a 401 response. And it would
      * be assumed that SPNEGO based authenticatin is not working and therefore user would be shown a login page.
      */
     public class SSOManager extends EventDispatcher implements ISSOManager
     {
         private static const SSO_URL:String = "um/login";
         private static const SSO_LOGOUT_URL:String = "um/logout";
         private static const AUTH_COOKIE_NAME:String = "lcAuthToken";
 
         private var _serverUrl:String;
         private var _assertionId:String;
 
         /**
          * Constructs an SSOManager with the given server url.
          *
          * @param serverUrl - The uri of the server to connect to. it must be without any context path for example,
          * http://localhost:8080/. The SSOManager would directly append the path of UM exposed SSO url to it
          * for its operations
          */
         public function SSOManager(serverUrl:String)
         {
             _serverUrl = serverUrl;
         }
 
         public function singleSignOn():void
         {
             sendRequest(SSO_URL,true);
         }
 
         public function login(username:String, password:String):void
         {
             sendRequest(SSO_URL,false,
                 function(request:URLRequest,vars:URLVariables):void
                 {
                     vars.j_username = username;
                     vars.j_password = password;
                 }
             );
         }
 
         public function logout():void
         {
             sendRequest(SSO_LOGOUT_URL);
         }
 
         public function get assertionId():String
         {
             return _assertionId;
         }
 
 
 
         /**
          * Connects to the UM security service.
          */
         private function sendRequest(relativeUrl:String,authenticationRequest:Boolean=false, requestProcessor:Function=null):void
         {
             var loader:URLLoader = new URLLoader();
             loader.dataFormat = URLLoaderDataFormat.VARIABLES;
             var request:URLRequest = new URLRequest(_serverUrl + relativeUrl);
             trace("[SSOmanager] Contacting ["+request.url+"]");
             var vars:URLVariables = new URLVariables();
             vars.um_no_redirect = "true";
             request.data = vars;
             if(requestProcessor != null){
                 requestProcessor(request,vars);
             }
 
             loader.addEventListener(Event.COMPLETE,authHandler);
             //if its an authentication request then only treat io error as a possible 401
             //for others treat them as faults
             if(authenticationRequest){
                 loader.addEventListener(IOErrorEvent.IO_ERROR,httpAuthenticationHandler);
             }else{
                 loader.addEventListener(IOErrorEvent.IO_ERROR,authFaultHandler);
             }
             trace("[SSOmanager] Sending request "+ ObjectUtil.toString(request));
             loader.load(request);
         }
 
         private function authHandler(event:Event):void
         {
             var loader:URLLoader = URLLoader(event.target);
             var response:URLVariables = URLVariables(loader.data);
             trace("[SSOmanager] Processing response ["+ObjectUtil.toString(response)+"]");
             handleAuthResult(response["authstate"],response);
         }
 
         /**
          * Handles the IOErrorEvent. Flash would dispatch IOEvent in response to HTTP 401.
          * There is no way to distinguish it from the genuine IOError.
          */
         private function httpAuthenticationHandler(event:IOErrorEvent):void
         {
             trace("[SSOmanager] Processing IOErrorEvent ["+ObjectUtil.toString(event)+"]");
             handleAuthResult("CREDENTIAL_CHALLENGE");
 
         }
 
         /**
          * Dispatches appropriate <code>SSOEvent</code> on the basis of the <code>authstate</code>
          * value of the response.
          * The response is url encoded in for of
          * <pre>
          * authenticated=false&authstate=SPNEGO_CHALLENGE
          * </pre>
          * Depending on <code>authstate</code> the SSOEvent is dispatched
          */
         private function handleAuthResult(authState:String,response:URLVariables = null):void
         {
             trace("[SSOmanager] processing state "+authState);
             switch(authState)
             {
                 case "FAILED"  :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAILED));
                     break;
                 case "COMPLETE" :
                     _assertionId = response ? response["assertionid"] : null;
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_SUCCESS));
                     break;
                 case "CREDENTIAL_CHALLENGE" :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
                 case "LOGGED_OUT" :
                     dispatchEvent(new SSOEvent(SSOEvent.LOGOUT_COMPLETE));
                     break;
                 default:
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
             }
         }
 
         private function authFaultHandler(event:Event):void
         {
             dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAULT,event));
         }
 
     }
 }
```

### Creación del archivo UserManager.as {#creating-the-usermanager-as-file}

El siguiente código representa el archivo UserManager.as.

```java
 package um
 {
     import flash.events.Event;
     import mx.rpc.soap.WebService;
     import mx.rpc.soap.Operation;
     import mx.rpc.IResponder;
     import mx.rpc.events.FaultEvent;
     import mx.rpc.events.ResultEvent;
     import mx.rpc.soap.LoadEvent;
 
     public class UserManager
     {
         private var _ssoManager:ISSOManager;
         private var _serverUrl:String;
 
         public function UserManager(ssoManager:ISSOManager,serverUrl:String)
         {
             _serverUrl = serverUrl;
             _ssoManager = ssoManager;
         }
 
         public function retrieveAssertion(responder:IResponder):String
         {
             var assertionId:String = _ssoManager.assertionId;
             if(!assertionId)
             {
                 trace("[UserManager] AssertionId not found");
                 return null;
             }
 
             var ws:WebService = new WebService();
             var wsdl:String = _serverUrl+'soap/services/AuthenticationManagerService?wsdl&lc_version=8.2.1';
             ws.loadWSDL(wsdl);
             ws.addEventListener(LoadEvent.LOAD,
                 function(event:Event):void
                 {
                     trace("[UserManager] WSDL loaded");
                     var authenticate:Operation = ws.authenticateWithHttpToken as Operation;
                     authenticate.resultFormat = "e4x";
                     authenticate.addEventListener(ResultEvent.RESULT,
                         function(event:Event):void
                         {
                             responder.result(event);
                         }
                     );
                     authenticate.send({assertionId:assertionId});
                 }
             );
 
             ws.addEventListener(FaultEvent.FAULT,
                 function(event:Event):void
                 {
                     responder.fault(event);
                 }
             );
             return null;
         }
     }
 }
```

### Creación del archivo login.xml {#creating-the-login-mxml-file}

El siguiente código representa el archivo login.xml.

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Script>
         <![CDATA[
             import mx.core.Application;
             public function showLoginFailed():void
             {
                 loginMessage.text = "Username or Password incorrect";
             }
 
             private function doLogin():void
             {
                 Application.application.ssoManager.login(j_username.text,j_password.text);
                 Application.application.showBusy();
             }
 
         ]]>
     </mx:Script>
 
     <mx:VBox height="113" width="244" x="128" y="144" horizontalAlign="center" verticalGap="10">
         <mx:HBox width="100%">
             <mx:HBox width="100%" verticalAlign="middle" horizontalAlign="center" height="32">
                 <mx:Label text="Username" fontWeight="bold"/>
                 <mx:TextInput id="j_username"/>
             </mx:HBox>
         </mx:HBox>
         <mx:HBox width="100%" height="33" horizontalAlign="center" horizontalGap="10" verticalAlign="middle">
             <mx:Label text="Password" fontWeight="bold"/>
             <mx:TextInput displayAsPassword="true" id="j_password"/>
         </mx:HBox>
         <mx:Button label="Login" click="doLogin()"/>
     </mx:VBox>
     <mx:Text x="128" y="122" id="loginMessage" width="230" height="14"/>
     <mx:Label x="154" y="65" text="AEM Forms SSO Demo" fontFamily="Georgia" fontSize="20" color="#0A0A0A"/>
 </mx:Canvas>
 
```

### Creación del archivo logout.xml {#creating-the-logout-mxml-file}

El siguiente código representa el archivo logout.xml.

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Label x="97" y="188" text="You have successfully logged out from the application"/>
 
 </mx:Canvas>
 
```

### Creación del archivo progress.xml {#creating-the-progress-mxml-file}

El siguiente código representa el archivo progress.xml.

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas >
     <mx:Label x="151" y="141" text="Wait...."/>
     <mx:SWFLoader source="LoadingCircle.swf" width="50" height="50" horizontalCenter="0" verticalCenter="0"/>
 </mx:Canvas>
```

### Creación del archivo remoting.xml {#creating-the-remoting-mxml-file}

El siguiente código representa el archivo remoting.xml que invoca el proceso `MyApplication/EncryptDocument`. Dado que se pasa un documento al proceso, la lógica de aplicación responsable de pasar un documento seguro a AEM Forms se encuentra en este archivo. (Consulte [Pasar documentos seguros para invocar procesos mediante Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)).

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="664" height="400" creationComplete="initializeChannelSet()" xmlns:views="views.*">
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
             import um.UserManager;
             import mx.rpc.events.ResultEvent;
             import mx.rpc.events.FaultEvent;
             import mx.core.Application;
             import mx.rpc.Responder;
             import mx.utils.ObjectUtil;
 
             // Classes used in file retrieval
             private var fileRef:FileReference = new FileReference();
             private var docRef:DocumentReference = new DocumentReference();
             private var parentResourcePath:String = "/";
             //private var serverPort:String = "'[server]:[port]'";
             private var serverPort:String = "'[server]:[port]'";
             private var now1:Date;
             private var userManager:UserManager;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Holds information returned from AEM Forms
             [Bindable]
             public var progressList:ArrayCollection = new ArrayCollection();
 
 
             // Set up channel set to invoke AEM Forms.
             // This must be done before calling any service or process, but only
             // once for the entire application.
             private function initializeChannelSet():void {
                 cs = new ChannelSet();
                 cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
                 EncryptDocument.channelSet = cs;
 
             //Get the user that is authenticated
             userManager = new UserManager(Application.application.ssoManager,Application.application.serverUrl);
             userManager.retrieveAssertion(
                     new mx.rpc.Responder(
                         function(event:ResultEvent):void
                         {
                             var name:String = XML(event.currentTarget.lastResult)..*::authenticatedUser.*::userid.text();
                             username.text = "Welcome "+name;
                         },
                         function(event:FaultEvent):void
                         {
                             mx.controls.Alert.show(event.fault.faultString,'Error')
                         }
                     )
                 );
 
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
 
                 // Set the docRefs url and referenceType parameters
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
                 token = EncryptDocument.invoke(params);
                 token.name = name;
             }
 
 
             // This method handles a successful conversion invocation
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
 
 
             private function resultHandler(event:ResultEvent):void {
             // Do anything else here.
 
             }
 
             private function logout():void
             {
                 Application.application.ssoManager.logout();
                 Application.application.showBusy();
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
                   id="username"/>
 
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
     <mx:Button label="Select File" click="uploadFile()" />
     <mx:Button label="Logout"  click="logout()" />
     </mx:Panel>
 </mx:Canvas>
 
 
```

### Información adicional {#additional-information}

En las siguientes secciones se proporcionan detalles adicionales que describen la comunicación entre la aplicación cliente y el servlet de seguridad del Administrador de usuarios.

### Se produce una nueva autenticación {#a-new-authentication-occurs}

En este caso, el usuario intenta iniciar sesión desde una aplicación cliente en AEM Forms por primera vez. (no existe ninguna sesión anterior que implique al usuario). En el evento `applicationComplete`, se invoca el método `SSOManager.singleSignOn` que envía una solicitud al administrador de usuarios.

`GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1`

El servlet de seguridad del Administrador de usuarios responde con el siguiente valor:

`HTTP/1.1 200 OK`

`authenticated=false&authstate=CREDENTIAL_CHALLENGE`

Como respuesta a este valor, se distribuye un valor `SSOEvent.AUTHENTICATION_REQUIRED`. Como resultado, la aplicación cliente muestra una pantalla de inicio de sesión al usuario. Las credenciales se vuelven a enviar al servlet de seguridad del Administrador de usuarios.

`GET /um/login?um%5Fno%5Fredirect=true&j%5Fusername=administrator&j%5Fpassword=password HTTP/1.1`

El servlet de seguridad del Administrador de usuarios responde con el siguiente valor:

```verilog
 HTTP/1.1 200 OK
 Set-Cookie: lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A; Path=/
 authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

Como resultado, se envía `authstate=COMPLETE the SSOEvent.AUTHENTICATION_SUCCESS`. La aplicación cliente puede realizar un procesamiento adicional si es necesario. Por ejemplo, se puede crear un registro que registre la fecha y la hora en que se autenticó al usuario.

### El usuario ya se ha autenticado {#the-user-is-already-authenticated}

En este caso, el usuario ya ha iniciado sesión en AEM Forms y, a continuación, navega a la aplicación cliente. La aplicación cliente se conecta al servlet de seguridad del Administrador de usuarios durante el inicio.

```verilog
 GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1
 Cookie: JSESSIONID=A4E0BCC2DD4BCCD3167C45FA350BD72A; lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

Como el usuario ya está autenticado, la cookie del Administrador de usuarios está presente y se envía al servlet de seguridad del Administrador de usuarios. A continuación, el servlet obtiene el valor `assertionId` y comprueba si es válido. Si es válido, se devuelve `authstate=COMPLETE`. De lo contrario, se devuelve `authstate=CREDENTIAL_CHALLENGE`. La siguiente es una respuesta típica:

```verilog
 HTTP/1.1 200 OK
        authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

En este caso, no se muestra al usuario una pantalla de inicio de sesión y, en su lugar, se le redirige directamente a una pantalla de bienvenida.
