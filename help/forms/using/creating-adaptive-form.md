---
title: Crear un formulario adaptable
description: Obtenga información sobre cómo crear un formulario adaptable mediante  [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Profundice en cómo crear un formulario adaptable basado en un modelo de datos de formulario, una plantilla de formulario XFA y un esquema XML o JSON.
role: User, Developer
level: Beginner
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 94%

---

# Crear un formulario adaptable {#creating-an-adaptive-form}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=es) |
| AEM 6.5 | Este artículo |

## Crear un formulario adaptable {#strong-create-an-adaptive-form-strong}

Siga estos pasos para crear un formulario adaptable.

1. Acceda [!DNL Experience Manager Forms]a la instancia de autor en `https://'[server]:[port]'/<custom-context-if-any>.`.

1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager.

   Cuando haya iniciado sesión, en la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

   >[!NOTE]
   >
   >Para una instalación predeterminada, el inicio de sesión es `admin` y la contraseña es `admin`.

1. Seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**.
1. Aparecerá una opción para seleccionar una plantilla. Para obtener más información sobre las plantillas, consulte [Plantillas de formularios adaptables](creating-adaptive-form.md#p-adaptive-form-templates-p). Seleccione una plantilla para seleccionarla y haga clic en Siguiente.
1. Aparecerá la opción “Agregar propiedades”. Especifique los valores para los siguientes campos de propiedad. Los campos Título y Nombre son obligatorios:

   * **[!UICONTROL Título:]** Especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se sustituyen por guiones.
   * **[!UICONTROL Descripción:]** especifica la información detallada sobre el formulario.
   * **[!UICONTROL Etiquetas:]** especifica etiquetas para identificar de forma exclusiva el formulario adaptable. Las etiquetas ayudan a buscar en el formulario. Para crear etiquetas, escriba nuevos nombres de etiqueta en el cuadro **[!UICONTROL Etiquetas]**.

1. Puede crear un formulario adaptable en base a uno de los siguientes modelos de formulario:

   * [Modelo de datos de formulario](#fdm)
   * [Plantilla de formulario XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Esquema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Ninguno o sin modelo de formulario

   Puede configurarlos desde la pestaña **[!UICONTROL Modelo de formulario]** en la página **[!UICONTROL Agregar propiedades]**. De forma predeterminada, el modelo de formulario seleccionado es **[!UICONTROL Ninguno]**.

1. Seleccione **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo.

   Una vez que haya terminado de especificar todas las propiedades, haga clic en **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo.

1. Seleccione **[!UICONTROL Abrir]** para abrir el formulario recién creado en una pestaña nueva. El formulario se abrirá para editarlo y mostrará el contenido disponible en la plantilla. También mostrará la barra lateral para personalizar el formulario recién creado según las necesidades.

   En base al tipo de formulario adaptable, los elementos del formulario presentes en la plantilla del formulario XFA, el esquema XML o JSON asociados se muestran en la pestaña **[!UICONTROL Objetos del modelo de datos]** del **[!UICONTROL Explorador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

   Para obtener información sobre la interfaz de creación de formularios adaptables y los componentes disponibles, consulte [Introducción a la creación de formularios adaptables](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Permita que las ventanas emergentes del explorador abran el formulario recién creado en una pestaña nueva.

## Crear un formulario adaptable basado en un modelo de datos de formulario {#fdm}

La integración de datos de [[!DNL Experience Manager Forms] ](data-integration.md) permite integrar varias fuentes de datos y unir sus entidades y servicios para crear un modelo de datos de formulario. Es una extensión del esquema JSON. Puede utilizar un modelo de datos de formulario para crear un formulario adaptable. Las entidades u objetos del modelo de datos configurados en un modelo de datos de formulario están disponibles como objetos del modelo de datos para la creación de formularios. Están enlazados a los respectivas fuentes de datos y se utilizan para rellenar previamente un formulario y escribir los datos enviados en las fuentes de datos respectivas. También puede llamar a servicios configurados en un modelo de datos de formulario mediante reglas de formularios adaptables.

Para utilizar un modelo de datos de formulario para crear un formulario adaptable haga lo siguiente:

1. En la pestaña Modelo de formulario de la pantalla Agregar propiedades, seleccione **[!UICONTROL Modelo de datos de formulario]** en la lista desplegable **[!UICONTROL Seleccionar desde]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Seleccione para expandir **[!UICONTROL Seleccionar modelo de datos de formulario]**. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de formulario.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>También puede cambiar el modelo de datos de formulario para un formulario adaptable. Para ver los pasos detallados, consulte [Editar las propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Crear un formulario adaptable basado en una plantilla de formulario XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Puede cambiar el propósito de plantillas de formulario XFA para crear formularios adaptables. Para cambiar el propósito, cargue y asocie una plantilla de formulario XFA con un formulario adaptable. Los elementos de la plantilla de formulario (formulario XFA) están disponibles para utilizarlas en el buscador de contenido en el momento de creación de los formularios adaptables. Desde el buscador de contenido, puede arrastrar y soltar los elementos de la plantilla de formulario en el formulario.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## Crear un formulario adaptable basado en un esquema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Los esquemas XML y JSON representan la estructura en la que el sistema back-end de su organización produce o consume los datos. Puede asociar el esquema a un formulario adaptable y utilizar sus elementos para agregarle contenido dinámico. Los elementos del esquema están disponibles en la pestaña Objeto del modelo de datos del explorador de contenidos para crear formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.

Consulte los siguientes documentos para saber cómo diseñar esquemas XML o JSON para crear formularios adaptables.

* [Crear formularios adaptables mediante un esquema XML](adaptive-form-xml-schema-form-model.md)
* [Crear formularios adaptables mediante un esquema JSON](adaptive-form-json-schema-form-model.md)

Haga lo siguiente para utilizar el esquema XML o JSON como modelo de formulario para un formulario adaptable:

1. En el paso **[!UICONTROL Agregar propiedades]** de la página de creación de formularios adaptables, seleccione en la pestaña **[!UICONTROL Modelo de formulario]**.
1. En la pestaña Modelo de formulario, seleccione **[!UICONTROL Esquema]** del campo desplegable **[!UICONTROL Seleccionar desde]**.

1. Seleccione **[!UICONTROL Seleccionar esquema]** y realice una de las siguientes acciones:

   * **[!UICONTROL Cargar desde disco]**: seleccione esta opción y seleccione Cargar definición de esquema para examinar y cargar un esquema XML o JSON desde su sistema de archivos. El archivo de esquema cargado reside con el formulario y no es accesible para otros formularios adaptables.
   * **[!UICONTROL Buscar en el repositorio]**: seleccione esta opción para seleccionar archivos disponibles en el repositorio de la lista de archivos de definición. Seleccione el archivo de esquema XML o JSON como modelo de formulario. El esquema seleccionado está asociado al formulario por referencia y es accesible para utilizarlo en otros formularios adaptables.

   >[!CAUTION]
   >
   >Asegúrese de que el nombre de archivo del esquema JSON termina con **.schema.json**. Por ejemplo: mySchema.schema.json

   ![Seleccionar el esquema XML o JSON](assets/upload-schema.png)
   **Figura:** *Seleccionar el esquema XML o JSON*

1. (Solo para esquema XML) Después de seleccionar o cargar un esquema XML, especifique un elemento raíz del archivo XSD seleccionado para asignarlo al formulario adaptable.

   ![Seleccionar el elemento raíz XSD](assets/xsd-root-element.png)
   **Figura:** *seleccionar el elemento raíz XSD*

>[!NOTE]
>
>También puede cambiar el esquema de un formulario adaptable. Para ver los pasos detallados, consulte [Editar las propiedades del modelo de formulario de un formulario adaptable](#edit-form-model).

## Plantillas de formularios adaptables {#adaptive-form-templates}

Una plantilla de formulario adaptable proporciona una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Además, puede utilizar el editor de plantillas para crear sus propias plantillas. Para obtener más información sobre cómo trabajar con plantillas, consulte [Plantillas de formularios adaptables](template-editor.md).

>[!NOTE]
>
>Cuando se abre un formulario adaptable creado con la plantilla avanzada para su edición, aparece un mensaje de error. La plantilla avanzada tiene un componente Paso de firma y Adobe Sign está habilitado para él de forma predeterminada. Cree y seleccione una [Configuración de nube de Adobe Sign](adobe-sign-integration-adaptive-forms.md) y [configure un firmante](working-with-adobe-sign.md#addsignerstoanadaptiveform) para resolver el error.

## Editar propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

Los formularios adaptables se crean sin un modelo de formulario (con la opción Ninguno del modelo de formulario) o mediante un modelo de formulario como una plantilla de formulario, un esquema XML o JSON o un modelo de datos de formulario. Puede cambiar el modelo de formulario para un formulario adaptable de Ninguno a otro modelo de formulario. Si el formulario adaptable se basa en un modelo de formulario, puede elegir otro esquema de formulario, esquema XML o JSON o modelo de datos de formulario para el mismo modelo de formulario. Pero no puede cambiar de un modelo de formulario a otro.

1. Seleccione el formulario adaptable y seleccione el icono **Propiedades**.
1. Abra la pestaña **[!UICONTROL Modelo de formulario]** y haga una de las siguientes acciones.

   * Si el formulario adaptable no cuenta con un modelo de formulario, puede elegir otro modelo de formulario y, en consecuencia, seleccionar una plantilla de formulario, un esquema XML o JSON o el modelo de datos de formulario.
   * Si el formulario adaptable se basa en un modelo de formulario, puede elegir otra plantilla de formulario, esquema XML o JSON o modelo de datos de formulario para el mismo modelo de formulario.

1. Seleccione **[!UICONTROL Guardar]** para guardar las propiedades.

## Guardar automáticamente un formulario adaptable {#auto-save-an-adaptive-form}

De forma predeterminada, el contenido de un formulario adaptable se guarda con una acción del usuario, como al pulsar el botón guardar. También puede configurar un formulario adaptable para que empiece a guardar automáticamente el contenido en función de un evento o intervalo de tiempo. La opción de guardado automático es útil para lo siguiente:

* Guardar automáticamente el contenido para usuarios anónimos y con sesión iniciada
* Guardar el contenido de un formulario sin la intervención mínima del usuario
* Empezar a guardar contenido de un formulario basado en un evento de usuario
* Guardar el contenido de un formulario repetidamente después de un intervalo de tiempo especificado

### Habilitar el guardado automático para un formulario adaptable {#enable-auto-save-for-an-adaptive-form}

De forma predeterminada, la opción de guardado automático no está activada. Puede habilitar la opción de guardado automático desde la pestaña Guardado automático de un formulario adaptable. La pestaña Guardar automáticamente también proporciona otras opciones de configuración. Realice los siguientes pasos para habilitar y configurar la opción de guardado automático para un formulario adaptable:

1. Para acceder a la sección de guardado automático de las propiedades, seleccione un componente, luego seleccione ![nivel de campo](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, seleccione ![cmppr](assets/cmppr.png).
1. En la sección **[!UICONTROL Guardar automáticamente]**, **[!UICONTROL habilite]** la opción Guardar automáticamente.
1. En el cuadro **[!UICONTROL Evento de formulario adaptable]** especifique 1 o TRUE para comenzar a guardar automáticamente el formulario cuando se cargue en el explorador. También se puede especificar una expresión condicional para un evento, que cuando se activa y devuelve el valor “True”, comienza a guardar el contenido del formulario.
1. Especifique el Activador. El guardado automático se activará según la configuración. Las opciones son las siguientes:

   * **[!UICONTROL En base a tiempo:]** seleccione esta opción para comenzar a guardar el contenido en función de un intervalo de tiempo específico.
   * **[!UICONTROL En base a eventos:]** seleccione esta opción para comenzar a guardar el contenido en función de cuándo se activa un evento.

   Cuando selecciona un activador, se activará el cuadro Configuración de estrategia. El cuadro Configuración de estrategia le permite:

   * Especificar un intervalo de tiempo si selecciona el activador **[!UICONTROL En base a tiempo]**.
   * Especificar un nombre de evento si selecciona el activador **[!UICONTROL En base a eventos]**.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo guardado automático en base a tiempo) Realice los siguientes pasos para configurar las opciones de guardado automático en base a tiempo.

   1. En el cuadro **[!UICONTROL Guardar automáticamente en este intervalo]** especifique el intervalo de tiempo en segundos. El formulario se guarda repetidamente después de que transcurra el número de segundos especificado en el cuadro de intervalo.

1. (Solo guardado automático basado en eventos) Realice los siguientes pasos para configurar las opciones de guardado automático en base a eventos.

   1. En el cuadro **[!UICONTROL Guardar automáticamente después de este evento]**, especifique un evento [GuideBridge](https://helpx.adobe.com/es/aem-forms/6/javascript-api/GuideBridge.html). El formulario se guardará cada vez que la expresión se evalúe como TRUE.

1. (Opcional) Para guardar automáticamente el contenido para usuarios anónimos, seleccione la opción **[!UICONTROL Habilitar el guardado automático para usuarios anónimos]** y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Para que la opción de guardado automático funcione para usuarios anónimos, asegúrese de configurar el servicio de configuración común de Forms para permitir que todos los usuarios puedan obtener una vista previa, comprobar y firmar formularios.
   >
   >Para configurar el servicio, vaya a la configuración de la consola web de Adobe Experience Manager en `https://'[server]:[port]'system/console/configMgr` y edite el **[!UICONTROL Servicio de configuración común de Forms]** para elegir la opción **[!UICONTROL Todos los usuarios]** en el campo **[!UICONTROL Permitir]** y guarde la configuración.


## ¿Cómo se cambia el nombre a un formulario adaptable de AEM? {#rename-an-AEM-Adaptive-Form}

Para cambiar el nombre de un formulario adaptable, realice los siguientes pasos:

1. Seleccione un formulario adaptable en la interfaz de usuario de AEM Forms.
1. Haga clic en **Propiedades** situado en el carril superior.

   ![Propiedades](/help/forms/using/assets/rename-form-properties.png)

1. Cambie el nombre del formulario en la pestaña **Título**, como se muestra en la siguiente imagen.
1. Haga clic en **Guardar y cerrar**.

   ![Cambiar el nombre de un formulario adaptable de AEM](/help/forms/using/assets/rename-form-title.png)
