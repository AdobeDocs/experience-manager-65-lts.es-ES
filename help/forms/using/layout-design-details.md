---
title: Diseño
description: Detalles del diseño explica cómo crear diseños para utilizarlos en sus cartas o comunicaciones interactivas.
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2171'
ht-degree: 90%

---

# Diseño{#layout-design}

Las plantillas de formulario XFA o XDP permiten crear lo siguiente:

* [Cartas](/help/forms/using/create-letter.md)
* [Canal de impresión](/help/forms/using/web-channel-print-channel.md#printchannel) de [Interactive Communications](/help/forms/using/interactive-communications-overview.md)

* Fragmentos de diseños

Los XDP se diseñan en Adobe Forms Designer. Este artículo contiene detalles cómo diseñar los XDP para crear correspondencias/comunicaciones interactivas eficaces, como dónde utilizar los campos de formulario o las áreas de destino y cuándo usar fragmentos de diseño.

## Creación de un diseño para cartas o para el canal de impresión de Interactive Communications {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Un diseño define el diseño gráfico del canal de una carta o el canal de impresión de una comunicación interactiva. El diseño puede contener campos de formulario comunes, como &quot;Dirección&quot; y &quot;Número de referencia&quot;. También contiene subformularios vacíos que denotan áreas de destino. Cree el diseño en Forms Designer y, al terminar, el especialista en aplicaciones la cargará en un servidor de AEM. Desde allí, puede seleccionar el diseño al crear una plantilla de correspondencia o el canal de impresión de una comunicación interactiva.

![Designer: crear un diseño](assets/claimsubrogationlayout.png)

Siga estos pasos para crear diseños para cartas o el canal de impresión de Interactive Communications:

1. Analice el diseño y determine el contenido que se repite en todas las páginas; normalmente, el encabezado y pie de página pertenecen a esta categoría. Este contenido se coloca en las páginas maestras del diseño. El contenido restante se coloca en las páginas del cuerpo del diseño. En las disposiciones generales de una póliza, el logotipo y la dirección de la compañía se pueden agregar al encabezado y al pie de página de la página maestra. Por ejemplo, los avisos de cancelación utilizan el mismo diseño.
1. Al diseñar las páginas del cuerpo, divida el contenido de las páginas en secciones. Cada sección está diseñada como un subformulario incrustado en el propio diseño o como un diseño de fragmento. Si la sección contiene una tabla, modélela como un fragmento de diseño.
1. Un diseño se puede diseñar de la siguiente forma:

   1. Cree cada sección como un subformulario independiente que contenga todos los elementos de la sección.
   1. Diseñe cada subformulario de sección como secundario al mismo subformulario principal. El diseño del subformulario principal está establecido en una posición variable para permitir que las secciones se desplacen hacia abajo si hay datos grandes que se combinen en secciones anteriores.
   1. La sección Domicilio habitual también se puede reutilizar en otros diseños. Créela como un diseño de fragmento.
   1. La sección Detalles de interés adicionales contiene únicamente dos elementos colocados uno debajo de otro, pueden contener datos grandes y se ha diseñado con una posición variable.
   1. Otras secciones contienen elementos en posiciones específicas, por lo que se crean como diseños de posición fija.
   1. Desglose las secciones en subformularios si contienen elementos con grandes cantidades de datos en posiciones específicas. A continuación, organice los subformularios para obtener el comportamiento deseado.
   1. Agregue un área objetivo de marcador de posición para la sección Domicilio habitual. Este marcador de posición está enlazado al fragmento Domicilio habitual cuando se diseña la carta o la comunicación interactiva.
   1. Cargue el diseño (y el fragmento, si lo hay, que utiliza el diseño) en el servidor de AEM Forms.

### Uso de subformularios en una plantilla XDP {#usesubformxdp}

Una vez analizado el diseño necesario para crear la comunicación interactiva, puede crear subformularios en la plantilla XDP con Forms Designer. Los componentes de subformulario en blanco utilizados en la plantilla XDP dan como resultado la visualización de áreas de destino en el canal de impresión de la comunicación interactiva.

>[!NOTE]
>
>Añada contenido al canal de impresión de la comunicación interactiva en lugar de añadir contenido al componente de subformulario en la plantilla XDP. Añada contenido a las áreas de destino del canal de impresión mediante [fragmentos de documento, gráficos, imágenes](create-interactive-communication.md#step2) y fragmentos de diseño.

Realice los siguientes pasos para utilizar el subformulario en una plantilla XDP:

1. Abra Forms Designer, seleccione **Archivo** > **Nuevo** > **Use un formulario en blanco**, seleccione **Siguiente** y, a continuación, seleccione **Finalizar** para abrir el formulario y crear plantillas.

   Asegúrese de que las opciones **Biblioteca de objetos** y **Objeto** se seleccionan en el menú **Ventana**.

1. Arrastre y suelte el componente **Subformulario** de la **Biblioteca de objetos** al formulario.

   ![Diseñador de componentes](assets/subform_component_designer_new.png)

1. Seleccione el subformulario para mostrar sus opciones en la ventana **Objeto** del panel derecho.
1. Seleccione la pestaña **Subformulario** y luego seleccione **De posición variable** en la lista desplegable **Contenido**. Arrastre el extremo izquierdo del subformulario para ajustar la longitud.

   ![Subformulario de posición variable](assets/object_subform_flowed_new.png)

1. En la pestaña **Enlace**:

   1. Especifique un nombre para el subformulario en el campo **Nombre**.
   1. Seleccione **Sin enlace de datos** en la lista desplegable **Enlace de datos**.

1. Del mismo modo, seleccione el subformulario raíz en el panel izquierdo.

   ![Subformulario raíz](assets/root_subform_designer_new.png)

1. Seleccione la pestaña **Subformulario** y luego seleccione **De posición variable** en la lista desplegable **Contenido**. En la pestaña **Enlaces**:

   1. Especifique un nombre para el subformulario en el campo **Nombre**.
   1. Seleccione **Sin enlace de datos** en la lista desplegable **Enlace de datos**.

   Repita los pasos del 2 al 5 para agregar más subformularios a la plantilla XDP. Agregue [texto, fragmentos de documento, imágenes y gráficos](create-interactive-communication.md#step2) a las áreas de destino solo durante la creación de la comunicación interactiva.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especificar un nombre para la plantilla XDP.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Seleccione **Guardar**.

### Uso del componente Campo de imagen en una plantilla XDP {#use-image-field-component-in-an-xdp-template}

Utilice los componentes Campo de imagen o Subformulario en la plantilla XDP y añada una imagen durante la creación de la comunicación interactiva.

>[!NOTE]
>
>Agregue una imagen al canal de impresión de la comunicación interactiva en lugar de agregar una imagen a los componentes Campo de imagen o Subformulario en la plantilla XDP. Para obtener más información, consulte [Añadir contenido a la comunicación interactiva](../../forms/using/create-interactive-communication.md#step2).

Siga estos pasos para utilizar el componente Campo de imagen en una plantilla XDP:

1. Arrastre y suelte el componente **Campo de imagen** de la **Biblioteca de objetos** al formulario.
1. Seleccione el subformulario para mostrar sus opciones en la ventana **Objeto** del panel derecho.
1. En la pestaña **Enlace**:

   1. Especifique un nombre para el campo de imagen en el campo **Nombre**.
   1. Seleccione **Sin enlace de datos** en la lista desplegable **Enlace de datos**.

### Crear una plantilla XDP para fragmentos de diseño {#xdplayoutfragments}

Utilice el componente Tabla de Forms Designer para crear fragmentos de diseño y, a continuación, utilizarlos para crear tablas durante la creación del canal de impresión de la comunicación interactiva. El uso de fragmentos de diseño para crear tablas garantiza que el contenido de la tabla conserve la estructura cuando el canal web se genera automáticamente mediante el canal de impresión.

>[!NOTE]
>
>Introduzca texto en las celdas de la tabla o [cree un enlace con los objetos del modelo de datos del formulario](create-interactive-communication.md#step2) solo durante la creación de la comunicación interactiva.

Siga los siguientes pasos para utilizar el componente Tabla en la plantilla XDP mediante Forms Designer:

1. Arrastre y suelte el componente **Tabla** desde la **Biblioteca de objetos** hasta el formulario.
1. En el cuadro de diálogo **Insertar tabla**:

   1. Especifique el número de filas y columnas de la tabla.
   1. Seleccione la casilla de verificación **Incluir fila de encabezado en tabla** para incluir una fila para el encabezado de tabla.
   1. Seleccione **Aceptar**.

1. Seleccione **+** en el panel izquierdo junto al nombre de la tabla, haga clic con el botón secundario en los nombres de celda incluidos en el encabezado y en otras filas y seleccione **Cambiar nombre de objeto** para cambiar el nombre de las celdas de la tabla.
1. Haga clic en los campos de texto del encabezado de la tabla de la **vista Diseño** y cambie su nombre.
1. Arrastre y suelte el componente **Campo de texto** de la **Biblioteca de objetos** en cada una de las celdas de la tabla en la **vista Diseño**. Realice este paso para poder enlazar las celdas de tabla con los objetos del modelo de datos de formulario durante la creación de la comunicación interactiva.

   ![Campos de texto en una tabla](assets/text_fields_table_new.png)

1. Seleccione el nombre de la fila en el panel izquierdo y seleccione **Objeto** > **Enlace** > **Repetir fila para cada elemento de datos**. Realice este paso para asegurarse de que si se crea un enlace entre las celdas de la tabla de esta fila con objetos del modelo de datos de formulario de tipo colección, la fila de la tabla se repetirá automáticamente para cada uno de los elementos de datos disponibles en la base de datos.

   Introduzca texto en las celdas de la tabla o [cree un enlace con los objetos del modelo de datos del formulario](create-interactive-communication.md#step2) solo durante la creación de la comunicación interactiva.

1. Seleccione **Archivo** > **Guardar como** para guardar el archivo en el sistema de archivos local:

   1. Vaya a la ubicación para guardar el archivo y especifique el nombre de la plantilla XDP.
   1. Seleccione **.xdp** en la lista desplegable **Guardar como tipo**.

   1. Seleccione **Guardar**.

### Cargar una plantilla XDP en el servidor de AEM Forms {#uploadxdptemplate}

Una vez creada una plantilla XDP con el Forms Designer, debe cargarla en el servidor de AEM Forms para que la plantilla esté disponible para su uso durante la creación de comunicaciones interactivas.

1. Seleccione **Forms** > **Formularios y documentos**.
1. Seleccione **Crear** > **Carga de archivo**.
1. Vaya a la ubicación de la plantilla XDP en el sistema de archivos local y seleccione **Abrir** para importar la plantilla XDP al servidor de AEM Forms.

## Uso del esquema {#using-schema}

Puede utilizar un esquema en un diseño o un fragmento de diseño, pero no es obligatorio. Si utiliza un esquema, asegúrese de lo siguiente:

1. El diseño y todos los diseños de fragmento utilizados en una carta o comunicación interactiva utilizan el mismo esquema que la carta o la comunicación interactiva.
1. Todos los campos que deben rellenarse con datos están enlazados al esquema.

## Creación de campos relacionados {#creating-relatable-fields}

De forma predeterminada, todos los campos se consideran relacionados con otras fuentes de datos. Si la presentación contiene campos que no están relacionados con una fuente de datos, asigne un nombre al campo con el sufijo &quot;_int&quot; (interno); por ejemplo, pageCount_int.

Un campo relacionado debe:

* ser un &lt;field> o &lt;exclGroup> XFA
* tener una referencia de enlace XFA
* si es un &lt;exclGroup>, debe tener al menos un campo de botón de opción secundario; de lo contrario, no se puede terminar su tipo de valor

Un campo relacionado debe:

* tener un nombre

Un campo relacionado no debe:

* Incluir un sufijo &quot;_int&quot; en su nombre
* Tener el enlace establecido como &quot;ninguno&quot;
* Ser un elemento secundario de un elemento &lt;exclGroup>

Siempre que un campo relacionado cumpla los criterios descritos anteriormente, puede estar en cualquier ubicación y en cualquier profundidad de anidación del diseño. Puede utilizar campos relacionados en las páginas maestras.

Los campos son más flexibles en términos de configuración de diseño que los subformularios de área de destino; sin embargo, están vinculados a un solo tipo de valor. Puede aumentar el tamaño de un campo o establecerlo en una anchura y altura fijas, etc. El módulo o resultado de regla resuelto se inserta en el campo.

## Decidir cuándo usar subformularios y campos de texto {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Utilice un subformulario si desea capturar el contenido de varios módulos en un diseño vertical de flujo superior (varios párrafos o imágenes). El diseño debe controlar el hecho de que el subformulario aumenta en altura para ajustarse al contenido. Si no puede estar seguro de que la longitud del contenido asociado al subformulario o destino nunca va a exceder el espacio reservado para el subformulario en el diseño, cree el subformulario como elemento secundario en un contenedor de subformulario de posición variable. Este proceso garantiza que los objetos de diseño situados debajo del subformulario vayan desplazándose hacia abajo a medida que este crece.

Utilice un campo si desea capturar datos de módulo o datos de elementos del diccionario de datos en el esquema del diseño (porque los campos están enlazados a datos), o para mostrar el contenido del módulo en una página maestra. Recuerde que el contenido de una página maestra no puede desplazarse con el contenido de las páginas del cuerpo, por lo que debe asegurarse de que el campo de imagen se utiliza como logotipo de encabezado. Esta tabla proporciona más criterios para decidir cuándo utilizar un subformulario o un campo en un diseño.

<table>
 <tbody>
  <tr>
   <td><p><strong>Utilice un subformulario en los siguientes casos:</strong></p> </td>
   <td><p><strong>Utilice un campo de texto en los siguientes casos:</strong></p> </td>
  </tr>
  <tr>
   <td><p>Si contiene una combinación de elementos, como el Apellido y el Nombre.</p> </td>
   <td><p>Si contiene un solo elemento, como un Número de póliza.</p> </td>
  </tr>
  <tr>
   <td><p>Si incluye varios párrafos.</p> </td>
   <td><p>El texto está ajustado y justificado.</p> </td>
  </tr>
  <tr>
   <td><p>Los grupos de datos repetidos, opcionales y condicionales están enlazados a subformularios para reducir el riesgo de que se produzcan errores de diseño en el caso de utilizar scripts para obtener los mismos resultados.</p> </td>
   <td><p>Elementos como el logotipo y la dirección de su organización aparecen en todas las páginas de una carta o comunicación interactiva. En ese caso, cree campos de formulario para esos elementos y colóquelos en la página maestra. Si establece el enlace de campo en la opción "Sin enlace de datos", estos campos no aparecen como campos relacionados en el Editor de cartas/comunicaciones interactivas. Si desea relacionar algún tipo de contenido con estos campos, deben tener enlaces.</p> <p>Si la dirección de la compañía contiene más de una línea de datos, utilice el campo de texto con la opción "Permitir líneas múltiples" para representar la dirección en el diseño.</p> <p>Si el tipo de datos de un campo de texto está definido como texto sin formato, se utiliza la versión de texto sin formato de la salida del módulo en lugar de la versión de texto enriquecido (se descarta todo el formato). Para conservar el formato, establezca el tipo de datos del campo de texto en Texto enriquecido.</p> </td>
  </tr>
  <tr>
   <td><p>El texto está en una posición variable</p> </td>
   <td><p>Los campos de texto y los campos de imagen se utilizan en las páginas maestras. Las páginas maestras no pueden utilizar subformularios como áreas de destino.</p> </td>
  </tr>
  <tr>
   <td><p>Los objetos se agrupan y organizan sin enlazar el subformulario a un elemento de datos</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Hay un campo de texto dentro del subformulario. El subformulario puede crecer y no sobrescribir los objetos que aparecen debajo de él en el diseño.</p> </td>
   <td><p>Necesita acceder fácilmente a los datos en el proceso de publicación.</p> </td>
  </tr>
 </tbody>
</table>

## Configuración de elementos repetidos {#setting-up-repetitive-elements}

Cuando elementos como el logotipo y la dirección de su organización aparezcan en todas las páginas de una carta o comunicación interactiva, cree campos de formulario para esos elementos y colóquelos en la página maestra. Utilice el enlace Nombre (Nombre de campo) para estos campos.

## Especificar el formato de renderización del servidor {#specify-the-server-nbsp-render-format}

Utilice el formato de renderización del servidor del diseño en Formulario XML dinámico; de lo contrario, las cartas o comunicaciones interactivas basadas en este diseño no se podrán procesar correctamente. De forma predeterminada, el formato de renderización del servidor de Forms Designer está establecido en Formulario XML dinámico. Para asegurarse de que está utilizando el formato correcto:

* En Designer, haga clic en **Archivo** > **Propiedades del formulario** > **Valores predeterminados**, y asegúrese de que la configuración Representación/Formato del PDF está establecida en Formulario XML dinámico.
