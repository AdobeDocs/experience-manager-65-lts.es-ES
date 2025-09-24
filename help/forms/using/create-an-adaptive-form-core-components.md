---
title: Crear un formulario adaptable
description: Obtenga información sobre cómo crear un formulario adaptable mediante  [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Descubra más información sobre cómo crear un formulario adaptable basado en un modelo de datos de formulario y un esquema XML o JSON.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: eb857ab1-ab1b-4c77-af3b-4507f53a8241
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 76%

---

# Crear componentes principales basados en Forms adaptable {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe recomienda utilizar los componentes principales para [añadir Formularios adaptables a una página de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) o para [crear Formularios adaptables independientes](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es).

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

Los formularios adaptables le permiten crear formularios que son atractivos, receptivos, dinámicos y adaptables. AEM Forms proporciona una interfaz de usuario fácil de usar para las empresas que crea rápidamente Forms adaptable. La IU de ofrece una navegación rápida por las pestañas para seleccionar fácilmente plantillas, estilos, campos y opciones de envío preconfiguradas para crear un formulario adaptable.

Antes de empezar, obtenga información sobre el tipo de componentes de Forms disponibles para usted:

* [Componentes principales de formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es): son componentes estandarizados de captura de datos. Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital. Un desarrollador puede personalizar y aplicar estilo fácilmente a estos componentes. Adobe recomienda aprovechar estos componentes modernos y ampliables para desarrollar formularios adaptables.

* [Componentes de base de formularios adaptables](creating-adaptive-form.md): estos son componentes clásicos (antiguos) de captura de datos. Puede seguir utilizándolos para editar su Formulario adaptable basado en componentes de base existentes. Si está creando formularios, Adobe recomienda usar [Componentes principales de Forms adaptable](/help/forms/using/create-adaptive-form.md) para crear un Forms adaptable.

## Requisitos previos

Para crear un formulario adaptable, es necesario lo siguiente:

* **Habilite los componentes principales de Forms adaptable para su entorno**: se requiere la versión 41 o posterior del proyecto de tipo de archivo de AEM para [habilitar los componentes principales para su entorno](/help/forms/using/enable-adaptive-forms-core-components.md). Al habilitar los componentes principales para su entorno, se agregarán a su entorno la plantilla **Forms adaptable (componente principal)** y el tema Lienzo.

* **Una plantilla de formulario adaptable**: Una plantilla ofrece una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. También ofrece opciones para definir una temática y una acción de envío. La temática define la apariencia, y la acción de envío define la acción que debe realizarse al enviar un Formulario adaptable. También puede implementar [plantillas de muestra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es) en su entorno. Esto le ayuda a empezar a crear formularios rápidamente.

  >[!NOTE]
  >
  > Si no tiene la plantilla de **Formularios adaptables (componente principal)** en su entorno, [Habilite los componentes principales de formularios adaptables para su entorno](/help/forms/using/enable-adaptive-forms-core-components.md). Al habilitar los componentes principales para su entorno, la plantilla de **Formularios adaptables (componente principal)** se agrega al entorno.

* **Una temática de formulario adaptable**: Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes.  El tema `Canvas` se agrega de manera predeterminada al habilitar los componentes principales para su entorno. Puedes [descargar y personalizar los temas estándar](create-or-customize-themes-for-adaptive-forms-core-components.md). Para **temas predeterminados**, puede implementar [temas de ejemplo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es) en su entorno. Esto le ayudará a dar estilo a los formularios y le proporcionará una estructura base para crear o personalizar una temática según sus necesidades empresariales.

* **Permisos**: añada sus usuarios al grupo [!DNL forms-users]. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable. Para obtener una lista detallada de los formularios y grupos de usuarios específicos, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Creación de un formulario adaptable {#create-an-adaptive-form}

1. Inicie sesión en [AEM author instance](/help/sites-deploying/deploy.md#author-and-publish-installs) local.

1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Crear Forms adaptable]**.

1. Seleccione una plantilla de componentes principales de Forms adaptable y haga clic en **[!UICONTROL Siguiente]**.

1. Aparecerá **[!UICONTROL Agregar propiedades]**. Especifique los valores para los siguientes campos de propiedad. Los campos Título y Nombre son obligatorios:

   * **[!UICONTROL Título:]** Especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos.
   * **[!UICONTROL Descripción:]** especifica la información detallada sobre el formulario.
   * **[!UICONTROL Biblioteca cliente de temáticas]:** Especifica el tema de un formulario adaptable. De manera predeterminada, el tema `adaptiveform.theme.canvas3` está seleccionado. También puede elegir una temática diferente del menú desplegable **[!UICONTROL Biblioteca cliente de temáticas]**.
   * **[!UICONTROL Contenedor de configuración:]** Define una ubicación donde se almacenan los archivos de configuración para Forms adaptable. Estos archivos de configuración contienen ajustes y propiedades relacionados con el comportamiento y el aspecto de Adaptive Forms.
   * **[!UICONTROL Etiquetas:]** Especifica etiquetas para identificar de forma exclusiva el formulario adaptable. Las etiquetas ayudan a buscar en el formulario. Para crear etiquetas, escriba nuevos nombres de etiqueta en el cuadro **[!UICONTROL Etiquetas]**.
1. Seleccione **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo.


1. Seleccione **[!UICONTROL Editar]** para abrir el formulario recién creado en una pestaña nueva. El formulario se abrirá para editarlo y mostrará el contenido disponible en la plantilla. También muestra la barra lateral para personalizar el formulario recién creado.


## Utilice los componentes principales de Forms adaptable para crear el formulario

Después de abrir el formulario para editarlo, puede utilizar los componentes principales adaptables de Forms disponibles para agregar campos de formulario al formulario. Puede arrastrar y soltar o utilizar la opción + [insertar componente] para agregar estos componentes a un formulario. Consulte la documentación de componentes principales de AEM para obtener más información sobre los [componentes principales de Forms adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es#components) disponibles. También puede visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver los componentes principales disponibles en acción.

## Configuración de una acción de envío para un formulario adaptable {#configure-submit-action-for-form}

Una acción de envío permite elegir el destino de los datos capturados mediante un formulario adaptable. Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Los formularios adaptables incluyen algunas acciones de envío listas para usar. También puede ampliar las acciones de envío predeterminadas para crear su propia acción de envío personalizada. Para configurar una acción de envío para el formulario:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.

1. Haga clic en la pestaña **[!UICONTROL Envío]**.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una acción de envío](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Seleccione y configure una **[!UICONTROL acción de envío]** según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redireccionamiento del usuario a una página o mostrar un mensaje de agradecimiento al enviar el formulario

Al enviar un formulario, puede redirigir al usuario a otra página web o a un mensaje. Para redirigir al usuario o configurar el mensaje de agradecimiento:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable para configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione la opción **[!UICONTROL Redirigir a URL]** y examine y seleccione una página de AEM Sites, o proporcione una URL de una página externa.

   * Para configurar un mensaje personalizado o de agradecimiento, por ejemplo, en la opción Enviar, seleccione la opción **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en la casilla **[!UICONTROL Contenido del mensaje.]** Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

## Configuración de un esquema o un modelo de datos de formulario para un formulario adaptable {#configure-schema-or-data-model-for-form}

Puede utilizar el modelo de datos de formulario para conectar un formulario a una fuente de datos para enviar y recibir datos en función de las acciones del usuario. También puede conectar un formulario a un esquema JSON para recibir los datos enviados en un formato predefinido. En función del requisito, conecte el formulario a un esquema JSON o a un modelo de datos de formulario:

* [Crear un esquema JSON y cargarlo en su entorno](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Crear modelo de datos de formulario](/help/forms/using/create-form-data-models.md)

### Configuración de un esquema JSON o un modelo de datos de formulario para su formulario

Para configurar un esquema JSON o un modelo de datos de formulario para su formulario:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Modelo de datos]**.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable para configurar un esquema JSON o un modelo de datos de formulario](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleccione y configure un esquema JSON o un modelo de datos de formulario según sus necesidades:

   * Al seleccionar la variable **[!UICONTROL Modelo de formulario]**, utilice la opción **[!UICONTROL Seleccionar modelo de datos de formulario]** para seleccionar un modelo de datos de formulario preconfigurado.
   * Al seleccionar la opción **[!UICONTROL Esquema]**, utilice la opción **[!UICONTROL Esquema]** para seleccionar un esquema JSON para el formulario.

1. Haga clic en **[!UICONTROL Listo]**.

>[!NOTE]
>
> Puede editar el esquema JSON o el modelo de datos de formulario para un formulario adaptable mediante las propiedades del contenedor de la guía.

## Configuración de un servicio de rellenado previo  {#configure-prefill-service-for-form}

Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Puede hacer lo siguiente:

* [Crear un servicio de rellenado previo personalizado](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Servicio de rellenado previo de modelo de datos de formulario](#fdm-prefill-service)

### Utilización del servicio de rellenado previo del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable {#fdm-prefill-service}

Puede utilizar el servicio de rellenado previo del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable mediante el uso de un modelo de datos de formulario o un servicio de rellenado previo personalizado. El servicio de rellenado previo del modelo de datos de formulario utiliza el [Obtener servicio del modelo de datos de formulario configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar datos. Para utilizar el servicio de rellenado previo del modelo de datos de formulario de un formulario adaptable, haga lo siguiente:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable para configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Seleccionar modelo de datos de formulario. Abra la pestaña **[!UICONTROL Básico]**. En el servicio de rellenado previo, seleccione **[!UICONTROL Servicio de rellenado previo del modelo de datos de formulario]**.
1. Haga clic en **[!UICONTROL Listo]**. El formulario adaptable ahora está configurado para utilizar el rellenado previo del modelo de datos de formulario. Ahora puede usar el [editor de reglas](rule-editor.md) para crear reglas para rellenar previamente los campos del formulario.

## ¿Cómo se cambia el nombre a un formulario adaptable de AEM?{#rename-an-AEM-Adaptive-Form}

Para cambiar el nombre de un formulario adaptable, realice los siguientes pasos:

1. Seleccione un formulario adaptable en la interfaz de usuario de AEM Forms.
1. Haga clic en **Propiedades** situado en el carril superior.

   ![Propiedades](/help/forms/using/assets/rename-form-properties.png)

1. Cambie el nombre del formulario en la pestaña **Título**, como se muestra en la siguiente imagen.
1. Haga clic en **Guardar y cerrar**.

   ![Cambiar el nombre de un formulario adaptable de AEM](/help/forms/using/assets/rename-form-title.png)


<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## Siguientes pasos

* [Utilice el editor de reglas para agregar un comportamiento dinámico al formulario](rule-editor.md)
* [Crear o personalizar temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Ver también

* [Crear un formulario adaptable basado en componentes principales](create-an-adaptive-form-core-components.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Plantillas temáticas y modelos de datos de formulario de ejemplo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es)
