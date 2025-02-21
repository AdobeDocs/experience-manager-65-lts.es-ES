---
title: Personalizar plantillas para componentes del portal de Forms
description: Descubra cómo la interfaz de usuario de AEM Forms permite a los usuarios agregar metadatos a los formularios. Los metadatos personalizados mejoran la experiencia del usuario en la búsqueda y la lista de formularios.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
feature: Forms Portal
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 78%

---

# Personalizar plantillas para componentes del portal de Forms{#customizing-templates-for-forms-portal-components}

## Requisitos previos {#prerequisites}

[Administrar metadatos de formulario](../../forms/using/manage-form-metadata.md)

Conocimientos prácticos de HTML y CSS

## Información general {#overview}

La interfaz de usuario de AEM Forms permite agregar metadatos a cualquier formulario. Los metadatos personalizados pueden mejorar la experiencia del usuario al enumerar y buscar formularios de su organización.

El portal de formularios permite utilizar metadatos personalizados en listas de formularios. Al crear plantillas personalizadas para los recursos, puede modificar su diseño y utilizar metadatos personalizados con el conjunto de estilos CSS.

Haga lo siguiente para poder crear una plantilla personalizada para varios componentes del portal de Forms.

## Crear una plantilla personalizada {#creating-a-nbsp-custom-template}

1. Cree un nodo sling:Folder en /apps

   Agregue la propiedad “fpContentType”. Especifique los valores adecuados para la propiedad en función del componente para el que defina la plantilla personalizada.

   * Componente Buscar y listar: “/libs/fd/fp/formTemplate”
   * Componente Borradores y envíos:

      * Sección Borradores: /libs/fd/fp/draftsTemplate
      * Sección Envíos: /libs/fd/fp/submissionsTemplate

   * Componente de vínculo: /libs/fd/fp/linkTemplate

   Agregue un título que desee que se muestre al seleccionar plantillas de diseño.

   >[!NOTE]
   >
   >El título puede ser diferente del nombre de nodo de sling:Folder que ha creado.

   La siguiente imagen muestra la configuración del componente Buscar y listar.
   ![Crear una sling:Folder](assets/1.png)

1. Cree un archivo template.html en esta carpeta para que pueda servir como plantilla personalizada.
1. Escriba la plantilla personalizada y utilice metadatos personalizados como se describe a continuación.

## Ejemplo práctico {#working-example}

A continuación se muestra una implementación de ejemplo de una plantilla personalizada en la que el portal de formularios adquiere un diseño de tarjeta de gobierno personalizado de Geometrixx para el componente Buscar y listar.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## Especificaciones técnicas de las plantillas personalizadas {#technical-specifications-for-custom-templates}

Una plantilla personalizada para cualquier componente del portal de formularios incluye entradas repetibles y no repetibles. Las entradas repetibles son entidades básicas para las listas. Ejemplos de entradas repetibles son los componentes Buscar y listar, Borradores y envíos y Vínculo.

Forms Portal proporciona una sintaxis para que los marcadores de posición muestren metadatos personalizados/predeterminados. Los marcadores de posición se rellenan después de mostrar los resultados de los formularios, borradores o envíos.

Para incluir una entrada repetible, configure el valor del atributo **data-repeatable** a **true**.

*En el ejemplo analizado, hay dos elementos Div presentes en la parte superior de la plantilla personalizada. El primero, con la clase CSS “__FP_boxes-container” funciona como un elemento de contenedor para los formularios que se enumeran. El segundo, con la clase CSS “__FP_boxes” es una plantilla para las entidades básicas, en este caso un formulario. El atributo **data-repeatable**presente en el elemento Div tiene el valor **true**.*

Cada marcador de posición tiene un conjunto exclusivo de metadatos predeterminados. Para mostrar metadatos personalizados en un lugar determinado del formulario, agregue la **propiedad ${metadata_prop}**, en el lugar.

*En el ejemplo, la propiedad metadata se usa en varias instancias. Por ejemplo, se utiliza en **descripción**,**nombre**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**y **ruta**de la manera prescrita.*

## Metadatos predeterminados {#out-of-the-box-metadata}

Varios componentes del portal de Forms proporcionan conjuntos exclusivos de metadatos predeterminados que puede utilizar para incluirlos en la lista.

### Componente Buscar y listar {#search-amp-lister-component}

* **Título:** título del formulario
* **nombre**: nombre del formulario (la mayoría es el mismo que el título)
* **descripción**: descripción del formulario
* **formUrl**: URL para procesar el formulario como HTML
* **pdfUrl**: URL para procesar el formulario como PDF
* **assetType**: tipo de recurso. Los valores válidos incluyen **Form**, **PDF Form**, **Print Form** y **Adaptive Form**

* **htmlStyle** y **pdfStyle**: estilo de visualización de los iconos HTML y PDF respectivamente utilizados para el procesamiento. Los valores válidos son “**__FP_display_none**” o en blanco.

>[!NOTE]
>
>Recuerde utilizar la clase __FP_display_none en la hoja de estilo personalizada.

* **downloadUrl**: URL para descargar un recurso.

Compatibilidad con la localización, clasificación y uso de propiedades de configuración en la interfaz de usuario (solo Buscar y listar):

1. **Compatibilidad con localización**: para localizar texto estático, use el atributo `${localize-YOUR_TEXT}` y haga que el valor localizado esté disponible, si no existe todavía.
   *En el ejemplo analizado, los atributos `${localize-Apply}` y `${localize-Download}` se utilizan para localizar el texto Aplicar y Descargar.*

1. **Compatibilidad con la ordenación**: haga clic en el elemento HTML para ordenar los resultados de la búsqueda. Para implementar la ordenación en un diseño de tabla, agregue el atributo &quot;data-sortKey&quot; en el encabezado de tabla concreto. Además, agregue su valor como metadatos para los que desea ordenar.
Por ejemplo, para el encabezado “Título” en la vista de cuadrícula, el valor del encabezado “data-sortKey” es “título”. Haga clic en el encabezado para poder ordenar los valores de una columna en particular.

1. **Usar las propiedades de configuración**: el componente Buscar y listar tiene varias configuraciones que puede utilizar en la interfaz de usuario. Por ejemplo, para mostrar el texto de información del objeto HTML guardado a través del cuadro de diálogo de edición, utilice el atributo `${config-htmlLinkText}`. **Del mismo modo, para el texto de información del objeto PDF, utilice el atributo** `${config-pdfLinkText}`.

### Componente Vínculo {#link-component}

* **Título:** título del formulario
* **formUrl**: URL para procesar el formulario como HTML
* **destino**: atributo de destino del vínculo. Los valores válidos son “_blank” y ”_self”.
* **linkText**: pie de ilustración del vínculo

### Componente Borradores y envíos {#drafts-amp-submissions-component}

* **Ruta**: ruta del nodo de metadatos de borradores/envíos. Utilícelo con la extensión .HTML como URL para poder abrir un borrador o un envío.
* **contextPath**: ruta de contexto de la instancia de AEM
* **firstLetter**: primera letra (mayúscula) del título del formulario adaptable, que se guardó como borrador o se envió.
* **formName**: título del formulario adaptable, que se guardó como borrador o se envió.
* **DraftID**: ID del borrador que aparece en la lista (utilícelo solamente en la plantilla de la sección Borrador).
* **submitID**: ID del envío que aparece en la lista (utilícelo solamente en la plantilla de la sección Envío).
* **estado**: estado del formulario enviado. (Se utiliza solo en la plantilla de la sección Envío).
* **descripción**: descripción del formulario adaptable asociado al borrador o al envío.
* **diffTime**: diferencia entre la hora actual y la última acción de guardado del borrador. Alternativamente, la diferencia entre la hora actual y la última acción enviada para la presentación.
* **iconClass**: la clase CSS utilizada para mostrar la primera letra del borrador/envío. El portal de formularios incluye las siguientes clases, que proporcionan distintos fondos de colores.
* **propietario**: usuario que ha creado el borrador/envío.
* **Hoy**: Fecha de creación del borrador o del envío en formato `DD:MM:YYYY`.
* **TimeNow**: hora de creación del borrador o del envío en formato de 24 horas `HH:MM:SS`

*Nota:*

1. Para la opción de eliminación de la sección Borradores del componente Borradores y envíos, asigne a la clase CSS el nombre “__FP_deleteDraft”. Además, incluya el atributo “DraftID” con el valor **${draftID}**, que es el ID borrador del borrador correspondiente.

1. Al crear vínculos para abrir borradores y envíos, puede especificar **${path}.html** como el valor del atributo **href** para la etiqueta de anclaje.

![Nodo Borradores y envíos](assets/raw-image-with-index.png)

**A**. Elemento Contenedor

**B.** Metadatos de “ruta” con una jerarquía fija para obtener la miniatura almacenada para cada formulario.

**C.** Atributo repetible de datos utilizado en la sección de la plantilla para cada formulario

**D.** Localice la cadena &quot;Aplicar&quot;

**E.** Usar la propiedad de configuración pdfLinkText

**F.** Usar los metadatos “pdfUrl”

## Sugerencias, trucos y problemas conocidos {#tips-tricks-and-known-issues}

1. No utilice comillas simples (&#39;) en ninguna plantilla personalizada.
1. Para los metadatos personalizados, almacene esta propiedad solamente en el nodo **jcr:content/metadata**. Si lo almacena en cualquier otro lugar, Forms Portal no podrá mostrar los metadatos.
1. Asegúrese de que el nombre de cualquier metadato personalizado o existente no incluya dos puntos ( : ). Si es así, no se podrá mostrar en la interfaz de usuario.
1. **data-repeatable** no tiene ningún significado para un componente **Vínculo**. Adobe recomienda evitar utilizar esta propiedad en la plantilla para un componente Vínculo.

## Artículos relacionados

* [Habilitar componentes del portal de Forms](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de Forms](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de Forms](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
