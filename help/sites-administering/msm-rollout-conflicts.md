---
title: Conflictos de despliegue de MSM
description: Aprenda a lidiar con los conflictos de despliegue del Administrador de varios sitios.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 18%

---

# Conflictos de despliegue de MSM{#msm-rollout-conflicts}

Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre en la rama del modelo y en una rama de Live Copy dependiente.

Estos conflictos deben gestionarse y resolverse en el momento del despliegue.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en las ramas de modelo y Live Copy), MSM le permite definir cómo (o incluso si) deben gestionarse.

Para garantizar que el despliegue no esté bloqueado, las definiciones posibles pueden incluir las siguientes:

* qué página (modelo o live copy) tiene prioridad durante el despliegue,
* qué páginas se cambian de nombre (y cómo),
* cómo afecta esto a cualquier contenido publicado.

  El comportamiento predeterminado de Adobe Experience Manager (AEM) (predeterminado) es que el contenido publicado no se ve afectado. Por lo tanto, si se ha publicado una página creada manualmente en la rama de Live Copy, ese contenido se sigue publicando después de la gestión y el despliegue del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflicto personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Escenario de ejemplo {#example-scenario}

En las secciones siguientes, debe utilizar el ejemplo de una nueva página `b`, creada tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

* modelo: `/b`

  Una página maestra; con una página secundaria, bp-level-1.

* live copy: `/b`

  Una página creada manualmente en la rama de Live Copy; con una página secundaria, `lc-level-1`.

   * Se activó al publicar como `/b`, junto con la página secundaria.

**Antes del despliegue**

<table>
 <tbody>
  <tr>
   <td><strong>modelo antes del despliegue</strong></td>
   <td><strong>live copy antes del despliegue</strong></td>
   <td><strong>publicar antes del despliegue</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (creado en la rama del modelo, listo para su despliegue)<br /> </td>
   <td><code>b</code><br /> <br /> (creado manualmente en la rama de live copy)<br /> </td>
   <td><code>b</code><br /> <br /> (contiene el contenido de la página b que se creó manualmente en la rama de live copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (creado manualmente en la rama de live copy)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (contiene el contenido de la página <br /> child-level-1 que se creó manualmente en la rama de live copy)</td>
  </tr>
 </tbody>
</table>

## Administrador de despliegue y gestión de conflictos {#rollout-manager-and-conflict-handling}

El administrador de despliegue le permite activar o desactivar la administración de conflictos.

Esto se hace con la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **Administrador de despliegue de CQ WCM por día**:

* **Controlar conflictos con páginas creadas manualmente**:

  ( `rolloutmgr.conflicthandling.enabled`)

  Se establece en true si el administrador de despliegue debe gestionar los conflictos de una página creada en Live Copy con un nombre que exista en el modelo.

AEM tiene [comportamiento predefinido cuando se ha desactivado la administración de conflictos](#behavior-when-conflict-handling-deactivated).

## Controladores de conflictos {#conflict-handlers}

AEM utiliza controladores de conflictos para resolver cualquier conflicto de páginas que surja al desplegar contenido desde un modelo a una Live Copy. Cambiar el nombre de las páginas es un método (el habitual) para resolver estos conflictos. Puede haber más de un controlador de conflictos en funcionamiento para permitir una selección de comportamientos diferentes.

AEM proporciona lo siguiente:

* El [controlador de conflictos predeterminado](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* La posibilidad de implementar un [controlador personalizado](#customized-handlers).
* Mecanismo de clasificación de servicios que permite establecer la prioridad de cada controlador individual. Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflictos predeterminado:

* Se llama `ResourceNameRolloutConflictHandler`

* Con este controlador, la página de modelo tiene prioridad.
* La clasificación de servicio de este controlador se establece en un nivel bajo (es decir, por debajo del valor predeterminado para la propiedad `service.ranking`), ya que se supone que los controladores personalizados necesitan una clasificación más alta. Sin embargo, la clasificación no está al nivel mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflictos da prioridad al modelo. La página Live Copy `/b` se ha movido (dentro de la rama de Live Copy) a `/b_msm_moved`.

* live copy: `/b`

  Se mueve (dentro de la Live Copy) a `/b_msm_moved`. Esto actúa como una copia de seguridad y garantiza que no se pierda contenido.

   * `lc-level-1` no se mueve.

* modelo: `/b`

  Se despliega en la página de Live Copy `/b`.

   * `bp-level-1` se ha implementado en la Live Copy.

**Después del despliegue**

<table>
 <tbody>
  <tr>
   <td><strong>modelo tras el despliegue</strong></td>
   <td><strong>live copy después del despliegue</strong><br /> </td>
   <td></td>
   <td><strong>Live Copy después del despliegue</strong><br /> <br /> <br /> </td>
   <td><strong>publicar después del despliegue</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (tiene el contenido de la página de modelo b que se desplegó)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (tiene el contenido de la página b que se creó manualmente en la rama de live copy)</td>
   <td><code>b</code><br /> <br /> (sin cambios; contiene el contenido de la página original b que se creó manualmente en la rama de live copy y ahora se llama b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (sin cambios)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (sin cambios)</td>
  </tr>
 </tbody>
</table>

### Controladores personalizados {#customized-handlers}

Los controladores de conflicto personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflicto personalizados pueden tener lo siguiente:

* Nombrado según sus necesidades.
* Desarrollado/configurado según sus necesidades; por ejemplo, puede desarrollar un controlador para que la página de Live Copy tenga prioridad.
* Diseñado para configurarse con la [configuración OSGi](/help/sites-deploying/configuring-osgi.md); en particular:

   * **Clasificación del servicio**:

     Define el orden relacionado con otros controladores de conflictos ( `service.ranking`).

     El valor predeterminado es 0.

### Comportamiento Cuando Se Desactiva La Gestión De Conflictos {#behavior-when-conflict-handling-deactivated}

Si [desactiva manualmente la administración de conflictos](#rollout-manager-and-conflict-handling), AEM no realiza ninguna acción en ninguna página en conflicto (las páginas que no entran en conflicto se despliegan según lo esperado).

>[!CAUTION]
>
>AEM no da ninguna indicación de que se estén ignorando los conflictos, ya que este comportamiento debe configurarse explícitamente, por lo que se supone que es el comportamiento requerido.

En este caso, la Live Copy tiene prioridad. La página de modelo `/b` no se copia y la página de Live Copy `/b` no se modifica.

* modelo: `/b`

  No se copia en absoluto y se ignora.

* live copy: `/b`

  Lo mismo.

<table>
 <caption>
   Después del despliegue
 </caption>
 <tbody>
  <tr>
   <td><strong>modelo tras el despliegue</strong></td>
   <td><strong>Live Copy después del despliegue</strong><br /> <br /> <br /> </td>
   <td><strong>publicar después del despliegue</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (sin cambios; tiene el contenido de la página b que se creó manualmente en la rama de live copy)</td>
   <td><code>b</code><br /> <br /> (sin cambios; contiene el contenido de la página b que se creó manualmente en la rama de live copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (sin cambios)</td>
   <td><code> /lc-level-1</code><br /> <br /> (sin cambios)</td>
  </tr>
 </tbody>
</table>

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
