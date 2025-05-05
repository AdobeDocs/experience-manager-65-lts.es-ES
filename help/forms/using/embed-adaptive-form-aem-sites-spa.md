---
title: Incrustar un formulario adaptable o una comunicación interactiva en una aplicación de una sola página de AEM Sites
description: Incrustar formularios adaptables o comunicaciones interactivas en páginas de AEM Sites. Los usuarios pueden rellenar y enviar formularios sin salir de la página de Sites.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 94%

---

# Incrustar un formulario adaptable o una comunicación interactiva en una aplicación de una sola página de AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar fácilmente formularios adaptables y comunicaciones interactivas en una aplicación de una sola página (SPA) de AEM Sites. El formulario adaptable y las comunicaciones interactivas incrustados son completamente funcionales y los usuarios pueden rellenarlos y enviarlos sin abandonar la página. Esto permite al usuario mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario o la comunicación interactiva.

En la aplicación de una sola página de AEM Sites, puede agregar un formulario adaptable o una comunicación interactiva mediante el [Componente Contenedor de la SPA de AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) [.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Es un componente de AEM Forms para la SPA de AEM Sites que puede agregar a su página de Sites.

Para obtener información sobre la incrustación de un formulario adaptable en una página de AEM Sites que no sea una SPA, consulte [Incrustar un formulario adaptable o una comunicación interactiva en una página de AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable o una comunicación interactiva en una SPA de AEM Sites con el componente Contenedor de la SPA de AEM Forms, asegúrese de que ha instalado:

* El kit de desarrollo Java SE 8 o posterior
* Apache Maven 3.3.1 o posterior
* La instancia de autor de AEM
* [El paquete de complementos de AEM Forms 6.4.2](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) en la instancia de autor

## Instalar el componente Contenedor de la SPA de AEM Forms  {#install-aem-forms-spa-container-component}

Ejecute los siguientes pasos para instalar el componente Contenedor de la SPA de AEM Forms:

1. [Clonar o descargar el componente de AEM Forms para la SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Instalar el componente de AEM Forms para la SPA. Las instrucciones para instalar el componente están disponibles en el archivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   El componente incluye un [componente React de muestra](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) que se puede utilizar para integrar el componente Contenedor de la SPA con un proyecto de la SPA basado en React.

1. [Clonar o descargar un proyecto de la SPA basado en React](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integrar el componente Contenedor de la SPA con un proyecto de la SPA basado en React al seguir las instrucciones disponibles en el archivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa—editor).

   Después de instalar el componente Contenedor de la SPA de AEM Forms e integrar el componente con un proyecto de la SPA basado en React, puede incrustar formularios adaptables y comunicaciones interactivas en la página de AEM Sites.

## Incrustar un formulario adaptable o una comunicación interactiva {#af-component}

Para incrustar un formulario adaptable o una comunicación interactiva con el componente Contenedor de la SPA de AEM Forms:

1. Abra la página de AEM Sites, en el modo de edición, en la que desee incrustar un formulario adaptable o comunicación interactiva.
1. Inserte el **formulario de AEM para la SPA** en la página mediante cualquiera de las siguientes opciones:

   * Seleccione el contenedor de diseño en la página de Sites, seleccione **+** y el componente **AEM Form for SPA**.

   * En el panel Explorador de componentes, arrastre y suelte el componente **Formulario de AEM para la SPA** en la página.
   * Busque un formulario adaptable o una comunicación interactiva en el explorador de recursos y arrástrelo y suéltelo en la página de Sites. Incrusta el formulario en un contenedor de componentes de la SPA de AEM Forms.

   >[!NOTE]
   >
   >No se admite procesar varios componentes del componente Contenedor de la SPA de AEM Forms en una misma página. Puede tener varios Contenedores de la SPA de AEM Forms en una página, pero solo se procesará uno a la vez. Asegúrese de que solo esté visible un componente en la página para evitar discrepancias.

1. Seleccione el componente Contenedor de la SPA de AEM Forms incrustado en la página de Sites y, a continuación, seleccione ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abrirá el cuadro de diálogo **Editar contenedor de la SPA de AEM Forms**.
1. En el cuadro de diálogo **Editar contenedor de AEM Forms**, especifique lo siguiente:

   * **Tipo de recurso:** seleccione el tipo de recurso que desea incrustar. Las opciones son **Formulario adaptable** y **Comunicación interactiva**

   * **Ruta del recurso**: busque y seleccione el formulario adaptable que desea incrustar. El campo se rellena automáticamente si se inserta un formulario adaptable o una comunicación interactiva mediante el explorador de recursos.
   * **Canal** (Solo comunicación interactiva): seleccione el tipo de canal interactivo que desea incrustar. Las opciones son **Canal web** y **Canal de impresión**.

   * **Temática**: seleccione una temática que defina el estilo de los componentes del formulario adaptable o de la comunicación interactiva. El estilo incluye propiedades de apariencia, como el estilo de fuente, el color de fondo, las dimensiones y la alineación.

1. Seleccione ![done_icon](assets/done_icon.png) para guardar la configuración. El formulario adaptable o la comunicación interactiva están incrustados en la página.

## Publicar formularios adaptables y comunicaciones interactivas incrustados {#publish-embedded-adaptive-form-and-interactive-communication}

Considere los siguientes escenarios para publicar un recurso incrustado (formulario adaptable o comunicación interactiva) en la página de AEM Sites:

* Si publica la página de AEM Sites por primera vez y esta incluye un formulario adaptable o una comunicación interactiva incrustados, publique la página de Sites y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable o la comunicación interactiva incrustados en una página de Sites ya publicada, publique el recurso original y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada incluye una referencia al recurso y no requiere que vuelva a publicar la página.
* Si ha modificado la página de Sites y el formulario adaptable integrado o la comunicación interactiva, vuelva a publicar la página y el recurso incrustado.

## Modificar el formulario adaptable y las comunicaciones interactivas integrados {#modify-embedded-adaptive-form-and-interactive-communication}

La página de AEM Sites mantiene una referencia al formulario adaptable y a la comunicación interactiva en el contenedor de AEM Forms. Por lo tanto, todas las configuraciones y propiedades configuradas en el formulario adaptable original, como la temática, los estilos y la acción de envío, se mantienen en el formulario adaptable o la comunicación interactiva incrustados.

Para modificar cualquier configuración o propiedad del formulario adaptable o de la comunicación interactiva incrustados, realice una de las siguientes acciones.

* Abra el formulario original en formularios adaptables o comunicaciones interactivas en sus respectivos editores y modifíquelos.
* Seleccione el formulario adaptable o la comunicación interactiva desde la página de Sites en el modo de edición y, a continuación, seleccione **Editar en una nueva ventana**. El formulario original se abrirá en el modo de edición.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de AEM Sites:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de los usuarios y los envíos de formularios incrustados son compatibles y visibles en las pestañas Borradores y Formularios enviados del portal de formularios.
* La acción de envío configurada en el formulario original se mantiene en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Puede utilizar la segmentación de experiencias en la página de Sites para presentar diferentes formularios basados en perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en esta aplicación. Sin embargo, no está disponible en el informe de análisis de Forms.
