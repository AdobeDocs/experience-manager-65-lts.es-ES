---
title: Editor de imágenes
description: El editor de imágenes es una parte esencial de AEM y los componentes lo pueden utilizar para facilitar la manipulación de imágenes por parte de los autores de contenido.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 9%

---

# Editor de imágenes{#image-editor}

El editor de imágenes es una parte esencial de AEM y los componentes lo pueden utilizar para facilitar la manipulación de imágenes por parte de los autores de contenido.

>[!CAUTION]
>
>Para usar las características del Editor de imágenes descritas en este artículo, [se debe instalar el paquete de características 24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267).

## Unidades relativas para mapa de imagen {#relative-units-for-image-map}

El Editor de imágenes mantiene las áreas de mapa de imagen como unidades absolutas y relativas. Las unidades relativas son útiles cuando se proporcionan como atributos de datos para cambiar dinámicamente el tamaño de un mapa de imagen (en relación con el tamaño de la imagen) en el lado del cliente en un componente de imagen interactivo.

### Propiedad imageMap {#imagemap-property}

El Editor de imágenes mantiene las coordenadas del mapa de imagen en el JCR como propiedad `imageMap`. Tiene el siguiente formato.

La propiedad almacena las áreas de mapas de la siguiente manera:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Ejemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Compatibilidad con imágenes de SVG {#support-for-svg-images}

Los gráficos vectoriales escalables (SVG) son compatibles con el editor de imágenes.

* Se admiten las funciones de arrastrar y soltar un recurso SVG desde DAM y de cargar un archivo SVG cargado desde un sistema de archivos local.

## Habilitación de complementos por tipo MIME {#enabling-plugins-by-mime-type}

En determinadas situaciones, las acciones de creación deben restringirse para determinados tipos MIME, debido a la falta de compatibilidad en el procesamiento del lado del servidor. Por ejemplo, es posible que no se permita editar imágenes de SVG.

Los complementos del Editor de imágenes se pueden habilitar selectivamente por tipo MIME al establecer una propiedad `supportedMimeTypes` en el nodo de configuración del complemento individual.

### Ejemplos {#example}

Por ejemplo, supongamos que la capacidad de recorte solo debe permitirse para imágenes de GIF, JPEG, PNG, WEBP y TIFF.

La propiedad `supportedMimeTypes` debe establecerse como una cadena de los tipos MIME permitidos en el nodo de configuración del complemento en el nodo `cq:editConfig` del componente de imagen.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
