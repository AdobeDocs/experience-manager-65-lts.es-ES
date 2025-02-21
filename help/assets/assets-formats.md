---
title: Formatos de archivo y tipos MIME admitidos
description: Formatos de archivo y tipos MIME admitidos por  [!DNL Assets] y [!DNL Dynamic Media] y las características admitidas para cada formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 26%

---

# Formatos admitidos en [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] admite una amplia gama de formatos de archivo y cada funcionalidad tiene compatibilidad variada con diferentes tipos MIME. Para integrar [!DNL Assets] con otras soluciones de administración de recursos digitales (DAM) y software de escritorio compatibles con los estándares, use [!DNL Extensible Metadata Platform] (XMP) de Adobe.

Utilice la leyenda para comprender el nivel de compatibilidad.

| Nivel de soporte | Descripción |
| :-----------: | ------------------------------ |
| ✓ | Compatibilidad |
| &#42; | Compatible con funciones de complemento |
| − | No aplicable |

## Formatos de imagen rasterizada admitidos en [!DNL Experience Manager] {#supported-raster-image-formats}

Los formatos de imagen rasterizada admitidos en [!DNL Assets] son:

| Formato | Almacenamiento | Administración de metadatos | Extracción de metadatos | Generación de miniaturas | Edición | Reescritura de metadatos | Perspectivas |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡ La imagen combinada se extrae del archivo PSD. Es una imagen generada por Adobe Photoshop y que se incluye en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

Además de la información anterior, tenga en cuenta lo siguiente:

* La compatibilidad con archivos EPS se aplica solo a imágenes rasterizadas. Por ejemplo, la generación de miniaturas para imágenes vectoriales de EPS no es compatible de forma predeterminada. Para agregar compatibilidad, [configure ImageMagick](best-practices-for-imagemagick.md). Para integrar herramientas de terceros y habilitar capacidades adicionales, consulte [Controlador de medios basado en la línea de comandos](media-handlers.md#command-line-based-media-handler).

* La reescritura de metadatos funciona para el formato de archivo PSB cuando se agrega al controlador `NComm`.

* Para archivos EPS, la reescritura de metadatos es compatible con la versión 3.0 o posterior de la Convención de estructuración de documentos de PostScript (PS-Adobe).

## Formatos 3D compatibles {#support-3d-formats}

Se admite la siguiente lista de formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Vista previa de miniaturas | Previsualización 3D | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## Biblioteca de rasterizadores de PDF compatible {#supported-pdf-rasterizer-library}

La biblioteca Rasterizer de Adobe PDF genera miniaturas y vistas previas de alta calidad para archivos de PDF y [!DNL Adobe Illustrator] grandes y que requieren gran cantidad de contenido. Adobe recomienda utilizar la biblioteca PDF Rasterizer para lo siguiente:

* Archivos de PDF/IA que requieren gran cantidad de contenido y que requieren muchos recursos para procesarse.
* Archivos de IA/PDF, para los que las miniaturas no se generan de forma predeterminada.
* Archivos AI con colores del Sistema de coincidencia de Pantone (PMS).

Consulte [Uso de PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificación de imágenes compatible {#supported-image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de administración de imágenes, como codificación, transcodificación, remuestreo y cambio de tamaño.

La biblioteca de transcodificación de imágenes es compatible con los tipos MIME JPG/JPEG, PNG (8 y 16 bits), GIF, BMP, TIFF/TIFF comprimido (excepto archivos TIFF de 32 bits y archivos PTIFF), ICO e ICN.

Consulte [Biblioteca de transcodificación de imágenes](imaging-transcoding-library.md).

## Camera Raw compatible {#supported-camera-raw}

La biblioteca [!DNL Adobe Camera Raw] permite que [!DNL Assets] ingrese imágenes sin procesar. Ver [Soporte de Camera Raw](camera-raw.md).

## Formatos de documento [!DNL Assets] compatibles {#supported-document-formats}

Los formatos de documento admitidos para las funciones de administración de recursos son los siguientes:

| Formato | Almacenamiento | [Administración de metadatos](metadata.md) | Extracción de texto completo <br> | [Extracción de metadatos](metadata.md) | Generación de <br> en miniatura | [Extracción de subrecursos](managing-linked-subassets.md) | [Reescritura de metadatos](xmp-writeback.md) | [Recursos conectados](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| PUNTO | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| EPUB | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## Formatos multimedia admitidos {#supported-multimedia-formats}

| | Almacenamiento | Administración de metadatos | Extracción de metadatos | Generación de miniaturas | Transcodificación FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## Formatos de archivo compatibles {#supported-archive-formats}

Los formatos de archivo admitidos y la aplicabilidad de los flujos de trabajo comunes de DAM se tratan en la siguiente tabla.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Otros formatos admitidos {#other-supported-formats}

A continuación, se describe la aplicabilidad de las funcionalidades habituales de DAM para algunos formatos de archivo específicos.

| Formatos | Almacenamiento | Versiones | Flujo de trabajo | Publicación | Control de acceso | Entrega de Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (cuando se configura con su propio dominio de envío) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>La carga y distribución de archivos de JavaScript puede ser o no segura. Si es necesario, puede utilizar superposiciones para evitar que los usuarios carguen archivos JS.

## Tipos MIME admitidos {#supported-mime-types}

De manera predeterminada, [!DNL Experience Manager] detecta el tipo de archivo mediante la extensión de archivo. [!DNL Experience Manager] puede detectarlo a partir del contenido de los archivos. Para esto último, seleccione la opción [!UICONTROL Detectar MIME a partir del contenido] en [!UICONTROL Servicio Day CQ DAM Mime Type] en la consola web de [!DNL Experience Manager].

Hay disponible una lista de tipos MIME admitidos en CRXDE Lite en `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extensión de archivo | Tipo MIME/tipo de medio de Internet | Valor predeterminado de jobParam | Valor jobParam permitido |
|---|---|---|---|
| Imagen | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | El parámetro jobParam predeterminado se aplica a todos los recursos de tipo MIME de imagen.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| 3GP | video/3gpp | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| IA | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| BMP | image/bmp | | |
| CSS | texto/css | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| M4V | video/x-m4v | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MOV | video/quicktime | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MPEG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MPG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| SOC | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF/TIFF | image/tiff | | |
| TTC | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | video/dvd | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media: Formatos de vídeo de entrada compatibles para la transcodificación {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensión de archivo de vídeo | Contenedor | Códecs de vídeo recomendados | Códecs de vídeo no compatibles |
|---|---|---|---|
| AVI | Entrelazado A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (archivos de animación vectorial) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 y HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| MP4 | MPEG-4 | H264/AVC (todos los perfiles) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| ‡ MXF | MXF | XDCAM de Sony, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Pantalla Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

‡ Este formato de vídeo aún no es compatible con vídeos interactivos de Dynamic Media ni con anotaciones de Experience Manager Assets.

## Dynamic Media: formatos de documento compatibles {#supported-document-formats-dynamic-media}

| Formato | Cargar<br> (formato de entrada) | Crear <br> imagen<br> ajuste preestablecido<br> (formato de salida) | Vista previa <br> representación dinámica <br> | Enviar<br> representación <br> dinámica | Descargar <br> representación <br> dinámica |
|---|:---:|:---:|:---:|:---:|:---:|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (consulte la nota a continuación) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>En el caso de los PDF seguros, solo se admite la carga.

Además de la funcionalidad anterior, tenga en cuenta lo siguiente:

* Para usar Dynamic Media para generar representaciones dinámicas para archivos de PDF, consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar Dynamic Media para obtener una vista previa y generar representaciones dinámicas para archivos AI, consulte [Formatos de archivo Adobe Illustrator (AI), Postscript (EPS) y PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar Dynamic Media para generar representaciones dinámicas para archivos INDD, consulte [Formato de archivo de InDesign (INDD)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media: Formatos de imagen rasterizada compatibles {#supported-raster-image-formats-dynamic-media}

| Formato | Cargar (formato de entrada) | Crear ajuste preestablecido de imagen (formato de salida) | Previsualizar representación dinámica | Ofrecer representación dinámica | Descargar representación dinámica | Establecer tipos compatibles con este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md) y [Giro](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md) y [Giro](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md) y [Giro](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagen](/help/assets/image-sets.md), [Medios mixtos](/help/assets/mixed-media-sets.md) y [Giro](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ La imagen combinada se extrae del archivo PSD. Es una imagen generada por Adobe Photoshop y que se incluye en el archivo PSD. Según la configuración, la imagen combinada puede ser o no la imagen real.

* La compatibilidad con archivos EPS se aplica solo a imágenes rasterizadas. Por ejemplo, la generación de miniaturas para imágenes vectoriales de EPS no es compatible de forma predeterminada. Para agregar compatibilidad, [configure ImageMagick](best-practices-for-imagemagick.md). Para integrar herramientas de terceros y habilitar capacidades adicionales, consulte [Controlador de medios basado en la línea de comandos](media-handlers.md#command-line-based-media-handler).

* Para usar [!DNL Dynamic Media] con el fin de obtener una vista previa y generar representaciones dinámicas para los archivos de EPS, consulte los formatos de archivo [Adobe Illustrator (AI), Postscript (EPS) y PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para archivos EPS, la reescritura de metadatos es compatible con la versión 3.0 o posterior de la Convención de estructuración de documentos de PostScript (PS-Adobe).

## Dynamic Media: formatos de imagen rasterizada no compatibles {#unsupported-image-formats-dynamic-media}

La siguiente lista describe los subtipos de formatos de archivo de imagen rasterizada que *no* son compatibles con Dynamic Media.

Consulte también el artículo de la base de conocimiento [Detectar formatos de archivo no compatibles para Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* Archivos PNG con un tamaño de fragmento IDAT superior a 100 MB.
* Archivos PSB.
* Los archivos PSD con un espacio de color distinto de CMYK, RGB, escala de grises o mapa de bits no son compatibles. No se admiten los espacios de color DuoTone, Lab e Indexed.
* Archivos PSD con una profundidad de bits superior a 16.
* Archivos TIFF que tienen datos de punto flotante.
* Archivos TIFF que tienen espacio de color Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media: Formatos 3D compatibles {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos 3D.

Consulte también [Uso de recursos 3D en Dynamic Media](/help/assets/assets-3d.md).

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | Incluye los materiales y las texturas como un solo recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | *Sólo se admite la ingesta; no hay visualización ni interacción disponible.* USDZ es un formato 3D propietario que los dispositivos Safari y iOS pueden ver de forma nativa. |

>[!MORELIKETHIS]
>
>* [Habilitar compatibilidad con parámetros de trabajo de carga de Assets y Dynamic Media Classic basados en tipos MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configurar MIME basado en tipos para admitir parámetros de trabajo de carga](config-dynamic.md).
