---
title: Prácticas recomendadas para traducir recursos
description: Prácticas recomendadas para una administración eficaz de los recursos a fin de sincronizar varias versiones traducidas y optimizar los flujos de trabajo de traducción.
contentOwner: AG
role: Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Prácticas recomendadas para traducir recursos {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] admite flujos de trabajo multilingües para traducir binarios, metadatos y etiquetas para recursos digitales a varias configuraciones regionales y administrar los recursos traducidos. Para obtener más información, consulte [Assets multilingüe](multilingual-assets.md).

Para administrar los recursos de manera eficiente a fin de garantizar que las distintas versiones traducidas permanezcan sincronizadas, cree [copias de idioma](preparing-assets-for-translation.md) de los recursos antes de ejecutar los flujos de trabajo de traducción.

Una copia de idioma de un recurso o un grupo de recursos es un elemento del mismo nivel de idioma (o una versión de los recursos en un idioma asociado) con una jerarquía de contenido similar.

Cada copia de idioma es un recurso independiente. Por lo tanto, traducir recursos a varias configuraciones regionales puede aumentar drásticamente el tamaño del repositorio de CRX. Por ejemplo, la traducción de recursos con un tamaño combinado de 10 GB a dos idiomas puede aumentar el tamaño del repositorio en aproximadamente 20 GB (10 GB para cada idioma).

Los binarios de recursos ocupan un espacio de almacenamiento mucho mayor en comparación con los metadatos y las etiquetas. Por lo tanto, si la traducción de metadatos y etiquetas solo sirve para su propósito, omita traducir los binarios. Puede conservar la copia original de los binarios en el repositorio para asociarla con metadatos y etiquetas traducidos a distintas configuraciones regionales. Mantener una sola copia de binarios, en lugar de varias versiones traducidas, minimiza el impacto en el tamaño del repositorio.

El almacén de datos de archivos y el almacén de datos de Amazon S3 proporcionan una infraestructura de almacenamiento que se adapta mejor a estos escenarios. Estos repositorios de almacenamiento almacenan una sola copia de los binarios de recursos (incluidas las representaciones) que los metadatos y las etiquetas pueden compartir en varias configuraciones regionales. Por lo tanto, la creación de copias de idioma de recursos y la traducción de metadatos y etiquetas no afectan al tamaño del repositorio.

También puede realizar algunos cambios de configuración en un par de flujos de trabajo y en el marco de trabajo de integración de traducciones para optimizar aún más el proceso.

1. Realice una de las siguientes acciones:

   * [Configurar el almacén de datos de archivos](/help/sites-deploying/data-store-config.md)
   * [Configuración del almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Habilite el flujo de trabajo [!UICONTROL Establecer fecha de última modificación].

   El flujo de trabajo [!UICONTROL DAM MetaData Writeback] configura la última fecha de modificación de un recurso. Debido a que deshabilita este flujo de trabajo en el paso 2, [!DNL Assets] ya no puede mantener actualizada la última fecha de modificación de los recursos. Por lo tanto, habilite el flujo de trabajo *Establecer fecha de última modificación* para asegurarse de que las fechas de última modificación de los recursos estén actualizadas. Assets con fechas de última modificación obsoletas puede causar errores.

1. [Configure el marco de trabajo de integración de traducciones](/help/sites-administering/tc-tic.md) para detener la traducción de binarios de recursos. Anule la selección de la opción **[!UICONTROL Traducir Assets]** en la ficha [!UICONTROL Assets] para detener la traducción de los binarios de recursos.
1. Traducir metadatos/etiquetas de recursos usando [Flujos de trabajo de recursos multilingües](multilingual-assets.md).
