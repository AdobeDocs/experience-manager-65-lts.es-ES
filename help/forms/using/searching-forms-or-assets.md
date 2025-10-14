---
title: Buscar formularios y recursos
description: Puede buscar formularios y recursos en la instancia de AEM mediante la búsqueda de AEM. La búsqueda básica y avanzada permite localizar rápidamente los recursos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 98%

---

# Buscar formularios y recursos{#searching-for-forms-and-assets}

Puede buscar formularios o recursos de formulario, mediante una cadena de texto o una cadena de texto junto con caracteres comodín. También puede limitar la búsqueda mediante los criterios disponibles en varias categorías en el panel Buscar.

Cuando selecciona uno o más criterios y también especifica una cadena de texto, la intersección del texto y los criterios se devuelven como resultados de la búsqueda. Los resultados de la búsqueda son tan buenos como el formulario y los metadatos de recursos proporcionados.

Haga clic en ![aem6forms_search](assets/aem6forms_search.png), para mostrar u ocultar el panel de búsqueda.

## Búsqueda básica {#basic-search}

Una búsqueda básica es la búsqueda predeterminada, que se ejecuta sin especificar ningún filtro. AEM Forms lleva a cabo una búsqueda de texto completo en las propiedades de los metadatos.

Para ejecutar una búsqueda básica, escriba la consulta en el campo de texto y pulse Devolver. También puede introducir el carácter comodín (&#42;) para que coincida con cualquier número de caracteres.

Adobe Experience Manager busca el texto introducido en las propiedades de los metadatos y devuelve los resultados correspondientes. Si escribe más de una palabra, la operación de búsqueda coincidirá con el texto completo para la búsqueda.

Tenga en cuenta los siguientes puntos sobre la búsqueda básica:

* La búsqueda se realiza mediante las propiedades de metadatos de formulario y recursos.
* Si escribe más de una palabra, la operación de búsqueda coincidirá con el texto completo para la búsqueda.
* La búsqueda no distingue entre mayúsculas y minúsculas. Por ejemplo, al escribir `geometrixx`, recursos con títulos `Geometrixx`, `GEOMETRIXX` y `GeoMetRixx` se muestran en los resultados de la búsqueda.

* No se admiten coincidencias parciales de una palabra. Para buscar mediante cadenas parciales, utilice el comodín &#42;. Pero si la consulta de búsqueda coincide con una palabra completa, se mostrará el formulario o recurso correspondiente.
* Los espacios adicionales se respetarán y no se recortarán durante la búsqueda. Por ejemplo, `My form` no es la misma consulta de búsqueda que `My form`.

* Si los datos y los valores de visualización de los campos en las propiedades de metadatos son diferentes, no puede utilizar valores de visualización como parámetros de búsqueda. Por ejemplo, no se puede buscar en función de un estado, como Modificado o Publicado, ya que estas propiedades se almacenan en un formato diferente.

## Búsqueda avanzada {#advanced-search}

En los criterios de búsqueda, además de la consulta, puede especificar algunos parámetros para que la búsqueda básica sea más eficiente y centrada.

![Campo de búsqueda y parámetros o filtros para buscar formularios y recursos de AEM &#x200B;](assets/search_forms_assets.png)

Campo de búsqueda y parámetros o filtros para buscar formularios y recursos de AEM 

### Ruta de recursos {#asset-path}

Mediante el filtro de rutas de recursos, puede limitar los resultados de la búsqueda al directorio actual. Si la opción Buscar en directorio actual no está seleccionada, los resultados de la búsqueda contendrán recursos del directorio base. Si la página actual no es un directorio y la opción “buscar en el directorio actual” está seleccionada, la búsqueda devolverá los recursos presentes en el directorio principal.

### Modificación de recursos {#asset-modification}

Seleccione una de las siguientes opciones para buscar en todos los recursos modificados dentro de un período de tiempo específico.

| **Opción** | **Descripción** |
|---|---|
| Hace dos horas | Busque en todos los recursos modificados en las últimas dos horas. |
| Hace una semana | Busque todos los recursos modificados en la última semana. |
| Hace un mes | Busque en todos los recursos modificados durante el último mes. |
| Hace un año | Busque en todos los recursos modificados durante el último año. |

### Estado de los recursos {#asset-status}

Puede buscar recursos mediante uno de los siguientes estados:

* **Publicado**: buscar todos los recursos publicados y no modificados después de la publicación.

* **Sin publicar**: buscar todos los recursos que no se hayan publicado nunca.

* **Modificado**: buscar todos los recursos que se hayan modificado o cancelado la publicación después de la publicación.

### Tipo de recurso {#asset-type}

Puede seleccionar cualquier tipo de recurso. La búsqueda devuelve la unión de todos los tipos de recursos seleccionados.

<table>
 <tbody>
  <tr>
   <th>Opción</th> 
   <th>Descripción</th> 
  </tr>
  <tr>
   <td>Plantilla de formulario<br /> </td> 
   <td>Buscar en todas las plantillas de formulario.<br /> </td> 
  </tr>
  <tr>
   <td>Formulario PDF</td> 
   <td>Busca en todos los documentos PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Busca en todos los documentos.</td> 
  </tr>
  <tr>
   <td>Formulario adaptable<br /> </td> 
   <td>Busca en todos los formularios adaptables.</td> 
  </tr>
  <tr>
   <td>Recurso</td> 
   <td>Busca en todos los recursos.<br /> </td> 
  </tr>
 </tbody>
</table>

### Etiquetas {#tags}

Las etiquetas son etiquetas adjuntas a los recursos para su identificación. Al buscar, seleccione cualquier número de etiquetas de la lista desplegable o agregue etiquetas personalizadas, si fuera necesario. Un resultado de búsqueda contiene la intersección de las etiquetas seleccionadas.
