---
title: Configuración manual de la integración con Adobe Target
description: Obtenga información sobre cómo configurar manualmente la integración con Adobe Target.
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: a83de8a787f0e446d4d231fdffbf37a11dfd9c53
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 28%

---

# Configuración manual de la integración con Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Puede modificar las configuraciones del asistente de inclusión que realizó al utilizar el asistente o puede integrarlas manualmente con Adobe Target sin utilizar el asistente.

## Modificación de las configuraciones del asistente de Opt-In {#modifying-the-opt-in-wizard-configurations}

El [asistente de inclusión](/help/sites-administering/opt-in.md) que [integra AEM con Adobe Target](/help/sites-administering/target.md) crea automáticamente una configuración de nube de Target llamada Configuración de Target aprovisionada. El asistente también crea un marco de trabajo de Target para la configuración de nube denominada Marco de trabajo de Target aprovisionado. Si es necesario, puede modificar las propiedades de la configuración y el marco de trabajo de la nube.

También puede configurar Adobe Target para que utilice Adobe Target como fuente de informes al segmentar contenido. Para ello, configure la Configuración de Analytics Cloud de A4T.

Para localizar la configuración de la nube y el marco de trabajo, vaya a **Cloud Services** a través de **Herramientas** > **Implementación** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
Debajo de Adobe Target, haga clic en **Mostrar configuraciones**.

### Propiedades de configuración de Target aprovisionadas {#provisioned-target-configuration-properties}

Los siguientes valores de propiedad se utilizan en la configuración de nube de Configuración de Target aprovisionada que crea el asistente de inclusión:

* **Código de cliente:** tal como se especificó en el asistente de inclusión.
* **Correo electrónico:** Tal como se especificó en el asistente de inclusión.
* **Contraseña:** tal como se especificó en el asistente de inclusión.
* **Tipo de API:** REST
* **Sincronizar Segmentos De Adobe Target:** Seleccionados.

* **Biblioteca de cliente:** mbox.js.
* **Usar DTM para entregar la biblioteca de cliente:** No seleccionada. Seleccione esta opción si [usa DTM](/help/sites-administering/dtm.md) u otro sistema de administración de etiquetas para alojar el archivo mbox.js o AT.js. Adobe recomienda utilizar DTM en lugar de AEM para distribuir la biblioteca.

* **mbox.js personalizado:** Ninguno especificado para que se use el archivo mbox.js predeterminado. Especifique el archivo mbox.js personalizado que desee utilizar, según sea necesario. Solo aparece si ha seleccionado mbox.js.
* **AT.js personalizado:** Ninguno especificado para que se use el archivo AT.js predeterminado. Especifique un archivo AT.js personalizado que desee utilizar, según sea necesario. Solo aparece si ha seleccionado AT.js.

>[!NOTE]
>
>En AEM 6.3, puede seleccionar el archivo de la biblioteca de Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), que es una nueva biblioteca de implementación para Adobe Target diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página.
>
>AT.js ofrece varias mejoras con respecto a la biblioteca mbox.js:
>
>* Se han mejorado los tiempos de carga de las páginas en implementaciones web
>* Seguridad mejorada
>* Mejores opciones de implementación para aplicaciones de una sola página
>* AT.js contiene los componentes que se incluían en target.js, de modo que ya no se llama a target.

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Propiedades de Target Framework aprovisionadas {#provisioned-target-framework-properties}

El marco de trabajo de Target aprovisionado que crea el asistente de inclusión está configurado para enviar datos de contexto desde el almacén de datos de perfil. Los elementos de datos de edad y sexo del almacén se envían a Target de forma predeterminada. Es probable que la solución requiera que se envíen parámetros adicionales.

![Marco de destino aprovisionado](assets/chlimage_1-158.png)

Puede configurar el marco de trabajo para enviar información de contexto adicional a Target como se describe en [Agregar un marco de trabajo de Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configuración de A4T Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Puede configurar Adobe Target para que utilice Adobe Analytics como fuente de informes al segmentar contenido.

>[!NOTE]
>
>La autenticación de credencial de usuario (heredada) no funciona con A4T (tanto para Target como para Analytics). Como tal, los clientes deben utilizar la autenticación IMS en lugar de la autenticación de credencial de usuario.

Para ello, especifique con qué configuración de nube de A4T conectar su configuración de nube de Adobe Target:

1. Vaya a **Cloud Services** a través de **AEM logo** > **Herramientas** > **Implementación** > **Cloud Services**.
1. En la sección **Adobe Target**, haga clic en **Configurar ahora**.
1. Vuelva a conectarse a la configuración de Adobe Target.
1. En el menú desplegable **Configuración de Analytics Cloud de A4T**, seleccione el módulo.

   >[!NOTE]
   >
   >Solo están disponibles las configuraciones de análisis habilitadas para A4T.
   >
   >Al configurar A4T con AEM, es posible que vea una entrada que falta en Referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   >
   >1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya al [Cuadro de diálogo de configuración de A4T Analytics](#a4t-analytics-config-dialog) (ver a continuación)
   1. Establezca la propiedad **disable** a **false**.
   1. Haga clic en **Guardar todo**.

#### Cuadro de diálogo Configuración de A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Haga clic en **Aceptar**. Al segmentar contenido con Adobe Target, puede [seleccionar el origen del informe](/help/sites-authoring/content-targeting-touch.md).

## Integración manual con Adobe Target {#manually-integrating-with-adobe-target}

Integre manualmente con Adobe Target en lugar de utilizar el asistente de inclusión.

>[!NOTE]
>
El archivo de la biblioteca de Target [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/) es una nueva biblioteca de implementación para Adobe Target que está diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página. Adobe recomienda usar AT.js en lugar de mbox.js como biblioteca de cliente.
>
AT.js ofrece varias mejoras con respecto a la biblioteca mbox.js:
>
* Se han mejorado los tiempos de carga de las páginas en implementaciones web
* Seguridad mejorada
* Mejores opciones de implementación para aplicaciones de una sola página
* AT.js contiene los componentes que se incluían en target.js, de modo que ya no se llama a target.js
>
Puede seleccionar AT.js o mbox.js en el menú desplegable **Biblioteca de cliente**.

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Creación de una configuración de Target Cloud {#creating-a-target-cloud-configuration}

Para permitir que AEM interactúe con Adobe Target, cree una configuración de nube de Target. Para crear la configuración, proporcione el código de cliente de Adobe Target y las credenciales de usuario.

La configuración de la nube de Target solo se crea una vez porque se puede asociar con varias campañas de AEM. Si tiene varios códigos de cliente de Adobe Target, cree una configuración para cada código de cliente.

Puede configurar la configuración de nube para sincronizar segmentos desde Adobe Target. Si activa la sincronización, los segmentos se importan desde Target en segundo plano cuando se guarda la configuración de la nube.

Utilice el siguiente procedimiento para crear una configuración de nube de Target en AEM:

1. Vaya a **Cloud Services** a través de **AEM logo** > **Herramientas** > **Cloud Services** > **Cloud Services heredados**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Se abre la página de información general de **Cloud Services**.

1. En la sección **Adobe Target**, haga clic en **Configurar ahora**.
1. En el cuadro de diálogo **Crear configuración**:

   1. Asigne una configuración a **Título**.
   1. Seleccione la plantilla **Configuración de Adobe Target**.

      ![Configuración de Adobe Target](assets/adobe-target-create-configuration.png)

1. Haga clic en **Crear**.

   Se abre el cuadro de diálogo de edición.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   Al configurar A4T con AEM, es posible que vea una entrada que falta en Referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   >
   1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Establezca la propiedad **disable** a **false**.
   1. Haga clic en **Guardar todo**.

1. En el cuadro de diálogo, proporcione valores para estas propiedades.

   * **Código de cliente**: el código de cliente de la cuenta de Target
   * **Correo electrónico**: el correo electrónico de la cuenta de Target.
   * **Contraseña**: la contraseña de la cuenta de Target.
   * **Tipo de API**: REST o XML
   * **Configuración de Analytics Cloud de A4T**: seleccione la configuración de Analytics Cloud que se usa para las métricas y los objetivos de las actividades de Target. Necesita esta configuración si utiliza Adobe Analytics como fuente de informes al segmentar contenido. Si no ve la configuración de nube, consulte la nota en [Configuración de A4T Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Use objetivos precisos:** De forma predeterminada, esta casilla de verificación está seleccionada. Si se selecciona, la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Véase la nota siguiente.
   * **Sincronizar segmentos desde Adobe Target:** Seleccione esta opción para poder descargar los segmentos definidos en Target y utilizarlos en AEM. Seleccione esta opción cuando la propiedad Tipo de API sea REST, ya que los segmentos en línea no son compatibles y debe utilizar segmentos de Target. (El término de AEM de &quot;segmento&quot; equivale a la &quot;audiencia&quot; de Target).
   * **Biblioteca de cliente:** Seleccione si desea la biblioteca de cliente mbox.js o AT.js.
   * **Usar DTM para entregar la biblioteca de cliente**: seleccione esta opción para usar AT.js o mbox.js desde DTM u otro sistema de administración de etiquetas. Configure [la integración de DTM](/help/sites-administering/dtm.md) para usar esta opción. Adobe recomienda utilizar DTM en lugar de AEM para distribuir la biblioteca.
   * **mbox.js personalizado**: déjelo en blanco si marcó la casilla de la DTM o para usar el mbox.js predeterminado. También puede cargar su mbox.js personalizado. Solo aparece si ha seleccionado mbox.js.
   * **AT.js personalizado**: déjelo en blanco si marcó la casilla de DTM o para usar el AT.js predeterminado. También puede cargar su archivo AT.js personalizado. Solo aparece si ha seleccionado AT.js.

   >[!NOTE]
   >
   De forma predeterminada, al entrar en el asistente de configuración de Adobe Target, el direccionamiento preciso está habilitado.
   >
   El direccionamiento preciso significa que la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Como resultado, en términos de rendimiento, un direccionamiento preciso puede provocar un retraso de unos milisegundos antes de cargar el contenido.
   >
   El direccionamiento preciso siempre está habilitado en la instancia de autor. Sin embargo, en la instancia de publicación puede optar por desactivar el direccionamiento preciso globalmente, desactivando la marca de verificación junto al direccionamiento preciso en la configuración del servicio en la nube (**http://localhost:4502/etc/cloudservices.html**). También puede activar y desactivar el direccionamiento preciso para componentes individuales independientemente de la configuración del servicio en la nube.
   >
   Si ***ya*** ha creado componentes de destino y cambia esta configuración, los cambios no afectan a esos componentes. Cambie esos componentes directamente.

1. Haga clic en **Conectarse a Target** para inicializar la conexión con Target. Si la conexión se realiza correctamente, aparecerá el mensaje **Conexión correcta**. Haga clic en **OK** en el mensaje y, a continuación, **OK** en el cuadro de diálogo.

   Si no puede conectarse a Target, consulte la sección [solución de problemas](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Adición de un marco de trabajo de destino {#adding-a-target-framework}

Después de configurar la nube de Target, agregue un marco de trabajo de Target. El módulo identifica los parámetros predeterminados que se envían a Adobe Target desde los componentes [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) disponibles. Target usa los parámetros para determinar los segmentos que se aplican al contexto actual.

Puede crear varios marcos de trabajo para una sola configuración de Target. Los marcos de trabajo múltiples son útiles cuando debe enviar un conjunto diferente de parámetros a Target para diferentes secciones del sitio web. Cree un marco de trabajo para cada conjunto de parámetros que envíe. Asocie cada sección del sitio web con el marco de trabajo adecuado. Una página web solo puede utilizar un marco de trabajo a la vez.

1. En la página de configuración de Target, haga clic en **+** (signo más) junto a Marcos disponibles.
1. En el cuadro de diálogo Crear marco de trabajo, especifique un **Título**, seleccione **Adobe Target Framework** y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/chlimage_1-161.png)

   Se abre la página marco de trabajo. Sidekick proporciona componentes que representan información de [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) que puede asignar.

   ![Componentes para el módulo](assets/chlimage_1-162.png)

1. Arrastre el componente Client Context que representa los datos que desea utilizar para la asignación al destino de colocación. También puede arrastrar el componente **ContextHub Store** al marco de trabajo.

   >[!NOTE]
   >
   Al asignar, los parámetros se pasan a un mbox mediante cadenas simples. No se pueden asignar matrices desde ContextHub.

   Por ejemplo, para usar **Datos de perfil** acerca de los visitantes del sitio para controlar la campaña de Target, arrastre el componente **Datos de perfil** a la página. Aparecen las variables de datos de perfil disponibles para su asignación a parámetros de Target.

   ![Datos de perfil](assets/chlimage_1-163.png)

1. Seleccione las variables que desea que sean visibles para el sistema de Adobe Target seleccionando la casilla de verificación **Compartir** en las columnas correspondientes.

   ![Compartir](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   La sincronización de parámetros es solo de una manera, de AEM a Adobe Target.

Se crea el marco de trabajo. Para replicar el marco de trabajo en la instancia de publicación, utilice la opción **Activar marco de trabajo** de la barra de tareas.

### Asociación de actividades con la configuración de nube de Target  {#associating-activities-with-the-target-cloud-configuration}

Asocie sus [actividades de AEM](/help/sites-authoring/activitylib.md) con la configuración de la nube de Target para poder reflejar las actividades en [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
Los tipos de actividades estarán disponibles dependiendo de lo siguiente:
>
>
* Si la opción **xt_only** está habilitada en el inquilino de Adobe Target (clientcode) que se usa en AEM para conectarse a Adobe Target, puede crear **solo** actividades XT en AEM.
>
* Si la opción **xt_only** está habilitada para **not** en el inquilino de Adobe Target (clientcode), puede crear actividades **XT y A/B de** en AEM.
>
**Nota adicional:** La opción **xt_only** es una configuración aplicada a un determinado inquilino de Target (clientcode) y solo se puede modificar directamente en Adobe Target. No puede activar ni desactivar esta opción en AEM.

### Asociación del marco de trabajo de Target con el sitio {#associating-the-target-framework-with-your-site}

Después de crear un marco de trabajo de Target en AEM, asocie las páginas web al marco de trabajo. Los componentes de destino de las páginas envían los datos definidos por el marco de trabajo a Adobe Target para su seguimiento. (Consulte [Segmentación de contenido](/help/sites-authoring/content-targeting-touch.md).)

Cuando asocia una página con el marco de trabajo, las páginas secundarias heredan la asociación.

1. En la consola **Sitios**, desplácese hasta el sitio que desee configurar.
1. Con [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions) o [modo de selección](/help/sites-authoring/basic-handling.md), seleccione **Ver propiedades.**
1. Seleccione la pestaña **Cloud Services**.
1. Haga clic en **Editar**.
1. Haga clic en **Agregar configuración** en **Configuraciones de Cloud Service** y seleccione **Adobe Target**.

   ![Agregar configuración](assets/chlimage_1-165.png)

1. Seleccione el marco de trabajo que desee en **Referencia de configuración**.

   >[!NOTE]
   >
   Asegúrese de seleccionar el **framework** específico que creó y no la configuración de nube de Target en la que se creó.

1. Haga clic en **Listo**.
1. Active la página raíz del sitio web para replicarla en el servidor de publicación. (Consulte [Cómo Publicar Páginas](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   >
   Si el marco de trabajo adjunto a la página aún no se ha activado, se abre un asistente que también le permite publicarlo.

## Solución de problemas de conexión de Target {#troubleshooting-target-connection-problems}

Para solucionar los problemas que se producen al conectarse a Target, puede realizar las siguientes tareas:

* Asegúrese de que las credenciales de usuario que ha proporcionado son correctas.
* Asegúrese de que la instancia de AEM puede conectarse al servidor de Target. Por ejemplo, asegúrese de que las reglas del cortafuegos no bloquean las conexiones salientes de AEM o de que AEM está configurado para utilizar los proxies necesarios.
* Busque mensajes útiles en el registro de errores de AEM. El archivo error.log se encuentra en el directorio **crx-quickstart/logs** en el que está instalado AEM.
* Al editar la actividad en Adobe Target, la URL apunta a localhost. Solucione este problema estableciendo AEM Externalizer en la dirección URL correcta.
