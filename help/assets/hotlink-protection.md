---
title: Activar la protección de vínculos interactivos en Dynamic Media
description: Información sobre cómo activar la protección de vínculos interactivos en Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
feature: Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Activar la protección de vínculos interactivos en Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

La vinculación activa se produce cuando un sitio web de terceros utiliza código HTML para mostrar una imagen del sitio web. Utilizan el ancho de banda cada vez que se solicita la imagen, ya que el explorador del visitante accede a ella directamente desde el servidor. La protección de vínculos interactivos *protection* es un método para evitar que otros sitios web se vinculen directamente a imágenes, CSS o JavaScript en sus páginas web. Este tipo de escudo ayuda a reducir el uso innecesario del ancho de banda en su cuenta de Dynamic Media.

[Atención al cliente de Experience Manager](https://experienceleague.adobe.com/es?support-solution=Experience+Manager&amp;lang=es#support) puede configurar un filtro de referente en el nivel CDN (red de distribución de contenido) para que el contenido de Dynamic Media solo se ofrezca a los sitios web de su lista de sitios web permitidos para el dominio.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada que está integrada en Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada. Para activar la protección de vínculos interactivos, un administrador debe crear un ticket de asistencia al cliente de Adobe para solicitar el cambio de configuración a su cuenta de Dynamic Media. La activación de la protección de vínculos interactivos no supone ningún coste adicional.
