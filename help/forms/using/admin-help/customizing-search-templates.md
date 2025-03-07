---
title: Personalizar plantillas de búsqueda
description: Puede crear plantillas de búsqueda para utilizarlas en Workspace y buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar plantillas de búsqueda existentes.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 7e6346ec-3cab-4f88-91b3-b111bd19983e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Personalizar plantillas de búsqueda {#customizing-search-templates}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede crear plantillas de búsqueda para utilizarlas en Workspace y buscar instancias de procesos en las páginas Tareas pendientes y Seguimiento. También puede editar o eliminar plantillas de búsqueda existentes.

Al crear o editar una plantilla de búsqueda, puede especificar el diseño y el orden de los resultados de búsqueda. Sin embargo, los usuarios pueden modificar esta configuración en Workspace después de que aparezcan los resultados de búsqueda.

Puede crear tantas plantillas de búsqueda como sea necesario.

>[!NOTE]
>
>Al guardar una plantilla de búsqueda, debe asignarle un nombre único. De lo contrario, se puede sobrescribir una plantilla existente sin un mensaje de advertencia.

## Crear una plantilla de búsqueda simple {#create-a-simple-search-template}

1. En la consola de administración, haga clic en Servicios > Workspace > Buscar plantillas.
1. En la ficha Identificación, en el cuadro Descripción de la plantilla de búsqueda, indique el propósito de la plantilla.
1. (Opcional) Haga clic en la pestaña Criterios y especifique los criterios de búsqueda para la plantilla.
1. Haga clic en la ficha Guardar, escriba un nombre exclusivo para la plantilla y, a continuación, haga clic en Guardar.

## Creación o edición de una plantilla de búsqueda {#create-or-edit-a-search-template}

1. En la consola de administración, haga clic en Servicios > Workspace > Buscar plantillas.
1. (Opcional) Si está editando una plantilla existente o está utilizando una plantilla existente como base para una nueva plantilla, seleccione la plantilla en la lista Buscar nombre de plantilla.
1. En el cuadro Buscar descripción de plantilla, indique el propósito de la plantilla.
1. (Opcional) En el cuadro Instrucciones para el usuario, proporcione las instrucciones que puedan ayudarle a utilizar la plantilla. Estas instrucciones se muestran en Workspace cuando un usuario selecciona la plantilla de búsqueda.
1. Haga clic en la pestaña Criterios. Aquí es donde se definen uno o más criterios de búsqueda. Para agregar un criterio de búsqueda:

   * En la parte superior de la pestaña Criterios, seleccione un elemento de proceso o un elemento de tarea.

     **Sugerencia**: *Si seleccionó previamente el elemento Nombre del proceso y especificó un proceso, también se podrá seleccionar cualquier variable de proceso definida en ese proceso.*

     **Sugerencia**: *Si selecciona el elemento Task Visible, los usuarios podrán quitar las tareas completadas de los resultados de búsqueda.*

     Los campos de criterios de búsqueda para el elemento seleccionado aparecen en la parte inferior de la pestaña Criterios.

   * Para cada elemento de proceso, elemento de tarea y variable de proceso que seleccione, rellene los campos de búsqueda correspondientes en la parte inferior de la pestaña Criterios:

      * Seleccione un operador relacional (como &quot;ser igual a&quot;) de la lista proporcionada y especifique el valor del operando en el cuadro que aparece junto a él.
      * (Opcional) Para permitir que los usuarios cambien el valor del operando en Workspace, seleccione Permitir al usuario cambiar el operando.
      * (Opcional) Para permitir que los usuarios cambien el operador relacional, seleccione Permitir al usuario seleccionar otro operador relacional. En la lista que aparece, seleccione los operadores que deben estar disponibles para el usuario.

     **Sugerencia**: *Si seleccionó Nombre del proceso como elemento, puede hacer clic en el icono situado junto al campo de operando para mostrar una lista donde puede seleccionar un proceso que se esté ejecutando en el servidor de Forms. Después de seleccionar un proceso, todas las variables de proceso definidas en ese proceso están disponibles para su selección en Variables de proceso en la sección superior de la ficha Criterios.*

     **Sugerencia**: *Puede eliminar un elemento de la plantilla de búsqueda haciendo clic en el icono Eliminar situado junto a los criterios de búsqueda del elemento.*

1. (Opcional) Para que el encabezado de cada columna se muestre en los resultados de búsqueda, haga clic en la pestaña Diseño y realice los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Columnas de Informe.
   * En la lista Columnas para el informe, seleccione el proceso o elemento de tarea y haga clic en la flecha arriba o en la flecha abajo para moverlo a su lugar en el orden de columna. Los encabezados de columna de los resultados de búsqueda aparecerán en el orden en que se enumeran aquí.
   * (Opcional) Para cambiar el nombre del elemento para el encabezado de la columna, seleccione el elemento de la lista Columnas para el informe y proporcione el nuevo nombre.

   >[!NOTE]
   >
   >El diseño especificado en la plantilla de búsqueda anula las preferencias del usuario especificadas para los encabezados de columna en Workspace.

1. (Opcional) Para que cada columna se ordene en los resultados de búsqueda, haga clic en la pestaña Ordenar y realice los siguientes pasos:

   * Seleccione un elemento de proceso o tarea y haga clic en la flecha derecha para moverlo a la lista Orden de clasificación.
   * En la lista Orden de clasificación, seleccione el proceso o elemento de tarea y haga clic en las flechas arriba o abajo para moverlo a su lugar en el orden de clasificación. Las columnas de los resultados de búsqueda se ordenarán según el orden en que aparezcan aquí.
   * (Opcional) Para ordenar una columna en orden descendente, active la casilla de verificación situada junto al nombre del elemento. Si la casilla de verificación no está seleccionada, la columna se ordena en orden ascendente.

1. Haga clic en la pestaña Save.
1. (Opcional) Si crea una plantilla de búsqueda, asígnele un nombre único. Si no especifica un nombre único, puede sobrescribir una plantilla existente.
1. Haga clic en el botón Save.

## Eliminación de una plantilla de búsqueda {#delete-a-search-template}

1. En la ficha Identificación, seleccione un nombre de la lista Buscar nombre de plantilla.
1. Haga clic en Eliminar esta plantilla y luego en Aceptar.
