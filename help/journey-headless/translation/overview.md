---
title: Recorrido de traducción de AEM sin encabezado
description: Empiece aquí un recorrido guiado a través de la traducción de contenido sin encabezado utilizando las potentes herramientas de traducción de AEM.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 93%

---

# Recorrido de traducción de AEM sin encabezado {#aem-headless-translation-journey}

Empiece aquí un recorrido guiado a través de la traducción de contenido sin encabezado utilizando las potentes herramientas de traducción de AEM.

## Introducción {#introduction}

La implementación sin encabezado es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal, la región o la configuración regional.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones de pila completa y se centra en la creación de fragmentos de contenido neutros y reutilizables para el canal y en su entrega multicanal. Mediante las potentes herramientas de traducción de AEM, estos fragmentos reutilizables se pueden traducir fácilmente y enviar a su audiencia dondequiera que se encuentren.

Esta guía le lleva a través de los temas más importantes de la traducción sin encabezado para que al terminar:

* Obtener información general sobre qué es la entrega de contenido sin encabezado.
* Tener un conocimiento básico de las funciones de AEM sin encabezado.
* Conocer las funciones de traducción de AEM y cómo se relacionan con el contenido sin encabezado.
* Tener la posibilidad de empezar a traducir su propio contenido sin encabezado.

El objetivo es ofrecerle un amplio panorama de la tecnología sin encabezado, cómo AEM sirve el contenido sin encabezado y cómo traducirlo. Si no está familiarizado con ninguno de estos temas, este es el lugar ideal para empezar.

Si ya está familiarizado con AEM, el contenido sin encabezado y su traducción, es posible que ya tenga los conocimientos básicos de este recorrido. Si es así, contemple la posibilidad de consultar nuestra documentación técnica vinculada en la [sección de recursos adicionales a continuación.](#additional-resources)

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/home.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si quiere saber lo recomienda Adobe para resolver los casos empresariales sin encabezado con AEM, [Los recorridos de AEM sin encabezado](/help/journey-headless/overview.md) es dónde debe empezar.

## Audiencia {#audience}

Este recorrido está diseñado para el especialista en traducción, a menudo denominado gestor de proyectos de traducción o TPM. Este recorrido establece los requisitos, pasos y métodos para traducir contenido sin encabezado en AEM. El recorrido puede definir usuarios adicionales con los que debe interactuar el especialista en traducción, pero el punto de vista del recorrido es el del especialista en traducción.

Este recorrido supone que el lector tiene experiencia en la traducción de contenido en un sistema CMS grande, pero no asume ningún conocimiento en tecnología sin encabezado o de AEM.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Rol en el recorrido |
|---|---|---|
| Especialista en traducción | Define qué contenido debe traducirse y gestiona esos flujos de trabajo | Audiencia de este recorrido |
| Autor de contenido | Crea y administra contenido que se entrega sin encabezado | Los autores de contenido crean contenido que el especialista en traducción debe traducir. |
| Administrador | Gestiona la configuración base de AEM | El especialista en traducción trabaja con el administrador para realizar los cambios de configuración necesarios para la traducción, como instalar un conector de traducción. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin encabezado y define la estructura de estos datos | Los especialistas en traducción trabajan con el arquitecto de contenido para definir la organización del contenido y así poder traducirlo fácilmente. |

Por supuesto, la información de este recorrido puede ser útil para todas las personas, pero parte de la información puede ser superflua para ciertas funciones. Manténgase atento a [recorridos futuros que cubran funciones adicionales.](/help/journey-documentation/home.md#journeys)

## El recorrido de traducción sin encabezado {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre la traducción de contenido sin encabezado en AEM y le permiten acceder a documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por consiguiente, si es nuevo en la traducción sin encabezado en AEM, Adobe recomienda que empiece por el principio y vaya avanzando en orden consecutivo.

| # | Artículo | Descripción |
|---|---|---|
| 0 | Recorrido de traducción de AEM sin encabezado | Este documento |
| 1 | [Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM](learn-about.md) | Aprenda conceptos sin encabezado, cómo se asignan a AEM y la teoría de la traducción de AEM. |
| 2 | [Introducción a la traducción sin encabezado AEM](getting-started.md) | Conozca cómo organizar su contenido sin encabezado y cómo funcionan las herramientas de traducción de AEM. |
| 3 | [Configuración de la integración de traducción](configure-connector.md) | Aprenda a conectar AEM a un servicio de traducción. |
| 4 | [Configuración de reglas de traducción](translation-rules.md) | Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir. |
| 5 | [Traducir contenido](translate-content.md) | Utilice la integración de traducción y las reglas para traducir el contenido sin encabezado. |
| 6 | [Publicar contenido traducido](publish-content.md) | Aprenda a publicar el contenido traducido y a actualizar la traducción cuando se actualiza el contenido subyacente. |

## Siguientes pasos {#what-is-next}

Ya está listo para empezar su recorrido de traducción sin encabezado de Adobe. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Aprenda sobre el contenido sin encabezado y cómo traducirlo en AEM](learn-about.md)

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema empresarial al proporcionar una narrativa que lo guía a través de procesos y características complejas e interrelacionadas. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Como tal, los recorridos están diseñados para mantenerse por sí mismos. Sin embargo, varios de ellos pueden estar relacionados entre sí. Consulte estos recorridos adicionales para obtener más información sobre cómo las potentes funciones de AEM trabajan juntas.

* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md). Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones sin encabezado de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin encabezado.
* [Recorrido para arquitectos Headless](/help/journey-headless/architect/overview.md): Empiece aquí para ver una introducción a las potentes y flexibles funciones headless de Adobe Experience Manager y cómo diseñar contenido para su proyecto.
* [Recorrido para desarrolladores de contenido sin encabezado de AEM](/help/journey-headless/developer/overview.md): empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones sin encabezado de AEM, sus capacidades y cómo utilizarlas en su primer proyecto de desarrollo.
* [Documentación técnica de AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es): si ya tiene una comprensión sólida de las tecnologías AEM y sin encabezado, puede que desee consultar directamente nuestros documentos técnicos detallados.
   * Una [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)
* [Tutoriales de contenido sin encabezado de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es): si prefiere aprender con la práctica y tiene interés por la tecnología, siga nuestros tutoriales prácticos organizados por API y el marco de trabajo, que exploran la creación y el uso de aplicaciones creadas en el contenido sin encabezado AEM.
* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
