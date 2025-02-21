---
title: Usar Adobe Sign en un formulario adaptable
description: Habilite los flujos de trabajo de firma electrónica (Adobe Sign) para un formulario adaptable con el fin de automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente los formularios desde dispositivos móviles.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components,Acrobat Sign
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3875'
ht-degree: 93%

---

# Usar [!DNL Adobe Sign] en un formulario adaptable{#using-adobe-sign-in-an-adaptive-form}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=es) |
| AEM 6.5 | Este artículo |


[!DNL Adobe Sign] habilita los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de administración de recursos humanos y más.

Cuando se trabaja con [!DNL Adobe Sign] y los formularios adaptables, normalmente los usuarios rellenan un formulario adaptable para solicitar un servicio. Por ejemplo, una solicitud de hipoteca y tarjeta de crédito requiere firmas legales de todos los prestatarios y cosolicitantes. Para habilitar los flujos de trabajo de firma electrónica para situaciones similares, se puede integrar [!DNL Adobe Sign] con AEM[!DNL Forms]. Algunos ejemplos más. Puede usar [!DNL Adobe Sign] para lo siguiente:

* Cerrar acuerdos desde cualquier dispositivo con procesos de propuesta, presupuesto y contrato totalmente automatizados.
* Finalizar los procesos de Recursos Humanos más rápido y ofrecer a sus empleados las experiencias digitales.
* Reducir los tiempos de ciclo de contrato e incorporar a sus proveedores más rápido.
* Crear flujos de trabajo digitales que automaticen procesos comunes.

La integración de [!DNL Adobe Sign] con AEM [!DNL Forms] es compatible con los siguientes elementos:

* Flujos de trabajo de firma de usuarios únicos y múltiples
* Flujos de trabajo de firma secuenciales y simultáneos
* Experiencias de firma dentro y fuera de formulario
* Firma de formularios como usuario anónimo o con sesión iniciada
* Procesos de firma dinámica (integración con flujo de trabajo de AEM [!DNL Forms])
* Autenticación mediante una base de conocimiento, un teléfono y perfiles sociales

Conozca las [prácticas recomendadas para utilizar Adobe Sign con formularios adaptables](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) para crear mejores experiencias de firma.

## Requisitos previos {#prerequisites}

Antes de usar [!DNL Adobe Sign] en un formulario adaptable:

* Asegurarse de que AEM [!DNL Forms] Cloud Service está configurado para usar [!DNL Adobe Sign]. Para obtener más información, consulte [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Tenga la lista de firmantes preparada. Se requiere al menos una dirección de correo electrónico para cada firmante.

## Configurar [!DNL Adobe Sign] para un formulario adaptable {#configure-adobe-sign-for-an-adaptive-form}

Siga estos pasos para configurar [!DNL Adobe Sign] para un formulario adaptable:

1. [Editar las propiedades de formulario adaptables para Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Agregar campos de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Seleccionar Adobe Sign Cloud Service para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Agregar firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Seleccionar la acción de envío para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Datos del firmante](assets/signer_details_new.png)

### Editar propiedades de formulario adaptables para [!DNL Adobe Sign] {#enableadobesign}

Configurar propiedades de formulario adaptables para [!DNL Adobe Sign] para un formulario adaptable existente o nuevo.

[Crear un formulario adaptable para Adobe Sign](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) describe los pasos para crear un formulario adaptable básico. Consulte [Crear un formulario adaptable](../../forms/using/creating-adaptive-form.md) para conocer otras opciones disponibles al crear un formulario adaptable.

#### Crear un formulario adaptable para [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Siga estos pasos para crear un formulario adaptable con firma habilitada:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparece una lista de plantillas. Seleccione la plantilla y seleccione **[!UICONTROL Siguiente]**.
1. En la pestaña **[!UICONTROL Básico]**:

   1. Especifique el **[!UICONTROL Nombre]** y el **[!UICONTROL Título]** para el formulario adaptable.

   1. Seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar [!DNL Adobe Sign] con AEM [!DNL Forms].

      >[!NOTE]
      >
      >La lista desplegable **[!UICONTROL Adobe Sign Cloud Service]** muestra los servicios en la nube que están configurados en el contenedor de configuración que seleccione en este campo. La lista desplegable **[!UICONTROL Adobe Sign Cloud Service]** está disponible en la sección **[!UICONTROL Firma electrónica]** de las propiedades del formulario adaptable al seleccionar la opción **[!UICONTROL Habilitar Adobe Sign]**.

1. En la pestaña **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla Documento de registro]** y seleccione una plantilla de documento de registro. Si utiliza un formulario adaptable basado en una plantilla de formulario, los documentos enviados para firmar solo mostrarán aquellos campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generar documento de registro]**. Si utiliza la opción Documento de registro habilitada para el formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Seleccione **[!UICONTROL Crear.]** Se crea un formulario adaptable con firma, que se puede utilizar para agregar [!DNL Adobe Sign] campos.

#### Editar un formulario adaptable para [!DNL Adobe Sign] {#editafsign}

Siga estos pasos para usar [!DNL Adobe Sign] en un formulario adaptable existente:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario adaptable y seleccione **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Básico]**, seleccione el [contenedor de configuración](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al configurar [!DNL Adobe Sign] con AEM [!DNL Forms].
1. En la pestaña **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   * Seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla Documento de registro]** y seleccione una plantilla de documento de registro. Si utiliza un formulario adaptable basado en una plantilla de formulario, los documentos enviados para firmar solo mostrarán aquellos campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   * Seleccione la opción **[!UICONTROL Generar documento de registro]**. Si utiliza la opción Documento de registro habilitada para el formulario adaptable, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Seleccione **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL Adobe Sign].

### Agregar campos de Adobe Sign a un formulario adaptable {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] tiene varios campos que se pueden colocar en un formulario adaptable. Estos campos aceptan varios tipos de datos, como firmas, iniciales, empresa o título, y ayudan a recopilar información adicional durante la firma, junto con las firmas. Puede usar el componente del bloque [!DNL Adobe Sign] para colocar campos de [!DNL Adobe Sign] en varias ubicaciones en un formulario adaptable.

Realice los siguientes pasos para agregar campos a un formulario adaptable y personalizar varias opciones relacionadas con estos campos:

1. Arrastre y suelte el componente **[!UICONTROL del bloque de Adobe Sign]** del explorador del componente en el formulario adaptable. El componente del bloque [!DNL Adobe Sign] cuenta con los campos [!DNL Adobe Sign] compatibles. De forma predeterminada, agrega un campo de **Firma** al formulario adaptable.

   ![Bloque de firma](assets/sign_block_new.png)

   De forma predeterminada, el bloque [!DNL Adobe Sign] no es visible en el formulario adaptable publicado. Solo se ve en los documentos de firma. Puede cambiar la visibilidad del bloque [!DNL Adobe Sign] en las propiedades del componente del bloque [!DNL Adobe Sign].

   >[!NOTE]
   >
   >    * El uso del bloque [!DNL Adobe Sign] no es obligatorio para utilizar [!DNL Adobe Sign] en un formulario adaptable. Si no usa el bloque de [!DNL Adobe Sign] y agrega campos para los firmantes, el campo de firma predeterminado se muestra al final de los documentos de firma.
   >    * Use el bloque de [!DNL Adobe Sign] solo para los formularios adaptables que generan automáticamente el documento de registro. Si utiliza un XDP personalizado para generar un documento de registro o un formulario basado en un formulario adaptable, el bloque [!DNL Adobe Sign] no es compatible.
   >
   >

1. Seleccione el componente **[!UICONTROL Adobe Sign Block]** y seleccione el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra las opciones para agregar campos y formatear la apariencia de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleccione y agregue campos de [!DNL Adobe Sign]. **B.** Amplíe el bloque [!DNL Adobe Sign] a vista de pantalla completa.

1. Seleccione el icono **[!UICONTROL Adobe Sign] Field** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos de [!DNL Adobe Sign].

   Amplíe el campo desplegable **[!UICONTROL Tipo]** para seleccionar un campo de [!DNL Adobe Sign] y seleccione el icono de ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) Listo para agregar el campo seleccionado al bloque de [!DNL Adobe Sign]. El campo desplegable **[!UICONTROL Tipo]** incluye los tipos de campo Firma, Información de firmante y Datos. La integración de [!DNL Adobe Sign] con AEM [!DNL Forms] admite campos enumerados solo en el cuadro desplegable [!UICONTROL Tipo]. Para obtener información detallada sobre los campos de [!DNL Adobe Sign], consulte [Documentación de Adobe Sign](https://helpx.adobe.com/es/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Es obligatorio proporcionar un nombre único para un campo. También puede seleccionar la opción necesaria para marcar un campo como obligatorio. Además de las opciones **[!UICONTROL Nombre]** y **[!UICONTROL Requerido]**, otros campos de [!DNL Adobe Sign] cuentan con más donde elegir. Por ejemplo, máscara y líneas múltiples. Además, especifique un nombre único para cada campo de [!DNL Adobe Sign] si los campos residen en el mismo o en diferentes bloques de [!DNL Adobe Sign].

   Si selecciona **[!UICONTROL Firma digital]** en la lista desplegable, puede aplicar firmas digitales al formulario adaptable:

   * En línea, se usan firmas de la nube para firmar con un [ID digital](https://helpx.adobe.com/es/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicios de confianza.
   * De forma local, se descarga el documento con Adobe Acrobat o Reader usando una tarjeta inteligente, un token USB o un ID digital basado en archivos.

### Habilitar [!DNL Adobe Sign] para un formulario adaptable {#enableadobsignforanadaptiveform}

De serie, [!DNL Adobe Sign] no está habilitado para un formulario adaptable. Siga estos pasos para habilitarlo:

1. En el navegador de contenido, seleccione **[!UICONTROL Contenedor de formulario]** y seleccione el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, amplíe el acordeón **[!UICONTROL Firma electrónica]** y seleccione la opción **[!UICONTROL Habilitar Adobe Sign]**. Se habilita [!DNL Adobe Sign] para un formulario adaptable.

### Seleccione [!DNL Adobe Sign] Cloud Service y la petición de firma {#selectadobesigncloudserviceforanadaptiveform}

Puede configurar varios servicios de [!DNL Adobe Sign] para una instancia de AEM [!DNL Forms]. Es aconsejable tener un conjunto de servicios separados para cada función (Recursos Humanos, Finanzas, etc.). Facilita el seguimiento y la creación de informes de documentos firmados. Por ejemplo, un banco tiene varios departamentos. Puede tener una configuración separada para cada departamento para realizar un mejor seguimiento de los documentos.

Un documento también puede tener varios firmantes. Por ejemplo, una solicitud de tarjeta de crédito puede tener varios solicitantes. Un banco requiere firmas de todos los solicitantes antes de iniciar la solicitud de procesamiento. En los casos de varios firmantes, puede seleccionar firmar el documento en orden secuencial o simultáneo.

Siga estos pasos para seleccionar un servicio en la nube y el orden de firma:

![cloud-service](assets/cloud-service.png)

1. En el navegador de contenido, seleccione **[!UICONTROL Contenedor de formulario]** y seleccione el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, amplíe el acordeón **[!UICONTROL Firma electrónica]** y seleccione la opción **[!UICONTROL Habilitar Adobe Sign]**. Se habilita [!DNL Adobe Sign] para un formulario adaptable.
1. Seleccione un servicio de Cloud Service de la lista ya configurada de [!DNL Adobe Sign] Cloud Services.

   Si la lista **[!UICONTROL Adobe Sign Cloud Service]** está vacía, consulte el artículo [Configurar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) para configurar el servicio.

   La lista desplegable enumera los servicios de Cloud Service que existen en la carpeta `global` en Herramientas > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Además, la lista desplegable también enumera los servicios de Cloud Service que existen en la carpeta que selecciona en el campo **[!UICONTROL Contenedor de configuración]** al crear un formulario adaptable.

1. Seleccione el orden de firma del cuadro de diálogo **[!UICONTROL Los firmantes pueden firmar]**. [!DNL Adobe Sign] Los firmantes pueden firmar un formulario adaptable **[!UICONTROL secuencialmente]** (un firmante tras otro) o **[!UICONTROL simultáneamente]** (en cualquier orden).

   En orden secuencial, un firmante recibe el formulario para firmar a la vez. Una vez que un firmante completa la firma del documento, el formulario se envía al siguiente firmante, y así sucesivamente.

   En orden simultáneo, varios firmantes pueden firmar un formulario a la vez.

1. [Agregue firmantes a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) y seleccione el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios.


### Agregar firmantes a un formulario adaptable {#addsignerstoanadaptiveform}

Solo se puede tener un firmante o varios firmantes para un formulario adaptable. Al agregar un firmante, también puede configurar los detalles de autenticación del firmante. También puede seleccionar si el usuario que rellena el formulario y el firmante son la misma persona. Realice los siguientes pasos para agregar y proporcionar varios detalles sobre un firmante:

1. En el explorador de contenido, seleccione **[!UICONTROL Contenedor de formulario]** y seleccione el icono **[!UICONTROL Configurar]** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades con las propiedades del contenedor de formularios adaptables.
1. En el navegador de propiedades, amplíe el acordeón **[!UICONTROL Firma electrónica]** y seleccione la opción **[!UICONTROL Habilitar Adobe Sign]**. Se habilita [!DNL Adobe Sign] para un formulario adaptable.
1. Seleccione **[!UICONTROL Agregar firmante]** en **[!UICONTROL Configuración del firmante]**. Agrega un firmante al formulario adaptable. Puede agregar varios firmantes [!DNL Adobe Sign] a un formulario adaptable.
   ![phone-details](assets/phone-details.png)

1. Haga clic en el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png) para especificar la siguiente información sobre el firmante:

   * **[!UICONTROL Título]:** Especifique un título para identificar un firmante de forma única.

   * **[!UICONTROL ¿El firmante y quien rellena el formulario son la misma persona?]:** Seleccione **Sí**, si la persona que rellena el formulario y el primer firmante son la misma persona. Si la opción se establece en **No,** a continuación, no utilice el componente paso de firma en el formulario adaptable. Si el formulario contiene un componente Paso de firma, el campo se establece automáticamente como Sí.

   * **[!UICONTROL Dirección de correo electrónico del firmante]:** Especifique la dirección de correo electrónico del firmante. El firmante recibe los documentos/formularios a firmar en la dirección de correo electrónico especificada. Puede elegir utilizar una dirección de correo electrónico proporcionada en un campo de formulario, en el perfil de AEM del usuario que ha iniciado sesión o escribir manualmente una dirección de correo electrónico. Es un paso obligatorio. Asegúrese de que la dirección de correo electrónico del primer firmante o del único firmante (si hay solo uno) no sea idéntica al de la cuenta de [!DNL Adobe Sign] utilizada para configurar AEM Cloud Services.

   * **[!UICONTROL Método de autenticación del firmante]:** Especifique el método para autenticar a un usuario antes de abrir un formulario para su firma. Puede elegir entre teléfono, base de conocimiento y autenticación social basada en identidad. Para Adobe Acrobat Sign Solutions para Administración Pública, solo están disponibles las opciones de autenticación por teléfono y basada en conocimientos.

   >[!NOTE]
   >
   >    * De forma predeterminada, la autenticación basada en la identidad social proporciona una opción para autenticarse con Facebook, Google y LinkedIn. Puede ponerse en contacto con la ayuda técnica de [!DNL Adobe Sign] para habilitar otros proveedores de autenticación social.
   >
   >

   * Campos de **[!DNL Adobe Sign]para rellenar o firmar:** seleccione campos de [!DNL Adobe Sign] para el firmante. Un formulario adaptable puede tener varios campos de [!DNL Adobe Sign]. Puede elegir habilitar campos específicos para un firmante. El campo muestra todos los bloques del bloque [!DNL Adobe Sign] disponibles. Al seleccionar un bloque, se seleccionan todos los campos del bloque. Puede utilizar el icono X para anular la selección de un campo.

   ![signer-details](assets/signer-details.png)

   La imagen anterior tiene dos ejemplos del bloque [!DNL Adobe Sign]: Información personal y detalles de Office

   Seleccione el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Se agrega y configura el firmante.

### Seleccionar la acción de envío para un formulario adaptable {#selectsubmitactionforanadaptiveform}

Después de agregar campos de [!DNL Adobe Sign] a un formulario adaptable, habilite [!DNL Adobe Sign] en el contenedor de formularios, seleccione [!DNL Adobe Sign] Cloud Service y agregue [!DNL Adobe Sign] firmantes. Finalmente, seleccione una acción de envío adecuada para el formulario adaptable. Para obtener información detallada sobre las acciones de envío de los formularios adaptable, consulte [Configurar la acción de envío](../../forms/using/configuring-submit-actions.md).

Además, el formulario adaptable habilitado [!DNL Adobe Sign] solo se envía después de que todos los firmantes firmen el formulario. Puede encontrar formularios parcialmente firmados en la sección Firma pendiente del Portal de Forms. [!DNL Adobe Sign] El servicio de configuración sigue encuestando el servidor [!DNL Adobe Sign] a [intervalos regulares](../../forms/using/adobe-sign-integration-adaptive-forms.md) para verificar el estado de las firmas. Si todos los firmantes completan la firma del formulario, se inicia el servicio de acción de envío y se envía el formulario. Si utiliza una acción de envío personalizada y el formulario utiliza [!DNL Adobe Sign], actualice la acción de envío personalizada para utilizar el servicio de acción de envío.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. Use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

La experiencia de firma de formularios está lista. Puede obtener una vista previa del formulario para comprobar la experiencia de firma. En el formulario publicado, los campos del bloque [!DNL Adobe Sign] se muestran cuando un firmante recibe el formulario para firmar a través de un correo electrónico. Esta experiencia también se conoce como experiencia de firma fuera de formulario. También puede configurar una experiencia de firma en el formulario para el primer firmante; para ver los pasos detallados, consulte [Crear una experiencia de firma en formularios](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configurar firmas en la nube para un formulario adaptable {#configure-cloud-signatures-for-an-adaptive-form}

Las firmas digitales o firmas remotas basadas en la nube son una nueva generación de firmas digitales que funcionan en equipos de escritorio, dispositivos móviles y la web, y cumplen los niveles más altos de conformidad y seguridad para la autenticación de firmantes. Puede firmar un formulario adaptable con firmas digitales basadas en la nube.

Después de [editar las propiedades del formulario adaptable para Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobesign), siga estos pasos para agregar el campo de firma en la nube a un formulario adaptable:

1. Arrastre y suelte el componente **[!UICONTROL del bloque de Adobe Sign]** del explorador del componente en el formulario adaptable. El componente [!UICONTROL Adobe Sign Block] cuenta con los campos de [!DNL Adobe Sign] compatibles. De forma predeterminada, agrega un campo de **[!UICONTROL Firma]** al formulario adaptable.

   ![Bloque de firma](assets/sign-block-new.png)

1. Seleccione el componente **[!UICONTROL Adobe Sign Block]** y seleccione el icono **Editar** ![aem_6_3_edit](assets/aem_6_3_edit.png). Muestra las opciones para agregar campos y formatear la apariencia de un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleccione y agregue campos de [!DNL Adobe Sign]. **B.** Amplíe el bloque [!DNL Adobe Sign] a vista de pantalla completa.

1. Seleccione el icono **[!UICONTROL Campo de Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png). Muestra las opciones para seleccionar y agregar campos de [!DNL Adobe Sign].

   Amplíe el campo desplegable **[!UICONTROL Tipo]** para seleccionar **[!UICONTROL Firma digital]** y seleccione el icono **Listo** para agregar el campo seleccionado al bloque de [!DNL Adobe Sign].

   ![Firmas digitales](assets/digital_signatures_new.png)

   Es obligatorio proporcionar un nombre único para un campo.

   Aplicar firmas digitales al formulario adaptable mediante:

   * Firmas en la nube: firme con un [ID digital](https://helpx.adobe.com/es/sign/kb/digital-certificate-providers.html) alojado por un proveedor de servicios de confianza. La opción Firma en la nube no está disponible para Adobe Acrobat Sign Solutions para Administración Pública.

   * Adobe Acrobat o Reader: descargue y abra el documento con Adobe Acrobat o Reader para firmarlo con una tarjeta inteligente, un token USB o un ID digital basado en archivos.

   Después de agregar el campo de firma de nube al formulario adaptable, realice los siguientes pasos para completar el proceso de configuración:

   * [Habilitar Adobe Sign para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Seleccionar Adobe Sign Cloud Service para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Agregar firmantes de Adobe Sign a un formulario adaptable](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Seleccionar la acción de envío para un formulario adaptable](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

## Crear una experiencia de firma en formularios {#create-in-form-signing-experience}

Un usuario también puede firmar un formulario adaptable mientras lo rellena. Esta experiencia también se conoce como experiencia de firma en formularios. La experiencia de firma en formularios solo está disponible para el primer firmante en un entorno de varios firmantes. Siga estos pasos para crear una experiencia de firma en formularios para un formulario adaptable:

1. [Agregar y configurar el componente Paso de firma](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [Agregar el componente Paso de resumen](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Experiencia de firma en formulario](assets/in_form_signing_experience_new.png)

### Agregar y configurar el componente Paso de firma {#add-and-configure-the-signature-step-component}

Utilice el componente Paso de firma para proporcionar un área donde firmar electrónicamente el formulario rellenado. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión PDF identificable del formulario rellenado. El componente Paso de firma ocupa el ancho completo disponible en el formulario. Se recomienda no colocar ningún otro componente en la sección que contiene el componente Paso de firma.

Realice los siguientes pasos para configurar el componente Paso de firma:

1. Arrastre y suelte el componente **[!UICONTROL Paso de firma]** del explorador de componentes al formulario.
1. Seleccione el componente del paso Firma recién agregado y seleccione el icono **Configurar** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del Paso de firma. Configure las siguientes propiedades:

   * **[!UICONTROL Nombre]**: Especifique el nombre del componente.

   * **[!UICONTROL Título]:** Especifique un título único para el componente.
   * **[!UICONTROL Mensaje de plantilla]:** Especifique el mensaje que se mostrará mientras se carga el PDF de firma. Los servicios de [!DNL Adobe Sign] tardan algún tiempo en preparar y cargar el PDF de firma.
   * **[!UICONTROL Servicio de firma]:** Seleccione la opción **[!DNL Adobe Sign]**.

   * **[!UICONTROL Usar el componente de firma electrónica heredado]**: Si utiliza el formulario adaptable correspondiente en [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), la aplicación de AEM [!DNL Forms] o el formulario adaptable subyacente tiene un componente de firma electrónica heredado, seleccione la opción **Usar el componente de firma electrónica heredado**.

   * **[!UICONTROL Configuración]**: Seleccione una configuración ([!DNL Adobe Sign] Cloud Service). El cuadro desplegable solo está disponible si la opción **Usar el componente de firma electrónica heredado** está activada.

   * **[!UICONTROL Clase CSS]**: Especifique la clase CSS para el componente.

   Seleccione el icono Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios.

   ![Paso de firma](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* Cuando arrastra y suelta el componente **[!UICONTROL Paso de firma]** al formulario, **[!UICONTROL ¿el firmante y quien rellena el formulario son la misma persona?La opción]** se configura automáticamente como **Sí**. Es necesario mantener el formulario en funcionamiento.
   >* Utilice el componente Paso de resumen después del componente Paso de firma para obtener la mejor experiencia. El paso Resumen envía el formulario de forma automática e inmediata después de completar la firma de un formulario en el componente Paso de firma. Si no utiliza el paso de resumen, se activa un envío automático solo después del intervalo establecido mediante el [Servicio de configuración de Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   >
   >Algunas prácticas recomendadas son:
   >
   >* El panel de formulario adaptable que contiene el paso de firma siempre se encuentra en el último o el segundo último panel de un formulario adaptable. Puede ser el segundo último panel solo cuando el último panel contiene el paso Resumen.
   >* El panel que contiene el componente de paso de firma o resumen no puede contener ningún otro componente.
   >* Los formularios adaptables que contienen el paso de firma no pueden tener botón de envío.
   >* El envío de los formularios adaptables que contienen el Paso de firma se administra mediante un servicio en segundo plano o el paso Resumen. Si hay un firmante configurado que también esté rellenando el formulario, la ventaja de administrar el envío del formulario adaptable mediante el paso Resumen es que evalúa inmediatamente que el firmante ha firmado el formulario e invoca la acción de envío. Un servicio en segundo plano tarda más en evaluar si todos los firmantes configurados han firmado el formulario y retrasa la presentación del formulario adaptable.
   >* Diseñe el formulario para que el usuario no pueda volver atrás desde un panel que contenga el paso de Firma o Resumen.


### Configurar la página de agradecimiento o el componente de paso de resumen {#configure-the-thank-you-page-or-summary-step-component}

El componente **Paso de resumen** envía automáticamente el formulario, rellena la información dentro de la página Resumen personalizada y muestra el resumen del formulario enviado. También obtiene la información necesaria en el mapa de retorno. El componente Paso de resumen ocupa el ancho completo disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de resumen.

Ahora, la experiencia de firma de formularios en está lista. Puede obtener una vista previa del formulario para comprobar la experiencia de firma.

## Preguntas frecuentes {#frequently-asked-questions}

**P:** Puede incrustar un formulario adaptable en otro formulario adaptable. ¿Se puede habilitar [!DNL Adobe Sign] para el formulario adaptable incrustado?
**R:** No, AEM [!DNL Forms] no es compatible con el uso de un formulario adaptable que incrusta un formulario adaptable con [!DNL Adobe Sign] habilitado para firmar.

**P:** Cuando creo un formulario adaptable utilizando la plantilla avanzada y lo abro para editarlo, aparece un mensaje de error “La firma electrónica o los firmantes no están correctamente configurados” . ¿Cómo se resuelve el mensaje de error?
**R:** El formulario adaptable creado con la plantilla avanzada está configurado para usar [!DNL Adobe Sign]. Para resolver el error, cree y seleccione una configuración de nube de [!DNL Adobe Sign] y configure un firmante de [!DNL Adobe Sign] para el formulario adaptable.

**P:** ¿Puedo usar etiquetas de texto de [!DNL Adobe Sign] en un componente de texto estático de un formulario adaptable?
**R:** Sí, puede utilizar etiquetas de texto en un componente de texto para agregar campos de [!DNL Adobe Sign] a un [documento de registro](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (solo para la opción Documento de registro generado automáticamente) habilitado como formulario adaptable. Para obtener más información sobre el procedimiento y las reglas para crear una etiqueta de texto, consulte [Documentación de Adobe Sign](https://helpx.adobe.com/es/sign/using/text-tag.html). Tenga en cuenta también que los formularios adaptables tienen una compatibilidad limitada con las etiquetas de texto. Puede utilizar las etiquetas de texto para crear solo los campos compatibles con [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**P:** AEM [!DNL Forms] proporciona ambos [!UICONTROL bloque de Adobe Sign] y componentes del Paso de firma. ¿Se pueden utilizar simultáneamente en un formulario adaptable?
**R:** Puede utilizar ambos componentes simultáneamente en un formulario. Estas son algunas recomendaciones para utilizar estos componentes:

**Bloque de Adobe Sign:** Puede usar el [!UICONTROL Bloque de Adobe Sign] para agregar campos de [!UICONTROL Adobe Sign] en cualquier parte del formulario adaptable. También ayuda a asignar campos específicos a los firmantes. Cuando se previsualiza o publica un formulario adaptable, el bloque de [!UICONTROL Adobe Sign] no está visible de forma predeterminada. Estos bloques solo están habilitados en el documento de firma. En el documento de firma, solo se activan los campos asignados a un firmante. [!UICONTROL El bloque de Adobe Sign] se puede utilizar con los primeros y siguientes firmantes.

**Componente del paso de firma:** Puede utilizar el componente del paso de firma para crear una experiencia de firma en el formulario. Solo permite que el primer firmante firme mientras se rellena el formulario. Cuando se representa la sección que contiene el componente Paso de firma, muestra una versión PDF firmable del formulario. Generalmente es la última o la penúltima sección seguida del componente de resumen de un formulario.

## Solución de problemas {#troubleshoot}

### Errores del acuerdo de [!DNL Adobe Sign] {#adobe-sign-agreement-failures}

**Problema**
Cuando el servicio de [!DNL Adobe Sign] está configurado para un formulario adaptable, el servicio no consigue crear un acuerdo de [!DNL Adobe Sign] para el formulario adaptable subyacente.

**Resolución**

* Compruebe la [configuración de Adobe Sign Cloud Service](../../forms/using/adobe-sign-integration-adaptive-forms.md) que se utiliza en el formulario adaptable.
* Asegúrese de que la aplicación API en el servidor [!DNL Adobe Sign] utilizada para configurar [!DNL Adobe Sign] Cloud Service tiene los permisos necesarios.
* Si utiliza varios servicios de [!DNL Adobe Sign] Cloud Services, señale la **[!UICONTROL URL oAuth]** de todos los servicios al mismo sistema para **[!UICONTROL compartir de Adobe Sign]**.

* Use direcciones de correo electrónico independientes para configurar la cuenta de [!DNL Adobe Sign] y para el primer y único firmante. La dirección de correo electrónico del primer firmante o del único firmante (si hay solo uno) no puede ser idéntica al de la cuenta de [!DNL Adobe Sign] utilizada para configurar AEM Cloud Services.

### El flujo de trabajo de AEM [!DNL Forms] configurado para un formulario adaptable habilitado para [!DNL Adobe Sign] no se inicia {#adobe-sign-aem-form-workflow-failures}

**Problema**
Cuando [!DNL Adobe Sign] está configurado para un formulario adaptable, el flujo de trabajo configurado con la opción Invocar flujo de trabajo de [!DNL Forms] no se inicia.

**Resolución**

* Cuando utilice [!DNL Adobe Sign] sin el paso de firma o el formulario requiere firmas de varias personas, el servidor de AEM [!DNL Forms] espera a que el planificador confirme que todas las personas han firmado el formulario. El planificador envía el formulario adaptable solo después de que todas las personas hayan completado la firma y el flujo de trabajo se inicie solo después de que se haya enviado correctamente el formulario adaptable. Puede acortar el intervalo del [planificador](adobe-sign-integration-adaptive-forms.md) para comprobar el estado de la firma del formulario a intervalos rápidos y el envío rápido del formulario.


## Artículos relacionados {#related-articles}

* [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Prácticas recomendadas para utilizar Adobe Sign con formularios adaptables](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Usar Adobe Sign con AEM Forms (vídeo)](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=es)
