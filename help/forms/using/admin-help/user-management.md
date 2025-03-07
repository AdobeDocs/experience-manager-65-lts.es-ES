---
title: Administración de usuarios
description: La administración de usuarios permite habilitar el SSO entre los módulos de formularios de AEM y las aplicaciones protegidas por Netegrity SiteMinder mediante SAML. Este documento proporciona más información sobre la administración de usuarios.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5a87e340-053b-4b72-99a0-df14d7bf304c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Administración de usuarios {#user-management}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La administración de usuarios permite habilitar el inicio de sesión único (SSO) entre los módulos de formularios de AEM y las aplicaciones protegidas por Netegrity SiteMinder mediante el lenguaje de marcado de aserción de seguridad (SAML). Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM Forms no son necesarias y no se muestran si el usuario ya se ha autenticado a través del portal de la empresa.

Para obtener información acerca de cómo mejorar el rendimiento de sincronización de directorios y bases de datos para DB2, vea [Base de datos IBM DB2: Ejecutar comandos para el mantenimiento regular](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Si tiene un servidor LDAP habilitado para SSL, configure Administración de usuarios para que funcione con él. (Consulte [Configurar la administración de usuarios para un servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)).

## Configurar privilegios de usuario para utilizarlos con Document Security {#setting-user-privileges-for-use-with-document-security}

Cree un usuario administrador que tenga los privilegios adecuados para crear usuarios y grupos. Si el entorno de AEM Forms incluye Document Security, conceda el privilegio de administrar usuarios invitados y locales a un usuario que sea el administrador de estos usuarios. Asigne también la función Usuario de la consola de administración para proporcionar al usuario acceso a la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Para ver los usuarios y grupos de los dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o administrador de conjuntos de directivas debe seleccionar y agregar dominios (creados en Administración de usuarios) a la lista de usuarios y grupos visibles para cada conjunto de directivas creado.

La lista de usuarios y grupos visibles está visible para el coordinador de conjuntos de directivas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregarlos a las directivas. Si no se realiza esta tarea, el coordinador del conjunto de directivas no encontrará ningún usuario o grupo que agregar a la directiva. Puede haber más de un coordinador de conjunto de directivas para un conjunto de directivas determinado.

>[!NOTE]
>
>La creación de dominios debe realizarse antes de poder crear cualquier directiva.

### Establecer usuarios y grupos visibles {#set-visible-users-and-groups}

Después de instalar y configurar el entorno de formularios de AEM con Document Security, configure todos los dominios adecuados en Administración de usuarios.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Directivas y, a continuación, haga clic en la pestaña Conjuntos de directivas.
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.
1. Vaya a Servicios > Document Security > Configuración > Mis directivas y haga clic en la pestaña Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.

## Restricciones de usuario de administrador {#administrator-user-restrictions}

Los usuarios con ciertos tipos de privilegios de administrador no pueden acceder a las páginas web del usuario final de Workspace por motivos de seguridad. Dado que estas páginas web pueden existir fuera de un firewall, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. Solo los usuarios que tienen privilegios de administrador de Workspace o de usuario de Workspace pueden acceder a las páginas web del usuario final.

>[!NOTE]
>
>Flex Workspace está en desuso para la versión de formularios de AEM.
