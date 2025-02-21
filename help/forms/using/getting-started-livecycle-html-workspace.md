---
title: Introducción a AEM Forms Workspace
description: Introducción al uso de LiveCycle AEM Forms Workspace para administrar los procesos de automatización empresarial.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 95%

---

# Introducción a AEM Forms Workspace {#getting-started-with-aem-forms-workspace}

Puede utilizar AEM Forms Workspace para realizar las siguientes tareas:

* Iniciar un proceso empresarial
* Ver y actuar sobre las tareas asignadas a usted o a otras listas de tareas pendientes a las que tiene acceso
* Realizar un seguimiento de las tareas que forman parte de los procesos ha iniciado o en los que ha participado

## Navegar por AEM Forms Workspace {#navigating-html-workspace}

La interfaz de usuario de AEM Forms Workspace muestra distintos elementos según el proceso y la tarea en los que está trabajando. Puede que vea o no las pestañas Resumen, Formularios, Detalles, Historial, Archivos adjuntos o Notas, o todos los botones que se describen en esta Ayuda en todo momento.

Puede navegar por la interfaz de usuario principal de AEM Forms Workspace mediante cualquiera de los siguientes métodos:

* Haga clic en los elementos de la barra de navegación superior para acceder a las opciones Iniciar proceso, Lista de tareas pendientes, Preferencias, Seguimiento, Ayuda y Cerrar sesión.
* Haga clic en la pestaña Iniciar proceso, Tareas pendientes o Seguimiento para acceder a las tres áreas de trabajo principales.
* En las pestañas Iniciar proceso, Tareas pendientes y Seguimiento, haga clic en los elementos de la lista del panel izquierdo para acceder a los favoritos, las categorías de proceso, las plantillas de búsqueda, los borradores o las tareas asignadas. Utilice la barra de desplazamiento para ver los elementos adicionales de la lista.
* Todos los botones de acción (Aprobar, Rechazar, Reenviar, Consultar, Bloquear y Compartir) muestran el documento y la propiedad.
* Haga clic en el icono Todas las opciones de la barra de navegación, en la parte inferior de la página, para reenviar la tarea a otro usuario, compartirla o consultarla con él, o bloquear la tarea.
* En la pestaña Historial, seleccione una tarea para mostrar las pestañas Archivos adjuntos y Asignaciones de esa tarea.
* Utilice la tecla TAB, las teclas de dirección y la barra espaciadora para navegar por AEM Forms Workspace sin utilizar el ratón.

## Uso de AEM Forms Workspace con lectores de pantalla {#using-html-workspace-with-screen-readers}

AEM Forms Workspace es una aplicación HTML basada en web compatible con lectores de pantalla. Puede navegar por la interfaz de AEM Forms Workspace utilizando el teclado.

Para usar AEM Forms Workspace con un lector de pantalla, tenga en cuenta los siguientes puntos:

* AEM Forms Workspace es una aplicación HTML estándar que cumple los requisitos de cualquier herramienta de lector de pantalla estándar. No se necesita ningún script específico para ejecutar una herramienta de lector de pantalla.
* En AEM Forms Workspace, toda la navegación se realiza mediante etiquetas de anclaje, a las cuales se puede acceder fácilmente mediante pestañas.
* Forms puede tardar unos segundos en cargarse. El lector de pantalla no le informa de forma sonora de que el formulario se está cargando y que debe esperar.

## Navegar por AEM Forms Workspace utilizando un teclado {#navigating-html-workspace-using-a-keyboard}

Cuando navega por AEM Forms Workspace utilizando un teclado, la navegación se ajusta a las convenciones de accesibilidad de HTML. En algunas situaciones, el orden de tabulación no sigue el orden convencional tradicional. Las siguientes sugerencias le ayudarán a navegar por la interfaz:

* Si tiene problemas para desplazarse por las barras de herramientas en la parte superior del explorador, pulse Ctrl+Tab para acceder a la pestaña del contenido de la ventana del explorador.
* La Ayuda de AEM Forms Workspace se abre en una ventana independiente del explorador. Después de ver la Ayuda, el enfoque vuelve a la ventana del explorador que contiene AEM Forms Workspace. El menú Ayuda permanece enfocado cuando se vuelve a enfocar.
* Cuando se abre un formulario para iniciar un proceso o completar una tarea, el enfoque permanece en el elemento existente y no cambia al formulario. Utilice la pestaña para desplazar el enfoque al formulario y navegar por él. El orden de tabulación del formulario depende del tipo y el diseño del formulario.

  En el caso de los formularios PDF cuando se desplaza hasta el final del formulario o se envía el formulario, el enfoque del cursor salta a la barra de direcciones del explorador. Vuelva a desplazarse por los menús (pero no por todo el formulario) para ir a los botones de acción del formulario, como Guardar como borrador y Completar. Si el formulario sigue abierto, también puede desplazarse más allá de los botones y volver a él.

## Administración de preferencias {#managing-preferences}

Puede establecer las distintas preferencias de AEM Forms Workspace en las siguientes categorías:

**Fuera de la oficina:** establezca las preferencias para controlar cómo se asignarán las tareas a otras personas mientras esté fuera de la oficina. Consulte [Configuración de las preferencias de Fuera de la oficina](todo-lists.md#setting-out-of-office-preferences).

**Colas:** Establezca preferencias para compartir la lista de tareas pendientes con otros usuarios o para solicitar acceso a la lista de otro usuario. Consulte [Trabajo con tareas de grupos y colas compartidas](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Configuración de la interfaz de usuario:** establezca sus preferencias para interactuar con AEM Forms Workspace. Consulte [Establecer las preferencias de la interfaz de usuario](#set-user-interface-preferences).

### Establecer las preferencias de interfaz de usuario {#set-user-interface-preferences}

Establezca las preferencias de interfaz de usuario en la pestaña Preferencias > Configuración de la interfaz de usuario. Están disponibles las siguientes preferencias.

* **Ubicación inicial:** especifica la página que aparece al iniciar sesión en AEM Forms Workspace. Las cuatro opciones disponibles son Iniciar proceso, Tareas pendientes, Seguimiento y Favoritos.
* **Mensaje de cierre de sesión:** especifica si se le pedirá que confirme que desea cerrar la sesión después de hacer clic en Cerrar sesión.
* **Formato de fecha:** especifica el formato de visualización de fecha que se utiliza en AEM Forms Workspace.
* **Formato de hora**: especifica el formato de visualización de hora utilizado en AEM Forms Workspace.
* **Notificar eventos de tarea por correo electrónico:** especifica si recibirá notificaciones por correo electrónico de los eventos de tarea, incluidas las asignaciones de tareas, los recordatorios y las fechas límite de las tareas de la lista de tareas pendientes y de las listas de tareas pendientes de grupo a las que pertenece.
* **Adjuntar los formularios en el correo electrónico:** especifica si se adjunta una copia del formulario en los mensajes de las notificaciones por correo electrónico. Los archivos adjuntos solo son compatibles con los formularios PDF y XDP.
* **Guardar borrador periódicamente:** especifica si los borradores de formulario se guardan automáticamente de forma periódica o no. Para guardar los borradores periódicamente, habilite esta opción y establezca una duración de guardado automático de entre 1 y 30 minutos. Cuando el guardado automático está habilitado y un usuario está trabajando en un borrador, el borrador se guarda periódicamente una vez transcurrido el número especificado de minutos. El borrador solo se guarda automáticamente si se ha modificado desde la última vez que se guardó o desde el último guardado automático. Cuando se guarda el borrador, aparece un mensaje de alerta en la pantalla.
