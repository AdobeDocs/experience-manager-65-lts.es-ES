---
title: Client Context en detalle
description: Client Context representa una colección ensamblada dinámicamente de datos de usuario.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
feature: Context Hub,Developing,Personalization
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2969'
ht-degree: 1%

---

# Client Context en detalle{#client-context-in-detail}

>[!NOTE]
>
>ContextHub ha reemplazado a Client Context. Consulte la [documentación relacionada](/help/sites-developing/contexthub.md) para obtener detalles.

Client Context representa una colección ensamblada dinámicamente de datos de usuario. Puede utilizar los datos para determinar el contenido que se mostrará en una página web en una situación determinada (segmentación de contenido). Los datos también están disponibles para el análisis de sitios web y para cualquier JavaScript de la página.

Client Context consta principalmente de los siguientes aspectos:

* El almacén de sesión que contiene los datos de usuario.
* Interfaz de usuario que muestra los datos del usuario y proporciona herramientas para simular la experiencia del usuario.
* Una [API de JavaScript](/help/sites-developing/ccjsapi.md) para interactuar con almacenes de sesión.

Para crear un almacén de sesiones independiente y agregarlo a Client Context, o para crear un almacén de sesiones vinculado a un componente de almacén de contexto. Adobe Experience Manager (AEM) instala varios componentes de la tienda de contexto que puede utilizar de inmediato. Puede utilizar estos componentes como base para sus componentes.

Para obtener información sobre cómo abrir Client Context, configurar la información que muestra y simular la experiencia del usuario, consulte [Client Context](/help/sites-administering/client-context.md).

## Almacenes de sesión {#session-stores}

Client Context incluye varios almacenes de sesiones que contienen datos de usuario. Los datos de almacenamiento proceden de las siguientes fuentes:

* El explorador web del cliente.
* El servidor (consulte [Almacén JSONP](/help/sites-administering/client-context.md#main-pars-variable-8) para almacenar información de fuentes de terceros)

El módulo de Client Context proporciona una [API de JavaScript](/help/sites-developing/ccjsapi.md) que puede usar para interactuar con almacenes de sesión a fin de leer y escribir datos de usuario, así como para escuchar y reaccionar ante eventos de almacén. También puede crear almacenes de sesión para los datos de usuario que utilice para la segmentación de contenido u otros fines.

Los datos del almacén de sesión permanecen en el cliente. Client Context no vuelve a escribir datos en el servidor. Para enviar datos al servidor, utilice un formulario o desarrolle JavaScript personalizado.

Cada almacén de sesión es una colección de pares propiedad-valor. El almacén de sesión representa una colección de datos (de cualquier tipo), cuyo significado conceptual puede decidir el diseñador, el desarrollador o ambos. En el siguiente ejemplo de código JavaScript se define un objeto que representa los datos de perfil que el almacén de sesión puede contener:

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

Un almacén de sesiones se puede mantener entre sesiones de explorador o solo puede durar la sesión de explorador en la que se crea.

>[!NOTE]
>
>La persistencia del almacenamiento utiliza el almacenamiento del explorador o cookies (la cookie `SessionPersistence`). El almacenamiento del explorador es más común.
>
>Cuando se cierra y se vuelve a abrir el explorador, se puede cargar un almacén de sesiones con los valores de un almacén persistente. Es necesario borrar la caché del explorador para eliminar los valores antiguos.

### Componentes de tienda de contexto {#context-store-components}

Un componente de almacén de contexto es un componente de CQ que se puede agregar a Client Context. Normalmente, los componentes de almacén de contexto muestran datos de un almacén de sesión con el que están asociados. Sin embargo, la información que muestran los componentes del almacén de contexto no se limita a los datos del almacén de sesión.

Los componentes del almacén de contexto pueden incluir los siguientes elementos:

* Scripts JSP que definen el aspecto en Client Context.
* Propiedades para enumerar el componente en Sidekick.
* Cuadros de diálogo de edición para configurar instancias de componente.
* JavaScript que inicializa el almacén de sesión.

Para obtener una descripción de los componentes de Context Store instalados que puede agregar al Context Store, consulte [Componentes de Client Context disponibles](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>Los datos de página ya no están en el contexto de cliente como componente predeterminado. Si es necesario, puede agregarlo editando el contexto del cliente, agregando el componente **Propiedades de almacenamiento genérico** y configurándolo para definir **Almacén** como `pagedata`.

### Entrega de contenido segmentado {#targeted-content-delivery}

La información de perfil también se usa para entregar [contenido de destino](/help/sites-authoring/content-targeting-touch.md).

![clientcontext_targetedcontentdelivery](assets/clientcontext_targetedcontentdelivery.png) ![clientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## Añadir Client Context A Una Página {#adding-client-context-to-a-page}

Incluya el componente Client Context en la sección del cuerpo de las páginas web para habilitar Client Context. La ruta del nodo del componente Client Context es `/libs/cq/personalization/components/clientcontext`. Para incluir el componente, agregue el siguiente código al archivo JSP del componente de página, ubicado justo debajo del elemento `body` de su página:

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

El componente clientcontext hace que la página cargue las bibliotecas de cliente que implementan Client Context.

* La API de JavaScript de Client Context.
* Marco de Client Context que admite almacenes de sesión, administración de eventos, etc.
* Segmentos que se han definido.
* Los scripts init.js generados para cada componente de almacén de contexto que se ha agregado a Client Context.
* (Solo la instancia de autor) La interfaz de usuario de Client Context.

La IU de Client Context solo está disponible en la instancia de autor.

## Ampliación de Client Context {#extending-client-context}

Para ampliar Client Context, cree un almacén de sesiones y, opcionalmente, muestre los datos del almacén:

* Cree un almacén de sesión para los datos de usuario que necesita para la segmentación de contenido y el análisis web.
* Cree un componente de almacén de contexto para permitir a los administradores configurar el almacén de sesión asociado y mostrar los datos del almacén en Client Context con fines de prueba.

>[!NOTE]
>
>Si tiene (o crea) un servicio `JSONP` que puede proporcionar los datos, simplemente puede utilizar el componente de almacén de contexto `JSONP` y asignarlo al servicio JSONP. Esto administra el almacén de sesión.

### Creación de un almacén de sesión {#creating-a-session-store}

Cree un almacén de sesión para los datos que debe agregar y recuperar de Client Context. Por lo general, utilice el siguiente procedimiento para crear un almacén de sesiones:

1. Cree una carpeta de biblioteca de cliente que tenga un valor de propiedad `categories` de `personalization.stores.kernel`. Client Context carga automáticamente las bibliotecas de cliente de esta categoría.

1. Configure la carpeta de biblioteca de cliente para que dependa de la carpeta de biblioteca de cliente `personalization.core.kernel`. La biblioteca de cliente `personalization.core.kernel` proporciona la API de JavaScript de Client Context.

1. Agregue el JavaScript que crea e inicializa el almacén de sesiones.

Al incluir JavaScript en la biblioteca de cliente personalization.store.kernel, se crea el almacén cuando se carga el marco de Client Context.

>[!NOTE]
>
>Si está creando un almacén de sesiones como parte de un componente de almacén de contexto, puede colocar alternativamente la JavaScript en el archivo init.js.jsp del componente. En este caso, el almacén de sesiones se crea únicamente si el componente se agrega a Client Context.

#### Tipos de almacenes de sesión {#types-of-session-stores}

Los almacenes de sesión se crean y quedan disponibles durante una sesión del explorador, o se conservan en el almacenamiento del explorador o en las cookies. La API de JavaScript de Client Context define varias clases que representan ambos tipos de almacenes de datos:

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`: estos objetos solo residen en el DOM de la página. Los datos se crean y persisten durante la duración de la página.
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`: estos objetos residen en el DOM de la página y se conservan en el almacenamiento del explorador o en las cookies. Los datos están disponibles en todas las páginas y en todas las sesiones de usuario.

La API también proporciona extensiones de estas clases especializadas en almacenar datos JSON o datos JSONP:

* Objetos de solo sesión: [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) y [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* Objetos persistentes: [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) y [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### Creación del objeto de almacén de sesiones {#creating-the-session-store-object}

La JavaScript de la carpeta de biblioteca del cliente crea e inicializa el almacén de sesiones. El almacén de sesión debe registrarse mediante el Administrador de tienda de contexto. En el ejemplo siguiente se crea y registra un objeto [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

Para almacenar datos JSON, en el siguiente ejemplo se crea y registra un objeto [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore).

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### Crear un componente de tienda de contexto {#creating-a-context-store-component}

Cree un componente de almacén de contexto para procesar los datos del almacén de sesión en Client Context. Una vez creado, puede arrastrar el componente de almacén de contexto a Client Context para procesar los datos de un almacén de sesión. Los componentes del almacén de contexto constan de los siguientes elementos:

* Script JSP para procesar los datos.
* Un cuadro de diálogo de edición.
* Script JSP para inicializar el almacén de sesión.
* (Opcional) Una carpeta de biblioteca de cliente que crea el almacén de sesiones. No es necesario incluir la carpeta de biblioteca del cliente si el componente utiliza un almacén de sesiones existente.

#### Ampliación de los componentes del almacén de contexto proporcionados {#extending-the-provided-context-store-components}

AEM proporciona los componentes genericstore y genericstoreproperties del almacén de contexto que puede ampliar. La estructura de los datos de la tienda determina el componente que se amplía:

* Pares propiedad-valor: ampliar el componente `GenericStoreProperties`. Este componente procesa automáticamente los almacenes de pares propiedad-valor. Se proporcionan varios puntos de interacción:

   * `prolog.jsp` y `epilog.jsp`: interacción de componentes que permite agregar lógica del lado del servidor antes o después del procesamiento del componente.

* Datos complejos: ampliar el componente `GenericStore`. El almacén de sesiones necesita un método de &quot;procesador&quot; al que se llame cada vez que se deba representar el componente. La función de procesamiento se llama con dos parámetros:

   * `@param {String} store`
El almacén que se procesará

   * `@param {String} divId`
El ID del div en el que se debe procesar el almacén.

>[!NOTE]
>
>Todos los componentes de Client Context son extensiones de los componentes Almacén genérico o Propiedades de almacenamiento genérico. Hay varios ejemplos instalados en la carpeta `/libs/cq/personalization/components/contextstores`.

#### Configuración del aspecto visual en Sidekick {#configuring-the-appearance-in-sidekick}

Al editar Client Context, los componentes del almacén de contexto aparecen en Sidekick. Al igual que con todos los componentes, las propiedades `componentGroup` y `jcr:title` del componente Client Context determinan el grupo y el nombre del componente.

Todos los componentes que tienen un valor de propiedad `componentGroup` de `Client Context` aparecen en Sidekick de forma predeterminada. Si utiliza un valor diferente para la propiedad `componentGroup`, debe agregar manualmente el componente a Sidekick mediante el modo de diseño.

#### Instancias de componente de tienda de contexto {#context-store-component-instances}

Cuando agrega un componente de almacén de contexto a Client Context, se crea un nodo que representa la instancia del componente debajo de `/etc/clientcontext/default/content/jcr:content/stores`. Este nodo contiene los valores de propiedad que se configuran mediante el cuadro de diálogo de edición del componente.

Cuando se inicializa Client Context, se procesan estos nodos.

#### Inicialización del almacén de sesión asociado {#initializing-the-associated-session-store}

Agregue un archivo init.js.jsp al componente para generar código JavaScript que inicialice el almacén de sesiones que utiliza el componente de almacén de contexto. Por ejemplo, utilice el script de inicialización para recuperar las propiedades de configuración del componente y utilizarlas para rellenar el almacén de sesiones.

La JavaScript que se genera se agrega a la página cuando Client Context se inicializa al cargar la página tanto en la instancia de autor como en la de publicación. Este JSP se ejecuta antes de que se cargue y procese la instancia del componente de almacén de contexto.

El código debe establecer el tipo MIME del archivo en `text/javascript`; de lo contrario, no se ejecutará.

>[!CAUTION]
>
>El script init.js.jsp se ejecuta en la instancia de autor y publicación, pero solo si se agrega el componente de almacén de contexto a Client Context.

El siguiente procedimiento crea el archivo de secuencias de comandos init.js.jsp y agrega el código que establece el tipo mime correcto. El código que realiza la inicialización del almacén sería el siguiente.

1. Haga clic con el botón derecho en el nodo de componente de almacén de contexto y haga clic en Crear > Crear archivo.
1. En el campo Nombre, escriba `init.js.jsp` y haga clic en Aceptar.
1. En la parte superior de la página, agregue el siguiente código y haga clic en Guardar todo.

   ```java
   <%@page contentType="text/javascript" %>
   ```

### Procesar datos del almacén de sesiones para componentes genéricos storeproperties {#rendering-session-store-data-for-genericstoreproperties-components}

Muestra los datos del almacén de sesión en Client Context mediante un formato coherente.

#### Visualización de datos de propiedad {#displaying-property-data}

Las etiquetas de personalización proporcionan la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta, incluya la siguiente línea de código en su archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

El atributo `propertyName` es el nombre de la propiedad de almacén que se va a mostrar. El atributo `store` es el nombre del almacén registrado. La siguiente etiqueta de ejemplo muestra el valor de la propiedad `authorizableId` del almacén `profile`:

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### Estructura HTML {#html-structure}

La carpeta de la biblioteca de cliente personalization.ui (/etc/clientlibs/foundation/personalization/ui/themes/default) proporciona los estilos CSS que Client Context utiliza para dar formato al código HTML. El siguiente código ilustra la estructura sugerida para utilizar para mostrar los datos del almacén:

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

El componente de almacén de contexto `/libs/cq/personalization/components/contextstores/profiledata` utiliza esta estructura para mostrar los datos del almacén de sesión de perfil. La clase `cq-cc-thumbnail` coloca la imagen en miniatura. Las clases `cq-cc-store-property-level*x*` dan formato a los datos alfanuméricos:

* level0, level1 y level2 se distribuyen verticalmente y utilizan una fuente blanca.
* level3 y los niveles adicionales se distribuyen horizontalmente y utilizan una fuente blanca con un fondo más oscuro.

![chlimage_1-4](assets/chlimage_1-4.png)

### Procesamiento de datos del almacén de sesiones para componentes genéricos {#rendering-session-store-data-for-genericstore-components}

Para procesar datos de almacén mediante un componente genéricos, debe hacer lo siguiente:

* Añada la etiqueta personalization:storeRendererTag al script JSP del componente para identificar el nombre del almacén de sesión.
* Implemente un método de procesamiento en la clase de almacén de sesiones.

#### Identificación del almacén de sesiones de genericstore {#identifying-the-genericstore-session-store}

Las etiquetas de personalización proporcionan la etiqueta `personalization:storePropertyTag` que muestra el valor de una propiedad de un almacén de sesiones. Para utilizar la etiqueta, incluya la siguiente línea de código en su archivo JSP:

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

La etiqueta tiene el siguiente formato:

```java
<personalization:storeRendererTag store="store_name"/>
```

#### Implementación del método de procesamiento del almacén de sesiones {#implementing-the-session-store-renderer-method}

El almacén de sesiones necesita un método de &quot;procesador&quot; al que se llame cada vez que se deba representar el componente. La función de procesamiento se llama con dos parámetros:

* @param almacén {String}
El almacén que se procesará
* @param {String} divId
El ID del div en el que se debe procesar el almacén.

## Interactuar con almacenes de sesiones {#interacting-with-session-stores}

Utilice JavaScript para interactuar con almacenes de sesiones.

### Acceso a almacenes de sesión {#accessing-session-stores}

Obtenga un objeto de almacén de sesión para leer o escribir datos en el almacén. [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) proporciona acceso a las tiendas en función del nombre de la tienda. Una vez obtenido, use los métodos de [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) o [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) para interactuar con los datos del almacén.

El ejemplo siguiente obtiene el almacén `profile` y, a continuación, recupera la propiedad `formattedName` del almacén.

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### Creación de un Listener para Reaccionar a una Actualización de Session Store {#creating-a-listener-to-react-to-a-session-store-update}

La sesión almacena eventos de activación, por lo que es posible añadir oyentes y eventos de déclencheur basados en estos eventos.

Los almacenes de sesión se basan en el patrón `Observable`. Extienden [`CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) que proporciona el método ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`.

En el siguiente ejemplo se agrega un agente de escucha al evento `update` del almacén de sesión `profile`.

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### Comprobación de que se ha definido e inicializado un almacén de sesión {#checking-that-a-session-store-is-defined-and-initialized}

Los almacenes de sesión no están disponibles hasta que se cargan e inicializan con datos. Los siguientes factores pueden afectar al tiempo de disponibilidad del almacén de sesiones:

* Carga de página
* JavaScript cargando
* Tiempo de ejecución de JavaScript
* Tiempos de respuesta para solicitudes XHR
* Cambios dinámicos en el almacén de sesión

Use los métodos [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) y [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) del objeto [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) para obtener acceso a los almacenes de sesión únicamente cuando estén disponibles. Estos métodos permiten registrar detectores de eventos que reaccionan a los eventos de registro e inicialización de sesión.

>[!CAUTION]
>
>Si depende de otra tienda, debe tener en cuenta el caso de que la tienda nunca se haya registrado.

El ejemplo siguiente utiliza el evento `onStoreRegistered` del almacén de sesión `profile`. Cuando se registra el almacén, se agrega un agente de escucha al evento `update` del almacén de sesión. Cuando se actualiza el almacén, el contenido del elemento `<div class="welcome">` de la página se actualiza con el nombre del almacén `profile`.

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### Exclusión de una propiedad de la cookie sessionpersistence {#excluding-a-property-from-the-sessionpersistence-cookie}

Para evitar que una propiedad de `PersistedSessionStore` se mantenga (es decir, que se excluya de la cookie `sessionpersistence`), agregue la propiedad a la lista de propiedades no persistentes del almacén de sesiones persistentes.

Ver ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## Configuración del deslizador del dispositivo {#configuring-the-device-slider}

### Condiciones {#conditions}

La página actual debe tener una página móvil correspondiente; esto se determina únicamente si la página tiene un LiveCopy configurado con una configuración de despliegue móvil ( `rolloutconfig.path.toLowerCase` contiene `mobile`).

#### Configuración {#configuration}

Al cambiar de la página de escritorio a su equivalente móvil:

* Se carga el DOM de la página móvil.
* El elemento principal `div` (obligatorio) que contiene el contenido, se extrae y se inserta en la página de escritorio actual.

* Las clases CSS y body que se cargan deben configurarse manualmente.

Por ejemplo:

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## Ejemplo: Creación de un componente de almacén de contexto personalizado {#example-creating-a-custom-context-store-component}

En este ejemplo, se crea un componente de almacén de contexto que recupera datos de un servicio externo y los almacena en el almacén de sesiones:

* Extiende el componente genericstoreproperties.
* Inicializa un almacén con un objeto CQ_Analytics.JSONPStore de JavaScript.
* Llama a un servicio JSONP para recuperar datos y agregarlos al almacén.
* Procesa los datos en Client Context.

### Añadir el componente geoloc {#add-the-geoloc-component}

Cree una aplicación CQ y agregue el componente geoloc.

1. Abra CRXDE Lite en el explorador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Haga clic con el botón derecho en la carpeta `/apps` y haga clic en Crear > Crear carpeta. Especifique un nombre de `myapp` y haga clic en Aceptar.
1. Del mismo modo, debajo de `myapp`, cree una carpeta llamada `contextstores`. &quot;
1. Haga clic con el botón derecho en la carpeta `/apps/myapp/contextstores` y haga clic en Crear > Crear componente. Especifique los siguientes valores de propiedad y haga clic en Siguiente:

   * Etiqueta: geoloc
   * Título: Tienda de ubicación
   * Super Type: cq/personalization/components/contextstore/genericstoreproperties
   * Grupo: Client Context

1. En el cuadro de diálogo Crear componente, haga clic en Siguiente en cada página hasta que se active el botón Aceptar y, a continuación, haga clic en Aceptar.
1. Haga clic en Guardar todo.

### Crear el cuadro de diálogo Editar geolocalización {#create-the-geoloc-edit-dialog}

El componente de almacén de contexto requiere un cuadro de diálogo de edición. El cuadro de diálogo de edición geográfica contiene un mensaje estático que indica que no hay propiedades que configurar.

1. Haga clic con el botón derecho en el nodo `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` y haga clic en Copiar.
1. Haga clic con el botón derecho en el nodo `/apps/myapp/contextstores/geoloc` y haga clic en pegar.
1. Elimine todos los nodos secundarios debajo del nodo /apps/myapp/contextstore/geoloc/dialog/items/items/tab1/items:

   * almacenar
   * propiedades
   * miniatura

1. Haga clic con el botón derecho en el nodo `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` y haga clic en Crear > Crear nodo. Especifique los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: static
   * Tipo: cq:Widget

1. Agregue las siguientes propiedades al nodo:

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | cls | Cadena | x-form-fieldset-description |
   | text | Cadena | El componente geoloc no requiere ninguna configuración. |
   | xtype | Cadena | estático |

1. Haga clic en Guardar todo.

   ![chlimage_1-5](assets/chlimage_1-5.png)

### Creación del script de inicialización {#create-the-initialization-script}

Agregue un archivo init.js.jsp al componente geoloc y utilícelo para crear el almacén de sesiones, recuperar los datos de ubicación y agregarlo al almacén.

El archivo init.js.jsp se ejecuta cuando la página carga Client Context. En este momento, la API de JavaScript de Client Context ya está cargada y disponible para el script.

1. Haga clic con el botón derecho en el nodo /apps/myapp/contextstore/geoloc y haga clic en Crear > Crear archivo. Especifique un Nombre de init.js.jsp y haga clic en Aceptar.
1. Agregue el siguiente código a la parte superior de la página y haga clic en Guardar todo.

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### Procesar los datos del almacén de sesión geolocalizada {#render-the-geoloc-session-store-data}

Agregue el código al archivo JSP del componente geoloc para procesar los datos del almacén en Client Context.

![chlimage_1-6](assets/chlimage_1-6.png)

1. En CRXDE Lite, abra el archivo `/apps/myapp/contextstores/geoloc/geoloc.jsp`.
1. Agregue el siguiente código HTML debajo del código auxiliar:

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. Haga clic en Guardar todo.

### Añadir el componente a Client Context {#add-the-component-to-client-context}

Agregue el componente Almacén de ubicaciones a Client Context para que se inicialice cuando se cargue la página.

1. Abra la página principal de Geometrixx Outdoors en la instancia de autor ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Haga clic en Ctrl-Alt-c (Windows) o control-opción-c (Mac) para abrir Client Context.
1. Haga clic en el icono de edición en la parte superior de Client Context para abrir Client Context Designer.

   ![Editar icono indicado por un lápiz dentro de un cuadrado.](do-not-localize/chlimage_1.png)

1. Arrastre el componente Almacén de ubicaciones a Client Context.

### Consulte la información de ubicación en Client Context {#see-the-location-information-in-client-context}

Abra la página de inicio de Geometrixx Outdoors en modo de edición y, a continuación, abra Client Context para ver los datos del componente Almacén de ubicación.

1. Abra la página en inglés del sitio de Geometrixx Outdoors. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html))
1. Para abrir Client Context, pulse Ctrl-Alt-c (Windows) o control-opción-c (Mac).

## Creación de un Client Context personalizado {#creating-a-customized-client-context}

Para crear un segundo contexto de cliente, duplique la rama:

`/etc/clientcontext/default`

* La subcarpeta:
  `/content`
contiene el contenido del contexto de cliente personalizado.

* La carpeta:
  `/contextstores`
permite definir diferentes configuraciones para las tiendas de contexto.

Para utilizar el contexto de cliente personalizado, edite la propiedad
`path`
en el estilo de diseño del componente contexto de cliente, como se incluye en la plantilla de página. Por ejemplo, como ubicación estándar de:
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
