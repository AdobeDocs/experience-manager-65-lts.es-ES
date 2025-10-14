---
title: Vídeo 360/VR
description: Aprenda a trabajar con 360 y el vídeo de realidad virtual (VR) en Dynamic Media y a utilizarlos.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: 360 VR Video
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# Vídeo 360/VR {#vr-video}

Los vídeos de 360 grados graban una vista en todas las direcciones al mismo tiempo. Se filman con una cámara omnidireccional o una colección de cámaras. Durante la reproducción en una pantalla plana, el usuario tiene control del ángulo de visión; las reproducciones en dispositivos móviles suelen utilizar sus controles giroscópicos integrados.

Dynamic Media: el modo Scene7 incluye compatibilidad nativa para la entrega de recursos de vídeo 360. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. Puede entregar vídeo 360 con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

En esta sección se describe el trabajo con el visualizador de vídeo 360/VR para procesar vídeo equirectangular y obtener una experiencia de visualización envolvente de una sala, propiedad, ubicación, paisaje, procedimiento médico, etc.

Actualmente no se admite audio espacial; si el audio se mezcla en estéreo, el equilibrio (I/D) no cambia a medida que el cliente cambia el ángulo de visión de la cámara.

Consulte también [Administración de ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

## Vídeo 360 en acción {#video-in-action}

Seleccione [Estación espacial 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir una ventana del explorador y ver un vídeo de 360 grados. Durante la reproducción de vídeo, arrastre el puntero del mouse a una nueva ubicación para cambiar el ángulo de visualización.

![Muestra de 360 vídeos con la estación espacial internacional flotando en el espacio exterior y la tierra y el sol detrás.](assets/6_5_360videoiss_simplified.png)
*Fotograma de vídeo de la Estación Espacial 360*

## Vídeo 360/VR y Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Puede utilizar Adobe Premier Pro para ver y editar material de archivo de 360/VR. Por ejemplo, puede colocar logotipos y texto correctamente en una escena y aplicar efectos y transiciones diseñados específicamente para medios equirectangulares.

Ver [Editar vídeo de 360/VR](https://helpx.adobe.com/es/premiere-pro/how-to/edit-360-vr-video.html).

## Carga de recursos para utilizarlos con el visualizador de vídeo 360 {#uploading-assets-for-use-with-the-video-viewer}

360 recursos de vídeo que se han cargado en Adobe Experience Manager están etiquetados como **Multimedia** en una página de Asset, de manera similar a un recurso de vídeo normal.

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*Se ha cargado un recurso de vídeo de 360 visualizado en la vista de tarjeta. El recurso está etiquetado como Multimedia.*

**Cargar recursos para usarlos con el visor de vídeo 360:**

1. Se ha creado una carpeta dedicada a su recurso de vídeo 360.
1. [Aplicar un perfil de vídeo adaptable a la carpeta](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   La representación de contenido de vídeo de 360 bits exige mayores requisitos para la resolución de vídeo de origen y para la resolución de representaciones codificadas que el contenido de vídeo estándar que no es de 360 bits.

   Puede utilizar el perfil de vídeo adaptable incorporado que ya viene con Dynamic Media. Sin embargo, resulta en una calidad de vídeo 360 perceptiblemente menor que la que obtendría con un vídeo no 360 codificado con los mismos ajustes procesados con un visor no 360. Por lo tanto, si se requiere vídeo 360 de alta calidad, haga lo siguiente:

   * Lo ideal es que el contenido original de vídeo de 360 bits tenga una de las siguientes resoluciones:

      * 1080p - 1920 x 1080, conocida como resolución Full HD o FHD o,
      * 2160p: 3840 x 2160, conocida como resolución 4k, UHD o Ultra HD. Esta resolución de pantalla grande se encuentra más a menudo en televisores y monitores de ordenador de primera calidad. La resolución de 2160p se denomina a menudo &quot;4k&quot; porque la anchura está cerca de los 4000 píxeles. En otras palabras, ofrece cuatro veces los píxeles de 1080p.

   * [Crear un perfil de vídeo adaptable personalizado](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) con representaciones de mayor calidad. Por ejemplo, cree un perfil de vídeo adaptable que contenga las tres configuraciones siguientes:

      * anchura=auto; altura=720; velocidad de bits=2500 kbps
      * anchura=auto; altura=1080; velocidad de bits=5000 kbps
      * anchura=auto; altura=1440; velocidad de bits=6600 kbps

   * Procesar contenido de vídeo de 360 en una carpeta dedicada exclusivamente a recursos de vídeo de 360.

   Este enfoque impone mayores exigencias a la red y al CPU del usuario final.

1. [Cargue el vídeo en la carpeta](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## Anular la proporción de aspecto predeterminada de 360 vídeos  {#overriding-the-default-aspect-ratio-of-videos}

Para que un recurso cargado se califique como vídeo 360 que desea utilizar con el visualizador de vídeo 360, el recurso debe tener una proporción de aspecto de 2.

De forma predeterminada, Experience Manager detecta el vídeo como &quot;360&quot; si su relación de aspecto (anchura/altura) es 2,0. Si es administrador, puede anular el valor predeterminado de proporción de aspecto de 2 estableciendo la propiedad opcional `s7video360AR` en CRXDE Lite en el siguiente enlace:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Tipo de propiedad** - Doble
   * **Valor** - proporción de aspecto de punto flotante, valor predeterminado 2.0.

Después de establecer esta propiedad, se aplica inmediatamente tanto a los vídeos existentes como a los vídeos cargados recientemente.

La proporción de aspecto se aplica a 360 recursos de vídeo para la página de detalles de recursos y el [componente WCM de medios de vídeo 360](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Comience por cargar 360 vídeos.

## Vista previa del vídeo 360 {#previewing-video}

Puede usar Vista previa para ver el aspecto del vídeo 360 para los clientes y asegurarse de que se comporta según lo esperado.

Consulte también [Editar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

Cuando esté satisfecho con el vídeo 360, puede publicarlo.

Ver [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/embed-code.md).
Ver [URL de vínculo a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para obtener una vista previa del vídeo 360:**

1. En **[!UICONTROL Assets]**, desplácese hasta un vídeo 360 existente que haya creado. Seleccione el recurso de vídeo 360 para poder abrirlo en el modo de vista previa.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Seleccione el recurso de vídeo de 360 bits para poder previsualizar el vídeo.

1. En la página de vista previa, cerca de la esquina superior izquierda de la página, selecciona la lista desplegable y luego selecciona **[!UICONTROL Visualizadores]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   En la lista Visualizadores, seleccione **[!UICONTROL Video360_social]** y, a continuación, siga uno de estos procedimientos:

   * Arrastre el puntero del ratón por el vídeo si desea modificar el ángulo de visualización de la escena estática.
   * Seleccione el botón **[!UICONTROL Reproducir]** del vídeo si desea que comience la reproducción. A medida que se reproduce el vídeo, arrastre el puntero del mouse (ratón) por el vídeo para modificar el ángulo de visualización.

   ![Captura de pantalla de la estación espacial internacional flotando en el espacio exterior con la Tierra y el Sol en segundo plano &#x200B;](assets/6_5_360video-preview-video360-social.png)*Captura de pantalla de 360 píxeles.*

   * En la lista Visualizadores, seleccione **[!UICONTROL Video360VR]**.

     El vídeo de realidad virtual (VR) es contenido de vídeo envolvente al que se accede mediante auriculares de realidad virtual. Al igual que con los vídeos normales, puede crear vídeos de realidad virtual al principio cuando se graba o captura un vídeo con cámaras de vídeo de 360 grados.

   ![Captura de pantalla de un primer plano de la estación espacial internacional flotando en el espacio ultraterrestre con la Tierra y el Sol parcialmente visibles en segundo plano](assets/6_5_360video-preview-video360vr.png)
   *Captura de pantalla de un vídeo de RV de 360.*

1. Cerca de la parte superior derecha de la página de vista previa, seleccione **[!UICONTROL Cerrar]**.

## Publicación de vídeo 360 {#publishing-video}

Publique el vídeo 360 para poder utilizarlo. La publicación de un vídeo 360 activa la URL y el código de incrustación. También publica el vídeo 360 en la nube de Dynamic Media, que está integrada con una CDN para una entrega escalable y con buen rendimiento.

Consulte [Publicar recursos de Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar vídeo 360.
Consulte también [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/embed-code.md).
Ver también [URL de vínculo a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte también [Agregar recursos de Dynamic Media a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).
