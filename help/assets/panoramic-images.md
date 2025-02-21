---
title: Imágenes panorámicas
description: Aprenda a trabajar con imágenes panorámicas en Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Imágenes panorámicas{#panoramic-images}

En esta sección se describe el trabajo con el visualizador de imágenes panorámicas para procesar imágenes panorámicas esféricas y obtener una experiencia de visualización inmersiva de 360 grados de una habitación, propiedad, ubicación o paisaje.

Consulte también [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

![imagen-panorámica2](assets/panoramic-image2.png)

## Carga de recursos para utilizarlos con el visualizador de imágenes panorámicas {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para que un recurso cargado se califique como imagen panorámica esférica que desea utilizar con el visualizador de imágenes panorámicas, el recurso debe tener uno o ambos de los siguientes elementos:

* Una proporción de aspecto de 2.
Puede anular la configuración de proporción de aspecto predeterminada de 2 en CRXDE Lite en los siguientes casos:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Etiquetado con las palabras clave `equirectangular`, o `spherical` y `panorama`, o `spherical` y `panoramic`. Consulte [Uso de etiquetas](/help/sites-authoring/tags.md).

Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles de recursos y el componente WCM `Panoramic Media`.

Para cargar recursos para usarlos con el visor de imágenes panorámicas, consulte [Cargar Assets](/help/assets/manage-assets.md#uploading-assets).

## Configuración de Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Para que el visualizador de imágenes panorámicas funcione correctamente en Adobe Experience Manager, sincronice los ajustes preestablecidos del visualizador de imágenes panorámicas con Dynamic Media Classic y metadatos específicos de Dynamic Media Classic para que los ajustes preestablecidos del visualizador se actualicen en el JCR. Para realizar esta sincronización, configure Dynamic Media Classic de la siguiente manera:

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En la página Publicar en el servidor de imágenes, en el menú desplegable **[!UICONTROL Contexto de publicación]**, cerca de la parte superior, seleccione **[!UICONTROL Servicio de imágenes]**.

1. En la misma página de publicación del servidor de imágenes, busque el encabezado **[!UICONTROL Atributos de solicitud]**.
1. Bajo el encabezado de Solicitar atributos, busque **[!UICONTROL Límite de tamaño de imagen de respuesta]**. A continuación, en los campos asociados Anchura y Altura, aumente el tamaño máximo de imagen permitido para las imágenes panorámicas.

   Dynamic Media Classic tiene un límite de 25 000 000 de píxeles. El tamaño máximo permitido para imágenes con una relación de aspecto 2:1 es de 7000 x 3500. Sin embargo, para las pantallas de escritorio típicas, 4096 x 2048 píxeles es suficiente.

   >[!NOTE]
   >
   >Solo se admiten las imágenes que se encuentren dentro del tamaño de imagen máximo permitido. Las solicitudes de imágenes que superan el límite de tamaño dan como resultado una respuesta 403.

1. Bajo el encabezado Atributos de solicitud, haga lo siguiente:

   * Definir modo de confusión de solicitud en **[!UICONTROL Deshabilitado]**.
   * Establecer el modo de bloqueo de solicitud en **[!UICONTROL Deshabilitado]**.

   Esta configuración es necesaria para usar el componente WCM `Panoramic Media` en Experience Manager.

1. En la parte inferior izquierda de la página Publicación del servidor de imágenes, seleccione **[!UICONTROL Guardar]**.

1. En la esquina inferior derecha, seleccione **[!UICONTROL Cerrar]**.

### Solución de problemas del componente WCM de medios panorámicos {#troubleshooting-the-panoramic-media-wcm-component}

Si ha colocado una imagen en el componente de medios panorámicos del WCM y el marcador de posición de componente está contraído, solucione los siguientes problemas:

* Si experimenta un error 403 prohibido, podría deberse a que el tamaño de imagen solicitado es demasiado grande. Revise la configuración de **[!UICONTROL Límite de tamaño de imagen de respuesta]** en [Configurar Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Para ver un &quot;bloqueo no válido&quot; en el recurso o un &quot;error de análisis&quot; en la página, marque los modos Ofuscación de solicitud y Bloqueo de solicitud para asegurarse de que estén desactivados.
* Para un error de lienzo contaminado, configure una ruta de archivo de definición de conjunto de reglas e invalide CTN para las solicitudes anteriores del recurso de imagen.
* Si la calidad de la imagen se vuelve baja después de una solicitud de imagen con un tamaño superior al límite admitido, compruebe que la configuración **[!UICONTROL Atributos de codificación de JPEG > Calidad]** no esté vacía. Una configuración típica para el campo **[!UICONTROL Calidad]** es `95`. Puede encontrar la configuración en la página Publicación del servidor de imágenes. Para obtener acceso a la página, consulte [Configuración de Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Previsualizar imágenes panorámicas {#previewing-panoramic-images}

Ver [Vista previa de Assets](/help/assets/previewing-assets.md).

## Publicar imágenes panorámicas {#publishing-panoramic-images}

Ver [Publicar Assets](/help/assets/publishing-dynamicmedia-assets.md).
