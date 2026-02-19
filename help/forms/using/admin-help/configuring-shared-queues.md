---
title: Configurar colas compartidas
description: Las colas compartidas permiten configurar y administrar las colas de usuario de forma eficaz. Obtenga información sobre cómo configurar colas compartidas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6665b95a-39fd-472a-b3b5-8b97257c69a7
source-git-commit: 66696da39b1b790b2155b2ec08d936371f87b979
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Configurar colas compartidas{#configuring-shared-queues}

Las colas compartidas permiten configurar y administrar las colas de usuario de forma eficaz. Una cola de usuarios son simplemente todas las tareas asignadas a un usuario. Vea [Listas de tareas pendientes](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) para obtener más información. Puede asignar, anular la asignación y reasignar colas de usuario según sus necesidades organizativas. Puede administrar colas compartidas de dos formas:

**Administrar El Acceso A Un Usuario**

Puede administrar el acceso a una cola de usuario seleccionada mediante esta opción.

**Administrar El Acceso De Un Usuario**

Puede administrar las colas compartidas asignadas a un usuario seleccionado mediante esta opción.

## Administrar el acceso a una cola de usuarios seleccionada {#managing-access-to-a-selected-user-queue}

La funcionalidad Administrar el acceso a un usuario permite administrar el acceso a una cola de usuarios seleccionada. Puede conceder o revocar el acceso a una cola de usuario seleccionada a otros usuarios de su organización. Por ejemplo, Kara Bowman está fuera de la oficina. Con la funcionalidad Administrar el acceso a un usuario, la cola de Kara se puede compartir con Akira Tanaka y John Jacobs para su finalización. En un momento posterior, cuando Kara vuelva a la oficina, podrá revocar el acceso a su cola a Akira Tanaka y John Jacobs.

Una vez compartidas, el usuario puede completar estas tareas, con acceso a la cola, mediante Workspace.

>[!NOTE]
>
>Flex Workspace ya no se utiliza para la versión de formularios AEM.

### Configurar el acceso a una cola de usuarios seleccionada {#configuring-access-to-a-selected-user-queue}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > **Forms Workflow** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione el usuario. Haga clic en Compartir.
1. Haga clic en Guardar para completar el proceso.

### Revocar acceso a una cola de usuario seleccionada {#revoking-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > **Forms Workflow** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desee administrar.
1. El panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada. Seleccione el usuario y haga clic en Revocar.
1. Haga clic en Guardar para completar el proceso.

## Administrar colas asignadas a un usuario {#managing-queues-assigned-to-a-user}

La funcionalidad Administrar el acceso de un usuario permite administrar las colas asignadas a un usuario seleccionado. Puede conceder o revocar el acceso a las colas de usuario a un usuario seleccionado de forma individual. Por ejemplo, desea asignar las colas de usuario de Akira Tanaka y John Jacobs a Kara Bowman. Con la funcionalidad Administrar el acceso de un usuario, puede buscar Kara Bowman y conceder acceso a las tareas asignadas a Akira Tanaka y John Jacobs. En un momento posterior, puede revocar el acceso de Kara Bowman a estas colas de usuarios.

Una vez asignadas, el usuario puede completar estas tareas mediante Workspace.

>[!NOTE]
>
>Flex Workspace ya no se utiliza para la versión de formularios AEM.

### Conceder acceso a una cola de usuario seleccionada {#granting-access-to-a-selected-user-queue}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > **Forms Workflow** > **Cola compartida**.

1. En la pestaña Administrar el acceso a un usuario, busque y seleccione el usuario cuya cola desee compartir. En cualquier momento, el panel inferior derecho muestra la lista de usuarios con acceso a la cola de usuarios seleccionada.
1. En el panel inferior izquierdo, busque y seleccione las colas de usuario que desea compartir con el usuario seleccionado. Haga clic en Compartir.
1. Haga clic en Guardar para completar el proceso.

### Revocar acceso a una cola de usuario seleccionada {#revoking_access_to_a_selected_user_queue-1}

1. Inicie sesión en la consola de administración con una cuenta de administrador.
1. Seleccione **Servicios** > **Forms Workflow** > **Cola compartida**.

1. En la pestaña Administrar el acceso de un usuario, busque y seleccione el usuario cuya cola desea administrar.
1. El panel inferior derecho muestra la lista de colas de usuario asignadas al usuario seleccionado. Seleccione la cola del usuario y haga clic en Revocar.
1. Haga clic en Guardar para completar el proceso.
