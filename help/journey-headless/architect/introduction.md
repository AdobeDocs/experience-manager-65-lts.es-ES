---
title: Recorrido de arquitecto de contenido sin encabezado de Adobe Experience Manager
description: Una introducción a las potentes y flexibles funciones sin encabezado de Adobe Experience Manager y cómo diseñar contenido para su proyecto.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin,Developer
exl-id: cb64e012-7001-47a3-b038-8f8f6891c6a0
source-git-commit: e3106e87f72484568667873c1772abd30a108e51
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 100%

---

# Modelado de contenido para Headless con AEM: introducción {#architect-headless-introduction}

En esta parte del [Recorrido de arquitectos de contenido AEM Headless](overview.md), podrá aprender los conceptos (básicos) y la terminología necesarios para comprender el modelado de contenido para la entrega de contenido sin encabezado con Adobe Experience Manager (AEM).

Este documento le ayuda a comprender la entrega de contenido sin encabezado, cómo AEM admite sin encabezado y cómo se modela el contenido para que no tenga encabezado. Después de leer, debería haber logrado lo siguiente:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarizarse con la forma en que AEM admite el modelado de contenido y sin encabezado.

## Objetivo {#objective}

* **Público**: principiante
* **Objetivo**: introducir los conceptos y la terminología relevantes para el Modelado de contenido sin encabezado.

## Entrega de contenido de pila completa {#full-stack}

Desde que han surgido los sistemas de administración de contenido (CMS) a gran escala y fáciles de usar, las organizaciones los han utilizado como una ubicación central que permite administrar los mensajes, la promoción de la marca y las comunicaciones. El uso de CMS como punto central para administrar experiencias ha mejorado la eficiencia al eliminar la necesidad de duplicar tareas en sistemas dispares.

![El CMS de pila completa clásico](/help/journey-headless/developer/assets/full-stack.png)

En un CMS de pila completa, toda la funcionalidad para manipular contenido está en el CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

* Hay un solo sistema que mantener.
* El contenido se administra de forma centralizada.
* Todos los servicios del sistema están integrados.
* La creación de contenido es directa.

Por consiguiente, si se necesita agregar un nuevo canal o admitir nuevos tipos de experiencias, se pueden insertar uno o más componentes nuevos en la pila, y solo hay un lugar donde realizar cambios.

![Agregar un nuevo canal a la pila](/help/journey-headless/developer/assets/adding-channel.png)

Sin embargo, la complejidad de las dependencias dentro de la pila se hace evidente rápidamente, puesto que otros elementos de la pila deben ajustarse para adaptarse a los cambios.

## HEAD sin encabezado {#the-head}

El HEAD de cualquier sistema es generalmente el procesador de salida de dicho sistema, normalmente en forma de GUI u otra salida gráfica.

Cuando hablamos de un CMS sin encabezado, el CMS administra el contenido y continúa entregándolo a los consumidores. Sin embargo, al entregar únicamente **contenido** de forma estandarizada, un CMS sin encabezado omite el procesamiento de salida final, dejando la **presentación** del contenido al servicio que lo consume.

![CMS sin encabezado](/help/journey-headless/developer/assets/headless-cms.png)

Los servicios que consumen, ya sean experiencias AR, una tienda web, experiencias móviles, aplicaciones web progresivas (PWA), etc., reciben contenido del CMS sin encabezado y proporcionan su propia representación. Se ocupan de proporcionar sus propios HEADS para su contenido.

Omitir el HEAD simplifica el CMS al eliminar la complejidad. Al hacerlo, también se traslada la responsabilidad de procesar el contenido a los servicios que realmente necesitan el contenido y que a menudo son más adecuados para dicho procesamiento.

## Modelado de contenido {#content-modeling}

El modelado de contenido (también conocido como modelado de datos) es su especialidad, por lo que ¿qué debe tenerse en cuenta al modelar sin encabezado?

Para que las aplicaciones sin encabezado puedan acceder a su contenido y hacer algo con él, el contenido realmente necesita tener una estructura predefinida. Sería posible tener su contenido como forma libre, pero complicaría *mucho* la vida útil de las aplicaciones.

En AEM, usted, como arquitecto de contenido, realizará el modelado de contenido para diseñar una gama de **Modelos de fragmento de contenido**. Definen la estructura utilizada cuando los autores de contenido crean **Fragmentos de contenido** que alojan el contenido.

### Acceso al contenido {#access-content}

Se trata más bien de un detalle de desarrollo, pero puede interesarle para completar la historia.

Una vez haya creado los modelos de fragmento de contenido y que los autores los hayan utilizado para generar el contenido, las aplicaciones sin encabezado tendrán que acceder a este contenido.

Adobe Experience Manager (AEM) puede acceder de forma selectiva a sus fragmentos de contenido mediante la API de GraphQL de AEM para devolver solo el contenido necesario. Con la API, un desarrollador puede formular consultas que seleccionan contenido específico. Este proceso de selección se basa en *sus* Modelos de fragmento de contenido.

Esto significa que el proyecto puede realizar una entrega sin encabezado de contenido estructurado para usarlo en las aplicaciones.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos y la terminología, el siguiente paso consiste en [Aprender los conceptos básicos del modelado con Modelos de fragmentos de contenido](basics.md).

## Recursos adicionales {#additional-resources}

* Recorrido para desarrolladores de AEM headless
   * [Obtenga más información acerca del desarrollo de CMS sin encabezado](/help/journey-headless/developer/learn-about.md)
   * [Aprenda cómo modelar el contenido](/help/journey-headless/developer/model-your-content.md)
* [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
