---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Habilitar la detección de recursos duplicados {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en [!DNL Adobe Experience Manager Assets], la característica de detección de duplicados lo identificará como duplicado. La detección de duplicados está desactivada de forma predeterminada. Para habilitar la función, siga estos pasos:

1. Abra la página de configuración de la consola web [!DNL Experience Manager] al obtener acceso a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleccione la opción **[!UICONTROL detectar duplicado]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción de detección de duplicados en el servlet](assets/chlimage_1-377.png)

   *Imagen: seleccione la opción Detectar duplicados en el servlet.*

La característica de detección de duplicados ahora está habilitada en [!DNL Assets]. Cuando un usuario intenta cargar un recurso que existe en [!DNL Experience Manager], el sistema comprueba si hay algún conflicto y lo indica. Los recursos se identifican mediante el hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan recursos duplicados independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Activos duplicados en el repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Detectar recursos duplicados en AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
