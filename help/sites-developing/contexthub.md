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
exl-id: c7c42bcd-d90a-430a-bbcd-b104d0670ebf
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '285'
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
