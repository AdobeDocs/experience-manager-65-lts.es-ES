---
title: Explicación de la segmentación al crear una campaña
description: La segmentación es una consideración clave al crear una campaña.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 46%

---

# Información acerca de la segmentación{#understanding-segmentation}

La segmentación es una consideración clave al crear una campaña. Normalmente, debe tener los segmentos ya definidos antes de iniciar la campaña.

Los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Comprender estos objetivos y cumplir las expectativas es un factor de éxito importante para el marketing en línea.

La segmentación ayuda a conseguirlo al analizar y caracterizar el comportamiento de un visitante:

* actividad en el sitio web
* perfil
* actividad en otros sitios web

El contenido puede personalizarse según las necesidades y los intereses del visitante, según los segmentos con los que coincidan.

## Uso de la segmentación {#using-segmentation}

Los segmentos se definen en [Configuración de la segmentación](/help/sites-administering/campaign-segmentation.md). Se utilizan para dirigir el contenido real que visualiza un público objetivo específico.

## Terminología de segmentación {#segmentation-terminology}

Al analizar la segmentación, se emplea la siguiente terminología:

**Visitante**: Un visitante es una persona que visita un sitio web. La visita de esa persona suele comenzar desde una página de referencia y luego pasa a una o más vistas de página del sitio web. Se puede crear un perfil de comportamiento a partir de los detalles de la visita de esa persona.

**Usuario**: Un usuario es un visitante que se registra con el sitio web para recibir un perfil de cuenta. Para generar su perfil, proporcionan una identificación adicional, como una dirección de correo electrónico y el sexo, entre otros. También se puede recopilar información adicional, como actividad de la comunidad y patrones de compra, entre otros. A partir de la información proporcionada en el perfil, se puede crear un perfil demográfico.

**Pista**: Una pista es una característica o propiedad de un visitante que se puede usar para determinar la pertenencia en un segmento específico.

**Segmento**: Un segmento es un conjunto de visitantes que comparten determinadas características. Los segmentos deben ser distintivos, con un mínimo de superposición con otros segmentos.

**Características de comportamiento**: Las características de comportamiento son las que se relacionan con el comportamiento de un visitante en el sitio web. Entre estas características se incluyen:

* Interés en el sitio web, incluidas las páginas visitadas y los productos comprados.
* Interés en el sitio web de referencia, incluidos los términos de búsqueda utilizados o los anuncios en los que se hizo clic.
* Interés en otros sitios; se determina con herramientas como Spyjax.
* Fidelidad del visitante; duración de la visita, frecuencia de las visitas.

**Características demográficas** - Son características de población seleccionadas, incluidas:

* Edad
* Ingresos
* Tamaño de familia
* Estado civil
* Sexo
* Lugar de residencia

**Características derivadas**: Algunas características demográficas son difíciles de determinar sin registro, pero se pueden obtener combinando características demográficas y de comportamiento.

Por ejemplo, si combina la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)), los propietarios del sitio podrán obtener características demográficas de los visitantes.

**Subsegmentos**: Un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.

**Página teaser**: Una página de teaser se dirige a una audiencia específica. Contiene contenido reutilizable que se puede utilizar en el párrafo de teaser.

**Campaña**: Una campaña es una colección de páginas de teaser y de páginas de marketing por correo electrónico como, por ejemplo, newsletters o invitaciones. Una campaña se suele llevar a cabo durante un período limitado y está precedida de otra campaña.

**Párrafo teaser**: Se trata de un párrafo que extrae el contenido de otra página que depende de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.

**Lista**: Una lista se extrae de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.

>[!NOTE]
>
>Consulte [Segmentación](/help/sites-administering/campaign-segmentation.md) para obtener más información sobre los segmentos en Adobe Experience Manager.
