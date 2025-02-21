---
title: Prácticas recomendadas para procesar los formatos de archivo admitidos
description: Prácticas recomendadas para procesar los distintos tipos de archivo admitidos mediante  [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Prácticas recomendadas de formato de archivo Assets {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] admite muchas bibliotecas de formato de archivos de propiedad y de terceros para satisfacer diversos requisitos de compatibilidad con archivos de los usuarios. Las bibliotecas de Adobe admitidas son [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer y [!DNL Adobe InDesign Server]. Además, [!DNL Experience Manager Assets] admite bibliotecas de terceros, incluidas [!DNL ImageMagick], [!DNL TwelveMonkeys], etc.

Para ver los formatos de archivo admitidos, consulte [Formatos compatibles con Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Si utiliza [!DNL Experience Manager] en Adobe Managed Services (AMS), póngase en contacto con Asistencia al cliente de Adobe si planea procesar muchos archivos PSD o PSB grandes. Póngase en contacto con el representante de Asistencia al cliente de Adobe para implementar estas prácticas recomendadas en su implementación de AMS y para elegir las mejores herramientas y modelos posibles para los formatos propietarios de Adobe. [!DNL Experience Manager] no puede procesar archivos PSB de muy alta resolución que tengan más de 30000 x 23000 píxeles.

## [!DNL Adobe Camera Raw] biblioteca {#adobe-camera-raw-library}

Para obtener un rendimiento óptimo, Adobe recomienda usar la biblioteca [!DNL Adobe Camera Raw] para archivos RAW y DNG.

La biblioteca [!DNL Adobe Camera Raw] admite el perfil de color CMYK como entrada. Sin embargo, genera la salida en el espacio de color de RGB y solo admite la salida en formato JPEG. No conserva el espacio de color del archivo de origen (por ejemplo, CMYK) en las miniaturas.

Para obtener más información, consulte [Soporte técnico de Camera Raw](/help/assets/camera-raw.md).

## Biblioteca Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obtener los mejores resultados, Adobe recomienda utilizar la biblioteca Adobe PDF Rasterizer para los siguientes archivos:

* Archivos PDF pesados y con gran cantidad de contenido
* Archivos AI con miniaturas no generadas de forma predeterminada
* Para archivos AI con colores SPOT (PMS)

Las miniaturas y vistas previas generadas con PDF Rasterizer son de mejor calidad en comparación con la salida de trama predeterminada. La biblioteca Rasterizer de Adobe PDF no admite ninguna conversión de espacio de color. Independientemente del espacio de color del archivo PDF de origen, Adobe PDF Rasterizer genera únicamente la salida de RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recomienda usar [!DNL Adobe InDesign Server] para extraer representaciones específicas de [!DNL Adobe InDesign], como IDML y HTML. Para obtener más información, consulte [Agregar recursos de Experience Manager como referencias en Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento. Proporciona experiencias de visualización interactivas y optimiza el proceso de administración de campañas digitales. Para obtener más información sobre cómo habilitar [!DNL Dynamic Media], consulte [Configuración de Dynamic Media](/help/assets/config-dynamic.md).

Actualmente, [!DNL Dynamic Media] admite vídeos con hasta 15 GB de contenido por archivo.

## Biblioteca de ImageMagick {#imagemagick-library}

Adobe recomienda utilizar la biblioteca ImageMagick en los siguientes casos:

* Para generar representaciones de miniaturas para archivos EPS.
* Para conservar la información del perfil de la imagen.
* Para preservar la transparencia.
* Para procesar archivos PSD y PSB.

Para saber cómo configurar la biblioteca [!DNL ImageMagick] en [!DNL Experience Manager], consulte [Usar ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obtener un uso óptimo, consulte [Prácticas recomendadas para configurar ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificación de imágenes {#image-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes que realiza funciones básicas de administración de imágenes, como codificación, transcodificación, remuestreo, cambio de tamaño, etc.

La biblioteca de transcodificación de imágenes admite los siguientes tipos MIME:

* JPG/JPEG
* PNG (8 y 16 bits)
* GIF
* BMP
* TIFF/TIFF comprimido (excepto TIFF de 32 bits y TIFF).
* ICO
* ICN

Para obtener más información, consulte [Biblioteca de transcodificación de imágenes](/help/assets/imaging-transcoding-library.md).
