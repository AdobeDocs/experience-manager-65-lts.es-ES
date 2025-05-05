---
title: Solución de problemas de índices Oak
description: Obtenga información sobre cómo identificar si la indexación es lenta, encontrar la causa y resolver el problema.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 6f92750a-4eaa-43cf-8f67-b1a65b1c6930
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Solución de problemas de índices Oak{#troubleshooting-oak-indexes}

## Reindexación lenta  {#slow-re-indexing}

El proceso de reindexación interna de AEM recopila datos del repositorio y los almacena en índices de Oak para admitir la consulta de contenido con rendimiento. En circunstancias excepcionales, el proceso puede ralentizarse o incluso atascarse. Esta página actúa como una guía de solución de problemas para identificar si la indexación es lenta, encontrar la causa y resolver el problema.

Es importante distinguir entre una reindexación que lleva una cantidad de tiempo inapropiadamente larga y una reindexación que lleva una cantidad de tiempo larga porque está indexando grandes cantidades de contenido. Por ejemplo, el tiempo que se tarda en indexar el contenido se escala con la cantidad de contenido, por lo que los repositorios de producción grandes tardan más en reindexarse que los pequeños.

Consulte las [Prácticas recomendadas en consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obtener información adicional sobre cuándo y cómo reindexar contenido.

## Detección inicial {#initial-detection}

La detección inicial requiere una indexación lenta de `IndexStats` MBeans de JMX. En la instancia de AEM afectada, haga lo siguiente:

1. Abra la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Vaya a `IndexStats` MBean.
1. Abra los `IndexStats` MBeans para &quot;`async`&quot; y &quot;`fulltext-async`&quot;.

1. Para ambos MBeans, compruebe si la marca de tiempo **Done** y **LastIndexTime** están a menos de 45 minutos de la hora actual.

1. Para MBean, si el valor de tiempo (**Listo** o **ÚltimoTiempoIndexado**) es mayor que 45 minutos desde el momento actual, el trabajo de índice está fallando o está tardando demasiado. Este problema hace que los índices asíncronos estén obsoletos.

## La indexación se detiene después de un cierre forzado {#indexing-is-paused-after-a-forced-shutdown}

Un apagado forzado provoca que AEM suspenda la indexación asincrónica durante un máximo de 30 minutos después del reinicio. Y, por lo general, se requieren otros 15 minutos para completar el primer pase de reindexación, lo que equivale a un total de aproximadamente 45 minutos (vinculándolos al periodo de tiempo de [Detección inicial](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) de 45 minutos). Si la indexación está en pausa después de un apagado forzado:

1. En primer lugar, determine si la instancia de AEM se cerró de forma forzada (el proceso de AEM se cerró a la fuerza o se produjo un error de alimentación) y luego se reinició.

   * [El registro de AEM](/help/sites-deploying/configure-logging.md) se puede revisar con este fin.

1. Si se produce el apagado forzado, al reiniciar, AEM suspende automáticamente la reindexación durante un máximo de 30 minutos.
1. Espere aproximadamente 45 minutos para que AEM reanude las operaciones normales de indexación asincrónica.

## Grupo de subprocesos sobrecargado {#thread-pool-overloaded}

En circunstancias excepcionales, el grupo de subprocesos utilizado para administrar la indexación asincrónica puede sobrecargarse. Para aislar el proceso de indexación, se puede configurar un grupo de hilos para evitar que otros trabajos de AEM interfieran con la capacidad de Oak para indexar contenido de manera oportuna. En estos casos, haga lo siguiente:

1. Defina un nuevo grupo de hilos aislado para el planificador de Apache Sling que se utilizará para la indexación asíncrona:

   * En la instancia de AEM afectada, vaya a la Consola web OSGi de AEM>OSGi>Configuración>Planificador de Apache Sling o a https://&lt;host>:&lt;port>/system/console/configMgr (por ejemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Agregue una entrada al campo &quot;Grupos de hilos permitidos&quot; con el valor &quot;oak&quot;.
   * Para guardar los cambios, haz clic en **Guardar** en la parte inferior derecha.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Compruebe que el nuevo grupo de hilos del Planificador de Apache Sling esté registrado y se muestre en la consola web Estado del planificador de Apache Sling.

   * Vaya a la consola web de AEM OSGi>Estado>Planificador de Sling o a https://&lt;host>:&lt;port>/system/console/status-slingscheduler (por ejemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler)).
   * Compruebe que existen las siguientes entradas de grupo:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La cola de observación está llena {#observation-queue-is-full}

Si se realizan demasiados cambios y confirmaciones en el repositorio en un corto período de tiempo, la indexación se puede retrasar debido a una cola de observación completa. En primer lugar, determine si la cola de observación está llena:

1. Vaya a la consola web y haga clic en la pestaña JMX o vaya a https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra el MBean Estadísticas del repositorio de Oak y determine si algún valor de `ObservationQueueMaxLength` es mayor que 10 000.

   * En las operaciones normales, este valor máximo siempre debe reducirse finalmente a cero (especialmente en la sección `per second`) para comprobar que las métricas de segundos de `ObservationQueueMaxLength` sean 0.
   * Si los valores son 10 000 o más y aumentan de forma constante, indica que al menos una cola (posiblemente más) no se puede procesar tan rápido como se producen nuevos cambios (confirmaciones).
   * Cada cola de observación tiene un límite (10 000 de forma predeterminada) y, si la cola alcanza ese límite, se degrada su procesamiento.
   * Al utilizar MongoMK, a medida que la longitud de la cola aumenta, el rendimiento interno de la caché de Oak se degrada. Esta correlación se puede ver en un aumento de `missRate` para la caché de `DocChildren` en el MBean de estadísticas de `Consolidated Cache`.

1. Para evitar superar los límites aceptables de la cola de observación, se recomienda:

   * Reduzca la tasa constante de confirmaciones. Los picos cortos en las confirmaciones son aceptables, pero la tasa constante debe reducirse.
   * Aumente el tamaño de `DiffCache` como se describe en [Consejos de rendimiento > Ajuste del almacenamiento Mongo > Tamaño de la caché del documento](/help/sites-deploying/configuring-performance.md).

## Identificación y corrección de un proceso de reindexación bloqueado {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindexación se puede considerar &quot;completamente atascada&quot; bajo dos condiciones:

* La reindexación es lenta, hasta el punto de que no se informa de ningún progreso significativo en los archivos de registro con respecto al número de nodos atravesados.

   * Por ejemplo, si no hay mensajes en el transcurso de una hora o si el progreso es tan lento que tarda una semana o más en finalizar.

* La reindexación se bloquea en un bucle interminable si aparecen excepciones repetidas en los archivos de registro (por ejemplo, `OutOfMemoryException`) en el subproceso de indexación. La repetición de una o más excepciones en el registro indica que Oak intenta indexar lo mismo repetidamente, pero falla en el mismo problema.

Para identificar y corregir un proceso de reindexación atascado, haga lo siguiente:

1. Para identificar la causa de la indexación atascada, se debe recopilar la siguiente información:

   * Recopile 5 minutos del volcado de hilos, un volcado de hilos cada 2 segundos.
   * [Establecer nivel de depuración y registros para los anexadores](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * Recopilar datos del MBean `IndexStats` asincrónico:

      * Vaya a la consola web de AEM OSGi>Principal>JMX>IndexStat>asíncrona

        o ve a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * Utilice el modo de consola [oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para recopilar los detalles de lo que existe bajo el nodo * `/:async`*.
   * Recopile una lista de puntos de comprobación del repositorio mediante el MBean `CheckpointManager`:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

        o ve a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. Después de recopilar toda la información descrita en el paso 1, reinicie AEM.

   * El reinicio de AEM puede solucionar el problema si hay una carga simultánea alta (desbordamiento de la cola de observación o algo similar).
   * Si un reinicio no soluciona el problema, abre un problema con el [Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/es?support-solution=General&amp;support-tab=home&amp;lang=es#support) y proporciona toda la información recopilada en el paso 1.

## Anulación segura de la reindexación asíncrona {#safely-aborting-asynchronous-re-indexing}

La reindexación se puede cancelar de forma segura (se detuvo antes de que se complete) a través de las rutas de indexación `async, async-reindex` y `ulltext-async` ( `IndexStats` MB). Para obtener más información, consulte también la documentación de Apache Oak sobre [Cómo abortar la reindexación](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Además, tenga en cuenta lo siguiente:

* La reindexación de los índices de propiedades Lucene y Lucene se puede cancelar porque son asíncronos por naturaleza.
* La reindexación de los índices de propiedades de Oak solo se puede anular si la reindexación se inició a través de `PropertyIndexAsyncReindexMBean`.

Para anular la reindexación de forma segura, siga estos pasos:

1. Identifique el MBean IndexStats que controla el carril de reindexación que debe detenerse.

   * Vaya al MBean IndexStats adecuado a través de la consola JMX en AEM OSGi Web Console>Main>JMX o https://&lt;host>:&lt;port>/system/console/jmx (por ejemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
   * Abra el MBean IndexStats en función de la ruta de reindexación que desee detener ( `async`, `async-reindex` o `fulltext-async`)

      * Para identificar el carril adecuado y, por lo tanto, la instancia de MBean IndexStats, observe la propiedad &quot;async&quot; de Oak Indexes. La propiedad &quot;async&quot; contiene el nombre de ruta: `async`, `async-reindex` o `fulltext-async`.
      * El carril también está disponible si accede al Administrador de índices de AEM en la columna &quot;Asíncrona&quot;. Para acceder al Administrador de índices, vaya a Operaciones>Diagnóstico>Administrador de índices.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoque el comando `abortAndPause()` en el MBean `IndexStats` apropiado.
1. Marque correctamente la definición de índice de Oak para evitar que se reanude la reindexación cuando se reanude la ruta de indexación.

   * Al reindexar un índice **existing**, establezca la propiedad reindex en false

      * `/oak:index/someExistingIndex@reindex=false`

   * De lo contrario, para un índice **new**, ya sea:

      * Establezca la propiedad type como disabled

         * `/oak:index/someNewIndex@type=disabled`

      * o elimine la definición del índice por completo

   Confirme los cambios en el repositorio cuando se hayan completado.

1. Finalmente, reanude la indexación asíncrona en la ruta de indexación anulada.

   * En el MBean `IndexStats` que emitió el comando `abortAndPause()` en el paso 2, invoque el comando `resume()`.

## Prevención de la reindexación lenta {#preventing-slow-re-indexing}

Es mejor reindexar durante periodos de inactividad (por ejemplo, no durante una ingesta de contenido de gran tamaño), e idealmente durante periodos de mantenimiento en los que la carga de AEM se conozca y controle. Además, asegúrese de que la reindexación no se produzca durante otras actividades de mantenimiento.
