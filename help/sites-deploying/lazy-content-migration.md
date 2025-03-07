---
title: Migración de contenido diferido
description: Obtenga información acerca de la migración de contenido diferido en Adobe Experience Manager 6.4.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: 78c5486c-ed84-4ec8-b0b0-42d4e8611098
source-git-commit: 09d2e75729060135f9eff1fc9f0126b0f940310b
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# Migración de contenido diferido {#lazy-content-migration}

En aras de la compatibilidad con versiones anteriores, el contenido y la configuración en **/etc** y **/content** a partir de Adobe Experience Manager (AEM) 6.3 no se tocarán ni transformarán inmediatamente con la actualización. Esto se hace para garantizar que las dependencias de las aplicaciones de los clientes en esas estructuras permanezcan intactas. La funcionalidad relacionada con estas estructuras de contenido sigue siendo la misma aunque el contenido de una versión predeterminada de AEM 6.5 se aloje en otro lugar.

Aunque no todas esas ubicaciones se pueden transformar automáticamente, hay algunas `CodeUpgradeTasks` retrasadas que también se denominan Migración de contenido diferido. Esto permite a los clientes almacenar en déclencheur esas transformaciones automáticas reiniciando la instancia con esta propiedad del sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Esto hace que `CodeUpgradeTasks` se ejecute durante la migración.

Aunque el objetivo es una ejecución eficaz, este proceso de actualización es sincrónico y, por lo tanto, conlleva un tiempo de inactividad en función de la cantidad de contenido que se debe procesar. Adobe recomienda evaluar los tiempos de ejecución en un entorno de ensayo antes de un sistema de producción para planificar una ventana de mantenimiento adecuada.

Dado que esto suele requerir el ajuste de la aplicación, esta actividad debe realizarse junto con la implementación de la aplicación correspondiente.

A continuación se muestra la lista completa de `CodeUpgradeTasks` introducidos en 6.5:

| **Nombre** | **Relevante** **para las versiones de AEM anteriores a** | **Migración** **Tipo** | **Detalles** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Inmediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6,0 | Inmediato | Detecta todos(as) los/las `LiveRelationShips` de `VersionStorage` que se han eliminado y agrega la propiedad de exclusión al elemento principal |
| `Cq61CloudServicesContentUpgrade` | &lt; 6,1 | Inmediato | Reestructura Cloud Services para una configuración segura de forma predeterminada |
| `Cq62ConfContentUpgrade` | &lt; 6,2 | Inmediato | Quita la vinculación basada en propiedades de **/content** a **/conf** (reemplazado por el mecanismo OSGi) y genera la configuración OSGi correspondiente |
| `Cq62FormsContentUpgrade` | &lt; 6,2 | Inmediato | Debido a la gestión merge_preserve, la regla de denegación segura de forma predeterminada anula los permisos dados, lo que provoca la necesidad de reordenar en la actualización |
| `CQ62Html5SmartFileUpgrade` | &lt; 6,2 | Inmediato | Detecta componentes mediante el widget Html5SmartFile, busca usos del componente en el contenido y reestructura la persistencia, moviendo efectivamente el binario un nivel hacia abajo y no lo almacena en el nivel de componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6,2 | Inmediato | Mueve proyectos de estilo antiguos de **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6,2 | Inmediato | Introduce una capa contenedora en la jerarquía (Areas) y ajusta las referencias. |
| `Cq62TargetContentUpgrade` | &lt; 6,2 | Inmediato | Establece nombres de ubicación fijos para los componentes de destino. |
| `Cq62WorkflowContentUpgrade` | &lt; 6,2 | Inmediato | Transformación compleja de modelos de flujo de trabajo anteriores a las estructuras, instancias y notificaciones de la versión 6.2 y que vuelven a combinarse desde la ubicación de copia de seguridad de **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6,3 | Inmediato | Mueve recursos, esquemas de metadatos personalizados y perfiles de procesamiento de **/apps** a **/conf** y traduce los formularios de esquema de metadatos y perfiles de metadatos de coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6,3 | Inmediato | Mueve recursos y facetas de búsqueda personalizadas de **/apps** a **/conf** y traduce los formularios de esquema de metadatos y perfiles de metadatos de coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6,3 | Inmediato | Actualiza la Bandeja de entradaElementos para ordenar los elementos de la Bandeja de entrada (ajustar los metadatos para una ordenación eficaz) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6,3 | Inmediato | Ajusta la propiedad metadataSchema de la carpeta al reemplazar las rutas relativas a **/conf** en lugar de **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6,3 | Inmediato | Ajuste de la estructura de navegación |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6,3 | Inmediato | Mueve configuraciones personalizadas para los paneles de supervisión de **/libs** y **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6,3 | Inmediato | Traduce la propiedad processingProfile (utilizada hasta 6.1) en Assets para que coincida con la estructura de 6.3 y posteriores. También ajusta las rutas relativas del perfil a **/conf** en lugar de **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6,3 | Inmediato | Tarea de actualización que elimina las entradas de menú de CRXDE Lite y consola web obsoletas en caso de que se produzca una actualización. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6,3 | Retrasado | Al mover las configuraciones de nube de SRP, las configuraciones de palabras clave de observación de la comunidad, se limpian **/etc/social** y **/etc/enablement** (cualquier referencia y dato debe ajustarse cuando se ejecute la migración diferida; ya no debe existir ninguna parte de la aplicación que dependa de esta estructura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6,4 | Retrasado | Limpia **/etc/cloudsettings** (que contiene la configuración de ContextHub). La configuración se migra automáticamente en el primer acceso. En caso de que se inicie la migración de contenido diferido junto con la actualización, este contenido en **/etc/cloudsettings** debe conservarse mediante el paquete antes de la actualización y reinstalarse para que se inicie la transformación implícita, junto con una desinstalación posterior del paquete una vez finalizado. |
| `CQ64UsersTitleFixTask` | &lt; 6,4 | Retrasado | Ajusta la estructura de título heredada al título en el nodo de perfil del usuario. |
| `CQ64CommerceMigrationTask` | &lt; 6,4 | Retrasado | Migrar contenido comercial de **/etc/commerce** a **/var/commerce**. Durante la migración, el contenido se mueve y las referencias al contenido movido se actualizan para reflejar la nueva ubicación. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Retrasado | Migrar la configuración del catálogo heredado y la configuración de los servicios de nube de Dynamic Media de **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Retrasado | Limpiar clientlibs heredados existentes en **/etc/clientlibs** |
