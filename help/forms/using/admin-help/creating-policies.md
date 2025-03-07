---
title: Crear y administrar directivas
description: Una directiva es un conjunto de configuraciones de confidencialidad y usuarios que pueden acceder a un documento al que se aplica. Puede crear y administrar varios tipos de directivas mediante formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e8faf76e-5287-4b0c-b440-f348443287f3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 0%

---

# Crear y administrar directivas {#creating-and-managing-policies}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Una *directiva* define un conjunto de configuraciones de confidencialidad y usuarios que pueden tener acceso a un documento al que se aplica la directiva. Se usa un *conjunto de directivas* para agrupar un conjunto de directivas que tienen un propósito comercial común. Estos conjuntos de directivas se ponen a disposición de un subconjunto de usuarios del sistema. Para obtener detalles acerca de las directivas, vea [Directivas y documentos protegidos por directivas](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipos de directivas {#types-of-policies}

La seguridad de los documentos proporciona los siguientes tipos de directivas.

**Políticas personales**

Los usuarios pueden crear, editar, copiar, eliminar y aplicar sus propias directivas con la configuración adecuada para una situación concreta. Solo la persona que crea una directiva y el administrador pueden acceder a esa directiva personal. Las directivas personales aparecen en la ficha Mis directivas de la página Directivas.

Los usuarios invitados también pueden crear, editar, copiar y eliminar directivas personales si el administrador habilita esta capacidad.

**Directivas compartidas**

Los administradores y coordinadores de conjuntos de directivas crean directivas compartidas basadas en los requisitos de confidencialidad que su organización identifica para distintos tipos de documentos y usuarios. Las directivas compartidas se incluyen en los conjuntos de directivas y están disponibles para todos los usuarios autorizados (editores de documentos, coordinadores de conjuntos de directivas y destinatarios de documentos) de un conjunto de directivas concreto. Los administradores y coordinadores de conjuntos de directivas pueden habilitar y deshabilitar directivas compartidas. Las directivas compartidas aparecen en los conjuntos de directivas de la ficha Conjuntos de directivas de la página Directivas.

Cuando instala Document Security por primera vez, contiene una directiva compartida, denominada *Restringir a todas las identidades*. Cuando esta directiva se aplica a un documento, cualquier usuario que pueda iniciar sesión en Document Security puede acceder al documento. Esta directiva se encuentra en el conjunto de directivas denominado *Conjunto de directivas globales*. De forma predeterminada, esta directiva no está habilitada. Puede habilitarlo si se adapta a las necesidades de su organización.

**Directivas generadas automáticamente por Microsoft® Outlook**

Con Acrobat, puede aplicar directivas a documentos que envíe como datos adjuntos de correo electrónico en Microsoft® Outlook. En Outlook, puede proteger un documento utilizando una directiva existente. O bien, puede utilizar una directiva generada automáticamente y que Acrobat genera con la configuración de confidencialidad predeterminada y se aplica al documento adjunto a un mensaje de correo electrónico. (Consulte *[Ayuda de Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Para que una directiva esté disponible en Outlook, debe establecerla como favorita en Acrobat. Todas las demás directivas, incluidas las del editor, no se muestran en Outlook.

## Quién puede crear y administrar directivas y conjuntos de directivas {#who-can-create-and-manage-policies-and-policy-sets}

La forma en que interactúa con las directivas y los conjuntos de directivas depende de la función que tenga dentro de la organización:

**Usuarios:** Los usuarios pueden crear, editar y eliminar sus directivas personales. Los usuarios invitados también pueden crear directivas personales si el administrador habilita esta capacidad.

**Coordinadores de conjuntos de directivas:** Los coordinadores de conjuntos de directivas pueden crear y administrar directivas compartidas en los conjuntos de directivas en los que están designados como coordinadores. Un coordinador de conjunto de políticas suele ser un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas concreto.

**Administradores:** Los administradores pueden editar las directivas personales de cualquier usuario. Pueden crear directivas compartidas. También pueden crear, editar y eliminar conjuntos de directivas y designar coordinadores de conjuntos de directivas.

Para obtener más información sobre las distintas funciones de seguridad de documentos, consulte [Acerca de los usuarios de seguridad de documentos](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Crear y editar directivas {#creating-and-editing-policies}

Los usuarios pueden crear o editar directivas personales para su propio uso. Los administradores y coordinadores de conjuntos de directivas pueden crear o editar directivas compartidas para su organización.

### Consideraciones para editar directivas {#considerations-for-editing-policies}

Cuando edita una directiva, los cambios afectan a los documentos que la directiva protege actualmente y a los documentos que la directiva protege posteriormente. Por ejemplo, si elimina destinatarios de una directiva aplicada a un documento, los destinatarios ya no podrán abrir el documento.

El estado del documento determina cuándo se aplica el cambio:

* Si el documento está en línea, los cambios se aplican inmediatamente a menos que el usuario tenga el documento abierto. En este caso, el usuario debe cerrar el documento para que los cambios surtan efecto.
* Si un destinatario utiliza el documento sin conexión (por ejemplo, en un equipo portátil), los cambios surtirán efecto la próxima vez que el destinatario ponga el documento en línea. A continuación, se sincroniza con Document Security abriendo cualquier documento protegido por directivas.

>[!NOTE]
>
>Las directivas que Acrobat genera automáticamente para los destinatarios de documentos adjuntos a mensajes de correo electrónico en Microsoft® Outlook no aparecen en la lista de directivas. Sólo puede ver estas directivas si abre la página Detalle del documento para el documento asociado.

Al editar directivas, se aplican estas restricciones:

* Los usuarios invitados solo pueden editar directivas si el administrador habilita esta capacidad. Si no puede editar directivas, la opción Editar no está disponible.
* Los coordinadores de conjuntos de directivas solo pueden editar directivas dentro de conjuntos de directivas si tienen los permisos correctos. El superusuario o el administrador de conjuntos de directivas establece estos permisos en la interfaz de administrador de Document Security.
* Si la directiva tiene una marca de agua configurada que el administrador eliminó desde que se creó la directiva, esta marca de agua ya no se aplicará a los documentos si edita y guarda la directiva. Las marcas de agua eliminadas permanecen en vigor únicamente para las directivas existentes siempre que no edite la directiva. Si edita la directiva, debe seleccionar otra marca de agua para reemplazar la eliminada.
* No se puede conceder acceso anónimo a un documento editando la directiva aplicada. Si edita la directiva, los usuarios deben iniciar sesión para acceder al documento. Para aplicar el acceso anónimo a este documento, primero quite la directiva en la aplicación cliente y, a continuación, aplique otra directiva que permita el acceso anónimo.
* Las directivas que Acrobat genera automáticamente para los destinatarios de un documento adjunto a un mensaje de correo electrónico en Microsoft Outlook no aparecen en la lista de directivas. Para tener acceso a esta directiva, busque el documento en la página Documentos, abra la página Detalle del documento y haga clic en el nombre de la directiva en la lista de detalles del documento.

**Crear o editar una directiva**

1. En la página Document Security, haga clic en Directivas y, a continuación, en una de estas fichas:

   * Para crear o editar una directiva personal, haga clic en la pestaña Mi directiva.
   * Para crear o editar una directiva compartida, si tiene permiso, haga clic en la ficha Conjuntos de directivas y en el nombre del conjunto de directivas correspondiente; a continuación, haga clic en la ficha Directivas.

1. Haga clic en Nuevo o seleccione la directiva que desee editar en la lista.
1. En el cuadro Nombre, escriba un nombre que identifique de forma exclusiva la directiva. En el cuadro Descripción, describa lo que hace la directiva y cuándo utilizarla. Si la directiva se encuentra dentro de un conjunto de directivas, el nombre y la descripción aparecen en la lista de directivas de todos los usuarios especificados. Las directivas personales solo están disponibles para el usuario y los administradores.

   No se pueden utilizar los siguientes caracteres en el nombre o la descripción:

   * signo menos que (&lt;)
   * signo de mayor que (>)
   * y comercial (&amp;)
   * comilla tipográfica simple (&#39;)
   * comillas dobles (&quot;)
   * barra invertida (\)
   * barra diagonal (/)

   Si utilizó el siguiente carácter en el nombre o la descripción, se convierten en espacios:

   * retorno de carro (carácter ASCII 13)
   * nueva línea (carácter ASCII 10).

   >[!NOTE]
   >
   >Puede crear un nombre de directiva que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea una directiva, se realiza una comparación para comprobar si existe una directiva con el mismo nombre. La comparación no puede distinguir entre nombres que son iguales excepto para caracteres acentuados. Se supone que la directiva ya se ha agregado a la base de datos y que la nueva no se ha agregado.

1. Agregue usuarios y grupos a la directiva y establezca los permisos adecuados. (Consulte [Usuarios y grupos](creating-policies.md#users-and-groups).)
1. En Configuración general, seleccione las opciones adecuadas. (Consulte [Configuración general](creating-policies.md#general-settings).)
1. (Opcional) Si procede, seleccione un proveedor de autorización externa y especifique sus propiedades. Si no desea utilizar un proveedor de autorización externo, haga clic en Quitar proveedor predeterminado.

   Se utiliza un proveedor de autorización externa para configurar propiedades dentro de la directiva y, cuando se selecciona, el proveedor de autorización externa utiliza esta información para evaluar la directiva. El administrador y la persona que instala el software configuran las propiedades disponibles.

1. En Configuración avanzada, seleccione las opciones adecuadas. (Consulte [Configuración avanzada](creating-policies.md#advanced-settings).)
1. En Configuración avanzada inmodificable, seleccione las opciones adecuadas. (Consulte [Configuración avanzada inmodificable](creating-policies.md#unchangeable-advanced-settings).)
1. Haga clic en Guardar. La directiva aparece en la lista de directivas. Aparece un icono con un círculo rojo junto a la nueva directiva, que indica que aún está deshabilitada.

   Para que la directiva esté disponible para los usuarios, actívela. (Consulte [Habilitar o deshabilitar directivas compartidas](creating-policies.md#enable-or-disable-shared-policies).)

### Usuarios y grupos {#users-and-groups}

En el área Usuarios y grupos, especifique los usuarios que tienen acceso a los documentos protegidos con la directiva. Para cada usuario o grupo que especifique, también debe establecer los privilegios de uso del documento.

>[!NOTE]
>
>El editor del documento es el usuario que protege el documento con la directiva. Este usuario siempre se incluye de forma predeterminada en una directiva, con derechos de acceso completos, incluidas las capacidades de revocación y cambio de directivas. Sin embargo, los administradores pueden cambiar los derechos de acceso del editor del documento para las directivas compartidas. Por ejemplo, el administrador puede restringir el acceso al documento o cambiar la directiva al editor del documento.

**Agregar usuario o grupo:** Para agregar un usuario o grupo de usuarios, haga clic en Agregar usuario o grupo y, a continuación, haga clic en Búsqueda avanzada para encontrar usuarios o grupos. Los usuarios incluyen a los usuarios internos de su organización y a los usuarios invitados que se han registrado en Document Security. Al seleccionar esta opción, aparecerá la página Agregar Usuario o Grupo:

* En el cuadro Buscar, escriba el nombre de usuario o de grupo o la dirección de correo electrónico.
* En la lista Utilizando, seleccione Nombre o Correo electrónico.
* En la lista Tipo, seleccione Usuario o Grupo.
* Seleccione el dominio que desea buscar en la lista En y haga clic en Buscar.
* Cuando se devuelvan los resultados, seleccione el usuario o grupo que desee añadir y haga clic en Add.

>[!NOTE]
>
>Si introduce un nombre de usuario o una dirección de correo electrónico invitados correctos y no se devuelve ningún resultado, es posible que el usuario no se haya registrado aún o que la cuenta se haya eliminado. Puede intentar agregar el usuario como tipo de usuario invitado o ponerse en contacto con el administrador.

**Invitar nuevo usuario:** Para agregar un usuario invitado, haga clic en Invitar nuevo usuario, escriba la dirección de correo electrónico del usuario en el cuadro que aparece y haga clic en Invitar. Esta opción solo está disponible si el administrador la ha activado. Cuando se agregan nuevos usuarios invitados a una directiva, Document Security envía un correo electrónico de invitación de registro si aún no se invita a los usuarios a registrarse. Los usuarios deben utilizar el vínculo del correo electrónico para crear una cuenta y, a continuación, deben activarla.

Después de registrarse, los usuarios invitados pueden utilizar los documentos protegidos por directivas para los que tienen autorización. Según las capacidades que habilite el administrador, los usuarios externos podrán tener permiso para aplicar directivas a documentos, crear, editar y eliminar directivas y agregar otros usuarios externos a directivas.

**Agregar usuario anónimo:** Para permitir el acceso de usuarios anónimos, haga clic en Agregar usuario anónimo. Esta opción solo está disponible si el administrador ha habilitado el acceso de usuario anónimo para Document Security. (Consulte Configuración del servidor de Document Security). Esta opción concede a todos acceso a los documentos protegidos por esta directiva, independientemente de si tienen una cuenta de Document Security. Si selecciona esta opción, no puede agregar otros tipos de usuarios a la directiva.

>[!NOTE]
>
>Para permitir el acceso anónimo a un documento protegido por una directiva que actualmente no lo tiene, quite la directiva existente y aplique una directiva que permita el acceso anónimo. Si cambia o cambia la directiva existente, los usuarios deben iniciar sesión para acceder al documento.

#### Especifique los permisos de documento para usuarios y grupos {#specify-the-document-permissions-for-users-and-groups}

Puede especificar permisos de documento para un usuario o grupo a la vez, o puede seleccionar varios usuarios y grupos de la lista y cambiar sus permisos mediante las opciones del área de encabezados de columna.

De forma predeterminada, todos los documentos protegidos por directivas tienen un permiso que permite a los usuarios abrirlos mientras están en línea.

La pestaña Permisos y opciones se muestra en Document Security.

Estos permisos de documento están disponibles en la pestaña Permisos. Puede aplicar estos permisos a archivos de PDF, PTC Pro/E y Microsoft Office.

**Imprimir:** permite al usuario imprimir un documento protegido por esta directiva. Para los archivos de Office y Pro/E, puede activar la casilla de verificación Imprimir para permitir la impresión o desactivarla para evitar la impresión. Si activa la casilla de verificación Mostrar permisos personalizados para PDF, puede seleccionar una de estas opciones:

**No permitido:** El usuario no tiene permiso para imprimir PDF.

**Permitido:** El usuario tiene permiso para imprimir el PDF.

**Baja resolución. Solamente:** El usuario tiene permiso para imprimir el PDF en baja resolución.

**Modificar:** Permite al usuario modificar un documento protegido con esta directiva. Para los archivos de Office y Pro/E, puede activar la casilla de verificación Modificar para permitir modificaciones o desactivarla para evitar modificaciones. Si activa la casilla de verificación Mostrar permisos personalizados para PDF, puede seleccionar una de estas opciones:

**No permitido:** El usuario no tiene permiso para modificar PDF.

**Cualquiera:** El usuario puede modificar el PDF.

**Colaborar:** El usuario puede colaborar con otros usuarios mediante las opciones de Colaborar de Adobe Acrobat. Este permiso permite al usuario copiar datos de formulario incluso si el permiso de copia no se proporciona explícitamente en la directiva.

**Modificar páginas:** El usuario tiene permiso para agregar y quitar páginas y editar contenido en PDF.

**Rellenar y firmar:** El usuario tiene permiso para rellenar campos de formulario en PDF y firmarlos.

**Copiar:** permite al usuario copiar texto de un documento protegido por esta directiva.

**Reader de pantalla:** Este permiso se muestra si activa la casilla de verificación Mostrar permisos personalizados para PDF. Cuando se selecciona esta opción, Adobe Acrobat tiene permiso para agregar etiquetas temporales al PDF para mejorar su legibilidad con un lector de pantalla.

Estos permisos de documento están disponibles en la ficha Opciones. Puede aplicar estos permisos a archivos de PDF, PTC Pro/E y Microsoft Office:

**Sin conexión:** permite al usuario ver un documento sin conexión protegido por esta directiva.

**Validez del permiso:** Los permisos de selección siempre son válidos o establezca un período de validez de permiso de documento. Si selecciona un periodo de validez, haga clic en el icono del calendario para seleccionar una fecha y utilice las flechas para especificar la hora en formato de 24 horas.

En el caso de las directivas compartidas, los administradores pueden deshabilitar los siguientes privilegios para el editor del documento (el usuario que aplica la directiva a un documento):

**Revocar:** permite que el editor del documento revoque los privilegios de acceso al documento.

**Conmutador:** Permite que el editor del documento cambie los privilegios de la directiva.

### Configuración general {#general-settings}

El área Configuración general contiene la siguiente configuración:

**Período de validez:** Período de tiempo durante el cual los destinatarios autorizados pueden obtener acceso al documento protegido por una directiva. Puede elegir entre estas opciones de periodo de validez:

**El documento no será válido después de:** Se puede obtener acceso al documento durante el número de días especificado a partir del momento en que se protegió el documento.

**El documento no será válido después de esta fecha:** El documento es válido desde la fecha en que se aplica la directiva al documento hasta la fecha de finalización especificada.

**Válido desde, hasta:** El documento es válido durante las fechas especificadas. Puede utilizar el calendario para seleccionar una fecha, cuando corresponda, haciendo clic en el icono de calendario.

**El documento siempre es válido:** El período de validez del documento no caduca.

>[!NOTE]
>
>Las fechas de validez se basan en la zona horaria del sistema de seguridad de documentos, no en la del equipo local.

**Auditoría:** Habilite o deshabilite la auditoría de los eventos asociados con un documento protegido por una directiva. Por ejemplo, Document Security puede registrar eventos como intentos de abrir un documento. Los eventos auditados aparecen en la lista de la página Eventos. Si no selecciona esta opción, Document Security no registra eventos para los documentos asociados a la directiva.

>[!NOTE]
>
>El administrador también debe habilitar la auditoría de servidores en la página Configuración de auditoría y privacidad para que funcione la función de auditoría.

**Seguimiento de uso extendido:** Habilite o deshabilite el seguimiento de uso extendido. La seguridad de los documentos admite el seguimiento de eventos de usuario asociados con varias operaciones realizadas en un archivo PDF. Se puede acceder al objeto de seguridad del documento mediante un JavaScript. Un clic en un botón, un archivo multimedia que se está reproduciendo o el guardado de un archivo son algunos ejemplos de eventos que se activan desde un PDF protegido por una directiva. Con el objeto Document Security, también puede recuperar información del usuario. El seguimiento de eventos puede habilitarse desde el servidor de Document Security a nivel global o de directiva.

**Período de concesión sin conexión automática:** El número máximo de días que el destinatario puede utilizar el documento sin conexión protegido por directivas (sin una conexión activa a Internet o a la red). Cuando caduca el período de concesión, el destinatario debe sincronizar de nuevo el documento para seguir utilizándolo.

### Proveedores de autorización externa {#external-authorization-providers}

Seleccione los proveedores de autenticación externos si ya ha configurado alguno. Se enumeran los proveedores disponibles.

### Configuración de autenticación {#authentication-settings}

Puede anular la configuración de autenticación configurada en el servidor y especificar las opciones de autenticación relevantes para esta directiva. Seleccione Anular configuración de autenticación global y, a continuación, las opciones de autenticación correspondientes a esta directiva. Están disponibles las siguientes opciones de autenticación:

**Permitir autenticación de contraseña de nombre de usuario:** Seleccione esta opción si desea habilitar las aplicaciones cliente para que utilicen la autenticación de nombre de usuario y contraseña al conectarse al servidor.

**Permitir autenticación Kerberos:** Seleccione esta opción si desea habilitar las aplicaciones cliente para que utilicen la autenticación Kerberos al conectarse al servidor.

**Permitir autenticación de certificado de cliente:** Seleccione esta opción si desea habilitar las aplicaciones cliente para que utilicen autenticación de certificado al conectarse al servidor.

**Permitir autenticación extendida** Seleccione para habilitar la autenticación extendida. Al seleccionar esta opción, las aplicaciones cliente pueden utilizar la autenticación extendida. La autenticación extendida proporciona procesos de autenticación personalizados y diferentes opciones de autenticación configuradas en el servidor de Document Security

Si va a anular la configuración de autenticación global, puede elegir las opciones de autenticación correspondientes a esta directiva. Por ejemplo, si ha habilitado tres opciones de autenticación (nombre de usuario y contraseña, certificado de cliente y autenticación extendida) en el servidor, puede anular esa configuración global y seleccionar sólo autenticación extendida para esta directiva. Asegúrese de que la opción de autenticación que selecciona aquí ya está configurada en el servidor. En este ejemplo, no puede seleccionar Kerberos como opción de autenticación porque no está configurado en el servidor.

>[!NOTE]
>
>La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

### Configuración avanzada {#advanced-settings}

El área Configuración avanzada contiene la siguiente configuración:

**Marca de agua dinámica:** Seleccione una marca de agua que se mostrará dinámicamente en las páginas de un documento (por ejemplo, cuando un destinatario imprima el documento). Las marcas de agua dinámicas identifican de forma exclusiva un documento, lo que contribuye a garantizar su confidencialidad y a evitar la infracción de los derechos de autor. Por ejemplo, el administrador puede configurar una marca de agua dinámica que muestre la fecha actual, el nombre de usuario o el identificador de la persona que utiliza el documento. O bien, el nombre de la directiva utilizada para proteger el documento. Una marca de agua también puede mostrar texto personalizado o elementos gráficos, si están configurados. Los administradores configuran las opciones de marca de agua, y los administradores y usuarios pueden aplicarlas a las directivas.

(Consulte [Configurar marcas de agua dinámicas](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Si está editando una directiva y el administrador eliminó una marca de agua configurada que seleccionó anteriormente para esta directiva, aparecerá una nota en la página Editar directiva. En este caso, si está guardando el documento editado, seleccione una nueva marca de agua si desea que aparezca en el documento.

>[!NOTE]
>
>En el caso de las directivas que proporcionan acceso de usuario anónimo, el nombre de usuario y el identificador de un usuario anónimo no se muestran como una marca de agua aunque seleccione este tipo de marca de agua.

**Usar solo complementos de Acrobat certificados para PDF:** Si se selecciona esta opción para una directiva, esta opción especifica que Acrobat 8.0 y posterior debe ejecutarse en modo certificado al abrir documentos protegidos con la directiva. Cuando Acrobat se ejecuta en modo certificado, no carga ningún complemento de terceros.

Seleccione esta opción si le preocupa que un destinatario de documento escriba un complemento que pueda eludir cualquiera de las protecciones de documentos de Acrobat 8.0 y posteriores. No seleccione esta opción si los destinatarios del documento deben utilizar complementos de terceros en Acrobat para interactuar con documentos.

Esta opción solo habilita el modo certificado en Acrobat 8.0 o posterior; el administrador debe deshabilitar el acceso para Acrobat 7.0.

(Consulte [Configurar el servidor de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)).

Esta opción no se aplica a Adobe Reader.

**Mensaje de error de acceso denegado:** Mensaje que aparece para cualquiera que intente abrir un documento protegido por una directiva sin permiso. Este mensaje aparece en Acrobat. Los clientes que no pueden mostrar este mensaje muestran un mensaje predeterminado para indicar que se ha denegado el acceso.

### Configuración avanzada inmodificable {#unchangeable-advanced-settings}

El área Configuración avanzada inmodificable contiene la siguiente configuración. No puede cambiar esta configuración después de guardar la directiva.

**Algoritmo de cifrado y longitud de clave:** Se usa para proteger los documentos. Puede elegir entre estas opciones:

* AES de 128 bits
* AES de 256 bits. Solo Acrobat 9.0 y versiones posteriores admiten esta opción. Para utilizar el cifrado AES 256 en archivos PDF, obtenga e instale los archivos de política de jurisdicción de fuerza ilimitada de la Extensión de criptografía de Java (JCE). Estos archivos reemplazan los archivos local_policy.jar y US_export_policy.jar en la carpeta [JAVE_HOME]/lib/security. Por ejemplo, si está utilizando Sun JDK 1.6, copie los archivos descargados en la carpeta [dep root]/Java/jdk1.6.0_26/lib/security. Puede descargar estos archivos desde [Descargas de Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Sin cifrado. Actualmente, Acrobat 9.0 y versiones posteriores admiten esta opción. Si selecciona esta opción, las opciones de Restricciones de documento estarán desactivadas. Esta opción puede resultar útil si desea utilizar Document Security para la auditoría de documentos o el control de versiones, pero no desea cifrar el documento.

**Restricciones de documentos:** Seleccione los componentes de documentos de PDF que desea cifrar. Otras aplicaciones cliente cifran todo el documento, pero no los archivos vinculados o incrustados. Puede elegir entre estas opciones:

* Todo el documento, incluidos los archivos adjuntos y metadatos. *Metadatos* es información sobre el documento y su contenido que puede ver a través del cuadro de diálogo Propiedades del documento o del menú Avanzado de Acrobat. En Acrobat, puede adjuntar archivos de diferentes tipos (por ejemplo, archivos de texto, audio y vídeo) a documentos de PDF.
* El documento y sus archivos adjuntos, pero no los metadatos.
* Sólo los documentos adjuntos. Puede cifrar los archivos adjuntos en un archivo PDF sin cifrar el contenido del documento.

## Habilitar o deshabilitar directivas compartidas {#enable-or-disable-shared-policies}

Para que una directiva compartida esté disponible, el administrador o el coordinador de conjuntos de directivas deben habilitarla. Puede habilitar nuevas directivas o directivas deshabilitadas anteriormente. Las directivas compartidas que deshabilite se seguirán aplicando a los documentos protegidos por ellas.

Aparece una X roja junto a una directiva deshabilitada.

>[!NOTE]
>
>Los administradores no pueden deshabilitar las directivas personales y los usuarios no pueden habilitar ni deshabilitar sus propias directivas.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en la ficha Conjuntos de directivas.
1. Haga clic en el nombre del conjunto de directivas correspondiente y haga clic en la ficha Directivas.
1. Seleccione la casilla de verificación situada junto a la directiva adecuada, haga clic en Habilitar o Deshabilitar y, a continuación, haga clic en Aceptar.

## Ver información sobre una directiva {#view-information-about-a-policy}

Mediante la ficha Mis directivas, puede buscar directivas personales.

Los conjuntos de directivas que crean los administradores se muestran en la ficha Conjuntos de directivas de la página Directivas. Contienen información sobre el conjunto de directivas, incluido su nombre, la fecha de creación y modificación, y una descripción. Haga clic en el nombre de un conjunto de directivas para ver sus detalles. Los coordinadores de conjuntos de directivas que tienen permiso para administrar directivas pueden crear directivas compartidas dentro de un conjunto de directivas concreto.

Al crear o editar una directiva, se muestra una página donde puede configurar el nombre de la directiva, los niveles de permisos, la configuración de confidencialidad y los destinatarios que se incluirán en ella.

El administrador puede configurar las siguientes opciones de confidencialidad para una directiva:

* Opciones generales de confidencialidad de documentos, como el período de validez del documento y el período de concesión sin conexión
* Los usuarios autorizados, así como las restricciones y privilegios de documentos para cada uno de ellos
* Opciones avanzadas de confidencialidad de documentos, incluidas marcas de agua dinámicas y cifrado de documentos

Los usuarios pueden ver las directivas que han creado y las directivas compartidas a las que tienen acceso. Los administradores pueden ver todas las directivas personales y compartidas que se encuentran en Document Security.

Puede ver información más detallada sobre una directiva que aparece en la lista, incluidos los usuarios o grupos que se incluyen en la directiva y la configuración de confidencialidad especificada para esos usuarios.

>[!NOTE]
>
>Las directivas que Acrobat genera automáticamente para los destinatarios de documentos adjuntos a mensajes de correo electrónico en Microsoft Outlook no aparecen en la lista de directivas. Sólo puede ver estas directivas si abre la página Detalle del documento para el documento asociado.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en la ficha Mis directivas.
1. Rellene la información de búsqueda para poder buscar directivas personales.
1. Seleccione la directiva adecuada en la lista.
1. En la página Detalles de la directiva, puede ver los detalles de la directiva, editarla o ver eventos relacionados con ella.

## Buscar directivas {#search-for-policies}

Los administradores pueden buscar directivas compartidas y directivas personales creadas por otros usuarios.

1. Para buscar una directiva compartida, haga clic en Directivas y, a continuación, haga clic en la ficha Conjuntos de directivas. Haga clic en un conjunto de directivas de la lista y, a continuación, haga clic en la ficha Directivas.

   Para buscar una directiva personal, en la página Document Security, haga clic en Directivas y, a continuación, en la ficha Mis directivas.

1. En la lista Buscar, seleccione una de estas opciones:

   **Id. de directiva:** Número de identificación de directiva que se genera cuando el usuario crea la directiva. Escriba el ID exacto de la directiva.

   **Nombre de directiva:** El nombre de la directiva. Puede buscar parte del nombre de la directiva o todo.

1. En el cuadro de texto, escriba el valor correspondiente. Por ejemplo, si ha seleccionado Nombre de directiva, escriba el nombre de directiva que está buscando.
1. En la lista Mostrar, seleccione el número de resultados que desea mostrar y, a continuación, haga clic en Buscar. Se muestran los resultados de la búsqueda.
1. (Opcional) Para ver los detalles de la directiva, haga clic en ella.

## Copiar una directiva {#copy-a-policy}

Puede copiar una directiva existente y guardarla con un nombre y una descripción nuevos. Copiar directivas es una forma eficaz de crear directivas utilizando la configuración existente.

Los usuarios externos solo pueden copiar directivas si el administrador habilita esta capacidad. Si no puede crear directivas, la opción Copiar no está disponible.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en la ficha Mi directiva.
1. Seleccione la directiva adecuada en la lista.
1. En la página Detalles de la directiva, haga clic en Copiar.
1. En el cuadro Nuevo nombre de directiva, escriba el nuevo nombre de directiva. De forma opcional, escriba una nueva descripción.

   No se pueden utilizar los siguientes caracteres en el nombre o la descripción:

   * signo menos que (&lt;)
   * signo de mayor que (>)
   * y comercial (&amp;)
   * comilla tipográfica simple (&#39;)
   * comillas dobles (&quot;)
   * barra invertida (\)
   * barra diagonal (/)

   Si utilizó el siguiente carácter en el nombre o la descripción, se convierten en espacios:

   * retorno de carro (carácter ASCII 13)
   * nueva línea (carácter ASCII 10).

   >[!NOTE]
   >
   >Puede crear un nombre de directiva que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea una directiva, se realiza una comparación para comprobar si existe una directiva con el mismo nombre. La comparación no puede distinguir entre nombres que son iguales excepto para caracteres acentuados. Se supone que la directiva ya se ha agregado a la base de datos y que la nueva no se ha agregado.

1. Haga clic en Aceptar.

## Eliminar una política {#delete-a-policy}

Puede eliminar las directivas que haya creado. Los administradores pueden eliminar las directivas que cualquier usuario haya creado. Los coordinadores de conjuntos de directivas pueden eliminar directivas en sus conjuntos de directivas. Las directivas que elimine se seguirán aplicando a los documentos protegidos por ellas. Puede eliminar varias directivas a la vez.

Los usuarios invitados solo pueden eliminar directivas si el administrador habilita esta capacidad. Si no puede eliminar directivas, la opción Eliminar no está disponible.

1. En la página Document Security, haga clic en Directivas.
1. Haga clic en la pestaña Mi directiva.
1. Para eliminar una directiva compartida, haga clic en la ficha Conjuntos de directivas y en el nombre del conjunto de directivas correspondiente.
1. Seleccione la casilla de verificación situada junto a la directiva adecuada, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

>[!NOTE]
>
>Utilice la aplicación cliente para quitar directivas de los documentos. (Consulte la Ayuda de Acrobat o la Ayuda de las extensiones de Acrobat Reader DC correspondientes).

## Ordenar la lista de directivas {#sort-the-policy-list}

Puede ordenar la lista de directivas por encabezados de columna para buscar directivas con mayor facilidad. Un icono de triángulo junto al encabezado de la columna indica qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica un orden ascendente, mientras que un triángulo que señala hacia abajo indica un orden descendente.

1. En la página Document Security, haga clic en Directivas y, a continuación, en la ficha Conjunto de directivas.
1. Seleccione un conjunto de directivas y, a continuación, haga clic en la ficha Directivas.
1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en la columna.
