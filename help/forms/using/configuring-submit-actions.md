---
title: Configurar la acción de envío
description: Forms permite configurar una acción de envío para definir cómo se procesa un formulario adaptable después del envío. Puede utilizar acciones de envío integradas o escribir las suyas propias desde cero.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 94%

---

# Configurar la acción de envío {#configuring-the-submit-action}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | Este artículo |


## Introducción al envío de acciones {#introduction-to-submit-actions}

Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Puede configurar la acción de envío en el formulario adaptable. Los formularios adaptables proporcionan algunas acciones de envío listas para usar. También puede copiar y ampliar las acciones de envío predeterminadas para crear la suya propia. Sin embargo, según sus necesidades, puede escribir y registrar su propia acción de envío para procesar los datos en el formulario enviado. Una acción de envío puede utilizar [el envío sincrónico o asincrónico](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Puede configurar una acción de envío en la sección **Envío** de las propiedades del contenedor del formulario adaptable, en la barra lateral.

![Configurar la acción de envío](assets/thank-you-setting.png)

Configurar la acción de envío

Las acciones de envío predeterminadas disponibles con los formularios adaptables son las siguientes:

* Enviar al punto final REST
* Enviar correo electrónico
* Enviar PDF por correo electrónico
* Invocar un flujo de trabajo de formularios
* Enviar mediante modelo de datos de formulario
* Acción de envío de portal de formularios
* Invocar un flujo de trabajo de AEM
* Enviar a Power Automate

>[!NOTE]
>
>La acción Enviar PDF por correo electrónico solo se aplica a los formularios adaptables que utilizan una plantilla XFA como modelo de formulario.

>[!NOTE]
>
>Asegúrese de que el archivo [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM
>existe. Necesitará el directorio para almacenar los archivos adjuntos temporalmente. Si el directorio no existe, créelo.

>[!CAUTION]
>
>Si [rellena previamente](../../forms/using/prepopulate-adaptive-form-fields.md) una plantilla de formulario, un modelo de datos de formulario o un formulario adaptable basado en esquemas con datos XML o JSON reclamados a un esquema (esquema XML, esquema JSON, plantilla de formulario o modelo de datos de formulario) cuyos datos no contengan las etiquetas &lt;afData>, &lt;afBoundData> y &lt;/afUnboundData>, los datos de los campos no enlazados (los campos no enlazados son campos de formularios adaptables sin la propiedad [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) ) del formulario adaptable se perderán.

Puede escribir una acción de envío personalizada para formularios adaptables para que cumplan con su caso de uso. Para obtener más información, consulte [Escribir una acción de envío personalizada para formularios adaptables](../../forms/using/custom-submit-action-form.md).

## Enviar al punto final REST {#submit-to-rest-endpoint}

La opción de envío **Enviar al punto final REST** envía los datos rellenados en el formulario a una página de confirmación configurada como parte de la petición HTTP GET. Puede agregar el nombre de los campos que desea solicitar. El formato de la solicitud es el siguiente:

`{fieldName}={request parameter name}`

Como se muestra en la siguiente imagen, `param1` y `param2` se pasan como parámetros con valores copiados de los campos **cuadro de texto** y **del cuadro numérico** para la siguiente acción.

También puede **Habilitar la petición POST** y proporcionar una URL para publicar la solicitud. Para enviar datos al servidor de Experience Manager que aloja el formulario, utilice una ruta relativa correspondiente a la ruta raíz del servidor de Experience Manager. Por ejemplo, /content/forms/af/SampleForm.html. Para enviar datos a cualquier otro servidor, utilice la ruta absoluta.

![Configurar la acción de envío del punto final de REST.](assets/action-config.png)

Configurar la acción de envío del punto final de REST.

>[!NOTE]
>
Para pasar los campos como parámetros en una URL REST, todos los campos deben tener nombres de elementos diferentes, incluso si se colocan en paneles diferentes.

### Publicar datos enviados en un recurso o punto final REST externo  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Utilice la acción **Enviar al punto final REST** para publicar los datos enviados en una URL de REST. La URL puede ser de un servidor interno (el servidor en el que se procesa el formulario) o externo.

Para enviar datos a un servidor interno, proporcione la ruta del recurso. Los datos se publican en la ruta del recurso. Por ejemplo, /content/restEndPoint. Para esas peticiones POST se utiliza la información de autenticación de la solicitud de envío.

Para enviar datos a un servidor externo, proporcione una URL. El formato de la dirección URL es https://host:port/path_to_rest_end_point. Asegúrese de configurar la ruta para controlar la petición POST de forma anónima.

![Asignación de valores de campo pasados como parámetros de la página de agradecimiento](assets/post-enabled-actionconfig.png)

En el ejemplo anterior, el usuario ha escrito información en `textbox` y se captura mediante el parámetro `param1`. La sintaxis para anunciar datos capturados con `param1` es la siguiente:

`String data=request.getParameter("param1");`

Del mismo modo, los parámetros que utiliza para publicar datos XML y archivos adjuntos son `dataXml` y `attachments`.

Por ejemplo, utiliza estos dos parámetros en el script para analizar los datos en un punto final de REST. Se utiliza la siguiente sintaxis para almacenar y analizar los datos:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

En este ejemplo, `data` almacena los datos XML y `att` almacena datos adjuntos.

## Enviar correo electrónico {#send-email}

Puede usar la acción de envío **Enviar correo electrónico** para enviar un correo electrónico a uno o varios destinatarios cuando el formulario se haya enviado correctamente. El correo electrónico generado puede contener datos de formulario en un formato predefinido.

>[!NOTE]
>
Todos los campos del formulario deben tener nombres de elemento diferentes, incluso si se colocan en paneles diferentes), para incluir los datos del formulario en un mensaje de correo electrónico.

## Enviar PDF por correo electrónico {#send-pdf-via-email}

La acción de envío **Enviar PDF por correo electrónico** envía un mensaje de correo electrónico con un PDF que contiene datos del formulario a uno o varios destinatarios cuando el formulario se envía correctamente.

>[!NOTE]
>
Esta acción de envío está disponible para formularios adaptables basados en XFA y en XSD que tienen la plantilla Documento de registro.

## Invocar un flujo de trabajo de formularios {#invoke-a-forms-workflow}

La acción de envío **Enviar al flujo de trabajo de Forms** envía un xml de datos y archivos adjuntos (si los hay) a un Adobe LiveCycle existente o a AEM Forms en un proceso JEE.

Para obtener información sobre cómo configurar la acción Enviar a la acción de envío del flujo de trabajo de Forms, consulte [Enviar y procesar los datos del formulario mediante flujos de trabajo de formulario](../../forms/using/submit-form-data-livecycle-process.md).

## Enviar mediante modelo de datos de formulario {#submit-using-form-data-model}

La acción de envío **Enviar mediante el modelo de datos de formulario** escribe los datos del formulario adaptable enviados para el objeto del modelo de datos especificado en un modelo de datos de formulario en su fuente de datos. Al configurar la acción de envío, puede elegir un objeto de modelo de datos cuyos datos enviados desee volver a escribir en su fuente de datos.

Además, puede enviar a la fuente de datos un archivo adjunto de formulario mediante un modelo de datos de formulario y un documento de registro (DoR).

Para obtener información sobre el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

## Acción de envío de portal de formularios {#forms-portal-submit-action}

La opción **Acción de envío del portal de formularios** hace que los datos de formulario estén disponibles a través del portal de AEM Forms.

Para obtener más información sobre el portal de formularios y la acción de envío, consulte [Componente Borradores y presentaciones](../../forms/using/draft-submission-component.md).

## Invocar un flujo de trabajo de AEM {#invoke-an-aem-workflow}

La acción de envío **[!UICONTROL Invocar un flujo de trabajo de AEM]** asocia un formulario adaptable con un [Flujo de trabajo de AEM](/help/sites-developing/workflows-models.md). Cuando se envía un formulario, el flujo de trabajo asociado se inicia automáticamente en la instancia de autor. Puede guardar el archivo de datos, los archivos adjuntos y el documento de registro en la ubicación de carga útil del flujo de trabajo o en una variable. Si el flujo de trabajo está marcado para almacenar datos externos, estará disponible la opción de variable y no la de carga útil. Puede seleccionar de la lista de variables disponibles para el modelo de flujo de trabajo. Si el flujo de trabajo está marcado para el almacenamiento de datos externos en una fase posterior y no en el momento de la creación del flujo de trabajo, asegúrese de que las configuraciones de variables requeridas estén establecidas.

Antes de usar la acción de envío **Invocar un flujo de trabajo de AEM**, [configure el DS de Experience Manager](../../forms/using/configuring-the-processing-server-url.md). Para obtener información sobre crear un flujo de trabajo de AEM, consulte [Flujos de trabajo centrados en formularios en OSGi](../../forms/using/aem-forms-workflow.md).

La acción de envío coloca lo siguiente en la ubicación de carga útil del flujo de trabajo. Sin embargo, tenga en cuenta que solo se mostrará la opción Variable si el modelo de flujo de trabajo está marcado para almacenar datos externos y no para la opción de carga útil.

* **Archivo de datos**: Contiene datos enviados al formulario adaptable. Puede usar la opción **[!UICONTROL Ruta del archivo de datos]** para especificar el nombre y la ruta del archivo en relación con la carga útil. Por ejemplo, la ruta `/addresschange/data.xml` crea una carpeta llamada `addresschange` y la coloca en relación a la carga útil. También puede especificar únicamente `data.xml` para enviar solo los datos enviados sin crear una jerarquía de carpetas. Utilice la opción Variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.

>[!NOTE]
>
Se pueden utilizar variables tanto si el modelo de flujo de trabajo está marcado para almacenar datos externo como si no.

* **Archivos adjuntos**: Puede usar la opción **[!UICONTROL Ruta de archivos adjuntos]** para especificar el nombre de la carpeta en la que se almacenarán los archivos adjuntos cargados en el formulario adaptable. La carpeta se creará en relación con la carga útil. Si el flujo de trabajo está marcado para el almacenamiento de datos externos, utilice la opción de variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.

* **Documento de registro**: Contiene el documento de registro generado para el formulario adaptable. Puede usar la opción **[!UICONTROL Ruta del documento de registro]** para especificar el nombre y la ruta del documento de registro en relación con la carga útil. Por ejemplo, la ruta `/addresschange/DoR.pdf` crea una carpeta llamada `addresschange` en relación con la carga útil y coloca `DoR.pdf` en relación con la carga útil. También puede especificar únicamente `DoR.pdf` para guardar solo el documento de registro sin crear una jerarquía de carpetas. Si el flujo de trabajo está marcado para el almacenamiento de datos externos, utilice la opción de variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.

## Enviar a Power Automate {#microsoft-power-automate}

Puede configurar un formulario adaptable para ejecutar un flujo de nube de Microsoft® Power Automate en el envío. El formulario adaptable configurado envía los datos capturados, los archivos adjuntos y el documento de registro al flujo de nube de Power Automate para su procesamiento. Le ayuda a crear una experiencia de captura de datos personalizados mientras aprovecha el poder de Microsoft® Power Automate para crear lógicas empresariales en torno a los datos capturados y automatizar los flujos de trabajo de los clientes. A continuación se muestran algunos ejemplos de lo que puede hacer después de integrar un formulario adaptable con Microsoft® Power Automate:

* Usar datos de formularios adaptables en procesos empresariales de Power Automate
* Utilice Power Automate para enviar datos capturados a más de 500 fuentes de datos o a cualquier API disponible públicamente
* Realizar cálculos complejos en los datos capturados
* Guardar datos de formularios adaptables en sistemas de almacenamiento con una programación predefinida

El editor de formularios adaptables ofrece la acción de envío **Invocar un flujo de Microsoft® Power Automate** para enviar datos de formularios adaptables, archivos adjuntos y documentos de registro a flujos de nube de Power Automate. Para usar la acción Enviar para enviar los datos capturados a Microsoft® Power Automate, [Conecte la instancia de AEM Forms con Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md)

Después de una configuración correcta, utilice la acción de envío [Invocar un flujo de Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) para enviar datos a un flujo de Power Automate.

## Enviar a la lista de Microsoft® SharePoint{#submit-to-sharedrive}

>[!NOTE]
>
La característica Enviar a Microsoft® SharePoint List se introdujo con AEM 6.5 Forms Service Pack 19 (6.5.19.0).

La acción de envío **[!UICONTROL Enviar a SharePoint]** conecta un formulario adaptable con un almacenamiento de Microsoft® SharePoint. Puede enviar el archivo de datos de formulario, los archivos adjuntos o el documento de registro al almacenamiento de Microsoft® SharePoint conectado.

### Conectar un formulario adaptable a la lista de Microsoft® SharePoint {#connect-af-sharepoint-list}

Para conectar un formulario adaptable a la lista de Microsoft® SharePoint:

1. [Crear una configuración de lista de SharePoint](#create-sharepoint-list-configuration): conecta AEM Forms a su almacenamiento de de lista de Sharepoint de Microsoft®.
1. [Use la acción de envío **Enviar mediante el modelo de datos de formulario** en un formulario adaptable](#use-submit-using-fdm): envía los datos del formulario adaptable al SharePoint de Microsoft® configurado.

#### Crear configuración de lista de SharePoint {#create-sharepoint-list-configuration}

Para conectar AEM Forms a su lista de Sharepoint de Microsoft®:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Seleccione un **Contenedor de configuración**. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Lista de SharePoint]** en la lista desplegable. Aparecerá el asistente de configuración de SharePoint.
1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL URL de OAuth]**. Para obtener información sobre cómo recuperar el ID de cliente, el secreto de cliente o el ID de inquilino para la URL de OAuth, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).
   * Puede recuperar la variable `Client ID` y `Client Secret` de su aplicación desde el portal de Microsoft® Azure.
   * En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
   * Adición de los permisos de API `offline_access` y `Sites.Manage.All` en la pestaña **Microsoft® Graph** para proporcionar permisos de lectura y escritura. Agregue el permiso `AllSites.Manage` en la ficha **Sharepoint** para interactuar de forma remota con los datos de SharePoint.
   * Use la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

     >[!NOTE]
     >
     El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Haga clic en **[!UICONTROL Conectar]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.
1. Seleccionar **[!UICONTROL Sitio de SharePoint]** y **[!UICONTROL Lista de SharePoint]** en la lista desplegable.
1. Pulse **[!UICONTROL Crear]** para crear la configuración de nube para Microsoft® SharePointList.

#### Usar la acción de envío Enviar con el modelo de datos de formulario en un formulario adaptable {#use-submit-using-fdm}

Puede utilizar la configuración de lista de SharePoint creada en un formulario adaptable para guardar datos o el documento de registro generado en una lista de SharePoint. Siga estos pasos para usar una configuración de almacenamiento de lista de SharePoint en un formulario adaptable como:

1. [Crear un modelo de datos de formulario con Microsoft](/help/forms/using/create-form-data-model.md)
1. [Configurar el modelo de datos de formulario para recuperar y enviar datos](/help/forms/using/work-with-form-data-model.md#configure-services)
1. [Crear un formulario adaptable](/help/forms/using/create-adaptive-form.md).
1. [Configurar la acción de envío mediante un modelo de datos de formulario](/help/forms/using/configuring-submit-actions.md#submit-using-form-data-model-submit)

Al enviar el formulario, los datos se guardan en el almacenamiento de lista de Sharepoint de Microsoft® especificado.

>[!NOTE]
>
En la lista de Microsoft® SharePoint, no se admiten los siguientes tipos de columnas:
* columna de imagen
* columna de metadatos
* columna de persona
* columna de datos externos


>[!NOTE]
>
Para establecer los valores de una configuración, [Generar configuraciones OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implemente la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) a su instancia de Cloud Service.

## Revalidación del lado del servidor en formularios adaptables {#server-side-revalidation-in-adaptive-form}

Normalmente, en cualquier sistema de captura de datos en línea, los desarrolladores colocan algunas validaciones de JavaScript en el lado del cliente para aplicar algunas reglas empresariales. Sin embargo, en los exploradores modernos, los usuarios finales tienen la forma de evitar esas validaciones y realizar envíos manualmente mediante diversas técnicas, como la consola de desarrolladores del explorador web. Estas técnicas también son válidas para formularios adaptables. Un desarrollador de formularios puede crear varias lógicas de validación, pero técnicamente, los usuarios finales pueden omitir esas lógicas de validación y enviar datos no válidos al servidor. Los datos no válidos romperían las reglas empresariales que ha impuesto un autor de formularios.

La característica de revalidación del lado del servidor permite ejecutar también las validaciones que ha proporcionado un autor de formularios adaptables al diseñar un formulario adaptable en el servidor. Evita cualquier posible compromiso en el envíos de datos y violaciones de reglas empresariales representadas en términos de validaciones de formularios.

### ¿Qué se debe validar en el servidor? {#what-to-validate-on-server-br}

Todas las validaciones de campo listas para usar de un formulario adaptable que se vuelven a ejecutar en el servidor son las siguientes:

* Requerido
* Cláusula de imagen de validación
* Expresión de validación

### Habilitar la validación del lado del servidor {#enabling-server-side-validation-br}

Utilice **Revalidar en el servidor** en el contenedor de formularios adaptables en la barra lateral para habilitar o deshabilitar la validación del lado del servidor para el formulario actual.

![Habilitar la validación del lado del servidor](assets/revalidate-on-server.png)

Habilitar la validación del lado del servidor

Si el usuario final omite esas validaciones y envía los formularios, el servidor volverá a realizar la validación. Si la validación falla al final del servidor, se detendrá la transacción del envío. Al usuario final se le volverá a presentar el formulario original. Los datos capturados y enviados se presentarán al usuario como un error.

>[!NOTE]
>
La validación del lado del servidor valida el modelo de formulario. Se recomienda crear una biblioteca de cliente independiente para las validaciones y no mezclarla con otras cosas como el estilo del HTML y la manipulación DOM en la misma biblioteca de cliente.

### Compatibilidad con funciones personalizadas en expresiones de validación {#supporting-custom-functions-in-validation-expressions-br}

A veces, si hay reglas de validación complejas, el script de validación exacta reside en funciones personalizadas y el autor llama a estas funciones personalizadas desde la expresión de validación de campo. Para que esta biblioteca de funciones personalizadas sea conocida y esté disponible mientras se realizan las validaciones del lado del servidor, el autor del formulario puede configurar el nombre de la biblioteca de cliente de AEM en la pestaña **Básico** de las propiedades del contenedor del formulario adaptable como se muestra a continuación.

![Compatibilidad con funciones personalizadas en expresiones de validación](assets/clientlib-cat.png)

Compatibilidad con funciones personalizadas en expresiones de validación

El autor puede configurar la biblioteca customJavaScript para formularios adaptables. En la biblioteca, mantenga solo las funciones reutilizables, que dependen de las bibliotecas de terceros jquery y underscore.js.

## Tratar errores en la acción de envío {#error-handling-on-submit-action}

Como parte de las directrices de seguridad y endurecimiento de Experience Manager, configure páginas de error personalizadas como, 404.jsp y 500.jsp. Se llama a estos controladores cuando aparecen errores 404 o 500 al enviar un formulario. También se llama a los controladores cuando estos códigos de error se activan en el nodo Publish.

Para obtener más información, consulte [Personalizar páginas que muestra el Controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md).
