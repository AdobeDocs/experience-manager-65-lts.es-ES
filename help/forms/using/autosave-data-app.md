---
title: Usar el guardado automático en la aplicación de AEM Forms
description: Aprenda a utilizar la función de guardado automático en la aplicación de AEM Forms para evitar la pérdida de datos.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 90%

---

# Usar el guardado automático en la aplicación de AEM Forms{#using-autosave-in-aem-forms-app}

Cuando un usuario introduce datos en la aplicación de Adobe Experience Manager Forms, la función de guardado automático los guarda a intervalos regulares. La función de guardado automático de la aplicación de AEM Forms ayuda a evitar la pérdida de datos si la aplicación se cierra accidentalmente.

La aplicación se puede cerrar accidentalmente en los siguientes casos:

* Si el dispositivo se apaga debido a una batería baja
* Si el usuario cierra la aplicación
* Si se produce un bloqueo inesperado

Puede especificar los intervalos tras los cuales la aplicación guardará los datos introducidos.

>[!NOTE]
>
>Seleccione la frecuencia de guardado automático de forma correcta. Las operaciones frecuentes de guardado automático pueden tener un impacto notable en el rendimiento del dispositivo.

Siga estos pasos para utilizar la función de guardado automático en la aplicación de AEM Forms:

1. Inicie sesión en la aplicación y navegue hasta **Configuración > General**.
1. En la pantalla General, utilice la opción **Frecuencia de guardado automático** para seleccionar los intervalos a los que desea que la aplicación guarde los datos introducidos.
   [![Estableciendo frecuencia de guardado automático](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Cuando reinicie la aplicación e inicie sesión con el mismo usuario, se le pedirá que restaure la tarea con el cuadro de diálogo Recuperar tarea no guardada. Haga clic en **Aceptar** en el cuadro de diálogo Recuperar tarea no guardada para reanudar el trabajo con la tarea guardada. Puede hacer clic en **Cancelar** para eliminar los datos guardados correspondientes al último guardado automático activado y comenzar a trabajar con una tarea nueva.

   Al hacer clic en **Aceptar**, la tarea se restaurará con los datos correspondientes a la última función de guardado automático activada antes de que la aplicación se bloqueara. Incluye los datos del formulario y todos los archivos adjuntos asociados a la tarea.
   [![Recuperando una tarea &#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Un formulario de trabajo en curso **B.** Aplicación cerrada a la fuerza **C.** Aplicación reiniciada con el cuadro de diálogo Recuperar tarea no guardada **D.** Formulario restaurado con datos originales
