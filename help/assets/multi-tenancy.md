---
title: Inquilinos múltiples para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite separar el contenido en el repositorio de CRX en función de la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
role: Developer,Admin,Leader
feature: Collections
solution: Experience Manager, Experience Manager Assets
exl-id: 39e14f89-8e60-4b5e-8859-d69ebd51864e
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c73531c3-4c05-471e-beff-cefb35857910
    internal-label: Collections
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%
---
# Inquilinos múltiples para colecciones, fragmentos y plantillas de fragmentos {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La función de varios alquileres le permite separar el contenido en CRX en función del prefijo de la organización y el ID de la organización para proteger el contenido del acceso no autorizado de usuarios de otras organizaciones.

[!DNL Adobe Experience Manager Assets] almacena los datos de cada organización en una ruta de acceso diferente. Cada ruta específica de la organización se identifica mediante el prefijo y el ID de organización
que se incluye en la ubicación tradicional, donde se almacenan distintos tipos de recursos en CRX.

Por ejemplo, si crea una carpeta denominada `Demo`, los recursos de [!DNL Experience Manager] almacenan tradicionalmente la carpeta en `../content/dam/Demo`. Con la opción de inquilinos múltiples habilitada, ahora puede almacenar los datos en `../content/dam/<organization prefix>/<organization id>Demo`

Por ejemplo, si para [!DNL Adobe Marketing Cloud] usuarios de [!DNL Assets] (bajo demanda) asignados a la organización `aodpremium`, puede utilizar la característica de inquilinos múltiples para configurar la ruta de acceso de `../content/dam/<mac>/<aodpremium>Demo` y separar su contenido. En este ejemplo, `mac` es el prefijo de organización y `aodpremium` es el identificador de organización.

En función de la organización y el ID del usuario, esta ruta de acceso completa se muestra en la interfaz [!DNL Assets] y en varios asistentes, incluidos los asistentes para crear movimiento y fragmentos de código para aplicar la segregación.

La función de inquilinos múltiples le permite separar los siguientes tipos de activos y componentes:

* Colecciones
* Colecciones públicas
* Catálogos (incluido el asistente Agregar/Seleccionar página)
* Plantillas
* Plantillas de fragmento
* Lightbox
