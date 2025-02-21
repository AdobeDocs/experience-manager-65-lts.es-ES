---
title: Compatibilidad con scripts para formularios HTML5
description: JavaScript, propiedades de FormCalc y otros métodos compatibles con formularios HTML5.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3916'
ht-degree: 92%

---

# Compatibilidad con scripts para formularios HTML5 {#scripting-support-for-html-forms}

Las propiedades de JavaScript, FormCalc y los métodos compatibles con los formularios HTML5 son los siguientes:

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>Propiedad </th>
   <th>Descripción<br /> </th>
   <th>Excepción</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>Especifica el contenido del campo antes de los cambios determinados por las acciones de un usuario. El valor puede recuperarse de la misma manera que una función deshacer.</td>
   <td><p>No funciona para cuadros de lista y listas desplegables. <code>PrevText </code> no funciona correctamente en los siguientes casos:</p>
    <ul>
     <li>Al escribir caracteres especiales (por ejemplo, $ o , o &amp; o @ y más) en los campos numéricos de iPad, y </li>
     <li>Para el campo Fecha (cuando la fecha se introduce mediante el calendario).<br /> </li>
    </ul> <p>No es compatible la configuración del valor mediante script.</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>Especifica el objeto sobre el que actúa el evento.</td>
   <td>No es compatible la configuración del valor mediante script.<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>Especifica el contenido del campo después de los cambios determinados por las acciones de un usuario.</td>
   <td><p>La propiedad <code>newText</code> no funciona correctamente en los siguientes casos:</p>
    <ul>
     <li>Al seleccionar o reemplazar textos</li>
     <li>Al eliminar, copiar y pegar textos.</li>
     <li>Al escribir caracteres especiales (por ejemplo, $ o , o &amp; o @ y más) en los campos numéricos<br /> </li>
     <li>Al utilizar la combinación Mayús+alfanumérico. </li>
     <li>Al usar los campos de fecha y hora.</li>
    </ul>
    <div>
      No es compatible la configuración del valor mediante script.
    </div> </td>
  </tr>
  <tr>
   <td>change</td>
   <td>Especifica el valor que un usuario escribe o pega en un campo inmediatamente después de realizar la acción. </td>
   <td><p>La propiedad change no funciona correctamente en los siguientes casos:</p>
    <ul>
     <li>Al seleccionar o reemplazar textos</li>
     <li>Al eliminar, copiar y pegar textos.</li>
     <li>Al escribir caracteres especiales (por ejemplo, $ o , o &amp; o @ y más) en los campos numéricos<br /> </li>
     <li>Al utilizar la combinación Mayús+alfanumérico. </li>
     <li>Al usar los campos de fecha y hora.</li>
    </ul> <p>No es compatible la configuración del valor mediante script.</p> </td>
  </tr>
  <tr>
   <td>keydown</td>
   <td>Determina si un usuario está presionando una tecla de dirección para realizar una selección. Esta propiedad solo está disponible para cuadros de lista y listas desplegables.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>modifier</td>
   <td>Determina si se mantiene pulsada la tecla modificadora (por ejemplo, Ctrl en Microsoft® Windows®) cuando se ejecuta un suceso concreto.</td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
   <th>Excepción</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>Devuelve el tipo de aplicación del host. Disponible solo para aplicaciones cliente.</td>
   <td>Devuelve <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Devuelve el nombre de la aplicación actual.</td>
   <td>Devuelve el nombre del explorador y su versión. Por ejemplo, en el explorador Chrome, el valor devuelto es <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>Devuelve el número de páginas del documento.</td>
   <td>La directiva de paginación de los formularios HTML5 no es idéntica a la de los formularios PDF. Por lo tanto, la API numPages puede devolver valores diferentes en ambos casos.</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>Devuelve una cadena que representa la plataforma del equipo que ejecuta el script.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>Especifica el título del documento. Solo está disponible para aplicaciones de cliente.</td>
   <td>Devuelve el título del documento de HTML en formulario, en lugar del título de los metadatos del formulario como si hubiera PDF forms.</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>Devuelve una cadena que representa el número de versión de la aplicación actual.</td>
   <td>Devuelve la versión del formulario.</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>Especifica si se ejecutarán los scripts de cálculo.<br /> </td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>Especifica si se ejecutarán los scripts de validación.<br /> </td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>Se mueve a la página anterior.</td>
   <td>Los formularios HTML5 no siguen la misma directiva de paginación que los formularios PDF, por lo que la página anterior de un formulario HTML5 es diferente de la página anterior de un formulario PDF.</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>Se desplaza a la siguiente página de un formulario. Utilice el método pageDown durante la ejecución.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>Define el foco del teclado en el campo especificado. El campo se especifica como objeto o mediante la expresión SOM del campo. Solo está disponible para aplicaciones de cliente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>Restablece los campos a sus valores predeterminados dentro de un documento.</td>
   <td>Borra todos los datos de un formulario con datos combinados, en lugar de restaurarlos a valores predeterminados.</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>Muestra un cuadro de diálogo en la pantalla. Solo está disponible para aplicaciones de cliente</td>
   <td>El cuadro de mensaje de tipo Sí/No se convierte a Aceptar/Cancelar. No se admite el cuadro de mensaje con tres botones.</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>Define la página activa actualmente de un documento en tiempo de ejecución.</p> <p>Los valores de página empiezan por 0, así la primera página de un documento devuelve un valor de 0.</p> <p>La propiedad currentPage está disponible cuando layout:ready se ejecuta en un cliente. Sin embargo, no está disponible cuando layout:ready se ejecuta en el servidor porque la propiedad no se ejecutará hasta que se ejecute la presentación del formulario.</p> </td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

### field {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>Propiedad</span></strong></th>
   <th><strong><span>Descripción<br /> </span></strong></th>
   <th><strong><span>Excepción</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>Controla la participación del objeto asociado en diferentes fases del procesamiento. Si el objeto es un contenedor, su contenido heredará las restricciones que aplique este control.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>Controla el acceso del usuario al contenido.</td>
   <td>No funciona para el grupo de exclusión. Además, los formularios HTML5 dan el mismo tratamiento a los objetos no interactivos y protegidos.<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>Identificador que se utiliza para identificar este elemento en expresiones de script.</td>
   <td>Los formularios HTML5 no permiten establecer la propiedad name para los objetos. Es una propiedad de solo lectura para formularios HTML5.</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>Elemento de contenido que incluye solo una unidad de contenido de datos.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>Especifica el valor sin formatear del campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>Especifica el valor formateado del campo.</td>
   <td>La configuración <code>formattedValue</code> mediante script no es compatible.</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>Especifica el valor de edición para este campo.</td>
   <td>La configuración <code>editValue </code> mediante script no es compatible.</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>Especifica la cadena del mensaje de validación de formato para este campo.</td>
   <td>La configuración <code>formatMessage </code> mediante script no es compatible.</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>Especifica el valor del color de fondo para este campo. Debe establecer la propiedad border.fill.presence en visible por separado.</td>
   <td>No devuelve correctamente el color predeterminado del campo.</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>El objeto border describe el borde que rodea a un objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>El objeto ui incluye la descripción de la interfaz de usuario de un objeto de formulario.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>Especifica el valor nullTest del campo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>Especifica el valor de color de borde de este campo. Debe establecer la propiedad border.edge.presence en visible por separado.</td>
   <td>No devuelve correctamente el color de borde predeterminado del campo.</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>El número de elementos de la lista.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>Agrega nuevos elementos al campo actual.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>Quita todos los elementos del campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>Obtiene el valor de enlace de un elemento concreto de visualización específico de una lista desplegable o cuadro de lista.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>Ejecuta el script de cálculo del campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>Ejecuta el script de validación del campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>Ejecuta el script de suceso del objeto.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>Devuelve el estado de selección del elemento especificado</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>Define el estado de selección del elemento especificado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>Recupera el texto de visualización del elemento para el índice del elemento especificado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>Recupera el valor de los datos para el índice del elemento especificado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>Elimina el elemento del índice especificado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>Define los elementos especificados en el campo actual. Sustituye a los elementos preexistentes.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Una medición del alto para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Medición que especifica el ancho para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica la coordenada x del punto de ancla del contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica la coordenada Y del punto de ancla de un contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>El objeto caption describe una etiqueta descriptiva que se asocia a un objeto del diseño del formulario.<br /> </td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>El objeto validate controla la validación de los datos proporcionados por el usuario en un formulario. El objeto validate se puede activar varias veces durante el ciclo de vida de un formulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>Especifica el subformulario principal (página) de este campo.</td>
   <td>Siempre devuelve el subformulario principal en lugar del primer subformulario principal sin ámbito.<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>El índice del primer elemento seleccionado.</td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

## Formulario {#form}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| formNodes | Devuelve una lista de todos los objetos del modelo de formulario enlazados a un objeto de datos concreto. |  |

## InstanceManager {#instancemanager}

| Propiedad | Descripción |
|---|---|
| `name` | Identificador que se utiliza para identificar este elemento en expresiones de script. |
| `occur` | Describe las restricciones en el número de instancias posibles para el contenedor que lo rodea. |
| `min` | Especifica el número mínimo de instancias en las que se pueden crear instancias. |
| `max` | Especifica el número máximo de instancias en las que se pueden crear instancias. |
| `count` | Especifica el número actual de instancias en las que se crean instancias. |
| `setInstances` | Agrega o quita los subformularios o conjuntos de subformularios especificados de este nodo. |
| `addInstance` | Agrega una nueva instancia de un subformulario o conjunto de subformularios a este nodo. |
| `removeInstance` | Quita un subformulario o conjunto de subformularios de este nodo. |
| `moveInstance` | Mueve un objeto secundario de un objeto de modelo de formulario a otra ubicación especificada dentro del modelo de formulario. La información del modelo de datos correspondiente para el objeto también se reubica dentro del modelo de datos. |
| `insertInstance` | Inserta una nueva instancia de un subformulario o conjunto de subformularios a este nodo. |

## list {#list}

| Propiedad | Descripción |
|---|---|
| `length` | Número de elementos de la lista. |
| `item` | Un índice de base cero en la colección. |
| `append` | Anexa un nodo al final de la lista de nodos. |
| `remove` | Quita un nodo de la lista de nodos. |
| `insert` | Inserta un nodo antes de uno especificado en la lista de nodos. |

## node {#node}

| Propiedad | Descripción | Excepción |
|---|---|---|
| createNode | Crea un nuevo nodo basado en un nombre de clase válido. | Ninguno |
| `isContainer` | Especifica si este objeto es un objeto contenedor. | Ninguno |
| `isNull` | Indica si el valor de los datos actuales es un valor nulo. | Ninguno |
| `resolveNode` | Evalúa la expresión SOM especificada, comenzando por el objeto del modelo de objeto de formulario XML actual y devuelve el valor del objeto especificado en la expresión SOM. | Ninguno |
| `resolveNodes` | Evalúa la expresión SOM especificada, comenzando por el objeto del modelo de objeto de formulario XML actual y devuelve el valor del objeto especificado en la expresión SOM. | Ninguno |
| oneOfChild | Crea un nuevo nodo basado en un nombre de clase válido. | Ninguno |
| getElement | Devuelve un objeto secundario especificado. | Ninguno |
| getAttribute | Obtiene un valor de propiedad especificado. | Ninguno |
| setAttribute | Define el valor de una propiedad especificada. | Ninguno |

## model {#model}

| Propiedad | Descripción | Excepción |
|---|---|---|
| ND | ND | ND |

## Subformulario {#subform}

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
   <th>Excepción</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>Especifica el índice del objeto, en relación con las demás instancias que contienen instancias.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>Ejecuta el script de suceso del objeto.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>Devuelve una lista de los nodos contenidos en este subformulario (incluido) que no hayan superado la prueba de validación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>border</td>
   <td>El objeto border describe el borde que rodea a un objeto.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica el valor de color de borde de este campo. Debe establecer la propiedad border.edge.presence en visible por separado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Una medición del alto para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Medición que especifica el ancho para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica la coordenada x del punto de ancla del contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica la coordenada Y del punto de ancla de un contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>El objeto validate controla la validación de los datos proporcionados por el usuario en un formulario. El objeto validate se puede activar varias veces durante el ciclo de vida de un formulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificador que se utiliza para identificar este elemento en expresiones de script.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica la visibilidad de un objeto.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controla el acceso del usuario al contenido de un contenedor, como un subformulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>Calcula el índice de un subformulario o conjunto de subformularios a partir de su ubicación, en relación con otras instancias del mismo objeto de formulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>El objeto instanceManager administra la creación de instancias, la eliminación y el movimiento de objetos del modelo de formulario.<br /> </td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

### submit {#submit}

| Propiedad | Descripción |
|---|---|
| target | Dirección URL a la que se envían los datos. La omisión de este atributo implica que la aplicación de procesamiento XFA obtiene el URI mediante una técnica específica del producto, como el acceso a información específica del producto en el objeto de configuración. |

## tree {#tree}

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
   <th>Excepción</th>
  </tr>
  <tr>
   <td>nodes</td>
   <td>Devuelve una lista con todos los objetos secundarios del objeto actual.</td>
   <td>
    <ul>
     <li>No compatible con xfa.nodes, desc</li>
     <li>El número de nodos informados para PDF y HTML es diferente. </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica el nombre de este nodo.</td>
   <td>No se permite establecer el nombre mediante scripts en HTML.</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>Obtiene el elemento principal de este nodo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>index</td>
   <td>Devuelve la posición de este nodo en su colección de nodos de nombres semejantes, dentro de ámbito y con relación a los secundarios.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>Obtiene la expresión SOM para este nodo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>Evalúa la expresión SOM especificada, comenzando por el objeto del modelo de objeto de formulario XML actual y devuelve el valor del objeto especificado en la expresión SOM.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>Evalúa la expresión SOM especificada, comenzando por el objeto del modelo de objeto de formulario XML actual y devuelve el valor del objeto especificado en la expresión SOM.</td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| Propiedad | Descripción | Excepción |
|---|---|---|
| instanceManager | El objeto instanceManager administra la creación de instancias, la eliminación y el movimiento de objetos del modelo de formulario. | Ninguno |

## content {#content}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| isNull | Indica si el valor de los datos actuales es el valor nulo. |  |

## dataValue {#datavalue}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| isNull | Indica si el valor de los datos actuales es el valor nulo. |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad </strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para el objeto pattern.</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## fill {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>Las propiedades de color definen un color de relleno único.</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linear {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para un relleno degradado lineal de un formulario.</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## line {#line}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>El objeto edge describe un arco, una línea o un lado del borde de un rectángulo.<br /> </td>
   <td>No se admiten atributos como color, límite, etc.<br /> </td>
  </tr>
 </tbody>
</table>

## pattern {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para el objeto pattern. </td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radial {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para el objeto radial</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## stipple {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para el objeto stipple.</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>Propiedad</td>
   <td>Descripción</td>
   <td>Excepción</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>El objeto ui incluye la descripción de la interfaz de usuario de un objeto de formulario.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>El objeto caption describe una etiqueta descriptiva que se asocia a un objeto del diseño del formulario.</td>
   <td> </td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica la visibilidad de un objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica un identificador que puede usarse para indicar este objeto o suceso en expresiones de scripts.</td>
   <td>La configuración del valor en tiempo de ejecución no es compatible</td>
  </tr>
  <tr>
   <td>value</td>
   <td>El objeto value incluye una unidad de contenido de datos.<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## corner {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>La propiedad color describe un color único para el objeto de esquina.</td>
   <td>
    <ul>
     <li>No se puede recuperar el valor predeterminado. </li>
     <li>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>El objeto border describe el borde que rodea a un objeto. </td>
   <td>Los cambios se reflejan en el modelo y están disponibles para scripts, pero no se sincronizan con elementos HTML. Por lo tanto, los cambios no se reflejan en la interfaz de usuario.<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>El objeto border describe el borde que rodea a un objeto choiceList.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| border | El objeto border describe el borde que rodea a un objeto dateTimeEdit. |  |

## Imagen {#image}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>Especifica el tipo del contenido en el documento al que se hace referencia, expresado como un tipo MIME.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>Identificador que se utiliza para identificar este elemento en expresiones de script.</td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| border | El objeto border describe el borde que rodea a un objeto imageEdit. |  |

## numericEdit {#numericedit}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| border | El objeto border describe el borde que rodea a un objeto. | ninguno |

## objeto {#object}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>Determina el nombre de la clase de este objeto.<br /> </td>
   <td>ninguno</td>
  </tr>
 </tbody>
</table>

## rectangle {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>El objeto edge describe un arco, una línea o un lado del borde de un rectángulo.<br /> </td>
   <td>No se admiten atributos como color, límite, etc.</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>El objeto border describe el borde que rodea a un objeto.<br /> </td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>layout</td>
   <td>Especifica la estrategia de presentación que utilizará el objeto.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>border</td>
   <td>Especifica el borde que rodea este campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>Especifica el valor nullTest del campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>Especifica el valor del color del borde para este campo. Se debe definir un borde antes de poder cambiar el color mediante scripts.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>Especifica el ancho de borde de este campo.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>h</td>
   <td>Una medición del alto para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>transient</td>
   <td>Indica si la aplicación de procesamiento debe guardar el valor del grupo de exclusión como parte de un envío de formulario o de una operación de guardado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>w</td>
   <td>Medición que especifica el ancho para la presentación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>x</td>
   <td>Especifica la coordenada x del punto de ancla del contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>y</td>
   <td>Especifica la coordenada Y del punto de ancla de un contenedor en relación con la esquina superior izquierda del contenedor principal cuando se coloca con el diseño posicionado.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>El objeto caption describe una etiqueta descriptiva que se asocia a un objeto del diseño del formulario.<br /> </td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>El objeto validate controla la validación de los datos proporcionados por el usuario en un formulario. El objeto validate se puede activar varias veces durante el ciclo de vida de un formulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>Obtiene el nodo de datos al que está enlazado un nodo de formulario después de la combinación.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>Especifica la visibilidad de un objeto.</td>
   <td> </td>
  </tr>
  <tr>
   <td>access</td>
   <td>Controla el acceso del usuario al contenido de un contenedor, como un subformulario.</td>
   <td>Para elementos individuales de exclgrp, siempre devuelve open. </td>
  </tr>
  <tr>
   <td>name</td>
   <td>Especifica un identificador que puede usarse para indicar este objeto o suceso en expresiones de scripts.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>miembros</td>
   <td>Especifique los miembros del grupo de exclusión. </td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>Devuelve el miembro seleccionado de un grupo de exclusión.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>Ejecuta cualquier script en el suceso calculate del objeto especificado así como cualquier objeto secundario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>calculate</td>
   <td>El objeto calculate controla el cálculo del valor de un campo.<br /> </td>
   <td>Ninguno</td>
  </tr>
 </tbody>
</table>

## arc {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<strong></strong></strong></td>
   <td><strong>Descripción<strong></strong></strong></td>
   <td><strong>Excepción<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>El objeto edge describe un arco, una línea o un lado del borde de un rectángulo.<br /> </td>
   <td>No se admiten atributos como color, límite, etc. </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<strong></strong></strong></td>
   <td><strong>Descripción<strong></strong></strong></td>
   <td><strong>Excepción<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>El objeto edge describe un arco, una línea o un lado del borde de un rectángulo.<br /> </td>
   <td>No se admiten atributos como color, límite, etc. </td>
  </tr>
 </tbody>
</table>

## $layout {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Excepción</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>Determina la altura de un objeto de diseño de formulario especificado.<br /> </td>
   <td>
    <ul>
     <li>La propiedad Altura (h) no es compatible con el área de página y el área de contenido. </li>
     <li>No es compatible el parámetro “Desplazamiento desde el primer área de contenido en el que se produce el objeto XFA-Form”</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>Determina la anchura de un objeto de diseño de formulario especificado.</td>
   <td>
    <ul>
     <li>La propiedad Anchura (w) no es compatible con el área de página y el área de contenido. </li>
     <li>No es compatible el parámetro “Desplazamiento desde el primer área de contenido en el que se produce el objeto XFA-Form”</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>Determina la coordenada x de un objeto de diseño de formulario especificado en relación con su objeto principal</td>
   <td>
    <ul>
     <li>La propiedad Coordenadas x (x) no es compatible con el área de página y el área de contenido. </li>
     <li>No es compatible el parámetro “Desplazamiento desde el primer área de contenido en el que se produce el objeto XFA-Form”</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>Determina la coordenada y de un objeto de diseño de formulario especificado en relación con su objeto principal</td>
   <td>
    <ul>
     <li>La propiedad Coordenadas y (y) no es compatible con el área de página y el área de contenido. </li>
     <li>No es compatible el parámetro “Desplazamiento desde el primer área de contenido en el que se produce el objeto XFA-Form”</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>Determina el número de páginas del formulario actual.</td>
   <td>
    <ul>
     <li>El método layout.pageCount() devuelve valores diferentes para los formularios PDF y HTML.</li>
     <li>Al reducir el número de páginas al ocultar un objeto, el método abspagecount devuelve un valor incorrecto.<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>Recupera tipos de objetos de diseño de formulario en una página especificada del formulario.</td>
   <td>Ninguno</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>Determina el número de páginas del formulario actual.</td>
   <td>
    <ul>
     <li>El método layout.pageCount() devuelve valores diferentes para los formularios PDF y HTML.</li>
     <li>Al reducir el número de páginas al ocultar un objeto, el método abspagecount devuelve un valor incorrecto.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## items {#items}

| **Propiedad** | **Descripción** | **Excepción** |
|---|---|---|
| presence | Especifica la visibilidad de un objeto. | Ninguno |

## FormCalc {#formcalc}

FormCalc es un lenguaje específico de XFA para crear una lógica y unos cálculos centrados en el formulario electrónico. FormCalculation proporciona un conjunto potente de funciones de generación.

### Funciones compatibles con FormCalc {#formcalc-supported-functions}

### Compatibilidad con expresiones FormCalc {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>Categoría </strong></td>
   <td><strong>Descripción </strong></td>
   <td><strong>Muestra </strong></td>
  </tr>
  <tr>
   <td>Expresión simple</td>
   <td>Agregar, restar, multiplicar, dividir y paréntesis</td>
   <td>(A+b) x 3</td>
  </tr>
  <tr>
   <td>Declaración variable</td>
   <td>Definir una variable</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>Expresión lógica</td>
   <td>
    <ul>
     <li>Lógica (y/o)</li>
     <li>Comparación (mayor/menor/igual)</li>
    </ul> </td>
   <td>A o 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A o 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>Expresión If</td>
   <td><br type="_moz" /> </td>
   <td>if (a&gt;b) then 2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>while (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>for</td>
   <td><br type="_moz" /> </td>
   <td>for i = 100 downto 1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>for each</td>
   <td><br type="_moz" /> </td>
   <td>for each i in (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>declaración de funciones</td>
   <td>Definir una función personalizada en FormCalc</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Compatibilidad con la API de Acrobat {#acrobat-api-support}

1. **Funciones aritméticas**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Count()
   1. Floor()
   1. Max()
   1. Min()
   1. Mod()
   1. Round()
   1. Sum()

1. **Funciones científicas**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. Log()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **Funciones financieras**

   1. Apr()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Term()

1. **Funciones lógicas**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **Funciones de cadena**

   1. At()
   1. Concat()
   1. Left()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Replace()
   1. Right()
   1. Rtrim()
   1. Space()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **Fecha y hora**

   1. Date()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>Descripción</strong></td>
   <td><strong>Aberración</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>Esta API de Acrobat envía la salida a la consola de JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>Esta API de Acrobat envía un mensaje de alerta a través de la ventana emergente JavaScript.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>Hace que el sistema reproduzca un sonido.</td>
   <td>No se realiza ninguna acción.</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>Presenta un cuadro de diálogo modal al usuario. El usuario debe cerrar los cuadros de diálogo modales antes de que la aplicación host pueda volver a utilizarse directamente.</td>
   <td>No se realiza ninguna acción.<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>Inicia una dirección URL en una ventana del explorador.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>Especifica una script JavaScript y un período de tiempo. El script se ejecuta cada vez que transcurre el periodo. El valor devuelto de este método debe mantenerse en una variable JavaScript. De lo contrario, el objeto de intervalo está sujeto a la colección de residuos, lo que haría que se detuviera el reloj. Para finalizar la ejecución periódica, pase el objeto de intervalo devuelto a clearInterval.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>Especifica una script JavaScript y un período de tiempo. El script se ejecuta una sola vez, después de que transcurra el periodo. El valor devuelto de este método debe mantenerse en una variable JavaScript. De lo contrario, el objeto timeout está sujeto a la colección de residuos, lo que haría que se detuviera el reloj. Para cancelar el evento timeout, pase el objeto timeout devuelto a clearTimeOut.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>Cancela un intervalo registrado anteriormente establecido inicialmente por el método setInterval.</td>
   <td>En los formularios HTML5, la API no funciona correctamente.</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>Cancela un intervalo de tiempo de espera registrado previamente. Este intervalo se establece inicialmente mediante setTimeOut.</td>
   <td>En los formularios HTML5, la API no funciona correctamente.<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>Ejecuta un script determinado.</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>Matriz que contiene el objeto Doc para cada documento activo. Si no hay documentos activos, activeDocs no devuelve nada; es decir, tiene el mismo comportamiento que d = new Array(0) en JavaScript principal.</td>
   <td>Devuelve una matriz vacía para formularios HTML5.</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>Si es true (el valor predeterminado), se pueden realizar cálculos. Si es false, no se permiten los cálculos.</td>
   <td>Siempre es true para formularios HTML5.</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>Un objeto envolvente para mantener varios valores de constante. Actualmente, esta propiedad devuelve un objeto con una sola propiedad, align.</td>
   <td>Los formularios HTML5 devuelven un objeto align vacío.</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>Activa y desactiva el rectángulo de enfoque. El rectángulo de enfoque es la línea discontinua tenue alrededor de botones, casillas de verificación, botones de opción y firmas para indicar que el campo del formulario está seleccionado para usarlo con el teclado. El valor true activa el rectángulo de enfoque.</td>
   <td>Siempre es true para formularios HTML5.</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>Número de versión del software de formularios del visualizador. Compruebe esta propiedad para determinar si los objetos, propiedades o métodos de las versiones más recientes del software están disponibles si desea mantener la compatibilidad con versiones anteriores en los scripts.</td>
   <td>11.001 always.</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>El idioma del visualizador de Acrobat en ejecución.</td>
   <td>Siempre “ENU” para formularios HTML5.</td>
  </tr>
 </tbody>
</table>

## Eventos XFA compatibles {#supported-xfa-events}

Los siguientes eventos XFA del lado del cliente son compatibles:

* Inicializar
* Validate
* Calcular
* Hacer clic
* Entrar
* Salir
* Cambiar
* ValidationState

>[!NOTE]
>
>Los formularios HTML5 se representan en el lado del cliente (explorador). Use scripts del lado del cliente **validate** y **calculate** en lugar de scripts del lado del servidor.
