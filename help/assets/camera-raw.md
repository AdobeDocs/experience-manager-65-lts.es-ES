---
title: Compatibilidad con [!DNL Adobe Camera Raw] para procesar recursos digitales
description: Aprenda a habilitar la compatibilidad con  [!DNL Adobe Camera Raw] en [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Procesar imágenes con [!DNL Adobe Camera Raw] {#camera-raw-support}

Puede habilitar la compatibilidad con [!DNL Adobe Camera Raw] para procesar formatos de archivo sin procesar, como CR2, NEF y RAF, y procesar las imágenes en formato JPEG. La funcionalidad es compatible con [!DNL Adobe Experience Manager Assets] mediante el [paquete de Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponible en Distribución de software.

>[!NOTE]
>
>La funcionalidad solo admite representaciones de JPEG. Es compatible con Windows de 64 bits, Mac OS y RHEL 7.x.

Para habilitar la compatibilidad con [!DNL Camera Raw] en [!DNL Experience Manager Assets], siga estos pasos:

1. Descargar el [[!DNL Camera Raw] paquete](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) de [!DNL Software Distribution].
1. Acceso `https://[aem_server]:[port]/workflow`. Abra el flujo de trabajo **[!UICONTROL Recurso de actualización DAM]**.
1. Edite el paso **[!UICONTROL Procesar miniaturas]**.
1. Proporcione la siguiente configuración en la ficha **[!UICONTROL Miniaturas]**:

   * **[!UICONTROL Miniaturas]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Tipos MIME omitidos]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. En la ficha **[!UICONTROL Imagen Web habilitada]**, en el campo **[!UICONTROL Omitir lista]**, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. En el panel lateral, agregue el paso **[!UICONTROL Controlador Camera Raw/DNG]** debajo del paso **[!UICONTROL Procesar miniaturas]**.
1. En el paso **[!UICONTROL Controlador Camera Raw/DNG]**, agregue la siguiente configuración en la pestaña **[!UICONTROL Argumentos]**:

   * **[!UICONTROL Tipos MIME]**: `image/dng` y `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Asegúrese de que la configuración anterior sea la misma que la configuración del **[!UICONTROL Recurso de actualización DAM de muestra con Camera Raw y el paso de administración DNG]**.

Ahora puede importar archivos RAW de cámara en Assets. Después de instalar el paquete de Camera Raw y configurar el flujo de trabajo necesario, la opción **[!UICONTROL Ajuste de imagen]** aparece en la lista de paneles laterales.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opciones en el panel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Imagen: use la opción para realizar ediciones ligeras en las imágenes.*

Después de guardar las ediciones en una imagen [!DNL Camera Raw], se genera una nueva representación `AdjustedPreview.jpg` para la imagen. Para otros tipos de imagen excepto [!DNL Camera Raw], los cambios se reflejan en todas las representaciones.

## Prácticas recomendadas, problemas conocidos y limitaciones {#best-practices}

La funcionalidad tiene las siguientes limitaciones:

* La funcionalidad solo admite representaciones de JPEG. Es compatible con Windows de 64 bits, Mac OS y RHEL 7.x.
* La reescritura de metadatos no es compatible con los formatos RAW y DNG.
* La biblioteca [!DNL Camera Raw] tiene limitaciones en torno al total de píxeles que puede procesar a la vez. Actualmente, puede procesar un máximo de 65000 píxeles en el lado largo de un archivo o 512 MP, según los criterios que se encuentren primero.
