---
title: Recorrido por el sitio de referencia de contratación de empleados
description: El sitio de referencia de AEM Forms muestra cómo las organizaciones pueden utilizar las funciones de AEM Forms para implementar el flujo de trabajo de contratación de empleados.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 90%

---

# Recorrido por el sitio de referencia de contratación de empleados {#employee-recruitment-reference-site-walkthrough}

## Información general {#overview}

We.Finance es una organización que permite a los candidatos solicitar el empleo a través del portal de referencia. La organización también utiliza el portal para administrar la programación de entrevistas, la lista de preseleccionados y la comunicación interna de los candidatos. El sitio administra lo siguiente:

* Los candidatos que buscan y solicitan trabajos
* La selección y preselección de candidatos
* El proceso de entrevistas
* La recopilación de detalles de los candidatos
* La comprobación del entorno del candidato
* El despliegue de ofertas para los candidatos seleccionados

>[!NOTE]
>
>Los casos de uso de contratación de empleados están disponibles en los sitios de referencia de We.Finance y We.Gov. Los ejemplos, imágenes y descripciones utilizados en los tutoriales utilizan el sitio de referencia We.Finance. Sin embargo, puede ejecutar estos casos de uso y revisar los artefactos también mediante We.Gov. Para ello, sustituya **we-finance** por **we-gov** en las URL mencionadas.

### Modelos de flujo de trabajo implicados {#workflow-models-involved}

El caso de uso de contratación de empleados implica dos flujos de trabajo:

* Antes de la entrevista: flujo de trabajo de contratación de empleados de We Finance
* Después de la entrevista: flujo de trabajo posterior a la entrevista de contratación de empleados de We Finance

Estos flujos de trabajo se crean en AEM y se pueden encontrar en las siguientes ubicaciones:

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### Flujo de trabajo de contratación de empleados de We Finance {#we-finance-employee-recruiting-workflow}

A continuación se muestra el modelo del flujo de trabajo de contratación de empleados de We Finance seguido en este documento.

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### Flujo de trabajo posterior a la entrevista de contratación de empleados de We Finance {#we-finance-employee-recruiting-post-interview-workflow}

A continuación, se muestra el modelo del flujo de trabajo de la contratación de empleados tras la entrevista de We Finance seguido en este documento.

![we-finance-employee-recruiting-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### Personas {#personas}

El escenario incluye las siguientes personas:

* Sarah Rose, la candidata que solicita un puesto en la organización
* John Jacobs, el reclutador
* Gloria Rios, la administradora de contrataciones
* John Doe, el trabajador de Recursos Humanos

## Sarah solicita un trabajo {#sarah-applies-for-a-job}

Sarah Rose busca una oportunidad de trabajo en la empresa. Visita su portal web y explora las ofertas de empleo enumeradas en la página Empleo. Encuentra una oferta de empleo que le interesa y la solicita.

![home-page](assets/home-page.png)

Página de inicio de We.Finance

![career-page](assets/career-page.png)

Página Empleos de We.Finance

Sarah hace clic en Solicitar en una publicación de trabajo. Se abre el formulario de solicitud de trabajo. Completa todos los detalles de la solicitud y la envía.

![job-application-form](assets/job-application-form.png)

### Funcionamiento {#how-it-works}

La página de inicio de We.Finance y la página Empleo son páginas de AEM Sites. La página Empleo incrusta un formulario adaptable, que utiliza un panel repetible para recuperar las ofertas de trabajo mediante un servicio y las enumera en la página. Puede revisar el formulario adaptable en `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### Puede verlo usted mismo {#see-it-yourself}

Vaya a `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` y haga clic en **[!UICONTROL Empleo]**. Haga clic en **[!UICONTROL Buscar]** para rellenar la lista de trabajos y, a continuación, haga clic en **[!UICONTROL Aplicar]** para un trabajo. Rellene los detalles del formulario y envíe la solicitud.

Asegúrese de especificar un correo electrónico válido en la solicitud, ya que cualquier comunicación a través de este tutorial se enviará al ID de correo electrónico especificado.

## John Jacobs selecciona el perfil de Sarah Rose como candidata para el administrador de contrataciones {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

La organización recibe la solicitud de empleo presentada por Sarah. A John Jacobs, el reclutador, se le asigna la tarea de revisar el perfil de Sarah. John revisa la tarea en su bandeja de entrada de AEM, encuentra el perfil que coincide con el requisito del trabajo y hace clic en Seleccionar. El perfil de Sarah se reenvía a Gloria Rios, la administradora de contrataciones, para su aprobación.

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

Bandeja de entrada de AEM de John

![candidate-shortlist](assets/candidate-shortlist.png)

John Jacobs selecciona el perfil de Sarah Rose como candidata para el administrador de contrataciones

**Funcionamiento**

La acción de envío del formulario de solicitud de empleo activa un flujo de trabajo que crea una tarea en la bandeja de entrada de John Jacobs para revisar la solicitud. Cuando John revisa y selecciona la solicitud, el flujo de trabajo crea una tarea en el administrador de contratación, la bandeja de entrada de Gloria.

### Puede verlo usted mismo {#see-it-yourself-1}

Vaya a `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`e inicie sesión mediante jjacobs/password como nombre de usuario/contraseña para John Jacobs. Abra la tarea Revisar perfil de candidato y seleccione el solicitante.

## Gloria revisa la solicitud y aprueba al solicitante para una entrevista {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

Gloria, la administradora de contratación, recibe el perfil preseleccionado como una tarea en su Bandeja de entrada de AEM. Lo revisa y aprueba a la candidata, Sarah Rose, para realizar una entrevista.

![gloriainbox](assets/gloriainbox.png)

Bandeja de entrada de AEM de Gloria

![gloriaschedulesinterview](assets/gloriaschedulesinterview.png)

Gloria aprueba a Sarah Rose para realizar una entrevista

**Funcionamiento**

Cuando Gloria aprueba al candidato para realizar una entrevista, el flujo de trabajo crea una tarea en la Bandeja de entrada de AEM de John Doe, que es el reclutador de We.Finance.

### Puede verlo usted mismo {#see-it-yourself-2}

Vaya a `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e inicie sesión con jjacobs/password como nombre de usuario/contraseña para John Jacobs. Abra la tarea Revisar perfil de candidato y seleccione el solicitante.

Vaya a `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` e inicie sesión con grios/password como nombre de usuario/contraseña para Gloria Rios. Abra la tarea Revisar perfil de candidato y haga clic en Programar entrevista.

## John Doe programa una entrevista {#john-doe-schedules-an-interview}

John Doe recibe la tarea de programar una entrevista en su bandeja de entrada. John Doe selecciona y abre la tarea y fija la fecha y hora de la entrevista, el lugar y la persona de RRHH responsable de la entrevista como John Jacob. John Doe hace clic en Enviar correo electrónico de invitación. Se envía un correo electrónico a Sarah y se asigna una tarea a Gloria, la administradora de contratación, para entrevistar a Sarah.

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

Bandeja de entrada de AEM de John Doe

![johndoescheduleinterview](assets/johndoescheduleinterview.png)

John Doe programa la entrevista y envía los detalles a Sarah Rose

## Sarah Rose recibe el correo electrónico con la programación de la entrevista {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose recibe el correo electrónico con la programación de la entrevista, el lugar de celebración y otros detalles. Sarah hace clic en Aceptar para indicar que está de acuerdo con el horario y el lugar de la entrevista. Según la información, Sarah llegará a las entrevistas.

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

Sarah Rose recibe el programa de entrevistas

## Después de las entrevistas, la administradora de contrataciones selecciona a Sarah Rose {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Después de que Sarah Rose revise las entrevistas y las borre, Gloria Rios, la administradora de contrataciones, abre la tarea de selección de candidatos desde su bandeja de entrada y hace clic en Seleccionar. La decisión de Gloria Rios se transmite al trabajador de Recursos Humanos, John Doe, para su posterior procesamiento.

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Bandeja de entrada de AEM de Gloria

![gloriariosselectcandidate](assets/gloriariosselectcandidate.png)

Gloria Rios selecciona a Sarah Rose después de las entrevistas

## John Doe solicita más información {#john-doe-requests-more-information}

Antes de pedir a un candidato que se una a la organización, se deben comprobar los antecedentes de Sarah. John Doe abre y revisa los detalles de la candidata seleccionada y ve que algunos de sus detalles de empleo y educación todavía no están completos. John Doe hace clic en Necesito más información.

![johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe solicita más información de Sarah Rose sobre su educación y experiencia laboral

## Sarah Rose recibe un correo electrónico en el que se le solicita más información {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose recibe un correo electrónico en el que se le notifica que se necesita más información para procesar su solicitud de empleo. El correo electrónico incluye un vínculo al formulario para rellenar la información necesaria.

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose recibe un correo electrónico en el que se notifica que se requiere más información para procesar su solicitud de empleo

Sarah hace clic en el vínculo Proporcionar detalles del correo electrónico. Aparece un formulario. Sarah rellena los detalles requeridos sobre su educación y empleo como lo solicitó John Doe y hace clic en Enviar.

![additionalinformation1](assets/additionalinformation1.png)

Sarah abre el formulario de información adicional al hacer clic en el vínculo del correo electrónico

![additionalinformation2](assets/additionalinformation2.png)

Sarah rellena la información adicional que ha solicitado John Doe y hace clic en Enviar

## John Doe revisa el perfil del candidato seleccionado para obtener información adicional {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe selecciona la solicitud de revisión de candidato y la abre. John Doe ve que Sarah ha rellenado toda la información según se le solicitaba. Después de revisar la solicitud, John Doe hace clic en Aprobar. Con la aprobación de John Doe, la solicitud para realizar una comprobación de antecedentes de Sarah Rose se reenvía a John Jacobs.

![johndoeadditionainformationinbox](assets/johndoeadditionainformationinbox.png)

Bandeja de entrada de AEM de John Doe

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe revisa la información adicional proporcionada por Sarah y la aprueba

## John Jacobs recibe una solicitud de comprobación de antecedentes {#john-jacobs-receives-a-background-check-request}

John Jacobs ve la solicitud de comprobación de antecedentes en su bandeja de entrada. John Jacobs abre la tarea y revisa la información proporcionada por Sarah Rose. Después de realizar una comprobación de los antecedentes, John Jacobs hace clic en Continuar para indicar que la comprobación de antecedentes se ha realizado correctamente.

![johnjacobsbackgroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

Bandeja de entrada de AEM de John Jacobs

![johnjacobsbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

Después de realizar la comprobación de antecedentes, John Jacobs hace clic en Continuar

## John Doe envía la carta de unión a Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe recibe una solicitud en su Bandeja de entrada de AEM para enviar la carta de unión. John abre la solicitud y ve los detalles. John Doe adjunta el PDF la carta de unión y, a continuación, hace clic en Adjuntar y enviar carta de unión.

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

Bandeja de entrada de AEM de John Doe

![johndoejoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe envía la carta de unión para que se firme

## Sarah Rose la recibe y la firma {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose recibe la carta de unión para firmarla. Sarah hace clic en Hacer clic aquí para revisar y firmar la carta de unión. El PDF de la carta de unión se abre con un campo para firmar el documento.

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose recibe la carta de unión para firmarla

Sarah puede elegir entre escribir, dibujar a mano, insertar una imagen de su firma o usar la pantalla táctil de su móvil para firmar. Sarah escribe su nombre, hace clic en Haga clic para firmar y descarga la copia firmada de la carta de unión.

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah escribe su nombre para firmar la carta de unión

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah hace clic en Hacer click aquí para firmar para completar la firma de la carta de unión
