---
title: Publicación de un correo electrónico para proveedores de servicios de correo electrónico
description: Puede publicar boletines en servicios de correo electrónico como ExactTarget y Silverpop Engage.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 2%

---

# Publicación de un correo electrónico para proveedores de servicios de correo electrónico{#publishing-an-email-to-email-service-providers}

Puede publicar boletines en servicios de correo electrónico como ExactTarget y Silverpop Engage. En este documento se describe cómo configurar AEM para que publique una newsletter en estos servicios de correo electrónico.

>[!NOTE]
>
>Debe configurar el proveedor de servicios para poder crear y publicar un correo electrónico. Consulte [Configuración de ExactTarget](/help/sites-administering/exacttarget.md) y [Configuración de Silverpop Engage](/help/sites-administering/silverpop.md) para obtener más información.

Para publicar el correo electrónico en el proveedor de servicios de correo electrónico, debe realizar los siguientes pasos:

1. Cree un correo electrónico.
1. Aplique la configuración del servicio de correo electrónico al correo electrónico.
1. Publique el correo electrónico.

>[!NOTE]
>
>Si actualiza los proveedores de correo electrónico, realiza una prueba de vuelo o envía una newsletter, estas operaciones fallan si la newsletter no se publica primero en la instancia de publicación o si la instancia de publicación no está disponible. Asegúrese de publicar la newsletter y de que la instancia de publicación esté activa y en ejecución.

## Creación de un correo electrónico {#creating-an-email}

Un correo electrónico o newsletter que desee publicar en un servicio de correo electrónico se puede crear en una campaña utilizando la plantilla **Geometrixx Newsletter**. También puede usar la plantilla **Geometrixx Outdoors E-Mail**. Ejemplo de correo electrónico/newsletter basado en la plantilla **Geometrixx Outdoors E-Mail** disponible en `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

Para crear un correo electrónico publicado en el servicio de correo electrónico configurado:

1. Vaya a **Sitios web** y luego a **Campañas**. Seleccione una campaña.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página**.
1. Escriba el título, el nombre y seleccione la plantilla **Geometrixx Newsletter** de la lista de plantillas disponibles.
1. Haga clic en **Crear**.
1. Abra el correo electrónico creado.
1. Cambie al modo de diseño para seleccionar los componentes que desea mostrar en la barra de tareas.
1. Cambie al modo de edición y empiece a agregar contenido (texto, imágenes, [herramientas de correo electrónico](#adding-exacttarget-email-tools-to-your-email), [variables de personalización](#adding-text-and-personalization-tool-to-your-e-mail), etc.) al correo electrónico.

### Añadir las herramientas de correo electrónico de ExactTarget al correo electrónico {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>Esta sección es específica del servicio ExactTarget.

El componente **Herramientas de correo electrónico** para ExactTarget puede agregar más funciones de correo electrónico al correo electrónico/newsletter.

1. Abra un correo electrónico para publicarlo en ExactTarget.
1. Agregue el componente **ET - Herramientas de correo electrónico** a su página mediante la barra de tareas. Abra el componente en modo de edición.

   ![chlimage_1](assets/chlimage_1.gif)

1. Seleccione una opción del menú **Opciones**:

<table>
 <tbody>
  <tr>
   <td>Dirección física de envío (obligatoria)</td>
   <td>Este componente inserta la dirección de correo física de la organización en el correo electrónico.</td>
  </tr>
  <tr>
   <td>Centro de perfiles (obligatorio)</td>
   <td>El centro de perfiles es una página web en la que los suscriptores pueden introducir y mantener la información personal que mantiene sobre ellos.</td>
  </tr>
  <tr>
   <td>Ver correo electrónico como página Web</td>
   <td>Este componente permite al usuario ver el correo electrónico como una página web.</td>
  </tr>
  <tr>
   <td>Política de privacidad</td>
   <td>Este componente inserta el vínculo a la directiva de privacidad en el correo electrónico.<br /> </td>
  </tr>
  <tr>
   <td>Centro de cancelación de suscripciones</td>
   <td>Da la opción al usuario de cancelar la suscripción a su lista de correo.</td>
  </tr>
  <tr>
   <td>Centro de suscripciones</td>
   <td>Un centro de suscripciones es una página web en la que un suscriptor puede controlar los mensajes que recibe de su organización.</td>
  </tr>
  <tr>
   <td>Seguimiento de aperturas de correo electrónico</td>
   <td>Componente oculto que le permite utilizar la característica de seguimiento ExactTarget.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El menú desplegable **Opciones** solo se rellena si se aplica la configuración de ExactTarget al correo electrónico. Consulte [Aplicación de la configuración del servicio de correo electrónico a la configuración del correo electrónico](#applying-e-mail-service-configuration-to-e-mail-settings) para obtener más información.

1. Publique el correo electrónico en ExactTarget.

   El correo electrónico con las herramientas de correo electrónico está disponible para su uso en la cuenta configurada de ExactTarget.

>[!NOTE]
>
>* Las direcciones URL de las herramientas de correo electrónico se reemplazan (en el correo electrónico recibido) por sus valores reales solo cuando se envía un correo electrónico con **Envío simple** o **Envío guiado**, pero no con **Envío de prueba**.
>
>* Se requieren dos herramientas de correo electrónico: **Dirección física de correo (obligatoria)** y **Centro de perfiles (obligatoria)**. Cuando el correo electrónico se publica en ExactTarget, estas dos herramientas de correo electrónico se agregan al final de cada correo de forma predeterminada.
>

### Agregar la herramienta Texto y Personalization al correo electrónico {#adding-text-and-personalization-tool-to-your-e-mail}

Puede agregar campos personalizados en un correo electrónico agregando el componente **Texto y Personalization** a la página:

1. Abra el correo electrónico que va a publicar en el servicio de correo electrónico.
1. Para habilitar el campo de personalización desde el servicio de correo electrónico, añada la configuración del marco de trabajo al configurar el servicio de correo electrónico. Consulte [Configuración de Silverpop Engage](/help/sites-administering/silverpop.md) y [Configuración de Exact Target](/help/sites-administering/exacttarget.md) para obtener más información.
1. Agregue el componente **Texto y Personalization** de la barra de tareas. Este componente forma parte del grupo de newsletter. Abra este componente en modo de edición.

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. Agregue el campo personalizado requerido al texto seleccionando el campo en el menú desplegable y haciendo clic en **Insertar**.
1. Haga clic en **Aceptar** para finalizar.

## Aplicar la configuración del servicio de correo electrónico a la configuración de correo electrónico {#applying-e-mail-service-configuration-to-e-mail-settings}

Para aplicar la configuración del servicio de correo electrónico a un boletín informativo:

1. Cree una configuración de servicio de correo electrónico.
1. Abra el correo electrónico o la newsletter.
1. Abra la configuración del correo electrónico/newsletter haciendo clic en **Configuración** o haciendo clic en **Propiedades de página en** la barra de tareas.
1. Haga clic en **Agregar servicio** en la ficha **Cloud Services**. Verá la lista de servicios. Seleccione la configuración necesaria, ya sea **ExactTarget** o **Silverpop**, en la lista desplegable.

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. Haga clic en **OK**.

## Publicar correos electrónicos en el servicio de correo electrónico {#publishing-emails-to-email-service}

Los correos electrónicos/boletines se pueden publicar en el servicio de correo electrónico siguiendo estos pasos:

1. Abra el correo electrónico.
1. Antes de publicar un correo electrónico, asegúrese de que ha aplicado la configuración correcta a su correo electrónico.
1. Haga clic en **Publicar**. Se abrirá la ventana **Publicar newsletter en el proveedor de servicios de correo electrónico**.
1. Rellene el campo **Nombre de la newsletter**. El correo electrónico/newsletter se publica en el proveedor de servicios de correo electrónico con este nombre. Si no se proporciona un nombre de correo electrónico, el correo electrónico se publica con el nombre de página del boletín en AEM.
1. Haga clic en **Publicar**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   Si lo consigue, AEM confirma que puede ver el correo electrónico en ExactTarget o Silverpop Engage.

   Si existe ExactTarget, el correo electrónico publicado se puede ver haciendo clic en **Ver correo electrónico publicado**. Esto lo lleva directamente a la newsletter publicada en ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/)).

>[!NOTE]
>
>Si se publica un correo electrónico/newsletter con el mismo nombre que el de un correo electrónico/newsletter ya publicado, el correo electrónico/newsletter anterior no se reemplaza. En su lugar, se crea un nuevo correo electrónico/boletín con el mismo nombre (los ID de dos boletines son, sin embargo, diferentes).
>
>La publicación del correo electrónico/newsletter en el proveedor de servicios de correo electrónico también publica el correo electrónico/newsletter en la instancia de publicación de AEM.
>

### Actualizar Un Correo Electrónico Publicado {#updating-a-published-e-mail}

El botón **Actualizar** del cuadro de diálogo Publicar le permite actualizar un boletín ya publicado en un proveedor de servicios de correo electrónico. Si la newsletter aún no se ha publicado y se hace clic en el botón **Actualizar**, se mostrará el mensaje **La newsletter no se ha publicado**.

Para actualizar un correo electrónico publicado:

1. Abra el correo electrónico o la newsletter que se ha publicado anteriormente en un proveedor de servicios de correo electrónico que desee volver a publicar después de realizar cambios en el correo electrónico o la newsletter.
1. Haga clic en **Publicar**. Se muestra la ventana **Publicar newsletter en el proveedor de servicios de correo electrónico**. Haga clic en **Actualizar**.

   Para comprobar si el correo electrónico o la newsletter se han actualizado en ExactTarget, haga clic en **Ver correo electrónico publicado**. Esto le lleva al correo electrónico publicado en ExactTarget.

   Para comprobar si el correo electrónico o la newsletter se han actualizado en el servicio de correo electrónico de Silverpop, visite el sitio de participación de Silverpop.
