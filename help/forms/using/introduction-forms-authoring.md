---
title: Introducción a la creación de formularios adaptables
description: AEM Forms proporciona una interfaz fácil de usar pero potente para la creación de formularios adaptables. Ofrece una serie de componentes y herramientas que puede utilizar para crear formularios.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
docset: aem65
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 96%

---

# Introducción a la creación de formularios adaptables {#introduction-to-authoring-adaptive-forms}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring.html) |
| AEM 6.5 | Este artículo |


## Información general {#overview}

Los formularios adaptables permiten crear formularios atractivos, interactivos, dinámicos y adaptables. AEM Forms proporciona una interfaz de usuario intuitiva y componentes predeterminados para crear y trabajar con formularios adaptables. Puede elegir crear un formulario adaptable en base a un modelo o esquema de formulario o sin un modelo de formulario. Es importante elegir cuidadosamente un modelo del formulario que no solo se adapte a sus necesidades, sino que amplíe sus inversiones y recursos de infraestructura existentes. Puede elegir entre las siguientes opciones para crear un formulario adaptable:

* **Uso del modelo de datos de formulario**
  La [integración de datos](../../forms/using/data-integration.md) permite integrar entidades y servicios de diferentes fuentes de datos en un modelo de datos de formulario que puede utilizar para crear formularios adaptables. Elija un modelo de datos de formulario si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varias fuentes de datos.

* **Usar una plantilla de formulario XDP**
Es un modelo de formulario ideal si tiene inversiones en formularios XFA o XDP. Proporciona una forma directa de convertir los formularios basados en XFA en formularios adaptables. Cualquier regla XFA existente se conservará en el formulario adaptable asociado. El formulario adaptable resultante admitirá construcciones XFA, como validaciones, eventos, propiedades y patrones.

* **Usar una definición de esquema XML (XSD) o un esquema JSON**
Los esquemas XML y JSON representan la estructura en la que el sistema back-end de su organización produce o consume los datos. Puede asociar el esquema a un formulario adaptable y utilizar sus elementos para agregarle contenido dinámico. Los elementos del esquema estarán disponibles para su uso en la pestaña Objetos del modelo de datos del Explorador de contenido al crear formularios adaptables.

* **No usar ninguno o no usar un modelo de formulario**
Los formularios adaptables creados con esta opción no utilizan ningún modelo de formulario. El XML de datos generado a partir de estos formularios tiene una estructura plana con campos y valores correspondientes.

Para obtener más información sobre la creación de un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).

## IU de creación de formularios adaptables {#adaptive-form-authoring-ui}

La IU táctil optimizada para crear formularios adaptables es intuitiva y proporciona lo siguiente:

* Funcionalidad de arrastrar y soltar
* Componentes de formulario estándar
* Repositorio integrado para recursos

Cuando crea o edita un formulario adaptable existente, utiliza los siguientes elementos de la interfaz de usuario:

* [Barra lateral](#sidebar)
* [Barra de herramientas de la página](#page-toolbar)
* [Barra de herramientas de los componentes](#component-toolbar)
* [Página de formulario adaptable](#af-page)

![IU de creación de formularios adaptables](assets/formeditor.png)

**A.** Barra lateral **B.** Barra de herramientas de la página **C.** Página del formulario adaptable

### Barra lateral {#sidebar}

La barra lateral le permite

* Consultar el contenido del formulario, como paneles, componentes, campos y diseño.
* Editar las propiedades del componente.
* Buscar, ver y utilizar recursos en su repositorio de administración de recursos digitales de AEM (DAM).
* Agregar componentes al formulario.

![Barra lateral](assets/sidebar-comps.png)

**A.** Explorador de contenido **B.** Explorador de propiedades **C.** Explorador de recursos **D.** Explorador de componentes

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barra lateral consta de los siguientes exploradores:

* **Explorador de contenido**
En el Explorador de contenido, puede ver lo siguiente:

   * **Objetos del formulario**
Muestra la jerarquía de objetos del formulario. El autor puede desplazarse a un componente específico del formulario al pulsar ese elemento en el árbol de objetos del formulario. El autor puede buscar objetos y reorganizarlos desde este árbol.

   * **Objetos del modelo de datos**
Permite ver la jerarquía del modelo del formulario. 
Permite arrastrar y soltar elementos del modelo del formulario en el formulario adaptable. Los elementos agregados se convierten automáticamente en componentes de formulario y conservan sus propiedades originales. Puede ver objetos del modelo de datos cuando el formulario utilice un esquema XML, un esquema JSON o una plantilla XDP.

* **Explorador de propiedades**

  Permite editar las propiedades de un componente. Las propiedades cambian según el componente. Para ver las propiedades del contenedor de formulario adaptable, haga lo siguiente:

  Seleccione un componente, luego seleccione ![field-level](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y luego seleccione ![cmppr](assets/cmppr.png).

* **Explorador de recursos**

  Segmenta contenido de distintos tipos, como imágenes, documentos, páginas, películas, etc.

* **Explorador de componentes**

  Incluye componentes que puede utilizar para crear un formulario adaptable. Puede arrastrar componentes desde y hasta el formulario adaptable para agregar elementos de formulario y configurar los elementos agregados según los requisitos. En la siguiente tabla se describen los componentes enumerados en el explorador de componentes.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funcionalidad</strong></th>
  </tr>
  <tr>
   <td>Bloque de Adobe Sign</td>
   <td>Agrega un bloque de texto con marcadores de posición para que los campos se completen al firmar mediante Adobe Sign.</td>
  </tr>
  <tr>
   <td>Botón</td>
   <td>Agrega un botón, que puede configurar para realizar acciones como guardar, restablecer, ir al siguiente, ir al anterior, etc.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Agrega la validación CAPTCHA mediante el servicio reCAPTCHA de Google. Para obtener más información, consulte <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Uso de Captcha en formularios adaptables</a>.</td>
  </tr>
  <tr>
   <td>Gráfico</td>
   <td>Agrega un gráfico que puede usar en formularios adaptables y documentos para la representación visual de datos bidimensionales en paneles repetibles y filas de tabla.</td>
  </tr>
  <tr>
   <td>Casilla de verificación</td>
   <td>Agrega una casilla de verificación.</td>
  </tr>
  <tr>
   <td>Campo de introducción de fecha</td>
   <td>Utilice el componente Campo de introducción de fecha en el formulario para permitir a los clientes rellenar los campos de día, mes y año por separado en tres cuadros. Puede personalizar el aspecto del componente y cambiar el formato de la fecha. Por ejemplo, puede permitir que sus clientes introduzcan fechas en formato MM/DD/AAAA o DD/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Selector de fecha</td>
   <td>Agrega un campo de calendario para elegir una fecha.</td>
  </tr>
  <tr>
   <td>Fragmento de documento</td>
   <td>Permite agregar componentes reutilizables de una correspondencia.</td>
  </tr>
  <tr>
   <td>Grupo de fragmentos de documento</td>
   <td>Permite agregar un grupo de fragmentos de documento relacionados que se pueden usar en una plantilla de carta como una sola unidad.</td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td>Agrega una lista desplegable: de selección única o múltiple</td>
  </tr>
  <tr>
   <td>Correo electrónico</td>
   <td><p>Agrega un campo para capturar la dirección de correo electrónico. El componente Correo electrónico, de forma predeterminada, valida las direcciones de correo electrónico con la siguiente expresión regular.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;'*+/=?^_&grave;{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Archivo adjunto</td>
   <td><p>Agrega un botón que permite a los usuarios examinar y adjuntar documentos de apoyo a un formulario. Puede adjuntar varios archivos a un componente Archivo adjunto. También puede especificar el **[!UICONTROL Tamaño máximo de archivo]** y los **[!UICONTROL Tipos de archivo compatibles]** de los archivos adjuntos en el Explorador de propiedades del componente. </p> <p><strong> Nota: </strong><ul> <li> El componente no permite adjuntar archivos con un nombre de archivo que empiece por los caracteres (.), o que contenga los caracteres \ / : * ? " &lt; &gt; | ; % $, o nombres de archivo especiales reservados para el sistema operativo Windows, como nul, prn, con, lpt o com. </li> <li> Para adjuntar varios archivos a un componente Archivo adjunto abierto en el explorador Safari de Apple, seleccione y adjunte los archivos uno a uno. No puede seleccionar y adjuntar varios archivos a la vez.</li> <li>El componente Archivo adjunto es compatible con un conjunto predefinido de formatos de archivo en formularios adaptables habilitados para Adobe Sign. Para obtener más información, consulte <a href="https://helpx.adobe.com/es/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formatos de archivo compatibles</a>. </li></ul></p> </td>
  </tr>
  <tr>
   <td>Lista de archivos adjuntos</td>
   <td>Agrega un campo que enumera todos los archivos adjuntos cargados mediante el componente Archivo adjunto.</td>
  </tr>
  <tr>
   <td>Encabezado<br /> </td>
   <td>Agrega el encabezado, que generalmente incluye el logotipo de una corporación, el título del formulario y el resumen.<br /> </td>
  </tr>
  <tr>
   <td>Pie de página</td>
   <td>Agrega el pie de página que generalmente incluye información sobre el copyright y vínculos a otras páginas. </td>
  </tr>
  <tr>
   <td>Imagen</td>
   <td>Insertar una imagen.</td>
  </tr>
  <tr>
   <td>Opción de imagen</td>
   <td>Permite a los clientes seleccionar una imagen para proporcionar información. Puede utilizar la información para proporcionar servicios personalizados a sus clientes.</td>
  </tr>
  <tr>
   <td>Botón Siguiente</td>
   <td>Agrega un botón para ir al siguiente panel en un formulario.</td>
  </tr>
  <tr>
   <td>Cuadro numérico</td>
   <td>Agrega un campo para capturar valores numéricos</td>
  </tr>
  <tr>
   <td>Stepper numérico</td>
   <td>Utilice Stepper numérico en el formulario para permitir que los clientes escriban un valor numérico, que puede aumentar o disminuir en función de un paso predefinido.</td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><p>Agrega un panel o subpanel.</p> <p>También puede agregar un componente de panel desde la barra de herramientas del panel principal mediante el botón <span class="uicontrol">Agregar panel secundario</code> botón. |Del mismo modo, puede agregar una barra de herramientas específica de un panel mediante el botón <span class="uicontrol">Agregar barra de herramientas del panel</code> botón. Puede configurar la posición de la barra de herramientas del panel mediante el cuadro de diálogo Editar panel.</p> </td>
  </tr>
  <tr>
   <td>Cuadro de contraseña</td>
   <td>Agrega un campo para capturar una contraseña.</td>
  </tr>
  <tr>
   <td>Botón Anterior</td>
   <td>Agrega un botón que los usuarios necesitan para volver a la página o panel anterior.</td>
  </tr>
  <tr>
   <td>Botón de opción</td>
   <td>Agrega botones de radio.</td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Agrega un botón para restablecer los campos del formulario.</td>
  </tr>
  <tr>
   <td>Botón Guardar</td>
   <td>Agrega un botón para guardar los datos del formulario.</td>
  </tr>
  <tr>
   <td>Firma manuscrita</td>
   <td>Agrega un campo para capturar firmas manuscritas.</td>
  </tr>
  <tr>
   <td>Separador</td>
   <td>Habilita la segregación visual de paneles en el formulario.</td>
  </tr>
  <tr>
   <td>Paso de firma</td>
   <td>Muestra la información proporcionada en el formulario y los campos de firma para que el usuario compruebe y firme el formulario.</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>Especificar texto estático.</td>
  </tr>
  <tr>
   <td>Botón Enviar</td>
   <td>Agrega un botón de envío para enviar el formulario a la acción de envío configurada.</td>
  </tr>
  <tr>
   <td>Paso de resumen</td>
   <td>Envía el formulario y muestra el texto de resumen que especifican los autores tras enviarlo. </td>
  </tr>
  <tr>
   <td>Interruptor</td>
   <td>Agrega un interruptor que realiza una acción de conmutación o de habilitar/deshabilitar. No se pueden agregar más de dos opciones en el componente Interruptor. Dado que un interruptor solo puede tener dos valores: Encendido o Apagado, la obligatoriedad no es aplicable. Se guarda al menos un valor independientemente de la entrada del usuario. <br /> </td>
  </tr>
  <tr>
   <td>Tabla</td>
   <td>Agrega una tabla que le permite organizar los datos en filas y columnas. </td>
  </tr>
  <tr>
   <td>Teléfono</td>
   <td><p>Agrega un campo para capturar el número de teléfono. El componente Teléfono permite a los autores configurar uno de los siguientes tipos de números de teléfono. Cada tipo está asociado con una expresión regular predeterminada para la validación.</p>
    <ul>
     <li>La validación del tipo internacional la realiza <code>^[+][0-9]{0,14}$</code>.</li>
     <li>La validación del tipo USPhoneNumber la realiza <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>La validación del tipo UKPhoneNumber la realiza <code>text{'+'99 999 999 9999}</code>.</li>
     <li>El tipo personalizado no proporciona ningún patrón de validación predeterminado. Toma el valor del último tipo de número de teléfono seleccionado. También puede especificar su propio patrón de validación personalizado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Términos y condiciones<br /> </td>
   <td>Agrega un campo que los autores pueden utilizar para especificar los términos y condiciones que deben revisar los usuarios antes de rellenar el formulario.</td>
  </tr>
  <tr>
   <td>Cuadro de texto </td>
   <td><p>Agrega un cuadro de texto en el que un usuario puede especificar la información necesaria. </p> <p>De forma predeterminada, el componente Cuadro de texto solo acepta texto sin formato. Puede habilitar un componente Cuadro de texto para que acepte texto enriquecido. Un componente de texto enriquecido permite agregar encabezados, cambiar estilos de caracteres (negrita, cursiva, subrayado de caracteres), crear listas ordenadas y sin ordenar, cambiar el fondo y el color del texto y agregar hipervínculos. Para habilitar el texto enriquecido para un cuadro de texto, active la opción <strong>Permitir texto enriquecido</strong> en las propiedades del componente.</p> </td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Especifica un título para el formulario adaptable.</td>
  </tr>
  <tr>
   <td>Paso de verificación</td>
   <td><p>Agrega un marcador de posición para mostrar el formulario rellenado para la verificación del usuario.</p> <p><strong>Nota</strong>: Los formularios adaptables que contienen el componente Verificar no admiten usuarios anónimos. Además, no se recomienda utilizar el componente Verificar en un fragmento de formulario adaptable.</p> </td>
  </tr>
 </tbody>
</table>

#### Prácticas recomendadas para trabajar con componentes {#best-practices}

Estas son algunas de las prácticas recomendadas y los puntos clave que deben tenerse en cuenta a la hora de trabajar con componentes de formulario adaptable:

* Cada componente tiene propiedades asociadas que controlan su aspecto y su funcionalidad. Para configurar las propiedades de un componente, seleccione el componente y seleccione ![cmppr](assets/cmppr.png) para abrir las propiedades del componente en el Explorador de propiedades.
* Cada componente se identifica con su nombre de elemento. Al seleccionar ![cmppr](assets/cmppr.png), puede cambiar el nombre del componente cambiando el valor del campo **[!UICONTROL Nombre del elemento]** en el explorador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permite ningún otro tipo de caracteres especiales, y el nombre del elemento debe comenzar con una letra.

* Puede modificar la propiedad Título de los componentes en línea de un formulario adaptable en el Editor de formularios sin abrir el Explorador de propiedades siempre que el título esté visible en el formulario. Para ello:

   1. Seleccione para seleccionar un componente que tenga la propiedad **[!UICONTROL Título]** y cuya propiedad **[!UICONTROL Ocultar título]** esté deshabilitada.

   1. Seleccione ![aem_6_3_edit](assets/aem_6_3_edit.png) para poder editar el título.

   1. Modifique el título y seleccione la tecla Retroceso o seleccione en cualquier sitio fuera del componente para guardar los cambios.  Seleccione la tecla Esc para descartar los cambios.

* Algunos componentes de los formularios adaptables, como Correo electrónico y Teléfono, incluyen patrones de validación listos para usar. Sin embargo, puede especificar una validación personalizada actualizando el campo **[!UICONTROL Patrón de validación]** en el acordeón Patrones de las propiedades del componente. Consulte las descripciones de componentes de la tabla anterior para obtener más información sobre las validaciones predeterminadas.

* Los campos de formulario adaptable, como Cuadro numérico y Correo electrónico, se pueden configurar para incluir tipos de entrada HTML5 especializados. Cuando estos campos están enfocados en dispositivos móviles y tabletas, el teclado muestra inicialmente el alfabeto, los números y los caracteres específicos que se utilizan normalmente para introducir información en los campos. Esto permite a los usuarios introducir la información rápidamente sin tener que alternar entre conjuntos de caracteres en el teclado. Para permitir entradas especializadas en un componente, active la casilla de verificación **[!UICONTROL Usar número de tipo HTML]** en las propiedades de ese componente.

* Puede habilitar un componente Cuadro de texto para que acepte texto enriquecido. Para habilitar el texto enriquecido en un cuadro de texto, active la casilla de verificación **[!UICONTROL Permitir texto enriquecido]** en las propiedades del componente.

* Puede activar los componentes Cuadro de texto, Correo electrónico y Teléfono para rellenar automáticamente los valores de campos como Nombre, Dirección, Tarjeta de crédito, Teléfono y Correo electrónico a partir de la información almacenada en la configuración de relleno automático del explorador. Para habilitar esta función, seleccione **[!UICONTROL Habilitar relleno automático]** en las propiedades del componente y seleccione un **[!UICONTROL atributo de relleno automático]**. Cuando un usuario cumplimenta un formulario adaptable, los valores se sugieren desde el perfil de relleno automático del explorador o se basan en los valores rellenados anteriormente por el usuario. Tenga en cuenta que el relleno automático funciona si la configuración de relleno automático está activada en el explorador del usuario.

* Especifique valores para los elementos de Botón de opción y Casilla de verificación en el formato `{value}={text}` desde las propiedades de los componentes.
* De forma predeterminada, el componente Archivo adjunto permite al usuario adjuntar un único archivo. Sin embargo, puede configurar las propiedades del componente para que admita varios archivos adjuntos. Además, si un usuario adjunta varios archivos con el mismo nombre de archivo, los archivos adjuntos pueden causar algunos problemas. Por lo tanto, se recomienda asociar un identificador único a cada archivo adjunto enviado cuando se envía el formulario. Para ello:

   1. En el servidor de AEM Forms, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
   1. Busque y seleccione **[!UICONTROL Servicio de configuración de formularios adaptables]**.
   1. En el cuadro de diálogo Servicio de configuración de formularios adaptables, active la opción **[!UICONTROL Asignar nombres de archivo únicos]**. De forma predeterminada, está desactivada.

* Para permitir que los usuarios adjunten un PDF mediante el explorador Safari, asegúrese de que agrega **aplicación/pdf** a la propiedad Tipos de archivo compatibles del componente Archivo adjunto. Los formularios adaptables creados con versiones anteriores de AEM Forms pueden contener **.pdf** en lugar de **aplicación/pdf** en la propiedad Tipos de archivo compatibles.

Para conocer las prácticas recomendadas en los formularios adaptables, consulte [Prácticas recomendadas para usar formularios adaptables](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.

### Barra de herramientas de la página {#page-toolbar}

La barra de herramientas de la parte superior de la página ofrece opciones que permiten obtener una vista previa del formulario, cambiar las propiedades del formulario y editar el diseño del formulario. Puede obtener una vista previa del formulario cuando lo cree y realizar los cambios correspondientes. En la barra de herramientas de la página, verá lo siguiente:

* **Alternar panel lateral** ![toggle-side-panel](assets/toggle-side-panel.png): permite mostrar u ocultar la barra lateral.

* **Información de la página** ![theme-options](assets/theme-options.png): Permite ver las propiedades de página, publicar o cancelar la publicación de un formulario, iniciar un flujo de trabajo de un formulario y abrir el formulario en la IU clásica.

* **Emulador** ![regla](assets/ruler.png): Permite emular el aspecto del formulario para diferentes tamaños de visualización, como tabletas y teléfonos.

* **Editar**: Permite seleccionar otros modos, como: **[!UICONTROL Editar]**, **[!UICONTROL Estilo]**, **[!UICONTROL Desarrollador]** y **[!UICONTROL Diseño]**.

   * **Editar**: Permite editar las propiedades del formulario y sus componentes. Por ejemplo, agregar un componente, soltar una imagen y especificar campos obligatorios.
   * **Estilo**: Permite aplicar estilo al aspecto de los componentes del formulario. Por ejemplo, en el modo Estilo, puede seleccionar un panel y especificar su color de fondo.

   * **Desarrollador**: Permite a un desarrollador lo siguiente:

      * Descubrir de qué se componen los formularios.
      * Depurar lo que sucede, dónde y cuándo, lo que a su vez ayuda a resolver problemas.

   * **Diseño**. Permite habilitar o deshabilitar componentes personalizados o componentes integrados que no aparecen en la barra lateral.

* **Vista previa**: Permite obtener una vista previa del aspecto del formulario cuando se publica.

### Barra de herramientas de los componentes {#component-toolbar}

![Barra de herramientas de componentes en la IU táctil](assets/component-toolbar.png)

Al seleccionar un componente, aparece una barra de herramientas que le permite trabajar con él. Puede obtener opciones para cortar, pegar, mover y especificar propiedades de los componentes. Las opciones son las siguientes:

A.**Configurar**: al seleccione **[!UICONTROL Configurar]**, las propiedades de los componentes se pueden ver en la barra lateral.  La configuración de estas propiedades permite personalizar la experiencia de captura de datos. Puede cambiar el nombre del elemento del componente, especificar el texto de la etiqueta en el campo Título del componente. El nombre del elemento permite capturar los valores que introducen los usuarios mediante el componente. En las propiedades del componente, se especifica el comportamiento del componente y se administran los datos que haya introducido el usuario. Configure las propiedades en la barra lateral para capturar los datos de usuario y utilizarlos en un procesamiento posterior. Las propiedades del contenedor de formularios adaptables permiten especificar la configuración de las bibliotecas de cliente, los diseños, los temas, los documentos de registro, las opciones de guardado, los envíos y los metadatos.

B.**Copiar**: Puede utilizar la opción Copiar para copiar un componente y pegarlo en otros lugares del formulario. Al pegar un componente, este recibirá un nombre de elemento nuevo, pero conservará las propiedades del componente copiado.

C.**Cortar**: Puede utilizar la opción Cortar para mover un componente de un lugar a otro en el formulario adaptable.

D. **Eliminar**: Permite eliminar un componente del formulario.

E. **Insertar**: Permite insertar un componente sobre el componente seleccionado.

F. **Pegar**: Permite pegar el componente cortado o copiado mediante las opciones descritas anteriormente.

G. **Editar reglas**: Permite abrir el editor de reglas. Para obtener más información, consulte [Editor de reglas](../../forms/using/rule-editor.md).

H. **Grupo**: Permite seleccionar varios componentes si desea cortar, copiar o pegar más de un componente a la vez.

I. **Principal**: Permite seleccionar el elemento principal de un componente. Por ejemplo, un campo de texto se encuentra dentro de una subsección, que reside en una sección. La sección se encuentra en el panel raíz de la guía, y el contenedor del formulario adaptable es el elemento principal del panel raíz. Puede ver todas las opciones de un componente con la jerarquía ordenada en la parte inferior.

Por ejemplo, si selecciona **[!UICONTROL Principal]** en un cuadro de texto, podrá ver lo siguiente:

* Subsección
* Sección
* guideRootPanel
* Contenedor del formulario adaptable

J. **Otros**: Proporciona más opciones para trabajar con el componente seleccionado.

* Ver expresión SOM
* Guardar panel como fragmento (solo para paneles)
* Agregar panel secundario (solo para paneles)
* Agregar barra de herramientas del panel (solo para paneles)
* Reemplazar (excepto para paneles)

### Página de formulario adaptable {#af-page}

La página del formulario adaptable es el formulario real. Es como cualquier otra página WCM modelada como componente WCM `cq:Page`. La siguiente imagen muestra la estructura del contenido de un formulario adaptable tradicional.

![Estructura del contenido de la página WCM de un formulario adaptable](assets/afstructure.png)

La estructura del contenido suele contener los siguientes componentes principales:

* **guideContainer**: La raíz de un formulario adaptable, que se marca como el **[!UICONTROL Inicio del formulario adaptable]** en la interfaz de usuario del formulario. En este componente, puede especificar lo siguiente:

   * *Diseño móvil del formulario adaptable*: Define el aspecto del formulario en dispositivos móviles.
   * *Página de agradecimiento*: Define la página a la que se redirige al usuario después de enviar el formulario.
   * *Enviar acción*: Define cómo se procesa el formulario en el servidor una vez que el usuario lo envía.
   * *Estilo*: Especifica la ruta al archivo CSS utilizado para personalizar el aspecto del formulario.

* **rootPanel:** El panel raíz de un formulario adaptable. Puede contener subpaneles bajo el nodo de elementos. Cada panel, incluido el panel raíz, puede tener un diseño asociado. El diseño del panel dicta cómo se coloca el formulario. Por ejemplo, en el diseño Acordeón, los elementos se muestran como pasos de Acordeón.

* **barra de herramientas:** Un contenedor de formulario adaptable tiene asociada una barra de herramientas global que es global para el formulario. Esta barra de herramientas se puede agregar mediante la acción **[!UICONTROL Agregar barra de herramientas]** en la barra de edición, que permite a los autores agregar acciones, como Enviar, Guardar, Restablecer, etc.

* **recursos:** Este nodo contiene información adicional utilizada para la creación de formularios. Por ejemplo, detalles del modelo del formulario, detalles de localización, etc).
