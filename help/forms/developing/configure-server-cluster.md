---
title: Configuración y solución de problemas de AEM Forms en un clúster de servidores JEE
description: Obtenga información sobre cómo configurar y solucionar problemas de Adobe Experience Manager (AEM) Forms en un clúster de servidores JEE.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3943'
ht-degree: 0%

---

# Configurar y solucionar problemas de AEM Forms en un clúster de servidores JEE {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## Conocimientos previos requeridos {#prerequisites}

Familiaridad con Adobe Experience Manager (AEM) Forms en servidores de aplicaciones JEE, JBoss®, WebSphere® y WebLogic, servidores de bases de datos Red Hat® Linux®, SUSE® Linux®, Microsoft® Windows, IBM® AIX® o Sun Solaris™, servidores de bases de datos Oracle, IBM® DB2® o SQL Server y entornos web.

## Nivel de usuario {#user-level}

Avanzado 

Un clúster de AEM Forms en JEE es una topología diseñada para permitir que AEM Forms en JEE sea resistente al error de un clúster. También permite a la topología escalar la capacidad del sistema más allá de las capacidades de un solo nodo. Un clúster combina varios nodos en un único sistema lógico que comparte datos y permite que las transacciones abarquen varios nodos en su ejecución. Un clúster es la forma más general de escalar AEM Forms en JEE, ya que se puede admitir cualquier combinación de servicios que administren cualquier combinación de cargas de trabajo. Un clúster de AEM Forms en JEE no es necesariamente la mejor opción para todos los tipos de implementaciones y, una arquitectura de equilibrio de carga de servidor no agrupada puede ser apropiada.

Este documento analiza los requisitos de configuración específicos y las posibles áreas problemáticas que puede encontrar con un AEM Forms en un clúster JEE.

## ¿Qué hay en un clúster? {#what-is-in-cluster}

Los nodos del clúster de AEM Forms en JEE se comunican entre sí y comparten información para permitir que el clúster en su conjunto tenga una configuración y un estado de aplicación únicos y coherentes. El uso compartido de información dentro del clúster se realiza de varias formas diferentes y simultáneamente que se utilizan en diferentes contextos. En la figura siguiente se ilustran los métodos básicos de intercambio de información:

![Clúster de Application Server](assets/application-server-cluster.jpg)

### Clúster del servidor de aplicaciones {#application-server-cluster}

Un clúster de AEM Forms en JEE se basa en las capacidades de agrupación en clúster del servidor de aplicaciones subyacente. Los clústeres de servidores de aplicaciones permiten que la configuración del clúster se administre en su conjunto y proporcionan servicios de clúster de bajo nivel, como Java™ Naming and Directory Interface (JNDI), que permiten que los componentes de software se encuentren entre sí en el clúster. La sofisticación de los servicios de clúster y las dependencias técnicas subyacentes que tiene el servidor de aplicaciones dependen del servidor de aplicaciones. WebSphere® y WebLogic tienen funcionalidades de administración sofisticadas para clústeres, mientras que JBoss® tiene un enfoque básico.

### Caché de GemFire {#gemfire-cache}

La caché de GemFire es un mecanismo de caché distribuida implementado en cada nodo de clúster. Los nodos se encuentran entre sí y crean una única caché lógica que se mantiene coherente entre los nodos. Los nodos que se encuentran entre sí se unen para mantener una sola caché nocional que se muestra como una nube en la Figura 1. A diferencia del GDS y la base de datos, la caché es una entidad puramente conceptual. El contenido en caché real se almacena en la memoria y en el directorio `LC_TEMP` de cada uno de los nodos del clúster.

### Base de datos {#database}

Todos los nodos del clúster comparten la base de datos AEM Forms en JEE, a la que se accede mediante las fuentes de datos JDBC IDP_DS, EDC_DS y otras. La mayoría de los datos persistentes sobre el estado de AEM Forms en JEE, como qué transacciones están en curso, los datos de usuario asociados con transacciones en curso y los datos sobre cómo se ha configurado el sistema, se encuentran en esta base de datos.

### Almacenamiento global de documentos {#global-document-storage}

El almacenamiento global de documentos (GDS) es un área de almacenamiento basada en el sistema de archivos que utiliza Document Manager (clase IDPDocument) en AEM Forms en JEE. El GDS almacena archivos de corta y larga duración a los que todos los nodos del clúster deben tener acceso.

### Otros elementos {#other-items}

Además de estos recursos compartidos principales, hay otros elementos que tienen un comportamiento de clúster específico, como Cuarzo. Quartz es un subsistema de planificador utilizado por AEM Forms en JEE, y utiliza tablas de base de datos para mantener su conocimiento de lo que se ha programado y qué actividades programadas se están ejecutando. El cuarzo debe configurarse de forma diferente para instalaciones y clústeres de nodo único, y sigue el ejemplo de otros ajustes de AEM Forms en JEE.

## Problemas comunes de configuración {#common-configuration}

Una de las cosas más frustrantes sobre el mantenimiento o la solución de problemas de una AEM Forms en un clúster JEE es que no hay un solo lugar para comprobar de forma positiva que el clúster esté en buen estado. Para confirmar que todo está bien en el clúster se necesita un poco de investigación y análisis, y hay varios modos de error para el funcionamiento del clúster, dependiendo de lo que esté mal con la configuración del clúster. La figura siguiente ilustra un clúster mal configurado en el que varios de los recursos compartidos se comparten de forma incorrecta.

![Clúster configurado incorrectamente](assets/bad-configuration-cluster.png)

Comprenda el funcionamiento de la agrupación en clúster y los tipos de elementos que puede buscar y comprobar en un clúster, incluso si no tiene intención de ejecutar AEM Forms en JEE en un clúster. El motivo es que algunas partes de AEM Forms en JEE pueden seguir sus indicaciones sobre cómo operar en un clúster incorrectamente y asumir un comportamiento de clúster que no espera.

Entonces, ¿qué hay de malo con la configuración para compartir de la figura anterior? Las secciones siguientes describen los problemas:

### (1) Configuración del clúster de GemFire {#gemfire-cluster-configuration}

Hay varias cosas que pueden salir mal con el caché de Gemfire. Dos escenarios típicos son:

* Los nodos que deberían poder encontrarse entre sí no pueden hacerlo.

* Los nodos que están agrupados pueden encontrarse entre sí y compartir una caché cuando no deberían.

Si tiene nodos que desea agrupar, es necesario que se encuentren en la red. De forma predeterminada, lo hacen con mensajes UDP de multidifusión. Cada nodo envía mensajes de difusión anunciando que está presente y cualquier nodo que reciba un mensaje de este tipo comienza a hablar con los demás nodos que encuentra. Este tipo de método de autodescubrimiento es común, y muchos tipos de software y dispositivos lo hacen.

Un problema común con la detección automática es que la red puede filtrar los mensajes de multidifusión. Esto puede ser parte de una directiva de red, debido a reglas de firewall de software o porque no pueden enrutarse a través de la red que existe entre nodos. Debido a la dificultad general para que la detección automática de UDP funcione en redes complejas, es habitual que las implementaciones de producción utilicen un método de detección alternativo: localizadores TCP. Se puede encontrar una descripción general de los localizadores TCP en las referencias.

**¿Cómo sé si estoy usando localizadores o UDP?**

Las siguientes propiedades de JVM controlan el método que utiliza la caché de GemFire para encontrar otros nodos.

Configuración de multidifusión:

* `adobe.cache.multicast-port`: puerto de multidifusión utilizado para comunicarse con otros miembros del sistema distribuido. Si se establece en cero, la multidifusión está deshabilitada tanto para la detección como para la distribución de miembros.

* `gemfire.mcast-address` (opcional): invalida la dirección IP predeterminada que usa Gemfire.

Configuración del localizador TCP:

* `adobe.cache.cluster-locators`: la dirección IP/nombre de host del localizador TCP y el puerto del localizador TCP para todos los localizadores utilizados por los miembros del sistema para comunicarse con los localizadores en ejecución.

La lista debe incluir todos los localizadores actualmente en uso y debe configurarse de manera consistente para cada miembro del sistema de clústeres.

Si la lista Ubicadores TCP está vacía, no se usan localizadores y se utiliza el método de multidifusión.

**¿Cómo puedo comprobar si mi localizador TCP se está ejecutando?**

En primer lugar, si los localizadores TCP están en uso, debe tener los localizadores TCP enumerados en la siguiente propiedad JVM en todos los nodos del clúster:

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

No es necesario ejecutar los localizadores en los nodos de clúster de AEM Forms en JEE; si lo desea, se pueden ejecutar en otros sistemas separados del clúster. Más de un sistema puede ejecutar ubicaciones. Y, se considera una práctica recomendada tener localizadores funcionando en dos ubicaciones frente a la posibilidad de que un solo error de los localizadores pueda causar un problema con el reinicio del clúster. En cada uno de los sistemas que ejecutan localizadores, debe poder comprobar que se están ejecutando utilizando los siguientes comandos en esos equipos:

`netstat -an | grep 22345`

La respuesta esperada debe ser esta:

`tcp 0 0 *.22345 *.* LISTEN`

Otro comando de verificación es el siguiente:

`ps -ef | grep gemfire`

La respuesta esperada debería tener un aspecto similar al siguiente:

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**¿Cómo veo los nodos que GemFire piensa que están en el clúster?**

GemFire genera información de registro que puede utilizarse para diagnosticar qué miembros del clúster han sido encontrados y adoptados por la caché de GemFire. Se puede utilizar para comprobar que se encuentran todos los miembros de clúster correctos y que no se está realizando ninguna detección de nodos de clúster adicional o incorrecta. El archivo de registro de GemFire se encuentra en el directorio temporal configurado de AEM Forms en JEE:

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

La cadena numérica después de `adobeZZ_` es única para el nodo de servidor, por lo que debe buscar el contenido real del directorio temporal. Los dos caracteres posteriores a `adobe` dependen del tipo de servidor de aplicaciones: `wl`, `jb` o `ws`.

Los siguientes registros de ejemplo muestran lo que sucede cuando se encuentra un clúster de dos nodos.

En el primer nodo, AP-HP8:

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

En el otro nodo, AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**¿Qué sucede si GemFire encuentra nodos que no debería?**

Cada clúster distinto que comparte una red corporativa debe utilizar un conjunto independiente de localizadores TCP, si se utilizan localizadores TCP, o un número de puerto UDP independiente si se utiliza la configuración UDP de multidifusión. Debido a que la detección automática de UDP es la configuración predeterminada para AEM Forms en JEE y que el mismo puerto predeterminado 33456 está siendo utilizado por varios clústeres, es posible que los clústeres que no deberían intentar comunicarse lo estén haciendo de forma inesperada. Por ejemplo, los clústeres de producción y control de calidad deben permanecer separados, pero pueden conectarse entre sí mediante multidifusión UDP.

La situación más común en la que se pueden detectar puertos duplicados en una red en la que GemFire está creando clústeres incorrectamente es durante la Bootstrap de un clúster. Lo que puede encontrar es que el proceso de Bootstrap falla sin una causa clara. Normalmente, se ven errores como este:

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

En este caso, el programa previo está trabajando con GemFire para acceder a las tablas requeridas. Además, existe una incoherencia entre las tablas a las que se accede a través de JDBC y la información de tablas en caché devuelta por GemFire, que proviene de un clúster diferente con una base de datos subyacente diferente.

Aunque un puerto duplicado suele ser evidente durante Bootstrap, es posible que esta situación se muestre más adelante. Esto puede ocurrir cuando se reinicia un clúster después de estar inactivo cuando se produjo la Bootstrap del otro clúster. O bien, cuando se cambia la configuración de red para que los clústeres que antes estaban aislados, con fines de multidifusión, sean visibles entre sí.

Para diagnosticar estas situaciones, observe los registros de GemFire y considere cuidadosamente si solo se encuentran los nodos esperados. Para corregir el problema, es necesario cambiar la propiedad `adobe.cache.multicast-port` a un valor diferente en uno o ambos clústeres.

### 2) Uso compartido de GDS {#gds-sharing}

El uso compartido de GDS está configurado fuera de AEM Forms en JEE, en el nivel O/S, donde debe organizar que la misma estructura de directorios compartidos esté disponible para todos los nodos de clúster. En sistemas del tipo Windows, esto se logra mediante la configuración de un recurso compartido de archivos de un nodo al otro, o de un sistema de archivos remoto como un dispositivo NAS a todos los nodos. En sistemas UNIX®, el uso compartido de GDS suele realizarse a través del uso compartido de archivos NFS, de nuevo, ya sea de un nodo a otro o desde un dispositivo NAS.

Un posible modo de error para el clúster es si este recurso compartido de archivos remoto deja de estar disponible o tiene problemas sutiles. Un montaje remoto puede fallar debido a problemas de red, configuración de seguridad o configuración incorrecta. Un reinicio del sistema puede provocar cambios de configuración realizados días o semanas antes de que entren en vigor, y esto puede causar sorpresas.

**¿Qué sucedería si un recurso compartido NFS no se monta?**

En UNIX®, la forma en que los montajes NFS se asignan a la estructura de directorios puede permitir que un directorio GDS aparentemente utilizable esté disponible, incluso si el montaje falla. Tenga en cuenta lo siguiente:

* Servidor NAS: carpeta compartida NFS /u01/iapply/livecycle_gds
* Nodo 1: un punto de montaje en la carpeta compartida (alojada en el servidor DB) ubicada aquí: /u01/iapply/livecycle_gds
* Nodo 2: un punto de montaje en la carpeta compartida (alojada en el servidor DB) ubicada aquí: /u01/iapply/livecycle_gds

* LCES especifica la ruta a GDS: /u01/iapply/livecycle_gds

Si se produce un error en el montaje del nodo 1, la estructura del directorio aún contiene una ruta de acceso `/u01/iapply/livecycle_gds` al punto de montaje vacío y el nodo parece ejecutarse correctamente. Sin embargo, como el contenido de GDS no se comparte realmente con el otro nodo, el clúster no funciona correctamente. Esto puede ocurrir y sucede, y el resultado es que el clúster falla de maneras misteriosas.

La práctica recomendada es organizar las cosas para que el punto de montaje de Linux® no se use como raíz del GDS, sino que se use algún directorio dentro de él como raíz del GDS:

* Si tiene un servidor NFS, puede tener un directorio: /some/storage/lc_cluster_dev/LC_GDS
* Y en el nodo de clúster tiene un punto de montaje: /u01/iapply/shared
* Monte nfs_server: /some/storage/lc_cluster_dev/u01/iapply/shared
* Dirija su GDS a /u01/iapply/shared/LC_GDS

Ahora, si por alguna razón el montaje no tiene éxito, el punto de montaje no contiene un directorio LC_GDS y el clúster falla de forma predecible porque no puede encontrar ningún GDS.

**¿Cómo puedo verificar que todos los nodos ven el mismo GDS y tienen permisos?**

La verificación del acceso y el uso compartido de GDS se realiza mejor accediendo a cada uno de los nodos como un usuario interactivo. Puede hacerlo a través de SSH o telnet a nodos UNIX®, o a través del escritorio remoto a sistemas Windows. Debe poder navegar al directorio o sistema de archivos GDS configurado en cada nodo y crear archivos de prueba a partir de cada nodo que esté visible en todos los demás nodos.

Preste atención al ID de usuario con el que funciona AEM Forms en JEE. En instalaciones llave en mano de Windows, se trata de un administrador local. En UNIX®, puede ser como un usuario de servicio específico configurado en el script de inicio o en la configuración del servidor de aplicaciones. Es importante que este ID de usuario pueda crear y manipular archivos GDS de forma equitativa en todos los nodos.

En sistemas UNIX®, las configuraciones NFS suelen ser predeterminadas para desconfiar de la propiedad raíz o de los derechos de acceso raíz a archivos y objetos. Si está ejecutando el servidor de aplicaciones como usuario raíz, puede que necesite especificar opciones en el servidor NFS, en el nodo que monta los archivos o en ambos. Al hacerlo, se permite el acceso y control bilateral de los archivos creados por un nodo y a los que se accede desde otro.

### (3) Uso compartido de bases de datos {#database-sharing}

Para que un clúster funcione correctamente, todos los miembros del clúster deben compartir la misma base de datos. El margen para equivocarse en esto es más o menos:

* configurar accidentalmente IDP_DS, EDC_DS, AdobeDefaultSA_DS u otras fuentes de datos necesarias de forma diferente en nodos de clúster independientes, de modo que los nodos apunten a bases de datos diferentes.
* configurar accidentalmente varios nodos independientes para compartir una base de datos cuando no deberían hacerlo.

Según el servidor de aplicaciones, puede ser natural que la conexión JDBC se defina en un ámbito de clúster, por lo que no es posible utilizar definiciones diferentes en nodos diferentes. Sin embargo, en JBoss® es totalmente posible configurar cosas para que una fuente de datos, como IDP_DS, apunte a una base de datos en el nodo 1, pero apunte a otra cosa en el nodo 2.

El problema de la marcha atrás es más común. Es decir, una situación en la que varios nodos independientes (o de clúster) de AEM Forms en nodos JEE apuntan accidentalmente al mismo esquema cuando no están pensados para hacerlo. Esto suele ocurrir cuando un DBA, sin saberlo, proporciona una sola información de conexión de AEM Forms en la base de datos JEE a los equipos de configuración de DEV y QA. Ninguno de los dos equipos se da cuenta de que las instancias de DEV y QA requieren bases de datos independientes.

## Clúster del servidor de aplicaciones {#application-server-cluster-1}

Para tener un clúster de AEM Forms en JEE correcto, el servidor de aplicaciones debe configurarse y funcionar correctamente como un clúster. En WebSphere® y WebLogic, se trata de un proceso directo y bien documentado. En JBoss®, la configuración de clústeres es un poco más práctica, y garantizar que los nodos estén configurados para actuar como un clúster y que, de hecho, encuentren y se comuniquen entre sí puede ser un desafío. JBoss® se basa internamente en JGroups, que utiliza multidifusión UDP para buscar y coordinar con nodos del mismo nivel. Algunos de los problemas mencionados con GemFire pueden ocurrir, como los nodos que no se encuentran entre sí cuando deberían, o que se encuentran entre sí cuando no deberían.

Referencias:

* [Servicios empresariales de alta disponibilidad mediante clústeres JBoss®](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Clústeres que usan Oracle WebLogic Server](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### ¿Cómo puedo comprobar si JBoss® se está agrupando correctamente? {#check-jboss-clustering}

Cuando se inicia JBoss®, a medida que se detectan miembros del clúster, los mensajes de nivel INFO sobre el nodo que se une al clúster se registran en el archivo o la consola de registro.

Si se especificó un nombre de clúster mediante la opción de línea de comandos -g durante la ejecución, verá mensajes similares a los siguientes:

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Planificador de cuarzo {#quartz-scheduler}

Por lo general, AEM Forms en el uso de JEE del programador Quartz interno en un clúster está diseñado para seguir automáticamente la configuración de clúster global de AEM Forms en JEE en general. Sin embargo, hay un error, #2794033, que hace que la configuración automática de clúster de Quartz falle si se están utilizando localizadores TCP para Gemfire en lugar de la detección automática de multidifusión. En este caso, Quartz se ejecuta incorrectamente en un modo no agrupado. Esto crea interbloqueos y datos dañados en las tablas de Quartz. Los efectos secundarios son peores en la versión 8.2.x que en la 9.0, ya que el cuarzo no se usa tanto, pero sigue ahí.

Las correcciones están disponibles de la siguiente manera para este problema: 8.2.1.2 QF2.143 y 9.0.0.2 QF2.44.

También existe una solución alternativa, que es establecer estas dos propiedades:

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

Una configuración utiliza un punto entre &quot;cluster&quot; y &quot;locators&quot; y la otra utiliza un guión. Esto es fácil de implementar y menos riesgoso que aplicar un parche de software, pero implica crear artificialmente una configuración adicional confusa y con nombre incorrecto.

### ¿Cómo puedo comprobar que Quartz se está ejecutando como un solo nodo o clúster? {#check-quartz}

Para determinar cómo se ha configurado Quartz, debe consultar los mensajes generados por el servicio Programador de AEM Forms en JEE durante el inicio. Estos mensajes se generan con una gravedad INFO y puede ser necesario ajustar el nivel de registro y reiniciar para obtener los mensajes. Dentro de la secuencia de inicio de AEM Forms en JEE, la inicialización de Quartz comienza con la siguiente línea:

INFORMACIÓN `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
Es importante localizar esta primera línea en los registros. El motivo es que algunos servidores de aplicaciones utilizan también Quartz y sus instancias de Quartz no deben confundirse con las instancias que utiliza el servicio Programador de AEM Forms en JEE. Esta es la indicación de que el servicio Planificador se está iniciando y las líneas que lo siguen le indican si se está iniciando correctamente en modo agrupado. Varios mensajes aparecen en esta secuencia, y es el último mensaje &quot;iniciado&quot; que revela cómo Quartz está configurado:

Aquí se proporciona el nombre de la instancia de Quartz: `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. El nombre de la instancia Quartz del programador siempre comienza con la cadena `IDPSchedulerService_$_`. La cadena que se anexa al final de esto le indica si Quartz se está ejecutando en modo agrupado. El identificador único largo generado a partir del nombre de host del nodo y una cadena larga de dígitos, aquí `ap-hp8.ottperflab.adobe.com1312883903975`, indican que está funcionando en un clúster. Si funciona como un solo nodo, el identificador es un número de dos dígitos, &quot;20&quot;:

Se inició el programador de información `[org.quartz.core.QuartzScheduler]` `IDPSchedulerService_$_20`.
Esta comprobación debe realizarse en todos los nodos del clúster por separado, ya que el programador de cada nodo determina de forma independiente si se debe operar en modo de clúster.

### ¿Qué tipo de problemas se producen si Quartz se está ejecutando en el modo incorrecto? {#quartz-running-in-wrong-mode}

Si Quartz está configurado para ejecutarse como un solo nodo, pero se está ejecutando en un clúster y comparte tablas de bases de datos de Quartz con otros nodos, el resultado es un funcionamiento poco fiable del servicio Programador de AEM Forms en JEE. Y a menudo va acompañado de interbloqueos en las bases de datos. Este es un seguimiento de pila bastante típico que podría ver en esta situación:

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Could not remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### ¿Cómo se sincronizan los relojes del sistema en un clúster? {#synchronize-system-clocks-cluster}

Para que un clúster funcione sin problemas, los relojes de todos los nodos del clúster deben estar estrechamente sincronizados. Esto no se puede hacer de forma adecuada a mano y debe hacerlo algún tipo de servicio de sincronización de tiempo que se ejecute regularmente. Los relojes de todos los nodos deben estar separados por un segundo entre sí. La práctica recomendada dicta que no solo se sincronicen los nodos de clúster, sino también el equilibrador de carga, el servidor de base de datos, el servidor NAS de GDS y cualquier otro componente.

La sincronización horaria de Windows tiende a ser al controlador de dominio. Los sistemas UNIX® pueden sincronizarse usando NTP a una fuente de tiempo diferente. Es mejor si todos los sistemas (tanto los nodos de AEM Forms en JEE como otros componentes del sistema) se sincronizan con el mismo origen, si es posible.

No es suficiente, incluso en los entornos de prueba más temporales, configurar manualmente los relojes en los nodos. La configuración manual de los relojes no ofrece suficiente sincronización precisa, y los relojes de los dos nodos inevitablemente se desvían entre sí, incluso durante un período de solo un día. Un mecanismo de sincronización de tiempo activo es esencial para un funcionamiento fiable del clúster.

### Equilibrador de carga {#load-balancer}

Un requisito típico de un clúster que proporciona servicios interactivos para el usuario es un equilibrador de carga HTTP que distribuye las solicitudes HTTP a través del clúster. El uso correcto de un equilibrador de carga con un AEM Forms en un clúster JEE requiere la configuración de lo siguiente:

* permanencia de sesión

* Reglas de reescritura de URL

* comprobación de estado del nodo

### ¿Qué debo hacer con la función de comprobación de estado del equilibrador de carga? {#load-balancer-health-check}

Algunos equilibradores de carga se pueden configurar para realizar una comprobación de estado periódica en los nodos que se equilibran de carga. Normalmente, es la dirección URL de una función de la aplicación a la que intenta acceder el equilibrador de carga. Si la carga se realiza correctamente, se supone que el nodo está en buen estado y se mantiene en el conjunto de equilibrio de carga. Si la dirección URL no se puede cargar, se asume que el nodo es defectuoso y se elimina del conjunto. Normalmente, la URL de comprobación de estado está conectada a AEM Forms en la página de inicio de sesión de la IU del administrador de JEE. Esta no es una comprobación de estado ideal para un miembro del clúster y sería mejor implementar un proceso de corta duración y utilizar la URL de la API de REST como función de comprobación de estado.

## Ruta de archivo temporal y configuración de clúster similar {#temporary-file-path-cluster-settings}

Ciertas configuraciones de ruta de archivo dentro de AEM Forms en JEE se establecen en todo el clúster y tienen la misma configuración efectiva en cada nodo, pero se interpretan de forma independiente en cada nodo para hacer referencia a archivos locales. Los elementos clave que hay que tener en cuenta son la configuración de rutas de fuentes y la configuración de directorios temporales. Vaya a la pantalla AdminUI Core Configurations (Inicio > Configuración > Sistema principal > Configuraciones principales)

Se deben comprobar las siguientes configuraciones:

1. Ubicación del directorio temporal
1. Ubicación del directorio de Adobe Server Fonts
1. Ubicación del directorio de fuentes del cliente
1. Ubicación del directorio de fuentes del sistema
1. Ubicación del archivo de configuración de los servicios de datos

El clúster sólo tiene una única ruta de acceso para cada una de estas opciones de configuración. Por ejemplo, la ubicación del directorio Temp podría ser `/home/project/QA2/LC_TEMP`. En un clúster, es necesario que cada nodo tenga realmente esta ruta particular accesible. Si un nodo tiene la ruta de archivo temporal esperada y otro nodo no, el nodo que no la tiene funciona incorrectamente.

Aunque estos archivos y rutas de acceso pueden compartirse entre los nodos o ubicarse por separado, o en sistemas de archivos remotos, se recomienda que sean copias locales en el almacenamiento en disco del nodo local.

La ruta del Directorio temporal, en particular, no debe compartirse entre nodos. Un procedimiento similar al descrito para verificar que el GDS debe usarse para verificar que el directorio temporal no se está compartiendo. Vaya a cada nodo, cree un archivo temporal en la ruta indicada por la configuración de ruta y, a continuación, compruebe que los demás nodos no comparten el archivo. La ruta del directorio temporal debe hacer referencia al almacenamiento en disco local en cada nodo, si es posible, y debe comprobarse.

Para cada una de las configuraciones de ruta, asegúrese de que la ruta realmente existe y es accesible desde cada nodo del clúster, utilizando la identidad de uso efectiva en la que se ejecuta AEM Forms en JEE. El contenido del directorio de fuentes debe ser legible. El directorio temporal debe permitir lectura, escritura y control.
