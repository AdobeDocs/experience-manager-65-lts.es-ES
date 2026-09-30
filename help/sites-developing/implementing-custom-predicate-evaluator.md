---
title: Implementación de un evaluador de predicados personalizado para Query Builder
description: El Generador de consultas es una forma sencilla de consultar el repositorio de contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: 5c98915c-e516-4505-9f9e-76f4509ba581
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: 74ec00bc-0862-520e-86dc-e377aeccc141
    internal-label: Search
  - id: 4e98bff0-c1e9-5ae2-adfb-81189dc510c5
    internal-label: Query Builder
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%
---
# Implementación de un evaluador de predicados personalizado para Query Builder{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

En esta sección se describe cómo ampliar [Query Builder](/help/sites-developing/querybuilder-api.md) implementando un evaluador de predicados personalizado.

## Información general {#overview}

[Query Builder](/help/sites-developing/querybuilder-api.md) es una forma sencilla de consultar el repositorio de contenido. CQ se envía con un conjunto de evaluadores de predicados que le ayudan a trabajar con sus datos.

Sin embargo, es posible que desee simplificar las consultas implementando un evaluador de predicados personalizado que oculte cierta complejidad y garantice una mejor semántica.

Un predicado personalizado también podría realizar otras acciones que no son directamente posibles con XPath, por ejemplo:

* buscar algunos datos de algún servicio
* filtrado personalizado basado en el cálculo

>[!NOTE]
>
>Los problemas de rendimiento deben tenerse en cuenta al implementar un predicado personalizado.

>[!NOTE]
>
>Puede encontrar ejemplos de consultas en la sección [Generador de consultas](/help/sites-developing/querybuilder-api.md).

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub.

* [Abra el proyecto aem-search-custom-predicate-evaluator en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### Evaluador de predicados en detalle {#predicate-evaluator-in-detail}

Un evaluador de predicados administra la evaluación de ciertos predicados, que son las restricciones de definición de una consulta.

Asigna una restricción de búsqueda de nivel superior (como &quot;anchura > 200&quot;) a una consulta JCR específica que se ajusta al modelo de contenido real (por ejemplo, metadatos/@width > 200). O puede filtrar manualmente nodos y comprobar sus restricciones.

>[!NOTE]
>
>Para obtener más información sobre `PredicateEvaluator` y el paquete `com.day.cq.search`, consulte la [documentación de Java™](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementación de un evaluador de predicados personalizado para metadatos de replicación {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como ejemplo, esta sección describe cómo crear un evaluador de predicados personalizado que ayude a los datos en función de los metadatos de replicación:

* `cq:lastReplicated` que almacena la fecha de la última acción de replicación

* `cq:lastReplicatedBy` que almacena el identificador del usuario que activó la última acción de replicación

* `cq:lastReplicationAction` que almacena la última acción de replicación (por ejemplo, Activación, Desactivación)

#### Consulta de metadatos de replicación con evaluadores de predicado predeterminados {#querying-replication-metadata-with-default-predicate-evaluators}

La siguiente consulta recupera la lista de nodos de la rama `/content` que han sido activados por `admin` desde el comienzo del año.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Esta consulta es válida, pero difícil de leer y no resalta la relación entre las tres propiedades de replicación. La implementación de un evaluador de predicados personalizado reduce la complejidad y mejora la semántica de esta consulta.

#### Objetivos {#objectives}

El objetivo de `ReplicationPredicateEvaluator` es admitir la consulta anterior mediante la siguiente sintaxis.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Agrupar predicados de metadatos de replicación con un evaluador de predicados personalizado ayuda a crear una consulta significativa.

#### Actualización de dependencias de Maven {#updating-maven-dependencies}

>[!NOTE]
>
>[How to Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md) ha documentado la configuración de nuevos proyectos de Adobe Experience Manager (AEM) usando maven.

En primer lugar, actualice las dependencias Maven del proyecto. El elemento `PredicateEvaluator` forma parte del artefacto `cq-search`, por lo que debe agregarse al archivo pom.xml de Maven.

>[!NOTE]
>
>El ámbito de la dependencia `cq-search` se ha establecido en `provided` porque el contenedor `OSGi` ha proporcionado `cq-search`.

pom.xml

El siguiente fragmento muestra las diferencias en [formato de diferencia unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [pom.xml](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### Escritura De ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

El proyecto `cq-search` contiene la clase abstracta `AbstractPredicateEvaluator`. Esto se puede ampliar con algunos pasos para implementar su propio evaluador de predicados personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>El siguiente procedimiento explica cómo generar una expresión `Xpath` para filtrar datos. Otra opción sería implementar el método `includes` que selecciona los datos en base a filas. Consulte la [documentación de Java™](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) para obtener más información.

1. Cree una clase Java™ que extienda `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Anotar su clase con un `@Component` como el siguiente

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   El siguiente fragmento muestra las diferencias en [formato de diferencia unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```
   @@ -19,8 +19,11 @@
     */
   package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +
   import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
   public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
   }
   ```

   [aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

   >[!NOTE]
   >
   >`factory` debe ser una cadena única que comience por `com.day.cq.search.eval.PredicateEvaluator/` y termine con el nombre de su `PredicateEvaluator` personalizado.

   >[!NOTE]
   >
   >El nombre de `PredicateEvaluator` es el nombre del predicado, que se utiliza al crear consultas.

1. Anular:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   En el método de invalidación, se genera una expresión `Xpath` basada en el argumento `Predicate` dado en.

### Ejemplo de un evaluador de predicados personalizado para metadatos de replicación {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

La implementación completa de este(a) `PredicateEvaluator` puede ser similar a la siguiente clase.

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
