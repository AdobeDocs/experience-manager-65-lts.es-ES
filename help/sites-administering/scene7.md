---
title: Integración de Adobe Experience Manager con Dynamic Media Classic
description: Obtenga información sobre cómo integrar Adobe Experience Manager con Dynamic Media Classic.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '5425'
ht-degree: 0%

---

# Integración de Adobe Experience Manager con Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic es una solución alojada para administrar, mejorar, publicar y distribuir recursos de medios enriquecidos en pantallas e impresiones web, móviles, de correo electrónico y conectadas a Internet.

Para utilizar Dynamic Media Classic, debe configurar la configuración de la nube para que Dynamic Media Classic y Adobe Experience Manager Assets puedan interactuar entre sí. Este documento describe cómo configurar Experience Manager y Dynamic Media Classic.

Para obtener información sobre cómo usar todos los componentes de Dynamic Media Classic en una página y trabajar con vídeo, consulte [Usar Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* La plataforma de visor DHTML de Dynamic Media Classic llegó oficialmente al final de su vida útil el 31 de enero de 2014. Para obtener más información, consulte las [preguntas frecuentes sobre la finalización de la vida útil del visor DHTML](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Antes de configurar Dynamic Media Classic para que funcione con Experience Manager, consulte [Prácticas recomendadas](#best-practices-for-integrating-scene-with-aem) para integrar Dynamic Media Classic con Experience Manager.
>* Si utiliza Dynamic Media Classic con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de Experience Manager utilizan las API 3.x y otras las API 4.x. 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) y 4.x con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>

## Integración de Experience Manager/Dynamic Media Classic y Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Los usuarios de Experience Manager pueden elegir entre dos soluciones para trabajar con Dynamic Media. Puede utilizar una de las siguientes opciones:

* Integre la instancia de Experience Manager con Dynamic Media Classic.
* Utilice Dynamic Media, que está integrado en Experience Manager.

Utilice los siguientes criterios para determinar qué solución elegir:

* ¿Es un cliente de Dynamic Media Classic **existente** cuyos recursos residen en Dynamic Media Classic para su publicación y envío, pero desea integrar esos recursos con la creación de Sites (WCM), o Experience Manager Assets, o ambos? Si es así, use la [integración punto a punto de Experience Manager/Dynamic Media Classic](#aem-scene-point-to-point-integration) que se describe en este documento.

* Si es un cliente de Experience Manager **new** que necesita distribución de medios enriquecidos, seleccione la opción [Dynamic Media](#aem-dynamic-media). Esta opción tiene mayor sentido si no tiene una cuenta de S7 existente y muchos recursos almacenados en ese sistema.

* En algunos casos, utilice ambas soluciones. El [escenario de doble uso](/help/sites-administering/scene7.md#dual-use-scenario) describe ese escenario.

### Integración punto a punto de Experience Manager/Dynamic Media Classic {#aem-scene-point-to-point-integration}

Al trabajar con recursos en esta solución, realice una de las siguientes acciones:

* Cargue los recursos directamente en Dynamic Media Classic y luego acceda a ellos a través del explorador de contenido **Dynamic Media Classic** para la creación de páginas o
* Cargue en Experience Manager Assets y, a continuación, habilite la publicación automática en Dynamic Media Classic; puede acceder a él a través del explorador de contenido **Assets** para la creación de páginas

Los componentes que usa para esta integración se encuentran en el área de componentes de **Dynamic Media Classic** en [Modo de diseño](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience Manager Dynamic Media es la unificación de funciones de Dynamic Media Classic directamente dentro de la plataforma de Experience Manager.

Cuando trabaje con recursos en esta solución, siga este flujo de trabajo:

1. Cargue recursos de imagen y vídeo únicos directamente en Experience Manager.
1. Codifique vídeos directamente en Experience Manager.
1. Cree conjuntos basados en imágenes directamente en Experience Manager.
1. Si procede, añada interactividad a imágenes o vídeos.

Los componentes que usa para Dynamic Media se encuentran en el área de componentes de **[!UICONTROL Dynamic Media]** en [modo de diseño](/help/sites-authoring/author-environment-tools.md#page-modes). Entre ellos se incluyen los siguientes:

* **[!UICONTROL Dynamic Media]**: el componente **[!UICONTROL Dynamic Media]** es inteligente; dependiendo de si agrega una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor es adaptable: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores de HTML5.

* **[!UICONTROL Medios interactivos]** - El componente **[!UICONTROL Medios interactivos]** es para recursos como banners de carrusel, imágenes interactivas y vídeo interactivo. Estos recursos tienen interactividad en ellos, como puntos interactivos o mapas de imagen. Este componente es inteligente. Es decir, dependiendo de si agrega una imagen o un vídeo, tiene varias opciones. Además, el visor es adaptable: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores de HTML5.

### Situación de doble uso {#dual-use-scenario}

De forma predeterminada, puede utilizar simultáneamente las funciones de integración de Dynamic Media y Dynamic Media Classic de Experience Manager. La siguiente tabla de casos de uso describe cuándo se activan y desactivan determinadas áreas.

Para usar Dynamic Media y Dynamic Media Classic simultáneamente:

1. Configurar [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) en Cloud Services.
1. Siga las instrucciones específicas específicas del caso de uso:

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Integración de Dynamic Media Classic</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>Si usted es ...</strong></td>
    <td><strong>Flujo de trabajo de casos de uso</strong></td>
    <td><strong>Imágenes/Vídeo</strong></td>
    <td><strong>Componente de Dynamic Media</strong></td>
    <td><strong>Explorador de contenido y componentes de S7</strong></td>
    <td><strong>Carga automática de Assets a S7</strong></td>
    </tr>
    <tr>
    <td>Novedades en Sites y Dynamic Media</td>
    <td>Cargue recursos en Experience Manager y utilice el componente Dynamic Media de Experience Manager para crear recursos en las páginas de Sites</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Al por menor, y nuevo en Sites y Dynamic Media</td>
    <td>Cargar recursos que no sean productos en Experience Manager para su administración y entrega. Cargue recursos de PRODUCTOS en Dynamic Media Classic y utilice el explorador de contenido de Dynamic Media Classic en Experience Manager y el componente para crear páginas de detalles de producto en los sitios.</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Novedades en Assets y Dynamic Media</td>
    <td>Cargue recursos en Experience Manager Assets y utilice el código incrustado/URL publicado desde Dynamic Media</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Novedades en Dynamic Media y plantillas</td>
    <td>Utilice Dynamic Media para imágenes y vídeo. Cree plantillas de imagen en Dynamic Media Classic y utilice el buscador de contenido de Dynamic Media Classic para incluir plantillas en las páginas de Sites.</td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">Activado</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente de Dynamic Media Classic existente y es nuevo en Sites</td>
    <td>Cargue recursos a Dynamic Media Classic y utilice el explorador de contenido Dynamic Media Classic de Experience Manager para buscar y crear recursos en las páginas de Sites</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td>Desactivado</td>
    </tr>
    <tr>
    <td>Un cliente de Dynamic Media Classic existente y son nuevos en Sites y Assets</td>
    <td>Cargue recursos en DAM y publique automáticamente en Dynamic Media Classic para su envío. Utilice el explorador de contenido de Experience Manager Dynamic Media Classic para buscar y crear recursos en páginas de Sites.</td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">Activado</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Consulte el paso 4)</p> </td>
    </tr>
    <tr>
    <td>Cliente existente de Dynamic Media Classic y nuevo en Assets</td>
    <td><p>Cargue recursos en Experience Manager y utilice Dynamic Media para generar representaciones para descargar o compartir. Publique automáticamente recursos de Experience Manager en Dynamic Media Classic para su envío.</p> <p><strong>Importante:</strong> incurre en procesamiento duplicado y las representaciones generadas en Experience Manager no se sincronizan con Dynamic Media Classic</p> </td>
    <td><p>Activado</p> <p>(Consulte el paso 3)</p> </td>
    <td>Desactivado</td>
    <td>Desactivado</td>
    <td><p><a href="#configuringautouploadingfromaemassets">Activado</a></p> <p>(Consulte el paso 4)</p> </td>
    </tr>
    </tbody>
    </table>

1. (Opcional; consulte la tabla de casos de uso): configure la [configuración de la nube de Dynamic Media](/help/assets/config-dynamic.md) y [habilite el servidor de Dynamic Media](/help/assets/config-dynamic.md).
1. (Opcional; consulte la tabla de casos de uso): si decide habilitar la carga automática desde Assets a Dynamic Media Classic, debe añadir lo siguiente:

   1. Configure la carga automática en Dynamic Media Classic.
   1. Agregue el paso **Carga de Dynamic Media Classic** después de todos los pasos del flujo de trabajo de Dynamic Media *al final del flujo de trabajo* **Recurso de actualización Dam** ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Opcional) Restrinja la carga de recursos de Dynamic Media Classic por tipo MIME en [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). Los tipos MIME de recursos que no están en esta lista no se cargan en el servidor de Dynamic Media Classic.
   1. (Opcional) Configure el vídeo en la configuración de Dynamic Media Classic. Puede habilitar la codificación de vídeo para Dynamic Media y Dynamic Media Classic simultáneamente, o para ambos. Las representaciones dinámicas se utilizan para la previsualización y reproducción locales en Experience Manager, mientras que las representaciones de vídeo de Dynamic Media Classic se generan y almacenan en servidores de Dynamic Media Classic. Al configurar los servicios de codificación de vídeo para Dynamic Media y Dynamic Media Classic, aplique un [perfil de procesamiento de vídeo](/help/assets/video-profiles.md) a la carpeta de recursos de Dynamic Media Classic.
   1. (Opcional) [Configuración de la vista previa segura en Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### Limitaciones {#limitations}

Cuando tiene habilitados tanto Dynamic Media Classic como Dynamic Media, existen las siguientes limitaciones:

* La carga manual en Dynamic Media Classic al seleccionar un recurso y arrastrarlo a un componente de Dynamic Media Classic en una página de Experience Manager no funciona.
* Aunque los recursos sincronizados de Experience Manager y Dynamic Media Classic se actualizan automáticamente en Dynamic Media Classic cuando el recurso se edita en Assets, una acción de reversión no almacena en déclencheur una nueva carga. Como tal, Dynamic Media Classic no obtiene la versión más reciente inmediatamente después de una reversión. La solución consiste en volver a editar una vez completada la reversión.
* ¿Es necesario utilizar Dynamic Media para un caso de uso e integración de Dynamic Media Classic para otro para que los recursos de Dynamic Media no interactúen con el sistema de Dynamic Media Classic? Si es así, no aplique la configuración de Dynamic Media Classic a la carpeta Dynamic Media. Tampoco aplique la configuración de Dynamic Media (perfil de procesamiento) a una carpeta de Dynamic Media Classic.

## Prácticas recomendadas para integrar Dynamic Media Classic con Experience Manager {#best-practices-for-integrating-scene-with-aem}

Al integrar Dynamic Media Classic con Experience Manager, hay algunas prácticas recomendadas importantes que deben tenerse en cuenta en las siguientes áreas:

* Prueba de conducción de la integración
* Se recomienda cargar recursos directamente desde Dynamic Media Classic para determinadas situaciones

Ver [limitaciones conocidas](#known-limitations-and-design-implications).

### Pruebe y controle su integración {#test-driving-your-integration}

Adobe recomienda probar la integración haciendo que la carpeta raíz apunte únicamente a una subcarpeta, en lugar de a toda una compañía.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía de Dynamic Media Classic existente puede tardar mucho tiempo en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos (por ejemplo, la carpeta raíz suele tener demasiados recursos y puede bloquear el sistema).

### Carga de recursos desde Experience Manager Assets frente a desde Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}

Puede cargar recursos mediante la funcionalidad Assets (administración de recursos digitales) o accediendo a Dynamic Media Classic directamente en Experience Manager a través del explorador de contenido de Dynamic Media Classic. La elección de la opción dependerá de los siguientes factores:

* Los tipos de recursos de Dynamic Media Classic que Experience Manager Assets aún no admite deben agregarse a un sitio web de Experience Manager directamente desde Dynamic Media Classic, a través del explorador de contenido de Dynamic Media Classic. Por ejemplo, plantillas de imagen.
* Para los tipos de recursos compatibles con Experience Manager Assets y Dynamic Media Classic, la decisión de cómo cargarlos depende de lo siguiente:

   * Dónde se encuentran los recursos hoy Y
   * La importancia de administrarlos en un repositorio común

Supongamos que los recursos ya están en Dynamic Media Classic y que administrarlos en un repositorio común no es importante. En ese caso, la exportación de los recursos a Experience Manager Assets solo para sincronizarlos de nuevo con Dynamic Media Classic para su entrega es una ida y vuelta innecesaria. Adobe recomienda mantener los recursos en un único repositorio y sincronizarlos con Dynamic Media Classic solo para su envío.

## Configuración de la integración con Dynamic Media Classic {#configuring-scene-integration}

Puede configurar Experience Manager para que cargue recursos en Dynamic Media Classic. Assets desde una carpeta de destino CQ se puede cargar (automática o manualmente) desde Experience Manager a una cuenta de empresa de Dynamic Media Classic.

>[!NOTE]
>
>Adobe recomienda utilizar únicamente la carpeta de destino designada para importar recursos de Dynamic Media Classic. Los recursos digitales que residen fuera de la carpeta de destino solo se pueden utilizar en componentes de Dynamic Media Classic en páginas en las que se haya habilitado la configuración de Dynamic Media Classic. Además, se colocan en una carpeta bajo demanda en Dynamic Media Classic. La carpeta bajo demanda no está sincronizada con Experience Manager (pero los recursos se pueden detectar en el explorador de contenido de Dynamic Media Classic).

**Para configurar la integración de Dynamic Media Classic con Experience Manager:**

1. [Definir una configuración de nube](#creating-a-cloud-configuration-for-scene): define la asignación entre una carpeta Dynamic Media Classic y una carpeta Assets. Complete este paso aunque solo desee una sincronización unidireccional (de Experience Manager Assets a Dynamic Media Classic).
1. [Habilitar el **Receptor Dam de Adobe CQ s7dam**](#enabling-the-adobe-cq-scene-dam-listener) - Listo en la consola [!UICONTROL OSGi].
1. Si desea que Experience Manager Assets se cargue automáticamente en Dynamic Media Classic, debe activar esa opción y agregar Dynamic Media Classic al flujo de trabajo [!UICONTROL DAM Update Asset]. También puede cargar recursos manualmente.
1. Añadir componentes de Dynamic Media Classic a la barra de tareas. Esta funcionalidad permite a los usuarios utilizar componentes de Dynamic Media Classic en sus páginas de Experience Manager.
1. [Asigne la configuración a la página en Experience Manager](#enabling-scene-for-wcm). Este paso es necesario para ver cualquier ajuste preestablecido de vídeo que haya creado en Dynamic Media Classic. También es necesario si debe publicar un recurso desde fuera de la carpeta de destino de CQ en Dynamic Media Classic.

En esta sección se explica cómo realizar todos estos pasos y se enumeran las limitaciones importantes.

### Funcionamiento de la sincronización entre Dynamic Media Classic y Experience Manager Assets {#how-synchronization-between-scene-and-aem-assets-works}

Al configurar la sincronización de Experience Manager Assets y Dynamic Media Classic, es importante comprender lo siguiente:

#### Cargar en Dynamic Media Classic desde Experience Manager Assets {#uploading-to-scene-from-aem-assets}

* Hay una carpeta de sincronización designada en Experience Manager para las cargas de Dynamic Media Classic.
* Las cargas a Dynamic Media Classic se pueden automatizar si los recursos digitales se colocan en la carpeta de sincronización designada.
* La estructura de carpetas y subcarpetas de Experience Manager se duplica en Dynamic Media Classic.

>[!NOTE]
>
>Experience Manager incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic as a XMP.

#### Limitaciones conocidas e implicaciones de diseño {#known-limitations-and-design-implications}

Con la sincronización entre Experience Manager Assets y Dynamic Media Classic, actualmente existen las siguientes limitaciones o implicaciones de diseño:

<table>
 <tbody>
  <tr>
   <td><strong>Implicación de limitación/diseño</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Una carpeta de sincronización designada (destino)</td>
   <td>Solo puede tener una carpeta designada por compañía en Experience Manager para cargas de Dynamic Media Classic. Puede crear varias configuraciones si necesita tener acceso a más de una cuenta de compañía en Dynamic Media Classic.</td>
  </tr>
  <tr>
   <td>Estructura de carpetas</td>
   <td>Si elimina una carpeta sincronizada con recursos, se eliminarán todos los recursos remotos de Dynamic Media Classic, pero la carpeta permanecerá.</td>
  </tr>
  <tr>
   <td>Carpeta bajo demanda</td>
   <td>Los Assets que residen fuera de la carpeta de destino y que se cargan manualmente en Dynamic Media Classic en WCM se colocan automáticamente en una carpeta bajo demanda independiente en Dynamic Media Classic. Puede configurar esta carpeta en la configuración de nube de Experience Manager.</td>
  </tr>
  <tr>
   <td>Medios mixtos</td>
   <td>Los conjuntos de medios mixtos aparecen en Experience Manager, aunque no son compatibles con Experience Manager.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Los PDF generados a partir de catálogos electrónicos en Dynamic Media Classic se importan en la carpeta de destino CQ.</td>
  </tr>
  <tr>
   <td>Actualización de IU</td>
   <td>Al sincronizar entre Experience Manager y Dynamic Media Classic, asegúrese de actualizar la interfaz de usuario para ver los cambios. </td>
  </tr>
  <tr>
   <td>Miniaturas de vídeo</td>
   <td>Si carga un vídeo en Experience Manager Assets para codificarlo mediante Dynamic Media Classic, las miniaturas de vídeo y los vídeos codificados pueden tardar algún tiempo en estar disponibles en Experience Manager Assets, según el tiempo de procesamiento del vídeo.</td>
  </tr>
  <tr>
   <td>Subcarpetas de destino</td>
   <td><p>Si utiliza subcarpetas dentro de la carpeta de destino, asegúrese de utilizar nombres únicos para cada recurso (independientemente de la ubicación). Además, asegúrese de configurar Dynamic Media Classic (en el área Configuración ) para que no sobrescriba recursos, independientemente de la ubicación.</p> <p>De lo contrario, se cargan los recursos con el mismo nombre que se cargan en una subcarpeta de destino de Dynamic Media Classic, pero se elimina el recurso con el mismo nombre de la carpeta de destino. </p> </td>
  </tr>
 </tbody>
</table>

### Configuración de servidores de Dynamic Media Classic {#configuring-scene-servers}

Si ejecuta Experience Manager detrás de un proxy o tiene una configuración especial de cortafuegos, debe activar de forma explícita los hosts de las distintas regiones. Los servidores se administran en el contenido de `/etc/cloudservices/scene7/endpoints` y se pueden personalizar según sea necesario. Seleccione una dirección URL y, a continuación, edite para cambiarla, si es necesario. En versiones anteriores de Experience Manager, estos valores estaban codificados.

Si va a `/etc/cloudservices/scene7/endpoints.html`, verá los servidores en la lista (y podrá editarlos tocando la dirección URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Cree una configuración de nube para Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}

Una configuración de nube define la asignación entre una carpeta de Dynamic Media Classic y una carpeta de Experience Manager Assets. Debe configurarse para sincronizar Experience Manager Assets con Dynamic Media Classic. Consulte Funcionamiento de la sincronización para obtener más información.

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía de Dynamic Media Classic existente puede tardar mucho tiempo en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos. Por ejemplo, la carpeta raíz suele tener demasiados recursos.
>
>Si desea probar la integración, haga que la carpeta raíz apunte únicamente a una subcarpeta, en lugar de a toda la compañía.

>[!NOTE]
>
>Puede tener varias configuraciones: una configuración de nube representa a un usuario en una compañía de Dynamic Media Classic. Si desea acceder a otras empresas o usuarios de Dynamic Media Classic, debe crear varias configuraciones.

**Para crear una configuración de nube para Dynamic Media Classic:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]** para poder acceder a Adobe Dynamic Media Classic.

1. Seleccione **[!UICONTROL Configurar ahora]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. En el campo **[!UICONTROL Título]** y, opcionalmente, en el campo **[!UICONTROL Nombre]**, escriba la información adecuada. Seleccione **[!UICONTROL Crear]**.

   >[!NOTE]
   >
   >Al crear más configuraciones, se muestra el campo **[!UICONTROL configuración principal]**.
   >
   >**no** cambia la configuración principal. Si cambia la configuración principal, se puede interrumpir la integración.

1. Escriba la dirección de correo electrónico, la contraseña y la región de su cuenta de Dynamic Media Classic y seleccione **[!UICONTROL Conectarse a Dynamic Media Classic]**. Está conectado al servidor de Dynamic Media Classic y el cuadro de diálogo se amplía con más opciones.

1. Escriba el nombre de **[!UICONTROL Compañía]** y **[!UICONTROL Ruta raíz]**. Esta información es el nombre del servidor publicado junto con la ruta de acceso que desee especificar. Si no conoce el nombre del servidor publicado, vaya a **[!UICONTROL Configuración > Configuración de aplicación]** en Dynamic Media Classic.

   >[!NOTE]
   >
   >La ruta raíz de Dynamic Media Classic es la carpeta de Dynamic Media Classic a la que se conecta Experience Manager. Se puede reducir a una carpeta específica.

   >[!CAUTION]
   >
   >Según el tamaño de la carpeta Dynamic Media Classic, la importación de una carpeta raíz puede llevar mucho tiempo. Además, los datos de Dynamic Media Classic podrían superar el almacenamiento de Experience Manager. Asegúrese de importar la carpeta correcta. La importación de demasiados datos puede detener el sistema.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. Seleccione **[!UICONTROL Aceptar]**. Experience Manager guarda la configuración.

>[!NOTE]
>
>Si va a volver a conectar:
>
>* Al volver a conectarse a Dynamic Media Classic en la publicación, restablecer la contraseña al publicar o volver a conectar no funciona (no es un problema en la instancia de autor).
>* Si modifica valores como la región o el nombre de la empresa, debe volver a conectarse a Dynamic Media Classic. Si las opciones de configuración se han modificado pero no se han guardado, Experience Manager indica erróneamente que la configuración es válida. Asegúrese de volver a conectar.
>

### Habilitar el Adobe CQ Dynamic Media Classic Dam Listener {#enabling-the-adobe-cq-scene-dam-listener}

Habilite el Adobe CQ Dynamic Media Classic Dam Listener, que está deshabilitado de forma predeterminada.

**Para habilitar el Receptor Dam de Adobe CQ Dynamic Media Classic:**

1. Seleccione el icono [!UICONTROL Herramientas] y luego vaya a **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la consola web, vaya a **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** y active la casilla de verificación **[!UICONTROL Habilitado]**.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Seleccione **[!UICONTROL Guardar]**.

### Añadir tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic {#adding-configurable-timeout-to-scene-upload-workflow}

Cuando se configura una instancia de Experience Manager para que gestione la codificación de vídeo a través de Dynamic Media Classic, de forma predeterminada se agota el tiempo de espera de 35 minutos en cualquier trabajo de carga. Para dar cabida a los trabajos de codificación de vídeo de ejecución más prolongada, puede configurar esta opción.

1. Vaya a **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. Cambie el número como desee en el campo **[!UICONTROL Tiempo de espera del trabajo activo]**. Se acepta cualquier número no negativo con la unidad de medida en segundos. De forma predeterminada, este número se establece en 2100.

   >[!NOTE]
   >
   >Práctica recomendada: La mayoría de los recursos se incorporan en cuestión de minutos como máximo (por ejemplo, imágenes). Sin embargo, en algunos casos (por ejemplo, en vídeos de mayor tamaño), aumenta el valor de tiempo de espera a 7200 segundos (dos horas) para adaptarse a un tiempo de procesamiento largo. De lo contrario, este trabajo de carga de Dynamic Media Classic se marcará como **[!UICONTROL UploadFailed]** en los metadatos JCR (repositorio de contenido Java™).

1. Seleccione **[!UICONTROL Guardar]**.

### Carga automática desde Experience Manager Assets {#autouploading-from-aem-assets}

A partir de Experience Manager 6.3.2, Experience Manager Assets se configura de modo que los recursos digitales cargados se actualicen en Dynamic Media Classic si se encuentran en una carpeta de destino CQ.

Cuando se añade un recurso a Experience Manager Assets, se carga y publica automáticamente en Dynamic Media Classic.

>[!NOTE]
>
>El tamaño máximo de archivo para la carga automática de Experience Manager Assets a Dynamic Media Classic es de 500 MB.

**Para cargar automáticamente desde Experience Manager Assets:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. Bajo el encabezado Dynamic Media, en Configuraciones disponibles, seleccione **[!UICONTROL dms7 (Dynamic Media]**).
1. Seleccione la ficha **[!UICONTROL Avanzado]**, active la casilla de verificación **[!UICONTROL Habilitar carga automática]** y, a continuación, seleccione **[!UICONTROL Aceptar]**. Configure el flujo de trabajo de recursos DAM para incluir la carga en Dynamic Media Classic.

   >[!NOTE]
   >
   >Consulte [Configuración del estado (publicado/no publicado) de los recursos insertados en Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) para obtener información sobre cómo insertar recursos en Dynamic Media Classic en estado no publicado.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Vuelva a la página de bienvenida de Experience Manager y seleccione **[!UICONTROL Flujos de trabajo]**. Haga doble clic en el flujo de trabajo **DAM Update Asset** para que se abra.
1. En la barra de tareas, vaya a los componentes de **[!UICONTROL Flujo de trabajo]** y seleccione **[!UICONTROL Dynamic Media Classic]**. Arrastre **[!UICONTROL Dynamic Media Classic]** al flujo de trabajo y seleccione **[!UICONTROL Guardar]**. Los Assets que se agreguen a Experience Manager Assets en la carpeta de destino se cargan automáticamente en Dynamic Media Classic.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* Al añadir recursos después de la automatización, si no se colocan en la carpeta de destino de CQ, no se cargan en Dynamic Media Classic.
   >* Experience Manager incrusta todos los metadatos como XMP antes de cargarlos en Dynamic Media Classic, por lo que todas las propiedades del nodo de metadatos están disponibles en Dynamic Media Classic as a XMP.

### Configuración del estado (publicado/no publicado) de los recursos insertados en Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Si está insertando recursos de Experience Manager Assets en Dynamic Media Classic, puede publicarlos automáticamente (comportamiento predeterminado) o insertarlos en Dynamic Media Classic en un estado sin publicar.

Es posible que no desee publicar los recursos inmediatamente en Dynamic Media Classic si desea probarlos en un entorno de ensayo antes de publicarlos. Puede utilizar Experience Manager con el entorno de prueba segura de Dynamic Media Classic para insertar recursos directamente desde Assets en Dynamic Media Classic en un estado sin publicar.

Los recursos de Dynamic Media Classic siguen estando disponibles a través de una previsualización segura. Solo cuando los recursos se publican en Experience Manager, los recursos de Dynamic Media Classic también se activan en la producción.

Si desea publicar recursos inmediatamente al insertarlos en Dynamic Media Classic, no es necesario configurar ninguna opción. Esta funcionalidad es el comportamiento predeterminado.

Sin embargo, si no desea que los recursos insertados en Dynamic Media Classic se publiquen automáticamente, en esta sección se describe cómo configurar Experience Manager y Dynamic Media Classic para que realicen esta funcionalidad.

#### Requisitos previos para insertar recursos en Dynamic Media Classic sin publicar {#prerequisites-to-push-assets-to-scene-unpublished}

Para poder insertar recursos en Dynamic Media Classic sin publicarlos, debe configurar lo siguiente:

1. [Use Admin Console para crear un caso de soporte](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). En su caso de asistencia, solicite la activación de la previsualización segura para su cuenta de Dynamic Media Classic.
1. [Configure la vista previa segura para su cuenta de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=es).

Estos pasos son los mismos que seguiría para crear cualquier configuración de prueba segura en Dynamic Media Classic.

>[!NOTE]
>
>Si el entorno de instalación es un sistema operativo UNIX® de 64 bits, consulte [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) con respecto a otras opciones de configuración que debe establecer.

#### Limitaciones conocidas para insertar recursos en estado sin publicar  {#known-limitations-for-pushing-assets-in-unpublished-state}

Si utiliza esta función, tenga en cuenta las siguientes limitaciones:

* No se admite el control de versiones.
* Si un recurso ya se ha publicado en Experience Manager y se crea una versión posterior, esa nueva versión se publica inmediatamente en producción. La publicación tras la activación solo funciona con la publicación inicial de un recurso.

>[!NOTE]
>
>Si desea publicar recursos al instante, se recomienda mantener **[!UICONTROL Habilitar vista previa segura]** establecido en **[!UICONTROL Inmediatamente]** y usar la característica **[!UICONTROL Habilitar carga automática]**.

### Definir el estado de los recursos insertados en Dynamic Media Classic como sin publicar {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>Si un usuario publica el recurso en Experience Manager, déclencheur automáticamente el recurso S7 en el recurso de producción/activo (el recurso ya no está en previsualización segura/sin publicar).

**Para establecer el estado de los recursos insertados en Dynamic Media Classic como no publicados:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Seleccione la pestaña **[!UICONTROL Avanzadas]**.
1. En el menú desplegable **[!UICONTROL Habilitar vista segura]**, seleccione **[!UICONTROL Tras la activación de publicación de AEM]** para insertar los recursos en Dynamic Media Classic sin publicarlos. (De manera predeterminada, este valor se establece en **[!UICONTROL Inmediatamente]**, donde los recursos de Dynamic Media Classic se publican inmediatamente).

   Consulte [Documentación de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=es) para obtener más información sobre cómo probar recursos antes de publicarlos.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. Seleccione **[!UICONTROL Aceptar]**.

Habilitar la vista previa segura significa que los recursos se insertan en el servidor de vista previa segura y se cancela su publicación.

Para ver si **[!UICONTROL Vista previa segura]** está habilitada, ve a un componente de Dynamic Media Classic en una página de Experience Manager. Seleccione **[!UICONTROL Editar]**. El recurso tiene el servidor de previsualización segura enumerado en la dirección URL. Después de publicar en Experience Manager, el dominio del servidor en la referencia de archivo se actualiza de la URL de vista previa a la URL de producción.

### Habilitar Dynamic Media Classic para WCM {#enabling-scene-for-wcm}

Habilitar Dynamic Media Classic para WCM es necesario por dos motivos:

* Habilita la lista desplegable de perfiles de vídeo universales para la creación de páginas. Sin esta lista, la lista desplegable **[!UICONTROL Ajuste preestablecido de vídeo universal]** está vacía y no se puede establecer.
* Si un recurso digital no está en la carpeta de destino, puede cargarlo en Dynamic Media Classic si habilita Dynamic Media Classic para esa página en las propiedades de página. A continuación, arrastre y suelte el recurso en un componente de Dynamic Media Classic. Se aplican reglas de herencia normales (lo que significa que las páginas secundarias heredan la configuración de la página principal).

Al habilitar Dynamic Media Classic para WCM, como con otras configuraciones, se aplican reglas de herencia. Puede habilitar Dynamic Media Classic para WCM en la interfaz de usuario táctil o clásica.

#### Habilitar Dynamic Media Classic para WCM en la interfaz de usuario táctil optimizada {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Seleccione el icono de Experience Manager, vaya a **[!UICONTROL Sites]** y luego a la página raíz del sitio web (no específico del idioma).

1. En la barra de herramientas, seleccione el icono [!UICONTROL settings] y seleccione **[!UICONTROL Abrir propiedades]**.

1. Seleccione **[!UICONTROL Cloud Services]**, **[!UICONTROL Agregar configuración]** y **[!UICONTROL Dynamic Media Classic]**.
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración que desee y seleccione **[!UICONTROL Aceptar]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en Experience Manager con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

#### Habilitar Dynamic Media Classic para WCM en la interfaz de usuario clásica {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. En Experience Manager, seleccione **[!UICONTROL Sitios web]** y vaya a la página raíz del sitio web (no específica del idioma).

1. En la barra de tareas, seleccione el icono **[!UICONTROL Página]** y seleccione **[!UICONTROL Propiedades de página]**.

1. Seleccione **[!UICONTROL Cloud Services]** > **[!UICONTROL Agregar servicios]** > **[!UICONTROL Dynamic Media Classic]**.
1. En la lista desplegable **[!UICONTROL Adobe Dynamic Media Classic]**, seleccione la configuración que desee y seleccione **[!UICONTROL Aceptar]**.

   Los ajustes preestablecidos de vídeo de esa configuración de Dynamic Media Classic están disponibles para su uso en Experience Manager con el componente de vídeo de Dynamic Media Classic en esa página y en las páginas secundarias.

### Configurar una configuración predeterminada {#configuring-a-default-configuration}

Si tiene varias configuraciones de Dynamic Media Classic, puede especificar una de ellas como predeterminada para el explorador de contenido de Dynamic Media Classic.

Solo se puede marcar una configuración de Dynamic Media Classic como predeterminada en un momento determinado. La configuración predeterminada son los recursos de la empresa que se muestran de forma predeterminada en el Explorador de contenido de Dynamic Media Classic.

**Para configurar una configuración predeterminada:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Para abrir la configuración, seleccione **[!UICONTROL Editar]**.

1. En la ficha **[!UICONTROL General]**, active la casilla de verificación **[!UICONTROL Configuración predeterminada]** para que sea la compañía y la ruta de acceso raíz predeterminadas que aparecen en el explorador de contenido de Dynamic Media Classic.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >Si solo hay una configuración, seleccionar la casilla de verificación **[!UICONTROL Configuración predeterminada]** no tiene ningún efecto.

### Configuración de la carpeta Ad hoc {#configuring-the-ad-hoc-folder}

Puede configurar la carpeta bajo demanda en la que se cargan los recursos en Dynamic Media Classic cuando el recurso no está en la carpeta de destino CQ. Consulte Publicación de recursos desde fuera de la carpeta de destino de CQ.

**Para configurar la carpeta Ad hoc:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. Seleccione **[!UICONTROL Dynamic Media Classic]**.
1. Seleccione la configuración en Dynamic Media Classic.
1. Para abrir la configuración, seleccione **[!UICONTROL Editar]**.

1. Seleccione la ficha **[!UICONTROL Avanzadas]**. En el campo **[!UICONTROL Carpeta ad hoc]**, puede modificar la carpeta **Ad hoc**. De manera predeterminada, es el **nombre_de_la_compañía/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### Configurar ajustes preestablecidos de vídeo universales {#configuring-universal-presets}

Para configurar los ajustes preestablecidos de vídeo universales para el componente de vídeo, consulte [Vídeo](/help/assets/s7-video.md).

## Habilitar compatibilidad con parámetros de trabajo de carga de Assets/Dynamic Media Classic basados en tipos MIME {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Puede habilitar parámetros configurables de trabajos de carga de Dynamic Media Classic que se activan mediante la sincronización de recursos de Digital Asset Manager/Dynamic Media Classic.

Concretamente, puede configurar el formato de archivo aceptado por tipo MIME en el área OSGi (Open Service Gateway initiative) del panel Configuración de la consola web de Experience Manager. A continuación, puede personalizar los parámetros de trabajo de carga individuales que se utilizan para cada tipo MIME en el repositorio de contenido JCR (Java™).

**Para habilitar recursos basados en tipos MIME:**

1. Seleccione el icono de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En el panel Configuración de la consola web de Adobe Experience Manager, en el menú **[!UICONTROL OSGi]**, seleccione **[!UICONTROL Configuración]**.
1. En la columna Nombre, busque y seleccione **[!UICONTROL Servicio MIME de tipo de recurso de Adobe CQ Dynamic Media Classic]** para editar la configuración.
1. En el área Asignación de tipo MIME, seleccione cualquier signo más (+) para agregar un tipo MIME.

   Consulte [Tipos MIME admitidos](/help/assets/assets-formats.md#supported-mime-types).

1. En el campo de texto, escriba el nuevo nombre del tipo MIME.

   Por ejemplo, escribiría `<file_extension>=<mime_type>` como en `EPS=application/postscript` O `PSD=image/vnd.adobe.photoshop`.

1. En la esquina inferior derecha de la ventana de configuración, seleccione **[!UICONTROL Guardar]**.
1. Vuelva a Experience Manager y, en el carril izquierdo, seleccione **[!UICONTROL CRXDE Lite]**.
1. En la página de CRXDE Lite, en el carril izquierdo, vaya a `/etc/cloudservices/scene7/<environment>` (sustituya `<environment>` por el nombre real).
1. Expanda `<environment>` (sustituya `<environment>` por el nombre real) para mostrar el nodo `mimeTypes`.
1. Seleccione el mimeType que acaba de añadir.

   Por ejemplo, `mimeTypes > application_postscript` O `mimeTypes > image_vnd.adobe.photoshop`.

1. En el lado derecho de la página de CRXDE Lite, seleccione la pestaña **[!UICONTROL Propiedades]**.
1. Especifique un parámetro de trabajo de carga de Dynamic Media Classic en el campo de valor **[!UICONTROL jobParam]**.

   Por ejemplo, `psprocess="rasterize"&psresolution=120`.

   Consulte la [API del sistema de producción de imágenes de Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html?lang=es) para obtener más parámetros de trabajo de carga que pueda usar.

   >[!NOTE]
   >
   >Si está cargando archivos PSD y desea procesarlos como plantillas con extracciones de capas, introduzca lo siguiente en el campo de valor **[!UICONTROL jobParam]**:
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >Asegúrese de que el archivo PSD tenga &quot;capas&quot;. Si es estrictamente una imagen o una imagen con máscara, se procesa como imagen porque no hay capas que procesar.

1. En la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

## Solución de problemas de integración de Dynamic Media Classic y Experience Manager {#troubleshooting-scene-and-aem-integration}

Si tiene problemas para integrar Experience Manager con Dynamic Media Classic, consulte los siguientes escenarios para obtener soluciones.

**Si falla la publicación de recursos digitales en Dynamic Media Classic:**

* Compruebe que el recurso que está cargando esté en la carpeta **[!UICONTROL CQ target]** (especifique esta carpeta en la configuración de nube de Dynamic Media Classic).
* Si no es así, debe configurar la configuración de nube en **[!UICONTROL Propiedades de página]** para esa página a fin de permitir la carga en la carpeta **[!UICONTROL CQ ad hoc]**.

* Compruebe los registros para obtener cualquier información.

**Si no aparecen los ajustes preestablecidos de vídeo:**

* Asegúrese de haber configurado la configuración de nube de esa página mediante **[!UICONTROL Propiedades de página]**. Los ajustes preestablecidos de vídeo están disponibles en el componente de vídeo de Dynamic Media Classic.

**Si los recursos de vídeo no se reproducen en Experience Manager:**

* Asegúrese de que ha utilizado el componente de vídeo correcto. El componente de vídeo de Dynamic Media Classic es diferente del componente de vídeo base. Consulte [Componente de vídeo base frente a Componente de vídeo Dynamic Media Classic](/help/assets/s7-video.md).

**Si los recursos nuevos o modificados en Experience Manager no se cargan automáticamente en Dynamic Media Classic:**

* Asegúrese de que los recursos estén en la carpeta de destino de CQ. Solo se actualizan automáticamente los recursos que se encuentran en la carpeta de destino de CQ (siempre que haya configurado Experience Manager Assets para que cargue recursos automáticamente).
* Asegúrese de haber configurado Cloud Services para Habilitar la carga automática y de haber actualizado y guardado el flujo de trabajo de recursos DAM para incluir la carga de Dynamic Media Classic.
* Al cargar una imagen en una subcarpeta de la carpeta de destino de Dynamic Media Classic, asegúrese de realizar una de las siguientes acciones:

   * Asegúrese de que los nombres de todos los recursos, independientemente de la ubicación, sean únicos. De lo contrario, el recurso de la carpeta de destino principal se eliminará y solo permanecerá el recurso de la subcarpeta.
   * Cambie cómo Dynamic Media Classic sobrescribe los recursos en el área Configuración de la cuenta de Dynamic Media Classic. No configure Dynamic Media Classic para que sobrescriba recursos independientemente de la ubicación si utiliza recursos con el mismo nombre en subcarpetas.

**Si las carpetas o los recursos eliminados no están sincronizados entre Dynamic Media Classic y Experience Manager:**

* Assets y las carpetas eliminadas en Experience Manager Assets siguen apareciendo en la carpeta sincronizada en Dynamic Media Classic. Elimínelos manualmente.

**Si la carga del vídeo falla:**

* Si la carga de vídeo falla y utiliza Experience Manager para codificar vídeo a través de la integración de Dynamic Media Classic, consulte [Añadir un tiempo de espera configurable al flujo de trabajo de carga de Dynamic Media Classic](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>La importación de recursos desde una cuenta de compañía de Dynamic Media Classic existente puede tardar mucho tiempo en mostrarse en Experience Manager. Asegúrese de designar una carpeta en Dynamic Media Classic que no tenga demasiados recursos. Por ejemplo, la carpeta raíz suele tener demasiados recursos.
>
>Si desea probar la integración, haga que la carpeta raíz apunte únicamente a una subcarpeta, en lugar de a toda la compañía.
