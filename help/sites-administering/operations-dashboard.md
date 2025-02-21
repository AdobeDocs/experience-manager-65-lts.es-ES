---
title: Tablero de operaciones
description: Aprenda a utilizar el tablero de operaciones en Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '5743'
ht-degree: 2%

---

# Tablero de operaciones {#operations-dashboard}

## Introducción {#introduction}

El tablero de operaciones de AEM 6 ayuda a los operadores del sistema a monitorizar el estado del sistema de AEM de un vistazo. También proporciona información de diagnóstico generada automáticamente sobre aspectos relevantes de AEM y le permite configurar y ejecutar la automatización de mantenimiento independiente para reducir significativamente las operaciones del proyecto y los casos de soporte. El tablero de operaciones se puede ampliar con comprobaciones de estado y tareas de mantenimiento personalizadas. Además, se puede acceder a los datos del tablero de operaciones desde herramientas de monitorización externas a través de JMX.

**El tablero de operaciones:**

* Es un estado del sistema de un solo clic para ayudar a los departamentos de operaciones a ganar en eficiencia
* Proporciona información general sobre el estado del sistema en un solo lugar centralizado
* Reduce el tiempo para buscar, analizar y solucionar problemas
* Proporciona automatización de mantenimiento independiente que ayuda a reducir significativamente los costes de operaciones del proyecto

Se puede acceder a él yendo a **Herramientas** - **Operaciones** desde la pantalla de bienvenida de AEM.

>[!NOTE]
>
>Para poder acceder al tablero de operaciones, el usuario que ha iniciado sesión debe formar parte del grupo de usuarios &quot;Operadores&quot;. Para obtener más información, consulte la documentación sobre [Administración de usuarios, grupos y derechos de acceso](/help/sites-administering/user-group-ac-admin.md).

## Informes de estado {#health-reports}

El sistema de informes de estado proporciona información sobre el estado de una instancia de AEM mediante las comprobaciones de estado de Sling. Esta operación se realiza mediante solicitudes OSGI, JMX, HTTP (mediante JSON) o a través de la interfaz de usuario táctil. Ofrece mediciones y umbrales de ciertos contadores configurables y, a veces, ofrece información sobre cómo resolver el problema.

Tiene varias características que se describen a continuación.

## Comprobación del estado {#health-checks}

Los **Informes de mantenimiento** son un sistema de tarjetas que indican un estado de salud bueno o malo en un área específica del producto. Estas tarjetas son visualizaciones de las comprobaciones de estado de Sling, que agregan datos de JMX y otras fuentes y exponen de nuevo la información procesada como MBeans. Estos MBean también se pueden inspeccionar en la [consola web JMX](/help/sites-administering/jmx-console.md), en el dominio **org.apache.sling.healthCheck**.

Se puede acceder a la interfaz de los informes de estado a través del menú **Herramientas** - **Operaciones** - **Informes de estado** de la pantalla de bienvenida de AEM, o directamente a través de la siguiente URL:

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

El sistema de tarjetas expone tres estados posibles: **OK**, **WARN** y **CRITICAL**. Los estados son el resultado de reglas y umbrales, que se pueden configurar pasando el ratón sobre la tarjeta y haciendo clic en el icono de engranaje de la barra de acciones:

![chlimage_1-117](assets/chlimage_1-117.png)

### Tipos de comprobación de estado {#health-check-types}

Existen dos tipos de comprobaciones de estado en AEM 6:

1. Comprobaciones de estado individuales
1. Comprobación de estado compuesto

Una **comprobación de estado individual** es una única comprobación de estado que corresponde a una tarjeta de estado. Las comprobaciones de estado individuales se pueden configurar con reglas o umbrales y pueden proporcionar una o más sugerencias y vínculos para resolver los problemas de estado identificados. Veamos la comprobación &quot;Registrar errores&quot; como ejemplo: si hay entradas de ERROR en los registros de instancias, búsquelas en la página de detalles de la comprobación de estado. En la parte superior de la página, puede ver un vínculo al analizador &quot;Mensaje de registro&quot; en la sección Herramientas de diagnóstico, que le permite analizar estos errores con más detalle y reconfigurar los registradores.

Una **comprobación de estado compuesta** es una comprobación que agrega información de varias comprobaciones individuales.

Las comprobaciones de estado compuestas se configuran con la ayuda de **etiquetas de filtro**. En esencia, todas las comprobaciones individuales que tienen la misma etiqueta de filtro se agrupan como una comprobación de estado compuesta. Una comprobación de estado compuesta tiene el estado OK sólo si todas las comprobaciones únicas que agrega tienen también el estado OK.

### Cómo crear comprobaciones de estado {#how-to-create-health-checks}

En el tablero de operaciones, puede visualizar el resultado de las comprobaciones de estado individuales y compuestas.

### Creación de una comprobación de estado individual {#creating-an-individual-health-check}

La creación de una comprobación de estado individual implica dos pasos: implementar una comprobación de estado de Sling y agregar una entrada para la comprobación de estado en los nodos de configuración del panel.

1. Para crear una comprobación de estado de Sling, cree un componente OSGI que implemente la interfaz Sling HealthCheck. Añada este componente dentro de un paquete. Las propiedades del componente identifican completamente la comprobación de estado. Una vez instalado el componente, se crea automáticamente un MBean JMX para la comprobación de estado. Consulte la [Documentación de comprobación de estado de Sling](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) para obtener más información.

   Ejemplo de un componente Comprobación de estado de Sling, escrito con anotaciones del componente Servicio OSGI:

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >La propiedad `MBEAN_NAME` define el nombre del mbean generado para esta comprobación de estado.

1. Después de crear una comprobación de estado, se debe crear un nuevo nodo de configuración para que sea accesible en la interfaz del tablero de operaciones. Para este paso, es necesario conocer el nombre del MBean JMX de la comprobación de estado (la propiedad `MBEAN_NAME`). Para crear una configuración para la comprobación de estado, abra CRXDE y agregue un nodo (de tipo **nt:unstructured**) en la siguiente ruta: `/apps/settings/granite/operations/hc`

   Las siguientes propiedades deben establecerse en el nuevo nodo:

   * **Nombre:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valor:** `granite/operations/components/mbean`

   * **Nombre:** `resource`

      * **Tipo:** `String`
      * **Valor:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >La ruta de acceso al recurso anterior se crea de la siguiente manera: si el nombre de mbean de la comprobación de estado es &quot;test&quot;, agregue &quot;test&quot; al final de la ruta de acceso `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >Por lo tanto, el camino final es el siguiente:
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >Asegúrese de que la ruta de acceso `/apps/settings/granite/operations/hc` tiene las siguientes propiedades definidas como true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >Este proceso indica al administrador de configuración que combine las nuevas configuraciones con las existentes de `/libs`.

### Creación de una comprobación de estado compuesta {#creating-a-composite-health-check}

La función de una comprobación de estado compuesta es agregar varias comprobaciones de estado individuales que compartan un conjunto de características comunes. Por ejemplo, la comprobación de estado compuesta de seguridad agrupa todas las comprobaciones de estado individuales que realizan comprobaciones relacionadas con la seguridad. El primer paso para crear una comprobación compuesta es añadir una configuración OSGI. Para que se muestre en el tablero de operaciones, se debe agregar un nuevo nodo de configuración de la misma manera que una simple comprobación.

1. Vaya al Administrador de configuración web en la consola OSGI. Acceder a `https://serveraddress:port/system/console/configMgr`
1. Busque la entrada **Apache Sling Composite Health Check**. Cuando lo encuentre, verá que ya hay dos configuraciones disponibles: una para las comprobaciones del sistema y otra para las comprobaciones de seguridad.
1. Cree una configuración pulsando el botón &quot;+&quot; en el lado derecho de la configuración. Aparece una nueva ventana, como se muestra a continuación:

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. Cree una configuración y guárdela. Se crea un Mbean con la nueva configuración.

   El propósito de cada propiedad de configuración es el siguiente:

   * **Nombre (hc.name):** Nombre de la comprobación de estado compuesta. Se recomienda un nombre significativo.
   * **Etiquetas (hc.tags):** Las etiquetas para esta comprobación de estado. Si esta comprobación de estado compuesta debe formar parte de otra comprobación de estado compuesta (por ejemplo, en una jerarquía de comprobaciones de estado), agregue las etiquetas con las que está relacionada esta combinación.
   * **Nombre de MBean (hc.mbean.name):** El nombre del MBean que se le dio al MBean JMX de esta comprobación de estado compuesta.
   * **Etiquetas de filtro (filter.tags):** Propiedad específica de las comprobaciones de estado compuestas. Estas etiquetas se agregan mediante el compuesto. La comprobación de estado compuesta agrega bajo su grupo todas las comprobaciones de estado que tengan cualquier etiqueta que coincida con cualquiera de las etiquetas de filtro de este compuesto. Por ejemplo, una comprobación de estado compuesta que tiene las etiquetas de filtro **test** y **check**, agrega todas las comprobaciones de estado individuales y compuestas que tienen cualquiera de las etiquetas **test** y **check** en su propiedad tags ( `hc.tags`).

   >[!NOTE]
   >
   >Se crea un nuevo MBean JMX para cada nueva configuración de la comprobación de estado compuesta de Apache Sling.**

1. Por último, la entrada de la comprobación de estado compuesta que se ha creado debe agregarse en los nodos de configuración del tablero de operaciones. El procedimiento es el mismo que con las comprobaciones de estado individuales: se debe crear un nodo de tipo **nt:unstructured** en `/apps/settings/granite/operations/hc`. La propiedad resource del nodo está definida por el valor de **hc.media.name** en la configuración OSGI.

   Por ejemplo, si creó una configuración y estableció el valor **hc.mbean.name** en **diskusage**, los nodos de configuración lucirán de la siguiente manera:

   * **Nombre:** `Composite Health Check`

      * **Tipo:** `nt:unstructured`

   Con las siguientes propiedades:

   * **Nombre:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valor:** `granite/operations/components/mbean`

   * **Nombre:** `resource`

      * **Tipo:** `String`
      * **Valor:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >Si crea comprobaciones de estado individuales que pertenecen lógicamente a una comprobación compuesta que ya está presente en el panel de forma predeterminada, se capturan automáticamente y se agrupan en la comprobación compuesta correspondiente. Como tal, no es necesario crear un nodo de configuración para estas comprobaciones.
   >
   >Por ejemplo, si crea una comprobación de estado de seguridad individual, asígnele la etiqueta &quot;**security**&quot; y se instalará. Aparece automáticamente bajo la comprobación compuesta Comprobaciones de seguridad en el tablero de operaciones.

### Comprobaciones de estado proporcionadas con AEM {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de zHealthcheck</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Rendimiento de consultas</td>
   <td><p>Esta comprobación de estado se simplificó <strong>en AEM 6.4</strong>, y ahora comprueba el MBean <code>Oak QueryStats</code> refactorizado recientemente, más específicamente el atributo <code>SlowQueries </code>. Si las estadísticas contienen consultas lentas, la comprobación de estado devuelve una advertencia. De lo contrario, devuelve el estado OK.<br /> </p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=queriesStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Longitud de la cola de observación</td>
   <td><p>La longitud de la cola de observación se repite en todos los oyentes de eventos y observadores en segundo plano, compara su <code>queueSize </code> con su <code>maxQueueSize</code> y:</p>
    <ul>
     <li>devuelve el estado crítico si el valor <code>queueSize</code> supera el valor <code>maxQueueSize</code> (entonces se eliminarían los eventos)</li>
     <li>devuelve una advertencia si el valor <code>queueSize</code> supera el valor <code>maxQueueSize * WARN_THRESHOLD</code> (el valor predeterminado es 0,75) </li>
    </ul> <p>La longitud máxima de cada cola proviene de configuraciones independientes (Oak y AEM) y no se puede configurar a partir de esta comprobación de estado. El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=ObservationQueueLengthHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Límites de recorrido de la consulta</td>
   <td><p>Límites de recorrido de consultas comprueba el MBean <code>QueryEngineSettings</code>, más específicamente los atributos <code>LimitInMemory</code> y <code>LimitReads</code>, y devuelve el siguiente estado:</p>
    <ul>
     <li>devuelve el estado de advertencia si uno de los límites es igual o superior a <code>Integer.MAX_VALUE</code></li>
     <li>devuelve el estado de advertencia si uno de los límites es inferior a 10000 (la configuración recomendada de Oak)</li>
     <li>devuelve el estado Crítico si no se puede recuperar <code>QueryEngineSettings</code> o alguno de los límites</li>
    </ul> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=queryTraversalLimitsBundle,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Relojes sincronizados</td>
   <td><p>Esta comprobación solo es relevante para <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">clústeres de almacén de nodos de documentos</a>. Devuelve el siguiente estado:</p>
    <ul>
     <li>devuelve el estado Advertencia cuando los relojes de instancia no están sincronizados y sobrepasan un umbral bajo predefinido</li>
     <li>devuelve el estado Crítico cuando los relojes de instancia no están sincronizados y sobrepasan un umbral alto predefinido</li>
    </ul> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=slingDiscoveryOakSynchronizedClocks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Índices asíncronos</td>
   <td><p>Comprobación de los índices asíncronos:</p>
    <ul>
     <li>devuelve un estado crítico si falla al menos una ruta de indexación</li>
     <li>comprueba <code>lastIndexedTime</code> para todas las rutas de indización y:
      <ul>
       <li>devuelve un estado crítico si es hace más de dos horas </li>
       <li>devuelve un estado de advertencia si está entre 2 horas y 45 minutos atrás </li>
       <li>devuelve el estado OK si es hace menos de 45 minutos </li>
      </ul> </li>
     <li>si no se cumple ninguna de estas condiciones, devuelve el estado OK</li>
    </ul> <p>Los umbrales de estado Crítico y Avisar son configurables. El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=asyncIndexHealthCheck,type=HealthCheck</a>.</p> <p><strong>Nota: </strong>Esta comprobación de estado está disponible con AEM 6.4 y se ha trasladado a AEM 6.3.0.1.</p> </td>
  </tr>
  <tr>
   <td>Índices grandes de Lucene</td>
   <td><p>Esta comprobación utiliza los datos expuestos por el MBean <code>Lucene Index Statistics</code> para identificar índices y devoluciones grandes:</p>
    <ul>
     <li>un estado de advertencia si hay un índice con más de 1000 millones de documentos</li>
     <li>un estado crítico si hay un índice con más de 1500 millones de documentos</li>
    </ul> <p>Los umbrales se pueden configurar y el MBean de la comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=largeIndexHealthCheck,type=HealthCheck.</a></p> <p><strong>Nota: </strong>Esta comprobación está disponible con AEM 6.4 y se ha trasladado a AEM 6.3.2.0.</p> </td>
  </tr>
  <tr>
   <td>Mantenimiento del sistema</td>
   <td><p>Mantenimiento del sistema es una comprobación compuesta que devuelve el estado OK si todas las tareas de mantenimiento se están ejecutando según lo configurado. Tenga en cuenta que:</p>
    <ul>
     <li>cada tarea de mantenimiento va acompañada de una comprobación de estado asociada</li>
     <li>si una tarea no se añade a una ventana de mantenimiento, su comprobación de estado devuelve Crítico</li>
     <li>configure las tareas de mantenimiento Registro de auditoría y Depuración del flujo de trabajo o elimínelas de las ventanas de mantenimiento. Si no se configuran, estas tareas fallan en el primer intento de ejecución, por lo que la comprobación de mantenimiento del sistema devuelve el estado crítico.</li>
     <li><strong>Con AEM 6.4</strong>, también hay una comprobación para la tarea <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Mantenimiento de binarios de Lucene</a></li>
     <li>en AEM 6.2 y versiones posteriores, la comprobación de mantenimiento del sistema devuelve un estado de advertencia justo después del inicio, ya que las tareas nunca se ejecutan. A partir de la versión 6.3, funcionan correctamente si aún no se ha alcanzado la primera ventana de mantenimiento.</li>
    </ul> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthCheck:name=systemcheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Cola de replicación</td>
   <td><p>Esta comprobación recorre en iteración los agentes de replicación y observa sus colas. Para el elemento en la parte superior de la cola, la comprobación determina cuántas veces el agente ha reintentado la replicación. Si el agente reintentó la replicación más allá del valor del parámetro <code>numberOfRetriesAllowed</code>, devolverá una advertencia. El parámetro <code>numberOfRetriesAllowed</code> se puede configurar. </p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=replicationQueue,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Trabajos de Sling</td>
   <td>
    <div>
      Sling Jobs comprueba el número de trabajos en cola en JobManager, lo compara con el
     <code>maxNumQueueJobs</code> umbral y:
    </div>
    <ul>
     <li>devuelve un valor Critical si hay más de <code>maxNumQueueJobs</code> en la cola</li>
     <li>devuelve un valor Critical si hay trabajos activos de larga duración con más de una hora</li>
     <li>devuelve un valor Critical si hay trabajos en cola y la última hora de trabajo finalizada es anterior a 1 hora</li>
    </ul> <p>Solo se puede configurar el número máximo de trabajos en cola y tiene el valor predeterminado de 1000.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=slingJobs,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Rendimiento de solicitudes</td>
   <td><p>Esta comprobación determina <code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">la métrica Sling </a>y:</p>
    <ul>
     <li>devuelve un valor Critical si el valor del percentil 75 supera el umbral crítico (el valor predeterminado es 500 milisegundos)</li>
     <li>devuelve un valor Warn si el valor del percentil 75 supera el umbral de advertencia (el valor predeterminado es 200 milisegundos)</li>
    </ul> <p>El MBean para esta comprobación de estado es <em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=requestsStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Errores de registro</td>
   <td><p>Esta comprobación devuelve el estado de advertencia si hay errores en el registro.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=logErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Espacio en disco</td>
   <td><p>La comprobación Espacio en disco busca en el MBean <code>FileStoreStats</code>, recupera el tamaño del almacén de nodos y la cantidad de espacio en disco utilizable en la partición del almacén de nodos, y:</p>
    <ul>
     <li>devuelve una advertencia si la proporción de espacio en disco disponible respecto al tamaño del repositorio es menor que el umbral de advertencia (el valor predeterminado es 10)</li>
     <li>devuelve un valor Critical si la relación entre el espacio en disco disponible y el tamaño del repositorio es menor que el umbral crítico (el valor predeterminado es 2)</li>
    </ul> <p>Ambos umbrales se pueden configurar. La marca de verificación solo funciona en instancias con un almacén de segmentos.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=DiskSpaceHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Programador de comprobación de estado</td>
   <td><p>Esta comprobación devuelve una advertencia si la instancia tiene trabajos de Quartz en ejecución durante más de 60 segundos. El umbral de duración aceptable es configurable.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>Comprobaciones de seguridad</td>
   <td><p>La comprobación de seguridad es un compuesto que agrega los resultados de varias comprobaciones relacionadas con la seguridad. Estas comprobaciones de estado individuales solucionan problemas diferentes de la lista de comprobación de seguridad disponible en la página de documentación de <a href="/help/sites-administering/security-checklist.md">Lista de comprobación de seguridad.</a> La comprobación es útil como prueba de humo de seguridad cuando se inicia la instancia. </p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=securitycheck,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>Paquetes activos</td>
   <td><p>Paquetes activos comprueba el estado de todos los paquetes y:</p>
    <ul>
     <li>devuelve el estado Advertir si alguno de los paquetes no está activo o activo (a partir de, con activación diferida)</li>
     <li>ignora el estado de los paquetes en la lista de omisión</li>
    </ul> <p>El parámetro de lista de omisión se puede configurar.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=inactiveBundles,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Comprobación de caché de código</td>
   <td><p>Una comprobación de estado que comprueba varias condiciones de JVM que pueden almacenar en déclencheur un error de CodeCache presente en Java™ 7:</p>
    <ul>
     <li>devuelve un mensaje de advertencia si la instancia se está ejecutando en Java™ 7 y el vaciado de caché de código está habilitado</li>
     <li>devuelve un valor Warn si la instancia se está ejecutando en Java™ 7 y el tamaño de la caché de código reservada es inferior a un umbral mínimo (el valor predeterminado es 90 MB)</li>
    </ul> <p>El umbral <code>minimum.code.cache.size</code> se puede configurar. Para obtener más información sobre el error, consulte <a href="https://bugs.java.com/bugdatabase/"> y luego busque el identificador de error 8012547</a>.</p> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=codeCacheHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Errores de ruta de búsqueda de medios</td>
   <td><p>Comprueba si hay recursos en la ruta de acceso <code>/apps/foundation/components/primary</code> y:</p>
    <ul>
     <li>devuelve un valor de tipo Warn si hay nodos secundarios en <code>/apps/foundation/components/primary</code></li>
    </ul> <p>El MBean para esta comprobación de estado es <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthCheck:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Configuración de comprobación de estado {#health-check-configuration}

De forma predeterminada, para una instancia de AEM predeterminada, las comprobaciones de estado se ejecutan cada 60 segundos.

Puede configurar **Period** con la [configuración de OSGi](/help/sites-deploying/configuring-osgi.md) **Configuración de la comprobación de estado de la consulta** (com.adobe.granite.queries.impl.hc.QueryHealthCheckMetrics).

## Monitorización con servicios externos {#monitoring-with-external-services}

La integración es posible con tecnologías o proveedores externos. Consulte su documentación para obtener más información.

## Herramientas de diagnóstico {#diagnosis-tools}

El tablero de operaciones también proporciona acceso a las herramientas de diagnóstico, que pueden ayudar a encontrar y solucionar las causas básicas de las advertencias procedentes del tablero de comprobación de estado, así como a proporcionar información de depuración importante para los operadores del sistema.

Entre sus características más importantes se encuentran:

* Un analizador de mensajes de registro
* La capacidad de acceder a los volcados de pila e hilos
* Analizadores de rendimiento de consultas y solicitudes

Puede acceder a la pantalla Herramientas de diagnóstico si visita **Herramientas - Operaciones - Diagnóstico** desde la pantalla de bienvenida de AEM. También puede tener acceso a la pantalla si accede directamente a la siguiente dirección URL: `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### Mensajes de registro {#log-messages}

La interfaz de usuario de mensajes de registro muestra todos los mensajes de ERROR de forma predeterminada. Si desea que se muestren más mensajes de registro, configure un registrador con el nivel de registro adecuado.

Los mensajes de registro utilizan un anexador de registro en memoria y, por lo tanto, no están relacionados con los archivos de registro. Otra consecuencia es que al cambiar los niveles de registro en esta interfaz de usuario no se cambia la información que se registra en los archivos de registro tradicionales. Añadir y eliminar registradores en esta interfaz de usuario solo afecta al registrador de memoria. Además, el cambio de las configuraciones del registrador se refleja en el futuro del en el registrador de memoria. Las entradas que ya están registradas y ya no son relevantes no se eliminan, pero entradas similares no se registran en el futuro.

Puede configurar lo que se registra proporcionando configuraciones del registrador desde el botón del engranaje superior izquierdo de la interfaz de usuario. Aquí puede agregar, quitar o actualizar las configuraciones del registrador. Una configuración del registrador está compuesta por un **nivel de registro** (WARN / INFO / DEBUG) y un **nombre de filtro**. El **nombre de filtro** tiene la función de filtrar el origen de los mensajes de registro que se registran. Alternativamente, si un registrador debe capturar todos los mensajes de registro para el nivel especificado, el nombre del filtro debe ser &quot;**root**&quot;. Déclencheur Al establecer el nivel de un registrador, se capturan todos los mensajes con un nivel igual o superior al especificado.

Por ejemplo:

* Si planea capturar todos los mensajes de **ERROR**, no se requiere configuración. Todos los mensajes ERROR se capturan de forma predeterminada.
* Si planea capturar todos los mensajes de **ERROR**, **WARN** e **INFO**, el nombre del registrador debe establecerse en: &quot;**root**&quot; y el nivel del registrador en: **INFO**.

* Si planea capturar todos los mensajes procedentes de un paquete determinado (por ejemplo, com.adobe.granite), el nombre del registrador debe configurarse como: &quot;com.adobe.granite&quot;. Y el nivel del registrador establecido en: **DEBUG** (al hacerlo se capturan todos los mensajes de **ERROR**, **WARN**, **INFO** y **DEBUG**), como se muestra en la imagen siguiente.

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>No puede establecer un nombre de registrador para capturar solo los mensajes de ERROR a través de un filtro especificado. De forma predeterminada, se capturan todos los mensajes de ERROR.

>[!NOTE]
>
>La interfaz de usuario de mensajes de registro no refleja el registro de errores real. A menos que esté configurando otros tipos de mensajes de registro en la interfaz de usuario de, solo verá mensajes de ERROR. Para ver cómo mostrar mensajes de registro específicos, consulte las instrucciones anteriores.

>[!NOTE]
>
>La configuración de la página de diagnóstico no influye en lo que se registra en los archivos de registro y a la inversa. Por lo tanto, aunque el registro de errores puede capturar mensajes INFO, es posible que no los vea en la interfaz de usuario de mensajes de registro. Además, a través de la interfaz de usuario es posible capturar mensajes de DEPURACIÓN de ciertos paquetes sin que afecte al registro de errores. Para obtener más información sobre cómo configurar los archivos de registro, vea [Registro](/help/sites-deploying/configure-logging.md).

>[!NOTE]
>
>**Con AEM 6.4**, las tareas de mantenimiento se registran de forma predeterminada en un formato enriquecido más informativo a nivel INFO. Este flujo de trabajo ofrece una mejor visibilidad del estado de las tareas de mantenimiento.
>
>Si utiliza herramientas de terceros (como Splunk) para monitorizar y reaccionar ante la actividad de la tarea de mantenimiento, puede utilizar las siguientes instrucciones de registro:

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### Rendimiento de solicitudes {#request-performance}

La página Rendimiento de la Solicitud permite analizar las solicitudes de página más lentas procesadas. En esta página solo se registran solicitudes de contenido. Más específicamente, se capturan las siguientes solicitudes:

1. Solicitudes de acceso a recursos bajo `/content`
1. Solicitudes de acceso a recursos bajo `/etc/design`
1. Solicitudes que tienen la extensión `".html"`

![chlimage_1-122](assets/chlimage_1-122.png)

Se muestra la página:

* Hora a la que se realizó la solicitud
* La dirección URL y el método de solicitud
* La duración en milisegundos

De forma predeterminada, se capturan las 20 solicitudes de página más lentas, pero el límite se puede modificar en el Administrador de configuración.

### Rendimiento de consultas {#query-performance}

La página Rendimiento de la Consulta permite analizar las consultas más lentas realizadas por el sistema. El repositorio proporciona esta información en un Mbean JMX. En Jackrabbit, el MBean JMX `com.adobe.granite.QueryStat` proporciona esta información, mientras que en el repositorio de Oak, la ofrece `org.apache.jackrabbit.oak.QueryStats.`

Se muestra la página:

* Hora a la que se realizó la consulta
* El idioma de la consulta
* El número de veces que se emitió la consulta
* El enunciado de la consulta
* La duración en milisegundos

![chlimage_1-123](assets/chlimage_1-123.png)

### Explicar la consulta {#explain-query}

Para cualquier consulta determinada, Oak intenta averiguar la mejor manera de ejecutar en función de los índices de Oak definidos en el repositorio bajo el nodo **oak:index**. Oak puede elegir diferentes índices en función de la consulta. El primer paso para optimizar la consulta es comprender cómo ejecuta Oak una consulta.

Explicar consulta es una herramienta que explica cómo ejecuta Oak una consulta. Se puede acceder a él desde **Herramientas - Operaciones - Diagnóstico** desde la pantalla de bienvenida de AEM. A continuación, haga clic en **Rendimiento de la consulta** y cambie a la ficha **Explicar consulta**.

**Funciones**

* Admite los lenguajes de consulta Xpath, JCR-SQL y JCR-SQL2
* Notifica el tiempo de ejecución real de la consulta proporcionada
* Detecta consultas lentas y advierte sobre consultas que podrían ser potencialmente lentas
* Informa del índice de Oak utilizado para ejecutar la consulta
* Muestra la descripción real del motor de consultas de Oak
* Proporciona una lista de clics para cargar de consultas lentas y populares

Una vez que esté en la interfaz de usuario de Explicar consulta, ingrese la consulta y presione el botón **Explicar**:

![chlimage_1-124](assets/chlimage_1-124.png)

La primera entrada de la sección Explicación de la consulta es la explicación real. La explicación muestra el tipo de índice que se utilizó para ejecutar la consulta.

La segunda entrada es el plan de ejecución.

Al marcar la casilla **Incluir tiempo de ejecución** antes de ejecutar la consulta, también se muestra la cantidad de tiempo que se ejecutó la consulta. La opción **Incluir recuento de nodos** indica el recuento de nodos. El informe permite obtener más información que se puede utilizar para optimizar los índices de la aplicación o implementación.

![chlimage_1-125](assets/chlimage_1-125.png)

### El Administrador de índices {#the-index-manager}

El propósito del Administrador de índices es facilitar la administración de índices, como el mantenimiento de índices o la visualización de su estado.

Se puede acceder a él desde **Herramientas - Operaciones - Diagnóstico **desde la pantalla de bienvenida y, a continuación, haciendo clic en el botón **Administrador de índices**.

También se puede obtener acceso a él directamente desde esta dirección URL: `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![administrador_índice](assets/index_manager.png)

La interfaz de usuario se puede utilizar para filtrar índices en la tabla escribiendo los criterios de filtro en el cuadro de búsqueda en la esquina superior izquierda de la pantalla.

### Descargar zip de estado {#download-status-zip}

Esta acción almacena en déclencheur la descarga de un archivo zip que contiene información útil sobre el estado y la configuración del sistema. El archivo contiene configuraciones de instancia, una lista de paquetes, OSGI, métricas y estadísticas de Sling, que pueden dar como resultado un archivo grande. Puede reducir el impacto de los archivos de estado grandes mediante la ventana **Descargar ZIP de estado**. Se puede acceder a la ventana desde:**AEM > Herramientas > Operaciones > Diagnóstico > ZIP de estado de descarga.**

Desde esta ventana, puede seleccionar qué desea exportar (archivos de registro o volcados de procesos) y el número de días de registros incluidos en la descarga en relación con la fecha actual.

![download_status_zip](assets/download_status_zip.png)

### Descargar volcados de procesos {#download-thread-dump}

Esta acción almacena en déclencheur la descarga de un zip que contiene información sobre los hilos presentes en el sistema. Se proporciona información sobre cada subproceso, como su estado, el cargador de clases y el stacktrace.

### Descargar volcado de pila {#download-heap-dump}

Puede descargar una instantánea del montón para analizarla más adelante. Esta acción déclencheur la descarga de un archivo grande (de cientos de megabytes).

## Tareas de mantenimiento automatizadas {#automated-maintenance-tasks}

La página Tareas de mantenimiento automatizadas es un lugar en el que puede ver y realizar un seguimiento de las tareas de mantenimiento recomendadas programadas para su ejecución periódica. Las tareas están integradas con el sistema de comprobación de estado. Las tareas también se pueden ejecutar manualmente desde la interfaz.

Para llegar a la página de mantenimiento en el tablero de operaciones, en la pantalla de bienvenida de AEM, vaya a **Herramientas - Operaciones - Tablero - Mantenimiento** o siga directamente este vínculo:

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

Las siguientes tareas están disponibles en el tablero de operaciones:

1. La tarea **Limpieza de revisión**, ubicada en el menú **Ventana de mantenimiento diario**.
1. La tarea **Limpieza de binarios de Lucene**, ubicada en el menú **Ventana de mantenimiento diario**.
1. La tarea **Depurar flujo de trabajo**, ubicada en el menú **Ventana de mantenimiento semanal**.
1. La tarea **Recopilación de residuos del almacén de datos**, ubicada en el menú **Ventana de mantenimiento semanal**.
1. La tarea **Mantenimiento del registro de auditoría**, ubicada en el menú **Ventana de mantenimiento semanal**.
1. La tarea **Mantenimiento de purga de versiones**, ubicada en el menú **Ventana de mantenimiento semanal**.
1. La tarea de mantenimiento **Purga del proyecto**, ubicada en el menú **Ventana de mantenimiento semanal**; con la opción **Agregar**.
1. La tarea de mantenimiento **Purgar tareas ad hoc**, ubicada en el menú **Ventana de mantenimiento semanal**; con la opción **Agregar**.

El horario predeterminado para la ventana de mantenimiento diario es de 2:00 a.m. a 5:00 a.m. Las tareas configuradas para ejecutarse en la ventana de mantenimiento semanal se ejecutan entre la 1 y las 2 de la madrugada los sábados.

También puede configurar los horarios pulsando el icono de engranaje en cualquiera de las dos tarjetas de mantenimiento:

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>Desde AEM 6.1, los períodos de mantenimiento existentes también se pueden configurar para que se ejecuten mensualmente.

### Limpieza de revisión {#revision-clean-up}

Para obtener más información, consulte [Limpieza de revisión](/help/sites-deploying/revision-cleanup.md).

### Limpieza de archivos binarios de Lucene {#lucene-binaries-cleanup}

Mediante la tarea Limpieza de binarios de Lucene, puede depurar los binarios de Lucene y reducir el requisito de tamaño del almacén de datos en ejecución. La pérdida binaria de Lucene se reclama a diario en lugar de la dependencia anterior de una ejecución correcta de [recolección de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md).

Aunque la tarea de mantenimiento se desarrolló para reducir la basura de revisiones relacionada con Lucene, hay mejoras generales de eficiencia al ejecutar la tarea:

* La ejecución semanal de la tarea de recolección de elementos no utilizados del almacén de datos puede completarse más rápidamente.
* También puede mejorar ligeramente el rendimiento general de AEM.

Puede acceder a la tarea Limpieza de binarios de Lucene desde: **AEM > Herramientas > Operaciones > Mantenimiento > Ventana de mantenimiento diario > Limpieza de binarios de Lucene**.

### Recopilación de datos almacenados desechables {#data-store-garbage-collection}

Para obtener más información sobre la recolección de elementos no utilizados del almacén de datos, consulte la página de documentación de [Recopilación de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md).

### Depuración de flujo de trabajo {#workflow-purge}

Los flujos de trabajo también se pueden eliminar del Panel de mantenimiento. Para ejecutar la tarea Depuración del flujo de trabajo, haga lo siguiente:

1. Haga clic en la página **Ventana de mantenimiento semanal**.
1. En la página siguiente, haga clic en **Reproducir** en la tarjeta **Depuración del flujo de trabajo**.

>[!NOTE]
>
>Para obtener información más detallada sobre el mantenimiento del flujo de trabajo, consulte [Administración de instancias de flujo de trabajo](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances).

### Mantenimiento del registro de auditoría {#audit-log-maintenance}

Para el mantenimiento del registro de auditoría, consulte la [página de documentación independiente.](/help/sites-administering/operations-audit-log.md)

### Depuración de la versión {#version-purge}

Puede planificar la tarea de mantenimiento Depuración de versiones para que se eliminen automáticamente las versiones antiguas. Esta acción minimiza la necesidad de usar manualmente las [herramientas de depuración de versiones](/help/sites-deploying/version-purging.md). Puede programar y configurar la tarea Depuración de versiones si accede a **Herramientas > Operaciones > Mantenimiento > Ventana de mantenimiento semanal** y sigue estos pasos:

1. Haga clic en **Agregar**.
1. Elija **Depuración de versión** en el menú desplegable.

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. Para configurar la tarea Depuración de versiones, haga clic en el icono **engranajes** en la tarjeta de mantenimiento Depuración de versiones recién creada.

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**Con AEM 6.4**, puede detener la tarea de mantenimiento Depuración de versiones de la siguiente manera:

* Automáticamente: Si la ventana de mantenimiento programado se cierra antes de que la tarea pueda completarse, la tarea se detiene automáticamente. Se reanudará cuando se abra la siguiente ventana de mantenimiento.
* Manualmente: para detener manualmente la tarea, en la tarjeta de mantenimiento Depuración de versiones, haga clic en el icono **Detener**. En la siguiente ejecución, la tarea se reanudará de forma segura.

>[!NOTE]
>
>Detener la tarea de mantenimiento significa suspender su ejecución sin perder el seguimiento del trabajo ya en curso.

>[!CAUTION]
>
>Para optimizar el tamaño del repositorio, debe ejecutar la tarea de depuración de versiones con frecuencia. La tarea debe programarse fuera del horario laboral cuando haya una cantidad limitada de tráfico.

### Depuración del proyecto {#project-purge}

<!--
Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the folder `/apps/settings/granite/operations/maintenance/granite_weekly`, `granite_daily` or `granite_monthly`. See the Maintenance Window table below for additional configuration details.

Enable the maintenance task by adding another node under the node above (name it `granite_ProjectPurgeTask`) with the appropriate properties. 
-->

Configure las propiedades OSGI en **Configuración de purga de proyectos de Adobe** (com.adobe.cq.projects.purge.Scheduler).

### Depuración de tareas específicas {#purge-of-ad-hoc-tasks}

<!--
Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the folder `/apps/settings/granite/operations/maintenance/granite_weekly`, `granite_daily` or `granite_monthly`.

See the Maintenance Window table below for additional configuration details. Enable the maintenance task by adding another node under the node above. Name it `granite_TaskPurgeTask`, with attribute `sling:resourceType` set to `granite/operations/components/maintenance/task` and attribute `granite.maintenance.name` set to `TaskPurge`. 
-->

Configure las propiedades de OSGI en **Purga de tareas ad hoc** (`com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask`).

## Tareas de mantenimiento personalizadas {#custom-maintenance-tasks}

Las tareas de mantenimiento personalizadas se pueden implementar como servicios OSGi. Como la infraestructura de tareas de mantenimiento se basa en la administración de trabajos de Apache Sling, una tarea de mantenimiento debe implementar la interfaz Java™ ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`. Además, debe declarar varias propiedades de registro de servicio para que se detecten como una tarea de mantenimiento, como se muestra a continuación:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad de servicio</strong><br /> </td>
   <td><strong>Descripción</strong></td>
   <td><strong>Ejemplo</strong><br /> </td>
   <td><strong>Tipo</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>Atributo booleano que define si el usuario puede detener la tarea. Si una tarea declara que se puede detener, debe comprobar durante su ejecución si se ha detenido y, a continuación, actuar en consecuencia. El valor predeterminado es false.</td>
   <td>true</td>
   <td>Opcional</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>Atributo booleano que define si una tarea es obligatoria y debe ejecutarse periódicamente. Si una tarea es obligatoria pero actualmente no se encuentra en ninguna ventana de programación activa, una comprobación de estado informará de este error. El valor predeterminado es false.</td>
   <td>true</td>
   <td>Opcional</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>Un nombre único para la tarea: el nombre se utiliza para hacer referencia a la tarea y es solo un nombre simple.</td>
   <td>MyMaintenanceTask</td>
   <td>Requerido</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>Título mostrado para esta tarea</td>
   <td>Mi tarea de mantenimiento especial</td>
   <td>Requerido</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>Tema único de la tarea de mantenimiento.<br /> La administración de trabajos de Apache Sling inicia un trabajo con exactamente este tema para ejecutar la tarea de mantenimiento y, a medida que la tarea se registra para este tema, se ejecuta.<br />: el tema debe comenzar con <i>com/adobe/granite/maintenance/job/</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>Requerido</td>
  </tr>
 </tbody>
</table>

Aparte de las propiedades del servicio anteriores, el método `process()` de la interfaz `JobConsumer` debe implementarse agregando el código que debe ejecutarse para la tarea de mantenimiento. El(la) `JobExecutionContext` proporcionado(a) se puede usar para generar información de estado, comprobar si el usuario detuvo el trabajo y crear un resultado (correcto o fallido).

Para las situaciones en las que una tarea de mantenimiento no se debe ejecutar en todas las instalaciones (por ejemplo, ejecutar solo en la instancia de publicación), puede hacer que el servicio requiera que una configuración esté activa agregando `@Component(policy=ConfigurationPolicy.REQUIRE)`. A continuación, puede marcar la configuración correspondiente como dependiente del modo de ejecución en el repositorio. Para obtener más información, consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository).

A continuación se muestra un ejemplo de una tarea de mantenimiento personalizada que elimina archivos de un directorio temporal configurable que se han modificado en las últimas 24 horas:

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

Una vez implementado el servicio, se expone a la interfaz de usuario del tablero de operaciones. Puede añadirlo a uno de los programas de mantenimiento disponibles:

![chlimage_1-127](assets/chlimage_1-127.png)

Esta acción agrega el recurso correspondiente en /apps/granite/operations/config/maintenance/`schedule`/`taskname`. Si la tarea depende del modo de ejecución, la propiedad granite.operations.conditions.runmode debe configurarse en ese nodo con los valores de los modos de ejecución que deben estar activos para esta tarea de mantenimiento.

## Información general del sistema {#system-overview}

El **Panel de información general del sistema** muestra información general de alto nivel sobre la configuración, el hardware y el estado de la instancia de AEM. El estado del sistema es transparente y toda la información se agrega en un solo tablero.

>[!NOTE]
>
>También puedes [ver este vídeo](https://video.tv.adobe.com/v/21340) para ver una introducción al Panel de información general del sistema.

### Cómo Acceder A {#how-to-access}

Para acceder al Panel de información general del sistema, vaya a **Herramientas > Operaciones > Información general del sistema**.

![system_overview_dashboard](assets/system_overview_dashboard.png)

### Tablero de información general del sistema explicado {#system-overview-dashboard-explained}

En la tabla siguiente se describe toda la información mostrada en el tablero de información general del sistema. Cuando no hay información relevante que mostrar (por ejemplo, la copia de seguridad no está en curso, no hay comprobaciones de estado críticas), la sección correspondiente muestra el mensaje &quot;Sin entradas&quot;.

También puede descargar un archivo de `JSON` que resuma la información del panel haciendo clic en el botón **Descargar** en la esquina superior derecha del panel. El extremo `JSON` es `/libs/granite/operations/content/systemoverview/export.json` y se puede usar en un script `curl` para la supervisión externa.

<table>
 <tbody>
  <tr>
   <td><strong>Sección</strong></td>
   <td><strong>Qué información se muestra</strong></td>
   <td><strong>¿Cuándo es crítico?</strong></td>
   <td><strong>Vínculos a</strong></td>
  </tr>
  <tr>
   <td>Comprobación del estado</td>
   <td>
    <ul>
     <li>una lista de comprobaciones en estado crítico</li>
     <li>una lista de comprobaciones en estado de advertencia</li>
    </ul> </td>
   <td>Indicado visualmente:<br />
    <ul>
     <li>una etiqueta roja para las comprobaciones críticas</li>
     <li>una etiqueta naranja para las comprobaciones de advertencia</li>
    </ul> </td>
   <td>
    <ul>
     <li>Página Informes de estado</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tareas de mantenimiento</td>
   <td>
    <ul>
     <li>una lista de tareas que han fallado</li>
     <li>una lista de tareas que se están ejecutando actualmente</li>
     <li>una lista de tareas que se realizaron correctamente en la última ejecución</li>
     <li>una lista de tareas que nunca se han ejecutado</li>
     <li>una lista de tareas no programadas</li>
    </ul> </td>
   <td><p>Indicado visualmente:</p>
    <ul>
     <li>una etiqueta roja para las tareas fallidas</li>
     <li>una etiqueta naranja para ejecutar tareas (ya que podrían afectar al rendimiento).</li>
     <li>etiquetas grises cada dos estados</li>
    </ul> </td>
   <td>
    <ul>
     <li>Página Tareas de Mantenimiento</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Sistema</td>
   <td>
    <ul>
     <li>sistema operativo y versión del sistema operativo (por ejemplo, macOS X)</li>
     <li>promedio de carga del sistema, recuperado de <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeanusable</a></li>
     <li>espacio en disco (en la partición donde se encuentra el directorio particular)</li>
     <li>montón máximo, devuelto por <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a></li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Instancia</td>
   <td>
    <ul>
     <li>la versión de AEM</li>
     <li>lista de modos de ejecución</li>
     <li>la fecha en la que se inició la instancia</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Repositorio</td>
   <td>
    <ul>
     <li>la versión de Oak</li>
     <li>Tipo de almacén de nodos (Segment TAR o Document)
      <ul>
       <li>si el tipo es documento, se muestra el tipo de almacén de documentos (RDB o Mongo)</li>
      </ul> </li>
     <li>si hay un almacén de datos personalizado:
      <ul>
       <li>para un almacén de datos de archivos, se muestra la ruta</li>
       <li>para un almacén de datos S3, se muestra el nombre del contenedor S3</li>
       <li>para un almacén de datos compartidos de S3, se muestra el nombre del contenedor de S3</li>
       <li>para un almacén de datos de Azure, se muestra el contenedor</li>
      </ul> </li>
     <li>si no hay ningún almacén de datos externo personalizado, se muestra un mensaje que indica este hecho</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Agentes de distribución</td>
   <td>
    <ul>
     <li>una lista de agentes con colas bloqueadas</li>
     <li>una lista de agentes mal configurados ("Error de configuración")</li>
     <li>una lista de agentes con el procesamiento de cola en pausa</li>
     <li>una lista de agentes inactivos</li>
     <li>una lista de agentes en ejecución (que están procesando entradas actualmente)</li>
    </ul> </td>
   <td><p>Indicado visualmente:</p>
    <ul>
     <li>una etiqueta roja para agentes bloqueados o errores de configuración</li>
     <li>una etiqueta naranja para los agentes en pausa</li>
     <li>una etiqueta gris para los agentes en pausa, inactivos o en ejecución<br /> </li>
    </ul> </td>
   <td>Página de distribución <br /> </td>
  </tr>
  <tr>
   <td>Agentes de replicación</td>
   <td>
    <ul>
     <li>una lista de agentes con colas bloqueadas</li>
     <li>una lista de agentes inactivos</li>
     <li>una lista de agentes en ejecución (que están procesando entradas actualmente)</li>
    </ul> </td>
   <td><p>Indicado visualmente:<br /> </p>
    <ul>
     <li>una etiqueta roja para los agentes bloqueados</li>
     <li>una etiqueta gris para los agentes en pausa</li>
    </ul> </td>
   <td>Página Replicación</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td>
    <ul>
     <li>Trabajos de flujo:
      <ul>
       <li>número de trabajos de flujo de trabajo con errores (si los hay)</li>
       <li>número de trabajos de flujo de trabajo cancelados (si los hay)</li>
      </ul> </li>
    </ul>
    <ul>
     <li>Recuentos de flujos de trabajo: número de flujos de trabajo en un estado determinado (si los hay):
      <ul>
       <li>corriente</li>
       <li>error</li>
       <li>suspendido</li>
       <li>abortado</li>
      </ul> </li>
    </ul> <p>Para cada uno de los estados presentados arriba se realiza una consulta, con un límite de 400 milisegundos. A los 400 milisegundos, se muestra el número de entradas obtenidas hasta ese momento.</p> </td>
   <td><p>No interpretado:</p>
    <ul>
     <li>el usuario debe investigar cuando haya flujos de trabajo y trabajos en estados inesperados.</li>
    </ul> </td>
   <td>Página Errores de flujo de trabajo</td>
  </tr>
  <tr>
   <td>Trabajos de Sling</td>
   <td><p>Recuentos de trabajos de Sling: número de trabajos en un estado determinado (si los hay):</p>
    <ul>
     <li>error</li>
     <li>en cola</li>
     <li>cancelado</li>
     <li>activo</li>
    </ul> </td>
   <td><p>No interpretado:</p>
    <ul>
     <li>el usuario debe investigar cuando haya trabajos en estados inesperados o con recuentos altos.</li>
    </ul> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Número aproximado de nodos</td>
   <td><p>Número estimado de:</p>
    <ul>
     <li>páginas</li>
     <li>activos</li>
     <li>etiquetas</li>
     <li>autorizables</li>
     <li>número total de nodos <br /> </li>
    </ul> <p>El número total de nodos se obtiene de nodeCounterMBean, mientras que el resto de las estadísticas se obtienen de IndexInfoService.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Copia de seguridad</td>
   <td>Muestra "Copia de seguridad en línea en curso" si es así.</td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Indexación</td>
   <td><p>Muestra:</p>
    <ul>
     <li>"Indexación en curso"</li>
     <li>"Consulta en curso"</li>
    </ul> <p>Si hay un subproceso de indexación o consulta en el volcado de hilos.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>
