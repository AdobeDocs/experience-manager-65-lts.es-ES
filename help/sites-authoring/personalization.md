---
title: Personalización y segmentación de contenido
description: Descubra cómo Adobe Experience Manager 6.5 LTS puede crear contenido personalizado.
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
exl-id: da8a1341-55a9-46bb-b78d-ced79e22e87e
source-git-commit: 8a4f8ce12a67985f659d0e565f2950c97179bc01
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 36%

---

# Personalización y segmentación de contenido {#personalization}

## Personalización y segmentación de contenido {#personalization-and-content-targeting}

AEM proporciona un marco de herramientas para crear contenido dirigido y presentar experiencias personalizadas.

## Modo Targeting {#targeting-mode}

[Contenido segmentado por el autor mediante el modo de Segmentación de AEM. ](/help/sites-authoring/content-targeting-touch.md) En el modo segmentación y el componente de Target se proporcionan las herramientas necesarias para crear contenido para las experiencias de las actividades de marketing.

## Actividades {#activities}

Las actividades definen y organizan los esfuerzos de marketing. Las actividades comprenden las audiencias a las que se dirige y el período de tiempo en que se aplica el objetivo.

Por ejemplo, el catálogo de productos We.Retail incluye teasers que destacan los productos de temporada. La actividad Deportes de verano define los segmentos de marketing a los que se dirigen los teasers durante los meses de verano.

Las actividades también identifican el [motor de segmentación](/help/sites-authoring/personalization.md#targeting-engine) que utilizan sus páginas.

Use la [consola Actividades](/help/sites-authoring/activitylib.md) para crear y administrar las actividades de sus marcas. También puede crear actividades a medida que [crea contenido de destino](/help/sites-authoring/content-targeting-touch.md).

## Experiencias {#experiences}

Para cada actividad, se definen una o más experiencias que identifican los públicos a los que se va a dirigir. AEM permite controlar el contenido de que consta cada experiencia.

Las audiencias se basan en segmentos de marketing creados en AEM o Adobe Target. Cuando un visitante abre una página web, la lógica de la página determina la audiencia a la que pertenece y muestra el contenido que ha creado para esa audiencia.

Por ejemplo, una actividad define las experiencias para dos públicos independientes: mujeres mayores de 30 años y mujeres menores de 30 años. La página para mujeres del sitio web de We.Retail muestra diferentes productos para cada experiencia.

Las experiencias se definen para una actividad. Puede usar la [consola Actividades](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) o el [modo de segmentación](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) para agregar experiencias a una actividad.

## Ofertas {#offers}

Una oferta es contenido que aparece en una ubicación de una página para una experiencia. Utilice distintas ofertas para diferentes experiencias a fin de maximizar la eficacia del contenido para las audiencias.

Por ejemplo, la página para mujeres del sitio web de muestra de We.Retail puede utilizar ofertas para la imagen de teaser que aparece en la parte superior de la página. Se utiliza una oferta diferente como teaser para la experiencia de mujeres mayores de 30 años y de mujeres menores de 30 años.

Use la consola [Ofertas](/help/sites-authoring/offerlib.md) para crear ofertas que pueda usar en varias experiencias. Cree ofertas de un solo uso o agregue ofertas desde una biblioteca de ofertas al [crear contenido de destino](/help/sites-authoring/content-targeting-touch.md).

## Motor de segmentación {#targeting-engine}

El motor de segmentación es el mecanismo que determina la lógica para el contenido de destino. Las [actividades](/help/sites-authoring/activitylib.md) se configuran para utilizar uno de estos dos motores de segmentación disponibles: AEM y Adobe Target.

### AEM {#aem}

AEM proporciona un motor de segmentación integrado que procesa las solicitudes de páginas y determina el contenido que se va a mostrar. Al utilizar el motor de segmentación de AEM, el uso se limita a los segmentos que se crean en AEM para definir los públicos de las experiencias.

### Adobe Target {#adobe-target}

El motor de segmentación de Adobe Target hace que la información recopilada de las visitas a la página sean rastreadas en Adobe Target.

* Al utilizar este motor de segmentación, se usan los segmentos importados de Adobe Target para definir los públicos para las experiencias.
* Las actividades que utilizan el motor de Adobe Target se [sincronizan con Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Puede utilizar este motor cuando se haya [integrado con Adobe Target](/help/sites-administering/opt-in.md).
