---
title: Modelos con encabezado y sin encabezado en AEM
description: Los proyectos de AEM se pueden implementar en un modelo con o sin encabezado, pero la elección no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 88%

---

# Encabezado y sin encabezado en AEM {#headful-headless}

Los proyectos de Adobe Experience Manager se pueden implementar tanto en modelos con o sin encabezado, pero la elección no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto. Este documento proporciona una visión general de los diferentes modelos y describe los niveles de integración de SPA.

## Información general {#overview}

AEM ofrece potentes herramientas para gestionar la creación de contenido y su envío en una plataforma. Se trata de un modelo tradicional de administración de contenido “optimista”, en el que los autores y desarrolladores de contenido trabajan en la misma plataforma para enviar las experiencias a los consumidores de contenido.

AEM puede utilizarse simplemente para administrar el contenido, lo que permite que la presentación y el envío del contenido se gestionen mediante otra plataforma. Este es el modelo sin encabezado de la administración de contenido, donde los autores y desarrolladores de contenido trabajan en distintas plataformas para ofrecer experiencia a los consumidores de contenido.

Pero esto no tiene que ser una elección binaria. AEM ofrece una flexibilidad sin precedentes, lo que le permite aprovechar las ventajas de ambos modelos para su proyecto.

![Modelos de implementación de AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

En un modelo con encabezado o de pila completa, el contenido se administra en el repositorio de AEM y los componentes de AEM basados en Java, HTL, etc., se utilizan para procesar el contenido para la experiencia del usuario. En este modelo, la creación del contenido, el estilo, la presentación y la entrega se realizan en AEM.

En un modelo sin encabezado, el contenido se administra en el repositorio de AEM, pero se envía mediante una API como REST y GraphQL a otro sistema para procesar el contenido para la experiencia del usuario. En este modelo, el contenido se crea en AEM, pero el diseño, la presentación y entrega se realiza en otra plataforma.

Las aplicaciones de una sola página (SPA) suelen ser el destino del contenido que AEM entrega sin encabezado. Sin embargo, no es necesario que estos SPA sean completamente externos a AEM. AEM le permite decidir en qué medida sus SPA están integrados en AEM. Veamos un ejemplo.

## Ejemplo de la tienda web {#web-shop-example}

Digamos que tiene una tienda web existente para su empresa como SPA. Aquí encontrará todos los detalles e imágenes de productos. A continuación, introduzca AEM para impulsar sus esfuerzos de marketing, como sitios promocionales, blogs y contenido de campaña. ¿Cómo se integran los dos? AEM permite una amplia gama de opciones:

* **Permita que los sistemas funcionen de forma independiente.**
* **Proporcione contenido limitado de AEM a través de GraphQL a la tienda web.** Los autores pueden crear el contenido en AEM, pero solo se puede ver a través de las SPA de la tienda web.
* **Incruste las SPA de la tienda web en AEM.** Los autores pueden crear el contenido en AEM y verlo en contexto de la tienda web, pero no manipularlo.
* **Incruste las SPA de la tienda web en AEM y habilite puntos editables.** Los autores pueden crear el contenido en AEM y verlo en el AEM en el contexto de la tienda web. Los autores tienen una capacidad limitada para manipular el contenido de las SPA en la tienda web dentro de AEM.
* **Incruste las SPA de tiendas web en AEM y habilite zonas enteras para editarlas.** Los autores pueden crear el contenido en AEM y verlo en AEM en el contexto de la tienda web. Los autores tienen una capacidad limitada para manipular el contenido de las SPA en la tienda web dentro de AEM.

La siguiente sección explora estos niveles de integración con más detalle.

>[!NOTE]
>
>Por supuesto, también puede volver a implementar la SPA de la tienda web como una SPA que funcione completamente en AEM [con el marco de trabajo de un Editor de SPA en AEM.](/help/sites-developing/spa-walkthrough.md) Si ya tiene AEM y desea crear una tienda web u otra SPA, este es el método recomendado, pero está fuera del ámbito de este documento.

## Niveles de integración de las SPA {#integration-levels}

La integración de una SPA se encuentra en un rango de cuatro niveles en AEM.

* **Nivel 0: sin integración**
   * Las SPA y AEM existen por separado y no intercambian información.
   * El contenido se crea, gestiona y entrega de forma independiente en dos sistemas separados.
* **Nivel 1: integración de fragmentos de contenido**
   * Los [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar contenido limitado para las SPA.
   * Las SPA recuperan este contenido a través de la [API de GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) de AEM.
   * Algunos contenidos se administran en AEM, y otros, en un sistema externo.
   * El contenido solo se puede ver en las SPA.
* **Nivel 2: incrustar las SPA en AEM**
   * Los [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido de las SPA.
   * La SPA recupera este contenido a través de la [API de GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) de AEM.
   * Algunos contenidos se administran en AEM, y otros, en un sistema externo.
   * El contenido se puede ver en contexto dentro de AEM.
   * El contenido limitado se puede editar dentro de AEM.
* **Nivel 3: incrustar y habilitar completamente la SPA en AEM**
   * Los [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido de la SPA.
   * La SPA recupera este contenido a través de la [API de GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) de AEM.
   * El contenido se puede ver en contexto dentro de AEM.
   * La mayoría del contenido se puede editar dentro de AEM.

El nivel 1 es un ejemplo de una implementación típica sin encabezado. Sin embargo, los autores de contenido solo pueden ver su contenido en contexto dentro de la SPA. AEM es solo una herramienta de creación.

La ventaja y la flexibilidad de AEM se hacen evidentes con los niveles 2 y 3, al mismo tiempo que se conservan las ventajas de la SPA. Los autores de contenido pueden crear su contenido y también verlo en contexto dentro de AEM. La SPA adquiere la capacidad de crearse en AEM, pero se sigue entregando como una SPA.

## Implementación de los niveles de integración {#implementing}

Existen diferentes herramientas disponibles en AEM según el nivel de integración que elija. Cada nivel se basa en las herramientas utilizadas en el anterior nivel. La siguiente lista vincula los recursos pertinentes.

* **Nivel 1:** los fragmentos de contenido y el [marco de trabajo de AEM sin encabezado](/help/sites-developing/headless/introduction.md) se pueden utilizar para enviar contenido AEM a la SPA.
* **Nivel 2:** Además del nivel uno:
   * [El componente RemotePage](/help/sites-developing/spa-remote-page.md) se puede utilizar para integrar la SPA externa en AEM donde el contenido de AEM se puede ver en contexto.
   * Algunos puntos de la SPA también se pueden habilitar para [permitir la edición limitada en AEM.](/help/sites-developing/spa-edit-external.md)
* **Nivel 3:** Además del nivel dos:
   * Se pueden habilitar zonas enteras de la SPA para permitir una edición completa en AEM.
