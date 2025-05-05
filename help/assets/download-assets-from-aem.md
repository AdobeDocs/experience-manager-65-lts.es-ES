---
title: Descarga de recursos
description: Obtenga información sobre cómo descargar recursos de  [!DNL Adobe Experience Manager]  y habilitar o deshabilitar la funcionalidad de descarga.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# Descargar recursos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=es) |
| AEM 6.5 | Este artículo |

Puede descargar recursos, incluidas representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados están agrupados en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño de archivo máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 activos totales por trabajo de exportación.

>[!NOTE]
>
>Cualquier usuario que tenga permisos de lectura en la ubicación `/var/dam/share` puede acceder al vínculo de descarga compartido en el mensaje de correo electrónico.
>
>Cualquier usuario que tenga permisos de lectura en la ubicación `/var/dam/jobs/download` puede descargar recursos.
>
>Los tipos de recursos Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel no se pueden descargar.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Para descargar recursos, siga estos pasos:**

1. En la esquina superior izquierda, haga clic en el logotipo. En el carril izquierdo, haga clic en **[!UICONTROL Navegación]**.
1. En la página [!UICONTROL Navegación], haga clic en **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Vaya a una carpeta que contenga los recursos que desea descargar.
1. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta.
1. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.
1. En el cuadro de diálogo Descargar, seleccione las opciones de descarga que desee.

   | Opción de exportación o descarga | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir todos los recursos que descargue (incluidos los recursos de carpetas secundarias anidadas en la carpeta principal del recurso) en una carpeta del equipo local. Cuando esta opción no está seleccionada, de forma predeterminada, la jerarquía de carpetas se omite y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Se envía una notificación por correo electrónico al usuario. Las plantillas de correo electrónico estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que personaliza durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recurso(s)]** | Seleccione esta opción para descargar el recurso en su forma original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representación(es)]** | Una representación es la representación binaria de un recurso. Assets tiene una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desea descargar. Las representaciones disponibles dependen del recurso que seleccione. La opción está disponible si el recurso tiene alguna representación. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recortes inteligentes del recurso seleccionado desde AEM. Se crea un archivo zip con las representaciones de recorte inteligente y se descarga en el equipo local. |
   | **[!UICONTROL Representación(es) dinámica(es)]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Cuando selecciona esta opción, también selecciona las representaciones que desea crear dinámicamente seleccionando de la lista [Ajuste preestablecido de imagen](image-presets.md). <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como la inversión de la imagen. La opción solo está disponible si tiene habilitado [!DNL Dynamic Media]. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]**.

Al seleccionar una carpeta para descargar, se descarga la jerarquía de recursos completa debajo de la carpeta. Para incluir cada recurso que descargue (incluidos los recursos de las carpetas secundarias anidadas en la carpeta principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado en [!DNL Experience Manager] permite a los usuarios autenticados emitir solicitudes de descarga simultáneas y arbitrariamente grandes para crear archivos ZIP de recursos visibles para ellos que pueden sobrecargar el servidor y la red. Para mitigar los posibles riesgos DoS causados por esta característica, el componente OSGi `AssetDownloadServlet` está deshabilitado de forma predeterminada para las instancias de publicación.

Para permitir la descarga de recursos desde su DAM, por ejemplo, cuando utilice algo como Asset Share Commons u otra implementación similar a un portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda configurar el tamaño de descarga permitido lo más bajo posible sin afectar a los requisitos de descarga diarios. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombres que se dirija al modo de ejecución de publicación (`config.publish`): `/apps/<your-app-name>/config.publish`. Para definir las propiedades de configuración de un modo de ejecución, vea [Modos de ejecución](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. En la carpeta de configuración, cree un archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Establece un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El siguiente ejemplo configura el tamaño máximo de la descarga ZIP para que no supere los 100 kb.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

De manera predeterminada, para `GET` solicitudes de descarga de archivos, [!DNL Experience Manager] aplica un límite de 50 MB al tamaño de descarga del archivo ZIP. Las descargas iniciadas a través de `POST` solicitudes para la interfaz de usuario no se ven afectadas por este límite.

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede deshabilitar en una instancia de publicación de [!DNL Experience Manager] al actualizar la configuración de Dispatcher para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede deshabilitar manualmente a través de la consola OSGi directamente.

1. Para bloquear solicitudes de descarga de recursos a través de una configuración de Dispatcher, edite la configuración de `dispatcher.any` y agregue una regla a la [sección de filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Para deshabilitar el componente OSGi en una instancia de publicación, acceda a la consola OSGi en `http://[aem_server]:[port]/system/console/components`. Busque `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` y haga clic en **[!UICONTROL Deshabilitar]**.

>[!MORELIKETHIS]
>
>* [Descargar recursos mediante Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=es)
>* [Descargar recursos protegidos por DRM](drm.md).
>* [Descargar recursos mediante la aplicación de escritorio de Experience Manager en Windows o Mac Desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es#download-assets).
>* [Descargue recursos mediante Adobe Assets Link desde las aplicaciones de Adobe Creative Cloud admitidas](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html).
