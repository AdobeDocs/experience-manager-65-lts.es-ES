---
title: Assets Insights
description: Descubra cómo la funcionalidad Assets Insights le permite rastrear las clasificaciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y las soluciones creativas de Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 8%

---

# Assets Insights {#asset-insights}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Este artículo |

La función Assets Insights le permite realizar un seguimiento de las valoraciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y las soluciones creativas de Adobe. Ayuda a obtener perspectivas sobre su rendimiento y popularidad.

[!DNL Assets] Insights captura los detalles de la actividad del usuario, como la cantidad de veces que se clasifica, hace clic y genera impresiones una imagen (la cantidad de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las puntuaciones y las estadísticas de rendimiento para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Incluso puede formular políticas de archivado y renovación de licencias basadas en estas estadísticas.

Para que [!DNL Assets] Insights capture estadísticas de uso de imágenes de un sitio web, debe incluir el código incrustado de la imagen en el código del sitio web.

Para permitir que Assets Insights muestre las estadísticas de uso de los recursos, configure primero la función para recuperar los datos de informes de Adobe Analytics. Para obtener más información, consulte [Configuración de Assets Insights](/help/assets/configure-asset-insights.md). Para usar esta característica en una instalación On-Premise, adquiera la licencia [!DNL Adobe Analytics] por separado. Los clientes de [!DNL Managed Services] reciben [!DNL Analytics] licencia incluida con [!DNL Experience Manager]. Ver [descripción del producto de Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Las perspectivas solo son compatibles y se proporcionan para las imágenes.

## Visualización de estadísticas de una imagen {#viewing-statistics-for-an-image}

Puede ver las puntuaciones de Assets Insights desde la página de metadatos.

1. En la interfaz de usuario (IU) [!DNL Assets], seleccione la imagen y, a continuación, haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página Propiedades, haga clic en la ficha **[!UICONTROL Información]**.
1. Revise los detalles de uso del recurso en la ficha **[!UICONTROL Información]**. La sección **[!UICONTROL Puntuación]** describe el uso total de recursos y las puntuaciones de rendimiento de un recurso

   La puntuación de uso describe el número de veces que el recurso se utiliza en varias soluciones.

   La puntuación **[!UICONTROL Impresiones]** es el número de veces que el recurso se carga en el sitio web. El número mostrado bajo **[!UICONTROL Clics]** es el número de veces que se hace clic en el recurso.

1. Revise la sección **[!UICONTROL Estadísticas de uso]** para saber de qué entidades formaba parte el recurso y qué soluciones creativas lo utilizaron recientemente. Cuanto mayor sea el uso, mayores serán las probabilidades de que el recurso sea popular entre los usuarios. Los datos de uso se muestran bajo los siguientes encabezados:

   * **Recurso**: el número de veces que el recurso formaba parte de una colección o de un recurso compuesto
   * **Web y dispositivos móviles**: La cantidad de veces que el recurso formaba parte de sitios web y aplicaciones
   * **Social**: El número de veces que se usó el recurso en soluciones como Adobe Social y Adobe Campaign
   * **Correo electrónico**: El número de veces que el recurso se usó en campañas de correo electrónico

   ![estadísticas_de_uso](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Debido a que la función Assets Insights generalmente obtiene los datos de las soluciones de Adobe Analytics de forma periódica, es posible que la sección Soluciones no muestre los datos más recientes. El período de tiempo durante el cual se muestran los datos depende de la programación de la operación de recuperación que ejecuta Assets Insights para recuperar datos de Analytics.

1. Para ver las estadísticas de rendimiento del recurso gráficamente durante un período de tiempo, seleccione el período en la sección **[!UICONTROL Estadísticas de rendimiento]**. Los detalles, incluidos los clics y las impresiones, se muestran como líneas de tendencia de un gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A diferencia de los datos de la sección Soluciones, la sección Estadísticas de rendimiento muestra los datos más recientes.

1. Para obtener el código incrustado del recurso que incluye en los sitios web a fin de obtener datos de rendimiento, haga clic en **[!UICONTROL Obtener código incrustado]** debajo de la miniatura del recurso. Para obtener más información sobre cómo incluir el código incrustado en páginas web de terceros, consulte [Uso del rastreador de páginas e incrustar código en páginas web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualización de estadísticas acumuladas de imágenes {#viewing-aggregate-statistics-for-images}

Puede ver las puntuaciones de todos los recursos de una carpeta simultáneamente mediante la **[!UICONTROL Vista de la información]**.

1. En la interfaz de usuario [!DNL Assets], vaya a la carpeta que contiene los recursos de los cuales desea ver información.
1. Haga clic en Diseño en la barra de herramientas y, a continuación, elija **[!UICONTROL Vista de la información]**.
1. La página muestra las puntuaciones de uso de los recursos. Compare las clasificaciones de los distintos recursos y obtenga información.

## Programar trabajo en segundo plano {#scheduling-background-job}

Assets Insights obtiene datos de uso de recursos de los grupos de informes de Adobe Analytics de forma periódica. De forma predeterminada, Assets Insights ejecuta un trabajo en segundo plano cada 24 horas a las 2 a. m. para recuperar los datos. Sin embargo, puede modificar la frecuencia y la hora configurando el servicio **[!UICONTROL Trabajo de sincronización de informes de rendimiento de recursos CQ DAM de Adobe]** desde la consola web.

1. Haga clic en el logotipo de [!DNL Experience Manager] y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. Abra la configuración del servicio **[!UICONTROL Trabajo de sincronización de informes de rendimiento de recursos de Adobe CQ DAM]**.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique la frecuencia del programador deseada y la hora de inicio del trabajo en la expresión del programador de propiedades. Guarde los cambios.
