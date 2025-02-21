---
title: Instalación y configuración de ImageMagick
description: Obtenga información sobre el software ImageMagick, cómo instalarlo, configurar el paso del proceso de la línea de comandos y utilizarlo para editar, componer y generar miniaturas a partir de imágenes.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Instalar y configurar ImageMagick para que funcione con [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick es un complemento de software para crear, editar, componer o convertir imágenes de mapa de bits. Puede leer y escribir imágenes en varios formatos (más de 200), incluidos PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF y SVG. Utilice ImageMagick para cambiar el tamaño, voltear, reflejar, rotar, distorsionar, distorsionar y transformar imágenes. También puede ajustar los colores de la imagen, aplicar varios efectos especiales o dibujar texto, líneas, polígonos, elipses y curvas con ImageMagick.

Utilice el controlador multimedia [!DNL Adobe Experience Manager] de la línea de comandos para procesar imágenes mediante ImageMagick. Para trabajar con varios formatos de archivo mediante ImageMagick, consulte [Prácticas recomendadas de formatos de archivo Assets](/help/assets/assets-file-format-best-practices.md). Para obtener información acerca de todos los formatos de archivo compatibles, consulte [Formatos compatibles con Assets](/help/assets/assets-formats.md).

Para procesar archivos de gran tamaño con ImageMagick, tenga en cuenta los requisitos de memoria más altos de lo habitual, los posibles cambios necesarios en las políticas de mensajería instantánea y el impacto general en el rendimiento. Los requisitos de memoria dependen de varios factores como la resolución, la profundidad de bits, el perfil de color y el formato de archivo. Si tiene intención de procesar archivos muy grandes mediante ImageMagick, compare correctamente el servidor [!DNL Experience Manager]. Algunos recursos útiles se proporcionan al final.

>[!NOTE]
>
>Si usa [!DNL Experience Manager] en [!DNL Adobe Managed Services] (AMS), póngase en contacto con el servicio de atención al cliente de Adobe si planea procesar muchos archivos PSD o PSB de alta resolución. [!DNL Experience Manager] no puede procesar archivos PSB de muy alta resolución que tengan más de 30000 x 23000 píxeles.

## Instalar ImageMagick {#installing-imagemagick}

Hay varias versiones de los archivos de instalación de ImageMagic disponibles para varios sistemas operativos. Utilice la versión adecuada para su sistema operativo.

1. Descargue los [archivos de instalación de ImageMagick](https://www.imagemagick.org/script/download.php) adecuados para su sistema operativo.
1. Para instalar ImageMagick en el disco que hospeda el servidor [!DNL Experience Manager], inicie el archivo de instalación.

1. Defina la variable de entorno de ruta en el directorio de instalación de ImageMagic.
1. Para comprobar si la instalación se realizó correctamente, ejecute el comando `identify -version`.

## Configurar el paso del proceso de la línea de comandos {#set-up-the-command-line-process-step}

Puede configurar el paso del proceso de la línea de comandos para su caso de uso particular. Realice estos pasos para generar una imagen volteada y miniaturas (140x100, 48x48, 319x319 y 1280x1280) cada vez que agregue un archivo de imagen de JPEG a `/content/dam` en el servidor [!DNL Experience Manager]:

1. En el servidor [!DNL Experience Manager], vaya a la consola Flujo de trabajo (`https://[aem_server]:[port]/workflow`) y abra el modelo de flujo de trabajo **[!UICONTROL Recurso de actualización DAM]**.
1. En el modelo de flujo de trabajo **[!UICONTROL DAM Update Asset]**, abra el paso **[!UICONTROL miniaturas de EPS (con tecnología ImageMagick)]**.
1. En la ficha **[!UICONTROL Argumentos]**, agregue `image/jpeg` a la lista **[!UICONTROL Tipos MIME]**.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. En el cuadro **[!UICONTROL Comandos]**, escriba el siguiente comando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Seleccione los indicadores **[!UICONTROL Eliminar representación generada]** y **[!UICONTROL Generar representación web]**.

   ![select_flags](assets/select_flags.png)

1. En la ficha **[!UICONTROL Imagen Web]**, especifique los detalles de la representación con dimensiones de 1280 x 1280 píxeles. Además, especifique `image/jpeg` en el cuadro **[!UICONTROL Tipo MIME]**.

   ![imagen_habilitada_para_web](assets/web_enabled_image.png)

1. Haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

   >[!NOTE]
   >
   >Es posible que el comando `convert` no se ejecute con ciertas versiones de Windows (por ejemplo, Windows SE) porque está en conflicto con la utilidad nativa `convert` que forma parte de la instalación de Windows. En este caso, mencione la ruta completa de la utilidad ImageMagick. Por ejemplo, especifique,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Abra el paso **[!UICONTROL Procesar miniaturas]** y agregue el tipo MIME `image/jpeg` en **[!UICONTROL Omitir tipos MIME]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. En la ficha **[!UICONTROL Imagen Web habilitada]**, agregue el tipo MIME `image/jpeg` bajo la **[!UICONTROL Lista de omisión]**. Haga clic en **[!UICONTROL Aceptar]** para guardar los cambios.

   ![web_enabled](assets/web_enabled.png)

1. Guarde el flujo de trabajo.

1. Para comprobar el procesamiento correcto, cargue una imagen de JPG en [!DNL Assets]. Una vez completado el procesamiento, compruebe si se generan o no una imagen volteada y las representaciones.

## Mitigación de vulnerabilidades de seguridad {#mitigating-security-vulnerabilities}

El uso de ImageMagick para procesar imágenes presenta múltiples vulnerabilidades de seguridad. Por ejemplo, el procesamiento de imágenes enviadas por el usuario implica el riesgo de ejecución de código remoto (RCE).

Además, varios complementos de procesamiento de imágenes dependen de la biblioteca ImageMagick, incluidos, entre otros, la imagick de PHP, la imagemagick y el clip de papel de Ruby y la imagemagick de nodejs.

Si utiliza ImageMagick o una biblioteca afectada, Adobe recomienda mitigar las vulnerabilidades conocidas realizando al menos una de las siguientes tareas (pero preferiblemente ambas):

1. Compruebe que todos los archivos de imagen comienzan con los [&quot;bytes mágicos&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) esperados correspondientes a los tipos de archivo de imagen que admite antes de enviarlos a ImageMagick para su procesamiento.
1. Utilice un archivo de directiva para deshabilitar los codificadores de ImageMagick vulnerables. La directiva global de ImageMagick se encuentra en `/etc/ImageMagick`.
