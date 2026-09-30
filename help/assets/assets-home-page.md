---
title: Experiencia de página de inicio de [!DNL Assets]
description: Personalice la página de inicio [!DNL Experience Manager Assets] para disfrutar de una pantalla de bienvenida enriquecida que incluya una instantánea de las actividades recientes relacionadas con los recursos.
contentOwner: AG
feature: Asset Management
role: Admin, User
solution: Experience Manager, Experience Manager Assets
exl-id: cdf1f56c-d9b2-456b-be05-e0394ea6204f
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 96%
---
# Experiencia de página de inicio de [!DNL Adobe Experience Manager Assets] {#aem-assets-home-page-experience}

Personalice la página de inicio de [!DNL Adobe Experience Manager Assets] para disfrutar de una experiencia de pantalla de bienvenida enriquecida que incluya una instantánea de las actividades recientes relacionadas con los recursos.

La página de inicio de [!DNL Assets] proporciona una experiencia de pantalla de bienvenida enriquecida y personalizada, que incluye una instantánea de las actividades recientes, como los recursos vistos o cargados recientemente.

La página de inicio de [!DNL Assets] está desactivada de forma predeterminada. Para habilitarla, siga estos pasos:

1. Abra el administrador de configuración de [!DNL Experience Manager] `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Grabador de eventos CQ DAM de día]**.
1. Seleccione **[!UICONTROL Habilitar este servicio]** para activar la grabación de actividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. En la lista **[!UICONTROL Tipos de eventos]**, seleccione los eventos que desea registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones Recursos vistos, Proyectos vistos y Colecciones vistas, aumenta de manera significativa el número de eventos registrados.

1. Abra el servicio **[!UICONTROL Indicador de función de la página de inicio de recursos DAM]** desde el administrador de configuración `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione la opción `isEnabled.name` para habilitar la característica de página de inicio de [!DNL Assets]. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el cuadro de diálogo **[!UICONTROL Preferencias de usuario]** y seleccione **[!UICONTROL Habilitar la página de inicio de Assets]**. Guarde los cambios.

   ![Habilitación de la página de inicio de Assets en el cuadro de diálogo Preferencias de usuario](assets/Annotation-color.png)

Después de habilitar la página de inicio de [!DNL Assets], vaya a la interfaz de usuario de [!DNL Assets] desde la página de navegación o acceda a ella directamente desde la URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configuración de un vínculo de experiencia en la interfaz de usuario de Assets](assets/config-experience-link.png)

Haga clic en **[!UICONTROL Haga clic aquí para configurar el vínculo de experiencia]** y añada su nombre de usuario, imagen de fondo e imagen de perfil.

La página de inicio de [!DNL Assets] incluye las siguientes secciones:

* Sección de bienvenida
* Sección de widget

**Sección de bienvenida**

Si su perfil existe, la sección Bienvenida muestra un mensaje de bienvenida dirigido a usted. Además, presenta su imagen de perfil y una imagen de bienvenida (si ya está configurada).

Si su perfil está incompleto, la sección Bienvenida muestra un mensaje de bienvenida genérico y un marcador de posición para la imagen de perfil.

**Sección de widget**

Esta sección aparece debajo de la sección Bienvenida y muestra widgets predeterminados en las siguientes secciones:

* Actividad
* Reciente
* Descubrir

**Actividad**: en esta sección, el widget **[!UICONTROL Mi actividad]** muestra las actividades recientes realizadas por el usuario que ha iniciado sesión con recursos (incluidos los recursos sin representaciones); por ejemplo, cargas, descargas, creación, edición, comentarios, anotaciones y uso compartido de recursos.

**Reciente**: el widget **[!UICONTROL Visto recientemente]** de esta sección muestra entidades a las que ha accedido hace poco el usuario que ha iniciado sesión, incluidas carpetas, colecciones y proyectos.

**Descubrir**: el widget **[!UICONTROL Nuevo]** de esta sección muestra los recursos y representaciones cargados hace poco en la implementación de [!DNL Assets].

Para habilitar la depuración de los datos de actividad del usuario, habilite el **[!UICONTROL Servicio de depuración de eventos DAM]** desde el administrador de configuración. Después de habilitar este servicio, el sistema eliminará las actividades del usuario que ha iniciado sesión y que superen un número especificado.

La pantalla de bienvenida proporciona ayudas para la navegación sencillas como, por ejemplo, los iconos de la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Al habilitar los servicios [!UICONTROL Grabador de eventos CQ DAM de día] y [!UICONTROL Depuración de eventos DAM], aumentan las operaciones de escritura en JCR y la indexación de búsqueda, lo que incrementa de manera significativa la carga en el servidor [!DNL Experience Manager]. La carga adicional en el servidor [!DNL Experience Manager] puede afectar a su rendimiento.

>[!CAUTION]
>
>Capturar, filtrar y purgar las actividades de usuario necesarias para la página de inicio de [!DNL Assets] impone una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar la página de inicio de forma eficaz para los usuarios de destino.
>
>Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función Página de inicio del recurso para evitar un aumento en las actividades de los usuarios. Además, los administradores pueden excluir las actividades de grabación para usuarios específicos configurando el [!UICONTROL Grabador de eventos CQ DAM de día] desde el [!UICONTROL administrador de configuración].
>
>Si utiliza la función, Adobe le recomienda programar la frecuencia de depuración en función de la carga del servidor.
