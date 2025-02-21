---
title: Prácticas recomendadas para crear formularios en Forms Designer
description: Obtenga información sobre las prácticas de accesibilidad recomendadas para crear formularios en Forms Designer
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 1a4df932f0933e9644b40eb5d02900231b6a48c6
workflow-type: tm+mt
source-wordcount: '11687'
ht-degree: 0%

---

# Prácticas recomendadas para crear formularios en Forms Designer

LiveCycle Designer le permite crear contenido de formulario enriquecido y cumplir con las directrices de la sección 508. Esta guía contiene una descripción general de las prácticas recomendadas para crear un formulario accesible y directrices para implementar estas prácticas recomendadas mediante LiveCycle Designer. Se tratan las siguientes prácticas recomendadas:

1. [Utilice formularios sencillos y fáciles de usar](#keep-simple)
1. [Configurar las propiedades del formulario para generar información de accesibilidad](#configure-form-properties)
1. [Elija los controles adecuados](#choose-right-controls)
1. [Proporcionar equivalentes de texto para las imágenes](#provide-text-equivalents)
1. [Proporcionar las etiquetas adecuadas para los controles del formulario](#provide-proper-labels)
1. [Asegúrese de que la lectura y el orden de tabulación sean correctos](#ensure-reading-tab-order)
1. [Asegúrese de que los controles del formulario sean accesibles mediante teclado](#ensure-keyboard-accessible)
1. [Usar el color de forma responsable](#use-color-responsibly)
1. [Proporcionar celdas de encabezado para las tablas](#provide-heading-cells)
1. [Proporcionar una estructura de formulario navegable](#provide-navigable-form)
1. [Evitar scripts disruptivos](#avoid-disruptive-scripting)
1. [Asegúrese de que todo el contenido de audio y vídeo sea accesible](#ensure-audio-video-accessible)
1. [Identificar el lenguaje natural y cualquier cambio en el lenguaje](#identify-natural-language)

## Utilice formularios sencillos y fáciles de usar {#keep-simple}

Un formulario no es accesible si no es fácil de usar. Debe intentar diseñar formularios que sean sencillos y utilizables. Un diseño sencillo de controles y campos con subtítulos claros y significativos e información sobre herramientas hará que el formulario sea mucho más fácil de usar para todos los usuarios.
El diseño de formularios con una disposición clara y lógica, y que proporcionen instrucciones claras y sencillas, ayudará a todos los usuarios a rellenar los formularios con la mayor facilidad posible. Las funciones de navegación, como el orden de tabulación y los métodos abreviados del teclado, deben admitir el orden lógico de los objetos del formulario.

### Evite mover, cerrar o parpadear el contenido

Algunos individuos con epilepsia fotosensible pueden tener una convulsión desencadenada por el movimiento en frecuencias superiores a 2 Hz (1 Hz, o Hertz, es igual a uno por segundo) e inferiores a 55 Hz (55 por segundo).

El movimiento a menos de 2 Hz se considera lo suficientemente lento como para ser seguro para las personas con epilepsia fotosensible. El movimiento a más de 55 Hz se considera imperceptible.

Los desarrolladores deben tener en cuenta estos parámetros al utilizar cualquier movimiento en el contenido web.

Otros usuarios pueden tener discapacidades cognitivas que dificultan la concentración cuando hay contenido animado o parpadeante presente en el formulario.

En general, intente evitar utilizar efectos ópticos insertados por secuencias de comandos, como texto parpadeante o animación, en formularios interactivos. Estos efectos reducen la facilidad de uso de los formularios para determinados usuarios.

Puntos de comprobación relacionados
* Sección 508 §11934.21

   * (h) Cuando se visualice la animación, la información se podrá visualizar al menos en un modo de presentación no animado a elección del usuario.
   * (k) El software no debe utilizar texto parpadeante o intermitente, objetos u otros elementos que tengan una frecuencia de parpadeo mayor de 2 Hz e inferior a 55 Hz.
* Sección 508 §11934.22
   * (j) Las páginas estarán diseñadas para evitar que la pantalla parpadee con una frecuencia superior a 2 Hz e inferior a 55 Hz.
* WCAG 1.0
   * 7.1 Hasta que los agentes de usuario permitan a los usuarios controlar los parpadeos, evite que la pantalla parpadee. (P1)
   * 7.2 Hasta que los agentes de usuario permitan a los usuarios controlar los parpadeos, evite que el contenido parpadee (es decir, cambie la presentación a una velocidad normal, como encender y apagar) (P2).
   * 7.3 Hasta que los agentes de usuario permitan a los usuarios congelar el contenido en movimiento, evite el movimiento en las páginas.
   * 14.1 Utilice el lenguaje más claro y sencillo adecuado para el contenido de un sitio.
* WCAG 2.0
   * 2.2.2 Pausar, parar, ocultar: Para mover, parpadear, desplazar o actualizar automáticamente la información, todas las siguientes opciones son verdaderas: (Nivel A)
   * 2.3.1 Tres parpadeos o por debajo de los límites: Las páginas web no contienen nada que parpadee más de tres veces en un segundo período, o el parpadeo está por debajo de los umbrales generales de parpadeo y parpadeo rojo. (Nivel A)
   * 2.3.2 Tres parpadeos: Las páginas web no contienen nada que parpadee más de tres veces en un segundo periodo. (Nivel AAA)


## Configurar las propiedades del formulario para generar información de accesibilidad {#configure-form-properties}

Para que un formulario sea accesible, debe ser [perceptible](https://www.w3.org/TR/WCAG20/#perceivable) por la tecnología de asistencia. Por ejemplo, la mayoría de los lectores de pantalla no tendrán en cuenta el diseño visual del formulario, sino la estructura subyacente.

Para implementar esta estructura subyacente mediante LiveCycle Designer, debe crear un formulario de PDF con información de accesibilidad (a veces denominada etiquetas) incluida para que el lector de pantalla u otra tecnología de asistencia puedan leer el texto y los componentes del formulario. En un formulario con información de accesibilidad, cada elemento contiene información sobre su propia estructura, además de información sobre cómo está relacionado con otros elementos o depende de ellos. Los lectores de pantalla solo pueden identificar y describir el contenido de un documento con precisión en los archivos PDF con información de accesibilidad incluida.

Para crear un formulario accesible, debe configurar las propiedades del formulario para que LiveCycle Designer genere la información de accesibilidad al guardar el diseño de formulario como archivo de PDF:
1. Elija Archivo > Propiedades del formulario.
1. Haga clic en la ficha Opciones de guardado y, en el área de PDF, asegúrese de que la opción Generar información de accesibilidad (etiquetas) para Acrobat está seleccionada.
1. Haga clic en Aceptar.

En LiveCycle Designer, esta opción está seleccionada de forma predeterminada.

>[!NOTE]
> Estas opciones solo se aplican al guardar el diseño de formulario como archivo PDF. No se aplican a los archivos de PDF creados con LiveCycle Forms, que tiene opciones de configuración independientes de esta opción en LiveCycle Designer.

**Puntos de comprobación relacionados**

* Sección 508 §1194.21
   * (d) La tecnología de asistencia dispondrá de información suficiente sobre un elemento de interfaz de usuario, incluida la identidad, el funcionamiento y el estado del elemento. Cuando una imagen representa un elemento de programa, la información transmitida por la imagen también debe estar disponible en texto.
   * (l) Cuando se utilicen formularios electrónicos, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.
* Sección 508 §1194.22
   * (n) Cuando los formularios electrónicos estén diseñados para ser cumplimentados en línea, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.


## Elija los controles adecuados {#choose-right-controls}

Al diseñar los formularios, utilice los objetos de desarrollo de las pestañas disponibles en la Biblioteca de objetos de LiveCycle Designer. Para mostrar este panel, seleccione Ventana > Biblioteca de objetos o presione Mayús+F12 (consulte la Figura 1).

![Panel de biblioteca de objetos](/help/forms/using/assets/image-1.png)

Figura 1: **Panel Biblioteca de objetos**

Si utiliza otros objetos, la tecnología de asistencia puede ignorarlos. El uso únicamente de los objetos estándar le ahorra el esfuerzo adicional de definir las propiedades de Accesibilidad para los objetos que ha creado usted mismo. Si crea y utiliza sus propios objetos personalizados, asegúrese de utilizar la paleta Accesibilidad para establecer propiedades de accesibilidad como Rol, Información del objeto, Prioridad de Reader de pantalla y Texto personalizado de Reader de pantalla. Para mostrar la paleta Accesibilidad, elija Ventana > Accesibilidad.

**Puntos de comprobación relacionados**
* Sección 508 §1194.21
   * (c) Se proporcionará una indicación en pantalla bien definida del enfoque actual que se mueva entre los elementos interactivos de la interfaz a medida que cambie el enfoque de entrada. El objetivo se expondrá mediante programación de modo que la tecnología de asistencia pueda rastrear el enfoque y los cambios de enfoque.
   * (d) La tecnología de asistencia dispondrá de información suficiente sobre un elemento de interfaz de usuario, incluida la identidad, el funcionamiento y el estado del elemento. Cuando una imagen representa un elemento de programa, la información transmitida por la imagen también debe estar disponible en texto.
   * (l) Cuando se utilicen formularios electrónicos, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.
* Sección 508 §1194.22
   * (n) Cuando los formularios electrónicos estén diseñados para ser cumplimentados en línea, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.

* WCAG 2.0
   * 3.2.4 Identificación coherente: Los componentes que tienen la misma funcionalidad dentro de un conjunto de páginas web se identifican de forma coherente. (Nivel AA).
   * 4.1.2 Nombre, Función, Valor: Para todos los componentes de la interfaz de usuario (incluidos, entre otros, elementos de formulario, vínculos y componentes generados por secuencias de comandos), el nombre y la función se pueden determinar mediante programación; los estados, las propiedades y los valores que el usuario puede definir se pueden definir mediante programación; y la notificación de los cambios en estos elementos está disponible para los agentes de usuario, incluidas las tecnologías de asistencia. (Nivel A)


## Proporcionar equivalentes de texto para las imágenes {#provide-text-equivalents}

Las imágenes pueden ayudar a mejorar la comprensión de los usuarios con algunos tipos de discapacidad. Sin embargo, para los usuarios de lectores de pantalla, las imágenes reducirán la accesibilidad del formulario si no proporciona una alternativa textual.

Si decide utilizar imágenes, proporcione descripciones de texto para todos los objetos de imagen y campo de imagen. Asegúrese de que el texto describa el objeto y su propósito en el formulario. Cuando define una alternativa de texto, el lector de pantalla leerá esta alternativa cuando encuentre la imagen. Por este motivo, una imagen que contenga información siempre debe tener especificada una alternativa textual.

Puede proporcionar descripciones de texto mediante las propiedades Información del objeto o Texto de Reader de pantalla personalizado en la paleta Accesibilidad o a través de campos de texto, títulos y nombres de objeto, tal como se especifica en la opción Nombre de la pestaña Enlace. Por ejemplo, la Figura 2 muestra un ejemplo de una imagen que contiene el texto &quot;Obtener Adobe Reader&quot;. Dado que un lector de pantalla no puede leer texto que forme parte de una imagen, debe incluir una alternativa de texto en el campo Texto de Reader de pantalla personalizada en la paleta Accesibilidad para este objeto. En la mayoría de los casos, el texto alternativo debe ser el mismo que el texto visible en la imagen (ver Figura 2).

![Especificar texto alternativo para una imagen mediante la paleta Accesibilidad](/help/forms/using/assets/image-2.png)

Figura 2: **Especificación de texto alternativo para una imagen mediante la paleta Accesibilidad**

Al especificar el texto alternativo, tenga en cuenta lo siguiente:
* Si el objeto de imagen o la imagen digitalizada incluyen información importante para el formulario, cree texto para la imagen en la paleta Accesibilidad que describa el objeto y su propósito. El texto del logotipo de una empresa, por ejemplo, podría consistir en las palabras &quot;logotipo de la empresa&quot; y el nombre de la empresa.
* Si el objeto de imagen contiene información de color semántico, incluya esto también en la descripción. Una descripción de un semáforo en verde, por ejemplo, podría ser &quot;Transmisión correcta&quot; y la descripción de una luz roja podría ser &quot;Transmisión fallida&quot;.
* Si utiliza gráficos complejos, como gráficos de barras, proporcione la información en una versión alternativa accesible, como una tabla o una descripción textual más larga.
* No cree descripciones de texto para imágenes estáticas que solo se utilicen para la decoración.
* No utilice datos escaneados como información de fondo. Esto puede ocurrir cuando un diseñador analiza un formulario de impresión y utiliza Adobe LiveCycle Designer para agregar nuevos campos al formulario. Los lectores de pantalla no pueden detectar los datos escaneados en este estado.

Cuando se incluye contenido gráfico puramente decorativo en los formularios, se recomienda asegurarse de que los lectores de pantalla no anuncien la presencia de la imagen. Para la mayoría de los lectores de pantalla, esto se puede lograr estableciendo la propiedad Texto de Reader de pantalla en Ninguno en la paleta Accesibilidad. Si no lo hace, algunos lectores de pantalla pueden anunciar la presencia de un gráfico, sin indicar lo que representa. En el caso de las imágenes dinámicas, como los objetos de campo de imagen, asegúrese de que las alternativas de texto se actualicen correctamente cuando se cambie la imagen. No cree descripciones de texto para objetos de campo de imagen que solo se utilicen para decoración. Puede utilizar el lenguaje de script FormCalc para asignar descripciones de texto a un objeto de campo de imagen de forma dinámica. FormCalc es el lenguaje de script estándar de Adobe LiveCycle Designer. Por ejemplo, considere un formulario con un campo de imagen denominado ImageField1 y el texto asociado en el nodo imagetext de los datos de tiempo de ejecución. Puede usar scripts para pasar este texto en un evento apropiado (como `form:ready`) de la siguiente manera:

`ImageField1.assist.toolTip = $record.imagetext.value`

Puntos de comprobación relacionados
* Sección 508 §1194.22
   * (a) Se proporcionará un equivalente textual para cada elemento no textual (por ejemplo, mediante &quot;alt&quot;, &quot;longdesc&quot; o en el contenido del elemento).
* WCAG 1.0
   * 1.1 Proporcione un equivalente textual para cada elemento no textual (por ejemplo, a través de &quot;alt&quot;, &quot;longdesc&quot; o en el contenido del elemento). Esto incluye: imágenes, representaciones gráficas de texto (incluidos símbolos), regiones de mapa de imagen, animaciones (por ejemplo, GIF animados), applets y objetos programáticos, arte ascii, fotogramas, scripts, imágenes utilizadas como viñetas de lista, espaciadores, botones gráficos, sonidos (reproducidos con o sin interacción del usuario), archivos de audio independientes, pistas de audio de vídeo y vídeo (P1).
* WCAG 2.0
   * 1.1.1 Contenido no textual: todo contenido no textual que se presenta al usuario tiene una alternativa textual que cumple el objetivo equivalente, excepto para las situaciones que se enumeran a continuación. (Nivel A)


## Proporcionar las etiquetas adecuadas para los controles del formulario{#provide-proper-labels}

La etiqueta o el rótulo de un control de formulario identifica lo que se supone que representa el control de formulario. Por ejemplo, el texto “Nombre” indica a los usuarios que deben introducir su nombre en un campo de texto. Para que los lectores de pantalla puedan acceder, la etiqueta debe asociarse mediante programación al control de formulario o este debe configurarse con información de accesibilidad adicional mediante la paleta Accesibilidad; no es suficiente con colocar un objeto de texto junto al control. Para los usuarios con visión reducida o con visión reducida, es importante que la etiqueta esté colocada adecuadamente junto al control. Ambas técnicas se analizarán en las secciones siguientes.

### Especificar texto de etiqueta accesible mediante la paleta Accesibilidad

La etiqueta que perciben los usuarios del lector de pantalla no necesariamente tiene que ser la misma que el pie de ilustración visual. En algunos casos, es posible que desee ser más específico sobre el propósito del control.
Para cada objeto de campo de un formulario, se puede utilizar la paleta Accesibilidad (consulte la Figura 3) para especificar lo que el lector de pantalla anunciará para identificar el campo de formulario específico.

Para utilizar la paleta Accesibilidad, siga estos pasos:

1. Muestre la paleta Accesibilidad seleccionando Ventana > Accesibilidad o pulsando Mayús+F6.
1. Seleccione un objeto del formulario. La paleta mostrará las propiedades de accesibilidad del objeto.

![La paleta de accesibilidad](/help/forms/using/assets/image-3.png)

Figura 3: **La paleta de accesibilidad**

Cuando el formulario se guarda como una PDF, LiveCycle Designer busca en el formulario las propiedades Texto personalizado, Información del objeto, Pie de ilustración y Nombre, en ese orden, para encontrar el texto que deben leer los lectores de pantalla. Puede anular este orden predeterminado si utiliza la opción Prioridad de Reader de pantalla en la paleta Accesibilidad:

1. Seleccione el objeto en el diseño de formulario.
1. Haga clic en la paleta Accesibilidad.
1. Seleccione cualquier opción de Prioridad de Reader de pantalla que no sea Ninguna.

Las opciones disponibles son las siguientes:

* **Texto personalizado**, que se establece en el campo Texto de Reader de pantalla personalizada de la paleta Accesibilidad. Esta opción le permite especificar el texto que desea que utilice la tecnología de asistencia, como lectores de pantalla. El uso de la configuración Pie de ilustración es mejor para la mayoría de las situaciones: la creación de texto de Reader en pantalla personalizado debe considerarse una opción solo cuando se utiliza Pie de ilustración o no es posible utilizar la información del objeto.
* **Información de objeto**, que se establece en el campo Información de objeto de la paleta Accesibilidad. Para la mayoría de los objetos, la información sobre herramientas aparece en tiempo de ejecución cuando el usuario pasa el puntero sobre el objeto. La información sobre herramientas aparece para algunos objetos de solo lectura, como el objeto de código de barras de un formulario en papel, solo cuando se utiliza un lector de pantalla.
* **Pie de ilustración**, lo que hará que LiveCycle Designer use la etiqueta (visual) asociada al campo de formulario como texto del lector de pantalla.
* **Nombre**, que se establece en el campo Nombre de la ficha Enlace. Tenga en cuenta que este nombre no puede contener espacios.
* **Ninguno**, lo que hará que el objeto no tenga un nombre. Esto nunca se recomienda para los controles del formulario.

Tenga en cuenta lo siguiente al utilizar la paleta Accesibilidad para el etiquetado de controles de formulario:

* Si el título del control de formulario describe correctamente el control, los lectores de pantalla podrán acceder a él. En este caso, deje vacíos los campos Texto personalizado y Información del objeto en la paleta Accesibilidad o cambie la Prioridad de Reader de pantalla a Pie de ilustración.
* Al segmentar lectores de pantalla, no tiene sentido especificar descripciones de texto diferentes para el mismo control de formulario, ya que solo se utilizará uno: El primer campo no vacío en el orden de prioridad de Screen Reader. Por ejemplo, no hay razón para especificar texto personalizado y texto de información del objeto para un lector de pantalla.
* De forma predeterminada, el lector de pantalla lee el pie de ilustración si no se especifica nada en el cuadro Información del objeto o en el cuadro de texto Reader de pantalla personalizada.
* No utilice la paleta Accesibilidad para crear descripciones de campos o áreas invisibles.
* Si tiene que crear una descripción con las opciones Información del objeto o Texto de Reader en pantalla personalizado, incluya siempre el pie de ilustración visible en el formulario, excepto cuando el pie de ilustración visible no tenga sentido, por ejemplo, cuando el propio pie de ilustración esté abreviado. Esto ayuda a los usuarios del lector de pantalla a comunicarse eficazmente con otros usuarios sobre los elementos de la interfaz de usuario. Estos diferentes grupos de usuarios tienen dificultades para identificar el mismo elemento de la interfaz de usuario si el texto del pie de ilustración difiere de la información del objeto o del texto personalizado de Reader en pantalla.
* Para los controles de casillas de verificación y listas desplegables de las celdas de la tabla, el lector de pantalla anunciará el título, la información del objeto o el texto personalizado del lector de pantalla que especifique para el objeto. Si desea utilizar el encabezado de columna para el texto alternativo de estos objetos cuando se colocan en una tabla, no proporcione ningún pie de ilustración, información del objeto ni texto personalizado del lector de pantalla.
* Si el control requiere instrucciones adicionales, asegúrese de que también se incluyan en la alternativa text. Incluya suficiente información verbal para que los usuarios sepan qué entrada se espera y cómo completar el campo correctamente, pero no sobrecargue a los usuarios con información redundante.
* No proporcione información innecesaria que describa cómo utilizar los controles: permita que las tecnologías de asistencia del usuario lo gestionen. Los usuarios pueden configurar el nivel de detalle para adaptarlo a sus niveles de comodidad.

La Figura 4 muestra un ejemplo de un campo de texto con un pie de ilustración visual que puede no ser claro para algunos usuarios del lector de pantalla. En este ejemplo, Texto personalizado de Reader en pantalla se establece en &quot;Número de páginas&quot; y la Prioridad de Reader en pantalla se establece en Texto personalizado. Como resultado, el lector de pantalla no utilizará el texto real (visual) del pie de ilustración (&quot;# of pages&quot;). Como alternativa, se podría haber especificado la información del objeto.

![Especificación de texto de Reader en pantalla personalizado cuando la etiqueta visible no es adecuada](/help/forms/using/assets/image-4.png)

Figura 4: **Especificación de texto personalizado de Reader en pantalla cuando la etiqueta visible no es adecuada**

### Etiquetado de botones de opción

Cuando un usuario con deficiencias visuales presiona un botón de opción, el lector de pantalla debe leer dos cosas:
* Una indicación del propósito del grupo de botones de opción
* Una etiqueta significativa para cada botón de opción
Para que los botones de opción sean accesibles mediante los títulos de los botones:
   1. En la paleta Jerarquía, seleccione el grupo de exclusión.
   1. Haga clic en la paleta Accesibilidad y, en el cuadro Texto personalizado de Reader de pantalla, escriba el texto que se leerá para el grupo. Por ejemplo, para un grupo de exclusión que indique las opciones de pago de varias tarjetas de crédito, escriba Seleccionar un método de pago.
   1. Si los subtítulos de cada botón de opción proporcionan texto que tendrá sentido cuando lo lea un lector de pantalla, en la paleta Objeto, seleccione la pestaña Enlace y anule la selección de Especificar valor de elemento.

  Para que los botones de opción sean accesibles mediante un valor de elemento especificado:
   1. En la paleta Jerarquía, seleccione el grupo de exclusión.
   1. Haga clic en la paleta Accesibilidad y, en el cuadro Texto personalizado de Reader de pantalla, escriba el texto que se leerá para el grupo. Por ejemplo, para un grupo de exclusión que indique las opciones de pago de varias tarjetas de crédito, escriba Seleccionar un método de pago.
   1. En la paleta Jerarquía, seleccione el primer botón de opción del grupo.
   1. En la paleta Objeto, haga clic en la pestaña Campo. En el área Elemento, haga doble clic en el elemento y escriba un valor significativo para el botón de opción seleccionado. Por ejemplo, para el primer botón de un grupo de métodos de pago, puede escribir Efectivo.
   1. Repita los pasos 3 y 4 para cada botón de opción del grupo de exclusión.

### Etiquetado de controles personalizados

Se recomienda encarecidamente utilizar componentes estándar en lugar de componentes personalizados, ya que proporcionarán a la tecnología de asistencia las señales y la información correctas de forma predeterminada. Sin embargo, si se utilizan controles personalizados, tenga en cuenta lo siguiente:
* Anunciar el estado de las casillas de verificación y los botones de opción.
* En los cuadros de lista y listas desplegables, anunciar el elemento predeterminado seleccionado en la lista. Asegúrese de que el usuario sepa que debe utilizar las teclas de flecha arriba y flecha abajo para desplazarse por los elementos de la lista. Tenga en cuenta que al pulsar la tecla Tab o la tecla Intro o Retorno se seleccionará el elemento de la lista. Mediante secuencias de comandos, puede establecer el evento Change del objeto para anunciar qué elemento se selecciona de la lista.
* Anuncie a los usuarios cualquier pulsación de tecla especial que necesiten para realizar una función, por ejemplo, presionando la barra espaciadora para seleccionar un botón o la tecla de flecha abajo para seleccionar un elemento de un cuadro de lista.

### Colocar correctamente el título de un control

La colocación de un título es importante porque los usuarios esperarán que se encuentren junto al control. Para los usuarios con ampliación de pantalla, esto es aún más importante, ya que es posible que no puedan ver el control y el pie de ilustración al mismo tiempo si están demasiado separados.

Al crear un objeto, LiveCycle Designer coloca automáticamente el título según lo especificado por el tipo de objeto. Los títulos de los botones de opción, por ejemplo, se colocan a la derecha. Esta ubicación predeterminada siempre es la mejor ubicación para un pie de ilustración accesible. Si debe cambiar la posición del texto de rótulo, siga estos pasos:
1. Seleccione el objeto moviendo el enfoque hacia él.
1. En la paleta Diseño, seleccione la posición del pie de ilustración del objeto en la opción Posición de la sección Pie de ilustración, en la parte inferior de la paleta.

El ejemplo de la Figura 5 muestra un cuadro de texto con un pie de ilustración encima. La Posición de la paleta Diseño se establece en Superior. La ubicación predeterminada del título es a la izquierda del cuadro de texto.

![Cambiando la posición del título mediante la paleta Diseño](/help/forms/using/assets/image-5.png)

Figura 5: **Cambio de la posición del título mediante la paleta Diseño**

En la tabla siguiente se proporciona información general sobre las reglas de colocación de etiquetas para los controles más utilizados.

| Tipo de control | Reglas de colocación |
|--------------|-----------------|
| Entrada de texto (incluidos los campos de fecha, hora y contraseña) | Coloque el título a la izquierda del control (valor predeterminado). Si esto no es posible, colóquelo inmediatamente encima o debajo de él. Las etiquetas deben colocarse cerca del control para los usuarios con mayor ampliación, de modo que sea más probable que la etiqueta y el control se vean juntos en la vista ampliada. |
| Casilla de verificación | Coloque el pie de ilustración a la derecha de la casilla de verificación (valor predeterminado). Para los controles de casilla de verificación de las celdas de la tabla, el lector de pantalla anunciará el pie de ilustración, la información del objeto o el texto personalizado del lector de pantalla que especifique para el objeto. Si desea utilizar el encabezado de columna como texto alternativo para una casilla de verificación en una tabla, no proporcione ningún pie de ilustración, información del objeto ni texto personalizado del lector de pantalla. |
| Grupo de botones de opción | Cree un título visible para el grupo de botones de opción creando un elemento de texto estático y colocándolo a la izquierda o encima del grupo. Para cada botón de opción individual, coloque la etiqueta a la derecha (valor predeterminado). |
| Lista desplegable | Coloque el pie de ilustración a la izquierda del objeto (valor predeterminado). Si esto no es posible, colóquelo inmediatamente encima. Para los controles de lista desplegable de las celdas de la tabla, el lector de pantalla anunciará el pie de ilustración, la información del objeto o el texto personalizado del lector de pantalla que especifique para el objeto. Si desea utilizar el encabezado de columna como texto alternativo para estos objetos en una tabla, no proporcione ningún pie de ilustración, información del objeto ni texto personalizado del lector de pantalla. |
| Cuadro de lista | El pie de ilustración se coloca encima del cuadro de lista de forma predeterminada cuando lo crea. |
| Botón | El pie de ilustración se coloca automáticamente en el botón y no tiene que colocarse manualmente. Asegúrese de que el texto del pie de ilustración describe correctamente el propósito del botón. |


### Rellenar dinámicamente un texto de información del objeto o de pantalla personalizada de Reader

También puede rellenar dinámicamente la alternativa de texto de un control de formulario, como la información sobre herramientas, con un valor de un origen de datos. Por ejemplo, puede mostrar una información de objeto personalizada para un objeto que esté en francés.
El esquema al que se conecte podría tener lo siguiente definido para una información del objeto:


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


El archivo de datos al que apunta podría tener lo siguiente definido para la información del objeto:

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. En la paleta Biblioteca de objetos, haga clic en la categoría Estándar y arrastre un objeto al diseño de formulario. Por ejemplo, inserte un objeto Campo de texto.
1. (Opcional) En la paleta Objeto, haga clic en la ficha Campo y escriba un título para el objeto en el cuadro Título. Por ejemplo, escriba Quantité.
1. En la paleta Accesibilidad, haga clic en la etiqueta activa de información del objeto.
1. Seleccione la conexión de datos.
1. Haga clic en el triángulo situado junto al cuadro Enlace y seleccione un enlace. Por ejemplo, seleccione información del objeto > @dp_tt.

La cadena siguiente aparece en el cuadro Enlace: $record.tooltip.dp_tt Sugerencia: puede escribir esta cadena en el cuadro Elementos en lugar de seleccionarla.
1. Haga clic en Aceptar.
1. Vea el formulario en la pestaña Vista previa de PDF.

### Proporcionar texto del vínculo

Los usuarios de tecnología de asistencia pueden tener diferentes métodos para leer texto vinculado. Por ejemplo, los usuarios de lectores de pantalla suelen utilizar una lista de vínculos como la que se muestra en la Figura 6 para analizar rápidamente los vínculos disponibles en una página.

![Cuadro de diálogo Lista de vínculos de JAWS](/help/forms/using/assets/image-6.png)

Figura 6: **Cuadro de diálogo Lista de vínculos de JAWS**

Por esta razón, los vínculos deben ser autodescriptivos; ese es su significado no debe depender de su contexto (el texto que los rodea). Por ejemplo, las palabras &quot;haga clic aquí&quot; podrían formar el elemento de vínculo real en la frase &quot;haga clic aquí para descargar nuestro formulario de solicitud&quot;. Este vínculo sería difícil de entender cuando se lee a través de una lista de vínculos, especialmente cuando hay varios vínculos que contienen el mismo texto.

Cuando utilice vínculos en el formulario, asegúrese de que cada vínculo describe correctamente su propósito, sin depender del texto o la posición que lo rodea en la página. Por ejemplo, en lugar de utilizar una frase como &quot;Haga clic aquí&quot; como texto del vínculo, utilice &quot;Descargar formulario de solicitud&quot; como texto del vínculo.

**Puntos de comprobación relacionados**

* Sección 508 §1194.21
   * (d) La tecnología de asistencia dispondrá de información suficiente sobre un elemento de interfaz de usuario, incluida la identidad, el funcionamiento y el estado del elemento. Cuando una imagen representa un elemento de programa, la información transmitida por la imagen también debe estar disponible en texto.
   * (l) Cuando se utilicen formularios electrónicos, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.
* Sección 508 §1194.22
   * (n) Cuando los formularios electrónicos estén diseñados para ser cumplimentados en línea, el formulario permitirá a las personas que utilicen tecnología de asistencia acceder a la información, los elementos de campo y la funcionalidad necesarios para cumplimentar y enviar el formulario, incluidas todas las direcciones y señales.
* WCAG 1.0
   * 12.4 Asociar explícitamente las etiquetas con sus controles (P2).
   * 13.1 Identificar claramente el objetivo de cada vínculo (P2).
* WCAG 2.0
   * 1.1.1 Contenido no textual: todo contenido no textual que se presenta al usuario tiene una alternativa textual que cumple el objetivo equivalente, excepto para las situaciones que se enumeran a continuación. (Nivel A)
   * 2.4.6 Encabezados y etiquetas: Los encabezados y las etiquetas describen el tema o el propósito. (Nivel AA)
   * 3.2.4 Identificación coherente: Los componentes que tienen la misma funcionalidad dentro de un conjunto de páginas web se identifican de forma coherente. (Nivel AA)
   * 3.3.2 Etiquetas o instrucciones: se proporcionan etiquetas o instrucciones cuando el contenido requiere la entrada del usuario. (Nivel A)
   * 4.1.2 Nombre, Función, Valor: Para todos los componentes de la interfaz de usuario (incluidos, entre otros, elementos de formulario, vínculos y componentes generados por secuencias de comandos), el nombre y la función se pueden determinar mediante programación; los estados, las propiedades y los valores que el usuario puede definir se pueden definir mediante programación; y la notificación de los cambios en estos elementos está disponible para los agentes de usuario, incluidas las tecnologías de asistencia. (Nivel A)


## Asegúrese de que la lectura y el orden de tabulación sean correctos {#ensure-reading-tab-order}

Garantizar un orden de lectura significativo es muy importante a la hora de diseñar formularios accesibles para los usuarios con deficiencias visuales u otras discapacidades. Estos usuarios no suelen utilizar el ratón para desplazarse por un formulario, por lo que dependen del teclado. El orden de lectura determina la secuencia que utilizan los usuarios del lector de pantalla cuando leen el formulario. Además, el orden de tabulación permite a los usuarios pasar rápidamente de un control de formulario interactivo al siguiente mediante las teclas Tab o Mayús+Tab. Un orden de tabulación lógico garantiza que tengan acceso a todos los campos del formulario y que puedan desplazarse por el formulario de una manera sensata y eficaz.

El orden de lectura del formulario incluye todos los objetos estáticos (como texto e imágenes) y objetos de campo, pero solo los controles interactivos del formulario forman parte del orden de tabulación.

>[!NOTE]
> En muchos casos, el orden de tabulación está estrechamente relacionado con el orden de lectura. Para simplificar, en esta guía se utiliza el término &quot;orden de tabulación&quot; en lugar de &quot;orden de tabulación o lectura&quot;.

### El orden de tabulación predeterminado en los formularios de LiveCycle Designer

El orden de tabulación predeterminado se crea automáticamente al guardar el formulario como PDF etiquetado. Inicialmente, el orden de tabulación de un formulario se determina a partir de la posición local de los objetos mediante las siguientes reglas:

* Todos los objetos se ordenan de izquierda a derecha y de arriba a abajo (orden local), empezando por la esquina superior izquierda del formulario.
* Todos los subformularios que cree se tratarán como unidades independientes y se desplazará de izquierda a derecha y de arriba a abajo. Si hay dos subformularios colocados uno junto al otro que contienen objetos, el orden de lectura se desplaza por todos los objetos del primer subformulario antes de pasar al siguiente.

Para los formularios simples (es decir, formularios con un diseño de izquierda a derecha, de arriba a abajo), el orden de tabulación predeterminado suele ser correcto. Para comprobarlo, debe examinar el orden de tabulación predeterminado antes de publicar el formulario. Puede hacer visible el orden de tabulación con cualquiera de los siguientes métodos:

* Seleccione Ver > Mostrar orden de tabulación.
* Haga clic en Mostrar orden en la paleta Orden de tabulación.

Todos los objetos se mostrarán con un número en la esquina superior derecha, que indica el lugar del objeto en el orden de tabulación predeterminado. Los objetos interactivos de esta secuencia forman el orden de tabulación. La figura 7 muestra la visualización del orden de lectura de un formulario básico.

![Visualización del orden de lectura predeterminado para un formulario de pedido típico](/help/forms/using/assets/image-7.png)

Figura 7: **Visualización del orden de lectura predeterminado para un formulario de pedido típico**

Cada número de orden de tabulación se muestra en una forma de color. Las formas tienen el siguiente significado:
* Los círculos grises (#1 y #4) se utilizan para los objetos del área de contenido.
* Los círculos verdes (#6 y #7) se utilizan para los objetos de la página maestra.
* Los cuadrados de lavanda (#2 y #3) se utilizan para objetos dentro de un fragmento.

Puede elegir mostrar únicamente los controles de formulario interactivos (que conforman el orden de tabulación) o todos los objetos en el orden de lectura (que también incluye objetos estáticos como texto e imágenes). Para cambiar esta preferencia, elija Herramientas > Opciones > Orden de tabulación y seleccione Mostrar sólo orden de tabulación para los campos.

En un formulario complejo, puede resultar difícil ver cómo fluye la tabulación de un objeto al siguiente. Puede utilizar ayudas visuales para ver el flujo de tabulación en el formulario. Con las ayudas visuales activadas, cuando pasa el puntero sobre el objeto, las flechas azules muestran el flujo de tabulación para los dos objetos anteriores y dos siguientes en el orden de tabulación (consulte la Figura 8).

![Las ayudas visuales resaltan el orden de tabulación](/help/forms/using/assets/image-8.png)

Figura 8: **Las ayudas visuales resaltan el orden de tabulación**

Para habilitar las ayudas visuales, utilice los métodos siguientes:
* Elija Herramientas > Opciones > Orden de tabulación y, en el panel Orden de tabulación, seleccione Mostrar ayudas visuales adicionales para el orden de tabulación.
* En el menú de la paleta Orden de tabulación, seleccione Mostrar ayudas visuales.

### Utilizar la posición para influir en el orden de tabulación predeterminado

Para influir en el orden de tabulación predeterminado, puede cambiar las coordenadas de un objeto moviéndolo a una ubicación diferente. Por ejemplo, en la Figura 9, el campo Product Name aparece en el orden de tabulación antes del campo Quantity. Para cambiar este pedido, puede mover el campo Nombre del producto para que se coloque debajo o a la derecha del campo Cantidad.

![El orden de tabulación predeterminado es de izquierda a derecha](/help/forms/using/assets/image-9.png)

Figura 9: **El orden de tabulación predeterminado es de izquierda a derecha**

Para cambiar la posición de un objeto, siga uno de estos procedimientos:
* Arrástrela con el ratón
* Selecciónelo y muévalo utilizando las teclas de flecha del teclado.

>[!NOTE]
> Puede resultar útil mantener la alineación de los objetos seleccionando Ver > Ajustar a cuadrícula.

Puede cambiar las coordenadas de un objeto con mayor precisión mediante la paleta Diseño (se muestra en la Figura 10). Esta paleta le permite especificar las coordenadas X e Y, así como la anchura y altura del objeto.

![Utilizando coordenadas para colocar con precisión un objeto con la paleta Diseño](/help/forms/using/assets/image-10.png)

Figura 10: **Uso de coordenadas para colocar con precisión un objeto con la paleta Diseño**

>[!NOTE]
> Cuando no se combinan el título y el control, la posición del título de un control de formulario es independiente del orden en que los lectores de pantalla leen el objeto y sus elementos. Para obtener más información sobre los subtítulos, consulte la sección 2.5 Proporcionar las etiquetas adecuadas para los controles del formulario en esta guía.

### Usar subformularios para influir en el orden de tabulación predeterminado

Como se ha mencionado anteriormente, los subformularios permiten insertar grupos de objetos que tienen su propio orden de tabulación. Puede crear un subformulario mediante uno de los procedimientos siguientes:
* Elija Insertar > Estándar > Subformulario.
* Seleccione los objetos en la paleta Jerarquía y agrúpelos en un subformulario seleccionando Insertar > Ajustar en subformulario.
* Seleccione los objetos en el formulario real, haga clic con el botón derecho en la selección y elija Ajustar en subformulario

Cuando dos subformularios que contienen objetos de campo se colocan en paralelo, la secuencia de tabulación recorrerá los campos del primer subformulario antes de pasar al siguiente. Esto se muestra en la figura 11, donde se utilizan dos subformularios para crear un orden de tabulación predeterminado basado en columnas.

![Orden de tabulación predeterminado al usar subformularios](/help/forms/using/assets/image-11.png)

Figura 11: **Orden de tabulación predeterminado al usar subformularios**

Los subformularios, los botones de opción y las áreas de contenido, junto con la posición vertical de los objetos en una página y su página maestra, afectan al orden de tabulación.

### Creación de un orden de tabulación personalizado mediante la paleta Orden de tabulación

Puede cambiar el orden de tabulación predeterminado cuando necesite una secuencia diferente en el formulario y el cambio no se pueda lograr colocando o agrupando los subformularios. Para cambiar el orden de tabulación predeterminado, puede crear un orden de tabulación personalizado con la paleta Orden de tabulación.
La paleta Orden de tabulación (consulte la Figura 12) le permite inspeccionar y modificar el orden en que la tecnología de asistencia lee los objetos del formulario y se desplazan mediante la tecla de tabulación del usuario.

![La paleta Orden de tabulación](/help/forms/using/assets/image-12.png)

Figura 12: **La paleta Orden de tabulación**

La paleta Orden de tabulación proporciona una vista alternativa del orden de tabulación del formulario. Muestra todos los objetos del formulario en una lista numerada, donde cada número representa la posición del objeto en el flujo de tabulación.
Para abrir la paleta Orden de tabulación, seleccione Ventana > Orden de tabulación.


La paleta Orden de tabulación proporciona los siguientes marcadores visuales:
* Una barra gris marca cada página del formulario. El orden de tabulación de cada página comienza con el número 1.
* La letra M dentro de un círculo verde indica los objetos de la página maestra (visible sólo cuando se ve el formulario en la ficha Vista Diseño).
* Un rango de números indica objetos dentro de un fragmento.
* El fondo amarillo indica el elemento seleccionado actualmente.
* Un icono de candado junto al primer objeto de la página indica que el objeto no se puede mover dentro del orden de tabulación (visible sólo cuando se ve el formulario en la ficha Páginas maestras).

La lista muestra los mismos números de orden de tabulación que los números mostrados en el propio formulario al elegir Ver > Mostrar orden de tabulación. Para cambiar la posición de un objeto en el orden de tabulación, mueva el objeto hacia arriba o hacia abajo en la lista de la paleta Orden de tabulación. Puede mover un solo objeto o un grupo de objetos. Esto se puede lograr mediante uno de los siguientes métodos:

* Arrastre el objeto seleccionado hacia arriba o hacia abajo en la lista y colóquelo en la ubicación deseada. Un controlador negro marca la posición actual en la lista antes de colocar el objeto.
* En la paleta Orden de tabulación, haga clic en los botones de flecha arriba o abajo hasta que el objeto seleccionado se coloque en la posición correcta. También puede pulsar Ctrl+Flecha arriba o Ctrl+Flecha abajo.
* En el menú de la paleta Orden de tabulación, seleccione Subir o Bajar.
* En la lista Orden de tabulación, haga clic en el objeto seleccionado (o selecciónelo y presione F2) para que el número que aparece junto al nombre del objeto sea editable. A continuación, escriba el número que indica la nueva posición del objeto en el orden de tabulación y presione Entrar.
* Seleccione Copiar en el menú de la paleta Orden de tabulación y, en la lista, seleccione el objeto sobre el que desea colocar el objeto que está moviendo y, a continuación, seleccione Pegar en el menú.

Cuando se mueve el objeto a un nuevo lugar en el orden, LiveCycle Designer reasigna los números de orden de tabulación. Aunque el orden de tabulación de los objetos ubicados en una página maestra se muestra en la ficha Vista Diseño, sólo se puede cambiar el orden de estos objetos en la ficha Páginas maestras. Si utiliza referencias de fragmento en el formulario, el orden de tabulación dentro de un fragmento es visible al ver el orden del formulario. Para cambiar el orden de tabulación dentro de un fragmento, debe abrir el archivo de origen del fragmento para editarlo, realizar el cambio y guardar el archivo. Cualquier formulario que utilice este fragmento se verá afectado por este cambio.

Si decide que no desea el orden de tabulación personalizado en el formulario, puede volver rápidamente al orden de tabulación automático (predeterminado) siguiendo estos pasos (perderá los cambios realizados en el orden de tabulación):
1. En la paleta Orden de tabulación, seleccione Automático.
1. En el cuadro de mensaje que aparece, haga clic en Sí para confirmar la eliminación del orden de tabulación personalizado.

**Puntos de comprobación relacionados**
* Sección 508 §1194.21
   * (a) Cuando el software esté diseñado para ejecutarse en un sistema que tenga un teclado, las funciones de producto deberán ser ejecutables desde un teclado en el que la función en sí o el resultado de realizar una función puedan discernirse textualmente.
* WCAG 1.0
   * 9.2 Garantizar que cualquier elemento que tenga su propia interfaz pueda funcionar de manera independiente del dispositivo.
* WCAG 2.0
   * 1.3.2 Secuencia significativa: Cuando la secuencia en la que se presenta el contenido afecta su significado, se puede determinar una secuencia de lectura correcta mediante programación. (Nivel A)
   * 2.1.1 Teclado: Toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para pulsaciones de teclas individuales, excepto cuando la función subyacente requiera una entrada que dependa de la ruta del movimiento del usuario y no solo de los extremos. (Nivel A)
   * 2.1.3 Teclado (sin excepción): toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para pulsaciones de teclas individuales. (Nivel AAA)
   * 2.4.3 Orden de enfoque: Si una página web se puede navegar secuencialmente y las secuencias de navegación afectan al significado o al funcionamiento, los componentes enfocables reciben atención en un orden que preserva el significado y la operabilidad. (Nivel A)


## Asegúrese de que los controles del formulario sean accesibles mediante teclado{#ensure-keyboard-accessible}

Los usuarios deben poder rellenar el formulario por completo utilizando solo el teclado o un dispositivo de entrada alternativo equivalente. Es posible que los usuarios con movilidad reducida o problemas de visión no tengan otra opción que utilizar el teclado, y muchos usuarios que pueden utilizar un ratón simplemente prefieren utilizar el teclado. Al permitir varios métodos de entrada, no solo se crean formularios accesibles, sino que también se crean formularios que se adaptan mejor a las preferencias de todos los usuarios.

En LiveCycle Designer, la forma más sencilla de asegurarse de que los controles son accesibles mediante el teclado es utilizar los controles que aparecen en la ficha Común de la paleta Biblioteca de objetos. Estos controles responden a la entrada del ratón y del teclado de forma predeterminada. Para obtener más información, consulte la sección 2.3 Elija los controles adecuados en esta guía.

Otro aspecto importante de la accesibilidad del teclado es garantizar que cada elemento interactivo forme parte del orden de tabulación del formulario. Esto permite al usuario mover el cursor hacia adelante y hacia atrás por el formulario con las teclas Tab y Mayús+Tab. Asegúrese de establecer un orden de tabulación lógico que incluya todos los campos y botones. Para obtener más información, consulte la sección 2.6. Asegúrese de que la lectura y el orden de las pestañas sean correctos en esta guía.

Por último, es importante asegurarse de que el comportamiento generado por scripts también sea accesible mediante el teclado y no dependa de eventos específicos del dispositivo. El evento MouseEnter de mouse, por ejemplo, no se puede ejecutar mediante el teclado. Además, estos controladores de eventos no deben interferir con la accesibilidad del teclado. Por ejemplo, asegúrese de que los eventos Change utilizados en listas desplegables o cuadros de lista no almacenan en déclencheur las acciones inesperadas.

**Puntos de comprobación relacionados**
* Sección 508 §1194.21
   * (a) Cuando el software esté diseñado para ejecutarse en un sistema que tenga un teclado, las funciones de producto deberán ser ejecutables desde un teclado en el que la función en sí o el resultado de realizar una función puedan discernirse textualmente.
* WCAG 1.0
   * 6.4 Para scripts y applets, asegúrese de que los controladores de eventos son independientes del dispositivo de entrada (P2).
   * 9.2 Garantizar que cualquier elemento que tenga su propia interfaz pueda funcionar de manera independiente del dispositivo (P2).
   * 9.3 Para los scripts, especifique controladores de eventos lógicos en lugar de controladores de eventos dependientes del dispositivo (P2).
* WCAG 2.0
   * 2.1.1 Teclado: Toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para pulsaciones de teclas individuales, excepto cuando la función subyacente requiera una entrada que dependa de la ruta del movimiento del usuario y no solo de los extremos. (Nivel A)
   * 2.1.2 Sin trampas para el foco del teclado: si es posible mover el foco a un componente de la página mediante una interfaz de teclado, entonces el foco se puede mover de ese componente usando solo una interfaz de teclado y, si se requiere algo más que las teclas de dirección o de tabulación sin modificar u otros métodos de salida estándar, se informa al usuario del método para mover el foco. (Nivel A)
   * 2.1.3 Teclado (sin excepción): toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para pulsaciones de teclas individuales. (Nivel AAA)


## Usar el color de forma responsable{#use-color-responsibly}

El diseño de formularios para la accesibilidad implica considerar algunas directrices adicionales para utilizar el color. Los diseñadores utilizan colores para mejorar el aspecto de los formularios, resaltando los distintos componentes del formulario. Sin embargo, el uso inadecuado del color puede hacer que la información en su forma sea difícil o imposible de leer para las personas con discapacidades.

### No transmitir información utilizando solo el color

Los colores pueden resaltar y mejorar ciertas partes del formulario, pero no debe transmitir la información únicamente por el color.

Cualquier información que se transmita únicamente en color (colores con significado semántico) no es accesible para los usuarios ciegos. Lo mismo se aplica a los usuarios con deficiencias de visión del color, o a los usuarios que utilizan esquemas de color diferentes, como una pantalla de color de alto contraste con texto blanco o en primer plano sobre un fondo negro. También debe tener en cuenta que los lectores de pantalla no pueden detectar la información de color automáticamente.

Por ejemplo, la Figura 13 muestra un campo de formulario que tiene un pie de ilustración rojo (especificado con la paleta Fuente) para indicar que el campo de formulario es obligatorio. En este ejemplo, el color es el único indicador de la diferencia entre los campos de entrada obligatorios y los opcionales, lo que hace imposible que los usuarios ciegos o los usuarios con ciertos tipos de daltonismo los diferencien.

![Usar solo el color para transmitir información](/help/forms/using/assets/image-13.png)

Figura 13: **Uso del color solo para transmitir información**

Para resolver este problema, indique también el estado requerido del formulario en el texto alternativo del control del formulario (como se describe en la sección 2.5 Proporcionar las etiquetas adecuadas para los controles del formulario). Por ejemplo, puede configurar el texto del lector de pantalla en &quot;Código postal (obligatorio)&quot;. Para los usuarios que tienen dificultades para ver el color en determinadas combinaciones, se recomienda establecer el tipo de campo de texto en Usuario introducido: obligatorio en la paleta Objeto, además de texto alternativo que indica que el campo es obligatorio. Como alternativa, puede utilizar indicaciones distintas del color, como texto visual, estilos de texto y estilos de borde. Sin embargo, para los usuarios del lector de pantalla, seguirá teniendo que transmitir la información necesaria mediante la paleta Accesibilidad.

Además, cuando proporcione descripciones o instrucciones al usuario del formulario, tenga en cuenta que las instrucciones basadas en el color por sí solas no son suficientes para los usuarios con un deterioro visual. Por ejemplo, en lugar de una instrucción como &quot;Haga clic en el botón verde para continuar&quot;, use una descripción de texto para acciones como &quot;Haga clic en el botón Siguiente para continuar&quot;.

>[!NOTE]
> Esta práctica recomendada no prohíbe el uso del color. Prohíbe el uso del color como único medio para transmitir información importante. Si se desea una indicación visual para este tipo de información, el diseñador podría utilizar un asterisco o un indicador visual similar para marcar los campos obligatorios.

### Proporcionar suficiente contraste de color

Muchos usuarios con deficiencias visuales dependen del alto contraste entre el texto y el fondo para leer los formularios. Cuando el contraste entre los colores del fondo y el primer plano no es suficiente, la lectura de un formulario puede resultar difícil, si no imposible, para algunos usuarios. La figura 14 muestra un ejemplo de un formulario con contraste insuficiente.

![Formulario con contraste de color insuficiente](/help/forms/using/assets/image-14.png)

Figura 14: **Un formulario con contraste de color insuficiente**

Se recomienda encarecidamente utilizar la fuente y los colores de fondo predeterminados: negro sobre fondo blanco. Si debe cambiar estos colores predeterminados, asegúrese de elegir una combinación adecuada de colores de alto contraste; utilice un color de primer plano oscuro en un color de fondo claro o viceversa. Para estar seguros, utilice una herramienta (como el Analizador de contraste de color WAT-C) para verificar que el contraste sea suficiente.

Adobe Reader y Adobe Acrobat permiten a los usuarios especificar si se deben reemplazar los colores para satisfacer sus necesidades visuales. Los usuarios pueden especificar su propio esquema de contraste o pueden optar por utilizar uno proporcionado por el sistema operativo. Además, Adobe Reader y Adobe Acrobat tienen su propio esquema de alto contraste que se puede activar. Para que estas opciones tengan éxito, el mejor enfoque es utilizar siempre colores predeterminados.

Al diseñar el formulario, pruébelo con frecuencia con una configuración de combinación de colores similar a la que muchos usuarios con deficiencias visuales utilizarán para completarlo. Esta práctica le ayuda a descubrir y corregir problemas al principio del proceso de diseño.

Recomendaciones para el uso de colores:
* Asegúrese de que no se pierde información si el color semántico no es visible.
* Si no puede utilizar colores predeterminados, asegúrese de que los colores tengan un alto contraste, como el negro sobre un fondo claro (blanco). Los usuarios con visión parcial generalmente requieren un alto contraste entre el texto y su fondo para poder leerlo.
* Pruebe la legibilidad de los formularios cambiando la pantalla a una pantalla de alto contraste, tanto en Windows como en Adobe Reader o Adobe Acrobat. Mac OSX solo ofrece un filtro simple en escala de grises para un alto contraste, por lo que no es suficiente para realizar pruebas.
* No transmita información basada únicamente en el color. Por ejemplo, no utilice solo el color para resaltar fragmentos importantes de texto. Utilice también otros métodos de resaltado y descripciones de texto.
* No utilice demasiados colores, ya que esto puede dificultar la lectura de la información real del contenido. Mantenga siempre la legibilidad de la información como su principal prioridad cuando decida qué colores utilizar.

**Puntos de comprobación relacionados**
* Sección 508 §1194.21
   * (i) El código de colores no se utilizará como único medio para transmitir información, indicar una acción, provocar una respuesta o distinguir un elemento visual.
* WCAG 1.0
   * 2.1 Asegúrese de que toda la información transmitida con el color también esté disponible sin color, por ejemplo, desde el contexto o el marcado.
   * 2.2 Asegúrese de que las combinaciones de colores de primer plano y de fondo ofrezcan suficiente contraste cuando las vea alguien con deficiencias de color o cuando las vea en una pantalla en blanco y negro. [Prioridad 2 para imágenes, Prioridad 3 para texto] (P2).
* WCAG 2.0
   * 1.4.1 Uso del color: el color no se utiliza como el único medio visual para transmitir información, indicar una acción, pedir una respuesta o distinguir un elemento visual. (Nivel A)
   * 1.4.3 Contraste (mínimo): La presentación visual de texto e imágenes de texto tiene una relación de contraste de al menos 4.5:1, excepto para lo siguiente: (Nivel AA)
   * 1.4.6 Contraste (mejorado): La presentación visual de texto e imágenes de texto tiene una relación de contraste de al menos 7:1, excepto para lo siguiente: (Nivel AAA)


## Proporcionar celdas de encabezado para las tablas{#provide-heading-cells}

Las tablas son una forma eficaz de organizar y presentar el contenido en formularios accesibles. Cuando se utilizan correctamente, las filas y columnas de una tabla proporcionan una estructura predecible y coherente para el contenido del formulario. Por ejemplo, cuando un usuario de lector de pantalla navega a una celda de fila del cuerpo, el lector de pantalla especifica la ubicación de la celda y, a continuación, lee el contenido de la celda. El lector de pantalla especifica la ubicación de la celda mediante una combinación de encabezados de fila y columna o números de fila y columna. Dado que los lectores de pantalla proporcionan información que orienta al usuario hacia la ubicación del contenido en la tabla, su diseño afecta directamente a la accesibilidad de la tabla.

Puede especificar las siguientes funciones para los elementos de tabla a medida que construye tablas. Estas funciones permiten a los lectores de pantalla navegar por la estructura de la tabla utilizando métodos abreviados especiales y transmiten al usuario la relación entre las celdas de la tabla y las celdas de encabezado correspondientes.
* Tabla
Asigna la función de una tabla al subformulario seleccionado. Cuando el usuario navega a este subformulario, la mayoría de los lectores de pantalla lo identifican como una tabla e indican el número de filas y columnas.
* Fila de encabezado
Asigna la función de una fila de encabezado al subformulario o fila de tabla seleccionados. Al hablar del contenido de una celda de fila del cuerpo, la mayoría de los lectores de pantalla identifican primero el contenido de la celda correspondiente en la fila de encabezado.
* Fila del cuerpo
Asigna la función de una fila de cuerpo al subformulario o fila de tabla seleccionados. Si una celda contiene un subformulario, los lectores de pantalla suelen mencionar el contenido de la celda correspondiente en la fila de encabezado, seguido de los campos del subformulario.
* Fila de pie
Asigna la función de una fila de pie de página al subformulario o fila de tabla seleccionados.
* (Ninguno)
Especifica una fila que transmite información sobre la tabla o su contenido. La fila no se considera parte de la tabla; sin embargo, el lector de pantalla leerá su contenido.

Cuando se utilizan correctamente, las tablas son una forma eficaz de organizar y presentar la información tabular. Evite las tablas demasiado complejas, como las que tienen tablas y secciones anidadas.

### Hacer accesibles las tablas simples

Se recomiendan tablas con diseños simples. Las tablas simples comienzan con una sola fila de encabezado seguida de las filas del cuerpo.

Al diseñar tablas sencillas para la accesibilidad, tenga en cuenta las siguientes directrices:

* El orden de tabulación de una tabla es el orden geográfico, que es el mismo que para el propio formulario. Asegúrese de que el contenido de la tabla esté organizado de modo que tenga sentido cuando se lea de izquierda a derecha y de arriba a abajo.
* La mayoría de los lectores de pantalla interpretan la primera fila de una tabla como la fila de encabezado. Al leer el contenido de una celda de fila de cuerpo, estos lectores de pantalla leen primero el contenido de la celda de fila de encabezado asociada. Asegúrese de que el contenido de cada celda de fila de encabezado describe de forma significativa el contenido de la columna.
* Evite celdas que abarquen dos o más columnas, tablas anidadas o secciones de tabla. Algunos lectores de pantalla tienen dificultades para interpretar correctamente estas funciones o es posible que no las utilicen. Por ejemplo, si una celda de una fila del cuerpo abarca dos columnas, es posible que los lectores de pantalla no hagan referencia al contenido de celda correcto en la fila de encabezado al leer la siguiente celda de la fila.

### Hacer accesibles las tablas complejas

Al diseñar tablas para fines de accesibilidad, procure que el diseño de la tabla sea sencillo, con una fila de encabezado seguida de filas de cuerpo. Por supuesto, algunos contenidos pueden requerir un diseño de tabla más complejo. Por ejemplo, es posible que necesite utilizar el intervalo de celdas o más de un encabezado para transmitir de forma eficaz el contenido.

Puede crear tablas complejas utilizando el objeto de tabla o combinando objetos de subformulario. El objeto table permite utilizar funciones que ayudan al proceso de diseño, como opciones para insertar y cambiar el tamaño de columnas y filas.

Con la paleta Accesibilidad, puede especificar funciones relacionadas con tablas de subformularios para crear una tabla compleja accesible. Según la experiencia de diseño y las preferencias, puede elegir crear tablas complejas combinando objetos de subformulario. Por ejemplo, puede crear un subformulario que incluya dos filas y especificar este subformulario como encabezado para la tabla y especificar otro subformulario para las filas del cuerpo de la tabla.

Cuando se utilizan objetos de subformulario en lugar de objetos de tabla para crear tablas, se requieren los siguientes pasos adicionales:
* En la pestaña Subformulario, establezca el tipo de cada subformulario en Colocado.
* En la paleta Accesibilidad, defina la función de subformulario adecuada para cada subformulario que forme la tabla. Por ejemplo, asigne la función Fila de encabezado al subformulario que se utiliza como encabezado de tabla.
* En el caso de las filas que transmiten información sobre la tabla o su contenido pero que no se consideran parte de la tabla, asigne la función de subformulario Ninguno. El lector de pantalla leerá el contenido de la fila.

Las funciones que admite el lector de pantalla determinan la información leída para una tabla compleja. Por ejemplo, considere una tabla que incluya una fila de encabezado y una sección con una fila de encabezado. Cuando el usuario navega a una celda de fila del cuerpo en la sección de tabla, los lectores de pantalla generalmente leen el siguiente contenido en orden:
* Contenido de la celda adecuada en la fila de encabezado de la tabla
* Contenido de la celda adecuada en la fila de encabezado de la sección
* Contenido de la celda seleccionada
Sin embargo, es posible que algunos lectores de pantalla no lean el contenido de ambas filas de encabezado.

Cree nombres o títulos visibles significativos para las tablas. Puede crear un nombre de tabla como texto estático en Adobe LiveCycle Designer y colocarlo delante de la tabla. Puede agrupar una tabla y su nombre en un subformulario. Los subformularios son especialmente útiles cuando desea combinar objetos asociados en un diseño.

Para los controles de las celdas de la tabla, el lector de pantalla anunciará el título, la información del objeto o el texto personalizado del lector de pantalla que especifique para el objeto. Si desea utilizar el encabezado de columna como texto alternativo para un control de una tabla, no proporcione ningún título, información del objeto ni texto personalizado del lector de pantalla. Sin embargo, tenga en cuenta que esta estrategia no siempre es tan clara para los usuarios del lector de pantalla, ya que los lectores de pantalla solo pueden asociar el encabezado de columna con el control cuando el usuario no está en el modo de interacción de formulario del lector de pantalla.

**Puntos de comprobación relacionados**
* Sección 508 §1194.22
   * (g) Los encabezados de fila y columna se identificarán para los cuadros de datos.
   * (h) El marcado se utilizará para asociar celdas de datos y celdas de encabezado para tablas de datos que tengan dos o más niveles lógicos de encabezados de fila o columna.
* WCAG 1.0
   * 5.1 Para las tablas de datos, identifique los encabezados de fila y columna (P1).
   * 5.2 Para las tablas de datos que tienen dos o más niveles lógicos de encabezados de fila o columna, utilice el marcado para asociar celdas de datos y celdas de encabezado (P1)
* WCAG 2.0
   * 1.3.1 Información y relaciones: la información, la estructura y las relaciones transmitidas a través de la presentación pueden determinarse mediante programación o están disponibles en texto. (Nivel A)


## Proporcionar una estructura de formulario navegable{#provide-navigable-form}

Cuando un formulario se vuelve largo y complejo, su facilidad de uso se verá muy influida por la forma en que está estructurado. Así como un libro se vuelve más fácil de entender cuando se divide en capítulos y secciones, un formulario se vuelve más fácil de usar cuando se divide en encabezados y subencabezados. Esta partición es especialmente útil para los usuarios de lectores de pantalla por las siguientes razones:
* Cada encabezado indica al usuario del lector de pantalla qué se puede esperar en la sección que sigue al encabezado.
* Los lectores de pantalla proporcionan métodos abreviados para saltar rápidamente de un lado a otro entre los diferentes encabezados del formulario y también permiten al usuario acceder a una lista de encabezados, lo que proporciona una visión general de la estructura del documento y permite una navegación rápida.

Proporcionar mecanismos que permitan a los usuarios saltar a otras áreas del formulario puede hacer que el formulario sea más cómodo. Puede agregar una estructura de encabezado al formulario mediante la paleta Accesibilidad de LiveCycle Designer.

### Proporcionar mecanismos de omisión

Los usuarios con visión pueden analizar una página en cualquier orden. Pueden comenzar mirando la esquina inferior derecha de la página y escanear hacia atrás a través del contenido. El usuario del lector de pantalla no tiene esta opción porque el lector de pantalla empezará a leer la página en la esquina superior izquierda (como se muestra en el código fuente) y se moverá por la página en orden lineal. Además, el usuario puede escanear la página en busca de enlaces interesantes y activarlos con el ratón. Un usuario lector de pantalla debe desplazarse por la página secuencialmente.

La forma más fácil y eficaz de proporcionar una estructura de formulario navegable es utilizar encabezados estructurales y listas definidas correctamente en el formulario.
También puede proporcionar mecanismos que permitan al usuario saltar a otras áreas del formulario, por ejemplo, agregando botones de navegación al principio y al final del formulario. En la parte superior de un formulario, puede incluir botones como Abrir archivo de datos, Página anterior y Página siguiente. En la parte inferior del formulario puede incluir botones como Guardar datos, Enviar datos por correo electrónico, Ir a la parte superior de la página e Imprimir.

Los campos inteligentes pueden ser una forma eficaz de facilitar el rellenado de algunos formularios. Por ejemplo, un formulario de solicitud de viaje puede tener varias filas y columnas de campos. Si una fila en particular está vacía, al presionar la tecla Tab en el último elemento de esa fila, se puede saltar a la siguiente sección del formulario en lugar de seguir presionando el tabulador en varios campos que permanecerán vacíos.

### Agregar encabezados mediante la paleta Accesibilidad

Puede utilizar la paleta Accesibilidad para asignar funciones a objetos en función de para qué se utiliza el objeto. Estas funciones se pueden aplicar para crear encabezados en diferentes niveles.

![Especificando un rol de encabezado en la paleta Accesibilidad](/help/forms/using/assets/image-15.png)
Figura 15: **Especificación de una función de encabezado en la paleta Accesibilidad**

Siga estos pasos para crear un encabezado en el formulario:

1. Identifique el inicio de cada segmento lógico del formulario mediante etiquetas de texto estático.
1. Para cada etiqueta y seleccione una de las opciones de encabezado como el Rol en la paleta Accesibilidad. Los diferentes niveles de encabezado (de 1 a 6) permiten crear una estructura de encabezado en el formulario. Comience con el nivel 1 y, a continuación, utilice el nivel 2 y así sucesivamente para las subsecciones anidadas.

La mayoría de los lectores de pantalla permiten a los usuarios navegar rápidamente entre elementos de encabezado según su nivel. La figura 16 muestra un formulario que se divide en segmentos más pequeños utilizando encabezados. En este ejemplo, se utiliza la siguiente estructura de encabezado:

* Nivel de encabezado 1: Solicitud de producto
   * Nivel de encabezado 2: detalles del pedido
      * Nivel de encabezado 3: Opciones de envío
* Nivel de encabezado 2: información adicional
   * Nivel de encabezado 3: Detalles personales
   * Nivel de encabezado 3: Dirección

![Estructurar un formulario mediante encabezados](/help/forms/using/assets/image-16.png)

Figura 16: **Estructurar un formulario mediante encabezados**

Estos encabezados son solo elementos de texto estático a los que se les ha dado un tamaño de fuente específico y una función de encabezado con el nivel adecuado.

>[!NOTE]
> Cambiar la apariencia visual de una etiqueta de texto para que parezca un encabezado no hará que los lectores de pantalla lo reconozcan como un encabezado. Debe aplicar una función de encabezado.

Asegúrese siempre de que el orden de los niveles de encabezado sea lógico. Por ejemplo, una subsección de un encabezado de nivel 2 siempre debe ser un encabezado de nivel 3; nunca debe omitir niveles al marcar subsecciones. Los usuarios del lector de pantalla utilizan los diferentes niveles para comprender mejor la estructura del formulario. Por ejemplo, después de encontrar un encabezado de nivel 2, el usuario puede utilizar un acceso directo para buscar encabezados de nivel 3 y determinar si hay alguna subsección. Si omite niveles, el usuario tendrá dificultades para identificar estas subsecciones.

### Marcado de listas

A veces, también puede resultar útil agregar contenido de lista al formulario. Las listas son útiles para agrupar elementos relacionados y permiten a los usuarios del lector de pantalla saber cuántos elementos hay en una lista y desplazarse rápidamente por ella. Marcar correctamente las listas hace que la estructura del formulario sea más clara para los usuarios del lector de pantalla.

En LiveCycle Designer, puede crear listas mediante subformularios con los pasos siguientes:

1. Seleccione un subformulario que contenga el contenido que se marcará como elementos de lista.
1. En la paleta Accesibilidad, seleccione Lista como rol.
1. Seleccione cada subformulario anidado dentro del subformulario Lista y establezca su función en Elemento de lista.

>[!NOTE]
> Una función Elemento de lista sólo se puede asignar a un subformulario contenido en un subformulario que tenga especificada una función Lista. No puede definir una tabla o fila de tabla como una lista o elemento de lista; sin embargo, un elemento de lista puede contener una tabla.

**Puntos de comprobación relacionados**
* Sección 508 §11934.22
   * (o) Se facilitará un método que permita a los usuarios omitir los enlaces de navegación repetitivos.
* WCAG 1.0
   * 3.5 Utilice elementos de encabezado para transmitir la estructura del documento y utilizarlos según la especificación (P2).
   * 3.6 Marcar correctamente las listas y los elementos de la lista. (P2).
   * 12.3 Dividir grandes bloques de información en grupos más manejables donde sea natural y apropiado. (P2).
   * 13.3 Proporcionar información sobre la presentación general de un sitio (por ejemplo, un mapa del sitio o un índice).
   * 13.4 Utilizar los mecanismos de navegación de manera coherente (P2).
* WCAG 2.0
   * 1.3.2 Secuencia significativa: Cuando la secuencia en la que se presenta el contenido afecta su significado, se puede determinar una secuencia de lectura correcta mediante programación. (Nivel A)
   * 2.4.1 Omitir bloques: Existe un mecanismo disponible para evitar bloques de contenido que se repiten en varias páginas web. (Nivel A)
   * 2.4.5 Múltiples maneras: Hay más de una manera de localizar una página web dentro de un conjunto de páginas web, excepto cuando la página web es el resultado de un proceso o un paso en él. (Nivel AA)
   * 2.4.6 Encabezados y etiquetas: Los encabezados y las etiquetas describen el tema o el propósito. (Nivel AA)
   * 2.4.10 Encabezados de sección: Los encabezados de sección se utilizan para organizar el contenido. (Nivel AAA)
   * 3.2.3 Navegación coherente: Los mecanismos de navegación que se repiten en varias páginas web dentro de un conjunto de páginas web se producen en el mismo orden relativo cada vez que se repiten, a menos que el usuario inicie un cambio. (Nivel AA)


## Evitar scripts disruptivos{#avoid-disruptive-scripting}

Como parte del proceso de diseño del formulario, los desarrolladores de formularios pueden utilizar secuencias de comandos para proporcionar una mejor experiencia de usuario. Puede agregar scripts a la mayoría de los campos y objetos de formulario. Por ejemplo, puede crear scripts simples para actualizar dinámicamente los valores de un formulario interactivo en respuesta a los datos introducidos por el usuario.

Al diseñar secuencias de comandos para accesibilidad, tenga en cuenta las siguientes directrices generales:

* Mantenga el contenido del formulario libre de interrupciones visuales. Por ejemplo, evite las funciones que hacen que el contenido parpadee, parpadee o se mueva.
* Asegúrese de que las ventanas emergentes solo aparezcan como resultado de acciones iniciadas por el usuario. Del mismo modo, no permita que el enfoque actual del formulario (la vista actual del usuario) cambie o el contenido se vuelva a mostrar a menos que lo inicie el usuario. Por ejemplo, si el usuario está rellenando campos en la mitad inferior del formulario, no permita que el enfoque cambie a la esquina superior izquierda del formulario a menos que el usuario decida desplazarse a esta ubicación.
* Es posible que los usuarios con discapacidades necesiten más tiempo para proporcionar datos en los campos. No especifique respuestas basadas en el tiempo para campos de entrada.
* Tenga en cuenta que los scripts del lado del cliente pueden interferir con los lectores de pantalla y los teclados si el script cambia el enfoque de la aplicación cliente. Por ejemplo, los eventos change y mouseEnter, cuando se utilizan con listas desplegables o cuadros de lista, pueden provocar acciones inesperadas. Compruebe que los scripts del lado del cliente no presentan problemas para los usuarios del lector de pantalla y los usuarios solo de teclado.
* Los usuarios de tecnología de asistencia a veces necesitan más tiempo para completar las tareas. En cualquier caso en el que una rutina temporizada esté a punto de caducar, muestre un mensaje accesible para permitir una extensión. La tecnología de asistencia puede utilizar los cuadros de alerta creados mediante JavaScript. También se puede implementar una nueva ventana con un mensaje que avise al usuario de un tiempo de espera inminente.

**Puntos de comprobación relacionados**:
* Sección 508 §1194.22
   * (l) Cuando las páginas utilicen lenguajes de secuencias de comandos para mostrar contenido o crear elementos de interfaz, la información proporcionada por la secuencia de comandos se identificará con un texto funcional que pueda ser leído por la tecnología de asistencia.
   * (p) Cuando se requiera una respuesta temporizada, se alertará al usuario y se le dará tiempo suficiente para indicar que se requiere más tiempo.
* WCAG 1.0
   * 1.4 Para cualquier presentación multimedia basada en el tiempo (por ejemplo, una película o animación), sincronice alternativas equivalentes (por ejemplo, subtítulos o descripciones auditivas de la pista visual) con la presentación (P1).
   * 6.2 Asegúrese de que los equivalentes del contenido dinámico se actualicen cuando cambie el contenido dinámico.
   * 6.3 Asegúrese de que las páginas se puedan utilizar cuando los scripts, applets u otros objetos de programación estén desactivados o no sean compatibles. Si no es posible, proporcione información equivalente en una página alternativa accesible.
   * 6.5 Asegúrese de que el contenido dinámico sea accesible o proporcione una presentación o página alternativa (P2).
   * 8.1 Hacer que elementos programáticos como scripts y applets sean accesibles o compatibles con las tecnologías de asistencia [Prioridad 1 si la funcionalidad es importante y no se presenta en ninguna otra parte]; en caso contrario (P2).
   * 9.3 Para los scripts, especifique controladores de eventos lógicos en lugar de controladores de eventos dependientes del dispositivo (P2).
   * 10.1 Hasta que los agentes de usuario permitan a los usuarios desactivar las ventanas generadas, no haga que aparezcan ventanas emergentes u otras ventanas y no cambie la ventana actual sin informar al usuario.
* WCAG 2.0
   * 3.2.1 Enfoque: Cuando cualquier componente recibe enfoque, no se inicia un cambio de contexto. (Nivel A)
   * 3.2.2 Al recibir entradas: Cambiar la configuración de cualquier componente de interfaz de usuario no provoca automáticamente un cambio de contexto a menos que se haya informado al usuario del comportamiento antes de utilizar el componente. (Nivel A)
   * 3.2.5 Cambio en la solicitud: los cambios de contexto solo se inician mediante una solicitud del usuario o hay un mecanismo disponible para desactivarlos. (Nivel AAA)

## Asegúrese de que todo el contenido de audio y vídeo sea accesible{#ensure-audio-video-accessible}

Si los formularios incorporan contenido de audio o vídeo, incluidos clips de audio y vídeo, debe asegurarse de que este contenido sea accesible. Concretamente, asegúrese de que los clips de vídeo incorporados a los formularios contengan subtítulos (a veces denominados subtítulos) para usuarios sordos y con dificultades auditivas, y descripciones de vídeo para usuarios ciegos. Para los archivos de audio que no están sincronizados con el contenido de vídeo, una simple transcripción es suficiente.
Para medios basados en Flash, consulte [vínculo](/help/forms/using/best-practices-for-creating-forms-in-designer.md) para obtener información sobre cómo proporcionar subtítulos.

**Puntos de comprobación relacionados**:
* Sección 508 §1194.22
   * (b) Las alternativas equivalentes para cualquier presentación multimedia se sincronizarán con la presentación.
* WCAG 1.0
   * 1.1 Proporcione un equivalente textual para cada elemento no textual (por ejemplo, a través de &quot;alt&quot;, &quot;longdesc&quot; o en el contenido del elemento). Esto incluye: imágenes, representaciones gráficas de texto (incluidos símbolos), regiones de mapa de imagen, animaciones (por ejemplo, GIF animados), applets y objetos programáticos, arte ascii, fotogramas, scripts, imágenes utilizadas como viñetas de lista, espaciadores, botones gráficos, sonidos (reproducidos con o sin interacción del usuario), archivos de audio independientes, pistas de audio de vídeo y vídeo (P1).
   * 1.3 Hasta que los agentes de usuario puedan leer automáticamente en voz alta el texto equivalente a una pista visual, proporcione una descripción auditiva de la información importante de la pista visual de una presentación multimedia (P1).
   * 1.4 Para cualquier presentación multimedia basada en el tiempo (por ejemplo, una película o animación), sincronice alternativas equivalentes (por ejemplo, subtítulos o descripciones auditivas de la pista visual) con la presentación (P1).
* WCAG 2.0
   * 1.2.1 Solo audio y solo vídeo (pregrabado): Para los medios pregrabados solo audio y solo vídeo, los siguientes son verdaderos, excepto cuando el audio o vídeo es una alternativa para el texto y está claramente etiquetado como tal: (Nivel A)
   * 1.2.2 Subtítulos (pregrabados): se proporcionan subtítulos para todo el contenido de audio pregrabado en medios sincronizados, excepto cuando los medios son una alternativa para el texto y se etiquetan claramente como tal. (Nivel A)
   * 1.2.3 Descripción del audio o medios alternativos (pregrabados): Se ofrece una alternativa para los medios basados en el tiempo o la descripción del audio del contenido de vídeo pregrabado para los medios sincronizados, excepto cuando los medios son una alternativa para el texto y se etiquetan claramente como tal. (Nivel A)
   * 1.2.4 Subtítulos (en vivo): se proporcionan subtítulos para todo el contenido de audio en vivo en medios sincronizados. (Nivel AA)
   * 1.2.5 Descripción del audio (pregrabado): se proporciona la descripción del audio de todo el contenido de vídeo pregrabado en medios sincronizados. (Nivel AA)
   * 1.2.6 Lenguaje de señas (pregrabado): Se proporciona interpretación del lenguaje de señas para todo el contenido de audio pregrabado en medios sincronizados. (Nivel AAA)
   * 1.2.7 Descripción del audio extendido (pregrabado): cuando las pausas en el audio en primer plano son insuficientes para permitir que las descripciones del audio transmitan el sentido del vídeo, se proporciona una descripción del audio ampliada para todo el contenido de vídeo pregrabado en medios sincronizados. (Nivel AAA)
   * 1.2.8 Alternativa a los medios (pregrabados): se ofrece una alternativa a los medios basados en el tiempo para todos los medios sincronizados pregrabados y para todos los medios solo de vídeo pregrabados. (Nivel AAA)
   * 1.2.9 Solo audio (en vivo): Se proporciona una alternativa para los medios basados en el tiempo que presentan información equivalente para el contenido solo de audio en vivo. (Nivel AAA)

## Identificar el lenguaje natural y cualquier cambio en el lenguaje{#identify-natural-language}

Las tecnologías de asistencia que utilizan sintetizadores de voz específicos del idioma leerán el contenido del formulario, por lo que es importante identificar correctamente el idioma principal del formulario para garantizar que los formularios se lean en el idioma deseado.

Si el texto (o el texto alternativo) de los formularios se presenta en más de un idioma, debe identificar las áreas del formulario en las que se realiza un cambio de un idioma a otro.

En LiveCycle Designer, para establecer el idioma principal se establece la propiedad Configuración regional del formulario y la propiedad Configuración regional del subformulario de nivel superior. Para identificar los cambios en el idioma principal, cambie la propiedad Locale de cualquier objeto que utilice un idioma distinto del del formulario.

Para establecer la propiedad Locale de un formulario:
1. Elija Archivo > Propiedades del formulario y seleccione la pestaña Predeterminado
2. Seleccione el idioma apropiado para la configuración regional del formulario (consulte la figura 17)
3. Haga clic en Aceptar

![Cambiar la configuración regional del formulario en el cuadro de diálogo Propiedades del formulario](/help/forms/using/assets/image-17.png)

Figura 17: **Cambio de la configuración regional del formulario en el cuadro de diálogo Propiedades del formulario**

Para establecer la propiedad Local del subformulario de nivel superior o de un objeto que requiera un idioma diferente:
1. Seleccione el subformulario u objeto de nivel superior en la vista Diseño
1. Muestre la paleta Objeto seleccionando Ventana > Objeto
1. En la paleta Objeto, seleccione la pestaña Campo y, en la lista Configuración regional, seleccione el idioma que desea utilizar para el objeto (consulte la figura 18). Al aplicar diferentes opciones de configuración regional a objetos individuales, tenga en cuenta que los objetos que se encuentran en tablas y subformularios reciben automáticamente la misma configuración regional que el objeto de tabla y subformulario.

![Cambiando la configuración regional de un objeto](/help/forms/using/assets/image-18.png)

Figura 18: **Cambio de la configuración regional de un objeto**

**Puntos de comprobación relacionados**:
* WCAG 1.0
   * 4.1 Identifique claramente los cambios en el lenguaje natural del texto de un documento y cualquier equivalente textual (por ejemplo, subtítulos).
* WCAG 2.0
   * 3.1.1 Idioma de la página: el lenguaje humano predeterminado de cada página web se puede determinar mediante programación. (Nivel A)
   * 3.1.2 Lenguaje de las Partes: El lenguaje humano de cada pasaje o frase en el contenido puede ser determinado mediante programación, excepto para nombres propios, términos técnicos, palabras de lenguaje indeterminado, y palabras o frases que se han convertido en parte de la lengua vernácula del texto inmediatamente circundante. (Nivel AA)
