---
title: Seleccionar un tipo de persistencia para una instalación de AEM Forms
description: Elija bien un tipo de persistencia. Le ayudará a crear un entorno de AEM Forms eficiente y escalable.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 8ddfc767-08a5-4045-86a7-97150e028a14
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 96%
---
# Seleccionar un tipo de persistencia para una instalación de AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Elija bien un tipo de persistencia. Le ayudará a crear un entorno de AEM Forms eficiente y escalable.

La persistencia es el método para almacenar contenido en los almacenes físicos. Define la estructura de datos real y el mecanismo de almacenamiento de los mismos. Los microkernels actúan como administradores de persistencia en AEM Forms. AEM Forms admite persistencia (MicroKernals) de tipo TarMK, MongoMK y RDBMK. Puede elegir un tipo de persistencia para AEM Forms según el propósito y el tipo de implementación (un solo servidor, una granja o un clúster) de una instancia de AEM Forms.

>[!NOTE]
>
>LiveCycle ES4 SP1 utiliza la persistencia TarPM para almacenar contenido.

La siguiente tabla muestra todos los tipos de persistencia admitidos, así como varios parámetros que le ayudarán a elegir un tipo de persistencia para su entorno:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo de instalación / Coste</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuración independiente</strong></th>
   <td>Compatibilidad<br /> </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <th><strong>Configuración del clúster</strong></th>
   <td>No compatible</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <th><strong>Coste de licencia</strong></th>
   <td>Incluido con AEM </td>
   <td>Licencia por separado requerida</td>
   <td>Licencia por separado requerida</td>
  </tr>
 </tbody>
</table>

TarMK está diseñado para el rendimiento, mientras que MongoMK y RDBMK están diseñados para la escalabilidad. Adobe recomienda encarecidamente TarMK como tecnología de persistencia predeterminada para todos los escenarios de implementación de AEM Forms, tanto para instancias de autor como de publicación, excepto en los casos de uso descritos en la sección [Elegir entre Mongo o un Microkernel de base de datos relacional sobre TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para obtener la lista de microkernels admitidos, consulte [AEM Forms sobre los requisitos técnicos de OSGi](/help/sites-deploying/technical-requirements.md) <!--or [AEM Forms on JEE supported platform combinations](/help/forms/using/aem-forms-jee-supported-platforms.md) articles-->.

## Elegir entre Mongo o un Microkernel de base de datos relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un entorno de AEM Forms escalable (agrupado) es un conjunto de dos o más instancias de autor activas configuradas horizontalmente. Puede elegir ejecutar más de una instancia de autor si un solo servidor, que admita todas las actividades de creación concurrentes, ya no es sostenible.

<!--Only MongoMK and RDBMK persistence type are supported for a scalable (clustered) AEM Forms on JEE environment.-->

La cantidad de servidores o el tamaño del entorno escalable varía según la instalación. Para obtener una lista de consideraciones y ejemplos, consulte los artículos [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) y [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). También puede ponerse en contacto con el servicio de asistencia de AEM Forms para obtener información detallada sobre la planificación de la capacidad de AEM Forms con RDBMK y TarMK.
