---
title: Integrar [!DNL Assets] con [!DNL InDesign Server]
description: Aprenda a integrar [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 2%

---

# Integrar [!DNL Adobe Experience Manager Assets] con [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] utiliza:

* Un proxy para distribuir la carga de ciertas tareas de procesamiento. Un proxy es una instancia de [!DNL Experience Manager] que se comunica con un trabajador proxy para realizar una tarea específica y otras instancias de [!DNL Experience Manager] para entregar los resultados.
* Un trabajador proxy para definir y administrar una tarea específica.
Pueden cubrir una amplia variedad de tareas; por ejemplo, usar un [!DNL InDesign Server] para procesar archivos.

Para cargar completamente los archivos a [!DNL Experience Manager Assets] que creó con [!DNL Adobe InDesign], se usa un proxy. Utiliza un trabajador proxy para comunicarse con [!DNL Adobe InDesign Server], donde se ejecutan [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) para extraer metadatos y generar varias representaciones para [!DNL Experience Manager Assets]. El trabajador proxy habilita la comunicación bidireccional entre las instancias de [!DNL InDesign Server] y [!DNL Experience Manager] en una configuración de nube.

>[!NOTE]
>
>[!DNL Adobe InDesign] se ofrece como dos ofertas independientes. [Aplicación de escritorio Adobe InDesign](https://www.adobe.com/products/indesign.html) que se usa para diseñar diseños de página para impresión y distribución digital. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) le permite crear documentos automatizados mediante programación basándose en lo que ha creado con [!DNL InDesign]. Funciona como un servicio que ofrece una interfaz a su motor [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting). Los scripts se escriben en [!DNL ExtendScript], que es similar a [!DNL JavaScript]. Para obtener información acerca de [!DNL InDesign] scripts, consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Funcionamiento de la extracción {#how-the-extraction-works}

El [!DNL Adobe InDesign Server] se puede integrar con [!DNL Experience Manager Assets] para que los archivos INDD creados con [!DNL InDesign] se puedan cargar, generar representaciones, extraer todos los medios (por ejemplo, vídeo) y almacenar como recursos:

>[!NOTE]
>
>Las versiones anteriores de [!DNL Experience Manager] pudieron extraer XMP y la miniatura, ahora se pueden extraer todos los medios.

1. Suba su archivo INDD a [!DNL Experience Manager Assets].
1. Un módulo envía scripts de comandos a [!DNL InDesign Server] a través de SOAP (Simple Object Access Protocol).
Esta secuencia de comandos:

   * Recupere el archivo INDD.
   * Ejecutar [!DNL InDesign Server] comandos:

      * Se extraerán la estructura, el texto y los archivos multimedia.
      * Se generan las representaciones de PDF y JPG.
      * Se generan las representaciones HTML e IDML.

   * Volver a publicar los archivos resultantes en [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML es un formato basado en XML que procesa todo el contenido del archivo [!DNL InDesign]. Se almacena como un paquete comprimido con la compresión [ZIP](https://www.techterms.com/definition/zip). Para obtener más información, vea [Formatos de intercambio InDesign INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Si [!DNL InDesign Server] no está instalado o no está configurado, puede cargar un archivo INDD en [!DNL Experience Manager]. Sin embargo, las representaciones generadas se limitan a PNG y JPEG. No podrá generar representaciones de HTML, .idml ni de la página.

1. Después de la generación de la extracción y la representación:

   * La estructura se replica en un `cq:Page` (tipo de representación).
   * El texto y los archivos extraídos se almacenan en [!DNL Experience Manager Assets].
   * Todas las representaciones se almacenan en [!DNL Experience Manager Assets], en el propio recurso.

## Integrar [!DNL InDesign Server] con Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar [!DNL InDesign Server] para usarlo con [!DNL Experience Manager Assets] y después de configurar el proxy, debe:

1. [Instalar InDesign Server](#installing-the-indesign-server).
1. Si es necesario, [configure el flujo de trabajo de Experience Manager Assets](#configuring-the-aem-assets-workflow).
Esto solo es necesario si los valores predeterminados no son adecuados para su instancia.
1. Configure un trabajador proxy [para InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instalar [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar [!DNL InDesign Server] para utilizarlo con [!DNL Experience Manager]:

1. Descargue e instale [!DNL InDesign Server].

1. Si es necesario, puede personalizar la configuración de su instancia de [!DNL InDesign Server].

1. Desde la línea de comandos, inicie el servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Esto inicia el servidor con el complemento de SOAP que escucha en el puerto 8080. Todos los mensajes de registro y los resultados se escriben directamente en la ventana de comandos.

   >[!NOTE]
   >
   >Si desea guardar los mensajes de salida en un archivo, utilice la redirección; por ejemplo, en Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurar el flujo de trabajo [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tiene un flujo de trabajo preconfigurado **[!UICONTROL DAM Update Asset]**, que tiene varios pasos de proceso específicos para [!DNL InDesign]:

* [Extracción de medios](#media-extraction)
* [Extracción de página](#page-extraction)

Este flujo de trabajo está configurado con valores predeterminados que se pueden adaptar a la configuración en las distintas instancias de autor (se trata de un flujo de trabajo estándar, por lo que hay más información disponible en [Edición de un flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Si utiliza los valores predeterminados (incluido el puerto SOAP), no es necesaria ninguna configuración.

Después de la configuración, cargar [!DNL InDesign] archivos en [!DNL Experience Manager Assets] (mediante cualquiera de los métodos habituales) déclencheur el flujo de trabajo para procesar el recurso y preparar las distintas representaciones. Pruebe la configuración cargando un archivo INDD en [!DNL Experience Manager Assets] para confirmar que ve las diferentes representaciones creadas por IDS en `<*your_asset*>.indd/Renditions`

#### Extracción de medios {#media-extraction}

Este paso controla la extracción de medios del archivo INDD.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de medios]**.

![Argumentos de extracción de medios y rutas de script](assets/media_extraction_arguments_scripts.png)

Argumentos de extracción de medios y rutas de scripts

* **Biblioteca ExtendScript**: Se trata de una biblioteca de método http get/post simple, requerida por los demás scripts.

* **Ampliar scripts**: aquí puede especificar diferentes combinaciones de scripts. Si desea que se ejecuten sus propios scripts en [!DNL InDesign Server], guárdelos en `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>No cambie la biblioteca ExtendScript. Esta biblioteca proporciona la funcionalidad HTTP necesaria para comunicarse con Sling. Esta configuración especifica la biblioteca que se enviará a [!DNL InDesign Server] para su uso allí.

El script `ThumbnailExport.jsx` ejecutado por el paso del flujo de trabajo de extracción de medios genera una representación de miniaturas en formato JPG. El paso del flujo de trabajo Procesar miniaturas utiliza esta representación para generar las representaciones estáticas que requiere [!DNL Experience Manager].

Puede configurar el paso del flujo de trabajo Procesar miniaturas para generar representaciones estáticas en diferentes tamaños. Asegúrese de no quitar los valores predeterminados, ya que son necesarios para la interfaz [!DNL Experience Manager Assets]. Por último, el paso de flujo de trabajo Eliminar representación de previsualización de imagen elimina la representación de miniaturas de JPG, ya que ya no es necesaria.

#### Extracción de página {#page-extraction}

Esto crea una página [!DNL Experience Manager] a partir de los elementos extraídos. Se utiliza un controlador de extracción para extraer datos de una representación (actualmente HTML o IDML). Estos datos se utilizan para crear una página con PageBuilder.

Para personalizar, puede editar la pestaña **[!UICONTROL Argumentos]** del paso **[!UICONTROL Extracción de página]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Controlador de extracción de página**: en la lista emergente, seleccione el controlador que desee utilizar. Un controlador de extracción funciona en una representación específica, elegida por un elemento relacionado `RenditionPicker` (consulte la API `ExtractionHandler`). En una instalación estándar de [!DNL Experience Manager] está disponible lo siguiente:
   * Controlador de extracción de exportación IDML: opera en la representación `IDML` generada en el paso MediaExtract.

* **Nombre de página**: especifique el nombre que desea asignar a la página resultante. Si se deja en blanco, el nombre es &quot;página&quot; (o un derivado si &quot;página&quot; ya existe).

* **Título de página**: especifique el título que desea asignar a la página resultante.

* **Ruta de acceso raíz de página**: La ruta de acceso a la ubicación raíz de la página resultante. Si se deja en blanco, se utiliza el nodo que contiene las representaciones del recurso.

* **Plantilla de página**: La plantilla que se usará al generar la página resultante.

* **Diseño de página**: El diseño de página que se va a usar al generar la página resultante.

### Configurar el trabajador proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>El trabajador reside en la instancia de proxy.

1. En la consola Herramientas, expanda **[!UICONTROL Configuraciones de Cloud Services]** en el panel izquierdo. A continuación, expanda **[!UICONTROL Configuración de proxy de nube]**.

1. Haga doble clic en el programa de **[!UICONTROL IDS de trabajo]** para abrirlo y configurarlo.

1. Haga clic en **[!UICONTROL Editar]** para abrir el cuadro de diálogo de configuración y definir la configuración necesaria:

   ![proxy_disworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Grupo IDS**
Extremos de SOAP que se utilizarán para comunicarse con [!DNL InDesign Server]. Puede añadir, quitar y ordenar los elementos que sean necesarios.

1. Haga clic en Aceptar para guardar.

### Configurar el externalizador de vínculos CQ de día {#configuring-day-cq-link-externalizer}

Si [!DNL InDesign Server] y [!DNL Experience Manager] se encuentran en hosts diferentes o una o ambas aplicaciones no funcionan en puertos predeterminados, configure [!UICONTROL Day CQ Link Externalizer] para establecer el nombre de host, el puerto y la ruta de contenido para [!DNL InDesign Server].

1. Acceda a la consola web en `https://[aem_server]:[port]/system/console/configMgr`.
1. Busque la configuración **[!UICONTROL Day CQ Link Externalizer]**. Haga clic en **[!UICONTROL Editar]** para abrir.
1. La configuración del externalizador de vínculos ayuda a crear direcciones URL absolutas para la implementación de [!DNL Experience Manager] y para [!DNL InDesign Server]. Utilice el campo **[!UICONTROL Dominios]** para especificar el nombre de host de [!DNL Adobe InDesign Server]. Haga clic en **Guardar**.

   En direcciones URL absolutas, utilice `localhost` como nombre de host para la instancia local (autor) y el nombre de host o la dirección IP para la instancia de publicación, como se muestra en la siguiente ilustración.

   ![Configuración del externalizador de vínculos](assets/link-externalizer-config.png)

### Habilitar el procesamiento de trabajos en paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Ahora puede habilitar el procesamiento de trabajos en paralelo para los ID. Determinar el número máximo de trabajos paralelos (`x`) que un [!DNL InDesign Server] puede procesar:

* En un solo equipo multiprocesador, el número máximo de trabajos paralelos (`x`) que un [!DNL InDesign Server] puede procesar es uno menos que el número de procesadores que ejecutan IDS.
* Cuando ejecuta IDS en varios equipos, necesita contar el número total de procesadores disponibles (es decir, en todos los equipos) y luego restar el número total de equipos.

Para configurar el número de trabajos de IDS paralelos:

1. Abra la ficha **[!UICONTROL Configuraciones]** de la Consola Felix; por ejemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Seleccione la cola de procesamiento de IDS en `Apache Sling Job Queue Configuration`.

1. Establecer:

   * **Tipo** - `Parallel`
   * **Máximo de trabajos paralelos** - `<*x*>` (según el cálculo anterior)

1. Guarde estos cambios.
1. Para habilitar la compatibilidad con varias sesiones para Adobe CS6 y versiones posteriores, marque la casilla de verificación `enable.multisession.name`, en la configuración de `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Cree un [grupo de `x` trabajadores de IDS agregando puntos de conexión de SOAP a la configuración de IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Si hay varios equipos que ejecutan [!DNL InDesign Server], agregue puntos finales de SOAP (número de procesadores por equipo -1) para cada equipo.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Al trabajar con grupos de empleados, puede habilitar la lista de bloqueados de los empleados de IDS.
>
>Para ello, habilite la casilla de verificación **[!UICONTROL enable.retry.name]**, en la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, que habilita los reintentos de trabajos de IDS.
>
>Además, en la configuración `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, establezca un valor positivo para el parámetro `max.errors.to.blacklist` que determina el número de reintentos de trabajos antes de excluir un ID de la lista de controladores de trabajos.
>
>De forma predeterminada, después del tiempo configurable (`retry.interval.to.whitelist.name`) en minutos, el trabajador de IDS se vuelve a validar. Si el trabajador se encuentra en línea, se elimina de la lista de bloqueados.

## Habilitar compatibilidad con [!DNL InDesign Server] 10.0 o posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 o superior, realice los siguientes pasos para habilitar la compatibilidad con varias sesiones.

1. Abra el Administrador de configuración desde la instancia `https://[aem_server]:[port]/system/console/configMgr` de [!DNL Experience Manager Assets].
1. Edite la configuración `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Seleccione la opción **[!UICONTROL ids.cc.enable]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Para la integración de [!DNL InDesign Server] con [!DNL Experience Manager Assets], use un procesador de núcleo múltiple porque la característica de compatibilidad de sesión necesaria para la integración no es compatible con los sistemas de un solo núcleo.

## Configurar credenciales de [!DNL Experience Manager] {#configure-aem-credentials}

Puede cambiar las credenciales de administrador predeterminadas (nombre de usuario y contraseña) para obtener acceso a [!DNL InDesign Server] desde la implementación de [!DNL Experience Manager] sin romper la integración con [!DNL InDesign Server].

1. Vaya a `/etc/cloudservices/proxy.html`.
1. En el cuadro de diálogo, especifique el nuevo nombre de usuario y contraseña.
1. Guarde las credenciales.

>[!MORELIKETHIS]
>
>* [Acerca del Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
