---
title: Informes sobre el uso y uso compartido de recursos
description: Informes sobre sus recursos en  [!DNL Adobe Experience Manager Assets] que le ayudarán a comprender el uso, la actividad y el uso compartido de sus recursos digitales.
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# Informes de recurso {#asset-reports}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | Este artículo |

Los informes de recursos le permiten evaluar la utilidad de su implementación de [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets], puede generar varios informes para sus recursos digitales. Los informes proporcionan información útil sobre el uso del sistema, cómo interactúan los usuarios con los recursos y cuáles se descargan y comparten.

Utilice la información de los informes para derivar métricas de éxito clave para medir la adopción de [!DNL Assets] en su empresa y por parte de los clientes.

El marco de informes [!DNL Assets] usa [!DNL Sling] trabajos para procesar de forma asincrónica las solicitudes de informes de forma ordenada. Es escalable para repositorios grandes. El procesamiento asincrónico de informes aumenta la eficacia y la velocidad con que se generan los informes.

La interfaz de administración de informes es intuitiva e incluye opciones y controles específicos para acceder a informes archivados y ver los estados de ejecución de informes (correcto, fallido y en cola).

Cuando se genera un informe, se le notifica mediante un correo electrónico (opcional) y una notificación de la bandeja de entrada. Puede ver, descargar o eliminar un informe desde la página de lista de informes, en la que se muestran todos los informes generados anteriormente.

## Requisitos previos {#prerequisite-for-reporting}

Para generar informes, haga lo siguiente:

* Habilite el servicio [!UICONTROL Day CQ DAM Event Recorder] desde **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
* Seleccione las actividades o eventos sobre los que desee crear informes. Por ejemplo, para generar un informe sobre los recursos descargados, seleccione [!UICONTROL Recurso descargado (DESCARGADO)].

![Habilitar informes de recursos en la consola web](assets/reports-config-day-cq-dam-event-recorder.png)

## Generación de informes {#generate-reports}

[!DNL Experience Manager Assets] genera los siguientes informes estándar para usted:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de [!DNL Brand Portal]
* Uso del disco
* Archivos
* Vínculos compartidos

Los administradores de [!DNL Adobe Experience Manager] pueden generar y personalizar fácilmente estos informes para su implementación. Un administrador puede seguir estos pasos para generar un informe:

1. En la interfaz de [!DNL Experience Manager], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.

   ![Página de herramientas para navegar por el informe de recursos](assets/AssetsReportNavigation.png)

1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.

   ![Seleccionar tipo de informe](assets/choose_report.png)

   >[!NOTE]
   >
   >De manera predeterminada, los fragmentos de contenido y los vínculos compartidos se incluyen en el informe del recurso [!UICONTROL Descargar]. Seleccione la opción adecuada para crear un informe de vínculos compartidos o para excluir fragmentos de contenido del informe de descarga.

   >[!NOTE]
   >
   >El informe [!UICONTROL Descargar] muestra detalles de solo aquellos recursos que se descargan después de seleccionarlos individualmente o que se descargan mediante Acción rápida. Sin embargo, no incluye los detalles de los recursos que se encuentran dentro de una carpeta descargada.

1. Configure detalles del informe, como el título, la descripción, la miniatura y la ruta de la carpeta en el repositorio de CRX donde se almacena el informe. De manera predeterminada, la ruta de la carpeta es `/content/dam`. Puede especificar una ruta diferente.

   ![Página para agregar detalles del informe](assets/report_configuration.png)

   Elija el intervalo de fechas para el informe.

   Puede optar por generar el informe ahora o en una fecha y hora futuras.

   >[!NOTE]
   >
   >Si decide programar el informe más adelante, asegúrese de especificar la fecha y la hora en los campos Fecha y Hora. Si no se especifica ningún valor, el motor de informes lo trata como un informe que se va a generar instantáneamente.

   Los campos de configuración pueden variar según el tipo de informe que cree. Por ejemplo, el informe **[!UICONTROL Uso del disco]** proporciona opciones para incluir representaciones de recursos al calcular el espacio en disco utilizado por los recursos. Puede elegir incluir o excluir recursos en subcarpetas para el cálculo del uso del disco.

   >[!NOTE]
   >
   >El informe **[!UICONTROL Uso del disco]** no incluye campos de intervalo de fechas porque solo indica el uso actual del espacio en disco.

   ![Página de detalles del informe de uso del disco](assets/disk_usage_configuration.png)

   Al crear el informe **[!UICONTROL Archivos]**, puede incluir o excluir subcarpetas. Sin embargo, no puede incluir representaciones de recursos para este informe.

   ![Página de detalles del informe de archivos](assets/files_report.png)

   El informe **[!UICONTROL Vínculo compartido]** muestra las direcciones URL de los recursos compartidos con usuarios externos desde [!DNL Assets]. Incluye los ID de correo electrónico del usuario que ha compartido los recursos, los ID de correo electrónico de los usuarios con los que se comparten los recursos, la fecha de uso compartido y la fecha de caducidad del vínculo. Las columnas no se pueden personalizar.

   El informe **[!UICONTROL Vínculo compartido]** no incluye opciones para subcarpetas y representaciones porque solo publica las direcciones URL compartidas que aparecen en `/var/dam/share`.

   ![Página de detalles del informe de vínculos compartidos](assets/link_share.png)

1. Haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.

1. En la página **[!UICONTROL Configurar columnas]**, algunas columnas están seleccionadas para aparecer en el informe de forma predeterminada. Puede seleccionar más columnas. Cancelar la selección de una columna para excluirla en el informe.

   ![Seleccionar o cancelar la selección de columnas del informe](assets/configure_columns.png)

   Para mostrar un nombre de columna personalizado o una ruta de acceso a la propiedad, configure las propiedades del binario de recursos en el nodo `jcr:content` en CRX. Como alternativa, agréguela mediante el selector de rutas de propiedades.

   ![Seleccionar o cancelar la selección de columnas del informe](assets/custom_columns.png)

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.
1. En la página [!UICONTROL Informes de recursos], el estado de generación de informes se basa en el estado actual del trabajo de informes como, por ejemplo, [!UICONTROL Éxito], [!UICONTROL Error], [!UICONTROL En cola] o [!UICONTROL Programado]. El mismo estado aparece en la bandeja de entrada de notificaciones. Para ver la página del informe, haga clic en el vínculo del informe. También puede seleccionar el informe y hacer clic en **[!UICONTROL Ver]** en la barra de herramientas.

   <!--![A generated report](assets/report_page.png)-->
   [Estado del informe](assets/report-status.JPG)

   Haga clic en **[!UICONTROL Descargar]** en la barra de herramientas para descargar el informe en formato CSV.

## Añadir columnas personalizadas {#add-custom-columns}

Puede agregar columnas personalizadas a los siguientes informes para mostrar más datos para sus requisitos personalizados:

* Cargar
* Descargar
* Vencimiento
* Modificación
* Publicación
* Publicación de [!DNL Brand Portal]
* Archivos

Para añadir columnas personalizadas a estos informes, siga estos pasos:

1. En [!DNL Manager interface], haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.
1. En la página [!UICONTROL Informes de recursos], haga clic en **[!UICONTROL Crear]** en la barra de herramientas.

1. En la página **[!UICONTROL Crear informe]**, elija el informe que desee crear y haga clic en **[!UICONTROL Siguiente]**.
1. Configure los detalles del informe, como el título, la descripción, la miniatura, la ruta de la carpeta y el intervalo de fechas según corresponda.

1. Para mostrar una columna personalizada, especifique el nombre de la columna debajo de **[!UICONTROL Columnas personalizadas]**.

   ![Especifique un nombre para la columna personalizada del informe](assets/custom_columns-1.png)

1. Agregue la ruta de la propiedad en el nodo `jcr:content` de CRXDE mediante el selector de ruta de propiedad. También puede escribir la ruta en el campo de ruta de la propiedad.

   ![Asignar la ruta de la propiedad desde las rutas en jcr:content](assets/property_picker.png)

   Para agregar más columnas personalizadas, haga clic en **[!UICONTROL Agregar]** y repita los pasos 5 y 6.

1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas. Un mensaje notifica que se ha iniciado la generación del informe.

## Configuración del servicio de depuración {#configure-purging-service}

Para eliminar los informes que ya no necesite, configure el servicio de depuración de informes de DAM desde la consola web para depurar los informes existentes en función de su cantidad y antigüedad.

1. Acceda a la consola web (administrador de configuración) desde `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra la configuración del **[!UICONTROL Servicio de purga de informes DAM]**.
1. Especifique la frecuencia (intervalo de tiempo) para el servicio de purga en el campo `scheduler.expression.name`. También puede configurar la edad y el umbral de cantidad para los informes.
1. Guarde los cambios.

## Información, sugerencias y limitaciones de solución de problemas {#best-practices-and-limitations}

* Si algunos informes o números de los informes no están disponibles o no se muestran según lo esperado, asegúrese de que el servicio [!UICONTROL Grabador de eventos de CQ DAM de día] esté habilitado.

* Elimine los informes que ya no sean necesarios. Utilice las opciones de configuración del servicio de depuración de informes de DAM para configurar los criterios de depuración de informes.

* Si el Informe de uso del disco no se genera y está usando [!DNL Dynamic Media], asegúrese de que todos los recursos procedan correctamente. Para resolverlo, vuelva a procesar los recursos y, a continuación, genere el informe de nuevo.
