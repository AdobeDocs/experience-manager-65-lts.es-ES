---
title: Importar y administrar archivos
description: Obtenga información sobre cómo importar y administrar archivos. Archiva, importa y administra los LCA creados en Workbench. Puede importar, configurar, utilizar y eliminar un archivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a42d1094-293e-4f1a-a8f7-376dc8d34807
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 0%

---

# Importar y administrar archivos {#import-and-manage-archives}

Utilice la pestaña de archivos para importar y administrar los LCA creados en Workbench.

## Importar un archivo {#import-an-archive}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la pestaña de archivos.
1. Haga clic en Importar.
1. Haga clic en Examinar para buscar el archivo que desea importar y, a continuación, haga clic en Vista previa.
1. Revise la lista de recursos y objetos que se instalarán con el archivo. Asegúrese de que no haya conflictos con los recursos, objetos y configuraciones de servicio existentes porque no hay capacidad de deshacer disponible.

   Si selecciona importar las configuraciones del servicio, AEM Forms importará todos los archivos de configuración de proceso (extremos, perfiles de seguridad y parámetros de configuración de servicio) utilizados por los procesos en el LCA.

1. Haga clic en Importar.
1. Revise los resultados de la importación y haga clic en Omitir configuración para finalizar el proceso de importación o haga clic en Configurar para configurar el archivo.

   >[!NOTE]
   >
   >Si hace clic en Omitir configuración, puede configurar el archivo más adelante.

1. Si hace clic en Configurar, aparecerá la página Configurar puntos de conexión, donde podrá realizar los cambios necesarios:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de tareas, haga clic en Agregar Administrador de tareas. Para obtener detalles acerca de la configuración del Administrador de tareas, vea [Configurar los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un punto final de carpeta inspeccionada, haga clic en Agregar carpeta inspeccionada. Para obtener más información acerca de la configuración de la carpeta inspeccionada, consulte [Configuración del extremo de la carpeta inspeccionada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para añadir un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información acerca de la configuración de correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un extremo de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo de SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar Remoting. Para obtener detalles acerca de la configuración de Remoting, consulte [Configuración de extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Tenga en cuenta la URL de invocación de REST que se muestra en la página Agregar extremo de REST.
   * Para quitar un extremo, seleccione la casilla que hay junto a él y haga clic en Quitar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio del LCA tiene parámetros de configuración, aparecerá la página Configurar parámetros, donde configurará los parámetros del servicio y hará clic en Siguiente.
1. En la página Configurar perfil de seguridad, realice los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** Esta configuración indica si el servicio se puede invocar con o sin credenciales.

     Si se muestran *los llamadores que deben autenticarse* en este momento, el llamador del servicio debe estar autenticado y la entidad de seguridad del usuario para ese llamador debe estar autorizada para invocar el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadores no autenticados.

     Si se muestra *No se requiere que los llamadores se autentiquen*, no es necesario autenticar al llamador del servicio. La invocación del servicio siempre se realizará correctamente porque no hay ninguna comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **Ejecutar como:** Especifica la identidad en tiempo de ejecución utilizada por un servicio después de invocarlo. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

     **Sin especificar:** Se usa el comportamiento predeterminado.

     **Invocador:** Usa la misma identidad que el usuario que invocó el servicio.

     **Sistema:** ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para procesos de larga duración.

     **Usuario designado:** Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar al usuario.

   * Para agregar un principal al perfil de seguridad, haga clic en Agregar principal y seleccione el usuario o grupo que desee agregar como principal. Haga clic en Siguiente y, a continuación, seleccione los permisos que desee asignar a esta entidad de seguridad:

     **INVOKE_PERM:** Para invocar todas las operaciones del servicio

     **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

     **SUPERVISOR_PERM:** Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso

     **START_STOP_PERM:** Para iniciar y detener un servicio

     **ADD_REMOVE_ENDPOINTS_PERM:** Para agregar, quitar y modificar extremos de un servicio

     **CREATE_VERSION_PERM:** Para crear una versión del servicio

     **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

     **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

     **READ_PERM:** Para ver el servicio

     Haga clic en Finalizado para agregar el principal al perfil de seguridad.

1. Haga clic en Finalizado para completar la configuración.

## Configurar los formularios de AEM que forman parte de un archivo {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la pestaña de archivos.
1. En la página Administración de archivos, seleccione el archivo que desea configurar.
1. En la página Ver archivo, seleccione el recurso de archivo resaltado.
1. Configure el archivo de proceso importado.

## Utilice el asistente de configuración para configurar los formularios de AEM que forman parte de un archivo {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones y, a continuación, haga clic en la pestaña de archivos.
1. Haga clic en Configurar junto al archivo para configurarlo.
1. Aparecerá la página Configurar extremos, donde podrá realizar los cambios que necesite:

   * Para cambiar el nombre de un extremo o editar su descripción, haga clic en él.
   * Para agregar un extremo del Administrador de tareas, haga clic en Agregar Administrador de tareas. Para obtener detalles acerca de la configuración del Administrador de tareas, vea [Configurar los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para agregar un punto final de carpeta inspeccionada, haga clic en Agregar carpeta inspeccionada. Para obtener más información acerca de la configuración de la carpeta inspeccionada, consulte [Configuración del extremo de la carpeta inspeccionada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para añadir un extremo de correo electrónico, haga clic en Añadir correo electrónico. Para obtener más información acerca de la configuración de correo electrónico, consulte [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para agregar un extremo de EJB, haga clic en Agregar EJB y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo de SOAP, haga clic en Agregar SOAP y especifique un nombre y una descripción para el extremo.
   * Para agregar un extremo Remoting, haga clic en Agregar Remoting. Para obtener detalles acerca de la configuración de Remoting, consulte [Configuración de extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para agregar un extremo REST, haga clic en Agregar REST y especifique un nombre y una descripción para el extremo. Tenga en cuenta la URL de invocación de REST que se muestra en la página Agregar extremo de REST.
   * Para quitar un extremo, seleccione la casilla que hay junto a él y haga clic en Quitar.

1. Haga clic en Siguiente.
1. Si un proceso o servicio del LCA tiene parámetros de configuración, aparecerá la página Configurar parámetros, donde configurará los parámetros del servicio y hará clic en Siguiente.
1. En la página Configurar perfil de seguridad, puede realizar los cambios que necesite:

   * **Requerir que los llamadores se autentiquen:** Esta configuración indica si el servicio se puede invocar con o sin credenciales.

     Si se muestran *los llamadores que deben autenticarse* en este momento, el llamador del servicio debe estar autenticado y la entidad de seguridad del usuario para ese llamador debe estar autorizada para invocar el servicio; de lo contrario, se rechazará el intento de invocación. Para eliminar la necesidad de autenticarse, haga clic en Permitir llamadores no autenticados.

     Si se muestra *No se requiere que los llamadores se autentiquen*, el llamador del servicio puede o no estar autenticado. La invocación del servicio siempre se realizará correctamente porque no hay ninguna comprobación de autorización. Para requerir autenticación, haga clic en Requerir que los llamadores se autentiquen.

   * **Ejecutar como:** Especifica la identidad en tiempo de ejecución utilizada por un servicio después de invocarlo. Para cambiar esta opción, haga clic en Cambiar. Elija entre las siguientes opciones:

     **Sin especificar:** Se usa el comportamiento predeterminado.

     **Invocador:** Usa la misma identidad que el usuario que invocó el servicio.

     **Sistema:** ejecuta el servicio con privilegios completos. Esta es la configuración predeterminada para procesos de larga duración.

     **Usuario designado:** Permite ejecutar el servicio como un usuario específico. Esta es la configuración predeterminada para procesos de corta duración. Cuando seleccione esta opción, haga clic en Seleccionar usuario para mostrar la página Seleccionar principal, donde puede buscar y seleccionar al usuario.

   * Para agregar un principal al perfil de seguridad, haga clic en Agregar principal y seleccione el usuario o grupo que desee agregar como principal. Haga clic en Siguiente y, a continuación, seleccione los permisos que desee asignar a esta entidad de seguridad:

     **INVOKE_PERM:** Para invocar todas las operaciones del servicio

     **MODIFY_CONFIG_PERM:** Para modificar la configuración de un servicio

     **SUPERVISOR_PERM:** Para ver los datos de instancia de proceso de un servicio creado a partir de un proceso

     **START_STOP_PERM:** Para iniciar y detener un servicio

     **ADD_REMOVE_ENDPOINTS_PERM:** Para agregar, quitar y modificar extremos de un servicio

     **CREATE_VERSION_PERM:** Para crear una versión del servicio

     **DELETE_VERSION_PERM:** Para eliminar una versión del servicio

     **MODIFY_VERSION_PERM:** Para modificar una versión del servicio

     **READ_PERM:** Para ver el servicio

     Haga clic en Finalizado para agregar el principal al perfil de seguridad.

## Eliminación de un archivo {#remove-an-archive}

>[!NOTE]
>
>Para quitar un archivo que contiene recursos almacenados en un repositorio de terceros (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager), también debe eliminar los archivos de recursos del repositorio mediante Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de archivos.
1. En la página Administración de archivos, active la casilla de verificación del archivo que desea quitar y haga clic en Quitar.
