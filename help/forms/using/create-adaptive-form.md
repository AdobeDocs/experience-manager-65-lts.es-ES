---
title: 'Tutorial: Crear un formulario adaptable'
description: Aprenda a crear, diseñar y previsualizar un formulario adaptable. Además, aprenda a configurar las acciones de envío.
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 85%

---

# Tutorial: Crear un formulario adaptable {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](/help/forms/using/create-your-first-adaptive-form.md). Se recomienda seguir la serie en orden cronológico para comprender, realizar y mostrar el caso de uso del tutorial completo.

## Información sobre el tutorial {#about-the-tutorial}

Los formularios adaptables son formularios de nueva generación dinámicos y adaptables. Puede utilizar formularios adaptables para ofrecer experiencias personalizadas. También puede integrar formularios adaptables con [!DNL Adobe Analytics] para estadísticas de uso y [!DNL Adobe Campaign] para la administración de campañas. Para obtener más información sobre las capacidades de los formularios adaptables, consulte [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

Cuando se sigue un proceso adecuado, es más fácil crear y administrar formularios. En este artículo, aprenderá lo siguiente:

* [Crear un formulario adaptable que permita a un cliente agregar una dirección de envío](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Diseñar campos de un formulario adaptable para mostrar y aceptar información de un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Crear una acción de envío para enviar un correo electrónico que contenga contenido de formulario](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Previsualizar y enviar un formulario adaptable](/help/forms/using/create-adaptive-form.md)

Al final del artículo tendrá un formulario similar al siguiente:\
[![Vista previa del formulario en dispositivos móviles](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Paso 1: Crear el formulario adaptable {#step-create-the-adaptive-form}

1. Inicie sesión en la instancia de autor de AEM y navegue hasta **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**. La dirección URL predeterminada es [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparecerá una opción para seleccionar una plantilla. Seleccione la plantilla **[!UICONTROL En blanco]** para seleccionarla y seleccione **[!UICONTROL Siguiente]**.

1. Aparecerá una opción para **[!UICONTROL Agregar propiedades]**. Los campos **[!UICONTROL Título]** y **[!UICONTROL Nombre]** son obligatorios:

   * **Título:** especifique `Add new or update shipping address` en el campo **[!UICONTROL Título]**. El campo Título especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de AEM [!DNL Forms].
   * **Nombre:** especifique `shipping-address-add-update-form` en el campo **[!UICONTROL Nombre]**. El campo Nombre especifica el nombre para mostrar del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se sustituyen por guiones.

1. Seleccione **[!UICONTROL Crear]**. Se creará un formulario adaptable y aparecerá un cuadro de diálogo para abrir el formulario y editarlo. Seleccione **[!UICONTROL Abrir]** para abrir el formulario recién creado en una pestaña nueva. El formulario se abrirá para editarlo. También mostrará la barra lateral para personalizar el formulario recién creado según las necesidades.

   Para obtener información sobre la interfaz de creación de formularios adaptables y los componentes disponibles, consulte [Introducción a la creación de formularios adaptables](/help/forms/using/creating-adaptive-form.md).

   ![Formulario adaptable recién creado.](assets/newly-created-adaptive-form.png)

## Paso 2: Agregar un encabezado y pie de página {#step-add-header-and-footer}

AEM [!DNL Forms] proporciona muchos componentes para mostrar información en un formulario adaptable. Los componentes Encabezado y Pie de página ayudan a proporcionar una apariencia coherente a un formulario. Un encabezado suele incluir el logotipo de una empresa, el título del formulario y el resumen. Un pie de página suele incluir información de copyright y vínculos a otras páginas.

1. Seleccione ![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Se abre el explorador de componentes. Arrastre el componente **[!UICONTROL Encabezado]** desde el explorador de componentes hasta el formulario adaptable.
1. Seleccionar **[!UICONTROL logotipo]**. Aparecerá la barra de herramientas. Seleccione ![aem_6_3_edit](assets/aem_6_3_edit.png) en la barra de herramientas, escriba **We.Retail** y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Seleccione Imagen. Aparecerá la barra de herramientas. Seleccione ![cmppr](assets/cmppr.png). El explorador de propiedades se abrirá a la izquierda de la pantalla. **[!UICONTROL Examine]** y cargue la imagen del logotipo. Seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). La imagen aparecerá en el encabezado.

   Puede seleccionar Obtener archivo para descargar el logotipo utilizado en este artículo si no lo tiene.

[Obtener archivo](assets/logo.png)

1. Arrastre el componente **[!UICONTROL Pie de página]** desde ![treeexpandall](assets/treeexpandall.png) hasta el formulario adaptable. En esta fase, el formulario tendrá el siguiente aspecto:

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## Paso 3: Agregar componentes para capturar y mostrar información {#step-add-components-to-capture-and-display-information}

Los componentes son componentes básicos de un formulario adaptable. AEM [!DNL Forms] proporciona muchos componentes para capturar y mostrar información en un formulario adaptable. Puede arrastrar los componentes desde ![treeexpandall](assets/treeexpandall.png) hasta un formulario. Para obtener más información sobre los componentes disponibles y las funcionalidades correspondientes, consulte [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

1. Arrastre el **[!UICONTROL Componente Cuadro numérico]** hasta el formulario adaptable. Colóquelo antes del componente Pie de página. Abra las propiedades del componente, cambie el **[!UICONTROL Título]** del componente a **`Customer ID`**, cambie el **[!UICONTROL Nombre del elemento]** a **`customer_ID`**, habilite la opción **[!UICONTROL Campo requerido]**, habilite la opción **[!UICONTROL Usar tipo de entrada de número HTML5]** y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Arrastre tres componentes Cuadro de texto hasta el formulario adaptable. Colóquelos antes del componente Pie de página. Defina las siguientes propiedades para estos cuadros de texto.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propiedad</b></td> 
      <td><b>Cuadro de texto 1<br/></b></td> 
      <td><b>Cuadro de texto 2<br/></b></td> 
      <td><b>Cuadro de texto 3</b></td> 
     </tr> 
     <tr> 
      <td>Título</td> 
      <td>Nombre<br /> </td> 
      <td>Dirección de envío</td> 
      <td>Estado</td> 
     </tr> 
     <tr> 
      <td>Nombre de elemento</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>Campo obligatorio</td> 
      <td>Habilitado</td> 
      <td>Habilitado</td> 
      <td>Habilitado</td> 
     </tr> 
     <tr> 
      <td>Permitir varias líneas<br /> </td> 
      <td>Deshabilitado</td> 
      <td>Habilitado</td> 
      <td>Deshabilitado</td> 
     </tr> 
    </tbody> 
   </table>

1. Arrastre un componente **[!UICONTROL Cuadro numérico]** antes del componente Pie de página. Abra las propiedades del componente, establezca los valores enumerados en la siguiente tabla, seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Valor |
   |---|---|
   | Título | Código ZIP |
   | Nombre de elemento | customer_ZIPCode |
   | Número máximo de dígitos | 6 |
   | Campo obligatorio | Habilitado |
   | Tipo de patrón de visualización | Sin patrón |

1. Arrastre un componente **[!UICONTROL Correo electrónico]** antes del componente Pie de página. Abra las propiedades del componente, establezca los valores enumerados en la siguiente tabla y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Valor |
   |---|---|
   | Título | Correo electrónico |
   | Nombre de elemento | customer_Email |
   | Campo obligatorio | Habilitado |

1. Arrastre un **[!UICONTROL Archivo adjunto]** antes del componente Pie de página. Abra las propiedades del componente, establezca los valores enumerados en la siguiente tabla y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propiedad</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Título</td> 
      <td>Prueba de dirección aprobada por el gobierno<br /> </td> 
     </tr> 
     <tr> 
      <td>Nombre de elemento</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>Campo obligatorio</td> 
      <td>Habilitado</td> 
     </tr> 
    </tbody> 
   </table>

1. Arrastre un componente **[!UICONTROL Botón de envío]** hasta el formulario adaptable. Colóquelo antes del componente Pie de página. Abra las propiedades del componente, cambie el Nombre del elemento a `address_addition_update_submit`, seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). La presentación del formulario estará completa y el formulario tendrá el siguiente aspecto:

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Paso 4: Configurar la acción de envío para el formulario adaptable {#step-configure-submit-action-for-the-adaptive-form}

Se activa una acción de envío cuando un usuario pulsa el botón Enviar en un formulario adaptable. Puede utilizar una acción de envío para guardar datos de formulario en el repositorio local, enviar datos de formulario a un extremo REST, enviar datos de formulario como correo electrónico, etc. Los formularios adaptables proporcionan algunas acciones de envío integradas. Para obtener información detallada, consulte [Configurar la acción de envío](/help/forms/using/configuring-submit-actions.md).

Con los siguientes pasos, puede configurar la acción de envío por correo electrónico y la acción de envío de demostración del formulario:

1. Configure el servidor de correo electrónico. Para obtener más información, consulte [Configurar notificaciones de correo electrónico](/help/sites-administering/notification.md).


1. Seleccione **[!UICONTROL Contenedor de formulario]** en el Explorador de contenido y seleccione ![cmppr](assets/cmppr.png). El explorador de propiedades se abrirá a la izquierda.
1. Vaya a **[!UICONTROL Envío]** > **[!UICONTROL Enviar acción]**. Seleccione **[!UICONTROL Enviar correo electrónico]**. Especifique los siguientes valores y seleccione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Valor |
   |--- |--- |
   | De | `donotreply@weretail.com` |
   | Para | `${customer_Email}` |
   | Asunto | Reconocimiento: Ha agregado la dirección de envío al sitio web de We.Retail. |
   | Plantilla de correo electrónico | Hola,`${customer_Name}`: La siguiente dirección se agrega como dirección de envío de la cuenta: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Saludos, We.Retail |
   | Incluir datos adjuntos | Habilitado |

   Su formulario está listo. Ahora puede obtener previsualizar el formulario y probar la funcionalidad. Si ha utilizado el nombre mencionado en el tutorial y ha accedido al formulario en el equipo que ejecuta el servidor de AEM [!DNL Forms], el formulario estará disponible en [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Paso 5: Previsualizar y enviar el formulario adaptable {#step-preview-and-submit-the-adaptive-form}

Puede usar la opción **[!UICONTROL Previsualizar]** para evaluar la apariencia y el comportamiento de un formulario. Puede enviar un formulario en el modo de previsualización y también comprobar las validaciones aplicadas a un formulario. Por ejemplo, si se muestra un error cuando un campo obligatorio se deja vacío.

Los formularios adaptables también proporcionan una opción para emular la experiencia de un formulario para varios dispositivos. Por ejemplo, iPhone, iPad y escritorio. Puede usar tanto la opción de **[!UICONTROL Previsualización]** como el **[!UICONTROL Emulador]** ![regla](assets/ruler.png) junto con otras opciones para obtener una vista previa de un formulario para dispositivos con diferentes tamaños de pantalla.

1. Seleccione la opción **[!UICONTROL Vista previa]** a la derecha del editor de formularios. El formulario se abrirá en el modo de previsualización. Si ha utilizado el nombre mencionado en el tutorial, la dirección URL de vista previa del formulario es [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Usar ![regla](assets/ruler.png) para ver el aspecto del formulario en varios dispositivos.
1. Rellene los campos del formulario y seleccione **[!UICONTROL Enviar]**. El formulario se enviará y se le redirigirá a la página **de agradecimiento** predeterminada. También puede especificar una página de agradecimiento personalizada. Para obtener más información, consulte [Configurar la página de redireccionamiento](/help/forms/using/configuring-redirect-page.md).

El formulario adaptable al que agregar una dirección está listo. Si ha utilizado el nombre mencionado en el tutorial y accede al formulario en el equipo que ejecuta el servidor de AEM Forms, el formulario estará disponible en [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
