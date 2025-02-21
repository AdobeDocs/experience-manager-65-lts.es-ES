---
title: Componentes de Adobe Campaign
description: Al integrar con Adobe Campaign, tiene componentes disponibles para cuando trabaja con boletines informativos y con formularios.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 5%

---

# Componentes de Adobe Campaign{#adobe-campaign-components}

Al integrar con Adobe Campaign, tiene componentes disponibles para cuando trabaja con boletines informativos y con formularios. Ambos se describen en este documento.

>[!CAUTION]
>
>Los componentes de correo electrónico de AEM se han quedado obsoletos. Debido a la naturaleza del correo electrónico, que combina contenido y estilo, los componentes de correo electrónico proporcionados de forma predeterminada por AEM se vuelven de reutilización limitada para los clientes debido a la necesidad de implementar estilos personalizados en los componentes que sean necesarios para los proyectos.
>
>Los componentes de correo electrónico se pueden implementar en el nivel de proyecto y los componentes de correo electrónico de AEM obsoletos ilustran cómo se puede lograr. Sin embargo, no utilice estos componentes obsoletos en proyectos.

## Componentes de newsletter de Adobe Campaign {#adobe-campaign-newsletter-components}

Todos los componentes de Campaign siguen las prácticas recomendadas descritas en [Prácticas recomendadas para plantillas de correo electrónico](/help/sites-administering/best-practices-for-email-templates.md) y se basan en el lenguaje de marcado Adobe [HTL](https://helpx.adobe.com/es/experience-manager/htl/using/overview.html).

Cuando abra una newsletter o un correo electrónico configurados para integrarse con Adobe Campaign, debería ver los siguientes componentes en la sección **Newsletter de Adobe Campaign**:

* Encabezado (Campaign)
* Imagen (Campaign)
* Vínculo (campaña)
* Plantilla de imagen de Scene7 (Campaign)
* Referencia de destino (Campaign)
* Texto e imagen (Campaign)
* Texto y personalización (Campaign)

En la siguiente sección se ofrece una descripción de estos componentes.

![chlimage_1-81](assets/chlimage_1-81.png)

### Encabezado (Campaign) {#heading-campaign}

El componente de encabezado puede:

* Para mostrar el nombre de la página actual, deja en blanco el campo **Título**.
* Muestre el texto que especifique en el campo **Título**.

Usted edita directamente el componente **Encabezado (Campaign)**. Dejar vacío para utilizar el título de página.

![chlimage_1-82](assets/chlimage_1-82.png)

Puede configurar lo siguiente:

* **Título**
Si desea utilizar un nombre que no sea el título de la página, introdúzcalo aquí.

* **Nivel de encabezado (1, 2, 3, 4)**
El nivel de encabezado basado en los tamaños de encabezado de HTML 1-4.

El siguiente ejemplo muestra un componente Encabezado (Campaign).

![chlimage_1-83](assets/chlimage_1-83.png)

### Imagen (Campaign) {#image-campaign}

El componente de imagen (campaña) muestra una imagen y el texto correspondiente según los parámetros especificados.

Puede cargar una imagen y luego editarla y manipularla (por ejemplo, recortar, rotar, agregar vínculo/título/texto).

Puede cargar una imagen y luego editarla y manipularla (por ejemplo, recortar, rotar, agregar vínculo/título/texto). Puede arrastrar y soltar una imagen del [Buscador de contenido](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui) directamente en el componente o en su cuadro de diálogo Editar. También puede hacer doble clic en el área central del cuadro de diálogo Editar para examinar el sistema de archivos local y cargar una imagen. Las dos pestañas del cuadro de diálogo Editar también controlan todas las definiciones y manipulación de la imagen:

![chlimage_1-84](assets/chlimage_1-84.png)

Cuando se carga una imagen, puede configurar lo siguiente:

* **Mapa**
Para asignar una imagen, seleccione Mapa. Puede especificar cómo desea crear el mapa de imagen (rectángulo, polígono, etc.) y hacia dónde debe apuntar el área.

* **Recortar**
Seleccione Recortar para recortar una imagen. Utilice el ratón para recortar la imagen.

* **Rotar**
Para rotar una imagen, seleccione Rotar. Use repetidamente hasta que la imagen gire de la forma que desee.

* **Borrar**
Eliminar la imagen actual.

* Barra de zoom (sólo clásica)
Para acercar y alejar la imagen, utilice la barra deslizante situada debajo de la imagen (encima de los botones Aceptar y Cancelar)
* **Título**
Título de la imagen.

* **Texto alternativo**
Texto alternativo que se puede utilizar al crear contenido accesible.

* **Vincular A**
Cree un vínculo a recursos u otras páginas dentro del sitio web.

* **Descripción**
Una descripción de la imagen.

* **Tamaño**
Establece la altura y la anchura de la imagen.

>[!NOTE]
>
>Escriba información en el campo **Texto alternativo** de la ficha **Avanzado** o la imagen no se puede guardar y verá el siguiente mensaje de error:
>
>`Validation failed. Verify the values of the marked fields.`
>

El siguiente ejemplo muestra un componente de imagen (Campaign).

![chlimage_1-85](assets/chlimage_1-85.png)

### Vínculo (campaña) {#link-campaign}

El componente Vínculo (Campaña) permite añadir un vínculo a la newsletter. Este componente solo está disponible en la interfaz de usuario clásica, aunque puede agregar uno en la interfaz de usuario táctil optimizada y abrirlo en modo de compatibilidad.

![chlimage_1-86](assets/chlimage_1-86.png)

Puede configurar lo siguiente en las pestañas **Mostrar**, **Información de URL** o **Avanzado**:

* **Rótulo de vínculo**
El pie de ilustración del vínculo. Este es el texto que ven los usuarios.

* **Sugerencia de vínculo**
Agrega información adicional sobre cómo utilizar el vínculo.

* **LinkType**
En la lista desplegable, seleccione entre una **URL personalizada** y un **documento adaptable**. Este campo es obligatorio. Si selecciona Dirección URL personalizada, puede proporcionar la Dirección URL del vínculo. Si selecciona Documento adaptable, puede proporcionar la ruta del documento.

* **Parámetro de URL adicional**
Añada cualquier parámetro de URL adicional. Haga clic en Agregar elemento para agregar varios elementos.

>[!NOTE]
>
>Escriba información en el campo **Tipo de vínculo** de la ficha **Información de dirección URL** o el componente no se puede guardar y verá el siguiente mensaje de error:
>
>`Validation failed. Verify the values of the marked fields.`
>

El siguiente ejemplo muestra un componente Vínculo (campaña).

![chlimage_1-87](assets/chlimage_1-87.png)

### Referencia de destino (Campaign) {#targeted-reference-campaign}

El componente Referencia de destino (Campaign) permite crear una referencia a un párrafo de destino.

En este componente, se desplaza al párrafo de destino para seleccionarlo.

Haga clic en el menú desplegable para desplazarse hasta el párrafo al que desee hacer referencia. Cuando termine, haga clic en **Aceptar**.

### Texto e imagen (Campaign) {#text-image-campaign}

El componente Texto e imagen (Campaign) añade un bloque de texto y una imagen.

![chlimage_1-88](assets/chlimage_1-88.png)

Al igual que con los componentes Texto y Personalization (Campaign) e Imagen (Campaign), puede configurar lo siguiente:

* **Texto**
Escriba texto. Utilice la barra de herramientas para modificar el formato, crear listas y añadir vínculos.

* **Imagen**
Arrastre una imagen desde el buscador de contenido o haga clic para buscar una imagen. Recorte o gire según sea necesario.

* **Propiedades de imagen** (**Propiedades de imagen avanzadas**)
Permite especificar lo siguiente:

   * **Título**
Título del bloque; se muestra con el ratón.

   * **Texto alternativo**
Texto alternativo que se mostrará si no se puede mostrar la imagen.

   * **Vínculo a**
Cree un vínculo a recursos u otras páginas dentro del sitio web.

   * **Descripción**
Una descripción de la imagen.

   * **Tamaño**
Establece la altura y anchura de la imagen.

>[!NOTE]
>
>El campo **Texto alternativo** de la ficha **Avanzado** es obligatorio o el componente no se puede guardar y verá el siguiente mensaje de error:
>
>`Validation failed. Verify the values of the marked fields.`
>

El siguiente ejemplo muestra un componente Texto e imagen (Campaign).

![chlimage_1-89](assets/chlimage_1-89.png)

### Texto y personalización (Campaign) {#text-personalization-campaign}

El componente Texto y Personalization (Campaign) le permite introducir un bloque de texto mediante un editor de WYSIWYG, con la funcionalidad proporcionada por el [editor de texto enriquecido](/help/sites-authoring/rich-text-editor.md). Además, este componente le permite utilizar campos de contexto y bloques de personalización disponibles en Adobe Campaign; consulte también [Inserción de Personalization](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization).

La selección de iconos le permite dar formato al texto, incluidas las características de la fuente, la alineación, los vínculos, las listas y la sangría.

Agregue texto como lo haría normalmente en el editor de texto enriquecido. Añada personalización seleccionando el menú desplegable Adobe Campaign y los campos según corresponda.

![chlimage_1-90](assets/chlimage_1-90.png)

Puede añadir los campos de texto y contexto o los bloques personalizados para crear el contenido. A continuación, seleccione Client Context para probar los datos en los perfiles de persona. Después de seleccionar una persona, los campos de personalización se sustituyen automáticamente por los datos del perfil seleccionado.

>[!NOTE]
>
>Solo se tienen en cuenta los campos definidos en el esquema **nms:seedMember** o una de sus extensiones. Los atributos de las tablas vinculadas a `nms:seedMember` no están disponibles.

## Componentes de formulario Adobe Campaign {#adobe-campaign-form-components}

Los componentes de Adobe Campaign se utilizan para crear un formulario que los usuarios rellenan para suscribirse a un boletín informativo, cancelar la suscripción a un boletín informativo o actualizar sus perfiles de usuario. Consulte [Creación de Adobe Campaign Forms](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md) para obtener más información.

Cada campo de componente se puede vincular a un campo de base de datos de Adobe Campaign. Los campos disponibles difieren según el tipo de datos que contengan, tal como se describe en la sección [Componentes y tipo de datos](#components-and-data-type). Si amplía el esquema de destinatario en Adobe Campaign, los nuevos campos estarán disponibles en los componentes cuyos tipos de datos coincidan.

Cuando abra un formulario configurado para integrarse con Adobe Campaign, verá los siguientes componentes en la sección **Adobe Campaign**:

* Casilla (Campaign)
* Campo de fecha (Campaign) y Campo de fecha/HTML5 (Campaign)
* Clave principal cifrada (Campaign)
* Visualización de error (Campaign)
* Clave de conciliación oculta (Campaign)
* Campo numérico (Campaign)
* Campo de opción (Campaign)
* Lista de comprobación de suscripciones (Sightly)
* Campo de texto (Campaign)

Esta sección describe cada componente en detalle.

### Componentes y tipo de datos {#components-and-data-type}

En la tabla siguiente se describen los componentes disponibles para mostrar y modificar los datos de perfil de Adobe Campaign. Cada componente se puede asignar a un campo de perfil de Adobe Campaign para mostrar su valor y actualizar el campo cuando se envíe el formulario. Los diferentes componentes solo pueden coincidir con campos de un tipo de datos adecuado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo de datos del campo Adobe Campaign</strong></p> </td>
   <td><p><strong>Campo de ejemplo</strong></p> </td>
  </tr>
  <tr>
   <td><p>Casilla (Campaign)</p> </td>
   <td><p>booleano</p> </td>
   <td><p>Ya no se puede contactar (por ningún canal)</p> </td>
  </tr>
  <tr>
   <td><p>Campo de fecha (Campaign)</p> <p>Campo de fecha/HTML 5 (Campaign)</p> </td>
   <td><p>fecha</p> </td>
   <td><p>Fecha de nacimiento</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico (Campaign)</p> </td>
   <td><p>numérico (byte, corto, largo, doble)</p> </td>
   <td><p>Edad</p> </td>
  </tr>
  <tr>
   <td><p>Campo de opción (Campaign)</p> </td>
   <td><p>byte con valores asociados</p> </td>
   <td><p>Sexo</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto (Campaign)</p> </td>
   <td><p>cadena</p> </td>
   <td><p>Correo electrónico</p> </td>
  </tr>
 </tbody>
</table>

### Configuración común a la mayoría de los componentes {#settings-common-to-most-components}

Los componentes de Adobe Campaign tienen configuraciones que son comunes en todos los componentes (excepto en los componentes Clave principal cifrada y Clave de reconciliación oculta).

En la mayoría de los componentes, puede configurar lo siguiente:

#### Título y texto {#title-and-text}

* **Título**
Si desea utilizar un nombre que no sea el nombre del elemento, introdúzcalo aquí.

* **Ocultar título**
Active esta casilla de verificación si no desea que el título sea visible.

* **Descripción**
Agregue una descripción al campo para proporcionar más información a los usuarios.

* **Mostrar solo valor**
Solo muestra el valor, si hay uno

#### Adobe Campaign {#adobe-campaign}

Puede configurar lo siguiente:

* **Asignación**
Seleccione un campo de personalización de Adobe Campaign, si corresponde.

* **Clave de reconciliación**
Active esta casilla de verificación si este campo forma parte de la clave de reconciliación.

#### Restricciones {#constraints}

* **Obligatorio**: seleccione esta casilla de verificación para que este componente sea obligatorio; es decir, los usuarios deben escribir un valor.
* **Mensaje obligatorio**: de forma opcional, agregue un mensaje que indique que el campo es obligatorio.

#### Estilo {#styling}

* **CSS**
Introduzca las clases CSS que desee utilizar para este componente.

### Casilla (Campaign) {#checkbox-campaign}

El componente Casilla de verificación (Campaign) permite al usuario modificar los campos de perfil de Adobe Campaign que son de tipo de datos booleano. Por ejemplo, puede tener un componente Casilla de verificación (Campaña) que permita al destinatario especificar que no desea que se le contacte a través de ningún canal.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Casilla de verificación (Campaign).

El siguiente ejemplo muestra un componente Casilla de verificación (Campaign).

![chlimage_1-91](assets/chlimage_1-91.png)

### Campo de fecha (Campaign) y Campo de fecha/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilice el campo date para permitir que los destinatarios indiquen una fecha; por ejemplo, puede que desee que los destinatarios especifiquen sus fechas de nacimiento. El formato de fecha coincide con el formato utilizado en la instancia de Adobe Campaign.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones - Restricción** - Puede seleccionar - **Ninguna** o **Fecha** para agregar la restricción de una restricción de fecha o ninguna restricción. Si selecciona fecha, la respuesta que introducen los usuarios en el campo debe tener un formato de fecha.

* **Mensaje de restricción**: además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar formato a sus respuestas correctamente.
* **Estilo - Anchura** - Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-** o introduciendo un número.

El siguiente ejemplo muestra un componente Campo de fecha (Campaign) con la anchura ajustada mostrada.

![chlimage_1-92](assets/chlimage_1-92.png)

### Clave principal cifrada (Campaign) {#encrypted-primary-key-campaign}

Este componente define el nombre del parámetro de URL que contendrá el identificador de un perfil de Adobe Campaign (**Identificador de recurso principal** o **Clave principal cifrada** en Adobe Campaign Standard y 6.1, respectivamente).

Cada formulario que muestra y modifica los datos de perfil de Adobe Campaign **debe** incluir un componente de clave principal cifrada.

Puede configurar lo siguiente en el componente Clave principal cifrada (Campaign):

* **Título y texto - Nombre de elemento** - El valor predeterminado es encryptionPK. Solo es necesario cambiar el nombre del elemento cuando entra en conflicto con el nombre de otro elemento del formulario. Dos campos de formulario no pueden tener el mismo nombre de elemento.
* **Adobe Campaign - URL Parameter** - Agregue el parámetro de URL para el EPK. Por ejemplo, puede usar el valor **epk**.

El siguiente ejemplo muestra un componente de clave principal cifrada (Campaign).

![chlimage_1-93](assets/chlimage_1-93.png)

### Visualización de error (Campaign) {#error-display-campaign}

Este componente permite mostrar los errores del servidor. La gestión de errores del formulario debe establecerse en Forward para que el componente funcione correctamente.

El siguiente ejemplo muestra un componente Visualización de error (Campaign).

![chlimage_1-94](assets/chlimage_1-94.png)

### Clave de conciliación oculta (Campaign) {#hidden-reconciliation-key-campaign}

El componente Clave de reconciliación oculta (Campaign) permite agregar campos ocultos como parte de la clave de reconciliación a un formulario.

Puede configurar lo siguiente en el componente Clave de reconciliación oculta (Campaign):

* **Título y texto - Nombre de elemento** - El valor predeterminado es econcilKey. Solo es necesario cambiar el nombre del elemento cuando entra en conflicto con el nombre de otro elemento del formulario. Dos campos de formulario no pueden tener el mismo nombre de elemento.
* **Adobe Campaign - Asignación** - Asignar a un campo de personalización de Adobe Campaign.

El siguiente ejemplo muestra un componente Clave de reconciliación oculta (Campaign).

![chlimage_1-95](assets/chlimage_1-95.png)

### Campo numérico (Campaign) {#numeric-field-campaign}

Utilice el campo numérico para permitir que los destinatarios introduzcan números, por ejemplo, su edad.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones: restricción** desplegable
Puede seleccionar - **Ninguno** o **Numérico -** para agregar la restricción de un número o de ninguna restricción. Si selecciona un número, la respuesta que introducen los usuarios en el campo debe ser numérica.

* **Mensaje de restricción**: además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar formato a sus respuestas correctamente.
* **Estilo - Anchura** - Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-** o introduciendo un número.

El siguiente ejemplo muestra un componente de campo numérico (Campaign) con la anchura configurada en pantalla.

![chlimage_1-96](assets/chlimage_1-96.png)

### Campo de opción (Campaign) {#option-field-campaign}

Esta lista desplegable permite seleccionar una opción; por ejemplo, el sexo o el estado de un destinatario.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Campo de opción (Campaign). Para rellenar la lista desplegable, seleccione el campo correspondiente en los campos personalizados de Adobe Campaign tocando o haciendo clic en el símbolo de Adobe Campaign y navegando al campo.

El siguiente ejemplo muestra un componente Campo de opción (Campaign).

![chlimage_1-97](assets/chlimage_1-97.png)

### Lista de comprobación de suscripciones (Sightly) {#subscriptions-checklist-campaign}

Utilice el componente **Lista de comprobación de suscripciones (Campaign)** para modificar las suscripciones asociadas a un perfil de Adobe Campaign.

Cuando se agrega a un formulario, este componente muestra todas las suscripciones disponibles como casillas de verificación y permite al usuario seleccionar las suscripciones deseadas. Cuando los usuarios envían el formulario, este componente suscribe o cancela la suscripción del usuario a los servicios seleccionados según el tipo de acción del formulario (**Adobe Campaign: Suscribirse a los servicios** o **Adobe Campaign: cancelar la suscripción a los servicios**).

>[!NOTE]
>
>El componente no comprueba a qué servicios ya está suscrito/canceló la suscripción el usuario.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Lista de comprobación de suscripciones (Campaign). (No hay configuraciones de Adobe Campaign disponibles para este componente).

El siguiente ejemplo muestra un componente Lista de comprobación de suscripciones (Campaign).

![chlimage_1-98](assets/chlimage_1-98.png)

### Campo de texto (Campaign) {#text-field-campaign}

Componente Campo de texto (Campaign) que permite introducir datos de tipo cadena, como nombre, apellidos, dirección, dirección de correo electrónico, etc.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones - Restricción** - lista desplegable - Puede seleccionar - **Ninguno**, **Correo electrónico**, **Nombre** (sin diéresis) para agregar la restricción de una dirección de correo electrónico, un nombre o ninguna restricción. Si selecciona correo electrónico, la respuesta que introducen los usuarios en el campo debe ser una dirección de correo electrónico. Si selecciona un nombre, debe ser un nombre (no se permiten diéresis).

* **Mensaje de restricción**: además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar formato a sus respuestas correctamente.
* **Estilo - Anchura** - Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-** o introduciendo un número.

El siguiente ejemplo muestra un componente Campo de texto (Campaign).

![chlimage_1-99](assets/chlimage_1-99.png)
