---
title: 'Tutorial: Publicar un formulario adaptable'
description: Publique el formulario adaptable como una página AEM, incrústuelo en una página de AEM Sites o incruste el formulario adaptable en una página web externa.
contentOwner: khsingh
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 90%

---

# Tutorial: Publicar un formulario adaptable {#tutorial-publish-your-adaptive-form}

![Imagen-héroe](do-not-localize/13-publish-your-adaptive-form-small.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](Https://helpx.adobe.com/es/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Se recomienda seguir la serie en orden cronológico para comprender, realizar y mostrar el caso de uso del tutorial completo.

Una vez que el formulario adaptable esté listo, puede publicarlo para que los usuarios finales puedan acceder a él. Los usuarios finales pueden abrir el formulario publicado en cualquier dispositivo y explorador de Internet. Cuando se publica un formulario adaptable, el formulario y el contenido relacionado se copian de una instancia de autor de AEM a una instancia de publicación. El formulario está disponible para el usuario final a través de la instancia de publicación.

Puede utilizar los siguientes métodos para publicar un formulario adaptable:

* [Publicar el formulario adaptable como una página de AEM](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [Incrustar el formulario adaptable en una página de AEM Sites](#embed-the-adaptive-form-in-an-aem-sites-page)
* [Incrustar el formulario adaptable en una página web externa (una página web que no pertenezca a AEM y esté alojada fuera de este)](../../forms/using/publish-your-adaptive-form.md)

## Antes de comenzar {#before-you-start}

* **[Configuración de una instancia de publicación de AEM Forms](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**: la instancia de publicación es una instancia pública de AEM [!DNL Forms] se ejecuta en el modo Publicación. En entornos de producción, la instancia de publicación está fuera del cortafuegos de la organización.
* **[Configurar la replicación y la replicación inversa](https://helpx.adobe.com/es/experience-manager/6-3/help/sites-deploying/replication.html)**: la replicación copia el contenido de la instancia de autor en una instancia de publicación y devuelve los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) desde la instancia de publicación a la instancia de autor.

## Publicar el formulario adaptable como una página de AEM {#publish-the-adaptive-form-as-an-aem-page}

Cuando el formulario adaptable se publica como una página de AEM, toda la página web contiene únicamente un formulario publicado. Puede utilizar la URL del formulario adaptable para vincularlo desde otra página web. Para publicar el formulario adaptable **Formulario-actualizar-agregar-dirección-envío** como una página de AEM:

1. Inicie sesión en la instancia de autor de AEM [!DNL Forms] y busque el formulario adaptable Formulario-actualizar-agregar-dirección-envío en la interfaz de usuario de AEM [!DNL Forms].
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. Seleccione el formulario adaptable Formulario-actualizar-agregar-dirección-envío y seleccione **[!UICONTROL Publicar]**. Se muestra un cuadro de diálogo que contiene recursos relacionados con el formulario adaptable. Seleccione **[!UICONTROL Publicar]**. El formulario adaptable se publica y aparece un cuadro de diálogo con un mensaje de éxito.
1. Abra el formulario en la instancia de publicación. El formulario está disponible para que el usuario final lo rellene y lo envíe.
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## Incrustar el formulario adaptable en una página de AEM Sites {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] permite a los desarrolladores de formularios incrustar fácilmente formularios adaptables en una página de AEM [!DNL Sites]. El formulario adaptable incrustado es completamente funcional, y los usuarios pueden rellenarlo y enviarlo sin abandonar la página. Esto permite al usuario mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

AEM [!DNL Forms] proporciona un componente, el Contenedor de AEM [!DNL Forms], para incrustar un formulario adaptable en una página de AEM [!DNL Sites]. De forma predeterminada, el componente no está visible en el contenedor de AEM [!DNL Sites]. Siga estos pasos para habilitar el componente Contenedor de AEM [!DNL Forms] e incrustar el formulario adaptable en una página de AEM [!DNL Sites]:

1. Cree y abra una página en el sitio de We.Retail para editarla. Por ejemplo, [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). El formulario adaptable se incrusta en la página de [!DNL Sites].

   También puede incrustar el formulario adaptable en una página de We.Retail de [!DNL Site's] existente; por ejemplo, la página ABOUT US [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). Esto le permite ahorrar tiempo a la hora de crear una página. Los pasos siguientes utilizan la página recién creada.

   El sitio de We.Retail se proporciona junto con AEM. Si no ha instalado el sitio de We.Retail, consulte [Implementación de referencia de We.Retail](https://helpx.adobe.com/es/experience-manager/6-3/help/sites-developing/we-retail.html) para instalarlo.

1. Seleccione la información de página ![properties](assets/properties.png) y seleccione la opción **[!UICONTROL Editar plantilla]** en la página de sitio de We.Retail recién creada. La plantilla de la página se abre en una nueva pestaña del explorador.
1. Seleccione dentro del cuadro **[!UICONTROL contenedor de diseño]** y seleccione ![feedmanagement](assets/feedmanagement.png). En la ficha **[!UICONTROL Componentes permitidos]**, expanda el acordeón **[!UICONTROL General]**, seleccione la opción **[!UICONTROL Formulario de AEM]** y seleccione ![save_icon](assets/save_icon.svg). El componente Contenedor de AEM [!DNL Forms]está habilitado para la página.

1. Abra la pestaña del explorador que contiene la página de AEM [!DNL Sites] que abrió en el paso 1. Seleccione el cuadro **[!UICONTROL Arrastrar componentes aquí]** y seleccione **+.** En el cuadro **[!UICONTROL Insertar nuevo componente]**, seleccione **[!UICONTROL Formulario de AEM]**. El componente **[!UICONTROL Contenedor de AEM Forms]** se añade a la página.
1. Seleccione el componente **[!UICONTROL contenedor de AEM Forms]** y seleccione ![configure-icon](assets/configure-icon.svg). Aparece un cuadro de diálogo con las propiedades del contenedor de AEM [!DNL Forms]. En el campo **[!UICONTROL Ruta del recurso]**, busque y seleccione el formulario adaptable Formulario-actualizar-agregar-dirección-envío. Seleccione ![icono_guardar](assets/save_icon.svg). El formulario adaptable se incrusta en la página.
1. Publique el formulario adaptable y la página de [!DNL Sites]. Tenga en cuenta lo siguiente:

   * Si publica la página de AEM [!DNL Sites] por primera vez y esta incluye un formulario incrustado, publique la página de [!DNL Sites] y el formulario incrustado.
   * Si ha modificado únicamente el formulario incrustado en una página de Sites ya publicada, publique el formulario original, y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada contiene una referencia al formulario, y no es necesario que vuelva a publicarla.
   * Si modifica la página de [!DNL Sites] y el formulario incrustado, vuelva a publicar la página de [!DNL Sites] y el formulario.

     ![incrustado-en-aem-sites](assets/embed-in-aem-sites.png)

   Formulario Cambio de la dirección de envío y facturación añadido a una página de AEM [!DNL Sites].

## Incrustar el formulario adaptable en una página web externa {#embed-the-adaptive-form-in-an-external-webpage}

Puede incrustar un formulario adaptable en una página web externa (una página web que no pertenezca a AEM y que esté alojada fuera de este) insertando unas líneas de JavaScript en la página web externa. El código JavaScript envía una solicitud HTTP al servidor de AEM [!DNL Forms] para el formulario adaptable y los recursos relacionados, y agrega el formulario adaptable a la página web. Para ver los pasos detallados, consulte [Incrustar formulario adaptable en una página web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).
