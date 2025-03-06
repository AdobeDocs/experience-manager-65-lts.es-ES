---
title: Evaluación de la complejidad de la actualización con AEM Analyzer
description: Aprenda a utilizar AEM Analyzer para evaluar la complejidad de la actualización.
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 87c30912-c89a-42f1-b37b-ec439e7318c7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 15%

---

# Evaluación de la complejidad de la actualización con AEM Analyzer {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## Información general {#overview}

AEM 6.5 LTS Analyzer proporciona una evaluación de su implementación actual de AEM indicando las áreas que es necesario actualizar para proporcionar una experiencia de actualización perfecta a 6.5 LTS.

La herramienta genera un informe que identifica las áreas de posible refactorización.

## Informe de AEM 6.5 LTS Analyzer {#aem-65lts-analyzer-report}

El informe de AEM 6.5 LTS Analyzer se utiliza para obtener una comprensión de alto nivel de la preparación general para la actualización. El informe consiste en categorías de problemas que deben abordarse para garantizar una actualización correcta a AEM 6.5 LTS.

El informe de AEM 6.5 LTS Analyzer incluye las siguientes categorías:

* Funcionalidad de la aplicación que se debe refactorizar.
* Elementos de repositorio que deben moverse a una ubicación admitida.
* Problemas de configuración
* Funciones de AEM 6.5 que se han eliminado con nuevas funciones o que actualmente no son compatibles con AEM 6.5 LTS
* Eliminar el uso de la API de Java y Guava

Se proporciona información adicional acerca de las categorías y posibles implicaciones y soluciones asociadas con dichas categorías mediante vínculos desde el informe de AEM 6.5 LTS Analyzer.

## Disponibilidad {#analyzer-availability}

AEM Analyzer se puede descargar como archivo zip desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Puede instalar el paquete mediante [Administrador de paquetes](/help/sites-administering/package-manager.md) en la instancia de AEM de origen.

## Consideraciones importantes sobre el uso de AEM Analyzer {#important-considerations-for-using-aem-analyzer}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar AEM Analyzer:

* El informe del analizador se ha creado con los resultados de AEM [Pattern Detector](/help/sites-deploying/pattern-detector.md). La versión de Pattern Detector utilizada por Analyzer se incluye en el paquete de instalación de AEM Analyzer
* Solo el usuario **admin** o un usuario del grupo **administradores** pueden ejecutar AEM Analyzer
* El analizador es compatible con instancias de AEM de la versión 6.5 y posteriores.

>[!NOTE]
>
>Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar AEM Analyzer en un entorno de ensayo lo más cercano posible al entorno de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de Author de producción.

* La generación del contenido de los informes de AEM Analyzer puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores
* Debido al tiempo considerable que puede ser necesario para generar el contenido del informe, se genera mediante un proceso en segundo plano y se almacena en caché. Ver y descargar el informe debería ser relativamente rápido, ya que utiliza la caché de contenido hasta que caduque o hasta que el informe se actualice de forma explícita. Durante la generación del contenido del informe, puede cerrar la pestaña del explorador y regresar más tarde para ver el informe una vez que su contenido esté disponible en la caché.

## Visualización del informe de AEM Analyzer {#viewing-the-aem-analyzer-report}

Siga los pasos a continuación para ver el informe de AEM Analyzer:

1. Seleccione Adobe Experience Manager y vaya a **Herramientas - Operaciones - Modernizador de LTS 6.5**

   ![Ver informe de analizador 1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. Haga clic en **AEM 6.5 LTS Analyzer** para abrirlo

   ![Ver informe de analizador 2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. Haga clic en **Generar informe** para ejecutar AEM Analyzer

   ![Ver informe de analizador 3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. Mientras AEM Analyzer genera el informe, puede ver en pantalla el progreso realizado por la herramienta. Muestra el progreso en términos del porcentaje completado. También muestra el número de elementos analizados y el número de conclusiones

   ![Ver informe de analizador 4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. Una vez generado el informe de 6.5 LTS Analyzer, muestra un resumen y la cantidad de conclusiones en un formato tabular organizado por el tipo de búsqueda y el nivel de importancia. Para obtener más detalles sobre una búsqueda determinada, puede hacer clic en el número que corresponda al tipo de búsqueda de la tabla

   ![Ver informe de analizador 5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. Tiene la opción de descargar el informe en formato de valores separados por comas (CSV) haciendo clic en **Exportar a CSV**. Puede forzar al analizador a borrar su caché y regenerar el informe haciendo clic en **Actualizar informe**. Si la caché caduca, debe volver a generar el informe.

## Interpretación del informe de AEM Analyzer {#interpreting-the-aem-analyzer-report}

Cuando la herramienta Analizador de 6.5 LTS se ejecuta en la instancia de AEM, el informe se muestra en los resultados de la ventana de herramientas.

El formato del informe es el siguiente:

* **Información general del informe**: información sobre el informe que incluye lo siguiente:

   * **Hora del informe**: Cuando se generó el contenido del informe y se puso a disposición por primera vez
   * **Hora de caducidad**: cuando caduque la caché de contenido del informe
   * **Período de tiempo de generación**: Cantidad de tiempo en que se generó el informe
   * **Recuento de búsqueda**: El número total de resultados incluidos en el informe

* **Información general del sistema**: Información sobre el sistema AEM en el que se ejecutó el analizador
* **Búsqueda de categorías**: varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: nombre de la categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

  ![Resumen del informe del analizador](/help/sites-deploying/assets/analyzer-report-summary.png)

  Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción.

>[!NOTE]
>
>Para obtener más información sobre cada categoría de búsqueda, consulte [Categorías de Pattern Detector](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso).

Para comprender los niveles de importancia, siga la tabla siguiente:

| Importancia | Descripción |
|---|---|
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este resultado es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |

## Interpretación del informe CSV de AEM 6.5 LTS Analyzer {#interpreting-the-aem-65lts-analyzer-report}

Al hacer clic en la opción **CSV** desde la instancia de AEM, el formato CSV del informe del analizador se crea desde la caché de contenido y se devuelve al explorador. Según la configuración del explorador, este informe se descarga automáticamente como archivo con el nombre predeterminado `report.csv`.

Si la caché ha caducado, el informe se regenera antes de crear y descargar el archivo CSV.

El formato CSV del informe incluye información que se genera a partir de los resultados de Pattern Detector, ordenados y organizados por tipo de categoría, subtipo y nivel de importancia. Su formato es adecuado para visualizarlo y editarlo en una aplicación como Microsoft Excel. Su finalidad es proporcionar toda la información de búsqueda en un formato repetible que pueda resultar útil al comparar los informes a lo largo del tiempo para medir el progreso.

Las columnas del informe de formato CSV son las siguientes:

* **Código**: el código de categoría.
* **Tipo**: el nombre de la categoría.
* **Subtipo**: subtipo de categoría.
* **Importancia**: el nivel de importancia.
* **Identificador**: el identificador principal de la búsqueda.
* **Mensaje**: el mensaje proporcionado para la búsqueda.
* **Contexto**: una cadena JSON de búsqueda de datos.

El valor &quot;`\N`&quot; en una columna para una búsqueda individual indica que no se proporcionaron datos.

## Interfaz HTTP {#http-interface}

El analizador LTS 6.5 proporciona una interfaz HTTP que puede utilizarse como alternativa a su interfaz de usuario en AEM. La interfaz admite comandos `HEAD` y `GET`. Se puede utilizar para generar el informe del analizador y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

Las siguientes direcciones URL están disponibles para el acceso HTTP, donde `<host>` es el nombre de host, junto con el puerto si es necesario, del servidor en el que está instalado el analizador:

* `http://<host>/apps/aem66-analyzer/analysis/report.json` para el formato JSON
* `http://<host>/apps/aem66-analyzer/analysis/report.csv` para el formato CSV
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv` para el formato TSV

### Ejecución de una solicitud HTTP {#executing-an-http-request}

Una forma sencilla de ejecutar una solicitud HTTP es abrir una pestaña en el mismo explorador en el que ya ha iniciado sesión en AEM como administrador. Puede escribir la dirección URL en la pestaña del explorador y mostrar o descargar los resultados.

También puede utilizar una herramienta de línea de comandos como `curl` o `wget` y cualquier aplicación cliente HTTP. Cuando no utilice una pestaña de explorador con una sesión autenticada, debe proporcionar el nombre de usuario y la contraseña de administración como parte del comentario.

A continuación se muestra un ejemplo de cómo se puede realizar esto:

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## Ajuste de la duración de caché {#adjusting-the-cache-lifetime}

La duración predeterminada de la caché del Analizador LTS de AEM 6.5 es de 24 horas. Con la opción para actualizar un informe y regenerar la caché, tanto en la instancia de AEM como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del analizador LTS de AEM 6.5. Si el tiempo de generación de informes es especialmente largo para la instancia de AEM, es posible que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de caché se almacena como la propiedad `maxCacheAge` en el siguiente nodo de repositorio:

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante CRX/DE Lite.

## Uso del transformador de contenido {#using-content-transformer}

### Disponibilidad {#content-transformer-availability}

El transformador de contenido está incorporado al analizador LTS de AEM 6.5, que se puede descargar como archivo zip desde el portal de distribución de software.

### Consideraciones importantes sobre el uso del transformador de contenido {#important-considerations-for-using-content-transformer}

Consulte la sección siguiente para comprender las consideraciones importantes al utilizar el transformador de contenido (CT):

* Para utilizar el transformador de contenido, primero debe ejecutar AEM Analyzer en el entorno de AEM
* Aunque puede ejecutar el transformador de contenido en el entorno de producción, se recomienda ejecutar el transformador de contenido en un clon del entorno de producción. Y lo que es más importante, debe asegurarse de que el AEM Analyzer y la TC se ejecuten en el mismo entorno
* Debe ser administrador en el entorno en el que desea ejecutar el transformador de contenido
* Una operación de eliminación que puede cambiar el contenido de origen creará un paquete de copia de seguridad de las rutas de origen bajo `/etc/packages/modernizer-content-transformation` de forma predeterminada antes de la transformación. Aunque el cuadro de diálogo de operación de eliminación tiene una opción para deshabilitar o habilitar la creación del paquete de copia de seguridad, se recomienda encarecidamente tener siempre seleccionada la opción de habilitar la creación del paquete
* Cada página del transformador de contenido está configurada para enumerar un máximo de 50 conclusiones. Por lo tanto, se pueden transformar un máximo de 50 hallazgos a la vez. Esto se hace para proporcionar una respuesta oportuna en la interfaz de usuario de.

### Abrir el transformador de contenido {#opening-the-content-transformer}

1. Inicie sesión en la instancia de AEM de origen como administrador y vaya a la página de inicio en *https://host:port/aem/start.htm*
1. Vaya a **Herramientas - Operaciones - Modernizador de 6.5 LTS**

   ![Abriendo transformador de contenido 1](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. Haga clic en la tarjeta **Transformador de contenido para 6.5 LTS Analyser report**

   ![Abriendo transformador de contenido 2](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. Si no se genera el informe de Analyser, la página **Transformar contenido** mostrará **Ningún informe**. El mismo mensaje **Sin informe** también aparecerá si se han eliminado todos los resultados relacionados con el contenido

   ![Abriendo transformador de contenido 3](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. A continuación se muestra un ejemplo del aspecto que tendrá la página Información general del transformador de contenido si la creación del informe de AEM Analyzer se ha realizado correctamente y si ha encontrado problemas relacionados con el contenido.

El tiempo de caducidad que queda para el informe de AEM Analyzer se muestra en la barra lateral. Se recomienda ejecutar el transformador de contenido con el último informe de AEM Analyzer para evitar perder cualquier resultado relacionado con el contenido

![Abriendo transformador de contenido 4](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. Puede filtrar los problemas en función del código de patrón, el subtipo, la importancia y Source

   ![Abriendo transformador de contenido 5](/help/sites-deploying/assets/opening-content-transformer-5.png)

### Eliminación de rutas {#removing-paths}

1. Puede seleccionar todos los problemas o problemas específicos y seleccionar **Eliminar** para resolverlos

   ![Eliminando rutas 1](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >Una operación Remove crea de forma predeterminada un paquete de copia de seguridad de las rutas de acceso de origen bajo `/etc/packages/modernizer-content-transformation`, antes de la transformación. Aunque el cuadro de diálogo de operación de eliminación tiene una opción para deshabilitar o habilitar la creación del paquete de copia de seguridad, se recomienda encarecidamente tener siempre seleccionada la opción de habilitar la creación del paquete.

   ![Eliminando rutas 2](/help/sites-deploying/assets/removing-paths-2.png)

1. A continuación, se muestra un ejemplo de un paquete de copia de seguridad creado para la operación de eliminación de las rutas. Puede hacer clic en **Instalar** para recuperar las rutas de origen

   ![Eliminando rutas 3](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >No elimine `/etc/packages/modernizer-content-transformation`, ya que es la ubicación donde residen los paquetes de copia de seguridad. Puede eliminar esta ubicación para reducir el tamaño del repositorio solo cuando esté seguro de que ya no necesita estos paquetes.

1. De forma opcional, puede empaquetar conclusiones de contenido seleccionadas para su uso futuro. Para ello, seleccione los resultados que desee incluir y luego haga clic en **Paquete** en la parte superior izquierda. Escriba un nombre de paquete, elija una ruta de paquete y haga clic en el botón **Paquete** para completar el proceso.

   ![Eliminando rutas 3](/help/sites-deploying/assets/removing-paths-4.png)

### Problemas conocidos {#known-issues}

* En ocasiones, la operación Quitar puede mostrar la notificación: *&quot;Algunas rutas no se quitaron correctamente, compruebe los registros e inténtelo de nuevo.*&quot;. Sin embargo, si las rutas se eliminaron, puede ignorar este mensaje de forma segura
* Del mismo modo, la operación del paquete puede fallar con el siguiente error: *&quot;Error al realizar la operación deseada, compruebe los registros e inténtelo de nuevo.*&quot;. Es probable que se deba a la caducidad de la sesión. En estos casos, el problema se debe resolver reintentando la operación.
