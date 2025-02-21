---
title: Migración al complemento de AEM Commerce integration framework (CIF)
description: Migración al complemento AEM Commerce integration framework (CIF) desde una versión antigua.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%

---

# Guía de migración para el complemento de Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de complementos de Experience Manager.

## Complemento de CIF

El complemento de CIF está disponible para AEM 6.5 a través de [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas funciones que el complemento de CIF para Experience Manager as a Cloud Service.

Consulte [Introducción al contenido de AEM y Commerce](getting-started.md).

Para apoyar proyectos que implementen CIF, Adobe proporciona [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components).

## Catálogo de productos

El complemento de CIF no admite la importación de datos del catálogo de productos. Al usar las entidades de seguridad de complementos de CIF, las solicitudes de productos y catálogos se realizan bajo demanda mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Experiencias del catálogo de productos con el procesamiento en AEM

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. El complemento de CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante plantillas de catálogo de AEM. Ya no se requiere replicación de datos o páginas de productos.

## Interacción de datos y compras no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complemento al carro, búsqueda) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. Elimine cualquier llamada en la que AEM sea solo un proxy.
