---
title: Detección del tipo MIME de los recursos mediante Apache Tika
description: Habilite Apache Tika para ayudar a  [!DNL Experience Manager Assets] detectar el tipo MIME de los recursos del flujo de contenido durante la operación de carga en lugar de la extensión de archivo.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---

# Detectar tipo MIME de recursos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta el tipo MIME de los recursos que se cargan desde su extensión de archivo.

Si usa [!DNL Apache Tika] para cargar recursos, [!DNL Assets] detecta su tipo MIME del flujo de contenido durante la operación de carga en lugar de la extensión de archivo.

Esta función está desactivada de forma predeterminada. Para habilitar la característica, configure el servicio **[!UICONTROL Day CQ DAM Mime Type]** desde [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La detección de tipos MIME mediante la biblioteca [!DNL Apache Tika] es una operación que consume muchos recursos.

1. Para abrir la consola web de Configuration Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.

1. En la lista de servicios, busque **[!UICONTROL Day CQ DAM Mime Type Service]** y haga clic en **[!UICONTROL Editar]**.

1. Seleccione la opción **[!UICONTROL Detectar MIME a partir del contenido]** para habilitar el análisis de los recursos cargados y determinar su tipo MIME al omitir las extensiones de archivo. De forma predeterminada, esta opción no está seleccionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.
