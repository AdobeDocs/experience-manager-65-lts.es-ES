---
title: Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web
description: Obtenga información sobre cómo incrustar vídeos, imágenes o imágenes 3D de Dynamic Media en una página web
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 20%

---

# Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilice la función **[!UICONTROL Código incrustado]** cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código incrustado]**.

Solo puede incrustar direcciones URL si *no* usa Adobe Experience Manager como WCM. Si usa Experience Manager como WCM, [agrega los recursos directamente en la página](adding-dynamic-media-assets-to-pages.md).

Ver [URL de vínculo a su aplicación web](linking-urls-to-yourwebapplication.md).

Ver [Entregar imágenes optimizadas para un sitio adaptable](responsive-site.md).

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visualizador o de imagen.
>
>Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

**Para incrustar el vídeo, el visor de imágenes o el visor dimensional de Dynamic Media en una página web:**

1. Vaya al vídeo o recurso de imagen *publicado* cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visualizador o de imagen.

   Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione el menú desplegable y seleccione **[!UICONTROL Visualizadores]**.
1. En el carril izquierdo, seleccione un nombre de ajuste preestablecido de visualizador. El ajuste preestablecido de visualizador se aplica al recurso.
1. Seleccionar **[!UICONTROL Incrustar]**.
1. En el cuadro de diálogo **[!UICONTROL Código incrustado]**, copie todo el código en el portapapeles y, a continuación, seleccione **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Uso de HTTP/2 para entregar los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que los exploradores y servidores se comunican. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora se puede realizar a través de HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Entrega HTTP2 de contenido](http2.md) para obtener información detallada sobre cómo empezar a usar HTTP/2 con su cuenta de Dynamic Media.
