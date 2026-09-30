---
title: Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL
description: Obtenga información sobre cómo actualizar los fragmentos de contenido para el filtrado optimizado de GraphQL en Adobe Experience Manager para la entrega de contenido sin encabezado.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
exl-id: 40211033-7084-4117-a3e2-73e504283266
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 38%
---
# Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para optimizar el rendimiento de los filtros de GraphQL, ejecute un procedimiento para actualizar los fragmentos de contenido.

>[!NOTE]
>
>Después de actualizar los fragmentos de contenido, puede seguir las recomendaciones de [Optimización de las consultas de GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Requisitos previos {#prerequisites}

Asegúrese de que cuenta con un mínimo de 6.5.17.0 versiones de AEM.

## Actualización de los fragmentos de contenido {#updating-content-fragments}

Para ejecutar el procedimiento, siga estos pasos:

1. [Configure las opciones de OSGi](/help/sites-deploying/configuring-osgi.md) para la **Configuración del trabajo de migración de fragmentos de contenido**:

   ![Configuración del trabajo de migración de fragmentos de contenido OSGi](assets/cfm-graphql-update-01.png "Configuración del trabajo de migración de fragmentos de contenido OSGi")

1. En el cuadro de diálogo, establezca estos dos parámetros de la siguiente manera:

   * **ContentFragmentMigration:Enabled**: `1`
   * **ContentFragmentMigration:Enforce**: `1`

1. **Guardar** las especificaciones: se inicia el procedimiento de actualización.

1. Espere hasta que se complete el procedimiento. El procedimiento se completa cuando la propiedad `cfGlobalVersion` aparece en `/content/dam` y se establece en `1`.

1. Vuelva a la configuración de OSGi para desactivar el procedimiento.

   En el cuadro de diálogo de la **Configuración del trabajo de migración de fragmentos de contenido** establezca estos dos parámetros de la siguiente manera:

   * **ContentFragmentMigration:Enabled**: `0`
   * **ContentFragmentMigration:Enforce**: `0`

## Limitaciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* Optimizar el rendimiento de los filtros de GraphQL solo será posible después de una actualización completa de todos los fragmentos de contenido (indicada por la presencia de la propiedad `cfGlobalVersion` para el nodo JCR `/content/dam`).

* Si los fragmentos de contenido se importan desde un paquete de contenido (mediante `crx/de`) después de ejecutar el procedimiento de actualización, esos fragmentos de contenido no se tendrán en cuenta en los resultados de la consulta de GraphQL hasta que se vuelva a ejecutar el procedimiento de actualización.
