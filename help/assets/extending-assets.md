---
title: Personalizar y ampliar  [!DNL Assets]
description: Conozca las formas en que puede personalizar y ampliar Asset Share y el Editor de recursos, que presenta a los usuarios una interfaz y un conjunto de funcionalidades específicamente adaptados.
contentOwner: AG
role: Developer
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Personalizar y ampliar [!DNL Assets] {#customizing-and-extending-assets}

El editor de recursos es el principal punto de acceso que los usuarios de un sitio web de Adobe Enterprise Manager utilizan para buscar, ver y manipular los recursos digitales del repositorio.

Como desarrollador de [!DNL Experience Manager], puede personalizar y ampliar el Editor de recursos de varias formas, presentando a los usuarios una interfaz específicamente diseñada y un conjunto de funcionalidades.

Los siguientes aspectos de la funcionalidad se pueden personalizar o mejorar:

* [Ampliar editor de recursos](asseteditorx.md)
* [Ampliar búsqueda de Assets](searchx.md)
* [Procesar Assets mediante controladores de medios y flujos de trabajo](media-handlers.md)
* [Integrar Assets con el flujo de actividad](extending-activity-stream.md)
* [Desarrollo de proxy de Assets](proxy.md)
* [Prácticas recomendadas para configurar ImageMagick](best-practices-for-imagemagick.md)

## Personalizar la apariencia {#customizing-the-look-and-feel}

Los siguientes aspectos de la apariencia del editor de recursos son personalizables:

* Logotipo: puede agregar el logotipo de su propia organización a la interfaz.
* Colores y fuentes: puede cambiar los colores y las fuentes utilizados en la interfaz.
* Código HTML: para una personalización más detallada, puede cambiar el código HTML subyacente que define las interfaces.

## Personalizar representaciones {#customizing-renditions}

En la terminología [!DNL Experience Manager Assets], una representación es la forma en que se presenta un recurso. En general, un recurso concreto puede tener varias representaciones. Por ejemplo, una imagen a todo color puede tener una representación en su tamaño original, otra en tamaño reducido y otra en escala de grises.

Las representaciones en las que está disponible un recurso concreto se pueden personalizar y se pueden crear nuevas representaciones.
