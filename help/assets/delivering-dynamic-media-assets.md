---
title: Entrega de recursos de Dynamic Media
description: Obtenga información sobre cómo distribuir recursos de Dynamic Media, como vídeos e imágenes, a sus páginas web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 9%

---

# Entrega de recursos de Dynamic Media{#delivering-dynamic-media-assets}

La forma de entregar los recursos de Dynamic Media, tanto de vídeo como de imágenes, depende de cómo se implemente el sitio web.

Con Dynamic Media, tiene varias opciones:

* Si el sitio web está alojado en Adobe Experience Manager, quiere añadir los recursos de Dynamic Media directamente a la página.
* Si el sitio web no está en Experience Manager, puede elegir una de estas opciones:

   * Incrustar el vídeo o la imagen en el sitio web.
   * Vincule las URL a la aplicación web. Utilice la vinculación cuando desee distribuir un reproductor de vídeo como ventana emergente o modal.
   * Si tu sitio es interactivo, puedes [ofrecer imágenes optimizadas](/help/assets/responsive-site.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan inteligencia en el último milisegundo de entrega para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión del explorador o de la red. Consulte [Imágenes inteligentes](/help/assets/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Adición de recursos de Dynamic Media a páginas web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md)
* [Activación de la protección de enlaces interactivos en Dynamic Media](/help/assets/hotlink-protection.md)
* [Vinculación de URL en la aplicación web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribución de imágenes optimizadas para un sitio adaptable](/help/assets/responsive-site.md)
* [Entrega HTTP2 de contenido](/help/assets/http2.md)
* [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de reglas para transformar URL](/help/assets/using-rulesets-to-transform-urls.md)


## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que los exploradores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Entrega HTTP/2 de contenido con las preguntas más frecuentes](/help/sites-administering/scene7-http2faq.md).
