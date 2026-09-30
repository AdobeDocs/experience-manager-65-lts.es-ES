---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: ba54ecc2-a158-462a-8724-f6103b692edc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '190'
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
