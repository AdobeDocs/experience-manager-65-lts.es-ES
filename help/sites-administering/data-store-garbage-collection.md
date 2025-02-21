---
title: Recopilación de datos almacenados desechables
description: Obtenga información sobre cómo configurar la recolección de elementos no utilizados del almacén de datos para liberar espacio en disco.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# Recopilación de datos almacenados desechables {#data-store-garbage-collection}

Cuando se quita un recurso WCM convencional, la referencia al registro del almacén de datos subyacente se puede quitar de la jerarquía de nodos, pero el registro del almacén de datos en sí permanece. Este registro de almacén de datos al que no se hace referencia se convierte en &quot;basura&quot; que no necesita conservarse. En los casos en que existen varios recursos de basura, es beneficioso deshacerse de ellos para conservar espacio y optimizar el rendimiento del mantenimiento del sistema de archivos y la copia de seguridad.

En su mayor parte, una aplicación WCM tiende a recopilar información, pero no a eliminarla casi con la misma frecuencia. Aunque se añaden nuevas imágenes, incluso sustituyendo a las versiones antiguas, el sistema de control de versiones conserva la antigua y admite la reversión a ella si es necesario. Por lo tanto, la mayor parte del contenido que pensamos que se añade al sistema se almacena de forma efectiva de forma permanente. Entonces, ¿cuál es la fuente típica de &quot;basura&quot; en el repositorio que podríamos querer limpiar?

AEM utiliza el repositorio como almacenamiento para varias actividades internas y de mantenimiento:

* Paquetes creados y descargados
* Archivos temporales creados para la replicación de publicación
* Cargas del flujo de trabajo
* Assets creado temporalmente durante el procesamiento DAM

Cuando cualquiera de estos objetos temporales es lo suficientemente grande como para requerir almacenamiento en el almacén de datos y cuando el objeto deja de usarse, el registro del almacén de datos permanece como &quot;basura&quot;. En una aplicación típica de WCM de autor/publicación, la mayor fuente de residuos de este tipo suele ser el proceso de activación de la publicación. Cuando los datos se replican en Publish, se recopilan por primera vez en colecciones en un formato de datos eficaz denominado &quot;Durbo&quot; y se almacenan en el repositorio en `/var/replication/data`. Los paquetes de datos suelen superar el umbral de tamaño crítico para el almacén de datos y, por lo tanto, terminan almacenados como registros del almacén de datos. Cuando se complete la replicación, se eliminará el nodo de `/var/replication/data`, pero el registro del almacén de datos permanecerá como &quot;basura&quot;.

Otra fuente de residuos recuperables son los paquetes. Los datos del paquete, como todo lo demás, se almacenan en el repositorio y, por lo tanto, para los paquetes que superan los 4 KB, en el almacén de datos. En el transcurso de un proyecto de desarrollo o a lo largo del tiempo mientras se mantiene un sistema, los paquetes se pueden crear y reconstruir muchas veces, cada compilación resulta en un nuevo registro de almacén de datos, dejando huérfano el registro de la compilación anterior.

## ¿Cómo funciona la recolección de elementos no utilizados del almacén de datos? {#how-does-data-store-garbage-collection-work}

Si el repositorio se ha configurado con un almacén de datos externo, [la recolección de elementos no utilizados del almacén de datos se ejecutará automáticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) como parte de la ventana de mantenimiento semanal. El administrador del sistema también puede [ejecutar la recolección de elementos no utilizados del almacén de datos manualmente](#running-data-store-garbage-collection) según sea necesario. En general, se recomienda que la recolección de elementos no utilizados del almacén de datos se realice periódicamente, pero que se tengan en cuenta los siguientes factores al planificar las colecciones de elementos no utilizados del almacén de datos:

* Las recopilaciones de elementos no utilizados del almacén de datos tardan tiempo y pueden afectar al rendimiento, por lo que se deben planificar en consecuencia.
* La eliminación de los registros de basura del almacén de datos no afecta al rendimiento normal, por lo que no se trata de una optimización del rendimiento.
* Si la utilización del almacenamiento y factores relacionados como los tiempos de copia de seguridad no son un problema, la recolección de elementos no utilizados del almacén de datos podría aplazarse con seguridad.

El recolector de elementos no utilizados del almacén de datos toma nota primero de la marca de tiempo actual cuando comienza el proceso. La recopilación se lleva a cabo utilizando un algoritmo de patrón de barrido/marca de paso múltiple.

En la primera fase, el recolector de elementos no utilizados del almacén de datos realiza un recorrido completo de todo el contenido del repositorio. Para cada objeto de contenido que tiene una referencia a un registro de almacén de datos, localizó el archivo en el sistema de archivos, realizando una actualización de metadatos (modificando el atributo &quot;última modificación&quot; o MTIME). En este punto, los archivos a los que se accede mediante esta fase se convierten en más recientes que la marca de tiempo de línea de base inicial.

En la segunda fase, el recolector de elementos no utilizados del almacén de datos atraviesa la estructura de directorios física del almacén de datos de la misma manera que un &quot;hallazgo&quot;. Examinó el atributo &quot;última modificación&quot; o MTIME del archivo y realiza la siguiente determinación:

* Si MTIME es más reciente que la marca de tiempo de línea de base inicial, el archivo se encontró en la primera fase o es un archivo completamente nuevo que se agregó al repositorio mientras el proceso de recopilación estaba en curso. En cualquiera de estos casos, el registro se considera activo y el archivo no se elimina.
* Si MTIME es anterior a la marca de tiempo de línea de base inicial, el archivo no es un archivo al que se hace referencia de forma activa y se considera basura extraíble.

Este método funciona bien para un solo nodo con un almacén de datos privado. Sin embargo, el almacén de datos se puede compartir y, si es así, las referencias activas potencialmente activas a registros del almacén de datos de otros repositorios no se comprueban y los archivos a los que se hace referencia activos se pueden eliminar por error. Es imperativo que el administrador del sistema entienda la naturaleza compartida del almacén de datos antes de planificar las colecciones de elementos no utilizados y que utilice únicamente el proceso de recopilación de elementos no utilizados integrado simple del almacén de datos cuando sepa que el almacén de datos no se comparte.

>[!NOTE]
>
>Al realizar la recolección de elementos no utilizados en una configuración de almacén de datos en clúster o compartido (con Mongo o Segment TAR), el registro puede mostrar advertencias sobre la incapacidad para eliminar ciertos ID de blob. Esto sucede porque otros clústeres o nodos compartidos que no tienen información sobre las eliminaciones de ID hacen referencia de nuevo incorrectamente a los ID de blob eliminados en una colección de residuos anterior. Como resultado, cuando se realiza la recolección de elementos no utilizados, se registra una advertencia cuando se intenta eliminar un ID que ya se ha eliminado en la última ejecución. Este comportamiento no afecta al rendimiento ni a la funcionalidad.

## Ejecución de la recolección de basura del almacén de datos {#running-data-store-garbage-collection}

Existen tres formas de ejecutar la recolección de elementos no utilizados del almacén de datos, según la configuración del almacén de datos en el que se esté ejecutando AEM:

1. Mediante [Limpieza de revisión](/help/sites-deploying/revision-cleanup.md): un mecanismo de recolección de elementos no utilizados que se usa generalmente para la limpieza del almacén de nodos.

1. Mediante [recolección de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard): un mecanismo de recolección de elementos no utilizados específico para los almacenes de datos externos, disponible en el tablero de operaciones.
1. Mediante la [consola JMX](/help/sites-administering/jmx-console.md).

Si TarMK se usa como almacén de nodos y como almacén de datos, Revision Cleanup se puede usar para la recolección de elementos no utilizados tanto del almacén de nodos como del almacén de datos. Sin embargo, si se configura un almacén de datos externo como el almacén de datos del sistema de archivos, la recopilación de elementos no utilizados del almacén de datos se debe activar explícitamente de forma independiente de la Limpieza de revisión. La recopilación de elementos no utilizados del almacén de datos se puede activar mediante el tablero de operaciones o la consola JMX.

En la tabla siguiente se muestra el tipo de recolección de elementos no utilizados del almacén de datos que debe usarse para todas las implementaciones de almacén de datos admitidas en AEM 6:

<table>
 <tbody>
  <tr>
   <td><strong>Almacén de nodos</strong><br /> </td>
   <td><strong>Almacén de datos</strong></td>
   <td><strong>Mecanismo de recolección de basura</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Limpieza de revisión (los binarios están alineados con el almacén de segmentos)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>Sistema de archivos externo</td>
   <td><p>Tarea de recolección de basura del almacén de datos mediante el tablero de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Tarea de recolección de basura del almacén de datos mediante el tablero de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>Sistema de archivos externo</td>
   <td><p>Tarea de recolección de basura del almacén de datos mediante el tablero de operaciones</p> <p>Consola JMX</p> </td>
  </tr>
 </tbody>
</table>

### Ejecución de la recopilación de basura del almacén de datos mediante el tablero de operaciones {#running-data-store-garbage-collection-via-the-operations-dashboard}

La ventana de mantenimiento semanal integrada, disponible a través de [Operations Dashboard](/help/sites-administering/operations-dashboard.md), contiene una tarea integrada para almacenar en déclencheur la recolección de elementos no utilizados del almacén de datos a la 1 a. m. los domingos.

Si necesita ejecutar la recolección de basura del almacén de datos fuera de este tiempo, se puede activar manualmente a través del Tablero de operaciones.

Antes de ejecutar la recolección de elementos no utilizados del almacén de datos, debe comprobar que no se estén ejecutando copias de seguridad en ese momento.

1. Abra el tablero de operaciones en **Navegación** > **Herramientas** > **Operaciones** > **Mantenimiento**.
1. Haga clic en **Ventana de mantenimiento semanal**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Seleccione la tarea **Recopilación de residuos del almacén de datos** y, a continuación, haga clic en el icono **Ejecutar**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. La recolección de elementos no utilizados del almacén de datos se ejecuta y su estado se muestra en el panel.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>La tarea de recolección de elementos no utilizados del almacén de datos solo estará visible si ha configurado un almacén de datos de archivo externo. Consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obtener información sobre cómo configurar un almacén de datos de archivos.

### Ejecución de la recopilación de basura del almacén de datos mediante la consola JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Esta sección trata sobre la ejecución manual de la recopilación de residuos del almacén de datos a través de la consola JMX. Si la instalación está configurada sin un almacén de datos externo, esto no se aplica a la instalación. En su lugar, consulte las instrucciones sobre cómo ejecutar Revision cleanup en [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Si está ejecutando TarMK con un almacén de datos externo, es necesario que ejecute primero Revision Cleanup para que la recolección de elementos no utilizados sea efectiva.

Para ejecutar la recolección de elementos no utilizados:

1. En la consola de administración de Apache Felix OSGi, resalte la pestaña **Main** y seleccione **JMX** del siguiente menú.
1. A continuación, busque y haga clic en el MBean **Administrador de repositorios** (o vaya a `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Haga clic en **startDataStoreGC(boolean markOnly)**.
1. escriba &quot;`true`&quot; para el parámetro `markOnly` si es necesario:

   | **Opción** | **Descripción** |
   |---|---|
   | boolean markOnly | Establezca como true para marcar únicamente referencias y no barrer en la operación de marca y barrido. Este modo se utiliza cuando el BlobStore subyacente se comparte entre varios repositorios diferentes. En todos los demás casos, establézcalo en False para realizar la recolección de elementos no utilizados completa. |

1. Haga clic en **Invocar**. CRX ejecuta la recolección de elementos no utilizados e indica cuándo se ha completado.

>[!NOTE]
>
>La recolección de elementos no utilizados del almacén de datos no recopilará los archivos que se hayan eliminado en las últimas 24 horas.

>[!NOTE]
>
>La tarea de recolección de elementos no utilizados del almacén de datos solo se iniciará si ha configurado un almacén de datos de archivo externo. Si no se ha configurado un almacén de datos de archivo externo, la tarea devolverá el mensaje `Cannot perform operation: no service of type BlobGCMBean found` después de invocar. Consulte [Configuración de almacenes de nodos y almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obtener información sobre cómo configurar un almacén de datos de archivos.

## Automatización de la recolección de basura del almacén de datos {#automating-data-store-garbage-collection}

Si es posible, la recolección de elementos no utilizados del almacén de datos debe ejecutarse cuando haya poca carga en el sistema, por ejemplo, por la mañana.

La ventana de mantenimiento semanal integrada, disponible a través de [Operations Dashboard](/help/sites-administering/operations-dashboard.md), contiene una tarea integrada para almacenar en déclencheur la recolección de elementos no utilizados del almacén de datos a la 1 a. m. los domingos. También debe comprobar que no hay copias de seguridad en ejecución en este momento. El inicio de la ventana de mantenimiento se puede personalizar mediante el panel de control según sea necesario.

>[!NOTE]
>
>El motivo por el que no se ejecuta simultáneamente es para que también se realice una copia de seguridad de los archivos del almacén de datos antiguos (y que no se utilicen), de modo que si es necesario revertir a una revisión antigua, los binarios sigan ahí en la copia de seguridad.

Si no desea ejecutar la recolección de elementos no utilizados del almacén de datos con la ventana de mantenimiento semanal del tablero de operaciones, también se puede automatizar mediante los clientes HTTP wget o curl. A continuación se muestra un ejemplo de cómo automatizar la recolección de elementos no utilizados mediante curl:

>[!CAUTION]
>
>En el siguiente ejemplo `curl` comandos es posible que se deban configurar varios parámetros para la instancia; por ejemplo, el nombre de host ( `localhost`), el puerto ( `4502`), la contraseña de administrador ( `xyz`) y varios parámetros para la recolección de elementos no utilizados del almacén de datos real.

Este es un ejemplo de comando curl para invocar la recolección de elementos no utilizados del almacén de datos a través de la línea de comandos:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

El comando curl vuelve inmediatamente.

## Comprobación de coherencia del almacén de datos {#checking-data-store-consistency}

La comprobación de coherencia del almacén de datos informará de cualquier binario del almacén de datos que falte, pero al que aún se haga referencia. Para iniciar una comprobación de coherencia, siga estos pasos:

1. Vaya a la consola JMX. Para obtener información sobre cómo usar la consola JMX, consulte [Supervisión de recursos del servidor mediante la consola JMX](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Busque el MBean **BlobGarbageCollection** y haga clic en él.
1. Haga clic en el vínculo `checkConsistency()`.

Una vez completada la comprobación de coherencia, un mensaje mostrará el número de binarios notificados como faltantes. Si el número es mayor que 0, compruebe `error.log` para obtener más detalles sobre los binarios que faltan.

A continuación, se muestra un ejemplo de cómo se informan los binarios que faltan en los registros:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
