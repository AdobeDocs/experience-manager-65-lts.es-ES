---
title: Administración de proyectos
description: Proyectos permite organizar el proyecto agrupando recursos en una entidad a la que se puede acceder y administrar en la consola Proyectos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 18%

---


# Administración de proyectos {#managing-projects}

En la consola **Proyectos**, tiene acceso a sus proyectos y los administra.

![La consola Proyectos](assets/projects-console.png)

Con la consola, puede crear un proyecto, asociar recursos al proyecto y también eliminar un proyecto o vínculos a recursos.

## Requisitos de acceso {#access-requirements}

Los proyectos son una función estándar de AEM y no requieren ninguna configuración adicional.

Sin embargo, para que los usuarios de los proyectos puedan ver a otros usuarios o grupos mientras utilizan Proyectos como, por ejemplo, al crear proyectos, crear tareas/flujos de trabajo o ver y administrar el equipo, dichos usuarios necesitan tener acceso de lectura en `/home/users` y `/home/groups`.

La forma más sencilla de hacerlo es conceder acceso de lectura al grupo **projects-users** a `/home/users` y `/home/groups`.

## Creación de un proyecto {#creating-a-project}

Siga estos pasos para crear un proyecto.

1. En la consola **Proyectos**, haga clic en **Crear** para abrir el asistente **Crear proyecto**.
1. Seleccione una plantilla y haga clic en **Siguiente**. Puede obtener más información acerca de las plantillas de proyecto estándar [aquí.](/help/sites-authoring/projects.md#project-templates)

   ![Asistente para crear proyectos](assets/create-project-wizard.png)

1. Defina **Title** y **Description** y agregue una imagen de **miniatura** si es necesario. También puede agregar o eliminar usuarios y a qué grupo pertenecen.

   ![Paso Propiedades del asistente](assets/create-project-wizard-properties.png)

1. Haga clic en **Crear**. La confirmación le solicitará si desea abrir el nuevo proyecto o volver a la consola.

El procedimiento para crear un proyecto es el mismo para todas las plantillas de proyecto. La diferencia entre los tipos de proyectos está relacionada con los [roles de usuario](/help/sites-authoring/projects.md) y [flujos de trabajo disponibles.](/help/sites-authoring/projects-with-workflows.md)

### Asociación de recursos al proyecto {#associating-resources-with-your-project}

Los proyectos permiten agrupar recursos en una entidad para administrarlos en su conjunto. Por lo tanto, debe asociar recursos al proyecto. Estos recursos se agrupan dentro del proyecto como **Mosaicos**. Los tipos de recursos que puede añadir se describen en [Mosaicos del proyecto](/help/sites-authoring/projects.md#project-tiles).

Para asociar recursos al proyecto, haga lo siguiente:

1. Abra el proyecto desde la consola **Proyectos**.
1. Haga clic en **Agregar mosaico** y seleccione el mosaico que desee vincular a su proyecto. Puede seleccionar varios tipos de mosaicos.

   ![Agregar mosaico](assets/project-add-tile.png)

1. Haga clic en **Crear**. El recurso está vinculado al proyecto y, a partir de ahora, podrá acceder a él desde el proyecto.

### Adición de elementos a un mosaico {#adding-items-to-a-tile}

En algunos mosaicos, puede que desee añadir más de un elemento. Por ejemplo, puede tener más de un flujo de trabajo que se ejecuta al mismo tiempo o más de una experiencia.

Para agregar elementos a un mosaico:

1. En **Proyectos**, navegue hasta el proyecto y haga clic en el icono de cheurón descendente en la parte superior derecha del mosaico al que desee agregar un elemento y seleccione la opción adecuada.

   * La opción depende del tipo de mosaico. Por ejemplo, puede ser **Crear tarea** para el mosaico **Tareas** o **Iniciar flujo de trabajo** para el mosaico **Flujos de trabajo**.

   ![Sujeción de mosaico](assets/project-tile-create-task.png)

1. Agregue el elemento al mosaico como lo haría al crear un mosaico. Los mosaicos del proyecto se describen [aquí.](/help/sites-authoring/projects.md#project-tiles)

## Visualización de información del proyecto {#viewing-project-info}

El propósito principal de los proyectos es agrupar la información asociada en un solo lugar para que sea más accesible y procesable. Existen varias formas de acceder a esta información.

### Apertura de un mosaico {#opening-a-tile}

Es posible que desee ver qué elementos se incluyen en un mosaico actual o modificar o eliminar elementos en el mosaico.

Para abrir un mosaico para poder ver o modificar elementos, haga lo siguiente:

1. Haga clic en el icono de elipses en la parte inferior derecha del mosaico.

   ![Mosaico de tareas](assets/project-tile-tasks.png)

1. AEM abre la consola para los tipos de elementos asociados con el mosaico y filtra en función del proyecto seleccionado.

   ![Tareas de proyecto](assets/project-tasks.png)

### Visualización de la cronología de un proyecto {#viewing-a-project-timeline}

La cronología del proyecto proporciona información sobre la última vez que se utilizaron los recursos del proyecto. Para ver la cronología del proyecto, siga estos pasos.

1. En la consola **Proyectos**, haga clic en **Cronología** en el selector de carril en la parte superior izquierda de la consola.
   ![Seleccionando modo de escala de tiempo](assets/projects-timeline-rail.png)
2. En la consola, seleccione el proyecto cuya cronología desee ver.
   ![Vista de escala de tiempo del proyecto](assets/project-timeline-view.png)

Los Assets se muestran en el carril. Utilice el selector de raíl para volver a la vista normal cuando haya terminado.

### Visualización de proyectos inactivos {#viewing-active-inactive-projects}

Para alternar entre sus proyectos activos e [inactivos,](#making-projects-inactive-or-active) en la consola **Proyectos**, haga clic en el icono **Alternar proyectos activos** de la barra de herramientas.

![Icono de alternar proyectos activos](assets/projects-toggle-active.png)

De forma predeterminada, la consola muestra los proyectos activos. Haga clic en el icono **Alternar proyectos activos** una vez para cambiar a la visualización de proyectos inactivos. Vuelva a hacer clic para volver a los proyectos activos.

## Organización de proyectos {#organizing-projects}

Hay varias opciones disponibles para organizar sus proyectos de modo que la consola **Proyectos** se pueda administrar.

### Carpetas de proyecto {#project-folders}

Puede crear carpetas en la consola **Proyectos** para agrupar y organizar proyectos similares.

1. En la consola **Proyectos**, haga clic en **Crear** y luego en **Crear carpeta**.

   ![Crear carpeta](assets/project-create-folder.png)

1. Asigne un título a la carpeta y haga clic en **Crear**.

1. La carpeta se agregará a la consola.

Ahora puede crear proyectos dentro de la carpeta. Puede crear varias carpetas y también anidar carpetas.

### Inactivando proyectos {#making-projects-inactive-or-active}

Es posible que desee marcar un proyecto como inactivo si se completa, pero aun así desea mantener la información sobre el proyecto. [Los proyectos inactivos ahora muestran](#viewing-active-inactive-projects) de forma predeterminada en la consola **Proyectos**.

Para que un proyecto quede inactivo, siga estos pasos.

1. Abra la ventana **Propiedades del proyecto**.
   * Puede hacerlo desde la consola seleccionando el proyecto o desde el proyecto a través del mosaico **Información del proyecto**.
1. En la ventana **Propiedades del proyecto**, cambie el regulador **Estado del proyecto** de **Activo** a **Inactivo**.

   ![Selector de estado del proyecto en la ventana de propiedades](assets/project-status.png)

1. Haga clic en **Guardar y cerrar** para guardar los cambios.

### Eliminación de proyectos {#deleting-a-project}

Siga estos pasos para eliminar un proyecto.

1. Vaya al nivel superior de la consola **Proyectos**.
1. Selección del proyecto en la consola.
1. Haga clic en **Eliminar** en la barra de herramientas.
1. AEM puede eliminar o modificar los datos de proyecto asociados al eliminar el proyecto. Seleccione las opciones que necesite en el cuadro de diálogo **Eliminar proyecto**.
   * Eliminar los grupos y las funciones de proyecto
   * Eliminar carpeta Assets del proyecto
   * Completar los flujos de trabajo del proyecto

   ![Opciones de eliminación de proyecto](assets/project-delete-options.png)
1. Haga clic en **Eliminar** para eliminar el proyecto con las opciones seleccionadas.

Para obtener más información sobre los grupos creados automáticamente por los proyectos, consulte [Creación automática de grupos](/help/sites-authoring/projects.md#auto-group-creation) para obtener más información.
