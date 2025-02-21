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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

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
