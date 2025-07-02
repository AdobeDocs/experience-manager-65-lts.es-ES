---
title: Reescritura de XMP en representaciones
description: Descubra cómo la función de reescritura de XMP propaga los cambios de metadatos de un recurso a todas las representaciones del recurso o a algunas específicas.
role: User, Admin
feature: Metadata
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: e3972784-9ded-4da8-b90c-ec2da9c3297a
source-git-commit: 863ec2b6d8a6e22705c2f48a4f7bbb76fa34f7c7
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 6%

---

# Reescritura de XMP en representaciones {#xmp-writeback-to-renditions}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 LTS | Este artículo |

Esta característica de reescritura de XMP en [!DNL Adobe Experience Manager Assets] replica los cambios de metadatos en las representaciones del recurso original. Al cambiar los metadatos de un recurso desde Assets o al cargar el recurso, los cambios se almacenan inicialmente en el nodo de metadatos de la jerarquía de recursos.

La función de reescritura de XMP permite propagar los cambios de metadatos a todas las representaciones del recurso o a algunas específicas. La característica sólo devuelve las propiedades de metadatos que utilizan áreas de nombres registradas, es decir, se devuelve una propiedad denominada `dc:title` pero no una propiedad denominada `mytitle`.

Imagine un escenario en el que modifica la propiedad [!UICONTROL Title] del recurso con título `Classic Leather` a `Nylon`.

![metadatos](assets/metadata.png)

En este caso, [!DNL Experience Manager Assets] guarda los cambios realizados en la propiedad **[!UICONTROL Title]** en el parámetro `dc:title` para los metadatos de recursos almacenados en la jerarquía de recursos.

![metadata_stored](assets/metadata_stored.png)

Sin embargo, [!DNL Experience Manager Assets] no propaga automáticamente ningún cambio de metadatos a las representaciones de un recurso. Consulte [cómo habilitar la reescritura en XMP](#enable-xmp-writeback).

## Habilitar reescritura de XMP {#enable-xmp-writeback}

Para permitir que los cambios de metadatos se propaguen a las representaciones del recurso al cargarlo, modifique la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]** en el Administrador de configuración.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración de **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Seleccione la opción **[!UICONTROL Propagate XMP]** y, a continuación, guarde los cambios.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Habilitar la reescritura en XMP para representaciones específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que la función de reescritura de XMP propague los cambios de metadatos a ciertas representaciones, especifique estas representaciones en el paso del flujo de trabajo Proceso de reescritura de XMP de [!UICONTROL flujo de trabajo de reescritura de metadatos DAM]. De forma predeterminada, este paso se configura con la representación original.

Siga estos pasos para que la función de reescritura de XMP propague metadatos a las miniaturas de representación 140.100.png y 319.319.png.

1. En la interfaz de Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos, abra el modelo de flujo de trabajo **[!UICONTROL DAM Metadata Writeback]**.
1. En la página de **[!UICONTROL propiedades de escritura de metadatos DAM]**, abra el paso **[!UICONTROL Proceso de escritura XMP]**.
1. En el cuadro de diálogo [!UICONTROL Propiedades del paso], haga clic en la ficha **[!UICONTROL Proceso]**.
1. En el cuadro **Argumentos**, agregue `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` y haga clic en **[!UICONTROL Aceptar]**.

   ![step_properties](assets/step_properties.png)

1. Guarde los cambios.
1. Para regenerar las representaciones piramidales de TIFF de [!DNL Dynamic Media] imágenes con los nuevos atributos, agregue el paso **[!UICONTROL Dynamic Media Process Image Assets]** al flujo de trabajo [!UICONTROL DAM Metadata Writeback].

   Las representaciones PTIFF solo se crean y almacenan localmente en una implementación híbrida de Dynamic Media.

1. Guarde el flujo de trabajo.

Los cambios de metadatos se propagan a las representaciones representaciones thumbnail.140.100.png y thumbnail.319.319.png del recurso, y no a las demás.

>[!NOTE]
>
>Para las plataformas admitidas, consulte [Requisitos previos para la reescritura de metadatos de XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrado de metadatos de XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] admite el filtrado de lista de bloqueados y lista de permitidos de propiedades/nodos para metadatos de XMP que se leen desde binarios de recursos y se almacenan en JCR cuando se incorporan recursos.

El filtrado mediante una lista de bloqueados permite importar todas las propiedades de metadatos de XMP excepto las propiedades especificadas para la exclusión. Sin embargo, para tipos de recursos como archivos INDD que tienen grandes cantidades de metadatos de XMP (por ejemplo, 1000 nodos con 10 000 propiedades), los nombres de nodos que se van a filtrar no siempre se conocen de antemano. Si el filtrado mediante una lista de bloqueados permite importar un gran número de recursos con numerosos metadatos de XMP, la implementación de [!DNL Experience Manager] puede encontrar problemas de estabilidad, por ejemplo, colas de observación obstruidas.

El filtrado de metadatos de XMP mediante lista de permitidos resuelve este problema al permitirle definir las propiedades de XMP que desea importar. De este modo, se ignoran todas las demás propiedades de XMP o desconocidas. Para la compatibilidad con versiones anteriores, puede agregar algunas de estas propiedades al filtro que utiliza una lista de bloqueados.

>[!NOTE]
>
>El filtrado solo funciona para las propiedades derivadas de fuentes de XMP en binarios de recursos. Para las propiedades derivadas de orígenes que no son de XMP, como los formatos EXIF y IPTC, el filtrado no funciona. Por ejemplo, la fecha de creación del recurso se almacena en la propiedad denominada `CreateDate` en EXIF TIFF. Experience Manager almacena este valor en un campo de metadatos denominado `exif:DateTimeOriginal`. Como el origen no es de XMP, el filtrado no funciona en esta propiedad.

1. Para abrir el Administrador de configuración, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar el filtrado mediante una lista de permitidos, seleccione **[!UICONTROL Aplicar Lista de permitidos a las propiedades de XMP]** y especifique las propiedades que desea importar en el cuadro **[!UICONTROL Nombres XML permitidos para el filtrado de XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar las propiedades de XMP bloqueadas después de aplicar el filtrado mediante lista de permitidos, especifique las que aparecen en el cuadro **[!UICONTROL Nombres XML bloqueados para el filtrado de XMP]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Aplicar Lista de bloqueados a las propiedades de XMP]** está seleccionada de forma predeterminada. En otras palabras, el filtrado con una lista de bloqueados está habilitado de forma predeterminada. Para deshabilitar dicho filtrado, cancele la selección de la opción **[!UICONTROL Aplicar Lista de bloqueados a las propiedades de XMP]**.

1. Guarde los cambios.
