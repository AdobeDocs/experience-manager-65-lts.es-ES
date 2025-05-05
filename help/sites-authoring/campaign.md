---
title: Uso de Adobe Campaign Classic y Adobe Campaign Standard
description: Puede crear contenido de correo electrónico en AEM y procesarlo en correos electrónicos de Adobe Campaign
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2770'
ht-degree: 0%

---

# Uso de Adobe Campaign Classic y Adobe Campaign Standard{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

Puede crear contenido de correo electrónico en AEM y procesarlo en correos electrónicos de Adobe Campaign. Para ello, debe:

1. Cree una newsletter en AEM a partir de una plantilla específica de Adobe Campaign.
1. Seleccione [un servicio de Adobe Campaign](#selecting-the-adobe-campaign-cloud-service-and-template) antes de editar el contenido para acceder a toda la funcionalidad.
1. Edite el contenido.
1. Valide el contenido.

A continuación, el contenido se puede sincronizar con una entrega en Adobe Campaign. Las instrucciones detalladas se describen en este documento.

Consulte también [Creación de Adobe Campaign Forms en AEM](/help/sites-authoring/adobe-campaign-forms.md).

>[!NOTE]
>
>Antes de usar esta funcionalidad, debes configurar AEM para que se integre con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Envío de contenido de correo electrónico mediante Adobe Campaign {#sending-email-content-via-adobe-campaign}

Después de configurar AEM y Adobe Campaign, puede crear contenido de envío de correo electrónico directamente en AEM y luego procesarlo en Adobe Campaign.

Al crear contenido de Adobe Campaign en AEM, debe vincular a un servicio de Adobe Campaign antes de editar el contenido para acceder a todas las funcionalidades.

Hay dos casos posibles:

* El contenido se puede sincronizar con una entrega desde Adobe Campaign. Esto permite utilizar contenido de AEM en una entrega.
* (Solo Adobe Campaign Classic) El contenido se puede enviar directamente a Adobe Campaign, que genera automáticamente un nuevo envío de correo electrónico. Este modo tiene limitaciones.

Las instrucciones detalladas se describen en este documento.

### Creación de nuevo contenido de correo electrónico {#creating-new-email-content}

>[!NOTE]
>
>Al agregar plantillas de correo electrónico, asegúrese de agregarlas en **/content/campaigns** para que estén disponibles.

#### Creación de nuevo contenido de correo electrónico {#creating-new-email-content-1}

1. En AEM, seleccione **Sitios**, luego **Campañas** y busque dónde se administran sus campañas de correo electrónico. En el ejemplo siguiente, la ruta es **Sitios** > **Campañas** > **Geometrixx Outdoors** > **Campañas de correo electrónico**.

   >[!NOTE]
   >
   >[Las muestras de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md). Descargue contenido de Geometrixx de muestra desde Package Share.

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. Seleccione **Crear** y luego **Crear página**.
1. Seleccione una de las plantillas disponibles específicas a la cual se está conectando Adobe Campaign y luego haga clic en **Siguiente**. Hay tres plantillas disponibles de forma predeterminada:

   * **Correo electrónico de Adobe Campaign Classic**: permite agregar contenido a una plantilla predefinida (dos columnas) antes de enviarlo a Adobe Campaign Classic para su envío.
   * **Correo electrónico de Adobe Campaign Standard**: permite agregar contenido a una plantilla predefinida (dos columnas) antes de enviarlo a Adobe Campaign Standard para su envío.

1. Rellene **Title** y, opcionalmente, **Description** y haga clic en **Crear**. El título se utiliza como asunto de la newsletter/correo electrónico a menos que lo sobrescriba al editar el correo electrónico.

### Selección del servicio en la nube y la plantilla de Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Para integrarse con Adobe Campaign, debe añadir un servicio de nube de Adobe Campaign a la página. Al hacerlo, puede acceder a la personalización y a otra información de Adobe Campaign.

Además, es posible que también tenga que seleccionar la plantilla de Adobe Campaign, cambiar el asunto y añadir contenido de texto sin formato para los usuarios que no verán el correo electrónico en HTML.

Puede seleccionar el servicio en la nube desde la pestaña **Sitios** o desde el correo electrónico o boletín informativo una vez que lo haya creado.

El método recomendado es seleccionar el servicio en la nube desde la ficha **Sitios**. La selección del servicio en la nube desde el correo electrónico/newsletter requiere una solución alternativa.

Desde la página **Sitios**:

1. En AEM, seleccione la página de correo electrónico y haga clic en **Ver propiedades**.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Seleccione **Editar** y, a continuación, la pestaña **Cloud Services**, desplácese hacia abajo hasta la parte inferior, haga clic en el signo + para agregar una configuración y, por último, seleccione **Adobe Campaign**.

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. Seleccione la configuración que coincida con su instancia de Adobe Campaign en la lista desplegable y confirme haciendo clic en **Guardar**.
1. Para ver la plantilla que el correo electrónico le ha aplicado, haga clic en la ficha **Adobe Campaign**. Si desea seleccionar otra plantilla, puede acceder a ella desde el correo electrónico mientras la edita.

   Si desea aplicar una plantilla de envíos de correo electrónico específica (de Adobe Campaign), que no sea la plantilla de correo predeterminada, en **Propiedades**, seleccione la pestaña **Adobe Campaign**. Introduzca el nombre interno de la plantilla de envíos de correo electrónico en la instancia de Adobe Campaign relacionada.

   La plantilla que seleccione determinará qué campos de personalización están disponibles en Adobe Campaign.

   ![chlimage_1-18](assets/chlimage_1-18a.png)

En la newsletter/el correo electrónico de la creación, es posible que no pueda seleccionar la configuración del servicio en la nube de Adobe Campaign en **Propiedades de página** debido a un problema de diseño. Puede utilizar la solución que se describe aquí:

1. En AEM, seleccione la página de correo electrónico y haga clic en **Editar**. Haga clic en **Abrir propiedades**.

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. Seleccione **Cloud Services** y haga clic en **+** para agregar una configuración. Seleccione cualquier configuración visible (no importa cuál). Haga clic en el signo **+** para agregar otra configuración y luego seleccione **Adobe Campaign**.

   >[!NOTE]
   >
   >También puede seleccionar los servicios en la nube seleccionando **Ver propiedades** en la pestaña **Sitios**.

1. Seleccione la configuración que coincida con la instancia de Adobe Campaign en la lista desplegable, elimine la primera configuración que creó que no era para Adobe Campaign y, a continuación, confirme haciendo clic en la marca de verificación.
1. Siga con el paso 4 del procedimiento anterior para seleccionar plantillas y agregar texto sin formato.

### Edición de contenido de correo electrónico {#editing-email-content}

Para editar el contenido del correo electrónico:

1. Abra el correo electrónico y, de forma predeterminada, introduzca el modo Editar.

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. Si desea cambiar el asunto del correo electrónico o agregar texto sin formato para los usuarios que no verán el correo electrónico en HTML, seleccione **Correo electrónico** y agregue un asunto y un texto. Seleccione el icono de página para generar automáticamente una versión de texto sin formato desde HTML. Haga clic en la marca de verificación cuando termine.

   Puede personalizar la newsletter mediante los campos de personalización de Adobe Campaign. Para agregar un campo de personalización, abra el selector de campos de personalización haciendo clic en el botón que muestra el logotipo de Adobe Campaign. A continuación, puede elegir entre todos los campos disponibles para esta newsletter.

   >[!NOTE]
   >
   >Si los campos de personalización de las propiedades desde el editor están atenuados, vuelva a examinar la configuración.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Abra el panel Componentes en la parte izquierda de la pantalla y seleccione **Adobe Campaign Newsletter** del menú desplegable para encontrar esos componentes.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Arrastre los componentes directamente a la página y edítelos en consecuencia. Por ejemplo, puede arrastrar un componente **Texto y Personalization (Campaign)** y agregar texto personalizado.

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   Consulte [Componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obtener una descripción detallada de cada componente.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### Inserción de personalización {#inserting-personalization}

Al editar el contenido, puede insertar:

* Campos de contexto de Adobe Campaign. Son campos que se pueden insertar dentro del texto y que se adaptan a los datos del destinatario (por ejemplo, nombre, apellidos o cualquier dato de la dimensión objetivo).
* Bloques de personalización de Adobe Campaign. Son bloques de contenido predefinido que no están relacionados con los datos del destinatario, como un logotipo de una marca o un vínculo a una página espejo.

Consulte [Componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obtener una descripción completa de los componentes de Campaign.

>[!NOTE]
>
>* Solo se tienen en cuenta los campos de la dimensión de segmentación **Profiles** de Adobe Campaign.
>* Al ver las propiedades de **Sites**, no tiene acceso a los campos de contexto de Adobe Campaign. Puede acceder a ellas directamente desde el correo electrónico mientras edita.

Para insertar una personalización:

1. Inserte un nuevo componente **Newsletter** > **Texto y Personalization (Campaign)** arrastrándolo a la página.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Abra el componente haciendo clic en el icono Lápiz. Se abre el editor en contexto.

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**Para Adobe Campaign Standard:**
   >
   >* Los campos de contexto disponibles corresponden a la dimensión de segmentación **Profiles** en Adobe Campaign.
   >* Ver [Vincular una página de AEM a un correo electrónico de Adobe Campaign](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard).
   >
   >**Para Adobe Campaign Classic:**
   >
   >* Los campos de contexto disponibles se recuperan dinámicamente del esquema **nms:seedMember** de Adobe Campaign. Los datos de la extensión de Target se recuperan dinámicamente del flujo de trabajo que contiene la entrega sincronizada con el contenido. (Consulte la sección [Sincronización del contenido creado en AEM con un envío de Adobe Campaign](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)).
   >
   >* Para agregar u ocultar elementos de personalización, consulte [Administración de campos y bloques de personalización](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks).
   >* **Importante**: todos los campos de la tabla semilla también deben estar en la tabla de destinatarios (o en la tabla de contacto correspondiente).

1. Inserte texto escribiendo. Inserte campos de contexto o bloques de personalización haciendo clic en los componentes de Adobe Campaign y seleccionándolos. Cuando termine, seleccione la marca de verificación.

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   Después de insertar campos de contexto o bloques de personalización, puede obtener una vista previa del boletín informativo y probar los campos. Ver [Vista previa de una newsletter](#previewing-a-newsletter).

### Previsualización de una newsletter {#previewing-a-newsletter}

Puede obtener una vista previa del aspecto que tendrá la newsletter y previsualizar la personalización.

1. Con la newsletter abierta, haz clic en **Vista previa** en la esquina superior derecha de AEM. AEM muestra el aspecto de la newsletter cuando los usuarios la reciben.

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >Si utiliza Adobe Campaign Standard y la plantilla de ejemplo, dos bloques de personalización que muestran contenido inicial - **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** y **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;** - generarán errores al importar el contenido durante la entrega. Puede ajustarlos seleccionando los bloques correspondientes con el selector de bloques personalizado.

1. Para obtener una vista previa de la personalización, abra ContextHub tocando o haciendo clic en el icono correspondiente de la barra de herramientas. Las etiquetas de los campos de personalización ahora se sustituyen por los datos semilla de la persona seleccionada. Consulte cómo se adaptan las variables al cambiar de perfil en ContextHub.

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. Puede ver los datos semilla procedentes de Adobe Campaign que están asociados al usuario seleccionado actualmente. Para ello, haga clic en el módulo Adobe Campaign en la barra de ContextHub. Se abrirá un cuadro de diálogo en el que se mostrarán todos los datos semilla del perfil actual. De nuevo, los datos se adaptan cuando se cambia a una persona diferente.

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### Aprobación de contenido en AEM {#approving-content-in-aem}

Una vez finalizado el contenido, puede iniciar el proceso de aprobación. Vaya a la pestaña **Workflow** del cuadro de herramientas y seleccione el flujo de trabajo **Aprobar para Adobe Campaign**.

Este flujo de trabajo predeterminado tiene dos pasos: revisión y luego aprobación, o revisión y luego rechazo. Sin embargo, este flujo de trabajo se puede ampliar y adaptar a un proceso más complejo.

![chlimage_1-31](assets/chlimage_1-31a.png)

Para aprobar contenido para Adobe Campaign, aplique el flujo de trabajo seleccionando **Flujo de trabajo** y **Aprobar para Adobe Campaign**, y haga clic en **Iniciar flujo de trabajo**. Siga los pasos y apruebe el contenido. También puede rechazar el contenido seleccionando **Rechazar** en lugar de **Aprobar** en el último paso del flujo de trabajo.

![chlimage_1-32](assets/chlimage_1-32a.png)

Una vez aprobado el contenido, aparece como aprobado en Adobe Campaign. A continuación, se puede enviar el correo electrónico.

En Adobe Campaign Standard:

![chlimage_1-33](assets/chlimage_1-33a.png)

En Adobe Campaign Classic:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>El contenido no aprobado se puede sincronizar con un envío en Adobe Campaign, pero el envío no se puede ejecutar. Solo se puede enviar contenido aprobado a través de envíos de Campaign.

## Vinculación de AEM con Adobe Campaign Standard y Adobe Campaign Classic {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

La forma de vincular o sincronizar AEM con Adobe Campaign depende de si utiliza Adobe Campaign Standard basado en suscripción o Adobe Campaign Classic local.

Consulte las secciones siguientes para obtener instrucciones basadas en la solución de Adobe Campaign:

* [Vinculación de una página de AEM a un correo electrónico de Adobe Campaign (Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [Sincronización del contenido creado en AEM con un envío de Adobe Campaign Classic](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### Vinculación de una página de AEM a un correo electrónico de Adobe Campaign (Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard permite recuperar y vincular contenido creado en AEM con:

* Un correo electrónico.
* Una plantilla de correo electrónico.

Al hacerlo, puede enviar el contenido. Verá si un boletín informativo está vinculado a un único envío por el código que se muestra en la página.

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
>
>Si un boletín informativo está vinculado a varios envíos, se muestra el número de envíos vinculados (pero no todos los ID).

Para vincular una página creada en AEM con un correo electrónico de Adobe Campaign:

1. Cree un correo electrónico basado en una plantilla de correo electrónico específica de AEM. Consulte [Creación de correos electrónicos en Adobe Campaign Standard](https://helpx.adobe.com/campaign/standard/channels/using/creating-an-email.html) para obtener más información.

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. Abra el bloque **Content** del panel de envío.

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. Seleccione **Vínculo con contenido de Adobe Experience Manager** en la barra de herramientas para acceder a la lista de contenido disponible en AEM.

   >[!NOTE]
   >
   >Si la opción **Vínculo con un Adobe Experience Manager** no aparece en la barra de acciones, compruebe que el **Modo de edición de contenido** esté configurado correctamente en **Adobe Experience Manager** en las propiedades de correo electrónico.

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. Seleccione el contenido que desee utilizar en el correo electrónico.

   Esta lista especifica:

   * La etiqueta del contenido en AEM.
   * El estado de aprobación del contenido en AEM. Si el contenido no está aprobado, puede sincronizarlo, pero tendrá que aprobarse antes de realizar la entrega. Sin embargo, puede ejecutar determinadas operaciones, como enviar una prueba o la prueba de previsualización.
   * La fecha de la última modificación del contenido.
   * Cualquier contenido que ya esté vinculado a una entrega.

   >[!NOTE]
   >
   >De forma predeterminada, el contenido que ya está sincronizado con una entrega está oculto. Sin embargo, puede mostrarlo y utilizarlo. Por ejemplo, si desea utilizar el contenido como plantilla para varios envíos.

   Cuando el correo electrónico está vinculado a un contenido de AEM, el contenido no se puede editar en Adobe Campaign.

1. Especifique los demás parámetros del correo electrónico desde su panel (audiencias, programación de ejecución).
1. Ejecute la entrega de correo electrónico. Durante el análisis de la entrega, se recupera la versión más actualizada del contenido de AEM.

   >[!NOTE]
   >
   >Si el contenido se actualiza en AEM mientras está vinculado a un correo electrónico, se actualiza automáticamente en Adobe Campaign durante el análisis. La sincronización también se puede ejecutar manualmente usando **Actualizar contenido de Adobe Experience Manager** desde la barra de acciones de contenido.
   >
   >Puede cancelar el vínculo entre un correo electrónico y el contenido de AEM usando **Eliminar el vínculo con el contenido de Adobe Experience Manager** de la barra de acciones de contenido. Este botón solo está disponible si un contenido ya está vinculado con la entrega. Para vincular un contenido diferente a una entrega, debe eliminar el vínculo de contenido actual antes de poder establecer un vínculo nuevo.
   >
   >Cuando se elimina el vínculo, el contenido local se conserva y se puede editar en Adobe Campaign. Si vuelve a vincular el contenido después de haberlo modificado, se perderán todos los cambios.

### Sincronización del contenido creado en AEM con un envío de Adobe Campaign Classic {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign permite recuperar y sincronizar contenido creado en AEM con:

* Entrega de una campaña
* Una actividad de envío en un flujo de trabajo de campaña
* Un envío recurrente
* Un envío continuo
* Un envío del centro de mensajes
* Una plantilla de envíos

En AEM, si un boletín informativo está vinculado a un solo envío, el código de envío se muestra en la página.

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
>
>Si la newsletter está vinculada a varios envíos, se muestra el número de envíos vinculados (pero no todos los ID).
>
>[!NOTE]
>
>El paso del flujo de trabajo **Publicar en Adobe Campaign** está obsoleto en AEM 6.1. Este paso formaba parte de la integración de AEM 6.0 con Adobe Campaign y ya no es necesario.

Para sincronizar contenido creado en AEM con un envío de Adobe Campaign:

1. Cree una entrega o agregue una actividad de entrega a un flujo de trabajo de campaña seleccionando la plantilla de entrega **Email delivery with AEM content (mailAEMContent)**.

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. Seleccione **Sincronizar** en la barra de herramientas para acceder a la lista de contenido disponible en AEM.

   >[!NOTE]
   >
   >Si la opción **Synchronize** no aparece en la barra de herramientas de la entrega, compruebe que el campo **Content editing mode** esté configurado correctamente en **AEM** seleccionando **Properties** > **Advanced**.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Seleccione el contenido que desea sincronizar con su envío.

   Esta lista especifica:

   * La etiqueta del contenido en AEM.
   * El estado de aprobación del contenido en AEM. Si el contenido no está aprobado, puede sincronizarlo, pero tendrá que aprobarse antes de realizar la entrega. Sin embargo, puede ejecutar determinadas operaciones, como enviar una BAT o la prueba de vista previa.
   * La fecha de la última modificación del contenido.
   * Cualquier contenido que ya esté vinculado a una entrega.

   >[!NOTE]
   >
   >De forma predeterminada, el contenido que ya está sincronizado con una entrega está oculto. Sin embargo, puede mostrarlo y utilizarlo. Por ejemplo, si desea utilizar el contenido como plantilla para varios envíos.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Especifique los demás parámetros de la entrega (objetivo, etc.)
1. Si es necesario, inicie el proceso de aprobación de la entrega en Adobe Campaign. Se necesita la aprobación de contenido en AEM, además de las aprobaciones configuradas en Adobe Campaign (presupuesto, objetivo, etc.). La aprobación de contenido en Adobe Campaign solo es posible si el contenido ya está aprobado en AEM.
1. Ejecute la entrega. Durante el análisis de envío, se recupera la versión más actualizada del contenido de AEM.

   >[!NOTE]
   >
   >* Una vez sincronizados el envío y el contenido, el contenido de la entrega en Adobe Campaign se convierte en de solo lectura. El asunto del correo electrónico y su contenido ya no se pueden modificar.
   >* Si el contenido se actualiza en AEM mientras está vinculado a una entrega en Adobe Campaign, se actualiza automáticamente en la entrega durante el análisis de la entrega. La sincronización también se puede ejecutar manualmente con el botón **Actualizar contenido ahora**.
   >* Puede cancelar la sincronización entre un envío y el contenido de AEM mediante el botón **Desincronizar**. Esto solo está disponible si un contenido ya está sincronizado con el envío. Para sincronizar un contenido diferente con una entrega, debe cancelar la sincronización de contenido actual antes de poder establecer un nuevo vínculo.
   >* Si se desincroniza, el contenido local se conserva y se puede editar en Adobe Campaign. Si vuelve a sincronizar el contenido después de haberlo modificado, perderá todos los cambios.
   >* En el caso de los envíos recurrentes y continuos, la sincronización con el contenido de AEM se detiene cada vez que se ejecuta el envío.
