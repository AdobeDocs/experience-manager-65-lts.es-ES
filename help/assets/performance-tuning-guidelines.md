---
title: Ajuste de rendimiento [!DNL Assets].
description: Sugerencias e instrucciones sobre la configuración de  [!DNL Experience Manager] y cambios en el hardware, el software y los componentes de red para eliminar cuellos de botella y optimizar el rendimiento de [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guía de optimización de rendimiento {#assets-performance-tuning-guide}

Una configuración de [!DNL Experience Manager Assets] contiene varios componentes de hardware, software y red. Según el escenario de implementación, es posible que necesite realizar cambios de configuración específicos en los componentes de hardware, software y red para eliminar los cuellos de botella de rendimiento.

Además, identificar y cumplir ciertas directrices de optimización de hardware y software ayuda a crear una base sólida que permite que la implementación de [!DNL Experience Manager Assets] cumpla las expectativas en cuanto a rendimiento, escalabilidad y confiabilidad.

Un rendimiento deficiente en [!DNL Experience Manager Assets] puede afectar a la experiencia del usuario en torno al rendimiento interactivo, el procesamiento de recursos, la velocidad de descarga y otras áreas.

De hecho, la optimización del rendimiento es una tarea fundamental que se realiza antes de establecer métricas de destino para cualquier proyecto.

Estas son algunas áreas de enfoque clave en torno a las cuales se descubren y corrigen problemas de rendimiento antes de que afecten a los usuarios.

## Plataforma {#platform}

Aunque Experience Manager es compatible con varias plataformas, Adobe ha encontrado la mayor compatibilidad con herramientas nativas en Linux y Windows, lo que contribuye a un rendimiento óptimo y a una implementación sencilla. Lo ideal es implementar un sistema operativo de 64 bits para satisfacer los altos requisitos de memoria de una implementación de [!DNL Experience Manager Assets]. Al igual que con cualquier implementación de Experience Manager, debe implementar TarMK siempre que sea posible. Aunque TarMK no puede escalar más allá de una sola instancia de autor, se encuentra que tiene un mejor rendimiento que MongoMK. Puede agregar instancias de descarga TarMK para aumentar la potencia de procesamiento del flujo de trabajo de su implementación de [!DNL Experience Manager Assets].

### Carpeta temporal {#temp-folder}

Para mejorar los tiempos de carga de los recursos, utilice un almacenamiento de alto rendimiento para el directorio temporal de Java. En Linux y Windows, se podría utilizar una unidad RAM o SSD. En entornos basados en la nube, se podría utilizar un tipo de almacenamiento de alta velocidad equivalente. Por ejemplo, en Amazon EC2, se puede usar una unidad [efímera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) para la carpeta temporal.

Si el servidor tiene suficiente memoria, configure una unidad de RAM. En Linux, ejecute estos comandos para crear una unidad de 8 GB de RAM:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

En el sistema operativo Windows, utilice un controlador de terceros para crear una unidad RAM o simplemente utilice un almacenamiento de alto rendimiento como SSD.

Una vez que el volumen temporal de alto rendimiento esté listo, establezca el parámetro de JVM `-Djava.io.tmpdir`. Por ejemplo, puede agregar el parámetro JVM siguiente a la variable `CQ_JVM_OPTS` en el script `bin/start` de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuración de Java {#java-configuration}

### Versión de Java {#java-version}

Adobe recomienda implementar [!DNL Experience Manager Assets] en Java 8 para obtener un rendimiento óptimo.

<!-- TBD: Link to the latest official word around Java.
-->

### Parámetros de JVM {#jvm-parameters}

Establezca los siguientes parámetros de JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuración del almacén de datos y la memoria {#data-store-and-memory-configuration}

### Configuración del almacén de datos de archivos {#file-data-store-configuration}

Se recomienda separar el almacén de datos del almacén de segmentos para todos los usuarios de [!DNL Experience Manager Assets]. Además, configurar los parámetros `maxCachedBinarySize` y `cacheSizeInMB` puede ayudar a maximizar el rendimiento. Establezca `maxCachedBinarySize` en el tamaño de archivo más pequeño que se pueda guardar en la caché. Especifique el tamaño de la caché en memoria que se utilizará para el almacén de datos en `cacheSizeInMB`. Adobe recomienda establecer este valor entre el 2 % y el 10 % del tamaño total de la pila. Sin embargo, las pruebas de carga y rendimiento pueden ayudar a determinar la configuración ideal.

### Configurar el tamaño máximo de la caché de imágenes almacenadas en búfer {#configure-the-maximum-size-of-the-buffered-image-cache}

Al cargar grandes cantidades de recursos en [!DNL Adobe Experience Manager], para permitir picos inesperados en el consumo de memoria y evitar que JVM falle con OutOfMemoryErrors, reduzca el tamaño máximo configurado de la caché de imágenes almacenadas en búfer. Imagine un ejemplo que tiene un sistema con un montón máximo (- `Xmx`param) de 5 GB, un Oak BlobCache establecido en 1 GB y un Document Cache establecido en 2 GB. En este caso, la caché almacenada en búfer tardaría un máximo de 1,25 GB y memoria, lo que dejaría solo 0,75 GB de memoria para picos inesperados.

Configure el tamaño de la caché almacenada en búfer en la consola web de OSGi. En `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, establezca la propiedad `cq.dam.image.cache.max.memory` en bytes. Por ejemplo, 1073741824 es 1 GB (1024 x 1024 x 1024 = 1 GB).

En Experience Manager 6.1 SP1, si utiliza un nodo `sling:osgiConfig` para configurar esta propiedad, asegúrese de establecer el tipo de datos en Long. Para obtener más información, consulte [CQBufferedImageCache consume mucha información durante las cargas de recursos](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Almacenes de datos compartidos {#shared-data-stores}

La implementación de un almacén de datos de archivos compartidos o S3 puede ayudar a ahorrar espacio en disco y aumentar el rendimiento de la red en implementaciones a gran escala. Para obtener más información sobre las ventajas y desventajas de utilizar un almacén de datos compartido, consulte [Guía de tamaño de Assets](/help/assets/assets-sizing-guide.md).

### Almacén de datos de S3 {#s-data-store}

La siguiente configuración del almacén de datos de S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ayudó a Adobe a extraer 12,8 TB de objetos binarios grandes (BLOB) de un almacén de datos de archivo existente en un almacén de datos de S3 en un sitio de cliente:

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Optimización de red {#network-optimization}

Adobe recomienda habilitar HTTPS porque muchas empresas tienen servidores de seguridad que detectan el tráfico HTTP, lo que afecta negativamente a las cargas y corrompe los archivos. Para cargas de archivos grandes, asegúrese de que los usuarios tengan conexiones cableadas a la red, ya que la red WiFi se satura rápidamente. Para obtener instrucciones sobre cómo identificar cuellos de botella de red, consulte [Guía de tamaño de Assets](/help/assets/assets-sizing-guide.md). Para evaluar el rendimiento de la red mediante el análisis de la topología de red, vea [Consideraciones de red de Assets](/help/assets/assets-network-considerations.md).

Principalmente, la estrategia de optimización de la red depende de la cantidad de ancho de banda disponible y de la carga de la instancia de [!DNL Experience Manager]. Las opciones de configuración comunes, incluidos los servidores de seguridad o los servidores proxy, pueden ayudar a mejorar el rendimiento de la red. A continuación se indican algunos puntos clave que se deben tener en cuenta:

* Según el tipo de instancia (pequeña, moderada, grande), asegúrese de que dispone de suficiente ancho de banda de red para la instancia de Experience Manager. Una asignación de ancho de banda adecuada es especialmente importante si [!DNL Experience Manager] está alojado en AWS.
* Si la instancia de [!DNL Experience Manager] está alojada en AWS, puede beneficiarse de tener una política de escalado versátil. Actualice la instancia si los usuarios esperan una carga alta. Reduzca el tamaño para una carga moderada/baja.
* HTTPS: la mayoría de los usuarios tienen servidores de seguridad que detectan el tráfico HTTP, lo que puede afectar negativamente a la carga de archivos o incluso dañar los archivos durante la operación de carga.
* Cargas de archivos grandes: Asegúrese de que los usuarios tengan conexiones cableadas a la red (las conexiones WiFi se saturan rápidamente).

## Flujos de trabajo {#workflows}

### Flujos de trabajo transitorios {#transient-workflows}

Siempre que sea posible, establezca el flujo de trabajo [!UICONTROL Recurso de actualización DAM] en Transitorio. La configuración reduce significativamente los costes generales necesarios para procesar flujos de trabajo porque, en este caso, los flujos de trabajo no necesitan pasar por los procesos normales de seguimiento y archivo.

1. Vaya a `/miscadmin` en la implementación de [!DNL Experience Manager] en `https://[aem_server]:[port]/miscadmin`.

1. Expandir **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL dam]**.

1. Abra **[!UICONTROL recurso de actualización DAM]**. En el panel de herramientas flotante, cambie a la ficha **[!UICONTROL Página]** y, a continuación, haga clic en **[!UICONTROL Propiedades de página]**.

1. Seleccione **[!UICONTROL Flujo de trabajo transitorio]** y haga clic en **[!UICONTROL Aceptar]**.

   >[!NOTE]
   >
   >Algunas funciones no admiten flujos de trabajo transitorios. Si la implementación de [!DNL Assets] requiere estas características, no configure flujos de trabajo transitorios.

En los casos en que no se puedan usar flujos de trabajo transitorios, ejecute la depuración del flujo de trabajo con regularidad para eliminar los flujos de trabajo de [!UICONTROL DAM Update Asset] archivados para garantizar que el rendimiento del sistema no se degrade.

Normalmente, ejecuta los flujos de trabajo de depuración de forma semanal. Sin embargo, en situaciones que requieren muchos recursos, como durante la ingesta de recursos a gran escala, puede ejecutarla con mayor frecuencia.

Para configurar la depuración del flujo de trabajo, añada una nueva configuración de depuración del flujo de trabajo de Adobe Granite a través de la consola OSGi. A continuación, configure y programe el flujo de trabajo como parte de la ventana de mantenimiento semanal.

Si la depuración se ejecuta durante demasiado tiempo, se agota el tiempo de espera. Por lo tanto, debe asegurarse de que los trabajos de depuración se completen para evitar situaciones en las que los flujos de trabajo de depuración no se completen debido al alto número de flujos de trabajo.

Por ejemplo, después de ejecutar numerosos flujos de trabajo no transitorios (que crea nodos de instancia de flujo de trabajo), puede ejecutar [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) según sea necesario. Elimina inmediatamente las instancias de flujo de trabajo redundantes y completadas, en lugar de esperar a que se ejecute el planificador de depuración del flujo de trabajo de Adobe Granite.

### Máximo de trabajos paralelos {#maximum-parallel-jobs}

De manera predeterminada, [!DNL Experience Manager] ejecuta un número máximo de trabajos paralelos igual al número de procesadores del servidor. El problema con esta configuración es que durante los períodos de carga pesada, todos los procesadores están ocupados por [!UICONTROL flujos de trabajo de recursos de actualización DAM], lo que ralentiza la capacidad de respuesta de la interfaz de usuario e impide que [!DNL Experience Manager] ejecute otros procesos que salvaguardan el rendimiento y la estabilidad del servidor. Como práctica recomendada, establezca este valor en la mitad de los procesadores disponibles en el servidor realizando los siguientes pasos:

1. El autor de [!DNL Experience Manager], acceda a `https://[aem_server]:[port]/system/console/slingevent`.

1. Haga clic en **[!UICONTROL Editar]** en cada cola de flujo de trabajo que sea relevante para su implementación; por ejemplo, **[!UICONTROL Cola de flujo de trabajo transitorio de Granite]**.

1. Actualice el valor de **[!UICONTROL Máximo de trabajos paralelos]** y haga clic en **[!UICONTROL Guardar]**.

Establecer una cola en la mitad de los procesadores disponibles es una solución viable para empezar. Sin embargo, es posible que tenga que aumentar o disminuir este número para lograr el máximo rendimiento y ajustarlo por entorno. Hay colas independientes para flujos de trabajo transitorios y no transitorios y otros procesos, como flujos de trabajo externos. Si varias colas configuradas al 50% de los procesadores están activas simultáneamente, el sistema puede sobrecargarse rápidamente. Las colas muy utilizadas varían en gran medida entre las implementaciones de los usuarios. Por lo tanto, es posible que tenga que configurarlos cuidadosamente para lograr la máxima eficiencia sin sacrificar la estabilidad del servidor.

### Configuración de recursos de actualización DAM {#dam-update-asset-configuration}

El flujo de trabajo [!UICONTROL DAM Update Asset] contiene un conjunto completo de pasos configurados para tareas, como la generación de PTIFF de Dynamic Media y la integración de [!DNL Adobe InDesign Server]. Sin embargo, es posible que la mayoría de los usuarios no requieran varios de estos pasos. Adobe recomienda crear una copia personalizada del modelo de flujo de trabajo [!UICONTROL Recurso de actualización DAM] y eliminar los pasos innecesarios. En este caso, actualice los iniciadores de [!UICONTROL DAM Update Asset] para que apunten al nuevo modelo.

La ejecución intensiva del flujo de trabajo [!UICONTROL DAM Update Asset] puede aumentar considerablemente el tamaño del almacén de datos de archivos. Los resultados de un experimento realizado por Adobe han mostrado que el tamaño del almacén de datos puede aumentar en aproximadamente 400 GB si se realizan alrededor de 5500 flujos de trabajo en un plazo de 8 horas.

Se trata de un aumento temporal y el almacén de datos vuelve a su tamaño original después de ejecutar la tarea de recolección de elementos no utilizados del almacén de datos.

Normalmente, la tarea de recolección de elementos no utilizados del almacén de datos se ejecuta semanalmente junto con otras tareas de mantenimiento programadas.

Si tiene poco espacio en disco y ejecuta [!UICONTROL DAM Update Asset] flujos de trabajo de forma intensiva, considere la posibilidad de programar la tarea de recolección de elementos no utilizados con más frecuencia.

#### Generación de representación en tiempo de ejecución {#runtime-rendition-generation}

Los clientes utilizan imágenes de diversos tamaños y formatos en su sitio web o para su distribución a socios comerciales. Dado que cada representación aumenta el espacio del recurso en el repositorio, Adobe recomienda utilizar esta función con prudencia. Para reducir la cantidad de recursos necesarios para procesar y almacenar imágenes, puede generar estas imágenes en tiempo de ejecución en lugar de como representaciones durante la ingesta.

Muchos clientes de Sites implementan un servlet de imagen que cambia de tamaño y recorta las imágenes en el momento en que se solicitan, lo que impone una carga adicional a la instancia de publicación. Sin embargo, mientras estas imágenes se puedan almacenar en caché, el desafío se puede mitigar.

Un enfoque alternativo es utilizar la tecnología Dynamic Media para entregar completamente la manipulación de imágenes. Además, puede implementar Brand Portal que no solo se haga cargo de las responsabilidades de generación de representaciones desde la infraestructura de [!DNL Experience Manager], sino también de todo el nivel de publicación.

#### ImageMagick {#imagemagick}

Si personaliza el flujo de trabajo [!UICONTROL DAM Update Asset] para generar representaciones mediante ImageMagick, Adobe recomienda modificar el archivo `policy.xml` en `/etc/ImageMagick/`. De forma predeterminada, ImageMagick utiliza todo el espacio disponible en disco en el volumen del sistema operativo y la memoria disponible. Realice los siguientes cambios de configuración en la sección `policymap` de `policy.xml` para limitar estos recursos.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

Además, establezca la ruta de la carpeta temporal de ImageMagick en el archivo `configure.xml` (o estableciendo la variable de entorno `MAGICK_TEMPORARY_PATH`) en una partición de disco que tenga espacio suficiente e IOPS.

>[!CAUTION]
>
>Una configuración incorrecta puede hacer que el servidor sea inestable si ImageMagick utiliza todo el espacio en disco disponible. Los cambios de directiva necesarios para procesar archivos grandes mediante ImageMagick pueden afectar al rendimiento de [!DNL Experience Manager]. Para obtener más información, consulte [instalar y configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Los archivos de ImageMagick `policy.xml` y `configure.xml` están disponibles en `/usr/lib64/ImageMagick-&#42;/config/` en lugar de `/etc/ImageMagick/`. Consulte la [documentación de ImageMagick](https://www.imagemagick.org/script/resources.php) para ver la ubicación de los archivos de configuración.

Si utiliza [!DNL Experience Manager] en Adobe Managed Services (AMS), póngase en contacto con Asistencia al cliente de Adobe si planea procesar muchos archivos PSD o PSB grandes. Póngase en contacto con el representante de Asistencia al cliente de Adobe para implementar estas prácticas recomendadas en su implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] no puede procesar archivos PSB de muy alta resolución que tengan más de 30000 x 23000 píxeles.

### reescritura de XMP {#xmp-writeback}

La reescritura de XMP actualiza el recurso original cada vez que se modifican los metadatos en [!DNL Experience Manager], lo que da como resultado lo siguiente:

* Se modifica el recurso en sí
* Se crea una versión del recurso
* [!UICONTROL Recurso de actualización DAM] se ejecuta con el recurso

Los resultados enumerados consumen recursos considerables. Por lo tanto, Adobe recomienda deshabilitar la reescritura de XMP si no es necesaria. Para obtener más información, consulte [reescritura de XMP](/help/assets/xmp-writeback.md).

La importación de una gran cantidad de metadatos puede dar como resultado una actividad de reescritura de XMP que consuma muchos recursos si se marca el indicador ejecutar flujos de trabajo. Planifique una importación de este tipo durante el uso del servidor lean para que el rendimiento de otros usuarios no se vea afectado.

## Replicación {#replication}

Al replicar recursos en un gran número de instancias de publicación, por ejemplo, en una implementación de Sites, Adobe recomienda utilizar la replicación en cadena. En este caso, la instancia de autor se replica en una sola instancia de publicación, que a su vez se replica en las demás instancias de publicación, liberando la instancia de autor.

### Configurar replicación de cadena {#configure-chain-replication}

1. Elija la instancia de publicación que desea utilizar para encadenar las replicaciones
1. En esa instancia de publicación, agregue agentes de replicación que apunten a las demás instancias de publicación
1. En cada uno de estos agentes de replicación, habilite &quot;Recepción&quot; en la pestaña &quot;Déclencheur&quot;

>[!NOTE]
>
>Adobe no recomienda la activación automática de recursos. Sin embargo, si es necesario, Adobe recomienda hacerlo como el paso final de un flujo de trabajo, normalmente Recurso de actualización DAM.

## Buscar índices {#search-indexes}

Instale [los Service Packs más recientes](/help/release-notes/release-notes.md) y las revisiones relacionadas con el rendimiento, ya que suelen incluir actualizaciones de los índices del sistema. Consulte [consejos para la optimización del rendimiento](https://experienceleague.adobe.com/docs/experience-manager-65-lts/assets/administer/performance-tuning-guidelines.html?lang=en) para ver algunas optimizaciones del índice.

Cree índices personalizados para consultas que ejecute con frecuencia. Para obtener más información, consulte [metodología para analizar consultas lentas](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) y [crear índices personalizados](/help/sites-deploying/queries-and-indexing.md). Para obtener información adicional sobre las prácticas recomendadas de consultas e índices, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configuraciones de índice de Lucene {#lucene-index-configurations}

Se pueden realizar algunas optimizaciones en las configuraciones del índice de Oak que pueden ayudar a mejorar el rendimiento de [!DNL Experience Manager Assets]. Actualice las configuraciones de índice para mejorar el tiempo de reindexación:

1. Abra CRXDe `/crx/de/index.jsp` e inicie sesión como un usuario administrativo.
1. Vaya a `/oak:index/lucene`.
1. Agregue una propiedad `String[]` `excludedPaths` con los valores `/var`, `/etc/workflow/instances` y `/etc/replication`.
1. Vaya a `/oak:index/damAssetLucene`. Agregar una propiedad `String[]` `includedPaths` con el valor `/content/dam`. Guardar cambios.

Si los usuarios no necesitan realizar búsquedas de texto completo de recursos, por ejemplo, buscando texto en documentos de PDF, desactívelo. Se mejora el rendimiento del índice al deshabilitar la indexación de texto completo. Para deshabilitar la extracción de texto de [!DNL Apache Lucene], siga estos pasos:

1. En la interfaz [!DNL Experience Manager], obtenga acceso al [!UICONTROL Administrador de paquetes].
1. Cargue e instale el paquete disponible en [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Total de estimación {#guess-total}

Cuando cree consultas que generen grandes conjuntos de resultados, utilice el parámetro `guessTotal` para evitar el uso excesivo de la memoria al ejecutarlas.

## Problemas conocidos {#known-issues}

### Archivos grandes {#large-files}

Hay dos problemas conocidos importantes relacionados con archivos grandes en [!DNL Experience Manager]. Cuando los archivos alcanzan tamaños superiores a 2 GB, la sincronización en espera en frío puede encontrarse con una falta de memoria. En algunos casos, evita que se ejecute la sincronización en espera. En otros casos, hace que la instancia principal se bloquee. Este escenario se aplica a cualquier archivo de [!DNL Experience Manager] que tenga más de 2 GB, incluidos los paquetes de contenido.

Del mismo modo, cuando los archivos alcanzan los 2 GB de tamaño mientras se utiliza un almacén de datos S3 compartido, puede tardar algún tiempo en persistir completamente desde la caché al sistema de archivos. Como resultado, cuando se utiliza la replicación sin binarios, es posible que los datos binarios no se hayan mantenido antes de que finalice la replicación. Esta situación puede dar lugar a problemas, especialmente si la disponibilidad de datos es importante.

## Pruebas de rendimiento {#performance-testing}

Para cada implementación de [!DNL Experience Manager], establezca un régimen de pruebas de rendimiento que pueda identificar y resolver cuellos de botella rápidamente. Estas son algunas áreas clave en las que centrarse.

### Pruebas de red {#network-testing}

Para todos los problemas de rendimiento de red del cliente, realice las siguientes tareas:

* Pruebe el rendimiento de la red desde la red del cliente
* Pruebe el rendimiento de la red desde la red de Adobe. Para los clientes de AMS, colabore con su CSE para probar desde la red de Adobe.
* Prueba del rendimiento de la red desde otro punto de acceso
* Mediante el uso de una herramienta de referencia de red
* Comprobación con el despachante

### Pruebas de implementación de [!DNL Experience Manager] {#aem-deployment-testing}

Para minimizar la latencia y lograr un alto rendimiento mediante la utilización eficiente de CPU y el uso compartido de la carga, supervise regularmente el rendimiento de su implementación de [!DNL Experience Manager]. En particular:

* Ejecute pruebas de carga en la implementación [!DNL Experience Manager].
* Monitorice el rendimiento de carga y la capacidad de respuesta de IU.

## [!DNL Experience Manager Assets] lista de comprobación de rendimiento e impacto de las tareas de administración de recursos {#checklist}

* Habilite HTTPS para evitar cualquier detector de tráfico HTTP corporativo.
* Utilice una conexión con cable para cargar recursos pesados.
* Implementación en Java 8.
* Establezca los parámetros óptimos de JVM.
* Configurar un almacén de datos del sistema de archivos o un almacén de datos de S3.
* Deshabilite la generación de subrecursos. Si está activada, el flujo de trabajo de AEM crea un recurso independiente para cada página en un recurso de varias páginas. Cada una de estas páginas es un recurso individual que consume espacio en disco adicional, requiere versiones y un procesamiento de flujo de trabajo adicional. Si no necesita páginas separadas, deshabilite la generación de subrecursos y las actividades de extracción de páginas.
* Habilitar flujos de trabajo transitorios.
* Ajuste las colas del flujo de trabajo de Granite para limitar los trabajos simultáneos.
* Configure [!DNL ImageMagick] para limitar el consumo de recursos.
* Quite los pasos innecesarios del flujo de trabajo [!UICONTROL Recurso de actualización DAM].
* Configure el flujo de trabajo y la depuración de versiones.
* Optimice los índices con los últimos Service Packs y revisiones. Consulte con Asistencia al cliente de Adobe cualquier optimización de índice adicional que pueda estar disponible.
* Utilice guessTotal para optimizar el rendimiento de la consulta.
* Si configura [!DNL Experience Manager] para que detecte los tipos de archivo a partir del contenido de los archivos (habilitando el **[!UICONTROL Servicio Day CQ DAM Mime Type]** en la **[!UICONTROL consola web de AEM]**), cargue muchos archivos de forma masiva durante las horas de menor afluencia, ya que consume muchos recursos.
