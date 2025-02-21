---
title: Desarrollo sin encabezado para sitios de AEM 6.5
description: Descubra cómo las potentes funciones sin encabezado de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, trabajan juntos para permitirle administrar sus experiencias de forma centralizada y atenderlas en todos los canales.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 32%

---

# Desarrollo sin encabezado para sitios de AEM 6.5 {#headless-development}

Descubra cómo las potentes funciones sin encabezado de AEM 6.5, como los modelos de contenido, los fragmentos de contenido y la API de GraphQL, trabajan juntos para permitirle administrar sus experiencias de forma centralizada y atenderlas en todos los canales.

## Información general {#overview}

La implementación sin encabezado es cada vez más importante para ofrecer experiencias a su audiencia, independientemente de su canal.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones híbridas y full-stack y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y en su entrega multicanal. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

![Modelos de implementación de AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Comparación entre con encabezado y sin encabezado {#headful-headless}

Este documento se centra en el modelo completo de implementación sin encabezado de AEM. Sin embargo, con encabezado o sin encabezado no necesita ser una opción binaria en AEM. Las funciones sin encabezado se pueden utilizar para administrar y entregar el contenido a una variedad de puntos de conexión, al tiempo que permiten a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

>[!TIP]
>
>Consulte el documento [Con encabezado y sin encabezado en AEM](/help/sites-developing/headful-headless.md) para obtener más información.

## AEM 6.5 y sin encabezado {#aem-headless}

AEM 6.5 es una herramienta flexible para el modelo de implementación sin encabezado que ofrece tres potentes servicios:

1. Modelos de contenido
   * Los modelos de contenido son una representación estructurada del contenido.
   * Los definen los arquitectos de información en el editor del modelo de fragmentos de contenido de AEM.
   * Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   * Los fragmentos de contenido son instancias de modelos de contenido.
   * Los crean los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   * Se almacenan en AEM Assets y se administran en la IU del administrador de Assets.
1. API de contenido para envío
   * La API de GraphQL de AEM es compatible con la entrega de fragmentos de contenido.
   * La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   * La entrega de contenido directa también es posible con la exportación JSON del [componente principal del fragmento de contenido.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)

## Primeros pasos con AEM Headless {#first-steps}

Hay varios recursos disponibles para que sus clientes empiecen a utilizar las funciones sin encabezado de AEM. Están pensados para diferentes casos de uso, pero todos proporcionan una visión general fiable de las funciones sin encabezado de AEM.

| Recurso | Descripción | Tipo | Audiencia | EST Hora |
|---|---|---|---|---|
| [Recorrido para desarrolladores de Headless](/help/journey-headless/developer/overview.md) | **Para usuarios nuevos en las tecnologías AEM y sin encabezado**, es recomendable empezar aquí para ver una introducción completa a AEM y sus características sin encabezado, desde la teoría sobre esta tecnología hasta publicar su primer proyecto sin encabezado. | Guía  | Desarrolladores **nuevos en las tecnologías de AEM y sin encabezado** | 1 hora |
| [Guía de introducción sin encabezado](/help/sites-developing/headless/getting-started/introduction.md) | **Para usuarios de AEM con experiencia** que necesiten un breve resumen de las funciones principales de AEM sin encabezado, se recomienda consultar esta descripción general de inicio rápido. | Inicio rápido | Desarrolladores, administradores **con experiencia en AEM** | 20 minutos |
| [Tutorial práctico de introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es) | **Si prefiere un enfoque práctico y está familiarizado con AEM**, este tutorial se adentra directamente en la creación de un proyecto sencillo sin encabezado. | Tutorial | Desarrolladores | 2 horas |
| [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es) | Esta colección de recursos se proporciona para **nuevos** y **desarrolladores con experiencia**. | Colección de recursos | Desarrolladores | |
