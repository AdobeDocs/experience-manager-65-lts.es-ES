---
title: Administrar las categorías mostradas en Workspace
description: En Workspace, los procesos que puede iniciar un usuario se muestran en categorías en el panel de navegación izquierdo. Descubra cómo puede administrar estas categorías que se muestran en Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f9ffbe56-757b-4fd0-b33a-2522695aed35
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 2%

---

# Administrar las categorías mostradas en Workspace {#managing-the-categories-displayed-in-workspace}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

En Workspace, los procesos que puede iniciar un usuario se muestran en categorías en el panel de navegación izquierdo. Puede configurar las categorías en la consola de administración o los diseñadores de procesos pueden configurarlas en Workbench. Cuando los diseñadores de procesos crean procesos, los asignan a categorías.

Cuando especifique nombres de categorías, créelos de modo que aparezcan correctamente en el panel de navegación de Workspace. De forma predeterminada, el panel de navegación izquierdo tiene una anchura fija de 210 píxeles, que es de aproximadamente 24 caracteres. Si el nombre de categoría especificado es demasiado largo para ajustarse a la anchura fija del panel de navegación izquierdo, se trunca. El nombre completo sólo aparece cuando el puntero del mouse (ratón) se detiene sobre él. Intente evitar nombres de categoría que se trunquen. Los siguientes ejemplos ilustran los nombres de categoría que caben y los que se truncan:

**Nombre de categoría que cabe en:** Asistencia y licencia

**Nombre de categoría truncado:** Asistencia y permiso (Estados Unidos)

En Workspace, los procesos dentro de una categoría generalmente se muestran como tarjetas en la página Iniciar proceso. En general, se pueden mostrar seis tarjetas en la pantalla para una categoría antes de que el usuario tenga que desplazarse para ver las tarjetas restantes. Dado que el desplazamiento dificulta la búsqueda de un proceso, considere la posibilidad de limitar cada categoría a seis procesos o, según la resolución, limitar el número de procesos que se pueden mostrar en la pantalla sin necesidad de ningún desplazamiento.

Si utiliza MySQL como base de datos de formularios AEM Forms, la consola de administración no puede diferenciar entre dos nombres de categoría que solo difieren en el uso de caracteres extendidos. Por ejemplo, si crea una categoría denominada abcde y otra denominada âbcdè, se considerarán iguales.

## Agregar una categoría {#add-a-category}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de categorías.
1. Haga clic en Agregar. Si desea agregar una subcategoría, seleccione una y haga clic en Agregar.
1. En el cuadro Nombre, escriba un nombre para la categoría y, en el cuadro Descripción, escriba una descripción de la categoría.
1. Haga clic en Agregar. La categoría se muestra en la página Administración de categorías.

   ***nota **: solo puede agregar hasta cinco niveles de jerarquía al crear categorías.*

## Editar una categoría {#edit-a-category}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de categorías.
1. Seleccione la categoría que desee editar y haga clic en Editar. También puede hacer doble clic en una categoría para editarla.
1. Edite el nombre de la categoría en el cuadro Nombre.

## Eliminar una categoría {#remove-a-category}

Solo se pueden eliminar las categorías que no estén en uso.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de categorías.
1. En la página Administración de categorías, active la casilla de verificación de la categoría que desea quitar y haga clic en Quitar. La categoría ya no se muestra.
