---
title: Actualización del contenido mediante las API de AEM Assets
description: En esta parte del recorrido para desarrolladores de contenido de AEM sin encabezado, descubra cómo utilizar la API de REST para acceder y actualizar el contenido de sus fragmentos de contenido.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 87%

---

# Actualización del contenido mediante las API de AEM Assets {#update-your-content}

En esta parte del [Recorrido para desarrolladores de contenido de AEM sin encabezado](overview.md), descubra cómo utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md), aprendió a acceder al contenido sin encabezado en AEM mediante la API de GraphQL de AEM, por lo que ahora debería poder hacer lo siguiente:

* Tener conocimientos avanzados de GraphQL.
* Comprender cómo funciona la API de GraphQL de AEM.
* Comprender algunos ejemplos prácticos de consultas.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo actualizar el contenido sin encabezado existente en AEM a través de la API de REST.

## Objetivo {#objective}

* **Audiencia**: avanzadas
* **Objetivo**: aprender a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido.
   * Presentar la API HTTP de AEM Assets.
   * Presentar y comentar la compatibilidad de los fragmentos de contenido en la API.
   * Indicar detalles de la API.

<!--
  * Look at sample code to see how things work in practice.
-->

## ¿Por qué se necesita la API HTTP de Recursos para los fragmentos de contenido? {#why-http-api}

En la fase anterior del recorrido sin encabezado, se ha aprendido a utilizar la API de GraphQL de AEM para recuperar el contenido mediante consultas.

Entonces, ¿por qué se necesita otra API?

La API HTTP de Assets no le permite **leer** su contenido, pero también le permite **crear**, **actualizar** y **eliminar** contenido: acciones que no son posibles con la API de GraphQL.

La API de REST de Assets está disponible en cada instalación predeterminada de una versión reciente de Adobe Experience Manager.

## API HTTP de Recursos {#assets-http-api}

La API HTTP de Recursos incluye lo siguiente:

* La API de REST de Recursos
* incluye compatibilidad con los fragmentos de contenido

La implementación actual de la API HTTP de Recursos se basa en el estilo arquitectónico de **REST** y le permite acceder al contenido (almacenado en AEM) mediante operaciones **CRUD** (crear, leer, actualizar y eliminar).

Con estas operaciones, la API le permite utilizar Adobe Experience Manager como CMS sin encabezado (sistema de administración de contenido) proporcionando servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON. Por ejemplo, las aplicaciones de una sola página (SPA) basadas en marcos de trabajo o personalizados, requieren contenido proporcionado a través de una API, a menudo en formato JSON.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## API HTTP de Recursos y fragmentos de contenido {#assets-http-api-content-fragments}

Los fragmentos de contenido se utilizan para entregas sin encabezado y un fragmento de contenido es un tipo de recurso especial. Se utilizan para acceder a datos estructurados, como textos, números, fechas, entre otros.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Uso de la API REST de Recursos {#using-aem-assets-rest-api}

### Acceso {#access}

La API REST de Recursos utiliza el punto final `/api/assets` y necesita la ruta del recurso para acceder a él (sin el `/content/dam` inicial).

* Esto significa que para acceder al recurso en:
   * `/content/dam/path/to/asset`
* Debe solicitar:
   * `/api/assets/path/to/asset`

Por ejemplo, para acceder a `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acceso:
>
>* `/api/assets` **no** necesita el uso del selector `.model`.
>* `/content/path/to/page` **sí** necesita el uso del selector `.model`.

### Operación {#operation}

El método HTTP determina la operación que se va a ejecutar:

* **GET**: recuperar una representación JSON de un recurso o una carpeta.
* **POST**: crear nuevos recursos o carpetas.
* **PUT**: actualizar las propiedades de un recurso o carpeta.
* **DELETE**: eliminar un recurso o carpeta.

>[!NOTE]
>
>El cuerpo de solicitud o los parámetros de URL se pueden usar para configurar algunas de estas operaciones; por ejemplo, definir que una carpeta o un recurso deben crearse mediante una solicitud **POST**.

El formato exacto de las solicitudes compatibles se define en la documentación de referencia de la API.

El uso puede variar en función de si utiliza un entorno de publicación o autor de AEM, junto con el caso de uso específico.

* Se recomienda encarecidamente que la creación esté vinculada a una instancia de autor (actualmente, no hay forma de replicar un fragmento para publicarlo con esta API).
* La entrega es posible desde ambos, ya que AEM sirve contenido solicitado solo en formato JSON.

   * El almacenamiento y el envío desde una instancia de autor de AEM deben ser suficientes para las aplicaciones de la biblioteca de medios, detrás del cortafuegos.

   * Para la entrega web activa, se recomienda una instancia de publicación de AEM.

>[!CAUTION]
>
>La configuración de Dispatcher en las instancias de AEM podría bloquear el acceso a `/api`.

>[!NOTE]
>
>Para obtener más información, consulte la Referencia de API. En particular, la [API de Adobe Experience Manager Assets: fragmentos de contenido](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### Lectura/entrega {#read-delivery}

El uso se realiza mediante:

`GET /{cfParentPath}/{cfName}.json`

Por ejemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

La respuesta es un archivo JSON serializado con el contenido estructurado como en el fragmento de contenido. Las referencias se envían como direcciones URL de referencia.

Se pueden realizar dos tipos de operaciones de lectura:

* Al leer un fragmento de contenido específico por la ruta, se devuelve la representación JSON del fragmento de contenido.
* Lectura de una carpeta de fragmentos de contenido por la ruta: se devuelven las representaciones JSON de todos los fragmentos de contenido de la carpeta.

### Crear {#create}

El uso se realiza mediante:

`POST /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON del fragmento de contenido que se va a crear, incluido cualquier contenido inicial que se deba establecer en los elementos del fragmento de contenido. Es obligatorio establecer la propiedad `cq:model` y debe señalar a un modelo de fragmento de contenido válido. Si no lo hace, se producirá un error. También es necesario añadir el encabezado `Content-Type` que se establece en `application/json`.

### Actualizar {#update}

El uso se realiza mediante

`PUT /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON de lo que se debe actualizar para el fragmento de contenido determinado.

Puede ser simplemente el título o la descripción de un fragmento de contenido, o un solo elemento, o todos los valores de elementos o metadatos.

### Eliminar {#delete}

El uso se realiza mediante:

`DELETE /{cfParentPath}/{cfName}`

Para obtener más información sobre el uso de la API REST de AEM Assets, puede hacer referencia a lo siguiente:

* API HTTP de Adobe Experience Manager Assets (recursos adicionales)
* Compatibilidad con los fragmentos de contenido en la API HTTP de AEM Assets (recursos adicionales)

## Siguientes pasos {#whats-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Comprender los conceptos básicos de la API HTTP de AEM Assets.
* Comprender cómo se admiten los fragmentos de contenido en esta API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page is not going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Debe continuar con su recorrido sin encabezado de AEM revisando el documento [Cómo publicar su aplicación sin encabezado](go-live.md), donde realmente pone en marcha su proyecto sin encabezado de AEM.

## Recursos adicionales {#additional-resources}

* [API HTTP de Recursos](/help/assets/mac-api-assets.md)
* [API de REST de fragmentos de contenido](/help/assets/assets-api-content-fragments.md)
   * [Referencia de la API](/help/assets/assets-api-content-fragments.md#api-reference)
* [API de Adobe Experience Manager Assets: fragmentos de contenido](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
* [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [Explicación de CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=es)
* [Vídeo: Desarrollo para CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=es)
* Una [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)
* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
