---
title: Importar y exportar la configuración global
description: Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f5b45667-87df-4069-8f08-2b6daf4bad1e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 1%

---

# Importar y exportar la configuración global {#importing-and-exporting-global-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede importar y exportar definiciones de plantillas de búsqueda y configuración global para Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.

Por ejemplo, puede pasar de un entorno de desarrollo a un entorno de producción exportando las definiciones de plantillas de búsqueda y la configuración global de un entorno e importándolas en el otro.

Después de exportar el archivo de configuración global, puede modificar la configuración en un editor de texto o XML. Sin embargo, los únicos ajustes que puede que desee editar son JChannelConnectionProperties, formViewOnly y specialRoutes. Para obtener más información, consulte [Configuración global de Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Si cambia las propiedades del evento en el archivo de configuración global, debe reiniciar el servidor.

## Importar una definición de plantilla de búsqueda {#import-a-search-template-definition}

1. En la consola de administración, haga clic en Servicios > Workspace > Administración global.
1. En el cuadro Importar definición de plantilla de búsqueda, haga clic en Elegir archivo y seleccione la plantilla de búsqueda. Solo puede importar definiciones de plantillas de búsqueda que se exportaron originalmente desde una instancia de Workspace.
1. Haga clic en Importar.

## Exportar una definición de plantilla de búsqueda {#export-a-search-template-definition}

1. En la página Administración global, en Exportar definición de plantilla de búsqueda, haga clic en Mostrar todo.
1. En la lista de plantillas de búsqueda, seleccione la plantilla que desea exportar.

   >[!NOTE]
   >
   >Puede seleccionar más de una plantilla, pero solo se exportará la última seleccionada.

1. Haga clic en Exportar y, a continuación, guarde el archivo en el equipo.

## Importar configuración global {#import-global-settings}

1. En la página Administración global, en Importar configuración global, haga clic en Elegir archivo y seleccione el archivo de configuración global. El archivo de configuración global debe estar en formato XML.
1. Haga clic en Importar.

## Exportar configuración global {#export-global-settings}

1. En la página Administración global, en Exportar configuración global, haga clic en Exportar.
1. Guarde el archivo en el equipo.

## Configuración global de Workspace {#workspace-global-settings}

Puede modificar el archivo de configuración global; sin embargo, los únicos valores que puede que desee editar son JChannelConnectionProperties, formViewOnly y specialRoutes.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.

El archivo de configuración global de Workspace incluye la siguiente configuración:

### configuración specialRoutes {#specialroutes-settings}

La configuración *specialRoutes* especifica las propiedades de las rutas especiales, aprobar y denegar, en Workspace. En determinadas situaciones, los botones de estas rutas aparecen en las tarjetas de tareas de Workspace y el usuario puede seleccionarlos sin abrir el formulario. Puede modificar la configuración specialRoutes en el archivo de configuración global para agregar nombres personalizados para aprobar y denegar o para crear rutas adicionales.

**client_specialRoutes_routes_approve_style:** Nombre del estilo que se encuentra en el tema de Workspace, que identifica los iconos del botón de aprobación. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }`: el archivo CSS de Workspace está incrustado en el archivo workspace-theme.swf, que se encuentra en el archivo adobe-workspace-client.ear > adobe-workspace-client.war. Para cambiar el aspecto de Workspace, debe volver a compilar el archivo workspace-theme.swf.

**client_specialRoutes_routes_deny_names:** La variedad de cadenas que un usuario de Workbench puede usar para ser interpretadas como &quot;denegadas&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es denegar. Si el usuario de Workbench utiliza la palabra Denegar en un proceso, la palabra no se reconoce. Se debe agregar la palabra Denegar a esta configuración para que el botón de ruta se personalice y se le aplique el estilo.

**client_specialRoutes_routes_deny_style:** Nombre del estilo que se encuentra en el archivo de temas de Workspace, que identifica los iconos del botón de denegación. El estilo debe incluir valores para un icono habilitado y un icono deshabilitado. Para definir un estilo para un botón personalizado, debe utilizar la siguiente plantilla:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names:** La variedad de cadenas que un usuario de Workbench puede usar para interpretarse como &quot;aprobar&quot;. Las cadenas distinguen entre mayúsculas y minúsculas. Por ejemplo, el valor predeterminado es approve. Si el usuario de Workbench utiliza la palabra Aprobar en un proceso, la palabra no se reconocerá. Se debe agregar la palabra Aprobar a esta configuración para que el botón de ruta se personalice y se le aplique el estilo.

**client_specialRoutes_names:** Claves utilizadas para localizar el valor de cadena personalizado de los archivos de recursos. Cada entrada de esta configuración debe incluir los valores de los nombres y el estilo.

### Configuración de JGroup {#jgroup-settings}

Esta configuración solo aparece si ha actualizado desde Adobe LiveCycle ES 2.5 o anterior.

**server_remoteevents_ClientTimeoutMilliseconds:** Tiempo máximo que JGroup espera mensajes de evento. Esta configuración no debe cambiarse.

**server_remoteevents_ServerTimeoutMilliseconds:** Tiempo de espera para recibir mensajes JGroup en el servidor. Esta opción establece el retraso para enviar mensajes del servidor al cliente.

**server_remoteevents_JChannelConnectionProperties:** Propiedades de conexión del grupo JGroup que se utilizan para la comunicación entre el servidor (en el que el servicio RemoteEvent procesa un evento de servicio) y todas las instancias de Workspace.

Es posible que tenga que cambiar los valores UDP para la dirección IP de multidifusión (mcast_addr), el puerto IP de multidifusión (mcast_port) y el TTL para los paquetes de multidifusión (ip_ttl). De forma predeterminada, los valores de dirección IP y puerto de multidifusión se generan aleatoriamente y, por lo general, no es necesario cambiar los valores. Sin embargo, si su empresa tiene directivas de red con respecto a intervalos de multidifusión específicos para direcciones IP de multidifusión, es posible que tenga que cambiar los valores.

>[!NOTE]
>
>El TTL debe ser mayor que el número de conmutadores de red entre los servidores del clúster; sin embargo, si el valor se establece demasiado alto, puede hacer que los paquetes de multidifusión viajen a subredes, donde se descartarán.

Las propiedades restantes de esta configuración no deben cambiarse.

**server_remoteevents_JGroupName:** Nombre del JGroup utilizado para la comunicación de eventos remotos. Este valor se genera de forma aleatoria para evitar conflictos en los clústeres. Este valor no debe cambiarse.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### Configuración de formView {#formview-settings}

**client_formView_openFormInFullScreen:** Para mostrar todos los formularios en Workspace en modo de pantalla completa, establezca esta opción en true. De forma predeterminada, esta opción se establece en false y los formularios no se muestran en el modo de pantalla completa. El servicio de usuario contiene una opción para abrir el documento asociado a una tarea en modo de pantalla completa. Esto permite controlar la visualización por proceso.

**client_routes_formViewOnly:** Cuando se establece en True, las rutas no se muestran en la vista de tarjeta o en la vista de lista de Workspace. El valor predeterminado es False, lo que significa que las rutas se muestran en la vista de tarjeta y en la vista de lista.

### Otra configuración {#other-settings}

**client_mimeTypes_openOutsideBrowser:** El tipo MIME de los documentos que se abren fuera de la instancia del explorador Workspace. Si los procesos de su organización requieren un tipo MIME adicional, especifíquelo aquí. Los valores predeterminados son:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** Almacena en caché una interfaz de usuario de tarea personalizada.

**server_debugLevel:** No cambie esta configuración.

**client_pollingInterval:** establece el intervalo de sondeo (en segundos) utilizado en (obsoleto para formularios AEM en JEE) Flex Workspace para detectar tareas nuevas y modificadas. El valor predeterminado es de 3 segundos. Esto no funciona para AEM Forms Workspace.

**client_systemContext_name:** Especifique un nombre personalizado (por ejemplo, Ciudadano) para mostrar en el campo Agregado por (en la pestaña Archivos adjuntos) para los archivos adjuntos de una tarea en AEM Forms Workspace.

Para definir el nombre personalizado:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Para la aplicación Demo, el nombre para mostrar predeterminado es **Citizen**. Para una aplicación personalizada que cree, el nombre para mostrar predeterminado es **Cuenta de contexto del sistema**.
>
>**client_inactiveTimeout:** Cuando un usuario permanece inactivo durante un período de tiempo específico, caduca la sesión de AEM Forms Workspace. Para habilitar la característica, agregue una entrada a la Configuración global &lt;client_inactiveTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_inactiveTimeout>. Puede especificar el valor 0 para deshabilitar el tiempo de espera de inactividad. La cantidad de tiempo se especifica en segundos.
