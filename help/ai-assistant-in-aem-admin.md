---
title: Configuración del asistente de IA en AEM
description: Obtenga información sobre cómo configurar el asistente de IA mediante Admin Console en Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3cf3d5c83a91fbc582840c2a3b11b3b705f86712
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Configuración del asistente de IA en AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Para utilizar el asistente de IA en AEM (Adobe Experience Manager), su organización debe registrarse en el nivel de Admin Console. Un administrador de productos crea (o elige) un grupo de usuarios y le concede el nuevo permiso &quot;Asistente de IA&quot;. Cualquier persona agregada a ese grupo accede instantáneamente al asistente de IA en AEM. Si el objetivo es la disponibilidad en toda la compañía, el administrador simplemente asigna todos los usuarios a ese grupo.

Desde la perspectiva de un empleado, el proceso es sencillo: identifique al administrador de productos de Adobe Experience Manager en su organización y solicite que se le añada al grupo de usuarios con IA habilitada. Una vez que aparezca en ese grupo, el icono Ayudante se mostrará automáticamente la próxima vez que inicie sesión.

Los administradores deben tener en cuenta el control normal de Cloud Manager. Mantenga los derechos de administrador de productos en Admin Console para crear perfiles, administrar grupos de usuarios o editar permisos. Si los usuarios también necesitan la característica **Crear vale de soporte** integrada del Ayudante, agregue el rol estándar **Administrador de soporte** (rol estándar de Admin Console) a las mismas personas o grupos.

El proceso de configuración del asistente de IA en AEM consta de los siguientes pasos:

1. [Crear un nuevo perfil de producto en Adobe Admin Console](#create-profile).
1. [Habilite el permiso Conocimiento del producto del Asistente para IA](#enable-permission).
1. [Crear un nuevo grupo de usuarios (o usar uno existente)](#create-user-group).
1. [Agregar usuarios al grupo](#add-users).
1. [Asigne el perfil de producto al grupo de usuarios](#assign-product-profile).

**Requisitos previos**

Antes de empezar, asegúrese de cumplir los siguientes requisitos previos:

* Debe tener derechos de administrador de productos como mínimo en Adobe Admin Console.
* Tiene una comprensión de la estructura de administración de usuarios de su organización.

**Consideraciones de configuración**

* Tiempo de procesamiento: Los recursos creados en Cloud Manager pueden tardar hasta 2 minutos en mostrarse en Admin Console para la configuración de permisos.
* Múltiples perfiles: los usuarios pueden formar parte de varios perfiles y los permisos se combinan de todos los perfiles asignados.
* Ámbito de organización: algunos permisos pueden aplicarse en el nivel de organización en todos los programas.
* Perfiles predefinidos: no elimine perfiles de permiso predefinidos de Admin Console.


## 1 - Crear un nuevo perfil de producto en Adobe Admin Console{#create-profile}

1. Siga las instrucciones detalladas de [Crear un nuevo perfil de producto en Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) que se encuentra en la documentación de Experience Platform.

1. Al crear el nuevo perfil de producto, puede utilizar los siguientes valores sugeridos para el asistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nombre del perfil del producto | `AI Assistant in AEM` (o su nombre descriptivo preferido) |
   | Nombre para mostrar (opcional) | `AI Assistant` |
   | Descripción (opcional) | `Product profile for managing AI Assistant in AEM access` |
   | Notificación | Configure en función de las preferencias de su organización |


## 2 - Habilite el permiso Conocimiento del producto del asistente de IA{#enable-permission}

El proceso de asignación de permisos personalizados a perfiles de producto sigue el flujo de trabajo estándar de permisos personalizados de Adobe Cloud Manager.

Artículo de referencia: [Asignar permisos personalizados al nuevo perfil de producto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. En Admin Console, haga clic en el nombre del perfil de producto recién creado (`AI Assistant in AEM`)

   ![Captura de pantalla](/help/assets/assets-ai/ai-assistant-console.png)

1. Para ver la lista de permisos editables, haga clic en la ficha **Permisos**.

1. En la lista de la tabla, busque el permiso `AI Assistant Product Knowledge`.

   ![Pestaña Permisos del asistente de IA en Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. A la derecha del nombre del permiso, haga clic en ![Icono de lápiz o Editar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. En la página **Editar permisos para el asistente de IA**, active la opción **Conocimiento del producto del asistente de IA**.

   ![Editar página de permisos para la opción de alternancia Conocimiento del producto del Asistente de IA](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.

   El perfil de producto ahora tiene habilitado el permiso Conocimiento del producto del asistente de IA.


## 3 - Crear un grupo de usuarios nuevo (o usar uno existente){#create-user-group}

1. Realice una de las siguientes acciones:

>[!BEGINTABS]

>[!TAB Crear un nuevo grupo de usuarios]

1. En Admin Console, haga clic en **Usuarios** > **Grupos de usuarios**.

   ![Grupos de usuarios](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. En la página **Grupos de usuarios**, haga clic en **Nuevo grupo de usuarios**.

   ![Botón Nuevo grupo de usuarios en la página Grupos de usuarios](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. En la página **Crear un nuevo grupo de usuarios**, proporcione la siguiente información:

   | Opción | Valor sugerido |
   | --- | --- |
   | Nombre del grupo de usuarios | `AI Assistant in AEM` (o su nombre preferido) |
   | Descripción (opcional) | `User group for managing AI Assistant in AEM access` |

   ![Crear una nueva página de grupo de usuarios](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.

>[!TAB Usar un grupo de usuarios existente]

Puede utilizar un grupo de usuarios de AEM existente si cumple los requisitos de acceso del Asistente de IA, en lugar de crear un nuevo grupo.

>[!ENDTABS]

## 4 - Añadir usuarios al grupo de usuarios{#add-users}

1. Realice una de las siguientes acciones:

>[!BEGINTABS]

>[!TAB Agregar usuarios individuales]

1. En la página **Grupos de usuarios**, en la tabla **Nombre de grupo**, haga clic en el nombre del grupo de usuarios que acaba de crear o en un nombre de grupo de usuarios existente.

   ![Página de grupos de usuarios que muestra el Asistente de IA en el nombre del grupo de usuarios de AEM en la tabla](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. En la página **Grupos de usuarios** para el **Asistente de IA en AEM**, haga clic en la ficha **Usuarios** y, a continuación, haga clic en **Agregar usuarios**.

   ![El Asistente de IA en la página de grupos de usuarios de AEM, que muestra la ficha Usuarios y la botón Agregar usuarios](/help/assets/assets-ai/ai-assistant-add-users.png)

1. En la página **`Add users to this user group`**, busque y seleccione usuarios que necesiten acceder al asistente de IA en AEM.

   ![Agregar usuarios a esta página de grupo de usuarios](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.
1. Ahora, [asigne el perfil de producto al grupo de usuarios](#assign-product-profile).

>[!TAB Agregar usuarios de forma masiva]

Puede utilizar la función de carga masiva en Admin Console.

1. Prepare un archivo CSV con información de usuario.
1. Utilice la opción **`Add users by CSV`** para una adición masiva eficiente.
1. Ahora, [asigne el perfil de producto al grupo de usuarios](#assign-product-profile).

>[!ENDTABS]


## 5 - Asignar el perfil de producto al grupo de usuarios{#assign-product-profile}

Este paso sigue el flujo de trabajo estándar de Adobe Admin Console para asignar perfiles de producto a grupos de usuarios.

Artículo de referencia: [Administrar perfiles de producto para usuarios empresariales](https://helpx.adobe.com/es/enterprise/using/manage-product-profiles.html?lang=es)

1. Mientras sigue en el asistente de IA en el grupo de usuarios de AEM desde [4 - Agregar usuarios al grupo de usuarios](#add-users), haga clic en la ficha **Perfiles de producto asignados**.
1. Haga clic en **Asignar perfil**.

   ![Asistente de IA en la página del grupo de usuarios de AEM con la ficha Perfiles de producto asignados seleccionada](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. En la página **Asignar productos y perfiles**, en el cuadro de diálogo **Seleccionar perfiles de producto**, busque y seleccione su perfil de producto **Asistente de IA**.

   ![La página &quot;Asignar productos y perfiles&quot;, que muestra el cuadro de diálogo &quot;Seleccionar perfiles de producto&quot; y el perfil de producto &quot;Asistente de IA&quot; seleccionado](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Cerca de la esquina inferior derecha del cuadro de diálogo, haga clic en **Aplicar**.
1. Cerca de la esquina inferior derecha de la página **Asignar productos y perfiles**, haga clic en **Guardar**.

   ![Se muestra el perfil de producto del Asistente de IA asignado al Asistente de IA en el grupo de usuarios de AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Compruebe la configuración

* Compruebe que el perfil de producto muestra el número correcto de grupos de usuarios asignados.
* Compruebe que el grupo de usuarios muestra el número correcto de usuarios.
* Confirme que el permiso Conocimiento del producto del asistente de IA está habilitado y configurado correctamente.


## Prueba de la configuración

Haga que un usuario del grupo asignado haga lo siguiente:

1. Inicie sesión en AEM.
2. Compruebe que las funciones del Asistente de IA son accesibles.
3. Pruebe la funcionalidad del asistente de IA para garantizar una activación adecuada.

## Véase también

* [Asistente de IA en AEM](/help/ai-assistant-in-aem.md)
* [Control de acceso de Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
