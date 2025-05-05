---
title: Ruta hacia la primera experiencia para usar AEM sin encabezado
description: En esta parte del Recorrido para desarrolladores de AEM sin encabezado, comprenderá los pasos para aplicar su primera experiencia sin encabezado en AEM, incluidas las consideraciones de planificación, y también aprenderá las prácticas recomendadas para que su ruta sea lo más fluida posible.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 91%

---

# Ruta hacia la primera experiencia para usar AEM sin encabezado {#path-to-first-experience}

En esta parte del [Recorrido para desarrolladores de AEM sin encabezado](overview.md) comprenderá los pasos para aplicar su primera experiencia sin encabezado en AEM, incluidas las consideraciones de planificación, y también aprenderá las prácticas recomendadas para que su ruta sea lo más fluida posible.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin encabezado de AEM, [Introducción a AEM Headless](getting-started.md), ha aprendido la teoría básica de lo que es un CMS sin encabezado y ahora debería hacer lo siguiente:

* Comprender los conceptos básicos de las características de AEM sin encabezado.
* Conozca los requisitos previos para utilizar las características de AEM sin encabezado.
* Tener en cuenta los niveles de integración de AEM sin encabezado.
* Ser capaz de definir el proyecto en términos del ámbito.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto de AEM sin encabezado.

## Objetivo {#objective}

Este documento le ayudará a comprender los pasos necesarios para implementar su primer proyecto. Después de leerlo, debería poder hacer lo siguiente:

* Comprender las consideraciones de planificación importantes para diseñar su contenido.
* Comprender los pasos para implementar contenido sin encabezado en AEM.
* Conocer qué herramientas y configuraciones de AEM son necesarias.
* Conocer las prácticas recomendadas para que su recorrido sin encabezado sea fluido, mantenga la eficiencia de la generación de contenido y asegurarse de que el contenido se entregue rápidamente.

## Requisitos  {#requirements}

Antes de continuar con este documento, asegúrese de haber revisado el documento anterior en el Recorrido para desarrolladores de AEM Headless, [Introducción a AEM Headless](getting-started.md), y de haber hecho lo siguiente:

* Cumplir los requisitos enumerados.
* Tener en cuenta su propia definición de proyecto, en la que se incluya ámbito, funciones y rendimiento.

## Planificación para el éxito {#planning-for-success}

Para iniciar su primer proyecto de AEM sin encabezado debe asegurarse de que dispone de un modelo de contenido que admita la personalización y las actualizaciones que desee realizar en todos los canales.

Independientemente de AEM, también debe asegurarse de que tiene un entorno de desarrollo adecuado configurado si está generando una aplicación del lado del cliente para poder probar su cliente con llamadas de API a AEM.

### Definición de los modelos de contenido y las API {#defining-models}

Debe impulsar una experiencia coherente y administrar campañas personalizadas en todos los canales, de modo que pueda ver cada canal individual y superficie como su propia estructura de contenido distinta a la que enviar. Sin embargo, tener cada canal con su propio modelo de contenido será difícil de mantener.

En su lugar, debe tener en cuenta cómo se relaciona el contenido en diferentes superficies basándose en los principios de la organización, como jerarquías de productos y marcas, categorías de bienes o superficies o pasos en el recorrido del cliente. Por ejemplo, si tiene un conjunto de superficies que admiten una marca específica de automóviles que fabrica, puede que desee comenzar con un modelo de contenido para obtener información general que sea verdadera para todo el automóvil, y que luego tenga elementos más específicos, como el contenido necesario, desde cuando el automóvil comience a funcionar hasta que haya problemas con el servicio. Este modelo impondrá la herencia del contenido general de la marca del automóvil, al tiempo que permitirá cambios basados en el contexto específico necesario. También le ayudará a gestionar las actualizaciones de este contenido en el futuro, ya que puede aplicar un control basándose en las funciones como la de experto en marketing general o gestor de productos para toda la marca, frente a un autor responsable de la experiencia de “arrancar el automóvil”.

Una vez que tenga el modelo de contenido y una vista clara de los distintos clientes a los que debe mostrarse el contenido, debe asegurarse de que GraphQL o las API asociadas con el acceso a varios modelos de contenido se publiquen para todos los clientes que necesiten este contenido. Existen diferentes opciones para acceder a cierto contenido. Puede solicitar un contenido específico que sea estático y que permita el almacenamiento en caché del contenido y un rendimiento superior. También puede solicitar contenido que se genere dinámicamente y que requiera más procesamiento. Asegúrese de que los clientes aprovechan las API más eficientes para sus necesidades empresariales.

## Explicación de los entornos {#understanding-environments}

Dentro de AEM hay tres tipos de entornos: de desarrollo, ensayo y producción.

Los entornos de desarrollo (puede tener varios) son un lugar seguro para experimentar y probar ideas. Durante la fase inicial del proyecto, Adobe recomienda utilizar los entornos de desarrollo para probar variaciones de modelos de contenido y ver cuáles proporcionan la salida deseada para las superficies.

El entorno de ensayo de los proyectos sin encabezado se utiliza para validar las nuevas versiones de productos de AEM antes de que se implementen en la producción. Mantenga una lista actualizada de los modelos de contenido de producción y un subconjunto del contenido, de modo que pueda tener archivos JSON procesados para comparar si siguen proporcionando la misma salida, a medida que realiza cambios o que la versión de AEM introduce cambios.

La producción es donde los autores de contenido crean y administran su contenido real. Los cambios de modelo en la producción deben llevarse a cabo con cuidado y teniendo en cuenta la compatibilidad con versiones anteriores.

Durante la fase de desarrollo, se recomienda trabajar con un entorno de desarrollo y ensayo. Al pasar a las pruebas de rendimiento, tendrá que pasar al entorno de producción.

### Cooperación entre desarrolladores y autores de contenido {#cooperation}

Los desarrolladores necesitan un entorno de desarrollo de AEM configurado con los modelos de contenido rellenados. El desarrollador desarrolla el cliente que consumirá el contenido desde AEM sin in encabezado, ya que los autores de contenido siguen creándolo. Por eso las definiciones de API son muy importantes. Al aprovechar el SDK de AEM, el desarrollador puede crear un enlace de prueba para que se puedan crear pruebas de cliente y unidad a fin de garantizar que el cliente pueda procesar el contenido correctamente.

Los autores de contenido crean contenido en función de los modelos de contenido que se han definido en el entorno de ensayo. Con la herramienta de creación de fragmentos de contenido, el autor crea un nuevo fragmento de contenido o edita un fragmento de contenido existente. Antes de publicarlo, el autor puede obtener una previsualización del aspecto que tendrá para el cliente si trabaja con el desarrollador para impulsar el modelo de contenido al desarrollo o configurar un entorno de desarrollador solo para que los autores puedan obtener una vista previa del aspecto que tendría para el cliente.

## Configuración {#setup}

Antes de empezar con el contenido sin encabezado de AEM, debe asegurarse de que todas las funciones necesarias estén habilitadas. Esta sección describe lo que se requiere. Los pasos reales para realizar estos pasos se detallan más adelante en la sección [Recorrido para desarrolladores de AEM sin encabezado.](#overview.md)

Opcionalmente, también puede ver los [recursos adicionales](#additional-resources) para obtener más información sobre los temas individuales.

### Configuración {#configuration}

1. Habilitar los fragmentos de contenido
1. Habilitar GraphQL
1. Configurar el SDK sin encabezado

## Implementación de su primera aplicación de AEM sin encabezado

Se trata de información general de lo que necesita para implementar su primera aplicación de AEM sin encabezado para entregar su contenido. La forma de llevar a cabo estos pasos se describirá en detalle en partes posteriores del Recorrido para desarrolladores de contenido sin encabezado.

1. Crear los modelos de fragmentos de contenido
1. Crear fragmentos de contenido
1. Consultar contenido con GraphQL

## Prácticas recomendadas {#best-practices}

Un proyecto sin encabezado no solo es exitoso debido a la tecnología implementada, sino también debido a la buena planificación y gestión de los proyectos. A continuación se indican algunas prácticas recomendadas a tener en cuenta por los autores y desarrolladores de contenido al planificar el proyecto.

### Organización del contenido {#organizing-content}

* Haga su estructura tan compleja como sea necesario, pero manténgala lo más simple posible. Las estructuras de contenido más sencillas ayudan la gestión del contenido y a mejorar el rendimiento del sistema.
* Priorice la reutilización del contenido en su estrategia. Cree submodelos y referencias de contenido que se puedan reutilizar en varios modelos y canales de nivel superior.
* Haga que las estructuras de contenido sean lo más evidentes posible para que los autores de contenido puedan aprender y adaptarse rápidamente a las tareas de creación.
* Si tiene restricciones de acceso, intente alinear su modelo de contenido con los requisitos de acceso.
* Cuando tiene requisitos de acceso, deben dirigir su jerarquía de contenido. Agrupe el contenido que edita el mismo grupo de personas.
* Agrupe contenido similar en una carpeta.
   * Es más probable que un autor de contenido copie y pegue el contenido existente para crear contenido nuevo. Por lo tanto, hacer esto en la misma carpeta lo hace más eficiente.
   * AEM permite establecer los modelos permitidos por carpeta, de modo que el botón **Crear nuevo** solo muestra los modelos compatibles con esa ubicación.
* La creación del editor de fragmentos de contenido en línea de nuevos fragmentos de contenido se puede simplificar si la carpeta raíz está configurada en el modelo. Entonces el profesional no tiene que elegir una ubicación, solo necesita proporcionar un nombre para comenzar a editar la referencia nueva.

### Creación de contenido {#authoring}

* Para versiones específicas del canal de su contenido, considere la posibilidad de utilizar variaciones de fragmento de contenido. Las variaciones se sincronizan con el contenido principal para optimizar la administración de los cambios de contenido.
* Invite a otros productores de contenido a revisar el contenido y proporcionar comentarios con anotaciones y comentarios, que están disponibles en el editor de fragmentos de contenido y globalmente entre contenidos en Admin Console de fragmentos de contenido.
* Mantenga las cosas en movimiento con el menor número posible de elementos obligatorios. Los elementos obligatorios pueden bloquear el flujo de trabajo.

### Creación de contenido global {#localization}

* Establezca reglas de gestión para la traducción de contenido. Para reducir la carga del sistema, establezca la traducción como un proceso asincrónico que se pueda ejecutar en intervalos más largos. Espere un tiempo para el control de calidad de la localización y la corrección de errores.
* Aprovecha todas las funcionalidades proporcionadas por tu sistema de tecnología de traducción que puedes integrar con AEM, como la memoria de traducción.
* Comprenda si el contenido con medios enriquecidos, como imágenes y vídeos, necesita ser localizado.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Comprender las consideraciones de planificación importantes para diseñar su contenido.
* Comprender los pasos para implementar contenido sin encabezado en AEM.
* Conocer qué herramientas y configuraciones de AEM son necesarias.
* Conocer las prácticas recomendadas para que su recorrido sin encabezado sea fluido, mantenga la eficiencia de la generación de contenido y asegurarse de que el contenido se entregue rápidamente.

Queremos que a partir de estos conocimientos básicos comprenda plenamente el potencial y la flexibilidad de AEM sin encabezado, de modo que pueda aprovecharlos para sus propios proyectos. Para ello, tiene varias opciones.

### Elija su propia aventura {#choose-your-path}

Sea cual sea su estilo de aprendizaje, Adobe quiere que tenga éxito a la hora de empezar a trabajar con su proyecto AEM sin encabezado.

* Si prefiere continuar con la **información sobre los conceptos y las tecnologías sin encabezado de AEM**, debe continuar con su recorrido sin encabezado de AEM revisando el documento [Modelo del contenido como modelos de contenido de AEM](model-your-content.md) donde aprenderá a modelar la estructura de contenido en AEM.
* Si prefiere **aprender practicando**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es) donde irá directamente al desarrollo de AEM sin encabezadoimplementando un proyecto simple para exponer contenido sin encabezado de AEM.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo sin encabezado revisando el documento [Modelo del contenido como modelos de contenido de AEM,](model-your-content.md) a continuación se incluyen algunos recursos opcionales adicionales que profundizan en varios conceptos mencionados en este documento, pero que no son necesarios para continuar el recorrido sin encabezado.

* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md): este recorrido de documentación le ofrece una amplia descripción de la tecnología sin encabezado, cómo sirve AEM el contenido sin encabezado y cómo puede traducirlo.
* [Desarrollo sin encabezado para AEM Sites](/help/sites-developing/headless/introduction.md): una introducción rápida para orientar al desarrollador sin encabezado de AEM con las características necesarias
* [Tutoriales de contenido sin encabezado de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es): utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin encabezado con AEM y elegir el más adecuado para usted.
* [Administración de contenido sin encabezado mediante las API de GraphQL](https://experienceleague.adobe.com/es?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=es#courses): siga este curso para obtener una descripción general de la API de GraphQL implementada en AEM. Se requiere autenticación con AdobeID.
* [AEM Guides de WKND, GraphQL](https://github.com/adobe/aem-guides-wknd-graphql): este proyecto de GitHub incluye aplicaciones de ejemplo que destacan las API de GraphQL de AEM.
* [Guía de introducción sin encabezado](/help/sites-developing/headless/introduction.md#getting-started): Una introducción rápida a las funciones sin encabezado de AEM para usuarios que ya conocen AEM.
* [Crear modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md): documentación técnica sobre los modelos de fragmentos de contenido.
* [Crear fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): documentación técnica sobre fragmentos de contenido.
* [Consulta de contenido con GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md): documentación técnica sobre la API de GraphQL.
* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
