---
title: Crear apariencias personalizadas para campos de formularios adaptables
description: Personalice el aspecto de los componentes integrados en formularios adaptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 96%

---

# Crear apariencias personalizadas para campos de formularios adaptables{#create-custom-appearances-for-adaptive-form-fields}

## Introducción {#introduction}

Los formularios adaptables utilizan el [marco de trabajo de apariencia](/help/forms/using/introduction-widgets.md) para ayudarle a crear apariencias personalizadas para campos de formularios adaptables y proporcionar una experiencia de usuario diferente. Por ejemplo, reemplace los botones de radio y las casillas de verificación por botones de alternancia o utilice complementos jQuery personalizados para restringir las entradas de los usuarios en campos como números de teléfono o ID de correo electrónico.

En este documento se explica cómo utilizar un complemento jQuery para crear estas experiencias alternativas para campos de formularios adaptables. Además, muestra un ejemplo para crear una apariencia personalizada para que el componente de campo numérico aparezca como un salto numérico o un control deslizante.

Veamos primero los términos y conceptos clave utilizados en este artículo.

**Apariencia** Se refiere al estilo, la apariencia y la organización de varios elementos de un campo de formulario adaptable. Normalmente incluye una etiqueta, un área interactiva para proporcionar entradas, un icono de ayuda y descripciones cortas y largas del campo. La personalización de la apariencia que se describe en este artículo es aplicable a la apariencia del área de entrada del campo.

**Complemento jQuery** Proporciona un mecanismo estándar, basado en el marco de trabajo del widget jQuery, para implementar una apariencia alternativa.

**ClientLib** Es un sistema de bibliotecas del lado del cliente en procesamiento del lado del cliente de AEM impulsado por código CSS y JavaScript complejo. Para obtener más información, consulte Uso de bibliotecas del lado del cliente.

**Arquetipo** Es un conjunto de herramientas de creación de plantillas de proyecto de Maven definidas como patrón o modelo original para los proyectos de Maven. Para obtener más información, consulte Introducción a los tipos de archivo.

**Control de usuario** Se refiere al elemento principal de un widget que contiene el valor del campo y se utiliza en la estructura de la apariencia para enlazar la interfaz de usuario del widget personalizado con el modelo del formulario adaptable.

## Pasos para crear una apariencia personalizada {#steps-to-create-a-custom-appearance}

Los pasos, en un nivel superior, para crear una apariencia personalizada son los siguientes:

1. **Crear un proyecto**: cree un proyecto de Maven que genere un paquete de contenido para implementarlo en AEM.
1. **Ampliar una clase de widget existente**: amplíe una clase de widget existente y anule las clases requeridas.
1. **Crear una biblioteca de cliente**: cree una biblioteca `clientLib: af.customwidget` y agregue los archivos JavaScript y CSS necesarios.

1. **Crear e instalar el proyecto**: cree el proyecto Maven e instale el paquete de contenido generado en AEM.
1. **Actualizar el formulario adaptable**: actualice las propiedades del campo del formulario adaptable para utilizar la apariencia personalizada.

### Crear un proyecto {#create-a-project}

Un arquetipo Maven es un punto de partida para crear una apariencia personalizada. Los detalles del arquetipo a utilizar son los siguientes:

* **Repositorio**: https://repo1.maven.org/maven2/com/adobe/
* **ID del artefacto**: custom-appearance-archetype
* **ID de grupo**: com.adobe.aemforms
* **Versión**: 1.0.4

Ejecute el siguiente comando para crear un proyecto local basado en el arquetipo:

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

El comando descarga los complementos de Maven y la información del arquetipo desde el repositorio y genera un proyecto basado en la siguiente información:

* **groupId**: ID de grupo utilizado por el proyecto Maven generado
* **artifactId**: ID del artefacto utilizado por el proyecto Maven generado.
* **versión**: versión del proyecto Maven generado.
* **paquete**: paquete utilizado para la estructura de archivos.
* **artifactName**: nombre del artefacto del paquete de AEM generado.
* **packageGroup**: grupo de paquetes del paquete de AEM generado.
* **widgetName**: nombre de aspecto que se utiliza como referencia.

El proyecto generado tiene la siguiente estructura:

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### Ampliar una clase de widget existente {#extend-an-existing-widget-class}

Una vez creada la plantilla del proyecto, realice los siguientes cambios según sea necesario:

1. Incluya la dependencia del complemento de terceros al proyecto.

   1. Coloque los complementos de jQuery personalizados o de terceros en la carpeta `jqueryplugin/javascript` y los archivos CSS relacionados en la carpeta `jqueryplugin/css`. Para obtener más información, consulte los archivos JS y CSS en la carpeta `jqueryplugin/javascript and jqueryplugin/css`.

   1. Modifique el `js.txt` y `css.txt` para incluir cualquier archivo JavaScript y CSS adicional del complemento jQuery.

1. Integre el complemento de terceros con el marco para permitir la interacción entre el marco de trabajo de apariencia personalizada y el complemento jQuery. El widget nuevo solo funcionará después de ampliar o de anular las siguientes funciones.

<table>
 <tbody>
  <tr>
   <td><strong>Función</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>La función de procesamiento devuelve el objeto jQuery para el elemento HTML predeterminado del widget. El elemento HTML predeterminado debe ser de tipo enfocable. Por ejemplo, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code> y <code>&lt;li&gt;</code>. El elemento devuelto se usa como <code>$userControl</code>. Si el <code>$userControl</code> especifica la restricción anterior, las funciones de la clase <code>AbstractWidget</code> funcionarán como se espera, de lo contrario, algunas de las API comunes (enfoque, clic) requierirán cambios. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Devuelve un mapa para convertir eventos HTML en eventos XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Este ejemplo muestra que <code>blur</code> es un evento HTML y <code>XFA_EXIT_EVENT</code> es el evento XFA correspondiente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Devuelve un mapa que proporciona detalles sobre la acción que se va a realizar al cambiar una opción. Las claves son las opciones que se proporcionan al widget y los valores son funciones a las que se llama cada vez que se detecta un cambio en la opción. El widget proporciona controladores para todas las opciones comunes (excepto <code>value</code> y <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>El marco de trabajo del widget jQuery carga la función siempre que su valor se guarde en el modelo XFA (por ejemplo, en el evento de salida de un campo de texto). La implementación debe devolver el valor guardado en el widget. El controlador se proporciona con el nuevo valor para la opción.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>De forma predeterminada, en XFA en el evento de entrada, se muestra el <code>rawValue</code> del campo. Esta función se llama para mostrar el <code>rawValue</code> al usuario. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>De forma predeterminada, en XFA en el evento de salida, se muestra el <code>formattedValue</code> del campo. Esta función se llama para mostrar el <code>formattedValue</code> al usuario. </td>
  </tr>
 </tbody>
</table>

1. Actualice el archivo JavaScript en la carpeta `integration/javascript`, según sea necesario.

   * Reemplace el texto `__widgetName__` con el nombre del widget.
   * Amplíe el widget desde una clase de widget adecuada. En la mayoría de los casos, es la clase de widget correspondiente al widget existente que reemplaza. El nombre de clase principal se utiliza en varias ubicaciones, por lo que se recomienda buscar todas las instancias de la cadena `xfaWidget.textField` en el archivo y reemplzarlas por la clase principal real utilizada.
   * Amplíe el método `render` para proporcionar una interfaz de usuario alternativa. Es la ubicación desde la que se invocará el complemento jQuery para actualizar la interfaz de usuario o el comportamiento de la interacción. El método `render` debe devolver un elemento de control de usuario.

   * Amplíe el método `getOptionsMap` para anular cualquier configuración de opción afectada por un cambio en el widget. La función devuelve un mapa que proporciona detalles para que la acción se realice al cambiar una opción. Las claves son las opciones proporcionadas para el widget y los valores son las funciones a las que se llama cada vez que se detecta un cambio en la opción.
   * El método `getEventMap` mapea los eventos activados por el widget, con los eventos requeridos por el modelo de formulario adaptable. El valor predeterminado asigna eventos HTML estándar para el widget predeterminado y debe actualizarse si se activa un evento alternativo.
   * El `showDisplayValue` y `showValue` aplican la cláusula de visualización y de edición de imagen y se pueden sobrescribir para que tengan un comportamiento alternativo.

   * El método `getCommitValue` es invocado por el marco de trabajo de formularios adaptables cuando se produce el evento `commit`. Generalmente, ocurre en el evento de salida, excepto para los elementos de lista desplegable, el botón de radio y la casilla de verificación al cambiar). Para obtener más información, consulte [Expresiones de formularios adaptables](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * El archivo de plantilla proporciona una implementación de muestra para varios métodos. Quite los métodos que no se vayan a ampliar.

### Crear una biblioteca de cliente {#create-a-client-library}

El proyecto de ejemplo generado por el tipo de archivo Maven crea automáticamente las bibliotecas de cliente necesarias y las envuelve en una biblioteca de cliente con una categoría `af.customwidgets`. Los archivos JavaScript y CSS disponibles en el `af.customwidgets` se incluyen automáticamente durante la ejecución.

### Generar e instalar {#build-and-install}

Para crear el proyecto, ejecute el siguiente comando en shell para generar un paquete CRX que necesite instalarse en el servidor de AEM.

`mvn clean install`

>[!NOTE]
>
>El proyecto Maven hace referencia a un repositorio remoto dentro del archivo POM. Esto es solo para fines de referencia y según los estándares Maven, la información del repositorio se captura en el archivo `settings.xml`.

### Actualizar el formulario adaptable {#update-the-adaptive-form}

Para aplicar la apariencia personalizada a un campo de formulario adaptable, haga lo siguiente:

1. Abra el formulario adaptable en modo de edición.
1. Abra el cuadro de diálogo **Propiedad** para el campo en el que desea aplicar la apariencia personalizada.
1. En la pestaña **Estilo**, actualice la propiedad `CSS class` para agregar el nombre de la apariencia en el formato `widget_<widgetName>`. Por ejemplo: **widget_numericstepper**

## Ejemplo: Crear una apariencia personalizada   {#sample-create-a-custom-appearance-nbsp}

Veamos un ejemplo para crear una apariencia personalizada para que un campo numérico aparezca como un salto numérico o un control deslizante. Siga estos pasos:

1. Ejecute el siguiente comando para crear un proyecto local basado en el tipo de archivo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Le solicitará que especifique valores para los siguientes parámetros.
   *Los valores utilizados en esta muestra se resaltan en negrita*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Navegue hasta el directorio `customWidgets` (valor especificado para la propiedad `artifactID`) y ejecute el siguiente comando para generar un proyecto Eclipse:

   `mvn eclipse:eclipse`

1. Abra la herramienta Eclipse y haga lo siguiente para importar el proyecto Eclipse:

   1. Seleccione **[!UICONTROL Archivo > Importar > Proyectos existentes en el espacio de trabajo]**.

   1. Busque y seleccione la carpeta en la que ejecutó el comando `archetype:generate`.

   1. Haga clic en **[!UICONTROL Finalizar]**.

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. Seleccione el widget que se utilizará para la apariencia personalizada. Este ejemplo utiliza el siguiente widget de saltos numéricos:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   En el proyecto Eclipse, revise el código del complemento en el archivo `plugin.js` para asegurarse de que coincida con los requisitos de la apariencia. En este ejemplo, la apariencia visual cumple los siguientes requisitos:

   * El salto numérico debe extenderse desde `- $.xfaWidget.numericInput`.
   * El método `set value` del widget define el valor después de que el foco esté en el campo. Es un requisito obligatorio para un widget de formulario adaptable.
   * El método `render` debe anularse para invocar el método `bootstrapNumber`.

   * No hay dependencia adicional para el complemento que no sea el código fuente principal del complemento.
   * El ejemplo no realiza ningún estilo en el salto, por lo que no se requiere CSS adicional.
   * El objeto `$userControl` debe estar disponible para el método `render`. Es un campo del tipo `text` que se clona con el código del complemento.

   * Los botones **+** y **-** deben deshabilitarse cuando el campo esté deshabilitado.

1. Reemplace el contenido del `bootstrap-number-input.js` (Complemento jQuery) por el contenido del archivo `numericStepper-plugin.js`.
1. En el archivo `numericStepper-widget.js`, agregue el siguiente código para anular el método de procesamiento para invocar el complemento y devolver el objeto `$userControl`:

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. En el archivo `numericStepper-widget.js`, omita la propiedad `getOptionsMap` para anular la opción de acceso y ocultar los botones + y - en modo deshabilitado.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. Guarde los cambios, navegue hasta la carpeta que contenga el archivo `pom.xml` y ejecute el siguiente comando Maven para crear el proyecto:

   `mvn clean install`

1. Instale el paquete mediante el administrador de paquetes de AEM.

1. Abra el formulario adaptable en modo de edición en el que desee aplicar la apariencia personalizada y haga lo siguiente:

   1. Haga clic con el botón derecho en el campo en el que desee aplicar la apariencia y haga clic en **[!UICONTROL Editar]** para abrir el cuadro de diálogo Editar componente.

   1. En la pestaña Estilo, actualice la propiedad **[!UICONTROL clase CSS]** para agregar `widget_numericStepper`.

La nueva apariencia que ha creado ya está disponible para su uso.
