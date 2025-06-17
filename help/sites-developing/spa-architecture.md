---
title: Desarrollo de SPA para Adobe Experience Manager
description: Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una SPA para Adobe Experience Manager (AEM) y ofrece una visión general de la arquitectura de AEM con respecto a las SPA que se deben tener en cuenta al implementar una SPA desarrollada en AEM.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 8670d700-6ccd-4809-b719-8580d6fb2cf8
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 5%

---


# Desarrollo de SPA para AEM{#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de Adobe Experience Manager (AEM) sin problemas para un sitio creado con esos marcos.

Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una SPA para AEM y ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

{{ue-over-spa}}

## Principios de desarrollo de SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. Si como desarrollador front-end sigue estas prácticas recomendadas generales y algunos principios específicos de AEM, su SPA funcionará con [AEM y sus capacidades de creación de contenido](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidad](/help/sites-developing/spa-architecture.md#portability) -** Al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](/help/sites-developing/spa-architecture.md#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing) -** La SPA es responsable del enrutamiento y AEM lo escucha y recupera en función de él. Cualquier enrutamiento también debe ser dinámico.

Si tiene en cuenta estos principios al desarrollar la SPA, será lo más flexible y seguro posible en el futuro, al tiempo que habilita todas las funcionalidades de creación de AEM admitidas.

Si no necesita admitir las características de creación de AEM, puede que tenga que considerar un [modelo de diseño de SPA](/help/sites-developing/spa-architecture.md#spa-design-models) diferente.

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

El SPA resultante debe crearse con componentes altamente portátiles y reutilizables.

### Estructura del sitio de unidades AEM {#aem-drives-site-structure}

El desarrollador front-end debe considerarse responsable de crear una biblioteca de componentes de SPA utilizados para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. [Sin embargo, AEM, en todo momento, posee la estructura del sitio.](/help/sites-developing/spa-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

La SPA solo debe depender de la renderización dinámica del contenido. Esta es la expectativa predeterminada en la que AEM recupera y procesa todos los elementos secundarios de la estructura de contenido.

Cualquier representación explícita que apunte a contenido específico se considera una representación estática y, aunque se admite, no es compatible con las funciones de creación de contenido de AEM. Esto también va en contra del principio de [portabilidad](/help/sites-developing/spa-architecture.md#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. En AEM, [la SPA siempre debe ser propietaria del enrutamiento](/help/sites-developing/spa-routing.md), y AEM lo escucha y recupera contenido basado en él.

Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](/help/sites-developing/spa-architecture.md#portability) y limita al autor al no ser compatible con las características de creación de contenido de AEM. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador front-end que lo haga.

## Arquetipo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Modelos de diseño SPA {#spa-design-models}

Si se siguen los [principios del desarrollo de SPA en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), su SPA funcionará con todas las funciones de creación de contenido de AEM admitidas.

Sin embargo, puede haber casos en los que esto no sea del todo necesario. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se usa como CMS sin encabezado sin usar el marco de trabajo <a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDK.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden utilizar la experiencia de creación de contenido de AEM.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador front-end utiliza el marco de trabajo de SDK del Editor SPA, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de AEM.</p> <p>El código corre el riesgo de no ser ni portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través del JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto utiliza completamente la SDK del Editor de SPA, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación con la experiencia de creación de contenido de AEM.<br /> </p> <p>La SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegado a AEM.</p> <p>El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos son compatibles con AEM, solo implementando el tercero (y, por lo tanto, siguiendo los principios de desarrollo de [SPA recomendados en AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) los autores de contenido pueden interactuar con el contenido del SPA en AEM y editarlo como están acostumbrados.

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Por lo general, si su SPA sigue los [Principios de desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), su SPA funcionará en AEM y se podrá editar con el Editor de SPA de AEM.

Siga estos pasos para preparar su SPA existente para trabajar con AEM.

1. **Haga que sus componentes JS sean modulares.**

   Permitir que se representen en cualquier orden, posición y tamaño.
1. **Use los contenedores proporcionados por SDK de Adobe para colocar los componentes en la pantalla.**

   AEM proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. **Cree un componente de AEM para cada componente JS.**

   Los componentes de AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La tarea principal al involucrar a un desarrollador front-end para crear una SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una SPA para AEM.

1. **Aceptar componentes y su modelo JSON**

   Los desarrolladores de front-end y de back-end de AEM deben acordar qué componentes son necesarios y un modelo, de modo que haya una coincidencia individualizada entre los componentes de SPA y los componentes de back-end.

   Los componentes de AEM siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En los componentes de React, acceda al modelo a través de`this.props.cqModel`**

   Una vez acordados los componentes y configurado el modelo JSON, el desarrollador front-end puede desarrollar la SPA y simplemente acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el método `render()` del componente**

   El desarrollador front-end implementa el método `render()` como crea conveniente y puede utilizar los campos de la propiedad `cqModel`. Esto genera el DOM y los fragmentos de HTML que se insertan en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso de AEM mediante`MapTo()`**

   La asignación almacena clases de componentes y el componente `Container` proporcionado la utiliza internamente para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina `EditConfig` del componente como parámetro para`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Extender la clase `Container` proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use la API HTML5 `History`.**

   Cuando `ModelRouter` está habilitado, al llamar a las funciones `pushState` y `replaceState` se déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM-Agnostic {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes de React y Angular no necesitan nada específico de Adobe o AEM.

* Todo lo que se encuentra dentro del componente JavaScript no depende de AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente de MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

El asistente de `MapTo` es el &quot;pegado&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML a HTML que procesa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` y la creación de SPA para AEM en general, consulte la guía de introducción para el marco de trabajo elegido.

* [Introducción a SPA en AEM: React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a SPA en AEM: Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitectura de AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo encaja el desarrollo de SPA en esta arquitectura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Entorno de compilación**

  Aquí es donde se extrae el origen de la fuente de la aplicación SPA y del origen del componente.

   * El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de SPA.
   * Esa biblioteca la toma Maven y la implementa el complemento de compilación de Maven junto con el componente al autor de AEM.

* **Autor de AEM**

  El contenido se crea en el autor de AEM, incluidas las SPA de creación.

  Cuando se edita una SPA con el Editor de SPA en el entorno de creación:

   1. La SPA solicita la HTML externa.
   1. Se carga el CSS.
   1. Se carga la JavaScript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación SPA, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluidos los atributos `cq-data`.
   1. Estos atributos de `cq-data` permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **Publicación de AEM**

  Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de la aplicación SPA, clientlibs y componentes, se publican para uso público.

* **Dispatcher / CDN**

  Dispatcher sirve como capa de almacenamiento en caché de AEM para los visitantes del sitio.

   * Las solicitudes se procesan de forma similar a como se encuentran en el Autor de AEM; sin embargo, no hay ninguna solicitud de información de página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>Dentro de AEM, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM solo aloja los artefactos compilados de la aplicación SPA.

## Siguientes pasos {#next-steps}

Para obtener una descripción general de cómo está estructurado un SPA simple en AEM y cómo funciona, consulte la guía de introducción para [React](/help/sites-developing/spa-getting-started-react.md) y [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el [Tutorial de introducción al Editor de SPA de AEM - WKND Events](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es).

Para obtener más información sobre la asignación de modelos dinámicos a componentes y cómo funciona en las SPA de AEM, consulte el artículo [Asignación de modelos dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un módulo que no sea React o Angular, o simplemente desea profundizar en cómo funciona SDK de SPA para AEM, consulte el artículo [Modelo SPA](/help/sites-developing/spa-blueprint.md).
