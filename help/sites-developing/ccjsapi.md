---
title: API de JavaScript de ClientContext
description: Obtenga información acerca de la API de JavaScript para Client Context en Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub,Developing,Personalization
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 2%

---

# API de JavaScript de ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

El objeto CQ_Analytics.ClientContextMgr es un objeto singleton que contiene un conjunto de almacenes de sesiones registrados automáticamente y proporciona métodos para registrar, mantener y administrar los almacenes de sesiones.

Amplía CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(nombre) {#getregisteredstore-name}

Devuelve un almacén de sesiones con un nombre especificado. Consulte también [Acceso a un almacén de sesión](/help/sites-developing/client-context.md#accessing-session-stores).

**Parámetros**

* name: String. Nombre del almacén de sesión.

**Devuelve**

Objeto CQ_Analytics.SessionStore que representa el almacén de sesión del nombre dado. Devuelve `null` cuando no existe ningún almacén del nombre dado.

#### register(sessionstore) {#register-sessionstore}

Registra un almacén de sesión con Client Context. Activa los eventos storeregister y storeupdate una vez completados.

**Parámetros**

* sessionstore: CQ_Analytics.SessionStore. El objeto de almacén de sesiones que se va a registrar.

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Proporciona métodos para detectar la activación y el registro del almacén de sesiones. Vea también [Comprobar que se ha definido e inicializado un almacén de sesión](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una función de llamada de retorno que se llama cuando se inicializa un almacén de sesión. En el caso de las tiendas que se inicialicen varias veces, especifique un retraso de devolución de llamada para que se llame a la función de devolución de llamada solo una vez:

* Cuando el almacén se inicializa durante el período de retardo de una inicialización anterior, se cancela la llamada a la función anterior y se vuelve a llamar a la función para la inicialización actual.
* Si el periodo de retardo transcurre antes de que se produzca una inicialización posterior, la función de llamada de retorno se ejecuta dos veces.

Por ejemplo, un almacén de sesiones se basa en un objeto JSON y se recupera mediante una solicitud JSON. Los siguientes escenarios de inicialización son posibles:

* La solicitud se completa, los datos se recuperan y se cargan en el almacén. En este caso, la inicialización se produce una vez.
* La solicitud falla (tiempo de espera). En este caso, la inicialización no se produce y no hay datos en el almacén.
* El almacén se rellena previamente con valores predeterminados (propiedades init), pero la solicitud falla (tiempo de espera). Solo hay una inicialización con valores predeterminados.
* El almacén se rellena previamente.

Cuando el retraso se establece en `true` o varios milisegundos, el método espera antes de llamar al método de devolución de llamada. Si se activa otro evento de inicialización antes de que transcurra el retraso, esperará hasta que se supere el tiempo de retraso sin que se produzca ningún evento de inicialización. Esto permite esperar a que se active un segundo evento de inicialización y llama a la función de llamada de retorno en el caso más óptimo.

**Parámetros**

* storeName: String. Nombre del almacén de sesiones para agregar el detector.
* callback: Función. La función a la que se llama tras la inicialización de la tienda.
* delay: booleano o número. La cantidad de tiempo para retrasar la llamada a la función de llamada de retorno, en milisegundos. Un valor booleano de `true` usa el retraso predeterminado de `200 ms`. Si se usa un valor booleano de `false` o un número negativo, no se producirá ningún retraso.

**Devuelve**

No hay valor devuelto.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una función de llamada de retorno que se llama cuando se registra un almacén de sesión. El evento register se produce cuando se registra un almacén en [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parámetros**

* storeName: String. Nombre del almacén de sesiones para agregar el detector.
* callback: Función. La función a la que se llama tras la inicialización de la tienda.

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Almacén de sesiones no persistente que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo. Utilice el método `getInstance` o `getRegisteredInstance` para crear una instancia de esta clase.

Amplía CQ_Analytics.JSONStore.

### Propiedades {#properties}

Consulte CQ_Analytics.JSONStore y CQ_Analytics.SessionStore para obtener las propiedades heredadas.

### Métodos {#methods-2}

Consulte también CQ_Analytics.JSONStore y CQ_Analytics.SessionStore para conocer los métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un objeto CQ_Analytics.JSONPStore.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona ningún nombre de almacén, el método devuelve nulo.
* serviceURL: String. La URL del servicio JSONP
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* deferLoading: (Opcional) Boolean. El valor true evita que se llame al servicio JSONP cuando se cree el objeto. El valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) String. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.JSONPStore o nulo si storeName es nulo.

#### getServiceURL() {#getserviceurl}

Recupera la dirección URL del servicio JSONP que este objeto utiliza para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio, o nula si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Llama al servicio JSONP. La URL de JSONP es la URL de servicio con el sufijo correspondiente a una función de devolución de llamada.

**Parámetros**

* serviceURL: (Opcional) String. El servicio JSONP al que llamar. Un valor nulo hace que se utilice la URL de servicio ya configurada. Un valor no nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* callback: (opcional) cadena. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No hay valor devuelto.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un objeto CQ_Analytics.JSONPStore y registra el almacén con Client Context.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona ningún nombre de almacén, el método devuelve nulo.
* serviceURL: (Opcional) String. La URL del servicio JSONP.
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* callback: (opcional) cadena. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Establece la dirección URL del servicio JSONP que se utiliza para recuperar datos JSON.

**Parámetros**

* serviceURL: String. La URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Un contenedor para un objeto JSON. Cree una instancia de esta clase para crear un almacén de sesiones no persistente que contenga datos JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Puede definir un conjunto de datos que rellene el almacén tras la inicialización.

Amplía CQ_Analytics.SessionStore.

### Propiedades {#properties-1}

#### LLAVE DE TIENDA {#storekey}

La clave que identifica el almacén. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename}

El nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-3}

Consulte también CQ_Analytics.SessionStore para conocer los métodos heredados.

#### clear() {#clear}

Quita los datos del almacén de sesiones y todas las propiedades de inicialización.

**Parámetros**

Ninguna.

**Devuelve**

No hay valor devuelto.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONtore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON).

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera los datos del almacén de sesión en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Un objeto que representa los datos de almacén en formato JSON.

#### init() {#init}

Borra el almacén de sesiones y lo inicializa con la propiedad de inicialización. Establece el indicador de inicialización en `true` y, a continuación, activa los eventos `initialize` y `update`.

**Parámetros**

Ninguna.

**Devuelve**

No se han devuelto datos.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crea propiedades de inicialización a partir de los datos de un objeto JSON. Si lo desea, puede eliminar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos del objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Para este ejemplo, se crean las siguientes propiedades en el almacén:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: El valor true conserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. El valor false elimina las propiedades de inicialización existentes antes de agregar las derivadas del objeto JSON.

**Devuelve**

No hay valor devuelto.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un objeto CQ_Analytics.JSONtore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON). El nuevo objeto se registra automáticamente con la Cloud Manager de flujo de navegación.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Activa eventos y permite que otros objetos escuchen estos eventos y reaccionen. Las clases que amplían esta clase pueden desencadenar eventos que hacen que se llame a los agentes de escucha.

### Métodos {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra un oyente para un evento. Consulte también [Creación de un agente de escucha para reaccionar ante una actualización de almacén de sesión](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parámetros**

* event: String. Nombre del evento que se va a escuchar.
* fct: Function. Función a la que se llama cuando se produce el evento.
* scope: (opcional) objeto. Ámbito en el que ejecutar la función de controlador. El contexto &quot;this&quot; de la función del controlador.

**Devuelve**

No hay valor devuelto.

#### removeListener(event, fct) {#removelistener-event-fct}

Quita el controlador de eventos dado para un evento.

**Parámetros**

* event: String. Nombre del evento.
* fct: Function. El controlador de eventos.

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Un contenedor persistente de un objeto JSON recuperado de un servicio JSONP remoto.

Extiende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte también CQ_Analytics.PersistedJSONStore para obtener métodos heredados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona ningún nombre de almacén, el método devuelve nulo.
* serviceURL: String. La URL del servicio JSONP
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* deferLoading: (Opcional) Boolean. El valor true evita que se llame al servicio JSONP cuando se cree el objeto. El valor false hace que se llame al servicio JSONP.
* loadingCallback: (Opcional) String. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El nuevo objeto CQ_Analytics.PersistedJSONPStore o nulo si storeName es nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera la dirección URL del servicio JSONP que este objeto utiliza para recuperar datos JSON.

**Parámetros**

Ninguna.

**Devuelve**

Cadena que representa la dirección URL del servicio, o nula si no se ha configurado ninguna dirección URL del servicio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Llama al servicio JSONP. La URL de JSONP es la URL de servicio con el sufijo correspondiente a una función de devolución de llamada.

**Parámetros**

* serviceURL: (Opcional) String. El servicio JSONP al que llamar. Un valor nulo hace que se utilice la URL de servicio ya configurada. Un valor no nulo establece el servicio JSONP que se utilizará para este objeto. (Consulte setServiceURL.)
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* callback: (opcional) cadena. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

No hay valor devuelto.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un objeto CQ_Analytics.PersistedJSONPStore y registra el almacén con Client Context.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas. Si no se proporciona ningún nombre de almacén, el método devuelve nulo.
* serviceURL: (Opcional) String. La URL del servicio JSONP.
* dynamicData: (opcional) objeto. Datos JSON que se anexan a los datos de inicialización del almacén antes de llamar a la función de devolución de llamada.
* callback: (opcional) cadena. Nombre de la función a la que se llama para procesar el objeto JSONP que devuelve el servicio JSONP. La función de llamada de retorno debe definir un único parámetro que sea un objeto CQ_Analytics.JSONPStore.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Establece la dirección URL del servicio JSONP que se utiliza para recuperar datos JSON.

**Parámetros**

* serviceURL: String. La URL del servicio JSONP que proporciona datos JSON

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Un contenedor persistente de un objeto JSON.

Extiende `CQ_Analytics.PersistedSessionStore`.

### Propiedades {#properties-2}

#### LLAVE DE TIENDA {#storekey-1}

La clave que identifica el almacén. Utilice el método `getInstance` para recuperar este valor.

#### STORENAME {#storename-1}

El nombre de la tienda. Utilice el método `getInstance` para recuperar este valor.

### Métodos {#methods-6}

Consulte también CQ_Analytics.PersistedSessionStore para obtener métodos heredados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONtore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON).

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera los datos del almacén de sesión en formato JSON.

**Parámetros**

Ninguna.

**Devuelve**

Un objeto que representa los datos de almacén en formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crea propiedades de inicialización a partir de los datos de un objeto JSON. Si lo desea, puede eliminar todas las propiedades de inicialización existentes.

Los nombres de las propiedades se derivan de la jerarquía de los datos del objeto JSON. El siguiente código de ejemplo representa un objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Para este ejemplo, se crean las siguientes propiedades en el almacén:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parámetros**

* jsonData: un objeto JSON que contiene los datos que se van a almacenar.
* doNotClear: El valor true conserva las propiedades de inicialización existentes y agrega las derivadas del objeto JSON. El valor false elimina las propiedades de inicialización existentes antes de agregar las derivadas del objeto JSON.

**Devuelve**

No hay valor devuelto.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un objeto CQ_Analytics.PersistedJSONtore con un nombre determinado e inicializado con los datos JSON dados (llama al método initJSON). El nuevo objeto se registra automáticamente con Client Context Manager.

**Parámetros**

* storeName: String. Nombre que se utilizará como propiedad STORENAME. El valor de la propiedad STOREKEY se establece en storeName con todos los caracteres en mayúsculas.
* jsonData: objeto. Un objeto que contiene datos JSON.

**Devuelve**

El objeto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Un contenedor de propiedades y valores. Los datos se mantienen mediante CQ_Analytics.SessionPersistence. Cree una instancia de esta clase para crear un almacén de sesiones persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Amplía CQ_Analytics.SessionStore.

### Propiedades {#properties-3}

#### LLAVE DE TIENDA {#storekey-2}

El valor predeterminado es `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para conocer los métodos heredados.

Cuando se usan los métodos heredados `clear`, `setProperty`, `setProperties`, `removeProperty` para cambiar los datos del almacén, los cambios persisten automáticamente, a menos que las propiedades modificadas estén marcadas como notPersisted.

#### getStoreKey() {#getstorekey}

Recupera la propiedad `STOREKEY`.

**Parámetros**

Ninguno

**Devuelve**

Valor de la propiedad `STOREKEY`.

#### isPersisted(nombre) {#ispersisted-name}

Determina si una propiedad de datos se mantiene.

**Parámetros**

* name: String. Nombre de la propiedad.

**Devuelve**

Un valor booleano de `true` si la propiedad persiste, y un valor de `false` si el valor no es una propiedad persistente.

#### persistst() {#persist}

Conserva el almacén de sesiones. El modo de persistencia predeterminado usa el explorador `localStorage` con `ClientSidePersistence` como nombre ( `window.localStorage.set("ClientSidePersistance", store);`)

Si localStorage no está disponible ni se puede escribir, el almacén se mantiene como propiedad de la ventana.

Activa el evento `persist` al finalizar.

**Parámetros**

Ninguno

**Devuelve**

No hay valor devuelto.

#### reset(deferEvent) {#reset-deferevent}

Quita todas las propiedades de datos del almacén y lo mantiene. Opcionalmente, no activa el evento `udpate` al finalizar.

**Parámetros**

* deferEvent: Un valor true evita que se active el evento `update`. Un valor de `false` hace que el evento de actualización se active.

**Devuelve**

No hay valor devuelto.

#### setNonPersisted(nombre) {#setnonpersisted-name}

Marca una propiedad de datos como no persistente.

**Parámetros**

* name: String. Nombre de la propiedad que no se va a mantener.

**Devuelve**

No hay valor devuelto.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore representa un almacén de sesión. Cree una instancia de esta clase para crear un almacén de sesiones:

`mystore = new CQ_Analytics.SessionStore`

Extiende CQ_Analytics.Observable.

### Propiedades {#properties-4}

#### STORENAME {#storename-2}

Nombre del almacén de sesión. Utilice getName para recuperar el valor de esta propiedad.

### Métodos {#methods-8}

#### addInitProperty(nombre, valor) {#addinitproperty-name-value}

Agrega una propiedad y un valor a los datos de inicialización del almacén de sesión.

Utilice loadInitProperties para rellenar los datos del almacén de sesión con los valores de inicialización.

**Parámetros**

* name: String. Nombre de la propiedad que se va a agregar.
* value: String. El valor de la propiedad que se va a agregar.

**Devuelve**

No hay valor devuelto.

#### clear() {#clear-1}

Quita todas las propiedades de datos del almacén.

**Parámetros**

Ninguna.

**Devuelve**

No hay valor devuelto.

#### getData(excluido) {#getdata-excluded}

Devuelve los datos del almacén. Opcionalmente, excluye las propiedades de nombre de los datos. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (opcional) matriz de nombres de propiedad que se excluirán de los datos devueltos.

**Devuelve**

Un objeto de propiedades y sus valores.

#### getInitProperty(nombre) {#getinitproperty-name}

Recupera el valor de una propiedad de datos.

**Parámetros**

* name: String. Nombre de la propiedad de datos que se va a recuperar.

**Devuelve**

El valor de la propiedad de datos. Devuelve `null` si el almacén de sesión no contiene ninguna propiedad del nombre dado.

#### getName() {#getname}

Devuelve el nombre del almacén de sesión.

**Parámetros**

Ninguna.

**Devuelve**

Valor de tipo String que representa el nombre del almacén.

#### getProperty(nombre, sin procesar) {#getproperty-name-raw}

Devuelve el valor de una propiedad. El valor se devuelve como propiedad sin procesar o como valor filtrado por XSS. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: String. Nombre de la propiedad de datos que se va a recuperar.
* raw: booleano. Un valor true hace que se devuelva el valor de la propiedad raw. Un valor false hace que el valor devuelto esté filtrado por XSS.

**Devuelve**

El valor de la propiedad de datos.

#### getPropertyNames(excluido) {#getpropertynames-excluded}

Devuelve los nombres de las propiedades que contiene el almacén de sesión. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

excluido: (opcional) matriz de nombres de propiedad que se omitirán de los resultados.

**Devuelve**

Matriz de valores de tipo String que representan los nombres de las propiedades de sesión.

#### getSessionStore() {#getsessionstore}

Devuelve el almacén de sesiones adjunto al objeto actual.

**Parámetros**

Ninguna.

**Devuelve**

esta

#### init() {#init-1}

Marca el almacén como inicializado y activa el evento `initialize`.

**Parámetros**

Ninguna.

**Devuelve**

No hay valor devuelto.

#### isInitialized() {#isinitialized}

Indica si el almacén de sesiones está inicializado.

**Parámetros**

Ninguna.

**Devuelve**

Un valor de `true` si se inicializa el almacén, y un valor de `false` si no se inicializa el almacén.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Agrega las propiedades de un objeto determinado a los datos de inicialización del almacén de sesiones. De forma opcional, los datos de objeto también se añaden al almacén de datos.

**Parámetros**

* obj: objeto que contiene propiedades enumerables.
* setValues: cuando es true, las propiedades de objeto se agregan a los datos del almacén de sesión si estos no incluyen ya una propiedad del mismo nombre. Cuando es false, no se agregan datos a los datos del almacén de sesión.

**Devuelve**

No hay valor devuelto.

#### removeProperty(nombre) {#removeproperty-name}

Quita una propiedad del almacén de sesión. Activa el evento `update` al finalizar. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: String. Nombre de la propiedad que se va a quitar.

**Devuelve**

No hay valor devuelto.

#### reset() {#reset}

Restaura los valores iniciales del almacén de datos. La implementación predeterminada simplemente elimina todos los datos. Activa el evento `update` al finalizar.

**Parámetros**

Ninguna.

**Devuelve**

No hay valor devuelto.

#### setProperties(properties) {#setproperties-properties}

Establece los valores de varias propiedades. Activa el evento `update` al finalizar. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* Properties: objeto. Objeto que contiene propiedades enumerables. Cada nombre y valor de propiedad se agrega al almacén.

**Devuelve**

No hay valor devuelto.

#### setProperty(nombre, valor) {#setproperty-name-value}

Establece el valor de una propiedad. Activa el evento `update` al finalizar. Llama al método `init` si la propiedad data del almacén no existe.

**Parámetros**

* name: String. Nombre de la propiedad.
* value: String. Valor de propiedad.

**Devuelve**

No hay valor devuelto.
