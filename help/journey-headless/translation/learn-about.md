---
title: Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM
description: Aprenda conceptos sin encabezado, cómo se asignan a AEM y la teoría de la traducción de AEM.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin,Developer,User,Leader
exl-id: b81293da-772a-4ff1-8606-cec92d8cbd72
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 100%
---
# Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM {#learn-about}

Aprenda conceptos sin encabezado, cómo se asignan a AEM y la teoría de la traducción de AEM.

## Objetivo {#objective}

Este documento le ayudará a comprender la entrega de contenido sin encabezado, cómo AEM lo admite y cómo puede traducirlo. Después de leer, debería haber logrado lo siguiente:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Estar familiarizado con el modo en que AEM admite la traducción sin encabezado.

## Entrega de contenido de pila completa {#full-stack}

Desde que han surgido los sistemas de administración de contenido (CMS) a gran escala y fáciles de usar, las organizaciones los han utilizado como una ubicación central que permite administrar los mensajes, la promoción de la marca y las comunicaciones. El uso de CMS como punto central para administrar experiencias ha mejorado la eficiencia al eliminar la necesidad de duplicar tareas en sistemas dispares.

![El CMS de pila completa clásico](/help/journey-headless/developer/assets/full-stack.png)

En un CMS de pila completa, toda la funcionalidad para manipular contenido está en el CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

* Hay un solo sistema que mantener.
* El contenido se administra de forma centralizada.
* Todos los servicios del sistema están integrados.
* La creación de contenido es directa.

Por lo tanto, si se debe añadir un nuevo canal o se requiere compatibilidad con nuevos tipos de experiencias, se pueden insertar uno o más componentes nuevos en la pila; solo hay un lugar donde realizar cambios.

![Adición de un nuevo canal a la pila](/help/journey-headless/developer/assets/adding-channel.png)

Sin embargo, la complejidad de las dependencias dentro de la pila se hace evidente rápidamente, ya que otros elementos de la pila deben ajustarse para adaptarse a los cambios.

## HEAD sin encabezado {#the-head}

El HEAD de cualquier sistema es generalmente el procesador de salida de dicho sistema, normalmente en forma de GUI u otra salida gráfica.

Cuando hablamos de un CMS sin encabezado, el CMS administra el contenido y continúa entregándolo a los consumidores. Sin embargo, al entregar únicamente **contenido** de forma estandarizada, un CMS sin encabezado omite el procesamiento de salida final, dejando la **presentación** del contenido al servicio que lo consume.

![CMS sin encabezado](/help/journey-headless/developer/assets/headless-cms.png)

Los servicios que consumen, ya sean experiencias de AR, una tienda web, experiencias móviles, aplicaciones web progresivas (progressive web apps, PWA), etc., reciben contenido del CMS sin encabezado y proporcionan su propia renderización. Se ocupan de proporcionar sus propios HEADS para su contenido.

Omitir el HEAD simplifica el CMS al eliminar la complejidad. Al hacerlo, también se traslada la responsabilidad de procesar el contenido a los servicios que realmente necesitan el contenido y que a menudo son más adecuados para dicho procesamiento.

## Traducción del contenido sin encabezado en AEM {#translating-in-aem}

Además de ofrecer herramientas sólidas para crear, gestionar y entregar páginas web tradicionales de forma totalmente apilada, AEM también ofrece la capacidad de crear selecciones de contenido independientes y servirlas sin encabezado.

La potencia de AEM le permite entregar contenido sin encabezado, en pilas completas o en ambos modelos al mismo tiempo. Para el especialista en traducción, se puede aplicar el mismo conjunto de herramientas de traducción a ambos tipos de contenido, lo que le ofrece un enfoque unificado para traducir el contenido.

Más adelante en el recorrido conocerá los detalles sobre cómo AEM traduce el contenido, pero a un alto nivel, el concepto es sencillo:

1. Defina una conexión a un servicio de traducción configurando el marco de trabajo de integración de traducción.
1. Defina qué contenido debe traducirse mediante reglas de traducción.
1. Cree un proyecto de traducción para recopilar el contenido, enviarlo al servicio de traducción y recibir los resultados.
1. Revise y publique el contenido traducido.

## Siguientes pasos {#what-is-next}

Gracias por iniciar el recorrido de traducción sin encabezado en AEM. Ahora que lee este documento, debe realizar lo siguiente:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Estar familiarizado con el modo en que AEM admite la traducción sin encabezado.

Aproveche este conocimiento y continúe con su recorrido de traducción de AEM sin encabezado revisando el documento [Introducción a la traducción sin encabezado de AEM](getting-started.md) donde encontrará información general sobre cómo AEM administra el contenido, y conocer sus herramientas de traducción.

## Recursos adicionales {#additional-resources}

Si bien se recomienda pasar a la siguiente parte del recorrido de traducción sin encabezado mediante la revisión del documento [Introducción a la traducción sin encabezado de AEM,](getting-started.md) los siguientes son algunos adicionales, recursos opcionales que hacen una inmersión más profunda en algunos conceptos mencionados en este documento, pero no están obligados a continuar en el recorrido sin encabezado.

* [MSM y traducción](/help/sites-administering/msm-and-translation.md): los detalles de Multi-Site Manager de AEM y cómo funciona con sus herramientas de traducción
* Una [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)
* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales para contenido sin encabezado en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
