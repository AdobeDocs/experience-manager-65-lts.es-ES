---
title: 'Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos'
description: El flujo de trabajo centrado en Forms sobre los pasos de OSGi le permite crear rápidamente flujos de trabajo basados en formularios adaptables.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
exl-id: 13d84b04-dab6-453f-bc0d-62a5f557c4f2
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '7613'
ht-degree: 90%

---

# Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos {#forms-centric-workflow-on-osgi-step-reference}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference).

Los modelos de flujo de trabajo se utilizan para convertir una lógica empresarial en un proceso repetitivo automatizado. Un modelo le ayuda a definir y ejecutar una serie de pasos. También puede definir propiedades del modelo, como si el flujo de trabajo es transitorio o utiliza varios recursos. Puede [incluir varios pasos del flujo de trabajo AEM en un modelo para lograr establecer una lógica empresarial](/help/sites-developing/workflows-models.md#extending-aem).

## Pasos de Forms Workflow {#forms-workflow-steps}

Los pasos de Forms Workflow realizan operaciones específicas de AEM Forms en un flujo de trabajo de AEM. Estos pasos le permiten crear rápidamente formularios adaptables basados en flujos de trabajo centrados en Forms en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, y procesos empresariales internos y a través del firewall. También puede seguir los pasos de Forms Workflow para iniciar servicios de documentos, integrarse con el flujo de trabajo de firmas de Adobe Sign y realizar otras operaciones de AEM Forms.

Los pasos del flujo de trabajo centrados en AEM Forms realizan operaciones específicas en un flujo de trabajo AEM. Estos pasos le permiten generar rápidamente un flujo de trabajo adaptable basado en Forms y centrado en Forms en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, y procesos empresariales internos y a través del firewall.

>[!NOTE]
>
>Si el modelo de flujo de trabajo está marcado para un almacenamiento externo, para todos los pasos del flujo de Forms Workflow, puede seleccionar solo la opción de variable para almacenar o recuperar archivos de datos y archivos adjuntos.

## Paso de tarea de asignación {#assign-task-step}

El paso para asignar una tarea crea una tarea y la asigna a un usuario o grupo. Además de asignar la tarea, el componente también especifica el formulario adaptable o el PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar los datos que han introducido los usuarios y un PDF no interactivo o un formulario adaptable de solo lectura solo se utiliza para revisar los flujos de trabajo.

También puede utilizar el componente para controlar el comportamiento de la tarea. Por ejemplo, crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, especificar la ruta de los datos enviados, especificar la ruta de los datos que se van a rellenar previamente y especificar las acciones predeterminadas. El paso para asignar una tarea tiene las siguientes propiedades:

* **Título:** título de la tarea. El título se muestra en la bandeja de entrada de AEM.
* **Descripción:** explicación de las operaciones que se realizan en la tarea. Esta información resulta útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **Ruta de la vista en miniatura:** ruta de la miniatura de la tarea. Si no se especifica ninguna ruta, se mostrará la miniatura predeterminada de un formulario adaptable y, para el documento de registro, se mostrará un icono predeterminado.
* **Fase del flujo de trabajo:** un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM. Puede definir estas fases en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Fases).
* **Prioridad:** la prioridad seleccionada se muestra en la bandeja de entrada de AEM. Las opciones disponibles son Alta, Media y Baja. El valor predeterminado es Media.
* **Fecha de vencimiento:** especifica el número de días u horas después de los cuales se marcará la tarea con retraso. Si selecciona **No**, la tarea nunca se marca como con retraso. También puede especificar un controlador de tiempo de espera para realizar tareas específicas después de que la tarea haya llegado a la fecha de vencimiento.

* **Días:** número de días antes de los cuales se completará la tarea. El número de días se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de días especificado en el campo Días, si se selecciona, se activa un controlador de tiempo de espera después de la fecha de vencimiento.
* **Horas:** número de horas antes de las cuales se completará la tarea. El número de horas se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de horas especificado en el campo Horas, si se selecciona, se activa un controlador de tiempo de espera después de las horas de vencimiento.
* **Tiempo de espera después de la fecha de vencimiento:** seleccione esta opción para habilitar el campo de selección Controlador de tiempo de espera.
* **Controlador de tiempo de espera:** seleccione el script que se ejecutará cuando el paso para asignar tareas sobrepase la fecha de vencimiento. Scripts colocados en el repositorio CRX en [apps]/fd/dashboard/scripts/timeoutHandler están disponibles para su selección. La ruta especificada no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla.
* **Resaltar la acción y el comentario de la última tarea en Detalles de la tarea:** seleccione esta opción para mostrar la última acción realizada y el comentario recibido en la sección de detalles de una tarea.
* **Tipo:** elija el tipo de documento que desea rellenar al iniciar el flujo de trabajo. Puede elegir un formulario adaptable, un formulario adaptable de solo lectura, un documento PDF no interactivo, una interfaz de usuario de agente de comunicación interactiva o un documento del canal Web de comunicación interactiva.
* **Utilizar formulario adaptable:** especifica el método para localizar el formulario adaptable de entrada. Esta opción está disponible si selecciona Formulario adaptable o Formulario adaptable de solo lectura en la lista desplegable Tipo. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta de acceso absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable de tipo cadena para especificar la ruta.\
  Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

* **Utilizar comunicación interactiva:** especifica el método para localizar la comunicación interactiva de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta de acceso absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable de tipo cadena para especificar la ruta. Esta opción estará disponible si selecciona la interfaz de usuario de agente de comunicación interactiva o el documento del canal Web de comunicación interactiva en la lista desplegable Tipo.

>[!NOTE]
>
>Debe tener asignaciones de cm-agent-users y de grupo de flujo de trabajo-usuarios para acceder a la interfaz de usuario de agente de comunicaciones interactivas en la bandeja de entrada de AEM.

* **Formulario adaptable o ruta de comunicación interactiva:** especifica la ruta del formulario adaptable o la comunicación interactiva. Puede utilizar el formulario adaptable o la comunicación interactiva que se envía al flujo de trabajo, que está disponible en una ruta absoluta, o recuperar el formulario adaptable de una ruta almacenada en una variable de tipo de datos de cadena.
* **Seleccionar el PDF de entrada mediante:** especifica la ruta de un documento de PDF no interactivo. El campo está disponible cuando se elige un documento PDF no interactivo en el campo Tipo. Puede seleccionar el PDF de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta de acceso absoluta o utilizando una variable con un tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/PDF/credit-card.pdf. La ruta no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla. Se necesita habilitar una opción de documento de registro o formulario adaptable basado en plantillas de formulario para usar la opción Ruta del PDF.
* **Para las tareas completadas, procese el formulario adaptable como:** cuando se marca una tarea como completada, puede procesar el formulario adaptable como un formulario adaptable de solo lectura o un documento PDF. Se necesita habilitar una opción de documento de registro o formulario adaptable basado en plantillas de formulario para procesar el formulario adaptable como documento de registro.
* **Rellenado previamente:** los siguientes campos sirven como entradas para la tarea:

   * **[!UICONTROL Seleccionar el archivo de datos de entrada mediante]**: ruta del archivo de datos de entrada (.json, .xml, .doc o modelo de datos de formulario). Puede recuperar el archivo de datos de entrada mediante una ruta relativa a la carga útil o recuperar el archivo almacenado en una variable con un tipo de datos Doc, XML o JSON. Por ejemplo, el archivo contiene los datos enviados para el formulario a través de una aplicación de bandeja de entrada AEM. Una ruta de ejemplo es [Payload_Directory]/workflow/data.

   * **Seleccionar datos adjuntos de entrada mediante:** los archivos adjuntos disponibles en la ubicación se adjuntarán al formulario asociado a la tarea. La ruta puede ser relativa a la carga útil o recuperar los archivos adjuntos almacenados en una variable del tipo ArrayList of Document. Una ruta de ejemplo es [Payload_Directory]/attachments/. Puede especificar archivos adjuntos colocados en relación con la carga útil o utilizar una variable de tipo Doc (Lista de matriz > Documento) para especificar un archivo adjunto de entrada para el formulario adaptable.

      * **Elegir el JSON de entrada:** selecciona un archivo JSON de entrada mediante una ruta relativa a la carga útil o almacenada en una variable de tipo de datos Documento, JSON o Modelo de datos de formulario. Esta opción estará disponible si selecciona la interfaz de usuario de agente de comunicación interactiva o el documento del canal Web de comunicación interactiva en la lista desplegable Tipo.
      * **Elegir un servicio de rellenado previo personalizado:** selecciona el servicio de rellenado previo para recuperar los datos y rellenar previamente el documento del canal Web de comunicación interactiva o la interfaz de usuario de agente.
      * **Utilizar el servicio de rellenado previo de la comunicación interactiva seleccionada arriba:** utilice esta opción para utilizar el servicio de rellenado previo de la comunicación interactiva definida en la lista desplegable Usar comunicación interactiva.
      * **Asignar atributos de solicitud:** utilice la sección Asignar atributos de solicitud para definir el [nombre y el valor del atributo de solicitud](../../forms/using/work-with-form-data-model.md#bindargument). Recupere los detalles de la fuente de datos en función del nombre del atributo y el valor especificados en la solicitud. Puede definir un valor de atributo de solicitud utilizando un valor literal o una variable de tipo de datos de cadena.\
        Las opciones de asignación de atributos de solicitud y servicio de prellenado solo estarán disponibles si selecciona la interfaz de usuario de agente de comunicación interactiva o el documento de canal Web de comunicación interactiva en la lista desplegable Tipo.

* **Información enviada:** los siguientes campos sirven como ubicaciones de salida para la tarea:

   * **Guardar el archivo de datos de salida mediante:** guarda el archivo de datos (.json, .xml, .doc o modelo de datos de formulario). El archivo de datos contiene información enviada a través del formulario asociado. Puede guardar el archivo de datos de salida utilizando una ruta relativa a la carga útil o almacenarla en una variable con un tipo de datos Doc, XML o JSON. Por ejemplo, [Payload_Directory]/Workflow/data, donde los datos son un archivo.
   * **Guardar archivos adjuntos mediante:** guarda los datos adjuntos del formulario proporcionados en una tarea. Puede guardar los archivos adjuntos mediante una ruta relativa a la carga útil o almacenarla en una variable de matriz con un tipo de datos documento.
   * **Guardar documento de registro mediante:** ruta para guardar un archivo de documento de registro. Por ejemplo, [Payload_Directory]/DocumentofRecord/credit-card.pdf. Puede guardar el documento de registro mediante una ruta relativa a la carga útil o almacenarlo en una variable con un tipo de datos Doc. Si selecciona **Relativo a la carga útil**, el documento de registro no se genera si el campo de ruta se deja vacío. Esta opción solo estará disponible si selecciona Formulario adaptable en la lista desplegable Tipo.

   * **Guardar los datos del canal Web mediante:** guarda el archivo de datos del canal Web mediante una ruta relativa a la carga útil o lo almacena en una variable de tipo de datos de Documento, JSON o Modelo de datos de formulario. Esta opción solo estará disponible si selecciona comunicación interactiva de la interfaz de usuario de agente en la lista desplegable Tipo.
   * **Guardar el documento PDF mediante:** guarda el documento PDF mediante una ruta relativa a la carga útil o lo almacena en una variable del tipo de datos Document. Esta opción solo estará disponible si selecciona comunicación interactiva de la interfaz de usuario de agente en la lista desplegable Tipo.
   * **Guardar plantilla de diseño mediante:** guarda la plantilla de diseño mediante una ruta relativa a la carga útil o la almacena en una variable de tipo de datos Document. La variable [plantilla de diseño](../../forms/using/layout-design-details.md) hace referencia a un archivo XDP que crea con Forms Designer. Esta opción solo estará disponible si selecciona comunicación interactiva de la interfaz de usuario de agente en la lista desplegable Tipo.

* **Usuario asignado > Asignar opciones:** especifica el método para asignar la tarea a un usuario. Puede asignar dinámicamente la tarea a un usuario o grupo mediante el script del selector de participantes o asignar la tarea a un usuario o grupo AEM específico.
* **Selector de participantes:** la opción estará disponible cuando la opción **Dinámicamente a un usuario o grupo** esté seleccionada en el campo Asignar opciones. Puede utilizar un ECMAScript o un servicio para seleccionar dinámicamente un usuario o un grupo.

* **Participantes:** el campo estará disponible cuando la opción **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** esté seleccionada en el campo **Selector de participantes**. El campo permite seleccionar usuarios o grupos para la opción RandomParticipantChooser.

* **Usuario asignado:** el campo estará disponible cuando esté seleccionado **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** en el campo **Selector de participantes**. El campo permite seleccionar una variable de tipo de datos de cadena para definir el usuario asignado.

* **Argumentos:** el campo estará disponible cuando se seleccione un script que no sea RandomParticipantChoose en el campo Selector de participantes. El campo permite proporcionar una lista de un argumento separado por comas para el script seleccionado en el campo Selector de participantes.

* **Usuario o grupo:** la tarea se asigna al usuario o grupo seleccionado. La opción estará disponible cuando la opción **Para un usuario o grupo específico** esté seleccionada en el campo **Asignar opciones**. El campo enumera todos los usuarios y grupos del grupo de usuarios del flujo de trabajo.\
  La lista **Usuario o grupo** en el menú desplegable enumera los usuarios y grupos a los que el usuario que ha iniciado sesión tiene acceso. La visualización del nombre de usuario depende de si tiene permisos de acceso en el nodo **usuarios** en el repositorio CRX para ese usuario en particular.

* **[!UICONTROL Enviar correo electrónico de notificación]**: seleccione esta opción para enviar notificaciones por correo electrónico al usuario asignado. Estas notificaciones se envían cuando se asigna una tarea a un usuario o a un grupo. Puede usar la variable **[!UICONTROL Dirección de correo electrónico del destinatario]** para especificar el mecanismo para recuperar la dirección de correo electrónico.

* **[!UICONTROL Dirección de correo electrónico del destinatario]**: puede almacenar la dirección de correo electrónico en una variable, usar un valor literal para especificar una dirección de correo electrónico permanente o usar la dirección de correo electrónico predeterminada del usuario asignado especificada en el perfil del mismo. Puede utilizar el valor literal o una variable para especificar la dirección de correo electrónico de un grupo. La opción de variable es útil para recuperar y utilizar dinámicamente una dirección de correo electrónico. La variable **[!UICONTROL Usar la dirección de correo electrónico predeterminada del usuario asignado]** es solo para un único usuario asignado. En este caso, se utiliza la dirección de correo electrónico almacenada en el perfil del usuario asignado.

* **Plantilla de correo electrónico HTML**: seleccione la plantilla de correo electrónico para el correo electrónico de notificación. Para editar una plantilla, modifique el archivo ubicado en /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt en el repositorio CRX.
* **Permitir delegación en:** la bandeja de entrada de AEM proporciona una opción al usuario que ha iniciado sesión para delegar el flujo de trabajo asignado a otro usuario. Se le permite delegar dentro del mismo grupo o al usuario del flujo de trabajo de otro grupo. Si la tarea está asignada a un único usuario y la opción **Permitir la delegación a los miembros del grupo de asignados** está seleccionada, no es posible delegar la tarea a otro usuario o grupo.
* **Compartir configuración:** la bandeja de entrada de AEM proporciona opciones para compartir una o todas las tareas de la bandeja de entrada con otros usuarios:
   * Cuando la opción **Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada** está seleccionada, el usuario puede hacer clic en la tarea y compartirla con otro usuario de AEM.
   * Cuando la opción **Permitir que el usuario asignado comparta a través del uso compartido de la bandeja de entrada** esté seleccionada y los usuarios compartan sus elementos de la bandeja de entrada o permitan que otros usuarios accedan a sus elementos de la bandeja de entrada, solo las tareas con la opción mencionada previamente se compartirán con otros usuarios.

* **Acciones > Acciones predeterminadas:** las acciones Enviar, Guardar y Restablecer están disponibles por defecto. De forma predeterminada, todas estas acciones están habilitadas.
* **Variable de ruta:** nombre de la variable de ruta. La variable de ruta captura las acciones personalizadas que selecciona un usuario en la bandeja de entrada de AEM.
* **Rutas:** una tarea puede ramificarse en diferentes rutas. Cuando se selecciona en la bandeja de entrada AEM, la ruta devuelve un valor y las ramas del flujo de trabajo se basan en la ruta seleccionada. Puede almacenar rutas en una variable de matriz de tipo de datos de cadena o seleccionar **Literal** para agregar rutas manualmente.

* **Título** especifica el título de la ruta. Se muestra en la bandeja de entrada AEM.
* **Icono coral**: especifique el atributo HTML de un icono coral. La biblioteca CorelUI de Adobe proporciona un amplio conjunto de iconos táctiles. Puede elegir y utilizar un icono para la ruta. Se muestra junto con el título en la bandeja de entrada AEM. Si almacena las rutas en una variable, las rutas utilizan un icono coral predeterminado de &#39;Etiquetas&#39;.
* **Permitir que el usuario asignado añada un comentario**: seleccione esta opción para habilitar los comentarios en la tarea. Un usuario asignado puede agregar los comentarios desde la bandeja de entrada AEM en el momento del envío de la tarea.
* **Guardar comentario en la variable:** guarda el comentario en una variable de tipo de datos de cadena. Esta opción solo se mostrará si selecciona la casilla de verificación **Permitir que el usuario asignado agregue un comentario**.

* **Permitir que el usuario asignado agregue archivos adjuntos a la tarea**: seleccione esta opción para habilitar los archivos adjuntos en la tarea. Un usuario asignado puede agregar los archivos adjuntos desde la bandeja de entrada de AEM en el momento del envío de la tarea.
* **Guardar archivos adjuntos de tareas de salida mediante**: especifique la ubicación de la carpeta de archivos adjuntos. Puede guardar archivos adjuntos de tareas de salida utilizando una ruta relativa a la carga útil o en una variable de matriz con un tipo de datos Doc. Esta opción solo se mostrará si selecciona la casilla de verificación **Permitir que el usuario asignado agregue archivos adjuntos a la tarea** y selecciona **Formulario adaptable**, **Formulario adaptable de solo lectura** o **Documento PDF no interactivo** de la lista desplegable **Tipo** en la pestaña **Formulario/Documento**.

>[!NOTE]
>
>Utilice la pestaña Archivos adjuntos de la interfaz de usuario de agente durante el tiempo de ejecución para asociar los archivos adjuntos a una comunicación interactiva. Los archivos adjuntos asociados se mostrarán como archivos adjuntos de la tarea en la barra de tareas después de abrir el elemento de trabajo en estado Completo.

* **Usar metadatos personalizados:** seleccione esta opción para habilitar el campo de metadatos personalizado. Los metadatos personalizados se utilizan en plantillas de correo electrónico.
* **Metadatos personalizados:** seleccione metadatos personalizados para las plantillas de correo electrónico. Los metadatos personalizados están disponibles en el repositorio CRX en apps/fd/dashboard/scripts/metadataScripts. La ruta especificada no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla. También puede utilizar un servicio para los metadatos personalizados. También puede ampliar la interfaz WorkitemUserMetadataService para proporcionar metadatos personalizados.
* **Mostrar datos de pasos anteriores:** seleccione esta opción para permitir que los usuarios asignados vean los destinatarios anteriores, las acciones ya realizadas en la tarea, los comentarios agregados a la tarea y el documento de registro de la tarea completada, si está disponible.
* **Mostrar datos de pasos siguientes:** seleccione esta opción para permitir que el usuario asignado actual vea las acciones que realicen y los comentarios que agreguen a la tarea los usuarios asignados posteriores. También permite al usuario asignado actual ver un documento de registro de la tarea finalizada, si está disponible.
* **Visibilidad del tipo de datos:** de forma predeterminada, un usuario asignado puede ver un documento de registro, los usuarios asignados, las medidas adoptadas y los comentarios que hayan agregado los usuarios asignados anteriores y posteriores. Utilice la opción del tipo de visibilidad de datos para limitar el tipo de datos visibles para los usuarios asignados.

>[!NOTE]
>
>Las opciones para guardar el paso Asignar tarea como borrador y para recuperar el historial de la tarea asignada se deshabilitarán al configurar un modelo de flujo de trabajo [!DNL Adobe Experience Manager]para el almacenamiento de datos externo. Además, en la bandeja de entrada, la opción para guardar está deshabilitada.

## Paso para enviar correo electrónico {#send-email-step}

Utilice este paso para enviar un correo electrónico, por ejemplo, con un documento de registro, un vínculo de un formulario adaptable o con un documento de PDF adjunto. Este paso es compatible con el [correo electrónico HTML](https://es.wikipedia.org/wiki/Correo_HTML). Los correos electrónicos HTML responden y se adaptan al cliente de correo electrónico y al tamaño de pantalla de los destinatarios. Puede utilizar una plantilla de correo electrónico HTML para definir el aspecto, el esquema de colores y el comportamiento del correo electrónico.

El paso de correo electrónico utiliza el servicio de correo de Day CQ para enviar correos electrónicos. Antes de utilizar el paso de correo electrónico, asegúrese de que el [servicio de correo electrónico ](../../forms/using/aem-forms-workflow.md)esté configurado. El paso de correo electrónico tiene las siguientes propiedades:

**Título:** el título ayuda a identificar el paso en el editor de flujo de trabajo.

**Descripción:** la explicación es útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

**Asunto del correo electrónico:** el asunto se puede recuperar de los metadatos de un flujo de trabajo, especificarse manualmente o recuperarse del valor almacenado en una variable. Seleccione entre las siguientes opciones:

* **Literal:** especifica manualmente un asunto.
* **Recuperar a partir de metadatos del flujo de trabajo**. Recupere el asunto de una propiedad de metadatos.
* **Variable**. Recupere el asunto del valor almacenado en una variable de tipo de datos de cadena.

**Plantilla de correo electrónico HTML**. Plantilla HTML para el correo electrónico. Puede especificar variables en una plantilla de correo electrónico. El paso de correo electrónico extrae y muestra todas las variables incluidas en una plantilla para las entradas.

**Metadatos de las plantillas de correo electrónico:** el valor de las variables de la plantilla de correo electrónico puede ser un valor especificado por el usuario, la ruta de un recurso de parte del autor o en el servidor de publicación, una imagen o una propiedad de metadatos de flujo de trabajo.

* **Literal:** utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, [example@example.com](mailto:example@example.com).

* **Metadatos del flujo de trabajo:** utilice esta opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Después de seleccionar la opción, indique el nombre de la propiedad de metadatos en el cuadro de texto vacío debajo de la opción Metadatos del flujo de trabajo. Por ejemplo, emailAddress.
* **Dirección URL del recurso:** utilice la opción para incrustar un vínculo web de una comunicación interactiva al correo electrónico. Después de seleccionar la opción, busque y elija la comunicación interactiva que desea incrustar. El recurso puede residir en el autor o en el servidor de publicación.
* **Imagen:** utilice esta opción para incrustar una imagen en el correo electrónico. Después de seleccionar la opción, busque y elija la imagen. La opción de imagen solo está disponible para las etiquetas de imagen (&lt;img src=&quot;&#42;&quot;/>) en la plantilla de correo electrónico.

**Dirección de correo electrónico del remitente/destinatario:** Seleccione la opción **Literal** para especificar manualmente una dirección de correo electrónico o seleccione la opción **Recuperar a partir de metadatos del flujo de trabajo** para recuperar la dirección de correo electrónico de una propiedad de metadatos. También puede especificar una lista de matrices de propiedades de metadatos para la opción **Recuperar a partir de metadatos del flujo de trabajo**. Seleccione la opción **Variable** para recuperar la dirección de correo electrónico a partir valor almacenado en una variable de tipo de datos de cadena.

**Archivo adjunto:** el recurso disponible en la ubicación especificada se adjunta al correo electrónico. La ruta del recurso puede ser relativa a la carga útil o a la ruta de acceso absoluta. Una ruta de ejemplo es [Payload_Directory]/attachments/.

Seleccione la opción **Variable** para recuperar el archivo adjunto almacenado en una variable con un tipo de datos Doc, XML o JSON.

**Nombre del archivo:** nombre del archivo adjunto del correo electrónico. El paso de correo electrónico cambia el nombre de archivo original del archivo adjunto al nombre de archivo especificado. El nombre se puede especificar manualmente o recuperar a partir de una propiedad de metadatos de flujo de trabajo o una variable. Utilice la opción **Literal** cuando sepa el valor exacto que desea especificar. Utilice la opción **Variable** para recuperar el nombre de archivo del valor almacenado en una variable de tipo de datos de cadena. Utilice la variable **Recuperar a partir de metadatos de flujo de trabajo** cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo.

## Paso para generar documentos de registro {#generate-document-of-record-step}

Cuando se rellena o se envía un formulario, se puede guardar un registro del formulario, en formato impreso o en formato de documento. Este registro se denomina Documento de registro (DoR). Puede utilizar el paso Generar documento de registro para crear una versión PDF de solo lectura o interactiva de un formulario adaptable. La versión en PDF contiene información rellenada en el formulario junto con la presentación del formulario adaptable.

El paso Documento de registro tiene las siguientes propiedades:

**Utilizar formulario adaptable:** especifica el método para localizar el formulario adaptable de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta de acceso absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable del tipo de datos de cadena para especificar la ruta en el campo **Seleccionar variable que resolver**.\
Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

**Ruta de formulario adaptable:** especifica la ruta del formulario adaptable. El campo está disponible al seleccionar la variable **Disponible en una ruta de acceso absoluta** del campo **Utilizar formulario adaptable**.

**Seleccionar datos de entrada mediante:** ruta de los datos de entrada para el formulario adaptable. Puede mantener los datos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos o recuperar datos almacenados en una variable con un tipo de datos Doc, JSON o XML. Los datos de entrada se combinan con el formulario adaptable para crear un documento de registro.

**Seleccionar ruta de acceso de los datos adjuntos de entrada mediante:** ruta de los archivos adjuntos. Estos archivos adjuntos se incluyen en el documento de registro. Puede mantener los archivos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los archivos adjuntos o recuperar los archivos adjuntos almacenados en una variable de matriz con un tipo de datos Doc.

Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntan al documento de registro. Si hay archivos disponibles en las carpetas accesibles directamente en la ruta de datos de los archivos adjuntos especificada, los archivos se incluyen en el documento de registro como archivos adjuntos. Si hay carpetas en carpetas accesibles directamente, esas carpetas se omiten.

**Guardar documento de registro generado mediante las siguientes opciones:** especifica la ubicación para mantener un archivo de documento de registro. Puede sobrescribir la carpeta de carga útil, colocar el documento de registro en una ubicación del directorio de carga útil o almacenar el documento de registro en una variable con un tipo de datos Doc.

**Configuración regional:** especifique el idioma del documento de registro. Seleccione **Literal** para elegir la configuración regional de una lista desplegable o seleccione **Variable** para recuperar la configuración regional a partir del valor almacenado en una variable de tipo de datos de cadena. Definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

## Paso para invocar el servicio de modelo de datos de formulario {#invoke-form-data-model-service-step}

Puede usar la [integración de datos de AEM Forms](../../forms/using/data-integration.md) para configurar y conectarse a fuentes de datos dispares. Estas fuentes de datos pueden ser una base de datos, un servicio web, un servicio REST, un servicio OData y una solución CRM. La integración de datos de AEM Forms permite crear un modelo de datos de formulario que incluya varios servicios para realizar operaciones de recuperación, adición y actualización de datos en la base de datos configurada. Puede usar el **paso para invocar el servicio de modelo de datos** para seleccionar un modelo de datos de formulario (FDM) y utilizar los servicios del FDM para recuperar, actualizar o agregar datos a distintas fuentes de datos.

Para explicar las entradas de los campos del paso, se utilizan como ejemplo la siguiente tabla de base de datos y el archivo JSON:

**Tabla de detalles del cliente de muestra**

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Valor<br /> </td> 
  </tr> 
  <tr> 
   <td>FirstName<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>LastName</td> 
   <td>Rose</td> 
  </tr> 
  <tr> 
   <td>ID de cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Dirección de correo electrónico<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**Archivo JSON de muestra**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

El paso para invocar el servicio de modelo de datos de formulario tiene los siguientes campos para facilitar las operaciones del modelo de datos de formulario:

* **Título:** título del paso. Ayuda a identificar el paso en el editor de flujo de trabajo.
* **Descripción:** explicación útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **Ruta del modelo de datos del formulario:** busca y selecciona un modelo de datos de formulario presente en el servidor.

* **Servicio:** lista de los servicios que proporciona el modelo de datos de formulario seleccionado.
* **Entrada para servicios > Proporcionar datos de entrada mediante metadatos literales, variables o de flujo de trabajo, y un archivo JSON**: un servicio puede tener varios argumentos. Seleccione la opción para obtener el valor de los argumentos de servicio de una propiedad de metadatos de flujo de trabajo, un objeto JSON o una variable, o indique directamente el valor en el cuadro de texto proporcionado:

   * **Literal:** utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, srose@we.info.
   * **Variable:** utilice la opción para recuperar el valor almacenado en una variable.
   * **Recuperar a partir de metadatos de flujo de trabajo:** utilice la opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Por ejemplo, emailAddress.
   * **[!UICONTROL Relativo a la carga útil]**: utilice la opción para recuperar el archivo adjunto guardado en una ruta relativa a la carga útil. Seleccione la opción y especifique el nombre de la carpeta que incluye el archivo adjunto o especifique el nombre del archivo adjunto en el cuadro de texto.

     Por ejemplo, si la carpeta Relativo a la carga útil en el repositorio CRX incluye un archivo adjunto en la ubicación `attachment\attachment-folder`, especifique `attachment\attachment-folder` en el cuadro de texto después de seleccionar la variable **[!UICONTROL Relativo a la carga útil]**.
   * **Notación de puntos JSON:** utiliza la opción cuando el valor que desea utilizar esté en un archivo JSON. Por ejemplo, insurance.customerDetails.emailAddress. La opción de notación de puntos JSON solo estará disponible si se selecciona la opción Asignar campos de entrada desde la entrada JSON.
   * **Asignar campos de entrada desde la entrada JSON:** especifica la ruta de un archivo JSON para obtener el valor de entrada de algunos argumentos de servicio del archivo JSON. La ruta del archivo JSON puede ser relativa a la carga útil, una ruta de acceso absoluta o puede seleccionar un documento JSON de entrada mediante una variable de tipo JSON o un modelo de datos de formulario.

* **Entrada para servicios > Proporcionar datos de entrada mediante una variable o un archivo JSON:** seleccione la opción para obtener valores para todos los argumentos de un archivo JSON guardado en una ruta de acceso absoluta, en una ruta relativa a la carga útil o en una variable.
* **Seleccionar el documento JSON de entrada mediante:** el archivo JSON que contiene valores para todos los argumentos de servicio. La ruta del archivo JSON puede ser **relativa a la carga útil** o una **ruta de acceso absoluta.** También puede recuperar el documento JSON de entrada mediante una variable de tipo de datos JSON o un modelo de datos de formulario.

* **Notación de puntos JSON:** deja el campo en blanco para utilizar todos los objetos del archivo JSON especificado como entrada para argumentos de servicio. Para leer un objeto JSON específico del archivo JSON especificado como entrada para los argumentos del servicio, especifique la notación de puntos para el objeto JSON. Por ejemplo, si tiene un archivo JSON similar al listado al principio de la sección, especifique insurance.customerDetails para proporcionar todos los detalles de un cliente como entrada al servicio.
* **Resultados del servicio > Asignación y escritura de valores de salida en variables o metadatos:** selecciona la opción para guardar los valores de salida como propiedades del nodo de metadatos de instancia del flujo de trabajo en el repositorio CRX. Especifique el nombre de la propiedad de metadatos y seleccione el atributo de salida del servicio correspondiente que se va a asignar con la propiedad de metadatos. Por ejemplo, asigne el número de teléfono devuelto por el servicio de salida con la propiedad phone_number (número de teléfono) de los metadatos del flujo de trabajo. Del mismo modo, se puede almacenar la salida en una variable de tipo de datos de registro. Al seleccionar una propiedad para la opción **[!UICONTROL Atributo de salida del servicio que se va a asignar]**, solo se rellenan las variables capaces de almacenar datos de la propiedad seleccionada para la opción **[!UICONTROL Guardar la salida en]**.

* **Resultados del servicio > Guardar resultados en una variable o un archivo JSON:** selecciona la opción para guardar los valores de salida en un archivo JSON en una ruta de acceso absoluta, en una ruta relativa a la carga útil o en una variable.
* **Guardar documento JSON de salida con las siguientes opciones:** guarda el archivo JSON de salida. La ruta del archivo JSON de salida puede ser relativa a la carga útil o a una ruta de acceso absoluta. También puede guardar el archivo JSON de salida con una variable de tipo de datos JSON o un modelo de datos de formulario.

## Paso para firmar el documento {#sign-document-step}

El paso Firmar documento le permite utilizar Adobe Sign para firmar documentos. El paso Firmar documento tiene las siguientes propiedades:

* **Nombre del contrato:** especifica el título del contrato. El nombre del acuerdo forma parte del asunto y del texto del cuerpo del correo electrónico enviado a los destinatarios. Puede almacenar el nombre en una variable de tipo de datos de cadena o seleccionar **Literal** para agregar el nombre manualmente.

* **Configuración regional:** especifica el idioma para las opciones de correo electrónico y de verificación. Puede almacenar la configuración regional en una variable de tipo de datos de cadena o seleccionar **Literal** para elegir la configuración regional de la lista de opciones disponibles. Definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

* **Configuración de Adobe Sign Cloud**: elige una configuración de Adobe Sign Cloud. Si no ha configurado Adobe Sign para AEM Forms, consulte [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Seleccionar documento para firmar mediante:** puede elegir un documento de una ubicación relativa a la carga útil, utilizar la carga útil como documento, especificar una ruta de acceso absoluta del documento o recuperar el documento almacenado en una variable con un tipo de datos Doc.


* **Seleccionar ruta de acceso de los datos adjuntos de entrada mediante:** ruta de los archivos adjuntos. Estos archivos adjuntos se incluyen en el documento de firma. Puede mantener los archivos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los archivos adjuntos o recuperar los archivos adjuntos almacenados en una variable de matriz con un tipo de datos Doc.


  Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntarán al documento de firma. Si hay archivos disponibles en las carpetas accesibles directamente en la ruta de datos de los archivos adjuntos especificada, los archivos se incluirán en el documento de firma como archivos adjuntos. Si hay carpetas en carpetas accesibles directamente, esas carpetas se omiten.

* **Días hasta la fecha límite:** un documento se marca como vencido (fecha límite superada) después de que no haya actividad en la tarea durante el número de días especificado en el campo **Días hasta la fecha límite**. El número de días se cuenta después de que el documento se asigne a un usuario para su firma.
* **Frecuencia del correo electrónico de recordatorio:** puede enviar un correo electrónico de recordatorio a intervalos diarios o semanales. La semana se cuenta desde el día en que se asigna el documento a un usuario para su firma.
* **Proceso de firma:** puede optar por firmar un documento en orden secuencial o paralelo. En orden secuencial, un solo destinatario recibe el documento a la vez para su firma. Una vez que el primer destinatario completa la firma del documento, este se envía al segundo destinatario, y así sucesivamente. En orden paralelo, varios destinatarios pueden firmar un documento a la vez.
* **URL de redireccionamiento:** especifica una URL de redireccionamiento. Una vez firmado el documento, puede redirigir al usuario asignado a una dirección URL. Normalmente, esta URL contiene un mensaje de agradecimiento o instrucciones adicionales.
* **Fase del flujo de trabajo:** un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM. Puede definir estas fases en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Fases).
* **Seleccionar destinatarios:** Especifique el método para elegir el destinatario para el documento. Puede asignar dinámicamente el flujo de trabajo a un usuario o grupo, o agregar manualmente los detalles de un firmante. Al seleccionar Manualmente en el menú desplegable, se agregan detalles del destinatario como Correo electrónico, Función y Método de autenticación.

  >[!NOTE]
  >
  >* En la sección Función, puede especificar la función de destinatario como Firmante, Aprobador, Aceptante, Destinatario certificado, Rellenador de formulario y Delegador.
  >* Si selecciona Delegador en la opción Función, el Delegado puede asignar la tarea de firma a otros destinatarios.
  >* Si ha configurado un método de autenticación para [!DNL Adobe Sign], en función de su configuración, seleccionará un método de autenticación, como autenticación basada en el teléfono, autenticación basada en la identidad social, autenticación basada en el conocimiento o autenticación basada en la identidad oficial.


* **Script o servicio para seleccionar destinatarios:** La opción solo está disponible si selecciona Dinámicamente en el campo Seleccionar destinatarios. Puede especificar un ECMAScript o un servicio para elegir destinatarios y opciones de verificación para un documento.
* **Detalles del destinatario:** La opción solo está disponible si la opción Manualmente está seleccionada en el campo Seleccionar destinatarios. Especifique la dirección de correo electrónico y elija un mecanismo de verificación opcional. Antes de seleccionar un mecanismo de verificación de 2 pasos, asegúrese de que la opción de verificación correspondiente esté habilitada para la cuenta configurada de Adobe Sign. Puede utilizar una variable del tipo de datos de cadena para los campos **[!UICONTROL Correo electrónico]**, **[!UICONTROL Código de país]** y **[!UICONTROL Número de teléfono]**. Los campos **[!UICONTROL Código de país]** y **[!UICONTROL Número de teléfono]** solo se mostrarán si selecciona **[!UICONTROL Verificación por teléfono]** de la lista desplegable **[!UICONTROL verificación en dos pasos]**.
* **Variable de estado:** un documento habilitado para Adobe Sign almacena el estado de la firma del documento en una variable de tipo de datos en cadena. Especifique el nombre de la variable de estado (adobeSignStatus). Una variable de estado de una instancia está disponible en CRXDE en /etc/workflow/instances/&lt;server>/&lt;date-time>/&lt;instance of workflow model>/workItems/&lt;node>/metaData contiene el estado de una variable.
* **[!UICONTROL Documento firmado]**: puede guardar el estado del documento firmado en Variable. Para añadir una pista de auditoría de firma electrónica para una mayor seguridad y legalidad al documento firmado, puede Incluir informe de auditoría. Puede guardar el documento firmado mediante variable o carpeta de carga útil.
  >[!NOTE]
  >
  > El informe de auditoría se añade a la última página del documento firmado.
<!--
* **Save signed document using below options:** Specify the location to keep signed documents. You can choose to overwrite the payload file, place the signed document at a location within the payload directory, or store the signed document in a variable of Document type.
-->

## Pasos de Servicios de documentos {#document-services-steps}

Los Servicios de documentos de AEM son un conjunto de servicios para crear, combinar y asegurar documentos PDF. AEM Forms proporciona un paso de AEM Workflow independiente para cada servicio de documentos.

Al igual que otros pasos del flujo de trabajo de AEM Forms, como Asignar tarea, Enviar correo electrónico y Firmar documento, puede utilizar variables en todos los pasos de los servicios de documentos de AEM. Para obtener información sobre la creación y la administración de variables, consulte [Variables en flujos de trabajo de AEM](../../forms/using/variable-in-aem-workflows.md).

### Paso Aplicar marca de fecha y hora a un documento {#apply-document-time-stamp-step}

Agregar una marca de hora a un documento. Proporcione detalles del documento, como la ruta y el nombre del documento de entrada y la ubicación para almacenar los datos exportados. Puede elegir entre sobrescribir el archivo de carga útil existente, elegir un nombre de archivo diferente para almacenar datos en un archivo diferente en la carpeta de carga útil, proporcionar una ruta absoluta a los datos o almacenar datos en una variable de tipo de datos Document.

### Paso Convertir en imagen {#convert-to-image-step}

Convierte el documento PDF a una lista de imágenes. Los formatos de imagen compatibles son JPEG, JPEG2000, PNG y TIFF. La siguiente información se aplica a las conversiones a imágenes de TIFF:

* Se genera un archivo TIFF de varias páginas.
* Algunas anotaciones no se incluyen en las imágenes de TIFF. No se incluyen las anotaciones que requieren que Acrobat genere su apariencia.

### Paso para convertir a PDF/A {#convert-to-pdf-a-step}

Convierte un documento PDF a formato PDF/A mediante las opciones proporcionadas. La versión del PDF/A de Portable Document Format (PDF) está especializada en archivar y conservar documentos a largo plazo.

### Paso Convertir a PS {#convert-to-ps-step}

Convertir documentos PDF a PostScript. Al convertir a PostScript, puede utilizar la operación de conversión para especificar el documento de origen y si desea convertir a PostScript de nivel 2 o 3. El documento PDF que convierta a un archivo PostScript no debe ser interactivo.

### Paso Crear PDF a partir del tipo especificado {#create-pdf-from-specified-type-step}

Genere un documento PDF a partir de un archivo de entrada. El documento de entrada puede ser relativo a la carga útil, tener una ruta de acceso absoluta, puede proporcionarse como carga útil o almacenarse en una variable con un tipo de datos Doc.

### Paso Crear PDF desde URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Genera un documento PDF a partir de la dirección URL, el HTML y el archivo ZIP proporcionados.

### Paso Exportar datos {#export-data-step}

Exporta datos de un archivo de formularios PDF o de un XDP. Es necesario que introduzca la ruta de archivo del documento de entrada y el formato de datos de exportación. Las opciones de formato de datos de exportación son Auto, XDP y XmlData.

### Paso Exportar PDF al tipo especificado {#export-pdf-to-specified-type-step}

Convierte un documento PDF en un formato seleccionado.

### Paso Generar PDF no interactivo {#generatenoninteractive}

Genera un PDF no interactivo. Proporciona varias opciones de personalización.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de la plantilla para los documentos de entrada. Almacena la ruta del archivo de plantilla en una variable del tipo de datos en cadena.

### Paso Importar datos {#import-data-step}

Combina datos de formulario en un formulario PDF. Puede importar datos de formulario en un formulario PDF.

### Paso para invocar DDX {#invokeddx}

Ejecuta el archivo DDX en el mapa especificado de documentos de entrada y devuelve los documentos PDF manipulados.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo DDX para los documentos de entrada. Almacena el archivo DDX en una variable de tipo de datos Document o XML.

### Paso Optimizar PDF {#optimize-pdf-step}

Optimiza los archivos PDF al reducir su tamaño. El resultado de esta conversión son archivos PDF que pueden ser menores que sus versiones originales. Esta operación también convierte los documentos PDF a la versión PDF especificada en los parámetros de optimización.

La configuración de optimización especifica cómo se optimizan los archivos. A continuación se muestra un ejemplo de configuración:

* Versión del PDF objetivo
* Descartar objetos, como acciones de JavaScript y miniaturas de páginas incrustadas
* Descartar datos de usuario, como comentarios y archivos adjuntos
* Descartar configuración no válida o no utilizada
* Comprimir datos sin comprimir o usar algoritmos de compresión más eficientes
* Eliminar fuentes incrustadas
* Configurar valores de transparencia

### Paso Procesar formulario PDF {#renderpdf}

Procesa un formulario creado en Forms Designer (XDP) en un formulario de PDF.

>[!NOTE]
>
>Puede utilizar variables para especificar el archivo de la plantilla para los documentos de entrada. Almacena la ruta del archivo de plantilla en una variable del tipo de datos en cadena.

### Paso Proteger documento {#secure-document-step}

Cifrar, firmar y certificar un documento. AEM Forms admite el cifrado basado en contraseña y en certificado. También puede elegir entre varios algoritmos para firmar documentos. Por ejemplo, SHA-256 y SH-512. También puede utilizar el paso del flujo de trabajo para ampliar los documentos PDF. El paso del flujo de trabajo ofrece la opción de habilitar la descodificación de código de barras, las firmas digitales, la importación y exportación de datos de PDF y otras opciones.

### Paso Enviar a la impresora {#send-to-printer-step}

Envíe un documento directamente a una impresora. Admite los siguientes mecanismos de acceso a la impresión:

* **Impresora de acceso directo:** una impresora instalada en el mismo equipo se denomina impresora de acceso directo y el equipo se denomina host de impresora. Este tipo de impresora puede ser una impresora local que esté conectada al equipo directamente.
* **Impresora de acceso indirecto:** se accede a la impresora instalada en un servidor de impresión desde otros equipos. Tecnologías como el sistema de impresión común UNIX® (CUPS) y el protocolo Line Printer Daemon (LPD) están disponibles para conectarlos a una impresora de la red. Para acceder a una impresora de acceso indirecto, especifique la IP o el nombre de host del servidor de impresión. Con este mecanismo, puede enviar un documento a un URI LPD cuando la red tenga un LPD en ejecución. El mecanismo permite enrutar el documento a cualquier impresora que esté conectada a la red que tenga una LPD en ejecución.

### Paso Generar una salida impresa {#generatePrintedOutput}

El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL a partir de un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le aplica un formato para imprimirlo. La salida generada por este paso se puede enviar directamente a una impresora o guardarse como archivo. Se recomienda utilizar este paso cuando desee utilizar diseños de formulario o datos de una aplicación. Si los diseños de formulario se encuentran en la red, el sistema de archivos local o la ubicación HTTP, utilice la operación generatePrintedOutput.

Por ejemplo, la aplicación requiere que combine un diseño de formulario con un archivo de datos. Los datos contienen cientos de registros. Además, requiere que la salida se envíe a una impresora compatible con ZPL. El diseño de formulario y los datos de entrada se encuentran en una aplicación. Utilice la operación generatePrintedOutput para combinar cada registro con un diseño de formulario y enviar la salida a una impresora compatible con ZPL.

El paso Generar salida impresa tiene las siguientes propiedades:

**Propiedades de entrada**

* **[!UICONTROL Seleccionar el archivo de plantilla mediante:]** especifica la ruta del archivo de la plantilla. Puede seleccionar la plantilla mediante la ruta relativa a la carga útil, guardada en una ruta absoluta o mediante una variable de tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla. Además, también puede aceptar la carga útil como archivo de datos de entrada.

* **[!UICONTROL Seleccionar documento de datos mediante]**: especificar la ruta de un archivo de datos de entrada. Puede seleccionar los datos de entrada mediante la ruta relativa a la carga útil, guardada en una ruta absoluta o mediante una variable de tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

* **[!UICONTROL Formato de impresora]**: valor del formato de impresión que especifica el idioma de descripción de la página que se utilizará, cuando no se proporcione un archivo XDC, para generar el flujo de salida. Si proporciona un valor literal, seleccione uno de estos valores:

   * **[!UICONTROL PCL personalizado]**: utilice la opción para especificar un archivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript personalizado]**: utilice la opción para especificar un archivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL personalizado]**: use la opción para especificar un archivo XDC personalizado para ZPL.
   * **[!UICONTROL Color genérico PCL (5c)]**: utilice un PCL de color genérico (5c).
   * **[!UICONTROL PostScript genérico Level3]**: utilice PostScript de nivel 3 genérico.
   * **[!UICONTROL ZPL 300 DPI]**: utilice ZPL 300 DPI. Se utiliza zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: utilice ZPL 600 DPI. Se utiliza el archivo zpl600.xdc.
   * **[!UICONTROL IPL personalizado]**: utilice la opción para especificar un archivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 DPI]**: utilice IPL 300 DPI. Se utiliza ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: utilice IPL 400 DPI. Se utiliza el archivo ipl400.xdc.
   * **[!UICONTROL TPCL personalizado]**: utilice la opción para especificar un archivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: utilice TPCL 300 DPI. Se utiliza el archivo tpcl305.xdc.
   * **[!UICONTROL PCL 600 DPI]**: utilice TPCL 600 DPI. Se utiliza el archivo tpcl600.xdc.
   * **[!UICONTROL DPL personalizado]**: utilice la opción para especificar un DPL de archivo XDC personalizado.
   * **[!UICONTROL DPL300DPI]**: utilice DPL 300 DPI. Se utiliza el archivo dpl300.xdc.
   * **[!UICONTROL DPL406DPI]**: utilice DPL 400 DPI. Se utiliza el dpl406.xdc.
   * **[!UICONTROL DPL600DPI]**: utilice DPL 600 DPI. Se utiliza el dpl600.xdc.

**Propiedades de salida**

* **[!UICONTROL Guardar documento de salida mediante]**: especifica la ubicación para guardar el archivo de salida. Puede guardar el archivo de salida en una ubicación relativa a la carga útil, en una variable o especificar una ubicación absoluta para guardar el archivo de salida. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

**Propiedades avanzadas**

* **[!UICONTROL Seleccionar la ubicación raíz del contenido mediante]**: la raíz del contenido es un valor de cadena que especifica el URI, la referencia absoluta o la ubicación en el repositorio para recuperar los recursos relativos que utiliza el diseño de formulario. Por ejemplo, si el diseño de formulario hace referencia a una imagen de forma relativa, como ../myImage.gif, myImage.gif debe estar ubicado en repository://. El valor predeterminado es repository://, que apunta al nivel raíz del repositorio.

  Cuando elige un recurso de la aplicación, la ruta del URI raíz del contenido debe tener la estructura correcta. Por ejemplo, si se selecciona un formulario de una aplicación denominada SampleApp y se coloca en SampleApp/1.0/forms/Test.xdp, el URI de raíz de contenido debe especificarse como repository://administrator@password/Applications/SampleApp/1.0/forms/ o repositorio:/Applications/SampleApp/1.0/forms/ (cuando la autoridad sea nula). Cuando se especifica el URI de raíz de contenido de esta manera, las rutas de todos los recursos a los que se hace referencia en el formulario se resuelven en relación con este URI.

* **[!UICONTROL Seleccionar el archivo XCI mediante]**: los archivos XCI se utilizan para describir fuentes y otras propiedades que se utilizan para elementos de diseño de formulario. Puede mantener un archivo XCI relativo a la carga útil, en una ruta absoluta o mediante una variable del tipo de datos Document.

* **[!UICONTROL Configuración regional]**: especifica el idioma que se utiliza para generar el documento PDF. Si proporciona un valor literal, seleccione un idioma de la lista o seleccione uno de estos valores:
   * **Para usar el servidor predeterminado**: (Predeterminado) Use la configuración regional configurada en el servidor de AEM Forms. La configuración regional se configura con la consola de administración. (Consulte [Ayuda de Designer](https://www.adobe.com/go/learn_aemforms_designer_65)).

   * **Para utilizar un valor personalizado**: escriba el código de configuración regional en el cuadro literal o seleccione una variable de cadena que contenga el código de configuración regional. Para obtener una lista completa de los códigos de configuración regional admitidos, consulte https://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copias]**: valor entero que especifica el número de copias que se generarán para la salida. El valor predeterminado es 1.

* **[!UICONTROL Impresión a doble cara]**: valor de Paginación que especifica si se utiliza la impresión a doble o a una sola cara. Las impresoras compatibles con PostScript y PCL utilizan este valor. Si proporciona un valor literal, seleccione uno de estos valores:
   * **[!UICONTROL Borde largo a doble cara]**: utiliza la impresión a doble cara y la impresión mediante paginación de borde largo.
   * **[!UICONTROL Borde corto a doble cara]**: utiliza la impresión a doble cara y la impresión mediante paginación de borde corto.
   * **[!UICONTROL Simple]**: utiliza la impresión a una sola cara.
