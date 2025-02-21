---
title: Perspectiva de contenido
description: La perspectiva de contenido proporciona información sobre el rendimiento de la página mediante análisis web y recomendaciones de SEO
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Perspectiva de contenido{#content-insight}

La perspectiva de contenido proporciona información sobre el rendimiento de la página mediante análisis web y recomendaciones de SEO. Utilice Perspectiva de contenido para tomar decisiones sobre cómo modificar páginas o conocer cómo los cambios anteriores han cambiado el rendimiento. Para cada página que cree, puede abrir Perspectiva de contenido para analizar la página.

![chlimage_1-311](assets/chlimage_1-311.png)

El diseño de la página Perspectiva de contenido cambia para adaptarse a las dimensiones de pantalla y a la orientación del dispositivo que está utilizando.

## Datos del informe

La página Perspectiva de contenido incluye informes que utilizan datos de Adobe SiteCatalyst, Adobe Target, Adobe Social y BrightEdge:

* SiteCatalyst: Hay disponibles informes para las siguientes métricas:

   * Page views
   * Tiempo promedio empleado en la página
   * Orígenes

* Target: informa sobre la actividad de campaña para la que la página incluye ofertas.
* BrightEdge: informa sobre las funciones de la página que mejoran la visibilidad de la página para los motores de búsqueda y recomienda las funciones que deben implementarse.

Consulte [Abrir Analytics y Recommendations para una página](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Período de informe

Los informes muestran datos correspondientes a un período de tiempo que usted controla. Al ajustar el período de informe, los informes se actualizan automáticamente con los datos de ese período. Las indicaciones visuales indican el momento en el que cambiaron las versiones de la página, de modo que puede comparar el rendimiento de cada versión.

>[!NOTE]
>
>La cronología del panel de información de contenido está en `GMT`.

También puede especificar la granularidad de los datos del informe; por ejemplo, puede ver datos diarios, semanales, mensuales o anuales.

Consulte [Cambio del período de informe](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>Los informes de Perspectivas de contenido requieren que el administrador haya integrado AEM con SiteCatalyst, Target y BrightEdge. Ver [Integración con SightCatalyst](/help/sites-administering/adobeanalytics.md), [Integración con Adobe Target](/help/sites-administering/target.md) e [Integración con BrightEdge](/help/sites-administering/brightedge.md).

## El informe Vistas {#the-views-report}

El informe Vistas incluye las siguientes funciones para evaluar el tráfico de la página:

* Número total de vistas de una página durante el período de informe.
* Gráfico del número de vistas en el período de informe:

   * Vistas totales.
   * Visitantes únicos.

![chlimage_1-312](assets/chlimage_1-312.png)

## El informe Promedio de páginas comprometidas {#the-page-average-engaged-report}

El informe Participación media de la página incluye las siguientes funciones para evaluar la eficacia de la página:

* Promedio de tiempo que la página permanece abierta durante todo el período de informe.
* Gráfico de la longitud promedio de una vista de página durante el período de informe.

![chlimage_1-313](assets/chlimage_1-313.png)

## El informe de fuentes {#the-sources-report}

El informe Fuentes indica cómo navegaron los usuarios hasta la página, por ejemplo, desde los resultados del motor de búsqueda o utilizando la dirección URL conocida.

![chlimage_1-314](assets/chlimage_1-314.png)

## El informe de devoluciones {#the-bounces-report}

El informe Devoluciones incluye un gráfico que muestra el número de devoluciones que se han producido para una página durante el periodo de informe seleccionado.

![chlimage_1-315](assets/chlimage_1-315.png)

## El informe Actividad de la campaña {#the-campaign-activity-report}

Para cada campaña para la cual la página está activa, aparece un informe llamado Actividad *Nombre de campaña*. El informe muestra las impresiones y conversiones de página de cada segmento para el que se proporciona una oferta.

![chlimage_1-316](assets/chlimage_1-316.png)

## El informe Recomendaciones de SEO {#the-seo-recommendations-report}

El informe Recomendaciones de SEO contiene los resultados del análisis de BrightEdge para la página. El informe es una lista de comprobación de las funciones de la página que indica qué funciones incluye y no incluye la página para maximizar la capacidad de búsqueda mediante motores de búsqueda.

El informe permite crear tareas para mejorar la búsqueda de páginas. Las recomendaciones indican que se han creado tareas para aplicar la recomendación. Consulte [Asignación de tareas para recomendaciones de SEO](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
