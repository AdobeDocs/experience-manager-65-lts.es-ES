---
title: Admin Consoles
description: Aprenda a utilizar las Admin Consoles disponibles en Adobe Experience Manager.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 9cc6e4b6-7170-4c9a-a2c0-6ba4603cfd17
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 2%
---
# Admin Consoles{#admin-consoles}

De forma predeterminada, la capacidad de cambiar a la IU clásica mediante Admin Consoles está desactivada. Por lo tanto, ya no se muestran los iconos emergentes que se veían al pasar el ratón por encima de ciertos iconos de la consola, lo que permitía el acceso a la IU clásica.

Cada consola que tiene una versión de IU clásica en `/libs/cq/core/content/nav` se puede volver a habilitar individualmente para que la opción **IU clásica** aparezca una vez más sobre el icono de la consola cuando se pasa el ratón por encima.

En este ejemplo, vuelve a habilitar la IU clásica para la consola Sitios.

1. Con CRXDE Lite, busque el nodo correspondiente a la Admin Console para la que desea volver a habilitar la IU clásica. Se encuentran en:

   `/libs/cq/core/content/nav`

   Por ejemplo

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleccione el nodo correspondiente a la consola para la que desea volver a habilitar la IU clásica. Para este ejemplo, está volviendo a habilitar la IU clásica para la consola Sitios.

   `/libs/cq/core/content/nav/sites`

1. Cree una superposición con la opción **Nodo de superposición**; por ejemplo:

   * **Ruta**: `/apps/cq/core/content/nav/sites`
   * **Ubicación de superposición**: `/apps/`
   * **Tipos de nodos coincidentes**: activo (seleccione la casilla de verificación)

1. Agregue la siguiente propiedad booleana al nodo superpuesto:

   `enableDesktopOnly = {Boolean}true`

1. La opción **IU clásica** vuelve a estar disponible como opción emergente en Admin Console.

   ![opción de ventana emergente de IU clásica](assets/syui-01-2019-02-27-15-16-55.png)

Repita estos pasos para cada consola para la que desee volver a habilitar el acceso a la versión de la IU clásica.
