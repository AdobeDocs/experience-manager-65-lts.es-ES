---
title: Crear una comunicación interactiva
description: Cree una comunicación interactiva con el editor de comunicaciones interactivas. Utilice la funcionalidad de arrastrar y soltar para crear la comunicación interactiva y previsualizar las salidas de impresión y web en diferentes tipos de dispositivos.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '6130'
ht-degree: 83%

---

# Crear una comunicación interactiva{#create-an-interactive-communication}

## Información general {#overview}

Comunicaciones interactivas centraliza y administra la creación, la combinación y la entrega de correspondencia personalizada e interactiva. Utilice la impresión como canal maestro para la web, puede minimizar la duplicación de esfuerzos al crear la salida web de la comunicación interactiva.

### Requisitos previos {#prerequisites}

Los siguientes son los requisitos previos para crear una comunicación interactiva:

* Configure un [Modelo de datos de formulario](/help/forms/using/data-integration.md) que contenga datos de prueba o una fuente de datos real, como una instancia de Microsoft® Dynamics.
* Asegúrese de tener los [Fragmentos de documento](/help/forms/using/document-fragments.md).
* Asegúrese de que tiene [Plantillas para impresión y canal Web](/help/forms/using/web-channel-print-channel.md).
* Asegúrese de que dispone de la [temática](/help/forms/using/themes.md) necesario para el canal Web.

## Crear comunicación interactiva {#createic}

1. Inicie sesión en la instancia de autor de AEM y navegue hasta **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Comunicación interactiva]**. Aparecerá la página Crear comunicación interactiva.

   ![create-interactive-communication](assets/create-interactive-communication.png)

1. Especifique la siguiente información. :

   * **[!UICONTROL Título]**: escriba el título de la comunicación interactiva.
   * **[!UICONTROL Nombre]**: el nombre de la comunicación interactiva se derivará del título que escriba. Edítela si es necesario.
   * **[!UICONTROL Descripción]**: escriba una descripción sobre la comunicación interactiva.
   * **[!UICONTROL Modelo de datos de formulario]**: busque y seleccione el modelo de datos de formulario. Para obtener más información sobre el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](/help/forms/using/data-integration.md).

   * **[!UICONTROL Servicio de rellenado previo]**: seleccione el servicio de rellenado previo para recuperar los datos y rellenar previamente la comunicación interactiva.
   * **[!UICONTROL Tipo de proceso posterior]**: puede seleccionar habilitar AEM o flujo de trabajo de Forms cuando se envíe la comunicación interactiva. Seleccione el tipo de flujo de trabajo que desea activar.

   * **[!UICONTROL Proceso posterior]**: seleccione el nombre del flujo de trabajo que desea activar. Cuando seleccione el flujo de trabajo de AEM, proporcione una ruta de datos adjuntos, una ruta de diseño, una ruta del PDF, una ruta de datos de impresión y una ruta de datos web.
   * **[!UICONTROL Etiquetas]**: seleccione las etiquetas que desea aplicar a la comunicación interactiva. También puede escribir un nombre de etiqueta nuevo/personalizado y pulsar Entrar para crearlo.
   * **[!UICONTROL Autor]**: el nombre del autor se toma automáticamente del nombre de usuario que ha iniciado sesión.
   * **[!UICONTROL Fecha de publicación:]** escriba la fecha de publicación de la comunicación interactiva.
   * **[!UICONTROL Cancelar publicación]**: escriba la fecha para cancelar la publicación de la comunicación interactiva.

1. Seleccione **[!UICONTROL Siguiente]**. Aparecerá la pantalla para especificar los detalles de los canales web y de impresión.
1. Escriba lo siguiente:

   * **[!UICONTROL Imprimir]**: seleccione esta opción para generar el canal Imprimir de la comunicación interactiva.
   * **[!UICONTROL Imprimir plantilla]**: busque y seleccione un XDP como plantilla de impresión.
   * **[!UICONTROL Web]**: seleccione esta opción para generar el canal Web o la salida interactiva de la comunicación interactiva.
   * **[!UICONTROL Plantilla web de comunicación interactiva]**: busque y seleccione la plantilla web.
   * **[!UICONTROL Temática]** y **[!UICONTROL Seleccionar tema]**: busque y seleccione la temática para aplicar un estilo al canal Web de la comunicación interactiva. Para obtener más información, consulte [Temáticas en AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Usar Imprimir como principal para el canal Web]**: seleccione esta opción para crear el canal Web sincronizado con el canal Imprimir. El uso del canal Imprimir como principal para el canal Web garantiza que el contenido y el enlace de datos del canal Web se deriven del canal Imprimir y que los cambios realizados en este se reflejen en el canal Web al seleccionar Sincronizar. Sin embargo, se permite a los autores romper la herencia de componentes específicos del canal Web, según sea necesario. Para obtener más información, consulte [Sincronizar el canal Web con el canal Imprimir](../../forms/using/create-interactive-communication.md#synchronize).
Si selecciona la opción **[!UICONTROL Usar Imprimir como principal para el canal Web]**, puede seleccionar cualquiera de los siguientes modos para generar el canal Web:

      * **[!UICONTROL Diseño automático]**: seleccione este modo para generar automáticamente marcadores de posición, contenido y enlaces de datos para el canal Web desde el canal Imprimir.
      * **[!UICONTROL Organizar manualmente]**: seleccione este modo para seleccionar manualmente los elementos del canal Imprimir y agregarlos al canal Web mediante el contenido principal disponible en la pestaña **[!UICONTROL Fuentes de datos]**. Para obtener más información, consulte [Seleccionar Imprimir elementos de canal para crear contenido de canal Web](#selectprintchannelelements).

   Para obtener más información sobre el canal Imprimir y el canal Web, consulte [Canal de impresión y canal Web](/help/forms/using/web-channel-print-channel.md).

1. Seleccione **[!UICONTROL Crear]**. Se creará la comunicación interactiva y aparecerá un cuadro de alerta. Seleccione **[!UICONTROL Editar]** para empezar a crear el contenido de la comunicación interactiva, tal como se explica en [Agregar contenido mediante la interfaz de usuario de creación de comunicaciones interactivas](#step2). También puede seleccionar **[!UICONTROL Listo]** y elegir editar la comunicación interactiva más adelante.

## Agregar contenido a la comunicación interactiva {#step2}

Después de crear una comunicación interactiva, puede utilizar la interfaz de creación de comunicaciones interactivas para crear su contenido.

Para obtener más información sobre la interfaz de creación de comunicaciones interactivas, consulte [Introducción a la creación de comunicaciones interactivas](/help/forms/using/introduction-interactive-communication-authoring.md).

1. La interfaz de creación de comunicaciones interactivas se inicia al seleccionar Editar como se menciona en [Crear comunicación interactiva](#createic). También puede navegar hasta un recurso de comunicación interactiva existente en AEM, seleccionarlo y seleccionar **[!UICONTROL Editar]** para iniciar la interfaz de creación de comunicaciones interactivas.

   De forma predeterminada, aparecerá el canal Imprimir de la comunicación interactiva, a menos que esta sea solo de canal Web. El canal Imprimir de la comunicación interactiva muestra las áreas de destino, tal como están disponibles en la plantilla de canal Imprimir/XDP seleccionada. En estas áreas y campos de destino, puede agregar componentes o recursos.

1. Con el canal Imprimir seleccionado, seleccione la pestaña **[!UICONTROL Componentes]**. Los siguientes componentes están disponibles en el canal Imprimir:

   | **Componente** | **Funcionalidad** |
   |---|---|
   | Gráfico | Agrega un gráfico que se puede usar en comunicaciones interactivas para la representación visual de datos bidimensionales recuperados de una colección de modelos de datos de formulario. Para obtener más información, consulte [Usar gráficos en comunicaciones interactivas](/help/forms/using/chart-component-interactive-communications.md). |
   | Fragmento de documento | Permite agregar un componente reutilizable, como texto, lista o condición, a una comunicación interactiva. El componente agregado puede estar basado en el modelo de datos de formulario o no. |
   | Imagen | Insertar una imagen. |

   Arrastre y suelte los componentes en la comunicación interactiva y configúrelos según sea necesario.

   También puede utilizar las operaciones de deshacer y rehacer mientras crea una comunicación interactiva para los canales de impresión y web.

   Utilice la operación de deshacer para descartar la última acción realizada y la operación de rehacer para incorporar de nuevo la acción descartada. Por ejemplo, si ha insertado una imagen o ha creado un enlace de datos en una comunicación interactiva y necesita descartarlo, utilice la operación Deshacer.

   ![Acciones Deshacer y Rehacer &#x200B;](assets/undo_redo_actions_new.png)

   Las opciones Deshacer y Rehacer se muestran en la barra de herramientas de la página de la interfaz de usuario de creación. La opción Deshacer solo se muestra después de realizar una acción. La opción Rehacer se muestra en la barra de herramientas de la página solo después de realizar una operación de deshacer. Estas acciones se restablecen al actualizar la página.

1. Con el canal Imprimir seleccionado, vaya a la pestaña **[!UICONTROL Recursos]** y aplique el filtro para mostrar solo los recursos que desee ver.

   Con el explorador de recursos, también puede arrastrar y soltar recursos directamente en las áreas de destino de comunicaciones interactivas.

   ![assets-docfragments](assets/assets-docfragments.png)

1. Arrastre y suelte los fragmentos del documento en la comunicación interactiva. A continuación se muestran los tipos de fragmentos de documento que puede utilizar en el canal Imprimir de comunicaciones interactivas.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de fragmento de documento</strong></td>
   <td><strong>Ejemplo de propósito</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Texto</a></td>
   <td>Texto para agregar la dirección, el correo electrónico del destinatario y el texto del cuerpo de la carta </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Condición</a></td>
   <td>Condición para agregar la imagen de encabezado adecuada a la comunicación en función del tipo de directiva: Standard o Premium. <br /> </td>
  </tr>
  <tr>
   <td>Lista</td>
   <td>Grupo de fragmentos de documento, incluidos texto, condiciones, otras listas e imágenes. <br /> </td>
  </tr>
 </tbody>
</table>

También puede reemplazar el enlace entre un área de destino y un fragmento de documento si suelta el nuevo fragmento en el área de destino mediante la pestaña **[!UICONTROL Recursos]**. El sombreado de color azul del área de destino mientras arrastra el fragmento indica que el fragmento del documento se puede soltar en el área de destino.

Para obtener más información sobre los fragmentos de documento, consulte [Fragmentos de documento](/help/forms/using/document-fragments.md).

La interfaz de creación permite distinguir entre los campos independientes y enlazados y las variables dentro de una comunicación interactiva. La interfaz resalta los campos y las variables independientes mediante un borde naranja.

![unbound_fields_variables_highlight_dc](assets/unbound_fields_variables_highlights_dc.jpg)

Además, cuando pasa el ratón sobre estos elementos, se muestra información del objeto con el mensaje Campo (sin enlazar) o Variable (sin enlazar).

Es posible que a veces no se muestre una variable independiente utilizada en un fragmento de documento en la interfaz de creación. Puede deberse a una regla de texto en línea dentro de un fragmento de documento o si hay un fragmento de condición. En estos casos, la información del objeto, resaltada en azul, se mostrará como parte del fragmento de documento. La información sobre herramientas muestra el número de variables independientes utilizadas dentro de un fragmento de documento.

![Variable sin enlazar &#x200B;](assets/df_unbound_variable_new.png)

Seleccione el fragmento de documento, seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y, a continuación, seleccione **[!UICONTROL Propiedades]** de la barra de tareas de la comunicación interactiva. La sección **[!UICONTROL Variables y objetos del modelo de datos]** enumera las variables, incluidas las variables ocultas y los objetos del modelo de datos utilizados en los fragmentos del documento. Utilice el icono ![editar](assets/edit.svg) (Editar) junto a cada objeto o variable del modelo de datos para editar las propiedades.

1. Para configurar el enlace de variables, seleccione una variable y seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y luego configure las propiedades del enlace en el panel Propiedades de la barra lateral.

   * **Ninguna**: el agente rellenará el valor de la variable.
   * **Fragmento de texto**: si está seleccionado, puede buscar y seleccionar un fragmento de documento de texto cuyo contenido se procese en el campo. Solo esos fragmentos de documento de texto pueden enlazarse a variables que no tengan variables dentro.
   * **Objeto de modelo de datos**: seleccione una propiedad del modelo de datos de formulario cuyo valor se rellene en el campo.
   * **Valor predeterminado:** puede definir un valor predeterminado para la variable mediante este campo. El valor se muestra al obtener una vista previa de la comunicación interactiva o en la interfaz de usuario de Agente.
   * **Patrón de visualización:** también puede definir un formato de visualización para una variable. Seleccione cualquiera de las opciones predefinidas en la lista desplegable **Tipo** para aplicar un formato de visualización a una variable. Seleccione **Personalizar** para definir un patrón de visualización que no esté disponible en la lista. Para obtener más información, consulte [Patrones de visualización de datos](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   Navegue hasta [Variables y objetos del modelo de datos](../../forms/using/create-interactive-communication.md#hiddenvariables) para configurar el enlace de variables ocultas en el fragmento de documento.

   También puede arrastrar y soltar elementos de la fuente de datos o fragmentos de documento de texto para configurar el enlace de variables. Para crear un enlace con cualquiera de los elementos de la fuente de datos, seleccione la pestaña **Fuentes de datos** y arrastre y suelte el elemento en el nombre de la variable. El elemento de la fuente de datos y la variable deben ser del mismo tipo para configurar el enlace correctamente. Si arrastra y suelta un elemento de fuente de datos en una variable ya enlazada, el nuevo elemento reemplazará al anterior para crear un enlace con la variable. Del mismo modo, seleccione la pestaña **Recursos** y arrastre y suelte el fragmento de documento de texto en el nombre de la variable para configurar el enlace entre ellos. El fragmento del documento de texto no debe contener ninguna variable.

1. Para agregar una tabla, con el canal Imprimir seleccionado, en la pestaña **[!UICONTROL Recursos]** aplique el filtro para mostrar solo los fragmentos de diseño. Arrastre y suelte el fragmento de diseño necesario en la comunicación interactiva. Un fragmento de diseño se basa en un XDP y se puede utilizar para crear diseños gráficos o tablas estáticas y dinámicas en comunicaciones interactivas que se rellenen con datos dinámicos.

   Ejemplo: Una tabla de diseño para mostrar la prima bruta, el descuento por fidelidad % y la disponibilidad de asistencia de emergencia en carretera para las directivas antiguas y nuevas.

   Para obtener más información sobre fragmentos de diseño, consulte [Fragmentos de documento](/help/forms/using/document-fragments.md).

1. Con el canal Imprimir seleccionado, en la pestaña **[!UICONTROL Recursos]** aplique el filtro para mostrar imágenes. Arrastre y suelte las imágenes necesarias en la comunicación interactiva, como el logotipo de la empresa.

   Además, administre lo siguiente en la comunicación interactiva:

   * [Agregar y configurar gráficos](/help/forms/using/chart-component-interactive-communications.md)
   * [Sincronizar el canal Web con el canal Imprimir](../../forms/using/create-interactive-communication.md#synchronize)

      * Sincronización automática
      * Cancelar herencia
      * Volver a habilitar la herencia
      * Sincronizar

   * [Archivos adjuntos y acceso a la biblioteca](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Propiedades del campo XDP/Diseño](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Agregar reglas a los componentes](../../forms/using/create-interactive-communication.md#rules)

1. Cambie a **[!UICONTROL Canal web]**. El canal Web aparecerá en el editor de comunicaciones interactivas. Cuando cambie del canal Imprimir al canal Web por primera vez, se producirá la sincronización automática. Para obtener más información, consulte [Sincronizar el canal Web desde el canal Imprimir](../../forms/using/create-interactive-communication.md#synchronize).

   Dado que en este ejemplo utilizamos Imprimir como principal para la web, los marcadores de posición del canal Imprimir el contenido y el enlace de datos se sincronizan con el canal Web. Sin embargo, puede cambiar y personalizar el contenido específico en el canal Web. [Cancele la herencia](#cancelinheritance) para las áreas de destino y las variables que se han generado mediante el canal Imprimir para poder personalizar el contenido.

   ![webchannelassets](assets/webchannelassets.png)

   Seleccione el fragmento de documento, seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y, a continuación, seleccione **[!UICONTROL Propiedades]** de la barra de tareas de la comunicación interactiva. La sección **[!UICONTROL Variables y objetos del modelo de datos]** enumera las variables, incluidas las variables ocultas y los objetos del modelo de datos utilizados en los fragmentos del documento. Utilice el icono ![editar](assets/edit.svg) (Editar) junto a cada objeto o variable del modelo de datos para editar las propiedades. Además, para los fragmentos de documento que se han [generado automáticamente](#synchronize) en el canal Web mediante el canal Imprimir utilice el icono ![cancelinheritance](assets/cancelinheritance.png) (Cancelar herencia) junto a cada objeto del modelo de datos y variable para [cancelar la herencia](#cancelinheritance) y poder editarlas.

1. Para agregar componentes adicionales al canal Web, con el canal Web seleccionado, seleccione **[!UICONTROL Componentes]**. Arrastre y suelte los componentes en el canal Web de la comunicación interactiva según sea necesario y proceda a configurarlos.

   | Componentes | Funcionalidad |
   |---|---|
   | Gráfico | Agrega un gráfico que se puede usar en comunicaciones interactivas para la representación visual de datos bidimensionales recuperados de una colección de modelos de datos de formulario. Para obtener más información, consulte [Usar el componente de gráfico](../../forms/using/chart-component-interactive-communications.md). |
   | Fragmento de documento | Permite agregar un componente, un texto, una lista o una condición reutilizables a una comunicación interactiva. El componente reutilizable que agregue a una comunicación interactiva puede estar basado en el modelo de datos de formulario o carecer de él. |
   | Imagen | Insertar una imagen. |
   | Panel | Le permite agregar un [panel](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) a la comunicación interactiva. |
   | Tabla | Agrega una tabla que le permite organizar los datos en filas y columnas. |
   | Área de destino | Inserta un área de destino en un canal web para organizar los componentes específicos de ese canal. El área de destino es un contenedor sin formato que le permite agrupar componentes específicos de canales web. |
   | Texto | Agrega texto enriquecido al canal Web de una comunicación interactiva. El texto también puede utilizar objetos del modelo de datos de formulario para hacer que el contenido sea dinámico. |
   | Botón | Le permite agregar un [botón](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) a la comunicación interactiva. Puede utilizar el componente Botón para navegar hasta otras comunicaciones interactivas, formularios adaptables, otros recursos como imágenes o fragmentos de documento o una URL externa. |
   | Separador | Permite insertar una línea horizontal dentro de una comunicación interactiva. Utilice este componente para distinguir entre secciones de una correspondencia. Por ejemplo, puede utilizar el componente Separador para distinguir entre las secciones Detalles del cliente y Detalles de la tarjeta de crédito en una instrucción de tarjeta de crédito. |

1. Si es necesario, inserte recursos en el canal Web.

   Puede [previsualizar la comunicación interactiva](#previewic) para ver el aspecto de las salidas de impresión y web de la comunicación interactiva y aplicar los cambios necesarios.

## Previsualizar la comunicación interactiva {#previewic}

Puede usar la **Opción de previsualización** para evaluar la apariencia de la comunicación interactiva. El canal Web de comunicaciones interactivas también ofrece la opción de emular la experiencia de una comunicación interactiva para varios dispositivos. Por ejemplo, iPhone, iPad y escritorio. Puede usar ambas reglas, **Vista previa** y **Emulador** ![regla](assets/ruler.png) junto con otras opciones para obtener una vista previa de las salidas web para dispositivos con diferentes tamaños de pantalla. Los datos de ejemplo de la vista previa se rellenan desde el modelo de datos de formulario especificado.

1. Seleccione el canal (de impresión o web) para obtener una vista previa y seleccione Previsualizar. Aparecerá la comunicación interactiva.

   >[!NOTE]
   >
   >La vista previa se rellenará con los datos de ejemplo del modelo de datos de formulario especificado. Para obtener más información sobre la vista previa de la comunicación interactiva con otros datos o el uso del servicio de rellenado previo, consulte [Usar el modelo de datos de formulario](/help/forms/using/using-form-data-model.md) y [Trabajar con el modelo de datos de formulario](/help/forms/using/work-with-form-data-model.md).

1. Para el canal Web, utilice ![reglas](assets/ruler.png) para ver el aspecto de la comunicación interactiva en varios dispositivos.

   ![webchannelpreview](assets/webchannelpreview.png)

Además, puede [Preparar y enviar comunicaciones interactivas mediante la interfaz de usuario de Agente](/help/forms/using/prepare-send-interactive-communication.md).

## Configurar propiedades en la comunicación interactiva  {#configure-properties-in-interactive-communication}

### Archivos adjuntos y acceso a la biblioteca {#attachmentslibrary}

En el canal Imprimir, puede configurar los archivos adjuntos y el acceso a la biblioteca para permitir que el agente administre los archivos adjuntos en la interfaz de usuario de Agente para la comunicación interactiva:

1. En el canal Imprimir, resalte el contenedor de documentos y seleccione **Propiedades**.

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   El panel Propiedades aparecerá en la barra lateral.

   ![propertiesattachments](assets/propertiesattachments.png)

1. Expanda los **Archivos adjuntos** y especifique las siguientes propiedades:

   * **[!UICONTROL Permitir acceso a la biblioteca]**: seleccione esta opción para habilitar el acceso a la biblioteca al agente en la interfaz de usuario de Agente. Si está activada, el agente podrá agregar archivos de la biblioteca mientras prepara la comunicación interactiva.
   * **[!UICONTROL Permitir reordenar archivos adjuntos]**: seleccione esta opción para permitir que el agente vuelva a ordenar los archivos adjuntos con la comunicación interactiva.
   * **[!UICONTROL Número máximo de archivos adjuntos permitidos]**: especifique el número máximo de archivos adjuntos permitidos con la comunicación interactiva.
   * **[!UICONTROL Archivos que se adjuntarán]**: seleccione **[!UICONTROL Agregar]**, busque los archivos que desea adjuntar y especifique lo siguiente:

      * **[!UICONTROL Adjuntar este archivo al documento de forma predeterminada]**: puede cambiar esta opción solo si el archivo adjunto no es obligatorio.
      * **[!UICONTROL Obligatorio:]** el agente no podrá quitar el archivo adjunto en la interfaz de usuario de Agente.

   ![attachfiles](assets/attachfiles.png)

1. Seleccione **[!UICONTROL Listo]**.

### Propiedades del campo XDP/Diseño {#xdplayoutfieldproperties}

1. Al editar el canal Imprimir de una comunicación interactiva, pase el ratón sobre un campo creado en la plantilla del canal Imprimir y seleccione ![configure_icon](assets/configure_icon.png) (Configurar).

   El cuadro de diálogo Propiedades aparecerá en la barra lateral.

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. Especifique lo siguiente:

   * **[!UICONTROL Nombre]**: nombre del nodo JCR.
   * **[!UICONTROL Título]**: escriba un título que sea visible para el agente en la interfaz de usuario de Agente y en el árbol del contenedor de documentos.
   * **[!UICONTROL Tipo de enlace]**: seleccione uno de los siguientes tipos de enlace para el campo.

      * Ninguno: el agente rellenará el valor de la propiedad.
      * Fragmento de texto: si está seleccionado, puede buscar y seleccionar un fragmento de documento de texto cuyo contenido se procese en el campo. También puede arrastrar y soltar el fragmento de documento de texto en el nombre del campo para configurar el enlace entre ellos. El fragmento del documento de texto no debe contener ninguna variable.
      * Objeto del modelo de datos: seleccione una propiedad del modelo de datos de formulario cuyo valor se rellene en el campo. Como alternativa, seleccione la pestaña **Fuentes de datos** y arrastre y suelte la propiedad en el campo.

   * **[!UICONTROL Valores predeterminados]**: el valor predeterminado garantiza que el campo no esté vacío cuando no haya ningún valor proporcionado por el objeto del modelo de datos especificado o el fragmento de texto. Si el tipo de enlace de datos es Ninguno, el valor predeterminado se rellenará previamente en el campo.
   * **[!UICONTROL Patrón de visualización]**: también puede definir un formato de visualización para un campo. Seleccione cualquiera de las opciones predefinidas en la lista desplegable **Tipo** para aplicar un formato de visualización a un campo. Seleccione **Personalizar** para definir un patrón de visualización que no esté disponible en la lista. Para obtener más información, consulte [Patrones de visualización de datos](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Editable por el agente]**: seleccione esta opción para permitir que el agente edite el valor en el campo de la interfaz de usuario de Agente. Esta configuración no es aplicable si el tipo de enlace es un fragmento de texto.
   * **[!UICONTROL Etiqueta]**: especifique una cadena de texto que se muestre con el campo al agente en la interfaz de usuario de Agente. Esta configuración no es aplicable si el tipo de enlace es un fragmento de texto.
   * **[!UICONTROL Información del objeto]**: escriba una cadena de texto que sea visible al pasar el ratón por encima del agente en la interfaz de usuario de Agente. Esta configuración no es aplicable si el tipo de enlace es un fragmento de texto.
   * **[!UICONTROL Obligatorio]**: seleccione esta opción para que el campo sea obligatorio para el agente. Esta configuración no es aplicable si el tipo de enlace es un fragmento de texto.
   * **[!UICONTROL Permitir varias líneas]**: seleccione este campo para permitir varias líneas de texto como entrada en el campo. Esta configuración no es aplicable si el tipo de enlace es un fragmento de texto.

1. Seleccione ![done_icon](assets/done_icon.png).

### Patrones de visualización de datos {#datadisplaypatterns}

La interfaz de creación permite definir patrones de visualización de datos para campos, variables y elementos del modelo de datos de formulario disponibles al crear una comunicación interactiva para canales web y de impresión.

Para configurar el patrón de visualización de datos, seleccione el elemento, seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y configure el patrón de visualización en el panel **[!UICONTROL Propiedades]** de la barra lateral. Seleccione cualquier opción predefinida en la lista desplegable **[!UICONTROL Tipo]** para ver el patrón asociado al tipo seleccionado. Seleccione **[!UICONTROL Personalizar]** de la lista desplegable **[!UICONTROL Tipo]** para definir un patrón que no esté disponible en la lista. Editar valores en el campo **[!UICONTROL Patrón]** modifica automáticamente el tipo a **[!UICONTROL Personalizado]**.

Para aplicar el patrón de visualización, el número de caracteres o dígitos definidos en el campo Patrón debe coincidir o superar los caracteres o dígitos definidos en el valor de los campos, variables y elementos del modelo de datos de formulario. Para obtener más información, consulte [ejemplo](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

Puede redefinir el patrón de visualización de un campo, variable o elemento del modelo de datos de formulario después de generar contenido web a partir del canal Imprimir. Como resultado, un elemento puede tener diferentes patrones de visualización definidos para los canales web y de impresión. Si no define un patrón de visualización para un elemento del canal Imprimir y genera automáticamente contenido web mediante el canal Imprimir, el enlace de datos definido para el elemento en el canal Imprimir definirá las opciones de patrón de visualización disponibles en la lista desplegable **[!UICONTROL Tipo]**. Si no hay ningún enlace definido para el elemento, el tipo de datos del elemento define las opciones disponibles del patrón de visualización. Por ejemplo, si crea un enlace de datos del tipo Número para un elemento del canal Imprimir, las opciones del patrón de visualización disponibles en la lista desplegable **[!UICONTROL Tipo]** serán de tipo Número en varios formatos.

Cambie al modo **Vista previa** o abra la interfaz de usuario de Agente para ver el patrón de visualización aplicado a estos elementos.

En la siguiente tabla se muestra un ejemplo de los valores que se muestran como resultado de la configuración del patrón de visualización de datos para una variable:

| Tipo | Valor predeterminado | Patrón de visualización | Mostrar valor | Descripción |
|---|---|---|---|---|
| SocialSecurityNumber | 123456789 | text{999-99-9999} | 123-45-6789 | El número de dígitos del campo de valor predeterminado coincide con el número de dígitos del campo Patrón. El valor basado en el patrón se muestra correctamente. |
| SocialSecurityNumber | 1234567 | text{999-99-9999} | 1-23-4567 | El número de dígitos del campo de valor predeterminado es menor que el número de dígitos del campo Patrón. El patrón se aplica a los siete dígitos disponibles. |
| SocialSecurityNumber | 1234567890 | text{999-99-9999} | 1234567890 | El número de dígitos del campo de valor predeterminado es mayor que el número de dígitos del campo Patrón. Como resultado, no hay ningún cambio en el valor de visualización. |

Si no se especifica un patrón de visualización para una variable o un elemento del modelo de datos de formulario, la [configuración global de fragmentos de documento](https://helpx.adobe.com/es/experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) se utiliza de forma predeterminada.

Si no se aplica un patrón de visualización a una variable de tipo de datos numérico, la vista previa de impresión mostrará el patrón según la configuración global del fragmento del documento. Si aplica cambios a la configuración del fragmento de documento global predeterminada, la interfaz de usuario de Agente aún mostrará el patrón según los separadores predeterminados definidos para la configuración regional.

Del mismo modo, para los campos, si no se especifica el patrón de visualización, se aplicará al campo el patrón definido al crear la plantilla de impresión (XDP). Si no hay ningún patrón al crear la plantilla de impresión, los patrones predeterminados basados en especificaciones XFA se aplicarán a los campos.

Además, si el patrón de visualización especificado es incorrecto o no se puede aplicar, los patrones predeterminados basados en especificaciones XFA se aplicarán a los campos, las variables o los elementos del modelo de datos de formulario.

## Aplicar reglas a los componentes de comunicaciones interactivas {#rules}

Para condicionalizar componentes o contenido en la comunicación interactiva, seleccione el componente o fragmento de contenido y seleccione ![createruleicon](assets/createruleicon.png) (Crear regla) para iniciar el Editor de reglas.

Para obtener más información, consulte:

* [Editor de reglas](/help/forms/using/rule-editor.md)
* [Introducción a la creación de comunicaciones interactivas](/help/forms/using/introduction-interactive-communication-authoring.md)

## Usar tablas {#tables}

### Tablas dinámicas en comunicaciones interactivas {#dynamic-tables-in-interactive-communication}

Puede agregar tablas dinámicas en la comunicación interactiva mediante fragmentos de diseño. Los siguientes pasos utilizan un ejemplo de instrucción de extracto de una tarjeta de crédito para ilustrar el uso de un fragmento de diseño para crear una tabla dinámica en una comunicación interactiva.

1. Asegúrese de que el fragmento de diseño necesario para crear la tabla esté disponible en AEM.
1. En el canal Imprimir de la comunicación interactiva, arrastre y suelte un fragmento de diseño (con una tabla de varias columnas) en un área de destino desde el explorador de recursos.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   Aparecerá una tabla en el área de diseño de la comunicación interactiva.

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Especifique el enlace de los datos para cada una de las celdas de la tabla. Para crear una fila repetible, inserte las propiedades del modelo de datos de formulario en la fila que pertenezca a una propiedad de colección común.

   1. Seleccione una celda de la tabla y seleccione ![configure_icon](assets/configure_icon.png) (Configurar).

      El cuadro de diálogo Propiedades aparecerá en la barra lateral.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Configure las propiedades:

      * **[!UICONTROL Nombre]**: nombre del nodo JCR.
      * **[!UICONTROL Título]**: escriba un título que sea visible en el editor de comunicaciones interactivas.
      * **[!UICONTROL Tipo de enlace]**: seleccione uno de los siguientes tipos de enlace para el campo.

         * **[!UICONTROL Ninguno]**
         * **[!UICONTROL Objeto del modelo de datos]**: el valor de una propiedad del modelo de datos de formulario se rellena en el campo. Como alternativa, seleccione la pestaña **Fuentes de datos** y arrastre y suelte la propiedad en el campo.

      * **[!UICONTROL Objeto de modelo de datos]**: propiedad del modelo de datos de formulario cuyo valor se rellena en el campo.
      * **[!UICONTROL Valor predeterminado]**: el valor predeterminado garantiza que el campo no esté vacío cuando el objeto del modelo de datos especificado no proporcione ningún valor. El valor predeterminado se rellena previamente en el campo.

      * **[!UICONTROL Editable por el agente]**: seleccione esta opción para permitir que el agente edite el valor en el campo de la interfaz de usuario de Agente.

   1. Seleccione ![done_icon](assets/done_icon.png).

1. Previsualice la comunicación interactiva para ver la tabla representada con los datos.

   ![lf_preview](assets/lf_preview.png)

### Tablas solo de canal Web {#webchanneltables}

Seleccione el panel raíz en la plantilla web y seleccione **+** para agregar un componente **Table** a la comunicación interactiva. En la comunicación interactiva se inserta una tabla que incluye dos filas. La primera fila de la tabla representa el encabezado de la tabla.

#### Agregar filas y columnas a la tabla {#addrowscolumnstable}

**Para agregar o eliminar columnas, haga lo siguiente:**

1. Seleccione el cuadro de texto predeterminado en la fila de encabezado de la tabla para ver la barra de herramientas de componentes.
1. Seleccione **Agregar columna** o **Eliminar columna** para agregar o eliminar columnas de la tabla respectivamente.

![component_toolbar_table1](assets/component_toolbar_table1.png)

**Para agregar o eliminar filas, haga lo siguiente:**

1. Seleccione cualquiera de las filas de la tabla para ver la barra de herramientas de componentes. También puede seleccionar la fila de la tabla mediante el explorador de contenido en la barra de tareas de la comunicación interactiva.
1. Seleccione **Agregar fila** o **Eliminar fila** para agregar o eliminar filas de tabla respectivamente. Utilice las opciones **Subir** y **Bajar** de la barra de herramientas para reorganizar las filas de la tabla.

![Barra de herramientas del componente](assets/component_toolbar_table_row_new.png)

**A.** Agregar fila **B.** Eliminar fila **C.** Subir **D.** Bajar

#### Agregar o editar texto en celdas de la tabla {#addedittexttable}

1. Seleccione el cuadro de texto predeterminado en la celda de la tabla y seleccione ![editar](assets/edit.png) (Editar).
1. Escriba el texto en la celda de la tabla y seleccione ![done_icon](assets/done_icon.png) para guardarlo.

#### Crear enlaces entre celdas de la tabla y elementos de objeto del modelo de datos {#createbindingtablecells}

1. Seleccione el cuadro de texto predeterminado en la fila de la tabla y seleccione ![editar](assets/edit.png) (Editar).
1. Seleccione la lista desplegable Objetos del modelo de datos y seleccione la propiedad.
1. Seleccione para guardar y crear un enlace entre la celda de la tabla y la propiedad del objeto del modelo de datos.

![Crear enlace de datos](assets/create_data_binding_table_new.png)

#### Crear un hipervínculo para texto en celdas de la tabla {#createhyperlinktable}

1. Seleccione el cuadro de texto predeterminado en la celda de la tabla y seleccione ![editar](assets/edit.svg) (Editar).
1. Seleccione el texto de la celda de la tabla y seleccione el icono Hipervínculo.
1. Especifique la URL en el campo **Ruta**.
1. Seleccione ![done_icon](assets/done_icon.png) para guardar las propiedades del hipervínculo.

![Crear hipervínculo](assets/create_hyperlink_table_new.png)

#### Crear tablas dinámicas {#createdynamictables}

Puede crear una tabla dinámica solo de canal Web en una comunicación interactiva mediante una propiedad del modelo de datos de tipo Colección. Esta tabla es una representación de las propiedades secundarias de una propiedad Colección. Solo se pueden editar las propiedades de formato de las distintas celdas de la tabla.

1. Cambie al canal Web y, a continuación, elija mostrar el explorador de fuentes de datos.
1. Arrastre y suelte una propiedad de colección en un subformulario. Se creará una tabla en el subformulario.
1. Obtenga una vista previa de la tabla en la vista previa web de la comunicación interactiva.

#### Ordenar columnas en una tabla {#sortcolumns}

Puede ordenar los datos en función de cualquier columna de una tabla en las comunicaciones interactivas. Los valores de la columna se pueden ordenar en orden ascendente o descendente.

El orden se puede aplicar a columnas de la tabla que contengan lo siguiente:

* Texto estático
* Propiedades del objeto del modelo de datos
* Combinación de texto estático y propiedades del objeto del modelo de datos

Para habilitar la ordenación:

1. Seleccione la tabla y seleccione ![configure_icon](assets/configure_icon.png) (Configurar). También puede seleccionar la tabla mediante el explorador **Contenido** en la barra de tareas de comunicación interactiva.
1. Seleccione **Habilitar ordenación.**
1. Seleccione ![done_icon](assets/done_icon.png) para guardar las propiedades de la tabla. Los iconos de clasificación, flechas arriba y abajo, de los encabezados de las columnas representan que se ha habilitado la ordenación.

   ![Habilitar ordenar](assets/enable_sorting_new-1.png)

1. Cambie a la **Vista previa** para ver el resultado. La tabla se ordenará automáticamente en función de la primera columna de la tabla.
1. Haga clic en el encabezado de la columna para ordenar los valores según la columna.

   Un encabezado de columna con una flecha hacia arriba representa lo siguiente:

   * que se ordena en función de esa columna.
   * que los valores de la columna se muestran en orden ascendente.

   ![Orden ascendente](assets/sorting_ascending_new-1.png)

   Del mismo modo, un encabezado de columna con una flecha hacia abajo representa que los valores de la columna se muestran en orden descendente.

## Editar propiedades de la comunicación interactiva {#edit-interactive-communication-properties}

Una vez creada una comunicación interactiva, puede editar sus propiedades en una fase posterior.

Utilice la página **Propiedades** para lo siguiente:

* Editar los valores de los campos especificados al crear la comunicación interactiva, como Título y Descripción.
* Agregar o eliminar el canal Web de una comunicación interactiva existente.
* Obtener una vista previa, descargar o eliminar la comunicación interactiva
* Abra la [IU del Agente](/help/forms/using/prepare-send-interactive-communication.md).

Para acceder a la página **Propiedades**, haga lo siguiente:

1. Inicie sesión en la instancia de autor de AEM y navegue hasta **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Seleccione la comunicación interactiva y seleccione **Propiedades**.
1. Seleccione la pestaña **General** para editar los campos **Título** y **Descripción**.

### Agregar o eliminar el canal Web {#add-or-delete-the-web-channel}

Ejecute los siguientes pasos para agregar el canal Web para una comunicación interactiva existente:

1. En la página **Propiedades** seleccione la pestaña **Canales**.
1. Seleccione la casilla de verificación **Web** y seleccione una plantilla para el canal Web.
1. Seleccione **Usar Imprimir como principal para el canal Web** para habilitar la sincronización entre el canal Web y el canal Imprimir
1. Seleccione **Guardar y cerrar** para guardar los cambios.

   Del mismo modo, puede seleccionar la casilla de verificación **Web** en la pestaña **Canales** para eliminar el canal Web de la comunicación interactiva.

## Agregar el componente Botón al canal Web {#add-button-component-to-the-web-channel}

Puede agregar Botón como componente al canal Web de la comunicación interactiva. Defina las reglas mediante el [editor de reglas](../../forms/using/rule-editor.md) para poder navegar hasta otras comunicaciones interactivas, formularios adaptables, otros recursos como imágenes o fragmentos de documento, o una URL externa al seleccionar el botón.

Para agregar un botón y definir las reglas que contiene, haga lo siguiente:

1. Seleccione el panel raíz en la plantilla web y seleccione **+** para agregar el componente **Button** a la comunicación interactiva.
1. Seleccione el componente de botón y seleccione ![edit-rules](assets/edit-rules.png) para definir las reglas al seleccionar el botón.
1. En la sección **Cuándo**, seleccione **al hacer clic** desde el estado de la lista desplegable de Botón.
1. En la sección **Entonces**:

   1. Seleccione una acción de la lista desplegable. Por ejemplo, seleccione **Ir a** como tipo de acción.

   1. Especifique la dirección URL de la comunicación interactiva, el formulario adaptable, un recurso o una página web. Por ejemplo, especifique la dirección URL en el siguiente formato para navegar hasta otra comunicación interactiva: https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;Interactive Communication name>/channels/&lt;channel name - print or web>.html
   1. Especifique la opción para abrir el recurso en la misma pestaña, en una pestaña nueva o en una ventana nueva.
   1. Seleccione **Listo** y, a continuación, seleccione **Cerrar** para guardar la regla.

   Del mismo modo, puede seleccionar otras opciones disponibles en la lista desplegable del tipo Acción, como Invocar servicio y Enviar formulario. Para obtener más información, consulte [Editor de reglas](../../forms/using/rule-editor.md).

1. Previsualice la comunicación interactiva y seleccione el botón para ver la comunicación interactiva, el formulario adaptable, un recurso o una página web especificada en el paso 4(b).

## Agregar el componente Panel al canal Web {#add-panel-component-to-the-web-channel}

El componente Panel es un marcador de posición para agrupar otros componentes y controla cómo se coloca un grupo de componentes, como acordeón y pestañas, en la comunicación interactiva. Un componente de panel también le permite hacer que un grupo de componentes se repita para el usuario final, por ejemplo, en varias entradas obligatorias para rellenar credenciales educativas.

Siga los siguientes pasos para agregar un componente Panel al canal Web:

1. Inserte el componente **Panel** en el canal Web mediante cualquiera de las siguientes opciones:

   * Seleccione un componente, seleccione **+** y seleccione el componente **Panel**.

   * En el panel del explorador del **Componente**, arrastre y suelte el componente **Panel** en la comunicación interactiva.

   * Seleccione el **Panel** en el panel del explorador **Contenido** y seleccione **Agregar panel secundario**. Al seleccionar la opción **Agregar panel secundario** se mostrará el cuadro de diálogo **Agregar panel secundario**. Escriba el título, una descripción y un nombre opcionales para el componente Panel.

1. Seleccione el panel en el explorador **Content** para realizar acciones adicionales en el panel, como configurar, editar reglas, copiar, eliminar e insertar componentes.

   También puede arrastrar y soltar un panel dentro del explorador de **Contenido** para reflejar el cambio en la estructura de la comunicación interactiva en el panel derecho.

## Sincronizar el canal Web con el canal Imprimir {#synchronize}

Al seleccionar Imprimir como principal para el canal Web al crear una comunicación interactiva, el canal Web se crea de forma sincronizada con el canal Imprimir y el contenido y el enlace de datos del canal Web se derivan del canal Imprimir y los cambios realizados en este podrían reflejarse en el canal Web al seleccionar Sincronizar.

Sin embargo, se permite a los autores romper la herencia de los componentes del canal Web, según sea necesario.

![Crear Imprimir como principal](assets/create_ic_print_master_new-1.png) ![Web Imprimir principal](assets/create_ic_print_master_web_new-1.png)

### Sincronización automática {#autosync}

Si selecciona la opción **[!UICONTROL Usar Imprimir como principal para el canal Web]**, puede seleccionar cualquiera de los siguientes modos para generar el canal Web:

* **[!UICONTROL Diseño automático]**: seleccione este modo para generar automáticamente marcadores de posición, contenido y enlaces de datos para el canal web desde el canal de impresión.
* **[!UICONTROL Organizar manualmente]**: seleccione este modo para seleccionar manualmente los elementos del canal Imprimir y agregarlos al canal Web mediante el contenido principal disponible en la pestaña Fuentes de datos. Para obtener más información, consulte [Seleccionar Imprimir elementos de canal para crear contenido de canal Web](#selectprintchannelelements).

![Crear opciones de IC](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>Al sincronizar los canales, se sincronizan únicamente los fragmentos de documento, las imágenes, las condiciones, las listas y los fragmentos de diseño del canal Imprimir al canal Web. Los subformularios o nodos principales que incluyen estos elementos no se sincronizan.

### Seleccione Imprimir elementos de canal para crear contenido de canal Web {#selectprintchannelelements}

Si selecciona Imprimir como principal mientras crea la comunicación interactiva y no selecciona la opción de sincronización automática, también puede arrastrar y soltar elementos del canal Imprimir en la interfaz de creación del canal Web.

Navegue hasta **Fuentes de datos** > **Contenido principal** para ver los elementos del canal Imprimir. Arrastre y suelte las áreas, campos o tablas de destino en la interfaz de creación del canal Web. Un icono de un círculo azul junto al nombre del elemento indica que el elemento del canal Imprimir ya se ha incluido en el canal Web.

![Contenido principal](assets/master_content.png)

### Cancelar herencia {#cancelinheritance}

En el canal Web, los componentes se incrustan en las áreas de destino.

Pase el ratón sobre el área o la variable de destino correspondiente del canal Web y seleccione ![cancelinheritance](assets/cancelinheritance.png) (Cancelar herencia) y, a continuación, en el cuadro de diálogo Cancelar herencia, seleccione **[!UICONTROL Sí]**.

La herencia de los componentes de dentro del área de destino se cancelarán y podrá editarlos según sea necesario.

### Volver a habilitar la herencia {#re-enable-inheritance}

En el canal Web, si ha cancelado la herencia de un componente, puede volver a activarla. Para volver a habilitar la herencia, pase el ratón sobre el límite del área de destino correspondiente que incluye el componente y seleccione ![reenableinheritance](assets/reenableinheritance.png).

Aparecerá el cuadro de diálogo Revertir herencia.

![revertinheritance](assets/revertinheritance.png)

Si es necesario, seleccione **[!UICONTROL Sincronizar la página después de revertir la herencia]**. Seleccione esta opción para sincronizar toda la comunicación interactiva. Si no selecciona esta opción, solo se sincronizará el área de destino correspondiente al restablecer la herencia.

Seleccione **[!UICONTROL Sí]**.

### Sincronizar {#synchronize-1}

Si utiliza Imprimir como principal para el canal Web y cambia el canal Imprimir, puede sincronizar el contenido para traer los cambios recién realizados al canal Web.

1. Para sincronizar el canal Web con el canal Imprimir, cambie al canal Web y seleccione el icono Más opciones.

   ![Opciones de sincronización automática](assets/auto_sync_options_new.png)

1. Seleccione una de las siguientes opciones:

   * **[!UICONTROL Sincronizar con Imprimir]**: sincroniza el contenido solo para las áreas de destino en las que no se cancela la herencia.
   * **[!UICONTROL Restablecer]**: sincroniza el contenido del canal Web con el canal Imprimir y descarta todos los cambios realizados en el canal Web.

### Utilice la barra de herramientas de componentes para realizar acciones en componentes heredados {#componenttoolbar}

Una vez que haya generado automáticamente contenido en el canal Web mediante la opción Sincronizar, puede realizar más acciones en los componentes sin cancelar la herencia.

![Barra de herramientas del componente](assets/component_toolbar_inherited_web_new.png)

Seleccione el componente para ver las siguientes opciones:

* **Copiar:** permite copiar un componente y péguelo en otros lugares de la comunicación interactiva.
* **Cortar:** permite mover un componente de un lugar a otro en la comunicación interactiva.
* **Insertar componente:** permite insertar un componente sobre el componente seleccionado.
* **Pegar**: permite pegar el componente cortado o copiado mediante las opciones descritas anteriormente.
* **Grupo**: permite seleccionar varios componentes si desea cortar, copiar o pegar más de un componente a la vez.
* **Principal**: seleccione el elemento principal de un componente.
* **Consultar expresión SOM:** permite consultar la [expresión SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para el componente.

* **Agrupar objetos en el panel:** permite agrupar los componentes en un panel para poder realizar operaciones en esos componentes simultáneamente. Para obtener más información, consulte [Agrupar objetos en el panel](#groupobjectspanel).

* **Cancelar herencia:** [permite cancelar la herencia](#cancelinheritance) de los componentes dentro del área de destino para editarlos.

### Agrupar objetos en Panel {#groupobjectspanel}

La interfaz de creación de canales web facilita la agrupación de los componentes en un panel para poder realizar operaciones en esos componentes simultáneamente. La pestaña **Contenido** enumera los componentes agrupados como elementos secundarios del panel en el árbol de contenido.

1. Seleccione un componente y seleccione la operación Grupo (![grupo](assets/group.jpg)).
1. Seleccione varios componentes y **objetos de grupo en el panel**.

   ![Agrupar objetos](assets/component_toolbar_group_objects_new.png)

1. En el cuadro de diálogo **Agrupar objetos en el panel**, escriba un nombre para el panel.
1. Escriba un título y una descripción opcionales para el panel.
1. Haga clic en ![bullet_checkmark](assets/bullet_checkmark.png).

   Los componentes agrupados se muestran como elementos secundarios del panel en el árbol de contenido.

   ![content_tree_grouping](assets/content_tree_grouping.png)

## Formato de salida para el canal Imprimir {#output-format-print-channel}

Utilice la API PrintChannel para definir el formato de salida del canal Imprimir de una comunicación interactiva. Si no define un formato de salida, AEM Forms generará la salida en formato PDF.

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

Para generar la salida en cualquier otro formato, especifique el tipo de formato de salida. Consulte [API PrintChannel](https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html) para obtener la lista de tipos de formato de salida compatibles.

Por ejemplo, puede utilizar el siguiente ejemplo para definir PCL como formato de salida para una comunicación interactiva:

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
