---
title: Vídeo en la creación de Sites Classic
description: Assets permite la administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para su codificación automática en Dynamic Media Classic, y acceder a los vídeos de día directamente desde Assets para la creación de páginas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 1%

---

# Vídeo{#video}

Assets proporciona una administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Assets para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección automática de dispositivos y ancho de banda).

* El componente de vídeo de Dynamic Media Classic detecta automáticamente el dispositivo y el ancho de banda para reproducir el formato y el vídeo de calidad adecuados en equipos de escritorio, tabletas y dispositivos móviles.
* Assets: puede incluir conjuntos de vídeos adaptables en lugar de recursos de vídeo únicos. Un conjunto de vídeos adaptable es un contenedor para todas las representaciones de vídeo que son necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo que se codifican a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Puede utilizar un conjunto de vídeos adaptable, junto con el componente de vídeo S7, para la transmisión de vídeo adaptable en varias pantallas, incluidos equipos de escritorio, iOS, Android™, BlackBerry® y dispositivos móviles Windows. Consulte [Documentación de Dynamic Media Classic sobre conjuntos de vídeos adaptables para obtener más información](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con perfiles de vídeo. Por lo tanto, el flujo de trabajo predeterminado [!UICONTROL DAM Update Asset] contiene los dos pasos siguientes del flujo de trabajo basado en ffmpeg:

* Miniaturas FFMPEG
* Codificación FFMPEG

Al habilitar y configurar la integración de Dynamic Media Classic, no se eliminan ni desactivan automáticamente estos dos pasos del flujo de trabajo de ingesta de [!UICONTROL DAM Update Asset], que está listo para usarse. Si ya utiliza la codificación de vídeo basada en FFMPEG en Adobe Experience Manager, es probable que tenga FFMPEG instalado en los entornos de creación. En este caso, un nuevo vídeo introducido mediante Experience Manager Assets se codifica dos veces: una desde el codificador FFMPEG y otra desde la integración de Dynamic Media Classic.

Si tiene configurada la codificación de vídeo basada en FFMPEG en Experience Manager y FFMPEG instalado, Adobe recomienda quitar los dos flujos de trabajo FFMPEG de los flujos de trabajo de [!UICONTROL DAM Update Asset].

### Formatos compatibles {#supported-formats}

Los siguientes formatos son compatibles con el componente de vídeo de Dynamic Media Classic:

* F4V H.264
* MP4 H.264

### Decida dónde cargar el vídeo {#deciding-where-to-upload-your-video}

La decisión sobre dónde cargar los recursos de vídeo depende de lo siguiente:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita control de versión para el recurso de vídeo?

Si la respuesta a alguna de estas preguntas es &quot;sí&quot;, cargue el vídeo directamente en Adobe DAM. Si la respuesta a ambas preguntas es &quot;no&quot;, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo para cada escenario se describe en la siguiente sección.

#### Si está cargando el vídeo directamente en Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Si necesita un flujo de trabajo o un control de versiones para sus recursos, primero debe cargarlos en Adobe Assets. El flujo de trabajo recomendado es el siguiente:

1. Cargue el recurso de vídeo en Adobe Assets y codifique y publique automáticamente en Dynamic Media Classic.
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la pestaña **[!UICONTROL Películas]** del Buscador de contenido.
1. Crear con un vídeo de Dynamic Media Classic o un componente de vídeo de base.

#### Si carga el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o control de versiones para sus recursos, debe cargarlos en Dynamic Media Classic. El flujo de trabajo recomendado es el siguiente:

1. En la aplicación de escritorio de Dynamic Media Classic, [configure una carga y codificación de FTP programadas en Dynamic Media Classic (sistema automatizado)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=es#upload-options).
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la pestaña **[!UICONTROL Dynamic Media Classic]** del Buscador de contenido.
1. Cree con el componente de vídeo de Dynamic Media Classic.

### Configuración de la integración con Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. En **[!UICONTROL Cloud Services]**, vaya a la configuración de **[!UICONTROL Dynamic Media Classic]** y seleccione **[!UICONTROL Editar]**.
1. Seleccione la ficha **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >La pestaña **[!UICONTROL Video]** no aparece si la página no tiene una configuración de nube. Consulte [Habilitar Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único predeterminado o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >Para obtener más información sobre el significado de los ajustes preestablecidos de vídeo, consulte [Ajustes preestablecidos de vídeo para codificar archivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe recomienda seleccionar ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o seleccionar la opción **[!UICONTROL Codificación de vídeo adaptable]**.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino CQ DAM configurada para esta configuración de nube de Dynamic Media Classic. Puede configurar varias configuraciones de nube de Dynamic Media Classic con diferentes carpetas de destino para aplicar diferentes perfiles de codificación según sea necesario.

### Actualización del visualizador y los ajustes preestablecidos de codificación {#updating-viewer-and-encoding-presets}

Actualice el visor y los ajustes preestablecidos de codificación para vídeo en Experience Manager si los ajustes preestablecidos se actualizaron en Dynamic Media Classic. En ese caso, vaya a la configuración de Dynamic Media Classic en la configuración de la nube y seleccione **Actualizar el visor y los ajustes preestablecidos de codificación**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Cargar el vídeo de origen principal {#uploading-your-master-video}

Para cargar el vídeo de origen principal en Dynamic Media Classic desde Adobe DAM:

1. Vaya a la carpeta de destino de CQ DAM donde ha configurado la configuración de nube con perfiles de codificación de Dynamic Media Classic.
1. Seleccione **[!UICONTROL Cargar]** para cargar el vídeo de origen principal. La carga y la codificación de vídeo se han completado una vez completado el flujo de trabajo de [!UICONTROL DAM Update Asset] y **[!UICONTROL Publish to Dynamic Media Classic]** tiene una marca de verificación.

   >[!NOTE]
   >
   >Las miniaturas de vídeo pueden tardar un poco en generarse.

   Al arrastrar el vídeo de origen principal DAM al componente de vídeo, se obtiene acceso a *todas* las representaciones de proxy codificadas en Dynamic Media Classic para su envío.

### Componente de vídeo base frente al componente de vídeo Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Al utilizar Experience Manager, puede acceder al componente de vídeo disponible en Sites y al componente de vídeo de Dynamic Media Classic. Estos componentes no son intercambiables.

El componente de vídeo de Dynamic Media Classic solo funciona para vídeos de Dynamic Media Classic. El componente de base funciona con vídeos almacenados desde Experience Manager (mediante ffmpeg) y vídeos de Dynamic Media Classic.

La siguiente matriz explica cuándo debe utilizar qué componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media Classic utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para su uso en Experience Manager. En Dynamic Media Classic, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en la página de Experience Manager.
>

## Componente de vídeo de Experience Manager {#aem-video-component}

Aunque se recomiende el uso del componente de vídeo de Dynamic Media Classic para ver vídeos de Dynamic Media Classic, en esta sección se describe el uso de vídeos de Dynamic Media Classic con el [!UICONTROL componente de vídeo Foundation] en Experience Manager para completar el proceso.

### Comparación de vídeo Experience Manager y vídeo Dynamic Media Classic {#aem-video-and-scene-video-comparison}

La siguiente tabla proporciona una comparación de alto nivel de las funciones compatibles entre el componente de vídeo de Experience Manager Foundation y el componente de vídeo de Dynamic Media Classic:

|   | Vídeo de Experience Manager Foundation | Dynamic Media Classic Video |
|---|---|---|
| Enfoque | Primer enfoque de HTML5. Flash solo se utiliza para la reserva que no sea de HTML5. | Flash en la mayoría de los escritorios. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Flujo adaptable |
| Seguimiento | Sí | Sí |
| Extensibilidad | Sí | No |
| Vídeo móvil | Sí | Sí |

### Configurar {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean según los ajustes preestablecidos de codificación de Dynamic Media Classic seleccionados en la Configuración en la nube de Dynamic Media Classic. Para que el componente de vídeo base los utilice, debe crear un perfil de vídeo para cada ajuste preestablecido de codificación de Dynamic Media Classic seleccionado. Permite al componente de vídeo seleccionar las representaciones DAM según corresponda.

>[!NOTE]
>
>Para poder publicar, deben activarse nuevos perfiles de vídeo y cambios en los mismos.

1. En Experience Manager, ve a **[!UICONTROL Herramientas]** y luego selecciona **[!UICONTROL Consola de configuración]**.
1. En la consola de configuración, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de vídeo]** en el árbol de navegación.
1. Cree un perfil de vídeo de Dynamic Media Classic. En el menú **[!UICONTROL Nuevo]**, seleccione **[!UICONTROL Crear página]**.
1. Seleccione la plantilla de perfil Dynamic Media Classic Video. Asigne un nombre a la nueva página de perfil de vídeo y seleccione **[!UICONTROL Crear]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que se seleccionó en la configuración de la nube.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Dynamic Media Classic | La configuración de nube que se utilizará para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación Dynamic Media Classic | Ajuste preestablecido de codificación con el que se asignará este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML5. Esta información no se proporciona mediante los ajustes preestablecidos de codificación de Dynamic Media Classic, pero es necesaria para procesar correctamente los vídeos mediante el elemento de vídeo HTML5. Se proporciona una lista de formatos comunes, pero se puede sobrescribir para otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desee utilizar en el componente de vídeo.

#### Configurar diseño {#configuring-design}

El componente de vídeo de base debe saber qué perfiles de vídeo utilizar para crear la lista de fuentes de vídeo. Abra el cuadro de diálogo de diseño de componentes de vídeo y configure el diseño de componentes para con los nuevos perfiles de vídeo.

>[!NOTE]
>
>Si utiliza el componente de vídeo base en una página móvil, repita estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren que su activación surta efecto en la publicación.

1. Abra el cuadro de diálogo de diseño del componente de vídeo de base y cambie a la pestaña **[!UICONTROL Perfiles]**. A continuación, elimine los perfiles predeterminados y agregue los nuevos perfiles de vídeo de Dynamic Media Classic. El orden de la lista de perfiles en el cuadro de diálogo de diseño también define el orden del elemento de fuentes de vídeo al procesar.
1. En los exploradores que no admiten HTML5, el componente Vídeo permite configurar una reserva de flash. Abra el cuadro de diálogo de diseño de componentes de vídeo y cambie a la ficha **[!UICONTROL Flash]**. Configure los ajustes de Flash Player y asigne un perfil de reserva para Flash Player.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de Dynamic Media Classic. Asegúrese de que los ajustes preestablecidos de codificación de vídeo estén configurados y de que el importador esté en ejecución.
1. Cree un perfil de vídeo de Dynamic Media Classic para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de la nube.
1. Los perfiles de vídeo deben activarse.
1. Configure el diseño del componente de vídeo de base en la página.
1. Active el diseño una vez que haya terminado con los cambios de diseño.
