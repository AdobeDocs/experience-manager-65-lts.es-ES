---
title: Introducción a AEM Content y Commerce
description: Obtenga información sobre cómo implementar un proyecto de AEM Content and Commerce.
topics: Commerce
feature: Commerce Integration Framework
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 4%

---

# Introducción a AEM Content y Commerce {#start}

Para empezar a usar AEM Content y Commerce, debe instalar el complemento AEM Content y Commerce para AEM 6.5.

## Requisito mínimo de software

Se requiere [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) 7 o posterior.

## Incorporación {#onboarding}

La incorporación de Contenido de AEM y Commerce es un proceso de dos pasos:

1. Instalación del complemento AEM Content and Commerce para AEM 6.5

2. Conecte AEM con su solución de comercio

### Instalación del complemento AEM Content and Commerce para AEM 6.5 {#install-add-on}

Descargue e instale el complemento AEM Commerce para AEM 6.5 desde el portal [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

Inicie e instale el paquete de servicio de AEM 6.5 necesario. Se recomienda instalar el último Service Pack disponible.

>[!NOTE]
>
>Esto lo hará el CSE para los clientes de AEM Managed Service.

### Conectar AEM a su sistema Commerce {#connect}

AEM se puede conectar a cualquier sistema comercial que tenga un punto final de GraphQL accesible para AEM. Estos extremos suelen estar disponibles públicamente o pueden conectarse a través de conexiones privadas VPN o locales, según la configuración individual del proyecto.

De forma opcional, se puede proporcionar un encabezado de autenticación para utilizar funciones de CIF adicionales que requieran autenticación.

Deben ajustarse los proyectos generados por [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) y [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) que ya están incluidos en la [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json).

Reemplace el valor de `url` en `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` por el extremo GraphQL de su sistema de comercio. Esta configuración se puede realizar a través de la consola OSGI o implementando la configuración OSGI a través del proyecto. Se admiten diferentes configuraciones para sistemas de ensayo y producción mediante diferentes modos de ejecución de AEM.

El complemento AEM Content and Commerce y los componentes principales de CIF utilizan conexiones del lado del servidor y del lado del cliente de AEM. Los componentes principales de CIF del lado del cliente y las herramientas de creación de complementos de CIF se conectan de forma predeterminada a `/api/graphql`. Esto se puede ajustar a través de la configuración de CIF Cloud Service si es necesario (consulte a continuación).

El complemento de CIF proporciona un servlet proxy de GraphQL en `/api/graphql` que se puede usar opcionalmente para [desarrollo local](develop.md). Para implementaciones de producción, se recomienda configurar un proxy inverso al extremo de GraphQL de comercio a través de AEM Dispatcher o en otras capas de red (como CDN).

## Configuración de tiendas y catálogos {#catalog}

El complemento y los [componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) se pueden usar en varias estructuras del sitio de AEM conectadas a diferentes tiendas de comercio (o vistas de tiendas, etc.). De forma predeterminada, el complemento de CIF se implementa con una configuración predeterminada que se conecta a la tienda y al catálogo predeterminados de Adobe Commerce.

Esta configuración se puede ajustar para el proyecto a través de la configuración de CIF Cloud Service siguiendo estos pasos:

1. En AEM, vaya a Herramientas > Cloud Services > Configuración de CIF

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración a través de la barra de acciones

![Configuración de CIF Cloud Services](/help/commerce/cif/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Esto debería permanecer en modo predeterminado.
- Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
- Ruta del proxy de GraphQL: la ruta URL que utiliza el proxy de GraphQL en AEM para las solicitudes de proxy al extremo de GraphQL backend de comercio.

  >[!NOTE]
  >
  >En la mayoría de las configuraciones, no se debe cambiar el valor predeterminado `/api/graphql`. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.

- Habilitar la compatibilidad con UID del catálogo: habilite la compatibilidad con UID en lugar del ID en las llamadas de GraphQL del backend comercial.

  >[!NOTE]
  >
  >La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda.

  >[!CAUTION]
  >
  >A partir de la versión 2.0.0 de los componentes principales de CIF, se quitó la compatibilidad con `id` y se reemplazó con `uid`. Si su proyecto utiliza los componentes principales de CIF versión 2.0.0, debe habilitar la compatibilidad con Catalog UID y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz de catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

Para obtener configuraciones más complejas que utilicen varias estructuras de sitio de AEM combinadas con distintos catálogos comerciales, consulte el tutorial [Configuración de varias tiendas Commerce](configuring/multi-store-setup.md).

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md)
