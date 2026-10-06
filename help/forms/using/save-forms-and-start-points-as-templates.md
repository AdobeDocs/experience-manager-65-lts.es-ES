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
exl-id: 5e5ce783-8d0c-421c-b938-7020215682a0
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2b710c6ef8d291a42b4a7658bf84f5e764422d5c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 71%
---
# Guardar formularios como plantillas {#save-forms-as-templates}

>[!NOTE]
>
>Las versiones de Android y iOS de la aplicación de AEM Forms se han suspendido. La aplicación de Android se canceló la publicación de Google Play en septiembre de 2026 y la aplicación de iOS se ha eliminado de Apple App Store.
>Estas aplicaciones ya no están disponibles para la instalación. Para obtener ayuda con la aplicación Android, comuníquese con [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

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
