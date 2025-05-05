---
title: Descargando trabajos
description: Obtenga información sobre cómo configurar y utilizar instancias de AEM en una topología para realizar tipos específicos de procesamiento.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c0b285b7-3b20-4412-88b8-04de4a703f42
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 1%

---

# Descargando trabajos{#offloading-jobs}

## Introducción {#introduction}

La descarga distribuye las tareas de procesamiento entre las instancias de Experience Manager en una topología. Con la descarga, puede utilizar instancias de Experience Manager específicas para realizar tipos específicos de procesamiento. El procesamiento especializado le permite maximizar el uso de los recursos de servidor disponibles.

La descarga se basa en las características de [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) y Sling JobManager. Para utilizar la descarga, agregue clústeres de Experience Manager a una topología e identifique los temas de trabajo que procesa el clúster. Los clústeres están formados por una o más instancias de Experience Manager, por lo que una sola instancia se considera un clúster.

Para obtener información acerca de cómo agregar instancias a una topología, vea [Administrar topologías](/help/sites-deploying/offloading.md#administering-topologies).

### Distribución de trabajos {#job-distribution}

Sling JobManager y JobConsumer permiten la creación de trabajos que se procesan en una topología:

* JobManager: servicio que crea trabajos para temas específicos.
* JobConsumer: servicio que ejecuta trabajos de uno o más temas. Se pueden registrar varios servicios JobConsumer para el mismo tema.

Cuando JobManager crea un trabajo, el marco de trabajo de descarga selecciona un clúster de Experience Manager en la topología para ejecutar el trabajo:

* El clúster debe incluir una o más instancias que ejecuten un JobConsumer registrado para el tema del trabajo.
* El tema debe estar habilitado al menos para una instancia del clúster.

Consulte [Configuración del consumo de temas](/help/sites-deploying/offloading.md#configuring-topic-consumption) para obtener información sobre cómo refinar la distribución de trabajos.

![chlimage_1-109](assets/chlimage_1-109.png)

Cuando el marco de trabajo de descarga selecciona un clúster para ejecutar un trabajo y el clúster consta de varias instancias, Sling Distribution determina qué instancia del clúster ejecuta el trabajo.

### Cargas del trabajo {#job-payloads}

El marco de trabajo de descarga admite cargas útiles de trabajos que asocian trabajos con recursos del repositorio. Las cargas de trabajo son útiles cuando se crean trabajos para procesar recursos y el trabajo se descarga en otro equipo.

Al crear un trabajo, solo se garantiza que la carga útil se encuentre en la instancia que crea el trabajo. Al descargar el trabajo, los agentes de replicación se aseguran de que la carga útil se cree en la instancia que finalmente consume el trabajo. Cuando se completa la ejecución del trabajo, la replicación inversa hace que la carga útil se copie de nuevo en la instancia que creó el trabajo.

## Administración de topologías {#administering-topologies}

Las topologías son clústeres de Experience Manager de correspondencia imprecisa que participan en la descarga. Un clúster consta de una o más instancias de servidor de Experience Manager (una sola instancia se considera un clúster).

Cada instancia de Experience Manager ejecuta los siguientes servicios relacionados con la descarga:

* Servicio de detección: envía solicitudes a un conector de topología para unirse a la topología.
* Conector de topología: recibe las solicitudes de unión y acepta o rechaza cada solicitud.

El servicio de detección de todos los miembros de la topología señala al conector de topología de uno de los miembros. En las secciones siguientes, este miembro se denomina miembro raíz.

![chlimage_1-110](assets/chlimage_1-110.png)

Cada clúster de la topología contiene una instancia que se reconoce como principal. El líder del clúster interactúa con la topología en nombre de los demás miembros del clúster. Cuando la directriz abandona el grupo, se elige automáticamente una nueva directriz para el grupo.

### Visualización de la topología {#viewing-the-topology}

Utilice el Explorador de topologías para explorar el estado de la topología en la que participa la instancia de Experience Manager. El Explorador de topología muestra los clústeres y las instancias de la topología.

Para cada clúster, verá una lista de miembros del clúster que indica el orden en que cada miembro se unió al clúster y qué miembro es el líder. La propiedad Current indica la instancia que está administrando actualmente.

Para cada instancia del clúster, puede ver varias propiedades relacionadas con la topología:

* Una lista de permitidos de temas para el consumidor de trabajos de la instancia.
* Los extremos que se exponen para conectarse con la topología.
* Temas de trabajo para los que se ha registrado la instancia para la descarga.
* Los temas de trabajo que procesa la instancia.

1. Con la IU táctil, haga clic en la pestaña Herramientas. ([http://localhost:4502/aem/start.html](http://localhost:4502/aem/start.html))
1. Para ver la descarga, haga clic en Mosaico de descarga en la sección Implementación.
1. Para ver la topología, haga clic en el mosaico Topología en la sección Implementación.

   Aparecen los clústeres que participan en la topología.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Haga clic en un cluster para ver una lista de las instancias del cluster y su ID, Estado actual y Estado de líder.
1. Haga clic en un ID de instancia para ver propiedades más detalladas.

También puede utilizar la consola web para ver información de topología. La consola proporciona más información sobre los clústeres de topología:

* ¿Qué instancia es la instancia local?
* Los servicios del Conector de topología que utiliza esta instancia para conectarse a la topología (saliente) y los servicios que se conectan a esta instancia (entrante).
* Cambiar el historial de las propiedades de topología e instancia.

Utilice el siguiente procedimiento para abrir la página Topology Management de la consola web:

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Sling > Administración de topología.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configuración de miembros de topología {#configuring-topology-membership}

El servicio de detección basado en recursos de Apache Sling se ejecuta en cada instancia para controlar cómo interactúan las instancias de Experience Manager con una topología.

El servicio de detección envía solicitudes POST periódicas (latidos) a los servicios del conector de topología para establecer y mantener conexiones con la topología. El servicio Conector de topología mantiene una lista de permitidos de direcciones IP o nombres de host que pueden unirse a la topología:

* Para unir una instancia a una topología, especifique la dirección URL del servicio Conector de topología del miembro raíz.
* Para permitir que una instancia se una a una topología, agregue la instancia a la lista de permitidos del servicio Conector de topología del miembro raíz.

Utilice la consola web o un nodo sling:OsgiConfig para configurar las siguientes propiedades del servicio org.apache.sling.discovery.impt.Config:

<table>
 <tbody>
  <tr>
   <th>Nombre de la propiedad</th>
   <th>Nombre de OSGi</th>
   <th>Descripción</th>
   <th>Valor predeterminado</th>
  </tr>
  <tr>
   <td>Tiempo de espera de Heartbeat (segundos)</td>
   <td>heartbeatTimeout</td>
   <td>Cantidad de tiempo en segundos que se debe esperar una respuesta de latido antes de que la instancia de destino se considere no disponible. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Intervalo de Heartbeat (segundos)</td>
   <td>heartbeatInterval</td>
   <td>Cantidad de tiempo en segundos entre latidos.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Retraso mínimo del evento (segundos)</td>
   <td>minEventDelay</td>
   <td><p>Cuando se produce un cambio en la topología, la cantidad de tiempo para retrasar el cambio de estado de TOPOLOGY_CHANGING a TOPOLOGY_CHANGED. Cada cambio que se produce cuando el estado es TOPOLOGY_CHANGING aumenta el retraso en esta cantidad de tiempo.</p> <p>Este retraso evita que los oyentes se inunden de eventos. </p> <p>Para no utilizar retardo, especifique 0 o un número negativo.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>URL del conector de topología</td>
   <td>topologyConnectorUrls</td>
   <td>Las direcciones URL de los servicios de Topology Connector para enviar mensajes de Heartbeat.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Lista de permitidos del conector de topología</td>
   <td>topologyConnectorWhitelist</td>
   <td>La lista de direcciones IP o nombres de host que el servicio local Topology Connector permite en la topología. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nombre del descriptor del repositorio</td>
   <td>leaderSelectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;sin valor&gt;</td>
  </tr>
 </tbody>
</table>

Utilice el siguiente procedimiento para conectar una instancia de CQ al miembro raíz de una topología. El procedimiento dirige la instancia a la dirección URL del conector de topología del miembro de topología raíz. Realice este procedimiento en todos los miembros de la topología.

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Principal > Administración de topología.
1. Haga clic en Configurar servicio de detección.
1. Agregue un elemento a la propiedad URL del conector de topología y especifique la dirección URL del servicio Conector de topología del miembro de la topología raíz. La dirección URL tiene el formato https://rootservername:4502/libs/sling/topology/connector.

Realice el siguiente procedimiento en el miembro raíz de la topología. El procedimiento agrega los nombres de los demás miembros de la topología a su lista de permitidos de Discovery Service.

1. Abra la consola web en el explorador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Haga clic en Principal > Administración de topología.
1. Haga clic en Configurar servicio de detección.
1. Para cada miembro de la topología, agregue un elemento a la propiedad de lista de permitidos Conector de topología y especifique el nombre de host o la dirección IP del miembro de la topología.

## Configuración del consumo de temas {#configuring-topic-consumption}

Utilice el Explorador de descarga para configurar el consumo de temas para las instancias de Experience Manager en la topología. Para cada instancia, puede especificar los temas que consume. Por ejemplo, para configurar la topología de modo que solo una instancia consuma temas de un tipo específico, deshabilite el tema en todas las instancias excepto en una.

Los trabajos se distribuyen entre instancias que tienen el tema asociado habilitado mediante la lógica de operación por turnos.

1. Con la IU táctil, haga clic en la pestaña Herramientas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. En el área Operaciones de Granite, haga clic en Explorador de descarga.
1. En el panel de navegación, haga clic en Explorador de descarga.

   Aparecen los temas de descarga y las instancias de servidor que pueden consumirlos.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Para desactivar el consumo de un tema para una instancia, debajo del nombre del tema, haga clic en Desactivar junto a la instancia.
1. Para configurar todo el consumo de temas de una instancia, haga clic en el identificador de instancia debajo de cualquier tema.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Haga clic en uno de los siguientes botones junto a un tema para configurar el comportamiento de consumo de la instancia y, a continuación, haga clic en Guardar:

   * Habilitada: esta instancia consume trabajos de este tema.
   * Deshabilitado: esta instancia no consume trabajos de este tema.
   * Exclusiva: esta instancia consume trabajos solo de este tema.

   **Nota:** Al seleccionar Exclusivo para un tema, todos los demás temas se establecen automáticamente como Deshabilitado.

### Consumidores de trabajos instalados {#installed-job-consumers}

Con Experience Manager se instalan varias implementaciones de JobConsumer. Los temas para los que se han registrado estos JobConsumers aparecen en el Explorador de descargas. Los temas adicionales que aparecen son los que JobConsumers personalizados han registrado. En la tabla siguiente se describen los JobConsumers predeterminados.

| Tema de trabajo | PID de servicio | Descripción |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Se instala con Apache Sling. Procesa los trabajos que genera el administrador de eventos OSGi para garantizar la compatibilidad con versiones anteriores. |
| com/day/cq/replication/job/&ast; | com.day.cq.replication.impl.AgentManagerImpl | Agente de replicación que replica cargas útiles de trabajo. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### Desactivación y activación de temas para una instancia {#disabling-and-enabling-topics-for-an-instance}

El servicio Administrador del consumidor de trabajos de Apache Sling proporciona propiedades de lista de permitidos y lista de bloqueados de temas. Configure estas propiedades para habilitar o deshabilitar el procesamiento de temas específicos en una instancia de Experience Manager.

**Nota:** Si la instancia pertenece a una topología, también puede usar el Explorador de descarga en cualquier equipo de la topología para habilitar o deshabilitar temas.

La lógica que crea la lista de temas habilitados permite primero todos los temas que están en la lista de permitidos y, a continuación, quita los temas que están en la lista de bloqueados. De forma predeterminada, todos los temas están habilitados (el valor de lista de permitidos es `*`) y no se deshabilitaron (la lista de bloqueados no tiene valor).

Utilice la consola web o un nodo `sling:OsgiConfig` para configurar las siguientes propiedades. Para nodos de `sling:OsgiConfig`, el PID del servicio Administrador de consumidores de trabajos es org.apache.sling.event.impl.jobs.JobConsumerManager.

| Nombre de propiedad en la consola web | ID de OSGi | Descripción |
|---|---|---|
| Lista de permitidos del tema | job.consumermanager.whitelist | Lista de temas que procesa el servicio JobManager local. El valor predeterminado de &ast; hace que todos los temas se envíen al servicio TopicConsumer registrado. |
| Lista de bloqueados del tema | job.consumermanager.blacklist | Lista de temas que el servicio JobManager local no procesa. |

## Creación De Agentes De Replicación Para Descargar {#creating-replication-agents-for-offloading}

El marco de trabajo de descarga utiliza la replicación para transportar recursos entre el autor y el trabajador. El marco de trabajo de descarga crea automáticamente agentes de replicación cuando las instancias se unen a la topología. Los agentes se crean con valores predeterminados. Cambiar manualmente la contraseña que utilizan los agentes para la autenticación.

>[!CAUTION]
>
>Un problema conocido con los agentes de replicación generados automáticamente requiere que cree manualmente nuevos agentes de replicación.

Cree los agentes de replicación que transportan las cargas útiles de trabajo entre instancias para la descarga. La siguiente ilustración muestra los agentes que es necesario descargar del autor a una instancia de trabajo. El autor tiene un Sling ID de 1 y la instancia de trabajo tiene un Sling ID de 2:

![chlimage_1-115](assets/chlimage_1-115.png)

Esta configuración requiere los tres agentes siguientes:

1. Un agente saliente en la instancia de autor que replica en la instancia de trabajador.
1. Un agente inverso en la instancia de autor que extrae de la bandeja de salida en la instancia de trabajador.
1. Un agente de bandeja de salida en la instancia de trabajador.

Este esquema de replicación es similar al utilizado entre las instancias de autor y publicación. Sin embargo, para la situación de descarga, todas las instancias implicadas son instancias de creación.

>[!NOTE]
>
>El marco de trabajo de descarga utiliza la topología para obtener las direcciones IP de las instancias de descarga. A continuación, el marco de trabajo crea automáticamente los agentes de replicación en función de estas direcciones IP. Si las direcciones IP de las instancias de descarga cambian posteriormente, el cambio se propaga automáticamente en la topología después de que se reinicie la instancia. Sin embargo, el marco de trabajo de descarga no actualiza automáticamente los agentes de replicación para reflejar las nuevas direcciones IP. Para evitar esta situación, utilice direcciones IP fijas para todas las instancias de la topología.

### Nombrar los agentes de replicación para la descarga {#naming-the-replication-agents-for-offloading}

Use un formato específico para la propiedad ***Name*** de los agentes de replicación para que el marco de trabajo de descarga utilice automáticamente el agente correcto para instancias de trabajo específicas.

**Nombrar al agente saliente en la instancia de autor:**

`offloading_<slingid>`, donde `<slingid>` es el ID de Sling de la instancia de trabajo.

Ejemplo: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Nombrar el agente inverso en la instancia de autor:**

`offloading_reverse_<slingid>`, donde `<slingid>` es el ID de Sling de la instancia de trabajo.

Ejemplo: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Nombrar la bandeja de salida en la instancia de trabajador:**

`offloading_outbox`

### Creación del agente saliente {#creating-the-outgoing-agent}

1. Crear un **agente de replicación** en el autor. (Consulte la [documentación de los agentes de replicación](/help/sites-deploying/replication.md)). Especifique cualquier **Título**. **Name** debe seguir la convención de nomenclatura.
1. Cree el agente con las siguientes propiedades:

   | Propiedad | Valor |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte > Usuario de transporte | Replicación del usuario en la instancia de destino |
   | Transporte > Contraseña de transporte | Contraseña de usuario de replicación en la instancia de destino |
   | Extendido > Método HTTP | PUBLICAR |
   | Déclencheur > Ignorar predeterminado | Verdadero |

### Creación del agente inverso {#creating-the-reverse-agent}

1. Crear un **agente de replicación inversa** en autor. (Consulte la [documentación de los agentes de replicación](/help/sites-deploying/replication.md).) Especifique cualquier **Título**. **Name** debe seguir la convención de nomenclatura.
1. Cree el agente con las siguientes propiedades:

   | Propiedad | Valor |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte > Usuario de transporte | Replicación del usuario en la instancia de destino |
   | Transporte > Contraseña de transporte | Contraseña de usuario de replicación en la instancia de destino |
   | Extendido > Método HTTP | GET |

### Creación del agente de bandeja de salida {#creating-the-outbox-agent}

1. Crear un **agente de replicación** en la instancia de trabajo. (Consulte la [documentación de los agentes de replicación](/help/sites-deploying/replication.md).) Especifique cualquier **Título**. **Name** debe ser `offloading_outbox`.
1. Cree el agente con las siguientes propiedades.

   | Propiedad | Valor |
   |---|---|
   | Configuración > Tipo de serialización | Predeterminado |
   | Transporte > URI de transporte | repo://var/replication/outbox |
   | Déclencheur > Ignorar predeterminado | Verdadero |

### Búsqueda del ID de Sling {#finding-the-sling-id}

Obtenga el ID de Sling de una instancia de Experience Manager mediante cualquiera de los siguientes métodos:

* Abra la consola web y, en la configuración de Sling, busque el valor de la propiedad Sling ID ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Este método es útil si la instancia aún no forma parte de la topología.
* Utilice el Explorador de topología si la instancia ya forma parte de la topología.

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## Lectura adicional {#further-reading}

Además de los detalles presentados en esta página, también puede leer lo siguiente:

* Para obtener información sobre el uso de las API de Java para crear trabajos y consumidores de trabajos, consulte [Creación y consumo de trabajos para descargar](/help/sites-developing/dev-offloading.md).
