---
title: Crear y configurar roles
description: Obtenga información sobre cómo asociar usuarios y grupos con funciones que ya forman parte de la base de datos de administración de usuarios. También puede crear, editar y eliminar roles.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: c68c602f-fa93-4e3d-9a8c-b61c3ab53000
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2495'
ht-degree: 0%

---

# Crear y configurar roles{#creating-and-configuring-roles}

Mediante las páginas web de Administración de usuarios, puede asociar usuarios y grupos con roles que ya forman parte de la base de datos de Administración de usuarios. También puede crear, editar y eliminar roles.

Administración de usuarios tiene dos tipos de funciones:

**Funciones mutables:** Este tipo de función se puede editar y eliminar, y los permisos de función se pueden agregar y eliminar de estos tipos de función. Cualquier función que cree se considerará una función mutable. Puede agregar o quitar usuarios y grupos asignados a funciones mutables.

**Funciones inmutables:** Las funciones predeterminadas que se incluyen en Administración de usuarios son funciones inmutables. Estas funciones no se pueden editar ni eliminar. Sin embargo, puede agregar o quitar usuarios y grupos asignados a funciones inmutables.

Las funciones mutables e inmutables también se pueden crear mediante las API de formularios AEM Forms.

## Funciones predeterminadas {#default-roles}

Las siguientes funciones predeterminadas se incluyen en la base de datos de administración de usuarios.

**Usuario de la consola de administración:** puede acceder a la consola de administración.

**Administrador de aplicaciones:** puede usar todas las características de Workbench. Puede utilizar las páginas Aplicaciones y servicios de la consola de administración para configurar las propiedades, los extremos y la seguridad del servicio en tiempo de ejecución.

**Administrador de formularios AEM Forms:** puede realizar todas las tareas para todos los servicios instalados.

**Administrador de seguridad:** controla la configuración de Administración de usuarios y administra los usuarios y grupos asociados a cualquier dominio de Administrador de usuarios

**Usuario de servicios:** puede ver e invocar cualquier servicio

**Superadministrador:** tiene acceso a todas las funciones administrativas del sistema, incluidos los servicios

**Administrador de confianza:** puede administrar la configuración de confianza de PKI y las credenciales de PKI administradas desde la página Administración del almacén de confianza en la consola de administración

### Funciones predeterminadas adicionales {#additional-default-roles}

Se pueden incluir las siguientes funciones predeterminadas adicionales, en función de los componentes de formularios AEM Forms que haya instalado

**Usuario de aplicación de carga de documentos:** puede cargar documentos mediante Flex Remoting.

**Administrador de Forms:** puede ver y modificar la configuración de la página de Forms en la consola de administración

**Administrador del espacio de contenido de formularios AEM Forms:** puede ver y modificar la configuración de la página Servicios de contenido (obsoleto) en la consola de administración

**Usuario de Contentspace de formularios AEM:** puede iniciar sesión en las páginas web de Contentspace (obsoleto)

**Administrador de Conector de Documentum:** Puede ver y modificar la configuración desde la página Documentum de Connector para EMC en la consola de administración

**Administrador del conector FileNet de formularios AEM:** puede ver y modificar la configuración de la página Conector para FileNet de IBM en la consola de administración

**Administrador del conector IBM CM de AEM Forms:** puede ver y modificar la configuración desde la página Conector para el administrador de contenido de IBM en la consola de administración

**Administrador de Rights Management:** realiza todas las tareas necesarias para todas las configuraciones de servidor en las páginas relevantes de Rights Management

**Usuario final de Rights Management:** Puede acceder a las páginas web de los usuarios finales de Rights Management

**Usuario invitado de Rights Management:** puede invitar a usuarios

**Rights Management administra usuarios invitados y locales:** puede realizar las tareas necesarias para administrar todos los usuarios invitados y locales en las páginas relevantes de Rights Management

**Administrador de conjunto de directivas de Rights Management:** realiza todas las tareas necesarias para todos los conjuntos de directivas en las páginas relevantes de Rights Management

**Superadministrador de Rights Management:** Realiza todas las tareas necesarias desde la página de Rights Management

**Administrador de AEM Forms Workspace:** Puede ver y modificar la configuración de la página de Workspace en la consola de administración

***nota &#x200B;**: Flex Workspace está obsoleto para la versión de formularios de AEM.*

**Usuario de Workspace:** puede iniciar sesión en la aplicación de usuario final de Workspace

**Administrador de salida:** puede ver y modificar la configuración desde la página Salida en la consola de administración

**Administrador de PDFG:** puede ver y modificar la configuración desde la página de PDF Generator en la consola de administración

**Usuario de PDFG:** puede acceder a todas las funciones que no sean administrativas de PDF Generator

**Aplicación web de extensiones de Acrobat Reader DC:** Puede usar la aplicación web de extensiones de Acrobat Reader DC

>[!NOTE]
>
>Los usuarios con ciertos tipos de privilegios de administrador no pueden acceder a las páginas web del usuario final de Workspace por motivos de seguridad. Dado que estas páginas pueden existir fuera de un cortafuegos, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. Solo los usuarios que tengan los privilegios de administrador de AEM Forms Workspace o usuario de AEM Forms Workspace pueden acceder a las páginas web del usuario final de Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.

## Crear una función {#create-a-role}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. En el cuadro Nombre de función, escriba un nombre para la función y, opcionalmente, escriba una descripción de la función y, a continuación, haga clic en Siguiente.

   >[!NOTE]
   >
   >Al utilizar MySQL, no se pueden crear dos funciones que tengan el mismo nombre pero que difieran en el uso de caracteres extendidos. Por ejemplo, si se intenta crear una función denominada abcde cuando ya existe una denominada âbcdè, se producirá un error.

1. Haga clic en Buscar permisos y seleccione los permisos que desea agregar a la función.
1. Haga clic en Aceptar y, a continuación, en Siguiente.
1. Asigne esta función a usuarios y grupos:

   * Haga clic en Buscar usuarios/grupos.
   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione Nombre, Correo electrónico o ID de usuario y, a continuación, Usuarios, Grupos o Usuarios y grupos.
   * Seleccione el dominio, seleccione el número de resultados que desea mostrar y haga clic en Buscar.
   * Seleccione las casillas de verificación de los usuarios y grupos a los que desea asignar esta función y haga clic en Aceptar.

1. Para ver los detalles del usuario y del grupo, seleccione la entidad.
1. Haga clic en Aceptar y, a continuación, en Finalizar.

## Editar una función {#edit-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Haga clic en la función que desea editar, edite la configuración general y haga clic en Guardar.
1. Para editar permisos de funciones, haga clic en la pestaña Permisos y realice las siguientes tareas:

   * Para agregar nuevos permisos, haga clic en Buscar permisos, active las casillas de verificación de los permisos que desea agregar, haga clic en Aceptar y, a continuación, haga clic en Guardar.
   * Para eliminar un permiso de la función, active la casilla de verificación del permiso, haga clic en Eliminar y, a continuación, haga clic en Guardar.

1. Para administrar a quién está asignado el rol, haga clic en la ficha Usuarios del rol y realice las tareas siguientes:

   * Para asignar la función a nuevos usuarios y grupos, haga clic en Buscar usuarios/grupos y complete la información de búsqueda. Active la casilla de verificación de cada usuario y grupo al que desee asignar esta función, haga clic en Aceptar y, a continuación, en Guardar.
   * Para quitar la función, active la casilla de verificación de los usuarios o grupos, haga clic en Anular asignación y, a continuación, haga clic en Guardar.

## Eliminar un rol {#delete-a-role}

Puede eliminar cualquiera de las funciones que ha creado, pero no las funciones predeterminadas de los formularios AEM Forms que se incluyen en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Active la casilla de verificación de la función que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Asignar una función a usuarios y grupos {#assign-a-role-to-users-and-groups}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique información para limitar la búsqueda y haga clic en Buscar. Los resultados de la búsqueda se muestran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Seleccione las casillas de verificación situadas junto a los usuarios y grupos que desea asociar a un rol y haga clic en Asignar rol.
1. Seleccione la función que desea asignar al usuario o grupo y haga clic en Aceptar.

También puede asignar funciones mediante la página Administración de funciones.

## Determinar quién está asignado a un rol {#determine-who-is-assigned-to-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. En la página Detalles del rol, haga clic en la ficha Usuarios del rol. Se muestra una lista de usuarios y grupos asociados directamente con la función.

## Cambiar permisos de funciones {#change-role-permissions}

Puede cambiar los permisos de cualquiera de las funciones que ha creado. No puede cambiar los permisos de las funciones predeterminadas de los formularios AEM Forms que se incluyen en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Seleccione la función para la que desea ver los permisos y haga clic en la pestaña Permisos.
1. Para cambiar estos permisos, haga clic en Buscar permisos, active las casillas de verificación de los permisos que desea agregar a la función, haga clic en Aceptar y, a continuación, haga clic en Guardar.
1. Para eliminar un permiso, selecciónelo, haga clic en Eliminar y, a continuación, haga clic en Guardar.

### Permisos de formularios AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Agregar, quitar y modificar extremos de un servicio

**Inicio de sesión de Admin Console:** Ver la consola de administración

**Modificación de certificado:** Modifique la configuración de confianza de cualquier certificado del Almacén de confianza

**Lectura de certificado:** Leer cualquier certificado del Almacén de confianza

**Escritura de certificado:** Agregue un certificado al Almacén de confianza

**Agregar componente:** Instale un nuevo componente en el sistema

**Eliminar componente:** Eliminar cualquier componente del sistema

**Lectura de componente:** Lectura de cualquier componente del sistema

**Administrador de Contentspace:** Permiso para el administrador de Contentspace (obsoleto)

**Inicio de sesión en la consola de Contentspace:** Permiso para el inicio de sesión en la consola de Contentspace (obsoleto)

**Control de configuración principal:** Administre la configuración en la página Configuración del sistema principal de la consola de administración

**CREATE_VERSION_PERM:** Cree una versión de un servicio

**Modificación de credencial:** Modifique cualquier credencial de firma en el Almacén de confianza

**Lectura de credencial:** Leer cualquier credencial de firma en el almacén de confianza

**Escritura de credencial:** Agregue una credencial de firma al Almacén de confianza

**Modificación de CRL:** Modificar cualquier CRL (Lista de revocación de certificados) en el Almacén de confianza

**Lectura de CRL:** Leer cualquier CRL en el Almacén de confianza

**Escritura de CRL:** Agregar una CRL al Almacén de confianza

**Delegado:** Establecer una ACL en un recurso

**DELETE_VERSION_PERM:** Eliminar una versión de un servicio

**Carga de documentos:** Cargar documentos en formularios de AEM

**Control de dominio:** Cree, elimine o modifique la configuración de cualquier dominio de administración de usuarios, incluidos los proveedores de autenticación y directorio

**Editar tipo de evento:** Editar en tipos de evento

**Control de suplantación de identidad:** suplantar identidad en el Administrador de usuarios

**INVOKE_PERM:** Invocar todas las operaciones de un servicio

**Control de modelo de datos LCDS:** leer e implementar modelos de datos en los servicios de datos

**Actualización del Administrador de licencias:** Actualizar información de licencia

**MODIFY_CONFIG_PERM:** Modificar la configuración de un servicio

**TERM** Modificar la versión de un servicio

**PDFGAdminPermission:** administrador de PDFG

**PDFGUserPermission:** usuario de PDFG

**PERM_DCTM_ADMIN:** administrador de Documentum Connector

**PERM_FILENET_ADMIN:** Administrador del conector FileNet

**PERM_FORMS_ADMIN:** administrador de Forms

**PERM_IBMCM_ADMIN:** Administrador del conector IBM CM

**PERM_OUTPUT_ADMIN:** Administrador de salida

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Utilice la aplicación web de extensiones de Acrobat Reader DC

**PERM_SP_ADMIN:** Administrar la configuración del conector de SharePoint

**PERM_WORKSPACE_ADMIN:** Administrar la configuración de Workspace

**PERM_WORKSPACE_USER:** Inicie sesión en la aplicación de usuario final de Workspace

**Control principal:** administre usuarios y grupos para cualquier dominio y administre asignaciones de roles para todos los usuarios y grupos de cualquier dominio

**Leer/Eliminar grabación de procesos:** Enumerar y recuperar instancias de auditoría de flujo de trabajo

**PROCESS_OWNER_PERM:** Ver datos de tendencia y realizar acciones administrativas en un servicio creado a partir de un proceso

**Leer:** leer el contenido de un recurso

**READ_PERM:** leer o ver un servicio

**Renovar aserción:** Renovar aserciones en Administración de usuarios

**Delegado de repositorio:** Establecer una ACL en un recurso

**Lectura de repositorio:** Leer el contenido de un recurso

**Recorrido del repositorio:** Incluya un recurso en una solicitud de recursos de lista o lea los metadatos de un recurso

**Escritura del repositorio:** Escribir metadatos y contenido del repositorio

**Propietario de cambio de directiva de Rights Management:** Cambiar propietario de directiva

**Inicio de sesión en la consola del usuario final de Rights Management:** Inicie sesión en la interfaz de usuario del usuario final de Rights Management

**Configuración de administración de Rights Management:** Administrar la configuración del servidor

**Rights Management administra usuarios invitados y locales:** administra usuarios invitados y locales

**Rights Management Administrar conjuntos de directivas:** Administrar todas las directivas y documentos dentro de cualquier conjunto de directivas

**Coordinador de adición del conjunto de directivas de Rights Management:** Agregar, quitar y cambiar permisos para coordinadores de conjuntos de directivas

**Conjunto de directivas de Rights Management Crear directiva:** Cree una directiva para un conjunto de directivas

**Directiva de eliminación de conjunto de directivas de Rights Management:** Quitar una directiva de un conjunto de directivas

**Editar conjunto de directivas de Rights Management:** Editar una directiva en un conjunto de directivas

**Conjunto de directivas de Rights Management Administrar editor de documentos:** Cuando crea conjuntos de directivas, asigna a los usuarios la función de editor de documentos. El editor del documento es el usuario que protege el documento con una directiva.

**Coordinador de eliminación de conjunto de directivas de Rights Management:** Quitar un coordinador de conjunto de directivas de un conjunto de directivas

**Documento revocado del conjunto de directivas de Rights Management:** Revocar acceso a documentos de un conjunto de directivas

**Directiva de modificador de conjunto de directivas de Rights Management:** directivas de modificador para un documento

**Documento sin revocar conjunto de directivas de Rights Management:** anular la revocación de un documento

**Evento de vista del conjunto de directivas de Rights Management:** vea los eventos de directivas y documentos de cualquier directiva o documento de un conjunto de directivas

**Eventos del servidor de vista de Rights Management:** Buscar y ver todos los eventos de auditoría

**Control de roles:** Crear, eliminar y modificar roles en Administración de usuarios

**Servicio activado:** Inicie cualquier servicio, para que esté disponible para la invocación

**Servicio agregado:** Implementar un nuevo servicio en el registro de servicios. Esto incluye añadir nuevos procesos y variantes de proceso

**Desactivación del servicio:** Detenga cualquier servicio del sistema

**Eliminación de servicio:** Elimine cualquier servicio del sistema, incluidos los procesos y las variantes de proceso

**Invocación de servicio:** Invoca cualquier servicio del registro de servicios disponible durante la ejecución

**Modificación del servicio:** Modifique las propiedades de configuración de cualquier servicio del sistema. Esto incluye bloquear y desbloquear un servicio en el IDE, y agregar o quitar extremos de un servicio

**Lectura de servicio:** Lectura de cualquier servicio del sistema. Esto incluye todos los procesos y variantes de procesos

**SERVICE_AGENT_PERM:** Ver datos e interactuar con instancias de proceso para un servicio creado a partir de un proceso

**SERVICE_MANAGER_PERM:** Realice acciones de equilibrio de carga y otras acciones administrativas en un servicio creado a partir de un proceso

**START_STOP_PERM:** Iniciar o detener un servicio

**SUPERVISOR_PERM:** Ver datos de instancia de proceso de un servicio creado a partir de un proceso

**Recorrer:** Incluir un recurso en una solicitud de recursos de lista o leer los metadatos de un recurso

**Escribir:** escribir metadatos y contenido del repositorio

**Abrir archivos en Workbench**

Para ver el contenido de la vista Recursos en Workbench y abrir archivos para verlos, un usuario necesita los siguientes permisos:

* Lectura de repositorio
* Recorrido del repositorio
* Invocación de servicio
* Lectura de servicio

## Quitar un usuario o grupo de una función {#remove-a-user-or-group-from-a-role}

Utilice la página Administración de Roles para eliminar usuarios y grupos de un rol concreto. Si el usuario o grupo heredó la asignación de funciones, no se puede quitar la función en el nivel de usuario o grupo. Quite el usuario o el grupo del árbol de herencia o quite la función del elemento principal.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. En la lista de funciones, haga clic en el nombre de la función que desea actualizar y, a continuación, haga clic en la ficha Usuarios de la función. Se mostrará una lista de los usuarios y grupos asociados a la función.
1. Seleccione las casillas de verificación de los usuarios y grupos que desea quitar de la función y haga clic en Anular asignación.
1. Haga clic en Guardar y luego en Aceptar.
