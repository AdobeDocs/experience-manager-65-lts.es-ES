---
title: Integrar [!DNL Assets] con el flujo de actividad
description: Describe las capacidades de grabación de  [!DNL Experience Manager]  y cómo configurarlo para que registre eventos específicos.
contentOwner: AG
role: Developer
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Integrar [!DNL Assets] con el flujo de actividad {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] usuarios realizan muchas acciones, como crear, cargar y eliminar Assets. Estas acciones se pueden registrar para que pueda proporcionar un historial de lo que ha hecho un usuario. En esta sección se describen las capacidades de grabación de [!DNL Experience Manager] y cómo configurar [!DNL Experience Manager] para que registre eventos específicos.

## Consideraciones de rendimiento y comportamiento predeterminado {#performance-considerations-and-default-behavior}

Esta integración podría consumir espacio en CPU y en disco, por ejemplo, al realizar una importación masiva. Por estos motivos, la integración de [!DNL Assets] con el flujo de actividad está deshabilitada de manera predeterminada.

## Eventos de acción admitidos {#supported-action-events}

Puede configurar los siguientes eventos para que se registren:

* Licencia aceptada (ACEPTADA)
* Recurso creado (ASSET_CREATED)
* Recurso movido (ASSET_MOVED)
* Recurso eliminado (ASSET_REMOVED)
* Licencia rechazada (RECHAZADA)
* Recurso descargado (DESCARGADO)
* Recurso con versión (VERSIONED)
* Versión del recurso restaurada (RESTAURADA)
* Metadatos de los recursos actualizados (METADATA_UPDATED)
* Recurso publicado en un sistema externo (PUBLISHED_EXTERNAL)
* Actualización del original del recurso (ORIGINAL_UPDATED)
* Representación de recursos actualizada (RENDITION_UPDATED)
* Representación de recursos eliminada (RENDITION_REMOVED)
* Subactivo actualizado (SUBASSET_UPDATED)
* Subactivo eliminado (SUBASSET_REMOVED)

## Configurar la grabación de eventos de [!DNL Assets] {#configuring-aem-assets-events-recording}

La [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso al ajuste del grabador de eventos de Assets. Para configurar el grabador de eventos de Assets, siga estos pasos:

1. Vaya a la **[!UICONTROL consola web]**

1. Haga clic en **[!UICONTROL Configuración]**.

1. Haga doble clic en **[!UICONTROL Grabador de eventos CQ DAM de día]**.

1. Marque **[!UICONTROL Habilita este servicio]**.

1. Compruebe qué **[!UICONTROL tipos de eventos]** desea que se registren en el flujo de actividad del usuario.

1. Haga clic en **[!UICONTROL Guardar]**.

## Leer eventos grabados {#reading-recorded-events}

Los eventos registrados se almacenan como actividades. Puede leerlas mediante programación usando la [API de Activity Manager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
