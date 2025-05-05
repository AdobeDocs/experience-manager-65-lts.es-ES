---
title: API de Form Bridge para formularios HTML5
description: Las aplicaciones externas utilizan la API de FormBridge para conectarse al formulario móvil XFA. La API distribuye un evento FormBridgeInitialized en la ventana principal.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 95%

---

# API de Form Bridge para formularios HTML5 {#form-bridge-apis-for-html-forms}

Puede utilizar las API de Form Bridge para abrir un canal de comunicación entre los formularios HTML5 basados en XFA y las aplicaciones. Las API de Form Bridge proporcionan una API de **Connect** para crear la conexión.

La API de **Connect** acepta un controlador como argumento. Después de crear correctamente una conexión entre el formulario HTML5 basado en XFA y Form Bridge, se invoca el controlador.

Puede utilizar el siguiente código de ejemplo para crear la conexión.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Asegúrese de crear una conexión antes de incluir el archivo formRuntime.jsp.

## API de Form Bridge disponible  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**:

devuelve el número de versión de la biblioteca de scripts.

* **Entrada**: ninguna.
* **Salida**: el número de versión de la biblioteca de scripts.
* **Errores**: ninguno.

**isConnected()**: comprueba si el estado del formulario se ha inicializado.

* **Entrada**: ninguna.
* **Salida**: **True** si el estado del formulario XFA se ha inicializado.

* **Errores**: ninguno.

**connect(handler, context)**: realiza una conexión con FormBridge y ejecuta la función después de establecer la conexión y de inicializar el estado del formulario.

* **Entrada**:

   * **handler**: la función que se ejecuta después de conectar Form Bridge.
   * **context**: el objeto en el que se establece el contexto (este) de la función *handler*.

* **Salida**: ninguna.
* **Error**: ninguno.

**getDataXML(options)**: devuelve los datos del formulario actual en formato XML.

* **Entrada:**

   * **options:** un objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: la función del controlador de errores.
      * **success**: la función del controlador de éxito. Esta función pasa a un objeto que contiene XML en la propiedad *data*.
      * **context**: el objeto en el que se establece el contexto (este) de la función *success*.
      * **validationChecker**: la función a la que se llama para comprobar los errores de validación recibidos del servidor. La función de validación se pasa a una matriz de cadenas de error.
      * **formState**: el estado JSON del formulario XFA para el que se debe devolver un XML de datos. Si no se especifica, devuelve el XML de datos del formulario procesado actualmente.

* **Salida:** ninguna.
* **Error:** ninguno.

**registerConfig(configName, config)**: registra las configuraciones específicas del usuario/portal con FormBridge. Estas configuraciones anulan las configuraciones predeterminadas. Las configuraciones admitidas se especifican en la sección de configuración.

* **Entrada:**

   * **configName:** el nombre de la configuración que desea anular.

      * **widgetConfig:** permite que el usuario anule los widgets predeterminados del formulario con widgets personalizados. La configuración se anula de la siguiente forma:

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&ast;configuration&ast;/})*

      * **pagingConfig:** permite al usuario anular el comportamiento predeterminado al procesar solo la primera página. La configuración se anula de la siguiente forma:

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** permite al usuario anular el nivel de registro, desactivar el registro de una categoría, mostrar la consola de registros o realizar el envío al servidor. La configuración se puede anular de la siguiente forma:

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig:** permita que los usuarios registren los servicios proxy de envío y registrador.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **config:** el valor de la configuración.

* **Salida:** el objeto que contiene el valor original de la configuración en la propiedad *data*.

* **Error:** ninguno.

**hideFields(fieldArray)**: oculta los campos cuyas expresiones Som se proporcionan en fieldArray. Establece la propiedad presence de los campos especificados como invisible

* **Entrada:**

   * **fieldArray:** la matriz de expresiones Som para los campos que desea ocultar.

* **Salida:** ninguna.
* **Error:** ninguno.

**showFields(fieldArray)**: muestra los campos cuyas expresiones Som se proporcionan en fieldArray. Establece la propiedad presence de los campos proporcionados como visible

* **Entrada:**

   * **fieldArray:** la matriz de expresiones Som para los campos que se van a mostrar.

* **Salida:** ninguna.
* **Error:** ninguno.

**hideSubmitButtons()**: oculta todos los botones de envío del formulario.

* **Entrada**: ninguna.
* **Salida**: ninguna.
* **Error**: inicia una excepción si el estado del formulario no está inicializado.

**getFormState()**: devuelve el JSON que representa el estado del formulario.

* **Entrada:** ninguna.
* **Salida:** el objeto que contiene el JSON que representa el estado del formulario actual en la propiedad *data*.

* **Error:** ninguno.

**restoreFormState(options)**: restaura el estado del formulario a partir del estado JSON proporcionado en el objeto options. Se aplica el estado y se llama a los controladores de éxito o de error una vez finalizada la operación

* **Entrada:**

   * **Options:** un objeto JavaScript que contiene las siguientes propiedades:

      * **Error**: la función del controlador de errores.
      * **success**: la función del controlador de éxito.
      * **context**: El objeto en el que se establece el contexto (este) de la función *success*.
      * **formState**: el estado JSON del formulario. El formulario se restaura al estado JSON.

* **Salida:** ninguna.
* **Error:** ninguno.

**setFocus (som)**: establece el enfoque en el campo especificado en la expresión Som.

* **Entrada:** la expresión Som del campo en el que se va a establecer el enfoque.
* **Salida:** ninguna.
* **Error:** inicia una excepción si hay una expresión Som incorrecta

**setFieldValue (som, value)**: establece el valor de los campos para las expresiones Som dadas.

* **Entrada:**

   * **som:** la matriz que contiene las expresiones Som del campo. La expresión Som para establecer el valor de los campos.
   * **value:** la matriz que contiene los valores correspondientes a las expresiones Som proporcionadas en una matriz **som**. Si el tipo de datos del valor no es el mismo que fieldType, el valor no se modifica.

* **Salida:** ninguna.
* **Error:** inicia una excepción si hay una expresión Som incorrecta

**getFieldValue (som)**: devuelve el valor de los campos de las expresiones Som dadas.

* **Entrada:** la matriz que contiene las expresiones Som de los campos cuyo valor debe recuperarse.
* **Salida:** el objeto que contiene el resultado como matriz en la propiedad **data**.

* **Error:** ninguno.

### Ejemplo de la API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)**: recupera la lista de valores de la propiedad dada de los campos especificados en las expresiones Som.

* **Entrada:**

   * **som:** la matriz que contiene las expresiones Som de los campos.
   * **property**: el nombre de la propiedad cuyo valor es obligatorio.

* **Salida:** el objeto que contiene el resultado como matriz en la propiedad *data*.

* **Error:** ninguno.

**setFieldProperties(som, property, values)**: establece el valor de la propiedad dada para todos los campos especificados en las expresiones Som.

* **Entrada:**

   * **som:** la matriz que contiene las expresiones Som de los campos cuyo valor debe establecerse.
   * **property**: la propiedad cuyo valor debe establecerse.
   * **value:** la matriz que contiene los valores de la propiedad dada para los campos especificados en las expresiones Som.

* **Salida:** ninguna.
* **Error:** ninguno.

## Ejemplo de uso de la API de Form Bridge {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
