---
title: Crear un índice personalizado para referencias de formulario adaptable
description: Aprenda a crear un índice de Lucene etiquetado para consultas de referencia de formularios adaptables en AEM Forms para evitar consultas de recorrido al publicar fragmentos de experiencias.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 2a0fa18b6c2084cba543425bd9db4b53ac879a58
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 1%
---

# Crear un índice personalizado para referencias de formularios adaptables {#create-custom-index-for-adaptive-forms-references}

Cree un índice de Lucene etiquetado para evitar consultas de recorrido cuando Adobe Experience Manager (AEM) Forms resuelva referencias de formularios adaptables. Sin un índice adecuado, la publicación de un fragmento de experiencia que contenga una referencia de formulario adaptable puede producir una advertencia `Traversal query (query without index)` en los registros.

En AEM Forms 6.5 LTS SP1 y versiones posteriores, la consulta de referencia utiliza la etiqueta de índice `aemformsAFReferences`. Estas versiones incluyen el cambio de consulta, pero debe crear un índice personalizado con esa etiqueta. Este artículo muestra cómo definir e implementar el índice.

Para AEM Forms 6.5, consulte [Crear un índice personalizado para referencias de formularios adaptables en AEM Forms 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references).

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* AEM Forms 6.5 LTS SP1 o posterior, con el complemento Forms correspondiente instalado.
* Acceso para crear un índice bajo `/oak:index` en la instancia de autor.
* Un proyecto de AEM con un módulo `ui.apps` si implementa el índice a través de un paquete de contenido o si tiene acceso a CRXDE Lite como alternativa de desarrollo.

Pruebe el índice en un entorno de ensayo o desarrollo antes de implementarlo en producción. [Crear un índice puede llevar tiempo en un repositorio grande](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes).

## Definición del índice personalizado {#define-the-custom-index}

Cree el índice en `/oak:index/customAFReferenceLuceneIndex-1`. Puede elegir un nombre de nodo de índice diferente, pero mantenga la etiqueta `aemformsAFReferences` sin cambios para que la consulta de referencia de Forms pueda seleccionar el índice.

Utilice la siguiente definición. Indexa `sling:resourceType` en `nt:unstructured` nodos bajo `/content`.

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

No agregue `analyzed=true`. La consulta de referencia usa restricciones de propiedad en lugar de una condición de `contains` de texto completo, por lo que no es necesario establecer esta configuración.

## Implementación del índice con un paquete de contenido {#deploy-the-index-with-a-content-package}

Utilice un paquete de contenido para implementaciones de producción.

1. En el módulo `ui.apps` de su proyecto de AEM, cree `ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`.
1. Cree `.content.xml` en ese directorio con la siguiente definición:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. Agregue el siguiente filtro dentro del elemento `workspaceFilter` existente en `ui.apps/src/main/content/META-INF/vault/filter.xml`. Mantenga los demás filtros del proyecto sin cambios.

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. Genere el proyecto utilizando su configuración de generación existente e instale el paquete de contenido resultante en la instancia de autor. Para obtener instrucciones de carga e instalación de paquetes, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system).
1. Confirme que `/oak:index/customAFReferenceLuceneIndex-1` existe. Permita que la indexación asíncrona se complete antes de comprobar el plan de consulta.

Si elige un nombre de índice diferente, utilice ese nombre de forma coherente en el directorio, filtro y ruta de acceso al repositorio.

## Creación del índice con CRXDE Lite {#create-the-index-with-crxde-lite}

Utilice esta alternativa en un entorno de desarrollo en lugar del método de paquete de contenido.

Utilice las siguientes propiedades al crear el nodo de índice:

| Propiedad | Tipo | Valor |
| --- | --- | --- |
| `selectionPolicy` | Cadena | `tag` |
| `compatVersion` | Largo | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | Cadena | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | Booleano | `true` |
| `reindex` | Booleano | `false` |

`String[]` significa una propiedad String de varios valores, incluso cuando contiene sólo un valor.

1. Abra `http://localhost:4502/crx/de/index.jsp`. Reemplace el host y el puerto por los de la instancia de autor.
1. Navegue hasta `/oak:index`. Haga clic con el botón derecho en el nodo y seleccione [!UICONTROL Crear] > [!UICONTROL Crear nodo].
1. Crear `customAFReferenceLuceneIndex-1` con tipo `oak:QueryIndexDefinition`.
1. Agregue las propiedades de la tabla anterior al nodo de índice.
1. En el nodo de índice, cree la siguiente jerarquía de nodos secundarios. Establezca el tipo de cada nodo secundario en `nt:unstructured`:

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. El `resourceType`, agregue `name` (cadena) con el valor `sling:resourceType` y `propertyIndex` (booleano) con el valor `true`.
1. Seleccione [!UICONTROL Guardar todo] y permita que se complete la indexación asincrónica.

## Compruebe que la consulta utiliza el índice {#verify-that-the-query-uses-the-index}

Compruebe el plan de consultas para confirmar que la consulta de referencia selecciona el índice personalizado.

1. Confirme que la indexación asíncrona ha finalizado. Use [Administrador de índices](/help/sites-administering/operations-dashboard.md#the-index-manager) para inspeccionar el estado del índice.
1. Abra [!UICONTROL Herramientas] > [!UICONTROL Operaciones] > [!UICONTROL Diagnóstico] > [!UICONTROL Rendimiento de la consulta] y seleccione [!UICONTROL Explicar consulta]. Seleccione el idioma de consulta XPath e introduzca:

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. Seleccione [!UICONTROL Explicar]. Confirme que el plan utiliza `lucene:customAFReferenceLuceneIndex-1` y `/oak:index/customAFReferenceLuceneIndex-1`, o el nombre de índice elegido, para las ramas de la consulta en lugar de un plan de recorrido. Para obtener más información, consulte [Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query).
1. Repita la operación de publicación del fragmento de experiencia que produjo la advertencia. Buscar nuevas advertencias de recorrido de `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences` en `error.log`.

Si el plan no selecciona el índice personalizado, compare la etiqueta, la jerarquía `indexRules` y la definición de propiedad `sling:resourceType` con los ejemplos anteriores. Para obtener más información, consulte [Solución de problemas de índices Oak](/help/sites-deploying/troubleshooting-oak-indexes.md).

## Tareas relacionadas {#related-tasks}

Para obtener más información sobre el rendimiento de las consultas y la configuración de índices, consulte:

* [Consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md)
* [Prácticas recomendadas para consultas e indexación](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Solución de problemas de consultas lentas](/help/sites-developing/troubleshooting-slow-queries.md)
