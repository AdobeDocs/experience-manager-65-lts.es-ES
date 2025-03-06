---
title: Configuración de los complementos del Editor de texto enriquecido
description: Aprenda a configurar los complementos del Editor de texto enriquecido de Adobe Experience Manager para habilitar las funcionalidades individuales.
contentOwner: AG
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: f185c622-1681-4221-a082-cac71d6b510b
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '4381'
ht-degree: 2%

---

# Configuración de los complementos del Editor de texto enriquecido {#configure-the-rich-text-editor-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con la propiedad features. Puede configurar la propiedad features para activar o desactivar una o varias funciones RTE. Este artículo describe cómo configurar específicamente los complementos RTE.

Para obtener más información sobre las otras configuraciones de RTE, consulte [Configurar editor de texto enriquecido](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Al trabajar con CRXDE Lite, se recomienda guardar los cambios con regularidad usando la opción [!UICONTROL Guardar todo].

## Activar un complemento y configurar la propiedad features {#activateplugin}

Para activar un complemento, siga estos pasos. Algunos pasos solo son necesarios cuando configura un complemento por primera vez, ya que los nodos correspondientes no existen.

De manera predeterminada, los complementos `format`, `link`, `list`, `justify` y `control` y todas sus características están habilitados en RTE.

>[!NOTE]
>
>El nodo `rtePlugins` respectivo se denomina `<rtePlugins-node>` para evitar duplicaciones en este artículo.

1. Con CRXDE Lite, busque el componente de texto para su proyecto.
1. Cree el nodo principal de `<rtePlugins-node>` si no existe antes de configurar los complementos RTE:

   * Según el componente, los nodos principales son:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo de configuración alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * Son del tipo: **jcr:primaryType** `cq:Widget`
   * Ambos tienen las siguientes propiedades:

      * **Nombre** `name`
      * **Tipo** `String`
      * **Valor** `./text`

1. Según la interfaz para la que esté configurando, cree un nodo `<rtePlugins-node>`, si no existe:

   * **Nombre** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. A continuación, cree un nodo para cada complemento que desee activar:

   * **Tipo** `nt:unstructured`
   * **Nombre**: se requiere el identificador del complemento.

Después de activar un complemento, siga estas instrucciones para configurar la propiedad `features`.

| | Habilitar todas las funciones | Habilitar algunas funciones específicas | Desactivar todas las funciones |
|---|---|---|---|
| Nombre | características | características | características |
| Tipo | Cadena | Cadena[] (varias cadenas; establezca Tipo en Cadena y haga clic en Varias en CRXDE Lite) | Cadena |
| Valor | `*` (un asterisco) | se establece en uno o más valores de función | - |

## Comprensión del complemento findreplace {#findreplace}

El complemento `findreplace` no necesita ninguna configuración. Funciona de forma predeterminada.

Al utilizar la funcionalidad de reemplazo, la cadena de reemplazo que se va a reemplazar debe introducirse al mismo tiempo que la cadena de búsqueda. Sin embargo, puede hacer clic en Buscar para buscar la cadena antes de reemplazarla. Si se introduce la cadena de reemplazo después de hacer clic en Buscar, la búsqueda se restablecerá al principio del texto.

El cuadro de diálogo buscar y reemplazar se volverá transparente cuando se haga clic en buscar y se volverá opaco cuando se haga clic en reemplazar. Esto permite al autor revisar el texto que reemplaza. Si los usuarios hacen clic en reemplazar todo, el cuadro de diálogo se cierra y muestra el número de reemplazos realizados.

## Configuración de los modos de pegado {#paste-modes}

Al utilizar RTE, los autores pueden pegar el contenido en uno de los tres modos siguientes:

* **Modo de explorador**: pegue texto usando la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcado no deseado.

* **Modo de texto sin formato**: pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en el componente [!DNL Experience Manager].

* **Modo MS® Word**: pegue el texto, incluidas las tablas, con formato al copiar desde MS® Word. No se admite la copia y pegado de texto desde otro origen, como una página web o MS® Excel, y sólo se conserva un formato parcial.

### Configurar las opciones de pegado disponibles en la barra de herramientas RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Puede proporcionar algunos, todos o ninguno de estos tres iconos a los autores en la barra de herramientas RTE:

* **[!UICONTROL Pegar (Ctrl+V)]**: se puede preconfigurar para que corresponda a uno de los tres modos de Pegar anteriores.

* **[!UICONTROL Pegar como texto]**: proporciona la funcionalidad de modo de texto sin formato.

* **[!UICONTROL Pegar desde Word]**: Proporciona funcionalidad de modo MS® Word.

Para configurar RTE para que muestre los iconos necesarios, siga estos pasos.

1. Vaya al componente, por ejemplo, `/apps/<myProject>/components/text`.
1. Vaya al nodo `rtePlugins/edit`. Consulte [activar un complemento](#activateplugin) si el nodo no existe.
1. Cree la propiedad `features` en el nodo `edit` y agregue una o más de las características. Guarde todos los cambios.

### Configure el comportamiento del icono Pegar (Ctrl+V) y del acceso directo {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puede preconfigurar el comportamiento del icono **[!UICONTROL Pegar (Ctrl+V)]**, para hacerlo, siga los siguientes pasos. Esta configuración también define el comportamiento del método abreviado de teclado Ctrl+V que los autores utilizan para pegar contenido.

La configuración permite los siguientes tres tipos de casos de uso:

* Pegue texto con la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcado no deseado. Configurado con `browser` a continuación.

* Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en el componente de AEM. Configurado con `plaintext` a continuación.

* Pegue el texto, incluidas las tablas, con formato al copiar desde MS® Word. No se admite la copia y pegado de texto desde otro origen, como una página web o MS® Excel, y sólo se conserva un formato parcial. Configurado con `wordhtml` a continuación.

1. En el componente, vaya al nodo `<rtePlugins-node>/edit`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. En el nodo `edit`, cree una propiedad con los siguientes detalles:

   * **Nombre** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** Uno de los modos de pegado necesarios `browser`, `plaintext` o `wordhtml`.

### Configurar los formatos permitidos al pegar contenido {#pasteformats}

El modo pegar como Microsoft Word (`paste-wordhtml`) se puede configurar para que pueda definir explícitamente qué estilos se permiten al pegar en AEM desde otro programa, como Microsoft® Word.

Por ejemplo, si solo se deben permitir formatos en negrita y listas al pegar en AEM, puede filtrar los demás formatos. Esto se denomina filtrado de pegado configurable y se puede hacer para lo siguiente:

* [Texto](#paste-modes)
* [Vínculos](#linkstyles)

En el caso de los vínculos, también puede definir los protocolos que se aceptan automáticamente.

Para configurar qué formatos se permiten al pegar texto en AEM desde otro programa:

1. En el componente, vaya al nodo `<rtePlugins-node>/edit`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. Cree un nodo bajo el nodo `edit` para poder mantener las reglas de pegado de HTML:

   * **Nombre** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Cree un nodo en `htmlPasteRules` para poder guardar los detalles de los formatos básicos permitidos:

   * **Nombre** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar los formatos individuales aceptados, cree una o varias de las siguientes propiedades en el nodo `allowBasics`:

   * **Nombre** `bold`
   * **Nombre** `italic`
   * **Nombre** `underline`
   * **Nombre** `anchor` (tanto para vínculos como para anclajes con nombre)
   * **Nombre** `image`

   Todas las propiedades son del **tipo** `Boolean`, por lo que en el **valor** apropiado puede seleccionar o quitar la marca de verificación para habilitar o deshabilitar la funcionalidad.

   >[!NOTE]
   >
   >Si no se define explícitamente, se utiliza el valor predeterminado de true y se acepta el formato.

1. Otros formatos también se pueden definir mediante un rango de otras propiedades o nodos, también aplicados al nodo `htmlPasteRules`. Guarde todos los cambios.

Puede usar las siguientes propiedades para `htmlPasteRules`.

| Propiedad | Tipo | Descripción |
|---|---|---|
| `allowBlockTags` | Cadena | Define la lista de etiquetas de bloque permitidas. Algunas etiquetas de bloque posibles son: <ul> <li>titulares (h1, h2, h3)</li> <li>párrafos p)</li> <li>listas (ol, ul)</li> <li>tablas (tabla)</li> </ul> |
| `fallbackBlockTag` | Cadena | Define la etiqueta de bloque utilizada para cualquier bloque que tenga una etiqueta de bloque no incluida en `allowBlockTags`. `p` suele ser suficiente. |
| tabla | nt:unstructured | Define el comportamiento al pegar tablas. Este nodo debe tener la propiedad `allow` (tipo booleano) para definir si se permite pegar tablas. Si allow se establece en `false`, debe especificar la propiedad `ignoreMode` (tipo String) para definir cómo se administra el contenido de tabla pegado. Los valores válidos para `ignoreMode` son: <ul> <li>`remove`: quita el contenido de la tabla.</li> <li>`paragraph`: convierte celdas de tabla en párrafos.</li> </ul> |
| list | nt:unstructured | Define el comportamiento al pegar listas. Debe tener la propiedad `allow` (tipo booleano) para definir si se permite pegar listas. Si `allow` está establecido en `false`, debe especificar la propiedad `ignoreMode` (tipo cadena) para definir cómo gestionar el contenido de la lista pegado. Los valores válidos para `ignoreMode` son: <ul><li> `remove`: quita el contenido de la lista.</li> <li>`paragraph`: convierte los elementos de lista en párrafos.</li> </ul> |

A continuación se muestra un ejemplo de una estructura `htmlPasteRules` válida.

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

## Configurar estilos de texto {#textstyles}

Los autores pueden aplicar estilos para cambiar el aspecto de una parte del texto. Los estilos se basan en clases CSS predefinidas en la hoja de estilos CSS. El contenido estilizado se incluye entre etiquetas `span` usando el atributo `class` para hacer referencia a la clase CSS. Por ejemplo, `<span class=monospaced>Monospaced Text Here</span>`.

Cuando el complemento Estilos está habilitado por primera vez, no hay estilos predeterminados disponibles. La lista emergente está vacía. Para proporcionar estilos a los autores, haga lo siguiente:

* Active el selector desplegable Estilo.
* Especifique las ubicaciones de las hojas de estilo.
* Especifique los estilos individuales que se pueden seleccionar de la lista desplegable Estilo.

Para configuraciones posteriores, por ejemplo, para agregar más estilos, siga sólo las instrucciones para hacer referencia a una nueva hoja de estilos y para especificar los estilos adicionales.

>[!NOTE]
>
>Puede definir estilos para [tablas o celdas de tabla](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Estas configuraciones requieren procedimientos independientes.

### Habilitar la lista desplegable de selectores de estilo {#styleselectorlist}

Para ello, habilite el complemento de estilo.

1. En el componente, vaya al nodo `<rtePlugins-node>/styles`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `styles`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Guarde todos los cambios.

>[!NOTE]
>
>Una vez habilitado el complemento Estilos, la lista desplegable Estilo se muestra en el cuadro de diálogo de edición. Sin embargo, la lista está vacía, ya que no se ha configurado ningún estilo.

### Especificar la ubicación de la hoja de estilos {#locationofstylesheet}

A continuación, especifique las ubicaciones de las hojas de estilo a las que desea hacer referencia:

1. Vaya al nodo raíz del componente de texto, por ejemplo, `/apps/<myProject>/components/text`.
1. Agregar la propiedad `externalStyleSheets` al nodo primario de `<rtePlugins-node>`:

   * **Nombre** `externalStyleSheets`
   * **Type** `String[]` (varias cadenas; haga clic en **Multi** en CRXDE)
   * **Valores** Ruta de acceso y nombre de archivo de cada hoja de estilos que desee incluir. Utilice las rutas del repositorio.

   >[!NOTE]
   >
   >Se pueden agregar referencias a hojas de estilos adicionales en cualquier momento posterior.

1. Guarde todos los cambios.

>[!NOTE]
>
>Cuando utilice RTE en un cuadro de diálogo (IU clásica), es posible que desee especificar hojas de estilo optimizadas para la edición de texto enriquecido. Debido a restricciones técnicas, el contexto CSS se pierde en el editor, por lo que es posible que desee emular este contexto para mejorar la experiencia de WYSIWYG.
>
>El Editor de texto enriquecido utiliza un elemento DOM contenedor con un identificador de `CQrte` que se puede utilizar para proporcionar diferentes estilos de visualización y edición:
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### Especifique los estilos disponibles en la lista emergente {#stylesindropdown}

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/styles`, tal como se creó en [Habilitación del selector desplegable de estilo](#styleselectorlist).
1. En el nodo `styles`, cree un nodo (también denominado `styles`) que contenga la lista disponible:

   * **Nombre** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo bajo el nodo `styles` para que pueda representar un estilo individual:

   * **Nombre**, puede especificar el nombre, pero debe ser adecuado para el estilo
   * **Tipo** `nt:unstructured`

1. Agregue la propiedad `cssName` a este nodo para poder hacer referencia a la clase CSS:

   * **Nombre** `cssName`
   * **Tipo** `String`
   * **Valor** El nombre de la clase CSS (sin &#39;.&#39; anterior; por ejemplo, `cssClass` en lugar de `.cssClass`)

1. Agregue la propiedad `text` al mismo nodo; esto define el texto mostrado en el cuadro de selección:

   * **Nombre** `text`
   * **Tipo** `String`
   * **Valor**: descripción del estilo; aparece en el cuadro de selección desplegable Estilo.

1. Guarde los cambios.

   Repita los pasos anteriores para cada estilo necesario.

### Configuración de RTE para saltos de palabra óptimos en japonés {#jpwordwrap}

Los autores que utilizan AEM para crear contenido en japonés pueden aplicar un estilo a los caracteres para evitar saltos de línea donde no es necesario un salto. Esto permite a los autores dejar que las frases se rompan en la posición deseada. El estilo de esta funcionalidad se basa en la clase CSS predefinida en la hoja de estilos CSS.

Para crear el estilo que los autores pueden aplicar al texto en japonés, siga estos pasos:

1. Cree un nodo en el nodo Estilos. Consulte [especificar un nuevo estilo](#stylesindropdown).
   * Nombre: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Agregue la propiedad `cssName` al nodo para poder hacer referencia a la clase CSS. Este nombre de clase es un nombre reservado para la función de ajuste de línea en japonés.
   * Nombre: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sin `.` anterior)

1. Añada el texto de la propiedad al mismo nodo. El valor es el nombre del estilo que ve el autor al seleccionar el estilo.
   * Nombre: `text`
*Tipo: `String`
   * Valor: `Japanese word-wrap`

1. Cree una hoja de estilos y especifique su ruta. Consulte [especificar la ubicación de la hoja de estilos](#locationofstylesheet). Agregue el siguiente contenido a la hoja de estilos. Cambie el color de fondo como desee.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Hoja de estilo para que la función de ajuste de línea en japonés esté disponible para los autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configuración de los formatos de párrafo {#paraformats}

Cualquier texto creado en RTE se coloca dentro de una etiqueta de bloque, siendo el valor predeterminado `<p>`. Al habilitar el complemento `paraformat`, puede especificar etiquetas de bloque adicionales que se pueden asignar a los párrafos mediante una lista de selección desplegable. Los formatos de párrafo determinan el tipo de párrafo asignando la etiqueta de bloque correcta. El autor puede seleccionarlos y asignarlos mediante el selector de formato. Las etiquetas de bloque de ejemplo incluyen, entre otros, el párrafo estándar &lt;p> y los encabezados &lt;h1>, &lt;h2>, etc.

>[!CAUTION]
>
>Este complemento no es adecuado para contenido con estructuras complejas, como listas o tablas.

>[!NOTE]
>
>Si una etiqueta de bloque, por ejemplo, una etiqueta &lt;hr>, no se puede asignar a un párrafo, no es un caso de uso válido para un complemento de paraformato.

Cuando el complemento Formatos de párrafo se activa por primera vez, no hay disponibles formatos de párrafo predeterminados. La lista emergente está vacía. Para proporcionar a los autores formatos de párrafo, haga lo siguiente:

* Habilite la lista desplegable Formato del selector.
* Especifique las etiquetas de bloque que se pueden seleccionar como formatos de párrafo en la lista desplegable.

Para configuraciones o reconfiguraciones posteriores, por ejemplo, para agregar más formatos, siga solo la parte correspondiente de las instrucciones.

### Habilite el selector desplegable Formato {#formatselectorlist}

En primer lugar, habilite el complemento de paraformato:

1. En el componente, vaya al nodo `<rtePlugins-node>/paraformat`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `paraformat`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
Si el complemento no se sigue configurando, se habilitan los siguientes formatos predeterminados:
>
* Párrafo (`<p>`)
* Encabezado 1 ( `<h1>`)
* Encabezado 2 ( `<h2>`)
* Encabezado 3 ( `<h3>`)
>

>[!CAUTION]
>
Al configurar el formato de párrafo del RTE, no elimine la etiqueta de párrafo &lt;p> como opción de formato. Si se quita la etiqueta `<p>`, el autor del contenido no podrá seleccionar la opción **Formatos de párrafo** aunque haya otros formatos configurados.

### Especificar los formatos de párrafo disponibles {#paraformatsindropdown}

Los formatos de párrafo podrán ser seleccionados por:

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/paraformat`, tal como se creó en [Habilitación del selector desplegable de formato](#styleselectorlist).
1. En el nodo `paraformat`, cree un nodo que contenga la lista de formatos:

   * **Nombre** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo bajo el nodo `formats`, que contiene detalles para un formato individual:

   * **Nombre**, puede especificar el nombre, pero debe ser adecuado para el formato (por ejemplo, myparagraph, myheading1).
   * **Tipo** `nt:unstructured`

1. A este nodo, agregue la propiedad para definir la etiqueta de bloque utilizada:

   * **Nombre** `tag`
   * **Tipo** `String`
   * **Valor**: etiqueta de bloque para el formato; por ejemplo: p, h1, h2.

     No es necesario introducir los corchetes angulares delimitadores.

1. Al mismo nodo, agregue otra propiedad para que el texto descriptivo aparezca en la lista desplegable:

   * **Nombre** `description`
   * **Tipo** `String`
   * **Valor** Texto descriptivo para este formato; por ejemplo, Párrafo, Encabezado 1, Encabezado 2. Este texto se muestra en la lista de selección Formato.

1. Guarde los cambios.

   Repita los pasos para cada formato requerido.

>[!CAUTION]
>
Si define formatos personalizados, se quitarán los formatos predeterminados (`<p>`, `<h1>`, `<h2>` y `<h3>`). Vuelva a crear el formato `<p>`, ya que es el formato predeterminado.

## Configuración de caracteres especiales {#spchar}

En una instalación estándar de AEM, cuando el complemento `misctools` está habilitado para caracteres especiales (`specialchars`), una selección predeterminada está disponible inmediatamente para su uso; por ejemplo, los símbolos de copyright y marca comercial.

Puede configurar el RTE para que su propia selección de caracteres esté disponible; ya sea definiendo caracteres distintos o una secuencia completa.

>[!CAUTION]
>
Si agrega sus propios caracteres especiales, se anulará la selección predeterminada. Si es necesario, defina o redefina estos caracteres en su propia selección.

### Definir un solo carácter {#definesinglechar}

1. En el componente, vaya al nodo `<rtePlugins-node>/misctools`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `misctools`:

   * **Nombre** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

         (o `String / *` si se aplican todas las características de este complemento)

1. En `misctools`, cree un nodo que contenga las configuraciones de caracteres especiales:

   * **Nombre** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. En `specialCharsConfig`, cree otro nodo que contenga la lista de caracteres:

   * **Nombre** `chars`
   * **Tipo** `nt:unstructured`

1. En `chars`, agregue un nodo que contenga una definición de carácter individual:

   * **Nombre**: puede especificar el nombre, pero debe reflejar el carácter; por ejemplo, la mitad.
   * **Tipo** `nt:unstructured`

1. Agregue la siguiente propiedad a este nodo:

   * **Nombre** `entity`
   * **Tipo** `String`
   * **Valor** representa en HTML el carácter requerido; por ejemplo, `&189;` para la fracción de la mitad.

1. Guarde los cambios.

En CRXDE, una vez guardada la propiedad, se muestra el carácter representado. Consulte a continuación el ejemplo de la mitad. Repita los pasos anteriores para que pueda poner más caracteres especiales a disposición de los autores.

![En CRXDE, agregue un solo carácter para que esté disponible en la barra de herramientas RTE](assets/chlimage_1-106.png "En CRXDE, agregue un solo carácter para que esté disponible en la barra de herramientas RTE")

### Definir un intervalo de caracteres {#definerangechar}

1. Use los pasos del 1 al 3 de [Definición de un solo carácter](#definesinglechar).
1. En `chars`, agregue un nodo que contenga la definición del intervalo de caracteres:

   * **Nombre**: puede especificar el nombre, pero debe reflejar el intervalo de caracteres; por ejemplo, lápices.
   * **Tipo** `nt:unstructured`

1. Bajo este nodo (denominado según su intervalo especial de caracteres), agregue las dos propiedades siguientes:

   * **Nombre** `rangeStart`
     **Tipo** `Long`
     **Value** representa [Unicode](https://unicode.org/) (decimal) del primer carácter del intervalo

   * **Nombre** `rangeEnd`
     **Tipo** `Long`
     **Valor**: la representación [Unicode](https://unicode.org/) (decimal) del último carácter del intervalo

1. Guarde los cambios.

   Por ejemplo, defina un rango 9998 10000 le proporcione los siguientes caracteres.

   ![En CRXDE, defina un rango de caracteres que estará disponible en RTE](assets/chlimage_1-107.png)

   *Figura: en CRXDE, defina un rango de caracteres que estarán disponibles en RTE*

   ![Los caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente](assets/rtepencil.png "Los caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente")

## Configurar estilos de tabla {#tablestyles}

Los estilos suelen aplicarse en el texto, pero también se puede aplicar un conjunto independiente de estilos en una tabla o en algunas celdas de la tabla. Estos estilos están disponibles para los autores desde el cuadro Selector de estilo en el cuadro de diálogo Propiedades de celda o Propiedades de tabla. Los estilos están disponibles al editar una tabla dentro de un componente Texto (o derivado) y no en el componente Tabla estándar.

>[!NOTE]
>
Puede definir estilos para tablas y celdas solo para la IU clásica.

>[!NOTE]
>
La copia y el pegado de tablas en o desde el componente RTE depende del explorador. No es compatible de serie con todos los exploradores. Puede obtener resultados variados según la estructura de la tabla y el explorador. Por ejemplo, cuando copia y pega una tabla en un componente RTE en Mozilla Firefox en la IU clásica y la IU táctil, el diseño de la tabla no se conserva.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/table`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `table`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

   >[!NOTE]
   >
   Si no desea habilitar todas las características de la tabla, puede crear la propiedad `features` como:
   >
   * **Tipo** `String[]`
   >
   * **Valor** uno o ambos de los siguientes, según sea necesario:
   * `table` para permitir la edición de propiedades de tabla; incluidos los estilos.
   * `cellprops` para permitir la edición de propiedades de celda, incluidos los estilos.

1. Defina la ubicación de las hojas de estilos CSS para que pueda hacer referencia a ellas. Consulte [Especificación de la ubicación de la hoja de estilos](#locationofstylesheet), ya que es lo mismo que al definir [estilos para texto](#textstyles). La ubicación puede definirse si ha definido otros estilos.
1. En el nodo `table`, cree los siguientes nodos nuevos (según sea necesario):

   * Para definir estilos para toda la tabla (disponible en **Propiedades de la tabla**):

      * **Nombre** `tableStyles`
      * **Tipo** `cq:WidgetCollection`

   * Para definir estilos para celdas individuales (disponibles en **Propiedades de celda**):

      * **Nombre** `cellStyles`
      * **Tipo** `cq:WidgetCollection`

1. Cree un nodo (bajo el nodo `tableStyles` o `cellStyles` según corresponda) para que pueda representar un estilo individual:

   * **Nombre**: puede especificar el nombre, pero debe reflejar el estilo.
   * **Tipo** `nt:unstructured`

1. En este nodo, cree las propiedades:

   * Para definir el estilo CSS al que se hará referencia

      * **Nombre** `cssName`
      * **Tipo** `String`
      * **Valor** representa el nombre de la clase CSS (sin `.` anterior, por ejemplo, `cssClass` en lugar de `.cssClass`)

   * Para definir un texto descriptivo que aparecerá en el selector desplegable

      * **Nombre** `text`
      * **Tipo** `String`
      * **Valor** el texto que aparecerá en la lista de selección

1. Guarde todos los cambios.

Repita los pasos anteriores para cada estilo necesario.

### Configuración de encabezados ocultos en tablas para fines de accesibilidad {#hiddenheader}

A veces, puede crear tablas de datos sin texto visual en un encabezado de columna suponiendo que el propósito del encabezado está implícito en la relación visual de la columna con otras columnas. En este caso, es necesario proporcionar texto interno oculto dentro de la celda en la celda del encabezado. Al hacerlo, los lectores de pantalla y otras tecnologías de asistencia pueden ayudar a los lectores con diversas necesidades a comprender el propósito de la columna.

Para mejorar la accesibilidad en estos casos, RTE admite celdas de encabezado ocultas. Además, proporciona opciones de configuración relacionadas con encabezados ocultos en tablas. Esta configuración permite aplicar estilos CSS a encabezados ocultos en los modos de edición y vista previa. Para ayudar a los autores a identificar los encabezados ocultos en el modo de edición, incluya los siguientes parámetros en el código:

* `hiddenHeaderEditingCSS`: especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto, cuando se edita RTE.
* `hiddenHeaderEditingStyle`: especifica una cadena Style que se aplica en la celda de encabezado oculto cuando se edita RTE.

Si especifica las cadenas CSS y Style en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Style.

Para ayudar a los autores a aplicar CSS en encabezados ocultos en el modo de vista previa, puede incluir los siguientes parámetros en el código:

* `hiddenHeaderClassName`: especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculta en el modo de vista previa.
* `hiddenHeaderStyle`: especifica una cadena Style que se aplica en la celda de encabezado oculto en el modo de vista previa.

Si especifica las cadenas CSS y Style en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Style.

## Agregar diccionarios para el corrector ortográfico {#adddict}

Cuando se activa el complemento corrector ortográfico, RTE utiliza diccionarios para cada idioma adecuado. A continuación, se seleccionan según el idioma del sitio web tomando la propiedad language del subárbol o extrayendo el idioma de la dirección URL. Por ejemplo, la rama `/en/` está marcada en inglés y la rama `/de/` en alemán.

>[!NOTE]
>
Se ve el mensaje `Spell checking failed` si se intenta realizar una comprobación en un idioma que no está instalado. Los diccionarios estándar se encuentran en `/libs/cq/spellchecker/dictionaries`, junto con los archivos léame correspondientes. No modifique los archivos.

Una instalación estándar de AEM incluye los diccionarios de inglés americano (`en_us`) e inglés británico (`en_gb`). Para agregar más diccionarios, siga estos pasos.

1. Vaya a la página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Realice una de las siguientes acciones para buscar un diccionario del idioma que haya elegido:

   * Busque el diccionario del idioma que haya elegido. En la página del diccionario, busque el vínculo a la página web de origen o del autor original. Busque los archivos de diccionario para v2.x en una página de este tipo.
   * Busque los archivos de diccionario v2.x en [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Descargue el archivo con las definiciones de ortografía. Extraiga el contenido del archivo en su sistema de archivos.

   >[!CAUTION]
   >
   Solo se admiten diccionarios con el formato `MySpell` para OpenOffice.org v2.0.1 o anterior. Como los diccionarios ahora son archivos de almacenamiento, se recomienda verificarlos después de la descarga.

1. Busque los archivos `.aff` y `.dic`. Mantenga el nombre del archivo en minúsculas. Por ejemplo, `de_de.aff` y `de_de.dic`.
1. Cargue los archivos `.aff` y `.dic` en el repositorio en `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
El corrector ortográfico RTE está disponible bajo demanda. No se ejecuta automáticamente cuando empieza a escribir texto. Para ejecutar el corrector ortográfico, haga clic en [!UICONTROL Corrector ortográfico] en la barra de herramientas. RTE revisa la ortografía de las palabras y resalta las palabras mal escritas.
>
Si incorpora cualquier cambio que sugiera el corrector ortográfico, el estado del texto cambia y las palabras mal escritas dejan de resaltarse. Para ejecutar el corrector ortográfico, vuelva a hacer clic en el botón Corrector ortográfico.

## Configuración del tamaño del historial para acciones de deshacer y rehacer {#undohistory}

RTE permite a los autores deshacer o rehacer algunas ediciones últimas. De forma predeterminada, se almacenan 50 ediciones en el historial. Puede configurar este valor según sea necesario.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/undo`. Cree estos nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. En el nodo `undo`, cree la propiedad:

   * **Nombre** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** indica el número de pasos de deshacer que desea guardar en el historial. El valor predeterminado es 50. Use `0` para deshabilitar por completo deshacer/rehacer.

1. Guarde los cambios.

## Configuración del tamaño de la pestaña {#tabsize}

Cuando se presiona el carácter de tabulación dentro de cualquier texto, se inserta un número predefinido de espacios; de forma predeterminada, son tres espacios sin saltos y un espacio.

Para definir el tamaño de la pestaña:

1. En el componente, vaya al nodo `<rtePlugins-node>/keys`. Cree los nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. En el nodo `keys`, cree la propiedad:

   * **Nombre** `tabSize`
   * **Tipo** `String`
   * **Valor** indica el número de caracteres de espacio que se utilizarán para el tabulador

1. Guarde los cambios.

## Establecer margen de sangría {#indentmargin}

Cuando la sangría está habilitada (opción predeterminada), puede definir el tamaño de la sangría:

>[!NOTE]
>
Este tamaño de sangría solo se aplica a párrafos (bloques) de texto; no afecta a la sangría de listas reales.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/lists`. Cree estos nodos si no existen. Para obtener más información, consulte [activar un complemento](#activateplugin).
1. En el nodo `lists`, cree el parámetro `indentSize`:

   * **Nombre**: `indentSize`
   * **Tipo**: `Long`
   * **Valor**: número de píxeles necesarios para el margen de sangría.

## Configurar la altura del espacio editable {#editablespace}

>[!NOTE]
>
Esto solo es aplicable cuando se utiliza el RTE en un cuadro de diálogo (no en la edición in situ en la IU clásica).

Puede definir la altura del espacio editable que se muestra en el cuadro de diálogo del componente:

1. En el nodo `../items/text` de la definición del cuadro de diálogo del componente, cree una propiedad:

   * **Nombre** `height`
   * **Tipo** `Long`
   * **Valor** representa la altura del lienzo de edición en píxeles.

   >[!NOTE]
   >
   Esto no cambia la altura de la ventana de diálogo.

1. Guarde los cambios.

## Configuración de estilos y protocolos para vínculos {#linkstyles}

Al añadir vínculos en AEM, puede definir lo siguiente:

* Estilos CSS que se van a utilizar
* Los protocolos aceptados automáticamente

Para configurar cómo se añaden los vínculos en AEM desde otro programa, defina las reglas de HTML.

1. Con CRXDE Lite, busque el componente de texto para su proyecto.
1. Cree un nodo en el mismo nivel que `<rtePlugins-node>`; es decir, cree el nodo en el nodo principal de `<rtePlugins-node>`:

   * **Nombre** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   >
   El nodo `../items/text` tiene la propiedad:
   >
   * **Nombre** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`
   >
   La ubicación del nodo `../items/text` puede variar, según la estructura del cuadro de diálogo; dos ejemplos son `/apps/myProject>/components/text/dialog/items/text` y `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. En `htmlRules`, cree un nodo.

   * **Nombre** `links`
   * **Tipo** `nt:unstructured`

1. En el nodo `links`, defina las propiedades según sea necesario:

   * Estilo CSS para vínculos internos:

      * **Nombre** `cssInternal`
      * **Tipo** `String`
      * **Valor** es el nombre de la clase CSS (sin &#39;.&#39; anterior; por ejemplo, `cssClass` en lugar de `.cssClass`)

   * Estilo CSS para vínculos externos

      * **Nombre** `cssExternal`
      * **Tipo** `String`
      * **Valor** es el nombre de la clase CSS (sin &#39;.&#39; anterior; por ejemplo, `cssClass` en lugar de `.cssClass`)

   * Matriz de **protocolos** válidos. Los protocolos admitidos son `http://`, `https://`, `file://` y `mailto:`.

      * **Nombre** `protocols`
      * **Tipo** `String[]`
      * **Valor** uno o más protocolos

   * **defaultProtocol** (propiedad de tipo **String**): Protocolo que se debe usar si el usuario no especificó uno explícitamente.

      * **Nombre** `defaultProtocol`
      * **Tipo** `String`
      * **Valor** uno o más protocolos predeterminados

   * Definición de cómo gestionar el atributo de destino de un vínculo. Cree un nodo:

      * **Nombre** `targetConfig`
      * **Tipo** `nt:unstructured`

     En el nodo `targetConfig`, defina las propiedades necesarias:

      * Especifique el modo de destino:

         * **Nombre** `mode`
         * **Tipo** `String`
         * **Valor**

            * `auto`: significa que se elige un destino automático

              (especificado por la propiedad `targetExternal` para vínculos externos o `targetInternal` para vínculos internos).

            * `manual`: no aplicable en este contexto
            * `blank`: no aplicable en este contexto

      * El destino de los vínculos internos:

         * **Nombre** `targetInternal`
         * **Tipo** `String`
         * **Value** es el destino de los vínculos internos (utilícelo únicamente cuando el modo sea `auto`)

      * El destino de los vínculos externos:

         * **Nombre** `targetExternal`
         * **Tipo** `String`
         * **Value** es el destino de los vínculos externos (solo se usa cuando el modo es `auto`).

1. Guarde todos los cambios.
