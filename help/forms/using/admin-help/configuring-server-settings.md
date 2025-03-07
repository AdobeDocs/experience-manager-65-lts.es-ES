---
title: Configurar el servidor
description: La página Configuración del servidor proporciona acceso al correo electrónico, a las notificaciones de tareas y a la configuración de las notificaciones del administrador.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: da8031f2-26ab-41e2-bf54-7032727ca192
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2643'
ht-degree: 0%

---

# Configurar el servidor {#configuring-server-settings}

La página Configuración del servidor proporciona acceso a varias configuraciones para el flujo de trabajo de formularios:

* **Configuración de correo electrónico** que habilita los mensajes de correo electrónico salientes, junto con la configuración del servidor de correo electrónico utilizada para esos mensajes. (Consulte [Configuración del correo electrónico](configuring-server-settings.md#configuring-email-settings).)
* **Configuración de notificaciones de tareas** que habilita, deshabilita o modifica los mensajes enviados en notificaciones por correo electrónico a usuarios finales y grupos con respecto a sus tareas. (Consulte [Configuración de notificaciones para usuarios y grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups)).
* **Configuración de notificaciones del administrador** que habilita, deshabilita o modifica los mensajes enviados en notificaciones por correo electrónico para tareas administrativas. (Consulte [Configuración de notificaciones para administradores](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configuración de correo electrónico {#configuring-email-settings}

Puede especificar una cuenta de correo electrónico para el servidor de Forms, a través de la cual enviará mensajes de correo electrónico a los usuarios y administradores de formularios AEM. Estos mensajes de correo electrónico se utilizan para notificar y recordar a los usuarios las tareas que deben completar, notificar al usuario las tareas que han alcanzado un plazo y notificar al administrador de cualquier error de proceso que se produzca.

Para habilitar el envío de mensajes de correo electrónico entre los formularios de AEM y los usuarios, configure las opciones del correo electrónico saliente en la página Configuración de correo electrónico. El correo electrónico saliente debe utilizar un servidor SMTP.

Para permitir que los formularios AEM reciban y administren mensajes de correo electrónico entrantes de los usuarios, cree un extremo de correo electrónico para el servicio Tarea completa. (Consulte [Crear un extremo de correo electrónico para el servicio Tarea completa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Si los procesos están diseñados e implementados sin requerir correo electrónico, no tiene que configurar ninguna de las opciones de la página Configuración de correo electrónico.

### Configuración del correo electrónico saliente {#configure-outgoing-email-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Configuración del servidor > Configuración de correo electrónico.
1. Seleccione Habilitar mensajes salientes.
1. En el cuadro Servidor SMTP, escriba el nombre o la dirección IP del servidor de correo electrónico. Todos los mensajes de correo electrónico de notificación del flujo de trabajo de formularios se envían desde este servidor de correo electrónico.
1. En los cuadros Nombre de usuario y Contraseña, escriba el nombre de inicio de sesión y la contraseña que se utilizarán cuando el servidor SMTP requiera autenticación. Déjelas en blanco si se permite el inicio de sesión anónimo.
1. En el cuadro Dirección de correo electrónico, escriba la dirección de correo electrónico que se utilizará como remite de los mensajes de correo electrónico que envía el flujo de trabajo de formularios.

   >[!NOTE]
   >
   >Si utiliza Microsoft Exchange Server y la dirección de correo electrónico no es válida, el servidor de Microsoft Exchange no enviará un correo electrónico a las listas de distribución. Para resolver el problema, seleccione la opción **Habilitar comunicación externa** por separado para cada lista de distribución en el servidor de Microsoft Exchange.

1. Haga clic en Guardar.

>[!NOTE]
>
>Si introduce información incorrecta, puede hacer clic en Cancelar para volver a la página mostrada anteriormente.

### Configuración de plantillas de correo electrónico para utilizar AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace ya no se utiliza para la versión de formularios AEM.

De forma predeterminada, los correos electrónicos enviados por los formularios de AEM contienen vínculos a (obsoleto para formularios de AEM en JEE) Flex Workspace. Puede configurar formularios AEM para enviar correos electrónicos con vínculos a AEM Forms Workspace. Para obtener más información sobre las ventajas de AEM Forms Workspace sobre (obsoleto para formularios AEM en JEE) Flex Workspace, consulte [este](/help/forms/using/features-html-workspace-available-flex.md) artículo.

1. En la consola de administración, haga clic en Inicio > Servicios > Forms workflow > Configuración del servidor > Notificaciones de tareas.
1. Abra la plantilla de asignación de tareas.
1. Establezca la plantilla en las notificaciones de tareas en lo siguiente: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configuración de notificaciones para usuarios y grupos {#configuring-notifications-for-users-and-groups}

En la página Notificación de tarea, puede configurar las plantillas que utilizará el flujo de trabajo de Forms para generar las notificaciones por correo electrónico que se envían a usuarios y grupos. Puede personalizar y dar formato a las notificaciones mediante variables de flujo de trabajo de formularios.

Puede configurar los siguientes tipos de notificaciones para usuarios y grupos:

* recordatorios
* asignaciones de tareas
* plazos

Para generar notificaciones por correo electrónico para un grupo, especifique una dirección de correo electrónico para el grupo en Administración de usuarios. <!--Fix broken link See Setting up and organizing users -->Cuando el flujo de trabajo de formularios envía una notificación por correo electrónico a un grupo, cada miembro del grupo que tenga especificada una dirección de correo electrónico recibe la notificación por correo electrónico. Cuando un miembro del grupo recibe una notificación por correo electrónico y desea reclamar la tarea, debe hacer clic en el vínculo de reclamación de la notificación por correo electrónico, que abre la página de detalles de la tarea en Workspace. Desde allí, el miembro puede reclamar o reclamar y abrir el elemento de trabajo.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.

### Configurar recordatorios para usuarios o grupos {#configure-reminders-for-users-or-groups}

Puede enviar notificaciones de recordatorio al usuario o grupo asignado cuando se aproxime una fecha límite para completar una tarea. El desarrollador de procesos determina las reglas para determinar exactamente cuándo se envía una notificación de recordatorio.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Recordatorio (para usuarios) o Grupo - Recordatorio (para grupos).
1. Seleccione Activar recordatorio o Activar grupo - recordatorio.
1. (Solo notificaciones de usuarios) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico del recordatorio, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que utilizarán la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configurar notificaciones de asignación de tareas para usuarios o grupos {#configure-task-assignment-notifications-for-users-or-groups}

Puede enviar notificaciones de asignación de tareas a un usuario o grupo cuando se les asigne una tarea.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Asignación de tareas para usuarios o en Grupo - Asignación de tareas para grupos.
1. Seleccione Habilitar asignación de tareas para los usuarios o Habilitar grupo - asignación de tareas para los grupos.
1. (Solo notificaciones de usuarios) Para incluir un archivo adjunto del formulario y sus datos con el mensaje de correo electrónico de asignación de tareas, seleccione Incluir datos del formulario.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que utilizarán la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configurar notificaciones de fechas límite para usuarios o grupos {#configure-deadline-notifications-for-users-or-groups}

Puede enviar notificaciones de fecha límite a usuarios y grupos cuando haya pasado la fecha límite para actuar sobre una tarea asignada. Una notificación de fecha límite suele ser informativa porque el usuario ya no puede actuar sobre la tarea asignada.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones de tareas.
1. En Tipo de notificación, haga clic en Plazo (para usuarios) o Grupo - Plazo (para grupos).
1. Seleccione Habilitar fecha límite o Habilitar grupo - fecha límite.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que utilizarán la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Ocultar la etiqueta DO NOT DELETE para todos los correos electrónicos {#hide-the-do-not-delete-tag-for-all-emails}

Puede configurar el correo electrónico para que se oculte en la etiqueta de seguimiento DO NOT DELETE en todos los correos electrónicos enviados en un proceso centrado en el ser humano.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configuración de notificaciones para administradores {#configuring-notifications-for-administrators}

Puede configurar las plantillas que utilizará Forms Workflow para generar las notificaciones por correo electrónico que se envían a los administradores.

Puede configurar los siguientes tipos de notificaciones para los administradores:

* rama estancada
* operación interrumpida

### Configurar notificaciones de ramas estancadas {#configure-stalled-branch-notifications}

Si una rama se detiene (deja de funcionar deliberadamente o debido a un error), puede hacer que se envíe una notificación por correo electrónico a un administrador u otro usuario, que puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones del administrador.
1. En Tipo de notificación, haga clic en Rama detenida.
1. Seleccione Habilitar rama estancada.
1. En el cuadro Dirección de correo electrónico, escriba las direcciones de los usuarios a los que notificar cuando se detenga una sucursal. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. En la lista Formato del mensaje, seleccione el formato en el que se envía el mensaje de correo electrónico, ya sea HTML o Texto. El formato predeterminado es HTML.
1. En la lista Codificación de correo electrónico, seleccione el formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que utilizan la mayoría de los usuarios fuera de Japón. Los usuarios de Japón pueden seleccionar ISO2022-JP.
1. Haga clic en Guardar.

### Configurar notificaciones de operaciones estancadas {#configure-stalled-operation-notifications}

Si una operación se detiene (deja de realizarse deliberadamente o debido a un error), puede hacer que se envíe una notificación por correo electrónico a un administrador u otro usuario, que puede investigar el problema.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Notificaciones del administrador.
1. En Tipo de notificación, haga clic en Operación detenida.
1. Seleccione Habilitar operación interrumpida.
1. En el cuadro Direcciones de correo electrónico, escriba las direcciones de los usuarios a los que se notificará cuando se detenga una operación. Utilice el formato user@domain.com y separe cada dirección con una coma. Normalmente, esta dirección de correo electrónico es para un administrador.
1. En el cuadro Asunto, escriba el texto de la línea de asunto del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications)
1. En el cuadro Plantilla de notificación, escriba el texto del cuerpo del mensaje de correo electrónico. Este campo se rellena previamente con el texto predeterminado. Para obtener detalles acerca de cómo personalizar este campo, vea [Personalizar el contenido de las notificaciones](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Haga clic en Guardar.

## Personalización del contenido de las notificaciones {#customizing-the-content-of-notifications}

Las páginas Notificaciones de tareas y Notificaciones del administrador proporcionan varias funciones que permiten personalizar los mensajes de notificación:

* editor de texto enriquecido
* selector de variables
* Generación de URL

### Editor de texto enriquecido {#rich-text-editor}

El área Plantilla de notificación es un editor de texto enriquecido que permite generar HTML para los mensajes de notificación por correo electrónico. Proporciona opciones de formato de fuente y párrafo, que se encuentran debajo del cuadro Plantilla de notificación. Las opciones incluyen tipo de fuente, tamaño, estilo y color, y alineación de párrafo y viñetas.

### Generación de URL {#url-generation}

Solo para las notificaciones de tareas, el flujo de trabajo de Forms incluye dos configuraciones de URL predefinidas que puede arrastrar desde la lista Generación de URL al cuadro Plantilla de notificación y, a continuación, personalizar:

* OpenTask está disponible para los tipos de notificación Recordatorio y Asignación de tareas. Esta URL proporciona un vínculo a la tarea en Workspace, lo que permite al usuario acceder rápidamente a la tarea desde la notificación por correo electrónico. Al arrastrar la URL de OpenTask al cuadro Plantilla de notificación, la URL tiene el siguiente formato:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask está disponible para los tipos de notificación Grupo - Recordatorio y Grupo - Asignación de tareas. Esta dirección URL proporciona un vínculo a la página de detalles de la tarea en Workspace, donde el usuario puede reclamar o reclamar y abrir el elemento de trabajo. Al arrastrar la dirección URL de la tarea de notificación al cuadro Plantilla de notificación, la dirección URL tiene el siguiente formato:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.

Si la solución se implementa en un entorno en clúster, reemplace `@@notification-host@@` por la dirección del clúster.

`<`*PORT* `>` es el número de puerto del detector HTTP para el servidor de aplicaciones. El puerto de escucha HTTP predeterminado para los servidores de aplicaciones admitidos es el siguiente:

**JBoss:** 8080

**Servidor Oracle WebLogic:** 7001

**IBM WebSphere:** 9080

Para que estas direcciones URL funcionen correctamente, reemplace `<`*PORT* `>` por el número de puerto apropiado para su entorno.

>[!NOTE]
>
>Si utiliza una aplicación web personalizada que no sea Forms para proporcionar a los usuarios acceso a las tareas, debe utilizar un formato de URL adecuado para la aplicación personalizada.

### Selector de variables {#variable-picker}

La lista Selector de variables proporciona variables útiles que puede arrastrar y soltar en los cuadros Asunto o Plantilla de notificación. Cuando suelta una variable en los cuadros Asunto o Plantilla de notificación, cambia al nombre real de la variable del flujo de trabajo de formularios con dos símbolos @ a cada lado, por ejemplo, `@@taskid@@`.

Para avisos, asignaciones de tareas y fechas límites para usuarios y grupos, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**description**: El contenido de la propiedad Description, tal como se define en el paso del usuario (punto de inicio, operación Asignar tarea o operación Asignar varias tareas) del proceso en Workbench.

**instrucciones** El contenido de la propiedad Instrucciones de tarea, tal como se define en el paso de usuario del proceso en Workbench.

**notification-host** El nombre de host del servidor de aplicaciones de AEM Forms

**process-name**: el nombre del proceso.

**operation-name**: Nombre del paso.

**taskid**: el identificador único de la tarea actual.

**actions** genera una lista numerada de rutas válidas (por ejemplo, Aprobar, Rechazar) en las que el destinatario puede hacer clic.

Además, para los recordatorios de grupo, las asignaciones de tareas de grupo y las fechas límite de grupo, también puede utilizar:

**nombre-grupo**: el nombre del grupo que tiene asignado el elemento de trabajo.

>[!NOTE]
>
>Si una variable no tiene valor, no se devuelve nada.

Para las ramas estancadas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**branch-id**: el identificador de la rama.

**process-id**: el identificador de la instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de AEM Forms

Para las operaciones estancadas, puede utilizar las siguientes variables en los cuadros Asunto y Plantilla de notificación:

**action-id**: el identificador de la operación.

**branch-id**: el identificador de la rama.

**process-id**: el identificador de la instancia de proceso.

**notification-host** El nombre de host del servidor de aplicaciones de AEM Forms

### Uso de una variable en el cuadro Asunto {#using-a-variable-in-the-subject-box}

Si escribe el siguiente texto en el cuadro Asunto de las notificaciones de asignación de tareas:

`Please complete task @@taskid@@`

El usuario recibe un mensaje de correo electrónico con el siguiente asunto si se le asigna la tarea 376:

`Please complete task 376`

### Uso de variables en el cuadro Plantilla de notificación {#using-variables-in-the-notification-template-box}

Si escribe el siguiente texto en el cuadro Plantilla de notificación para notificaciones de ramas paralizadas:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

El administrador recibe un mensaje de correo electrónico que contiene el siguiente contenido si el número de sucursal es 4868 y el nombre del servidor es `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurar conexiones de supervisión de la actividad empresarial {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, un módulo opcional, proporciona un conjunto de paneles operativos que proporcionan visibilidad en tiempo real de sus operaciones e indicadores clave de rendimiento.

En la página Valores de configuración de BAM, se establecen las conexiones al servidor que ejecuta BAM para que se pueda realizar un seguimiento de los eventos relacionados con el proceso y transmitirlos a ese servidor.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Configuración del servidor > Configuración de BAM.
1. En el cuadro Host de BAM, escriba el nombre del servidor que ejecuta BAM. El valor predeterminado es localhost.
1. En el cuadro Puerto de BAM, escriba el puerto que se utilizará para conectar con el servidor que ejecuta BAM. El puerto BAM predeterminado para JBoss es 8080, WebLogic es 7001 y WebSphere es 9080.
1. En el cuadro Host del servidor, escriba el nombre o la dirección IP del servidor host de Forms. El valor predeterminado es localhost.
1. En el cuadro Puerto del servidor, escriba el número de puerto que utiliza el servidor de Forms.
1. En los cuadros Nombre de usuario y Contraseña, escriba el Id. de usuario y la contraseña adecuados para tener acceso al servidor de BAM. El nombre de usuario predeterminado es CognosNowAdmin y la contraseña predeterminada es manager.
1. Haga clic en Guardar.
