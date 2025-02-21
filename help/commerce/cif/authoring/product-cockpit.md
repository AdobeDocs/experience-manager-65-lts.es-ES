---
title: Product Cockpit
description: Uso de la cabina de productos, que proporciona una visión general unificada de los catálogos de productos vinculados y el contenido asociado.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# Product Cockpit {#product-cockpit}

## Información general {#overview}

La cabina de productos proporciona una visión general unificada de los catálogos de productos vinculados y el contenido asociado. Todo el contenido asociado tiene vínculos para acceder rápidamente desde la cabina.

Los datos de productos clasificados incluyen cualquier mutación futura, como nuevas categorías, productos o propiedades actualizadas.

>[!NOTE]
>
>El término catálogo de productos es intercambiable con tienda de comercio, vista de tienda y expresiones similares.

## Configuración {#configuration}

Los catálogos de productos deben configurarse en AEM. Consulte [configurar el almacén y los catálogos](/help/commerce/cif/getting-started.md#catalog) para obtener más información.

La activación de las funciones de catálogo organizadas requiere autenticación. Consulte [Introducción](/help/commerce/cif/getting-started.md) para obtener más información.

>[!NOTE]
>
>Las funciones de catálogo organizadas solo están disponibles con Adobe Commerce y conectores de terceros que admitan la autenticación basada en tokens.

## Apertura de la cabina de productos {#opening-product-cockpit}

La forma más sencilla de acceder a la cabina del producto es a través del menú &quot;Commerce&quot; del menú principal de AEM. También es posible usar Omnisearch (buscar Commerce) o abrir `https://<yourAEMInstance>/commerce.html`.

![menú AEM](/help/commerce/cif/assets/aem-menu.png)

## Exploración de catálogos de productos {#browsing-product-catalogs}

La cabina de productos está organizada de forma jerárquica siguiendo la estructura del catálogo de productos. El primer nivel muestra el nivel de raíz del catálogo de todos los catálogos de productos configurados, incluida la información meta del backend de comercio.

![Catálogos configurados](/help/commerce/cif/assets/catalog-overview.png)

Al hacer clic en una categoría, se cargan los elementos secundarios de la categoría en la que se hizo clic.

![Categoría secundaria](/help/commerce/cif/assets/catalog-category-children.png)

Al hacer clic en un producto, se cargan variaciones de productos si están disponibles.

![Variaciones de productos](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>Los datos del catálogo de productos en AEM son datos que se recuperan en tiempo real a través del punto de conexión comercial configurado. No se almacenan datos del catálogo de productos en AEM.

## Buscando catálogos de productos {#searching-product-catalog}

Se proporciona una búsqueda de texto completo sobre el catálogo de productos completo en la pestaña del filtro izquierdo para encontrar productos rápidamente.

![búsqueda](/help/commerce/cif/assets/search-cockpit.png)

## Exploración del catálogo de productos escalonado {#staged-product-catalogs}

De forma predeterminada, la cabina de productos muestra los datos del catálogo de productos en directo. El uso del &quot;CATÁLOGO CLASIFICADO&quot; en la pestaña del filtro izquierdo carga el catálogo de productos para cualquier fecha seleccionada.

![catálogo ensayado](/help/commerce/cif/assets/staged-cockpit.png)

## Propiedades del catálogo de productos {#catalog-properties}

Al hacer clic en el icono de propiedades de un producto o categoría, se abre la vista de propiedades del objeto seleccionado. Las propiedades abiertas de una variante de producto son iguales para abrir las propiedades de producto principales.

### Fichas de Commerce {#tabs}

Las pestañas general y de variante muestran propiedades de comercio predefinidas que provienen del backend del comercio. Estos datos (incl. variantes) son datos de solo lectura en AEM, ya que el sistema de registro es el backend de commerce. La pestaña variante solo aparece para productos con variantes y muestra una lista de todas las variantes.

![propiedades de catálogo](/help/commerce/cif/assets/catalog-properties.png)

### Pestañas de contenido de AEM {#content-tabs}

Estas pestañas, agrupadas por tipos de contenido de AEM (fragmentos de experiencias, fragmentos de contenido, Assets asociado), muestran contenido de AEM asociado al objeto de comercio. La acción &quot;Ver detalles&quot; abre una nueva pestaña del explorador con el contenido seleccionado.

![propiedades de contenido](/help/commerce/cif/assets/content-properties.png)
