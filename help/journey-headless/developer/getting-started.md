---
title: Introducción a AEM sin encabezado
description: En esta parte del Recorrido para desarrolladores de contenido sin encabezado de AEM, obtenga información sobre los requisitos previos.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2999'
ht-degree: 95%

---

# Introducción a AEM sin encabezado {#getting-started}

En esta parte del [Recorrido para desarrolladores de contenido sin encabezado de AEM](overview.md) obtenga información sobre lo que se necesita para comenzar su propio proyecto con contenido sin encabezado de AEM.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin encabezado de AEM, [Obtenga información sobre el desarrollo sin encabezado de CMS](learn-about.md) aprendió la teoría básica de lo que es un CMS sin encabezado y ahora debería poder hacer lo siguiente:

* Comprender los conceptos básicos y la terminología de la entrega de contenido sin periféricos
* Comprender por qué y cuándo se requiere un proceso sin encabezado
* Conocer en un nivel superior cómo se utilizan los conceptos sin encabezado y cómo se interrelacionan

Este artículo se basa en estos fundamentos para que entienda cómo puede utilizar AEM para implementar una solución sin encabezado.

## Objetivo {#objective}

Este documento le ayudará a comprender el contenido sin encabezado de AEM dentro del contexto de su propio proyecto. Después de leer, debería haber logrado lo siguiente:

* Comprender los conceptos básicos de las características de AEM sin encabezado.
* Conozca los requisitos previos para utilizar las características de AEM sin encabezado.
* Tener en cuenta los niveles de integración de AEM sin encabezado.
* Ser capaz de definir el proyecto en términos del ámbito.

## Conceptos básicos de AEM {#aem-basics}

Antes de poder definir el proyecto sin encabezado dentro de AEM, es importante comprender algunos conceptos básicos.

### Ejemplo de autor {#author}

En su versión más sencilla, AEM consta de un ejemplo de autor y un [ejemplo de publicación](#publish) que trabajan juntos para crear, gestionar y publicar el contenido.

El contenido comienza con el ejemplo del autor. Aquí es donde los autores crean su contenido. El entorno de creación ofrece varias herramientas para que los autores creen, organicen y reutilicen su contenido.

### Instancia de publicación {#publish}

Una vez creado el contenido en el ejemplo de autor, debe publicarse para que esté disponible para otros servicios que lo consuman. Una instancia de publicación contiene todo el contenido que se ha publicado.

### Replicación {#replication}

La replicación es el acto de transferir contenido del ejemplo de autor al ejemplo de publicación. Esto se hace automáticamente AEM cuando un autor u otro usuario con los derechos adecuados publica contenido.

### Resumen de fundamentos de AEM {#aem-basics-summary}

En su nivel más sencillo, la creación de experiencias digitales en AEM requiere los siguientes pasos:

1. Sus autores de contenido crean su contenido sin encabezado en el ejemplo de autor.
1. Cuando este contenido está listo, se replica en el ejemplo de publicación.
1. Luego se puede llamar a las API para recuperar este contenido.

AEM sin encabezado crea esta base técnica al ofrecer herramientas potentes para administrar el contenido sin encabezado [se describe en la siguiente sección.](#aem-headless-basics)

## Conceptos básicos del contenido sin encabezado de AEM {#aem-headless-basics}

Las funcionalidades sin encabezado de AEM se basan en algunas funciones clave. Estos se explican en detalle en partes posteriores del recorrido. Ahora solo es importante conocer los conceptos básicos de lo que hacen y cómo se llaman.

### Modelos de fragmento de contenido {#content-fragment-models}

Los Modelos de fragmento de contenido definen la estructura de los datos y el contenido que creará y gestionará en AEM. Sirven como una especie de andamiaje para el contenido. Al elegir crear contenido, los autores elegirán entre los modelos de fragmento de contenido que defina, que los guiarán en la creación de contenido.

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido permiten diseñar, crear, depurar y publicar contenido independiente de cualquier página. Permiten preparar contenido listo para su uso en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

### Las API de GraphQL y REST {#apis}

Para modificar el contenido sin problemas, AEM ofrece dos API sólidas.

* La API de GraphQL permite crear solicitudes para acceder a fragmentos de contenido y enviarlos.
* La API de REST de Assets permite crear y modificar fragmentos de contenido (y otros recursos).

Aprenderá a utilizar estas API en una parte posterior del recorrido sin encabezado de AEM. O bien, vea la sección [recursos adicionales](#additional-resources) a continuación para obtener documentación adicional.

## Niveles de integración sin encabezado {#integration-levels}

AEM admite todos los modelos sin encabezado y los modelos tradicionales de pila completa o sin encabezado de un CMS. Sin embargo, AEM ofrece no solo estas dos opciones exclusivas, sino también la capacidad de soportar modelos híbridos que combinan las ventajas de ambos, ofreciendo una flexibilidad única para su proyecto sin encabezado.

Para garantizar su comprensión de los conceptos sin encabezado, este Recorrido para desarrolladores sin encabezado de AEM se centra en el modelo sin encabezado para ponerlo en marcha lo antes posible sin necesidad de utilizar codificación en AEM.

Sin embargo, hay que tener en cuenta las posibilidades híbridas adicionales que se abren una vez que entienda las características sin encabezado de AEM. Para su información, estos casos se detallan a continuación. Al final del recorrido, se le presentarán estos conceptos con más detalle en caso de que se requiera dicha flexibilidad para su proyecto.

### Ya tiene un consumo externo de contenido sin encabezado, como una aplicación de página única (SPA). {#already-have-a-spa}

Supongamos que su requisito básico es, como mínimo, entregar contenido de AEM a un servicio externo existente.

#### Nivel 1: integración de Fragmentos de contenido: modelo tradicional sin encabezado {#level-1}

Este nivel de integración es el modelo tradicional sin encabezado y permite a sus autores de contenido crear contenido en AEM y enviarlo sin necesidad de encabezado para un incontable número de servicios externos que utilicen GraphQL o editarlos desde servicios externos mediante la API de Recursos. No se requiere codificación en AEM.

En este modelo, AEM solo se utiliza para crear y servir el contenido mediante los Fragmentos de contenido de AEM. El procesamiento y la interacción con el contenido se delegan en la aplicación externa consumidora, a menudo en una aplicación de página única (SPA).

#### Nivel 2: incrustar la SPA en AEM, modelo híbrido {#level-2}

Este nivel de integración se basa en el primer nivel, pero también permite que la aplicación externa (SPA) se incruste en AEM para que los autores de contenido puedan ver el contenido en el contexto de la aplicación externa dentro de AEM. La aplicación también puede admitir una edición limitada de la aplicación externa dentro de AEM.

Este nivel tiene la ventaja de permitir que los autores de contenido creen contenido de forma flexible de AEM de forma progresiva, con su contenido presentado en contexto con una SPA externa integrada, a la vez que siguen entregando el contenido sin encabezado.

#### Nivel 3: incrustar y activar completamente la SPA en AEM, modelo híbrido {#level-3}

Este nivel de integración se basa en el nivel dos al permitir que la mayoría del contenido de la SPA externa se pueda editar dentro de AEM.

### Todavía no tiene un consumidor externo del contenido sin encabezado, como una aplicación de una sola página (SPA). {#do-not-have-a-spa}

Si su objetivo es crear una SPA que consuma contenido sin encabezado desde AEM, puede utilizar funciones como Fragmentos de contenido para administrar el contenido sin encabezado y también generar una SPA dentro del marco de trabajo del editor de SPA.

Con el editor de SPA, la SPA no solo consume contenido de AEM, sino que también es totalmente editable dentro de AEM por sus autores de contenido, lo que le ofrece la flexibilidad de envío sin encabezado y de edición en contexto dentro de AEM.

## Condiciones y requisitos previos {#requirements-prerequisites}

Antes de comenzar con su proyecto sin encabezado de AEM, existen varios requisitos.

### Conocimiento {#knowledge}

* GraphQL
* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente u otro consumidor de su contenido sin encabezado de AEM

## Definición del proyecto {#defining-your-project}

Para que cualquier proyecto tenga éxito, es importante definir claramente no solo los requisitos del proyecto, sino también las funciones y responsabilidades.

### Ámbito {#scope}

Es importante tener un ámbito claramente definido para el proyecto. El ámbito informa acerca de los criterios de aceptación y le permite establecer una definición de listo.

La primera pregunta que deben hacer es “¿Qué estoy tratando de lograr con el contenido sin encabezado de AEM?” La respuesta debería ser, en general, que tiene o tendrá en el futuro una aplicación de experiencia que ha creado con sus propias herramientas de desarrollo, no con AEM. Esta aplicación de experiencia puede ser una aplicación móvil, un sitio web o cualquier otra aplicación de experiencia orientada al cliente final. El objetivo de utilizar contenido sin encabezado de AEM es alimentar su aplicación de experiencia con contenido creado, almacenado y administrado en AEM con una API de última generación, la cual llama al contenido sin encabezado de AEM para recuperarlo o incluso contenido completamente CRUD directamente desde su aplicación de experiencia. Si esto no es lo que está buscando hacer, probablemente desee [volver a la documentación de AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es) y buscar la sección que mejor se adapte a lo que desea lograr.

### Funciones y responsabilidades {#roles-responsibilities}

Las funciones de cualquier proyecto individual varían, pero las importantes que se deben tener en cuenta en el desarrollo del contenido sin encabezado de AEM, son las siguientes:

* [Administrador](#administrator)
* [Autor de contenido](#content-author)
* [Arquitecto de contenido](#content-architect)
* [Desarrollador](#developer)

#### Administrador {#administrator}

El administrador es responsable de la configuración y configuración base de su sistema. Por ejemplo, el administrador configura su organización dentro del sistema de Adobe User Management, denominado Identity Management System (IMS). El administrador es el primer usuario de la organización que recibe una invitación por correo electrónico de Adobe una vez que su organización ha sido creada por Adobe dentro de IMS. El administrador puede iniciar sesión en IMS y agregar usuarios de otras personas.

Una vez que el administrador configura los usuarios, se les conceden los permisos para acceder a todos los recursos de AEM y realizar su trabajo como colaboradores para ofrecer la aplicación de experiencia mediante AEM Headless.

El administrador debe ser el usuario que configura AEM y prepara el entorno de tiempo de ejecución para que los [autores de contenido](#content-author) puedan crear y actualizan contenido y que los [desarrolladores](#developer) utilicen las API que recuperan o modifican contenido para sus aplicaciones de experiencia.

#### Autor de contenido {#content-author}

Los autores de contenido crean y administran el contenido sin encabezado que entrega AEM. Los autores de contenido utilizan funciones de AEM, como los fragmentos de contenido y la consola Recursos, para administrar el contenido.

Los autores de contenido deben tener en cuenta las siguientes prácticas recomendadas.

#### Plan de traducción {#translation}

Planifique la traducción justo al principio del proyecto. Considere al “Especialista de traducción” como una persona independiente, cuya responsabilidad es la de definir el contenido que debe ser traducido y el que no, y cuál contenido traducido puede ser modificado por los productores de contenido regionales o locales.

Cree un plan sobre la traducción de contenido que necesita.

* ¿Necesita idiomas diferentes o también idiomas que se adapten a las especificidades regionales?
* ¿Necesita contenido con medios enriquecidos, como imágenes o vídeos, para que sea diferente en diferentes configuraciones regionales?

Sea claro sobre el flujo de trabajo de actualización de contenido. ¿Cuál es el proceso de aprobación que debe admitir el sistema? ¿Se pueden utilizar los flujos de trabajo de AEM para automatizar este proceso?

Tenga en cuenta que la [jerarquía de contenido](#content-hierarchy) se puede utilizar para facilitar la traducción.

Consulte la sección [recursos adicionales](#additional-resources) para obtener documentación adicional sobre los flujos de trabajo de AEM y las herramientas de traducción, entre ellos, los vínculos al recorrido de traducción sin encabezado de AEM.

##### Aprovechar la jerarquía de contenido {#content-hierarchy}

La jerarquía de carpetas puede resolver dos problemas importantes con respecto a la administración de contenido:

* [Traducción](#translation): AEM administra la traducción del contenido manteniendo copias del contenido en carpetas específicas de la configuración regional.
* Organización: las carpetas se utilizan para definir una jerarquía de contenido necesaria con el fin de satisfacer las necesidades de traducción y administrar lógicamente los fragmentos de contenido.

AEM permite una estructura de contenido flexible, y una jerarquía puede ser arbitrariamente grande. Sin embargo, es importante darse cuenta de que cualquier cambio en la estructura de carpetas puede tener consecuencias no deseadas para las consultas existentes [basadas en la ruta de contenido.](#developer) Por lo tanto, una jerarquía bien definida y claramente establecida por adelantado, puede ser útil para sus autores de contenido.

Las carpetas también se pueden restringir para permitir solo ciertos tipos de contenido (según los modelos de fragmento de contenido). Se recomienda especificar siempre explícitamente qué modelos se permiten para todas las carpetas de la jerarquía. Especificación del contenido permitido para una carpeta determinada:

* Evita que los autores de contenido creen contenido que no pertenece a la carpeta.
* Optimiza el proceso de creación de contenido filtrando los tipos de contenido permitidos en la carpeta durante la creación para mostrar solo tipos de contenido válidos.

Al crear una estructura de contenido adecuada, resulta más fácil coordinar la creación de contenido sin encabezado entre canales para maximizar la reutilización del contenido. El aprovechamiento del contenido en varios canales mejora considerablemente la eficacia de la producción de contenido y la administración de cambios.

##### Establecimiento de convenciones de nombres adecuados {#naming-conventions}

Los nombres de los fragmentos de contenido deben ser descriptivos para los autores de contenido. AEM gestiona de forma transparente la omisión o el truncamiento de los nombres que usan los ID en el nivel del repositorio. Por lo tanto, los nombres lógicos proporcionados por los autores de contenido siempre deben ser legibles y representar el contenido.

* Nombre incorrecto: `cta_btn_1`
* Nombre correcto: `Call To Action Button`

Consulte la sección [recursos adicionales](#additional-resources) para obtener documentación adicional sobre AEM convenciones de asignación de nombres a páginas.

##### No ampliar en exceso el anidamiento de contenido {#content-nesting}

Los [fragmentos de contenido](#content-fragments) se utilizan en AEM para crear contenido sin encabezado. AEM admite hasta diez niveles de anidación de contenido para fragmentos de contenido. Sin embargo, es importante tener en cuenta que AEM debe resolver de forma iterativa cada referencia definida en el fragmento de contenido principal y, a continuación, comprobar si hay alguna referencia secundaria en todos los elementos del mismo nivel. Estas operaciones pueden sumarse rápidamente y convertirse en un problema de rendimiento.

Como regla general, las referencias de fragmento de contenido no deben anidarse más de cinco niveles.

#### Arquitecto de contenido {#content-architect}

Analiza los requisitos de los datos que deben entregarse sin encabezado y define la estructura de estos datos. Estas estructuras se denominan [Modelos de fragmento de contenido](#content-fragment-models) en AEM. Los modelos de fragmento de contenido se utilizan como base para los fragmentos de contenido que crean los autores de contenido.

Un enfoque útil a la hora de definir modelos de fragmento de contenido es crear modelos que se asignen a los componentes UX de las aplicaciones que consumen el contenido.

Dado que los autores de contenido interactúan con los modelos de forma continua a medida que crean contenido nuevo, alinear los modelos con el UX les ayuda a visualizar la experiencia digital resultante. Siguiendo con esta alineación, puede asignar iconos a los modelos de fragmento de contenido que representan el elemento UX para que los autores puedan seleccionar de forma intuitiva el modelo correcto en función de las indicaciones visuales.

#### Desarrollador {#developer}

Los desarrolladores son los responsables de unir el contenido que se crea sin encabezado en AEM para el consumidor de ese contenido, que a menudo puede ser una aplicación de página única (SPA), una aplicación web progresiva (PWA), una tienda web u otro servicio externo a AEM.

GraphQL sirve de nexo entre AEM y los consumidores de contenido sin encabezado. GraphQL es el idioma en que AEM consulta el contenido necesario.

Los desarrolladores deben tener en cuenta las siguientes recomendaciones básicas al planificar sus consultas:

* Las consultas no deben depender de una ruta fija (`ByPath`) para recuperar fragmentos de contenido.
   * [Los autores de contenido tienen control total sobre la jerarquía de fragmentos de contenido](#content-hierarchy) y podrían realizar cambios que podrían romper dicha consulta.
   * Las consultas deben optar por referencias del modelo de fragmento de contenido con parámetros de consulta dinámicos para filtrar los resultados y generar la carga útil deseada.
* Para obtener el mejor rendimiento de las consultas, utilice siempre consultas persistentes en AEM. De esto se habla más adelante en el recorrido.
* GraphQL es un lenguaje declarativo que sigue el lema “Pida exactamente lo que necesita, y obtenga exactamente eso”. Esto significa que, al crear consultas de GraphQL, evite siempre consultas de tipo `select *` que podría crear en una base de datos relacional.

Para una [implementación sin encabezado típica mediante AEM,](#level-1) el desarrollador no necesita tener conocimientos de codificación de AEM.

### Requisitos de rendimiento {#performance-requirements}

Para que cualquier proyecto sea un éxito, el rendimiento debe tenerse en cuenta antes de crear cualquier contenido.

Asegúrese de comprender las expectativas de los usuarios/visitantes y de diseñarlas para ellos. Establezca objetivos de nivel de servicio (SLO) y mídalos para comprender si cumple con las expectativas del usuario.

#### Patrones de tráfico {#traffic-patterns}

Para comprender el tráfico y los patrones de tráfico, comience por reunir lo que sabe del pasado y luego proyéctelo al crecimiento esperado en los próximos años. Algunas de las variables más importantes a tener en cuenta:

* ¿Cuántas llamadas a la API por hora, día o mes espera y cuál es el potencial para los picos y la estacionalidad?
* ¿Cuántos autores de contenido diferentes hay?
* ¿Cuántos autores de contenido espera que trabajen simultáneamente?
* ¿Cuál es la frecuencia de las actualizaciones de contenido?
* ¿Cuántos modelos de contenido se necesitan?
* ¿Cuántas instancias de modelos se necesitan?

#### Frecuencia de actualización {#update-frequency}

A menudo, las secciones de experiencias tienen distintas frecuencias de actualizaciones de contenido. Comprender esto es importante para poder ajustar las configuraciones de la red de distribución de contenido (CDN) y la caché. Esto también es una aportación importante para los [Arquitectos de contenido](#content-architects), ya que diseñan modelos para representar su contenido. Tenga en cuenta lo siguiente:

* ¿Deben caducar algunos tipos de contenido después de un período determinado?
* ¿Hay elementos que son específicos del usuario y que, por lo tanto, no se pueden almacenar en caché?

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Comprender los conceptos básicos de las características de AEM sin encabezado.
* Conozca los requisitos previos para utilizar las características de AEM sin encabezado.
* Tener en cuenta los niveles de integración de AEM sin encabezado.
* Ser capaz de definir el proyecto en términos del ámbito.

Debe continuar su recorrido sin encabezado de AEM revisando a continuación el documento [Ruta de la primera experiencia para usar el contenido sin encabezado de AEM](path-to-first-experience.md), donde aprenderá a configurar las herramientas necesarias y a empezar a pensar en modelar los datos en AEM.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo sin encabezado al revisar el documento [Ruta de la primera experiencia para usar el contenido sin encabezado de AEM,](path-to-first-experience.md) los siguientes son recursos opcionales que profundizan ciertos conceptos mencionados en este documento, pero que no son necesarios para continuar el recorrido sin encabezado.

* [Contenido con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md): un análisis completo de los niveles de integración sin encabezado disponibles en AEM

* Una [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)

* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md). Este recorrido de documentación te ofrece una amplia comprensión de la tecnología sin encabezado, cómo AEM presenta el contenido sin encabezado y cómo puedes traducirlo.

* [Tutoriales de contenido sin encabezado de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es): utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin encabezado con AEM y elegir el más adecuado para usted.
* [Administración de contenido sin encabezado mediante las API de GraphQL](https://experienceleague.adobe.com/es?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=es#courses): siga este curso para obtener una descripción general de la API de GraphQL implementada en AEM. Se requiere autenticación con AdobeID.
* [AEM Guides de WKND, GraphQL](https://github.com/adobe/aem-guides-wknd-graphql): este proyecto de GitHub incluye aplicaciones de ejemplo que destacan las API de GraphQL de AEM.
* [Conceptos sobre la creación](/help/sites-authoring/author.md): documentación técnica para el entorno de creación de AEM que incluye detalles sobre la configuración de creación y publicación
* [Publicación de páginas](/help/sites-authoring/publishing-pages.md): documentación técnica para la publicación de contenido en AEM
* [Convenciones de nomenclatura](/help/sites-developing/naming-conventions.md): documentación técnica de las restricciones de asignación de nombres a páginas en AEM
* [Traductor y administrador de varios sitios](/help/sites-administering/msm-and-translation.md): documentación técnica sobre potentes funciones de traducción de AEM
* [Flujos de trabajo de AEM](/help/sites-authoring/workflows.md): documentación técnica sobre cómo automatizar flujos de trabajo en AEM
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): documentación técnica para fragmentos de contenido.
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md): documentación técnica para modelos de fragmento de contenido.
* [Documentación técnica de GraphQL](https://graphql.org): la definición de GraphQL (vínculo externo)
* [API de GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md): documentación técnica que explica cómo crear solicitudes para acceder y enviar fragmentos de contenido
* [API de REST de Assets](/help/assets/assets-api-content-fragments.md): documentación técnica que explica cómo crear y modificar fragmentos de contenido (y otros recursos)
* [Consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md): documentación técnica sobre consultas persistentes en AEM
* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)