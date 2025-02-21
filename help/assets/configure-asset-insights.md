---
title: Configure Assets Insights para obtener análisis.
description: Configurar Assets Insights en  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 6%

---

# Configuración de Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] obtiene datos de uso de recursos digitales utilizados por sitios web de terceros de [!DNL Adobe Analytics]. Para permitir que Assets Insights recupere estos datos y genere información, primero configure la característica para integrarla con [!DNL Adobe Analytics]. Para usar esta característica en una instalación On-Premise, adquiera la licencia [!DNL Adobe Analytics] por separado. Los clientes de [!DNL Managed Services] reciben [!DNL Analytics] licencia incluida con [!DNL Experience Manager]. Ver [descripción del producto de Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para las imágenes.

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Haga clic en la tarjeta **[!UICONTROL Configuración de información]**.
1. En el asistente, seleccione un centro de datos y proporcione las credenciales, incluido el nombre de su organización, el nombre de usuario y el secreto compartido.

   ![Configurar Adobe Analytics para las estadísticas de Assets en Experience Manager](assets/insights_config2.png)

   *Figura: Configurar [!DNL Adobe Analytics] para las estadísticas de Assets en [!DNL Experience Manager].*

1. Haga clic en **[!UICONTROL Autenticar]**.
1. Una vez que [!DNL Experience Manager] haya autenticado sus credenciales, en la lista **[!UICONTROL Grupo de informes]**, elija un grupo de informes [!DNL Adobe Analytics] de donde quiera que Assets Insights obtenga datos. Haga clic en **[!UICONTROL Agregar]**.
1. Una vez que [!DNL Experience Manager] haya configurado el grupo de informes, haga clic en **[!UICONTROL Listo]**.

## Rastreador de página {#page-tracker}

Después de configurar la cuenta de [!DNL Adobe Analytics], se genera el código de seguimiento de página. Para permitir que Assets Insights rastree [!DNL Experience Manager] recursos utilizados en sitios web de terceros, incluya el código de rastreador de páginas en el código del sitio web. Use la utilidad [!UICONTROL Rastreador de páginas] en [!DNL Experience Manager Assets] para generar el código de rastreador de páginas. Para obtener más información sobre cómo incluir el código de rastreador de páginas en páginas web de terceros, consulte [Usar el rastreador de páginas e incrustar código en las páginas web](/help/assets/use-page-tracker.md).

1. En [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. En la página **[!UICONTROL Navegación]**, haga clic en la tarjeta **[!UICONTROL Rastreador de páginas de perspectivas]**.
1. Haga clic en **[!UICONTROL Descargar]** para descargar el código de rastreador de páginas.
