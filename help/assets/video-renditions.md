---
title: Representaciones de vídeo
description: Aprenda a utilizar Adobe Experience Manager Assets para generar representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
solution: Experience Manager, Experience Manager Assets
feature: Video
role: User
exl-id: da33f43b-7375-46f1-a80f-c1891fd90312
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: cb04d42d-1b70-43b0-9951-45998eb6e842
    internal-label: Video
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%
---
# Representaciones de vídeo {#video-renditions}

Adobe Experience Manager Assets genera representaciones de vídeo para recursos de vídeo de varios formatos, incluidos OGG, FLV, etc.

Experience Manager Assets admite representaciones estáticas y dinámicas (representaciones codificadas en DM) para recursos de medios.

Las representaciones estáticas se generan de forma nativa mediante FFMPEG (instalado y disponible en la ruta del sistema) y se almacenan en el repositorio de contenido.

Las representaciones codificadas en DM se almacenan en el servidor proxy y se proporcionan durante la ejecución.

Experience Manager Assets proporciona compatibilidad de reproducción para estas representaciones en el lado del cliente.

Para ver las representaciones de un recurso de vídeo concreto, abra su página de recursos y seleccione el icono Navegación global. A continuación, elija **[!UICONTROL Representaciones]** en la lista.

![chlimage_1-478](assets/chlimage_1-478.png)

La lista de representaciones de vídeo se muestra en el panel **[!UICONTROL Representaciones]**.

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar el servidor proxy para representaciones con codificación DM, [configure los servicios de nube de Dynamic Media](config-dynamic.md).

Para generar representaciones de vídeo con los parámetros deseados, [cree un perfil de vídeo correspondiente](video-profiles.md).

Después de configurar el servidor proxy y crear perfiles de vídeo, puede incluir este ajuste preestablecido de vídeo en un perfil de procesamiento y aplicar el perfil de procesamiento a una carpeta.

>[!NOTE]
>
>La reproducción de audio no funciona para archivos OGG y WAV en Microsoft® Internet Explorer 11. Se muestra un error `Invalid Source` en la página de detalles del recurso para los recursos con la extensión OGG o WAV.
>
>En MS® Edge y iPad, los archivos OGG no se reproducen y generan un error de formato no admitido.
