---
title: Administración del acceso a los flujos de trabajo
description: Obtenga información sobre cómo configurar Listas de control de acceso según las cuentas de usuario para permitir (o deshabilitar) el inicio y la participación en flujos de trabajo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# Administración del acceso a los flujos de trabajo{#managing-access-to-workflows}

Configure ACL según las cuentas de usuario para permitir (o deshabilitar) el inicio y la participación en flujos de trabajo.

## Permisos de usuario requeridos para flujos de trabajo {#required-user-permissions-for-workflows}

Se pueden llevar a cabo acciones sobre flujos de trabajo si:

* está trabajando con la cuenta `admin`
* la cuenta se ha asignado al grupo predeterminado `workflow-users`:

   * este grupo posee todos los privilegios necesarios para que los usuarios realicen acciones de flujo de trabajo.
   * cuando la cuenta está en este grupo, solo tiene acceso a los flujos de trabajo que ha iniciado.

* la cuenta se ha asignado al grupo predeterminado `workflow-administrators`:

   * este grupo posee todos los privilegios necesarios para que sus usuarios privilegiados monitoricen y administren flujos de trabajo.
   * cuando la cuenta está en este grupo, tiene acceso a todos los flujos de trabajo.

>[!NOTE]
>
>Estos son los requisitos mínimos. Su cuenta también debe ser el participante asignado o un miembro del grupo asignado para realizar pasos específicos.

## Configuración del acceso a los flujos de trabajo {#configuring-access-to-workflows}

Los modelos de flujo de trabajo heredan una lista de control de acceso (ACL) predeterminada para controlar cómo los usuarios pueden interactuar con los flujos de trabajo. Para personalizar el acceso de los usuarios a un flujo de trabajo, modifique la Lista de control de acceso (ACL) en el repositorio para la carpeta que contiene el nodo del modelo de flujo de trabajo:

* [Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Cree una subcarpeta en /var/workflow/models y aplique la ACL a ella](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obtener información sobre cómo usar CRXDE Lite para configurar ACL, consulte [Administración de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Si el modelo de flujo de trabajo está almacenado en `/var/workflow/models`, puede asignar una ACL específica, relevante solo para ese flujo de trabajo, en la carpeta:

1. Abra CRXDE Lite en el explorador web (por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. En el árbol de nodos, seleccione el nodo de la carpeta de modelos de flujo de trabajo:

   `/var/workflow/models`

1. Haga clic en la ficha **Control de acceso**.
1. En la tabla **Directivas de control de acceso local** (**Lista de control de acceso**), haga clic en el icono de signo más para **Agregar entrada**.
1. En el cuadro de diálogo **Agregar nueva entrada**, agregue una ACE con las siguientes propiedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegios**: `jcr:read`
   * **rep:glob**: referencia al flujo de trabajo específico

   ![wf-108](assets/wf-108.png)

   La tabla **Lista de control de acceso** incluye ahora la restricción para `content-authors` en el modelo de flujo de trabajo `prototype-wfm-01`.

   ![wf-109](assets/wf-109.png)

1. Haga clic en **Guardar todo**.

   El flujo de trabajo `prototype-wfm-01` ya no está disponible para los miembros del grupo `content-authors`.

### Cree una subcarpeta en /var/workflow/models y aplique la ACL a ella {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Su [equipo de desarrollo puede crear los flujos de trabajo en una subcarpeta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparable con los flujos de trabajo de DAM almacenados en

`/var/workflow/models/dam/`

A continuación, puede agregar una ACL a la propia carpeta.

1. Abra CRXDE Lite en el explorador web (por ejemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. En el árbol de nodos, seleccione el nodo para la carpeta individual en la carpeta de modelos de flujo de trabajo; por ejemplo:

   `/var/workflow/models/prototypes`

1. Haga clic en la ficha **Control de acceso**.
1. En la tabla **Directiva de control de acceso aplicable**, haga clic en el icono de signo más para **Agregar** una entrada.
1. En la tabla **Directivas de control de acceso local** (**Lista de control de acceso**), haga clic en el icono de signo más para **Agregar entrada**.
1. En el cuadro de diálogo **Agregar nueva entrada**, agregue una ACE con las siguientes propiedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegios**: `jcr:read`

   >[!NOTE]
   >
   >Al igual que con [Aplicar una ACL para el modelo de flujo de trabajo específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models), puede incluir una rep:glob para limitar el acceso a un flujo de trabajo específico.

   ![wf-110](assets/wf-110.png)

   La tabla **Lista de control de acceso** incluye ahora la restricción para `content-authors` en la carpeta `prototypes`.

   ![wf-111](assets/wf-111.png)

1. Haga clic en **Guardar todo**.

   Los modelos de la carpeta `prototypes` ya no están disponibles para los miembros del grupo `content-authors`.
