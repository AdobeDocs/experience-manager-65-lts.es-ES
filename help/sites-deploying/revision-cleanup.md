---
title: Limpieza de revisión
description: Aprenda a utilizar la funcionalidad Revision Cleanup en Adobe Experience Manager 6.5.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 114a77bc-0b7e-49ce-bca1-e5195b4884dc
source-git-commit: 3cbc2ddd4ff448278e678d1a73c4ee7ba3af56f4
workflow-type: tm+mt
source-wordcount: '5139'
ht-degree: 0%

---

# Limpieza de revisión{#revision-cleanup}

## Introducción {#introduction}

Cada actualización del repositorio crea una revisión de contenido. Como resultado, con cada actualización, el tamaño del repositorio aumenta. Las revisiones antiguas deben limpiarse para liberar recursos de disco. Esto es importante para evitar un crecimiento incontrolado del repositorio. Esta funcionalidad de mantenimiento se denomina Limpieza de revisión. Está disponible como rutina sin conexión desde Adobe Experience Manager (AEM) 6.0.

Con AEM 6.3 y versiones posteriores, se introdujo una versión en línea de esta funcionalidad denominada Limpieza de revisión en línea. En comparación con la Limpieza de revisión sin conexión, en la que hay que cerrar la instancia de AEM, la Limpieza de revisión en línea se puede ejecutar mientras la instancia de AEM está en línea. Limpieza de revisión en línea está activada de forma predeterminada y es la forma recomendada de realizar una limpieza de revisión.

**Nota**: [Vea el Vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html) para ver una introducción y cómo usar la Limpieza de revisión en línea.

El proceso de limpieza de revisión consta de tres fases: **estimación**, **compactación** y **limpieza**. La estimación determina si se debe ejecutar la siguiente fase (compactación) o no en función de la cantidad de basura que se pueda recolectar. Durante la fase de compactación, los segmentos y los archivos tar se vuelven a escribir sin tener en cuenta el contenido no utilizado. A continuación, la fase de limpieza elimina los segmentos antiguos, incluida la basura que puedan contener. El modo sin conexión generalmente puede recuperar más espacio porque el modo en línea debe tener en cuenta el conjunto de trabajo de AEM, que evita que se recopilen segmentos adicionales.

Para obtener más información sobre Revision Cleanup, consulte los siguientes vínculos:

* [Cómo ejecutar la limpieza de revisión en línea](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [Preguntas más frecuentes sobre Limpieza de revisiones en línea](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [Cómo ejecutar la limpieza de revisión sin conexión](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

También puede leer la [documentación oficial de Oak](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html).

### ¿Cuándo utilizar la Limpieza de revisión en línea y cuándo la Limpieza de revisión sin conexión? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Limpieza de revisión en línea es la forma recomendada de realizar la limpieza de revisión.** Limpieza de revisión sin conexión solo debe usarse de forma excepcional, por ejemplo, antes de migrar al nuevo formato de almacenamiento o si el Servicio de atención al cliente de Adobe le solicita que lo haga.

## Cómo ejecutar la limpieza de revisión en línea {#how-to-run-online-revision-cleanup}

La Limpieza de revisión en línea está configurada de forma predeterminada para ejecutarse automáticamente una vez al día tanto en las instancias de autor de AEM como en las de publicación. Todo lo que debe hacer es definir la ventana de mantenimiento durante un periodo con la menor actividad de usuario. Puede configurar la tarea Limpieza de revisión en línea de la siguiente manera:

1. En la ventana principal de AEM, vaya a **Herramientas - Operaciones - Panel de control - Mantenimiento** o dirija el explorador a: `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Pase el ratón sobre **Ventana de mantenimiento diario** y haga clic en el icono **Configuración**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Introduzca los valores deseados (periodicidad, hora de inicio, hora de finalización) y haga clic en **Guardar**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

Alternativamente, si desea ejecutar la tarea de limpieza de revisión manualmente, puede:

1. Vaya a **Herramientas - Operaciones - Panel de control - Mantenimiento** o busque directamente `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. Haga clic en **Ventana de mantenimiento diario**.
1. Pase el ratón sobre el icono **Limpieza de revisión**.
1. Haga clic en **Ejecutar**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### Ejecución De La Limpieza De Revisión En Línea Después De La Limpieza De Revisión Sin Conexión {#running-online-revision-cleanup-after-offline-revision-cleanup}

El proceso de limpieza de revisión reclama las revisiones antiguas por generaciones. Esto significa que cada vez que ejecuta la limpieza de revisión se crea una nueva generación y se mantiene en el disco. Sin embargo, hay una diferencia entre los dos tipos de limpieza de revisión: la limpieza de revisión sin conexión mantiene una generación, mientras que la limpieza de revisión en línea mantiene dos generaciones. Por lo tanto, cuando ejecuta la limpieza de revisión en línea **después de** la limpieza de revisión sin conexión, ocurre lo siguiente:

1. Después de la primera ejecución de limpieza de revisión en línea, el tamaño del repositorio se duplica. Esto sucede porque ahora hay dos generaciones que se mantienen en el disco.
1. Durante las ejecuciones posteriores, el repositorio crecerá temporalmente mientras se crea la nueva generación y luego se estabilizará de nuevo al tamaño que tenía después de la primera ejecución, a medida que el proceso de limpieza de revisión en línea reclama a la generación anterior.

Además, tenga en cuenta que según el tipo y el número de confirmaciones, cada generación puede variar en tamaño en comparación con la anterior, por lo que el tamaño final puede variar de una ejecución a otra.

Debido a este hecho, se recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio estimado inicialmente.

## Modos De Compactación Completa Y De Cola  {#full-and-tail-compaction-modes}

**AEM 6.5 LTS** tiene **dos modos** para la fase de **compactación** del proceso de limpieza de revisión en línea:

* El modo **compactación completa** reescribe todos los segmentos y archivos tar de todo el repositorio. La fase de limpieza posterior puede, por lo tanto, eliminar la cantidad máxima de residuos en el repositorio. Debido a que la compactación completa afecta a todo el repositorio, requiere una cantidad considerable de recursos del sistema y tiempo para completarse.
* El modo **tail compaction** solo reescribe los segmentos y archivos tar más recientes del repositorio. Los segmentos y archivos tar más recientes son los que se han añadido desde la última vez que se ejecutó la compactación completa o de cola. Por lo tanto, la fase de limpieza posterior solo puede eliminar la basura contenida en la parte reciente del repositorio. Debido a que la compactación de cola solo afecta a una parte del repositorio, requiere considerablemente menos recursos del sistema y tiempo para completarla que la compactación completa.

Estos modos de compactación constituyen un equilibrio entre la eficiencia y el consumo de recursos: aunque la compactación de cola es menos eficaz, también tiene menos impacto en el funcionamiento normal del sistema. Por el contrario, la compactación total es más eficaz, pero tiene un mayor impacto en el funcionamiento normal del sistema.

AEM 6.5 LTS cuenta con un mecanismo eficaz de deduplicación de contenido durante la compactación, lo que reduce aún más el espacio en disco del repositorio.


### Cómo configurar la compactación completa y de cola {#how-to-configure-full-and-tail-compaction}

La configuración predeterminada ejecuta la compactación de cola entre semana y la compactación completa los domingos. La configuración predeterminada se puede cambiar usando el nuevo valor de configuración `full.gc.days` de `RevisionCleanupTask` [tarea de mantenimiento](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

Al configurar el valor `full.gc.days`, la compactación completa se ejecuta durante los días definidos en el valor y la compactación de cola se ejecuta durante los días no definidos en el valor. Por ejemplo, si configura la compactación completa para que se ejecute el domingo, la compactación de cola se ejecuta de lunes a sábado. Por ejemplo, si configura la compactación completa para que se ejecute todos los días de la semana, la compactación de cola no se ejecuta en absoluto.

Además, tenga en cuenta que:

* **La compactación de cola** es menos efectiva y tiene menos impacto en las operaciones normales del sistema. Por lo tanto, está previsto que se ejecute durante los días laborables.
* **La compactación completa** es más efectiva, pero también tiene un mayor impacto en las operaciones normales del sistema. Por lo tanto, está previsto que se utilice fuera de los días hábiles.
* Tanto la compactación de cola como la compactación completa deben programarse para ejecutarse durante las horas de menor actividad.

### Solución de problemas {#troubleshooting}

Cuando utilice los nuevos modos de compactación, tenga en cuenta lo siguiente:

* Puede monitorizar la actividad de entrada/salida (E/S), por ejemplo: operaciones de E/S, CPU esperando E/S, tamaño de cola de confirmación. Esto ayuda a determinar si el sistema está enlazado a E/S y si es necesario convertir.
* `RevisionCleanupTaskHealthCheck` indica el estado general de la Limpieza de revisión en línea.
* Los mensajes de registro llevan información relevante sobre los modos de compactación. Por ejemplo, cuando se inicia la Limpieza de revisión en línea, los mensajes de registro correspondientes indican el modo de compactación. Además, en algunos casos extremos, el sistema vuelve a la compactación completa cuando estaba programado para ejecutar una compactación de cola y los mensajes de registro indican este cambio. Las siguientes muestras de registro indican el modo de compactación y el cambio de cola a compactación completa:

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### Limitaciones conocidas {#known-limitations}

A veces, la alternancia entre los modos de cola y compactación completa retrasa el proceso de limpieza. Más concretamente, el repositorio crecerá después de una compactación completa (se duplica en tamaño). El espacio adicional se recupera en la siguiente compactación de cola, cuando el repositorio cae por debajo del tamaño de compactación precompleta. También deben evitarse las ejecuciones de tareas de mantenimiento paralelas.

**Se recomienda cambiar el tamaño del disco al menos dos o tres veces más grande que el tamaño de repositorio estimado inicialmente.**

## Preguntas más frecuentes sobre Limpieza de revisiones en línea {#online-revision-cleanup-frequently-asked-questions}

### Ejecución de Limpieza de revisión en línea {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Preguntas</strong></td>
   <td><strong>Respuestas</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Con qué frecuencia se debe ejecutar Limpieza de revisión en línea?</strong></td>
   <td>Una vez al día. Esta es la configuración predeterminada en el tablero de operaciones.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo puedo configurar la hora de inicio de la tarea de mantenimiento Limpieza de revisiones en línea?</strong></td>
   <td>Consulte la sección <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">Cómo ejecutar la limpieza de revisión en línea</a>. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Existe una frecuencia máxima que no debe excederse para la Limpieza de revisiones en línea?</strong></td>
   <td>Se recomienda ejecutar la Limpieza de revisión en línea una vez al día, según la configuración predeterminada.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los indicadores clave que determinan la frecuencia con la que se debe ejecutar Limpieza de revisión en línea?</strong></td>
   <td>No es necesario determinar la frecuencia, ya que Limpieza de revisiones en línea está configurada como tarea de mantenimiento y se ejecuta automáticamente todos los días.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué Online Revision Cleanup no recupera ningún espacio cuando se ejecuta por primera vez?</strong></td>
   <td>Limpieza de revisiones en línea recupera las revisiones antiguas realizadas por las generaciones. Se genera una nueva generación cada vez que se ejecuta la limpieza de revisión. Solo se recupera el contenido que tenga al menos dos generaciones, lo que significa que en una primera ejecución no hay nada que recuperar.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué la primera Limpieza de revisión en línea no recupera ningún espacio cuando se ejecuta después de la Limpieza de revisión sin conexión?</strong></td>
   <td><p>Offline Revision Cleanup está reclamando todo menos la última generación en comparación con las dos últimas generaciones para Online Revision Cleanup. Si hay un repositorio nuevo, la Limpieza de revisión en línea no reclamará ningún espacio cuando se ejecute por primera vez después de la Limpieza de revisión sin conexión porque no hay ninguna generación lo suficientemente antigua como para reclamarse.</p> <p>Lea también la sección "Ejecución de la limpieza de revisión en línea después de la limpieza de revisión sin conexión" de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">este capítulo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Las ventanas Autor y Publicación suelen tener diferentes ventanas Limpieza de revisiones en línea?</strong></td>
   <td>Esto depende del horario de oficina y de los patrones de tráfico de la presencia en línea del cliente. Las ventanas de mantenimiento deben configurarse fuera de los tiempos de producción principales para permitir la mejor eficacia de limpieza. Para varias instancias de publicación de AEM (granja TarMK), las ventanas de mantenimiento para Limpieza de revisiones en línea deben estar escalonadas.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los factores que determinan la duración de la Limpieza de revisión en línea?</strong></td>
   <td>Los factores son:<br />
    <ul>
     <li>Tamaño del repositorio</li>
     <li>Carga en el sistema (solicitudes por minuto, específicamente operaciones de escritura)</li>
     <li>Patrón de actividad (lecturas o escrituras)</li>
     <li>Especificaciones de hardware (rendimiento de CPU, memoria, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Pueden los autores seguir trabajando mientras se ejecuta la Limpieza de revisión en línea?</strong></td>
   <td>Sí, Limpieza de revisiones en línea puede hacer frente a escrituras simultáneas. Sin embargo, Limpieza de revisión en línea funciona de forma más rápida y eficaz sin transacciones de escritura simultáneas. Adobe recomienda programar la tarea de mantenimiento Limpieza de revisiones en línea para un periodo de tiempo relativamente silencioso y sin mucho tráfico.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuáles son los requisitos mínimos para el espacio en disco y la memoria de la pila al ejecutar Online Revision Cleanup?</strong></td>
   <td><p>El espacio en disco se supervisa continuamente durante la Limpieza de revisiones en línea. Si el espacio disponible en disco cae por debajo de un valor crítico, el proceso se cancela. El valor crítico es el 25 % del espacio en disco actual del repositorio y no se puede configurar.</p> <p><strong>Adobe recomienda que el tamaño del disco sea al menos dos o tres veces mayor que el tamaño de repositorio estimado inicialmente.</strong></p> <p>El espacio libre en la pila se monitoriza continuamente durante el proceso de limpieza. Si el espacio libre en la pila cae por debajo de un valor crítico, el proceso se cancela. El valor crítico se configura mediante org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD. El valor predeterminado es 15 %.</p> <p>Las recomendaciones de tamaño mínimo de pila de compactación no están separadas de las recomendaciones de tamaño de memoria de AEM. Generalmente: <strong>Si una instancia de AEM tiene el tamaño suficiente para hacer frente a los casos de uso y a la carga útil esperada, el proceso de limpieza obtiene suficiente memoria.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es el impacto esperado en el rendimiento al ejecutar Online Revision Cleanup?</strong></td>
   <td>La limpieza de revisión en línea es un proceso en segundo plano que lee y escribe en el repositorio de forma simultánea en operaciones normales del sistema. En particular, es posible que necesite adquirir acceso exclusivo al repositorio durante un corto periodo de tiempo, lo que evita que otros subprocesos escriban en el repositorio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Durante cuánto tiempo se espera que se ejecute la Limpieza de revisión en línea?</strong></td>
   <td>No debería tardar más de dos horas en ejecutarse según las últimas pruebas de rendimiento que Adobe realizó internamente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué se debe hacer si la limpieza de revisión en línea tarda más?</strong></td>
   <td>
    <ul>
     <li>Asegúrese de que se ejecute a diario.<br /> </li>
     <li>Asegúrese de que se ejecuta durante las actividades mínimas del repositorio configurando las ventanas de mantenimiento en el tablero de operaciones en consecuencia.</li>
     <li>Ampliación de los recursos del sistema (CPU, memoria, E/S).</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si Limpieza de revisión en línea supera las Ventanas de mantenimiento configuradas?</strong></td>
   <td>Asegúrese de que otras tareas de mantenimiento no retrasen su ejecución. Este podría ser el caso si se ejecutan más tareas de mantenimiento que la Limpieza de revisión en línea dentro de la misma ventana de mantenimiento. Las tareas de mantenimiento se ejecutan secuencialmente sin un orden configurable.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Por qué se omite la recolección de basura de revisiones?</strong></td>
   <td><p>Limpieza de revisión se basa en una fase de estimación para decidir si hay suficiente basura para limpiar. El estimador compara el tamaño actual con el tamaño del repositorio después de la última vez que se compactó. Si el tamaño supera el delta configurado, se ejecuta la limpieza. El delta de tamaño se establece en 1 GB. Esto significa que si el tamaño del repositorio no ha aumentado en 1 GB desde la última ejecución de limpieza, se omitirá la nueva iteración de limpieza de revisión. </p> <p>A continuación se muestran las entradas de registro relevantes para la fase de estimación:</p>
    <ul>
     <li>Se ejecuta la revisión GC: <em>El delta de tamaño es N% o N/N (N/N bytes), por lo que se ejecuta la compactación</em></li>
     <li>El GC de revisión <strong>no se ejecuta </strong>: <em>El tamaño delta es N% o N/N (N/N bytes), por lo que se omitirá la compactación por ahora</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Es posible abortar de forma segura la compactación automática si el impacto en el rendimiento es demasiado alto?</strong></td>
   <td>Sí. A partir de AEM 6.3, se puede detener de forma segura mediante la ventana Tarea de mantenimiento dentro del tablero de operaciones o mediante JMX.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Si la instancia de AEM se apaga durante una tarea de limpieza programada, ¿el proceso se interrumpe de forma segura o se bloquea el apagado hasta que la compactación haya finalizado?</strong></td>
   <td>Revision Cleanup se interrumpe y el repositorio se apaga correctamente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede cuando el sistema se bloquea durante la Limpieza de revisión en línea?</strong></td>
   <td>En estos casos no existe riesgo de que los datos se dañen. Las sobras de basura se limpian con una ejecución posterior.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es el impacto de no ejecutar la Limpieza de revisión en línea?</strong></td>
   <td>Degradación del rendimiento con el tiempo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué revisiones se recopilan?</strong></td>
   <td>De forma predeterminada, Limpieza de revisión en línea solo recopila revisiones que tengan al menos 24 horas de antigüedad.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si hay demasiada interferencia de escrituras simultáneas en el repositorio?</strong></td>
   <td><p>Si hay concurrencia de escritura en el sistema, la limpieza de revisión en línea puede requerir acceso de escritura exclusivo para poder confirmar los cambios al final de un ciclo de compactación. El sistema entra en <strong>modo forceCompact</strong>, como se explica con más detalle en la <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">documentación de Oak</a>. Durante la compactación forzada, se adquiere un bloqueo de escritura exclusivo para confirmar finalmente los cambios sin que ninguna escritura simultánea interfiera. Para limitar el impacto en los tiempos de respuesta, se puede definir un valor de tiempo de espera. Este valor se define en un minuto de forma predeterminada, lo que significa que si force compact no se completa en un minuto, el proceso de compactación se interrumpe en favor de confirmaciones simultáneas.</p> <p>La duración de la fuerza de compactación depende de los siguientes factores:</p>
    <ul>
     <li>hardware: específicamente IOPS. La duración disminuye con más IOPS.</li>
     <li>tamaño del almacén de segmentos: la duración aumenta con el tamaño del almacén de segmentos.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Cómo se ejecuta Limpieza de revisión en línea en una instancia de espera?</strong></p> </td>
   <td><p>En una configuración de espera pasiva, solo la instancia principal debe configurarse para ejecutar Online Revision Cleanup. En la instancia de espera, Limpieza de revisión en línea no necesita programarse específicamente.</p> <p>La operación correspondiente en una instancia de espera es la Limpieza automática, que corresponde a la fase de limpieza de la Limpieza de revisión en línea. La Limpieza automática se ejecuta en la instancia de espera después de la ejecución de la Limpieza de revisión en línea en la instancia principal.</p> <p>Las fases de estimación y compactación no se ejecutarán en una instancia de espera.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Puede Offline Revision Cleanup liberar más espacio en disco que Online Revision Cleanup?</strong></td>
   <td><p>La Limpieza de revisión sin conexión puede eliminar inmediatamente las revisiones antiguas, mientras que la Limpieza de revisión en línea debe tener en cuenta las revisiones antiguas a las que hace referencia la pila de aplicaciones. De este modo, el primero puede eliminar la basura de forma más agresiva que el segundo si el efecto se amortiza en el transcurso de unos pocos ciclos de recogida de basura.</p> <p>Lea también la sección "Ejecución de la limpieza de revisión en línea después de la limpieza de revisión sin conexión" de <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">este capítulo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>¿Tiene en cuenta las operaciones de archivos asignados en memoria?</td>
   <td>
    <ul>
     <li><strong>En entornos de Windows</strong>, siempre se exige el acceso regular a los archivos para que no se utilice el acceso asignado a la memoria. Como consejo general, toda la RAM disponible debe asignarse al montón y el tamaño de segmentCache debe aumentarse. Para aumentar segmentCache, agregue la opción segmentCache.size a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (por ejemplo, segmentCache.size=20480). Recuerde dejar fuera un poco de RAM para el sistema operativo y otros procesos.</li>
     <li><strong>En entornos que no son Windows</strong>, aumente el tamaño de la memoria física para mejorar la asignación de memoria del repositorio.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Supervisar limpieza de revisión en línea {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Qué se debe supervisar durante la limpieza de revisión en línea?</strong></td>
   <td>
    <ul>
     <li>El espacio en disco debe supervisarse cuando Limpieza de revisión en línea está habilitada. La limpieza no se ejecuta o finaliza de forma preventiva cuando no hay suficiente espacio en disco.</li>
     <li>Consulte los registros para ver la hora de finalización de Limpieza de revisión en línea. No debe tardar más de 2 horas.</li>
     <li>Número de puntos de comprobación. Si hay más de 3 puntos de comprobación cuando se ejecuta la compactación, se recomienda limpiar los puntos de comprobación.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo se comprueba si la limpieza de revisión en línea se ha completado correctamente?</strong></td>
   <td><p>Puede comprobar si la Limpieza de revisión en línea se ha completado correctamente comprobando los registros.</p> <p>Por ejemplo, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>" significa que el paso de compactación se completó correctamente a menos que esté precedido por el mensaje "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>", lo que significa que hubo demasiada carga simultánea.</p> <p>En consecuencia, hay un mensaje "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>" para la finalización correcta del paso de limpieza.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>¿Dónde podemos encontrar las estadísticas de las últimas ejecuciones de Limpieza de revisión en línea?</strong></td>
   <td><p>El estado, el progreso y las estadísticas se exponen mediante JMX (<code>SegmentRevisionGarbageCollection</code> MBean). Para obtener más información sobre el MBean <code>SegmentRevisionGarbageCollection</code>, lea el <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">párrafo siguiente</a>.</p> <p>El progreso se puede rastrear a través del atributo <code>EstimatedRevisionGCCompletion</code> del <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>Puede obtener una referencia del MBean utilizando <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Las estadísticas solo están disponibles desde el último inicio del sistema. <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">Se podría usar la herramienta de supervisión externa para mantener los datos más allá del tiempo de actividad de AEM</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué son las entradas de registro relevantes?</strong></td>
   <td>
    <ul>
     <li>La limpieza de revisión en línea se ha iniciado o detenido
      <ul>
       <li>Limpieza de revisión en línea se compone de tres fases: estimación, compactación y limpieza. La estimación puede forzar que se omitan la compactación y la limpieza si el repositorio no contiene suficiente basura. En la última versión de AEM, el mensaje "<code>TarMK GC #{}: estimation started</code>" marca el inicio de la estimación, "<code>TarMK GC #{}: compaction started, strategy={}</code>" marca el inicio de la compactación y "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>" marca el inicio de la limpieza.</li>
      </ul> </li>
     <li>Espacio en disco obtenido por la limpieza de revisión
      <ul>
       <li>El espacio solo se recupera cuando finaliza la fase de limpieza. La finalización de la fase de limpieza se marca con el mensaje de registro "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". El tamaño de la limpieza posterior es de {} ({} bytes) y el espacio reclamado es de {} ({} bytes). La profundidad/peso del mapa de compactación es de {}/{} ({} bytes/{}).".</li>
      </ul> </li>
     <li>Se ha producido un problema durante la limpieza de revisión
      <ul>
       <li>Hay muchas condiciones de error, todas ellas están marcadas por mensajes de registro WARN o ERROR que comienzan con "TarMK GC".</li>
      </ul> </li>
    </ul> <p>Además, consulte la sección <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Solución de problemas basada en mensajes de error</a> a continuación.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo se puede comprobar cuánto espacio se ha reclamado después de que se haya completado la Limpieza de revisión en línea?</strong></td>
   <td>Hay un mensaje en el registro al final del ciclo de limpieza: "<code>TarMK GC #3: cleanup completed</code>" que incluye el tamaño del repositorio y la cantidad de basura reclamada.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo comprobar la integridad del repositorio después de que se haya completado la limpieza de revisión en línea?</strong></td>
   <td><p>No es necesaria una comprobación de integridad del repositorio después de la Limpieza de revisión en línea. </p> <p>Sin embargo, puede realizar las siguientes acciones para comprobar el estado del repositorio después de la limpieza:</p>
    <ul>
     <li>Una <a href="/help/sites-deploying/consistency-check.md" target="_blank">comprobación de recorrido</a> del repositorio</li>
     <li>Utilice la herramienta oak-run después de que se haya completado el proceso de limpieza para comprobar las incoherencias. Para obtener más información sobre cómo hacerlo, consulte la <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Documentación de Apache.</a> No necesita cerrar AEM para ejecutar la herramienta.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo detectar si la Limpieza de revisión en línea ha fallado y cuáles son los pasos para recuperarse?</strong></td>
   <td>Las condiciones de error se marcan con mensajes de registro WARN o ERROR que comienzan con "TarMK GC". Además, consulte la sección <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Solución de problemas basada en mensajes de error</a> a continuación.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué información se expone en la comprobación de estado de Revision Cleanup? ¿Cómo y cuándo contribuyen a los niveles de estado codificados por colores? </strong></td>
   <td><p>La comprobación de estado de limpieza de revisión forma parte del <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">tablero de operaciones</a>.<br /> </p> <p>El estado es <strong>VERDE</strong> si la última ejecución de la tarea de mantenimiento Limpieza de revisiones en línea se completó correctamente.</p> <p>Es <strong>AMARILLO</strong> si la tarea de mantenimiento Limpieza de revisión en línea se canceló una vez.<br /> </p> <p>Es <strong>RED</strong> si la tarea de mantenimiento Limpieza de revisiones en línea se canceló tres veces seguidas. <strong>En este caso se requiere interacción manual</strong> o es probable que Limpieza de revisión en línea vuelva a fallar. Para obtener más información, lea la sección <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">Solución de problemas</a> a continuación.<br /> </p> <p>Además, el estado de la comprobación de estado se restablece después de reiniciar el sistema. Por lo tanto, una instancia recién reiniciada muestra un estado verde en la comprobación de estado de limpieza de revisión.  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">Se podría usar la herramienta de supervisión externa para mantener los datos más allá del tiempo de actividad de AEM</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Cómo monitorizar la Limpieza automática en una instancia de espera?</strong></p> </td>
   <td><p>El estado, el progreso y las estadísticas se exponen mediante JMX usando el MBean <code>SegmentRevisionGarbageCollection</code>. Consulte también la siguiente <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">documentación de Oak</a>. </p> <p>Puede obtener una referencia del MBean utilizando <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Las estadísticas solo están disponibles desde el último inicio del sistema.  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">Se podría usar la herramienta de supervisión externa para mantener los datos más allá del tiempo de actividad de AEM</a>.</p> <p>Los archivos de registro también se pueden utilizar para comprobar el estado, el progreso y las estadísticas de Limpieza automática.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>¿Qué se debe monitorizar durante la limpieza automática en una instancia de espera?</strong></p> </td>
   <td>
    <ul>
     <li>El espacio en disco debe supervisarse cuando se ejecute el Liberador de espacio automático.</li>
     <li>Tiempo de finalización (a través de los registros) para garantizar que no se superen las 2 horas.</li>
     <li>Tamaño del almacén de segmentos después de ejecutar la limpieza automática. El tamaño del almacén de segmentos en la instancia de espera debe ser aproximadamente el mismo que el de la instancia principal.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Solución de problemas de revisión en línea {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Qué es lo peor que puede pasar si no ejecuta Limpieza de revisión en línea?</strong></td>
   <td>La instancia de AEM se queda sin espacio en disco, lo que provoca interrupciones en la producción.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Es problemático el alto tráfico de usuarios para ejecutar la limpieza de revisión en línea en una instancia de publicación?</strong></td>
   <td>El alto tráfico de usuarios afecta si la fase de compactación puede finalizar correctamente o no.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Según la comprobación de estado y las entradas de registro, Limpieza de revisiones en línea no se ha completado correctamente tres veces seguidas. ¿Qué se necesita para completar correctamente la limpieza de revisión en línea?</strong></td>
   <td>Puede realizar varios pasos para encontrar y solucionar el problema:<br />
    <ul>
     <li>Primero, compruebe las entradas de registro <br /> </li>
     <li>Según la información de los registros, realice las acciones adecuadas:
      <ul>
       <li>Si los registros muestran cinco ciclos compactos perdidos y un tiempo de espera en el ciclo <code>forceCompact</code>, programe la ventana de mantenimiento a un tiempo de inactividad cuando la cantidad de escrituras en el repositorio sea baja. Puede comprobar las escrituras del repositorio en la herramienta de monitorización de métricas del repositorio en <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>Si la limpieza se detuvo al final de la ventana de mantenimiento, asegúrese de que la configuración de la ventana de mantenimiento en la interfaz de usuario Tareas de mantenimiento es lo suficientemente grande</li>
       <li>Si la memoria de pila disponible no es suficiente, asegúrese de que la instancia tenga suficiente memoria.</li>
       <li>Si se produce una reacción tardía, el almacén de segmentos puede crecer demasiado para que Limpieza de revisión en línea se complete incluso dentro de un período de mantenimiento más largo. Por ejemplo, si no se completó correctamente la Limpieza de revisión en línea en la última semana, se recomienda planificar un mantenimiento sin conexión y ejecutar la Limpieza de revisión sin conexión para devolver el almacén de segmentos a un tamaño manejable.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué debe hacerse cuando la alerta Comprobación de estado está activada?</strong></td>
   <td>Véase el punto anterior.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué sucede si Limpieza de revisión en línea se queda sin tiempo durante la ventana de mantenimiento programado?</strong></td>
   <td>La Limpieza de revisión en línea se cancela y se quitan las sobras. Se inicia de nuevo la próxima vez que se programa la ventana de mantenimiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>¿Qué está causando que se registren <code>SegmentNotFoundException</code> instancias en <code>error.log</code> y cómo puedo recuperarme?</strong></td>
   <td><p>El TarMK registra un <code>SegmentNotFoundException</code> cuando intenta obtener acceso a una unidad de almacenamiento (un segmento) que no encuentra. Hay tres escenarios que podrían causar este problema:</p>
    <ol>
     <li>Una aplicación que elude los mecanismos de acceso recomendados (como Sling y la API JCR) y utiliza una API/SPI de nivel inferior para acceder al repositorio y, a continuación, supera el tiempo de retención de un segmento. Es decir, mantiene una referencia a una entidad más larga que el tiempo de retención permitido por Limpieza de revisión en línea (de forma predeterminada, 24 horas). Este caso es transitorio y no provoca daños en los datos. Para recuperarse, la herramienta oak-run debe utilizarse para confirmar la naturaleza transitoria de la excepción (la comprobación oak-run no debe notificar ningún error). Para ello, la instancia debe desconectarse y reiniciarse después.</li>
     <li>Un evento externo dañó los datos del disco. Esto puede ser un error de disco, espacio insuficiente en disco o una modificación accidental de los archivos de datos necesarios. En este caso, la instancia debe desconectarse y repararse mediante la comprobación de oak-run. Para obtener más información sobre cómo realizar la comprobación de oak-run, lea la siguiente <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">documentación de Apache</a>.</li>
     <li>Aborde todos los demás sucesos a través del <a href="https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support" target="_blank">Servicio de atención al cliente de Adobe</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Solución De Problemas Según Mensajes De Error {#troubleshooting-based-on-error-messages}

El error.log es detallado si hay incidentes durante el proceso de limpieza de revisión en línea. La siguiente matriz tiene como objetivo explicar los mensajes más comunes y proporcionar posibles soluciones:

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message does not mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Fase</th>
    <th>Mensajes de registro</th>
    <th>Explicación</th>
    <th>Siguientes pasos</th>
  </tr>  
  <tr>
    <td>Estimación</td>
    <td>TarMK GC #2: estimación omitida porque la compactación está en pausa.</td>
    <td>La fase de estimación se omite cuando la configuración desactiva la compactación en el sistema.</td>
    <td>Activar Limpieza de revisión en línea.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>#2 de GC TarMK: estimación interrumpida: ${REASON}. Omitiendo la compactación.</td>
    <td>La fase de estimación terminó prematuramente. Algunos ejemplos de eventos que podrían interrumpir la fase de estimación: no hay suficiente memoria o espacio en disco en el sistema host.</td>
    <td>Depende de la razón dada.</td>
  </td>
  </tr>
  <tr>
    <td>Compactación</td>
    <td>TarMK GC #2: compactación en pausa.</td>
    <td>Mientras la fase de compactación esté en pausa por la configuración, no se ejecuta ni la fase de estimación ni la fase de compactación.</td>
    <td>Activar limpieza de revisión en línea.</td>
  </td>
  </tr>
   <tr>
    <td>N/D</td>
    <td>#2 de TarMK GC: compactación cancelada: ${REASON}.</td>
    <td>La fase de compactación terminó prematuramente. Algunos ejemplos de eventos que podrían interrumpir la fase de compactación: no hay suficiente memoria o espacio en disco en el sistema host. Además, la compactación también se puede cancelar apagando el sistema o cancelándolo explícitamente a través de interfaces administrativas como la ventana de mantenimiento dentro del tablero de operaciones.</td>
    <td>Depende de la razón dada.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>TarMK GC #2: error de compactación en 32.902 min (1974140 ms), después de 5 ciclos.</td>
    <td>Este mensaje no significa que haya un error irrecuperable, sino que solo esa compactación se ha terminado después de algunos intentos. Lea también <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">el párrafo siguiente.</a></td>
    <td>Lea la siguiente <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">documentación de Oak</a> y la última pregunta de la sección Ejecución de la limpieza de revisión en línea.</a></td>
  </td>
  </tr>
  <tr>
    <td>Limpiar</td>
    <td>#2 de TarMK GC: limpieza interrumpida.</td>
    <td>La limpieza se ha cancelado cerrando el repositorio. No se espera que esto afecte a la coherencia. Además, es muy probable que el espacio en disco no se recupere en su totalidad. Se reclamará durante el siguiente ciclo de limpieza de revisión.</td>
    <td>Investigue por qué se ha cerrado el repositorio y continúe intentando evitar cerrarlo durante las ventanas de mantenimiento.</td>
  </td>
  </tr>
  </tbody>
</table>

## Cómo ejecutar la limpieza de revisión sin conexión {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>Utilice una versión de la herramienta ejecutada por Oak con un número de versión (principal y secundaria) que coincida con la versión principal de Oak de la instalación de AEM. Por ejemplo, si la instancia de AEM tiene Oak Core versión 1.22.x, debe utilizar la última versión de la herramienta 1.22.x ejecutada por Oak.

Adobe proporciona una herramienta llamada **Oak-run** para realizar la limpieza de revisión. Se puede descargar en la siguiente ubicación:

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

La herramienta es un JAR ejecutable que se puede ejecutar manualmente para compactar el repositorio. El proceso se denomina limpieza de revisión sin conexión porque el repositorio debe cerrarse para ejecutar correctamente la herramienta. Asegúrese de planificar la limpieza de acuerdo con la ventana de mantenimiento.

Para obtener sugerencias sobre cómo aumentar el rendimiento del proceso de limpieza, vea [Aumentar el rendimiento de la limpieza de revisiones sin conexión](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>También puede borrar los puntos de comprobación antiguos antes de que se realice el mantenimiento (pasos 2 y 3 del procedimiento que se describe a continuación). Esto solo se recomienda para instancias que tienen más de 100 puntos de comprobación.

1. Asegúrese siempre de tener una copia de seguridad reciente de la instancia de AEM.

   Cierre AEM.

1. (Opcional) Utilice la herramienta para buscar puntos de comprobación antiguos:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (Opcional) A continuación, elimine los puntos de comprobación sin referencia:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. Ejecute la compactación y espere a que se complete:

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### Aumento del rendimiento de la limpieza de revisión sin conexión {#increasing-the-performance-of-offline-revision-cleanup}

La herramienta oak-run introduce varias funciones que pretenden aumentar el rendimiento del proceso de limpieza de revisión y minimizar la ventana de mantenimiento en la medida de lo posible.

La lista incluye varios parámetros de línea de comandos, como se describe a continuación:

* **-mmap.** Puede establecer esto como verdadero o falso. Si se establece en true, se utiliza el acceso asignado a la memoria. Si se establece en false, se utiliza el acceso a archivos. Si no se especifica, el acceso asignado a memoria se utiliza en sistemas de 64 bits y el acceso a archivos se utiliza en sistemas de 32 bits. En Windows, el acceso regular a archivos siempre se aplica y esta opción se ignora. **Este parámetro ha reemplazado el parámetro -Dtar.memoryMapped.**

* **-Dupdate.limit**. Define el umbral para el vaciado de una transacción temporal en disco. El valor predeterminado es 10000.

* **-Dcompress-interval**. Número de entradas de mapa de compactación que se deben mantener hasta comprimir el mapa actual. El valor predeterminado es 1000000. Debe aumentar este valor a un número aún mayor para obtener un rendimiento más rápido, si hay suficiente memoria disponible. **Este parámetro se ha quitado en la versión 1.6 de Oak y no tiene ningún efecto.**

* **-Dcompaction-progress-log**. El número de nodos compactados que se registran. El valor predeterminado es 150000, lo que significa que los primeros nodos compactados 150000 se registran durante la operación. Utilícelo con el siguiente parámetro documentado a continuación.

* **-Dtar.PersistCompactionMap.** Establezca este parámetro en true para utilizar espacio en disco en lugar de memoria de montón para la persistencia de mapa de compactación. Requiere la herramienta oak-run **versiones 1.4** y superiores. Para obtener más información, consulte la pregunta 3 en la sección [Preguntas más frecuentes sobre la limpieza de revisiones sin conexión](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions). **Este parámetro se ha quitado en la versión 1.6 de Oak y no tiene ningún efecto.**

* **: forzar.** Forzar la compactación e ignorar una versión de almacén de segmentos no coincidente.

>[!CAUTION]
>
>Al usar el parámetro `--force`, se actualiza el almacén de segmentos a la versión más reciente, lo cual es incompatible con versiones de Oak anteriores. Además, considere que no es posible bajar de categoría. Por lo general, estos parámetros deben utilizarse con precaución y solo si tiene conocimientos sobre cómo utilizarlos.

Un ejemplo de los parámetros en uso:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### Métodos adicionales para activar la limpieza de revisión {#additional-methods-of-triggering-revision-cleanup}

Además de los métodos presentados anteriormente, también puede almacenar en déclencheur el mecanismo de limpieza de revisión mediante la consola JMX de la siguiente manera:

1. Abra la consola JMX yendo a [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. Haga clic en el MBean **RevisionGarbageCollection**.
1. En la siguiente ventana, haga clic en **startRevisionGC()** y luego en **Invoke** para iniciar el trabajo de recolección de basura de revisión.

### Preguntas más frecuentes sobre la limpieza de revisiones sin conexión {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>¿Cuáles son los factores que determinan la duración de la limpieza de revisión sin conexión?</strong></td>
   <td><p>El tamaño del repositorio y el número de revisiones que se deben limpiar determinan la duración de la limpieza.</p> </td>
  </tr>
  <tr>
   <td><strong>¿Cuál es la diferencia entre una revisión y una versión de página?</strong></td>
   <td>
    <ul>
     <li><strong>Revisión de Oak:</strong> Oak organiza todo el contenido en una jerarquía de árbol grande que consta de nodos y propiedades. Cada instantánea o revisión de este árbol de contenido es inmutable y los cambios en el árbol se expresan como una secuencia de nuevas revisiones. Normalmente, cada modificación de contenido déclencheur una nueva revisión. Consulte también <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> Seguir vínculo</a>.</li>
     <li><strong>Versión de la página:</strong> El control de versiones crea una "captura de pantalla" de una página en un momento específico. Normalmente, se crea una nueva versión cuando se activa una página. Para obtener más información, vea <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">Trabajar con versiones de página</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>¿Cómo acelerar la tarea de limpieza de revisión sin conexión si no se completa en un plazo de 8 horas?</strong></td>
   <td>Si la tarea de revisión no se completa en un plazo de 8 horas y los <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">volcados de subprocesos</a> revelan que el punto interactivo principal es <code>InMemoryCompactionMap.findEntry</code>, use el siguiente parámetro con la herramienta oak-run <strong>versiones 1.4 </strong>o superior: <code>-Dtar.PersistCompactionMap=true</code>. El parámetro <code>-Dtar.PersistCompactionMap</code> se ha quitado en la versión 1.6 de Oak.</td>
  </tr>
 </tbody>
</table>
