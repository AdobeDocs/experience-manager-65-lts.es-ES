---
title: Guardar formularios como plantillas
description: Aprenda a crear plantillas a partir de formularios con datos que se requieren repetidamente.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 83%

---

# Guardar formularios como plantillas {#save-forms-as-templates}

A veces, cuando los usuarios rellenan un formulario, las entradas de algunos campos son las mismas. Para estas instancias, puede rellenar los campos que requieran valores idénticos en cada caso y guardar el formulario o borrador como plantilla. Cada vez que cree una instancia de plantilla, los campos especificados ya se rellenarán con los valores especificados en la plantilla. Le ahorra tiempo y esfuerzo para rellenar el formulario.

Realice los siguientes pasos para crear una plantilla:

1. Abra un formulario y seleccione o rellene los campos que tengan valores casi idénticos cada vez que lo utilice. Puede incluir un archivo adjunto con la plantilla que suele agregar al rellenar el formulario.
1. Seleccione el icono **Guardar como plantilla** ![save_as_template](assets/save_as_template.png)icono. Aparecerá un cuadro de diálogo para especificar el nombre de la plantilla.
1. Especifique el nombre de la plantilla y seleccione **Guardar**. La plantilla aparecerá en la carpeta de plantillas.

   Si existe una plantilla con el mismo nombre, aparecerá un cuadro de diálogo para confirmar que se sobrescribe la plantilla existente. Para reemplazar la plantilla existente por una nueva, selecciona **Continuar** o para guardar la plantilla con un nombre diferente, selecciona **Cancelar**.

Ahora, puede abrir la plantilla guardada. Cada vez que se abre una plantilla, se crea un formulario o una tarea nuevos y el formulario muestra los datos guardados y las opciones. Con las plantillas, puede editar los datos precargados, agregar un archivo adjunto, guardar como borrador, enviar la tarea o crear otra plantilla que lo utilice. Las plantillas son específicas de los dispositivos móviles y no se sincronizan con el servidor de Adobe Experience Manager Forms.

También puede eliminar una plantilla si ya no es necesaria. Para eliminar una plantilla, navegue hasta la carpeta de plantillas, seleccione los puntos suspensivos y, a continuación, seleccione **Eliminar plantilla**.

>[!NOTE]
>
>Una plantilla está disponible de forma local y no se sincroniza con el servidor. Al borrar los datos locales de la aplicación, se eliminará la plantilla.
