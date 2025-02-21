---
title: Crear una página de portal de formularios
description: El portal de formularios proporciona a los desarrolladores web componentes para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
feature: Forms Portal
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 94%

---

# Crear una página de portal de formularios{#creating-a-forms-portal-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=es) |
| AEM 6.5 | Este artículo |

Los componentes del portal de formularios permiten a los desarrolladores web crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM). Para obtener una descripción general rápida del portal de formularios, consulte [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md).

## Requisitos previos {#prerequisites}

Los componentes del portal de formularios no están disponibles para usarlos de forma predeterminada. Asegúrese de que las siguientes categorías de componentes del portal de formularios estén habilitadas según se describe en [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md).

**Servicios de documentos** Incluye los componentes Buscar y listar, Vínculo y Borradores y envíos.

**Predicados de servicios de documentos** Incluye componentes predicados de fecha, de texto completo, de propiedades y de etiquetas. Estos componentes se utilizan para configurar la búsqueda en el componente Buscar y listar.

Una vez que se habiliten en una página de AEM Sites, estas categorías de componentes estarán disponibles para usarlas en el explorador de componentes.

![Componentes del portal de AEM Forms en el explorador de componentes](assets/component-categories.png)

Categorías de componentes del portal de formularios

## Componente Buscar y listar {#search-amp-lister-component}

El componente Buscar y listar, disponible en la categoría de componente Servicios de documentos, se utiliza para enumerar formularios en una página e implementar la búsqueda en ellos. El componente incluye dos paneles:

* Panel de lista donde se muestran los formularios.
* Panel de búsqueda donde se agrega la funcionalidad de búsqueda.

Puede arrastrar y soltar el componente Buscar y listar de la categoría del componente Servicios de documentos en el explorador de componentes a la página. El componente, cuando se agrega, tiene un aspecto similar al siguiente.

![Componente Buscar y listar en una página](assets/fp-grid-viw.png)

Componente Buscar y listar en una página con diseño de cuadrícula

### Panel de lista {#list-pane}

El panel Lista es un área en la que se enumeran los formularios. El componente Buscar y listar proporciona varias opciones de configuración que puede utilizar para controlar la visualización de formularios en el panel Lista.

Para configurar el panel Lista, seleccione el componente Buscar y listar y luego seleccione ![settings_icon](assets/settings_icon.png). Se abrirá el cuadro de diálogo **[!UICONTROL Editar componente]**.

![Panel Lista en modo de edición](assets/edit-list.png)

Panel Lista en modo de edición

El cuadro de diálogo **Editar** incluye varias pestañas que proporcionan las opciones de configuración descritas en la siguiente tabla. Seleccione **Aceptar** para guardar la configuración cuando haya terminado.

<table>
 <tbody>
  <tr>
   <th>Pestaña</th>
   <th>Configuración</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Carpetas de recursos</strong></code></td>
   <td>Agregar elemento</td>
   <td>Configura las carpetas en las que los recursos se cargan mediante la interfaz de usuario de AEM Forms. De forma predeterminada, muestra todos los recursos cargados. Para obtener más información sobre la interfaz de usuario de AEM Forms, consulte <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introducción a la administración de formularios</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Mostrar</strong></code></p> </td>
   <td>Texto del título</td>
   <td>Título del componente Buscar y listar. El título predeterminado es <strong>Portal de Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Diseño de los recursos. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Deshabilitar búsqueda avanzada</td>
   <td>Cuando está habilitado, oculta el icono de búsqueda avanzada.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Deshabilitar búsqueda de texto</td>
   <td>Cuando está habilitada, oculta la barra de búsqueda de texto completo.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resultado</strong></code></td>
   <td>Número de resultados por página</td>
   <td>Configura el número máximo de formularios que desea mostrar en una página.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de resultados</td>
   <td><p>Configura el texto de los resultados (por ejemplo, 1-12 de 601 <strong>Resultados</strong>). El valor predeterminado es <strong>Resultados</strong>.</p> <p>Por ejemplo, si especifica <strong>Formularios </strong>en este campo y hay un total de 601 formularios, el texto resultante cambiará a 1-12 de 601 <strong>formularios.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de página</td>
   <td><p>Configura el texto de la página (por ejemplo, <strong>Página </strong>1 de 51). El valor predeterminado es <strong>Página</strong>.</p> <p>Por ejemplo, si especifica <strong>Formulario de solicitud </strong>en este campo y hay 51 páginas, el texto de la página cambiará a <strong>Formulario de solicitud </strong>1 de 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>De texto</td>
   <td><p>Reemplaza la palabra <strong>de</strong> con el texto especificado (Página 1 <strong>de </strong>51). El valor predeterminado es <strong>de</strong>.</p> <p>Por ejemplo, si especifica <strong>de las </strong>en este campo, el texto cambiará a Página 1 <strong>de las </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Vínculo de formulario</strong></code></td>
   <td>Tipo de procesamiento</td>
   <td>Controla la lista de formularios en función del tipo de procesamiento especificado. Las opciones disponibles son PDF y HTML. Por ejemplo, si selecciona solo HTML como tipo de procesamiento, los formularios PDF se filtrarán.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Perfil HTML</td>
   <td>Configura el perfil del HTML que se utiliza para el procesamiento. Todos los perfiles disponibles se enumeran en la lista desplegable.</td>
  </tr>
  <tr>
   <td> </td>
   <td>URL de envío</td>
   <td><p>Configura un servlet en el que se envían los datos del formulario.</p> <p><strong>Nota:</strong> <em>La dirección URL de envío de un formulario se puede especificar en varios lugares y su orden de prioridad es el siguiente:</em></p>
    <ol>
     <li><em>La dirección URL de envío incrustada en el formulario (en el botón Enviar) tiene la prioridad más alta.</em></li>
     <li><em>La dirección URL de envío que se menciona en la interfaz de usuario de AEM Forms tiene la segunda prioridad más alta.</em></li>
     <li><em>Enviar URL mencionada en el portal de formularios tiene la prioridad más baja.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Información del objeto Acción de procesamiento del HTML</td>
   <td>Configura el texto de la información del objeto, que se muestra al pasar el puntero por encima <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (el icono HTML5).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Información del objeto Acción de procesamiento del PDF</td>
   <td>Configura el texto de la información del objeto, que se muestra al pasar el puntero por encima <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (el icono PDF).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Estilo</strong></code></td>
   <td>Tipo de estilo</td>
   <td>Permite especificar <strong>Sin estilo, estilo predeterminado</strong> o <strong>estilo personalizado </strong>para enumerar los formularios.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si seleccionó Personalizado como tipo de estilo, busque para especificar la ruta al CSS personalizado y, de lo contrario, seleccione Predeterminado.</td>
  </tr>
 </tbody>
</table>

### Panel Buscar {#search-pane}

El panel Buscar permite agregar los componentes Predicado de fecha, Predicado de texto completo, Predicado de propiedades y Predicado de etiquetas de la categoría Predicados de servicios de documentos de la barra de tareas de AEM. Estos componentes implementan la funcionalidad de búsqueda para que los usuarios realicen búsquedas en los formularios enumerados.

**Sugerencia:** *Puede controlar la lista de formularios mostrados en el portal de formularios en función de criterios preestablecidos y ocultar la funcionalidad de búsqueda para los usuarios finales. Para controlar la lista de formularios, utilice los componentes de predicado para aplicar filtros de búsqueda. También puede especificar los valores de filtro predeterminados y deshabilitar la búsqueda desde la pestaña Mostrar del cuadro de diálogo Editar componente.*

![Panel de búsqueda con los predicados Fecha, Texto completo, Propiedades y Etiquetas](assets/search-with-predicates.png)

Panel de búsqueda con los predicados Fecha, Texto completo, Propiedades y Etiquetas

#### Predicado Fecha {#date-predicate}

Cuando se agrega el componente Predicado Fecha, permite buscar en los formularios enumerados que se modificaron durante una duración especificada.

Para configurar el componente Predicado Fecha:

1. Seleccione el componente y luego seleccione ![settings_icon](assets/settings_icon.png). Se abrirá el cuadro de diálogo Editar.
1. Especifique lo siguiente:

   * **Tipo:** la única opción disponible es **Fecha de la última modificación**

   * **Texto:** etiqueta o rótulo para el componente Predicado Fecha. El valor predeterminado es **Fecha de la última modificación.**

   * **Etiqueta Fecha de inicio:** etiqueta o rótulo del campo de la fecha de inicio
   * **Etiqueta Fecha de finalización:** etiqueta o rótulo para el campo de la fecha de finalización
   * **Ocultar:** aplicar el filtro de fecha predeterminado a los formularios de lista

1. Seleccionar **Aceptar**

#### Predicado de texto completo {#full-text-predicate}

El componente Predicado Texto completo implementa la búsqueda de texto completo en los datos del formulario, como el nombre y la descripción. Los usuarios pueden buscar cualquier cadena de texto para devolver formularios que contengan el texto de su nombre o descripción.

Para configurar el componente Predicado Texto completo, haga lo siguiente:

1. Seleccione el componente y luego seleccione ![settings_icon](assets/settings_icon.png). Se abrirá el cuadro de diálogo Editar.
1. Especifique el título en el campo **Título principal**.
1. Seleccionar **Aceptar**

#### Predicado Propiedades {#properties-predicate}

El componente Predicado Propiedades implementa la búsqueda de formularios en función de sus propiedades, como título, autor y descripción.

Para configurar el componente Predicado Propiedades, haga lo siguiente:

1. Seleccione el componente y luego seleccione ![settings_icon](assets/settings_icon.png). Se abrirá el cuadro de diálogo Editar.
1. En la pestaña General, especifique la etiqueta de búsqueda. El valor predeterminado es **Propiedades**

1. En la ficha Opciones, seleccione **Agregar elemento.**
1. Seleccione una propiedad de la lista desplegable y especifique una etiqueta de búsqueda para ella en el campo situado debajo de la lista desplegable.
1. Repita el paso 4 para agregar más propiedades. También puede especificar un valor de filtro predeterminado para enumerar formularios en función de los criterios especificados y ocultar la propiedad para que la busquen los usuarios finales. Seleccione la casilla Ocultar de una propiedad y especifique el valor de filtro predeterminado.
Por ejemplo, si desea mostrar formularios que contengan “Viajar” en sus títulos, seleccione Ocultar junto a la propiedad Título. Además, especifique Viajar en el cuadro de texto con valor de filtro predeterminado.

1. Seleccionar **Aceptar**

#### Predicado Etiquetas {#tags-predicate}

El componente Predicado Etiquetas implementa la búsqueda de formularios en función de las etiquetas definidas en Forms Manager.

Para configurar el componente Predicado Etiquetas:

1. Seleccione el componente y luego seleccione ![settings_icon](assets/settings_icon.png). Se abrirá el cuadro de diálogo Editar.
1. Seleccione el botón de flecha hacia abajo situado junto al campo Etiquetas.
1. Seleccione las etiquetas adecuadas
1. Seleccionar **Aceptar**

Las etiquetas seleccionadas aparecerán en el panel Buscar junto con las casillas de verificación para seleccionarlas. Ahora los usuarios pueden limitar la búsqueda en función de las etiquetas.

## Enumerar formularios en una página {#list-forms-on-a-page-br}

Para enumerar formularios en una página, agregue el componente **[!UICONTROL Buscar y listar]** a la página y configure el **[!UICONTROL Panel Lista]**. Para permitir que los usuarios finales busquen formularios con fecha, texto y etiquetas, agregue un componente **[!UICONTROL Panel Buscar]**.

Para vincular un formulario desde cualquier lugar de la página, utilice el componente Vínculo. Para obtener más información sobre el componente de vínculo, consulte [Incrustar un componente Vínculo en una página](../../forms/using/embedding-link-component-page.md).

Para enumerar los formularios que están en estado de borrador y los que ya se han enviado, utilice el componente **[!UICONTROL Borradores y envíos]**. Para obtener más información, consulte [Personalizar el componente Borradores y envíos](../../forms/using/draft-submission-component.md).

## Compatibilidad con dispositivos móviles {#mobile-device-friendliness}

El componente Buscar y listar del portal de formularios es compatible con dispositivos móviles y se adapta a ellos. Las tres vistas predeterminadas: Cuadrícula, Tarjeta, Presentaciones de panel se adaptan según el dispositivo en el que se abra el sitio, siempre que la página web también se adapte. El simple hecho es que Buscar y listar es solo un componente y no controla el estilo de nivel de página.

La siguiente imagen muestra el componente Buscar y listar cuando se abre en un dispositivo móvil:

![Captura de pantalla del componente Buscar y listar](assets/search_lister.png)

Componente Buscar y listar

## Personalizar una página del portal de formularios {#customizing-a-forms-portal-page-br}

Puede personalizar una página del portal de formularios para que tenga un aspecto distinto. También puede agregar metadatos para mejorar la experiencia de búsqueda, cambiar el diseño de la página y agregar estilos CSS personalizados. Para obtener más información, consulte [Personalizar plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md).

La interfaz de usuario de AEM Forms permite agregar metadatos personalizados a los formularios. Los metadatos personalizados son útiles para ofrecer a los usuarios finales la experiencia de buscar y listar formularios. Para obtener más información sobre los metadatos personalizados, consulte [Personalizar plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md).

De forma predeterminada, el portal de formularios proporciona acciones de procesamiento. Puede personalizar el portal de formularios para agregar más acciones. Para obtener información detallada, consulte [Agregar acciones personalizadas a elementos de lista de formularios](../../forms/using/add-custom-action-form-lister.md)

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
