---
title: Actualización de Forms de búsqueda personalizada
description: Este artículo detalla los ajustes necesarios después de una actualización para que funcionen los formularios de búsqueda personalizados.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Actualización de Forms de búsqueda personalizada{#upgrading-custom-search-forms}

En AEM 6.2, la ubicación donde se almacenan los Forms de búsqueda personalizados en el repositorio ha cambiado. Al realizar la actualización, se les trasladará de su ubicación en 6.1 en:

* /apps/cq/gui/content/facets

a una nueva ubicación en:

* /conf/global/settings/cq/search/facets

Debido a esto, se requieren ajustes manuales después de una actualización para que los formularios sigan funcionando.

Esto se aplica a los nuevos Forms de búsqueda y Forms predeterminados que se han personalizado.

Para obtener más información, consulte la documentación sobre [Facetas de búsqueda](/help/assets/search-facets.md).

## Modificación de la propiedad resourceType {#changing-the-resourcetype-property}

A menos que se indique lo contrario, la mayoría de los ajustes que deben realizarse después de la actualización requieren cambiar la propiedad `sling:resourceType` para el Forms de búsqueda personalizado configurado. Esto es necesario para que la propiedad apunte a la ubicación correcta del script de procesamiento.

Puede cambiar la propiedad haciendo lo siguiente:

1. Abra CRXDE Lite yendo a `https://server:port/crx/de/index.jsp`
1. Vaya a la ubicación del nodo que debe ajustarse, como se especifica en la lista de [Forms de búsqueda personalizada](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) que aparece a continuación.
1. Haga clic en el nodo. En el panel de propiedades derecho, haga clic en y modifique la propiedad **sling:resourceType**.
1. Finalmente, guarde los cambios presionando el botón **Guardar todo**.

## Lista de Forms de búsqueda personalizada {#list-of-custom-search-forms}

A continuación, encontrará una lista de todos los Forms de búsqueda personalizados y las modificaciones que requieren después de la actualización. Hacen referencia a los nombres de `/conf/global/settings/cq/search/facets/sites/items`.

### Predicado de texto completo con nombre de nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nodo/s en el formulario de búsqueda predeterminado en 6.1</td>
   <td>texto completo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

En AEM 6.1, el predicado de texto completo estándar formaba parte del formulario de búsqueda. En la versión 6.2, el campo de texto completo se ha sustituido por OmniSearch. Este predicado se omite mediante programación y se puede eliminar.

**Acción:** Elimine el nodo por completo.

### Otros predicados de texto completo {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodos en la búsqueda predeterminada Desde en 6.1</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicados del explorador de rutas {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicados de etiquetas {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>etiquetas</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad **resourceType** (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de estado de la página {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

El estado de página se ha reemplazado por dos predicados de propiedad de opciones, uno para la publicación y otro para el estado de LiveCopy.

**Acciones:**

* Quitar el nodo `pagestatuspredicate`
* Copiar nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * hasta `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copiar nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * hasta `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Asegúrese de establecer la propiedad `listOrder` para el nodo `analyticspredicate` en &quot;**8**&quot;. Esto es necesario para evitar conflictos.

### Predicados de intervalo de fechas {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Filtro oculto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** No hay nada que ajustar.

### Predicado de Analytics {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>predicado analítico</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de intervalo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

>[!NOTE]
>
>Nota: A diferencia de 6.1, el predicado de rango ya no representa una etiqueta en la barra de búsqueda.

### Predicado de propiedad de opciones {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de intervalo del regulador {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de componentes {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de autor {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicado de plantillas {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodos en el formulario de búsqueda predeterminado en 6.1<br /> <br /> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso en 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso en 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

## Carril de búsqueda de administración de recursos {#assets-admin-search-rail}

Los nodos siguientes hacen referencia a los nombres de `/conf/global/settings/dam/search/facets/assets/items`

### Predicado de texto completo con nombre de nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | texto completo |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo de recurso en 6.2 | N/D |

En la versión 6.1, el predicado de texto completo estándar formaba parte del formulario de búsqueda. En 6.2, el campo de texto completo ha sido reemplazado por OmniSearch. Este predicado se omite mediante programación y se puede eliminar.

**Acción:** Quite el nodo mencionado anteriormente.

### Predicados del explorador de rutas {#path-browser-predicates-1}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | pathbrowser |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicados de tipo MIME {#mime-type-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | tipo MIME |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba).

### Predicados de tamaño de archivo {#file-size-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | tamaño de archivo |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Acción:** Ajustar `resourceType` como se muestra en la ubicación 6.2 anterior.

### Predicados de última modificación del recurso {#asset-last-modified-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Acción: ajuste la propiedad resourceType (agregue &quot;/coral&quot; como en la ubicación 6.2 indicada arriba).

### Publicar predicado {#publish-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | publicación |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**Acciones:**

* Ajustar la propiedad `resourceType` (agregar &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

* Agregue una propiedad `optionPaths` (de tipo cadena) con el valor: `/libs/dam/options/predicates/publish`

* Agregue la propiedad `singleSelect` con el valor booleano `true`.

### Predicados de estado {#status-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | status |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

### Predicados de estado de caducidad {#expiry-status-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | expirystatus |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

### Predicados de validez de metadatos {#metadata-validity-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | metadatavalidez |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

### Predicados de clasificación {#rating-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | clasificación |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

### Predicado de orientación {#orientation-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | Orientación |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso en 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Acciones:**

* Ajustar la propiedad `resourceType` (agregar &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

* Agregue una propiedad `fieldLabel` con el mismo valor que la propiedad `text` en el mismo nodo.

* Agregue una propiedad `emptyText` con el mismo valor que la propiedad `text` en el mismo nodo.

* Agregue una propiedad `rootPath` con el mismo valor que la propiedad `optionPaths` en el mismo nodo.

### Predicado de estilo {#style-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | estilo |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso en 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Acciones:**

* Ajustar la propiedad `resourceType` (agregar &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

* Agregue una propiedad `fieldLabel` con el mismo valor que la propiedad `text` en el mismo nodo.

* Agregue una propiedad `emptyText` con el mismo valor que la propiedad `text` en el mismo nodo.

* Agregue una propiedad `rootPath` con el mismo valor que la propiedad `optionPaths` en el mismo nodo.

### Predicados de formato de vídeo {#video-format-predicates}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | videoFormat |
|---|---|
| Tipo de recurso en 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso en 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)

### Predicado Mainasset {#mainasset-predicate}

| Nodo/s en el formulario de búsqueda predeterminado en 6.1 | recurso principal |
|---|---|
| Tipo de recurso en 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo de recurso en 6.2 | granite/ui/components/coral/foundation/form/hidden |

**Acción:** Ajuste la propiedad `resourceType` (agregue &quot;**/coral**&quot; como en la ubicación 6.2 indicada arriba)
