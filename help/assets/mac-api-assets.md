---
title: API HTTP [!DNL Assets].
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: Assets HTTP API,Developer Tools
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 7bb4aec8-e6c0-416a-a318-d3120f9688c4
source-git-commit: f0385f595035dfd0dce77fc7eb8b2413eaf5431a
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# API del HTTP [!DNL Assets] {#assets-http-api}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=es) |
| AEM 6.5 | Este artículo |

## Información general {#overview}

La API HTTP [!DNL Assets] permite realizar operaciones de creación, lectura, actualización y eliminación (CRUD) en recursos digitales, incluidos metadatos, representaciones y comentarios, así como contenido estructurado mediante [!DNL Experience Manager] fragmentos de contenido. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos de contenido](/help/assets/assets-api-content-fragments.md).

Para acceder a la API:

1. Abra el documento de servicio de API en `https://[hostname]:[port]/api.json`.
1. Seguir el vínculo de servicio [!DNL Assets] que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de la API es un archivo JSON para algunos tipos de MIME y un código de respuesta para todos los tipos de MIME. La respuesta JSON es opcional y es posible que no esté disponible, por ejemplo, para los archivos PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

Transcurrido el [!UICONTROL tiempo de inactividad], un recurso y sus representaciones no estarán disponibles a través de la interfaz web [!DNL Assets] ni a través de la API HTTP. La API devuelve el mensaje de error 404 si el [!UICONTROL Tiempo de activación] es futuro o el [!UICONTROL Tiempo de inactividad] es anterior.

>[!CAUTION]
>
>[La API HTTP actualiza las propiedades de metadatos](#update-asset-metadata) en el espacio de nombres `jcr`. Sin embargo, la interfaz de usuario de Experience Manager actualiza las propiedades de metadatos del espacio de nombres `dc`.

## Fragmentos de contenido {#content-fragments}

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Se puede utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que existen varias diferencias entre los recursos de `standard` (como imágenes o documentos), algunas reglas adicionales se aplican al manejo de fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## Modelo de datos {#data-model}

La API HTTP [!DNL Assets] expone dos elementos, carpetas y recursos principales (para recursos estándar).

Además, expone elementos más detallados para los modelos de datos personalizados que describen el contenido estructurado en Fragmentos de contenido. Consulte [Modelos de datos de fragmento de contenido](/help/assets/assets-api-content-fragments.md#content-fragments) para obtener más información.

### Carpetas {#folders}

Las carpetas son como los directorios de los sistemas de archivos tradicionales. Son contenedores para otras carpetas o aserciones. Las carpetas tienen los siguientes componentes:

**Entidades**: las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name` es el nombre de la carpeta. Es igual que el último segmento de la ruta URL sin la extensión.
* `title` es un título opcional de la carpeta que se puede mostrar en lugar de su nombre.

>[!NOTE]
>
>Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplaza por el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores de `jcr:title` y `jcr:description`, respectivamente.

**Vínculos** Las carpetas muestran tres vínculos:

* `self`: vínculo consigo mismo.
* `parent`: vínculo a la carpeta principal.
* `thumbnail`: (Opcional) vínculo a una imagen en miniatura de carpeta.

### Recursos {#assets}

En Experience Manager, un recurso contiene los siguientes elementos:

* Las propiedades y los metadatos del recurso.
* Varias representaciones, como la representación original (que es el recurso cargado originalmente), una miniatura y varias otras representaciones. Las representaciones adicionales pueden ser imágenes de diferentes tamaños, diferentes codificaciones de vídeo o páginas extraídas de PDF o archivos de [!DNL Adobe InDesign].
* Comentarios opcionales.

Para obtener información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

En [!DNL Experience Manager], una carpeta tiene los siguientes componentes:

* Entidades: las representaciones secundarias de los recursos.
* Propiedades.
* Vínculos.

La API HTTP [!DNL Assets] incluye las siguientes características:

* [Recuperar un listado de carpetas](#retrieve-a-folder-listing).
* [Crear una carpeta](#create-a-folder).
* [Crear un recurso](#create-an-asset).
* [Actualizar binario de recursos](#update-asset-binary).
* [Actualizar metadatos de recursos](#update-asset-metadata).
* [Crear una representación de recursos](#create-an-asset-rendition).
* [Actualizar una representación de recursos](#update-an-asset-rendition).
* [Crear un comentario de recurso](#create-an-asset-comment).
* [Copiar una carpeta o un recurso](#copy-a-folder-or-asset).
* [Mover una carpeta o un recurso](#move-a-folder-or-asset).
* [Eliminar una carpeta, recurso o representación](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar la legibilidad, los siguientes ejemplos omiten la notación cURL completa. De hecho, la notación no se correlaciona con [Resty](https://github.com/micha/resty), que es un contenedor de script para `cURL`.

**Requisitos previos**

* Acceso `https://[aem_server]:[port]/system/console/configMgr`.
* Vaya a **[!UICONTROL Filtro CSRF de Adobe Granite]**.
* Asegúrese de que la propiedad **[!UICONTROL Métodos de filtro]** incluya: `POST`, `PUT`, `DELETE`.

## Recuperar una lista de carpetas {#retrieve-a-folder-listing}

Recupera una representación de sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitud**: `GET /api/assets/myFolder.json`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - OK - success.
* 404 - NO ENCONTRADO: la carpeta no existe o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

**Respuesta**: La clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la dirección URL a la que apunta el vínculo con un `rel` de `self`.

## Crear una carpeta. {#create-a-folder}

Crea un nuevo(a) `sling`: `OrderedFolder` en la ruta dada. Si se proporciona `*` en lugar del nombre de un nodo, el servlet utiliza el nombre del parámetro como nombre de nodo. Los datos de solicitud aceptados son una representación de sirena de la nueva carpeta o un conjunto de pares de nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`, útiles para crear una carpeta directamente desde un formulario de HTML. Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

Una llamada de API produce un error con un código de respuesta `500` si el nodo principal de la ruta de acceso proporcionada no existe. Una llamada devuelve un código de respuesta `409` si la carpeta ya existe.

**Parámetros**: `name` es el nombre de la carpeta.

**Petición**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201 - CREADO: sobre creación correcta.
* 409 - CONFLICTO - si la carpeta ya existe.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear un recurso {#create-an-asset}

Coloque el archivo proporcionado en la ruta proporcionada para crear un recurso en el repositorio de DAM. Si se proporciona `*` en lugar de un nombre de nodo, el servlet utiliza el nombre de parámetro o el nombre de archivo como nombre de nodo.

**Parámetros**: los parámetros son `name` para el nombre del recurso y `file` para la referencia de archivo.

**Petición**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si el recurso se ha creado correctamente.
* 409 - CONFLICTO - si el activo ya existe.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar un binario de recursos {#update-asset-binary}

Actualiza el archivo binario de un recurso (representación con el nombre original). Una actualización déclencheur el flujo de trabajo de procesamiento de recursos predeterminado que se ejecutará, si está configurado.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar metadatos del recurso {#update-asset-metadata}

Actualiza las propiedades de los metadatos del recurso. Si actualiza cualquier propiedad en el espacio de nombres `dc:`, la API actualiza la misma propiedad en el espacio de nombres `jcr`. La API no sincroniza las propiedades en las dos áreas de nombres.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

### Sincronizar actualización de metadatos entre el espacio de nombres `dc` y `jcr` {#sync-metadata-between-namespaces}

El método API actualiza las propiedades de metadatos en el espacio de nombres `jcr`. Las actualizaciones realizadas mediante la interfaz de usuario cambian las propiedades de metadatos del espacio de nombres `dc`. Para sincronizar los valores de metadatos entre el espacio de nombres `dc` y `jcr`, puede crear un flujo de trabajo y configurar Experience Manager para que ejecute el flujo de trabajo tras la edición del recurso. Utilice un script ECMA para sincronizar las propiedades de metadatos requeridas. El siguiente script de ejemplo sincroniza la cadena de título entre `dc:title` y `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## Crear una representación de recursos {#create-an-asset-rendition}

Crear una representación de recursos para un recurso. Si no se proporciona el nombre del parámetro de solicitud, se utilizará el nombre de archivo como nombre de representación.

**Parámetros**: los parámetros son `name` para el nombre de la representación y `file` como referencia de archivo.

**Petición**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la representación se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitud**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si la representación se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Agregar un comentario en un recurso {#create-an-asset-comment}

Crea un nuevo comentario de recurso.

**Parámetros**: los parámetros son `message` para el cuerpo del mensaje del comentario y `annotationData` para los datos de anotación en formato JSON.

**Solicitud**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si el comentario se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso disponible en la ruta proporcionada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination`: un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - `infinity` o `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Use `F` para evitar que se sobrescriba un recurso en el destino existente.

**Solicitud**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso en la ruta determinada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination`: un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - `infinity` o `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Use `T` para forzar la eliminación de un recurso existente o `F` para evitar sobrescribir un recurso existente.

**Solicitud**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

No use `/content/dam` en la dirección URL. Un comando de ejemplo para mover recursos y sobrescribir los existentes es el siguiente:

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Eliminar una carpeta, un recurso o una representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta proporcionada.

**Petición**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Aceptar - si la carpeta se ha eliminado correctamente.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* [La API HTTP actualiza las propiedades de metadatos](#update-asset-metadata) en el espacio de nombres `jcr`. Sin embargo, la interfaz de usuario de Experience Manager actualiza las propiedades de metadatos del espacio de nombres `dc`.

* La API HTTP de Assets no devuelve los metadatos completos. Las áreas de nombres están codificadas y solo se devuelven esas áreas de nombres. Para ver los metadatos completos, consulte la ruta de recursos `/jcr_content/metadata.json`.
