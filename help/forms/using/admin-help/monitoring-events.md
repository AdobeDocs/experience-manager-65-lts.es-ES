---
title: Supervisar eventos
description: Cuando la capacidad de auditoría está habilitada, Document Security permite supervisar ciertos tipos de eventos. Puede buscar y ordenar fácilmente la lista de eventos mediante la seguridad de documentos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Supervisar eventos {#monitoring-events}

Cuando la capacidad de auditoría está habilitada, Document Security permite supervisar ciertos tipos de eventos. Los eventos que puede ver dependen de su función:

**Usuarios:** pueden ver eventos auditados para sus documentos protegidos por directivas y para cualquier documento protegido que reciban y utilicen.

**Coordinadores de conjuntos de directivas:** pueden ver eventos auditados, incluidos eventos de documentos y directivas, para documentos protegidos por directivas desde sus conjuntos de directivas.

**Administradores:** pueden ver eventos auditados relacionados con todos los documentos y usuarios protegidos por directivas. Los administradores también pueden realizar el seguimiento de otros tipos de eventos, como eventos de usuario, documento, directiva y sistema.

>[!NOTE]
>
>Los eventos que se realizan en una copia de un documento protegido por una directiva también se rastrean como eventos en el documento protegido original.

(Consulte [Opciones de auditoría de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Se registra un evento de error si un usuario no autorizado intenta ver un documento o intenta iniciar sesión con un nombre de usuario o una contraseña incorrectos.

>[!NOTE]
>
>Los eventos de acceso anónimo con errores para documentos se pueden registrar si se edita una directiva para quitar el acceso anónimo. Cuando un destinatario autorizado intenta acceder a un documento protegido por la directiva editada, se sigue intentando el acceso anónimo, pero no se consigue.

Si una directiva permite el acceso de usuarios anónimos pero el administrador desactiva posteriormente el acceso anónimo para la seguridad de los documentos, el acceso anónimo fallará para los documentos protegidos con la directiva y el evento no se registrará.

## Habilitar auditoría de eventos {#enable-event-auditing}

Estos requisitos de configuración deben cumplirse para que se realice la auditoría de eventos:

* El sistema o el administrador deben habilitar la capacidad de auditoría para el servidor.

  (Consulte [Configuración de auditoría de eventos y configuración de privacidad](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* La directiva que utilice para proteger el documento debe tener habilitada la auditoría. (Consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Búsqueda de un evento {#search-for-an-event}

Puede buscar en la lista de eventos y ver descripciones más detalladas sobre los eventos. Las descripciones detalladas incluyen información como el ID de evento, la descripción, la dirección IP, la organización, el usuario afectado, la fecha y la hora en que se produjo el evento, las actividades denegadas y los eventos sin conexión (cuando los usuarios intentan utilizar un documento cuando no están conectados a Document Security).

Puede buscar eventos en la página Eventos usando una combinación de criterios de búsqueda de eventos y las fechas en que se produjeron los eventos. Los eventos que puede buscar dependen de su función:

**Usuarios:** pueden ver eventos auditados para sus documentos protegidos por directivas y para cualquier documento protegido que reciban y utilicen. Estas opciones de búsqueda están disponibles:

**Eventos relacionados
para mí:** Los usuarios pueden encontrar eventos para cualquier documento protegido por directivas que hayan creado o recibido. Por ejemplo, si un usuario abre, visualiza o imprime un documento protegido por otra persona, solo verá estos eventos para ese documento.

**Eventos relacionados con mis documentos:** Los usuarios pueden encontrar todos los eventos relacionados con sus propios documentos protegidos por directivas. Los usuarios ven los eventos que generan todas las personas que administran sus documentos.

**Coordinadores de conjuntos de directivas:** pueden ver eventos auditados, incluidos eventos de documentos y directivas, para documentos protegidos por directivas desde sus conjuntos de directivas. Estas opciones están disponibles:

**Eventos de documento donde
Soy coordinador de conjuntos de directivas:** Los coordinadores de conjuntos de directivas que tienen el permiso de ver eventos pueden encontrar eventos relacionados con documentos que protegen las directivas de sus conjuntos de directivas.

**Eventos de directivas de los que soy coordinador de conjuntos de directivas:** Los coordinadores de conjuntos de directivas que tengan permiso para ver eventos pueden encontrar eventos relacionados con directivas en sus conjuntos de directivas.

**Administradores:** pueden ver eventos auditados relacionados con todos los documentos y usuarios protegidos por directivas. Los administradores también pueden realizar el seguimiento de otros tipos. Además, los administradores pueden subdividir aún más las búsquedas de eventos según el tipo de usuario:

**Usuarios conocidos:** Los usuarios se encuentran en los directorios de origen o están registrados como usuarios externos.

**Usuarios anónimos:** Usuarios desconocidos que tienen acceso a un documento protegido por una directiva que permite el acceso anónimo.

**Usuarios del sistema:** Eventos iniciados por el servidor, como una sincronización de directorios.

1. En la página Document Security, haga clic en Eventos.
1. En la lista Buscar, seleccione los criterios de búsqueda que desee utilizar. Según la selección realizada en la lista Buscar, se mostrará una segunda lista que proporciona criterios de búsqueda adicionales. Si procede, en el cuadro de texto, escriba los criterios de búsqueda.

   Para obtener más información acerca de los tipos de eventos específicos, vea [Opciones de auditoría de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. En la lista Usuario, seleccione el tipo de usuario que realizó el evento:

   * Si selecciona Usuario conocido, se muestra un segundo cuadro de búsqueda, en el que debe escribir el nombre de usuario o la dirección de correo electrónico del usuario.
   * Si no conoce estos valores, haga clic en el icono de búsqueda de la Libreta de direcciones para buscar el usuario por nombre de usuario o por dirección de correo electrónico.

1. En la lista Fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, aparecen cuadros donde escribe la fecha con el formato aaaa/mm/dd, o puede utilizar el Selector de fecha para especificar el intervalo de fecha:

   * Haga clic en el calendario para abrir el Selector de fecha.
   * Utilice las flechas para buscar un año y un mes.
   * Haga clic en un día del mes del calendario.
   * Haga clic en Aceptar para cerrar el Selector de fecha.

1. En la lista Mostrar, seleccione el número de resultados de búsqueda que desea mostrar por página.
1. Haga clic en Buscar.

   Todos los eventos fallidos se resaltan en la lista con un icono de denegado.

1. Para ver los detalles de un evento, haga clic en la descripción del evento en la lista.

## Ordenar la lista de eventos {#sort-the-event-list}

Puede ordenar la lista de eventos por encabezado de columna para buscar eventos más fácilmente. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica un orden ascendente, mientras que un triángulo que señala hacia abajo indica un orden descendente.

1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en el encabezado de la columna.
