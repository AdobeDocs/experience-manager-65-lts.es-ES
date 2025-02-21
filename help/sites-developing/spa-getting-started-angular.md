---
title: 'Introducción a SPA en AEM: Angular'
description: Este artículo presenta una aplicación de SPA de ejemplo, explica cómo se crea y le permite ponerse en marcha con su propia SPA rápidamente mediante el marco de trabajo de Angular.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: cd23626858b9061228718a0455c8dd0812de92b3
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 5%

---

# Introducción a SPA en AEM: Angular{#getting-started-with-spas-in-aem-angular}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA en AEM. Este artículo presenta una aplicación de SPA simplificada en el marco de trabajo de Angular, y explica cómo se crea, lo que le permite ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de trabajo de Angular. Para ver el documento correspondiente del módulo de React, consulte [Introducción a las SPA en AEM - React](/help/sites-developing/spa-getting-started-react.md).

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

Este documento recorrerá la estructura de una SPA simplificada e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propia SPA.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia esperada de Angular, la SPA de ejemplo puede utilizar bibliotecas adicionales para hacer que la creación de la SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete SPA general. Aquí se enumeran las dependencias mínimas de AEM requeridas.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator` se usa para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Más detalles acerca de [aem-clientlib-generator están disponibles en GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La versión mínima de `aem-clientlib-generator` requerida es 1.4.1.

`aem-clientlib-generator` está configurado en el archivo `clientlib.config.js` de la siguiente manera.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de SPA en funcionamiento que puede cargar en la instancia de AEM.

La siguiente sección de este documento le mostrará cómo se estructura un SPA en AEM, los archivos importantes que impulsan la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

El punto de entrada al SPA es el archivo `app.module.ts` que se muestra aquí simplificado para centrarse en el contenido importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

El archivo `app.module.ts` es el punto de partida de la aplicación, contiene la configuración inicial del proyecto y usa `AppComponent` para arrancar la aplicación.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para que estén disponibles posteriormente como propiedades de componente.

### app.component.ts {#app-component-ts}

Una vez que `app.module.ts` arranca `AppComponent`, puede inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Al procesar la página, `app.component.ts` llamadas `main-content.component.ts` se muestran aquí en una versión simplificada.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. Encontrará más información sobre `Page` en el documento [Modelo SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

`Page` está compuesto por componentes. Con el JSON introducido, `Page` puede procesar esos componentes como `image.component.ts`, como se muestra aquí.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

La idea central de las SPA en AEM es la idea de asignar componentes de SPA a componentes de AEM y actualizar el componente cuando se modifica el contenido (y a la inversa). Consulte el documento [Información general del editor de SPA](/help/sites-developing/spa-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente SPA al componente AEM. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede procesar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Uso compartido de información entre componentes de SPA {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estado como NgRx.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y extendiendo el componente contenedor.

## Siguientes pasos {#next-steps}

Para obtener una guía paso a paso sobre cómo crear su propia SPA, consulte el [Tutorial de introducción al Editor de SPA de AEM - WKND Events](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=es).

Para obtener más información acerca de cómo organizarse para desarrollar SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obtener más información sobre la asignación de modelos dinámicos a componentes y cómo funciona en las SPA de AEM, consulte el artículo [Asignación de modelos dinámicos a componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si desea implementar SPA en AEM para un módulo que no sea React o Angular, o simplemente desea profundizar en cómo funciona SDK de SPA para AEM, consulte el artículo [Modelo SPA](/help/sites-developing/spa-blueprint.md).
