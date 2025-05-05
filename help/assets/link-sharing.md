---
title: Uso compartido de recursos mediante un vínculo
description: Comparta recursos, carpetas y colecciones como una dirección URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 6%

---

# Compartir recurso como vínculo {#asset-link-sharing}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=es) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] le permite compartir recursos, carpetas y colecciones como una dirección URL con miembros de su organización y entidades externas, incluidos socios y proveedores. Compartir recursos a través de un vínculo es una manera cómoda de poner los recursos a disposición de terceros externos sin que tengan que iniciar sesión primero en [!DNL Assets].

>[!PREREQUISITES]
>
>* Se necesita el permiso `Edit ACL` en la carpeta o el recurso que desea compartir como vínculo.
>* Para enviar correos electrónicos a los usuarios, configure los detalles del servidor SMTP en [Servicio de correo CQ por día](#configmailservice).

## Compartir recursos {#share-assets}

Para generar la dirección URL de los recursos que desea compartir con los usuarios, use el cuadro de diálogo [!UICONTROL Uso compartido de vínculos].

* Los usuarios con privilegios de administrador o con permisos de lectura en la ubicación `/var/dam/share` pueden ver los vínculos compartidos con ellos.
* Los usuarios que tienen permisos de lectura en la ubicación `/var/dam/jobs/download` pueden descargar recursos desde el vínculo compartido.

1. En la interfaz de usuario [!DNL Assets], seleccione el recurso que desea compartir como vínculo.

1. En la barra de herramientas, haga clic en el icono **[!UICONTROL Compartir vínculo]** ![compartir recursos](assets/do-not-localize/assets_share.png). El vínculo que se crea después de hacer clic en **[!UICONTROL Compartir]** se muestra por adelantado en el campo [!UICONTROL Compartir vínculo]. El vínculo no se creará hasta que seleccione **[!UICONTROL Enviar]**.

   ![Cuadro de diálogo con el vínculo compartido](assets/share-assets-as-link.png)

   *Imagen: cuadro de diálogo para compartir recursos como vínculo.*

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. Puede agregar uno o más usuarios.

   >[!NOTE]
   >
   >Si escribe un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras [!UICONTROL Usuario externo] llevan como prefijo el ID de correo electrónico del usuario.

1. En el cuadro **[!UICONTROL Asunto]**, escriba un asunto para el recurso que desea compartir.

1. En el cuadro **[!UICONTROL Mensaje]**, escriba un mensaje opcional.

1. En el campo **[!UICONTROL Caducidad]**, especifique una fecha y hora de caducidad para que el vínculo deje de funcionar. El tiempo de caducidad predeterminado del vínculo es un día.

   ![Establecer fecha de caducidad para vínculo compartido](assets/Set-shared-link-expiration.png)

1. Para permitir que los usuarios descarguen el recurso original, seleccione **[!UICONTROL Permitir la descarga del archivo original]**. Para permitir que los usuarios descarguen solamente las representaciones de los recursos compartidos, seleccione **[!UICONTROL Permitir la descarga de representaciones de archivos]**.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios mediante un correo electrónico.

1. Para ver el recurso compartido, haga clic en el vínculo del correo electrónico que se envía al usuario. Para generar una vista previa del recurso, haga clic en el recurso compartido. Para cerrar la vista previa, haz clic en **[!UICONTROL Atrás]**. Si ha compartido una carpeta, haga clic en **[!UICONTROL Carpeta principal]** para volver a la carpeta principal.

   ![Vista previa del recurso compartido](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] admite la generación de la vista previa de recursos de solo [los tipos de archivo admitidos](/help/assets/assets-formats.md). Si se comparten otros tipos MIME, solo puede descargar los recursos y no puede obtener una vista previa.

1. Para descargar el recurso compartido, haz clic en **[!UICONTROL Seleccionar]** en la barra de herramientas, haz clic en el recurso y, a continuación, haz clic en **[!UICONTROL Descargar]** desde la barra de herramientas.

   ![Opción de barra de herramientas para descargar el recurso compartido](assets/chlimage_1-547.png)

1. Para ver los recursos que ha compartido como vínculos, vaya a la interfaz de usuario de [!DNL Assets] y haga clic en el logotipo de [!DNL Experience Manager]. Elija **[!UICONTROL Navegación]**. En el panel Navegación, elija **[!UICONTROL Vínculos compartidos]** para mostrar una lista de recursos compartidos.

1. Para dejar de compartir un recurso, selecciónelo y haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas. A continuación aparece un mensaje de confirmación. La entrada del recurso se eliminará de la lista.

## Configuración del servicio de correo Day CQ {#configure-day-cq-mail-service}

1. En la página principal de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la lista de servicios, busque **[!UICONTROL Day CQ Mail Service]**.
1. Haga clic en **[!UICONTROL Editar]** al lado del servicio y configure los siguientes parámetros para **[!UICONTROL Day CQ Mail Service]** con los detalles mencionados en relación con sus nombres:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario de SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña de SMTP: contraseña del servidor de correo electrónico

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Haga clic en **[!UICONTROL Guardar]**.

## Configurar el tamaño máximo de datos {#configure-maximum-data-size}

Cuando se descargan recursos desde el vínculo compartido mediante la característica de uso compartido de vínculos, [!DNL Experience Manager] comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, en ausencia de límites en la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos se someten a compresión, lo que provoca errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo con el parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]** para **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haz clic en el logotipo de [!DNL Experience Manager] y luego ve a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la consola web, busque la configuración **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Abra la configuración del servlet proxy **[!UICONTROL Day CQ DAM Adhoc Asset Share]** en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño de contenido máximo (sin comprimir)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Guarde los cambios.

## Prácticas recomendadas y solución de problemas {#best-practices-and-troubleshooting}

* Es posible que las carpetas de recursos o las colecciones que contienen un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, consulte con el administrador de [!DNL Experience Manager] cuáles son los [límites de descarga](#configure-maximum-data-size).
* Si no puede enviar correo electrónico con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte con su administrador de [!DNL Experience Manager] si el [servicio de correo electrónico](#configure-day-cq-mail-service) está configurado o no.
* Si no puede compartir recursos mediante la funcionalidad de uso compartido de vínculos, asegúrese de que tiene los permisos adecuados. Ver [compartir recursos](#share-assets).
* Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y a compartirlo con los usuarios.

* Si desea compartir vínculos de su implementación de autor de [!DNL Experience Manager] con entidades externas, asegúrese de exponer únicamente las siguientes direcciones URL que se usan para compartir vínculos, solo para solicitudes de `GET`. Bloquear otras direcciones URL por motivos de seguridad.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  En la interfaz de [!DNL Experience Manager], obtenga acceso a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Abra la configuración de **[!UICONTROL Day CQ Link Externalizer]** y modifique las siguientes propiedades en el campo **[!UICONTROL Dominios]** con los valores mencionados en `local`, `author` y `publish`. Para las propiedades `local` y `author`, proporcione la dirección URL para las instancias local y Author, respectivamente. Si ejecuta una sola instancia de autor de [!DNL Experience Manager], utilice el mismo valor para las propiedades `local` y `author`. Para instancias de publicación, proporcione la dirección URL de la instancia de publicación [!DNL Experience Manager].
