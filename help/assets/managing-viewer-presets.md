---
title: Administrar ajustes preestablecidos de visor
description: Crear, editar y administrar ajustes preestablecidos de visualizador en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Viewer Presets
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: bb860b28-19ee-4b1c-b420-3f61528156f0
source-git-commit: 6ceb03253f939734478cdc25b468737ceb83faa4
workflow-type: tm+mt
source-wordcount: '4396'
ht-degree: 7%

---

# Administrar ajustes preestablecidos de visor{#managing-viewer-presets}

Un ajuste preestablecido de visualizador es una colección de configuraciones que determinan cómo ven los usuarios los recursos de medios enriquecidos en las pantallas de sus equipos y dispositivos móviles. Si es administrador, puede crear ajustes preestablecidos de visualizador. Las opciones de configuración están disponibles para una matriz de opciones de configuración de visualizador. Por ejemplo, puede cambiar el tamaño de visualización del visor o el comportamiento de zoom.

Para obtener instrucciones sobre cómo crear y personalizar sus propios ajustes preestablecidos de visualizador de HTML5, consulte la *Documentación de la API de SDK del visualizador de HTML5* de Adobe Dynamic Media. SDK está disponible en el servidor de publicación de IS incrustado en el propio SDK. Cada versión de la biblioteca de tiene incluida su propia documentación de SDK.

Ruta: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
Por ejemplo, 3.10 SDK: [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

Consulte también la [Guía de referencia de visores de Dynamic Media de Adobe](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).

En esta sección se describe cómo crear, editar y administrar ajustes preestablecidos de visualizador. Puede aplicar un ajuste preestablecido de visualizador a un recurso en cualquier momento en el que lo previsualice. Consulte [Aplicación de ajustes preestablecidos de visor](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>No se admite la edición de *ajustes preestablecidos predefinidos listos para usar*. Si intenta editar un ajuste preestablecido de visualizador predeterminado, se le pedirá que guarde el ajuste preestablecido de visualizador con un nombre nuevo.

## Accesibilidad del teclado para visores {#keyboard-accessibility-for-viewers}

Todos los visores predeterminados admiten la accesibilidad del teclado.

Consulte también [Navegación y accesibilidad por teclado](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility).

## Administrar ajustes preestablecidos de visor {#managing-viewer-presets-1}

Puede agregar, editar, eliminar, publicar y cancelar la publicación y previsualizar ajustes preestablecidos de visualizador en Adobe Experience Manager al pulsar **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visualizador]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>De forma predeterminada, el sistema muestra 15 ajustes preestablecidos de visualizador al seleccionar Visualizadores en la vista de detalles de un recurso. Puede aumentar este límite. Consulte [Aumento del número de ajustes preestablecidos de visor que se muestran](#increasing-the-number-of-viewer-presets-that-display).

### Compatibilidad del visor con páginas web interactivas diseñadas {#viewer-support-for-responsive-designed-web-pages}

Las diferentes páginas web tienen diferentes necesidades. Por ejemplo, a veces desea una página web que proporcione un vínculo que abra el Visor de HTML5 en una ventana independiente del explorador. En otros casos, puede ser necesario incrustar el visualizador de HTML5 directamente en la página de alojamiento. En este último caso, la página web puede tener un diseño estático. O bien, puede ser &quot;adaptable&quot; y mostrarse de forma diferente en diferentes dispositivos o para diferentes tamaños de ventana del explorador. Para satisfacer estas necesidades, todos los visores HTML5 predefinidos e integrados que se incluyen con Dynamic Media admiten tanto páginas web estáticas como páginas web con diseño interactivo.

Consulte la [biblioteca de imágenes adaptables](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library) para obtener más información sobre cómo incrustar visores adaptables en las páginas web.

>[!NOTE]
>
>Publique todos los visores predeterminados antes de utilizarlos por primera vez.
>Ver [Ajustes preestablecidos de visor de publicación].(#publishing-viewer-presets)

### Compatibilidad del sistema de ajustes preestablecidos del visor {#viewer-preset-system-compatibility}

Todos los ajustes preestablecidos de visualizador integrados que se incluyen con Dynamic Media son totalmente compatibles con los siguientes sistemas:

* Equipos de escritorio
* Apple iPhone
* Apple iPad
* Smartphone Android™
* Android™ Tablet
* Para el vídeo, se proporciona compatibilidad adicional para la reproducción de MP4 en [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) y [Windows Phone](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs).

### Tipos de medios enriquecidos para ajustes preestablecidos de visualizador {#rich-media-types-for-viewer-presets}

Los administradores pueden añadir y personalizar los siguientes tipos de medios enriquecidos al crear ajustes preestablecidos de visualizador.

<table>
 <tbody>
  <tr>
   <td><strong>Conjunto de carrusel</strong><br /> </td>
   <td><p>Los puntos interactivos, los mapas de imagen o ambos se agregan a una serie de dos o más imágenes. Un cliente puede desplazar imágenes a la izquierda o a la derecha. A continuación, puede seleccionar un punto interactivo para obtener más información o realizar una compra directamente desde la categoría, la página principal o las páginas de aterrizaje de un sitio web.</p> </td>
  </tr>
  <tr>
   <td><strong>Dimensional</strong><br /> </td>
   <td><p>Muestre escenas 3D que le permitan girar, recorrer, ampliar o volver a centrar la cámara.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom flotante </strong></td>
   <td><p>Muestra una segunda imagen del área ampliada junto a la imagen original. No hay controles que utilizar: los usuarios mueven la selección sobre el área que desean ver.</p> <p>Al determinar el uso completo del ancho de banda para este visor, tenga en cuenta que tanto la imagen principal como la imagen flotante se proporcionan en el visor. El tamaño de la imagen principal (anchura y altura del escenario) y el factor de zoom determinan el tamaño de la imagen flotante. Para evitar que el tamaño del archivo flotante se vuelva demasiado grande, equilibre estos dos valores: si tiene un tamaño de imagen principal grande, reduzca el valor Factor de zoom. (La Anchura flotante y la Altura flotante determinan el tamaño de la ventana flotante, pero no el tamaño de la imagen flotante que se suministra al visualizador).</p> <p>Por ejemplo, si el tamaño de la imagen principal es de 350 por 350 píxeles, con un factor de zoom de 3, la imagen flotante resultante es de 1050 por 1050 píxeles. Si el tamaño de la imagen principal es de 300 por 300 píxeles, con un factor de zoom de 4, la imagen flotante es de 1200 por 1200 píxeles. Según la configuración de calidad de JPEG (la configuración recomendada está entre 80 y 90), puede reducir el tamaño del archivo significativamente. Los factores de zoom recomendados son de 2,5 a 4, según el tamaño de la imagen principal.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom en línea</strong></td>
   <td>Muestra una imagen del área ampliada dentro del visor original. No hay controles que utilizar. Es decir, los usuarios mueven la selección sobre el área que desean ver.</td>
  </tr>
  <tr>
   <td><strong>Conjunto de imágenes</strong></td>
   <td>En el visor de conjuntos de imágenes, los usuarios pueden ver diferentes vistas o variaciones de color de un elemento seleccionando una imagen en miniatura. Este visor también ofrece herramientas de zoom para examinar las imágenes de cerca.</td>
  </tr>
  <tr>
   <td><strong>Imagen interactiva</strong></td>
   <td>Los puntos interactivos se añaden a partes de una imagen que un cliente puede seleccionar para obtener más información o para comprarlos directamente desde la categoría, la página principal o las páginas de aterrizaje de un sitio web.</td>
  </tr>
  <tr>
   <td><strong>Vídeo interactivo</strong></td>
   <td>Las miniaturas se añaden a los segmentos de la cronología de un vídeo que un cliente puede seleccionar para obtener más información o para comprar directamente desde la categoría, la página principal o las páginas de aterrizaje de un sitio web.</td>
  </tr>
  <tr>
   <td><strong>Medios mixtos</strong></td>
   <td>Muestra diferentes tipos de medios en un visor. Puede incluir conjuntos de giros, conjuntos de imágenes, imágenes y vídeos.</td>
  </tr>
  <tr>
   <td><strong>Imagen panorámica</strong></td>
   <td><p>Los visores de imagen panorámica y de realidad virtual panorámica representan imágenes panorámicas esféricas para sumergir a los usuarios en una experiencia de visualización de 360 grados de una habitación, propiedad, ubicación o paisaje.</p> <p>Para que una imagen cargada pueda considerarse como un panorama esférico, debe tener uno o ambos de los siguientes elementos:</p>
    <ul>
     <li>Una relación de aspecto de 2:1.</li>
     <li>Etiquetado con las palabras clave <code>equirectangular</code>, o <code>spherical</code> y <code>panorama</code>, o <code>spherical </code> y <code>panoramic</code>. Consulte <a href="/help/sites-authoring/tags.md">Uso de etiquetas</a>.</li>
    </ul> <p>Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles de recursos y el componente WCM "Medios panorámicos".</p> <p><strong>Importante</strong>: este visor solo está disponible en modo Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Recorte inteligente de vídeos</strong><br /> </td>
   <td><p>Utilice este visor para detectar y recortar automáticamente al punto focal en cualquier vídeo.</p> </td>
  </tr>
  <tr>
   <td><strong>Conjunto de giros</strong></td>
   <td>Proporcionar varias vistas de una imagen para que los usuarios puedan girar el objeto y examinar los diferentes lados y ángulos.</td>
  </tr>
  <tr>
   <td><strong>Vídeo 360</strong></td>
   <td><p>Utilice el visualizador de vídeo 360/VR para procesar vídeo equirectangular y obtener una experiencia de visualización envolvente de una habitación, propiedad, ubicación, paisaje o procedimiento médico.</p> <p>Durante la reproducción en una pantalla plana, el usuario tiene control del ángulo de visión; la reproducción en dispositivos móviles suele aplicar sus controles giroscópicos integrados.</p> <p>El visor incluye compatibilidad nativa para la entrega de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. Puede entregar vídeo 360 con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.</p> <p><strong>Importante</strong>: este visor solo está disponible en modo Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Vídeo</strong></td>
   <td><p>Reproduce vídeo mediante flujo de bits progresivo o adaptable. La transmisión de velocidad de bits adaptable realiza automáticamente la detección de dispositivos y ancho de banda para ofrecer vídeo de la calidad correcta en el formato adecuado.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom vertical</strong></td>
   <td><p>El visor de zoom vertical le permite maximizar una experiencia de visualización de imágenes de producto para ofrecer a los usuarios la mejor representación de un producto. La ubicación vertical de las muestras hace lo siguiente:</p>
    <ul>
     <li>Garantiza que las muestras estén "por encima del pliegue".<br/>: con las muestras horizontales, según el tamaño de pantalla de escritorio del usuario, no serán visibles hasta que el usuario se desplace hacia abajo en la página. Al colocar las muestras verticalmente en el visor, se garantiza que sean visibles independientemente del tamaño de pantalla del usuario.</li>
     <li>Maximiza el tamaño de la imagen principal.<br />: con las muestras horizontales, es necesario reservar espacio en la página para asegurarse de que sean visibles. Este posicionamiento disminuyó el tamaño de la imagen principal. Sin embargo, con un diseño de muestra vertical, no es necesario asignar este espacio. De este modo, puede maximizar el tamaño de la imagen principal.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoom</strong></td>
   <td>Los usuarios pueden ampliar el área seleccionándola. Los usuarios pueden seleccionar controles para acercar, alejar y restablecer el tamaño predeterminado de la imagen.</td>
  </tr>
 </tbody>
</table>

### Lista de ajustes preestablecidos de visualizador integrados {#list-of-out-of-the-box-viewer-presets}

La siguiente tabla identifica todos los ajustes preestablecidos de visualizador predefinidos y listos para usar que se incluyen con Dynamic Media.

Ver también [demostraciones en vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

Para obtener información sobre las versiones compatibles del explorador web y el sistema operativo para los visualizadores, consulte las Notas de la versión de los visualizadores.

Consulte &quot;Notas de la versión de visores&quot; en la tabla de contenido de la [Guía de referencia de visores](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).

>[!NOTE]
>
>Todos los ajustes preestablecidos de visualizador listos para usar en Dynamic Media ya están activados (activados), pero debe publicarlos.
>Ver [Ajustes preestablecidos de visor de publicación](#publishing-viewer-presets).
>
>Los nuevos ajustes preestablecidos de visualizador que cree y agregue deben activarse y publicarse.
>Consulte [Activar o desactivar ajustes preestablecidos de visor](#activating-or-deactivating-viewer-presets) y [Publicar ajustes preestablecidos de visor](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>Título del ajuste preestablecido del visor</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nombre de archivo CSS</strong><br /> </td>
  </tr>
  <tr>
   <td>Carrusel_Dotted_dark</td>
   <td>Carrusel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Dotted_light</td>
   <td>Carrusel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Numérico_oscuro</td>
   <td>Carrusel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carrusel_Numeric_light</td>
   <td>Carrusel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Dimensional</td>
   <td>Dimensional</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>Flotante</td>
   <td>Zoom_flotante</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>Conjunto de imágenes</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>Conjunto de imágenes</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_oscuro</td>
   <td>Medios_Mixtos</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Medios_Mixtos</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Zoom_flotante</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_oscuro</td>
   <td>Medios_Mixtos</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Medios_Mixtos</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImage</td>
   <td>Imagen_panorámica</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Imagen_panorámica</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Vídeo</p> <p>(Incluye compatibilidad con subtítulos)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(Incluye controles básicos de reproducción de vídeo, el procesamiento de vídeo se realiza en modo estéreo, el control manual del punto de vista está desactivado, pero el control giroscópico está activado y no incluye funciones de medios sociales)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Diseñado para usuarios finales que utilizan gafas de realidad virtual. Incluye controles básicos de reproducción de vídeo y funciones de medios sociales)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(Incluye compatibilidad con subtítulos y medios sociales)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_oscuro<br /> </td>
   <td>Zoom<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>Zoom</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_oscuro<br /> </td>
   <td>Zoom_vertical</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Zoom_vertical</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Matriz de gestos de visores móviles admitidos {#supported-mobile-viewers-gestures-matrix}

La siguiente tabla identifica los gestos del visor móvil compatibles con los dispositivos iOS, Android™ 2.x y Android™ 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesto</strong></td>
   <td><strong>Zoom flotante </strong></td>
   <td><strong>Zoom</strong></td>
   <td><strong>Giro</strong></td>
  </tr>
  <tr>
   <td><p><strong>Arrastrar</strong></p> </td>
   <td><p>Panes</p> </td>
   <td><p>Panes</p> </td>
   <td><p>Panes</p> </td>
  </tr>
  <tr>
   <td><p><strong>Seleccionar</strong></p> </td>
   <td><p>Muestra una ventana flotante</p> </td>
   <td><p>Muestra u oculta la interfaz de usuario</p> </td>
   <td><p>Muestra u oculta la interfaz de usuario</p> </td>
  </tr>
  <tr>
   <td><p><strong>Seleccionar dos veces</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Aumenta o restablece</p> </td>
   <td><p>Aumenta o restablece</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pellizco abierto</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Amplía (solo iOS y Android™ 3 veces)</p> </td>
   <td><p>Amplía (solo iOS y Android™ 3 veces)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pellizco cerca</strong></p> </td>
   <td><p>No se aplica</p> </td>
   <td><p>Reduce (solo iOS y Android™ 3x)</p> </td>
   <td><p>Reduce (solo iOS y Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Barrido</strong></p> </td>
   <td><p>Barra de muestras de desplazamiento</p> </td>
   <td><p>Desplaza imágenes</p> </td>
   <td><p>Giros</p> </td>
  </tr>
  <tr>
   <td><p><strong>Flick</strong></p> </td>
   <td><p>Barra de muestras de desplazamiento</p> </td>
   <td><p>Desplaza imágenes</p> </td>
   <td><p>Giros</p> </td>
  </tr>
 </tbody>
</table>

## Aumente el número de ajustes preestablecidos de visualizador que se muestran {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager muestra una amplia variedad de ajustes preestablecidos de visor al ver un recurso desde **[!UICONTROL Vista de detalles]** > **[!UICONTROL Visualizadores]**. Puede aumentar o disminuir el número de visualizadores que se muestran.

**Aumentar el número de ajustes preestablecidos de visor que se muestran:**

1. Vaya a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Vaya al nodo de lista de ajustes preestablecidos de visualizador en la siguiente ubicación:

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. En la propiedad **[!UICONTROL limit]**, cambie el **[!UICONTROL valor]**, que se establece en 15 de forma predeterminada, por el número deseado.
1. Vaya al origen de datos del ajuste preestablecido de visor en `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. En la propiedad limit, cambie el número al deseado, por ejemplo, `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Seleccione **[!UICONTROL Guardar todo]**.

## Crear un ajuste preestablecido de visor {#creating-a-new-viewer-preset}

La creación de ajustes preestablecidos de visualizador permite aplicar varias configuraciones para ver e interactuar con los recursos. Sin embargo, no es necesario crear ajustes preestablecidos de visualizador. Si lo prefiere, puede utilizar los ajustes preestablecidos predeterminados del visualizador integrados que ya se incluyen con los AEM Assets.

Si decide crear un ajuste preestablecido de visualizador, después de guardarlo, su estado se activará automáticamente (se establecerá en **[!UICONTROL Activado]**) en la página de ajustes preestablecidos de visualizador. Este estado significa que está visible en el componente Dynamic Media y en el componente Interactive Media y siempre que se obtiene una vista previa de una imagen o vídeo.

Algunos ajustes preestablecidos del visualizador tienen ajustes exclusivos que pueden afectar al uso y al comportamiento general del visualizador. Según el ajuste preestablecido de visualizador que cree, es posible que desee tener en cuenta estas consideraciones especiales.

Consulte [Consideraciones especiales para crear un ajuste preestablecido de visualizador interactivo](#special-considerations-for-creating-an-interactive-viewer-preset).

Consulte [Consideraciones especiales para crear un ajuste preestablecido de visualizador de titulares de carrusel](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**Para crear un ajuste preestablecido de visor:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, haga clic en **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets] > [!UICONTROL Ajustes preestablecidos de visor]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. En la página Ajustes preestablecidos de visor, en la barra de herramientas, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Nuevo ajuste preestablecido de visor]**, en el campo **[!UICONTROL Nombre de ajuste preestablecido]**, escriba el nombre del nuevo ajuste preestablecido. Elija un nombre con cuidado; no se pueden editar después de seleccionar **[!UICONTROL Crear]**.

   Cuando guarde el ajuste preestablecido más adelante en estos pasos, el nombre aparecerá en la página Ajustes preestablecidos de visualizador bajo el encabezado de columna Título de ajuste preestablecido.

1. En el menú desplegable Tipo de medio enriquecido, seleccione el tipo de ajuste preestablecido de visualizador que desea crear y, a continuación, en la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]**.

   Consulte [Tipos de medios enriquecidos para ajustes preestablecidos de visor](#rich-media-types-for-viewer-presets).

1. En la página Editor de ajustes preestablecidos de visualizador, seleccione la ficha **[!UICONTROL Apariencia]**.
1. Realice una de las siguientes acciones:

   * En el menú desplegable **[!UICONTROL Tipo seleccionado]**, seleccione un componente cuyo diseño visual desee personalizar. Como alternativa, puede seleccionar cualquier elemento visual en el visor para seleccionarlo y configurarlo.

     El editor visual permite ver el efecto que una propiedad determinada tiene en un estilo. Establezca o ajuste cualquier propiedad para ver qué efecto tiene en el visor al instante mediante la muestra a la izquierda del editor.

     Las propiedades de estilo CSS para cada tipo de ajuste preestablecido de visor se describen en el tema de ayuda &quot;Personalización del visor *`<viewer name>`*&quot; de la [Guía de referencia de visores](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources). Por ejemplo, si está creando un ajuste preestablecido de visualizador de tipo `Mixed_Media`, consulte [Personalización del visualizador de medios mixtos](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer) para obtener una lista y una descripción de cada propiedad.

   * Si ha definido la configuración de estilo en un archivo CSS independiente, puede cargar el archivo CSS en los AEM Assets. Seleccione **[!UICONTROL Importar CSS]** del menú desplegable **[!UICONTROL Tipo seleccionado]**. Si es necesario, desplace el editor visual hacia arriba para buscar el archivo CSS cargado y asociarlo al ajuste preestablecido de visualizador.

     Al importar un archivo CSS, el editor visual comprueba si el CSS utiliza los marcadores de visor correctos. Por ejemplo, si está creando un visor de zoom, todas las reglas CSS que importe deben definirse con su nombre de clase de visor `.s7mixedmediaviewer` definido en un elemento de visor principal.

     Puede importar CSS arbitrario y hecho a mano siempre que defina correctamente los marcadores CSS de un visor determinado. (Los marcadores CSS se describen en cualquier tema de ayuda &quot;Personalización de *&lt;nombre del visor>* Visor&quot; de la [Guía de referencia de visores](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources). Por ejemplo, si desea leer acerca de los marcadores CSS para el visor de zoom, consulte [Personalización del visor de zoom](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer).) Sin embargo, es posible que el editor visual no entienda algunos valores CSS. En estos casos, el editor visual intenta anular los errores para que el CSS pueda seguir funcionando.

   >[!NOTE]
   >
   >Si prefiere editar la CSS directamente en su formulario sin procesar, seleccione **[!UICONTROL Mostrar / Ocultar CSS]** debajo del menú desplegable Tipo seleccionado (si es necesario, desplace el editor visual hacia arriba para verlo).
   >Al igual que el editor visual, cuando cambia una propiedad directamente en CSS, ve instantáneamente qué efecto tiene en la muestra del visor. Y, esa misma propiedad se actualiza automáticamente al mismo tiempo en el editor visual. Como tal, puede utilizar el editor CSS sin procesar o el editor visual, o utilizar ambos de forma intercambiable.

   >[!NOTE]
   >
   >Para las ilustraciones de botón, elija la imagen 2x y cargue obras de arte de alta resolución. Al trabajar con imágenes interactivas y titulares de ventas, también puede seleccionar entre varios botones de puntos interactivos predeterminados.

1. (Opcional) Cerca de la parte superior de la página Editar ajuste preestablecido de visor, seleccione **[!UICONTROL Escritorio]**, **[!UICONTROL Tablet]** o **[!UICONTROL Teléfono]** para definir estilos visuales únicos para diferentes tipos de dispositivos y pantallas.
1. En la página Editor de ajustes preestablecidos de visualizador, seleccione la ficha **[!UICONTROL Comportamiento]**. Como alternativa, puede seleccionar cualquier elemento visual en el visor para seleccionarlo y configurarlo.
Por ejemplo, para el tipo *VideoPlayer*, en **[!UICONTROL Modificadores]** > **[!UICONTROL Reproducción]**, puede seleccionar una de las tres opciones de flujo de velocidad de bits adaptable:

   * **[!UICONTROL dash]**: los vídeos se transmiten solo como dash. Sin embargo, en dispositivos Safari/iOS, debe seleccionar **[!UICONTROL hls]** como tipo en su lugar.
   * **[!UICONTROL hls]**: los vídeos se transmiten solo como hls.
   * **[!UICONTROL auto]**: práctica recomendada. La creación de flujos DASH y HLS está optimizada para el almacenamiento. Por lo tanto, Adobe recomienda que siempre seleccione **[!UICONTROL auto]** como tipo de reproducción. Los vídeos se transmiten como guión, hls o progresivo, como en el siguiente orden de reproducción:
      * Si el navegador admite DASH, primero se utiliza la transmisión por secuencias DASH.
      * Si el explorador no admite DASH, se utiliza la transmisión por secuencias de HLS en segundo lugar.
      * Si el navegador no es compatible con DASH o HLS, se utiliza la reproducción progresiva en último lugar.

1. En el menú desplegable **[!UICONTROL Tipo seleccionado]**, seleccione un componente cuyos comportamientos desee cambiar.

   Muchos componentes del editor visual tienen asociada una descripción detallada. Estas descripciones aparecen en los cuadros azules cuando se expande un componente para mostrar sus parámetros asociados.

   Algunos tipos de visualizador tienen componentes que permiten especificar comandos del servicio de imágenes en un campo de texto **[!UICONTROL Comando IS]**. Para obtener una lista de los comandos que puede utilizar, consulte la [Referencia de API del servicio de imágenes](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home).

   >[!NOTE]
   >
   >**Si usa un dispositivo táctil, como un teléfono o una tableta...**
   >
   >
   >Después de escribir un valor en el campo de texto, seleccione en cualquier otra parte de la interfaz de usuario para enviar el cambio y cerrar el teclado virtual. Si selecciona Entrar, no se producirá ninguna acción.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.
1. Publique el nuevo ajuste preestablecido de visualizador para que pueda utilizarlo en su sitio web.

   Ver [Ajustes preestablecidos de visor de publicación](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >Para los vídeos antiguos que usan un perfil de flujo de velocidad de bits adaptable, la URL seguirá reproduciéndose como de costumbre (con flujo HLS) hasta que [vuelva a procesar los recursos de vídeo](/help/assets/processing-profiles.md#reprocessing-assets). Después de volver a procesar, la misma dirección URL sigue funcionando, pero ahora con *streaming de DASH y HLS de* habilitado.

### Consideraciones especiales para crear un ajuste preestablecido de visualizador interactivo {#special-considerations-for-creating-an-interactive-viewer-preset}

**Acerca de los modos de visualización para miniaturas de imagen en el panel**

Al crear o editar un ajuste preestablecido de visualizador de vídeo interactivo, puede elegir un ajuste de Modo de visualización. Esta opción aparece cuando selecciona `InteractiveSwatches` del menú **[!UICONTROL Componente seleccionado]** en la ficha **[!UICONTROL Comportamiento]**. El modo de visualización que elija afecta a cómo y cuándo aparecerán las miniaturas mientras se reproduce el vídeo. Puede elegir un modo de visualización `segment` (predeterminado) o `continuous`.

<table>
 <tbody>
  <tr>
   <td><strong>Modo de visualización</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Segmento</td>
   <td><p><code>Segment </code>es el modo de visualización predeterminado para los ajustes preestablecidos predeterminados de visualizador de vídeo interactivo <code>Shoppable_Video_light</code> y <code>Shoppable_Video_dark</code>, y para cualquier ajuste preestablecido de visualizador de vídeo interactivo que cree usted mismo.</p> <p>En este modo, cuando hay menos miniaturas asignadas a un segmento de vídeo que el número de puntos visibles en el panel de visualización. Además, las miniaturas de los subsegmentos siguientes o anteriores no se <i>extraen para rellenar ningún punto vacío en el panel. </i> Es decir, conserva la visualización de muestras asignadas al segmento de vídeo concreto.</p> </td>
  </tr>
  <tr>
   <td>Continuo</td>
   <td><p>En el modo de visualización <code>continuous </code>, si el número de miniaturas de un segmento es menor que el número visible en el panel, el visor incluye automáticamente la visualización de miniaturas del siguiente segmento. O bien, el visor incluye automáticamente la visualización de las miniaturas del segmento anterior, en los casos en que se muestra la última miniatura.</p> <p>El <a href="/help/assets/interactive-videos.md">vídeo de este tema</a> es un ejemplo del modo de visualización <code>continuous </code>de.</p> </td>
  </tr>
 </tbody>
</table>

**Acerca del comportamiento de desplazamiento automático en el visor de vídeo interactivo**

El comportamiento Desplazamiento automático de las miniaturas en el visualizador de vídeo interactivo funciona independientemente del modo de visualización elegido.

Cuando crea o edita un ajuste preestablecido de visualizador de vídeo interactivo, accede al desplazamiento automático desde la pestaña Comportamiento. En la ficha Comportamiento, en el menú desplegable **[!UICONTROL Componentes seleccionados]**, seleccione **[!UICONTROL Muestras interactivas]**. La casilla de verificación Desplazamiento automático aparece debajo del campo de texto Comando IS.

Si desactiva el **[!UICONTROL desplazamiento automático]** (desactive la casilla de verificación) en el ajuste preestablecido de visualizador, durante la reproducción del vídeo por parte del usuario, el panel solo muestra la primera imagen en miniatura durante toda la duración del vídeo. Sin embargo, un usuario puede desplazarse manualmente por las miniaturas utilizando los iconos de flecha arriba y abajo, si lo desea.

Al activar (seleccionar) **[!UICONTROL Desplazamiento automático]** en el ajuste preestablecido de visualizador, durante la reproducción de vídeo, las imágenes en miniatura asignadas a un segmento de vídeo se desplazan hasta la vista al principio de un segmento. Sin embargo, hay instancias en las que ciertas miniaturas de un segmento se muestran el doble de tiempo que otras miniaturas antes o después de este segmento. Este comportamiento se produce porque el número de miniaturas de un segmento es mayor que el número visible en el panel y no se puede dividir de manera uniforme.

Para ilustrar, supongamos que tiene un segmento de vídeo de 30 segundos. Además, hay un total de nueve miniaturas que se mostrarán durante los 30 segundos. El tamaño del explorador es tal que hay cuatro posiciones de miniaturas visibles en el panel de visualización. El segmento de tiempo del vídeo de 30 segundos se divide en tres subsegmentos. La siguiente tabla muestra el desglose de las miniaturas que se muestran para un subsegmento de tiempo determinado:

| **Subsegmento de vídeo** | **Tiempo de subsegmento en segundos** | **Miniaturas visibles en el panel** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | De 10 a 20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

El subsegmento de vídeo 3 no se extiende más allá de las miniaturas que se le han asignado. Observe también que las miniaturas 4, 6 y 7 son visibles en el panel el doble de tiempo que las otras miniaturas.

La lógica que el visor utiliza para cuántas miniaturas se muestran en el panel según el número de posiciones disponibles es la siguiente:

* Número de subsegmentos = redondear hacia arriba hasta el siguiente subsegmento (número de miniaturas / número de ranuras visibles en el panel de miniaturas, según el tamaño de la ventana del explorador).
Con el ejemplo de la tabla anterior, 9 miniaturas / 4 ranuras = 2,25; la lógica del visor lo redondea hasta tres subsegmentos.

* Número de miniaturas = redondear hacia arriba hasta la miniatura siguiente (número de miniaturas / número de subsegmentos de vídeo).
Con el ejemplo de la tabla anterior, 9 miniaturas / 3 subsegmentos de vídeo = 3 miniaturas.

* Duración del subsegmento = duración total del vídeo / número de subsegmentos del vídeo.
En el ejemplo de la tabla anterior, 30 segundos / 3 subsegmentos de vídeo = visualización de 10 segundos de cada subsegmento de vídeo.

#### Consideraciones especiales para crear ajustes preestablecidos del visualizador de titulares de carrusel {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

Al crear ajustes preestablecidos de visualizador de titular de carrusel, se puede acceder a cambiar el estilo de las zonas interactivas de la siguiente manera:

| | **Descripción** | **Acciones** |
|---|---|---|
| **[!UICONTROL Icono de punto interactivo]** | Cambiar el icono utilizado para el punto interactivo | Para cambiar la imagen del icono de punto interactivo, en la ficha **[!UICONTROL Aspecto]**, en **[!UICONTROL Componente seleccionado]**, seleccione **[!UICONTROL ImageMapEffect]**. En **[!UICONTROL Icono]**, seleccione **[!UICONTROL Fondo]** y en el campo **[!UICONTROL Imagen]** vaya a la imagen de fondo que desee. |

## Activar o desactivar ajustes preestablecidos de visualizador {#activating-or-deactivating-viewer-presets}

Los ajustes preestablecidos de visualizador disponibles en la interfaz de usuario dependen de los que estén activos en el modo Autor. De forma predeterminada, un ajuste preestablecido de visualizador está &quot;Activado&quot; después de crearlo. Si desactiva el ajuste preestablecido, no lo verá en el modo Autor. Si se publica el ajuste preestablecido, siempre se publica independientemente de si está activado o desactivado. Es posible que desee desactivar los ajustes preestablecidos del visualizador si la lista resulta demasiado complicada o si no desea que un ajuste preestablecido del visualizador esté disponible para su uso.

**Para activar o desactivar los ajustes preestablecidos del visor:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, seleccione **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. En la página Ajuste preestablecido de visor, en el encabezado de columna **[!UICONTROL State]**, seleccione la opción para activar o desactivar un ajuste preestablecido de visor.

   Los ajustes preestablecidos del visor que están activados tienen el conmutador a la derecha, dentro de un cuadro azul; los ajustes preestablecidos del visor desactivados tienen el conmutador a la izquierda, dentro de un cuadro gris claro.

## Publicar ajustes preestablecidos de visor {#publishing-viewer-presets}

Activar (o activar) el estado de un ajuste preestablecido de visualizador significa que está visible en el componente Dynamic Media, en el componente Interactive Media y siempre que visualice un recurso.

Sin embargo, para *entregar* un recurso con un ajuste preestablecido de visualizador, también se debe publicar el ajuste preestablecido de visualizador. Todos los ajustes preestablecidos de visualizador se deben activar *y* se deben publicar para obtener la URL o el código incrustado de un recurso. Asegúrese de activar y publicar todos los ajustes preestablecidos de visualizador integrados que se incluyen con Dynamic Media. Los ajustes preestablecidos de visualizador personalizado que cree y agregue se activan automáticamente, pero también se deben publicar.

Consulte [Activar o desactivar ajustes preestablecidos de visor](#activating-or-deactivating-viewer-presets).

Ver también [Vista previa de Assets](/help/assets/previewing-assets.md).

**Para publicar ajustes preestablecidos de visor:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, haga clic en **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. Seleccione uno o varios ajustes preestablecidos de visualizador que desee publicar.
1. En la barra de herramientas, haga clic en el icono **[!UICONTROL Publicar]**.

## Ordenar ajustes preestablecidos de visor {#sorting-viewer-presets}

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, seleccione **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. Seleccione **[!UICONTROL Título de ajuste preestablecido]**, **[!UICONTROL Tipo]**, **[!UICONTROL Publicado]** o **[!UICONTROL Estado]** para ordenar por ese encabezado de columna. Por ejemplo, seleccione **[!UICONTROL Tipo]** para ordenar los tipos de ajustes preestablecidos de visor en orden alfabético o alfabético inverso.

## Editar ajustes preestablecidos de visor {#editing-viewer-presets}

No se admite la edición de *ajustes preestablecidos predefinidos listos para usar*. Si edita un ajuste preestablecido de visualizador predeterminado, se le pedirá que lo guarde con un nombre nuevo.

**Para editar los ajustes preestablecidos del visor:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, seleccione **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Recurso]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. Seleccione un ajuste preestablecido marcando la casilla a la izquierda del título del ajuste preestablecido del visualizador.
1. En la barra de herramientas, seleccione **[!UICONTROL Editar]**.
1. En la página **[!UICONTROL Editor de ajustes preestablecidos de visor]**, realice los cambios que desee en el ajuste preestablecido de visor con las opciones que se encuentran en las fichas **[!UICONTROL Apariencia]** y **[!UICONTROL Comportamiento]**.

   En la ficha **[!UICONTROL Aspecto]**, cerca de la esquina superior izquierda de la página Editor de ajustes preestablecidos de visor, seleccione **[!UICONTROL Escritorio]**, **[!UICONTROL Tableta]** o **[!UICONTROL Teléfono]** para cambiar el modo de presentación del recurso.

1. Cerca de la esquina superior derecha de la página, siga uno de estos procedimientos:

   * Seleccione **[!UICONTROL Guardar]** para guardar los cambios y volver a la página Ajuste preestablecido de visor.
   * Seleccione **[!UICONTROL Cancelar]** para anular los cambios realizados y volver a la página Ajuste preestablecido de visor.

## Eliminar ajustes preestablecidos de visor personalizados {#deleting-custom-viewer-presets}

Puede eliminar los ajustes preestablecidos de visualizador que haya creado y agregado a Dynamic Media.

**Para eliminar los ajustes preestablecidos de visor personalizado:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. A continuación, en el carril izquierdo, seleccione **[!UICONTROL Herramientas]** (icono de martillo) **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. En la página Ajustes preestablecidos de visor, marque un Título de ajuste preestablecido y luego seleccione el icono **[!UICONTROL Papelera]**.
1. Seleccione **[!UICONTROL Eliminar]**.

## Aplicar un ajuste preestablecido de visualizador a un recurso {#applying-a-viewer-preset-to-an-asset}

Si ya ha publicado el recurso y el visualizador seleccionado, los botones **[!UICONTROL URL]** e **[!UICONTROL Incrustar]** aparecerán después de seleccionar un ajuste preestablecido de visualizador.

**Para aplicar un ajuste preestablecido de visor a un recurso:**

1. Abra el recurso y cerca de la esquina superior izquierda de la página, seleccione el menú desplegable y luego seleccione **[!UICONTROL Visualizadores]**.

   >[!NOTE]
   >
   >Si ya ha publicado el recurso y el visualizador seleccionado, los botones **[!UICONTROL URL]** e **[!UICONTROL Incrustar]** aparecerán después de seleccionar un ajuste preestablecido de visualizador.

1. Seleccione un ajuste preestablecido de visualizador en el panel izquierdo para poder aplicarlo al recurso.

   Puede [copiar la dirección URL para compartir](/help/assets/linking-urls-to-yourwebapplication.md) con otros usuarios.

## Entrega de recursos con ajustes preestablecidos de visualizador {#delivering-assets-with-viewer-presets}

Para obtener las direcciones URL de los ajustes preestablecidos de visor, consulte [Vinculación de direcciones URL a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). Consulte también [Incrustación del visor de vídeo en una página web](/help/assets/embed-code.md).

Si utiliza Experience Manager como WCM, puede agregar recursos utilizando los ajustes preestablecidos del visualizador directamente en la página. Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).
