---
title: Canal de impresión y canal web
description: Importar plantillas del canal de impresión y crear y activar plantillas del canal web
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 86%

---

# Canal de impresión y canal web{#print-channel-and-web-channel}

Las comunicaciones interactivas se pueden entregar mediante dos canales: impresión y web. El canal de impresión se utiliza para crear PDF y comunicaciones en papel, como una carta impresa como recordatorio de pago de primas de seguro, mientras que el canal web se utiliza para ofrecer experiencias en línea, como un extracto de tarjeta de crédito en un sitio web.

Los autores de comunicaciones interactivas pueden reutilizar recursos como fragmentos de documento e imágenes para crear versiones impresas y web de la comunicación interactiva.

Uno de los requisitos previos para [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md) es tener las plantillas para impresión y/o canal web disponibles en el servidor. Mientras los autores de plantillas crean la plantilla del canal web en AEM, la plantilla de canal de impresión XDP se crea en Adobe Forms Designer y se carga en el servidor.

## Canal de impresión {#printchannel}

El canal de impresión de una comunicación interactiva utiliza la plantilla de formulario XFA, XDP. Los XDP se diseñan en Adobe Forms Designer. Para obtener más información sobre la creación de plantillas de canal de impresión, consulte [Diseño](../../forms/using/layout-design-details.md). Para utilizar una plantilla de canal de impresión en la comunicación interactiva, debe cargar la plantilla en el servidor de AEM Forms.

### Cargar plantilla del canal de impresión de comunicación interactiva {#upload-interactive-communication-print-channel-template}

Para cargar la plantilla, debe ser miembro del grupo de usuarios de formularios. Siga los siguientes pasos para cargar la plantilla del canal de impresión (XDP) en AEM Forms:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.

1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Carga de archivo]**.

   Desplácese, seleccione la plantilla de canal de impresión (XDP) adecuada y seleccione **[!UICONTROL Abrir]**.

## Canal web {#web-channel}

Los autores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Para permitir que otros usuarios creen plantillas web, debe otorgarles derechos. Para obtener más información, consulte [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md).

### Crear plantillas de canal web {#authoring-web-channel-template}

Para crear una plantilla de canal web, primero debe crear una carpeta de plantilla. Una vez que haya creado una plantilla web dentro de una carpeta de plantilla, debe habilitar la plantilla para permitir a los usuarios de los formularios crear un canal web de comunicación interactiva basada en la plantilla.

Para crear una plantilla de canal web, complete los siguientes pasos:

1. Cree una carpeta de plantilla para mantener las plantillas web de comunicación interactiva, si todavía no dispone de una. Para obtener más información, consulte Carpetas de plantilla en [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md).

   1. Seleccione **[!UICONTROL Herramientas]** ![herramientas](assets/tools.png) > **[!UICONTROL Explorador de configuración]**.
      * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
   1. En la página Explorador de configuración, seleccione **[!UICONTROL Crear]**.
   1. En el cuadro de diálogo Crear configuración, especifique un título para la carpeta, marque **[!UICONTROL Plantillas editables]** y seleccione **[!UICONTROL Crear]**.

      La carpeta se crea y se enumera en la página Explorador de configuración.

1. Vaya a la carpeta de plantillas adecuada y cree una plantilla web.

   1. Vaya a la carpeta de plantillas adecuada al seleccionar **[!UICONTROL Herramientas]** > **[!UICONTROL Plantillas]** > **`[Folder]`**.
   1. Seleccione **[!UICONTROL Crear]**.
   1. Seleccione **[!UICONTROL Comunicación interactiva - Canal web]** y seleccione **[!UICONTROL Siguiente]**.
   1. Escriba un título y una descripción de plantilla y luego seleccione **[!UICONTROL Crear]**.

      La plantilla se crea y aparece un cuadro de diálogo.

   1. Seleccione **[!UICONTROL Abrir]** para abrir la plantilla que creó en el Editor de plantillas.

      Aparecerá el editor de plantillas.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Al crear o editar una plantilla, hay distintos aspectos que el autor de plantillas pueden definir. Crear o editar una plantilla es similar a crear páginas. Para obtener más información, consulte Editar plantillas: autores de plantillas en [Crear plantillas de página](/help/sites-authoring/templates.md).

1. Para permitir el uso de esta plantilla para la creación de comunicaciones interactivas, habilite la plantilla.

   1. Seleccione **[!UICONTROL Herramientas]** ![herramientas](assets/tools.png) > **[!UICONTROL Plantillas]**.
   1. Vaya a la plantilla adecuada, selecciónela y seleccione **[!UICONTROL Habilitar]**. En el mensaje de alerta, seleccione **[!UICONTROL Habilitar]**.

      La plantilla está habilitada y su estado se muestra como Habilitada. Ahora puede continuar creando una comunicación interactiva en la que puede utilizar la plantilla de canal web recién creada.

### Imprimir canal como principal para el canal web {#print-channel-as-master-for-web-channel}

Durante la creación de una comunicación interactiva, los autores pueden seleccionar esta opción para crear el canal web sincronizado con el canal de impresión. Utilizar el canal de impresión como principal para el canal web garantiza que el contenido, la herencia y el enlace de datos del canal web se deriven del canal de impresión y que los cambios realizados en el canal de impresión se puedan reflejar en el canal web. Sin embargo, los autores de la comunicación interactiva pueden romper la herencia de componentes específicos del canal web, según sea necesario.

![Imprimir canal como principal](assets/create_ic_print_master_new.png) ![Canal web con canal de impresión como principal](assets/create_ic_print_master_web_new.png)
