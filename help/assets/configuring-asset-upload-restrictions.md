---
title: Configurar restricciones de carga de recursos
description: Restringir el tipo de recursos (archivos) que los usuarios pueden cargar
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 18%

---

# Configurar restricciones de carga de recursos {#configuring-asset-upload-restrictions}

Puede configurar [!DNL Adobe Experience Manager Assets] para restringir el tipo de recursos que los usuarios pueden cargar. Ayuda a evitar cargas accidentales de archivos malintencionados y formatos no deseados. El servicio `Day CQ DAM Asset Upload Restriction` le permite controlar el tipo de archivos que los usuarios pueden cargar. De manera predeterminada, [!DNL Assets] permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para restringir el acceso de los usuarios únicamente a la carga de archivos de tipos MIME específicos.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Restricción de carga de recursos CQ DAM por día]** en modo de edición. De manera predeterminada, la opción **Permitir todos los MIME** está seleccionada, lo que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir el acceso de los usuarios solo a archivos de ciertos tipos de MIME, anule la selección de la opción **[!UICONTROL Permitir todos los MIME]** y especifique los tipos de MIME permitidos en los campos **[!UICONTROL Recursos de MIME permitidos (regex)]** mediante expresiones regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios. Si especifica cadenas MIME para los tipos de MIME permitidos, la operación de carga falla con cualquier recurso que tenga un tipo de MIME que no coincida con las cadenas MIME configuradas en estos campos.
