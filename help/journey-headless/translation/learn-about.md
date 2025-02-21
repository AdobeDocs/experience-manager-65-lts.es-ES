---
title: Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM
description: Aprenda conceptos sin encabezado, cómo se asignan a AEM y la teoría de la traducción de AEM.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 98%

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

En un CMS de pila completa, toda la funcionalidad para manipular contenido se encuentra en CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

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
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
