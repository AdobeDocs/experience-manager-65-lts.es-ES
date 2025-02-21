---
title: Configurar Fuera de la oficina
description: La función Fuera de la oficina permite especificar cuándo un usuario estará fuera de la oficina y no podrá completar las tareas asignadas por los formularios de AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# Configurar Fuera de la oficina {#configuring-out-of-office-settings}

La función Fuera de la oficina permite a los usuarios o administradores especificar cuándo estará fuera de la oficina y no podrá completar las tareas asignadas por los formularios de AEM. Mientras un usuario está configurado en Fuera de la oficina, sus tareas se asignan a uno o más usuarios designados. Los usuarios pueden cambiar su configuración de Fuera de la oficina en Workspace o los administradores pueden cambiar la configuración en nombre de un usuario en el flujo de trabajo de formularios.

Al crear un proceso, el usuario de Workbench puede especificar si una tarea se puede redirigir debido a la configuración de Fuera de la oficina.

## Ver la información de Fuera de la oficina de un usuario {#view-a-user-s-out-of-office-information}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Fuera de la oficina.
1. En el cuadro situado cerca de la parte superior de la página Fuera de la oficina, puede realizar una de las siguientes acciones:

   **Buscar por nombre**

   Seleccione la opción Buscar por nombre. Escriba todo o parte del nombre de usuario y haga clic en Buscar. Si deja el campo en blanco, el flujo de trabajo de Forms devuelve una lista de todos los usuarios.

   **Buscar por intervalo de fecha**

   Seleccione la opción Buscar por intervalo de fechas. Especifique las fechas inicial y final junto con las marcas de tiempo deseadas para reducir el resultado de búsqueda. Haga clic en Buscar.

1. Haga clic en un nombre de usuario para mostrar la información de Fuera de la oficina del usuario debajo de la lista de usuarios.

## Cambiar el estado de Fuera de la oficina de un usuario {#change-a-user-s-out-of-office-status}

1. Busque el usuario, tal como se describe en [Ver la información de Fuera de la oficina de un usuario](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Haga clic en el nombre del usuario que desea cambiar.
1. En la lista *Nombre de usuario* actualmente, seleccione En la oficina o Fuera de la oficina.
1. Haga clic en Guardar.

## Agregar un intervalo de fechas de Fuera de la oficina para un usuario {#add-an-out-of-office-date-range-for-a-user}

1. Busque el usuario, tal como se describe en [Ver la información de Fuera de la oficina de un usuario](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Haga clic en el nombre del usuario que desea cambiar.
1. Haga clic en Agregar intervalo de fecha.
1. Introduzca una hora de inicio y una hora de finalización. Puede hacer clic en el icono del calendario para seleccionar una fecha. Si no especifica una hora de finalización, el usuario se establecerá como fuera de la oficina indefinidamente.
1. Haga clic en Guardar.

## Asignar un usuario para tareas fuera de la oficina {#assign-a-user-for-out-of-office-tasks}

Mientras un usuario está fuera de la oficina, puede asignar uno o más usuarios para que realicen cualquier tarea nueva para el usuario. Puede configurar las siguientes configuraciones:

* Asigne todas las tareas nuevas a un usuario predeterminado designado.
* No reasigne ninguna tarea. Las nuevas tareas permanecen asignadas al usuario que está fuera de la oficina.
* Asigne un usuario predeterminado que recibirá la mayoría de las tareas del usuario, pero especifique que las tareas de ciertos procesos se reasignen a otros usuarios o permanezcan asignadas al usuario que esté fuera de la oficina.
* No asigne un usuario predeterminado, sino que asigne determinadas tareas de determinados procesos a usuarios específicos.

   1. Busque el usuario, tal como se describe en [Ver la información de Fuera de la oficina de un usuario](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Haga clic en el nombre del usuario que desea cambiar.
   1. En la lista Usuario predeterminado para tareas fuera de la oficina, seleccione un usuario de la lista. Si no desea designar un usuario predeterminado para recibir los elementos reasignados, seleccione No asignar.

      Si el nombre de usuario apropiado no aparece en la lista, haga clic en Buscar usuario y utilice el cuadro de diálogo Buscar usuario para buscar el usuario. Seleccione el usuario adecuado de la lista y haga clic en Seleccionar usuario. También puede hacer clic en Ver programación del usuario en el cuadro de diálogo Buscar usuario para ver la programación de Fuera de la oficina del usuario seleccionado.

   1. Si hay algún proceso que no se debe enviar al usuario predeterminado, haga clic en Añadir una excepción, seleccione el proceso y seleccione otro usuario en la lista. También puede seleccionar No asignar para que la tarea permanezca asignada al usuario que está fuera de la oficina.
   1. Haga clic en Guardar.
