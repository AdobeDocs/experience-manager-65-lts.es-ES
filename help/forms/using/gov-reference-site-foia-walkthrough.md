---
title: Tutorial del sitio de referencia de We.Gov para el cumplimiento de la ley FOIA
description: Consulte el tutorial del sitio de referencia de We.Gov para comprender cómo AEM Forms ayuda a los gobiernos a recibir y proporcionar la información solicitada por individuos en virtud de la Ley de Libertad de Información (FOIA).
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 56%

---

# Tutorial del sitio de referencia de We.Gov para el cumplimiento de la ley FOIA {#we-gov-reference-site-foia-walkthrough}

## Escenario del sitio de referencia para el cumplimiento de la Ley de Libertad de Información {#reference-site-freedom-of-information-act-scenario}

We.Gov es una organización estatal que permite a los padres adoptivos inscribirse para recibir una pensión alimenticia si adoptan a un niño. We.Gov también permite a los padres solicitar información de los siguientes departamentos gubernamentales en virtud de la Ley de Libertad de Información:

* Agencia de Logística de Defensa
* Oficina del Inspector General del Departamento de Defensa
* Oficina de Políticas de Información del Departamento de Justicia
* Departamento de la Marina
* Agencia de Protección Medioambiental

Para obtener más información sobre la Ley de Libertad de Información, consulte [https://www.foia.gov/](https://www.foia.gov/index-es.html).

El escenario incluye las siguientes personas:

* Sarah Rose, la persona que solicita información en virtud de la ley;
* John Jacobs, la persona que gestiona la solicitud y la reenvía al departamento correspondiente;
* Gloria Ríos, la funcionaria del gobierno que facilita la información según la solicitud.

## Sarah inicia la solicitud de información en virtud de la ley FOIA. {#sarah-initiates-request-for-information-under-foia}

En virtud de la Ley de Libertad de Información, Sarah solicita una copia de los registros de los casos atendidos por la Administración para Niños y Familias durante los ejercicios de 2013 a 2016. Sarah presenta esta solicitud en la Oficina de Políticas de Información del Departamento de Justicia, y también indica que está dispuesta a pagar un máximo de 100 dólares en concepto de gastos de impresión y envío.

### Funcionamiento {#how-it-works}

### Puede verlo usted mismo {#see-it-yourself}

En el explorador, abra `https://<hostname>:<PublishPort>/wegov`. En el sitio de We.Gov, seleccione Solicitudes > Todas las solicitudes. En la página Todas las Solicitudes, seleccione Solicitar en Solicitud FOIA.

## Sarah comienza su solicitud de información en virtud de la ley FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah hace clic en **Solicitar**. En la página del formulario de solicitud de la Ley de Libertad de Información, introduce, entre otra, la siguiente información:

* **Organismo:** Sarah especifica que el organismo al que ha dirigido la solicitud es la Oficina de Políticas de Información del Departamento de Justicia.

* **Pagará hasta**: Sarah especifica que está preparada para pagar hasta 100 dólares en concepto de gastos de impresión y envío.
* **Describir la solicitud en detalle**: Sarah especifica &quot;Solicitud de una copia de los registros de los casos atendidos por la Administración para Niños y Familias durante los ejercicios fiscales de 2013 a 2016&quot;.

![Solicitud de una copia de los registros de los casos atendidos por la Administración para Niños y Familias durante los ejercicios fiscales de 2013 a 2016](assets/sarahfiosform.png)

Solicitud de una copia de los registros de los casos atendidos por la Administración para Niños y Familias durante los ejercicios fiscales de 2013 a 2016

En cualquier momento, Sarah puede seleccionar **Guardar** para guardar un borrador del formulario y volver más tarde para rellenarlo y enviarlo. Sarah envía el formulario.

>[!NOTE]
>
>El flujo de trabajo de reanudación por correo electrónico funciona únicamente con usuarios que han iniciado sesión. Asegúrese de añadir el usuario Sarah Rose en el escenario del sitio de referencia. Las credenciales de inicio de sesión de Sarah son `srose/password`.

## John Jacobs recibe y aprueba la solicitud. {#john-jacobs-receives-and-approves-the-application}

John Jacobs recibe la solicitud y la redirige a la persona adecuada. La bandeja de entrada AEM permite a John ver todas las solicitudes enviadas desde un mismo sitio.

### Funcionamiento {#how-it-works-1}

Cuando Sarah rellena y envía la solicitud FOIA, se envía un registro de la solicitud a la bandeja de entrada de John Jacobs. John Jacobs puede consultar la solicitud presentada y aceptarla o rechazarla.

### Puede verlo usted mismo {#see-it-yourself-1}

Puede obtener acceso a la Bandeja de entrada de AEM en https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la Bandeja de entrada AEM utilizando jjacobs/password como el nombre de usuario/contraseña de John Jacobs y vea la solicitud FOIA. Para obtener información sobre el uso de la Bandeja de entrada AEM para tareas de flujo de trabajo centradas en Forms, consulte [Administrar aplicaciones y tareas de Forms en Bandeja de entrada AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs puede ver, aprobar o rechazar la solicitud desde el panel de solicitudes. John Jacobs selecciona y abre los detalles de la solicitud y, después de revisarla, la aprueba.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah recibe un correo electrónico de confirmación</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Una vez que John Jacobs aprueba la solicitud, Sarah recibe un correo electrónico de confirmación del sitio de We.Gov. Sarah recibe información sobre las tarifas y el tiempo necesario para procesar su solicitud. El correo electrónico también incluye datos de correo electrónico y teléfono con los que Sarah puede ponerse en contacto para recibir actualizaciones sobre su solicitud.

![correo_electrónico_Sarah_Rose](assets/sarahroseemail.png)

## Gloria recibe la solicitud FOIA de aprobación de segundo nivel {#gloria-receives-the-foia-request-for-second-level-approval}

Una vez que John Jacobs rellena la información requerida y aprueba la solicitud de Sarah, esta pasa a Gloria Ríos para su aprobación final. Gloria revisa el documento de registro adjunto y aprueba la solicitud.

![bandeja_entrada_Gloria_Ríos](assets/gloriariosinbox.png)

### Funcionamiento {#how-it-works-2}

Cuando John Jacobs aprueba la solicitud FOIA, se crea un PDF o un documento de registro de la solicitud y se envía a la bandeja de entrada de Gloria Ríos. Gloria puede ver la solicitud enviada y aprobarla o rechazarla.

### Véalo usted mismo {#see-for-yourself}

Puede obtener acceso a la Bandeja de entrada de AEM en https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Inicie sesión en la Bandeja de entrada de AEM utilizando grios/password como el nombre de usuario/contraseña de Gloria Ríos y vea la solicitud FOIA.

Gloria abre la solicitud y examina los detalles de la solicitud FOIA. Después de revisar los detalles de la solicitud y estudiar la viabilidad de proporcionar los documentos requeridos, Gloria aprueba la solicitud.

![aprobación_Gloria_Ríos](assets/gloriariosapproves.png)

## Sarah recibe la notificación de que su solicitud ha sido aprobada {#sarah-receives-notification-that-her-request-is-approved}

Una vez que Gloria aprueba la solicitud FOIA, Sarah recibe un correo electrónico notificándole que su solicitud ha sido aprobada. El correo electrónico también incluye información sobre los plazos provisionales en los que se entregará el documento y los datos de contacto para el seguimiento de la solicitud.

![correo_aprobación_Sarah_Rose](assets/sarahroseemailapproval.png)
