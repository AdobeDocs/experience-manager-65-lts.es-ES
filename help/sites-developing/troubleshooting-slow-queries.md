---
title: Solución de problemas de consultas lentas
description: Aprenda a solucionar problemas de consultas lentas en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---

# Solución de problemas de consultas lentas{#troubleshooting-slow-queries}

## Clasificaciones de consulta lenta {#slow-query-classifications}

Existen tres clasificaciones principales de consultas lentas en AEM, enumeradas por gravedad:

1. **Consultas sin índice**

   * Las consultas que **no** se resuelven en un índice y atraviesan el contenido de JCR para recopilar resultados

1. **Consultas mal restringidas (o con ámbitos)**

   * Consultas que se resuelven en un índice, pero que deben atravesar todas las entradas de índice para recopilar resultados

1. **Consultas de conjunto de resultados grandes**

   * Consultas que devuelven grandes cantidades de resultados

Las dos primeras clasificaciones de consultas (sin índice y mal restringidas) son lentas. Son lentos porque obligan al motor de consultas de Oak a inspeccionar cada resultado **potencial** (nodo de contenido o entrada de índice) para identificar qué pertenece al conjunto de resultados **actual**.

El acto de inspeccionar cada resultado potencial es lo que se conoce como Traversing.

Dado que cada resultado potencial debe inspeccionarse, el coste para determinar el conjunto de resultados reales aumenta linealmente con el número de resultados potenciales.

Añadir restricciones de consulta e índices de ajuste permite almacenar los datos del índice en un formato optimizado, lo que permite una recuperación rápida de los resultados y reduce o elimina la necesidad de realizar una inspección lineal de los conjuntos de resultados potenciales.

En AEM 6.3, de forma predeterminada, cuando se alcanza un recorrido de 100 000, la consulta falla y genera una excepción. Este límite no existe de forma predeterminada en las versiones de AEM anteriores a AEM 6.3, pero se puede establecer mediante la configuración OSGi de Apache Jackrabbit Query Engine y el bean JMX de QueryEngineSettings (propiedad LimitReads).

### Detección de consultas sin índice {#detecting-index-less-queries}

#### Durante el desarrollo {#during-development}

Explique **todas** las consultas y asegúrese de que sus planes de consulta no contengan la explicación **/&amp;ast; traverse** en ellas. Ejemplo de plan de consulta de recorrido:

* **PLAN:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Posterior a la implementación {#post-deployment}

* Supervise `error.log` para consultas de recorrido sin índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Este mensaje solo se registra si no hay ningún índice disponible y si la consulta atraviesa potencialmente muchos nodos. Los mensajes no se registran si hay un índice disponible, pero la cantidad a recorrer es pequeña y, por lo tanto, rápida.

* Visite la consola de operaciones [Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#query-performance) de AEM y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscan explicaciones de consultas de recorrido o sin índice.

### Detección de consultas mal restringidas {#detecting-poorly-restricted-queries}

#### Durante el desarrollo {#during-development-1}

Explique todas las consultas y asegúrese de que se resuelven en un índice ajustado para que coincida con las restricciones de propiedad de la consulta.

* La cobertura del plan de consulta ideal tiene `indexRules` para todas las restricciones de propiedad y, como mínimo, para las restricciones de propiedad más estrictas de la consulta.
* Las consultas que ordenan resultados deben resolverse en un índice de propiedades de Lucene con reglas de índice para las propiedades que ordenan por las que se establecen `orderable=true.`

#### Por ejemplo, el valor predeterminado `cqPageLucene` no tiene una regla de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de añadir la regla de índice cq:tags

* **cq:etiquetas Regla de índice**

   * No existe de forma predeterminada

* **Consulta del Generador de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **Plan de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esta consulta se resuelve en el índice `cqPageLucene`, pero como no existe ninguna regla de índice de propiedad para `jcr:content` o `cq:tags`, cuando se evalúa esta restricción, se comprueba cada registro del índice `cqPageLucene` para determinar una coincidencia. Por lo tanto, si el índice contiene 1 millón de nodos `cq:Page`, se comprueban 1 millón de registros para determinar el conjunto de resultados.

Después de agregar la regla de índice cq:tags

* **cq:etiquetas Regla de índice**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Consulta del Generador de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **Plan de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

La adición de indexRule para `jcr:content/cq:tags` en el índice `cqPageLucene` permite almacenar los datos de `cq:tags` de forma optimizada.

Cuando se realiza una consulta con la restricción `jcr:content/cq:tags`, el índice puede buscar los resultados por valor. Esto significa que si 100 nodos `cq:Page` tienen `myTagNamespace:myTag` como valor, solo se devuelven esos 100 resultados y los otros 999 000 se excluyen de las comprobaciones de restricción, lo que mejora el rendimiento en un factor de 10 000.

Más restricciones de consulta reducen los conjuntos de resultados aptos y optimizan aún más la optimización de la consulta.

Del mismo modo, sin una regla de índice adicional para la propiedad `cq:tags`, incluso una consulta de texto completo con una restricción de `cq:tags` no funcionaría correctamente, ya que los resultados del índice devolverían todas las coincidencias de texto completo. La restricción de cq:tags se filtraría después de ella.

Otra causa del filtrado posterior a los índices son las Listas de control de acceso, que a menudo se pierden durante el desarrollo. Intente asegurarse de que la consulta no devuelva rutas que puedan ser inaccesibles para el usuario. Esto se puede hacer mediante una mejor estructura de contenido y proporcionando restricciones de ruta relevantes en la consulta.

Una forma útil de identificar si el índice Lucene devuelve muchos resultados para devolver un pequeño subconjunto como resultado de la consulta es habilitar los registros de depuración para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. Al hacerlo, puede ver cuántos documentos se cargan desde el índice. El número de resultados posibles frente al número de documentos cargados no debe ser desproporcionado. Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Posterior a la implementación {#post-deployment-1}

* Supervisar `error.log` para consultas de recorrido:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite la consola de operaciones [Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#query-performance) de AEM y [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas en busca de planes de consulta que no resuelvan las restricciones de propiedad de consulta para indizar las reglas de propiedad.

### Detección de consultas de conjuntos de resultados grandes {#detecting-large-result-set-queries}

#### Durante el desarrollo {#during-development-2}

Establezca umbrales bajos para oak.queryLimitInMemory (por ejemplo, 10000) y oak.queryLimitReads (por ejemplo, 5000) y optimice la consulta costosa al alcanzar una excepción UnsupportedOperationException que dice &quot;La consulta lee más de x nodos...&quot;

La configuración de umbrales bajos ayuda a evitar consultas que consuman muchos recursos (es decir, que no estén respaldadas por ningún índice o que estén respaldadas por un índice que cubra menos). Por ejemplo, una consulta que lee un millón de nodos produciría una gran cantidad de E/S y afectaría negativamente al rendimiento general de la aplicación. Por lo tanto, cualquier consulta que falle debido a límites superiores debe analizarse y optimizarse.

#### Posterior a la implementación {#post-deployment-2}

* Monitorice los registros para consultas que activen un recorrido de nodos grande o un gran consumo de memoria de montón: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimice la consulta para reducir el número de nodos atravesados.

* Monitorice los registros para consultas que activen un gran consumo de memoria:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimice la consulta para reducir el consumo de memoria.

En las versiones de AEM 6.0 a 6.2, puede ajustar el umbral para el recorrido de nodos mediante parámetros JVM en el script de inicio de AEM para evitar que las consultas grandes se sobrecarguen en el entorno. Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los dos parámetros anteriores están preconfigurados de forma predeterminada y se pueden modificar mediante OSGi QueryEngineSettings.

Más información disponible en: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste del rendimiento de consultas {#query-performance-tuning}

El lema de la optimización del rendimiento de las consultas en AEM es:

**&quot;Cuantas más restricciones, mejor.&quot;**

A continuación se describen los ajustes recomendados para garantizar el rendimiento de la consulta. En primer lugar, ajuste la consulta, una actividad menos intrusiva, y luego, si es necesario, ajuste las definiciones de índice.

### Ajuste de la instrucción de consulta {#adjusting-the-query-statement}

AEM admite los siguientes lenguajes de consulta:

* Query Builder
* JCR-SQL2
* XPath

El siguiente ejemplo utiliza Query Builder porque es el lenguaje de consulta más utilizado por los desarrolladores de AEM; sin embargo, los mismos principios se aplican a JCR-SQL2 y XPath.

1. Añada una restricción nodetype para que la consulta se resuelva en un índice de propiedades de Lucene existente.

* **Consulta no optimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  Las consultas que carecen de una restricción de tipo de nodo obligan a AEM a asumir el tipo de nodo `nt:base`, del que todos los nodos de AEM son un subtipo, lo que en la práctica no da como resultado ninguna restricción de tipo de nodo.

  Al establecer `type=cq:Page`, se restringe esta consulta solo a `cq:Page` nodos y se resuelve en cqPageLucene de AEM, limitando los resultados a un subconjunto de nodos (solo `cq:Page` nodos) en AEM.

1. Ajuste la restricción nodetype de la consulta para que la consulta se resuelva en un índice de propiedades de Lucene existente.

* **Consulta no optimizada**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` es el tipo de nodo primario de `cq:Page`. Suponiendo que `jcr:content/contentType=article-page` solo se aplica a los nodos `cq:Page` mediante la aplicación personalizada de Adobe, esta consulta solo devuelve `cq:Page` nodos donde `jcr:content/contentType=article-page`. Sin embargo, este flujo es una restricción subóptima, ya que:

   * Otros nodos heredan de `nt:hierarchyNode` (por ejemplo, `dam:Asset`) y se agregan innecesariamente al conjunto de resultados potenciales.
   * No existe ningún índice proporcionado por AEM para `nt:hierarchyNode`, sin embargo, ya que hay un índice proporcionado para `cq:Page`.

  Al establecer `type=cq:Page`, se restringe esta consulta solo a `cq:Page` nodos y se resuelve en cqPageLucene de AEM, limitando los resultados a un subconjunto de nodos (solo nodos cq:Page) en AEM.

1. O bien, ajuste las restricciones de propiedades para que la consulta se resuelva en un índice de propiedades existente.

* **Consulta no optimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  Si se cambia la restricción de propiedad de `jcr:content/contentType` (un valor personalizado) a la conocida propiedad `sling:resourceType`, la consulta se resolverá en el índice de propiedad `slingResourceType`, que indexa todo el contenido por `sling:resourceType`.

  Los índices de propiedades (a diferencia de los Índices de propiedades de Lucene) se utilizan mejor cuando la consulta no distingue por tipo de nodo y una sola restricción de propiedad domina el conjunto de resultados.

1. Añada a la consulta la restricción de ruta más estricta posible. Por ejemplo, prefiera `/content/my-site/us/en` sobre `/content/my-site`, o `/content/dam` sobre `/`.

* **Consulta no optimizada**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  El ámbito de la restricción de ruta de `path=/content` a `path=/content/my-site/us/en` permite que los índices reduzcan el número de entradas de índice que deben inspeccionarse. Cuando la consulta pueda restringir bien la ruta de acceso más allá de `/content` o `/content/dam`, asegúrese de que el índice tenga `evaluatePathRestrictions=true`.

  La nota que utiliza `evaluatePathRestrictions` aumenta el tamaño del índice.

1. Cuando sea posible, evite las funciones de consulta y las operaciones de consulta como: `LIKE` y `fn:XXXX`, ya que sus costos se escalan con el número de resultados basados en restricciones.

* **Consulta no optimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **Consulta optimizada**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  La condición LIKE es lenta de evaluar porque no se puede utilizar ningún índice si el texto comienza con un comodín (&quot;%...&#39;). La condición jcr:contains permite utilizar un índice de texto completo y, por lo tanto, se prefiere. Requiere que el índice de propiedades de Lucene resuelto tenga indexRule para `jcr:content/contentType` con `analayzed=true`.

  El uso de funciones de consulta como `fn:lowercase(..)` puede ser más difícil de optimizar, ya que no hay equivalentes más rápidos (fuera de configuraciones del analizador de índices más complejas y molestas). Es mejor identificar otras restricciones de ámbito para mejorar el rendimiento general de la consulta, lo que requiere que las funciones funcionen con el menor conjunto posible de resultados potenciales.

1. ***Este ajuste es específico del Generador de consultas y no se aplica a JCR-SQL2 o XPath.***

   Use [Query Builder&#39; guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) cuando el conjunto completo de resultados sea **no** necesario de inmediato.

   * **Consulta no optimizada**

     ```js
     type=cq:Page
     path=/content
     ```

   * **Consulta optimizada**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   En los casos en los que la ejecución de consultas es rápida pero el número de resultados es grande, la página `guessTotal` es una optimización crítica para las consultas del Generador de consultas.

   `p.guessTotal=100` indica a Query Builder que solo recopile los primeros 100 resultados. Y, para establecer un indicador booleano que indique si existe al menos un resultado más (pero no cuántos más, ya que el recuento de este número resulta en lentitud). Esta optimización sobresale en los casos de uso de paginación o carga infinita, donde solo se muestra un subconjunto de resultados de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Si la consulta óptima se resuelve en un índice de propiedades, no queda nada por hacer, ya que los índices de propiedades son mínimamente ajustables.
1. De lo contrario, la consulta debe resolverse en un índice de propiedades de Lucene. Si no se puede resolver ningún índice, vaya a Creación de un índice.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del Generador de consultas**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **XPath generado a partir de la consulta de Query Builder**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. Proporcione XPath (o JCR-SQL2) al generador de definición de índice de Oak en `https://oakutils.appspot.com/generate/index` para que pueda generar la definición de índice de propiedad de Lucene optimizada. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades de Lucene generada**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. Combine manualmente la definición generada en el índice de propiedades de Lucene existente de forma aditiva. Tenga cuidado de no eliminar las configuraciones existentes, ya que pueden utilizarse para satisfacer otras consultas.

   1. Busque el índice de propiedades de Lucene existente que cubre cq:Page (mediante el Administrador de índices). En este caso, `/oak:index/cqPageLucene`.
   1. Identifique el delta de configuración entre la definición de índice optimizada (Paso #4) y el índice existente (/oak:index/cqPageLucene), y agregue las configuraciones que faltan del índice optimizado a la definición de índice existente.
   1. Según las Prácticas recomendadas de reindexación de AEM, se debe realizar una actualización o reindexar en orden, en función de si el contenido existente podría verse afectado por este cambio de configuración de índice.

## Crear un nuevo índice {#create-a-new-index}

1. Compruebe que la consulta no se resuelve en un índice de propiedades de Lucene existente. Si es así, consulte la sección anterior sobre ajuste y índice existente.
1. Si es necesario, convierta la consulta a XPath o JCR-SQL2.

   * **Consulta del Generador de consultas**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **XPath generado a partir de la consulta de Query Builder**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. Proporcione XPath (o JCR-SQL2) al generador de definición de índice de Oak en `https://oakutils.appspot.com/generate/index` para que pueda generar la definición de índice de propiedad de Lucene optimizada. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definición del índice de propiedades de Lucene generada**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. Implemente la definición de índice de propiedades de Lucene generada.

   Agregue la definición XML proporcionada por el Generador de definiciones de índice de Oak para el nuevo índice al proyecto de AEM que administra las definiciones de índice de Oak (recuerde, trate las definiciones de índice de Oak como código, ya que el código depende de ellas).

   Implemente y pruebe el nuevo índice siguiendo el ciclo de vida habitual de desarrollo de software de AEM y compruebe que la consulta se resuelve en el índice y que la consulta es satisfactoria.

   En la implementación inicial de este índice, AEM lo rellena con los datos necesarios.

## ¿Cuándo son correctas las consultas sin índice y las consultas de recorrido? {#when-index-less-and-traversal-queries-are-ok}

Debido a la arquitectura de contenido flexible de AEM, es difícil predecir y garantizar que las ventas cruzadas de estructuras de contenido no evolucionen con el tiempo para ser inaceptablemente grandes.

Por lo tanto, asegúrese de que los índices satisfacen las consultas, excepto si la combinación de la restricción de ruta de acceso y la restricción de tipo de nodo garantiza que se atraviesen **menos de 20 nodos.**

## Herramientas de desarrollo de consultas {#query-development-tools}

### Compatible con Adobe {#adobe-supported}

* **Depurador de Query Builder**

   * Interfaz de usuario web para ejecutar consultas del Generador de consultas y generar la XPath de compatibilidad (para su uso en Explicar consulta o el Generador de definiciones de índice de Oak).
   * En AEM en [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Herramienta de consulta**

   * Interfaz de usuario web para ejecutar consultas XPath y JCR-SQL2.
   * En AEM en [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Herramientas > Consulta...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Un panel Operaciones de AEM que proporciona una explicación detallada (plan de consulta, tiempo de consulta y número de resultados) para cualquier consulta XPATH o JCR-SQL2 determinada.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Un panel Operaciones de AEM que enumera las consultas lentas y populares recientes ejecutadas en AEM.

* **[Administrador de índices](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Interfaz de usuario web de operaciones de AEM que muestra los índices en la instancia de AEM; facilita la comprensión de qué índices existen; se puede dirigir o aumentar.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro de Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Registro de ejecución de consultas de Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Configuración OSGi de la configuración del motor de consultas Apache Jackrabbit**

   * Configuración de OSGi que configura el comportamiento de error para consultas de recorrido.
   * En AEM en [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **MBean JMX de NodeCounter**

   * MBean de JMX utilizado para estimar el número de nodos en los árboles de contenido en AEM.
   * En AEM en [/system/console/jmx/org.apache.jackrabbit.oak%3Name%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Admitido por la comunidad {#community-supported}

* **Generador de definiciones de índice de Oak en`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Genere un índice de propiedades de Lucence óptimo a partir de instrucciones de consulta XPath o JCR-SQL2.

* **_Complemento de AEM Chrome_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * El complemento _AEM Chrome_ es una extensión de explorador web Google Chrome que expone datos de registro por solicitud, incluidas las consultas de ejecución y sus planes de consulta, en la consola de herramientas de desarrollo del explorador.
   * Requiere que instale y habilite [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) en AEM.
