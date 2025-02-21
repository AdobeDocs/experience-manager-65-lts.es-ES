---
title: Implementación de un componente de React para SPA
description: Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor de SPA de Adobe Experience Manager (AEM).
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: cd23626858b9061228718a0455c8dd0812de92b3
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 9%

---

# Implementación de un componente de React para SPA{#implementing-a-react-component-for-spa}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de Adobe Experience Manager (AEM) sin problemas para un sitio creado con marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA en AEM. Este artículo presenta un ejemplo de cómo adaptar un componente React simple y existente para trabajar con el Editor de SPA de AEM.

{{ue-over-spa}}

## Introducción {#introduction}

Gracias al contrato sencillo y ligero que requiere AEM y que se establece entre la SPA y el Editor de SPA, tomar una aplicación de JavaScript existente y adaptarla para usarla con una SPA en AEM es una cuestión sencilla.

Este artículo ilustra el ejemplo del componente meteorológico en la SPA de muestra de We.Retail Journal.

Debe estar familiarizado con la [estructura de una aplicación SPA para AEM](/help/sites-developing/spa-getting-started-react.md) antes de leer este artículo.

>[!CAUTION]
>Este documento usa la [aplicación We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) únicamente con fines de demostración. No lo utilice para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## El componente Meteorológico {#the-weather-component}

El componente meteorológico se encuentra en la parte superior izquierda de la aplicación We.Retail Journal. Muestra el tiempo actual de una ubicación definida, extrayendo datos meteorológicos de forma dinámica.

### Uso del widget del tiempo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Al crear contenido de la SPA en el Editor de SPA, el componente meteorológico aparece como cualquier otro componente de AEM, con una barra de herramientas y se puede editar.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ciudad se puede actualizar en un cuadro de diálogo como cualquier otro componente de AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

El cambio se mantiene y el componente se actualiza automáticamente con nuevos datos meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementación del componente meteorológico {#weather-component-implementation}

El componente meteorológico se basa en un componente React disponible públicamente, llamado [React Open Weather](https://www.npmjs.com/package/react-open-weather). Se ha adaptado para funcionar como un componente dentro de la aplicación de SPA de muestra de We.Retail Journal.

Los siguientes son fragmentos de la documentación de NPM del uso del componente React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Revisando el código del componente meteorológico personalizado (`Weather.js`) en la aplicación We.Retail Journal:

* **Línea 16**: El widget React Open Weather se carga según sea necesario.
* **Línea 46**: La función `MapTo` relaciona este componente de React con un componente de AEM correspondiente para que se pueda editar en el Editor SPA.

* **Líneas 22-29**: se define `EditConfig`, comprobando si la ciudad se ha rellenado y definiendo el valor si está vacío.

* **Líneas 31-44**: El componente Meteorológico amplía la clase `Component` y proporciona los datos necesarios definidos en la documentación de uso de NPM para el componente React Open Weather y procesa el componente.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Aunque ya debe existir un componente back-end, el desarrollador front-end puede utilizar el componente React Open Weather en la SPA de We.Retail Journal con poca codificación.

## Siguiente paso {#next-step}

Para obtener más información sobre el desarrollo de SPA para AEM, consulte el artículo [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md).
