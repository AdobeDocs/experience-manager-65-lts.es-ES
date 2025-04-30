---
title: Creación de etiquetas en una aplicación de AEM
description: Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Developing,Tagging
solution: Experience Manager, Experience Manager Sites
role: Developer
exl-id: c835a110-89cf-4857-9ee0-c0ad781a66ae
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Creación de etiquetas en una aplicación de AEM{#building-tagging-into-an-aem-application}

Para trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de AEM personalizada, esta página describe el uso de

* [API de etiquetado](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/tagging/package-summary.html)

Que interactúa con el

* [Marco de etiquetado](/help/sites-developing/framework.md)

Para obtener información relacionada con el etiquetado, consulte:

* [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre cómo crear y administrar etiquetas, y a qué etiquetas de contenido se han aplicado.
* [Usando etiquetas](/help/sites-authoring/tags.md) para obtener información sobre cómo etiquetar contenido.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación del [marco de etiquetado](/help/sites-developing/framework.md) en AEM permite administrar las etiquetas y el contenido de las etiquetas mediante la API de JCR TagManager garantiza que las etiquetas introducidas como valores en la propiedad de matriz de cadenas `cq:tags` no se dupliquen, elimina los TagID que apuntan a etiquetas no existentes y actualiza los TagID para las etiquetas movidas o combinadas. TagManager utiliza un detector de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en el paquete [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* JcrTagManagerFactory: devuelve una implementación basada en JCR de `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager`: permite resolver y crear etiquetas por rutas y nombres.
* `Tag`: define el objeto de etiqueta.

### Obtener un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia de TagManager, debe tener un JCR `Session` y llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling, también puede adaptarse a `TagManager` desde `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

Se puede recuperar un(a) `Tag` a través de `TagManager`, resolviendo una etiqueta existente o creando una:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` al JCR `Nodes`, puede utilizar directamente el mecanismo `adaptTo` de Sling si tiene el recurso (por ejemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Aunque una etiqueta solo se puede convertir *de *un recurso (no un nodo), una etiqueta se puede convertir *a *un nodo y un recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>No es posible adaptarse directamente de `Node` a `Tag`, ya que `Node` no implementa el método Sling `Adaptable.adaptTo(Class)`.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Búsqueda de etiquetas {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>El `RangeIterator` válido que se va a usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de etiquetas {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación (`Replicator`) con etiquetas porque las etiquetas son del tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Etiquetado en el lado del cliente {#tagging-on-the-client-side}

El widget de formulario `CQ.tagging.TagInputField` sirve para escribir etiquetas. Tiene un menú emergente para seleccionar entre las etiquetas existentes, incluye finalización automática y muchas otras funciones. Su xtype es `tags`.

## El recolector de basura de etiquetas {#the-tag-garbage-collector}

El recolector de etiquetas es un servicio en segundo plano que limpia las etiquetas ocultas y no utilizadas. Las etiquetas ocultas y no utilizadas son etiquetas por debajo de `/content/cq:tags` que tienen una propiedad `cq:movedTo` y no se utilizan en un nodo de contenido; tienen un recuento de cero. Al utilizar este proceso de eliminación diferida, no es necesario actualizar el nodo de contenido (es decir, la propiedad `cq:tags`) como parte de la operación de mover o combinar. Las referencias en la propiedad `cq:tags` se actualizan automáticamente cuando se actualiza la propiedad `cq:tags`, por ejemplo, a través del cuadro de diálogo de propiedades de página.

El recolector de elementos no utilizados se ejecuta de forma predeterminada una vez al día. Puede configurarlo en:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Búsqueda de etiquetas y Listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de TagID busca las etiquetas que tienen la propiedad `cq:movedTo` establecida en TagID y sigue a través de `cq:movedTo` TagIDs.

* La búsqueda de Título de etiqueta solo busca las etiquetas que no tienen una propiedad `cq:movedTo`.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Como se describe en la documentación para la administración de etiquetas, en la sección [Administración de etiquetas en diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), una etiqueta `title`se puede definir en diferentes idiomas. A continuación, se agrega una propiedad sensible al idioma al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo, `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúsculas y usar &quot;_&quot; en lugar de &quot;-&quot;, por ejemplo: `de_ch`.

Cuando se agrega la etiqueta **Animals** a la página **Productos**, el valor `stockphotography:animals` se agrega a la propiedad `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Se hace referencia a la traducción desde el nodo de etiqueta.

La API del lado del servidor ha localizado `title` métodos relacionados:

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Configuración regional)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Configuración regional)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Configuración regional)
   * createTagByTitle(String tagTitlePath, Configuración regional)
   * resolveByTitle(String tagTitlePath, Configuración regional)

En AEM, el idioma se puede obtener del idioma de la página o del idioma del usuario:

* para recuperar el idioma de la página en un JSP:

   * `currentPage.getLanguage(false)`

* para recuperar el idioma del usuario en un JSP:

   * `slingRequest.getLocale()`

`currentPage` y `slingRequest` están disponibles en un JSP a través de la etiqueta [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Para el etiquetado, la localización depende del contexto, ya que la etiqueta `titles` se puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo agregar un idioma (finés) al cuadro de diálogo **Editar etiqueta**:

1. En **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.

1. Agregue `fi_fi`, que representa la configuración regional finlandesa, y guarde los cambios.

El nuevo idioma (finés) ya está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el cuadro de diálogo **Editar etiqueta** al editar una etiqueta en la consola **Etiquetado**.

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas reconocidos por AEM. Es decir, debe estar disponible como nodo debajo de `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>La instalación del etiquetado relacionado con el contenido listo para usar a través de un paquete de actualización oficial (incluidos los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches y similares), restablece la propiedad de idiomas del nodo `/content/cq:tags` de forma predeterminada. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.
