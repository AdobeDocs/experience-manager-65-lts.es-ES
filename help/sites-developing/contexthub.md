---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

>[!NOTE]
>
>La [implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub y puede servir como referencia al integrar ContextHub en su propio proyecto.

>[!CAUTION]
>
>La ruta que contiene la configuración de ContextHub de ejemplo que usa la [implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) solo debe usarse como referencia para crear su propia configuración.
>
>No utilice en un proyecto como su propia configuración de ContextHub.

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. De este modo, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona [tipos de almacén de muestra](/help/sites-developing/ch-samplestores.md).
* Use las consolas de AEM para [crear tiendas](ch-configuring.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de almacén personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Los desarrolladores pueden [acceder a los datos del almacén](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) a través de JavaScript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede usar la API de JavaScript para [determinar los segmentos resueltos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentación {#presentation}

La [barra de herramientas de ContextHub](/help/sites-authoring/ch-previewing.md) permite a los especialistas en marketing y a los autores ver y manipular los datos del almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas consiste en grupos de módulos de interfaz de usuario que proporcionan acceso a los almacenes de ContextHub.

Cada módulo de IU de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona [tipos de módulos de ejemplo](/help/sites-developing/ch-samplemodules.md).
* Use las consolas de AEM para [agregar módulos de interfaz de usuario](ch-configuring.md#adding-a-ui-module) y [agruparlos en modos de interfaz de usuario](ch-configuring.md#adding-a-ui-mode).

* Los desarrolladores pueden [crear tipos de módulos personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [agregar el componente ContextHub a la página](/help/sites-developing/ch-adding.md).
