---
title: Uso de etiquetas
description: Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 76%

---


# Uso de etiquetas {#using-tags}

Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web. Las etiquetas pueden considerarse como palabras clave o etiquetas que se pueden adjuntar a una página, un recurso o cualquier otro contenido para que con las búsquedas se encuentre ese contenido y el relacionado.

* Consulte [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre cómo crear y administrar etiquetas y a qué etiquetas de contenido se han aplicado.
* Consulte [Etiquetado para desarrolladores](/help/sites-developing/tags.md) para obtener información sobre el marco de trabajo de etiquetado, así como la forma de incluir y ampliar las etiquetas en aplicaciones personalizadas.

## Diez motivos para utilizar etiquetas {#ten-reasons-to-use-tagging}

1. **Organización del contenido**: el etiquetado facilita las cosas a los creadores, ya que pueden organizar rápidamente el contenido con muy poco esfuerzo.
1. **Organización de etiquetas**: si bien las etiquetas organizan el contenido, las taxonomías jerárquicas o los espacios de nombres organizan las etiquetas.
1. **Etiquetas sumamente organizadas**: con la capacidad de crear etiquetas y subetiquetas, es posible expresar sistemas taxonómicos completos y cubrir términos, subtérminos y sus relaciones. Esto permite crear una segunda (o tercera) jerarquía de contenido en paralelo a la oficial.
1. **Etiquetado controlado**: el etiquetado puede controlarse aplicando permisos a las etiquetas o los espacios de nombres para controlar la creación y la aplicación de etiquetas.
1. **Etiquetado flexible**: las etiquetas tienen muchos nombres y rostros: etiquetas, términos de taxonomía, categorías, marcas y muchos más. Son flexibles en el modelo de contenido y en la manera de usarlas. Por ejemplo, al trazar información demográfica de destino, categorizar y calificar contenido o para crear una jerarquía de contenido secundario.
1. **Búsqueda mejorada**: el componente de búsqueda predeterminado en AEM incluye, en términos generales, las etiquetas creadas y las etiquetas aplicadas a los filtros que pueden emplearse para obtener únicamente los resultados relevantes.
1. **Habilitación de SEO**: las etiquetas aplicadas como propiedades de página se mostrarán automáticamente en las metaetiquetas de la página, por lo que serán visibles a los motores de búsqueda.
1. **Sofisticación simple**: las etiquetas se pueden crear simplemente a partir de una palabra y pulsar un botón. Después, se pueden añadir un título, una descripción y marcas ilimitadas para proporcionar más semántica a la etiqueta.
1. **Consistencia central**: el sistema de etiquetado es un componente central de AEM que todas las capacidades de AEM utilizan para categorizar contenido. Además, la API de etiquetado está disponible para los desarrolladores para que creen aplicaciones compatibles con el etiquetado con acceso a las mismas taxonomías.
1. **Combina estructura y flexibilidad**: AEM es ideal para trabajar con información estructurada, ya que anida páginas y rutas de acceso. También es extremadamente útil a la hora de trabajar con información sin estructurar, debido a la búsqueda incorporada de texto completo. El etiquetado combina las ventajas tanto de la estructura como de la flexibilidad.

A la hora de diseñar la estructura de contenido para un sitio y el esquema de metadatos para los recursos, considere la ligereza y la accesibilidad que proporciona el etiquetado.

## Aplicación de etiquetas   {#applying-tags}

En el entorno de creación, los creadores pueden aplicar etiquetas si acceden a las propiedades de página e introducen una o varias etiquetas en el campo **Etiquetas y palabras clave**.

Para aplicar [etiquetas predefinidas](/help/sites-administering/tags.md), en la ventana **Propiedades de página**, use el campo **Etiquetas** y la ventana **Seleccionar etiquetas**. La ficha **Etiquetas estándar** es el espacio de nombres predeterminado, lo que significa que no hay `namespace-string:` con el prefijo de la taxonomía.

![Ventana Seleccionar etiquetas; utilice el botón X para anular la selección de las etiquetas seleccionadas actualmente](assets/chlimage_1-41.png)

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
