---
title: Carpeta inspeccionada en AEM Forms
description: Un administrador puede colocar una carpeta en inspección e iniciar una operación de flujo de trabajo, servicio o script cuando se coloca un archivo en la carpeta que está viendo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '7164'
ht-degree: 95%

---

# Carpeta inspeccionada en AEM Forms{#watched-folder-in-aem-forms}

Un administrador puede configurar una carpeta de red, conocida como carpeta inspeccionada, de modo que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta inspeccionada, se inicie un flujo de trabajo preconfigurado, un servicio o una operación de script para procesar el archivo agregado. Una vez que el servicio realiza la operación especificada, guarda el archivo de resultados en una carpeta de salida especificada. Para obtener más información sobre el flujo de trabajo, el servicio y el script, consulte [Varios métodos para procesar archivos](#variousmethodsforprocessingfiles).

## Crear una carpeta inspeccionada {#create-a-watched-folder}

Puede utilizar uno de los siguientes métodos para crear una carpeta inspeccionada en el sistema de archivos:

* Al configurar las propiedades de un nodo de configuración de carpeta inspeccionada, escriba la ruta completa del directorio principal en la propiedad folderPath y agregue el nombre de la carpeta inspeccionada que se creará, como se muestra en el siguiente ejemplo: `C:/MyPDFs/MyWatchedFolder`
La carpeta `MyWatchedFolder`no existe; AEM Forms intenta crear la carpeta en la ruta especificada.

* Cree una carpeta en el sistema de archivos antes de configurar un punto final de carpeta inspeccionada y, a continuación, proporcione la ruta completa en la propiedad folderPath. Para obtener información detallada sobre la propiedad folderPath, consulte [Propiedades de la carpeta inspeccionada](#watchedfolderproperties).

>[!NOTE]
>
>En un entorno agrupado, la carpeta utilizada como carpeta inspeccionada debe ser accesible, modificable y compartida en el sistema de archivos o red. Cada instancia de servidor de aplicaciones del grupo debe tener acceso a la misma carpeta compartida. En Windows, cree una unidad de red asignada en todos los servidores y especifique la ruta de la unidad de red asignada en la propiedad folderPath.

## Crear nodo de configuración de carpeta inspeccionada {#create-watched-folder-configuration-node}

Para configurar una carpeta inspeccionada, cree un nodo de configuración de carpeta inspeccionada. Realice los siguientes pasos para crear el nodo de configuración:

1. Inicie sesión en CRX-DE lite como administrador y vaya a la carpeta /etc/fd/watchfolder/config.

1. Cree un nodo de tipo `nt:unstructured`. Por ejemplo, watchedfolder

   >[!NOTE]
   >
   >El nombre del nodo Carpeta inspeccionada no puede incluir espacios ni caracteres especiales.

1. Agregue las siguientes propiedades al nodo:

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   Para obtener una lista completa de las propiedades compatibles, consulte [Propiedades de la carpeta inspeccionada](#watchedfolderproperties).

1. Haga clic en **Guardar todo**. Una vez creado el nodo y guardadas las propiedades. Las carpetas `input`, `result`, `failure`, `preserve` y `stage` se crean en la ruta especificada en la propiedad `folderPath`.

   El trabajo de análisis comienza a analizar la carpeta inspeccionada a un intervalo de tiempo definido.

## Propiedades de la carpeta inspeccionada {#watchedfolderproperties}

Puede configurar las siguientes propiedades para una carpeta inspeccionada.

* **folderPath (String)**: Ruta de la carpeta que se va a analizar en intervalos de tiempo definidos. Para un entorno agrupado, la carpeta debe estar en una ubicación compartida con todos los servidores que tengan acceso completo al servidor. Es una propiedad obligatoria.
* **inputProcessorType (String)**: Tipo de proceso que se va a iniciar. Puede especificar el flujo de trabajo, el script o el servicio. Es una propiedad obligatoria.
* **inputProcessorId (String)**: El comportamiento de la propiedad inputProcessorId se basa en el valor especificado para la propiedad inputProcessorType. Es una propiedad obligatoria. La siguiente lista detalla todos los valores posibles de la propiedad inputProcessorType y los requisitos correspondientes para la propiedad inputProcessorType:

   * Para el flujo de trabajo, especifique el modelo de flujo de trabajo que se va a ejecutar. Por ejemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * Para el script, especifique la ruta JCR del script que se va a ejecutar. Por ejemplo, /etc/fd/watchfolder/test/testScript.ecma
   * Para el servicio, especifique el filtro utilizado para localizar un servicio OSGi. El servicio está registrado como una implementación de la interfaz com.adobe.aemfd.watchfolder.service.api.ContentProcessor.

* **runModes (String)**: Lista separada por comas de los modos de ejecución permitidos para la ejecución del flujo de trabajo. Algunos ejemplos son:

   * autor

   * publicación

   * autor, publicación

   * publicación, autor

>[!NOTE]
>
>Si el servidor que aloja la carpeta inspeccionada no tiene ninguno de los modos de ejecución especificados, entonces la carpeta inspeccionada siempre se activa independientemente de los modos de ejecución del servidor.

* **outputFilePattern (String)**: Patrón del archivo de salida. Puede especificar una carpeta o un patrón de archivo. Si se especifica un patrón de carpeta, los archivos de salida tienen nombres como se describe en los flujos de trabajo. Si se especifica un patrón de archivo, los archivos de salida tienen nombres como se describe en el patrón de archivo. [El patrón de archivos y carpetas](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) también puede especificar una estructura de directorio para los archivos de salida. Es una propiedad obligatoria.

* **stageFileExpirationDuration (Long, default -1)**: El número de segundos de espera antes de un archivo/carpeta de entrada que ya se ha seleccionado para el procesamiento debe tratarse como si se hubiera agotado el tiempo de espera y marcado como un error. Este mecanismo de caducidad solo se activa cuando el valor de esta propiedad es un número positivo.

>[!NOTE]
>
>Incluso cuando una entrada está marcada como con el tiempo de espera agotado con este mecanismo, puede que se esté procesando en segundo plano, pero tardando más tiempo del esperado. Si el contenido de entrada se consumió antes de que se iniciara el mecanismo de tiempo de espera, el procesamiento puede incluso continuar hasta la finalización más tarde y el resultado se volcará a la carpeta de resultados. Si el contenido no se consumió antes del tiempo de espera, es muy probable que el procesamiento genere un error más adelante al intentar consumir el contenido, y este error también se registrará en la carpeta de errores para la misma entrada. Por otro lado, si el procesamiento de la entrada nunca se activa debido a un error intermitente del trabajo/flujo de trabajo (que es el escenario que el mecanismo de caducidad pretende abordar), entonces no se producirá ninguna de estas dos situaciones. Por lo tanto, para cualquier entrada de la carpeta de errores que se haya marcado como errónea debido al tiempo de espera (busque los mensajes del formulario “Archivo no procesado después de una cantidad de tiempo significativa, ¡marcando como error!;” en el registro de errores), se recomienda analizar la carpeta de resultados (y también la carpeta de errores en sí para obtener otra entrada para la misma entrada) para comprobar si se ha producido alguna de las eventualidades descritas anteriormente.

* **deleteExpiredStageFileOnlyWhenThrottled (Boolean, default true):** Indica si el mecanismo de caducidad debe activarse solo cuando se restringe la carpeta del reloj. El mecanismo es más relevante para las carpetas de inspección restringidas, ya que un pequeño número de archivos que permanecen en estado sin procesar (debido a errores intermitentes en el trabajo/flujo de trabajo) pueden bloquear el procesamiento de todo el lote cuando se habilita la restricción. Si esta propiedad se mantiene como True (predeterminada), el mecanismo de caducidad no se activa para las carpetas de inspección que no estén restringidas. Si la propiedad se mantiene como False, el mecanismo siempre se activará siempre que la propiedad stageFileExpirationDuration sea un número positivo.

* **pollInterval (Long)**: Intervalo en segundos para analizar la carpeta inspeccionada para obtener información. A menos que la configuración Restringir esté habilitada, el intervalo de encuesta debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría sobrecargarse. El valor predeterminado es 5. Consulte la descripción del tamaño del lote para obtener más información. El valor del intervalo de encuesta debe ser mayor o igual a uno.
* **excludeFilePattern (String)**: Lista delimitada por punto y coma (;) de patrones que utiliza una carpeta inspeccionada para determinar qué archivos y carpetas analizar y recoger. Ningún archivo o carpeta con este patrón se analiza para su procesamiento. Esta configuración es útil cuando la entrada es una carpeta con varios archivos. El contenido de la carpeta se puede copiar en una carpeta con un nombre que recoge la carpeta inspeccionada. Esto evita que la carpeta inspeccionada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada. El valor predeterminado es nulo.
Puede usar [patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) para excluir:

   * Archivos con extensiones de nombre de archivo específicas; por ejemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Archivos con nombres específicos; por ejemplo, data&#42; excluiría archivos y carpetas llamados data1, data2, etc.
   * Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

      * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: Lista delimitada por punto y coma (;) de patrones que utiliza una carpeta inspeccionada para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si se introduce IncludeFilePattern&#42;, se recogen todos los archivos y carpetas que coinciden con la entrada&#42;. Esto incluye archivos y carpetas llamados input1, input2, etc. El valor predeterminado es &#42; e indica todos los archivos y carpetas. Puede utilizar patrones de archivo para incluir:

   * Archivos con extensiones de nombre de archivo específicas; por ejemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Archivos con nombres específicos; por ejemplo, data.&#42; incluiría archivos y carpetas llamados data1, data2, etc.

* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Acerca de los patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**: Tiempo, en milisegundos, que debe esperarse antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3 600 000 milisegundos (una hora) y el archivo se creó hace un minuto, el archivo se recopilará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0. Esta configuración es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y el archivo tarda diez minutos en descargarse, establezca el tiempo de espera en 10&#42;60 &#42;1000 milisegundos. Esto evita que la carpeta inspeccionada analice el archivo si no tiene diez minutos de antigüedad.
* **purgeDuration (Long)**: Los archivos y carpetas de la carpeta de resultados se depuran cuando son anteriores a este valor. Este valor se mide en días. Esta configuración es útil para garantizar que la carpeta de resultados no se llene. El valor de -1 días indica que nunca se eliminará la carpeta de resultados. El valor predeterminado es -1.
* **resultFolderName (String)**: La carpeta en la que se almacenan los resultados guardados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. Este valor puede ser una ruta absoluta o relativa con los siguientes patrones de archivo:

   * %F = prefijo del nombre de archivo
   * %E = extensión del nombre de archivo
   * %Y = año (completo)
   * %y = año (dos últimos dígitos)
   * %M = mes
   * %D = día del mes
   * %d = día del año
   * %H = hora (reloj de 24 horas)
   * %h = hora (reloj de 12 horas)
   * %m = minuto
   * %s = segundo
   * %l = milisegundo
   * %R = número aleatorio (entre 0 y 9)
   * %P = ID del proceso o trabajo

  Por ejemplo, si son las 20:00 del 17 de julio de 2009 y especifica C:/Test/WF0/failure/%Y/%M/%D/%H/, la carpeta de resultados es C:/Test/WF0/failure/2009/07/17/20

  Si la ruta de acceso no es absoluta sino relativa, la carpeta se crea dentro de la carpeta inspeccionada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta Resultado dentro de la carpeta inspeccionada. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Cuanto menor sea el tamaño de las carpetas de resultados, mejor será el rendimiento de la carpeta inspeccionada. Por ejemplo, si la carga estimada para la carpeta inspeccionada es de 1000 archivos cada hora, pruebe un patrón como result/%Y%M%D%H para que se cree una nueva subcarpeta cada hora. Si la carga es menor (por ejemplo, 1000 archivos por día), puede utilizar un patrón como result/%Y%M%D.

* **failureFolderName (String)**: Carpeta donde se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta inspeccionada. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. El valor predeterminado es failure/%Y/%M/%D/.
* **preserveFolderName (String):** Ubicación en la que se almacenan los archivos después de procesarlos correctamente. La ruta puede ser absoluta, relativa o nula. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados. El valor predeterminado es preserve/%Y/%M/%D/.
* **batchSize (Long)**: Número de archivos o carpetas que se van a recoger por análisis. Utilizar para evitar sobrecargas en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

  La configuración Intervalo de encuesta y Tamaño de lote determina cuántos archivos recoge la carpeta inspeccionada en cada análisis. La carpeta inspeccionada utiliza un grupo de hilos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de análisis es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se pierden con frecuencia en la carpeta vigilada, deberá reducir el intervalo de análisis. Si los archivos se pierden con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

  Si se pierde un gran volumen de archivos, aumente el tamaño del lote. Por ejemplo, si el servicio iniciado por el punto final de la carpeta inspeccionada puede procesar 700 archivos por minuto y los usuarios pueden soltar archivos en la carpeta de entrada a la misma velocidad, al establecer el tamaño del lote en 350 y el intervalo de encuesta en 30 segundos, ayuda al rendimiento de la carpeta inspeccionada sin incurrir en el coste de analizar la carpeta inspeccionada con demasiada frecuencia.

  Cuando se sueltan los archivos en la carpeta inspeccionada, se enumeran los archivos en la entrada, lo que puede reducir el rendimiento si la exploración se realiza cada segundo. El aumento del intervalo de análisis puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y el intervalo de encuesta en consecuencia. Por ejemplo, si se sueltan 10 archivos cada segundo, intente establecer el intervalo de encuesta en 1 segundo y el tamaño del lote en 10

* **throttleOn (Boolean)**: Cuando se selecciona esta opción, limita el número de trabajos de carpeta inspeccionada que procesa AEM Forms en un momento determinado. El número máximo de trabajos viene determinado por el valor Tamaño del lote. El valor predeterminado es True. (Consulte [Acerca de la restricción](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (Boolean)**: Cuando se establece en True, los archivos de la carpeta de resultados y de la carpeta de conservación se sobrescriben. Cuando se establece en False, se utilizan archivos y carpetas con un sufijo de índice numérico para el nombre. El valor predeterminado es False.
* **preserveOnFailure (Boolean)**: Conservar archivos de entrada si no se puede ejecutar la operación en un servicio. El valor predeterminado es True.
* **inputFilePattern (String)**: Especifica el patrón de los archivos de entrada para una carpeta inspeccionada. Crea una lista de permitidos de los archivos.
* **asynch (Boolean)**: Identifica el tipo de invocación como asincrónico o sincrónico. El valor predeterminado es True (asincrónico). El procesamiento de archivos es una tarea que consume recursos. Mantenga el valor del indicador asíncrono en True para evitar que se bloquee el hilo principal del trabajo de análisis. En un entorno agrupado, es fundamental mantener el indicador en True para permitir el equilibrio de carga para los archivos que se procesan en los servidores disponibles. Si el indicador es False, el trabajo de análisis intenta realizar secuencialmente el procesamiento de cada archivo/carpeta de nivel superior dentro de su propio hilo. No establezca el indicador en False sin un motivo específico, como el procesamiento basado en flujos de trabajo en una configuración de un solo servidor.

>[!NOTE]
>
>Por diseño, los flujos de trabajo son asincrónicos. Incluso si establece el valor en False, los flujos de trabajo se inician en modo asincrónico.

* **enabled (Boolean)**: Desactiva y activa el análisis de una carpeta inspeccionada. Configúrelo en True para comenzar a analizar la carpeta inspeccionada. El valor predeterminado es True.
* **payloadMapperFilter:** Cuando una carpeta se configura como carpeta inspeccionada, se crea una estructura de carpetas dentro de la carpeta inspeccionada. La estructura tiene carpetas para proporcionar entradas, recibir salidas (resultados), guardar datos para errores, conservar datos para procesos de larga duración y guardar datos para varias fases. La estructura de carpetas de una carpeta inspeccionada puede servir como carga útil de flujos de trabajo centrados en Forms. Un asignador de carga útil permite definir la estructura de una carga útil que utiliza una carpeta inspeccionada para la entrada, la salida y el procesamiento. Por ejemplo, si utiliza el asignador predeterminado, asigna el contenido de la carpeta inspeccionada con la carpeta [payload]\input y [payload]\output. Hay dos implementaciones de asignador de carga útil listas para usar. Si no tiene [una implementación personalizada](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilice una predeterminada:

   * **Asignador predeterminado:** utilice el asignador de cargas útiles predeterminado para mantener el contenido de entrada y salida de las carpetas vigiladas en carpetas de entrada y salida independientes en la carga útil. Además, en la ruta de carga útil de un flujo de trabajo, utilice las rutas [payload]/input/ y [payload]/output para recuperar y guardar contenido.

   * **Asignador de carga útil basado en archivos simples:** utilice el asignador de cargas útiles basado en archivos simples para mantener el contenido de entrada y salida directamente en la carpeta de carga útil. No crea ninguna jerarquía adicional, como el asignador predeterminado.

### Parámetros de configuración personalizados {#custom-configuration-parameters}

Junto con las propiedades de configuración de la carpeta inspeccionada que se enumeran anteriormente, también puede especificar parámetros de configuración personalizados. Los parámetros personalizados se pasan al código de procesamiento de archivos. Permite que el código cambie su comportamiento en función del valor del parámetro. Para especificar un parámetro:

1. Inicie sesión en CRXDE-Lite y vaya al nodo de configuración de la carpeta inspeccionada.
1. Agregue un parámetro de propiedad&lt;property_name> al nodo de configuración de la carpeta inspeccionada. El tipo de propiedad solo puede ser Boolean, Date, Decimal, Double, Long y String. Puede especificar propiedades de uno o varios valores.

>[!NOTE]
>
>Si el tipo de datos de la propiedad es Double, especifique un punto decimal en el valor de dichas propiedades. Para todas las propiedades, donde el tipo de datos es Double y no se especifica ningún punto decimal en el valor, el tipo se convierte a Long.

Estas propiedades se pasan como un mapa inmutable de tipo Map&lt;String, Object> al código de procesamiento. El código de procesamiento puede ser un ECMAScript, un flujo de trabajo o un servicio. Los valores proporcionados para las propiedades están disponibles como pares clave-valor en el mapa. Clave es el nombre de la propiedad y el valor es el valor de la propiedad. Para obtener más información acerca de los parámetros de configuración personalizados, consulte la siguiente imagen:

![Un nodo de configuración de carpeta de inspección de muestra con propiedades obligatorias, algunas propiedades opcionales y algunos parámetros de configuración](assets/custom-configuration-parameters.png)

Un nodo de configuración de carpeta de inspección de muestra con propiedades obligatorias, algunas propiedades opcionales y algunos parámetros de configuración.

#### Variables mutables para flujos de trabajo {#mutable-variables-for-workflows}

Puede crear variables mutables para los métodos de procesamiento de archivos basados en flujos de trabajo. Estas variables sirven como contenedores para los datos que fluyen entre los pasos de un flujo de trabajo. Para crear estas variables:

1. Inicie sesión en CRXDE-Lite y vaya al nodo de configuración de la carpeta inspeccionada.

1. Agregue una propiedad workflow.var.&lt;variable_name> al nodo de configuración de la carpeta inspeccionada.

   El tipo de propiedad solo puede ser Boolean, Date, Decimal, Double, Long y String. También se admiten propiedades de varios valores. Para propiedades de varios valores, el valor disponible para el paso de flujo de trabajo es una matriz de tipo especificado.

   >[!NOTE]
   >
   >Si el tipo de datos de la propiedad es Double, especifique un punto decimal en el valor de dichas propiedades. Para todas las propiedades, donde el tipo de datos es Double y no se especifica ningún punto decimal en el valor, el tipo se convierte a Long.

>[!NOTE]
>
>La especificación JCR exige un valor predeterminado para las propiedades. Los valores predeterminados están disponibles para los pasos de un flujo de trabajo para su procesamiento. Por lo tanto, especifique los valores predeterminados adecuados.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Varios métodos para procesar archivos {#variousmethodsforprocessingfiles}

Puede iniciar un flujo de trabajo, servicio o script para procesar los documentos colocados en una carpeta de inspección.

### Usar un servicio para procesar archivos de una carpeta inspeccionada   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Un servicio es una implementación personalizada de la interfaz `com.adobe.aemfd.watchfolder.service.api.ContentProcessor`. Está registrado con OSGi junto con algunas propiedades personalizadas. Las propiedades personalizadas de la implementación lo hacen único y ayudan a identificar la implementación.

#### Implementación personalizada de la interfaz ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

La implementación personalizada acepta un contexto de procesamiento (un objeto de tipo com.adobe.aemfd.watchfolder.service.api.ProcessorContext), lee documentos de entrada y parámetros de configuración del contexto, procesa las entradas y agrega el resultado de nuevo al
contexto. ProcessorContext tiene las siguientes API:

* **getWatchFolderId**: Devuelve el ID de la carpeta inspeccionada.
* **getInputMap**: Devuelve un mapa del tipo Map. Las claves del mapa son el nombre del archivo de entrada y un objeto de documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* **getConfigParameters**: Devuelve un mapa inmutable de tipo Map. El mapa contiene
los parámetros de configuración de una carpeta inspeccionada.

* **setResult**: La implementación ContentProcessor
utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida al API setResult. La API puede elegir utilizar o ignorar el archivo proporcionado según el patrón de carpeta/archivo de salida especificado. Si se especifica un patrón de carpeta, los archivos de salida tienen nombres como se describe en los flujos de trabajo. Si se especifica un patrón de archivo, los archivos de salida tienen nombres como se describe en el patrón de archivo.

Por ejemplo, el siguiente código es una implementación personalizada de la interfaz ContentProcessor con una propiedad personalizada foo=bar.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

Al [configurar una carpeta inspeccionada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), si especifica la propiedad inputProcessorId como (foo=bar) y la propiedad inputProcessorType como Servicio, se utilizará el servicio mencionado anteriormente (implementación personalizada) para procesar los archivos de entrada de la carpeta inspeccionada.

El siguiente ejemplo también es una implementación personalizada de la interfaz ContentProcessor. En el ejemplo, el servicio acepta archivos de entrada, los copia en una ubicación temporal y devuelve un objeto de documento con el contenido del archivo. El contenido del objeto de documento se guarda en la carpeta de resultados. La ruta física de la carpeta de resultados se configura en el [nodo de configuración de la carpeta inspeccionada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### Usar scripts para procesar archivos de una carpeta inspeccionada {#using-scripts-to-process-files-of-a-watched-folder}

Los scripts son el código personalizado de queja de ECMAScript que se escribe para procesar los documentos colocados en la carpeta inspeccionada. Un script se representa como un nodo JCR. Aparte de las variables estándar ECMAScript (log, sling y más), el script tiene una variable processorContext. La variable es del tipo ProcessorContext. ProcessorContext tiene las siguientes API:

* **getWatchFolderId**: Devuelve el ID de la carpeta inspeccionada.
* **getInputMap**: Devuelve un mapa del tipo Map. Las claves del mapa son el nombre del archivo de entrada y un objeto de documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* **getConfigParameters**: Devuelve un mapa inmutable de tipo Map. El mapa contiene los parámetros de configuración de una carpeta inspeccionada.
* **setResult**: La implementación ContentProcessor utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida al API setResult. La API puede elegir utilizar o ignorar el archivo proporcionado según el patrón de carpeta/archivo de salida especificado. Si se especifica un patrón de carpeta, los archivos de salida tienen nombres como se describe en los flujos de trabajo. Si se especifica un patrón de archivo, los archivos de salida tienen nombres como se describe en el patrón de archivo.

El siguiente código es un ejemplo de ECMAScript. Acepta archivos de entrada, los copia en una ubicación temporal y devuelve un objeto de documento con el contenido del archivo. El contenido del objeto de documento se guarda en la carpeta de resultados. La ruta física de la carpeta de resultados se configura en el [nodo de configuración de la carpeta inspeccionada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>La carpeta de salida y el prefijo del nombre de archivo se deciden según los parámetros de configuración de la carpeta inspeccionada.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Ubicación de los scripts y consideraciones de seguridad {#location-of-scripts-and-security-considerations}

De forma predeterminada, se proporciona una carpeta contenedora (/etc/fd/watchfolder/scripts) donde los clientes pueden colocar sus scripts y el usuario de servicio predeterminado que usa el marco de carpetas de inspección tiene los permisos necesarios para leer scripts desde esta ubicación.

Si planea colocar los scripts en una ubicación personalizada, es probable que el usuario de servicio predeterminado no tenga permisos de lectura sobre la ubicación personalizada. Para este escenario, realice los siguientes pasos para proporcionar los permisos necesarios a la ubicación personalizada:

1. Cree un usuario del sistema mediante programación o a través de la consola https://&#39;[server]:[port]&#39;/crx/explorer. También puede utilizar un usuario del sistema existente. Es importante trabajar con los usuarios del sistema aquí en lugar de con los usuarios normales.
1. Proporcione permisos de lectura al usuario del sistema recién creado o existente en la ubicación personalizada donde se almacenan los scripts. Puede tener varias ubicaciones personalizadas. Proporcione al menos permisos de lectura a todas las ubicaciones personalizadas.
1. En la consola de configuración de Felix (/system/console/configMgr), busque la asignación de usuario de servicio para las carpetas de inspección. Esta asignación es similar a “Mapping: adobe-aemds-core-watch-folder=...”.
1. Haga clic en la asignación. Para la entrada “adobe-aemds-core-watch-folder:scripts=fd-service”, cambie fd-service por el ID del usuario del sistema personalizado. Haga clic en Guardar.

Ahora, puede utilizar la ubicación personalizada configurada para guardar los scripts.

### Usar un flujo de trabajo para procesar archivos de una carpeta inspeccionada {#using-a-workflow-to-process-files-of-a-watched-folder}

Los flujos de trabajo permiten automatizar las actividades de Experience Manager. Los flujos de trabajo constan de una serie de pasos que se ejecutan en un orden específico. Cada paso realiza una actividad distinta, como activar una página o enviar un mensaje de correo electrónico. Los flujos de trabajo pueden interactuar con los recursos del repositorio, las cuentas de usuario y los servicios de Experience Manager. Por lo tanto, los flujos de trabajo pueden coordinarse de forma complicada.

* Antes de crear un flujo de trabajo, tenga en cuenta los siguientes puntos:
* El resultado de un paso debe estar disponible para todos los pasos siguientes.
Los pasos deben poder actualizar (o incluso eliminar) los resultados existentes generados por los pasos anteriores.
* Las variables mutables se utilizan para el flujo de datos dinámicos personalizados entre los pasos.

Realice los siguientes pasos para procesar archivos mediante flujos de trabajo:

1. Cree una implementación de la interfaz `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`. Es similar a la implementación creada para un Servicio.

   >[!NOTE]
   >
   >Puede crear la implementación completa en su totalidad en ECMAScript.

1. En un paso del flujo de trabajo, busque el servicio OSGi de tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService y llame al método execute() del servicio con los siguientes argumentos.

   * Su implementación personalizada de la interfaz WorkflowContextProcessor
   * workItem
   * workflowSession
   * metadata

Si utiliza el lenguaje de programación Java para implementar el flujo de trabajo, el motor de flujos de trabajo de AEM proporciona valor para las variables workItem, workflowSession y metadata. Estas variables se pasan como argumentos al método execute() de su implementación personalizada de WorkflowProcess.

Si utiliza ECMAScript para implementar el flujo de trabajo, el motor de flujos de trabajo de AEM proporciona un valor para las variables graniteWorkItem, graniteWorkflowSession y metadata. Estas variables pasan como argumentos al método WorkflowContextService.execute().

El argumento processWorkflowContext() es un objeto de tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. La interfaz WorkflowContext tiene las siguientes API para facilitar las consideraciones específicas del flujo de trabajo mencionadas anteriormente:

* getWorkItem: Devuelve el valor de la variable WorkItem. Las variables pasan al método WorkflowContextService.execute().
* getWorkflowSession: Devuelve el valor de la variable WorkflowSession. Las variables pasan al método WorkflowContextService.execute().
* getMetadata: Devuelve el valor de la variable Metadata. Las variables pasan al método WorkflowContextService.execute().
* getCommittedVariables: Devuelve un mapa de objetos de solo lectura que representa las variables establecidas por pasos anteriores. Si una variable no se modifica en ninguno de los pasos anteriores, se devuelve el valor predeterminado especificado durante la configuración de la carpeta inspeccionada.
* getCommittedResults: Devuelve un mapa de documento de solo lectura. El mapa representa los archivos de salida generados por los pasos anteriores.
* setVariable: La implementación WorkflowContextProcessor utiliza la variable para manipular las variables que representan los datos dinámicos personalizados que fluyen entre los pasos. El nombre y el tipo de las variables son idénticos al nombre de las variables especificadas durante la [configuración de la carpeta inspeccionada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). Para cambiar el valor de una variable, llame al API setVariable con un valor que no sea nulo. Para quitar una variable, llame a setVariable() con un valor nulo.

Las siguientes API de ProcessorContext también están disponibles:

* getWatchFolderId: Devuelve el ID de la carpeta inspeccionada.
* getInputMap: Devuelve un mapa del tipo Map&lt;String, Document>. Las claves del mapa son el nombre del archivo de entrada y un objeto de documento que contiene el contenido del archivo. Utilice la API getinputMap para leer los archivos de entrada.
* getConfigParameters: Devuelve un mapa inmutable de tipo Map&lt;String, Object>. El mapa contiene los parámetros de configuración de una carpeta inspeccionada.
* setResult: La implementación ContentProcessor utiliza la API para escribir el documento de salida en la carpeta de resultados. Puede proporcionar un nombre para el archivo de salida al API setResult. La API puede elegir utilizar o ignorar el archivo proporcionado según el patrón de carpeta/archivo de salida especificado. Si se especifica un patrón de carpeta, los archivos de salida tienen nombres como se describe en los flujos de trabajo. Si se especifica un patrón de archivo, los archivos de salida tienen nombres como se describe en el patrón de archivo

Consideración de la API setResult cuando se utiliza en flujos de trabajo:

* Para agregar un nuevo documento de salida que contribuya a la salida general del flujo de trabajo, llame al API setResult con un nombre de archivo que no se haya utilizado como nombre de archivo de salida en ningún paso anterior.
* Para actualizar un resultado generado por un paso anterior, llame al API setResult con un nombre de archivo ya utilizado por un paso anterior.
* Para eliminar un resultado generado por un paso anterior, llame a setResult con un nombre de archivo ya utilizado por un paso anterior y nulo como contenido.

>[!NOTE]
>
>Llamar al API setResult con contenido nulo en cualquier otro escenario provocaría un error.

El siguiente ejemplo se implementa como paso de flujo de trabajo. En el ejemplo, ECMAscript utiliza una variable stepCount para realizar un seguimiento del número de veces que se realiza una llamada a un paso en la instancia de flujo de trabajo actual.
El nombre de la carpeta de salida es una combinación del número de paso actual, el nombre del archivo original y el prefijo especificado en el parámetro outPrefix.

ECMAScript obtiene una referencia del servicio de contexto del flujo de trabajo y crea una implementación de la interfaz WorkflowContextProcessor. La implementación WorkflowContextProcessor acepta archivos de entrada, copia el archivo en una ubicación temporal y devuelve un documento que representa el archivo copiado. En función del valor de la variable booleana purgePrevious, el paso actual elimina el resultado generado la última vez por el mismo paso cuando el paso se inició en la instancia de flujo de trabajo actual. Al final, se invoca el método wfSvc.execute para ejecutar la implementación WorkflowContextProcessor. El contenido del documento de salida se guarda en la carpeta de resultados en la ruta física mencionada en el nodo de configuración de la carpeta inspeccionada.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### Crear un filtro de asignador de carga útil para asignar la estructura de una carpeta inspeccionada a la carga útil de un flujo de trabajo {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Cuando crea una carpeta inspeccionada, se crea una estructura de carpetas dentro de la carpeta que se está inspeccionando. La estructura de carpetas tiene carpetas de fase, resultado, conservación, entrada y error. La estructura de carpetas puede servir como carga útil de entrada al flujo de trabajo y aceptar la salida de un flujo de trabajo. También puede enumerar los puntos de error, si los hay.

Si la estructura de una carga útil es diferente de la estructura de la carpeta inspeccionada, puede escribir scripts personalizados para asignar la estructura de la carpeta inspeccionada a la carga útil. Este script se denomina filtro de asignador de cargas útiles. De forma predeterminada, AEM Forms proporciona un filtro de asignador de carga útil para asignar la estructura de la carpeta observada a una carga útil.

#### Crear un filtro personalizado del asignador de carga útil {#creating-a-custom-payload-mapper-filter}

1. Descargar el [SDK de cliente de Adobe](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Configure el SDK de cliente en la ruta de la versión del proyecto basado en Maven. Para empezar, puede descargar y abrir el siguiente proyecto basado en Maven en el IDE de su elección.
1. Edite el código de filtro del asignador de carga útil disponible en el paquete de ejemplo para adaptarlo a sus requisitos.
1. Utilice Maven para crear un paquete del filtro personalizado del asignador de carga útil.
1. Usar la [consola de paquetes de AEM](https://localhost:4502/system/console/bundles) para instalar el paquete.

   Ahora, el filtro personalizado del asignador de carga útil aparece en la interfaz de usuario de carpetas inspeccionadas de AEM. Puede utilizarlo con su flujo de trabajo.

   El siguiente código de ejemplo implementa un asignador simple basado en archivos para los archivos guardados en relación a una carga útil. Puede usarlo para empezar.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## Interacción de los usuarios con una carpeta inspeccionada {#how-users-interact-with-a-watched-folder}

Para un punto final de carpeta inspeccionada, los usuarios pueden iniciar operaciones de procesamiento de archivos al copiar o arrastrar archivos de entrada o carpetas desde sus escritorios a una carpeta inspeccionada. Los archivos se procesan en el orden de llegada.

En los puntos finales de carpeta inspeccionada, si un trabajo requiere un solo archivo de entrada, el usuario puede copiar ese archivo en la raíz de la carpeta inspeccionada.

Si el trabajo contiene más de un archivo de entrada, el usuario debe crear una carpeta fuera de la jerarquía de carpetas inspeccionadas que contenga todos los archivos necesarios. Esta nueva carpeta debe incluir los archivos de entrada (y opcionalmente un archivo DDX si el proceso lo necesita). Una vez construida la carpeta de trabajo, el usuario la copia en la carpeta de entrada de la carpeta inspeccionada.

>[!NOTE]
>
>Asegúrese de que el servidor de aplicaciones haya eliminado el acceso a los archivos de la carpeta inspeccionada. Si AEM Forms no puede eliminar los archivos de la carpeta de entrada después de analizarlos, el proceso asociado se iniciará indefinidamente.

## Información adicional acerca de las carpetas inspeccionadas {#additional-information-about-the-watched-folders}

### Acerca de la restricción {#about-throttling}

Cuando la restricción está habilitada para un punto final de carpeta de inspección, limita el número de trabajos de carpeta inspeccionada que se procesan en un momento dado. El número máximo de trabajos está determinado por el valor Tamaño del lote, también configurable en el punto final de la carpeta inspeccionada. Cuando se alcanza el límite de restricción, los documentos entrantes en el directorio de entrada de la carpeta inspeccionada no se encuesta. El documento también permanece en el directorio de entrada hasta que se completen otros trabajos de la carpeta inspeccionada y se realice otro intento de encuesta. Para el procesamiento sincrónico, todos los trabajos procesados en una sola encuesta se cuentan hacia el límite de restricción, aunque los trabajos se procesen consecutivamente en un solo hilo.

>[!NOTE]
>
>La restricción no se escala con un grupo. Cuando la restricción está habilitada, el grupo en su conjunto no procesará más del número de trabajos especificado en Tamaño de lote en un momento dado. Este límite es para todo el grupo y no es específico de cada nodo del grupo. Por ejemplo, con un tamaño de lote de 2, se podía alcanzar el límite de restricción con un solo nodo procesando dos trabajos, y ningún otro nodo encuestaría el directorio de entrada hasta que se complete uno de los trabajos.

#### Funcionamiento de la restricción {#how-throttling-works}

La carpeta inspeccionada analiza la carpeta de entrada en cada intervalo de encuesta, toma el número de archivos especificados en el tamaño del lote e invoca el servicio de destino para cada uno de estos archivos. Por ejemplo, si el tamaño del lote es de cuatro, en cada análisis, la carpeta inspeccionada recoge cuatro archivos, crea cuatro solicitudes de invocación e invoca al servicio de destino. Antes de que se completen estas solicitudes, si se invoca la carpeta inspeccionada, de nuevo se inician cuatro trabajos, independientemente de si se han completado o no los cuatro trabajos anteriores.

La restricción impide que la carpeta inspeccionada invoque nuevos trabajos cuando los trabajos anteriores no se completan. La carpeta inspeccionada detecta los trabajos en curso y procesa los nuevos trabajos en función del tamaño del lote menos los trabajos en curso. Por ejemplo, en la segunda invocación, si el número de trabajos completados es solo tres y un trabajo sigue en curso, la carpeta inspeccionada invoca solo tres trabajos más.

* La carpeta inspeccionada depende del número de archivos presentes en la carpeta de fase para averiguar cuántos trabajos hay en curso. Si los archivos permanecen sin procesar en la carpeta de fase, la carpeta inspeccionada no invoca más trabajos. Por ejemplo, si el tamaño del lote es de cuatro y hay tres trabajos paralizados, la carpeta inspeccionada solo invoca un trabajo en invocaciones posteriores. Existen varios escenarios que pueden hacer que los archivos permanezcan sin procesar en la carpeta de fase. Cuando los trabajos están paralizados, el administrador puede finalizar el proceso en la página de administración Administración de procesos para que la carpeta inspeccionada mueva los archivos fuera de la carpeta de fase.
* Si el servidor de AEM Forms se desactiva antes de que la carpeta inspeccionada invoque los trabajos, el administrador puede sacar los archivos de la carpeta de fase. Para obtener más información, consulte [Puntos de error y recuperación](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Si el servidor de AEM Forms se está ejecutando pero la carpeta inspeccionada no se está ejecutando cuando el servicio Administrador de trabajos devuelve la llamada, lo que ocurre cuando los servicios no se inician en la secuencia ordenada, el administrador puede sacar los archivos de la carpeta de fase. Para obtener más información, consulte [Puntos de error y recuperación](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Puntos de error, puntos recoveryFailure y recuperación {#failure-points-and-recoveryfailure-points-and-recovery}

En cada evento de encuesta, la carpeta inspeccionada bloquea la carpeta de entrada, mueve los archivos que coinciden con el patrón de archivo de inclusión a la carpeta de fase y, a continuación, desbloquea la carpeta de entrada. El bloqueo es necesario para que dos subprocesos no recojan el mismo conjunto de archivos y los procesen dos veces. Las posibilidades de que esto ocurra aumentan con un pequeño intervalo de encuesta y un gran tamaño de lote. Tras mover los archivos a la carpeta de fase, la carpeta de entrada se desbloquea para que otros hilos puedan analizar la carpeta. Este paso ayuda a proporcionar un alto rendimiento, ya que otros hilos pueden analizar mientras uno procesa los archivos.

Una vez que los archivos se mueven a la carpeta de fase, las solicitudes de invocación se crean para cada archivo y se invoca el servicio de destino. Puede haber casos en los que la carpeta inspeccionada no pueda recuperar los archivos de la carpeta de fase:

* Si el servidor se apaga antes de que la carpeta inspeccionada pueda crear la solicitud de invocación, los archivos de la carpeta de fase permanecen en la carpeta de fase y no se recuperan.

* Si la carpeta inspeccionada ha creado correctamente la solicitud de invocación para cada uno de los archivos de la carpeta de fase y el servidor se bloquea, hay dos comportamientos basados en el tipo de invocación:

   * **Sincrónica**: Si la carpeta inspeccionada está configurada para invocar el servicio sincrónicamente, todos los archivos de la carpeta de fase permanecen sin procesar en la carpeta de fase.
   * **Asincrónica**: En este caso, la carpeta inspeccionada depende del servicio Administrador de trabajos. Si el servicio Administrador de trabajos vuelve a llamar a la carpeta inspeccionada, los archivos de la carpeta de fase se mueven a la carpeta de conservación o de errores en función de los resultados de la invocación. Si el servicio Administrador de trabajos no vuelve a llamar a la carpeta inspeccionada, los archivos permanecerán sin procesar en la carpeta de fase. Esta situación ocurre cuando la carpeta inspeccionada no se está ejecutando cuando el administrador de trabajos vuelve a llamar.

#### Recuperar archivos de origen sin procesar en la carpeta de fase {#recover-unprocessed-source-files-in-the-stage-folder}

Cuando la carpeta inspeccionada no puede procesar los archivos de origen en la carpeta de fase, puede recuperar los archivos sin procesar.

1. Reinicie el servidor de aplicaciones o el nodo.

1. Detenga el procesamiento por parte de la carpeta inspeccionada de nuevos archivos de entrada. Si omite este paso, será mucho más difícil determinar qué archivos no se procesan en la carpeta de fase. Para evitar que la carpeta inspeccionada procese nuevos archivos de entrada, realice una de las siguientes tareas:

   * Cambie la propiedad includeFilePattern de la carpeta inspeccionada a algo que no coincida con ninguno de los nuevos archivos de entrada (por ejemplo, introduzca NOMATCH).
   * Suspenda el proceso que está creando nuevos archivos de entrada.

   Espere hasta que AEM Forms recupere y procese todos los archivos. La mayoría de los archivos deben recuperarse y los nuevos archivos de entrada deben procesarse correctamente. El tiempo que espera para que la carpeta inspeccionada se recupere y procese los archivos dependerá de la duración de la operación que se invoque y del número de archivos que se recuperarán.

1. Determine qué archivos no se pueden procesar. Si ha esperado una cantidad de tiempo adecuada y ha completado el paso anterior, y todavía quedan archivos sin procesar en la carpeta de fase, vaya al paso siguiente.

   >[!NOTE]
   >
   >Puede consultar la marca de fecha y hora de los archivos en el directorio de fase. Según el número de archivos y el tiempo de procesamiento normal, puede determinar qué archivos son lo suficientemente antiguos como para que se consideren atascados.

1. Copie los archivos sin procesar del directorio de fase al directorio de entrada.

1. Si ha impedido que la carpeta inspeccionada procese nuevos archivos de entrada en el paso 2, cambie el patrón de archivo de inclusión a su valor anterior o vuelva a habilitar el proceso que ha deshabilitado.

### Encadenar carpetas inspeccionadas {#chain-watched-folders-together}

Las carpetas inspeccionadas se pueden encadenar para que un documento resultante de una carpeta inspeccionada sea el documento de entrada de la siguiente carpeta inspeccionada. Cada carpeta inspeccionada puede invocar un servicio diferente. Al configurar las carpetas inspeccionadas de esta forma, se pueden invocar varios servicios. Por ejemplo, una carpeta inspeccionada podría convertir archivos PDF a Adobe PostScript® y una segunda carpeta inspeccionada podría convertir los archivos PostScript a formato PDF/A. Para ello, simplemente configure la carpeta de resultados de la carpeta inspeccionada definida por el primer punto final para que apunte a la carpeta de entrada de la carpeta inspeccionada definida por el segundo punto final.

El resultado de la primera conversión iría a \path\result. La entrada para la segunda conversión sería \path\result y el resultado de la segunda conversión iría a \path\result\result (o el directorio que defina en el cuadro Carpeta de resultados para la segunda conversión).

### Patrones de archivos y carpetas {#file-and-folder-patterns}

Los administradores pueden especificar el tipo de archivo que puede invocar un servicio. Se pueden establecer varios patrones de archivo para cada carpeta inspeccionada. Un patrón de archivo puede ser una de las siguientes propiedades de archivo:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
* Archivos con nombres específicos; por ejemplo, data.&#42;
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &#42;.[dD][Aa]&#39;port&#39;
   * &#42;.[Xx][Mm][Ll]

* El administrador puede definir el patrón de archivo de la carpeta de salida en la que desea almacenar los resultados. Para las carpetas de salida (resultado, conservar y error), el administrador puede especificar cualquiera de estos patrones de archivo:
* %Y = año (completo)
* %y = año (dos últimos dígitos)
* %M = mes
* %D = día del mes
* %d = día del año
* %h = hora
* %m = minuto
* %s = segundo
* %R = número aleatorio entre 0 y 9
* %J = Nombre del trabajo

Por ejemplo, la ruta a la carpeta de resultados puede ser C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Las asignaciones de parámetros de salida también pueden especificar patrones adicionales, como los siguientes:

* %F = Nombre de archivo de origen
* %E = Extensión de nombre de archivo de origen

Si el patrón de asignación de parámetros de salida termina con &quot;File.separator&quot; (que es el separador de rutas), se crea una carpeta y el contenido se copia en esa carpeta. Si el patrón no termina con “File.separator”, el contenido (archivo o carpeta de resultados) se crea con ese nombre.

## Usar el Generador de PDF con una carpeta inspeccionada {#using-pdf-generator-with-a-watched-folder}

Puede configurar una carpeta inspeccionada para iniciar un flujo de trabajo, servicio o script para procesar los archivos de entrada. En la siguiente sección, configuraremos una carpeta inspeccionada para iniciar un ECMAScript. El ECMAScript utilizaría el Generador de PDF para convertir documentos de Microsoft Word (.docx) en documentos PDF.

Realice los siguientes pasos para configurar una carpeta inspeccionada con el generador de PDF:

1. [Crear un ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Crear un flujo de trabajo](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configurar la carpeta inspeccionada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Crear un ECMAScript {#create-an-ecmascript}

ECMAScript utilizaría la API createPDF de PDF Generator para convertir documentos de Microsoft Word (.docx) en documentos de PDF. Siga estos pasos para crear el script:

1. Abra CRXDE lite en una ventana del explorador. La dirección URL es https://&#39;[server]:[port]&#39;/crx/de.

1. Vaya a /etc/workflow/scripts y cree una carpeta denominada PDFG.

1. En la carpeta PDFG, cree un archivo llamado pdfg-openOffice-sample.ecma y agregue el siguiente código al archivo:

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. Guarde y cierre el archivo.

### Crear un flujo de trabajo {#create-a-workflow}

1. Abra la interfaz de usuario del flujo de trabajo de AEM en una ventana del explorador.
   <https://[servername>]:&#39;port&#39;/workflow

1. En la vista Modelos, haga clic en **Nuevo**. En el cuadro de diálogo Nuevo flujo de trabajo, especifique **Título** y haga clic en **Aceptar**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Seleccione el flujo de trabajo recién creado y haga clic en **Editar**. El flujo de trabajo se abre en una nueva ventana.

1. Elimine el paso predeterminado del flujo de trabajo. Arrastre y suelte el paso Proceso de la barra de tareas al flujo de trabajo.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Haga clic con el botón derecho en el paso Proceso y seleccione **Editar**. Aparecerá la ventana Propiedades del paso.

1. En la pestaña Proceso, seleccione ECMAScript. Por ejemplo, el script pdfg-openOffice-sample.ecma creado en [Crear un ECMAScript](#p-create-an-ecmascript-p). Habilite la opción **Avance del controlador** y haga clic en **Aceptar**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurar la carpeta inspeccionada {#configure-the-watched-folder}

1. Abra CRXDE lite en una ventana del explorador. https://&#39;[server]:[port]&#39;/crx/de/

1. Vaya a la carpeta /etc/fd/watchfolder/config/ y cree un nodo de tipo nt:unstructured.

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Agregue las siguientes propiedades al nodo:

   * folderPath (String): Ruta de la carpeta que se va a analizar en intervalos de tiempo definidos. La carpeta debe estar en una ubicación compartida con todos los servidores que tengan acceso completo al servidor.
inputProcessorType (String): Tipo de proceso que se va a iniciar. En este tutorial, especifique el flujo de trabajo.

   * inputProcessorId (String): El comportamiento de la propiedad inputProcessorId se basa en el valor especificado para la propiedad inputProcessorType. En este ejemplo, el valor de la propiedad inputProcessorType es flujo de trabajo. Por lo tanto, para la propiedad inputProcessorId especifique la siguiente ruta del flujo de trabajo PDFG: /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (String): Patrón del archivo de salida. Puede especificar una carpeta o un patrón de archivo. Si se especifica un patrón de carpeta, los archivos de salida tienen nombres como se describe en los flujos de trabajo. Si se especifica un patrón de archivo, los archivos de salida tienen nombres como se describe en el patrón de archivo.

   Además de las propiedades obligatorias mencionadas anteriormente, las carpetas inspeccionadas también admiten algunas propiedades opcionales. Para obtener una lista y una descripción completas de las propiedades opcionales, consulte [Propiedades de la carpeta inspeccionada](#watchedfolderproperties).

## Problemas conocidos {#watched-folder-known-issues}

Al iniciar AEM 6.5 Forms en JEE, los archivos empiezan a procesarse antes de que JBoss se inicie completamente y los archivos no se procesen. Para evitarlo, antes de iniciar JBoss, borre todas las carpetas inspeccionadas.
