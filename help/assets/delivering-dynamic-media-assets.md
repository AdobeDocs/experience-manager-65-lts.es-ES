---
title: Entrega de recursos de Dynamic Media
description: Obtenga información sobre cómo distribuir recursos de Dynamic Media, como vídeos e imágenes, a sus páginas web.
role: User, Admin
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
exl-id: b91173b4-f1d1-4aad-97d2-782bc8aeaeab
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: e42ab83e-8918-43a7-98a3-62bebbd5bb3a
    internal-label: Renditions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 11%
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
* [Uso de conjuntos de reglas para transformar URL](/help/assets/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que los exploradores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Entrega HTTP/2 de contenido con las preguntas más frecuentes](/help/sites-administering/scene7-http2faq.md).
