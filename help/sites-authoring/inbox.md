---
title: Bandeja de entrada para administrar tareas
description: Administrar las tareas con la bandeja de entrada en Adobe Experience Manager 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 077407ef-1d7f-47ad-b924-0afa19f21119
source-git-commit: 524f1bcea6761e299141bc1d1496e32c498ffd14
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 39%

---

# Su bandeja de entrada{#your-inbox}

Puede recibir notificaciones de varias áreas de AEM, incluidos flujos de trabajo y proyectos; por ejemplo, acerca de:

* Tareas:

   * estas también se pueden crear en distintos puntos de la interfaz de usuario de AEM, por ejemplo, en **Proyectos**,
   * pueden ser el producto del paso **Crear tarea** o **Crear tarea de proyecto** de un flujo de trabajo.

* Flujos de trabajo:

   * elementos de trabajo que representan acciones que debe realizar en el contenido de la página;

      * estos son el producto de los pasos del flujo de trabajo **Participante**

   * elementos de error, para permitir que los administradores reintenten el paso con errores.

Estas notificaciones las recibe en su propia bandeja de entrada, donde puede verlas y realizar acciones.

>[!NOTE]
>
>AEM viene precargado con tareas administrativas asignadas al grupo de usuarios administradores. Consulte [Tareas administrativas listas para usar](#out-of-the-box-administrative-tasks) para obtener más información.

>[!NOTE]
>
>Para obtener más información sobre los tipos de elementos, consulte también:
>
>* [Proyectos](/help/sites-authoring/touch-ui-managing-projects.md)
>* [Proyectos: trabajo con tareas](/help/sites-authoring/task-content.md)
>* [Flujos de trabajo](/help/sites-authoring/workflows.md)
>* [Formularios](/help/forms/using/introduction-aem-forms.md)
>

## Bandeja de entrada en el encabezado {#inbox-in-the-header}

Desde cualquiera de las consolas, en el encabezado se muestra el número actual de elementos de la bandeja de entrada. El indicador también se puede abrir para proporcionar acceso rápido a las páginas que requieren acciones o acceso a la bandeja de entrada:

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>Algunas acciones también se mostrarán en la [vista de tarjeta del recurso adecuado](/help/sites-authoring/basic-handling.md#card-view).

## Tareas administrativas listas para usar  {#out-of-the-box-administrative-tasks}

AEM viene precargado con cuatro tareas asignadas al grupo de usuarios &quot;administrator&quot;.

* [Configurar Analytics y Targeting](/help/sites-administering/opt-in.md)
* [Aplicar la lista comprobación de seguridad de AEM](/help/sites-administering/security-checklist.md)
* Habilitar recopilación de estadísticas de uso agregadas
* [Configurar HTTPS](/help/sites-administering/ssl-by-default.md)

## Apertura de la bandeja de entrada    {#opening-the-inbox}

Para abrir la bandeja de entrada de notificaciones AEM:

1. Haga clic en el indicador de la barra de herramientas.

1. Seleccione **Ver todo**. Se abre la **Bandeja de entrada de AEM**. La bandeja de entrada muestra elementos de flujos de trabajo, proyectos y tareas.
1. La vista predeterminada es [Vista de lista](#inbox-list-view), pero también puede cambiar a [Vista de calendario](#inbox-calendar-view). Esto se realiza con el selector de vistas (barra de herramientas, arriba a la derecha).

   Para ambas vistas también puede definir [Configuración de vista](#inbox-view-settings); las opciones disponibles dependen de la vista actual.

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>La bandeja de entrada actúa como una consola, por lo que se aconseja utilizar [Navegación global](/help/sites-authoring/basic-handling.md#global-navigation) o [Buscar](/help/sites-authoring/search.md) para desplazarse a otra ubicación cuando haya terminado.

### Bandeja de entrada: vista de lista {#inbox-list-view}

Esta vista enumera todos los elementos, junto con información clave relevante:

![wf-82](assets/wf-82.png)

### Bandeja de entrada: vista de calendario {#inbox-calendar-view}

Esta vista presenta los elementos según su posición en el calendario y la vista exacta que haya seleccionado:

![wf-93](assets/wf-93.png)

Puede hacer lo siguiente:

* seleccionar una vista específica; **Cronología**, **Columna**, **Lista**

* especifique las tareas que se mostrarán según **Programa**; **Todos**, **Planificados**, **En curso**, **Vence pronto**, **Vencidos**

* explorar en profundidad un elemento para obtener información más detallada
* seleccione un intervalo de fechas en el que centrar la vista:

![wf-91](assets/wf-91.png)

### Bandeja de entrada - Configuración {#inbox-view-settings}

Para ambas vistas (Lista y Calendario) puede definir la siguiente configuración:

* **Vista de calendario**

  Para **Vista de calendario** puede configurar lo siguiente:

   * **Agrupar por**
   * **Programa** o **Ninguno**
   * **Tamaño de la tarjeta**

  ![wf-92](assets/wf-92.png)

* **Vista de lista**

  Para **Vista de lista** puede configurar el mecanismo de ordenación:

   * **Campo de ordenación**
   * **Orden de clasificación**

  ![wf-83](assets/inbox-settings.png)

### Bandeja de entrada - Control de administración {#inbox-admin-control}

La opción Admin Control permite a los administradores lo siguiente:

* Personalizar las columnas de la bandeja de entrada AEM

* Personalizar el texto y el logotipo del encabezado

* Controlar la visualización de los vínculos de navegación disponibles en el encabezado

La opción Control de administración solo está visible para los miembros del grupo `administrators` o `workflow-administrators`.

* **Personalización de columnas**: personalice una Bandeja de entrada AEM para cambiar el título predeterminado de una columna, reordenar la posición de una columna y mostrar columnas adicionales basadas en los datos de un flujo de trabajo.
   * **Agregar columna**: Seleccione una columna para agregarla a la Bandeja de entrada AEM.
   * **Editar columna**: Pase el ratón sobre el título de la columna y seleccione el icono ![editar](assets/edit.svg) para introducir un nombre para mostrar en la columna.
   * **Eliminar columna**: Seleccione el icono ![eliminar](assets/delete_updated.svg) para eliminar la columna de la bandeja de entrada AEM.
   * **Mover columna**: arrastre el icono ![mover](assets/move_updated.svg) para mover una columna a una nueva posición en la Bandeja de entrada de AEM.

  ![admin-control](assets/admin-control-column-customize.png)

* **Personalización de marca**

   * **Personalizar texto de encabezado:** Especifique el texto que se mostrará en el encabezado para reemplazar el texto predeterminado de **Adobe Experience Manager**.

   * **Personalizar logotipo:** Especifique la imagen que se mostrará en el encabezado como logotipo. Cargue una imagen en Digital Asset Management (DAM) y consulte esa imagen en el campo.

* **Navegación de usuario**
   * **Ocultar opciones de navegación:** Seleccione esta opción para ocultar las opciones de navegación disponibles en el encabezado. Las opciones de navegación incluyen vínculos a otras soluciones de, vínculos de ayuda y las opciones de creación disponibles al pulsar el logotipo o el texto de Adobe Experience Manager.
* **Guardar:** Haga clic en esta opción para guardar la configuración.

## Acción en un elemento {#taking-action-on-an-item}

>[!NOTE]
>
>Aunque es posible seleccionar más de un elemento, las acciones solo se pueden realizar en un elemento a la vez.


1. Para realizar una acción sobre un elemento, seleccione la miniatura correspondiente al elemento en cuestión. Los iconos de las acciones aplicables a ese elemento se muestran en la barra de herramientas:

   ![wf-84](assets/wf-84.png)

   Las acciones son apropiadas para el elemento y entre ellas se incluyen:

   * **Completar** acción; por ejemplo, una tarea o un elemento de flujo de trabajo.
   * **Volver a asignar**/**Delegar** un elemento.
   * **Abrir** un elemento; en función del tipo de elemento, esta acción puede:

      * mostrar las propiedades del elemento
      * abra un tablero o un asistente apropiado para realizar más acciones
      * abrir documentación relacionada

   * **Retroceder** a un paso anterior.
   * Consultar la carga útil de un flujo de trabajo.
   * Cree un proyecto a partir del elemento.

   >[!NOTE]
   >
   >Para obtener más información, consulte lo siguiente:
   >
   >* Elementos de flujo de trabajo: [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md)

1. En función del elemento seleccionado, se inicia una acción; por ejemplo:

   * se abrirá un cuadro de diálogo apropiado para la acción.
   * se iniciará un asistente de acciones.
   * se abrirá una página de documentación.

   Por ejemplo, **Reasignar** abre un cuadro de diálogo:

   ![wf-85](assets/wf-85.png)

   En función de si ha abierto un cuadro de diálogo, un asistente o una página de documentación, puede:

   * Confirme la acción adecuada; por ejemplo, Reasignar.
   * Cancele la acción.
   * Flecha hacia atrás; por ejemplo, si se ha abierto un asistente de acciones o una página de documentación, puede volver a la Bandeja de entrada.

## Creación de una tarea {#creating-a-task}

Desde la bandeja de entrada puede crear las siguientes tareas:

1. Seleccione **Crear** y a continuación, **Tarea**.
1. Complete los campos necesarios en las pestañas **Básico** y **Avanzado**; solo el **Título** es obligatorio, el resto son opcionales:

   * **Básico**:

      * **Título**
      * **Proyecto**
      * **Usuario asignado**
      * **Contenido**; similar a Carga útil, es una referencia de la tarea a una ubicación del repositorio
      * **Descripción**
      * **Prioridad de tareas**
      * **Fecha de inicio**
      * **Fecha de vencimiento**

   ![wf-86](assets/wf-86.png)

   * **Avanzado**

      * **Nombre**: se usa para formar la dirección URL; si está en blanco, se basará en el **Título**.

   ![wf-87](assets/wf-87.png)

1. Seleccione **Enviar**.

## Creación de un proyecto    {#creating-a-project}

Para determinadas tareas, puede crear un [Proyecto](/help/sites-authoring/projects.md) basado en esa tarea:

1. Seleccione la tarea adecuada pulsando o haciendo clic en la miniatura.

   >[!NOTE]
   >
   >Para crear un proyecto, solo se pueden utilizar las tareas que se crearon con la opción **Crear** de la **bandeja de entrada**.
   >
   >Los elementos de trabajo (de un flujo de trabajo) no se pueden utilizar para crear un proyecto.

1. Seleccione **Crear proyecto** en la barra de herramientas para abrir el asistente.
1. Seleccione la plantilla apropiada y, a continuación, **Siguiente**.
1. Especifique las propiedades necesarias:

   * **Básico**

      * **Título**
      * **Descripción**
      * **Fecha de inicio**
      * **Fecha de vencimiento**
      * **Usuario** y función

   * **Avanzado**

      * **Nombre**

   >[!NOTE]
   >
   >Consulte [Creación de un proyecto](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) para obtener información completa.

1. Seleccione **Crear** para confirmar la acción.

## Filtrado de elementos en la bandeja de entrada AEM    {#filtering-items-in-the-aem-inbox}

Puede filtrar los elementos enumerados:

1. Abra la **Bandeja de entrada AEM**.

1. Abra el selector de filtros:

   ![wf-88](assets/wf-88.png)

1. Puede filtrar los elementos enumerados según un rango de criterios, muchos de los cuales se pueden refinar; por ejemplo:

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >Con [Configuración de vista](#inbox-view-settings) también puede configurar el orden cuando se utiliza la [Vista de lista](#inbox-list-view).
