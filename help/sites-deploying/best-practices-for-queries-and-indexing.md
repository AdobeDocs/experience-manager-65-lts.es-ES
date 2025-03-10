---
title: Prácticas recomendadas para consultas e indexación
description: Este artículo proporciona directrices sobre cómo optimizar los índices y las consultas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
hide: true
hidefromtoc: true
exl-id: 3ffa7c80-ce59-41cf-bb50-c6caf77d9baa
source-git-commit: f145e5f0d70662aa2cbe6c8c09795ba112e896ea
workflow-type: tm+mt
source-wordcount: '4520'
ht-degree: 0%

---

# Prácticas recomendadas para consultas e indexación{#best-practices-for-queries-and-indexing}

Junto con la transición a Oak en AEM 6, se han realizado algunos cambios importantes en la forma en que se administran las consultas y los índices. En Jackrabbit 2, todo el contenido se indexaba de forma predeterminada y se podía consultar libremente. En Oak, los índices deben crearse manualmente en el nodo `oak:index`. Una consulta se puede ejecutar sin un índice, pero para conjuntos de datos grandes, se ejecutará lentamente o incluso se anulará.

Este artículo describe cuándo crear índices y cuándo no se necesitan, trucos para evitar utilizar consultas cuando no se necesitan y sugerencias para optimizar sus índices y consultas para que rindan del modo más óptimo posible.

Además, asegúrese de leer la [documentación de Oak sobre cómo escribir consultas e índices](/help/sites-deploying/queries-and-indexing.md). Además de que los índices son un nuevo concepto en AEM 6, existen diferencias sintácticas en las consultas de Oak que deben tenerse en cuenta al migrar código desde una instalación anterior de AEM.

## Cuándo usar consultas {#when-to-use-queries}

### Diseño de repositorios y taxonomías {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, se deben tener en cuenta varios factores. Estos incluyen controles de acceso, localización, componentes y herencia de propiedades de página, entre otros.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante tener en cuenta la &quot;transitabilidad&quot; del diseño de indexación. En este contexto, la transitabilidad es la capacidad de una taxonomía que permite acceder al contenido de forma predecible en función de su ruta. Esto hará que sea más fácil mantener un sistema con mejor rendimiento que el que requiere ejecutar muchas consultas.

Además, al diseñar una taxonomía, es importante tener en cuenta si la ordenación es importante. En los casos en los que no se requiere el orden explícito y se esperan muchos nodos del mismo nivel, se prefiere utilizar un tipo de nodo sin ordenar como `sling:Folder` o `oak:Unstructured`. En los casos en que se requiere orden, `nt:unstructured` y `sling:OrderedFolder` son más apropiados.

### Consultas en componentes {#queries-in-components}

Dado que las consultas pueden ser una de las operaciones más gravosas realizadas en un sistema AEM, es aconsejable evitarlas en los componentes. Tener varias consultas ejecutándose cada vez que se procesa una página puede a menudo degradar el rendimiento del sistema. Hay dos estrategias que se pueden usar para evitar la ejecución de consultas al procesar componentes: **nodos de recorrido** y **resultados de recuperación previa**.

#### Recorrido de nodos {#traversing-nodes}

Si el repositorio está diseñado de manera que permita un conocimiento previo de la ubicación de los datos necesarios, se puede implementar un código que recupere estos datos de las rutas necesarias sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería procesar contenido que se ajuste a una categoría determinada. Un método sería organizar el contenido con una propiedad category que se pueda consultar para rellenar un componente que muestre los elementos de una categoría.

Un mejor enfoque sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

El nodo `/content/myUnstructuredContent/parentCategory/childCategory` simplemente se puede recuperar, sus elementos secundarios se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño u homogéneo, puede ser más rápido atravesar el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, las consultas deben evitarse siempre que sea posible hacerlo.

#### Resultados de recuperación previa {#prefetching-results}

A veces, el contenido o los requisitos relacionados con el componente no permiten el uso del recorrido de nodos como método para recuperar los datos necesarios. En estos casos, es necesario ejecutar las consultas necesarias antes de procesar el componente para garantizar un rendimiento óptimo para el usuario final.

Si los resultados necesarios para el componente se pueden calcular en el momento en que se crea y no hay expectativas de que el contenido cambie, la consulta se puede ejecutar cuando el autor aplique la configuración en el cuadro de diálogo.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar en una programación o a través de un oyente para actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.

## Optimización de consultas {#query-optimization}

Al ejecutar una consulta que no utiliza un índice, se registran advertencias sobre el recorrido del nodo. Si se trata de una consulta que se va a ejecutar con frecuencia, cree un índice. Para determinar qué índice está usando una consulta determinada, se recomienda la [herramienta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query). Para obtener más información, se puede habilitar el registro de DEPURACIÓN para las API de búsqueda relevantes.

>[!NOTE]
>
>Después de modificar una definición de índice, el índice debe reconstruirse (reindexarse). Según el tamaño del índice, esto puede tardar algún tiempo en completarse.

Al ejecutar consultas complejas, puede haber casos en los que desglosar la consulta en varias consultas más pequeñas y unir los datos a través del código después del hecho sea más eficaz. La recomendación para estos casos es comparar el rendimiento de los dos enfoques para determinar qué opción sería mejor para el caso de uso en cuestión.

AEM permite escribir consultas de una de las tres maneras siguientes:

* A través de las [API de QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Uso de XPath (recomendado)
* Uso de SQL2

Aunque todas las consultas se convierten a SQL2 antes de ejecutarse, la sobrecarga de la conversión de consultas es mínima y, por lo tanto, la mayor preocupación al elegir un idioma de consulta será la legibilidad y el nivel de comodidad del equipo de desarrollo.

>[!NOTE]
>
>Al utilizar QueryBuilder, determina el recuento de resultados de forma predeterminada, que es más lento en Oak en comparación con las versiones anteriores de Jackrabbit. Para compensar esto, puede usar el [parámetro guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### La herramienta de consulta Explicar {#the-explain-query-tool}

Al igual que con cualquier idioma de consulta, el primer paso para optimizar una consulta es comprender cómo se ejecutará. Para habilitar esta actividad, puede usar la [herramienta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query) que forma parte del tablero de operaciones. Con esta herramienta, se puede conectar una consulta y explicarla. Se muestra una advertencia si la consulta causa problemas con un repositorio grande y con el tiempo de ejecución y los índices utilizados. La herramienta también puede cargar una lista de consultas lentas y populares que luego se pueden explicar y optimizar.

### Registro DEBUG para consultas {#debug-logging-for-queries}

Para obtener información adicional acerca de cómo elige Oak qué índice utilizar y cómo ejecuta realmente el motor de consultas una consulta, se puede agregar una configuración de registro **DEBUG** para los siguientes paquetes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Asegúrese de eliminar este registrador cuando haya terminado de depurar la consulta. Tiende a generar una gran cantidad de actividad y eventualmente puede llenar su disco con archivos de registro.

Para obtener más información sobre cómo hacerlo, consulte la [Documentación de registro](/help/sites-deploying/configure-logging.md).

### Estadísticas de índice {#index-statistics}

Lucene registra un bean JMX que proporcionará detalles sobre el contenido indexado, incluido el tamaño y el número de documentos presentes en cada uno de los índices.

Puede acceder a él desde la consola JMX en `https://server:port/system/console/jmx`

Una vez que haya iniciado sesión en la consola JMX, realice una búsqueda de **Estadísticas de índice de Lucene** para encontrarlas. Se pueden encontrar otras estadísticas de índice en el MBean **IndexStats**.

Para obtener estadísticas de consultas, observe el MBean denominado **Estadísticas de consultas de Oak**.

Si desea profundizar en sus índices usando una herramienta como [Luke](https://code.google.com/archive/p/luke/), debe usar la consola de Oak para volcar el índice desde `NodeStore` a un directorio del sistema de archivos. Para obtener instrucciones sobre cómo hacerlo, lea la [documentación de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

También puede extraer los índices del sistema en formato JSON. Para ello, debe tener acceso a `https://server:port/oak:index.tidy.-1.json`

### Límites de la consulta {#query-limits}

**Durante el desarrollo**

Defina umbrales bajos para `oak.queryLimitInMemory` (por ejemplo, 10000) y Oak. `queryLimitReads` (por ejemplo, 5000) y optimizar la consulta costosa al alcanzar una excepción UnsupportedOperationException diciendo &quot;La consulta leyó más de x nodos...&quot;

Esto ayuda a evitar consultas que requieren muchos recursos (es decir, que no estén respaldadas por ningún índice o que estén respaldadas por un índice que cubra menos). Por ejemplo, una consulta que lee 1 millón de nodos produciría un aumento de E/S y afectaría negativamente al rendimiento general de la aplicación. Cualquier consulta que falle debido a los límites anteriores debe analizarse y optimizarse.

#### **Posterior a la implementación** {#post-deployment}

* Monitorice los registros para consultas que activen un recorrido de nodos grande o un gran consumo de memoria de montón: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimizar la consulta para reducir el número de nodos atravesados

* Monitorice los registros para consultas que activen un gran consumo de memoria

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimizar la consulta para reducir el consumo de memoria

En las versiones de AEM 6.0 a 6.2, puede ajustar el umbral para el recorrido de nodos mediante parámetros JVM en el script de inicio de AEM para evitar que las consultas grandes se sobrecarguen en el entorno.

Los valores recomendados son:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

En AEM 6.3, los dos parámetros anteriores están preconfigurados de forma predeterminada y se pueden mantener mediante OSGi QueryEngineSettings.

Más información disponible en: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Sugerencias para crear índices eficientes {#tips-for-creating-efficient-indexes}

### ¿Debería crear un índice? {#should-i-create-an-index}

La primera pregunta que se debe hacer al crear o optimizar índices es si son necesarios para una situación determinada. Si sólo va a ejecutar la consulta en cuestión una vez o sólo ocasionalmente y en un momento de menor actividad para el sistema mediante un proceso por lotes, puede ser mejor no crear ningún índice.

Después de crear un índice, cada vez que se actualicen los datos indexados, también se debe actualizar el índice. Dado que esto tiene implicaciones de rendimiento para el sistema, los índices solo deben crearse cuando sean necesarios.

Además, los índices solo son útiles si los datos contenidos en ellos son lo suficientemente únicos como para justificarlos. Considere un índice en un libro y los temas que cubre. Al indexar un conjunto de temas en un texto, normalmente habrá cientos o miles de entradas, lo que le permite ir rápidamente a un subconjunto de páginas para encontrar rápidamente la información que está buscando. Si ese índice solo tuviera dos o tres entradas, cada una de las cuales indicara varios cientos de páginas, no sería útil. Este mismo concepto se aplica a los índices de base de datos. Si solo hay un par de valores únicos, el índice no será útil. Dicho esto, un índice también puede llegar a ser demasiado grande para ser útil. Para ver las estadísticas de índice, consulte [Estadísticas de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) más arriba.

### ¿Lucene o índices de propiedades? {#lucene-or-property-indexes}

Los índices Lucene se introdujeron en Oak 1.0.9 y ofrecen algunas optimizaciones potentes sobre los índices de propiedad que se introdujeron en el primer lanzamiento de AEM 6. Al decidir si utilizar índices de Lucene o índices de propiedad, tenga en cuenta lo siguiente:

* Los índices de Lucene ofrecen muchas más funciones que los índices de propiedades. Por ejemplo, un índice de propiedad solo puede indexar una sola propiedad, mientras que un índice Lucene puede incluir muchas. Para obtener más información sobre todas las características disponibles en los índices Lucene, consulte la [documentación](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Los índices de Lucene son asíncronos. Aunque esto ofrece un aumento considerable del rendimiento, también puede provocar un retraso entre el momento en que se escriben los datos en el repositorio y el momento en que se actualiza el índice. Si es vital que las consultas devuelvan resultados 100 % precisos, se requeriría un índice de propiedad.
* Debido a su carácter asincrónico, los índices Lucene no pueden aplicar restricciones de exclusividad. Si es necesario, es necesario establecer un índice de propiedades.

En general, se recomienda utilizar índices de Lucene a menos que exista una necesidad imperiosa de utilizar índices de propiedad para poder obtener los beneficios de un rendimiento y una flexibilidad mayores.

### Indexación de Solr {#solr-indexing}

AEM también admite la indexación Solr de forma predeterminada. Se utiliza para admitir la búsqueda de texto completo, pero también se puede utilizar para admitir cualquier tipo de consulta JCR. Solr debe tenerse en cuenta cuando las instancias de AEM no tienen la capacidad de CPU para gestionar la cantidad de consultas necesarias en implementaciones que requieren mucha búsqueda, como los sitios web impulsados por búsquedas con un alto número de usuarios simultáneos. Como alternativa, Solr se puede implementar con un enfoque basado en rastreadores para utilizar algunas de las funciones más avanzadas de la plataforma.

Los índices Solr se pueden configurar para que se ejecuten incrustados en el servidor de AEM para entornos de desarrollo o se pueden descargar en una instancia remota para mejorar la escalabilidad de la búsqueda en los entornos de producción y ensayo. Aunque la descarga de búsquedas mejora la escalabilidad, introduce latencia y, por ello, no se recomienda a menos que sea necesario. Para obtener más información sobre cómo configurar la integración de Solr y cómo crear índices de Solr, consulte la [documentación sobre consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Al mismo tiempo que se utiliza el enfoque de búsqueda integrada de Solr, se permite descargar la indexación en un servidor Solr. Si las funciones más avanzadas del servidor Solr se utilizan mediante un método basado en rastreador, se requiere un trabajo de configuración adicional.

El inconveniente de este enfoque es que, aunque de forma predeterminada, las consultas de AEM respetan las ACL y, por lo tanto, ocultan los resultados a los que un usuario no tiene acceso, la externalización de la búsqueda a un servidor Solr no admitirá esta función. Si la búsqueda se va a externalizar de esta manera, se debe tener especial cuidado para garantizar que los usuarios no reciban resultados que no deberían ver.

Casos de uso potenciales en los que este método puede ser adecuado son casos en los que puede ser necesario acumular datos de búsqueda de múltiples fuentes. Por ejemplo, es posible que tenga un sitio alojado en AEM y un segundo sitio alojado en una plataforma de terceros. Solr se puede configurar para que rastree el contenido de ambos sitios y los almacene en un índice agregado. Esto permitiría búsquedas entre sitios.

### Consideraciones de diseño {#design-considerations}

La documentación de Oak para índices de Lucene enumera varias consideraciones que se deben tener en cuenta al diseñar índices:

* Si la consulta usa diferentes restricciones de ruta, use `evaluatePathRestrictions`. Esto permite que la consulta devuelva el subconjunto de resultados bajo la ruta especificada y, a continuación, los filtre según la consulta. De lo contrario, la consulta busca todos los resultados que coincidan con los parámetros de consulta en el repositorio y, a continuación, los filtra en función de la ruta.
* Si la consulta usa la ordenación, tenga una definición de propiedad explícita para la propiedad ordenada y establezca `ordered` en `true` para ella. Esto permite ordenar los resultados como tales en el índice y ahorrar en costosas operaciones de ordenación en el momento de la ejecución de la consulta.

* Inserte únicamente lo que sea necesario en el índice. Añadir características o propiedades innecesarias hace que el índice crezca y reduzca el rendimiento.
* En un índice de propiedad, tener un nombre de propiedad único ayudaría a reducir el tamaño de un índice, pero para los índices Lucene, se debe usar `nodeTypes` y `mixins` para lograr índices coherentes. Consultar un(a) `nodeType` o `mixin` específico(a) resultará más eficaz que consultar `nt:base`. Al utilizar este enfoque, defina `indexRules` para `nodeTypes` en cuestión.

* Si las consultas solo se ejecutan en determinadas rutas, cree esos índices en esas rutas. Los índices no son necesarios para residir en la raíz del repositorio.
* Utilice un solo índice cuando todas las propiedades que se están indexando estén relacionadas para permitir que Lucene evalúe tantas restricciones de propiedad como sea posible de forma nativa. Además, una consulta solo utilizará un índice, incluso cuando realice una unión.

### CopiarAlLeer {#copyonread}

En los casos en que `NodeStore` se almacene de forma remota, se puede habilitar una opción denominada `CopyOnRead`. La opción hace que el índice remoto se escriba en el sistema de archivos local cuando se lee. Esto puede ayudar a mejorar el rendimiento de las consultas que a menudo se ejecutan con estos índices remotos.

Esto se puede configurar en la consola OSGi bajo el servicio **LuceneIndexProvider** y está habilitado de forma predeterminada a partir de Oak 1.0.13.

### Eliminación de índices {#removing-indexes}

Al eliminar un índice, siempre se recomienda deshabilitarlo temporalmente estableciendo la propiedad `type` en `disabled` y realizar pruebas para asegurarse de que la aplicación funciona correctamente antes de eliminarlo. Un índice no se actualiza mientras está deshabilitado, por lo que es posible que no tenga el contenido correcto si se vuelve a habilitar y sea necesario reindexarlo.

Después de quitar un índice de propiedad en una instancia de TarMK, se debe ejecutar la compactación para recuperar cualquier espacio en disco que esté en uso. Para los índices Lucene, el contenido del índice real se encuentra en el BlobStore, por lo que se requeriría una recopilación de elementos no utilizados del almacén de datos.

Al eliminar un índice en una instancia de MongoDB, el coste de eliminación es proporcional al número de nodos del índice. Dado que eliminar un índice grande puede causar problemas, el método recomendado es deshabilitar el índice y eliminarlo solamente durante una ventana de mantenimiento, con una herramienta como **oak-mongo.js**. Tenga en cuenta que este método no debe utilizarse para el contenido de nodo normal, ya que puede introducir incoherencias en los datos.

>[!NOTE]
>
>Para obtener más información sobre oak-mongo.js, consulte la [sección Herramientas de línea de comandos](https://jackrabbit.apache.org/oak/docs/command_line.html) de la documentación de Oak.

### Hoja de características clave de la consulta JCR {#jcrquerycheatsheet}

Para admitir la creación de consultas JCR y definiciones de índice eficientes, la [Hoja de referencia de consultas JCR](assets/JCR_query_cheatsheet-v1.1.pdf) está disponible para su descarga y uso como referencia durante el desarrollo. Contiene consultas de ejemplo para QueryBuilder, XPath y SQL-2, que cubren varios escenarios que se comportan de forma diferente en términos de rendimiento de la consulta. También proporciona recomendaciones sobre cómo crear o personalizar índices de Oak. El contenido de esta hoja de referencia se aplica a AEM 6.5 y AEM as a Cloud Service.

## Reindexación {#re-indexing}

Esta sección describe los **únicos** motivos aceptables para reindexar índices Oak.

Fuera de los motivos descritos a continuación, el inicio de reíndices de índices Oak **no** cambia el comportamiento o resuelve los problemas, y aumenta innecesariamente las cargas en AEM.

La reindexación de índices Oak debe evitarse a menos que esté cubierta por un motivo en los cuadros siguientes.

>[!NOTE]
>
>Antes de consultar las tablas siguientes para determinar si la reindexación es útil, **compruebe siempre**:
>
>* la consulta es correcta
>* la consulta responde al índice esperado (usando [Explicar consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* el proceso de indexación ha finalizado
>

### Cambios en la configuración del índice Oak {#oak-index-configuration-changes}

Las únicas condiciones aceptables sin errores para reindexar índices Oak son si la configuración de un índice Oak ha cambiado.

*La reindexación siempre debe abordarse teniendo en cuenta su impacto en el rendimiento general de AEM y realizarse durante períodos de baja actividad o períodos de mantenimiento.*

A continuación se detallan los posibles problemas junto con las resoluciones:

* [Cambio de definición de índice de propiedad](#property-index-definition-change)
* [Cambio de definición de índice de Lucene](#lucene-index-definition-change)

#### Cambio de definición de índice de propiedad {#property-index-definition-change}

* Se aplica a/si:

   * Todas las versiones de Oak
   * Solo [índices de propiedades](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Síntomas:

   * Los nodos existentes antes de la actualización de la definición del índice de propiedad no aparecen en los resultados

* Cómo verificar:

   * Determine si los nodos que faltan se crearon o modificaron antes de la implementación de la definición de índice actualizada.
   * Compruebe las propiedades `jcr:created` o `jcr:lastModified` de cualquier nodo que falte con la hora de modificación del índice

* Cómo resolver:

   * [Reindexar](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) el índice de Lucene
   * También puede tocar (realizar una operación de escritura benigna) los nodos que faltan

      * Requiere toques manuales o código personalizado
      * Requiere que se conozca el conjunto de nodos que faltan
      * Requiere cambiar cualquier propiedad del nodo

#### Cambio de definición de índice de Lucene {#lucene-index-definition-change}

* Se aplica a/si:

   * Todas las versiones de Oak
   * Solo [índices de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados
   * Los resultados de la consulta no reflejan el comportamiento esperado de la definición del índice
   * El plan de consulta no informa del resultado esperado según la definición del índice

* Cómo verificar:

   * Compruebe que la definición del índice se haya cambiado utilizando el Mbean JMX de estadísticas de índice de Lucene (LuceneIndex), método `diffStoredIndexDefinition`.

* Cómo resolver:

   * Versiones de Oak anteriores a 1.6:

      * [Reindexar](#how-to-re-index) el índice de Lucene

   * Oak versiones 1.6+

      * Si el contenido existente no se ve afectado por los cambios, solo es necesaria una actualización

         * [Actualice](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) el índice lucene estableciendo [oak:queryIndexDefinition]@refresh=true

      * De lo contrario, [reindexe](#how-to-re-index) el índice lucene

         * Nota: Se utiliza el estado de índice de la última reindexación buena (o indexación inicial) hasta que se active una nueva reindexación

### Errores y situaciones excepcionales {#erring-and-exceptional-situations}

En la tabla siguiente se describen los únicos errores aceptables y las situaciones excepcionales en las que la reindexación de índices Oak resuelve el problema.

Si experimenta un problema en AEM que no coincide con los criterios descritos a continuación, **no** vuelva a indexar ningún índice, ya que no resolverá el problema.

A continuación se detallan los posibles problemas junto con las resoluciones:

* [Falta el binario de índice de Lucene](#lucene-index-binary-is-missing)
* [El binario del índice Lucene está dañado](#lucene-index-binary-is-corrupt)

#### Falta el binario de índice de Lucene {#lucene-index-binary-is-missing}

* Se aplica a/si:

   * Todas las versiones de Oak
   * Solo [índices de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * El archivo de registro de errores contiene una excepción que indica que falta un binario del índice Lucene

* Cómo resolver:

   * Realice una comprobación del repositorio de recorrido; por ejemplo:

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     al atravesar el repositorio se determina si faltan otros binarios (además de los archivos lucene)

   * Si faltan binarios que no sean índices de Lucene, restaure desde la copia de seguridad
   * De lo contrario, [reindexe](#how-to-re-index) *todos* los índices de Lucene
   * Nota:

     Esta condición es indicativa de un almacén de datos mal configurado que puede dar como resultado que falte CUALQUIER binario (por ejemplo, binarios de recursos).

     En este caso, restaure a la última versión buena conocida del repositorio para recuperar todos los binarios que faltan.

#### El binario del índice Lucene está dañado {#lucene-index-binary-is-corrupt}

* Se aplica a/si:

   * Todas las versiones de Oak
   * Solo [índices de Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Síntomas:

   * El índice Lucene no contiene los resultados esperados

* Cómo verificar:

   * `AsyncIndexUpdate` (cada cinco segundos) producirá un error con una excepción en el error.log:

     `...a Lucene index file is corrupt...`

* Cómo resolver:

   * Elimine la copia local del índice de Lucene

      1. Detener AEM
      1. Eliminar la copia local del índice Lucene en `crx-quickstart/repository/index`
      1. Reiniciar AEM

   * Si esto no resuelve el problema y persisten las excepciones de `AsyncIndexUpdate`:

      1. [Reindexe](#how-to-re-index) el índice erróneo
      1. Presentar también un ticket de [Soporte técnico de Adobe](https://helpx.adobe.com/support.html)

### Cómo reindexar {#how-to-re-index}

>[!NOTE]
>
>En AEM 6.5, [oak-run.jar es el ÚNICO método compatible](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) para la reindexación en repositorios MongoMK o RDBMK.

#### Reindexación de índices de propiedades {#re-indexing-property-indexes}

* Use [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para reindexar el índice de propiedades
* Establezca la propiedad async-reindex en true en el índice de la propiedad

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindexe el índice de propiedad asincrónicamente usando la consola web a través del MBean **PropertyIndexAsyncReindex**;

  por ejemplo,

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindexación de índices de propiedades de Lucene {#re-indexing-lucene-property-indexes}

* Use [oak-run.jar para reindexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) el índice de propiedades de Lucene.
* Establezca la propiedad async-reindex en true en el índice de la propiedad lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sección anterior resume y enmarca la guía de reindexación de Oak de la [documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) en el contexto de AEM.

### Extracción previa de texto de binarios {#text-pre-extraction-of-binaries}

La preextracción de texto es el proceso de extraer y procesar texto de binarios, directamente desde el almacén de datos a través de un proceso aislado y exponer directamente el texto extraído a reindexaciones posteriores de índices Oak.

* Se recomienda la preextracción de texto de Oak para volver a indexar índices Lucene en repositorios con grandes volúmenes de archivos (binarios) que contienen texto extraíble (por ejemplo, PDF, documentos de Word, PPT, TXT, etc.) que cumplen los requisitos para la búsqueda de texto completo mediante índices de Oak implementados; por ejemplo, `/oak:index/damAssetLucene`.
* La preextracción de texto solo beneficia a la reindexación de índices de Lucene y NO a los índices de propiedades de Oak, ya que los índices de propiedades no extraen texto de binarios.
* La preextracción de texto tiene un alto impacto positivo cuando se reindexa texto completo de binarios con gran cantidad de texto (PDF, Doc, TXT, etc.), mientras que un repositorio de imágenes no disfrutará de la misma eficiencia, ya que las imágenes no contienen texto extraíble.
* La preextracción de texto realiza la extracción de texto relacionado con la búsqueda de texto completo de una manera extra eficiente y lo expone al proceso de reindexación de Oak de una manera que es extra eficiente de consumir.

#### ¿Cuándo se puede utilizar la preextracción de texto? {#when-can-text-pre-extraction-be-used}

Reindexando un índice lucene **existing** con extracción binaria habilitada

* Reindexando el procesamiento de **todo** contenido candidato en el repositorio; cuando los binarios de los que se extrae texto completo son numerosos o complejos, se coloca en AEM una mayor carga de cálculo para realizar la extracción de texto completo. La preextracción de texto mueve el &quot;trabajo computacionalmente costoso&quot; de la extracción de texto a un proceso aislado que accede directamente al Almacén de datos de AEM, evitando la sobrecarga y la contención de recursos en AEM.

Se admite la implementación de un índice **new** lucene en AEM con extracción binaria habilitada

* Cuando se implementa un nuevo índice (con extracción binaria habilitada) en AEM, Oak indexa automáticamente todo el contenido candidato en la siguiente ejecución asincrónica de índice de texto completo. Por los mismos motivos descritos anteriormente en la reindexación, esto puede provocar una carga indebida en AEM.

#### ¿Cuándo se puede utilizar la preextracción de texto NO? {#when-can-text-pre-extraction-not-be-used}

La preextracción de texto no se puede utilizar para el nuevo contenido añadido al repositorio, ni es necesaria.

El nuevo contenido se añade al repositorio de forma natural e incremental se indexará mediante el proceso de indexación asincrónica de texto completo (de forma predeterminada, cada 5 segundos).

En el funcionamiento normal de AEM, por ejemplo, al cargar Assets a través de la interfaz de usuario web o la ingesta programática de Assets, AEM indexará de forma automática e incremental el nuevo contenido binario. Dado que la cantidad de datos es incremental y relativamente pequeña (aproximadamente la cantidad de datos que se pueden almacenar en el repositorio en 5 segundos), AEM puede realizar la extracción de texto completo de los binarios durante la indexación sin afectar al rendimiento general del sistema.

#### Requisitos previos para utilizar la preextracción de texto {#prerequisites-to-using-text-pre-extraction}

* Reindexará un índice de Lucene que realiza una extracción binaria de texto completo o implementará un nuevo índice que indexará binarios de texto completo de contenido existente
* El contenido (binarios) del que se extrae previamente el texto debe estar en el repositorio
* Una ventana de mantenimiento para generar el archivo CSV Y para realizar la reindexación final
* Versión de Oak: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versión 1.7.4+
* Una carpeta/recurso compartido del sistema de archivos para almacenar el texto extraído accesible desde las instancias de indexación de AEM

   * La configuración OSGi de preextracción de texto requiere una ruta del sistema de archivos para los archivos de texto extraídos, por lo que deben ser accesibles directamente desde la instancia de AEM (unidad local o montaje del recurso compartido de archivos)

#### Cómo realizar la preextracción de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Los comandos oak-run.jar descritos a continuación están completamente enumerados en [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>El diagrama anterior y los pasos siguientes sirven para explicar y complementar los pasos técnicos de preextracción de texto descritos en la documentación de Apache Oak.

![Flujo del proceso de preextracción de texto](assets/chlimage_1-139.png)

**Generar lista de contenido para preextraer**

*Ejecute el paso 1(a-b) durante una ventana de mantenimiento o un período de poco uso, ya que el almacén de nodos se atraviesa durante esta operación, lo que puede provocar una carga significativa en el sistema.*

1 bis. Ejecute `oak-run.jar --generate` para crear una lista de nodos a los que se extraerá previamente el texto.

1 ter. La lista de nodos (1a) se almacena en el sistema de archivos como archivo CSV

Todo el almacén de nodos se atraviesa (tal como especifican las rutas en el comando oak-run) cada vez que se ejecuta `--generate` y se crea un archivo CSV **nuevo**. El archivo CSV **no** se ha reutilizado entre ejecuciones discretas del proceso de preextracción de texto (pasos 1 a 2).

**Extraer previamente texto al sistema de archivos**

*El paso 2(a-c) se puede ejecutar durante el funcionamiento normal de AEM si sólo interactúa con el almacén de datos.*

2 bis. Ejecute `oak-run.jar --tika` para extraer previamente texto para los nodos binarios enumerados en el archivo CSV generado en (1b)

2 ter. El proceso iniciado en (2a) accede a los nodos binarios definidos en el CSV en el almacén de datos directamente y extrae texto.

2 quater. El texto extraído se almacena en el sistema de archivos en un formato ingerible mediante el proceso de reindexación de Oak (3a)

El texto extraído previamente se identifica en el CSV mediante la huella digital binaria. Si el archivo binario es el mismo, se puede utilizar el mismo texto extraído previamente en todas las instancias de AEM. Dado que AEM Publish suele ser un subconjunto de AEM Author, el texto preextraído de AEM Author también se puede utilizar para reindexar AEM Publish (suponiendo que AEM Publish tenga acceso del sistema de archivos a los archivos de texto extraídos).

El texto extraído previamente se puede añadir gradualmente a a lo largo del tiempo. La preextracción de texto impedirá la extracción de binarios extraídos anteriormente, por lo que es recomendable mantener el texto preextraído en caso de que la reindexación deba volver a ocurrir en el futuro (suponiendo que el contenido extraído no sea prohibitivamente grande). Si es así, evalúe comprimir el contenido de forma provisional, ya que el texto se comprime bien).

**Reindexe índices Oak, obteniendo texto completo de archivos de texto extraídos**

*Ejecute la reindexación (Pasos 3a-b) durante un período de mantenimiento/bajo uso mientras el almacén de nodos se atraviesa durante esta operación, lo que puede incurrir en una carga significativa en el sistema.*

3 bis. Se ha invocado el [reíndice](#how-to-re-index) de índices Lucene en AEM.

3 ter. La configuración OSGi de Apache Jackrabbit Oak DataStore PreExtractTextProvider (configurada para señalar el texto extraído mediante una ruta del sistema de archivos) indica a Oak que obtenga texto completo de los archivos extraídos y evita visitar y procesar directamente los datos almacenados en el repositorio.
