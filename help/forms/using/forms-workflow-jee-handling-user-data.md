---
title: Flujos de trabajo JEE de Forms | Gestión de datos de usuario
description: Aprenda a utilizar los flujos de trabajo de JEE de AEM Forms para diseñar, crear y administrar procesos empresariales.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 80%

---

# Flujos de trabajo JEE de Forms | Gestión de datos de usuario {#forms-jee-workflows-handling-user-data}

Los flujos de trabajo de AEM Forms JEE proporcionan herramientas para diseñar, crear y administrar procesos empresariales. Un proceso de flujo de trabajo consiste en una serie de pasos que se ejecutan en un orden especificado. Cada paso realiza una acción específica, como asignar una tarea a un usuario o enviar un mensaje de correo electrónico. Un proceso puede interactuar con recursos, cuentas de usuario y servicios, y se puede activar mediante cualquiera de los siguientes métodos:

* Iniciar un proceso desde AEM Forms Workspace
* Usar el servicio SOAP o el servicio RESTful
* Enviar un formulario adaptable
* Usar una carpeta inspeccionada
* Usar el correo electrónico

Para obtener más información sobre la creación del proceso de flujo de trabajo JEE de AEM Forms, consulte la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65_es).

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

Cuando se activa un proceso, y a medida que avanza, captura datos sobre sus participantes, los datos introducidos por estos en el formulario asociado al proceso y los archivos adjuntos agregados al formulario. Los datos se almacenan en la base de datos del servidor JEE de AEM Forms y, si se configuran, algunos datos, como los archivos adjuntos, se almacenan en el directorio Global Document Storage (GDS). El directorio GDS se puede configurar en un sistema de archivos compartido o en una base de datos.

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Cuando se activa un proceso, se genera un ID de instancia de proceso único y un ID de invocación de larga duración que se asocian a la instancia del proceso. Puede acceder a los datos de una instancia de proceso y eliminarlos en función del ID de invocación de larga duración. Puede deducir el ID de invocación de larga duración de una instancia de proceso con el nombre de usuario del iniciador del proceso o los participantes en el proceso que han enviado sus tareas.

Sin embargo, no es posible identificar el ID de instancia de proceso de un iniciador en los siguientes casos:

* **El proceso se ha activado a través de una carpeta inspeccionada**: una instancia de proceso no se puede identificar por su iniciador si el proceso se activa mediante una carpeta inspeccionada. En este caso, la información del usuario se codifica en los datos almacenados.
* **El proceso se ha iniciado desde una instancia de publicación de AEM**: ninguna de las instancias de proceso activadas desde una instancia de publicación de AEM captura información sobre el iniciador. Sin embargo, los datos de usuario se pueden capturar en el formulario asociado al proceso, el cual se almacena en variables de flujo de trabajo.
* **El proceso se ha iniciado por correo electrónico**: el ID de correo electrónico del remitente se captura como una propiedad en una columna blob opaca de la tabla de bases de datos `tb_job_instance`, la cual no se puede consultar directamente.

### Identificar los ID de instancia de proceso cuando se conoce el iniciador o un participante del flujo de trabajo {#initiator-participant}

Realice los siguientes pasos para identificar los ID de instancia de proceso del iniciador o el participante de un flujo de trabajo:

1. Ejecute el siguiente comando en la base de datos de AEM Forms Server para recuperar el ID principal del iniciador o participante del flujo de trabajo de la tabla de base de datos `edcprincipalentity`.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La consulta devuelve el ID principal del `user_ID` especificado.

1. (**Para el iniciador del flujo de trabajo**) Ejecute el siguiente comando para recuperar todas las tareas asociadas al ID principal del iniciador de la tabla de bases de datos `tb_task`.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La consulta devuelve las tareas iniciadas por el `initiator`_ `principal_id` especificado. Las tareas son de dos tipos:

   * **Tareas completadas**: estas tareas se han enviado y muestran un valor alfanumérico en el campo `process_instance_id`. Tome nota de todos los ID de instancia de proceso de las tareas enviadas y continúe con los pasos.
   * **Tareas iniciadas pero no completadas**: estas tareas se han iniciado, pero aún no se han enviado. El valor del campo `process_instance_id` de estas tareas es **0** (cero). En este caso, tome nota de los ID de tarea correspondientes y consulte [Trabajo con tareas huérfanas](#orphan).

1. (**Para los participantes del flujo de trabajo**) Ejecute el siguiente comando para recuperar los ID de instancia de proceso asociados al ID principal del participante del proceso del iniciador de la tabla de bases de datos `tb_assignment`.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La consulta devuelve los ID de instancia de todos los procesos asociados a ese participante, incluidos aquellos en los que el participante no ha enviado ninguna tarea.

   Tome nota de todos los ID de instancia de proceso de las tareas enviadas y continúe con los pasos.

   Para las tareas huérfanas o aquellas tareas en las que el `process_instance_id` es 0 (cero), tome nota de los ID de tarea correspondientes y consulte [Trabajo con tareas huérfanas](#orphan).

1. Siga las instrucciones de la sección [Purgar datos de usuario de instancias de flujo de trabajo según los identificadores de instancia de proceso](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) para poder eliminar los datos de usuario de los identificadores de instancia de proceso identificados.

### Identificar los ID de instancia de proceso cuando los datos de usuario se almacenan en variables primitivas {#primitive}

Se puede diseñar un flujo de trabajo de modo que los datos del usuario se capturen en una variable que se almacene como un blob en la base de datos. En estos casos, los datos de usuario solo se pueden consultar si están almacenados en una de las siguientes variables de tipo primitivo:

* **Cadena**: contiene el ID de usuario directamente o como subcadena y se puede consultar mediante SQL.
* **Numérico**: contiene directamente el ID de usuario.
* **XML**: contiene el ID de usuario como una subcadena dentro del texto almacenado como columnas de texto en la base de datos, y se puede consultar en forma de cadenas.

Realice los siguientes pasos para determinar si un flujo de trabajo que almacena datos en variables de tipo primitivo contiene datos del usuario:

1. Ejecute el siguiente comando de base de datos:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La consulta devuelve un nombre de tabla con el formato `tb_<number>` para la aplicación y el flujo de trabajo especificados (`app_name`) y (`workflow_name`).

   >[!NOTE]
   >
   >El valor de la propiedad `name` puede ser complejo si el flujo de trabajo está anidado en subcarpetas dentro de la aplicación. Asegúrese de especificar la ruta completa exacta al flujo de trabajo, que puede obtener de la tabla de bases de datos `omd_object_type`.

1. Revise el esquema de tabla `tb_<number>`. La tabla contiene variables que almacenan los datos de usuario del flujo de trabajo especificado. Las variables de la tabla corresponden a las variables del flujo de trabajo.

   Identifique y tome nota de la variable que corresponde a la variable de flujo de trabajo que contiene el ID de usuario. Si la variable identificada es de tipo primitivo, puede ejecutar una consulta para determinar las instancias de flujo de trabajo asociadas a un ID de usuario.

1. Ejecute el siguiente comando de base de datos. En este comando, la variable `user_var` es la variable de tipo primitivo que contiene el ID de usuario.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La consulta devuelve todos los ID de instancia de proceso asociados al `user_ID` especificado.

1. Siga las instrucciones de la sección [Purgar datos de usuario de instancias de flujo de trabajo según los identificadores de instancia de proceso](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) para poder eliminar los datos de usuario de los identificadores de instancia de proceso identificados.

### Purgar los datos de usuario de las instancias de flujo de trabajo en función de los ID de instancia de proceso {#purge}

Ahora que ha identificado los ID de instancia de proceso asociados a un usuario, siga los siguientes pasos para eliminar los datos de usuario de las instancias de proceso correspondientes.

1. Ejecute el siguiente comando para poder recuperar el ID de invocación de larga duración y el estado de una instancia de proceso de la tabla `tb_process_instance`.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La consulta devuelve el ID de invocación de larga duración y el estado del `process_instance_id` especificado.

1. Cree una instancia del cliente público `ProcessManager` cliente (`com.adobe.idp.workflow.client.ProcessManager`) usando una instancia de `ServiceClientFactory` con la configuración de conexión correcta.

   Para obtener más información, consulte Referencia de la API de Java™ para [Class ProcessManager](https://helpx.adobe.com/es/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Compruebe el estado de la instancia del flujo de trabajo. Si el estado es distinto de 2 (COMPLETADA) o 4 (TERMINADA), termine la instancia primero llamando al siguiente método:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Purgue la instancia del flujo de trabajo llamando al siguiente método:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   El método `purgeProcessInstance` elimina por completo todos los datos del identificador de invocación especificado de la base de datos de AEM Forms Server y GDS, si están configurados.

### Trabajar con tareas huérfanas {#orphan}

Las tareas huérfanas son tareas cuyo proceso contenedor se ha iniciado, pero aún no se ha enviado. En este caso, `process_instance_id` es **0** (cero). Por lo tanto, no puede realizar un seguimiento de los datos de usuario de tareas huérfanas almacenados utilizando ID de instancias de proceso. Sin embargo, puede realizar un seguimiento de estos datos usando el ID de tarea de una tarea huérfana. Puede identificar los ID de tarea de la tabla `tb_task` de un usuario como se describe en [Identifique los ID de instancia de proceso cuando se conozca el iniciador o participante del flujo de trabajo](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Una vez que tenga los ID de tarea, siga los siguientes pasos para purgar los archivos y los datos asociados con una tarea huérfana de GDS y de la base de datos.

1. Ejecute el siguiente comando en la base de datos de AEM Forms Server para poder recuperar los ID de tarea identificados.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La consulta devuelve una lista de ID. Para cada ID (`fd_id`) que se devuelve en los resultados, cree una lista de cadenas de ID de sesión de la siguiente manera:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Dependiendo de si el GDS apunta a un sistema de archivos o a una base de datos, realice uno de los siguientes pasos:

   1. **GDS en un sistema de archivos**

      En el sistema de archivos GDS:

      1. Busque archivos con las siguientes cadenas de ID de sesión como extensiones:

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Los archivos con estas extensiones son los archivos de marcador. Se almacenan con nombres de archivo en el siguiente formato:

      `<file_name_guid>.session<session_id_string>`

      1. Elimine todos los archivos de marcador y otros archivos con ese nombre de archivo exacto como `<file_name_guid>` del sistema de archivos.

   1. **GDS en una base de datos**

      Ejecute los siguientes comandos para cada ID de sesión:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. Ejecute los siguientes comandos para poder eliminar los datos de los ID de tarea de la base de datos de AEM Forms Server:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
