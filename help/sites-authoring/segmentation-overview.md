---
title: Explicación de la segmentación al crear una campaña
description: La segmentación es una consideración clave al crear una campaña.
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
exl-id: 7167c672-8d24-4493-aff6-b5b453074bff
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 48%
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

**Pista**: Una pista es una característica o propiedad de un visitante que se puede usar para determinar el abono a un segmento específico.

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
* Género
* Lugar de residencia

**Características derivadas**: Algunas características demográficas son difíciles de determinar sin registro, pero se pueden obtener combinando características demográficas y de comportamiento.

Por ejemplo, si combina la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)), los propietarios del sitio podrán obtener características demográficas de los visitantes.

**Subsegmentos**: Un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.

**Página teaser**: Una página de teaser se dirige a un público específico. Contiene contenido reutilizable que se puede utilizar en el párrafo de teaser.

**Campaña**: Una campaña es una colección de páginas de teaser y de páginas de marketing por correo electrónico como, por ejemplo, newsletters o invitaciones. Una campaña se suele llevar a cabo durante un período limitado y está precedida de otra campaña.

**Párrafo teaser**: Se trata de un párrafo que extrae el contenido de otra página que depende de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.

**Lista**: Una lista se extrae de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.

>[!NOTE]
>
>Consulte [Segmentación](/help/sites-administering/campaign-segmentation.md) para obtener más información sobre los segmentos en Adobe Experience Manager.
