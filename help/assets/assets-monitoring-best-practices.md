---
title: Prácticas recomendadas para supervisar  [!DNL Assets] implementación
description: Prácticas recomendadas para supervisar el entorno y el rendimiento de su implementación de  [!DNL Adobe Experience Manager] después de implementarla.
contentOwner: AG
role: Admin, Architect
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 1%

---

# Prácticas recomendadas para supervisar la implementación de [!DNL Adobe Experience Manager Assets] {#assets-monitoring-best-practices}

Desde el punto de vista de [!DNL Experience Manager Assets], la monitorización debe incluir la observación y la creación de informes sobre los siguientes procesos y tecnologías:

* System CPU
* Uso de memoria del sistema
* Tiempo de espera de E/S del disco del sistema
* E/S de red del sistema
* MBean de JMX para el uso de la pila y los procesos asincrónicos, como flujos de trabajo
* Comprobaciones de estado de la consola OSGi

Normalmente, [!DNL Experience Manager Assets] se puede supervisar de dos formas: mediante supervisión en directo y mediante supervisión a largo plazo.

## Monitorización en directo {#live-monitoring}

Debe realizar la monitorización en directo durante la fase de prueba de rendimiento del desarrollo o durante situaciones de alta carga para comprender las características de rendimiento del entorno. Normalmente, la monitorización en directo debe realizarse con un conjunto de herramientas. Estas son algunas recomendaciones:

* [Visual VM](https://visualvm.github.io/): Visual VM le permite ver información detallada de Java VM, incluido el uso de CPU y el uso de memoria Java. Además, permite tomar muestras y evaluar el código que se ejecuta en una implementación.
* [Top](https://man7.org/linux/man-pages/man1/top.1.html): Top es un comando de Linux que abre un tablero, que muestra estadísticas de uso, incluyendo uso de CPU, memoria y E/S. Proporciona una descripción general de alto nivel de lo que está sucediendo en una instancia.
* [Htop](https://hisham.hm/htop/): Htop es un visor interactivo de procesos. Proporciona un uso detallado de la memoria y la CPU, además de lo que Top puede proporcionar. Htop se puede instalar en la mayoría de los sistemas Linux usando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop es un tablero detallado para el uso de E/S de disco. Muestra las barras y los medidores que muestran los procesos que utilizan E/S de disco y la cantidad que utilizan. Iotop se puede instalar en la mayoría de los sistemas Linux usando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop muestra información detallada sobre el uso de red/ethernet. Iftop muestra estadísticas por canal de comunicación sobre las entidades que utilizan Ethernet y la cantidad de ancho de banda que utilizan. Iftop se puede instalar en la mayoría de los sistemas Linux usando `yum install iftop` o `apt-get install iftop`.

* Java Flight Recorder (JFR): Una herramienta comercial de Oracle que puede utilizar libremente en entornos que no sean de producción. Para obtener más información, consulte [Cómo usar el registrador de vuelos Java para diagnosticar problemas de tiempo de ejecución de CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` archivo: puede investigar el archivo [!DNL Experience Manager] `error.log` para obtener detalles de los errores registrados en el sistema. Utilice el comando `tail -F quickstart/logs/error.log` para identificar los errores que se van a investigar.
* [Consola de flujo de trabajo](/help/sites-administering/workflows.md): aproveche la consola de flujo de trabajo para monitorizar los flujos de trabajo que se retrasan o se quedan atascados.

Normalmente, estas herramientas se utilizan juntas para obtener una idea completa del rendimiento de la implementación de [!DNL Experience Manager].

>[!NOTE]
>
>Estas herramientas son herramientas estándar y Adobe no las admite directamente. No requieren licencias adicionales.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Supervisión en vivo mediante la herramienta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitorización a largo plazo {#long-term-monitoring}

La supervisión a largo plazo de una implementación de [!DNL Experience Manager] implica la supervisión de las mismas partes que se supervisan en tiempo real durante un período más largo. También incluye la definición de alertas específicas para su entorno.

### Agregación de registros e informes {#log-aggregation-and-reporting}

Hay varias herramientas disponibles para agregar registros, por ejemplo, Splunk(TM) y Elastic Search, Logstash y Kabana (ELK). Para evaluar el tiempo de actividad de su implementación de [!DNL Experience Manager], es importante que entienda los eventos de registro específicos de su sistema y cree alertas basadas en ellos. Un buen conocimiento de las prácticas de desarrollo y operaciones puede ayudarle a comprender mejor cómo ajustar el proceso de agregación de registros para generar alertas críticas.

### Monitorización del entorno {#environment-monitoring}

La monitorización del entorno incluye monitorizar lo siguiente:

* Rendimiento de red
* E/S de disco
* Memoria
* Utilización de CPU
* MBeans de JMX
* Sitios web externos

Necesita herramientas externas, como NewRelic(TM) y AppDynamics(TM) para supervisar cada elemento. Con estas herramientas, puede definir alertas específicas del sistema, por ejemplo, alta utilización del sistema, copia de seguridad del flujo de trabajo, errores de comprobación de estado o acceso no autenticado al sitio web. Adobe no recomienda ninguna herramienta en particular sobre otras. Busque la herramienta que mejor se adapte a sus necesidades y utilícela para supervisar los elementos analizados.

#### Monitorización de aplicaciones internas {#internal-application-monitoring}

La supervisión de aplicaciones internas incluye la supervisión de los componentes de la aplicación que conforman la pila [!DNL Experience Manager], incluida JVM, el repositorio de contenido, y la supervisión mediante código de aplicación personalizado creado en la plataforma. En general, se realiza a través de Mbeans JMX que pueden ser monitoreados directamente por muchas soluciones de monitoreo populares, como SolarWinds (TM), HP OpenView (TM), Hyperic (TM), Zabbix (TM) y otras. En el caso de los sistemas que no admiten una conexión directa a JMX, puede escribir scripts de shell para extraer los datos JMX y exponerlos a estos sistemas en un formato que comprendan de forma nativa.

El acceso remoto a los Mbeans de JMX no está habilitado de forma predeterminada. Para obtener más información sobre la supervisión mediante JMX, consulte [Supervisión y administración con tecnología JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

En muchos casos, se requiere una línea de base para monitorizar una estadística de forma eficaz. Para crear una línea de base, observe el sistema en condiciones normales de trabajo durante un período predeterminado y luego identifique la métrica normal.

**Supervisión de JVM**

Al igual que con cualquier pila de aplicaciones basadas en Java, [!DNL Experience Manager] depende de los recursos que se le proporcionan a través de la máquina virtual Java subyacente. Puede monitorizar el estado de muchos de estos recursos a través de Platform MXeans que expone JVM. Para obtener más información sobre MXBeans, vea [Usar el servidor MBean de Platform y Platform MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Estos son algunos parámetros de línea de base que puede monitorizar para JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instancias: todos los servidores
* Umbral de alarma: cuando la utilización de la memoria (pila o no pila) supera el 75% de la memoria máxima correspondiente.
* Definición de alarma: la memoria del sistema es insuficiente o hay una fuga de memoria en el código. Analice un volcado de hilos para llegar a una definición.

>[!NOTE]
>
>La información proporcionada por este bean se expresa en bytes.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instancias: todos los servidores
* Umbral de alarma: cuando el número de hilos es mayor que el 150% de la línea de base.
* Definición de alarma: o bien hay un proceso de fuga activo, o una operación ineficiente consume una gran cantidad de recursos. Analice un volcado de hilos para llegar a una definición.

**Supervisar[!DNL Experience Manager]**

[!DNL Experience Manager] también expone un conjunto de estadísticas y operaciones a través de JMX. Esto puede ayudar a evaluar el estado del sistema e identificar posibles problemas antes de que afecten a los usuarios. Para obtener más información, consulte [documentación](/help/sites-administering/jmx-console.md) en [!DNL Experience Manager] MBeans de JMX.

Estos son algunos parámetros de línea de base que puede supervisar para [!DNL Experience Manager]:

Agentes de replicación

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Instancias: un autor y todas las instancias de publicación (para los agentes de vaciado)
* Umbral de alarma: cuando el valor de `QueueBlocked` es `true` o el valor de `QueueNumEntries` es mayor que el 150 % de la línea de base.

* Definición de alarma: presencia de una cola bloqueada en el sistema que indica que el destino de replicación está inactivo o no se puede acceder a él. A menudo, los problemas de red o infraestructura hacen que se pongan en cola entradas excesivas, lo que puede afectar negativamente al rendimiento del sistema.

>[!NOTE]
>
>Para los parámetros MBean y URL, reemplace `<AGENT_NAME>` por el nombre del agente de replicación que desea supervisar.

Contador de sesión

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Estadísticas de OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Instancias: todos los servidores
* Umbral de alarma: cuando las sesiones abiertas superan la línea de base en más del 50%.
* Definición de alarma: las sesiones pueden abrirse a través de un fragmento de código y nunca cerrarse. Esto puede ocurrir lentamente con el tiempo y, finalmente, causar fugas de memoria en el sistema. Aunque el número de sesiones debería fluctuar en un sistema, no deberían aumentar continuamente.

Comprobación del estado

Las comprobaciones de estado disponibles en el [tablero de operaciones](/help/sites-administering/operations-dashboard.md#health-reports) tienen los MBeans de JMX correspondientes para la supervisión. Sin embargo, puede escribir comprobaciones de estado personalizadas para exponer estadísticas de sistema adicionales.

Estas son algunas comprobaciones de estado listas para usar que son útiles para monitorizar:

* Comprobaciones del sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o CRÍTICA. Compruebe el atributo de registro para obtener más información sobre la causa del problema.

* Cola de replicación

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o CRÍTICA. Compruebe el atributo de registro para obtener más información sobre la cola que provocó el problema.

* Rendimiento de la respuesta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instancias: todos los servidores
   * Duración de la alarma: cuando el estado no es OK
   * Definición de alarma: el estado de una de las métricas es ADVERTENCIA o ESTADO CRÍTICO. Compruebe el atributo de registro para obtener más información sobre la cola que provocó el problema.

* Rendimiento de consultas

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Instancias: un autor, todos los servidores de publicación
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: una o más consultas que se ejecutan lentamente en el sistema. Consulte el atributo de registro para obtener más información sobre las consultas que causaron el problema.

* Paquetes activos

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Instancias: todos los servidores
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: presencia de paquetes OSGi inactivos o sin resolver en el sistema. Consulte el atributo de registro para obtener más información sobre los paquetes que causaron el problema.

* Errores de registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instancias: todos los servidores
   * Umbral de alarma: cuando el estado no es OK
   * Definición de alarma: hay errores en los archivos de registro. Compruebe el atributo de registro para obtener más información sobre la causa del problema.

## Problemas y resoluciones comunes  {#common-issues-and-resolutions}

En el proceso de supervisión, si encuentra problemas, aquí tiene algunas tareas de solución de problemas que puede realizar para resolver problemas comunes con implementaciones de [!DNL Experience Manager]:

* Si usa TarMK, ejecute la compactación de Tar con frecuencia. Para obtener más información, consulte [Mantener el repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Comprobar `OutOfMemoryError` registros. Para obtener más información, consulte [Analizar problemas de memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* Consulte en los registros cualquier referencia a consultas sin indexar, recorridos de árbol o recorridos de índice. Indican consultas no indexadas o consultas indexadas inadecuadamente. Para obtener prácticas recomendadas sobre cómo optimizar el rendimiento de consultas e indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilice la consola de flujo de trabajo para comprobar que los flujos de trabajo funcionan según lo esperado. Si es posible, condense varios flujos de trabajo en uno solo.
* Vuelva a realizar la monitorización en directo y busque cuellos de botella adicionales o grandes consumidores de cualquier recurso específico.
* Investigue los puntos de salida de la red del cliente y los puntos de entrada a la red de implementación [!DNL Experience Manager], incluido el despachante. Con frecuencia, estas son áreas de cuello de botella. Para obtener más información, consulte [Consideraciones sobre la red de Assets](/help/assets/assets-network-considerations.md).
* Aumente el tamaño del servidor [!DNL Experience Manager]. Es posible que tenga un tamaño inadecuado de su implementación de [!DNL Experience Manager]. La Asistencia al cliente de Adobe puede ayudarle a identificar si el tamaño del servidor es inferior al esperado.
* Examine los archivos `access.log` y `error.log` para ver si hay entradas en el momento en que se produjo algún problema. Busque motivos que puedan indicar anomalías de código personalizado. Añádalos a la lista de eventos que supervisa.
