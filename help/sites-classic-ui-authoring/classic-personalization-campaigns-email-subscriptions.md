---
title: Administración de suscripciones
description: Se puede pedir a los usuarios que se suscriban a las listas de correo de Email Service Provider con la ayuda del componente Formulario utilizado en una página web de AEM. Para preparar una página de AEM con un formulario de suscripción para suscribirse a las listas de correo del servicio de correo electrónico, debe aplicar la configuración del servicio correspondiente a la página de AEM que visitará el posible suscriptor.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# Administración de suscripciones{#managing-subscriptions}

>[!NOTE]
>
>Adobe no tiene previsto mejorar esta capacidad (administración de posibles clientes y listas).
>Se recomienda usar [Adobe Campaign y su integración con AEM](/help/sites-administering/campaign.md).

Se puede pedir a los usuarios que se suscriban a las **listas de correo del proveedor de servicios de correo electrónico** con la ayuda del componente **Formulario** que se usa en una página web de AEM. Para preparar una página de AEM con un formulario de suscripción para suscribirse a las listas de correo del servicio de correo electrónico, debe aplicar la configuración del servicio correspondiente a la página de AEM que visitará el posible suscriptor.

## Aplicación de la configuración del servicio de correo electrónico a una página {#applying-email-service-configuration-to-a-page}

Para configurar una página de AEM:

1. Vaya a la ficha **Sitios web**.
1. Seleccione la página que debe configurarse para el servicio. Haga clic con el botón derecho en la página y seleccione **Propiedades**.

1. Seleccione **Cloud Services** y después **Agregar servicio**. Seleccione una configuración de la lista de configuraciones disponibles.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Haga clic en **OK**.

## Creación de un formulario de suscripción en una página de AEM para suscribirse o cancelar la suscripción a listas {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Para crear un formulario de registro y configurarlo para suscripciones a las listas de correo del proveedor de servicios de correo electrónico:

1. Abra la página de AEM que visitará el usuario.
1. Aplique la configuración del proveedor de servicios de correo electrónico a la página.

1. Agregue un componente **Form** a la página arrastrando el componente desde la barra de tareas. Si el componente no está disponible, cambie al modo de diseño y habilite el grupo **Formulario**.
1. Haga clic en **Editar** en la barra de **Inicio del formulario** y vaya a la pestaña **Avanzado**.
1. En el menú desplegable **Formulario**, seleccione **Servicio de correo electrónico: Crear suscriptor** y agréguelo a la lista.
1. En la parte inferior del cuadro de diálogo, abra la lista desplegable **Configuración de acción**, que le permite seleccionar una o más listas de suscripción.
1. En **Seleccionar lista**, seleccione la lista a la que desee que se suscriban los usuarios. Puede agregar varias listas usando el botón más (**Agregar elemento**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >El cuadro de diálogo puede variar según el proveedor de servicios de correo electrónico.

1. En la pestaña **Formulario**, seleccione la página de agradecimiento a la que desee que vayan los usuarios una vez enviado el formulario (si se deja en blanco, el formulario se volverá a mostrar tras el envío). Haga clic en **Aceptar**. Aparece un componente **ID de correo electrónico** en el formulario, que le permite crear un formulario en el que los usuarios pueden enviar sus direcciones de correo electrónico para suscribirse o cancelar la suscripción a una lista de correo.
1. Agregue el componente de botón **Enviar** desde la sección **Formulario** de la barra de tareas.

   El formulario está listo. Publique la página configurada en los pasos anteriores junto con la página **gracias** en la instancia de publicación. Cualquier suscriptor potencial que visite la página puede rellenar el formulario y suscribirse a la lista proporcionada en la configuración.

   >[!NOTE]
   >
   >Para que la suscripción al formulario funcione correctamente, es necesario exportar e importar [claves de cifrado del autor en la instancia de publicación](#exporting-keys-from-author-and-importing-on-publish).

## Exportación de claves de autor e importación en publicación {#exporting-keys-from-author-and-importing-on-publish}

Para que el servicio de correo electrónico pueda suscribirse y cancelar la suscripción a través del formulario de registro en la instancia de publicación, debe seguir estos pasos:

1. En la instancia de autor de, vaya al Administrador de paquetes.
1. Cree un paquete. Establezca el filtro como `/etc/key`.
1. Genere y descargue el paquete.
1. Vaya al Administrador de paquetes en la instancia de publicación y cargue este paquete.
1. Vaya a la consola Publicar osgi y reinicie el paquete denominado **Adobe Granite Crypto Support**.

## Cancelar la suscripción de usuarios a listas {#unsubscribing-users-from-lists}

Para cancelar la suscripción de usuarios a listas:

1. Abra las propiedades de página de la página de AEM que tiene el formulario de registro para cancelar la suscripción de un posible cliente.
1. Aplique la configuración del servicio a la página.
1. Cree un formulario de registro en la página.
1. Al configurar el componente, seleccione la acción **Servicio de correo electrónico**: **Cancelar la suscripción del usuario a la lista.**
1. En el menú desplegable, seleccione la lista adecuada de la que se eliminará el usuario al cancelar la suscripción.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exporte las claves del autor para publicarlas.

## Configuración de correos electrónicos de respuesta automática para el servicio de correo electrónico {#configuring-auto-responder-emails-for-email-service}

Para configurar un correo electrónico de respuesta automática para un suscriptor:

1. Abra las propiedades de página de la página de AEM que tienen el formulario de registro para configurar el respondedor automático de un posible cliente.
1. Aplique la configuración de ExactTarget a la página.

1. Agregue un componente **Form** a la página arrastrando el componente desde la barra de tareas. Si el componente no está disponible, cambie al modo de diseño y habilite el grupo **Formulario**.
1. Haga clic en **Editar** en la barra de **Inicio del formulario** y vaya a la pestaña **Avanzado**.
1. En el menú desplegable **Formulario**, seleccione **Servicio de correo electrónico: Enviar correo electrónico de respuesta automática.**
1. **Seleccione un correo electrónico** (este es el correo que se envía como correo electrónico de respuesta automática).

1. **Seleccionar clasificación** (esta clasificación se usa para enviar el correo electrónico).
1. Seleccione la página **Gracias** (la página a la que se dirige a los usuarios cuando envían el formulario).

   En la pestaña **Formulario**, seleccione la página de agradecimiento a la que desee que vayan los usuarios una vez que envíen el formulario. (Si se deja en blanco, el formulario se vuelve a mostrar tras el envío). Haga clic en **Aceptar**.

1. Exporte las claves del autor para publicarlas.
1. Agregue el componente de botón **Enviar** desde la sección **Formulario** de la barra de tareas.

   El formulario de registro está listo. Publique la página configurada en los pasos anteriores junto con la página **gracias** en la instancia de publicación. Cualquier suscriptor potencial que visite la página puede rellenar el formulario y, al enviarlo, el visitante recibirá un correo electrónico de respuesta automática con el ID de correo electrónico rellenado en el formulario.

   >[!NOTE]
   >
   >Para que la suscripción al formulario de registro funcione correctamente, es necesario exportar e importar [claves de cifrado del autor en la instancia de publicación](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
