---
title: Planificación
description: Aprenda lo que necesita saber para planificar las pruebas de Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# Planificación{#planning}

En este documento se describe lo que necesita saber para planificar la prueba. Además, debe responder a estas preguntas antes de realizar las pruebas:

* [¿Qué entornos de prueba se necesitarán?](/help/sites-developing/test-environments.md)
* [Definición de los casos de prueba](/help/sites-developing/test-cases.md)
* [Pruebas: ¿cuándo y con quién?](/help/sites-developing/when-who.md)

## Antes de comenzar {#before-you-start}

Antes de comenzar con el análisis real y la definición de pruebas, revise la siguiente información:

**Arquitectura de AEM**: consulte Conceptos básicos para conocer la arquitectura y los principios básicos de AEM.

**Documentación**: consulte cualquiera de las secciones de documentación o los artículos Cómo para obtener más información.

**Principios básicos de las pruebas**: debe tener en cuenta los principios básicos de las pruebas de software y Assurance de calidad. Preferiblemente, debería tener experiencia en proyectos de prueba.

Existen muchos sitios web, libros y cursos que tratan sobre tales principios y por lo tanto no serán tratados en detalle en este documento.

**Suposiciones que se deben evitar**: la suposición más grande es que el sitio web debe atender millones de solicitudes todos los días. En ciertas circunstancias esto puede ser cierto, pero no se puede suponer.

Aunque los números futuros no se pueden predecir con una precisión del 100%, observar el sitio existente y el tráfico experimentado dará una buena indicación. A continuación, puede hacer que las estimaciones dependan del factor por el que espera / espera que aumente el tráfico.

**Compromiso con la calidad**: es de suma importancia que cualquier persona que realice pruebas se mantenga neutral y simplemente informe de los resultados de las pruebas realizadas.

Es responsabilidad del administrador del proyecto decidir e iniciar acciones en función de los resultados.

**Involucrarse** - Aunque es responsabilidad del gerente del proyecto asegurarse de que todas las partes estén completamente involucradas en cualquier reunión (estado, talleres, etc.), también debe tratar de involucrarse lo antes posible en el ciclo del proyecto, incluyendo la recopilación de información y los procesos de análisis de requisitos.

**Involucrar al cliente**: en un tema similar, intente involucrar al cliente (cuando sea posible) al definir los casos de prueba y el plan.

## Tipos de pruebas {#types-of-tests}

Existen varias clasificaciones estándar de pruebas que son adecuadas para su uso al probar un proyecto de AEM. Debe estar familiarizado con estos elementos para decidir cuál utilizar:

>[!NOTE]
>
>Se enumeran en su orden cronológico de aplicación.

**Pruebas de unidades**: pruebas (normalmente) realizadas por el equipo de desarrollo para garantizar que los elementos individuales se comporten correctamente, aunque de forma aislada.

**Pruebas de integración**: prueba módulos al combinarlos. Estas pruebas se realizan después de la prueba unitaria, pero antes de la prueba del sistema.

**Pruebas de humo**: se trata de pruebas rápidas y sucias que se utilizan para probar que el software se está ejecutando y que hay funcionalidad de alto nivel disponible. Los detalles no se prueban.

**Pruebas funcionales**: se utilizan para probar la funcionalidad del software. Se diseñará una serie de pruebas para cubrir todos los detalles funcionales, con entradas esperadas e inesperadas o erróneas.

Las pruebas de caja negra son pruebas funcionales de una unidad/componente/módulo completo, realizadas sin conocimiento del funcionamiento interno del elemento en cuestión.

**Pruebas del sistema**: estas pruebas comprueban todo el sistema una vez que se ha integrado e instalado completamente en una plataforma adecuada.

Prueban la funcionalidad en base a una caja negra.

**Pruebas de rendimiento**: las pruebas de rendimiento son cruciales al probar AEM.

Se utilizan para ilustrar el rendimiento en condiciones diferentes:

* Normal

  Condiciones que el sitio experimentará por ejemplo el 90% del tiempo. Por ejemplo, cuando solo una proporción de los autores utiliza el sistema.

* Pico

  Condiciones que se experimentarán durante un tiempo proporcionalmente corto debido a circunstancias especiales; por ejemplo, cuando todos los autores utilicen el sistema simultáneamente o cuando se publique nuevo contenido y un número mayor de visitantes vea el sitio.

* Extremo

  Se puede utilizar para emular la previsión de rendimiento cuando se publica contenido nuevo y extremadamente interesante en el sitio web. Entonces se puede ver un pico extremo, aunque esto no siempre es totalmente predecible.

  Estas circunstancias se ven a veces cuando se ponen a disposición entradas para eventos específicos, o cuando se publica por primera vez un sitio web muy esperado.

A continuación, los resultados se utilizan para ajustar la aplicación.

**Pruebas de esfuerzo**: las pruebas de esfuerzo se realizan para confirmar el comportamiento de un componente o aplicación en condiciones extremas. En particular, estas pruebas se utilizan para mostrar cómo se deteriora el comportamiento, cuándo falla el elemento y cómo.

**Pruebas de regresión**: se utilizan pruebas de regresión para confirmar que la funcionalidad ya probada en una versión anterior del software sigue funcionando correctamente.

Las pruebas de regresión son buenos candidatos para la automatización (si es posible) para garantizar que se puedan repetir de forma rápida y coherente.

**Pruebas de aceptación**: las pruebas de aceptación son una categoría especial, ya que se utilizan para indicar la aceptación del proyecto por parte del cliente.

La lista de pruebas de aceptación puede contener una combinación de pruebas de las distintas categorías anteriores y se seleccionan para comprobar que el proyecto cumple los requisitos del cliente

Consulte [Aceptación y desactivación](/help/sites-developing/acceptance-signoff.md) para obtener más información.

## Introducción {#getting-started}

Antes de comenzar con los casos de prueba y el plan de prueba detallados, puede hacer lo siguiente:

**Definir los objetivos**: defina los objetivos de alto nivel para que actúen como punto de partida para el ajuste a medida que avance la prueba. Tendrá lo siguiente:

* Pruebe la funcionalidad según la Especificación detallada de requisitos.
* Rendimiento de las pruebas según las [Métricas de destino](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre otros.

**Recopilar estadísticas de tráfico del sitio web existente**. Esta información se puede extraer de los archivos de registro. Consulte Supervisión del rendimiento para obtener más detalles.

Estas cifras darán una indicación del tráfico actual (volumen y difusión) en el sitio web existente y se pueden utilizar para formar un punto de base para el nuevo sitio web.

**Recopilar estadísticas de tráfico de sitios web externos**: si es posible, puede intentar recopilar estadísticas de tráfico de otros sitios web para compararlas, pero estas cifras no siempre se publican.

**Confirmar métricas de destino**: las métricas se usan para definir mediciones cuantitativas de la calidad del sitio web, ya que representan los objetivos de rendimiento que se van a lograr.

Deben definirse al principio del proyecto, junto con el cliente. Consulte [Métricas de destino](/help/sites-developing/planning.md) para obtener más información.
