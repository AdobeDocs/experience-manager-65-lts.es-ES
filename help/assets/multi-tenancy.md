---
title: Inquilinos múltiples para colecciones, fragmentos y plantillas de fragmentos
description: Descubra cómo la función de varios alquileres le permite separar el contenido en el repositorio de CRX en función de la organización del cliente para evitar el acceso no autorizado.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

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
