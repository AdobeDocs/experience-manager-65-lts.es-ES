---
title: Configuración del componente de vídeo
description: Aprenda a utilizar el componente Vídeo en Adobe Experience Manager para colocar un recurso de vídeo predefinido y listo para usar en su página.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Configuración del componente de vídeo {#configure-the-video-component}

El [componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) le permite colocar un recurso de vídeo predefinido y listo para usar en su página.

Para que se produzca la transcodificación adecuada, un administrador instala FFmpeg por separado. Consulte [Instalar FFmpeg y configurar AEM](#install-ffmpeg). Los administradores también [configuran perfiles de vídeo](#configure-video-profiles) para usarlos con elementos de HTML5.

>[!CAUTION]
>
>Este componente de base se ha desaprobado. Adobe recomienda usar el [componente incrustado de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) en su lugar.

>[!CAUTION]
>
>Ya no se espera que este componente funcione de forma predeterminada sin una amplia personalización en el nivel de proyecto.

## Configuración de perfiles de vídeo {#configure-video-profiles}

Para utilizar elementos de HTML5, defina perfiles de vídeo. Los elegidos aquí se utilizan por orden. Para acceder a, usa [Modo de diseño](/help/sites-authoring/default-components-designmode.md) (solo IU clásica) y selecciona la pestaña **[!UICONTROL Perfiles]**:

![chlimage_1-317](assets/chlimage_1-317.png)

Desde este cuadro de diálogo, también puede configurar el diseño del componente de vídeo y los parámetros de [!UICONTROL Reproducción], [!UICONTROL Flash] y [!UICONTROL Avanzado].

## Instalar FFmpeg y configurar AEM {#install-ffmpeg}

El componente de vídeo se basa en el producto de código abierto de terceros FFmpeg para transcodificar vídeos. Descargado de [https://ffmpeg.org/](https://ffmpeg.org/). Después de instalar FFmpeg, configure AEM para que utilice un códec de audio específico y opciones de tiempo de ejecución específicas.

Para instalar FFmpeg en **Windows**, siga estos pasos:

1. Descargue el binario compilado como `ffmpeg.zip`.
1. Desarchivar en una carpeta.
1. Establezca la variable de entorno del sistema `PATH` en &lt;*your-ffmpeg-location*>`\bin`.
1. Reinicie AEM.

Para instalar FFmpeg en **macOS X**, siga estos pasos:

1. Instale Xcode disponible en [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Instalar disponible en [XQuartz](https://www.xquartz.org) para obtener [X11](https://support.apple.com/en-us/100724).
1. Instale MacPorts disponibles en [www.macports.org](https://www.macports.org/).
1. En la consola, ejecute el comando `sudo port install ffmpeg` y siga las instrucciones que aparecen en la pantalla. Asegúrese de que la ruta de acceso del ejecutable `FFmpeg` se agrega a la variable del sistema `PATH`.

Para instalar FFmpeg en **macOS X 10.6**, usando la versión precompilada, siga estos pasos:

1. Descargue la versión precompilada.
1. Desarchivarlo en el directorio `/usr/local`.
1. En la consola, ejecute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Cambie la ruta según corresponda.

Para **configurar AEM**, siga estos pasos:

>[!NOTE]
>
>Estos pasos solo son necesarios si se requiere una mayor personalización de los códecs.

1. Abra [!UICONTROL CRXDE Lite] en su explorador web. Acceda a [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleccione el nodo `/libs/settings/dam/video/format_aac/jcr:content` y asegúrese de que las propiedades del nodo sean las siguientes:

   * `audioCodec` es `aac`.
   * `customArgs` es `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar la configuración, cree una superposición en el nodo `/apps/settings/` y mueva la misma estructura bajo el nodo `/conf/global/settings/`. No se puede editar en el nodo `/libs`. Por ejemplo, para superponer la ruta `/libs/settings/dam/video/fullhd-bp`, créela en `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Superponga y edite todo el nodo de perfil y no solo la propiedad que necesita modificación. Estos recursos no se resuelven mediante SlingResourceMerger.

4. Si cambió alguna de las propiedades, haga clic en **[!UICONTROL Guardar todo]**.

>[!NOTE]
>
>Los cambios en los modelos de flujo de trabajo predeterminados no se conservan al actualizar la instancia de AEM. Adobe recomienda copiar los modelos de flujo de trabajo modificados antes de editarlos. Por ejemplo, copie el modelo [!UICONTROL DAM Update Asset] incorporado antes de editar el paso de transcodificación FFmpeg en el modelo [!UICONTROL DAM Update Asset] para elegir los nombres de perfil de vídeo que existían antes de la actualización. A continuación, puede superponer el nodo `/apps` para permitir que AEM recupere los cambios personalizados del modelo predeterminado.
