---
title: Usar un formulario adaptable en el espacio de trabajo HTML
description: Aprenda a utilizar un formulario adaptable en HTML Workspace que permita a los trabajadores acceder al formulario en sus dispositivos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 78%

---

# Usar un formulario adaptable en el espacio de trabajo HTML {#using-an-adaptive-form-in-html-workspace}

AEM Forms en JEE permite utilizar un formulario adaptable en HTML Workspace.

Como se puede seleccionar un XDP durante el diseño del proceso, se ha agregado la capacidad de examinar desde un formulario adaptable de repositorio de AEM existente. La capacidad permite a Process Designer configurar un formulario adaptable en el punto de inicio y en la tarea.

## Experiencia en diseño de procesos {#process-design-experience}

Realice las siguientes acciones para permitir que los formularios adaptables se utilicen en el diseño de procesos:

* En Asignar tarea y Punto de inicio, puede examinar un recurso de formulario adaptable en el repositorio CRX al asignar un recurso de formulario a una tarea.
* En la hoja de propiedades de Workbench Asignar tarea/Iniciar punto de trabajo, puede ocultar la barra de herramientas global/de nivel superior de un formulario adaptable.
* Puede utilizar nuevos perfiles de acción para las acciones Representar y Enviar en los formularios adaptables.

### Exportar e importar la aplicación de LiveCycle {#livecycle-application-export-and-import}

Dado que los formularios adaptables están en el repositorio de AEM, la exportación de la aplicación de LiveCycle contiene solo las referencias para los formularios adaptables utilizados. Por lo tanto, la exportación e importación de la aplicación de LiveCycle es un proceso de dos pasos. La aplicación de LiveCycle incluye definiciones de procesos, etc. Un paquete independiente que contiene formularios adaptables se exporta como archivo ZIP desde AEM. Durante la importación, la aplicación de LiveCycle se importa mediante Workbench y los formularios adaptables se importan mediante AEM.

## Experiencia del usuario de formularios adaptables en HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace proporciona algunos controles adaptables específicos de formularios, además de los controles disponibles para Mobile Forms. Un usuario puede agregar archivos adjuntos, guardar, firmar, enviar y navegar por los formularios adaptables en HTML Workspace cuando abre una tarea o un punto de inicio. A continuación se incluyen los detalles específicos:

1. Para adjuntar archivos, utilice archivos adjuntos de tareas, como en Mobile Forms. Cualquier botón de tipo Archivo adjunto del formulario adaptable está oculto.

1. Para guardar un formulario adaptable, haga clic en **Guardar**, como en Mobile Forms. Cualquier botón de tipo Guardar del formulario adaptable está oculto.

1. Para enviar un formulario adaptable, utilice el botón **Enviar** o las acciones de ruta disponibles, como en Mobile Forms. Cualquier botón de tipo Enviar del formulario adaptable está oculto.

1. **Visibilidad global de la barra de herramientas del formulario adaptable**: si Process Designer oculta la barra de herramientas global/de nivel superior, la barra de herramientas y los botones no aparecerán en los formularios adaptables.

1. **Controles de navegación de Workspace para formularios adaptables**: Los botones Siguiente/Anterior están disponibles junto con los botones Guardar, Enviar y Acción de ruta para un formulario adaptable en HTML Workspace. Haga clic en los botones Siguiente/Anterior para poder navegar por los paneles de los formularios adaptables en HTML Workspace. Los botones Siguiente/Anterior proporcionan una navegación profunda, similar a los controles de navegación de la vista Móvil de los formularios adaptables.

1. **Servicios de firma electrónica y componente Resumen del formulario adaptable**: El componente Resumen no es operativo en HTML Workspace. En otras palabras, si un formulario adaptable tiene un componente Resumen, no es visible en el espacio de trabajo. En lugar de Enviar automáticamente en el componente Firma electrónica, el usuario del espacio de trabajo hace clic en Enviar o en una acción de ruta en HTML Workspace. Una vez firmado un documento, se puede ver como un documento con firma plano. Haga clic en **Enviar** o una acción de ruta para poder cerrar/completar la tarea o el punto de inicio.\
   El documento firmado se recopila del servidor de servicios de firma electrónica y el archivo xml de datos se reenvía al siguiente paso del proceso.

## Pasos para utilizar formularios adaptables en el diseño del proceso {#steps-to-use-adaptive-forms-in-process-design}

1. Abra Adobe Experience Manager Forms Workbench.

1. Vaya a **Archivo > Nuevo > Aplicación** o utilice la aplicación existente para crear una aplicación.

   ![Crear nueva aplicación](assets/create_new_appl.png)

   Crear aplicación

1. Cree un proceso o utilice un proceso existente en la aplicación.

   ![Crear nuevo proceso](assets/create_new_process.png)

   Crear proceso

1. Cree un punto de inicio o asigne una tarea y haga doble clic en ella.
1. En la sección **[!UICONTROL Presentación y datos]**, seleccione **[!UICONTROL usar un recurso CRX]** y haga clic en los puntos suspensivos antes del recurso.

   ![Usar un recurso CRX](assets/use_crx_asset.png)

   Usar un recurso CRX

1. Seleccione el formulario adaptable creado mediante la interfaz de usuario Administrar recursos y haga clic en **[!UICONTROL Aceptar]**.

   ![Seleccionar un formulario adaptable](assets/selecting_form.png)

   Seleccionar un formulario adaptable

   >[!NOTE]
   >
   >Para obtener más información sobre la creación de un formulario adaptable, consulte [Crear un formulario adaptable](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Para obtener más información sobre cómo crear un proceso, consulte [Crear y administrar procesos](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
