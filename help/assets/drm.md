---
title: Digital Rights Management de recursos
description: Obtenga información sobre cómo administrar los estados de caducidad de los recursos y la información de los recursos con licencia en  [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 7%

---

# Digital Rights Management para recursos {#digital-rights-management-in-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=es) |
| AEM 6.5 | Este artículo |

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración de uso. Dado que [!DNL Adobe Experience Manager Assets] está completamente integrado con la plataforma [!DNL Experience Manager], puede administrar de manera eficiente la información de caducidad y los estados de los recursos. También puede asociar la información de licencias con los recursos.

## Caducidad de recursos {#asset-expiration}

La caducidad de los recursos es una forma eficaz de aplicar los requisitos de licencia a los recursos. Garantiza que el recurso publicado se cancele la publicación cuando caduque, lo que evita la posibilidad de que se produzca cualquier infracción de licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en la consola [!DNL Assets] tanto en las vistas de tarjeta como de lista.

![lista_de_marcas_caducadas](assets/expired_flag_list.png)

*Imagen: en la vista de lista, la columna [!UICONTROL Estado] muestra el titular [!UICONTROL Caducado].*

Puede ver el estado de caducidad de un recurso en la [!UICONTROL cronología] del carril izquierdo.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de diferentes zonas horarias.

También puede ver el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]**. Administra los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los recursos secundarios, las colecciones y los proyectos a los que se hace referencia.

1. Desplácese hasta el recurso para el que desee ver las páginas web de referencia y los recursos compuestos.
1. Seleccione el recurso y abra **[!UICONTROL Referencias]** en el carril izquierdo. Para los recursos caducados, el carril [!UICONTROL Referencias] muestra el estado de caducidad **[!UICONTROL El recurso ha caducado]** en la parte superior.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Assets Si el recurso tiene recursos secundarios caducados, el carril [!UICONTROL Referencias] muestra el estado **[!UICONTROL El recurso tiene un subrecurso caducado]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Buscar recursos caducados {#search-expired-assets}

Puede buscar recursos caducados, incluidos los subrecursos caducados en el panel Buscar.

1. En la consola [!DNL Assets], haga clic en **[!UICONTROL Buscar]** en la barra de herramientas para mostrar el cuadro Omnisearch.

1. Con el cursor en el cuadro Omnisearch, seleccione la clave `Enter` para mostrar la página de resultados de la búsqueda.
1. Abra el panel de búsqueda en el carril izquierdo. Haga clic en la opción **[!UICONTROL Estado de caducidad]** para expandirla.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Elija **[!UICONTROL Caducado]**. Solo se muestran los recursos caducados después de filtrar los resultados de búsqueda.

Al elegir la opción **[!UICONTROL Caducado]**, la consola [!DNL Assets] solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que [!DNL Experience Manager] detecte que hacen referencia a recursos secundarios caducados la próxima vez que se ejecute el programador.

Si modifica la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo de programación actual, la programación sigue detectando este recurso como caducado la próxima vez que se ejecute y refleja su estado en consecuencia.

Además, si un fallo o error impide que el programador detecte los recursos caducados en el ciclo actual, vuelve a examinarlos en el ciclo siguiente y detecta su estado caducado.

Para permitir que la consola [!DNL Assets] muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure un flujo de trabajo **[!UICONTROL Notificación de caducidad de Adobe CQ DAM]** en el Administrador de configuración [!DNL Experience Manager].

1. Abra el Administrador de configuración de [!DNL Experience Manager].
1. Elija **[!UICONTROL Notificación de caducidad de Adobe CQ DAM]**. De forma predeterminada, está seleccionado **[!UICONTROL Programador basado en tiempo]**, que programa un trabajo para comprobar a una hora específica si un recurso tiene recursos secundarios caducados. Una vez finalizado el trabajo, los recursos que tienen recursos secundarios caducados y los recursos a los que se hace referencia se muestran como caducados en los resultados de búsqueda.

1. Para ejecutar el trabajo periódicamente, desactive el campo **[!UICONTROL Regla de planificador basada en tiempo]** y modifique el tiempo en segundos en el campo **[!UICONTROL Programador periódico]**. Por ejemplo, la expresión de ejemplo `0 0 0 * * ?` déclencheur el trabajo a las 00 horas.
1. Seleccione **[!UICONTROL enviar correo electrónico]** para recibir mensajes de correo electrónico cuando caduque un recurso.

   >[!NOTE]
   >
   >Solo el creador del recurso (la persona que carga un recurso en particular en [!DNL Assets]) recibe un mensaje de correo electrónico cuando caduca el recurso. Consulte [cómo configurar las notificaciones por correo electrónico](/help/sites-administering/notification.md) para obtener más información sobre cómo configurar las notificaciones por correo electrónico en el nivel general [!DNL Experience Manager].

1. En el campo **[!UICONTROL Notificación previa en segundos]**, especifique el tiempo en segundos antes de la hora en que caduca un recurso cuando desee recibir una notificación con respecto a la caducidad. Los creadores de recursos reciben un mensaje antes de la caducidad del recurso en el que se le notifica que el recurso está a punto de caducar después del tiempo especificado. Una vez que caduque el recurso, recibirá otra notificación que confirmará la caducidad. Además, los recursos caducados se desactivan.

1. Haga clic en **[!UICONTROL Guardar]**.

## Estados de los recursos {#asset-states}

La consola [!DNL Assets] puede mostrar varios estados para los recursos. Según el estado actual de un recurso determinado, la vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario [!DNL Assets], seleccione un recurso.
1. Haga clic en **[!UICONTROL Publicar]** en la barra de herramientas. Si no ve **Publicar** en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque la opción **[!UICONTROL Publicar]** ![publicar](assets/do-not-localize/publish-globe.png).
1. Elija **[!UICONTROL Publicar]** en el menú y luego cierre el cuadro de diálogo de confirmación.
1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora a la que se publicó el recurso.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Para mostrar la página de detalles del recurso, en la interfaz [!DNL Assets], seleccione un recurso y haga clic en **[!UICONTROL Propiedades]** ![propiedades de vista](assets/do-not-localize/info-circle-icon.png).

1. En la ficha [!UICONTROL Avanzado], establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Caduca]**.

   ![establezca la fecha y hora de caducidad del recurso en el campo Caduca](assets/asset-properties-advanced-tab.png)

   *Imagen: ficha [!UICONTROL Avanzadas] en la página del recurso [!UICONTROL Propiedades] para establecer la caducidad del recurso.*

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Cerrar]** para mostrar la consola Recursos.
1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. En la consola [!DNL Assets], seleccione una carpeta y cree una tarea de revisión en la carpeta.
1. Revise y apruebe o rechace los recursos en la tarea de revisión y haga clic en **[!UICONTROL Completar]**.
1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos que aprobó o rechazó se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para buscar recursos según su estado, haga clic en **[!UICONTROL Buscar]** ![opción de búsqueda](assets/do-not-localize/search_icon.png) para mostrar la barra Omnisearch.
1. Seleccione `Return` y haga clic en [!DNL Experience Manager] para mostrar el panel de búsqueda.
1. En el panel de búsqueda, haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Haga clic en **[!UICONTROL Estado de aprobación]** y haga clic en la opción adecuada para buscar recursos aprobados o rechazados.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel Buscar y elija la opción adecuada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que se hayan aprobado en una tarea de revisión y que aún no hayan caducado seleccionando las opciones adecuadas en las facetas de búsqueda.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

Esta característica exige la aceptación del acuerdo de licencia para poder descargar un recurso con licencia de [!DNL Adobe Experience Manager Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia para aceptar el acuerdo de licencia. Si no acepta el contrato de licencia, la opción **[!UICONTROL Descargar]** no estará disponible.

Si la selección contiene varios recursos protegidos, seleccione un recurso a la vez, acepte el acuerdo de licencia y proceda a descargar el recurso.

Un activo se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` señala a la ruta de acceso de la página que contiene el contrato de licencia del recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es una HTML sin procesar que especifica el contrato de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licenses` utilizada para almacenar licencias en versiones anteriores de [!DNL Experience Manager] está en desuso.
>
>Si crea o modifica páginas de licencias, o las transfiere de versiones anteriores de [!DNL Experience Manager], Adobe recomienda almacenarlas en `/apps/settings/dam/drm/licenses` o `/conf/&ast;/settings/dam/drm/licenses`.

### Descarga de recursos protegidos por DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desee descargar y haga clic en **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel [!UICONTROL Licencia], elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Haga clic en la opción **[!UICONTROL Descargar]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Descargar]** solo está habilitada cuando acepta el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel y la opción **[!UICONTROL Descargar]** está habilitada para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]** para descargar el recurso o sus representaciones.
