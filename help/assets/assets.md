---
title: Introducción a  [!DNL Adobe Experience Manager Assets]
description: Cree, administre, procese y distribuya recursos digitales en Experience Manager. Estas guías describen las prácticas recomendadas, las funciones de accesibilidad y cómo utilizar recursos de AEM 6.5 LTS.
hide: true
feature: Asset Management
role: Leader,Developer,User
solution: Experience Manager, Experience Manager Assets
exl-id: 2f2eb576-4924-4314-b348-c4b290a57fe3
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 5%

---

# Acerca de [!DNL Adobe Experience Manager Assets] como solución DAM {#administering-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/overview) |
| AEM 6.5 LTS | Este artículo |

AEM [!DNL Assets] es una herramienta de administración de activos digitales (DAM) que forma parte de la plataforma [!DNL Experience Manager] y permite a su empresa administrar y distribuir recursos digitales. Los usuarios de una organización pueden administrar, almacenar y acceder a muchos tipos de recursos digitales, como imágenes, vídeos, documentos, clips de audio, archivos 3D y medios enriquecidos, para usarlos en la web, en la impresión y para la distribución digital.

## ¿Qué es la administración de activos digitales? {#what-is-digital-asset-management}

[!DNL Assets] proporciona uso compartido y distribución en toda la empresa de los recursos digitales clave de una organización. Los usuarios de una organización pueden almacenar, administrar y acceder a recursos digitales, como imágenes, gráficos, audio, vídeo y documentos, a través de una interfaz web (o una carpeta CIFS o WebDAV).

La capacidad [!DNL Assets] de [!DNL Experience Manager] le permite hacer lo siguiente:

* Agregue y comparta imágenes, documentos, archivos de audio y archivos de vídeo en varios formatos de archivo.
* Administre los recursos agrupándolos por etiquetas, lightbox o estrellas (sus favoritos). Agregar anotaciones a recursos.
* Busque recursos buscando nombres de archivo, el texto completo de los documentos y buscando fechas, tipo de documento y etiquetas.
* Añada o edite la información de metadatos de los recursos. Las versiones de los metadatos se realizan automáticamente junto con el recurso correspondiente. Puede importar o exportar metadatos de recursos.
* Realizar funciones de edición de imágenes, como escalar y añadir filtros de imagen. Importe y exporte varios recursos digitales simultáneamente mediante una carpeta WebDAV o CIFS.
* Utilice flujos de trabajo y notificaciones para permitir el procesamiento y la descarga conjuntos de cualquier conjunto de recursos y administrar los derechos de acceso a los recursos.

### [!DNL Experience Manager Assets] está integrado con [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] se integra completamente con [!DNL Sites] y funciona sin problemas en todos los casos de uso. Por ejemplo, al crear páginas web, los autores de [!DNL Sites] pueden encontrar y utilizar los recursos digitales mediante el buscador de contenido. La interfaz de usuario de [!DNL Assets] es la misma que la de [!DNL Sites]. Vea [información general de Sites](/help/sites-authoring/page-authoring.md) para obtener detalles completos.

La interfaz de usuario básica es la misma que la de [!DNL Sites]. Consulte [Información general de los sitios](/help/sites-authoring/page-authoring.md) para obtener información detallada.

### Digital Asset Management versus image component {#digital-asset-management-versus-image-component}

When determining whether to put an image into the DAM repository or use an image component, consider the image lifecycle:

* If the image has the same lifecycle as the page, use the Image component.
* If the image has a separate life cycle, for example, if you use the image twice or outside WCM, use [!DNL Assets].

## What are digital assets? {#what-are-digital-assets}

An asset is a digital document, image, video, or audio (or part thereof) that can have multiple renditions. It can also have sub-assets, for example, layers in a Photoshop file, slides in a PowerPoint file, pages in a pdf, files in a ZIP.

An asset is essentially a binary plus metadata plus renditions plus sub-assets. See the [DAM Performance Guide](/help/sites-deploying/assets-performance-sizing.md) for detailed information.

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] deployment.

### [!DNL Experience Manager Assets] terminology {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], it helps if you understand the following terminology:

* **Collection**: A collection of assets, either based on physical location (folder), common properties (saved search folder), or user selection (lightbox folders).

* **Metadata** [!DNL Assets] have metadata; for example, author, expiry date, and DRM Information (Digital Rights Management). Metadata is under access control. [!DNL Assets] supports the following various common metadata schemata out of the box:

   * Dublin Core: including author, description, date, subject, and so on.
   * IPTC: including event, model, location, and so on.
   * WCM: including page properties, [!UICONTROL On Time] and [!UICONTROL Off Time], and so on.

* **Tagging**: [!DNL Assets] can be tagged and classified. See [organizing assets](/help/assets/organize-assets.md).

* **Renditions**: A rendition is the binary representation of an asset. [!DNL Assets] always have a primary representation - that of the uploaded file. They can have any number of additional representations that are created, for example, by customized workflow steps or when an asset is uploaded. Renditions may be of a different size, with a different resolution, with an added watermark, or some other changed characteristic.

* **Versiones**: el control de versiones crea una instantánea de los recursos digitales en un momento específico. Puede restaurar los recursos a versiones anteriores. Ver [versiones en [!DNL Assets]](manage-assets.md#asset-versioning).

* **Subrecursos**: Los subrecursos son recursos que constituyen un recurso, por ejemplo, capas de un archivo de [!DNL Adobe Photoshop] o páginas de un archivo de PDF. En [!DNL Assets], puede administrar subrecursos como lo haría con los recursos.

### Cómo trabajar con recursos digitales {#how-to-work-with-assets}

Realiza una acción en un recurso o una colección. Las acciones pueden crear o modificar recursos, colecciones y representaciones. Muchas de las acciones básicas que realiza en los recursos (cargar, eliminar, actualizar, guardar subrecursos) almacenan en déclencheur los flujos de trabajo preconfigurados. Se activan automáticamente en [!DNL Assets] y se describen en detalle en los controladores de medios [!DNL Assets].

Las tareas que puede realizar con estos flujos de trabajo preconfigurados:

* Guarde el recurso en el repositorio o elimínelo de él.
* Extraiga y guarde metadatos del recurso; los elementos de metadatos individuales se guardan como XMP.
* Generar representaciones y miniaturas del recurso, incluido el cambio de tamaño y el recorte automáticos cuando sea necesario.
* Transcodifique el recurso donde sea necesario. Por ejemplo, el vídeo para uso móvil y web se transcodifica con 24 fotogramas por segundo y el vídeo de descarga con 30 fotogramas por segundo. El audio para uso móvil y web se transcodifica con 128 Kbps, el audio para descarga con 192 Kbps.

También puede aplicar flujos de trabajo manualmente. Consulte [Controladores de Assets Media](media-handlers.md)para obtener una lista de flujos de trabajo predeterminados.

## [!DNL Experience Manager Assets] y [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consulte [Assets y Biblioteca multimedia](medialibrary.md) para obtener información sobre las diferencias.

>[!MORELIKETHIS]
>
>* [Introducción en vídeo: Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Comprender los conceptos de metadatos](/help/assets/metadata-concepts.md)
