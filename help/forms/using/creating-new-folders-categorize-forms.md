---
title: Crear carpetas nuevas para aplicar categorías a los formularios
description: Utilice carpetas para organizar las plantillas de formulario, los PDF, los recursos y los formularios adaptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 98%

---

# Crear carpetas nuevas para aplicar categorías a los formularios {#create-new-folders-to-categorize-forms}

Puede organizar mejor los recursos mediante carpetas. Dado que AEM Forms admite varios tipos de recursos (plantillas de formulario, PDF, documentos, recursos y formularios adaptables, con varios metadatos), puede utilizar carpetas para clasificar los formularios según los criterios deseados.

AEM Forms permite cambiar el título de una carpeta. El título no es el mismo que el nombre del nodo en el que se almacena la carpeta en el repositorio. En su lugar, el título se mantiene como metadatos para la carpeta. Si cambia el título de una carpeta, la ruta de cualquier recurso presente dentro de la carpeta no se verá afectada.

## Crear una carpeta. {#create-a-folder}

Puede crear una carpeta en AEM Forms de una de las siguientes maneras:

* Cargue un archivo ZIP que contenga recursos en la estructura de las carpetas deseadas (Consulte [Conseguir documentos XDP y PDF en AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Crear una carpeta vacía

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.
1. Vaya a la ubicación en la que desea crear una carpeta.
1. Haga clic en el icono ![aem6forms_add](assets/aem6forms_add.png) de la barra de herramientas y, a continuación, seleccione **[!UICONTROL Crear carpeta]**.

1. Introduzca la siguiente información:

   * **Título:** Nombre para mostrar de la carpeta
   * **Nombre:** *(Obligatorio)* El nombre del nodo en el que desea almacenar la carpeta en el repositorio

   >[!NOTE]
   >
   >De forma predeterminada, el valor del campo de nombre se rellena automáticamente a partir del título. El nombre solo puede contener caracteres alfanuméricos o los caracteres especiales guion (-) y guion bajo (_). Cualquier otro carácter especial especificado en el título se reemplaza automáticamente por un guion y se le solicita que confirme el nuevo nombre. Puede elegir continuar con el nombre sugerido o editarlo más adelante.

1. Haga clic en **[!UICONTROL Enviar].**

   Se muestra una nueva carpeta con el título que haya definido en la ubicación actual de la lista de recursos.

   Si existe una carpeta con el nombre especificado, el envío falla con un error. Puede ver el mensaje de error pasando el puntero sobre el icono de error ![aem6forms_error_alert](assets/aem6forms_error_alert.png) que aparece junto al campo de nombre.

### Editar el título de la carpeta {#edit-the-folder-title-br}

1. Seleccione la carpeta cuyo título desee editar.
1. Haga clic en el icono de edición ![aem6forms_edit](assets/aem6forms_edit.png) de la barra de herramientas.
1. Escriba el título nuevo. El campo de texto se rellena previamente con el valor actual del título de la carpeta. Puede cambiarlo a un valor nuevo.
1. Haga clic en **[!UICONTROL Enviar].**
