---
title: Referencia de predicados del generador de consultas
description: Referencia de predicado completa para la API de Query Builder.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: c044d541-24d6-4975-9b38-6a4317a16358
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 2%

---

# Referencia de predicados del generador de consultas{#query-builder-predicate-reference}

>[!CAUTION]
>
>La información de esta página no es exhaustiva.
>
>Para obtener información completa, consulte la lista en **Predicados disponibles** en la consola de Query Builder Debugger; por ejemplo, en:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Por ejemplo, consulte:
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## General {#general}

* [raíz](#root)
* [grupo](#group)
* [orderby](#orderby)

## Predicados {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [intervalo de fechas](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [texto completo](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [recurso principal](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nombre de nodo](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [propiedad](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeProperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [parecido](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [etiqueta](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Coincide en las propiedades BOOLEANAS JCR. Solo acepta los valores &quot; `true`&quot; y &quot; `false`&quot;. Si &quot;`false`&quot;, coincide si la propiedad tiene el valor &quot;`false`&quot; o si no existe. Esto puede resultar útil para comprobar si hay indicadores booleanos que solo se establecen cuando están habilitados.

El parámetro &quot; `operation`&quot; heredado no tiene significado.

Admite extracción de facetas. Proporciona bloques para cada valor `true` o `false`, pero solo para las propiedades existentes.

#### Propiedades {#properties}

* **boolproperty**
Ruta relativa a la propiedad, por ejemplo, `myFeatureEnabled` o `jcr:content/myFeatureEnabled`.

* **valor**
Valor para comprobar la propiedad de &quot;`true`&quot; o &quot;`false`&quot;.

### contentfragment {#contentfragment}

Restringe el resultado a fragmentos de contenido.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-1}

* **fragmento de contenido**
Se puede utilizar con cualquier valor para comprobar fragmentos de contenido.

### dateComparison {#datecomparison}

Compara dos propiedades JCR DATE entre sí. Puede comprobar si son iguales, desiguales, mayores o mayores que o iguales.

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

#### Propiedades {#properties-2}

* **propiedad1**

  Ruta a la primera propiedad de fecha.

* **propiedad2**

  Ruta a la segunda propiedad de fecha.

* **operación**

  &quot; `equals`&quot; para la coincidencia exacta, &quot; `!=`&quot; para la comparación de desigualdad, &quot; `greater`&quot; para la propiedad1 mayor que la propiedad2, &quot; `>=`&quot; para la propiedad1 mayor o igual que la propiedad2. El valor predeterminado es &quot; `equals`&quot;.

### intervalo de fechas {#daterange}

Hace coincidir las propiedades DATE de JCR con un intervalo de fecha y hora. Utiliza la norma ISO8601
formato para fechas y horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) y también permite representaciones parciales, como `YYYY-MM-DD`. Alternativamente, la marca de tiempo se puede proporcionar como el número de milisegundos desde 1970 en la zona horaria UTC, el formato de hora UNIX®.

Puede buscar cualquier cosa entre dos marcas de tiempo, cualquier cosa más reciente o anterior a una fecha determinada, y también elegir entre intervalos inclusivos y abiertos.

Admite extracción de facetas. Proporciona bloques &quot;hoy&quot;, &quot;esta semana&quot;, &quot;este mes&quot;, &quot;los últimos 3 meses&quot;, &quot;este año&quot;, &quot;el año pasado&quot; y &quot;antes del año pasado&quot;.

No admite el filtrado.

#### Propiedades {#properties-3}

* **propiedad**

  Ruta relativa a una propiedad `DATE`, por ejemplo, `jcr:lastModified`.

* **lowerBound**

  La fecha inferior enlazada a la propiedad check de, por ejemplo, `2014-10-01`.

* **lowerOperation**

  &quot; `>`&quot; (más reciente) o &quot; `>=`&quot; (más reciente o más reciente) se aplica a `lowerBound`. El valor predeterminado es &quot; `>`&quot;.

* **upperBound**

  Límite superior para comprobar la propiedad de, por ejemplo, `2014-10-01T12:15:00`.

* **upperOperation**

  &quot; `<`&quot; (anterior) o &quot; `<=`&quot; (igual o anterior) se aplica a `upperBound`. El valor predeterminado es &quot; `<`&quot;.

* **zona horaria**

  ID de zona horaria que se utilizará cuando no se proporcione como cadena de fecha ISO-8601. El valor predeterminado es la zona horaria predeterminada del sistema.

### excludepaths {#excludepaths}

Excluye nodos del resultado donde su ruta coincida con una expresión regular.

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

No admite la extracción de facetas.

#### Propiedades {#properties-4}

* **excludepaths**

  Expresión regular comparada con las rutas de resultados, excluyendo las coincidentes del resultado.

### texto completo {#fulltext}

Busca términos en el índice de texto completo.

No admite el filtrado.

No admite la extracción de facetas.

#### Propiedades {#properties-5}

* **texto completo**

  Los términos de búsqueda de texto completo.

* **relPath**

  La ruta relativa a la búsqueda en la propiedad o subnodo. Esta propiedad es opcional.

### grupo {#group}

Permite crear condiciones anidadas. Los grupos pueden contener grupos anidados. Todo lo que hay en una consulta del generador de consultas está implícito en un grupo raíz, que también puede tener `p.or` y `p.not` parámetros.

Ejemplo de coincidencia de una de las dos propiedades con un valor:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceptualmente es `(1_property` O `2_property)`.

Ejemplo para grupos anidados:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Esto busca el término &quot;**Administración**&quot; en las páginas de `/content/geometrixx/en` o en los recursos de `/content/dam/geometrixx`.

Conceptualmente es `fulltext AND ( (path AND type) OR (path AND type) )`. Estas uniones OR necesitan buenos índices para el rendimiento.

#### Propiedades {#properties-6}

* **p.o**

  Si se establece en &quot;`true`&quot;, solo debe coincidir un predicado del grupo. El valor predeterminado es &quot; `false`&quot;, lo que significa que todos deben coincidir

* **p.not**

  Si se establece en &quot; `true`&quot;, se anula el grupo (el valor predeterminado es &quot; `false`&quot;).

* **&lt;predicado>**

  Agrega predicados anidados.

* **N_&lt;predicado>**

  Agrega varios predicados anidados al mismo tiempo, como `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Restringe el resultado a elementos en los que la sesión actual tiene los [privilegios JCR especificados.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-7}

* **hasPermission**

  Privilegios JCR separados por comas que la sesión de usuario actual debe tener TODOS el nodo en cuestión. Por ejemplo, `jcr:write`, `jcr:modifyAccessControl`.

### language {#language}

Busca páginas de CQ en un idioma específico. Esto tiene en cuenta tanto la propiedad de idioma de la página como la ruta de página que a menudo incluye el idioma o la configuración regional en una estructura de sitio de nivel superior.

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite extracción de facetas. Proporciona bloques para cada código de lenguaje único.

#### Propiedades {#properties-8}

* **idioma**

  Código de idioma ISO, por ejemplo, &quot;`de`&quot;

### recurso principal {#mainasset}

Comprueba si un nodo es un recurso principal DAM y no un subrecurso. Básicamente, se trata de todos los nodos que no están dentro de un nodo &quot;subrecursos&quot;. Esto no comprueba el tipo de nodo `dam:Asset`. Para utilizar este predicado, establezca &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, no hay más propiedades.

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda.

Admite la extracción de facetas y proporciona dos contenedores para recursos principales y secundarios.

#### Propiedades {#properties-9}

* **recurso principal**

  Booleano, &quot; `true`&quot; para recursos principales, &quot; `false`&quot; para subrecursos.

### memberOf {#memberof}

Busca elementos que sean miembros de una [colección de recursos de sling](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) específica.

Este es un predicado solo de filtrado y no puede utilizar un índice de búsqueda. No admite la extracción de facetas.

#### Propiedades {#properties-10}

* **memberOf**

  Ruta de la colección de recursos de Sling.

### nombre de nodo {#nodename}

Coincide con los nombres de nodo JCR.

Admite extracción de facetas. Proporciona bloques para cada nombre de nodo único (nombre de archivo).

#### Propiedades {#properties-11}

* **nombre de nodo**

  Patrón de nombre de nodo que permite caracteres comodín: `*` = cualquiera o ningún carácter, `?` = cualquier carácter, `[abc]` = solo caracteres entre corchetes.

### notexpired {#notexpired}

Coincide con los elementos comprobando si una propiedad JCR DATE es mayor o igual que la hora actual del servidor. Se puede usar para comprobar una propiedad de &quot;`expiresAt`&quot; como fecha y limitar solo a las que aún no hayan caducado (`notexpired=true`) o que ya hayan caducado (`notexpired=false`).

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado daterange.

#### Propiedades {#properties-12}

* **notexpired**

  Booleano, &quot; `true`&quot; para no caducado aún (fecha futura o igual), &quot; `false`&quot; para caducado (fecha anterior) (obligatorio).

* **propiedad**

  Ruta relativa a la propiedad `DATE` que se va a comprobar (obligatorio).

### orderby {#orderby}

Permite ordenar los resultados. Si se requiere ordenar por varias propiedades, este predicado debe agregarse varias veces utilizando el prefijo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propiedades {#properties-13}

* **orderby**

  Nombre de propiedad JCR indicado por una @ inicial, por ejemplo, `@jcr:lastModified` o `@jcr:content/jcr:title`, o por otro predicado de la consulta, por ejemplo, `2_property`, en el que ordenar.

* **ordenar**

  Dirección de orden: &quot;`desc`&quot; para descendente o &quot;`asc`&quot; para ascendente (predeterminado).

* **caso**

  Si se establece en `ignore`, la ordenación no distingue entre mayúsculas y minúsculas, lo que significa que &quot;a&quot; va antes que &quot;B&quot;; si está vacía o se omite, la ordenación distingue entre mayúsculas y minúsculas, lo que significa que &quot;B&quot; va antes que &quot;a&quot;

### path {#path}

Busca dentro de una ruta determinada.

No admite la extracción de facetas.

#### Propiedades {#properties-14}

* **ruta**

  Patrón de ruta. Dependiendo de lo exacto, todo el subárbol coincide (como anexar `//*` en xpath, pero tenga en cuenta que esto no incluye la ruta base) (exacto=false, predeterminado), o solo una coincidencia de ruta exacta, que puede incluir caracteres comodín ( `*`); si se establece self, se busca todo el subárbol, incluido el nodo base.

* **exacto**

  Si `exact` es verdadero/activado, la ruta de acceso exacta debe coincidir, pero puede contener caracteres comodín simples ( `*`), que coincidan con los nombres, pero no con &quot; `/`&quot;; si es falso (predeterminado), se incluyen todos los descendientes (opcional).

* **piso**

  Busca sólo los elementos secundarios directos (como anexar &quot;`/*`&quot; en xpath) (sólo se usa si &#39;`exact`&#39; no es true, opcional).

* **auto**

  Busca en el subárbol pero incluye el nodo base dado como ruta (sin comodines).

### propiedad {#property}

Coincide en las propiedades JCR y sus valores.

Admite extracción de facetas. Proporciona bloques para cada valor de propiedad único en los resultados.

#### Propiedades {#properties-15}

* **propiedad**

  Ruta relativa a la propiedad, por ejemplo, `jcr:title`.

* **valor**

  Valor para comprobar la propiedad; sigue el tipo de propiedad JCR a las conversiones de cadena.

* **Valor_N**

  Use `1_value`, `2_value`, ... para buscar varios valores (combinados con `OR` de forma predeterminada, con `AND` si y = true) (desde 5.3).

* **y**

  Establezca como true para combinar varios valores (`N_value`) con AND (desde 5.3).

* **operación**

  &quot;`equals`&quot; para coincidencia exacta (predeterminado), &quot; `unequals`&quot; para comparación de desigualdad, &quot; `like`&quot; para usar la función xpath `jcr:like` (opcional), &quot; `not`&quot; para que no haya coincidencia (por ejemplo, &quot;`not(@prop)`&quot; en xpath, parámetro value se omite) o &quot; `exists`&quot; para la comprobación de existencia (el valor puede ser true - la propiedad debe existir, el valor predeterminado - o false - igual que &quot; `not`&quot;).

* **profundidad**

  Número de niveles de comodín bajo los cuales puede existir la propiedad o ruta relativa (por ejemplo, `property=size depth=2` comprueba nodo/tamaño, node/&amp;ast;/size y node/&amp;ast;/&amp;ast;/size).

### rangeProperty {#rangeproperty}

Hace coincidir una propiedad JCR con un intervalo. Esto se aplica a propiedades con tipos lineales como `LONG`, `DOUBLE` y `DECIMAL`. Para `DATE`, consulte el predicado daterange que ha optimizado la entrada de formato de fecha.

Puede definir un límite inferior y un límite superior o solo uno de ellos. La operación (por ejemplo, &quot;menor que&quot; o &quot;menor o igual que&quot;) también se puede especificar para los límites inferior y superior, individualmente.

No admite la extracción de facetas.

#### Propiedades {#properties-16}

* **propiedad**

  Ruta relativa a la propiedad.

* **lowerBound**

  Límite inferior para comprobar la propiedad de.

* **lowerOperation**

  &quot; `>`&quot; (predeterminado) o &quot; `>=`&quot;, se aplica a `lowerValue`

* **upperBound**

  Límite superior para comprobar la propiedad de.

* **upperOperation**

  &quot; `<`&quot; (predeterminado) o &quot; `<=`&quot;, se aplica a `lowerValue`

* **decimal**

  &quot; `true`&quot; si la propiedad marcada es de tipo Decimal

### relativedaterange {#relativedaterange}

Hace coincidir las propiedades de `JCR DATE` con un intervalo de fecha y hora mediante desplazamientos de tiempo en relación con la hora actual del servidor. Puede especificar `lowerBound` y `upperBound` mediante un valor de milisegundos o la sintaxis de bugzilla `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses, siete años). El prefijo &quot;`-`&quot; indica un desplazamiento negativo antes de la hora actual. Si solo especifica `lowerBound` o `upperBound`, el otro valor predeterminado es 0, es decir, la hora actual.

Por ejemplo:

* `upperBound=1h` (y ningún `lowerBound`) seleccionaría nada en la siguiente hora
* `lowerBound=-1d` (y ningún `upperBound`) seleccionaría nada en las últimas 24 horas
* `lowerBound=-6M` y `upperBound=-3M` seleccionarían cualquier cosa de 6 meses a 3 meses de edad
* `lowerBound=-1500` y `upperBound=5500` seleccionarían cualquier valor entre 1500 milisegundos en el pasado y 5500 milisegundos en el futuro
* `lowerBound=1d` y `upperBound=2d` seleccionarían cualquier cosa pasado mañana

No tiene en cuenta los años bisiestos y todos los meses son 30 días.

No admite el filtrado.

Admite la extracción de facetas del mismo modo que el predicado daterange.

#### Propiedades {#properties-17}

* **upperBound**

  La fecha superior enlazada en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses o siete años) con respecto al tiempo actual del servidor, utilice &quot;-&quot; para el desplazamiento negativo.

* **lowerBound**

  Reduzca el límite de la fecha en milisegundos o `1s 2m 3h 4d 5w 6M 7y` (un segundo, dos minutos, tres horas, cuatro días, cinco semanas, seis meses o siete años) en relación con el tiempo actual del servidor, use &quot;-&quot; para el desplazamiento negativo.

### raíz {#root}

Grupo de predicados raíz. Admite todas las funciones de un grupo y permite establecer parámetros de consulta globales.

El nombre &quot;root&quot; nunca se utiliza en una consulta, está implícito.

#### Propiedades {#properties-18}

* **p.offset**

  Número que indica el inicio de la página de resultados, es decir, cuántos elementos se deben omitir.

* **p.limit**

  Número que indica el tamaño de página.

* **p.guessTotal**

  Recomendado: evite calcular el total del resultado completo, que puede resultar costoso; ya sea un número que indique el total máximo que se va a contar hasta (por ejemplo, 1000, un número que proporcione a los usuarios suficientes comentarios sobre el tamaño aproximado y los números exactos para resultados más pequeños) o &quot; `true`&quot; para contar solo hasta el mínimo necesario `p.offset` + `p.limit`.

* **p.extracto**

  Si se establece en &quot; `true`&quot;, incluya un extracto de texto completo en el resultado.

* **p.hits**

  (solo para el servlet JSON) seleccione la forma en que se escriben las visitas como JSON, con estas estándar (ampliables mediante el servicio ResultHitWriter):

   * **simple**:

     Elementos mínimos como `path`, `title`, `lastmodified`, `excerpt` (si se establecieron).

   * **completo**:

     Representación del nodo JSON de Sling, con `jcr:path` indicando la ruta de la visita: de forma predeterminada solo enumera las propiedades directas del nodo, incluya un árbol más profundo con `p.nodedepth=N`, con 0 que significa todo el subárbol infinito; agregue `p.acls=true` para incluir los permisos JCR de la sesión actual en el elemento de resultado dado (asignaciones: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **selectivo**:

     Solo las propiedades especificadas en `p.properties`, que es una lista de rutas relativas separadas por espacios (utilice &quot;+&quot; en las direcciones URL); si la ruta relativa tiene una profundidad > 1, estas se representan como objetos secundarios; la propiedad especial jcr:path incluye la ruta de la visita

### savedquery {#savedquery}

Incluye todos los predicados de una consulta del generador de consultas persistente en la consulta actual como predicado de subgrupo.

Esto no ejecuta una consulta adicional, sino que amplía la consulta actual.

Las consultas se pueden mantener mediante programación usando `QueryBuilder#storeQuery()`. El formato puede ser una propiedad String multilínea o un nodo `nt:file` que contenga la consulta como archivo de texto en formato de propiedades Java™.

No admite la extracción de facetas para los predicados de la consulta guardada.

#### Propiedades {#properties-19}

* **savedquery**

  Ruta de acceso a la consulta guardada (propiedad String o nodo `nt:file`).

### parecido {#similar}

Búsqueda por similitud utilizando `rep:similar()` de JCR XPath.

No admite el filtrado. No admite la extracción de facetas.

#### Propiedades {#properties-20}

* **similar**
Ruta absoluta al nodo para el que se buscarán nodos similares.

* **local**
Una ruta relativa a un nodo descendiente o `.` para el nodo actual (opcional, el valor predeterminado es &quot; `.`&quot;).

### etiqueta {#tag}

Busca contenido etiquetado con una o más etiquetas, especificando las rutas de título de las etiquetas.

Admite extracción de facetas. Proporciona bloques para cada etiqueta única, utilizando su ruta de título de etiqueta actual.

#### Propiedades {#properties-21}

* **etiqueta**

  Etiquete la ruta del título que desee buscar, por ejemplo, &quot;Propiedades del recurso : Orientación / Horizontal&quot;.

* **Valor_N**

  Use `1_value`, `2_value`, ... para buscar varias etiquetas (combinadas con `OR` de forma predeterminada, con `AND` si y = true) (desde 5.6).

* **propiedad**

  Propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado &quot; `cq:tags`&quot;)

### tagid {#tagid}

Busca contenido etiquetado con una o más etiquetas, especificando los ID de etiqueta.

Admite extracción de facetas. Proporciona bloques para cada etiqueta única, utilizando su ID de etiqueta actual.

#### Propiedades {#properties-22}

* **tagid**

  Id. de etiqueta para que pueda buscar, por ejemplo, &quot;`properties:orientation/landscape`&quot;.

* **Valor_N**

  Use `1_value`, `2_value`, ... para buscar varios tagids (combinados con `OR` de forma predeterminada, con `AND` si y = true) (desde 5.6).

* **propiedad**

  Propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado &quot; `cq:tags`&quot;).

### tagsearch {#tagsearch}

Busca contenido etiquetado con una o más etiquetas, especificando palabras clave. Primero busca las etiquetas que contienen estas palabras clave en sus títulos y luego restringe el resultado a solo los elementos etiquetados con estas palabras clave.

No admite la extracción de facetas.

#### Propiedades {#Properties-1}

* **tagsearch**

  Palabra clave para buscar en títulos de etiquetas.

* **propiedad**

  Propiedad (o ruta relativa a la propiedad) que se va a ver (valor predeterminado `cq:tags`).

* **lang**

  Para buscar únicamente en un determinado título de etiqueta localizado (por ejemplo, `de`).

* **todo**

  (Bool) Busque texto completo de la etiqueta, es decir, todos los títulos, descripciones, etc. Tiene prioridad sobre &quot;l `ang`&quot;.

### tipo {#type}

Restringe los resultados a un tipo de nodo JCR específico, tanto del tipo de nodo principal como del tipo de mezcla. Esto también encuentra subtipos de ese tipo de nodo. Los índices de búsqueda del repositorio deben cubrir los tipos de nodo para una ejecución eficiente.

Admite extracción de facetas. Proporciona bloques para cada tipo único en los resultados.

#### Propiedades {#Properties-2}

* **tipo**

  Tipo de nodo o nombre de mezcla que buscar, por ejemplo, `cq:Page`.
