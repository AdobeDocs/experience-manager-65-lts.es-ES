---
title: Implementación de prácticas recomendadas
description: Aprenda a implementar y mantener Adobe Experience Manager (AEM) de la forma más eficiente y eficaz posible.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
hide: true
hidefromtoc: true
exl-id: 4f830ee9-e0e3-48df-b67d-709258cb1991
source-git-commit: 013c9155817811913963ca514f7a6369b338d487
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 5%

---

# Implementación de prácticas recomendadas{#deploying-best-practices}

Las prácticas recomendadas de implementación describen cómo implementar o mantener Adobe Experience Manager (AEM) de la forma más eficiente y eficaz posible. Esta lista cada vez más extensa de temas incluye diversas áreas de AEM.

Las siguientes áreas tienen documentación disponible sobre la implementación y el mantenimiento de las prácticas recomendadas y recomendaciones:

* [Oak](#oak)
* [IU](#ui)
* [Rendimiento](#performance)

Para conocer las prácticas recomendadas sobre la administración, el desarrollo o la creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas de administración](/help/sites-administering/administer-best-practices.md)
* [Desarrollo de prácticas recomendadas](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)

En las tablas siguientes se describen y vinculan documentos específicos.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) es un repositorio de contenido jerárquico escalable y con buen rendimiento que es la base de AEM.

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidad, rendimiento y recuperación ante desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Rendimiento y escalabilidad</a></td>
   <td>Proporciona un documento técnico en el que se describen las características técnicas de agilidad, alto rendimiento y recuperación ante desastres con sonido</td>
  </tr>
  <tr>
   <td>Implementaciones recomendadas de Oak</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implementaciones recomendadas</a></td>
   <td>Describe escenarios de implementación</td>
  </tr>
  <tr>
   <td>Topología Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Prácticas recomendadas de topología Mongo</a></td>
   <td>Describe la topología mongo: cuándo utilizar qué topología.</td>
  </tr>
  <tr>
   <td>Opciones de almacén de datos</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuración de almacenes de datos y nodos</a></td>
   <td>En este documento se explican las prácticas recomendadas sobre el almacenamiento de datos binarios y nodos de contenido. Incluye información sobre el uso del almacén de datos de Amazon S3.</td>
  </tr>
  <tr>
   <td>Buscar en Oak</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para consultas e indexación</a><br /> </td>
   <td>Describe las prácticas recomendadas sobre cómo indexar contenido.</td>
  </tr>
 </tbody>
</table>

## IU {#ui}

Actualmente, AEM tiene dos interfaces de usuario: la clásica y la táctil en la misma versión. Por lo tanto, los clientes deben tomar una decisión sobre cuál utilizar durante la implementación del proyecto. El objetivo de este documento es ayudar a encontrar la opción correcta.

## Rendimiento {#performance}

Las prácticas recomendadas en cuanto a rendimiento se enumeran a continuación:

<table>
 <tbody>
  <tr>
   <td>Prácticas recomendadas para Quality Assurance</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Prácticas recomendadas para Quality Assurance</a></td>
   <td>Una visión general estandarizada de los problemas relacionados con la definición de un concepto de prueba específicamente para pruebas de rendimiento en su entorno <em>publish</em>. Esto es principalmente de interés para los ingenieros de control de calidad, gestores de proyectos y administradores de sistemas.</td>
  </tr>
  <tr>
   <td>Utilizar Dispatcher con una CDN</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es#using-dispatcher-with-a-cdn">Utilizar Dispatcher con una CDN</a></td>
   <td>Una red de entrega de contenido (CDN), como Akamai Edge Delivery o Amazon Cloud Front, ofrece contenido desde una ubicación cercana al usuario final.</td>
  </tr>
  <tr>
   <td>Optimización de rendimiento</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Optimización de rendimiento</a></td>
   <td>Un problema clave es el tiempo que tarda el sitio web en responder a las solicitudes de los visitantes.</td>
  </tr>
  <tr>
   <td>Pruebas de rendimiento</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Prácticas recomendadas para las pruebas de rendimiento</a></td>
   <td>Describe las prácticas recomendadas para ejecutar pruebas de rendimiento en una implementación de AEM.<br /> </td>
  </tr>
 </tbody>
</table>
