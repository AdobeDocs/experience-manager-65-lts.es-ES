---
title: 'Introducción a SPA en AEM: React'
description: Este artículo presenta una aplicación de SPA de ejemplo, explica cómo se crea y le permite ponerse en marcha con su propia SPA rápidamente mediante el marco de trabajo React.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 9889b0fe-f39c-42dc-bc7b-8743d68e7503
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 4%

---


# Introducción a SPA en AEM: React{#getting-started-with-spas-in-aem-react}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA en AEM. Este artículo presenta una aplicación de SPA simplificada en el marco de trabajo de React, y explica cómo se crea, lo que le permite ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para ver el documento correspondiente del marco de Angular, consulte [Introducción a las SPA en AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

{{ue-over-spa}}

## Introducción {#introduction}

Este artículo resume el funcionamiento básico de un SPA simple y lo mínimo que necesita saber para poner en marcha el suyo.

Para obtener más información sobre cómo funcionan las SPA en AEM, consulte los siguientes documentos:

* [Introducción y tutorial de SPA](/help/sites-developing/spa-walkthrough.md)
* [Introducción a la creación de SPA](/help/sites-developing/spa-overview.md)
* [Modelo SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para poder crear contenido dentro de una SPA, el contenido debe almacenarse en AEM y ser expuesto por el modelo de contenido.
>
>Una SPA desarrollada fuera de AEM no será legible si no respeta el contrato del modelo de contenido.

Este documento recorrerá la estructura de una SPA simplificada creada con el marco de React e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propia SPA.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia de React esperada, la SPA de ejemplo puede utilizar bibliotecas adicionales para hacer que la creación de la SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete SPA general. Las dependencias AEM mínimas para una SPA en funcionamiento se enumeran aquí.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Dado que este ejemplo se basa en el marco de React, hay dos dependencias específicas de React que son obligatorias en el archivo `package.json`:

```
react
 react-dom
```

`aem-clientlib-generator` se usa para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Encontrará más detalles sobre [aem-clientlib-generator en GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima de `aem-clientlib-generator` requerida es 1.4.1.

`aem-clientlib-generator` está configurado en el archivo `clientlib.config.js` de la siguiente manera.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Generación {#building}

En realidad, al crear la aplicación se usa [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "webpack && clientlib --verbose"`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Arquetipo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de SPA en funcionamiento que puede cargar en la instancia de AEM.

La siguiente sección de este documento le mostrará cómo se estructura un SPA en AEM, los archivos importantes que impulsan la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

El punto de entrada al SPA es el archivo `index.js` que se muestra aquí simplificado para centrarse en el contenido importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La función principal de `index.js` es utilizar la función `ReactDOM.render` para determinar en qué parte del DOM insertar la aplicación.

Este es un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla del componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

### App.js {#app-js}

Al procesar la aplicación, `index.js` llama a `App.js`, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` sirve principalmente para envolver los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, `App.js` llamadas `Page.js` se muestran aquí en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la clase `AppPage` amplía `Page`, que contiene los métodos de contenido interno que se pueden utilizar posteriormente.

`Page` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. Encontrará más información sobre `Page` en el documento [Modelo SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Con la página representada, se pueden procesar los componentes como `Image.js` que se muestran aquí.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

La idea central de las SPA en AEM es la idea de asignar componentes de SPA a componentes de AEM y actualizar el componente cuando se modifica el contenido (y a la inversa). Consulte el documento [Información general del editor de SPA](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente SPA al componente AEM. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

## Exportación de contenido editable {#exporting-editable-content}

Puede exportar un componente y mantenerlo editable.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La función `MapTo` devuelve un `Component` que es el resultado de una composición que extiende el `PageClass` proporcionado con los nombres de clase y atributos que habilitan la creación. Este componente se puede exportar para que se cree una instancia más adelante en el marcado de la aplicación.

Cuando se exporta mediante las funciones `MapTo` o `withModel`, el componente `Page` se ajusta con un componente `ModelProvider` que proporciona acceso a los componentes estándar a la última versión del modelo de página o a una ubicación precisa en ese modelo de página.

Para obtener más información, consulte el [documento de modelo de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente al utilizar la función `withModel`.

## Uso compartido de información entre componentes de SPA {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, mediante React Context.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estados como Redux.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y extendiendo el componente contenedor.

## Siguientes pasos {#next-steps}

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el [Tutorial de introducción al Editor de SPA de AEM - WKND Events](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es).

Para obtener más información acerca de cómo organizarse para desarrollar SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obtener más información sobre la asignación de modelos dinámicos a componentes y cómo funciona en las SPA de AEM, consulte el artículo [Asignación de modelos dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un módulo que no sea React o Angular, o simplemente desea profundizar en cómo funciona SDK de SPA para AEM, consulte el artículo [Modelo SPA](/help/sites-developing/spa-blueprint.md).
