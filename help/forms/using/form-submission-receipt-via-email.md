---
title: Enviar una confirmación de envío de formulario por correo electrónico
description: AEM Forms permite configurar una acción de envío por correo electrónico que envía una confirmación a un usuario al enviar el formulario.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 93%

---

# Enviar una confirmación de envío de formulario por correo electrónico {#sending-a-form-submission-acknowledgement-via-email}

## Envío de datos de formularios adaptables {#adaptive-form-data-submission}

Los formularios adaptables proporcionan varios flujos de trabajo de [acciones de envío](../../forms/using/configuring-submit-actions.md) predeterminados para enviar los datos del formulario a diferentes extremos.

Por ejemplo, la acción de envío **[!UICONTROL Enviar correo electrónico]** envía un correo electrónico cuando se envía correctamente un formulario adaptable. También se puede configurar el envío de los datos del formulario y el PDF en el correo electrónico.

Este artículo detalla los pasos para habilitar la acción Enviar por correo electrónico en un formulario adaptable y las diferentes configuraciones que proporciona.

>[!NOTE]
>
>También puede usar la opción **[!UICONTROL Enviar PDF por correo electrónico]** para enviar el formulario completado por correo electrónico como archivo adjunto PDF. Las opciones de configuración disponibles para esta acción son las mismas que las disponibles para la acción **[!UICONTROL Enviar correo electrónico]**. La acción Enviar PDF por correo electrónico solo está disponible para formularios adaptables basados en XFA.

## Acción Enviar correo electrónico {#email-action}

La acción Enviar correo electrónico permite a un autor enviar correos electrónicos automáticamente a uno o varios destinatarios cuando el envío de un formulario adaptable se realiza correctamente.

>[!NOTE]
>
>Para utilizar la acción Enviar correo electrónico, debe configurar el servicio de correo electrónico de AEM como se describe en [Configuración del servicio de correo electrónico](/help/sites-administering/notification.md#configuring-the-mail-service).

### Habilitación de la acción Enviar correo electrónico en un formulario adaptable {#enabling-email-action-on-an-adaptive-form}

1. Abra un formulario adaptable en el modo **[!UICONTROL Edición]**.

1. En la pestaña **[!UICONTROL Contenido]**, seleccione **[!UICONTROL Contenedor de formulario]** y seleccione ![configurar](assets/configure-icon.svg) para ver las propiedades del formulario adaptable.

1. En la sección **[!UICONTROL Envío]**, seleccione **[!UICONTROL Enviar correo electrónico]** en la lista desplegable **[!UICONTROL Acción de envío]**.

   ![Acciones de envío](assets/submission-actions.png)

1. Especifique un ID de correo electrónico válido en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** y **[!UICONTROL CCO]**.

   Especifique el asunto y el cuerpo del correo electrónico en los campos **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]**, respectivamente.

   También puede especificar marcadores de posición de variables en los campos, en cuyo caso, los valores de los campos se procesarán cuando un usuario final envíe correctamente el formulario. Para obtener más información, consulte [Uso de nombres de campos de formulario adaptables para crear contenido de correo electrónico de forma dinámica](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Seleccione **[!UICONTROL Incluir datos adjuntos]** si el formulario incluye archivos adjuntos y desea adjuntarlos al correo electrónico.

   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Enviar PDF por correo electrónico]**, debe seleccionar la opción Incluir datos adjuntos.

1. Haga clic en ![Aceptar](assets/save_icon.svg) para guardar los cambios.

### Usar nombres de campo de formulario adaptable para crear contenido de correo electrónico de forma dinámica {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Los nombres de campo de un formulario adaptable se denominan marcadores de posición, y se reemplazan por el valor de ese campo una vez que un usuario envía el formulario.

En la acción **[!UICONTROL Enviar correo electrónico]**, puede utilizar marcadores de posición que se procesan cuando se realiza la acción. Eso significa que los encabezados del correo electrónico (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]** y **[!UICONTROL Asunto]**) se generan cuando el usuario envía el formulario.

Para definir un marcador de posición, especifique `${<field name>}` en un campo después de seleccionar **[!UICONTROL Enviar correo electrónico]** como acción de envío.

Por ejemplo, si el formulario contiene el campo **[!UICONTROL Dirección de correo electrónico]**, denominado `email_addr`, para capturar el ID de correo electrónico de un usuario, puede especificar lo siguiente en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** o **[!UICONTROL CCO]**.

`${email_addr}`

Cuando un usuario envía el formulario, se envía un correo electrónico al ID de correo electrónico introducido en el campo `email_addr` del formulario.

>[!NOTE]
>
>Puede encontrar el nombre de un campo en el cuadro de diálogo **[!UICONTROL Editar]** del campo.

Los marcadores de posición de variables también se pueden usar en los campos **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]**.

Por ejemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Los campos de los paneles repetibles no se pueden usar como marcadores de posición variables.
