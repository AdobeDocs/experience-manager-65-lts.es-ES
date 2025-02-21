---
title: Componentes compuestos en SPA
description: Aprenda a crear sus propios componentes compuestos, componentes formados por otros componentes, que funcionan con el Editor de aplicaciones de una sola página (SPA) de AEM.
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: cd23626858b9061228718a0455c8dd0812de92b3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Componentes compuestos en SPA {#composite-components-in-spas}

Los componentes compuestos utilizan la naturaleza modular de los componentes de AEM al combinar varios componentes básicos en uno solo. Un caso de uso de componente compuesto común es el componente de tarjeta, formado por una combinación de los componentes de imagen y texto.

Cuando los componentes compuestos se implementan correctamente dentro del marco de trabajo Editor de aplicaciones de una sola página (SPA) de AEM, los autores de contenido pueden arrastrar y soltar estos componentes como lo harían con cualquier otro componente, pero siguen teniendo la capacidad de editar individualmente cada componente que compone el componente compuesto.

Este artículo muestra cómo puede agregar un componente compuesto a la aplicación de una sola página para trabajar sin problemas con AEM SPA Editor.

{{ue-over-spa}}

## Caso práctico {#use-case}

Este artículo utiliza el componente de tarjeta típico como ejemplo de uso. Las tarjetas son un elemento de la interfaz de usuario común para muchas experiencias digitales y suelen estar formadas por una imagen y un texto o rótulo asociado. Un autor desea poder arrastrar y soltar toda la tarjeta, pero puede editar individualmente la imagen de la tarjeta y personalizar el texto asociado.

## Requisitos previos {#prerequisites}

Los siguientes modelos para admitir los casos de uso de componentes compuestos requieren los siguientes requisitos previos.

* La instancia de desarrollo de AEM se ejecuta localmente en el puerto 4502 con un proyecto de ejemplo.
* Tiene una aplicación React externa en funcionamiento [habilitada para la edición en AEM.](spa-edit-external.md)
* La aplicación React se cargó en el editor de AEM [mediante el componente RemotePage.](spa-remote-page.md)

## Adición de componentes compuestos a una SPA {#adding-composite-components}

Existen tres modelos diferentes para implementar el componente compuesto en función de la implementación de SPA dentro de AEM.

* [El componente no existe en el proyecto de AEM.](#component-does-not-exist)
* [El componente existe en el proyecto de AEM, pero el contenido requerido no.](#content-does-not-exist)
* [El componente y su contenido requerido existen en el proyecto de AEM.](#both-exist)

En las siguientes secciones se proporcionan ejemplos de implementación de cada caso utilizando el componente de tarjeta como ejemplo.

### El componente no existe en el proyecto de AEM. {#component-does-not-exist}

Comience creando los componentes que compondrán el componente compuesto, es decir, los componentes para la imagen y su texto.

1. Cree el componente Texto en el proyecto de AEM.
1. Agregue el(la) `resourceType` correspondiente del proyecto en el nodo `editConfig` del componente.

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. Use el asistente de `withMappable` para habilitar la edición del componente.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

El componente de texto será similar al siguiente.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

Si crea un componente de imagen de forma similar, puede combinarlo con el componente `AEMText` en un nuevo componente de tarjeta, utilizando los componentes de imagen y texto como elementos secundarios.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

Este componente compuesto resultante ahora se puede colocar en cualquier lugar de la aplicación y el agregará marcadores de posición para un componente de texto y de imagen en el Editor de SPA. En el siguiente ejemplo, el componente de tarjeta se agrega al componente principal debajo del título.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

Esto mostrará un marcador de posición vacío para un texto y una imagen en el editor. Al introducir valores para estos elementos mediante el editor, se almacenan en la ruta de página especificada, es decir, `/content/wknd-spa/home` en el nivel raíz con los nombres especificados en `itemPath`.

![Componente de tarjeta compuesta en el editor](assets/composite-card.png)

### El componente existe en el proyecto de AEM, pero el contenido requerido no. {#content-does-not-exist}

En este caso, el componente de tarjeta ya se ha creado en el proyecto de AEM que contiene los nodos de título e imagen. Los nodos secundarios (texto e imagen) tienen los tipos de recursos correspondientes.

![Estructura de nodos del componente de tarjeta](assets/composite-node-structure.png)

A continuación, puede añadirlo a su SPA y recuperar su contenido.

1. Cree un componente correspondiente en la SPA para esto. Asegúrese de que los componentes secundarios estén asignados a sus tipos de recursos de AEM correspondientes dentro del proyecto de SPA. En este ejemplo utilizamos los mismos componentes `AEMText` y `AEMImage` que se detallaron [en el caso anterior.](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. Dado que no hay contenido para el componente `imagecard`, agregue la tarjeta a la página. Incluya el contenedor existente de AEM en la SPA.
   * Si ya hay un contenedor en el proyecto de AEM, podemos incluirlo en la SPA en su lugar y agregar el componente al contenedor desde AEM.
   * Asegúrese de que el componente de tarjeta esté asignado al tipo de recurso correspondiente en la SPA.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. Agregue el componente `wknd-spa/components/imagecard` creado a los componentes permitidos para el componente contenedor [ en la plantilla de página.](/help/sites-authoring/templates.md)

Ahora el componente `imagecard` se puede agregar directamente al contenedor en el editor de AEM.

![Tarjeta compuesta en el editor](assets/composite-card.gif)

### El componente y su contenido requerido existen en el proyecto de AEM. {#both-exist}

Si el contenido existe en AEM, se puede incluir directamente en la SPA proporcionando la ruta al contenido.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![Ruta compuesta en la estructura del nodo](assets/composite-path.png)

El componente `AEMCard` es el mismo que se definió [ en el caso de uso anterior.](#content-does-not-exist) Aquí el contenido definido en la ubicación anterior del proyecto de AEM se incluye en la SPA.
