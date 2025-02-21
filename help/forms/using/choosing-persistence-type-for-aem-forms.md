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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 100%

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
   <td>Compatible </td>
  </tr>
  <tr>
   <th><strong>Configuración del clúster</strong></th>
   <td>No compatible</td>
   <td>Compatible</td>
   <td>Compatible </td>
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

Para obtener la lista de microkernels admitidos, consulte los artículos [Requisitos técnicos de OSGi en AEM Forms](/help/sites-deploying/technical-requirements.md) o [AEM Forms en combinaciones de plataformas compatibles con JEE](/help/forms/using/aem-forms-jee-supported-platforms.md).

## Elegir entre Mongo o un Microkernel de base de datos relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Un entorno de AEM Forms escalable (agrupado) es un conjunto de dos o más instancias de autor activas configuradas horizontalmente. Puede elegir ejecutar más de una instancia de autor si un solo servidor, que admita todas las actividades de creación concurrentes, ya no es sostenible.

Solo se admite el tipo de persistencia MongoMK y RDBMK para AEM Forms escalable (agrupado) en un entorno JEE. La cantidad de servidores o el tamaño del entorno escalable varía según la instalación. Para obtener una lista de consideraciones y ejemplos, consulte los artículos [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md) y [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). También puede ponerse en contacto con el servicio de asistencia de AEM Forms para obtener información detallada sobre la planificación de la capacidad de AEM Forms con RDBMK y TarMK.
