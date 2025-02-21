---
title: Trabajar con fragmentos de contenido
description: Descubra cómo los fragmentos de contenido en Adobe Experience Manager (AEM) le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas, lo que resulta ideal para una entrega sin encabezado.
feature: Content Fragments
role: User
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 69%

---

# Trabajar con fragmentos de contenido {#working-with-content-fragments}

Con Adobe Experience Manager (AEM), los fragmentos de contenido le permiten diseñar, crear, depurar y [publicar contenido independiente de cualquier página](/help/sites-authoring/content-fragments.md). Permiten preparar contenido listo para usar en varias ubicaciones/en varios canales, lo que resulta ideal para una entrega sin encabezado.

Los fragmentos de contenido incluyen contenido estructurado:

* Se basan en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md), que predefine una estructura para el fragmento resultante.
* La estructura puede variar entre lo siguiente:
   * Básico
      * Por ejemplo, un campo de texto de varias líneas.
      * Se utiliza para preparar contenido directo para su uso en la creación de páginas.
   * Complejo
      * Una combinación de muchos campos de diferentes tipos de datos, incluidos texto, número, booleano, datos y tiempo, entre otros.
      * Se utiliza para preparar contenido más estructurado para la creación de páginas o para su entrega a la aplicación.
   * Anidado
      * Los tipos de datos de referencia disponibles le permiten anidar el contenido.
      * Tiende a utilizarse para su entrega a la aplicación.

Los fragmentos de contenido también se pueden entregar en formato JSON, utilizando las capacidades de exportación del Modelo Sling (JSON) de los componentes principales de AEM. Esta forma de entrega:

* permite utilizar el componente para administrar qué elementos enviar de un fragmento.
* permite la entrega por lotes, añadiendo varios componentes principales de fragmento de contenido en la página que se utiliza para la entrega de API.

Esta y las siguientes páginas tratan sobre las tareas para crear, configurar, mantener y utilizar sus fragmentos de contenido:

* [Habilitación de la funcionalidad de fragmento de contenidos para la instancia](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-models.md): habilitando, creando y definiendo sus modelos
* [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md): cree sus fragmentos de contenido; a continuación, edite, publique y haga referencias
* [Variaciones, creación de contenido de fragmentos](/help/assets/content-fragments/content-fragments-variations.md): cree el contenido del fragmento y variaciones del principal
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md): uso de la sintaxis de markdown para el fragmento
* [Uso de contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md): añadir contenido asociado
* [Metadatos, propiedades del fragmento](/help/assets/content-fragments/content-fragments-metadata.md): visualización y edición de las propiedades del fragmento
* Use [Fragmentos de contenido, junto con GraphQL, para entregar contenido](/help/assets/content-fragments/content-fragments-graphql.md) para su uso en aplicaciones. Para ayudarle con esto, puede obtener una vista previa de [salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Estas páginas se pueden leer con:
>
>* [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md).
>* [Personalizar y ampliar fragmentos de contenido](/help/sites-developing/customizing-content-fragments.md)
>* [Fragmentos de contenido Configurar componentes para procesamiento](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/assets-api-content-fragments.md)
>* [API de GraphQL de AEM para su uso con fragmentos de contenido](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)

El número de canales de comunicación aumenta de forma anual. Normalmente, los canales hacen referencia al mecanismo de entrega, ya sea como los siguientes:

* Canal físico; por ejemplo, escritorio o móvil.
* Forma de entrega en un canal físico; por ejemplo, la “página de detalles del producto”, la “página de categoría del producto” para escritorio o la “web móvil” o la “aplicación móvil” para móvil.

Sin embargo, probablemente no desee utilizar el mismo contenido para todos los canales y debe optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Pensar en cómo llegar a las audiencias de destino de forma eficaz en todos los canales.
* Crear y administrar contenido editorial neutro para el canal.
* Creargrupos de contenido para una amplia gama de canales.
* Diseñar variaciones de contenido para canales específicos.
* Agregar imágenes al texto insertando recursos (fragmentos de medios mixtos).
* Cree contenido anidado para poder reflejar la complejidad de sus datos.

Estos fragmentos de contenido se pueden ensamblar para ofrecer experiencias en varios canales.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-authoring/experience-fragments.md)** son funciones distintas de AEM:
>
>* **Los fragmentos de contenido** son contenido editorial que puede utilizarse para acceder a datos estructurados, como textos, números y fechas, entre otros. Son contenidos puros, con definición y estructura, pero sin diseño visual o adicional.
>
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web. 
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.
>
>Para obtener más información, consulte [Explicación de los fragmentos de contenido y de experiencias en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments?lang=es).

>[!NOTE]
>
>Antes de AEM 6.3, los fragmentos de contenido se creaban con el uso de plantillas en lugar de modelos. Las plantillas ya no están disponibles para crear fragmentos, pero todos los fragmentos creados con una plantilla de este tipo siguen siendo compatibles.

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

La entrega se ejecuta en formato JSON utilizando el exportador de JSON.

Los fragmentos de contenido de AEM se pueden usar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener varios tipos de contenido; incluido texto, datos numéricos, booleanos, fecha y hora, etc.

Junto con las capacidades de exportación de JSON de los componentes principales de AEM, este contenido estructurado se puede utilizar para entregar contenido de AEM a canales que no sean páginas de AEM.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## Tipo de contenido {#content-type}

Los fragmentos de contenido son lo siguiente:

* Se almacenan como **Recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la consola **Assets**.
   * Se crean y editan en el editor de fragmentos de contenido.

* Utilizado en el editor de páginas [con el componente Fragmento de contenido](/help/sites-authoring/content-fragments.md) (componente de referencia):

   * El componente **Fragmento de contenido** está disponible para los autores de páginas. Les permite hacer referencia y entregar el fragmento de contenido requerido en formato HTML o JSON.

* Son accesibles mediante la [API de AEM GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

Los fragmentos de contenido son una estructura de contenido que:

* No tiene diseño (es posible aplicar algo de formato de texto en el modo Texto enriquecido).
* Tener una o más [partes constitutivas](#constituent-parts-of-a-content-fragment).
* Puede [contener imágenes o estar conectada a ellas](#fragments-with-visual-assets).
* Puede usar [contenido intermedio](#in-between-content-when-page-authoring-with-content-fragments) cuando está referenciada en una página.
* Es independiente del mecanismo de entrega (es decir, página, canal).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para que los autores tengan un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Assets se puede utilizar con un fragmento de contenido de varias formas, cada una con sus propias ventajas:

* **Insertan recursos** en un fragmento (fragmentos de medios mixtos)

   * Son parte del fragmento (consulte [Partes constitutivas de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Definen la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) en el editor de fragmentos para obtener más información.

  >[!NOTE]
  >
  >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se agrega el fragmento a una página, estos recursos se mueven en relación con ese párrafo al agregarse contenido intermedio.

* **Contenido asociado**

   * Están conectados a un fragmento; pero no una parte fija de este (consulte [Partes constitutivas de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Permiten cierta flexibilidad de posicionamiento.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte [Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el **explorador de Assets** del editor de páginas

   * Permiten flexibilidad total para la selección de un recurso.
   * Permiten cierta flexibilidad de posicionamiento.
   * No proporcionan el concepto de aprobarse para un fragmento específico.

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### Partes constitutivas de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los activos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que tienen contenido.
   * Utiliza un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de varios tipos de datos.

* **Párrafos de fragmento**

   * Bloques de texto (a menudo multilínea) que se delimitan como entidades individuales.

   * En los modos [Texto enriquecido](/help/assets/content-fragments/content-fragments-variations.md#rich-text) y [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un párrafo se puede formatear como un encabezado, en cuyo caso, ese párrafo y el siguiente se unirán como una sola unidad.

   * Habilite el control de contenido durante la creación de páginas.

* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y usados como contenido interno de un fragmento.
   * Están incrustados en el sistema de párrafos del fragmento.
   * Se les puede dar formato cuando el [fragmento se utiliza/referencia en una página](/help/sites-authoring/content-fragments.md).
   * Solo se pueden agregar, eliminar o mover dentro de un fragmento con el editor de fragmentos. Estas acciones no se pueden llevar a cabo en el editor de páginas.
   * Solo se pueden agregar, eliminar o mover dentro de un fragmento con el [formato de texto enriquecido en el editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Solo se puede añadir a elementos de texto multilínea (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).

     >[!CAUTION]
     >
     >Los recursos se pueden eliminar (de forma involuntaria) de un fragmento cambiando al texto sin formato.

     >[!NOTE]
     >
     >Los recursos también se pueden añadir como [contenido adicional (intermedio)](/help/sites-authoring/content-fragments.md#using-associated-content) al utilizar un fragmento en una página, usando contenido asociado o recursos del explorador Recursos.

* **Contenido asociado**

   * Es contenido externo a un fragmento, pero con relevancia editorial para él. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para su uso con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos están [asociados a fragmentos mediante colecciones](/help/assets/content-fragments/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos emplear cuando esté creando la página.

      * Las colecciones se pueden asociar a fragmentos como contenido predeterminado, o por parte de los autores durante la creación de fragmentos.
      * Las [Colecciones de recursos (DAM)](/help/assets/manage-collections.md) son la base del contenido asociado de los fragmentos.
   * De forma opcional, también puede añadir el fragmento a una colección para ayudar en el seguimiento.

* **Metadatos de fragmento**

   * Utilice los [Esquemas de metadatos de recursos](/help/assets/metadata-schemas.md).
   * Las etiquetas se pueden crear cuando hace lo siguiente:

      * Crea el fragmento
      * O luego:

         * Al visualizar o editar las **Propiedades** del fragmento desde la consola
         * Editando los **Metadatos** en el editor de fragmentos

  >[!CAUTION]
  >
  >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Una parte del fragmento

      * Cada fragmento de contenido tiene una instancia de Principal.
      * El Principal no se puede eliminar.

   * Se puede acceder al Principal en el editor de fragmentos, en **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)**.
   * El Principal no es una variación como tal, sino la base de todas las variaciones.

* **Variaciones**

   * Representaciones de texto de fragmento específicas para un propósito editorial; pueden estar relacionadas con el canal, pero no es obligatorio, y también pueden ser para modificaciones locales específicas.
   * Se crean como copias de **Principal**, pero se pueden editar según sea necesario; el contenido se superpone entre las propias variaciones.
   * Se pueden definir durante la creación de fragmentos.
   * Almacenadas en el fragmento para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con el Principal si se actualizó el contenido principal.
   * Pueden [resumirse](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponibles en la pestaña [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el editor de páginas al trabajar con fragmentos de contenido.
* Se ha agregado [contenido adicional dentro del flujo de un fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o se ha hecho referencia a él en una página.
* Está disponible para su uso en el [editor de páginas al trabajar con fragmentos de contenido](/help/sites-authoring/content-fragments.md).
* El contenido intermedio se puede añadir a cualquier fragmento donde solo haya un elemento visible.
* Se puede utilizar contenido asociado, así como recursos o componentes del explorador adecuado.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear fragmentos de contenido, tenga en cuenta lo siguiente:

* **Modelo de contenido**

   * Están [habilitados mediante el Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Son [creados mediante Herramientas](/help/assets/content-fragments/content-fragments-models.md).
   * Requerido para [crear un fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones de modelos de contenido requieren un título y un elemento de datos; todo lo demás es opcional.
   * El modelo puede definir el contenido predeterminado, si corresponde.
   * Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.
   * Los cambios realizados en un modelo después de crear fragmentos de contenido dependientes pueden afectar a esos fragmentos de contenido.

Para utilizar los fragmentos de contenido para la creación de páginas, también necesita lo siguiente:

* **Componente Fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Requerido para [hacer referencia al fragmento en una página](/help/sites-authoring/content-fragments.md).
   * Responsable del diseño y entrega de un fragmento; es decir, de los canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y proporcionar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asocia automáticamente el componente requerido.

## Uso de ejemplo {#example-usage}

Un fragmento, con sus elementos y variaciones, se puede utilizar para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utiliza y dónde.
