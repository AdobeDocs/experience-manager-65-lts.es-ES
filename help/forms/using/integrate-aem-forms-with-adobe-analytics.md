---
title: Integrar AEM Forms con Adobe Analytics
description: AEM Forms se integra con Adobe Analytics para permitirle capturar y realizar un seguimiento de las métricas de rendimiento de los formularios publicados.
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 95%

---

# Analytics con [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms se integra con [Adobe Analytics](https://experienceleague.adobe.com/es/docs/analytics-learn/tutorials/overview) para permitirle capturar y hacer un seguimiento de las métricas de rendimiento de sus formularios publicados. El objetivo detrás del análisis de estas métricas es permitir que los usuarios empresariales obtengan información sobre el comportamiento del usuario final y optimizar la experiencia de captura de datos. Puede capturar y hacer un seguimiento del comportamiento de los usuarios que iniciaron sesión y no los que iniciaron sesión (anónimos) mediante Adobe Analytics para formularios adaptables.

También puede realizar análisis con Cloud Service Framework. Para obtener más información sobre cómo integrar AEM Forms con Cloud Service Framework, consulte [Analytics con Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md). La principal ventaja de utilizar Launch de Adobe con Analytics mediante Cloud Service Framework es que, además de estos eventos predeterminados, también puede definir eventos personalizados. Los eventos personalizados se definen mediante el Editor de reglas o clientlibs de clientes, y se asignan a eventos en [!DNL Adobe Analytics].

Después de realizar las acciones mencionadas en este artículo, puede configurar y ver los informes en [!DNL Adobe Analytics], como se muestra en el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Puede usar [!DNL Adobe Analytics] para descubrir patrones de interacción y problemas que los usuarios afrontan al utilizar los formularios adaptables. De forma predeterminada, [!DNL Adobe Analytics] rastrea y almacena información sobre los siguientes eventos:

* **Procesar**: Número de veces que se abre un formulario.

* **Enviar**: Número de veces que se envía un formulario.

* **Abandonar**: Número de veces que los usuarios se van sin completar el formulario.

* **Error**: Número de errores identificados en el panel y en los campos del panel.

* **Ayuda**: Número de veces que un usuario abre la ayuda de un panel y los campos del panel.

* **Visita al campo**: Número de veces que un usuario visita un campo del formulario.

* **Guardar**: Número de veces que los usuarios guardan un formulario en el Portal de Forms.

Además de estos eventos predeterminados, también puede definir eventos personalizados.

La siguiente imagen ilustra las acciones que debe realizar antes de ver los informes en [!DNL Adobe Analytics]:

![Información general de Analytics](/help/forms/using/assets/analyticsworkflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], cree lo siguiente:

* Un Adobe ID para iniciar sesión en [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* Un [grupo de informes](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).


### Instalar AEM Forms y extensiones de [!DNL Adobe Analytics] {#install-extensions}

Siga estos pasos para configurar AEM Forms y las extensiones de [Adobe Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/tags/extensions/client/analytics/overview):

1. Inicie sesión en Adobe Experience Cloud y seleccione un nombre adecuado para la empresa.

1. Seleccione **[!UICONTROL Launch/Recopilación de datos]** y seleccione **[!UICONTROL Ir a Launch/Recopilación de datos]**.

1. Seleccione **[!UICONTROL Nueva propiedad]** y especifique un nombre para la configuración.

1. Especifique un nombre de dominio y seleccione **[!UICONTROL Guardar]** para guardar la propiedad.

1. Seleccione el nombre de configuración disponible en la lista de Propiedades de la etiqueta.

1. En la sección **[!UICONTROL Creación]**, seleccione **[!UICONTROL Extensiones]**.

1. Seleccione **[!UICONTROL Catálogo]** y seleccione **[!UICONTROL Instalar]** para la extensión **[!UICONTROL Adobe Experience Manager Forms]**. **[!UICONTROL Adobe Experience Manager Forms]** se muestra en la lista de extensiones instaladas disponibles en la pestaña **Instalado**.

1. Seleccione **[!UICONTROL Instalar]** para la extensión **[!UICONTROL Adobe Analytics]**.
1. Seleccione el nombre del grupo de informes en las listas desplegables **[!UICONTROL Grupos de informes de desarrollo]**, **[!UICONTROL Grupos de informes de pruebas]** y **[!UICONTROL Grupos de informes de producto]** y seleccione **[!UICONTROL Guardar]** para guardar la extensión.

### Configurar elementos de datos {#configure-data-elements}

Puede seleccionar cualquiera de los elementos de datos configurados en una regla creada para un evento. Cuando se produce un evento en un formulario adaptable, AEM Forms envía estos elementos de datos a [!DNL Adobe Analytics].

Tras instalar la extensión **[!UICONTROL Adobe Experience Manager Forms]**, puede crear los siguientes elementos de datos:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Realice los siguientes pasos para configurar los elementos de datos:

1. En la sección **[!UICONTROL Creación]**, seleccione **[!UICONTROL Elementos de datos]**.

1. Seleccione **[!UICONTROL Crear nuevo elemento de datos]**.

1. Especifique un nombre para el elemento de datos. Por ejemplo, título de formulario para el tipo de elemento de datos FormTitle.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el **[!UICONTROL Tipo de elemento de datos]**.

1. Seleccione **[!UICONTROL Guardar]** para guardar el elemento de datos.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar reglas {#configure-rules}

Realice los siguientes pasos para crear reglas basadas en la extensión **[!UICONTROL Adobe Experience Manager Forms]**:

1. En la sección **[!UICONTROL Creación]**, seleccione **[!UICONTROL Reglas]**.

1. Seleccione **[!UICONTROL Crear nueva regla]**.

1. Especifique un nombre para la regla. Por ejemplo, Envío del formulario para registrar los envíos de formularios.

1. En la sección **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el tipo de evento. La entrada para el campo **[!UICONTROL Nombre]** se rellena automáticamente en función del tipo de evento seleccionado.

1. Seleccione **[!UICONTROL Conservar cambios]** para guardar el evento.

1. En la sección **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Establecer variables]** como tipo de acción. Las opciones disponibles en la lista desplegable incluyen las siguientes:

   * **[!UICONTROL Establecer variables]**: Utilice este tipo de acción para definir el tipo de evento para el que se envían los elementos de datos seleccionados de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Enviar señalización]**: Utilice este tipo de acción para enviar datos de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Borrar variables]**: Utilice este tipo de acción para borrar la pista de datos de modo que el evento se registre solo una vez en [!DNL Adobe Analytics].

     El método recomendado es usar la acción **[!UICONTROL Establecer variables]** para configurar el evento y los elementos de datos y, a continuación, utilizar **[!UICONTROL Enviar señalización]** para enviar datos y, luego, usar **[!UICONTROL Borrar variables]** para borrar la pista de datos.

1. En la sección **[!UICONTROL Props]**, asigne las opciones del grupo de informes disponibles en la lista desplegable con los elementos de datos definidos mediante [Configurar elementos de datos](#configure-data-elements).

   Por ejemplo, para enviar el elemento de datos **FormTitle** de AEM Forms a [!DNL Adobe Analytics] al enviar un formulario:
   1. En la sección **[!UICONTROL Props]**, seleccione una propiedad para el título de formulario disponible en el grupo de informes y, a continuación, seleccione ![Icono de la base de datos](/help/forms/using/assets/database-icon.svg) para asignarlo al título del formulario creado en [Configurar elementos de datos](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Seleccione **[!UICONTROL Agregar otro]** para agregar más elementos de datos a la lista.

1. En la sección **[!UICONTROL Eventos]**, seleccione un evento de las opciones disponibles en el grupo de informes y seleccione **[!UICONTROL Conservar cambios]**.

1. En la sección **[!UICONTROL Acciones]**, seleccione + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Enviar señalización]** como tipo de acción. En el panel derecho, seleccione **[!UICONTROL s.t()]** para enviar datos a [!DNL Adobe Analytics] y tratarla como una vista de página o **[!UICONTROL s.tl()]** para enviar datos a [!DNL Adobe Analytics] y que no lo trate como una vista de página. Seleccione **[!UICONTROL Conservar cambios]**.

1. En la sección **[!UICONTROL Acciones]**, seleccione + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Borrar variables]** como tipo de acción. Seleccione **[!UICONTROL Conservar cambios]**.  Después de realizar estos pasos, la sección **[!UICONTROL Acciones]** se muestra de la siguiente forma:
   ![Configuración de acciones](/help/forms/using/assets/actions-config.png)

   Personalice la sección **[!UICONTROL Acciones]** según sus necesidades. Por ejemplo, puede definir dos pasos **Enviar señalización** en un flujo de acciones para enviar datos a [!DNL Adobe Analytics] y que se trate como una vista de página en un paso y enviar datos a [!DNL Adobe Analytics] y que no se trate como una vista de página en el segundo paso.

   ![Configuración de acciones](/help/forms/using/assets/actions-config-2.png)

1. Seleccione **[!UICONTROL Guardar]** para guardar la regla.

   Puede crear reglas para todos los tipos de eventos, como Abandonar, Error, Visita de campo, Ayuda, Procesar, Guardar y Enviar.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flujos de publicación {#publish-flow}

Tras crear los elementos de datos y utilizarlos en las reglas, publique la configuración para recopilar datos de formulario en [!DNL Adobe Analytics].

Siga estos pasos para publicar la configuración:

1. En la sección **[!UICONTROL Publicación]**, seleccione **[!UICONTROL Flujo de publicación]**.

1. Seleccione **[!UICONTROL Añadir biblioteca]**, especifique un nombre y seleccione el entorno de la biblioteca.

1. Seleccione **[!UICONTROL Añadir todos los recursos modificados]** y, a continuación, seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

1. En la sección **[!UICONTROL Desarrollo]**, seleccione ![Más opciones](/help/forms/using/assets/more-options-icon.svg) y, luego, **[!UICONTROL Aprobar y publicar en producción]**.

1. Confirme los cambios y el flujo de publicación se mostrará pronto en la sección **[!UICONTROL Publicado]**.

![Flujo de publicación](/help/forms/using/assets/publish-flow.png)

## 2. Configurar AEM Forms {#configure-aem-forms}

Antes de crear la configuración de Adobe Launch, cree una [Configuración de Adobe IMS utilizando Adobe Launch como solución de nube](https://experienceleague.adobe.com/es/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/connect-aem-tag-property-using-ims).

### Crear configuración de Adobe Launch {#create-adobe-launch-configuration}

Realice los siguientes pasos para crear una configuración de Adobe Launch:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuraciones de Adobe Launch]**.

1. Seleccione una carpeta para crear la configuración y seleccione **[!UICONTROL Crear]**.

1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.

1. Seleccione la [configuración de Adobe IMS asociada](https://experienceleague.adobe.com/es/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/connect-aem-tag-property-using-ims).

1. Seleccione el nombre de la empresa utilizada mientras [configura Adobe Analytics](#Configure-adobe-analytics).

1. Seleccione el nombre de la propiedad creada mientras [configura Adobe Analytics](#install-extensions).

1. Seleccione **[!UICONTROL Guardar y cerrar]**.

1. Publique la configuración.

>[!NOTE]
>
> Cuando [incrusta AEM Forms en una página de AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md), no se admiten las configuraciones de Adobe Launch en un iFrame para formularios adaptables. Para resolver esto, configure las reglas de Adobe Launch directamente en la página de Sites o migre las configuraciones de Adobe Launch existentes de AEM Forms a la página de Sites.


### Habilitar [!DNL Adobe Analytics] para un formulario adaptable {#enable-analytics-adaptive-form}

Para usar la configuración de [!DNL Adobe Launch] en un formulario adaptable existente:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario adaptable y seleccione **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Básico]**, seleccione el [contenedor de configuración](#create-adobe-launch-configuration) utilizado al crear la configuración de Adobe Launch.
1. Seleccione **[!UICONTROL Guardar y cerrar]**.  El formulario adaptable está habilitado para [!DNL Adobe Analytics].
1. Publicar el formulario.

Tras habilitar [!DNL Adobe Analytics] para un formulario adaptable, puede [validar](https://experienceleague.adobe.com/es/docs/platform-learn/implement-in-websites/implement-solutions/analytics#validate-the-page-view-beacon) si hay un flujo de eventos de datos adecuado entre AEM Forms y [!DNL Adobe Analytics]. La integración de AEM Forms con Adobe Analytics ha finalizado. Ahora puede [configurar y ver informes en Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>En caso afirmativo, si las funciones [Analytics con Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md) y **Analytics con Adobe Launch** se activan simultáneamente, **Analytics con Adobe Launch** tendrá prioridad.
> 

### Crear reglas para capturar eventos personalizados (opcional) {#capture-custom-events}

Cree reglas sobre campos específicos de un formulario adaptable mediante el editor de reglas para enviar datos de Analytics de un formulario adaptable a [!DNL Adobe Analytics].

En un proceso de dos fases, usted define una regla en un campo de un formulario adaptable. La regla envía un evento. El nombre del evento se asigna a un evento de captura personalizado en Adobe Launch.

Para crear reglas utilizando el editor de reglas en un formulario adaptable:

1. Seleccione el campo y seleccione ![Editor de reglas](/help/forms/using/assets/rule-editor-icon.svg) para abrir la página del editor de reglas.
1. Defina una condición en la sección [!UICONTROL Cuándo] de la regla.
1. En la sección [!UICONTROL Entonces] de la regla, seleccione **[!UICONTROL Evento de envío]** de la lista desplegable **[!UICONTROL Seleccionar acción]**.
1. Especifique el nombre del evento en el campo **[!UICONTROL Nombre del tipo de evento]**.

Por ejemplo, si la fecha de nacimiento es anterior a una fecha determinada, AEM Forms envía el evento **Seguridad**.

![Evento de envío](/help/forms/using/assets/security-event.png)

Para asignar el evento a un evento de captura personalizado en [!DNL Adobe Analytics]:

1. [Cree una regla](#configure-rules).

1. En la sección **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Capturar evento personalizado]** de la lista desplegable **[!UICONTROL Tipo de evento]**.

1. Especifique el nombre del evento que indicó en el paso 4 al crear una regla con el editor de reglas.

1. Seleccione **Conservar cambios** y realice el resto de las acciones especificadas en [Configurar reglas](#configure-rules).

## 3. Configurar y ver informes en [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Después de configurar un formulario adaptable para enviar datos de evento a [!DNL Adobe Analytics], puede comenzar a ver los informes en [!DNL Adobe Analytics]:

1. Seleccione ![Seleccionar producto](/help/forms/using/assets/select-analytics.png) y seleccione **[!UICONTROL Analytics]**.

1. Seleccione **[!UICONTROL Crear proyecto]** y seleccione **[!UICONTROL Proyecto en blanco]**.

1. Seleccione el nombre del grupo de informes en la lista desplegable de la parte superior derecha de la forma libre.

1. Especifique **Título del formulario** en el texto **[!UICONTROL Buscar elementos de dimensión]** para ver todos los títulos de los formularios.

1. Coloque el título del formulario adaptable en el cuadro de texto **[!UICONTROL Colocar un segmento aquí (o cualquier otro componente)]**.

1. En la sección **[!UICONTROL Métricas]**, suelte los eventos que desea rastrear en el cuadro de texto **[!UICONTROL Colocar una métrica aquí (o cualquier otro componente)]**.

1. Seleccione ![Visualizaciones](/help/forms/using/assets/visualization-icon.svg) y suelte un tipo de gráfico en la sección de la forma libre. Del mismo modo, puede agregar varios tipos de gráficos a la sección de la forma libre.

1. Seleccione las teclas Ctrl + S y especifique un nombre para guardar el proyecto.

Para obtener información detallada sobre la visualización de informes de Forms Analytics, consulte [Visualizar y compreder los informes de AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).
