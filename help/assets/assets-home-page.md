---
title: Experiencia de la página de inicio [!DNL Assets]
description: Personalice la  [!DNL Experience Manager Assets] página de inicio para disfrutar de una pantalla de bienvenida enriquecida que incluya una instantánea de las actividades recientes relacionadas con los recursos.
contentOwner: AG
feature: Asset Management
role: Admin, User
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# Experiencia en la página de inicio de [!DNL Adobe Experience Manager Assets] {#aem-assets-home-page-experience}

Personalice la página de inicio [!DNL Adobe Experience Manager Assets] para disfrutar de una pantalla de bienvenida enriquecida que incluya una instantánea de las actividades recientes relacionadas con los recursos.

La página de inicio de [!DNL Assets] proporciona una experiencia de pantalla de bienvenida enriquecida y personalizada, que incluye una instantánea de las actividades recientes, como los recursos que se vieron o cargaron recientemente.

La página principal [!DNL Assets] está deshabilitada de manera predeterminada. Para habilitarlo, realice los siguientes pasos:

1. Abra el Administrador de configuración [!DNL Experience Manager] `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Grabador de eventos CQ DAM de día]**.
1. Seleccione **[!UICONTROL Habilitar este servicio]** para habilitar la grabación de actividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. En la lista **[!UICONTROL Tipos de eventos]**, seleccione los eventos que desea registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones Recursos vistos, Proyectos vistos y Colecciones vistas, aumenta significativamente el número de eventos registrados.

1. Abra el servicio **[!UICONTROL Indicador de característica de página principal de recursos DAM]** desde el Administrador de configuración `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione la opción `isEnabled.name` para habilitar la característica de página de inicio [!DNL Assets]. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el cuadro de diálogo **[!UICONTROL Preferencias de usuario]** y seleccione **[!UICONTROL Habilitar la página de inicio de Assets]**. Guarde los cambios.

   ![Habilitar la página de inicio de los recursos en el cuadro de diálogo Preferencias de usuario](assets/Annotation-color.png)

Después de habilitar la página principal de [!DNL Assets], vaya a la interfaz de usuario de [!DNL Assets] desde la página de navegación o acceda a ella directamente desde la dirección URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar vínculo de experiencia en la interfaz de usuario de Assets](assets/config-experience-link.png)

Haz clic en **[!UICONTROL Haz clic aquí para configurar el vínculo de experiencia]** y añadir tu nombre de usuario, imagen de fondo e imagen de perfil.

La página de inicio [!DNL Assets] incluye las siguientes secciones:

* Sección de bienvenida
* Sección Widget

**Sección de bienvenida**

Si su perfil existe, la sección Bienvenido muestra un mensaje de bienvenida dirigido a usted. Además, muestra la imagen de perfil y una imagen de bienvenida (si ya está configurada).

Si el perfil está incompleto, la sección Bienvenida muestra un mensaje de bienvenida genérico y un marcador de posición para la imagen de perfil.

**Sección de widget**

Esta sección aparece debajo de la sección Bienvenido y muestra widgets predeterminados en las siguientes secciones:

* Actividad
* Reciente
* Descubrir

**Actividad**: en esta sección, el widget **[!UICONTROL Mi actividad]** muestra las actividades recientes realizadas por el usuario que ha iniciado sesión con recursos (incluidos los recursos sin representaciones), por ejemplo, cargas de recursos, descargas, creación de recursos, ediciones, comentarios, anotaciones y recursos compartidos.

**Reciente**: el widget **[!UICONTROL Vistos recientemente]** en esta sección muestra entidades a las que ha accedido recientemente el usuario que ha iniciado sesión, incluidas carpetas, colecciones y proyectos.

**Discover**: el widget **[!UICONTROL Nuevo]** de esta sección muestra los recursos y representaciones cargados recientemente en la implementación de [!DNL Assets].

Para habilitar la depuración de los datos de actividad del usuario, habilite el **[!UICONTROL Servicio de depuración de eventos DAM]** desde el Administrador de configuración. Después de habilitar este servicio, el sistema eliminará las actividades del usuario que haya iniciado sesión y que superen un número especificado.

La pantalla de bienvenida proporciona ayudas para la navegación sencillas como, por ejemplo, los iconos de la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Al habilitar los servicios [!UICONTROL Day CQ DAM Event Recorder] y [!UICONTROL DAM Event Purge] se aumentan las operaciones de escritura en JCR y la indexación de búsqueda, lo que aumenta significativamente la carga en el servidor [!DNL Experience Manager]. La carga adicional en el servidor [!DNL Experience Manager] puede afectar el rendimiento.

>[!CAUTION]
>
>Capturar, filtrar y purgar las actividades de usuario necesarias para la página principal de [!DNL Assets] impone una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar Página principal de forma eficaz para los usuarios de destino.
>
>Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función Página principal de recursos para evitar un aumento en las actividades de los usuarios. Además, los administradores pueden excluir las actividades de grabación para usuarios específicos configurando [!UICONTROL Day CQ DAM Event Recorder] desde [!UICONTROL Configuration Manager].
>
>Si utiliza la función, Adobe recomienda programar la frecuencia de depuración en función de la carga del servidor.
