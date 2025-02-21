---
title: 'Opcional: cómo crear aplicaciones de una sola página (SPA) con Adobe Experience Manager'
description: En esta continuación opcional del Recorrido para desarrolladores de Adobe Experience Manager (AEM) sin encabezado, aprenderá cómo AEM puede combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables mediante el marco de trabajo del Editor de SPA de AEM.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer
source-git-commit: 71b7f46de3619605c8a5aedc496cfb85ed582f59
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 76%

---

# Creación de aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional del [Recorrido para desarrolladores sin encabezado de AEM](overview.md), aprenderá cómo Adobe Experience Manager (AEM) puede combinar la entrega sin encabezado con las funciones tradicionales de CMS full-stack y cómo puede crear SPA editables utilizando el marco de trabajo del Editor de SPA de AEM, así como integrar SPA externas, habilitando las capacidades de edición según sea necesario.

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [Recorrido para desarrolladores de AEM sin encabezado](overview.md) y comprender los conceptos básicos de la entrega de contenido sin encabezado en AEM, incluido lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.

Por lo tanto, ya ha puesto en marcha su primer proyecto de AEM sin encabezado o tiene los conocimientos necesarios para hacerlo. Enhorabuena.

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que recuerde que en [Introducción](getting-started.md#integration-levels) hubo una breve discusión sobre cómo AEM no solo admite la entrega sin encabezado y los modelos full-stack tradicionales, sino que también admite modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin encabezado, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

Este artículo se basa en sus conocimientos de AEM sin encabezado para explorar en profundidad cómo puede crear sus propias aplicaciones de una sola página (SPA) que se pueden editar en AEM. De este modo, puede crear contenido y enviarlo sin encabezado a una SPA, pero esa SPA sigue siendo editable en AEM.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco de trabajo del editor de SPA de AEM. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender la función básica del editor de SPA.
* Conocer los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar las SPA externas en AEM.
* Comprender cómo se debe implementar o no el procesamiento en el lado del servidor.

## Condiciones y requisitos previos {#requirements-prerequisites}

Antes de empezar a trabajar con las SPA en AEM hay varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.
* No olvide revisar el documento [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md) para comprender los distintos niveles de integración de SPA posibles.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente (opcional, según el modelo de integración elegido).
* Tipo de archivo del proyecto AEM.

## ¿Qué es una SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas AJAX para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una carga de una sola página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizaciones de la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido de AEM.

## ¿Por qué una SPA? {#why-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, un SPA se convierte en una experiencia atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo funcionan los SPA.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona las SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. Como desarrollador front-end, si sigue estas prácticas recomendadas generales y algunos principios específicos de AEM, su SPA funcionará con AEM y sus funciones de creación de contenido.

* **Portabilidad**: al igual que con cualquier componente, los componentes de SPA deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **AEM impulsa la estructura del sitio**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **Procesamiento dinámico**: todo el procesamiento debe ser dinámico.
* **Enrutamiento dinámico**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona las SPA, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## El editor de SPA de AEM {#aem-spa-editor}

Los sitios creados con marcos de trabajo de las SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de las SPA dentro de AEM, se necesita una asignación entre la salida JSON de las SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

El soporte de las SPA en AEM introduce una capa delgada de JS que interactúa con el código JS de las SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de punto final de API de Servicios de contenido porque el contenido de las SPA debe cargarse mediante Servicios de contenido.

Para obtener una descripción completa del editor de SPA de AEM, consulte el apartado [recursos adicionales](#additional-resources) para obtener los vínculos a documentación más detallada.

## Adaptación de las SPA existentes {#existing-spas}

Si tiene una SPA existente, AEM permite integrarlo en AEM para que sea visible para los autores de contenido en el editor de AEM. Esto puede resultar útil para ver el contenido que están creando a través de fragmentos de contenido en el contexto de la aplicación final donde se consumirá.

Además, con tan solo unos pequeños cambios, puede habilitar una determinada capacidad de edición en la SPA externa dentro del editor de AEM.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer que una SPA externa se pueda editar en AEM, consulte la sección [recursos adicionales](#additional-resources) para obtener vínculos a documentación más detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propia SPA para AEM, revise los siguientes documentos:

* [Tutorial WKND de SPA](/help/sites-developing/spa-wknd.md)
* [Introducción a React](/help/sites-developing/spa-getting-started-react.md)
* [Introducción a Angular](/help/sites-developing/spa-getting-started-angular.md)

Si necesita adaptar una SPA existente para utilizarla en AEM, revise los documentos siguientes:

* [El componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/sites-developing/spa-edit-external.md)

Consulte los [recursos adicionales](#additional-resources) para profundizar en los temas de las SPA en AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md): una descripción de los diferentes modelos de entrega disponibles en AEM.
* [Introducción y tutorial de SPA.](/help/sites-developing/spa-walkthrough.md): una buena introducción a las SPA en AEM
* [Desarrollo de las SPA para AEM](/help/sites-developing/spa-architecture.md): directrices sobre cómo desarrollar las SPA para AEM
* [Información general del editor de SPA](/help/sites-developing/spa-overview.md): detalles del funcionamiento del editor de SPA.
* [Documentos de referencia de SPA](/help/sites-developing/spa-reference-materials.md): referencias de la API de JavaScript y vínculos a los proyectos de GitHub de SPA en AEM de código abierto
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): cómo crear fragmentos de contenido
* [Arquetipo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es): plantilla de Maven que crea un proyecto mínimo, basado en las prácticas recomendadas de Adobe Experience Manager (AEM) como punto de partida para su sitio web
