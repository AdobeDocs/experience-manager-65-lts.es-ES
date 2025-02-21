---
title: Solución de problemas y preguntas más frecuentes sobre MSM
description: Descubra cómo solucionar los problemas más comunes relacionados con MSM y obtenga respuestas a las preguntas más comunes relacionadas con MSM.
feature: Multi Site Manager
role: Admin
solution: Experience Manager, Experience Manager Sites
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 58%

---

# Solución de problemas y preguntas más frecuentes sobre MSM {#troubleshooting-msm}

## Primeros pasos en la solución de problemas {#first-steps}

Si está experimentando lo que cree que es un comportamiento incorrecto o un error en MSM, antes de comenzar y realizar la solución de problemas detallada, asegúrese de lo siguiente:

* Lea las [Preguntas más frecuentes sobre MSM](#faq), pues es posible que sus problemas o preguntas ya se hayan solucionado allí.
* Lea el [artículo de prácticas recomendadas de MSM](msm-best-practices.md), ya que se ofrecen varias sugerencias y aclaraciones sobre algunos conceptos erróneos.

## Búsqueda de información avanzada sobre el modelo y el estado de Live Copy {#advanced-info}

MSM registra varios servlets que se pueden solicitar con selectores en las direcciones URL de los recursos. Las utiliza la interfaz de usuario, pero también se pueden solicitar directamente para ver estados de MSM calculados avanzados y directamente adicionales para sus páginas:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Utilícelo en una página de modelo para recuperar la lista de todas las Live Copies vinculadas a ella, con información del estado de Live Copy adicional.
   * por ejemplo:
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Utilícelo en páginas de Live Copy para recuperar información avanzada sobre su conexión con sus páginas de modelo. Si la página no es una Live Copy, no se devuelve nada.
   * por ejemplo:
     `http://localhost:4502/content/wknd/ca/en.msm.json`

Estos servlets generan mensajes de registro de depuración a través del registrador `com.day.cq.wcm.msm` que también puede ser útil.

## Comprobación de información específica de MSM en el repositorio {#checking-repo}

Los servlets anteriores devolvían información calculada basada en los nodos y mezclas específicos de MSM. La información se almacena en el repositorio de la siguiente manera.

* `cq:LiveSync` tipo de mezcla
   * Esto está configurado en los nodos `jcr:content` y define las páginas raíz de Live Copy.
   * Estas páginas tienen un nodo secundario `cq:LiveSyncConfig` de tipo `cq:LiveCopy` que contiene información básica y obligatoria sobre Live Copy a través de las siguientes propiedades:
      * `cq:master` apunta a la página de modelo de Live Copy.
      * `cq:rolloutConfigs` indica las configuraciones de despliegue activas aplicadas a Live Copy.
      * `cq:isDeep` es verdadero si las páginas secundarias de esta página raíz de Live Copy están incluidas en Live Copy.
* `cq:LiveRelationship` tipo de mezcla
   * Cualquier página de Live Copy tiene este tipo de mezcla en su nodo`jcr:content`.
   * Si no es así, la página en algún momento se ha separado o creado manualmente mediante la interfaz de creación fuera de una acción de Live Copy (crear o desplegar).
* `cq:LiveSyncCancelled` tipo de mezcla
   * Se ha añadido a nodos `jcr:content` de páginas de Live Copy que se suspendieron.
   * Si la suspensión es efectiva también para páginas secundarias, `cq:isCancelledForChildren` la propiedad se establece en true en el mismo nodo.

La información presente en estas propiedades debe reflejarse en la interfaz de usuario, sin embargo, al solucionar problemas, puede resultar útil observar el comportamiento de MSM directamente en el repositorio a medida que se producen acciones de MSM.

Conocer esas propiedades también puede ser útil para consultar el repositorio y averiguar conjuntos de páginas que están en estados particulares. Por ejemplo:

* `select * from cq:LiveSync` devuelve todas las páginas raíz de Live Copy.

## Preguntas más frecuentes {#faq}

Estas son algunas de las preguntas más frecuentes relacionadas con MSM y Live Copy.

### ¿Por qué algunas propiedades (por ejemplo, título, anotaciones) no se actualizan durante un despliegue de MSM? {#missing-properties}

Las acciones de sincronización de MSM son altamente configurables. Las propiedades o los componentes que se modifican durante las implementaciones dependen directamente de las propiedades de dichas configuraciones.

Consulte [Prácticas recomendadas de MSM](msm-best-practices.md) para obtener más información sobre este tema.

### ¿Cómo puedo quitar los permisos de despliegue de un grupo de autores? {#remove-rollout-permissions}

No hay **despliegue** que se pueda establecer o eliminar para principales AEM (usuarios o grupos).

Como alternativa, puede hacer lo siguiente:

* Personalizar la interfaz de usuario del producto para ocultar las acciones de despliegue de un principal determinado.
* Elimine los privilegios de escritura del árbol de Live Copy para los autores a los que no se les permite desplegar.

### ¿Por qué veo páginas de Live Copy con el sufijo &quot;_msm_moved&quot;? {#moved-pages}

Si se despliega una página de modelo, actualiza su página de Live Copy o crea una nueva página de Live Copy si aún no existe. Por ejemplo, cuando se despliega por primera vez o cuando la página de Live Copy se eliminó manualmente.

Sin embargo, en este último caso, si una página sin una propiedad `cq:LiveRelationship` existe con el mismo nombre, se cambia el nombre de esta página antes de crear la página Live Copy.

De forma predeterminada, el despliegue espera una página de Live Copy vinculada, a la que se implementan las actualizaciones de los modelos. O bien, no espera ninguna página cuando se crea una página Live Copy.

Si se encuentra una página &quot;independiente&quot;, MSM elige cambiar el nombre de esta página y crear una página de Live Copy separada y vinculada.

Esta página independiente en un subárbol de Live Copy suele ser el resultado de una operación **Desasociar**, o bien la página anterior de Live Copy fue eliminada manualmente por un autor y luego recreada con el mismo nombre.

Para evitarlo, usa la característica de Live Copy **Suspender** en lugar de **Desasociar**. Encontrará más detalles sobre la acción **Desasociar** en [este artículo.](msm-livecopy.md)
