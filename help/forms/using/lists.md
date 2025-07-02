---
title: Fragmentos de documento en AEM
description: Los fragmentos de documento, como texto, listas, condiciones y fragmentos de diseño, de Administración de correspondencia le permiten formar los componentes estáticos, dinámicos y repetibles de la correspondencia del cliente.
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: ece49f03-e711-439f-9c2d-6308fe2998ae
source-git-commit: 4f2374a48687d39f7d365e09d9055edf583e2c20
workflow-type: tm+mt
source-wordcount: '6895'
ht-degree: 88%

---

# Fragmentos de documento{#document-fragments}

## Fragmentos de documento {#document-fragments-1}

Los fragmentos de documento son elementos o componentes reutilizables de una correspondencia mediante que se pueden utilizar para componer cartas o correspondencia. Los fragmentos del documento son de los siguientes tipos:

* **Texto**: un recurso de texto es un fragmento de contenido que consta de uno o más párrafos de texto. Un párrafo puede ser estático o dinámico.
* **Lista**: una lista es un grupo de fragmentos de documento que puede incluir texto, listas, condiciones e imágenes. El orden de los elementos de la lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de una lista para replicar un patrón de elementos reutilizable.
* **Condición**: las condiciones permiten definir qué contenido se incluye en el momento de la creación de la correspondencia en función de los datos suministrados. La condición se describe en términos de variables de control. Una variable de control puede ser un elemento de diccionario de datos o un marcador de posición.
* **Fragmento de diseño**: un fragmento de diseño es un diseño que se puede utilizar en una o varias cartas. Un fragmento de diseño se utiliza para crear patrones repetibles, especialmente tablas dinámicas. El diseño puede contener campos de formulario típicos, como “Dirección” y “Número de referencia”. También contiene subformularios vacíos que denotan áreas de destino. Los diseños (XDP) se crean en Designer y luego se cargan en AEM Forms.

## Texto {#text}

Un recurso de texto es un fragmento de contenido que consta de uno o más párrafos de texto. Un párrafo puede ser estático o dinámico. Un párrafo dinámico contiene referencias a elementos de datos, cuyos valores se proporcionan durante la ejecución. Por ejemplo, el nombre del cliente en el saludo de una carta podría ser un elemento de datos dinámico, y su valor estaría disponible durante la ejecución. Al cambiar estos valores, se puede utilizar la misma plantilla de carta para generar cartas para distintos clientes.

La solución de Administración de correspondencia admite dos tipos de elementos de datos dinámicos (datos variables):

* **Elementos de diccionario de datos**: estos elementos están enlazados al diccionario de datos y obtienen sus valores de la fuente de datos proporcionada. Una variable de diccionario de datos puede estar protegida o desprotegida. Durante la creación de la correspondencia, el usuario puede modificar el valor predeterminado de las variables de diccionario de datos no protegidas, pero no puede modificar las protegidas.
* **Marcadores de posición**: son variables que no están enlazadas a una fuente de datos back-end. Requieren que el usuario rellene un valor durante la creación de la correspondencia. Los marcadores de posición no están protegidos de forma predeterminada.

>[!NOTE]
>
>Las plantillas de Administración de correspondencia no obligan a crear nombres únicos al crear marcadores de posición. Si se crean dos marcadores de posición con el mismo nombre, como un texto y una condición, y se utilizan ambos en una plantilla de carta, los valores del último marcador de posición insertado se utilizan para ambos marcadores. Si dos marcadores de posición tienen el mismo nombre, se comparan sus tipos. Si los tipos son diferentes, su tipo se convierte en Cadena. Sin embargo, dentro de un módulo no se pueden crear varios marcadores de posición con el mismo nombre.

### Crear texto {#create-text}

1. Seleccione **Forms** > **Fragmentos de documento**.
1. Seleccione **Crear** > **Texto** O seleccione un recurso de texto y seleccione **Editar**.
1. Especifique la siguiente información para el texto:

   * **Título: (Opcional)** introduzca el título del recurso de texto. Los títulos no tienen por qué ser únicos, y pueden contener caracteres especiales y caracteres que no sean de inglés. Se hace referencia a los textos por sus títulos (cuando están disponibles); por ejemplo en las miniaturas y las propiedades de recursos.
   * **Nombre:** el nombre único del recurso de texto. No pueden existir dos recursos (texto, condición o lista) con el mismo nombre en ningún estado. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título. Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en Nombre, puede editarlo.
   * **Descripción**: escriba una descripción para el recurso.
   * **Diccionario de datos**: si lo desea, puede seleccionar el diccionario de datos que desea asignar al texto. Este atributo permite agregar referencias a elementos de diccionario de datos en el recurso de texto.
   * **Etiquetas**: si lo prefiere, puede crear una etiqueta personalizada introduciendo el valor en el campo de texto y pulsando Intro. Puede ver la etiqueta debajo del campo de texto de las etiquetas. Al guardar este texto, también se crean las etiquetas que acaba de agregar.

1. Seleccione **Siguiente**. Administración de correspondencia muestra la página Editor, donde puede agregar párrafos de texto y elementos de datos al texto.

   El corrector ortográfico predeterminado del explorador comprueba la ortografía en el Editor de texto. Para administrar la revisión ortográfica y gramatical, puede editar la configuración del corrector ortográfico del explorador o instalar complementos del explorador para revisar la ortografía y la gramática.

   También puede utilizar los distintos métodos abreviados de teclado en el Editor de texto para administrar, editar y dar formato al texto. Para obtener más información, consulte los métodos abreviados de teclado del [Editor de texto](/help/forms/using/keyboard-shortcuts.md#p-formatting-p) en Métodos abreviados de teclado de Administración de correspondencia.

1. Se abre el Editor de texto. Introduzca el texto. Utilice la barra de herramientas situada en la parte superior de la página para dar formato al texto e insertar condiciones, vínculos y saltos de página.

   ![Barra de herramientas](assets/advancedediting.png)

   * **Vínculo**: inserte un vínculo de [hipertexto](#insert-hyperlink) en el texto.
   * **Repetir**: Repetir imprime el elemento de colección en el diccionario de datos con un delimitador.
   * **Condición**: seleccione esta opción para insertar una condición. Inserte texto basado en una condición. Si la condición es verdadera, el texto es visible en la carta; de lo contrario, no.
   * **Agregar descripción**: agregue anotaciones a un fragmento de texto. Es un metadato visible para el autor, pero no forma parte de la carta creada.
   * **Salto de página**: si establece el atributo de salto de página de un módulo de texto en False, el módulo de texto no se divide entre las páginas.

   Se abre un editor de texto. Introduzca el texto. La barra de herramientas cambia según el tipo de ediciones que decida realizar: Párrafo, Alineación o Lista:

   ![Seleccione el tipo de barra de herramientas](assets/toolbarselection.png)

   Seleccione el tipo de barra de herramientas: párrafo, alineación o lista

   ![Barra de herramientas Párrafo](assets/fonteditingtoolbar.png)

   Barra de herramientas Párrafo
   [![Barra de herramientas de alineación](assets/paragrapheditingtoolbar.png)](assets/paragrapheditingtoolbar-1.png)Barra de herramientas de alineación

   ![Barra de herramientas de lista ](assets/bulleteditingtoolbar.png)

   Barra de herramientas Lista (haga clic en para abrir una imagen de tamaño completo)

1. Para reutilizar un párrafo de texto de otra aplicación, por ejemplo, de MS Word o páginas de HTML, copie y pegue el texto en el Editor de texto. El formato del texto copiado se mantiene en el Editor de texto.

   Puede copiar y pegar uno o varios párrafos de texto en un módulo de texto editable. Por ejemplo, es posible que tenga un documento de MS Word con una lista con viñetas de justificantes de domicilio aceptables como las siguientes:

   ![pastetextmsword-1](assets/pastetextmsword-1.png)

   Puede copiar y pegar directamente el texto del documento de MS Word en un módulo de texto editable. El formato, como la lista con viñetas, la fuente y el color del texto, se mantiene en el módulo de texto.

   ![pastetexttextmodule](assets/pastetexttextmodule.png)

1. Si es necesario, inserte caracteres especiales en el fragmento de documento. Por ejemplo, puede utilizar la paleta Caracteres especiales para insertar:

   * Símbolos monetarios como €, ￥ y £
   * Símbolos matemáticos como ∑, √, ∂ y ^
   * Símbolos de puntuación como ‟ y &quot;

   ![specialcharacters-1](assets/specialcharacters-1.png)

   Administración de correspondencia ha incorporado la compatibilidad con 210 caracteres especiales. El administrador puede [agregar compatibilidad con caracteres especiales adicionales o personalizados usando la personalización](/help/forms/using/custom-special-characters.md).

1. Para resaltar fragmentos de texto en un módulo en línea editable, seleccione el texto y elija Color de resaltado.

   ![textbackgroundcolorapplied](assets/textbackgroundcolorapplied.png)

   Puede seleccionar directamente un color básico `**[A]**` presente en la paleta Colores básicos o seleccionar **Seleccionar** después de usar el control deslizante `**[B]**` para elegir la sombra adecuada del color.

   Opcionalmente, también puede ir a la pestaña Avanzado para seleccionar el tono, la luminosidad y la saturación adecuados `**[C]**` para crear el color preciso y, a continuación, seleccionar Seleccionar `**[D]**` para aplicar el color para resaltar el texto.

   ![textbackgroundcolor-1](assets/textbackgroundcolor-1.png)

1. Arrastre y suelte los elementos del diccionario de datos y el marcador de posición al texto en el panel de datos.

   A:

   * Agregue un elemento de diccionario de datos al texto, seleccione un elemento de datos de la lista y seleccione Insertar ( ![insert](assets/insert.png)). Si selecciona Protegido, el elemento del diccionario de datos es de solo lectura y aparece en el Editor de cartas, pero no en la interfaz de usuario Crear correspondencia o Creador de correspondencia.
   * Agregue un elemento de marcador de posición en el texto; en el panel Elementos de datos, seleccione Crear nuevo, introduzca los detalles del nuevo elemento de datos y seleccione Crear para agregar el nuevo elemento a la lista. El nuevo marcador de posición se puede insertar en el texto del mismo modo que el elemento de diccionario de datos. Para editar un marcador de posición, seleccione un marcador y haga clic en Editar.

   ![Elementos de marcador de posición](assets/placeholder_elements_in_xmldata.png)

   Los elementos de marcador de posición, tal como se especifican en el archivo de datos de muestra de un diccionario de datos.

   ![Elementos de marcador de posición en una carta](assets/placeholder_elements_in_text.png)

   Los valores de los elementos de marcador de posición de la vista CCR se rellenan desde las variables del diccionario de datos, tal como se especifica en el archivo de datos de muestra.

   También puede utilizar el símbolo @ para buscar y agregar elementos de diccionario de datos y marcador de posición al Editor de texto. Coloque el cursor en el lugar donde desea insertar el elemento. Escriba @ seguido de la cadena de búsqueda. El Editor de texto realiza la operación de búsqueda en todos los elementos de diccionario de datos y marcador de posición disponibles en el fragmento de documento de texto. La operación de búsqueda recupera y muestra los elementos que contienen la cadena de búsqueda como una lista desplegable. Navegue por los resultados de búsqueda y haga clic en el elemento que desee insertar en la ubicación del cursor. Pulse Esc para ocultar los resultados de la búsqueda.

1. Puede utilizar condiciones en línea y repeticiones para que la carta tenga un carácter altamente contextual y esté bien estructurada. Para obtener más información sobre las condiciones en línea y las repeticiones, consulte [Condiciones en línea y repeticiones en cartas](/help/forms/using/cm-inline-condition.md).
1. Seleccione **Guardar**.

#### Insertar hipervínculo en un texto {#insert-hyperlink}

Realice los siguientes pasos para crear un hipervínculo en un recurso de texto:

1. Seleccione el texto o el objeto del modelo de datos en el Editor de texto.

2. Seleccione **[!UICONTROL Vínculo]**. Seleccione el campo **[!UICONTROL Texto alternativo]** para quitar el texto o nombre del objeto del modelo de datos existente.

3. Especifique la URL y seleccione ![Guardar](assets/save_icon.svg).

![Crear un hipervínculo en un recurso de texto](assets/text-create-hyperlink.png)

#### Buscar y reemplazar texto {#searching-and-replacing-text}

Cuando se trabaja con elementos de texto que contienen un gran cuerpo de texto, es necesario buscar una cadena de texto específica. También es posible que tenga que reemplazar una cadena de texto específica por una cadena alternativa.

La función Buscar y reemplazar permite buscar (y reemplazar) cualquier cadena de texto en un elemento de texto. La función también incluye una eficaz opción de búsqueda de expresiones regulares.

#### Búsqueda de texto en un módulo de texto {#to-search-text-in-a-text-module}

1. Abra el módulo de texto en el Editor de texto.

1. Seleccione Buscar y reemplazar.
1. Introduzca el texto que desea buscar en el cuadro de texto Buscar y pulse Buscar. El texto de búsqueda se resalta en el módulo de texto.
1. Para buscar la siguiente instancia del texto, pulse de nuevo Buscar.

   Si continúa pulsando el botón Buscar, la búsqueda continuará hacia la parte inferior de la página. Después de buscar la última instancia del texto, el mensaje **Se ha alcanzado el final del módulo** indica que no se han encontrado más resultados de búsqueda.

   Sin embargo, si no se encuentra ninguna instancia del texto de búsqueda en el módulo de texto, se muestra el mensaje **No se encontró ninguna coincidencia**.

1. Si vuelve a pulsar Buscar, la búsqueda continúa en la parte superior de la página.

#### Opciones de búsqueda {#search-options}

**Coincidir mayúsculas y minúsculas:** la búsqueda devuelve únicamente resultados que coinciden exactamente, con mayúsculas y minúsculas, con el texto que desea buscar.

**Palabra completa:** la búsqueda devuelve únicamente palabras completas.

>[!NOTE]
>
>Si introduce caracteres especiales en el cuadro de texto Buscar, se desactivará la opción Palabra completa.

**Expresiones regulares:** la búsqueda utiliza expresiones regulares. Por ejemplo, la siguiente expresión regular busca direcciones de correo electrónico en un módulo de texto:

`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}`

#### Buscar y reemplazar texto en un módulo de texto {#to-search-and-replace-text-in-a-text-module}

1. Abra el módulo de texto en el Editor de texto.
1. Seleccione Buscar y reemplazar.
1. Introduzca el texto que desea buscar en el cuadro de texto Buscar y el texto que reemplazará el texto de búsqueda, y pulse Reemplazar.
1. Cuando se encuentra el texto de búsqueda, este se reemplaza por el texto del cuadro Reemplazar.

   * Cuando se encuentra otra instancia del texto de búsqueda, dicha instancia se resalta en el módulo de texto. Si vuelve a pulsar Reemplazar, se reemplazará la instancia resaltada y el cursor se desplazará hacia adelante si se encuentra una tercera instancia.
   * Si no se encuentra ninguna otra instancia, el cursor se detendrá en la última instancia reemplazada.

1. Si vuelve a pulsar Buscar, la búsqueda continuará en la parte superior de la página.

   Utilice la opción Reemplazar todo para reemplazar todas las instancias de un texto en el módulo de texto. Si usa ``, se mostrará el número de reemplazos en forma de mensaje en el cuadro de diálogo Buscar y reemplazar.

#### Prácticas recomendadas, sugerencias y trucos para los módulos de texto {#best-practices-tips-and-tricks-for-text-modules}

* Utilice una convención de nomenclatura uniforme para evitar duplicaciones.
* Utilice el enlace de diccionario de datos adecuado en los módulos de texto.
* Al usar el Editor de texto para cambiar un recurso de texto, se aplican las siguientes reglas:

   * **Adición de variable:** permitido
   * **Eliminación de variable:** permitido
   * **Actualización de propiedades:** permitido
   * **Cambio del diccionario de datos:** permitido hasta que no se utilice el elemento de diccionario de datos. No se puede cambiar el diccionario de datos al actualizar.

## Lista {#list}

Una lista es un grupo de fragmentos de documento, que incluyen texto u (otras) listas, condiciones e imágenes. El orden de los elementos de la lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de una lista para replicar un patrón de elementos reutilizable. Las listas se comportan básicamente como destinos que se pueden anidar dentro de otros destinos.

### Implementación de listas {#implementing-lists}

La implementación de listas consta de dos pasos:

1. Definir las propiedades principales, como nombre, descripción o diccionario de datos.
1. Establecer la sección de contenido que forma parte de la lista y, a continuación, definir propiedades como el orden de bloqueo y el acceso a la biblioteca para ella.

### Crear una lista {#create-a-list}

Una lista es un grupo de contenido relacionado que se puede utilizar en una plantilla de carta como una unidad individual. Es posible añadir cualquier tipo de contenido a una lista. Además, las listas también se pueden anidar. Los módulos de lista se pueden especificar de la siguiente forma:

* **ORDENADO**: el orden no se puede cambiar durante el tiempo de ejecución de Crear correspondencia.
* **Acceso a la biblioteca**: los usuarios pueden agregar módulos a la lista. Este indicador especifica si el acceso a la biblioteca está habilitado. Si está habilitado (abierto), el usuario puede agregar módulos a la lista mientras previsualiza la carta.
* Al crear una lista, puede especificar un tipo, como, por ejemplo:
* **Sin formato**: no se aplica ningún formato de estilo adicional a la lista.
* **Con viñetas**: una lista con formato de viñeta simple.
* **Numerado**: una lista numérica con las opciones Estándar (1, 2,...), Romano superior (I, II,...) y Romano inferior (i, ii,...).
* **Con letras**: una lista alfabética con la opción de letras en minúsculas (a, b,...) y mayúsculas (A, B,...).
* **Personalizado**: puede crear cualquier tipo Numerado/Con letras y los valores de prefijo y sufijo que desee.

1. Seleccione **Forms** > **Fragmentos de documento**.

1. Seleccione **Crear** > **Lista**.

1. Especifique la siguiente información para la lista:

   * **Título (opcional): introduzca** un título para la lista. El título no tiene que ser único, y puede contener caracteres especiales y caracteres que no sean de inglés. Se hace referencia a las listas por sus títulos (cuando están disponibles); por ejemplo, en las miniaturas y las propiedades de recursos.
   * **Nombre:** el nombre único de la lista. No pueden existir dos recursos (texto, condición o lista) con el mismo nombre en ningún estado. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente con el valor del campo Título. Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en Nombre, puede editarlo.
   * **Descripción (opcional)**: escriba una descripción para el recurso.
   * **Diccionario de datos (opcional)**: si lo desea, puede seleccionar el diccionario de datos al que desea conectarse. Solo se pueden agregar a la lista recursos que utilicen el mismo diccionario de datos que la lista, o recursos que no tengan asignado ningún diccionario de datos. Asignar un diccionario de datos a una lista facilita a la persona que crea una plantilla de carta la tarea de encontrar la lista adecuada.
   * **Etiquetas (opcional)**: seleccione las etiquetas que desee aplicar. También puede escribir el nombre de una etiqueta nueva y crearla. (La etiqueta nueva se crea al seleccionar **Guardar**).

1. Seleccione **Siguiente**.
1. Seleccione **Agregar recurso**.
1. Para agregar recursos a la lista, selecciónelos en la página Seleccionar Assets y seleccione **Listo**.

   ![Seleccionar recursos para agregarlos a la lista](assets/selectassets.png)

1. Los recursos se agregan a la página Lista de elementos.
Para cambiar el orden de los recursos dentro de la lista, seleccione y mantenga presionado el icono en forma de flechas ( ![dragndrop](assets/dragndrop.png) ), y después arrástrelo y suéltelo. Cuando el usuario abre una plantilla de carta en la interfaz de usuario Crear correspondencia, el contenido se organiza en el orden definido aquí.

   ![Reordenar y configurar recursos en una lista](assets/listitems.png)

1. Puede seleccionar las siguientes opciones para especificar cómo se comporta la lista en la interfaz de usuario de CCR:

   * **Acceso a la biblioteca**: Para habilitar el acceso a la biblioteca para agregar recursos, seleccione Acceso a la biblioteca. Cuando el acceso a la biblioteca está habilitado, el Administrador de reclamaciones puede añadir más contenido a la lista. De lo contrario, el Administrador de reclamaciones se limita al contenido que haya definido para la lista.
   * **Bloquear orden**: para bloquear el orden de los recursos de la lista de modo que el Administrador de reclamaciones no pueda cambiarlo, seleccione Bloquear orden. Si no selecciona esta opción, el Administrador de reclamaciones puede cambiar el orden de los artículos de la lista.

   * **Agregar viñetas**: utilice esta opción para aplicar una viñeta o un estilo de numeración al módulo. Puede utilizar un estilo de lista prediseñado o personalizado. También puede especificar el texto que se mostrará antes y después de cada uno de los elementos de la lista.
   * **Salto de página**: seleccione esta opción ( ![salto](assets/break.png)) para agregar un salto de página entre los contenidos de la lista. Cuando esta opción no está seleccionada ( ![sin_salto](assets/nobreak.png)), si el contenido de la lista se desborda hasta la siguiente página, toda la lista pasa a esa página en lugar de insertar un salto de página en medio de la lista.

   * **Configuración de asignación**: utilice esta opción para especificar el número mínimo y máximo de recursos que se pueden agregar a la lista.

1. Puede seleccionar las siguientes opciones para especificar el comportamiento de cada recurso en la lista durante la ejecución:

   * **Editable:** cuando se selecciona esta opción, el contenido se puede editar en la interfaz de usuario Crear correspondencia. (Esta opción no está disponible para los módulos Lista e Imagen).
   * **Obligatorio:** cuando se selecciona esta opción, el contenido es obligatorio en la interfaz de usuario Crear correspondencia.
   * **Seleccionado:** cuando se selecciona esta opción, el contenido se preselecciona en la interfaz de usuario Crear correspondencia.
   * **Omitir estilo:** cuando se selecciona esta opción, el contenido omite las viñetas y la numeración en la interfaz de usuario Crear correspondencia. (Esta opción no está disponible para los módulos Imagen. Además, no es posible aplicar conjuntamente las opciones Omitir estilo, Compuesto e Ignorar estilo de lista al mismo módulo. Puede utilizar una de ellas si selecciona Agregar viñetas en ese módulo).
   * **Sangría:** puede cambiar el nivel de sangría de cada módulo/contenido seleccionado como parte de la lista. La sangría se especifica en términos de Niveles (empezando por cero), de forma que cada nivel de sangría corresponde a un relleno de 36 puntos.
   * **Compuesto:** Cuando se selecciona, la numeración compuesta se aplica como una combinación del estilo de la lista externa (principal) y su propio estilo. La numeración compuesta de esta lista anidada se basa en el orden en el que aparece en la lista externa.
   * **Ignorar estilo de lista:** si la opción Numeración compuesta no está seleccionada, se activa la opción Ignorar estilo de lista. Esta selección ignora el estilo de la lista anidada, y la numeración continúa desde la lista externa. Por lo tanto, los módulos de la lista anidada se tratan como parte de la propia lista externa, sin tener en cuenta los estilos especificados en la lista anidada. Si la opción Ignorar estilo de lista no está seleccionada para una lista anidada, los módulos que forman parte de esa lista tienen su propio estilo de numeración.
   * **Mantener con siguiente:** establece el salto de página de los recursos contenidos en una lista. Si establece la propiedad Mantener con siguiente del recurso de una lista en **Activado**, ese recurso y el siguiente permanecerán en la misma página. Eso significa que el contenido del recurso seleccionado y el del siguiente no se dividirán en varias páginas.

1. Seleccione **Guardar**.

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks}

* Utilice una convención de nomenclatura uniforme para evitar duplicaciones.
* Use un enlace de diccionario de datos adecuado.
* Al usar el Editor de listas para cambiar una lista, se aplican las siguientes reglas:

   * Actualización de propiedades: permitido
   * **Cambio del diccionario de datos:** permitido hasta que no haya ningún elemento que utilice el diccionario de datos asociado a él. No se puede cambiar el diccionario de datos al actualizar.

## Condiciones {#conditions}

Las condiciones permiten definir qué contenido se incluye en el momento de la creación de la correspondencia o la carta en función de los datos suministrados. La condición se describe en términos de variables de control. Cuando agregue una condición, puede decidir si desea incluir un recurso en función del valor de la variable de control.

Dependiendo de las opciones que elija, solo se evaluará la primera expresión que resulte ser True en función de la variable de condición actual, o toda la condición. Al rellenar la carta en Crear correspondencia (CCR), las condiciones se comportan como “cuadros blancos”. Si una condición genera una lista, se muestran todos los elementos obligatorios y preseleccionados de esta. Si alguno de estos elementos es una condición o una lista, el contenido resultante de estos también se genera como una lista plana de texto y contenido de imagen en orden descendente y por profundidad. Los resultados de la condición pueden ser de cualquier tipo (texto, lista, condición o imagen).

### Implementación de condiciones {#implementing-conditions}

El Editor de condiciones viene con una interfaz de usuario llamada [Generador de expresiones](/help/forms/using/expression-builder.md) que admite la creación de expresiones utilizando varios marcadores de posición y elementos de diccionario de datos. Puede utilizar operandos comunes y funciones locales o globales en dichas expresiones. Cada expresión se puede asociar con un determinado contenido y, alternativamente, puede haber una sección predeterminada si ninguna de las expresiones se evalúa como True. Todas las expresiones se evalúan en la secuencia en la que se definen, se seleccionan las primeras expresiones que devuelven el valor True, y el contenido asociado a ellas se devuelve mediante ese módulo condicional.

Por ejemplo, si el texto de los términos y condiciones de una carta depende del estado en el que se encuentra el cliente, y el diccionario de datos contiene un elemento llamado &quot;state&quot;, puede agregar la condición de la siguiente manera:
* state = NY, seleccione T&amp;C_NY text paragraph
* state = NC, seleccione T&amp;C_NC text paragraph

El Editor de condiciones permite especificar una condición predeterminada. Si el valor de las variables de control no coincide con ninguna de las condiciones, se utiliza el contenido asociado con la condición predeterminada. Después del ejemplo anterior, puede agregar esta fila de condición:
* De forma predeterminada, seleccione T&amp;C_Rest

### Creación de una condición {#create-a-condition}

1. Seleccione **Forms** > **Fragmentos de documento**.
1. Seleccione **Crear > Condición**.
1. Especifique la siguiente información para la lista:

   * **Título (opcional):** introduzca el título de la condición. El título no tiene que ser único, y puede contener caracteres especiales y caracteres que no sean de inglés. Se hace referencia a las condiciones por sus títulos (cuando están disponibles); por ejemplo, en las miniaturas y las propiedades de recursos.
   * **Nombre:** el nombre único de la condición. No pueden existir dos recursos (texto, condición o lista) con el mismo nombre en ningún estado. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título. Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en Nombre, puede editarlo.
   * **Descripción (opcional):** escriba una descripción para la condición.
   * **Diccionario de datos (opcional)**: si lo desea, puede seleccionar el diccionario de datos al que desea conectarse. Solo se pueden agregar a la lista recursos que utilicen el mismo diccionario de datos que la condición, o recursos que no tengan asignado un diccionario de datos. Asignar un diccionario de datos a una lista facilita a la persona que crea una plantilla de carta la tarea de encontrar la condición adecuada.
   * **Etiquetas (opcional)**: si lo desea, seleccione las etiquetas que desee aplicar. También puede escribir el nombre de una etiqueta nueva y crearla. (La etiqueta nueva se crea al seleccionar **Guardar**).

1. Seleccione **Siguiente**.
1. Seleccione **Agregar recurso**.
1. Para agregar un recurso a la condición, selecciónelo en la página Seleccionar Assets y seleccione **Listo**. Los recursos se agregan al panel Expresión.
1. Puede seleccionar las siguientes opciones para especificar el comportamiento de la condición durante la ejecución:

   * **Deshabilitar evaluación de varios resultados\Habilitar evaluación de varios resultados**: Cuando esta opción está habilitada (aparece como &quot;Habilitar evaluación...&quot;), todas las condiciones se evalúan, y el resultado es la suma de todas las condiciones True. Si esta opción está desactivada (aparece como &quot;Deshabilitar evaluación...&quot;), solo se evalúa la primera condición que resulta ser True, y se convierte en el resultado de la condición.
   * **Salto de página**: seleccione esta opción ( ![salto](assets/break.png)) para agregar un salto de página entre los módulos de las condiciones. Cuando esta opción no está seleccionada (![sin_salto](assets/nobreak.png)), si una condición se desborda hasta la siguiente página, toda la condición se pasa a esa página en lugar de insertar un salto de página en medio de la condición.

1. Para cambiar el orden de los recursos dentro de la condición, seleccione y mantenga presionado el icono en forma de flechas ( ![dragndrop](assets/dragndrop.png)), y después arrástrelo y suéltelo. Cuando el usuario abre una plantilla de carta en la interfaz de usuario Crear correspondencia, el contenido se organiza en el orden definido aquí.
1. Seleccione **Delete** para eliminar la fila. Si selecciona Eliminar para la fila predeterminada, solo se borra la información del recurso.
1. Seleccione **Copiar** para duplicar una fila.
1. Seleccione **Editar** para cambiar el recurso o editar la expresión.

   Además:

   * Para actualizar el recurso, seleccione el icono en forma de carpeta de la columna Recurso.
   * Para abrir el Generador de expresiones e insertar una expresión, seleccione el icono en forma de carpeta de la columna Expression. Para obtener más información sobre el Generador de expresiones, consulte [Generador de expresiones](/help/forms/using/expression-builder.md).

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks-1}

* Utilice una convención de nombres uniforme para facilitar la búsqueda y evitar duplicaciones.
* Las condiciones se comportan como instrucciones de caso, por lo que el orden de las condiciones es importante. Se devuelve la primera coincidencia.
* Use un enlace de diccionario de datos adecuado.
* Al usar el Editor de condiciones para editar una condición, se aplican las siguientes reglas:

   * **Adición de variable:** permitido
   * **Eliminación de variable:** permitido
   * **Actualización de propiedades:** permitido
   * **Cambio del diccionario de datos:** permitido hasta que no se utilice el elemento de diccionario de datos.

## Fragmentos de diseños {#layoutfragments}

Un fragmento de diseño se basa en XDP creados en Designer. Para crear fragmentos de diseño, debe crear los XDP y [cargarlos en AEM Forms](/help/forms/using/import-export-forms-templates.md).

Uno o más fragmentos de diseño pueden constituir secciones de una carta y definir el diseño gráfico de esas secciones. Un fragmento de diseño puede contener campos de formulario comunes, como Dirección y Número de referencia, y subformularios vacíos que denotan áreas de destino. Además, los fragmentos de diseño permiten crear tablas e insertarlas en cartas.

Un caso de uso común es localizar patrones de diseño reutilizables en cartas y crear fragmentos de diseño para ellos; por ejemplo, las secciones del saludo, la dirección y el asunto de la carta, que aparece en el mismo orden en varias cartas. Otro ejemplo puede ser una tabla con un número similar de filas y columnas utilizadas en varias cartas.

Puede crear un fragmento de diseño basado en un XDP existente. Un fragmento de diseño puede estar compuesto por campos y áreas de destino o por una o más tablas. Las tablas de un diseño pueden ser estáticas o dinámicas. Se crea un XDP en Designer y se [carga en AEM Forms](/help/forms/using/import-export-forms-templates.md). Un XDP puede conformar la estructura de un fragmento de diseño o de una carta. Más información sobre [Diseño](/help/forms/using/layout-design-details.md).

El uso de fragmentos enlazados a áreas de destino permite cambiar la carta en el momento de su creación. Se puede crear un fragmento de diseño con diferentes dimensiones, y el fragmento apropiado se puede enlazar al área de destino. Los fragmentos de diseño también permiten personalizar algunas de las propiedades de la tabla:

1. Puede aumentar el número de filas y columnas.
1. Puede especificar el texto del encabezado y el pie de página de más filas y columnas.
1. Puede definir la proporción de anchura de las columnas de la tabla. En tiempo de ejecución, las columnas de la tabla cambian de tamaño según la proporción definida y el espacio disponible. La suma de la proporción de anchura debe ser 100. De lo contrario, no es aplicable.
1. Si una tabla es un marcador de posición (contiene solo una celda en blanco), puede definir el tipo (área/campo de destino) de las nuevas columnas.
1. Puede ocultar las filas de encabezado y pie de página.

Antes de realizar este procedimiento, cree un fragmento XFA con Designer. El fragmento puede contener tablas para organizar campos y áreas de destino. Designer permite la creación de dos tipos de tablas: estáticas y dinámicas. Las tablas estáticas contienen un número fijo de filas. Las tablas estáticas pueden contener campos y áreas de destino. Estos campos y áreas de destino no se pueden enlazar a DDE repetitivos. Una tabla dinámica también puede contener una sola fila. Los datos enlazados a celdas de tabla determinan el número de filas de las tablas dinámicas. Una tabla dinámica solo puede contener campos. Los DDE pueden ser repetitivos o no repetitivos.

Tenga en cuenta los siguientes puntos al diseñar tablas:

1. Las tablas se pueden personalizar en el momento de crear el fragmento de diseño. Sin embargo, la opción de personalización solo está habilitada cuando el subformulario principal de la tabla tiene una posición variable.
1. En las tablas dinámicas, todos los campos, filas y tablas repetibles utilizan el enlace &quot;use name&quot; para combinar los datos correctamente.
1. En las tablas dinámicas, todos los DDE repetitivos enlazados a los campos de tabla forman parte de la misma jerarquía. En el caso de los DDE no repetitivos, no existe dicha restricción.
1. En el momento de combinar el fragmento de diseño en las tablas de área de destino principales, se cambia el tamaño según el espacio disponible, pero este cambio solo se produce cuando el fragmento de diseño no contiene ningún área de destino o campo directamente en el subformulario de nivel superior. El área de destino y los campos están permitidos en la tabla.
1. Puede crear tablas de marcador de posición. Las tablas de marcador de posición tienen una sola celda en blanco.

* En este tipo de tablas, puede personalizar las siguientes propiedades en el momento de la creación del fragmento.

   * recuento de filas
   * recuento de columnas
   * encabezado y pie de página de cada columna
   * tipo (área/campo de destino) de cada columna
   * proporción de anchura de cada columna

* En las tablas que no son de marcador de posición, puede personalizar las siguientes propiedades:

   * recuento de filas
   * recuento de columnas
   * encabezado y pie de página de una columna adicional
   * proporción de anchura de cada columna

Puede anidar fragmentos en una carta. Eso significa que puede agregar un fragmento dentro de otro. La solución Administración de correspondencia admite hasta cuatro niveles de anidamiento dentro de una carta: **Carta *>*Fragmento *>*Fragmento *>*Fragmento *>*Fragmento.**

Para ver un ejemplo detallado del uso de tablas estáticas y dinámicas en fragmentos de diseño, consulte [Ejemplo con archivos de ejemplo: uso de tablas estáticas y dinámicas en una carta](#examplewithsamplefiles).

### Creación de un fragmento de diseño {#creating-a-layout-fragment}

1. Seleccione **Crear** > **Fragmento de diseño**.
1. Administración de correspondencia muestra los XDP disponibles. Seleccione el XDP en el que desea basar el fragmento de diseño y seleccione **Siguiente**.
1. Especifique la siguiente información para el diseño:

   * **Título (opcional):** introduzca el título del fragmento de diseño. El título no tiene que ser único, y puede contener caracteres especiales y caracteres que no sean de inglés. Se hace referencia a los fragmentos de diseño por sus títulos (cuando están disponibles); por ejemplo, en las miniaturas y las propiedades de recursos.
   * **Nombre:** el nombre único del fragmento de diseño. No pueden existir dos recursos (texto, condición o lista) con el mismo nombre en ningún estado. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título. Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en Nombre, puede editarlo. Este nombre aparece en la lista de la interfaz de usuario Administrar recursos.
   * **Descripción (opcional)**: la descripción que aparece en la lista de la interfaz de usuario Administrar recursos.
   * **Etiquetas (opcional)**: si lo desea, seleccione las etiquetas que desea aplicar a la condición. También puede escribir el nombre de una etiqueta nueva y crearla.

1. Seleccione la ficha **Tabla** y especifique la siguiente información para el diseño:

   * **Configuración para**: seleccione la tabla que está configurando. El sufijo del nombre de tabla en la lista desplegable es (Estático) si la tabla es estática o (Dinámico) si la tabla es dinámica. Las tablas estáticas contienen un número fijo de filas. Las tablas estáticas pueden contener campos y áreas de destino. Estos campos y áreas de destino no se pueden enlazar a DDE repetitivos. Los datos enlazados a celdas de tabla determinan el número de filas de las tablas dinámicas.

   * **Filas**: seleccione el número de filas del diseño. El recuento de filas configurado debe ser mayor o igual que el recuento de filas original.
   * **Columnas**: seleccione el número de columnas del diseño. El recuento de columnas configurado debe ser mayor o igual que el recuento de columnas original.

   Es necesario proporcionar los siguientes detalles para cada columna:

   * **Encabezado**: el texto que se mostrará en el encabezado.
   * **Pie de página**: el texto que se mostrará en el pie de página.
   * **Tipo**: el tipo de columna adicional. Campo o área de destino. El tipo está habilitado para tablas estáticas de marcador de posición. El tipo se puede definir en el nivel de columna y no en el de celda. Todas las celdas de una columna ampliada serán del mismo tipo. En las tablas dinámicas, todas las columnas son del tipo Campo. En las tablas que no son de marcador de posición, no se puede definir el tipo de columnas adicionales. En este caso, el tipo de celdas adicionales de la columna ampliada es el mismo que el tipo de la última columna de esa fila; y el tipo de celda de la fila adicional es el mismo que el tipo de la última celda de esa columna.
   * **Proporción de anchura:** la proporción de las anchuras de columna de la tabla.

   Para ver un ejemplo detallado del uso de tablas estáticas y dinámicas en fragmentos de diseño, consulte [Ejemplo con archivos de ejemplo: uso de tablas estáticas y dinámicas en una carta](#examplewithsamplefiles).

1. Seleccione **Guardar**.

### Cargar un XDP en Administración de correspondencia {#upload-an-xdp-to-correspondence-management}

Para obtener instrucciones sobre cómo cargar/importar un XDP en Administración de correspondencia, consulte [Importación y exportación de recursos a AEM Forms](/help/forms/using/import-export-forms-templates.md).

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks-2}

#### Establecimiento del enlace predeterminado del subformulario {#set-the-default-subform-binding}

Al crear áreas de destino en Designer, es recomendable establecer el enlace predeterminado de todos los subformularios nuevos en &quot;ninguno&quot;.

Para establecer el enlace predeterminado:

1. En Designer, seleccione **Herramientas** > **Opciones** > **Enlaces de datos** > **Enlace de subformulario**.

1. En la lista Enlace predeterminado para nuevos subformularios, seleccione **Sin enlace de datos**.

Esto garantiza que a los subformularios insertados mediante el comando Insertar > Subformulario o arrastrando y soltando desde la paleta Objeto se les asigne como enlace la opción &quot;ninguno&quot; de forma predeterminada. Esto significa que, de forma predeterminada, cualquier nuevo subformulario es un área de destino a menos que se le agregue contenido, se cambie su configuración de enlace o se asigne un nombre al subformulario con el sufijo &quot;_int&quot;.

#### Sección 508 - Cumplimiento {#section-compliance}

Si la carta final creada en la interfaz de usuario Crear correspondencia se utiliza para rellenar un flujo de trabajo posterior, siga estas recomendaciones relacionadas con la Sección 508 durante la creación del diseño. En caso contrario, la carta PDF está destinada a su exhibición, y puede ignorar estas recomendaciones:

* Todos los subformularios de área de destino y todos los campos del diseño tienen un orden de tabulación.
* Los campos con pie de ilustración cumplen los requisitos establecidos por la Sección 508 de forma predeterminada. El atributo /field/help/speak@priority del campo está establecido en &quot;personalizado&quot; de forma predeterminada, lo que significa que, a menos que se proporcione texto personalizado para los lectores de pantalla, estos leerán el título del campo.
* Los campos sin pie de ilustración especifican información sobre herramientas e indican que los lectores de pantalla leen esa información configurando

`/field/assist/speak@priority="toolTip"` y especificando el texto de la información sobre herramientas en `/field/assist/toolTip`.

#### Formatos de fecha en Designer y el Administrador de configuración de recursos {#date-formats-in-designer-and-asset-configuration-manager}

Al diseñar un diseño en Designer, asegúrese de que los formatos de los campos de fecha coinciden con los formatos de fecha especificados en Formatos de visualización de datos en las [Propiedades de configuración de Administración de correspondencia](/help/forms/using/cm-configuration-properties.md). Para obtener más información, consulte &quot;Formatting field values and using patterns&quot; en la Ayuda de Designer.

#### Captura de intervalos de fechas {#capturing-date-ranges}

Cuando se trata de una combinación de fechas, como startDate - endDate, utilice un solo subformulario para garantizar su correcta alineación en la carta final y minimizar el número de campos.

#### Configuración del enlace a nivel de formulario {#setting-form-level-binding}

Cuando un diseño contiene un gran número campos y áreas de destino asignados a elementos XML únicos, utilice enlaces de nivel de formulario y cree un nodo independiente para cada elemento. Los campos enlazados en el nivel de formulario se omiten al asignar datos en Administración de correspondencia.

#### No utilice áreas de destino de subformulario en una página maestra {#do-not-use-subform-target-areas-in-a-master-page}

Las áreas de destino de subformulario de una página maestra no son visibles en la interfaz de usuario de Administrar recursos, y no se pueden asignar datos a ellas.

#### Elección de posiciones y tipos adecuados para las áreas de destino {#choosing-appropriate-positions-and-types-for-target-areas}

Al preparar el diseño, tenga cuidado al elegir los subformularios. Si la presentación contiene un solo subformulario, puede ser de tipo variable. Una vez colocados los campos en el subformulario, se puede ajustar en otro subformulario para que el subformulario ajustado también tenga posición variable y el diseño no se vea alterado.

#### Colocación de campos en páginas maestras {#placing-fields-on-master-pages}

Tenga en cuenta lo siguiente cuando coloque un campo en una página maestra:

* Establezca el enlace de los campos de la página maestra en Usar datos globales.
* No coloque el campo directamente debajo de la raíz PageArea de la página maestra.
* Ajuste el campo en un subformulario al que se le haya asignado un nombre y asegúrese de que el enlace de ese subformulario está definido en Usar nombre.

## Creación de tablas mediante fragmentos de diseño {#creating-tables-using-layout-fragments}

Muchas plantillas de carta contienen tablas. Las tablas pueden ser estáticas; por ejemplo, es el caso de las tablas de términos y condiciones, en las que cada fila representa una condición y cada fragmento se muestra en una columna independiente. Las tablas también pueden ser dinámicas; es el caso de la información de cuentas, que contiene información como el nombre del cliente, el ID de cuenta, el número de transacción y el importe.

* **Tablas estáticas**: a veces, las tablas se crean con filas que tienen un número diferente de columnas, como las tablas de términos y condiciones, en las que cada fila representa una condición y cada condición puede tener diferentes subfragmentos. Cada fragmento se muestra en una columna independiente.
* **Tablas dinámicas**: los fragmentos de diseño permiten enlazar los campos de una tabla dinámica a los DDE de colección. A la hora de crear la carta, las filas de la tabla se generan según el tamaño de los DDE de colección.

El DD tiene un elemento de colección denominado Nominee_details que tiene un elemento compuesto con tres elementos primitivos: Nominee_name, Nominee_address y Nominee_gender.
El XDP dinámico también tiene los mismos encabezados. Por lo tanto, puede asignar los campos XDP dinámicos a los campos de DD mencionados anteriormente.

### Ejemplo con archivos de ejemplo: uso de tablas estáticas y dinámicas en una carta {#examplewithsamplefiles}

En este ejemplo se muestra cómo crear una tabla dinámica y una tabla estática, cómo enlazar la tabla dinámica a DDE y, a continuación, cómo crear una carta que incluya esas dos tablas. Mientras trabaja con este ejemplo, puede crear los archivos desde cero o utilizar los archivos de entrada indicados en los pasos.

1. Cree el diccionario de datos (DD) que desee usar en el ejemplo, tal como se muestra en el gráfico.

   A continuación, seleccione el DD y exporte los datos de muestra. El archivo XML que obtiene contiene datos de empleados y tres instancias para Nominee_details (de forma predeterminada, se descargan 3 instancias. Puede agregar más o eliminarlas según sus necesidades). Actualice los valores y, a continuación, importe los datos de prueba en el DD. El archivo CMP es el paquete y contiene el DD. Importe el DD en Administración de correspondencia.

   Para obtener más información sobre cómo trabajar con el diccionario de datos y los datos de prueba, consulte [Diccionario de datos](/help/forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Estructura del diccionario de datos](assets/dd.jpeg)

[Obtener archivo](assets/exportpackage_1431709897770.cmp.zip)

1. Cree dos XDP (fragmentos de diseño) en Designer: una tabla dinámica y una tabla estática. En ambos diseños:

   * Agregue un subformulario a la columna de la tabla. Asegúrese de cambiar el diseño del subformulario principal de la tabla a De posición variable y de quitar los enlaces del subformulario de la tabla.
   * Agregue un subformulario a la celda de la tabla. Asegúrese de cambiar el diseño del subformulario principal de la tabla a De posición variable y de quitar los enlaces del subformulario de la tabla.

   También puede utilizar los XDP estáticos y dinámicos adjuntos a este paso.

   Para obtener más información sobre cómo trabajar con fragmentos de diseño, consulte [Fragmentos de diseños](#layoutfragments).
Para obtener más información sobre la creación de diseños, consulte [Ayuda de Designer](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/).

[Obtener archivo](assets/static.xdp.zip)

[Obtener archivo](assets/dynamic.xdp.zip)

1. Cargue los XDP en AEM Forms.
1. Cree un fragmento de diseño basado en el XDP dinámico. La pestaña Tabla de las propiedades muestra que la tabla es dinámica (campo Configuración para). El número de filas (1) y columnas (3) se deriva del fragmento de diseño o XDP.

   Los campos de este diseño se enlazan posteriormente al DD importado y, en la carta, el número de filas se crea dinámicamente en función del número de registros del archivo de datos de prueba (el archivo de datos XML adjunto al DD).

   ![Pantalla Creación de un fragmento de diseño](assets/dynamictableproperties.png)

   Haga clic en la imagen para abrirla a tamaño completo

1. Cree un fragmento de diseño basado en el XDP estático. La ficha Tabla de las propiedades muestra que la tabla es estática (campo Configuración para ). El número de filas (1) y columnas (3) se deriva del fragmento de diseño o XDP.

   Aquí puede cambiar el número de columnas y filas. Según lo que elija en esta pantalla, el número de filas y columnas de la tabla estática permanecerán fijos en la carta que se crea con este diseño.
   [![Pantalla Creación de un fragmento de diseño](assets/statictableproperties.png)](assets/statictableproperties-1.png)

1. Cree una carta utilizando ambos fragmentos de diseño. Cuando inserte el XDP dinámico en la carta, establezca el enlace de sus campos en los elementos de colección del diccionario de datos.

   Para obtener más información sobre la creación de cartas y plantillas de carta, consulte [Crear carta](/help/forms/using/create-letter.md).

1. Guarde la carta y previsualícela. Cuando se previsualiza la carta, los valores del diccionario de datos se muestran en ella. En el caso de la tabla dinámica, hay tres filas. Esto se debe a que los datos de prueba tienen tres registros en estas filas.

   En el caso de la tabla estática, hay tantas filas y columnas como haya especificado al crear el fragmento de diseño.

   ![Tabla estática en la carta](assets/statictableletter.png)

   En la tabla dinámica, las tres filas aparecen según el número de registros del archivo de datos de prueba. Esto ocurre porque, al agregar el diseño a la carta, se crea un enlace entre los campos de la tabla dinámica y los elementos de colección del diccionario de datos. Los valores Nombre, Dirección y Género se rellenan desde el archivo de datos de prueba utilizado.

   ![Tabla dinámica en la carta](assets/dynamictableletter.png)

## Creación de una copia de un fragmento de documento {#create-a-copy-of-a-document-fragment}

Para crear rápidamente un fragmento de documento con propiedades y contenido similares a los de un fragmento de documento existente, puede copiarlo y pegarlo.

1. Seleccione uno o varios fragmentos en la lista de fragmentos de documento. La interfaz de usuario muestra el icono Copiar.
1. Seleccione Copiar. La interfaz de usuario muestra el icono Pegar. Si lo desea, también puede abrir una carpeta antes de pegar el fragmento. Las carpetas pueden contener recursos con los mismos nombres. Para obtener más información sobre las carpetas, consulte [Carpetas y organización de recursos](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Seleccione Pegar. Aparecerá el cuadro de diálogo Pegar. Si está copiando y pegando los fragmentos del documento en el mismo sitio, el sistema asignará automáticamente nombres y títulos a las nuevas copias de las cartas, pero podrá editarlos.
1. Si es necesario, edite el Título y el Nombre con los que desea guardar la copia del fragmento de documento.
1. Seleccione Pegar. Se crea la copia del fragmento del documento.
