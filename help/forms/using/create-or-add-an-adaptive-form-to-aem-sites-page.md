---
title: Crear o agregar un formulario adaptable mediante la página de AEM Sites
description: Descubra cómo crear o agregar fácilmente un formulario adaptable a su página de AEM Sites. Conozca las técnicas paso a paso y las prácticas recomendadas para integrar formularios dinámicos y personalizables en su sitio web, optimizando las experiencias digitales para lograr el máximo impacto.
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 6e69ca67-883f-4079-96e2-5b7a9c843ada
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '2893'
ht-degree: 91%

---

# Crear o agregar un formulario adaptable mediante la página de AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=es).

Con AEM Forms, puede incorporar fácilmente formularios adaptables a sus páginas web. Esto permite a los visitantes rellenar y enviar formularios cómodamente sin salir de la página en la que se encuentran. Al hacerlo, pueden interactuar fácilmente con otros elementos del sitio web e interactuar activamente con el formulario.

Puede utilizar el Editor de páginas de AEM para crear y agregar rápidamente varios formularios a las páginas de AEM Sites. El uso del Editor de páginas de AEM permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de una página de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de procesos empresariales. También le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

AEM Forms proporciona el contenedor del formulario adaptable y los componentes incrustados de formularios adaptables. Puede utilizar el contenedor de formulario adaptable para crear un formulario en un fragmento de experiencia o una página de AEM Sites, mientras que el componente Forms adaptable: incrustado permite agregar un formulario adaptable existente o crear un formulario con el editor de Forms adaptable.

![Formulario adaptable en la página de sitios](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## Ventajas del uso del componente Contenedor de formulario adaptable en el editor de páginas o en el fragmento de experiencia de AEM

El uso del contenedor de formulario adaptable en el editor de páginas de AEM permite crear experiencias de captura de datos sin problemas dentro de una página de Sites gracias a la potencia de los componentes de Forms adaptable, que incluyen comportamiento dinámico, validaciones, integración de datos, generación de documentos de registro y automatización de procesos empresariales. También le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios, lo que mejora la experiencia general de creación y administración de formularios. Vamos a explorar algunas de estas características:

* **Versiones:** Las páginas de AEM Sites ofrecen [sólidas capacidades de versiones](/help/sites-authoring/working-with-page-versions.md), lo que le permite realizar un seguimiento y administrar diferentes versiones de los formularios. Esto le permite realizar cambios y mejoras en los formularios al tiempo que se mantiene la capacidad de restablecer versiones anteriores si es necesario. El control de versiones garantiza un enfoque controlado y organizado del desarrollo y la evolución de los formularios.
* **Segmentación (integración con Adobe Target):** Con las funcionalidades de segmentación de páginas de AEM Sites, también puede [personalizar la experiencia del formulario para diferentes públicos](/help/sites-administering/target.md). Al aprovechar los segmentos de usuario y los criterios de segmentación, puede adaptar el contenido, diseño o comportamiento del formulario a grupos específicos de usuarios. Esto le permite proporcionar una experiencia de formulario personalizada y relevante, lo que aumenta las tasas de participación y conversión.
* **Traducción: Integración perfecta de** AEM Sites [con los servicios de traducción](/help/sites-administering/translation.md), lo que le permite traducir fácilmente formularios a varios idiomas. Esta función simplifica el proceso de localización y garantiza que los formularios sean accesibles para un público global. Puede administrar las traducciones de forma eficaz dentro de los proyectos de traducción de AEM, lo que reduce el tiempo y el esfuerzo necesarios para la asistencia con formularios multilingües. Consulte la sección de consideraciones para obtener más información sobre la traducción.
* **Administración de varios sitios y Live Copy:** AEM Sites proporciona [Funciones de administración de varios sitios y Live Copy](/help/sites-administering/msm.md) sólidas, lo que permite crear y administrar varios sitios web en un único entorno. Ahora esta función le permite reutilizar formularios en diferentes sitios, lo que garantiza la consistencia y reduce los esfuerzos de duplicación. Con el control y la administración centralizados, puede mantener y actualizar de forma eficaz los formularios en varios sitios web.
* **Temáticas:** Las páginas de AEM Sites proporcionan un marco de trabajo para diseñar y mantener estilos visuales coherentes en varias páginas web. Estas definen colores, fuentes, hojas de estilo y otros elementos visuales que contribuyen a la apariencia general del sitio web. [Puede utilizar las temáticas diseñadas para una página de AEM Sites para un formulario adaptable, lo que ahorra tiempo y esfuerzo](/help/sites-authoring/style-system.md).
* **Etiquetado:** las páginas de AEM Sites le permiten [asignar etiquetas a una página, a un recurso o a otro contenido](/help/sites-authoring/tags.md). Las etiquetas son palabras clave o etiquetas de metadatos que proporcionan una forma de categorizar y organizar el contenido en función de criterios específicos. Puede asignar una o más etiquetas a páginas, recursos o a cualquier otro elemento de contenido dentro de AEM para mejorar la búsqueda y la clasificación de los archivos.
* **Bloquear y desbloquear contenido:** AEM Sites permite a los usuarios [controlar el acceso y las modificaciones de páginas](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) dentro del entorno de AEM Sites. Cuando una página está bloqueada, significa que está protegida contra cambios o ediciones no autorizados por parte de otros usuarios. Solo el usuario que ha bloqueado el contenido o un administrador designado pueden desbloquearlo para permitir modificaciones.


## Varias opciones para agregar un formulario adaptable en el editor de páginas de AEM

Puede aprovechar al máximo esta función utilizando las siguientes opciones:

* **[Agregar un formulario adaptable personalizado a una página de AEM Sites:](#create-an-adaptive-form-in-sites-editor)** Cree un formulario nuevo desde cero y adáptelo específicamente a sus necesidades y preferencias de diseño.

* **[Agregar un formulario adaptable personalizado a un fragmento de experiencia:](#create-an-adaptive-form-in-experience-fragment)** Amplíe el alcance de los formularios añadiéndolos a los fragmentos de experiencias de la AEM, lo que permite una reutilización perfecta en varias páginas o sitios.

* **[Convertir un formulario adaptable en fragmento de experiencia:](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** Convertir un formulario adaptable agregado a una página de AEM Sites en un fragmento de experiencia para reutilizar el formulario en varias páginas de AEM Sites.

* **Cree y agregue formularios basados en plantillas aprobadas a una página de AEM Sites:** Aproveche las plantillas aprobadas previamente para crear rápidamente formularios que se ajusten a las directrices de promoción de la marca y a los estándares de diseño de su organización. La opción solo está disponible para los formularios adaptables creados con el Editor de formularios adaptables o Formularios adaptables: componente incrustado.

* **Añada formularios existentes a una página de AEM Sites:** integre fácilmente formularios que ya haya creado en sus sitios web, lo que permite a los visitantes interactuar con ellos directamente. La opción solo está disponible para los formularios adaptables creados con el Editor de formularios adaptables o Formularios adaptables: componente incrustado.

* **Agregar varios formularios a una página de AEM Sites o a un fragmento de experiencia:**  Agregue varios formularios a una página para proporcionar varias opciones a los usuarios en función de sus preferencias y requisitos. Pueden ser una combinación de formularios nuevos desde cero y formularios existentes.

## Consideraciones {#consideration}

* Cuando se utiliza el Contenedor de formularios adaptables para crear o añadir un formulario, los formularios pasan por un proceso de traducción y localización a través del flujo de traducción de AEM Sites. Para cada idioma, se genera una copia independiente (copia de idioma) de la página de Sites y de los formularios correspondientes y, cuando un autor de contenido modifica una regla en un formulario de la página principal, se deben realizar los mismos cambios en todas las copias de idioma del formulario. El Contenedor de formularios adaptables también permite utilizar varias funcionalidades de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

* Cuando se crea o se añade un formulario utilizando el Formulario adaptable: componente incrustado, los formularios pasan por un proceso de traducción y localización utilizando el flujo de traducción de AEM Forms. En este caso, se mantiene un único formulario y se hace referencia a él en todas las copias de idioma de las páginas de Sites. El Formulario adaptable: componente incrustado no proporciona acceso a varias funcionalidades de páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.


## Antes de comenzar {#before-you-start}

+++  Habilitar los componentes principales de formularios adaptables para su entorno

Asegúrese de que los [componentes principales de Forms adaptable estén habilitados para su entorno](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=en).

+++ 

+++  Añada bibliotecas de cliente de formularios adaptables a los componentes de la página de AEM Sites y de la página de Fragmento de experiencia. 

Para habilitar la funcionalidad completa del componente Contenedor de formularios adaptables, añada las bibliotecas de cliente Customheaderlibs y Customfooterlibs a la página de AEM Sites mediante la canalización de implementación. Para añadir las bibliotecas:

1. Inicie sesión en la instancia de autor de AEM y abra CRX DE. La dirección URL predeterminada de una instancia de autor que se ejecuta localmente es `http://localhost:4502/crx/de`.

1. Abra el archivo `/apps/[your-sites-project]/components/page/customheaderlibs.html` y añada el siguiente código al archivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Abra el archivo `/apps/[your-sites-project]/components/page/customfooterlibs.html` y añada el siguiente código al archivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Abra el archivo `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` y añada el siguiente código al archivo:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Abra el archivo `/apps/[your-sites-project]/components/customfooterlibs.html` y añada el siguiente código al archivo:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Repita los pasos anteriores para todas las instancias de autor y publicación del entorno.

+++ 

+++ Habilitar el contenedor de formularios adaptables

Para habilitar el [!UICONTROL Contenedor de formularios adaptables] en la política de la plantilla, siga los siguientes pasos:

1. Abra la página de AEM Sites o el Fragmento de experiencia para editarlos. Para abrir la página para editarla, selecciónela y haga clic en Editar.
1. Abra la plantilla de su página Sites o Fragmento de experiencia. Para abrir la plantilla, vaya a [!UICONTROL Información de página] ![Información de página](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar plantilla]. Se abre la plantilla correspondiente en el editor de plantillas.
1. En la vista Estructura, haga clic en el icono **[!UICONTROL Política]** ![Política](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) en la barra de menús. En la lista **[!UICONTROL Componentes permitidos]**, seleccione la casilla de verificación **[!UICONTROL Contenedor de formularios adaptables]** en **[Nombre de proyecto de tipo de archivo de AEM] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Creación de un formulario adaptable {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puede crear un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño, directamente en una página de AEM Sites o en un Fragmento de experiencia. Para formularios de un solo uso, se recomienda la creación directa en una página de AEM Sites, mientras que los Fragmentos de experiencias son ideales para formularios que deben reutilizarse en varias páginas del sitio web.

* [Creación de un formulario en una página de AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creación de un formulario en un Fragmento de experiencia](#create-an-adaptive-form-in-experience-fragment)
* [Conversión de un formulario adaptable en una página de AEM Sites a un Fragmento de experiencia](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Creación de un formulario en una página de AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puede utilizar el componente Contenedor de formularios adaptables en el Editor de páginas de AEM para crear un formulario personalizado. El componente permite crear un formulario arrastrando y soltando los componentes del formulario. Los componentes de formulario se basan en los componentes principales. Puede personalizarlos fácilmente según los requisitos de su organización.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para crear un formulario adaptable en una página de Sites:

1. Abra la página de AEM Sites en el modo de edición.
1. Arrastre y suelte el componente **[!UICONTROL Contenedor de formularios adaptables]** del explorador de componentes a la página de Sites. Se creará un espacio en la página para el formulario. Puede utilizar el modo de diseño para cambiar el tamaño del espacio del contenedor.
1. Arrastre y suelte los componentes principales del formulario adaptable en el espacio del contenedor para crear el formulario.
1. Agregue el botón Enviar.

A continuación, [establezca la acción de envío](#configure-submit-action-for-form) y las propiedades avanzadas.

### Creación de un formulario en un Fragmento de experiencia {#create-an-adaptive-form-in-experience-fragment}

Puede ampliar el alcance de los formularios añadiéndolos a los Fragmentos de experiencias de AEM, lo que permite una reutilización perfecta en varias páginas o sitios. Por ejemplo, puede incluir un formulario de suscripción a una newsletter dentro de un Fragmento de experiencia. Esto le permite reutilizar con comodida el fragmento en varias páginas del sitio web, lo que elimina la necesidad de volver a crear el formulario repetidamente. Las actualizaciones o modificaciones realizadas en el formulario de suscripción a la newsletter dentro del Fragmento de experiencia se propagan automáticamente a todas las páginas donde se utiliza. Esto optimiza el proceso y garantiza una experiencia de usuario perfecta a la vez que simplifica la administración de sus formularios del sitio web.

Para crear un formulario adaptable en un Fragmento de experiencia:

1. Abra un Fragmento de experiencia.
1. Arrastre y suelte el componente de **[!UICONTROL Contenedor de formularios adaptables]** del Explorador de componentes al Fragmento de experiencia.
1. Arrastre y suelte los componentes principales del formulario adaptable en el espacio contenedor del fragmento de experiencia para crear el formulario.
1. Agregue el botón Enviar.

A continuación, [establezca la acción de envío](#configure-submit-action-for-form) y las propiedades avanzadas.

### Conversión de un formulario adaptable en una página de AEM Sites en un fragmento de experiencia {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Puede convertir un formulario adaptable existente en un editor de páginas de Sites a un Fragmento de experiencia para reutilizar el formulario en varias páginas o sitios.

Para convertir un formulario adaptable en una página de AEM Sites en un Fragmento de experiencia:

1. Abra la página de AEM Sites que contiene el formulario adaptable (en el componente Contenedor de formularios adaptables) en el modo Editar.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. En la barra de menús, seleccione el ![Icono Convertir para la variación del fragmento de experiencia](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) Icono Convertir en variación de Fragmento de experiencia.
   ![Convertir formulario de la página de Sites en un fragmento de experiencia](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Aparece un cuadro de diálogo para convertir el contenedor del formulario adaptable a un nuevo fragmento de experiencia o agregar a un fragmento de experiencia existente
1. En el cuadro de diálogo Convertir en variación de Fragmento de experiencia, establezca los valores de las siguientes opciones:

   * **Acción:** seleccione crear un Fragmento de experiencia o añadir a un Fragmento de experiencia existente.
   * **Ruta principal:** especifique la ruta de la carpeta en la que se alojará el Fragmento de experiencia. La opción solo está disponible para crear un Fragmento de experiencia.
   * **Plantilla:** especifique la ruta de la plantilla del Fragmento de experiencia. Si no tiene una plantilla de fragmento de experiencia, [créela](/help/sites-developing/experience-fragments.md). La opción solo está disponible para agregar formularios adaptables a un Fragmento de experiencia existente.
   * **Título del fragmento:** Especifique el título del Fragmento de experiencia. El título identifica de forma exclusiva un Fragmento de experiencia


## Configurar la acción de envío para el formulario {#configure-submit-action-for-form}

Una acción de envío permite elegir el destino de los datos capturados mediante un formulario adaptable. Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Los formularios adaptables incluyen algunas acciones de envío listas para usar. También puede ampliar las acciones de envío predeterminadas para crear su propia acción de envío personalizada. Para configurar una acción de envío para el formulario:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar las acciones de envío.
   ![Contenedor de formularios adaptables](/help/forms/using/assets/adaptive-forms-container.png)
1. Seleccione y configure una acción de envío según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](configuring-submit-actions.md)


## Configurar un esquema o un modelo de datos de formulario para un formulario {#configure-schema-or-data-model-for-form}

Puede utilizar el modelo de datos de formulario para conectar un formulario a una fuente de datos para enviar y recibir datos en función de las acciones del usuario. También puede conectar un formulario a un esquema JSON para recibir los datos enviados en un formato predefinido.

Antes de conectar un formulario a un esquema o a un modelo de datos de formulario

* [Crear un esquema JSON y cargarlo en su entorno](adaptive-form-json-schema-form-model.md)
* [Crear modelo de datos de formulario](create-form-data-models.md)

Para configurar un esquema JSON o un modelo de datos de formulario para su formulario:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Contenedor de formularios adaptables del modelo de datos de formulario](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. Seleccione y configure un esquema JSON o un modelo de datos de formulario según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](configuring-submit-actions.md).

   * Al seleccionar la variable **[!UICONTROL Modelo de formulario]**, utilice la opción **[!UICONTROL Seleccionar modelo de datos de formulario]** para seleccionar un modelo de datos de formulario preconfigurado.
   * Al seleccionar la opción **[!UICONTROL Esquema]**, utilice la opción **[!UICONTROL Esquema]** para seleccionar un esquema JSON para el formulario.

1. Haga clic en **[!UICONTROL Listo]**.

## Configurar un servicio de rellenado previo para un formulario {#configure-prefill-service-for-form}

Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Puede hacer lo siguiente:

* [Crear un servicio de rellenado previo personalizado](prepopulate-adaptive-form-fields.md)
* [Usar servicio de prerrellenado del modelo de datos de formulario](#fdm-prefill-service)

### Servicio de rellenado previo de modelo de datos de formulario {#fdm-prefill-service}

Puede utilizar el servicio de rellenado previo del modelo de datos de formulario para rellenar previamente los campos de un formulario mediante el uso de un modelo de datos de formulario configurado. El servicio de rellenado previo del modelo de datos de formulario utiliza el [Obtener servicio del modelo de datos de formulario configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar datos. Para utilizar el servicio de rellenado previo del modelo de datos de formulario de un formulario adaptable, haga lo siguiente:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Editor de páginas de aem sites del fdm del servicio de relleno previo](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. Seleccionar modelo de datos de formulario. Abra la pestaña **[!UICONTROL Básico]**. En el servicio de relleno previo, seleccione **[!UICONTROL Servicio de relleno previo de borrador del portal Forms]**.
1. Haga clic en **[!UICONTROL Listo]**.

## Redirigir al usuario a un nuevo usuario al enviar el formulario o mostrar un mensaje de agradecimiento

Al enviar un formulario, puede redirigir al usuario a otra página web o a un mensaje. Para redirigir al usuario o configurar el mensaje de agradecimiento:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/using/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
1. Abra la pestaña **[!UICONTROL Envío]**.

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione la opción Redirigir a URL y proporcione una dirección absoluta, una URL de redireccionamiento o una ruta relativa de una página de AEM Sites.

   * Para configurar un mensaje personalizado o de agradecimiento, por ejemplo, al enviar, seleccione la opción Mostrar mensaje y proporcione un mensaje en el cuadro Contenido del mensaje. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

## Ver también {#see-also}

* [Crear un formulario adaptable independiente basado en componentes principales](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Creación de estilos o temáticas para los formularios](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
