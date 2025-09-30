---
title: Migración al complemento de AEM Commerce integration framework (CIF)
description: Migración al complemento AEM Commerce integration framework (CIF) desde una versión antigua.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 847c33c1-17d6-447a-9f2c-91f2a81a3f04
source-git-commit: 981b175b039fd7ffbddf558a77d2da2fed52ad79
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 4%

---

# Guía de migración para el complemento de Experience Manager {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de complementos de Experience Manager.

## Complemento de CIF

El complemento de CIF está disponible a través de [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&2_group.propertyvalues.operation=equals&2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5-lts&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=16). Es compatible y proporciona las mismas funciones que el complemento de CIF para Experience Manager as a Cloud Service.

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
