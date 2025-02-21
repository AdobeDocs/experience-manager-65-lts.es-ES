---
title: Crear estilos CSS para formularios HTML5
description: Aprenda a cambiar el aspecto de los formularios HTML5 al modificar la clase CSS asociada al elemento del formulario HTML.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 100%

---

# Crear estilos CSS para formularios HTML5 {#creating-css-styles-for-html-forms}

La representación HTML5 de una plantilla de formulario basada en XFA consta de varios elementos HTML. Estos elementos se organizan en un orden. Cada elemento tiene clases CSS bien definidas. Puede utilizar estas clases CSS para seleccionar y cambiar el aspecto de un elemento.

>[!NOTE]
>
>En las clases CSS, no cambie el valor de los atributos anchura, altura, grosor del borde, arriba, izquierda, derecha, abajo, relleno, margen y otra posición y tamaño. Cualquier cambio en los atributos de posición y tamaño produce cambios en la presentación del formulario.

## Clases CSS para elementos  {#css-classes-nbsp-for-elements-nbsp}

Cada elemento contiene clases CSS bien definidas. Puede modificar estas clases para cambiar el aspecto de un elemento. Todos los elementos, excepto los de campo y dibujo, tienen dos clases CSS: Tipo y Nombre.

* La **clase Tipo** representa el tipo del campo XFA. Puede anular la clase `type` para modificar los estilos de todos los elementos de un tipo concreto.

* La **clase Nombre** corresponde al nombre del campo XFA. Puede anular la clase `name` para modificar y aplicar estilo personalizado a un elemento.

>[!NOTE]
>
>Algunos elementos XFA no tienen nombre. Para cambiar los estilos de dichos componentes, modifique todos los componentes de ese tipo concreto.

Para las páginas no nombradas en AEM Forms Designer, las páginas de un formulario HTML5 reciben un nombre en el orden creciente de su número. Por ejemplo, para un formulario HTML5 con dos páginas, las páginas se denominarán Página1, Página2.

## Elemento de campo {#field-element}

El elemento de campo contiene dos elementos anidados: widget y pie de ilustración.

**Elemento Widget**

El elemento widget contiene el elemento de interfaz de usuario para la interacción con los usuarios. Tiene tres clases CSS:

* **Widget**: cada widget tiene esta clase.
* **Nombre**: todos los widgets enviados con AEM contienen la clase de widget Nombre. Para los widgets personalizados, el desarrollador de widgets proporciona la clase de widget Nombre.
* **Tipo**: cada widget tiene un elemento de interfaz de usuario. Esta clase define el tipo del elemento de interfaz de usuario.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Además de las clases Tipo y Nombre, el componente de campo también contiene una clase CSS adicional denominada **subtipo**. Un subtipo identifica qué tipo de campo es, por ejemplo, NumericField, DateField, TextField. Puede anular la clase subtipo para modificar el estilo de todos los campos de este tipo.

## Clases CSS para diferentes componentes {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nombre</strong></td>
  </tr>
  <tr>
   <td>Página</td>
   <td>página</td>
   <td>Usuario<br /> o<br /> Página&lt;pageNumber&gt; definidos por el usuario (predeterminado)</td>
  </tr>
  <tr>
   <td>Área de contenido</td>
   <td>contentArea</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Subformulario</td>
   <td>subformulario</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Grupo de exclusión</td>
   <td>exclGroup</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Dibujar</td>
   <td>draw</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Campo</td>
   <td>field</td>
   <td>Nombre definido por el usuario</td>
  </tr>
  <tr>
   <td>Pie de ilustración</td>
   <td>caption</td>
   <td>ND</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>Lo define el desarrollador de widgets (para widgets definidos por el usuario, consulte la tabla en la siguiente sección)</td>
  </tr>
 </tbody>
</table>

## Clases CSS para diferentes campos {#css-classes-for-different-fields}

AEM Forms Designer admite distintos tipos de campos en un formulario, como NumericField, DecimalField y Date Field. Todos estos campos del HTML contienen las clases CSS mencionadas anteriormente. También contienen algunas clases adicionales según el tipo de campo.

Cada campo tiene un widget asociado que representa el elemento de la IU. A continuación se enumeran las clases de cada campo y los widgets asociados a ellos.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de campo</strong></td>
   <td><strong>Subtipo</strong></td>
   <td><strong>Nombre del widget</strong></td>
   <td><strong>Tipo de widget</strong></td>
   <td><strong>Etiqueta de la interfaz de usuario del HTML</strong></td>
  </tr>
  <tr>
   <td>Botón<br type="_moz" /> </td>
   <td>ND</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiofield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Clases CSS para diferentes elementos de dibujo {#css-classes-for-different-draw-elements}

Puede insertar elementos de dibujo estáticos, como texto e imágenes, mediante AEM Forms Designer. Para cada elemento de dibujo, se asocia una clase CSS distinta a ese elemento. La lista de clases CSS para los elementos de dibujo es la siguiente. Cada elemento de dibujo tiene una clase de dibujo asociada.

| **Tipo de dibujo** | **Clase de CSS** |
|---|---|
| Texto | text |
| Imagen | image |
| Rectángulo | rectangle |
| Línea | line |

## Aplicar estilo a otras partes del formulario {#styling-other-parts-of-the-form}

Además de la apariencia de los componentes de la interfaz de usuario del formulario HTML, puede cambiar el estilo de elementos como los errores y las advertencias dentro de la línea y los campos con errores de validación.

`Styling Inline Errors`

Cuando la validación de un campo da lugar a un error, se muestra un error de dentro de la línea cuando el campo está activo. Para cambiar el estilo de los errores de dentro de la línea, anule el CSS ID **error-msg**

`Styling Inline Warnings`

Cuando la validación de un campo da lugar a una advertencia, se muestra una advertencia dentro de la línea cuando el campo está activo. Para cambiar el estilo de las advertencias de dentro de la línea, anule el CSS ID **warning-msg**

`Styling Fields with Validation Errors`

Cuando la validación de un campo falle, el estilo del widget cambiará. Este cambio de estilo se realiza al aplicar una clase CSS **widgetError** en el componente Widget. Para modificar el estilo predeterminado, anule la clase **widgetError**.
