---
title: Uso de etiquetas
description: Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web. Las etiquetas pueden considerarse como palabras clave o etiquetas que se pueden adjuntar a una página, un recurso o cualquier otro contenido para que con las búsquedas se encuentre ese contenido y el relacionado.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 39%

---

# Uso de etiquetas{#using-tags}

Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web. Las etiquetas pueden considerarse como palabras clave o etiquetas que se pueden adjuntar a una página, un recurso o cualquier otro contenido para que con las búsquedas se encuentre ese contenido y el relacionado.

* Consulte [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre cómo crear y administrar etiquetas y a qué etiquetas de contenido se han aplicado.
* Consulte [Etiquetado para desarrolladores](/help/sites-developing/tags.md) para obtener información sobre el marco de trabajo de etiquetado, así como la forma de incluir y ampliar las etiquetas en aplicaciones personalizadas.

## Diez motivos para utilizar etiquetas {#ten-reasons-to-use-tagging}

1. Organización del contenido: el etiquetado facilita las cosas a los autores, ya que pueden organizar rápidamente el contenido con poco esfuerzo.
1. Organización de etiquetas : mientras que las etiquetas organizan el contenido, las taxonomías jerárquicas o los espacios de nombres organizan las etiquetas.
1. Etiquetas sumamente organizadas : con la capacidad de crear etiquetas y subetiquetas, es posible expresar sistemas taxonómicos completos y cubrir términos, subtérminos y sus relaciones. Esto permite crear una segunda (o tercera) jerarquía de contenido en paralelo a la oficial.
1. Etiquetado controlado: el etiquetado puede controlarse aplicando permisos a las etiquetas o los espacios de nombres para controlar la creación y la aplicación de etiquetas.
1. Etiquetado flexible: las etiquetas tienen muchos nombres y rostros: etiquetas, términos de taxonomía, categorías, etiquetas y muchos más. Son flexibles en el modelo de contenido y en la manera de usarlas. Por ejemplo, al trazar información demográfica de destino, categorizar y calificar contenido o para crear una jerarquía de contenido secundario.
1. Búsqueda mejorada : el componente de búsqueda predeterminado en AEM incluye, en términos generales, las etiquetas creadas y las etiquetas aplicadas a los filtros que pueden aplicarse para obtener únicamente los resultados relevantes.
1. Habilitación de SEO: las etiquetas aplicadas como propiedades de página se mostrarán automáticamente en las metaetiquetas de la página, por lo que serán visibles a los motores de búsqueda.
1. Sofisticación simple : las etiquetas se pueden crear simplemente a partir de una palabra y pulsar un botón. Después, se pueden añadir un título, una descripción y marcas ilimitadas para proporcionar más semántica a la etiqueta.
1. Consistencia central : el sistema de etiquetado es un componente central de AEM que todas las funcionalidades de AEM utilizan para categorizar contenido. Además, la API de etiquetado está disponible para los desarrolladores para que creen aplicaciones compatibles con el etiquetado con acceso a las mismas taxonomías.
1. Combina estructura y flexibilidad : AEM es ideal para trabajar con información estructurada, ya que anida páginas y rutas de acceso. También es extremadamente útil a la hora de trabajar con información sin estructurar, debido a la búsqueda incorporada de texto completo. El etiquetado combina las ventajas tanto de la estructura como de la flexibilidad.

A la hora de diseñar la estructura de contenido para un sitio y el esquema de metadatos para los recursos, considere la ligereza y la accesibilidad que proporciona el etiquetado.

## Aplicación de etiquetas   {#applying-tags}

En el entorno de creación, los creadores pueden aplicar etiquetas si acceden a las propiedades de página e introducen una o varias etiquetas en el campo **Etiquetas y palabras clave**.

Para aplicar [etiquetas predefinidas](/help/sites-administering/tags.md), en la ventana **Propiedades de página**, use la lista desplegable de campos `Tags/Keywords` para seleccionar de la lista de etiquetas permitidas para la página. La ficha **Etiquetas estándar** es el espacio de nombres predeterminado, lo que significa que no hay `namespace-string:` con el prefijo de la taxonomía.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Publicación de etiquetas {#publishing-tags}

Al igual que con las páginas, puede realizar lo siguiente en etiquetas y áreas de nombres:

**Activar**

* Activar etiquetas individuales.

  Al igual que con las páginas, las etiquetas recién creadas deben activarse antes de que estén disponibles en el entorno de publicación.

>[!NOTE]
>
>Al activar una página, se abre automáticamente un cuadro de diálogo que le permite activar las etiquetas no activadas que pertenecen a la página.

**Desactivar**

* Desactivar las etiquetas seleccionadas.

## Nubes de etiquetas {#tag-clouds}

Las nubes de etiquetas muestran una nube de etiquetas, ya sea para la página actual, todo el sitio web o los sitios a los que se accede con más frecuencia. Las nubes de etiquetas son un medio para resaltar los problemas que son (han sido) de interés para el usuario. El tamaño del texto utilizado para mostrar la etiqueta varía en relación con su uso.

El componente [Nube de etiquetas](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) (grupo de componentes General) se usa para agregar una nube de etiquetas a una página.

## Búsqueda de etiquetas {#searching-on-tags}

Puede buscar etiquetas en los entornos de creación y publicación.

### Uso del componente Buscar {#using-search-component}

Añadir un [componente de búsqueda](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) a una página ofrece la capacidad de búsqueda, que incluye etiquetas y se puede usar en los entornos de creación y publicación.

![chlimage_1-3](assets/chlimage_1-3a.png)
