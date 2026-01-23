---
title: Tutorial del sitio de referencia de We.Gov y We.Finance
description: Utilice usuarios y grupos ficticios para realizar tareas de AEM Forms mediante el paquete de demostración We.Gov y We.Finance.
contentOwner: anujkapo
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
exl-id: a9cbab12-62a6-4779-955f-2858166945e6
source-git-commit: 86ca5b498d0a51e21e247d07ce186d8a01c95baa
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 56%

---

# Tutorial del sitio de referencia de We.Gov y We.Finance {#we-gov-reference-site-walkthrough}

## Requisitos previos {#pre-requisites}

Configure el sitio de referencia tal como se describe en [Configure y configure el sitio de referencia de We.Gov y We.Finance](../../forms/using/forms-install-configure-gov-reference-site.md).

## Historia del usuario {#user-story}

* AEM Forms

   * Conversión de formularios automatizada
   * Creación
   * Modelos de datos de formulario/Fuentes de datos

* AEM Forms

   * Data Capture
   * (Opcional) Integración de datos (MS® Dynamics)
   * (Opcional) Adobe Sign

* Flujo de trabajo
* Notificaciones por correo electrónico
* (Opcional) Comunicaciones con los clientes

   * Canal de impresión
   * Canal web

* Adobe Analytics
* Integraciones de fuentes de datos

### Usuarios y grupos ficticios {#fictitious-users-and-groups}

El paquete de demostración de We.Gov viene con los siguientes usuarios ficticios integrados:

* **Aya Tan**: una ciudadana que reúne los requisitos para solicitar una prestación de una agencia pública.

![Usuario ficticio](/help/forms/using/assets/aya_tan_new.png)

* **George Lang**: analista empresarial de la agencia We.Gov.

![Usuario ficticio](/help/forms/using/assets/george_lang.png)

* **Camila Santos**: directora de CX de la agencia We.Gov.

![Usuario ficticio](/help/forms/using/assets/camila_santos.png)

También se incluyen los siguientes grupos:

* **Usuarios De Forms de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)

* **Usuarios de We.Gov**

   * George Lang (miembro)
   * Camila Santos (miembro)
   * Aya Tan (miembro)

### Leyenda de los términos de la descripción general de la demostración {#demo-overview-terms-legend}

1. **Suplantar**: los usuarios y grupos definidos en la demostración de AEM.
1. **Botón**: un rectángulo de color o una flecha en círculo para navegar por la demostración.
1. **Haga clic**: para ejecutar una acción en la historia del usuario.
1. **Vínculos**: En la parte superior del menú principal del sitio de We.Gov.
1. **Instrucciones para el usuario**: un conjunto de pasos numéricos a seguir cuando se navega por la historia del usuario.
1. **Portal de Forms**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*.
1. **Vista móvil**:We.Gov del usuario para replicar una vista móvil con un explorador cuyo tamaño se ha cambiado.
1. **Vista de escritorio**: el usuario de We.Gov para ver la demostración en un ordenador portátil o de escritorio.
1. **Formulario de prefiltrado**: un formulario de la página de inicio del sitio de We.Gov.
1. **Formulario adaptable**: el formulario de solicitud de la demostración de We.Gov.

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Sitio Web de We.Gov de Adobe**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Bandeja de entrada de Adobe**: el [icono en forma de campana](assets/bell.svg) situado en la barra de menús superior del back-end de AEM.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **Cliente de correo electrónico**: la forma preferida de ver los correos electrónicos (Gmail, Outlook).
1. **CTA**: llamada a la acción.
1. **Navegar**: permite localizar un punto de referencia específico en la página del explorador.
1. **AFC**: conversión de formularios automatizada.

## Conversión de formularios automatizada (Camila) {#automated-forms-conversion}

**Esta sección**: Camila, la directora de CX, tiene un formulario basado en PDF existente que ha sido utilizado como parte de un proceso basado en el papel. Como parte del esfuerzo de modernización, Camila desea utilizar este formulario de PDF para crear automáticamente un Forms adaptable moderno.

### Conversión de formularios automatizada - We.Gov (Camila) {#automated-forms-conversion-wegov}

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. Inicie sesión con:
   * **Usuario**: camila.santos
   * **Contraseña**: password
1. En la página principal, seleccione Forms > Forms y documentos > AEM Forms We.gov Forms > AFC.
1. Camila carga el PDF en AEM Forms.

   ![Cargar formulario](assets/aftia-upload-form.jpg)

1. A continuación, Camilla selecciona el formulario PDF y hace clic en **Iniciar conversión automatizada** para iniciar el proceso de conversión. Es posible que tenga que hacer clic en **Sobrescribir conversión** si ha convertido el formulario.

   >[!NOTE]
   >
   >Los ajustes de AFC están preconfigurados para el usuario final, lo que significa que no deben modificarse.

   * **Opcional**: si desea utilizar el Ultramarino accesible, simplemente haga clic en Especificar un tema para el formulario adaptable y seleccione el tema Accesible-Ultramarino que aparece en la lista de opciones.

   ![Iniciar conversión](assets/aftia-start-conversion.jpg)

   ![Temática Ultramarine](assets/aftia-upload-conversion-settings.jpg)

   El estado del porcentaje completado se muestra durante la conversión. Una vez que se muestre el estado **Convertido**, haga clic en la carpeta **output**, seleccione el formulario adaptable y haga clic en **Editar** para abrir el formulario convertido.

1. A continuación, Camilla revisa el formulario y se asegura de que todos los campos están presentes.

   ![Revisar conversión](assets/aftia-review-conversion.jpg)

1. A continuación, Camilla comienza a editar el formulario y selecciona Panel raíz > Editar (la llave inglesa) > selecciona Pestañas en la parte superior del menú desplegable Diseño del panel > selecciona la casilla de verificación.

   ![Revisar propiedades](assets/aftia-review-properties.jpg)

1. A continuación, Camilla realiza todas las modificaciones necesarias en el código CSS y en los campos para producir el producto final.

   ![Agregar CSS](assets/aftia-add-css.jpg)

### Modelo de datos de formulario y fuentes de datos (Camila) {#data-sources}

**Esta sección**: después de convertir el documento y de producir un formulario adaptable, Camila debe conectar el formulario adaptable a un origen de datos.

1. Abre las Propiedades del formulario convertido en [Conversión de formularios automatizada - We.Gov](#automated-forms-conversion-wegov).

1. A continuación, Camila selecciona Modelo de formulario. Luego selecciona Modelo de datos de formulario en el menú desplegable Seleccionar de y selecciona el FDM de solicitud de We.Gov en la lista de opciones.

1. Haga clic en Guardar y cerrar.

   ![Selección de FDM](assets/aftia-select-fdm.jpg)

1. Camila hace clic en la carpeta **output**, selecciona el formulario adaptable y hace clic en **Editar** para abrir el formulario de We.Gov completado.
1. Selecciona un campo de formulario adaptable y hace clic en ![Configurar icono](assets/configure-icon.svg) y crea un enlace con las entidades del modelo de datos de formulario utilizando el campo **Referencia de enlace**. Camila repite este paso en todos los campos del formulario adaptable.

### Probar la accesibilidad del formulario (Camila) {#form-accessibility-testing}

Camila también comprueba que el contenido creado se ha generado correctamente y es totalmente accesible de acuerdo con los estándares corporativos.

1. Camila hace clic en la carpeta **output**, selecciona el formulario adaptable y hace clic en **Vista previa** para abrir el formulario de We.Gov completado.

1. Abre la pestaña Auditoría en la herramienta para desarrolladores de Chrome.

1. Realiza una comprobación de accesibilidad para validar el formulario adaptable.

   ![Comprobación de accesibilidad](assets/aftia-accessibility.jpg)

## Demostración de la vista móvil del formulario adaptable (Aya) {#mobile-view-demo}

**Esta sección debe realizarse antes de la demostración.**

**Instrucciones para el usuario:**

1. Vaya a: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. Inicie sesión con:

   1. **Usuario**: aya.tan
   1. **Contraseña**: password

1. Cambie el tamaño de la ventana del explorador o utilice el emulador del explorador para replicar el tamaño de un dispositivo móvil.

### Sitio web de We.Gov (Aya) {#aya-user-story-we-gov-website}

![Usuario ficticio](/help/forms/using/assets/aya_tan_new-1.png)

**Esta sección**: Aya es una ciudadana y un amigo le cuenta que podría ser elegible para recibir un servicio de una agencia gubernamental. Aya visita el sitio web de We.Gov desde su teléfono móvil para obtener más información sobre las prestaciones para las que reúne los requisitos.

### Prefiltrado de We.Gov (Aya) {#aya-user-story-we-gov-pre-screener}

Aya responde a una serie de preguntas para confirmar que reúne los requisitos rellenando un breve formulario adaptativo en su teléfono móvil.

**Instrucciones para el usuario:**

1. Realice una selección en cada campo desplegable.

   >[!NOTE]
   >
   >Si el usuario gana más de 200 000 dólares al año, no reúne los requisitos.

1. Haga Clic En **¿Cumplo Los Requisitos?**.
1. Haga clic en **Solicitar ahora** para continuar.

   ![Vínculo Solicitar ahora](/help/forms/using/assets/apply_now_link.png)

### Formulario adaptable de We.Gov (Aya) {#aya-user-story-we-gov-adaptive-form}

Aya descubre que reúne los requisitos y comienza a rellenar su solicitud para solicitar la prestación desde su dispositivo móvil.

Debe revisar algunos documentos en casa antes de poder completar la solicitud de la prestación. Guarda y sale de la solicitud en su dispositivo móvil.

**Instrucciones para el usuario:**

1. Rellene los campos de Información básica. Los siguientes campos y listas desplegables son obligatorios:

   1. Información básica

      1. Nombre
      1. Apellidos
      1. Fecha de nacimiento
      1. Correo electrónico

1. Utilice la siguiente **lógica dinámica** para mostrar la función dinámica utilizando la lista desplegable **Situación familiar**:

   1. **Soltero**: mostrar el panel Familiares.
   1. **Casado**: mostrar el panel matrimonial dependiente
   1. **Divorciado**: mostrar el panel Familiares.
   1. **Viudo**: mostrar el panel Familiares.
   1. **¿Tiene hijos?**: botón de opción (Sí/No) para mostrar el panel secundario dependiente.

      1. Botón (Agregar/quitar) para agregar/quitar varios paneles secundarios dependientes.

1. Haga clic en la flecha derecha de la barra de menús gris.
1. Haga clic en el botón Guardar de la parte inferior.

   ![Detalles del formulario adaptable](/help/forms/using/assets/adaptive_form.png)

## Demostración de escritorio {#desktop-demo}

**Esta sección:** una vez en casa, Aya encuentra la información que necesitaba y continúa rellenando la solicitud desde su equipo de escritorio. Aya va al portal en línea de Forms para reanudar la solicitud. Mediante una sencilla personalización, las agencias también pueden generar un vínculo y enviarlo por correo electrónico automáticamente para continuar rellenando la solicitud.

### Formulario adaptable continuo (Aya) {#aya-user-story-continued-adaptive-form}

**Instrucciones para el usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. En la barra de navegación, seleccione **Servicios en línea**.
1. En el panel &quot;Borradores de formularios&quot;, seleccione la &quot;Solicitud de prestación sanitaria&quot; existente.

   ![Solicitud de prestación sanitaria](/help/forms/using/assets/enrollment_application.png)

   El aspecto es el mismo y no necesita volver a introducir ningún dato.

   **Instrucciones para el usuario:**

1. Haga clic con el botón derecho en Circle CTA para pasar a la siguiente sección.

   ![CTA en forma de círculo de la derecha](/help/forms/using/assets/right_circle_cta_new.png)

   El formulario se rellena hasta la última entrada de Aya. Aya ha introducido todos sus datos y está lista para enviar el formulario.

   ![Enviar el formulario adaptable](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Cuando Aya rellena el campo del número de teléfono, debe hacerlo con un número continuo de 11 dígitos sin rayas, espacios ni guiones.

   Después de enviar, Aya recibe una página de agradecimiento. De forma opcional, Aya también recibe un correo electrónico que puede abrir para firmar electrónicamente el documento de registro con Adobe Sign.

### Opcional: Adobe Sign (Aya) {#adobe-sign}

**Instrucciones para el usuario:**

1. Vaya a su cliente de correo electrónico y busque el correo electrónico de Adobe Sign.
1. Haga clic en el vínculo a Adobe Sign.

   ![Vínculo de Adobe Sign](/help/forms/using/assets/adobe_sign_link.png)

**Instrucciones para el usuario:**

1. Marque **Acepto**.
1. Haga clic en **Aceptar**.
1. Desplácese hasta la parte inferior del documento revisado.
1. Haga clic en la pestaña amarilla resaltada para firmar el documento.

   ![Firmar el documento](/help/forms/using/assets/sign_document_new.png) ![Firmar el documento de prueba](/help/forms/using/assets/sign_test_document.png)

## Funcionario público (George) {#government-agent-george}

![Funcionario público George](/help/forms/using/assets/george_lang-1.png)

**Esta sección:** George es un analista empresarial de la agencia pública en la que Aya ha solicitado la prestación. George tiene un solo panel de control desde el que puede ver todas las solicitudes de prestaciones que se le han asignado para su revisión.

### Bandeja de entrada de AEM (George) {#george-user-story-aem-inbox}

**Instrucciones para el usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú **Cerrar sesión** o **Suplantar como** si ha iniciado sesión con un usuario administrativo.

   1. Inicie sesión con:

      1. **Usuario:** george.lang
      1. **Contraseña:** password

   1. O Suplantar:

      1. Escriba `George` en el campo **Suplantar como**.

      1. Haga clic en Aceptar para suplantar a George.

1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en **Ver todo** para desplazarse a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la tarea **Revisión de solicitudes de prestaciones sanitarias** más reciente.

   ![Revisión de solicitudes de prestaciones sanitarias](/help/forms/using/assets/health_benefits.png)

### Opcional: Bandeja de entrada de AEM y MS® Dynamics (George) {#george-user-story-aem-inbox-and-ms-dynamics}

Gracias a las integraciones de datos y a los flujos de trabajo automatizados, la solicitud de Aya aparece junto con un registro CRM que se ha generado automáticamente al enviar los datos.

**Instrucciones para el usuario:**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en **Abrir MS® Dynamics** para abrir el registro de MS® Dynamics en una nueva ventana.
1. En CRM, verá toda la información que se puede actualizar.

   1. Si lo desea, también puede agregar algunas notas de revisión directamente en Dynamics.

1. Cierre y vuelva a la Bandeja de entrada de AEM.

   ![Registro de MS Dynamics](/help/forms/using/assets/ms_dynamics.png)

### Vuelva a la Bandeja de entrada de AEM (George) {#george-user-story-back-to-aem-inbox}

George aprueba la solicitud de Aya, y gracias a un flujo de trabajo automatizado existente, también se le envía un correo electrónico de confirmación.

**Instrucciones para el usuario:**

1. Vaya a la esquina superior izquierda y haga clic en **Aprobar** para aprobar la solicitud.
1. En el modal, puede dejar un mensaje para la directora de CX.
1. Haga clic en Listo.
1. (Función Ciudadano) Abra su cliente de correo electrónico para ver el correo electrónico enviado a Aya.

   ![Ver el correo electrónico enviado a Aya](/help/forms/using/assets/email_client.png)

## Directora de CX (Camila) {#cx-lead-camila}

![Camila (directora de CX)](/help/forms/using/assets/camila_santos-1.png)

**Esta sección:** Camila, la directora de CX, configura una llamada telefónica de bienvenida con Aya para explicarle cómo usar los servicios gubernamentales para los que está aprobada.

### (Opcional) Bandeja de entrada de AEM y MS® Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**Instrucciones para el usuario:**

1. Vaya a *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. Haga clic en el icono de usuario (esquina superior derecha) y utilice la opción de menú **Cerrar sesión** o **Suplantar como** si ha iniciado sesión con un usuario administrativo.

   1. Inicie sesión con:

      1. **Usuario**: camila.santos
      1. **Contraseña**: password

   1. O Suplantar:

      1. Escriba `Camila` en el campo **Suplantar como**.

      1. Haga clic en Aceptar para suplantar a George.

1. En la esquina superior derecha, haga clic en el icono Notificación (campana).
1. Haga clic en **Ver todo** para desplazarse a la Bandeja de entrada.
1. En la Bandeja de entrada, abra la tarea **Nueva aprobación de contacto** más reciente.

![Nueva aprobación de contacto](/help/forms/using/assets/new_contact_approval.png)

**Instrucciones para el usuario (Opcional):**

1. Abra e inspeccione el formulario adaptable de solo lectura.
1. Haga clic en **Abrir MS® Dynamics** para abrir el registro de MS® Dynamics en una nueva ventana.
1. En CRM puede ver toda la información que se puede actualizar.

   1. De forma opcional, agregue una actividad de llamada directamente en Dynamics.
   1. Abra la sección **Actividades**.
   1. Haz clic en **Nueva llamada de teléfono**.
   1. Agregue los datos de la llamada telefónica.
   1. Guarde su trabajo y cierre la ventana.

1. Cuando vuelva a AEM, vaya a la esquina superior izquierda y haga clic en **Enviar** para enviar la solicitud.
1. En el modal, puede dejar un mensaje.
1. Haga clic en Listo.

   ![Pestaña Actividades](/help/forms/using/assets/activities_tab.png) ![Confirmar nuevo contacto](/help/forms/using/assets/confirm_new_contact.png)

## (Opcional) Kit de bienvenida para el ciudadano (Aya) {#welcome-kit-citizen-aya}

**Esta sección:** Aya recibe un correo electrónico que contiene un vínculo a una comunicación interactiva con un resumen de su prestación y varios campos de formulario para rellenar. Con el documento PDF de la prestación adjunto y el vínculo a la carta de la comunicación interactiva en el correo (con el mismo tema/marca que la comunicación interactiva).

### Notificación del cliente de correo electrónico (Aya) {#aya-user-story-email-client}

**Instrucciones para el usuario:**

1. Busque y abra el correo electrónico del kit de bienvenida.
1. Desplácese hasta el archivo adjunto del PDF en la parte inferior de la página.
1. Haga clic en el archivo adjunto del PDF para abrirlo.
1. Desplácese hacia arriba en su cliente de correo electrónico y haga clic en **Ver kit de bienvenida en línea**.

   1. Se abre la versión del canal Web del mismo documento.

1. Para obtener una referencia rápida al PDF directamente:

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. Para obtener la referencia rápida al IC directamente:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![Manual de bienvenida para prestaciones](/help/forms/using/assets/welcome_benefits_handbook.png) ![Vínculo de la comunicación interactiva](/help/forms/using/assets/interactive_communication.png)

## Nuevo recordatorio para el ciudadano (Aya) {#renewal-reminder-citizen-aya}

**Esta sección:** Camila también programa una comunicación de recordatorio un año después. (Paso del flujo de trabajo que automatiza/ejecuta y el correo electrónico).

### Notificación del cliente de correo electrónico (Aya) {#aya-user-story-email-client-updated}

**Instrucciones para el usuario:**

1. Vaya a su cliente de correo electrónico.
1. Busque y abra el correo electrónico del recordatorio de renovación.
1. Haga clic en **Enviar una nueva solicitud** para poder abrir el formulario adaptable.

   1. Esta sección se deja vacía intencionadamente para admitir el relleno previo de datos en la fase 2.

   ![Correo electrónico del recordatorio de renovación](/help/forms/using/assets/renewal_reminder_email.png)

## (Opcional) Modelo de datos de formulario (Camila) {#form-data-model}

**Esta sección**: Camila va a Integraciones de datos de AEM Forms, donde puede realizar una prueba rápida para comprobar si realmente se ha incluido la información enviada a la fuente de datos externa mediante la integración del modelo de datos de formulario.

### Modelo de datos de Formulario (Camila) {#form-data-model-camila}

**Esta sección**: Camila va a la página Fuentes de datos para validar los datos que el servidor ha replicado en la base de datos de Derby.

1. Una vez que la experiencia del usuario y el envío del usuario se hayan completado, Camila va a la pestaña Fuentes de datos en AEM Forms (**Forms** > **Integraciones de datos**)

1. A continuación, Camila selecciona AEM Forms We.gov FDM y, a continuación, edita el **We.gov FDM de inscripción**.

1. Después, Camila selecciona el **Contacto** > **Servicio de lectura** que va a probar.

   ![Servicio de lectura de contactos](assets/aftia-contact-read-service.jpg)

1. A continuación, proporciona al servicio de prueba un id de contacto y hace clic en **Probar**. Por ejemplo, 1 o 2, si envió el formulario. Si no ha enviado el formulario, no se devuelve ningún dato.

   ![Servicio de lectura de contactos](assets/aftia-test-service.jpg)

1. A continuación, Camila puede validar que los datos se han insertado correctamente en la fuente de datos.

   * Los datos de Derby DS tienen un formato similar al siguiente:

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (Opcional) Analytics (Camila) {#analytics-cx-lead-camila}

**Esta sección:** Camila va a un panel donde puede ver los KPI de la agencia, como el % de ciudadanos que empiezan a rellenar un formulario de solicitud de prestación y lo abandonan, el tiempo promedio desde la presentación de la solicitud hasta la respuesta de aprobación/denegación y las estadísticas de participación de los manuales de prestaciones que ha enviado a los ciudadanos.

### Informes de sitios de Adobe Analytics (Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. Vaya a *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Seleccione **Sitio de We.Gov de AEM Forms** para ver las páginas del sitio.
1. Seleccione una de las páginas del sitio (por ejemplo, Inicio) y elija **Analytics &amp; Recommendations**.

   ![Analytics and Recommendations](/help/forms/using/assets/analytics_recommendation.jpg)

1. En esta página, verá información recuperada de Adobe Analytics que pertenece a la página de AEM Sites (NOTA: Por diseño, esta información se actualiza periódicamente desde Adobe Analytics y no se muestra en tiempo real).

   ![Métricas clave de Adobe Analytics](/help/forms/using/assets/analytics_key_metrics.jpg)

1. Cuando vuelva a la página de la vista de página (a la que se accede en el paso 3), también podrá ver la información de la vista de página cambiando la configuración de visualización para ver los elementos en **Vista de lista**.
1. Busque el menú desplegable **Vista** y seleccione **Vista de lista**.

   ![La vista de lista del menú desplegable Vista](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. En el mismo menú, seleccione **Configuración de vista** y las columnas que desee mostrar en la sección **Analytics**.

   ![Configuración de la visualización de las columnas](/help/forms/using/assets/view_setting_analytics.jpg)

1. Haga clic en **Actualizar** para que las columnas nuevas estén disponibles.

   ![Haga que las columnas nuevas estén disponibles](/help/forms/using/assets/new_columns_available.jpg)

### Informes de formularios de Adobe Analytics (Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. Vaya a

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*.

1. Seleccione el formulario adaptable **Solicitud de prestación sanitaria** y luego seleccione la opción **Informe de Analytics**.

   ![Solicitud de prestación sanitaria](/help/forms/using/assets/analytics_report_benefits.jpg)

1. Espere a que se cargue la página y vea los datos del informe de Analytics.

   ![Datos del informe de Analytics](/help/forms/using/assets/analytics_report_data_updated.jpg)
