---
title: Agregar una marca de agua a los recursos digitales
description: Aprenda a utilizar la función de marca de agua para agregar una marca de agua digital a los recursos.
contentOwner: AG
role: User, Admin
feature: Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Marca de agua de recursos digitales {#watermarking}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=es) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] le permite agregar una marca de agua digital a los recursos que ayuda a los usuarios a verificar la autenticidad y la propiedad de los derechos de autor de los recursos. [!DNL Experience Manager Assets] admite que el texto se utilice como marca de agua en archivos PNG y JPEG.

Para poder aplicar marcas de agua en los recursos, agregue el paso de marca de agua en el flujo de trabajo [!UICONTROL Recurso de actualización DAM].

1. Acceda a la interfaz de usuario [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Recurso de actualización DAM]** y haga clic en **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el paso **[!UICONTROL Agregar filigrana]** al flujo de trabajo [!UICONTROL Recurso de actualización DAM].

   ![Arrastre el paso [!UICONTROL Agregar filigrana] y agréguela al flujo de trabajo [!UICONTROL Recurso de actualización DAM]](assets/add_watermark_step_aem_assets.png)

   *Imagen: arrastre el paso [!UICONTROL Agregar filigrana] y agréguela al flujo de trabajo [!UICONTROL Recurso de actualización DAM].*

   >[!NOTE]
   >
   >Coloque el paso [!UICONTROL Agregar filigrana] en cualquier lugar antes del paso [!UICONTROL Procesar miniatura].

1. Abra el paso **[!UICONTROL Agregar filigrana]** para mostrar sus propiedades.
1. En la ficha **[!UICONTROL Argumentos]**, especifique valores válidos en los distintos campos, incluidos texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, haga clic en **[!UICONTROL Listo]**.

   ![Proporcione los argumentos en el paso Agregar marca de agua en [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Proporcione los argumentos en el paso Agregar marca de agua en [!DNL Assets].*

1. Guarde el flujo de trabajo **[!UICONTROL DAM Update Asset]** con el paso de marca de agua.
1. Desde la interfaz de usuario [!DNL Assets], cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición configurada en los pasos anteriores.

Para aplicar una marca de agua a los documentos de PDF mediante programación o con información dinámica, considere la posibilidad de utilizar la oferta [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Sugerencias y limitaciones {#tips-limitations}

* Solo se admiten marcas de agua basadas en texto. Las imágenes no se usan como marcas de agua, aunque se pueden cargar imágenes al crear el [!UICONTROL proceso Agregar marca de agua].
* Solo se admiten archivos PNG y JPEG para la marca de agua. Otros formatos de recurso no están marcados con agua.
