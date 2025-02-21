---
title: Configurar extremos de carpetas vigiladas
description: Obtenga información sobre cómo configurar puntos finales de carpetas vigiladas. Si un documento se coloca en una carpeta vigilada, se invoca una operación de servicio configurada y se manipula el archivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '7192'
ht-degree: 19%

---

# Configurar extremos de carpetas vigiladas {#configuring-watched-folder-endpoints}

Un administrador puede configurar una carpeta de red, conocida como *carpeta vigilada*, de forma que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se invoque una operación de servicio configurada y se manipule el archivo. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en una carpeta de salida especificada.

## Configuración del servicio de carpetas inspeccionadas {#configuring-the-watched-folder-service}

Antes de configurar un punto final de carpeta inspeccionada, configure el servicio de carpeta inspeccionada. Los parámetros de configuración del servicio de carpetas inspeccionadas tienen dos propósitos:

* Para configurar atributos que son comunes a todos los extremos de carpetas vigiladas
* Para proporcionar valores predeterminados para todos los extremos de carpeta vigilada

Después de configurar el servicio de carpetas inspeccionadas, agregue un punto final de carpeta inspeccionada para el servicio de destino. Al agregar el punto de conexión, establece valores, como el nombre del servicio y el nombre de la operación que se invocará cuando los archivos o carpetas se coloquen en la carpeta de entrada del servicio de carpeta inspeccionada configurado. Para obtener más información sobre la configuración del servicio de carpetas inspeccionadas, consulte [Configuración del servicio de carpetas inspeccionadas](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Crear una carpeta vigilada {#creating-a-watched-folder}

Puede crear una carpeta vigilada de las dos maneras siguientes:

* Al configurar los ajustes de un extremo de carpeta inspeccionada, escriba la ruta completa del directorio principal en el cuadro Ruta y anexe el nombre de la carpeta inspeccionada que se va a crear, como se muestra en este ejemplo:
  `  C:\MyPDFs\MyWatchedFolder`Dado que la carpeta MyWatchedFolder no existe todavía, AEM Forms intenta crearla en esa ubicación.

* Cree una carpeta en el sistema de archivos antes de configurar un punto final de carpeta vigilada y, a continuación, escriba la ruta de acceso completa en el cuadro Ruta.

En un entorno agrupado, la carpeta que se utiliza como carpeta vigilada debe ser accesible, modificable y compartida en el sistema de archivos o red. En esta situación, cada instancia de servidor de aplicaciones del clúster debe tener acceso a la misma carpeta compartida.

En Windows, si el servidor de aplicaciones se está ejecutando como un servicio, debe iniciarse con el acceso adecuado a la carpeta compartida de una de las siguientes maneras:

* Configure el servicio del servidor de aplicaciones Iniciar sesión como **parámetro** para que se inicie como un usuario específico con el acceso adecuado a la carpeta vigilada compartida.
* Configure el servicio del servidor de aplicaciones Iniciar como sistema local para permitir que el servicio interactúe con el escritorio. Esta opción requiere que todos puedan acceder y escribir en la carpeta vigilada compartida.

## Encadenamiento de carpetas vigiladas {#chaining-together-watched-folders}

Las carpetas inspeccionadas se pueden encadenar para que un documento resultante de una carpeta inspeccionada sea el documento de entrada de la siguiente carpeta inspeccionada. Cada carpeta vigilada puede invocar un servicio diferente. Al configurar las carpetas vigiladas de esta manera, se pueden invocar varios servicios. Por ejemplo, una carpeta inspeccionada podría convertir archivos de PDF a Adobe PostScript® y una segunda carpeta inspeccionada podría convertir los archivos de PostScript a formato PDF/A. Para ello, simplemente configure la carpeta *result* de la carpeta vigilada definida por el primer punto final para que apunte a la carpeta *input* de la carpeta vigilada definida por el segundo punto final.

El resultado de la primera conversión iría a \path\result. La entrada para la segunda conversión sería \path\result y el resultado de la segunda conversión iría a \path\result\result (o el directorio que defina en el cuadro Carpeta de resultados para la segunda conversión).

## Interacción de los usuarios con las carpetas vigiladas {#how-users-interact-with-watched-folders}

Para un punto final de carpeta inspeccionada, los usuarios pueden invocar copiando o arrastrando archivos de entrada o carpetas desde sus escritorios a una carpeta inspeccionada. Los archivos se procesarán en el orden en que lleguen.

En el caso de los extremos de carpeta inspeccionada, si el trabajo requiere un solo archivo de entrada, el usuario puede copiar ese archivo en la raíz de la carpeta inspeccionada.

Si el trabajo contiene más de un archivo de entrada, el usuario debe crear una carpeta fuera de la jerarquía de carpetas vigilada que contenga todos los archivos necesarios. Esta nueva carpeta debe incluir los archivos de entrada (y opcionalmente un archivo DDX si el proceso lo necesita). Una vez construida la carpeta de trabajo, el usuario la copia en la carpeta de entrada de la carpeta vigilada.

>[!NOTE]
>
>Asegúrese de que el servidor de aplicaciones haya eliminado el acceso a los archivos de la carpeta vigilada. Si los formularios AEM Forms no pueden eliminar los archivos de la carpeta de entrada después de analizarlos, el proceso asociado se invocará indefinidamente.

## Salida de carpeta inspeccionada {#watched-folder-output}

Cuando la entrada es una carpeta y el resultado consta de varios archivos, los formularios AEM Forms crean una carpeta de salida con el mismo nombre que la carpeta de entrada y copian los archivos de salida en esa carpeta. Cuando el resultado consiste en un mapa del documento que contiene un par clave-valor, como el resultado de un proceso de salida, la clave se utiliza como nombre del archivo de salida.

Los nombres de archivo de salida que resultan de un proceso de extremo no pueden contener caracteres que no sean letras, números y un punto (.) antes de la extensión del archivo. Los formularios AEM convierten otros caracteres en sus valores hexadecimales.

Las aplicaciones cliente recogen los documentos de resultados de la carpeta de resultados de la carpeta inspeccionada. Los errores de proceso se registran en la carpeta de errores de carpeta vigilada.

## Cómo funciona la carpeta inspeccionada {#how-watched-folder-works}

El módulo Carpeta inspeccionada contiene estos servicios:

* Servicio de carpetas inspeccionadas
* provider.file_scan_service
* provider.file_write_results_service

Además de los servicios enumerados anteriormente, la carpeta inspeccionada también depende de otros servicios, incluido el servicio Programador para programar los trabajos y el servicio Administrador de trabajos para admitir la invocación asincrónica de servicios de destino.

### Cómo procesa la carpeta inspeccionada una solicitud de invocación {#how-watched-folder-processes-an-invocation-request}

El servicio de carpetas inspeccionadas administra la creación, actualización y eliminación de los puntos de conexión. Una vez que el administrador crea los puntos de conexión, se programa su activación por el servicio Scheduler en función del intervalo de repetición o la expresión cron especificados.

Este diagrama ilustra cómo la carpeta inspeccionada procesa una solicitud de invocación.

![en_watchedfolder](assets/en_watchedfolder.png)

El proceso de invocar un servicio mediante carpetas vigiladas es el siguiente:

1. Una aplicación cliente coloca archivos o carpetas en la carpeta de entrada de la carpeta vigilada.
1. Cuando se produce el intervalo de análisis del trabajo, el servicio Planificador invoca al provider.file_scan_service para procesar los archivos o carpetas de la carpeta de entrada.
1. El provider.file_scan_service realiza estas tareas:


   * Analiza la carpeta de entrada en busca de archivos o carpetas que coincidan con el patrón de archivo de inclusión y excluye archivos o carpetas para el patrón de archivo de exclusión especificado. Primero se recogen los archivos o carpetas más antiguos. También se recogen los archivos y carpetas que son anteriores al tiempo de espera. En un análisis, el número de archivos o carpetas que se procesan se basa en el tamaño del lote. Para obtener información acerca de los patrones de archivo, vea [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns). Para obtener información sobre cómo establecer el tamaño del lote, consulte [Configuración del servicio de carpetas inspeccionadas](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Recopila los archivos o carpetas para su procesamiento. Si los archivos o carpetas no se descargan completamente, se recogerán en el siguiente análisis. Para asegurarse de que las carpetas se descargan completamente, los administradores deben crear una carpeta con un nombre mediante el patrón de exclusión de archivos. Una vez que la carpeta tenga todos los archivos, se debe cambiar el nombre al patrón especificado en el patrón de archivo de inclusión. Este paso garantiza que la carpeta tenga todos los archivos necesarios para invocar el servicio. Para obtener más información sobre cómo asegurar que las carpetas se descarguen completamente, consulte [Sugerencias y trucos para carpetas vigiladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Mueve los archivos o carpetas a la carpeta de fase después de seleccionarlos para su procesamiento.
   * Convierte los archivos o carpetas de la carpeta de fase a la entrada adecuada en función de las asignaciones de parámetros de entrada del extremo. Para ver ejemplos de asignaciones de parámetros de entrada, vea [Sugerencias y trucos para carpetas vigiladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. El servicio de destino configurado para el extremo se invoca sincrónica o asincrónicamente. El servicio de destino se invoca con el nombre de usuario y la contraseña configurados para el extremo.

   * La invocación sincrónica llama al servicio de destino directa e inmediatamente administra la respuesta.
   * Para las invocaciones asincrónicas, se llama al servicio de destino a través del servicio Administrador de trabajos, que coloca la solicitud en una cola. El servicio Administrador de trabajos, a su vez, llama al proveedor.file_write_results_service para administrar los resultados.

1. El provider.file_write_results_service administra la respuesta o el error de la invocación del servicio de destino. Cuando se realiza correctamente, la salida se guarda en la carpeta de resultados en función de la configuración del punto de conexión. El provider.file_write_results_service también conserva el origen si el extremo está configurado para conservar los resultados una vez completados correctamente.

   Cuando la invocación del servicio de destino produce un error, provider.file_write_results_service registra el motivo del error en un archivo failure.log y lo coloca en la carpeta de errores. La carpeta de errores se crea en función de los parámetros de configuración especificados para el punto de conexión. Cuando el administrador define la opción Conservar al producirse un error para la configuración del extremo, provider.file_write_results_service también copia los archivos de origen en la carpeta de errores. Para obtener información acerca de cómo recuperar archivos de la carpeta de errores, vea [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Configuración del extremo de carpeta inspeccionada {#watched-folder-endpoint-settings}

Utilice la siguiente configuración para configurar un punto final de carpeta vigilada.

**Nombre:** (obligatorio) identifica el extremo. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si va a introducir una dirección URL como nombre del extremo, asegúrese de que se ajusta a las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Una descripción del extremo. No incluya un carácter &lt; porque truncará la descripción mostrada en Workspace.

**Ruta de acceso:** (obligatoria) Especifica la ubicación de la carpeta vigilada. En un entorno en clúster, esta configuración debe apuntar a una carpeta de red compartida a la que se pueda tener acceso desde todos los equipos del clúster.

**Asincrónica:** Identifica el tipo de invocación como asincrónico o sincrónico. El valor predeterminado es asíncrono. Se recomienda asincrónico para procesos de larga duración y sincrónico para procesos transitorios o de corta duración.

**Expresión cron:** Escriba una expresión cron si la carpeta vigilada debe programarse mediante una expresión cron. Cuando se establece esta configuración, se ignora Repetir intervalo.

**Intervalo de repetición:** Intervalo en segundos para analizar la carpeta vigilada para obtener información. A menos que el ajuste Aceleración esté habilitado, el intervalo de repetición debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema puede sobrecargarse. El valor predeterminado es 5. Consulte la descripción del tamaño del lote para obtener más información.

**Recuento de repeticiones:** Número de veces que la carpeta vigilada analiza la carpeta o el directorio. El valor -1 indica un escaneo indefinido. El valor predeterminado es -1.

**Aceleración:** Cuando se selecciona esta opción, limita el número de trabajos de carpetas vigiladas que procesan los formularios AEM Forms en un momento dado. El número máximo de trabajos viene determinado por el valor Tamaño del lote. (Consulte Acerca de la restricción.)

**Nombre de usuario:** (obligatorio) El nombre de usuario que se usa al invocar un servicio de destino desde la carpeta vigilada. El valor predeterminado es SuperAdmin.

**Nombre de dominio:** (obligatorio) El dominio del usuario. El valor predeterminado es DefaultDom.

**Tamaño de lote:** El número de archivos o carpetas que se recogerán por análisis. Utilizar para evitar sobrecargas en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

La configuración Intervalo de repetición y Tamaño de lote determina cuántos archivos recoge la carpeta inspeccionada en cada análisis. La carpeta inspeccionada utiliza un grupo de hilos de Quartz para analizar la carpeta de entrada. El grupo de subprocesos se comparte con otros servicios. Si el intervalo de análisis es pequeño, los subprocesos analizarán la carpeta de entrada con frecuencia. Si los archivos se pierden con frecuencia en la carpeta vigilada, deberá reducir el intervalo de análisis. Si los archivos se pierden con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

Si se pierde un gran volumen de archivos, aumente el tamaño del lote. Por ejemplo, si el servicio invocado por el extremo de la carpeta inspeccionada puede procesar 700 archivos por minuto y los usuarios pueden soltar archivos en la carpeta de entrada a la misma velocidad, al establecer el tamaño del lote en 350 y el intervalo de repetición en 30 segundos, ayudará al rendimiento de la carpeta inspeccionada sin incurrir en el coste de analizar la carpeta inspeccionada con demasiada frecuencia.

Cuando se sueltan los archivos en la carpeta vigilada, se enumeran los archivos en la entrada, lo que puede reducir el rendimiento si la exploración se realiza cada segundo. El aumento del intervalo de análisis puede mejorar el rendimiento. Si el volumen de archivos que se van a soltar es pequeño, ajuste el tamaño del lote y repita el intervalo según corresponda. Por ejemplo, si se sueltan 10 archivos cada segundo, intente establecer el intervalo de repetición en 1 segundo y el tamaño del lote en 10.

**Tiempo de espera:** Tiempo, en milisegundos, que debe esperarse antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3 600 000 milisegundos (una hora) y el archivo se creó hace un minuto, el archivo se recopilará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0.

Esta configuración es útil para asegurarse de que un archivo o carpeta se copia completamente en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y tarda diez minutos en descargarse, establezca el tiempo de espera en 10&amp;ast;60 &amp;ast;1000 milisegundos. Esto evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.

**Patrón de exclusión de archivos:** Lista delimitada por punto y coma **;** de patrones que usa una carpeta vigilada para determinar qué archivos y carpetas analizar y recoger. Ningún archivo o carpeta con este patrón se analizará para su procesamiento.

Esta configuración es útil cuando la entrada es una carpeta con varios archivos. El contenido de la carpeta se puede copiar en una carpeta con un nombre que recogerá la carpeta vigilada. Esto evita que la carpeta inspeccionada recoja una carpeta para procesarla antes de que la carpeta se copie completamente en la carpeta de entrada.

Puede utilizar patrones de archivo para excluir:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Archivos con nombres específicos; por ejemplo, data.&amp;ast; excluiría archivos y carpetas llamados *data1*, *data2*, etc.
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).

**Patrón de archivo de inclusión:** (obligatorio) Lista delimitada por punto y coma **;** de patrones que la carpeta vigilada usa para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si el Patrón de archivo de inclusión es input&amp;ast;, todos los archivos y carpetas que coincidan con input&amp;ast; se recogerán. Esto incluye archivos y carpetas llamados input1, input2, etc.

El valor predeterminado es &amp;ast; e indica todos los archivos y carpetas.

Puede utilizar patrones de archivo para incluir:

* Archivos con extensiones de nombre de archivo específicas; por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Archivos con nombres específicos; por ejemplo, data.&amp;ast; incluiría archivos y carpetas llamados *data1*, *data2*, etc.
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).


**Carpeta de resultados:** Carpeta donde se almacenan los resultados guardados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. Este valor puede ser una ruta absoluta o relativa con los siguientes patrones de archivo:

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

Por ejemplo, si son las 20:00 del 17 de julio de 2009 y especifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la carpeta de resultados es `C:/Test/WF0/failure/2009/07/17/20`.

Si la ruta no es absoluta sino relativa, la carpeta se creará dentro de la carpeta vigilada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta de resultados dentro de la carpeta vigilada. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Cuanto menor sea el tamaño de las carpetas de resultados, mejor será el rendimiento de la carpeta inspeccionada. Por ejemplo, si la carga estimada para la carpeta vigilada es de 1000 archivos cada hora, pruebe un patrón como `result/%Y%M%D%H` para que se cree una nueva subcarpeta cada hora. Si la carga es menor (por ejemplo, 1000 archivos por día), puede utilizar un patrón como `result/%Y%M%D`.

**Conservar carpeta:** Ubicación en la que se almacenan los archivos después de realizar correctamente el análisis y la recogida. La ruta puede ser absoluta, relativa o nula. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados. El valor predeterminado es preserve/%Y/%M/%D/.

**Carpeta de error:** Carpeta donde se guardan los archivos de error. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados.

Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores.

El valor predeterminado es failure/%Y/%M/%D/.

**Conservar si se produce un error:** Conservar archivos de entrada si se produce un error al ejecutar la operación en un servicio. El valor predeterminado es True.

**Sobrescribir nombres de archivo duplicados:** Cuando se establece en True, los archivos de la carpeta de resultados y de la carpeta de conservación se sobrescriben. Cuando se establece en False, se utilizan archivos y carpetas con un sufijo de índice numérico para el nombre. El valor predeterminado es False.

**Duración de purga:** (obligatorio) Los archivos y carpetas de la carpeta de resultados se purgan cuando son anteriores a este valor. Este valor se mide en días. Esta configuración es útil para garantizar que la carpeta de resultados no se llene.

El valor de -1 días indica que nunca se eliminará la carpeta de resultados. El valor predeterminado es -1.

**Nombre de operación:** (obligatorio) Una lista de operaciones que se pueden asignar al extremo de la carpeta vigilada.

**Asignaciones de parámetros de entrada:** Se usa para configurar la entrada necesaria para procesar el servicio y la operación. La configuración disponible depende del servicio que utilice el punto final de la carpeta vigilada. Estos son los dos tipos de entradas:

**Literal:** La carpeta vigilada usa el valor introducido en el campo tal como se muestra. Se admiten todos los tipos básicos de Java. Por ejemplo, si una API utiliza entradas como String, long, int y Boolean, la cadena se convierte al tipo adecuado y se invoca el servicio.

**Variable:** El valor introducido es un patrón de archivo que la carpeta vigilada usa para elegir la entrada. Por ejemplo, si existe el servicio de cifrado de contraseñas, en el que el documento de entrada debe ser un archivo PDF, el usuario puede utilizar &amp;ast;.pdf como patrón de archivo. La carpeta inspeccionada recogerá todos los archivos de la carpeta inspeccionada que coincidan con este patrón e invocará el servicio para cada archivo. Cuando se utiliza una variable, todos los archivos de entrada se convierten en documentos. Solo se admiten las API que utilizan Document como tipo de entrada.

**Asignaciones de parámetros de salida:** Se usa para configurar los resultados del servicio y la operación. La configuración disponible depende del servicio que utilice el punto final de la carpeta vigilada.

La salida de la carpeta inspeccionada puede ser un solo documento, una lista de documentos o un mapa de documentos. Estos documentos de salida se guardan en la carpeta de resultados, utilizando el patrón especificado en Asignación de parámetros de salida.

>[!NOTE]
>
>Especificar nombres que resulten en nombres de archivo de salida únicos mejora el rendimiento. Por ejemplo, considere el caso en el que el servicio devuelve un documento de salida y la Asignación de parámetros de salida lo asigna a `%F.%E` (el nombre de archivo y la extensión del archivo de entrada). En este caso, si los usuarios sueltan archivos con el mismo nombre cada minuto y la carpeta de resultados está configurada en `result/%Y/%M/%D`, y la opción Sobrescribir nombre de archivo duplicado está desactivada, la carpeta inspeccionada intentará resolver los nombres de archivo duplicados. El proceso de resolver nombres de archivo duplicados puede afectar al rendimiento. En este caso, puede mejorar el rendimiento si se cambia la Asignación de parámetros de salida a `%F_%h_%m_%s_%l` para agregar horas, minutos, segundos y milisegundos al nombre o se garantiza que los archivos quitados tengan nombres únicos.

## Acerca de los patrones de archivo {#about-file-patterns}

Los administradores pueden especificar el tipo de archivo que puede invocar un servicio. Se pueden establecer varios patrones de archivo para cada carpeta vigilada. Un patrón de archivo puede ser una de las siguientes propiedades de archivo:

* Archivos con extensiones de nombre de archivo específicas. Por ejemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf
* Archivos con nombres específicos. Por ejemplo, datos.&amp;ast;
* Archivos con expresiones compuestas en el nombre y la extensión, como en estos ejemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

El administrador puede definir el patrón de archivo de la carpeta de salida en la que desea almacenar los resultados. Para las carpetas de salida (resultado, conservar y error), el administrador puede especificar cualquiera de estos patrones de archivo:

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

Por ejemplo, la ruta a la carpeta de resultados puede ser `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Las asignaciones de parámetros de salida también pueden especificar patrones adicionales, como los siguientes:

* %F = Nombre de archivo de origen
* %E = Extensión de nombre de archivo de origen

Si el patrón de asignación de parámetros de salida termina con &quot;File.separator&quot; (que es el separador de rutas), se crea una carpeta y el contenido se copia en esa carpeta. Si el patrón no termina con &quot;File.separator&quot;, el contenido (archivo o carpeta de resultados) se crea con ese nombre. Para obtener más información acerca de las asignaciones de parámetros de salida, vea [Sugerencias y trucos para carpetas vigiladas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## Acerca de la restricción {#about-throttling}

Cuando la restricción está habilitada para un punto final de carpeta de inspección, limita el número de trabajos de carpeta inspeccionada que se pueden procesar en un momento determinado. El número máximo de trabajos está determinado por el valor Tamaño del lote, también configurable en el punto final de la carpeta inspeccionada. Los documentos entrantes en el directorio de entrada de la carpeta vigilada no se sondearán cuando se haya alcanzado el límite de restricción. Los documentos también permanecerán en el directorio de entrada hasta que se completen otros trabajos de carpetas vigiladas y se realice otro intento de encuesta. Si hay procesamiento sincrónico, todos los trabajos procesados en una sola encuesta se contarán hasta el límite de restricción, aunque los trabajos se procesen consecutivamente en un solo hilo.

>[!NOTE]
>
>La restricción no se escala con un grupo. Cuando la restricción está habilitada, el grupo en su conjunto no procesará más del número de trabajos especificado en Tamaño de lote en un momento dado. Este límite es para todo el grupo y no es específico de cada nodo del grupo. Por ejemplo, con un tamaño de lote de 2, se podía alcanzar el límite de restricción con un solo nodo procesando dos trabajos, y ningún otro nodo encuestaría el directorio de entrada hasta que se complete uno de los trabajos.

### Funcionamiento de la restricción {#how-throttling-works}

La carpeta inspeccionada analiza la carpeta de entrada en cada intervalo de repetición, toma el número de archivos especificados en el tamaño del lote e invoca el servicio de destino para cada uno de estos archivos. Por ejemplo, si el tamaño del lote es de cuatro, en cada análisis, la carpeta inspeccionada recogerá cuatro archivos, creará cuatro solicitudes de invocación e invocará el servicio de destino. Antes de que se completen estas solicitudes, si se invoca la carpeta inspeccionada, de nuevo se iniciarán cuatro trabajos, independientemente de si se han completado los cuatro trabajos anteriores.

La restricción impide que la carpeta inspeccionada invoque nuevos trabajos cuando los trabajos anteriores no se completan. La carpeta inspeccionada detectará los trabajos en curso y procesará los nuevos trabajos en función del tamaño del lote menos los trabajos en curso. Por ejemplo, en la segunda invocación, si el número de trabajos completados es solo tres y un trabajo sigue en curso, la carpeta inspeccionada invoca solo tres trabajos más.

* La carpeta inspeccionada depende del número de archivos presentes en la carpeta de fase para averiguar cuántos trabajos hay en curso. Si los archivos permanecen sin procesar en la carpeta de fase, la carpeta inspeccionada no invocará más trabajos. Por ejemplo, si el tamaño del lote es de cuatro y hay tres trabajos paralizados, la carpeta inspeccionada solo invocará un trabajo en invocaciones posteriores. Existen varios escenarios que pueden hacer que los archivos permanezcan sin procesar en la carpeta de fase. Cuando los trabajos están paralizados, el administrador puede finalizar el proceso en la página de administración del flujo de trabajo de Forms para que la carpeta inspeccionada mueva los archivos fuera de la carpeta de fase.
* Si el servidor de Forms se desactiva antes de que la carpeta inspeccionada pueda invocar los trabajos, el administrador puede sacar los archivos de la carpeta de fase. Para obtener más información, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Si el servidor de Forms se está ejecutando pero la carpeta inspeccionada no se está ejecutando cuando el servicio Administrador de trabajos devuelve la llamada, lo que ocurre cuando los servicios no se inician en la secuencia ordenada, el administrador puede sacar los archivos de la carpeta de fase. Para obtener más información, consulte [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Rendimiento y escalabilidad {#performance-and-scalability}

La carpeta inspeccionada puede servir 100 carpetas en total en un solo nodo. El rendimiento de la carpeta inspeccionada depende del rendimiento del servidor de Forms. Para las invocaciones asincrónicas, el rendimiento depende más de la carga del sistema y de los trabajos que están en la cola del Administrador de trabajos.

El rendimiento de la carpeta inspeccionada se puede mejorar añadiendo nodos al clúster. Los trabajos de carpeta inspeccionada se distribuyen entre los nodos del clúster en virtud del programador Quartz y, si hay solicitudes asincrónicas, por el servicio Administrador de trabajos. Todos los trabajos se mantienen en la base de datos.

La carpeta inspeccionada depende del servicio Programador para programar, cancelar la programación y volver a programar los trabajos. Están disponibles otros servicios, como el servicio Administración de eventos, el servicio Administrador de usuarios y el servicio Proveedor de correo electrónico, que comparten el grupo de subprocesos del servicio Programador. Esto puede afectar al rendimiento de la carpeta inspeccionada. El ajuste del grupo de hilos del servicio Planificador será necesario cuando todos los servicios empiecen a utilizarlo.

## Carpetas inspeccionadas en un clúster {#watched-folders-in-a-cluster}

En un clúster, la carpeta inspeccionada depende del programador Quartz y del servicio Administrador de trabajos para el equilibrio de carga y la conmutación por error. Para obtener más información sobre el comportamiento del clúster de Quartz, consulte [Documentación de Quartz](https://www.quartz-scheduler.org/documentation).

La carpeta inspeccionada realiza estas tres tareas principales en cada encuesta:

* Analizar la carpeta
* Invocar el servicio de destinatario
* Gestión de los resultados

El comportamiento del equilibrio de carga y la conmutación por error cambia según si la carpeta vigilada está configurada para la invocación sincrónica o asincrónica.

### Carpeta vigilada sincrónica en un clúster {#synchronous-watched-folder-in-a-cluster}

Para invocaciones sincrónicas, el equilibrador de carga de Quartz decide qué nodo obtendrá el evento de sondeo. El nodo que obtiene el evento de sondeo realizará todas las tareas: analizar la carpeta, invocar el servicio de destino y administrar los resultados.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Para las invocaciones sincrónicas, cuando un nodo falla, el programador de Quartz envía nuevos eventos de sondeo a otros nodos. Las invocaciones iniciadas en el nodo con error se perderán. Para obtener más información acerca de cómo recuperar los archivos asociados con el trabajo fallido, vea [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Carpeta vigilada asincrónica en un clúster {#asynchronous-watched-folder-in-a-cluster}

Para invocaciones asincrónicas, el equilibrador de carga de Quartz decide qué nodo obtendrá el evento de sondeo. El nodo que obtiene el evento de sondeo analizará la carpeta de entrada e invocará el servicio de destino colocando la solicitud en la cola de servicios del Administrador de trabajos. El equilibrador de carga del servicio Administrador de trabajos, a su vez, es responsable de decidir qué nodo procesará la solicitud de invocación. Es posible que aunque el nodo A haya creado la solicitud de invocación, el nodo B termine procesando la solicitud. O el nodo que inició la solicitud de invocación también puede terminar procesando la solicitud.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Para las invocaciones asincrónicas, cuando un nodo falla, el programador de Quartz envía nuevos eventos de sondeo a otros nodos. Las solicitudes de invocación creadas en el nodo con error se incluirán en la cola de servicio del Administrador de trabajos y se enviarán a otros nodos para su procesamiento. Los archivos para los que no se crean solicitudes de invocación permanecerán en la carpeta de fase. Para obtener más información acerca de cómo recuperar los archivos asociados con el trabajo fallido, vea [Puntos de error y recuperación](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Puntos de error y recuperación {#failure-points-and-recovery}

En cada evento de encuesta, la carpeta inspeccionada bloquea la carpeta de entrada, mueve los archivos que coinciden con el patrón de archivo de inclusión a la carpeta de fase y, a continuación, desbloquea la carpeta de entrada. El bloqueo es necesario para que dos subprocesos no recojan el mismo conjunto de archivos y los procesen dos veces. Las posibilidades de que esto ocurra aumentan con un pequeño intervalo de repetición y un gran tamaño de lote. Tras mover los archivos a la carpeta de fase, la carpeta de entrada se desbloquea para que otros hilos puedan analizar la carpeta. Este paso ayuda a proporcionar un alto rendimiento, ya que otros hilos pueden analizar mientras uno procesa los archivos.

Una vez que los archivos se mueven a la carpeta de fase, las solicitudes de invocación se crean para cada archivo y se invoca el servicio de destino. Puede haber casos en los que la carpeta inspeccionada no pueda recuperar los archivos de la carpeta de fase:

* Si el servidor se apaga antes de que la carpeta inspeccionada pueda crear la solicitud de invocación, los archivos de la carpeta de fase permanecen en la carpeta de fase y no se recuperan.
* Si la carpeta inspeccionada ha creado correctamente la solicitud de invocación para cada uno de los archivos de la carpeta de fase y el servidor se bloquea, hay dos comportamientos basados en el tipo de invocación:

**Sincrónica:** Si la carpeta inspeccionada está configurada para invocar el servicio sincrónicamente, todos los archivos de la carpeta de fase permanecen sin procesar en la carpeta de fase.

**Asincrónica:** En este caso, la carpeta inspeccionada depende del servicio Administrador de trabajos. Si el servicio Administrador de trabajos vuelve a llamar a la carpeta inspeccionada, los archivos de la carpeta de fase se mueven a la carpeta de conservación o de errores en función de los resultados de la invocación. Si el servicio Administrador de trabajos no vuelve a llamar a la carpeta inspeccionada, los archivos permanecerán sin procesar en la carpeta de fase. Esta situación ocurre cuando la carpeta inspeccionada no se está ejecutando cuando el administrador de trabajos vuelve a llamar.

### Recuperación de archivos de origen sin procesar en la carpeta de fase {#recovering-unprocessed-source-files-in-the-stage-folder}

Cuando la carpeta inspeccionada no puede procesar los archivos de origen en la carpeta de fase, puede recuperar los archivos sin procesar.

1. Reinicie el servidor de aplicaciones o el nodo.
1. (Opcional) Detenga el procesamiento por parte de la carpeta inspeccionada de nuevos archivos de entrada. Si omite este paso, será mucho más difícil determinar qué archivos no se procesan en la carpeta de fase. Para evitar que la carpeta inspeccionada procese nuevos archivos de entrada, realice una de las siguientes tareas:

   * En Aplicaciones y servicios, cambie el parámetro Patrón de archivo de inclusión del extremo de la carpeta vigilada a algo que no coincida con ninguno de los nuevos archivos de entrada (por ejemplo, escriba `NOMATCH`).
   * Suspenda el proceso que está creando nuevos archivos de entrada.

   Espere hasta que los formularios AEM Forms recuperen y procesen todos los archivos. La mayoría de los archivos deben recuperarse y los nuevos archivos de entrada deben procesarse correctamente. El tiempo que espera para que la carpeta inspeccionada se recupere y procese los archivos dependerá de la duración de la operación que se invoque y del número de archivos que se recuperarán.

1. Determine qué archivos no se pueden procesar. Si ha esperado una cantidad de tiempo adecuada y ha completado el paso anterior, y todavía quedan archivos sin procesar en la carpeta de fase, vaya al paso siguiente.

   >[!NOTE]
   >
   >Puede consultar la marca de fecha y hora de los archivos en el directorio de fase. Según el número de archivos y el tiempo de procesamiento normal, puede determinar qué archivos son lo suficientemente antiguos como para que se consideren atascados.

1. Copie los archivos sin procesar del directorio de fase al directorio de entrada.
1. Si ha impedido que la carpeta inspeccionada procese nuevos archivos de entrada en el paso 2, cambie el patrón de archivo de inclusión a su valor anterior o vuelva a habilitar el proceso que ha deshabilitado.

## Consideraciones de seguridad para carpetas vigiladas {#security-considerations-for-watched-folders}

Cada carpeta vigilada se configura con un nombre de usuario y una contraseña. Estas credenciales se utilizan al invocar los servicios de. La carpeta inspeccionada se basa en el hecho de que la carpeta compartida está protegida con el sistema de archivos de seguridad subyacente para que solo el propietario de la carpeta inspeccionada pueda acceder a la carpeta compartida.

## Sugerencias y trucos para carpetas vigiladas {#tips-and-tricks-for-watched-folders}

Estos son algunos consejos y trucos al configurar el punto final de la carpeta inspeccionada:

* Si tiene una carpeta vigilada en Windows que está procesando archivos de imagen, especifique valores para las opciones Incluir patrón de archivo o Excluir patrón de archivo para evitar que la carpeta vigilada sondee el archivo Thumbs.db generado automáticamente por Windows.
* Si se especifica una expresión cron, se omite el intervalo de repetición. El uso de expresiones cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.
* El tamaño del lote es el número de archivos o carpetas que se recogerán en cada análisis de la carpeta vigilada. Si el tamaño del lote se establece en dos y se sueltan diez archivos o carpetas en la carpeta de entrada de la carpeta vigilada, solo se recogerán dos en cada análisis. En el siguiente análisis, que se realizará después del tiempo especificado en el intervalo de repetición, se recogerán los dos archivos siguientes.
* Para los patrones de archivo, los administradores pueden especificar expresiones regulares con compatibilidad añadida con patrones de comodines para especificar patrones de archivo. La carpeta inspeccionada modifica la expresión regular para admitir patrones de comodines como &amp;ast;.&amp;ast; o &amp;ast;.pdf. Estos patrones de comodines no son compatibles con las expresiones regulares.
* La carpeta inspeccionada analiza la carpeta de entrada en busca de la entrada y no sabe si el archivo o la carpeta de origen se copia completamente en la carpeta de entrada antes de comenzar a procesar el archivo o la carpeta. Para asegurarse de que el archivo o la carpeta de origen se copia completamente en la carpeta de entrada de la carpeta vigilada antes de que se recoja el archivo o la carpeta, realice estas tareas:

   * Usar tiempo de espera, que es el tiempo en milisegundos que la carpeta inspeccionada espera desde la última hora de modificación. Utilice esta función si tiene archivos grandes para procesar. Por ejemplo, si un archivo tarda 10 minutos en descargarse, especifique el tiempo de espera como 10&amp;ast;60 &amp;ast;1000 milisegundos. Esto evitará que la carpeta inspeccionada recoja el archivo si no tiene 10 minutos de antigüedad.
   * Utilice el patrón de archivo de exclusión y el patrón de archivo de inclusión. Por ejemplo, si el patrón de archivo de exclusión es `ex*` y el patrón de archivo de inclusión es `in*`, la carpeta inspeccionada recogerá los archivos que comienzan con &quot;en&quot; y no recogerá los archivos que comienzan con &quot;ex&quot;. Para copiar archivos o carpetas grandes, cambie primero el nombre del archivo o carpeta de modo que el nombre comience por &quot;ex&quot;. Una vez que el archivo o la carpeta denominada &quot;ex&quot; se haya copiado completamente en la carpeta vigilada, cambie su nombre a &quot;in&amp;ast;&quot;.

* Utilice la duración de la depuración para mantener la carpeta de resultados limpia. La carpeta inspeccionada limpia todos los archivos que son anteriores a la duración mencionada en la duración de la depuración. La duración es en días.
* Al agregar un punto final de carpeta inspeccionada, después de seleccionar el nombre de la operación, se rellena la asignación de parámetros de entrada. Para cada entrada de la operación, se genera un campo de asignación de parámetros de entrada. Estos son ejemplos de asignaciones de parámetros de entrada:

   * Para la entrada `com.adobe.idp.Document`: si la operación de servicio tiene una entrada de tipo `Document`, el administrador puede especificar el tipo de asignación como `Variable`. La carpeta inspeccionada recogerá la entrada de la carpeta de entrada de la carpeta inspeccionada en función del patrón de archivo especificado para el parámetro de entrada. Si el administrador especifica `*.pdf` como parámetro, cada archivo que tenga la extensión .pdf se recogerá, se convertirá en `com.adobe.idp.Document` y se invocará al servicio.
   * Para la entrada `java.util.Map`: si la operación de servicio tiene una entrada de tipo `Map`, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.pdf`. Por ejemplo, un servicio necesita un mapa de dos objetos `com.adobe.idp.Document` que representen dos archivos en la carpeta de entrada, como 1.pdf y 2.pdf. La carpeta inspeccionada creará un mapa con la clave como nombre de archivo y el valor como `com.adobe.idp.Document`.
   * Para la entrada `java.util.List`: si la operación de servicio tiene una entrada de tipo Lista, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.pdf`. Cuando se sueltan los archivos PDF en la carpeta de entrada, la carpeta inspeccionada creará una lista de los `com.adobe.idp.Document` objetos que representan estos archivos e invocará el servicio de destino.
   * Para `java.lang.String`: el administrador tiene dos opciones. En primer lugar, el administrador puede especificar el tipo de asignación como `Literal` e introducir un valor de asignación como cadena, como `hello.` La carpeta inspeccionada invocará el servicio con la cadena `hello`. Segundo, el administrador puede especificar el tipo de asignación como `Variable` e introducir un valor de asignación con un patrón como `*.txt`. En este último caso, los archivos con la extensión .txt se leerán como un documento forzado como una cadena para invocar el servicio.
   * Tipo primitivo de Java: el administrador puede especificar el tipo de asignación como `Literal` y proporcionar el valor. La carpeta inspeccionada invocará el servicio con el valor especificado.

* La carpeta inspeccionada está diseñada para trabajar con documentos. Los resultados admitidos son `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node`, y una lista y un mapa de estos tipos. Cualquier otro tipo producirá un resultado de error en la carpeta de errores.
* Si los resultados no están en la carpeta de resultados, compruebe la carpeta de errores para ver si se ha producido un error.
* La carpeta inspeccionada funciona mejor si se utiliza en modo asincrónico. En este modo, la carpeta inspeccionada coloca la solicitud de invocación en la cola y devuelve las llamadas. A continuación, la cola se procesa asincrónicamente. Cuando no se establece la opción Asincrónica, la carpeta inspeccionada invoca el servicio de destino sincrónicamente y el motor de procesos espera hasta que el servicio se realiza con la solicitud y se generan los resultados. Si el servicio de destino tarda mucho tiempo en procesar la solicitud, la carpeta inspeccionada puede obtener errores de tiempo de espera.
* La creación de carpetas vigiladas para operaciones de importación y exportación no permite la abstracción de la extensión del nombre de archivo. Al invocar el servicio de integración de datos de formulario mediante carpetas inspeccionadas, es posible que el tipo de extensión del nombre de archivo del archivo de salida no coincida con el formato de salida deseado para el tipo de objeto de documento. Por ejemplo, si el archivo de entrada a una carpeta inspeccionada que invoca la operación de exportación es un formulario XFA que contiene datos, el resultado debe ser un archivo de datos XDP. Para obtener un archivo de salida con la extensión de nombre de archivo correcta, puede especificarlo en la asignación de parámetros de salida. En este ejemplo, puede utilizar %F.xdp para la asignación de parámetros de salida.
* La carpeta inspeccionada puede procesar archivos de entrada antes de que se copien completamente en la carpeta. El bloqueo de archivos no es obligatorio en UNIX como lo es en Windows. Por este motivo, cuando se copia un archivo en una carpeta inspeccionada, esta puede mover el archivo al escenario sin esperar a que se complete la copia del archivo. Este comportamiento hace que solo se procese una parte del archivo de entrada. Actualmente hay dos soluciones:

   * Solución 1

      1. Especifique un patrón para Excluir patrón de archivo, como temp&amp;ast;.ps.
      1. Copie los archivos que comienzan por temp (por ejemplo, temp1.ps) en la carpeta vigilada.
      1. Una vez que el archivo se haya copiado completamente en la carpeta inspeccionada, cambie el nombre del archivo para que se corresponda con el patrón especificado para Patrón de archivo de inclusión. A continuación, la carpeta inspeccionada mueve el archivo completado al escenario.

   * Solución 2

     Si conoce la cantidad máxima de tiempo que tardará en copiarse los archivos en una carpeta vigilada, especifique el tiempo en segundos para el Tiempo de espera. La carpeta inspeccionada espera el tiempo especificado antes de mover el archivo al escenario.

     Esto no es un problema para los archivos en Windows porque Windows bloquea un archivo cuando un subproceso está escribiendo. Sin embargo, este es un problema para las carpetas en Windows. Para las carpetas, debe seguir los pasos de la Solución 1.

* Si el atributo de extremo Conservar nombre de carpeta para la carpeta inspeccionada se establece en una ruta de directorio nula, el directorio de ensayo no se limpia como debería. El directorio aún contiene el archivo procesado y la carpeta temporal.

## Recomendaciones específicas del servicio para carpetas vigiladas {#service-specific-recommendations-for-watched-folders}

Para todos los servicios, debe ajustar el tamaño del lote y el intervalo de repetición de la carpeta inspeccionada para que la velocidad a la que la carpeta inspeccionada recoge los nuevos archivos y carpetas para su procesamiento no supere la velocidad de los trabajos que puede procesar el servidor de AEM Forms. Los parámetros reales que se van a utilizar pueden variar según la cantidad de carpetas vigiladas configuradas, los servicios que utilicen carpetas vigiladas y la intensidad de los trabajos en el procesador.

### Generar recomendaciones de servicio de PDF {#generate-pdf-service-recommendations}

* El servicio Generate PDF sólo puede convertir un archivo a la vez para estos tipos de archivos: Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® y Adobe PageMaker®. Son trabajos de larga duración; por lo tanto, asegúrese de mantener el tamaño del lote en un valor bajo. Aumente también el intervalo de repetición si hay más nodos en el clúster.
* Para los tipos de archivo de PostScript (PS), PostScript encapsulado (EPS) e imagen, el servicio Generate PDF puede procesar varios archivos en paralelo. Debe ajustar cuidadosamente el tamaño del grupo de inicio de sesión (que gobierna el número de conversiones que se realizarán en paralelo) según la capacidad del servidor y el número de nodos del clúster. A continuación, aumente el tamaño del lote a un número igual al tamaño del grupo de frijoles de sesión para los tipos de archivo que está intentando convertir. La frecuencia de sondeo debe estar dictada por el número de nodos del clúster; sin embargo, como el servicio Generate PDF procesa este tipo de trabajos con bastante rapidez, puede configurar el intervalo de repetición en un valor bajo como 5 o 10.
* Aunque el servicio Generate PDF puede convertir solo un archivo de OpenOffice a la vez, la conversión es bastante rápida. La lógica anterior para PS, EPS y las conversiones de imagen también se aplica a las conversiones de OpenOffice.
* Para habilitar la distribución de carga uniforme en el clúster, mantenga el tamaño del lote bajo y aumente el intervalo de repetición.

### recomendaciones del servicio de formularios con códigos de barras {#barcoded-forms-service-recommendations}

* Para obtener el mejor rendimiento al procesar formularios con códigos de barras (archivos pequeños), escriba `10` para Tamaño de lote y `2` para Intervalo de repetición.
* Cuando se colocan muchos archivos en la carpeta de entrada, pueden producirse errores con archivos ocultos llamados *thumbs.db*. Por lo tanto, se recomienda establecer el Patrón de archivo de inclusión para los archivos de inclusión en el mismo valor especificado para la variable de entrada (por ejemplo, `*.tiff`). Esto evita que la carpeta inspeccionada procese los archivos de base de datos.
* Normalmente, es suficiente un valor de tamaño de lote de `5` y un intervalo de repetición de `2`, porque el servicio de Forms con códigos de barras tarda aproximadamente 0,5 segundos en procesar un código de barras.
* La carpeta inspeccionada no espera a que el motor de procesos finalice el trabajo antes de recoger los nuevos archivos o carpetas. Sigue analizando la carpeta vigilada e invocando el servicio de destino. Este comportamiento puede sobrecargar el motor, lo que provoca problemas de recursos y tiempos de espera. Asegúrese de utilizar el intervalo de repetición y el tamaño del lote para restringir la entrada de la carpeta inspeccionada. Puede aumentar el intervalo de repetición y reducir el tamaño del lote si existen más carpetas vigiladas o habilitar la restricción en el extremo. Para obtener información sobre la restricción, consulte [Acerca de la restricción](configuring-watched-folder-endpoints.md#about-throttling).
* La carpeta inspeccionada suplanta al usuario especificado en el nombre de usuario y el nombre de dominio. La carpeta inspeccionada invoca el servicio como este usuario si se invoca directamente o si el proceso es de corta duración. Para un proceso de larga duración, el proceso se invoca con el contexto System. Los administradores pueden establecer directivas del sistema operativo para la carpeta inspeccionada a fin de determinar a qué usuario permitir o denegar el acceso.
* Utilice patrones de archivo para organizar carpetas de resultados, errores y conservación. (Consulte [Acerca de los patrones de archivo](configuring-watched-folder-endpoints.md#about-file-patterns).)

* La carpeta inspeccionada depende del programador de Quartz para analizar las carpetas inspeccionadas. El programador Quartz tiene un grupo de hilos para analizarlos. Si el intervalo de repetición para la carpeta vigilada es muy bajo (&lt; 5 segundos) y el tamaño del lote es alto (> 2), puede producirse una condición de carrera. Cuando se produce esta condición, dos subprocesos de Quartz recogen un archivo:

   * Uno de los subprocesos encuentra correctamente el archivo e invoca el servicio de destino con el archivo.
   * El segundo subproceso ve el archivo pero falla cuando intenta averiguar si es válido (archivo de lectura o escritura), lo que provoca errores falsos que indican que el archivo no se puede procesar porque es de sólo lectura. Esto solo sucede con un intervalo de repetición bajo y un tamaño de lote alto.
