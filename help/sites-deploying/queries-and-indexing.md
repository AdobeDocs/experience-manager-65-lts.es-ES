---
title: Consultas e indexación de Oak
description: Obtenga información sobre cómo configurar índices en Adobe Experience Manager (AEM) 6.5 LTS.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 432fc767-a6b8-48f8-b124-b13baca51fe8
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 1%

---

# Consultas e indexación de Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Este artículo trata sobre la configuración de índices en AEM 6.5 LTS. Para obtener prácticas recomendadas sobre cómo optimizar el rendimiento de consultas e indexación, consulte [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introducción {#introduction}

A diferencia de Jackrabbit 2, Oak no indexa el contenido de forma predeterminada. Se deben crear índices personalizados cuando sea necesario, como con las bases de datos relacionales tradicionales. Si no hay ningún índice para una consulta específica, es posible que se atraviesen muchos nodos. La consulta puede seguir funcionando, pero es probable que sea lenta.

Si Oak encuentra una consulta sin índice, se imprime un mensaje de registro de nivel WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Idiomas de consulta admitidos {#supported-query-languages}

El motor de consultas de Oak es compatible con los siguientes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipos de indexador y cálculo de costes {#indexer-types-and-cost-calculation}

El back-end basado en Apache Oak permite que diferentes indexadores se conecten al repositorio.

Un indizador es **Property Index**, cuya definición de índice se almacena en el propio repositorio.

La implementación para **Apache Lucene** está disponible de manera predeterminada, y admite la indexación de texto completo.

Se usa el **índice de recorrido** si no hay ningún otro indizador disponible. Esto significa que el contenido no está indexado y que los nodos de contenido se atraviesan para encontrar coincidencias con la consulta.

Si hay varios indexadores disponibles para una consulta, cada indexador disponible calcula el coste de ejecución de la consulta. A continuación, Oak elige el indexador con el coste estimado más bajo.

![chlimage_1-148](assets/chlimage_1-148.png)

El diagrama anterior es una representación de alto nivel del mecanismo de ejecución de consultas de Apache Oak.

En primer lugar, la consulta se analiza en un árbol de sintaxis abstracta. A continuación, se comprueba la consulta y se transforma en SQL-2, que es el idioma nativo para las consultas de Oak.

A continuación, se consulta cada índice para estimar el coste de la consulta. Una vez completado este paso, se recuperan los resultados del índice más barato. Finalmente, los resultados se filtran, tanto para garantizar que el usuario actual tenga acceso de lectura al resultado como para que el resultado coincida con la consulta completa.

## Configuración de los índices {#configuring-the-indexes}

>[!NOTE]
>
>Para un repositorio grande, crear un índice es una operación que requiere mucho tiempo. Esto es así tanto para la creación inicial de un índice como para la reindexación (reconstrucción de un índice después de cambiar la definición). Vea también [Solución de problemas de índices Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) y [Prevención de la reindexación lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Si es necesario reindexar en repositorios grandes, especialmente cuando se utiliza MongoDB y para índices de texto completo, considere la preextracción de texto y el uso de oak-run para crear el índice inicial y reindexar.

Los índices se configuran como nodos en el repositorio bajo el nodo **Oak:index**.

El tipo del nodo de índice debe ser **oak:QueryIndexDefinition.** Hay varias opciones de configuración disponibles para cada indizador como propiedades de nodo. Para obtener más información, consulte los detalles de configuración de cada tipo de indizador a continuación.

### El índice de propiedades {#the-property-index}

El índice de propiedades es útil para consultas que tienen restricciones de propiedad pero no son de texto completo. Se puede configurar siguiendo el siguiente procedimiento:

1. Abra CRXDE yendo a `http://localhost:4502/crx/de/index.jsp`
1. Cree un nodo en **oak:index**
1. Asigne un nombre al nodo **PropertyIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Establezca las siguientes propiedades para el nuevo nodo:

   * **tipo:** `property` (de tipo cadena)
   * **propertyNames:** `jcr:uuid` (de tipo Nombre)

   En este ejemplo concreto se indiza la propiedad `jcr:uuid`, cuyo trabajo consiste en exponer el identificador único universal (UUID) del nodo al que está asociada.

1. Guarde los cambios.

El índice de propiedades tiene las siguientes opciones de configuración:

* La propiedad **type** especifica el tipo de índice y, en este caso, debe establecerse en **property**

* La propiedad **propertyNames** indica la lista de propiedades almacenadas en el índice. En caso de que falte, el nombre del nodo se utiliza como valor de referencia del nombre de propiedad. En este ejemplo, la propiedad **jcr:uuid**, cuyo trabajo es exponer el identificador único (UUID) de su nodo, se agrega al índice.

* El indicador **unique** que, si se establece en **true** agrega una restricción de unicidad en el índice de propiedad.

* La propiedad **declaringNodeTypes** permite especificar un tipo de nodo determinado al que el índice sólo se aplica.
* El indicador **reindex** que, si se establece en **true**, déclencheur un reíndice de contenido completo.

### El índice ordenado {#the-ordered-index}

El índice ordenado es una extensión del índice de propiedad. Sin embargo, ha quedado obsoleto. Los índices de este tipo deben reemplazarse con el [índice de propiedades Lucene](#the-lucene-property-index).

### Índice de texto completo de Lucene {#the-lucene-full-text-index}

Un indexador de texto completo basado en Apache Lucene está disponible en AEM 6.5 LTS.

Si se configura un índice de texto completo, todas las consultas que tienen una condición de texto completo utilizan el índice de texto completo, independientemente de si hay otras condiciones que están indizadas y de si hay una restricción de ruta.

Si no se configura ningún índice de texto completo, las consultas con condiciones de texto completo no funcionan según lo esperado.

Dado que el índice se actualiza mediante un subproceso en segundo plano asincrónico, algunas búsquedas de texto completo no están disponibles durante un período de tiempo breve hasta que finalizan los procesos en segundo plano.

Puede configurar un índice de texto completo de Lucene siguiendo el siguiente procedimiento:

1. Abra CRXDE y cree un nodo en **oak:index**.
1. Asigne un nombre al nodo **LuceneIndex** y establezca el tipo de nodo en **oak:QueryIndexDefinition**
1. Agregue las siguientes propiedades al nodo:

   * **tipo:** `lucene` (de tipo cadena)
   * **asincrónico:** `async` (de tipo cadena)

1. Guarde los cambios.

El índice Lucene tiene las siguientes opciones de configuración:

* La propiedad **type** que especifica el tipo de índice debe establecerse en **lucene**
* La propiedad **async** que se debe establecer en **async**. Esto envía el proceso de actualización del índice a un subproceso en segundo plano.
* La propiedad **includePropertyTypes**, que define qué subconjunto de tipos de propiedad se incluye en el índice.
* La propiedad **excludePropertyNames** que define una lista de nombres de propiedades: propiedades que deben excluirse del índice.
* El indicador **reindex** que, cuando se establece en **true**, déclencheur un reíndice de contenido completo.

### Explicación de la búsqueda de texto completo {#understanding-fulltext-search}

La documentación de esta sección se aplica a Apache Lucene, Elasticsearch e índices de texto completo de PostgreSQL, SQLite y MySQL, por ejemplo. El siguiente ejemplo es para AEM/Oak/Lucene.

<b>Datos para indexar</b>

El punto de partida son los datos que deben indexarse. Veamos los siguientes documentos, por ejemplo:

| <b>Id. de documento</b> | <b>Ruta</b> | <b>Texto Completo</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;Rubik es una marca finlandesa&quot;. |
| 200 | /content/rubiksCube | &quot;El cubo de Rubik fue inventado en 1974&quot;. |
| 300 | /content/cube | &quot;Un cubo es un objeto tridimensional.&quot; |


<b>Índice invertido</b>

El mecanismo de indexación divide el texto completo en palabras denominadas &quot;tokens&quot; y crea un índice denominado &quot;índice invertido&quot;. Este índice contiene la lista de documentos donde aparece para cada palabra.

Las palabras cortas y comunes (también denominadas &quot;palabras de parada&quot;) no se indexan. Todos los tokens se convierten a minúsculas y se aplica la derivación.

Los caracteres especiales como *&quot;-&quot;* no están indexados.

| <b>Token</b> | <b>Id. de documento</b> |
| --- | --- |
| 194 | ..., 200,... |
| marca | ..., 100,... |
| cubo | ..., 200, 300,... |
| dimensión | 300 |
| terminar | ..., 100,... |
| inventar | 200 |
| objeto | ..., 300,... |
| rubí | ..., 100, 200,... |

La lista de documentos está ordenada. Esto resulta útil cuando se realiza una consulta.

<b>Buscando</b>

A continuación se muestra un ejemplo de consulta. Observe que todos los caracteres especiales (como *&#39;*) se reemplazaron con un espacio:

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

Las palabras se identifican mediante token y se filtran del mismo modo que al indexar (por ejemplo, se eliminan las palabras de un solo carácter). Por lo tanto, en este caso, la búsqueda es para:

```
+:fulltext:rubik +:fulltext:cube
```

El índice consulta la lista de documentos para esas palabras. Si hay muchos documentos, la lista puede ser grande. A modo de ejemplo, supongamos que contienen lo siguiente:


| <b>Token</b> | <b>Id. de documento</b> |
| --- | --- |
| rubí | 10, 100, 200, 1000 |
| cubo | 30, 200, 300, 2000 |


Lucene intercambia las dos listas (o las listas de operación por turnos `n`, al buscar `n` palabras):

* Leído en el &quot;rubik&quot; obtiene la primera entrada: encuentra 10
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 10. 10 no se encuentra, el siguiente es 30.
* Leído en el &quot;rubik&quot; obtiene la primera entrada `>` = 30: encuentra 100.
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 100: encuentra 200.
* Leer en &quot;rubik&quot; obtiene la primera entrada `>` = 200. 200 se ha encontrado. Así que el documento 200 coincide para ambos términos. Esto se recuerda.
* Leer en el &quot;rubik&quot; obtiene la siguiente entrada: 1000.
* Leído en el &quot;cubo&quot; obtiene la primera entrada `>` = 1000: encuentra 2000.
* Leído en el &quot;rubik&quot; obtiene la primera entrada `>` = 2000: fin de la lista.
* Por último, puede detener la búsqueda.

El único documento encontrado que contiene ambos términos es 200, como en el ejemplo siguiente:

| 200 | /content/rubiksCube | &quot;El cubo de Rubik fue inventado en 1974&quot;. |
| --- | --- | --- |

Cuando se encuentran varias entradas, se ordenan por puntuación.

### Índice de propiedades de Lucene {#the-lucene-property-index}

Desde **Oak 1.0.8**, Lucene se puede usar para crear índices que impliquen restricciones de propiedad que no sean de texto completo.

Para obtener un índice de propiedades de Lucene, la propiedad **fulltextEnabled** siempre debe establecerse en false.

Consulte el siguiente ejemplo de consulta:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir un índice de propiedades de Lucene para la consulta anterior, puede agregar la siguiente definición creando un nodo en **`oak:index`:**

* **Nombre:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una vez creado el nodo, agregue las siguientes propiedades:

* **tipo:**

  ```xml
  lucene (of type String)
  ```

* **asincrónico:**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled:**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>En comparación con el Índice de propiedades normal, el Índice de propiedades de Lucene siempre se configura en modo asincrónico. Por lo tanto, es posible que los resultados devueltos por el índice no siempre reflejen el estado más actualizado del repositorio.

>[!NOTE]
>
>Para obtener información más específica sobre el índice de propiedades de Lucene, consulte la [página de documentación de Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analizadores Lucene {#lucene-analyzers}

Desde la versión 1.2.0, Oak admite analizadores Lucene.

Los analizadores se utilizan tanto cuando se indexa un documento como en el momento de la consulta. Un analizador examina el texto de los campos y genera un flujo de tokens. Los analizadores Lucene están compuestos por una serie de clases de tokenizer y filtro.

Los analizadores se pueden configurar a través del nodo `analyzers` (de tipo `nt:unstructured`) dentro de la definición `oak:index`.

El analizador predeterminado para un índice está configurado en el elemento secundario `default` del nodo de analizadores.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obtener una lista de los analizadores disponibles, consulte la documentación de la API de la versión de Lucene que está utilizando.

#### Especificar la clase de analizador directamente {#specifying-the-analyzer-class-directly}

Si desea utilizar cualquier analizador predeterminado, puede configurarlo siguiendo el siguiente procedimiento:

1. Busque el índice con el que desea utilizar el analizador bajo el nodo `oak:index`.

1. En el índice, cree un nodo secundario denominado `default` de tipo `nt:unstructured`.

1. Agregue una propiedad al nodo predeterminado con las siguientes propiedades:

   * **Nombre:** `class`
   * **Tipo:** `String`
   * **Valor:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   El valor es el nombre de la clase de analizador que desea utilizar.

   También puede configurar el analizador para utilizarlo con una versión de Lucene específica mediante la propiedad de cadena `luceneMatchVersion` opcional. Una sintaxis válida para utilizarla con Lucene 4.7 sería:

   * **Nombre:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valor:** `LUCENE_47`

   Si no se proporciona `luceneMatchVersion`, Oak utiliza la versión de Lucene con la que se envía.

1. Si desea agregar un archivo de palabras de detención a las configuraciones del analizador, puede crear un nodo bajo el `default` con las siguientes propiedades:

   * **Nombre:** `stopwords`
   * **Tipo:** `nt:file`

#### Creación de analizadores mediante composición {#creating-analyzers-via-composition}

Los analizadores también se pueden componer en función de `Tokenizers`, `TokenFilters` y `CharFilters`. Para ello, especifique un analizador y cree nodos secundarios de sus tokenizers y filtros opcionales que se apliquen en el orden indicado.

Consideremos esta estructura de nodos como un ejemplo:

* **Nombre:** `analyzers`

   * **Nombre:** `default`

      * **Nombre:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `HTMLStrip`
         * **Nombre:** `Mapping`

      * **Nombre:** `tokenizer`

         * **Nombre de propiedad:** `name`

            * **Tipo:** `String`
            * **Valor:** `Standard`

      * **Nombre:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nombre:** `LowerCase`
         * **Nombre:** `Stop`

            * **Nombre de propiedad:** `words`

               * **Tipo:** `String`
               * **Valor:** `stop1.txt, stop2.txt`

            * **Nombre:** `stop1.txt`

               * **Tipo:** `nt:file`

            * **Nombre:** `stop2.txt`

               * **Tipo:** `nt:file`

El nombre de los filtros, charFilters y tokenizers se forman eliminando los sufijos de fábrica. Así:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` se convierte en `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` se convierte en `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` se convierte en `Stop`

Cualquier parámetro de configuración necesario para la fábrica se especifica como propiedad del nodo en cuestión.

En el caso de casos como la carga de palabras de detención en los que se debe cargar contenido de archivos externos, el contenido se puede proporcionar creando un nodo secundario de tipo `nt:file` para el archivo en cuestión.

### Herramientas de indexación de AEM {#aem-indexing-tools}

AEM 6.1 también integra dos herramientas de indexación presentes en AEM 6.0 como parte del conjunto de herramientas de Adobe Consulting Services Commons:

1. **Explicar consulta**, una herramienta diseñada para ayudar a los administradores a comprender cómo se ejecutan las consultas;
1. **Administrador de índices Oak**, una interfaz de usuario web para mantener los índices existentes.

Ahora puede llegar a ellos yendo a **Herramientas - Operaciones - Panel de control - Diagnóstico** desde la pantalla de bienvenida de AEM.

Para obtener más información sobre cómo usarlos, consulte la [documentación del tablero de operaciones](/help/sites-administering/operations-dashboard.md).

#### Creación de índices de propiedades mediante OSGi {#creating-property-indexes-via-osgi}

El paquete ACS Commons también expone las configuraciones OSGi que se pueden utilizar para crear índices de propiedades.

Puede obtener acceso a él desde la consola web buscando &quot;**Asegúrese de que el índice de propiedades de Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solución de problemas de indexación {#troubleshooting-indexing-issues}

Pueden surgir situaciones en las que las consultas tardan mucho tiempo en ejecutarse y el tiempo de respuesta general del sistema es lento.

Esta sección presenta un conjunto de recomendaciones sobre lo que se debe hacer para rastrear la causa de estos problemas y consejos sobre cómo resolverlos.

#### Preparar información de depuración para análisis {#preparing-debugging-info-for-analysis}

La forma más sencilla de obtener la información necesaria para la consulta que se está ejecutando es mediante la [herramienta de consulta de explicación](/help/sites-administering/operations-dashboard.md#explain-query). Esto permite recopilar la información precisa necesaria para depurar una consulta lenta sin necesidad de consultar la información de nivel de registro. Esto es deseable si conoce la consulta que se está depurando.

Si no es posible por cualquier motivo, puede recopilar los registros de indexación en un solo archivo y utilizarlo para solucionar su problema concreto.

#### Activar registro {#enable-logging}

Para habilitar el registro, debe habilitar los registros de nivel **DEBUG** para las categorías que pertenecen a la indexación y las consultas de Oak. Estas categorías son:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La categoría **com.day.cq.search** solo es aplicable si utiliza la utilidad QueryBuilder de AEM.

>[!NOTE]
>
>Es importante que los registros solo estén configurados en DEPURACIÓN mientras se esté ejecutando la consulta que desea solucionar. De lo contrario, se generan muchos eventos en los registros a lo largo del tiempo. Debido a esto, una vez recopilados los registros necesarios, vuelva al registro de nivel INFO para las categorías mencionadas anteriormente.

Puede habilitar el registro siguiendo este procedimiento:

1. Dirija su explorador a `https://serveraddress:port/system/console/slinglog`
1. Haga clic en el botón **Agregar nuevo registrador** en la parte inferior de la consola.
1. En la fila recién creada, añada las categorías mencionadas anteriormente. Puede usar el signo **+** para agregar más de una categoría a un solo registrador.
1. Elija **DEBUG** de la lista desplegable **Nivel de registro**.
1. Establezca el archivo de salida en `logs/queryDebug.log`. Esto correlaciona todos los eventos de DEPURACIÓN en un solo archivo de registro.
1. Ejecute la consulta o procese la página que está utilizando la consulta que desea depurar.
1. Una vez ejecutada la consulta, vuelva a la consola de registro y cambie el nivel de registro del registrador recién creado a **INFO**.

#### Configuración del índice {#index-configuration}

La forma en que se evalúa la consulta se ve afectada en gran medida por la configuración del índice. Es importante analizar la configuración del índice o enviarla al servicio de asistencia. Puede obtener la configuración como paquete de contenido u obtener una representación JSON.

Normalmente, la configuración de indexación se almacena en el nodo `/oak:index` en CRXDE, puede obtener la versión JSON en:

`https://serveraddress:port/oak:index.tidy.-1.json`

Si el índice está configurado en una ubicación diferente, cambie la ruta según corresponda.

#### Salida de MBean {#mbean-output}

A veces resulta útil proporcionar el resultado de los MBeans relacionados con índices para la depuración. Para ello:

1. Vaya a la consola JMX en:
   `https://serveraddress:port/system/console/jmx`

1. Busque los siguientes MBeans:

   * Estadísticas de índice de Lucene
   * Estadísticas de compatibilidad con CopyOnRead
   * Estadísticas de consultas de Oak
   * IndexStats

1. Haga clic en cada uno de los MBean para obtener estadísticas de rendimiento. Cree una captura de pantalla o anótelas en caso de que sea necesario un envío de asistencia.

También puede obtener la variante JSON de estas estadísticas en las siguientes URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

También puede proporcionar una salida JMX consolidada mediante `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Esto incluiría todos los detalles de MBean relacionados con Oak en formato JSON.

#### Otros detalles {#other-details}

Puede recopilar más detalles para solucionar el problema, como los siguientes:

1. La versión de Oak en la que se está ejecutando la instancia. Puede verlo abriendo CRXDE y mirando la versión en la esquina inferior derecha de la página de bienvenida, o comprobando la versión del paquete `org.apache.jackrabbit.oak-core`.
1. Resultado de QueryBuilder Debugger de la consulta problemática. Se puede obtener acceso al depurador en: `https://serveraddress:port/libs/cq/search/content/querydebug.html`
