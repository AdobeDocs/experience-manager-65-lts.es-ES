---
title: Componentes para fragmentos de contenido
description: Los fragmentos de contenido de Adobe Experience Manager (AEM) se crean y administran como recursos independientes de la página
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
exl-id: 2196af09-8053-49c3-8a23-caf03bb9a39d
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Componentes para fragmentos de contenido{#components-for-content-fragments}

## Componentes para la creación de fragmentos {#components-for-fragment-authoring}

>[!CAUTION]
>
>No se recomienda ampliar ni cambiar los componentes reales utilizados en el editor de fragmentos, ya que siguen estando sujetos a cambios.

Consulte la [API de administración de fragmentos de contenido - del lado del cliente](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componentes para la creación de páginas {#components-for-page-authoring}

>[!CAUTION]
>
>Ahora se recomienda el [componente principal de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es). Consulte [Desarrollar componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) para obtener más información.
>
>Esta sección detalla el componente original enviado para su uso con fragmentos de contenido (**Fragmento de contenido** en el grupo **General**).

>[!NOTE]
>
>Consulte también [Fragmentos de contenido que configuran componentes para procesamiento](/help/sites-developing/content-fragments-config-components-rendering.md) para obtener más información.

Los fragmentos de contenido de Adobe Experience Manager (AEM) se [crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md). Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). [Al crear páginas de contenido, puede usar estos fragmentos y sus variaciones](/help/sites-authoring/content-fragments.md). También puede usar un recurso de fragmento de contenido existente al [arrastrarlo desde el explorador de recursos a la página](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (como para otros componentes basados en recursos, como el componente de base Imagen). El componente de fragmento de contenido predeterminado muestra solo un [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del fragmento de contenido al que se hace referencia. Con el cuadro de diálogo de componentes puede definir el [elemento, variación y rango de párrafos de fragmento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que desea mostrar en la página.

>[!NOTE]
>
>Este componente Fragmento de contenido se introdujo en AEM 6.2 como una versión mejorada del componente Artículo, que ha quedado obsoleto.

>[!NOTE]
>
>Los fragmentos de contenido no son compatibles con la IU clásica.

### Definición {#definition}

El componente **Fragmento de contenido** se usa para contener una referencia a un recurso de fragmento de contenido (recursos de texto mejorados de forma efectiva). El tipo de recurso para el fragmento de contenido es el siguiente:

`dam/cfm/components/contentfragment/contentfragment`

La referencia se define en la propiedad:

`fileReference`

Solo el editor de la IU táctil admite completamente los componentes de fragmento de contenido, que incluyen la biblioteca de cliente:

`cq.authoring.editor.plugin.cfm`

Esta biblioteca agrega funciones, específicas de los fragmentos de contenido, al editor. Por ejemplo, está disponible la compatibilidad con la capacidad de agregar y configurar fragmentos de contenido en la página, la capacidad de buscar recursos de fragmentos de contenido en el explorador de recursos y contenido asociado en el panel lateral.

### Contenido intermedio {#in-between-content}

El componente **Fragmento de contenido** t le permite soltar componentes adicionales entre los diferentes párrafos del [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) mostrado. Básicamente, el elemento mostrado está compuesto por diferentes párrafos (cada párrafo está marcado por un retorno de carro). Entre cada uno de esos párrafos, puede insertar contenido mediante otros componentes.

Desde un punto de vista técnico, cada párrafo del elemento mostrado reside en su propio parsys y cada componente que se añade entre los párrafos se inserta (bajo el capó) en el parsys.

En otras palabras, si la instancia del componente de fragmento de contenido está compuesta por tres párrafos, el componente tiene tres parsys diferentes en el repositorio. Todo el contenido intermedio que se añade al fragmento de contenido se encuentra realmente dentro de estos parsys.

En el repositorio, el contenido intermedio se almacena en relación con su posición dentro de la estructura general del párrafo, es decir, no se adjunta al contenido real del párrafo.

Para ilustrar esto, tenga en cuenta lo siguiente:

* Instancia de un fragmento de contenido compuesto por tres párrafos
* Y que parte del contenido ya se ha insertado después del segundo párrafo

   * Esto significa que el contenido se almacena en el segundo parsys.

Básicamente, si la estructura de párrafos de esta instancia cambia (al cambiar la variación, el elemento o el intervalo de párrafos mostrados), podría afectar al contenido intermedio que se muestra cuando se reproduce el contenido del fragmento de contenido:

* Se edita y se añade otro párrafo antes del segundo párrafo:

   * El contenido intermedio se muestra después del párrafo recién creado (el segundo parsys ahora contiene el párrafo recién creado).

* Se edita y se elimina el segundo párrafo:

   * El contenido intermedio se muestra después del párrafo que antes era el tercero (el segundo parsys ahora contiene el tercer párrafo anterior).

* Está configurado para que solo se muestre el primer párrafo:

   * No se muestra el contenido intermedio (el segundo parsys ya no se procesa debido a la nueva configuración).

### Personalización del componente Fragmento de contenido {#customizing-the-content-fragment-component}

Para utilizar el componente de fragmento de contenido listo para usar como modelo para la extensión, debe respetar el siguiente contrato:

* Reutilice el script de procesamiento HTL y su POJO asociado para poder ver cómo se implementa la función de contenido intermedio.
* Reutilizar el nodo de fragmento de contenido: `cq:editConfig`

   * Los oyentes `afterinsert`/ `afteredit`/ `afterdelete` se usan para almacenar en déclencheur eventos JS. Estos eventos se controlan en la biblioteca de cliente `cq.authoring.editor.plugin.cfm` para mostrar el contenido asociado en el panel lateral.
   * Los `cq:dropTargets` están configurados para admitir el arrastre de recursos de fragmentos de contenido.
   * `cq:inplaceEditing` está configurado para admitir la creación de un fragmento de contenido en el editor de páginas. El editor local de fragmentos está definido en la biblioteca de cliente `cq.authoring.editor.plugin.cfm` y permite abrir mediante un vínculo rápido el [elemento/variación](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) actual en el [editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md).

### Reescritura de recursos antes del procesamiento {#asset-rewriting-before-rendering}

La administración de fragmentos de contenido utiliza un proceso de renderización interna para generar la salida final de HTML para una página. Esto lo utiliza internamente el componente Fragmento de contenido, pero también el proceso en segundo plano que actualiza los fragmentos a los que se hace referencia en las páginas que hacen referencia.

Internamente, la reescritura de Sling se utiliza para esa renderización. La configuración respectiva se encuentra en `/libs/dam/config/rewriter/cfm` y se puede ajustar, si es necesario. Consulte [Reescritor de Apache Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) para obtener más información.

>[!CAUTION]
>
>Si ajusta/superpone la configuración de la reescritura:
>
>* `/libs/dam/config/rewriter/cfm`
>
>Entonces `serializerType` **debe** actualizarse a:
>
>* `serializerType="html5-serializer"`

La configuración predeterminada utiliza los siguientes transformadores:

* `transformer-cfm-payloadfilter` - para recuperar la parte `body` ( `<body>...</body>`) solo del HTML del fragmento

* `transformer-cfm-parfilter`: elimina los párrafos no deseados si se especifica un intervalo de párrafos (como se puede hacer con el componente Fragmento de contenido)
* `transformer-cfm-assetprocessor`: se utiliza internamente para recuperar una lista de los recursos incrustados en el fragmento

El proceso de representación se expone a través de [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) y los componentes personalizados lo pueden utilizar (por ejemplo), si es necesario.
