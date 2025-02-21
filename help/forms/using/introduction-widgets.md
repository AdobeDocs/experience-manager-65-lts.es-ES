---
title: Marco de aspecto para formularios adaptables y HTML5
description: Mobile Forms procesa las plantillas de formulario como formularios HTML5. Estos formularios utilizan archivos jQuery, Backbone.js y Underscore.js para el aspecto y para habilitar los scripts.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Mobile Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 100%

---

# Marco de aspecto para formularios adaptables y HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Los formularios (formularios adaptables y formularios HTML5) utilizan las bibliotecas de [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) y [Underscore.js](https://underscorejs.org/) para el aspecto y los scripts. Los formularios también utilizan la arquitectura de los [widgets de la interfaz de usuario](https://jqueryui.com/) **de jQuery** para todos los elementos interactivos (como campos y botones) del formulario. Esta arquitectura permite al desarrollador de formularios utilizar un completo conjunto de widgets y complementos de jQuery disponibles en Forms. También puede implementar lógica específica del formulario al capturar datos de usuarios, como restricciones de leadDigits/trailDigits o la implementación de cláusulas de imagen. Los desarrolladores de formularios pueden crear y utilizar funciones personalizadas para mejorar la experiencia de captura de datos y hacerla más fácil de usar.

Este artículo va dirigido a desarrolladores con los conocimientos adecuados de jQuery y los widgets de jQuery. Proporciona una perspectiva del marco de trabajo de aspecto visual y permite a los desarrolladores crear un aspecto alternativo para un campo de formulario.

El marco de trabajo de aspecto visual se basa en diversas opciones, eventos (activadores) y funciones para capturar las interacciones del usuario con el formulario, y responde a los cambios del modelo para informar al usuario final. Además:

* El marco proporciona un conjunto de opciones para el aspecto de un campo. Estas opciones son pares de clave-valor y se dividen en dos categorías: opciones comunes y opciones específicas de tipo de campo.
* El aspecto, como parte del contrato, activa un conjunto de eventos; por ejemplo, eventos de entrada y salida.
* El aspecto es necesario para implementar un conjunto de funciones. Algunas de las funciones son comunes, mientras que otras son específicas de las funciones de tipo de campo.

## Opciones comunes {#common-options}

A continuación se muestran las opciones globales establecidas. Estas opciones están disponibles para todos los campos.

<table>
 <tbody>
  <tr>
   <th>Propiedad </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Un identificador utilizado para especificar este objeto o evento en expresiones de scripts. Por ejemplo, esta propiedad especifica el nombre de la aplicación host.</td>
  </tr>
  <tr>
   <td>value</td>
   <td>El valor predeterminado del campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Se muestra este valor del campo. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>Los lectores de pantalla utilizan este valor para narrar información sobre el campo. El formulario proporciona el valor, y es posible anularlo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>La posición del campo en la secuencia de tabulación del formulario. Anule tabIndex solo si desea cambiar el orden de tabulación predeterminado del formulario.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>La función del elemento, por ejemplo, Encabezado o Tabla.</td>
  </tr>
  <tr>
   <td>height</td>
   <td>La altura del widget. Se especifica en píxeles. </td>
  </tr>
  <tr>
   <td>width</td>
   <td>La anchura del widget. Se especifica en píxeles.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Los controles utilizados para acceder al contenido de un objeto container, como un subformulario.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>La propiedad para de un elemento XFA del widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>La dirección del texto. Los valores posibles son ltr (de izquierda a derecha) y rtl (de derecha a izquierda).</td>
  </tr>
 </tbody>
</table>

Aparte de estas opciones, el marco proporciona otras opciones que varían según el tipo de campo. A continuación, se muestran los detalles de las opciones específicas de los campos.

### Interacción con el marco de formulario {#interaction-with-forms-framework}

Para interactuar con el marco de formulario, un widget activa una serie de eventos para permitir que funcione el script del formulario. Si el widget no desencadena estos eventos, algunos de los scripts escritos en el formulario para ese campo no funcionan.

#### Eventos activados por el widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Este evento se activa cada vez que el campo está enfocado. Permite que el script de "entrada" se ejecute en el campo. La sintaxis para activar el evento es<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Este evento se activa cada vez que el usuario abandona el campo. Permite que el motor establezca el valor del campo y ejecute su script de "salida". La sintaxis para activar el evento es<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Este suceso se activa para permitir que el motor ejecute el script de "cambio" escrito en el campo. La sintaxis para activar el evento es<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Este evento se activa cada vez que se hace clic en el campo. Permite al motor ejecutar el script de "clic" escrito en el campo. La sintaxis para activar el evento es<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implementadas por widget {#apis-implemented-by-widget}

El marco de apariencia llama a algunas funciones del widget que se implementan en los widgets personalizados. El widget debe implementar las siguientes funciones:

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>enfoque: function()</td>
   <td>Pone el enfoque en el campo.</td>
  </tr>
  <tr>
   <td>clic: function()</td>
   <td>Pone el enfoque en el campo y llama a XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>erorrMessage: cadena </em>representación del error<br /> <em>errorType: cadena ("advertencia"/"error")</em></p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Envía un mensaje de error y un tipo de error al widget. El widget muestra el error.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.</p> </td>
   <td>Se llama a esta función si se corrigen los errores en el campo. El widget oculta el error.</td>
  </tr>
 </tbody>
</table>

## Opciones específicas del tipo de campo {#options-specific-to-type-of-field}

Todos los widgets personalizados deben cumplir las especificaciones anteriores. Para utilizar las funciones de diferentes campos, el widget debe ajustarse a las directrices de ese campo en particular.

### TextEdit: campo de texto {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opción</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>multiline</td>
   <td>El valor es True si el campo admite la introducción de un carácter de nueva línea; en caso contrario, es False.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>El número máximo de caracteres que se pueden introducir en el campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: Aplicable únicamente a los formularios HTML5</p> </td>
   <td>Especifica el comportamiento del campo de texto cuando la anchura del texto supera la anchura del widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opción</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>value<br /> </td>
   <td>La matriz de los valores seleccionados.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>La matriz de objetos que se van a mostrar como opciones. Cada objeto contiene dos propiedades:<br /> save: el valor que desea guardar; display: el valor que desea mostrar.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>editable</p> <p><strong>Nota</strong>: Aplicable solo para formularios HTML5.<br /> </p> </td>
   <td>Si el valor es True, la entrada de texto personalizado está habilitada en el widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>La matriz de los valores que se van a mostrar.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>El valor es True si se permiten varias selecciones; en caso contrario, es False.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: el objeto que contiene el valor de visualización y guardado <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;save Value&gt;}</em></p> </td>
   <td>Agrega un elemento a la lista.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex: el índice del elemento que se va a eliminar de la lista<br /> </em><br /> <br /> </td>
   <td>Elimina una opción de la lista.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Borra todas las opciones de la lista.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| Opciones | Descripción |
|---|---|
| dataType | Cadena que representa el tipo de datos del campo (entero/decimal). |
| leadDigits | El máximo de dígitos iniciales permitido en el número decimal. |
| fracDigits | El máximo de dígitos de fracción permitidos en el número decimal. |
| zero | La representación de cadena del cero en la configuración regional del campo. |
| decimal | La representación de cadena del decimal en la configuración regional del campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opciones</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>La matriz de valores (activado/desactivado/neutro).</p> <p>Es una matriz de valores para los diferentes estados de checkButton. values[0] es el valor cuando el estado está ACTIVADO, values[1] es el valor cuando el estado está DESACTIVADO,<br /> values[2] es el valor cuando el estado es NEUTRAL. La longitud de la matriz de valores es igual a la opción Valor de estado.<br /> </p> </td>
  </tr>
  <tr>
   <td>states</td>
   <td><p>El número de estados permitidos. </p> <p>Dos para los formularios adaptables (Activado, Desactivado) y tres para los formularios HTML5 (Activado, Desactivado, Neutro).</p> </td>
  </tr>
  <tr>
   <td>state</td>
   <td><p>El estado actual del elemento.</p> <p>Dos para los formularios adaptables (Activado, Desactivado) y tres para los formularios HTML5 (Activado, Desactivado, Neutro).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Opción | Descripción |
|---|---|
| days | El nombre localizado de los días para ese campo. |
| months | El nombre localizado de los meses para ese campo. |
| zero | El texto localizado para el número 0. |
| clearText | El texto localizado para el botón Borrar. |
