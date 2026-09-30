---
title: ¿Qué entornos de prueba son necesarios?
description: Se deben considerar varios entornos como parte de las pruebas
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: f74fbf2b-62bb-4fac-9ecb-5ace90ba0275
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%
---
# ¿Qué entornos de prueba son necesarios?{#which-test-environments-will-be-needed}

Para definir qué configuraciones se deben probar, se debe tener en cuenta lo siguiente:

**Desarrollo** - Para Unidad y ciertas pruebas de integración.

**Pruebas** - Para la mayoría de las pruebas.

**Activo**: para las pruebas de esfuerzo y rendimiento finales. También para pruebas de aceptación con el cliente.

Decida qué instancias necesita y dónde (normalmente al menos una de cada una para todos los niveles de prueba):

**Autor**: esta instancia permite a los autores introducir y publicar contenido.

**Publicar**: esta instancia presenta el sitio web en su forma publicada para que los visitantes puedan acceder a él.

Probado con Dispatcher.

Por último, debe tenerse en cuenta el hardware real: cualquier prueba de rendimiento debe realizarse en un sistema lo más cerca posible del entorno en directo final. Por este motivo, también se recomienda dividir el lanzamiento del proyecto en un:

**Lanzamiento suave**: disponibilidad reducida; lo que permite tiempo para pruebas de rendimiento, ajuste y optimización en condiciones realistas en el entorno de producción.

**Lanzamiento duro** - Disponibilidad completa.
