---
title: Integración con componentes de Adobe Campaign
description: Al integrar con Adobe Campaign, tiene componentes disponibles para cuando trabaja con boletines informativos y con formularios.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: 20de763d-dd07-4ba6-a54d-a2b3b9b7e1ec
index: false
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '2857'
ht-degree: 4%

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

Los componentes aparecen de la siguiente manera:

![chlimage_1-43](assets/chlimage_1-43.png)

### Encabezado (Campaign) {#heading-campaign}

El componente de encabezado puede:

* Para mostrar el nombre de la página actual, deja en blanco el campo **Título**.
* Muestre el texto que especifique en el campo **Título**.

Usted edita directamente el componente **Encabezado (Campaign)**. Dejar vacío para utilizar el título de página.

![chlimage_1-44](assets/chlimage_1-44.png)

Puede configurar lo siguiente:

* **Título**
Si desea utilizar un nombre que no sea el título de la página, introdúzcalo aquí.

* **Nivel de encabezado (1, 2, 3, 4)**
El nivel de encabezado basado en los tamaños de encabezado de HTML 1-4.

El siguiente ejemplo muestra un componente Encabezado (Campaign).

![chlimage_1-45](assets/chlimage_1-45.png)

### Imagen (Campaign) {#image-campaign}

El componente de imagen (campaña) muestra una imagen y el texto correspondiente según los parámetros especificados.

Puede cargar una imagen y luego editarla y manipularla (por ejemplo, recortar, rotar, agregar vínculo/título/texto).

Puede arrastrar y soltar una imagen del [Explorador de recursos](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) directamente en el componente o en su [cuadro de diálogo de configuración](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). También puede cargar una imagen desde el cuadro de diálogo Configurar; este cuadro de diálogo también controla todas las definiciones y manipulación de la imagen:

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Escriba información en el campo **Texto alternativo** o la imagen no se podrá guardar.

Una vez que la imagen se haya cargado (y no antes), puede usar [la edición local](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) para recortar o girar la imagen según sea necesario:

![Barra de herramientas de edición local](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>El editor in situ utiliza el tamaño y la relación de aspecto originales de la imagen al editarla. También puede especificar las propiedades de altura y anchura. Las restricciones de tamaño y proporción de aspecto definidas en las propiedades se aplican al guardar los cambios de edición.
>
>Según la instancia, el [diseño de la página](/help/sites-developing/designer.md) también puede imponer restricciones mínimas y máximas, que se desarrollan durante la implementación del proyecto.

Hay varias opciones adicionales disponibles en el modo de edición de pantalla completa; por ejemplo, asignación y zoom:

![Modo de edición de pantalla completa](do-not-localize/chlimage_1-11.png)

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

![chlimage_1-47](assets/chlimage_1-47.png)

### Vínculo (campaña) {#link-campaign}

El componente Vínculo (Campaña) permite añadir un vínculo a la newsletter.

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

![chlimage_1-48](assets/chlimage_1-48.png)

### Plantilla de imagen de Dynamic Media Classic (Scene7) (Campaign) {#scene-image-template-campaign}

Las plantillas de imagen de Dynamic Media Classic (Scene7) se superponen a archivos de imagen superpuestos, donde el contenido y las propiedades pueden parametrizarse en función de la variabilidad. El componente **[!UICONTROL Image template]** le permite usar plantillas de Scene7 en boletines informativos y cambiar los valores de los parámetros de plantilla. Además, puede utilizar variables de metadatos de Adobe Campaign dentro de los parámetros para que cada usuario experimente la imagen de forma personalizada.

![chlimage_1-49](assets/chlimage_1-49.png)

Haga clic en **Editar** para configurar el componente. Puede configurar las opciones descritas en esta sección. Esta plantilla de imagen de Scene7 se describe en detalle en [Componente de plantilla de imagen de Scene7](/help/assets/scene7.md#image-template).

Además, el panel de parámetros enumera todos los parámetros de plantilla que se han definido para la plantilla en Scene7. Para cada uno de estos parámetros, puede adaptar el valor, insertar variables o restablecerlas a su valor predeterminado.

![chlimage_1-50](assets/chlimage_1-50.png)

### Referencia de destino (Campaign) {#targeted-reference-campaign}

El componente Referencia de destino (Campaign) permite crear una referencia a un párrafo de destino.

En este componente, se desplaza al párrafo de destino para seleccionarlo.

Haga clic en el icono de carpeta para desplazarse hasta el párrafo al que desee hacer referencia. Cuando termine, haga clic en la marca de verificación.

### Texto e imagen (Campaign) {#text-image-campaign}

El componente Texto e imagen (Campaign) añade un bloque de texto y una imagen.

Al hacer clic en para configurar el componente, se selecciona Texto o Imagen.

![chlimage_1-51](assets/chlimage_1-51.png)

Al seleccionar **Texto**, se muestra un editor en línea:

![Barra de herramientas de texto](do-not-localize/chlimage_1-12.png)

Al seleccionar **Imagen**, se muestra el editor local de imágenes:

![Barra de herramientas de imágenes](do-not-localize/chlimage_1-13.png)

Consulte [Componente de imagen (Campaign)](#image-campaign) para obtener más información sobre cómo trabajar con imágenes. Consulte [Componente Texto y Personalization (Campaign)](#text-personalization-campaign) para obtener más información sobre cómo trabajar con texto.

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

![chlimage_1-52](assets/chlimage_1-52.png)

### Texto y personalización (Campaign) {#text-personalization-campaign}

El componente Texto y Personalization (Campaign) le permite introducir un bloque de texto mediante un editor de WYSIWYG, con la funcionalidad proporcionada por el [editor de texto enriquecido](/help/sites-authoring/rich-text-editor.md). Además, este componente le permite utilizar campos de contexto y bloques de personalización disponibles en Adobe Campaign; consulte también [Inserción de Personalization](/help/sites-authoring/campaign.md#inserting-personalization).

La selección de iconos le permite dar formato al texto, incluidas las características de la fuente, la alineación, los vínculos, las listas y la sangría. La funcionalidad es básicamente la misma en [ambas interfaces](/help/sites-authoring/editing-content.md), aunque la apariencia es diferente:

![chlimage_1-53](assets/chlimage_1-53.png)

En el editor local puede añadir texto, cambiar la justificación, añadir y eliminar vínculos, añadir campos de contexto o bloques de personalización e introducir el modo de pantalla completa. Cuando termine de agregar texto/personalización, seleccione la marca de verificación para guardar los cambios (o x para cancelar). Consulte [Edición local](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) para obtener más información.

>[!NOTE]
>
>* Los campos de personalización disponibles dependen de la plantilla de Adobe Campaign a la que esté vinculado el boletín informativo.
>* Después de seleccionar una persona en ContextHub, los campos de personalización se sustituyen automáticamente por los datos del perfil seleccionado.
>
>Consulte [Inserción de Personalization](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Solo se tienen en cuenta los campos definidos en el esquema **nms:seedMember** o una de sus extensiones. Los atributos de las tablas vinculadas a **nms:seedMember** no están disponibles.

## Componentes de formulario Adobe Campaign {#adobe-campaign-form-components}

Los componentes de Adobe Campaign se utilizan para crear un formulario que los usuarios rellenan para suscribirse a un boletín informativo, cancelar la suscripción a un boletín informativo o actualizar sus perfiles de usuario. Consulte [Creación de Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md) para obtener más información.

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

Los componentes aparecen de la siguiente manera:

![chlimage_1-55](assets/chlimage_1-55.png)

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
   <td><p>Género</p> </td>
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

![chlimage_1-56](assets/chlimage_1-56.png)

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

![chlimage_1-57](assets/chlimage_1-57.png)

#### Restricciones {#constraints}

* **Obligatorio** Seleccione esta casilla de verificación para que este componente sea obligatorio; es decir, los usuarios deben escribir un valor.
* **Mensaje obligatorio** Si lo desea, agregue un mensaje que indique que el campo es obligatorio.

![chlimage_1-58](assets/chlimage_1-58.png)

#### Estilo {#styling}

* **CSS**
Introduzca las clases CSS que desee utilizar para este componente.

![chlimage_1-59](assets/chlimage_1-59.png)

### Casilla (Campaign) {#checkbox-campaign}

El componente Casilla de verificación (Campaign) permite al usuario modificar los campos de perfil de Adobe Campaign que son de tipo de datos booleano. Por ejemplo, puede tener un componente Casilla de verificación (Campaña) que permita al destinatario especificar que no desea que se le contacte a través de ningún canal.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Casilla de verificación (Campaign).

El siguiente ejemplo muestra un componente Casilla de verificación (Campaign).

![chlimage_1-60](assets/chlimage_1-60.png)

### Campo de fecha (Campaign) y Campo de fecha/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilice el campo date para permitir que los destinatarios indiquen una fecha; por ejemplo, puede que desee que los destinatarios especifiquen sus fechas de nacimiento. El formato de fecha coincide con el formato utilizado en la instancia de Adobe Campaign.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones: restricción** desplegable
Puede seleccionar - **Ninguno** o **Fecha -** para agregar la restricción de una fecha o ninguna restricción. Si selecciona fecha, la respuesta que introducen los usuarios en el campo debe tener un formato de fecha.

* **Mensaje de restricción** Además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar un formato correcto a sus respuestas.
* **Estilo - Anchura** Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-**, o bien introduciendo un número.

El siguiente ejemplo muestra un componente Campo de fecha (Campaign) con la anchura ajustada mostrada.

![chlimage_1-61](assets/chlimage_1-61.png)

### Clave principal cifrada (Campaign) {#encrypted-primary-key-campaign}

Este componente define el nombre del parámetro de URL que contendrá el identificador de un perfil de Adobe Campaign (**Identificador de recurso principal** o **Clave principal cifrada** en Adobe Campaign Standard y 6.1, respectivamente).

Cada formulario que muestra y modifica los datos de perfil de Adobe Campaign **debe** incluir un componente de clave principal cifrada.

Puede configurar lo siguiente en el componente Clave principal cifrada (Campaign):

* **Título y texto - Nombre de elemento** El valor predeterminado es encryptionPK. Solo es necesario cambiar el nombre del elemento cuando entra en conflicto con el nombre de otro elemento del formulario. Dos campos de formulario no pueden tener el mismo nombre de elemento.
* **Adobe Campaign - URL Parameter** Agregue el parámetro de URL para el EPK. Por ejemplo, puede usar el valor **epk**.

El siguiente ejemplo muestra un componente de clave principal cifrada (Campaign).

![chlimage_1-62](assets/chlimage_1-62.png)

### Visualización de error (Campaign) {#error-display-campaign}

Este componente permite mostrar los errores del servidor. La gestión de errores del formulario debe establecerse en Forward para que el componente funcione correctamente.

El siguiente ejemplo muestra un componente Visualización de error (Campaign).

![chlimage_1-63](assets/chlimage_1-63.png)

### Clave de conciliación oculta (Campaign) {#hidden-reconciliation-key-campaign}

El componente Clave de reconciliación oculta (Campaign) permite agregar campos ocultos como parte de la clave de reconciliación a un formulario.

Puede configurar lo siguiente en el componente Clave de reconciliación oculta (Campaign):

* **Título y texto: el nombre del elemento** tiene el valor predeterminado de la clave de reconciliación. Solo es necesario cambiar el nombre del elemento cuando entra en conflicto con el nombre de otro elemento del formulario. Dos campos de formulario no pueden tener el mismo nombre de elemento.
* **Adobe Campaign - Asignación** Asignación a un campo de personalización de Adobe Campaign.

El siguiente ejemplo muestra un componente Clave de reconciliación oculta (Campaign).

![chlimage_1-64](assets/chlimage_1-64.png)

### Campo numérico (Campaign) {#numeric-field-campaign}

Utilice el campo numérico para permitir que los destinatarios introduzcan números, por ejemplo, su edad.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones: restricción** desplegable
Puede seleccionar - **Ninguno** o **Numérico -** para agregar la restricción de un número o de ninguna restricción. Si selecciona un número, la respuesta que introducen los usuarios en el campo debe ser numérica.

* **Mensaje de restricción** Además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar un formato correcto a sus respuestas.
* **Estilo - Anchura** Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-**, o bien introduciendo un número.

El siguiente ejemplo muestra un componente de campo numérico (Campaign) con la anchura configurada en pantalla.

![chlimage_1-65](assets/chlimage_1-65.png)

### Campo de opción (Campaign) {#option-field-campaign}

Esta lista desplegable permite seleccionar una opción; por ejemplo, el sexo o el estado de un destinatario.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Campo de opción (Campaign). Para rellenar la lista desplegable, seleccione el campo correspondiente en los campos personalizados de Adobe Campaign tocando o haciendo clic en el símbolo de Adobe Campaign y navegando al campo.

![chlimage_1-66](assets/chlimage_1-66.png)

El siguiente ejemplo muestra un componente Campo de opción (Campaign).

![chlimage_1-67](assets/chlimage_1-67.png)

### Lista de comprobación de suscripciones (Sightly) {#subscriptions-checklist-campaign}

Utilice el componente **Lista de comprobación de suscripciones (Campaign)** para modificar las suscripciones asociadas a un perfil de Adobe Campaign.

Cuando se agrega a un formulario, este componente muestra todas las suscripciones disponibles como casillas de verificación y permite al usuario seleccionar las suscripciones deseadas. Cuando los usuarios envían el formulario, este componente suscribe o cancela la suscripción del usuario a los servicios seleccionados según el tipo de acción del formulario (**Adobe Campaign: Suscribirse a los servicios** o **Adobe Campaign: cancelar la suscripción a los servicios**).

>[!NOTE]
>
>El componente no comprueba a qué servicios ya está suscrito/canceló la suscripción el usuario.

Puede [configurar las opciones comunes a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components) en el componente Lista de comprobación de suscripciones (Campaign). (No hay configuraciones de Adobe Campaign disponibles para este componente).

El siguiente ejemplo muestra un componente Lista de comprobación de suscripciones (Campaign).

![chlimage_1-68](assets/chlimage_1-68.png)

### Campo de texto (Campaign) {#text-field-campaign}

Componente Campo de texto (Campaign) que permite introducir datos de tipo cadena, como nombre, apellidos, dirección, dirección de correo electrónico, etc.

Además de la configuración [común a la mayoría de los componentes de Adobe Campaign](#settings-common-to-most-components), puede configurar lo siguiente:

* **Restricciones: restricción** desplegable
Puede seleccionar - **Ninguno,** **Correo electrónico** o **Nombre** (sin diéresis) - para agregar la restricción de una dirección de correo electrónico, un nombre o ninguna restricción. Si selecciona correo electrónico, la respuesta que introducen los usuarios en el campo debe ser una dirección de correo electrónico. Si selecciona un nombre, debe ser un nombre (no se permiten diéresis).

* **Mensaje de restricción** Además, puede agregar un mensaje de restricción para que los usuarios sepan cómo dar un formato correcto a sus respuestas.
* **Estilo - Anchura** Ajuste la anchura del campo tocando o haciendo clic en los iconos **+** y **-**, o bien introduciendo un número.

El siguiente ejemplo muestra un componente Campo de texto (Campaign).

![chlimage_1-69](assets/chlimage_1-69.png)
