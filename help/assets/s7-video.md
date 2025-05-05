---
title: Vídeo
description: Obtenga información acerca de la administración centralizada de recursos de vídeo en Adobe Experience Manager Assets, donde puede cargar vídeos para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Experience Manager Assets. La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
role: User, Admin
mini-toc-levels: 3
feature: Video
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---

# Vídeo {#video}

Adobe Experience Manager Assets permite la administración centralizada de recursos de vídeo, donde puede cargar vídeos directamente en Assets para su codificación automática en Dynamic Media Classic y acceder a vídeos de Dynamic Media Classic directamente desde Assets para la creación de páginas.

La integración de vídeo de Dynamic Media Classic amplía el alcance del vídeo optimizado a todas las pantallas (detección automática de dispositivos y ancho de banda).

* El componente **[!UICONTROL Scene7 Video]** detecta automáticamente el dispositivo y el ancho de banda para reproducir el formato correcto y la calidad de vídeo correcta en equipos de escritorio, tabletas y dispositivos móviles.
* Assets: puede incluir conjuntos de vídeos adaptables en lugar de recursos de vídeo únicos. Un conjunto de vídeos adaptable contiene todas las representaciones de vídeo necesarias para reproducir vídeo sin problemas en varias pantallas. Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo que se codifican a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. Puede utilizar un conjunto de vídeos adaptable, junto con el componente de vídeo S7, para la transmisión de vídeo adaptable en varias pantallas, incluidos equipos de escritorio, iOS, Android™, BlackBerry® y dispositivos móviles Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Acerca de FFMPEG y Dynamic Media Classic {#about-ffmpeg-and-scene}

El proceso de codificación de vídeo predeterminado se basa en el uso de la integración basada en FFMPEG con perfiles de vídeo. Por lo tanto, el flujo de trabajo de ingesta de DAM predeterminado contiene los dos pasos siguientes del flujo de trabajo basado en ffmpeg:

* Miniaturas FFMPEG
* Codificación FFMPEG

Al habilitar y configurar la integración de Dynamic Media Classic, no se eliminan ni desactivan automáticamente estos dos pasos del flujo de trabajo de ingesta de DAM predeterminado. Si ya utiliza la codificación de vídeo basada en FFMPEG en Adobe Experience Manager, es probable que tenga FFMPEG instalado en los entornos de creación. En este caso, un nuevo vídeo introducido mediante DAM se codificaría dos veces: una desde el codificador FFMPEG y otra desde la integración de Dynamic Media Classic.

Si tiene configurada la codificación de vídeo basada en FFMPEG en Experience Manager y FFMPEG instalado, Adobe recomienda eliminar los dos flujos de trabajo FFMPEG de los flujos de trabajo de ingesta de DAM.

## Formatos admitidos {#supported-formats}

El componente de vídeo de Scene7 admite los siguientes formatos:

* F4V H.264
* MP4 H.264

## Decida dónde cargar el vídeo {#deciding-where-to-upload-your-video}

La decisión sobre dónde cargar los recursos de vídeo depende de lo siguiente:

* ¿Necesita un flujo de trabajo para el recurso de vídeo?
* ¿Necesita control de versión para el recurso de vídeo?

Si la respuesta a alguna de estas preguntas es &quot;sí&quot;, cargue el vídeo directamente en Adobe DAM. Si la respuesta a ambas preguntas es &quot;no&quot;, cargue el vídeo directamente en Dynamic Media Classic. El flujo de trabajo para cada escenario se describe en la siguiente sección.

### Si está cargando el vídeo directamente en Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Si necesita un flujo de trabajo o control de versiones para sus recursos, cárguelos primero en Adobe DAM. El flujo de trabajo recomendado es el siguiente:

1. Cargue el recurso de vídeo en Adobe DAM y codifique y publique automáticamente en Dynamic Media Classic.
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la pestaña **[!UICONTROL Películas]** del Buscador de contenido.
1. Autor con **[!UICONTROL Vídeo de Scene7]** o componente **[!UICONTROL Vídeo base]**.

### Si carga el vídeo en Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si no necesita un flujo de trabajo o control de versiones para sus recursos, cárguelos en Scene7. El flujo de trabajo recomendado es el siguiente:

1. En Dynamic Media Classic, [configure una carga y codificación de FTP programada en Scene7 (automatizado por el sistema)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=es#upload-files-using-via-ftp).
1. En Experience Manager, acceda a los recursos de vídeo en WCM en la pestaña **[!UICONTROL Scene7]** del Buscador de contenido.
1. Autor con el componente **[!UICONTROL Scene7 Video]**.

## Configuración de la integración con vídeo de Scene7 {#configuring-integration-with-scene-video}

1. En **[!UICONTROL Cloud Services]**, vaya a la configuración de **[!UICONTROL Scene7]** y seleccione **[!UICONTROL Editar]**.
1. Seleccione la ficha **[!UICONTROL Vídeo]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >La pestaña **[!UICONTROL Video]** no aparece si la página no tiene una configuración de nube.

1. Seleccione el perfil de codificación de vídeo adaptable, un perfil de codificación de vídeo único predeterminado o un perfil de codificación de vídeo personalizado.

   >[!NOTE]
   >
   >Para obtener más información sobre el significado de los ajustes preestablecidos de vídeo, consulte la [documentación de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=es#video-presets-for-encoding-video-files).
   >
   >Adobe recomienda seleccionar ambos conjuntos de vídeos adaptables al configurar los ajustes preestablecidos universales o seleccionar la opción **[!UICONTROL Codificación de vídeo adaptable]**.

1. Los perfiles de codificación seleccionados se aplican automáticamente a todos los vídeos cargados en la carpeta de destino CQ DAM que haya configurado para esta configuración de nube de Scene7. Puede configurar varias configuraciones de nube de Scene7 con diferentes carpetas de destino para aplicar diferentes perfiles de codificación según sea necesario.

## Actualizar los ajustes preestablecidos del visor y de codificación {#updating-viewer-and-encoding-presets}

Para actualizar el visor y los ajustes preestablecidos de codificación de vídeo porque se han actualizado en Scene7, vaya a la configuración de Scene7 en la configuración de nube y seleccione **[!UICONTROL Actualizar el visor y los ajustes preestablecidos de codificación]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Cargue el vídeo de origen principal a Scene7 desde Adobe DAM {#uploading-your-master-video}

1. Vaya a la carpeta de destino de CQ DAM en la que ha configurado la configuración de nube con perfiles de codificación de Scene7.
1. Seleccione **[!UICONTROL Cargar]** para cargar el vídeo de origen principal. La carga y la codificación de vídeo se han completado una vez completado el flujo de trabajo de [!UICONTROL DAM Update Asset] y **[!UICONTROL Publish to Scene7]** tiene una marca de verificación.

   >[!NOTE]
   >
   >Las miniaturas de vídeo tardan un tiempo en generarse.

   Al arrastrar el vídeo de origen principal DAM al componente de vídeo, se accede a *todas* las representaciones de proxy codificadas en Scene7 para la entrega.

## Componente de vídeo base frente al componente de vídeo de Scene7 {#foundation-video-component-versus-scene-video-component}

Al utilizar Experience Manager, puede acceder al componente de vídeo disponible en Sites y al componente de vídeo de Scene7. Estos componentes no son intercambiables.

El componente de vídeo de Scene7 solo funciona para vídeos de Scene7. El componente de base funciona con vídeos almacenados desde Experience Manager (mediante ffmpeg) y vídeos de Scene7.

La siguiente matriz explica cuándo utilizar qué componente:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo S7 utiliza el perfil de vídeo universal. Sin embargo, puede obtener el reproductor de vídeo basado en HTML5 para Experience Manager. En Scene7, copie el código incrustado del reproductor de vídeo HTML5 incorporado y colóquelo en la página de Experience Manager.

## Componente de vídeo de Experience Manager {#aem-video-component}

Incluso si se recomienda utilizar el componente de vídeo de Scene7 para ver vídeos de Scene7, en esta sección se describe el uso de vídeos de Scene7 con el componente de vídeo de base en Experience Manager, en aras de la exhaustividad.

### Comparación de vídeo de Experience Manager y vídeo de Scene7 {#aem-video-and-scene-video-comparison}

La siguiente tabla proporciona una comparación de alto nivel de las funciones compatibles entre el componente de vídeo de Experience Manager Foundation y el componente de vídeo de Scene7:

|   | Vídeo de Experience Manager Foundation | Vídeo de Scene7 |
|---|---|---|
| Enfoque | Primer enfoque de HTML5. Flash solo se utiliza para la reserva que no sea de HTML5. | Flash en la mayoría de los escritorios. HTML5 se utiliza para móviles y tabletas. |
| Entrega | Progresivo | Flujo adaptable |
| Seguimiento | Sí | Sí |
| Extensibilidad | Sí | No |
| Vídeo móvil | Sí | Sí |

### Configuración de {#setting-up}

#### Creación de perfiles de vídeo {#creating-video-profiles}

Las distintas codificaciones de vídeo se crean según los ajustes preestablecidos de codificación de S7 seleccionados en la configuración de nube de S7. Para que el componente de vídeo de base los utilice, se debe crear un perfil de vídeo para cada ajuste preestablecido de codificación S7 seleccionado. Este método permite al componente de vídeo seleccionar las representaciones DAM según corresponda.

>[!NOTE]
>
>Para poder publicar, deben activarse nuevos perfiles de vídeo y cambios en los mismos.

1. En Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Consola de configuración]**.
1. En la **[!UICONTROL consola de configuración]**, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL DAM]** > **[!UICONTROL Perfiles de vídeo]** en el árbol de navegación.
1. Cree un perfil de vídeo de S7. En **[!UICONTROL Nuevo]**. , seleccione **[!UICONTROL Crear página]** y luego seleccione la plantilla Perfil de vídeo de Scene7. Asigne un nombre a la nueva página de perfil de vídeo y seleccione **[!UICONTROL Crear]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Edite el nuevo perfil de vídeo. Seleccione primero la configuración de nube. A continuación, seleccione el mismo ajuste preestablecido de codificación que se seleccionó en la configuración de la nube.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propiedad | Descripción |
   |---|---|
   | Configuración de nube de Scene7 | La configuración de nube que se utilizará para los ajustes preestablecidos de codificación. |
   | Ajuste preestablecido de codificación de Scene7 | Ajuste preestablecido de codificación con el que se asignará este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Esta propiedad permite establecer el valor de la propiedad type del elemento de origen de vídeo HTML5. Esta información no la proporcionan los ajustes preestablecidos de codificación de S7, pero es necesaria para procesar correctamente los vídeos con el elemento de vídeo HTML5. Se proporciona una lista de formatos comunes, pero se puede sobrescribir para otros formatos. |

   Repita este paso para todos los ajustes preestablecidos de codificación seleccionados en la configuración de nube que desee utilizar en el componente de vídeo.

#### Configuración del diseño {#configuring-design}

El componente **[!UICONTROL Foundation Video]** debe saber qué perfiles de vídeo utilizar para generar la lista de fuentes de vídeo. Abra el cuadro de diálogo de diseño de componentes de vídeo y configure el diseño de componentes para con los nuevos perfiles de vídeo.

>[!NOTE]
>
>Si usa el componente **[!UICONTROL Vídeo base]** en una página móvil, repita estos pasos en el diseño de la página móvil.

>[!NOTE]
>
>Los cambios realizados en el diseño requieren que su activación surta efecto en la publicación.

1. Abra el cuadro de diálogo de diseño del componente **[!UICONTROL Foundation Video]** y cambie a la ficha **[!UICONTROL Perfiles]**. A continuación, elimine los perfiles predeterminados y añada los nuevos perfiles de vídeo de S7. El orden de la lista de perfiles en el cuadro de diálogo de diseño define el orden del elemento de orígenes de vídeo al procesarse.
1. En los exploradores que no admiten HTML5, el componente de vídeo permite configurar una reserva de Flash. Abra el cuadro de diálogo de diseño de componentes de vídeo y cambie a la ficha **[!UICONTROL Flash]**. Configure los ajustes del reproductor Flash y asigne un perfil de reserva para el reproductor Flash.

#### Lista de comprobación {#checklist}

1. Cree una configuración de nube de S7. Asegúrese de que los ajustes preestablecidos de codificación de vídeo estén configurados y de que el importador esté en ejecución.
1. Cree un perfil de vídeo S7 para cada ajuste preestablecido de codificación de vídeo seleccionado en la configuración de la nube.
1. Los perfiles de vídeo deben activarse.
1. Configure el diseño del componente **[!UICONTROL Vídeo de base]** en su página.
1. Active el diseño una vez que haya terminado con los cambios de diseño.
