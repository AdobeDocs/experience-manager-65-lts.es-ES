---
title: Configurar Connector para Documentum de EMC
description: Obtenga información sobre cómo configurar Connector para EMC Documentum para habilitar la comunicación entre AEM Forms y EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a9eae40f-531f-4354-ade0-853e84dd88d9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 2%

---

# Configurar Connector para Documentum de EMC {#configuring-connector-for-emc-documentum}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Connector para EMC Documentum permite la comunicación entre AEM Forms y EMC Documentum. Para obtener información adicional, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

La configuración de Connector para Documentum de EMC implica la configuración de la conexión del servidor y las credenciales del repositorio.

>[!NOTE]
>
>En versiones anteriores , los recursos se podían almacenar en un repositorio de ECM. En la versión actual, los recursos se almacenan en el repositorio nativo de los formularios de AEM y los servicios de proveedor del repositorio han quedado obsoletos. La migración de recursos de un repositorio de ECM al repositorio de AEM Forms se realiza al realizar una actualización a los formularios de AEM. Para obtener más información, consulte la Guía de actualización de formularios de AEM para su servidor de aplicaciones.

## Configuración de la conexión del servidor {#configuring-the-server-connection}

En este tema se describen las tareas de Connector para Documentum de EMC que puede realizar en la página Configuración.

>[!NOTE]
>
>Si está configurando todas las opciones simultáneamente, solo necesita hacer clic en Guardar una vez.

### Configuración del servidor {#configure-the-server}

Debe configurar la información del servidor del agente de conexión. Esta información es necesaria para conectarse a los repositorios de contenido de Documentum e iniciar Connector para Documentum de EMC.

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. En el área Información de configuración de Documentum, introduzca el nombre de host o la dirección IP y el número de puerto del agente de conexión. El número de puerto debe ser un entero positivo (por ejemplo, 1489).
1. Haga clic en Guardar.

### Configurar credenciales principales {#configure-principal-credentials}

Al configurar las credenciales principales, el nombre del repositorio proporcionado depende de si se proporciona un nombre de repositorio explícito durante el inicio de sesión.

Si escribe un nombre de usuario o una contraseña incorrectos, obtendrá los siguientes resultados, dependiendo de si el servicio se está ejecutando actualmente:

* Si se detienen tanto el servicio EMC Documentum Repository Provider como el servicio EMC Documentum Content Repository Connector, no aparece ningún error al guardar la información de configuración del servicio. Sin embargo, la próxima vez que inicie el servicio, se producirá una excepción y el servicio no se iniciará.
* Si se inicia el servicio EMC Documentum Repository Provider o el servicio EMC Documentum Content Repository Connector, al guardar la información de configuración del servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. En el área Información de credenciales principales de Documentum, escriba el nombre de usuario y la contraseña de un usuario con privilegios de superadministrador.
1. Si no se proporciona un nombre de repositorio explícito durante el inicio de sesión, introduzca el nombre del repositorio con el que están asociadas las credenciales.
1. Haga clic en Guardar.

### Cambio del proveedor de servicios del repositorio {#change-the-repository-service-provider}

Puede configurar qué proveedor de servicios de repositorio utilizar con Documentum. Las llamadas al servicio del repositorio se delegan al proveedor que configure. Las opciones disponibles son las siguientes:

**Nombre actual del proveedor de servicios del repositorio:** Nombre del proveedor de servicios del repositorio actual

**Proveedor del repositorio de Documentum de ECM:** Convierte al proveedor del repositorio de Documentum en el proveedor del repositorio. Esta opción ha quedado obsoleta

**proveedor del repositorio:** Convierte al proveedor del repositorio nativo en el proveedor del repositorio

>[!NOTE]
>
>Para seleccionar un proveedor de servicios de repositorio distinto de los enumerados, configure RepositoryService en Aplicaciones y servicios > Administración de servicios. <!-- Fix broken link (See Managing Services) -->.

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. En el área Información del proveedor de servicios de repositorio, seleccione el proveedor de servicios de repositorio alternativo.
1. Haga clic en Guardar.

## Configuración de credenciales del repositorio {#configuring-repository-credentials}

La información de credenciales de Documentum se utiliza en el contexto del sistema de AEM Forms. Las credenciales de repositorio son específicas de determinados repositorios de Documentum. Puede proporcionar credenciales para cualquier número de repositorios; sin embargo, solo puede especificar un conjunto de credenciales por repositorio.

### Agregar una credencial de repositorio {#add-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Configuración de credenciales de repositorio.
1. Haga clic en Agregar. Aparecerá la página Información de credenciales del sistema de Documentum.
1. Introduzca un nombre para el repositorio.
1. Introduzca un nombre de usuario y una contraseña.
1. Haga clic en Guardar.

Si se están ejecutando el servicio Content Repository Connector for EMC Documentum o el servicio Repository Service for EMC Documentum, la información de credenciales se comprueba con el repositorio especificado antes de almacenarse en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

### Quitar una credencial de repositorio {#remove-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. Seleccione la casilla de verificación situada junto al repositorio del que desea quitar las credenciales y haga clic en Quitar. Las credenciales del repositorio seleccionado se eliminan de la base de datos.

### Cambiar el nombre de usuario y la contraseña de una credencial de repositorio {#change-the-user-name-and-password-for-a-repository-credential}

1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. Haga clic en el nombre del repositorio para el que desea editar las credenciales.
1. Cambie el nombre de usuario o la contraseña del repositorio, o ambos. (El nombre del repositorio es de solo lectura).
1. Haga clic en Guardar.

Si se están ejecutando el servicio Content Repository Connector for EMC Documentum o el servicio Repository Service for EMC Documentum, la información de credenciales se comprueba con el repositorio especificado antes de almacenarse en la base de datos. Si las credenciales no son válidas o existen, se muestra un mensaje de error.

## Habilitar la solicitud para compartir colas de tareas de Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Se requieren algunos pasos manuales para garantizar que la función Solicitud de uso compartido de colas de tareas de Workspace funcione correctamente con Connector para Documentum de EMC.

1. Una vez que haya implementado formularios AEM y Workbench esté instalado, inicie sesión en Workbench y abra la vista Recursos. Determinará dónde se encuentra el archivo QueueSharing.swf desde esta vista.
1. Arrastre el archivo QueueSharing.swf desde la vista Recursos hasta el escritorio de Windows o una ubicación equivalente, dependiendo del sistema operativo.
1. En la consola de administración, haga clic en Servicios > Connector para Documentum de EMC > Ajustes de configuración.
1. En Información del proveedor del servicio de repositorio, cambie el proveedor del repositorio configurado a Proveedor del repositorio de Documentum de EMC.
1. Inicie Workbench y copie el archivo QueueSharing.swf desde la ubicación en la que lo copió originalmente (por ejemplo, el escritorio de Windows u otra ubicación) en un directorio existente dentro del repositorio de Documentum de EMC.
1. En la vista Procesos de Workbench, abra el proceso Compartir en cola.
1. En la vista Variables, abra las propiedades de la variable &quot;theForm&quot; y cambie el URI para que coincida con la ruta en la que colocó el archivo QueueSharing.swf en el paso 5.
1. Guarde el proceso.
1. Migre el proceso al entorno de producción según la política de su organización.
