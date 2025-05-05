---
title: Crear o configurar una carpeta vigilada
description: Obtenga información sobre cómo crear o eliminar una carpeta vigilada, o modificar las propiedades de una existente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 94%

---

# Crear o configurar una carpeta vigilada {#create-or-configure-a-watched-folder}

Un administrador puede configurar una carpeta de red, conocida como *carpeta vigilada*, de modo que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se inicie una operación preconfigurada y se manipule el archivo. Una vez realizada la operación especificada, la operación guardará el archivo modificado en una carpeta de salida especificada. Para obtener información detallada sobre la administración de una carpeta vigilada, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puede utilizar la interfaz de usuario de la carpeta vigilada para lo siguiente:

* Crear una carpeta vigilada
* Modificar propiedades de una carpeta vigilada existente
* Eliminar una carpeta vigilada

## Crear una carpeta vigilada {#create-a-watched-folder}

Antes de configurar una carpeta vigilada, asegúrese de lo siguiente:

* Las carpetas vigiladas son una característica avanzada de AEM Forms. Requiere un paquete de complementos de AEM Forms para funcionar. Asegúrese de que el paquete adecuado de complementos de AEM Forms esté instalado y configurado.
* Puede crear la carpeta vigilada en un almacenamiento compartido o local. Asegúrese de que el usuario de AEM Forms configurado para ejecutar la carpeta vigilada tenga permisos de lectura y escritura en la carpeta vigilada.
* Puede utilizar un servicio, un flujo de trabajo o un script para automatizar una operación con una carpeta vigilada. Asegúrese de que el servicio, el flujo de trabajo o el script correspondiente estén creados y listos para ejecutarse. Para obtener información sobre la creación de un servicio, un flujo de trabajo o un script, consulte [Varios métodos de procesar archivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una carpeta vigilada tiene varias propiedades, consulte [Propiedades de las carpetas vigiladas](watched-folder-in-aem-forms.md#watchedfolderproperties).

Realice los siguientes pasos para crear una carpeta vigilada:

1. Seleccione el icono **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Seleccione **Herramientas** > **Forms** > **Configurar carpeta inspeccionada.** Se mostrará una lista de las carpetas vigiladas ya configuradas.
1. Seleccione **Nuevo**. Se mostrará una lista de los campos necesarios para crear la carpeta vigilada:

   * **Nombre**: identifica la carpeta vigilada. Utilice solo caracteres alfanuméricos para el nombre.
   * **Ruta**: especifica la ubicación de la carpeta vigilada. En un entorno de clúster, esta configuración debe apuntar a una carpeta de red compartida a la que puedan acceder todos los usuarios que ejecuten AEM en diferentes nodos de un clúster.
   * **Procesar archivos mediante**: tipo de proceso que se va a iniciar. Puede especificar el flujo de trabajo, el script o el servicio.
   * **Nombre del servicio/Ruta de script/Ruta del flujo de trabajo**: el comportamiento del campo se basa en el valor especificado para el campo **Procesar archivos mediante**. Puede especificar los siguientes valores:

      * Para Flujo de trabajo, especifique el modelo del flujo de trabajo que se va a ejecutar. Por ejemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Para Script, especifique la ruta JCR del script que se va a ejecutar. Por ejemplo, /etc/watchfolder/test/testScript.ecma
      * En Servicio, especifique el filtro utilizado para localizar un servicio OSGi. El servicio está registrado como una implementación de la interfaz com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Por ejemplo, el siguiente código es una implementación personalizada de la interfaz ContentProcessor con una propiedad personalizada (foo=bar).

   >[!NOTE]
   >
   >Si ha seleccionado **Servicio** para el campo **Procesar archivos mediante**, el valor del campo Nombre del servicio (inputProcessorType) debe incluirse entre paréntesis. Por ejemplo (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Patrón del archivo de salida**: especifique una lista delimitada por punto y coma (;) de patrones que usa una carpeta vigilada para determinar el nombre y la ubicación de los archivos y carpetas de salida. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. Seleccione **Avanzado**. La pestaña Avanzadas contiene más campos. La mayoría de estos campos contienen un valor predeterminado.

   * **Filtro de asignador de cargas útiles:** cuando se crea una carpeta vigilada, se crea una estructura de carpetas dentro de la carpeta que se ve. La estructura de carpetas tiene carpetas de fase, resultado, conservación, entrada y error. La estructura de carpetas puede servir como carga útil de entrada al flujo de trabajo y aceptar la salida de un flujo de trabajo. También puede enumerar los puntos de error, si los hay. La estructura de una carga útil es diferente de la de una carpeta vigilada. Puede escribir scripts personalizados para asignar la estructura de una carpeta vigilada a la carga útil. Este script se denomina filtro de asignador de cargas útiles. Hay dos implementaciones de asignador de carga útil listas para usar. Si no tiene [una implementación personalizada](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilice una predeterminada:

      * **Asignador predeterminado:** utilice el asignador de cargas útiles predeterminado para mantener el contenido de entrada y salida de las carpetas vigiladas en carpetas de entrada y salida independientes en la carga útil.
      * **Asignador de cargas útiles basado en archivos simples:** utilice el asignador de cargas útiles basado en archivos simples para mantener el contenido de entrada y salida directamente en la carpeta de carga útil. No crea ninguna jerarquía adicional, como el asignador predeterminado.

   * **Modo de ejecución**: especifique la lista separada por comas de modos de ejecución permitidos para ejecutar el flujo de trabajo.
   * **Tiempo de espera agotado: archivos clasificados después**: especifique el número de segundos que hay que esperar antes de que un archivo o carpeta de entrada que ya se haya seleccionado para el procesamiento se trate como si se hubiera agotado el tiempo de espera y se marque como un error. El mecanismo de tiempo de espera solo se activa cuando el valor de esta propiedad es un número positivo.
   * **Eliminar archivos clasificados con tiempo de espera agotado al acelerarlos**: si está habilitado, el mecanismo **Tiempo de espera agotado: archivos clasificados después** se activará solo cuando se active la restricción para la carpeta vigilada.
   * **Analizar carpeta de entrada después de cada:** especifique el intervalo de tiempo, en segundos, para buscar entradas en la carpeta vigilada. A menos que el ajuste Aceleración esté habilitado, el intervalo de sondeo debe ser mayor que el tiempo para procesar un trabajo promedio; de lo contrario, el sistema podría sobrecargarse. El valor del intervalo debe ser mayor o igual a uno.
   * **Patrón de exclusión de archivos**: especifique una lista delimitada por punto y coma (;) de patrones que usa una carpeta vigilada para determinar qué archivos y carpetas analizar y recoger. Ningún archivo o carpeta con el patrón especificado se analizará para su procesamiento. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Patrón de archivo de inclusión**: especifique una lista delimitada por punto y coma (;) de patrones que la carpeta vigilada usa para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si el Patrón de archivo de inclusión es input&ast;, todos los archivos y carpetas que coincidan con input&ast; se recogerán. El valor predeterminado es &ast; e indica todos los archivos y carpetas. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tiempo de espera:** especifique el tiempo, en milisegundos, a esperar antes de analizar una carpeta o archivo después de crearlo. Por ejemplo, si el tiempo de espera es de 3 600 000 milisegundos (una hora) y el archivo se creó hace un minuto, el archivo se recopilará después de que hayan transcurrido 59 minutos o más. El valor predeterminado es 0.

     Esta configuración es útil para asegurarse de que todo el contenido del archivo o la carpeta se copia en la carpeta de entrada. Por ejemplo, si tiene un archivo grande para procesar y tarda diez minutos en descargarse, establezca el tiempo de espera en 10&ast;60 &ast;1000 milisegundos. Este intervalo evita que la carpeta vigilada analice el archivo si no tiene diez minutos de antigüedad.

   * **Eliminar resultados anteriores a:** especifique el tiempo, en número de días, a esperar antes de eliminar los archivos y carpetas anteriores al valor especificado. Esta configuración es útil para garantizar que la carpeta de resultados no se llene. El valor de -1 días indica que nunca se eliminará la carpeta de resultados. El valor predeterminado es -1.
   * **Nombre de la carpeta de resultados:** especifique el nombre de la carpeta para almacenar los resultados. Si los resultados no aparecen en esta carpeta, compruebe la carpeta de errores. Los archivos de solo lectura no se procesan y se guardan en la carpeta de errores. Puede utilizar una ruta absoluta o relativa con los siguientes patrones de archivo:

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
      * Por ejemplo, si son las 20:00 del 17 de julio de 2009 y especifica C:/Test/WF0/failure/%Y/%M/%D/%H/, la carpeta de resultados es C:/Test/WF0/failure/2009/07/17/20.
      * Si la ruta no es absoluta sino relativa, la carpeta se creará dentro de la carpeta vigilada. El valor predeterminado es result/%Y/%M/%D/, que es la carpeta de resultados dentro de la carpeta vigilada. Para obtener más información sobre los patrones de archivo, consulte [Información sobre los patrones de archivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **Nombre de la carpeta de errores:** especifique la carpeta en la que se guardan los archivos con errores. Esta ubicación siempre es relativa a la carpeta vigilada. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados.
   * **Conservar nombre de carpeta:** especifique la carpeta en la que se almacenan los archivos después de realizar el análisis y la recogida correctamente. La ruta puede ser un directorio absoluto, relativo o nulo. Puede utilizar patrones de archivo, tal como se describe para la carpeta Resultados. El valor predeterminado es preserve/%Y/%M/%D/.
   * **Tamaño del lote:** especifique el número de archivos o carpetas que se recogerán por análisis. Evita una sobrecarga en el sistema; el análisis de demasiados archivos al mismo tiempo puede provocar un bloqueo. El valor predeterminado es 2.

     Si el intervalo de análisis es pequeño, los subprocesos analizan la carpeta de entrada con frecuencia. Si los archivos se pierden con frecuencia en la carpeta vigilada, deberá reducir el intervalo de análisis. Si los archivos se pierden con poca frecuencia, utilice un intervalo de exploración mayor para que los demás servicios puedan utilizar los subprocesos.

   * **Acelerador activado:** cuando esta opción está habilitada, limita el número de trabajos de carpetas vigiladas que procesa AEM Forms en un momento dado. El valor Tamaño de lote determina el número máximo de trabajos. Para obtener más información, consulte [acelerador](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sobrescribir archivos existentes con un nombre similar**: cuando se establece en True, los archivos de la carpeta de resultados y de la carpeta de preservación se sobrescribirán. Cuando se establece en False, se utilizan archivos y carpetas con un sufijo de índice numérico para el nombre. El valor predeterminado es False.
   * **Conservar archivos en caso de error:** Cuando se establece en True, los archivos de entrada se conservan en caso de error. El valor predeterminado es True.
   * **Incluir archivos con patrón:** especifique una lista delimitada por punto y coma (;) de patrones que la carpeta vigilada usa para determinar qué carpetas y archivos analizar y recoger. Por ejemplo, si se introduce el Patrón de archivo de inclusión, se recogerán todos los archivos y carpetas que coincidan con la entrada. Para obtener más información, consulte [Ayuda de administración](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Invocar la carpeta vigilada asincrónicamente:** identifica el tipo de invocación como asíncrono o sincrónico. El valor predeterminado es asíncrono. Se recomienda asincrónico para procesos de larga duración y sincrónico para procesos transitorios o de corta duración.
   * **Habilitar carpeta vigilada:** cuando esta opción está habilitada, la carpeta vigilada está habilitada. El valor predeterminado es True.

## Modificar propiedades de una carpeta vigilada existente {#modify-properties-of-an-existing-watched-folder}

Además de cambiar el nombre de la carpeta vigilada, puede modificar todas las propiedades de una carpeta vigilada existente. Realice los siguientes pasos para modificar las propiedades de una carpeta vigilada existente:

1. Seleccione el icono **Adobe Experience Manager** en la esquina superior izquierda de la pantalla.
1. Seleccione **Herramientas** > **Forms** > **Configurar carpeta inspeccionada.** Se mostrará una lista de las carpetas vigiladas ya configuradas.
1. En la parte izquierda de la pantalla Carpeta vigilada, seleccione la carpeta vigilada y seleccione **Editar.** Se mostrará una lista de los campos necesarios para crear la carpeta vigilada. Los campos enumerados en la pestaña **Básico** son obligatorios. La pestaña Avanzadas contiene más campos. La mayoría de estos campos contienen un valor predeterminado. Puede modificar estas propiedades según sus necesidades.
1. Después de modificar las propiedades, seleccione **Actualizar**. Las propiedades modificadas se guardarán.
