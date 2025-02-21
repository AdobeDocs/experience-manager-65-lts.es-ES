---
title: Ver datos de análisis de página para medir la eficacia del contenido de la página
description: Utilice datos de análisis de página para medir la eficacia del contenido de su página
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# Visualización de datos de análisis de la página{#seeing-page-analytics-data}

Utilice datos de análisis de página para medir la eficacia del contenido de la página.

## Analytics visible desde la consola {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

Los datos de análisis de página se muestran en [Vista de lista](/help/sites-authoring/basic-handling.md#list-view) de la consola Sitios. Cuando las páginas se muestran en formato de lista, las siguientes columnas están disponibles de forma predeterminada:

* Vistas de la página
* Visitantes únicos
* Tiempo empleado en la página

Cada columna muestra un valor para el período de informe actual e indica si el valor ha aumentado o disminuido desde el período de informe anterior. Los datos que ve se actualizan cada 12 horas.

>[!NOTE]
>
>Para cambiar el período de actualización, [configure el intervalo de importación](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra la consola **Sitios**; por ejemplo, [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. En el extremo derecho de la barra de herramientas (esquina superior derecha), haga clic en el icono para seleccionar **Vista de lista** (el icono mostrado dependerá de la [vista actual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. De nuevo, en el extremo derecho de la barra de herramientas (esquina superior derecha), haga clic en el icono y seleccione **Ver configuración**. Se abre el cuadro de diálogo **Configurar columnas**. Realice los cambios necesarios y confirme con **Actualizar**.

   ![spad-02](assets/spad-02.png)

### Selección del período de informe {#selecting-the-reporting-period}

Seleccione el período de informe para el que aparecen los datos de Analytics en la consola Sitios:

* Datos de los últimos 30 días
* Datos de los últimos 90 días
* Datos de este año

El periodo de informe actual aparece en la barra de herramientas de la consola Sitios (a la derecha de la barra de herramientas superior). Utilice la lista desplegable para seleccionar el periodo de informe requerido.

![aa-05](assets/aa-05.png)

### Configuración de columnas de datos disponibles {#configuring-available-data-columns}

Los miembros del grupo de usuarios administradores de Analytics pueden configurar la consola Sitios para permitir que los autores vean columnas de Analytics adicionales.

>[!NOTE]
>
>Cuando un árbol de páginas contiene elementos secundarios asociados con diferentes configuraciones de nube de Adobe Analytics, no se pueden configurar las columnas de datos disponibles para las páginas.

1. En la vista de lista, use los selectores de vista (a la derecha de la barra de herramientas), seleccione **Ver configuración** y, a continuación, **Agregar datos personalizados de Analytics**.

   ![spad-03](assets/spad-03.png)

1. Seleccione las métricas que desee exponer a los autores en la consola Sitios y, a continuación, haga clic en **Agregar**.

   Las columnas que aparecen se recuperan de Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura de perspectivas de contenido desde sitios {#opening-content-insights-from-sites}

Abra [Perspectiva de contenido](/help/sites-authoring/content-insights.md) desde la consola Sitios para investigar más a fondo la efectividad de la página.

1. En la consola Sitios, seleccione la página para la que desea ver las perspectivas de contenido.
1. En la barra de herramientas, haga clic en el icono Analytics and Recommendations.

   ![Icono de Analytics y Recommendations](do-not-localize/chlimage_1-14.png)

## Análisis visible desde el Editor de páginas (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>Ahora se debe usar el complemento [ActivityMap proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es).
