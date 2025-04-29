---
title: Cómo ejecutar AEM con el modo de espera pasiva TarMK
description: Aprenda a crear, configurar y mantener una configuración de espera en frío de TarMK.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 71e3d2cd-4e22-44a2-88dd-1f165bf2b3d8
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 0%

---

# Cómo ejecutar AEM con el modo de espera pasiva TarMK{#how-to-run-aem-with-tarmk-cold-standby}

## Introducción {#introduction}

La capacidad de espera en frío del núcleo Tar Micro permite que una o más instancias de Adobe Experience Manager en espera (AEM) se conecten a una instancia principal. El proceso de sincronización es de una sola manera, lo que significa que solo se realiza desde la instancia principal a la instancia en espera.

El propósito de las instancias en espera es garantizar una copia de datos activa del repositorio principal y garantizar un cambio rápido sin pérdida de datos en caso de que el repositorio principal no esté disponible por algún motivo.

El contenido se sincroniza linealmente entre la instancia principal y las instancias en espera sin que la integridad compruebe si hay daños en el archivo o repositorio. Debido a este diseño, las instancias en espera son copias exactas de la instancia principal y no pueden ayudar a mitigar las incoherencias en las instancias principales.

>[!NOTE]
>
>La función de espera en frío está diseñada para proteger escenarios donde se requiere alta disponibilidad en **instancias de autor**. Para situaciones en las que se requiere alta disponibilidad en instancias de **Publish** que utilizan el núcleo de Tar Micro, Adobe recomienda utilizar una granja de servidores de publicación.
>
>Para obtener información sobre implementaciones más disponibles, consulte la página [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Cuando la instancia en espera está configurada o se deriva del nodo Principal, solo permite el acceso a la siguiente consola (para actividades relacionadas con la administración):
>
>* Consola web OSGI
>
>No se puede acceder a otras consolas.

## Funcionamiento {#how-it-works}

En la instancia principal de AEM, se abre un puerto TCP que escucha los mensajes entrantes. Actualmente, hay dos tipos de mensajes que los esclavos envían al maestro:

* un mensaje que solicita el ID de segmento del encabezado actual
* un mensaje que solicita datos de segmento con un ID especificado

El modo de espera solicita periódicamente el ID de segmento del encabezado actual del principal. Si el segmento es localmente desconocido, se recupera. Si ya está presente, se comparan los segmentos y se solicitan los segmentos a los que se hace referencia, si es necesario.

>[!NOTE]
>
>Las instancias en espera no reciben ningún tipo de solicitudes porque se ejecutan en modo de solo sincronización. La única sección disponible en una instancia de espera es la consola web para facilitar la configuración de paquetes y servicios.

Una implementación típica de TarMK en modo de espera en frío:

![chlimage_1](assets/chlimage_1.png)

## Otras características {#other-characteristics}

### Solidez {#robustness}

El flujo de datos está diseñado para detectar y gestionar automáticamente los problemas de conexión y de red. Todos los paquetes están empaquetados con sumas de comprobación y cuando se producen problemas con la conexión o paquetes dañados, se activan los mecanismos de reintento.

#### Rendimiento {#performance}

Habilitar el modo de espera en frío de TarMK en la instancia principal casi no tiene ningún impacto mensurable en el rendimiento. El consumo adicional de CPU es bajo y el disco duro y la E/S de red adicionales no deberían producir ningún problema de rendimiento.

En el modo de espera, se espera un alto consumo de CPU durante el proceso de sincronización. Como el procedimiento no es multiproceso, no se puede acelerar utilizando varios núcleos. Si no se cambian ni transfieren datos, no hay actividad mensurable. La velocidad de conexión varía según el hardware y el entorno de red, pero no depende del tamaño del repositorio ni del uso de SSL. Tenga esto en cuenta a la hora de estimar el tiempo necesario para una sincronización inicial o cuando se hayan cambiado muchos datos en el ínterin en el nodo principal.

#### Seguridad {#security}

Suponiendo que todas las instancias se ejecuten en la misma zona de seguridad de intranet, el riesgo de una infracción de seguridad se reduce en gran medida. Sin embargo, puede añadir una capa de seguridad adicional habilitando conexiones SSL entre los esclavos y el maestro. Al hacerlo, se reduce la posibilidad de que los datos se vean comprometidos por un intermediario.

Además, puede especificar las instancias de espera a las que se permite conectarse restringiendo la dirección IP de las solicitudes entrantes. Esto debería ayudar a garantizar que nadie en la intranet pueda copiar el repositorio.

>[!NOTE]
>
>Se recomienda añadir un equilibrador de carga entre Dispatcher y los servidores que forman parte de la configuración de la espera en frío. El equilibrador de carga debe configurarse para dirigir el tráfico de usuarios únicamente a la instancia **primary**. Esto es necesario para garantizar la coherencia y evitar que el contenido se copie en la instancia de espera por otros medios que no sean el mecanismo de espera en frío.

## Creación de una configuración de AEM TarMK Cold Standby {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>El PID del almacén de nodos de segmentos y el servicio de almacén en espera ha cambiado en AEM 6.3 en comparación con las versiones anteriores de la siguiente manera:
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService a org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Realice los ajustes de configuración necesarios para que reflejen este cambio.

Para crear una configuración de espera en frío de TarMK, cree primero las instancias de espera realizando una copia del sistema de archivos de toda la carpeta de instalación del principal en una nueva ubicación. A continuación, puede iniciar cada instancia con un modo de ejecución que especifique su función ( `primary` o `standby`).

A continuación se muestra el procedimiento que debe seguirse para crear una configuración con una instancia maestra y una en espera:

1. Instale AEM.

1. Cierre la instancia y copie su carpeta de instalación en la ubicación desde la que se ejecuta la instancia de espera pasiva. Aunque esté ejecutando desde equipos diferentes, asegúrese de asignar a cada carpeta un nombre descriptivo (como *aem-primary* o *aem-standby*) para diferenciar entre las instancias.
1. Vaya a la carpeta de instalación de la instancia principal y:

   1. Compruebe y elimine cualquier configuración de OSGi anterior que pueda tener bajo `aem-primary/crx-quickstart/install`

   1. Cree una carpeta llamada `install.primary` en `aem-primary/crx-quickstart/install`

   1. Cree las configuraciones necesarias para el almacén de nodos y el almacén de datos preferidos en `aem-primary/crx-quickstart/install/install.primary`
   1. Cree un archivo llamado `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` en la misma ubicación y configúrelo en consecuencia. Para obtener más información sobre las opciones de configuración, consulte [Configuración](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. Si usa una instancia de AEM TarMK con un almacén de datos externo, cree una carpeta denominada `crx3` en `aem-primary/crx-quickstart/install` denominada `crx3`

   1. Coloque el archivo de configuración del almacén de datos en la carpeta `crx3`.

   Por ejemplo, si está ejecutando una instancia de AEM TarMK con un almacén de datos de archivos externo, necesita estos archivos de configuración:

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   A continuación, busque configuraciones de ejemplo para la instancia principal:

   **Muestra de** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Muestra de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Inicie el principal asegurándose de especificar el modo de ejecución principal:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Cree un registrador de Apache Sling para el paquete **org.apache.jackrabbit.oak.segment**. Establezca el nivel de registro en &quot;Depuración&quot; y señale su salida de registro a un archivo de registro independiente, como */logs/tarmk-coldstandby.log*. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).
1. Vaya a la ubicación de la instancia **standby** e iníciela ejecutando el JAR.
1. Cree la misma configuración de registro que para el principal. A continuación, detenga la instancia.
1. A continuación, prepare la instancia de espera. Para ello, siga los mismos pasos que para la instancia principal:

   1. Elimine cualquier archivo que pueda tener bajo `aem-standby/crx-quickstart/install`.
   1. Cree una carpeta llamada `install.standby` en `aem-standby/crx-quickstart/install`

   1. Cree dos archivos de configuración llamados:

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. Cree una carpeta llamada `crx3` en `aem-standby/crx-quickstart/install`

   1. Cree la configuración del almacén de datos y colóquela en `aem-standby/crx-quickstart/install/crx3`. Para este ejemplo, el archivo que debe crear es:

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. Edite los archivos y cree las configuraciones necesarias.

   A continuación se muestran archivos de configuración de ejemplo para una instancia de espera típica:

   **Ejemplo de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Ejemplo de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Muestra de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Iniciar la instancia **standby** mediante el modo de ejecución en espera:

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

El servicio también se puede configurar a través de la consola web mediante:

1. Ir a la consola web en: *https://serveraddress:serverport/system/console/configMgr*
1. Buscando un servicio llamado **Apache Jackrabbit Oak Segment Tar Cold Standby Service** y haga doble clic para editar la configuración.
1. Guardar la configuración y reiniciar las instancias para que la nueva configuración surta efecto.

>[!NOTE]
>
>Puede comprobar el rol de una instancia en cualquier momento si comprueba la presencia de los modos de ejecución **primary** o **standby** en la consola web de configuración de Sling.
>
>Esto se puede hacer yendo a *https://localhost:4502/system/console/status-slingsettings* y comprobando la línea **&quot;Modos de ejecución&quot;**.

## Sincronización por primera vez {#first-time-synchronization}

Una vez finalizada la preparación y iniciada la espera por primera vez, hay mucho tráfico de red entre las instancias a medida que la espera alcanza el nivel principal. Puede consultar los registros para observar el estado de la sincronización.

En el *tarmk-coldstandby.log* en espera, puede ver entradas como las siguientes:

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

En *error.log* del modo de espera, debería ver una entrada como esta:

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

En el fragmento de registro anterior, *10.20.30.40* es la dirección IP del principal.

En **primary** *tarmk-coldstandby.log*, verá entradas como las siguientes:

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

En este caso, el &quot;cliente&quot; mencionado en el registro es la instancia de **standby**.

Una vez que estas entradas dejan de aparecer en el registro, puede suponer con seguridad que el proceso de sincronización ha finalizado.

Aunque las entradas anteriores muestran que el mecanismo de sondeo funciona correctamente, a menudo resulta útil saber si hay datos sincronizados mientras se realiza el sondeo. Para ello, busque entradas como las siguientes:

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

Además, cuando se ejecuta con un objeto `FileDataStore` no compartido, mensajes como los siguientes confirman que los archivos binarios se transmiten correctamente:

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuración {#configuration}

La siguiente configuración de OSGi está disponible para el servicio de espera en frío:

* **Configuración persistente:** si está habilitada, esto almacena la configuración en el repositorio en lugar de los archivos de configuración OSGi tradicionales. Adobe recomienda mantener esta configuración deshabilitada en los sistemas de producción para que el modo de espera no recupere la configuración principal.

* **Modo (`mode`):** esto elige el modo de ejecución de la instancia.

* **Puerto (puerto):** el puerto que se utilizará para la comunicación. El valor predeterminado es `8023`.

* **Host principal (`primary.host`):**: el host de la instancia principal. Esta configuración solo se aplica al modo de espera.
* **Intervalo de sincronización (`interval`):**: esta configuración determina el intervalo entre la solicitud de sincronización y solo se aplica a la instancia de espera.

* **Intervalos de IP permitidos (`primary.allowed-client-ip-ranges`):**: los intervalos de IP desde los que el principal permite conexiones.
* **Seguro (`secure`):** Habilitar el cifrado SSL. Para utilizar esta configuración, debe estar habilitada en todas las instancias.
* **Tiempo de espera de lectura en espera (`standby.readtimeout`):** Tiempo de espera para solicitudes emitidas desde la instancia en espera en milisegundos. El valor predeterminado utilizado es 60000 (un minuto).

* **Limpieza automática en espera (`standby.autoclean`):** Llame al método cleanup si el tamaño del almacén aumenta en un ciclo de sincronización.

>[!NOTE]
>
>Adobe recomienda que el repositorio principal y el de espera tengan ID de repositorio diferentes para que se puedan identificar por separado para servicios como la descarga.
>
>La mejor manera de asegurarse de que esto se cubre es eliminar *sling.id* en espera y reiniciar la instancia.

## Procedimientos de failover {#failover-procedures}

Si la instancia principal falla por algún motivo, puede establecer una de las instancias en espera para que asuma el rol de la principal cambiando el modo de ejecución de inicio como se detalla a continuación:

>[!NOTE]
>
>Edite los archivos de configuración para que coincidan con la configuración utilizada para la instancia principal.

1. Vaya a la ubicación donde está instalada la instancia de espera y deténgala.

1. Si tiene un equilibrador de carga configurado con la configuración, puede quitar el principal de la configuración del equilibrador de carga en este punto.
1. Haga una copia de seguridad de la carpeta `crx-quickstart` desde la carpeta de instalación en espera. Se puede utilizar como punto de partida al configurar una nueva espera.

1. Reinicie la instancia con el modo de ejecución `primary`:

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Añada el nuevo principal al equilibrador de carga.
1. Crear e iniciar una nueva instancia de espera. Para obtener más información, consulte el procedimiento anterior en [Creación de una configuración de espera en frío TarMK de AEM](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Aplicación de revisiones a una configuración de espera en frío {#applying-hotfixes-to-a-cold-standby-setup}

La forma recomendada de aplicar revisiones a una configuración de espera fría es instalándolas en la instancia principal y luego clonándolas en una nueva instancia de espera fría con las revisiones instaladas.

Para ello, siga los pasos descritos a continuación:

1. Para detener el proceso de sincronización en la instancia de espera fría, vaya a la consola JMX y use el bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Para obtener más información sobre cómo hacerlo, consulte la sección sobre [Supervisión](#monitoring).
1. Detenga la instancia de espera pasiva.
1. Instale la revisión en la instancia principal. Para obtener más información sobre cómo instalar una revisión, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).
1. Pruebe la instancia para ver si hay problemas después de la instalación.
1. Elimine la instancia de espera pasiva eliminando su carpeta de instalación.
1. Detenga la instancia principal y clóquela realizando una copia del sistema de archivos de toda la carpeta de instalación en la ubicación del modo de espera en frío.
1. Vuelva a configurar el clon recién creado para que actúe como una instancia de espera en frío. Ver [Creación de una configuración de espera en frío de AEM TarMK.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Inicie las instancias primaria y de espera en frío.

## Monitoreo {#monitoring}

La función expone información mediante JMX o MBeans. Al hacerlo, puede inspeccionar el estado actual del modo de espera y del maestro mediante la [consola JMX](/help/sites-administering/jmx-console.md). La información se encuentra en un MBean de `type org.apache.jackrabbit.oak:type="Standby"`llamados `Status`.

**En espera**

Al observar una instancia de espera, se expone un nodo. El ID suele ser un UUID genérico.

Este nodo tiene cinco atributos de solo lectura:

* `Running:` valor booleano que indica si el proceso de sincronización se está ejecutando o no.

* Cliente `Mode:`: seguido del UUID utilizado para identificar la instancia. Este UUID cambia cada vez que se actualiza la configuración.

* `Status:` es una representación textual del estado actual (como `running` o `stopped`).

* `FailedRequests:`número de errores consecutivos.
* `SecondsSinceLastSuccess:` el número de segundos desde la última comunicación correcta con el servidor. Muestra `-1` si no se realizó ninguna comunicación correcta.

También hay tres métodos invocables:

* `start():` inicia el proceso de sincronización.
* `stop():` detiene el proceso de sincronización.
* `cleanup():` ejecuta la operación de limpieza en modo de espera.

**Principal**

La observación de la principal expone cierta información general a través de un MBean cuyo valor de ID es el número de puerto que utiliza el servicio de espera TarMK (8023 de forma predeterminada). La mayoría de los métodos y atributos son los mismos que para el modo de espera, pero algunos difieren:

* `Mode:` siempre muestra el valor `primary`.

Además, se puede recuperar información para un máximo de diez clientes (instancias en espera) conectados al servidor maestro. El ID de MBean es el UUID de la instancia. No hay métodos invocables para estos MBean, pero hay algunos atributos útiles de solo lectura:

* `Name:` el ID del cliente.
* `LastSeenTimestamp:` marca de tiempo de la última solicitud en una representación de texto.
* `LastRequest:` la última solicitud del cliente.
* `RemoteAddress:` la dirección IP del cliente.
* `RemotePort:` el puerto que el cliente utilizó para la última solicitud.
* `TransferredSegments:` el número total de segmentos transferidos a este cliente.
* `TransferredSegmentBytes:`número total de bytes transferidos a este cliente.

## Mantenimiento del repositorio de espera en frío {#cold-standby-repository-maintenance}

### Limpieza de revisión {#revision-clean}

>[!NOTE]
>
>Si ejecuta [Limpieza de revisión en línea](/help/sites-deploying/revision-cleanup.md) en la instancia principal, no es necesario el procedimiento manual que se muestra a continuación. Además, si está utilizando Limpieza de revisión en línea, la operación `cleanup ()` en la instancia de espera se realiza automáticamente.

>[!NOTE]
>
>No ejecute la limpieza de revisión sin conexión en modo de espera. No es necesario y no reduce el tamaño del almacén de segmentos.

Adobe recomienda ejecutar el mantenimiento regularmente para evitar un crecimiento excesivo del repositorio a lo largo del tiempo. Para realizar manualmente el mantenimiento del repositorio de espera en frío, siga los pasos a continuación:

1. Detenga el proceso de espera en la instancia de espera en la consola JMX y use el **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)** bean. Para obtener más información sobre cómo hacerlo, consulte la sección anterior sobre [Supervisión](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. Detenga la instancia principal de AEM.
1. Ejecute la herramienta de compactación de Oak en la instancia principal. Para obtener más información, consulte [Mantenimiento del repositorio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Inicie la instancia principal.
1. Inicie el proceso en espera en la instancia de espera utilizando el mismo Bean JMX como se describe en el primer paso.
1. Vea los registros y espere a que se complete la sincronización. Es posible que actualmente se observe un crecimiento sustancial en el repositorio de reserva.
1. Ejecute la operación `cleanup()` en la instancia de espera, utilizando el mismo bean JMX como se describe en el primer paso.

La instancia de espera puede tardar más de lo normal en completar la sincronización con la compactación principal, ya que la compactación sin conexión reescribe efectivamente el historial del repositorio, lo que hace que el cálculo de los cambios en los repositorios tarde más tiempo. Una vez finalizado este proceso, el tamaño del repositorio en espera es aproximadamente el mismo que el del repositorio en el repositorio principal.

Como alternativa, el repositorio principal se puede copiar manualmente al modo de espera después de ejecutar la compactación en el repositorio principal, lo que básicamente reconstruye el modo de espera cada vez que se ejecuta la compactación.

### Recopilación de datos almacenados desechables {#data-store-garbage-collection}

Es importante ejecutar la recolección de basura en las instancias del almacén de datos de archivos de vez en cuando, de lo contrario, los binarios eliminados permanecen en el sistema de archivos y finalmente llenan la unidad. Para ejecutar la recolección de elementos no utilizados, siga el siguiente procedimiento:

1. Ejecute el mantenimiento del repositorio de espera en frío como se describe en la sección [anterior](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Una vez completado el proceso de mantenimiento y reiniciadas las instancias:

   * En el principal, ejecute la recolección de elementos no utilizados del almacén de datos mediante el Bean JMX correspondiente como se describe en [Ejecución de la recolección de elementos no utilizados del almacén de datos mediante la consola JMX](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * En espera, la recolección de elementos no utilizados del almacén de datos solo está disponible a través de **BlobGarbageCollection** MBean - `startBlobGC()`. El MBean **RepositoryManagement** no está disponible en espera.

   >[!NOTE]
   >
   >Si no utiliza un almacén de datos compartido, ejecute primero la recolección de elementos no utilizados en el principal y, a continuación, en espera.
