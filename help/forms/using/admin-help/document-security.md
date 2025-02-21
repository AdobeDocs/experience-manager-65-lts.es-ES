---
title: ¿Qué es Document Security?
description: Descubra cómo puede crear, almacenar y aplicar configuraciones de confidencialidad predefinidas, y distribuir su información de forma segura mediante Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 887dc1d6d7e11672b62ef5ca5463ea6181ff0320
workflow-type: tm+mt
source-wordcount: '3219'
ht-degree: 4%

---

# Acerca de la seguridad de los documentos {#about-document-security}

La seguridad de los documentos garantiza que solo los usuarios autorizados puedan utilizar los documentos. Con Document Security, puede distribuir de forma segura cualquier tipo de información guardada en un formato compatible. Los formatos de archivo admitidos son:

* Archivos Adobe PDF
* Archivos de Microsoft® Word, Excel y PowerPoint

Para obtener más información acerca de cómo las directivas protegen los tipos de archivo admitidos, vea [más información de seguridad de documentos](https://experienceleague.adobe.com/docs/experience-manager-65-2025/forms/use-document-security/document-security-offerings.html?lang=en).

Con Document Security, puede crear, almacenar y aplicar fácilmente parámetros de confidencialidad predefinidos a sus documentos. Para evitar que la información se propague más allá de su alcance, también puede monitorizar y controlar cómo los destinatarios utilizan los documentos después de distribuirlos.

Puede proteger los documentos mediante políticas. Una *directiva* es una recopilación de información que incluye parámetros de confidencialidad y una lista de usuarios autorizados. La configuración de confidencialidad especificada en una política determina cómo puede un destinatario utilizar un documento al que se aplica la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editarlo o agregar firmas y comentarios a documentos protegidos.

Los usuarios de seguridad de los documentos crean directivas a través de las páginas web del usuario final. Los administradores utilizan las páginas web de Document Security para crear conjuntos de directivas que contienen directivas compartidas disponibles para todos los usuarios autorizados.

Aunque las directivas se almacenan en Document Security, las aplica a los documentos a través de la aplicación cliente. En *Ayuda de Acrobat* se describe detalladamente cómo aplicar directivas a documentos de PDF. La aplicación de directivas mediante otras aplicaciones, como Microsoft® Office, está documentada en la *Ayuda de extensiones de Acrobat Reader DC* para la aplicación.

Cuando aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. La configuración de confidencialidad también protege cualquier archivo (texto, audio o vídeo) de un documento de PDF. Puede distribuir los documentos protegidos por una política a los destinatarios autorizados por esta.

**Control de acceso a documentos y auditoría**

El uso de una directiva para proteger un documento le proporciona un control continuo sobre ese documento, incluso después de distribuirlo. Puede supervisar el documento, cambiar la directiva, impedir que los usuarios sigan teniendo acceso al documento y cambiar la directiva que se aplica al documento.

A través de la seguridad de los documentos, puede monitorizar los documentos protegidos por directivas y rastrear eventos, como cuando un usuario autorizado o no autorizado intenta abrir el documento.

**Componentes**

La seguridad de los documentos consta de un servidor y una interfaz de usuario:

**Servidor:** Componente central a través del cual Document Security realiza transacciones como autenticación de usuarios, administración en tiempo real de directivas y aplicación de confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

**Páginas web:** Interfaz en la que se crean directivas, se administran documentos protegidos por directivas y se supervisan los eventos asociados a documentos protegidos por directivas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para usuarios invitados y administrar cuentas de usuario invitadas.

![rm_psworkflow](assets/rm_psworkflow.png)

Los pasos de la ilustración son los siguientes:

1. El propietario del documento crea directivas utilizando las páginas web. Los propietarios de documentos pueden crear directivas personales a las que sólo pueden tener acceso. Los administradores y coordinadores de conjuntos de directivas pueden crear directivas compartidas en conjuntos de directivas a las que pueden acceder los usuarios autorizados.
1. El propietario del documento aplica la directiva y, a continuación, guarda y distribuye el documento. El documento se puede distribuir por correo electrónico, a través de una carpeta de red o en un sitio web.
1. El destinatario abre el documento en la aplicación cliente adecuada. El destinatario puede utilizar el documento según su directiva.
1. El propietario del documento, el coordinador del conjunto de directivas o el administrador pueden realizar un seguimiento de los documentos y modificar el acceso a ellos mediante las páginas web.

## Acerca de los usuarios de Document Security {#about-document-security-users}

Varios tipos de usuarios trabajan con Document Security para realizar diferentes tareas:

* El administrador del sistema u otra persona de sistemas de información (IS) instala y configura Document Security. Esta persona también puede ser responsable de configurar los ajustes globales del servidor, las páginas web, las políticas y los documentos.

  Esta configuración puede incluir, por ejemplo, una URL de seguridad de documentos base, notificaciones de auditoría y privacidad, avisos de registro de usuarios invitados y períodos de alquiler sin conexión predeterminados.

* Los administradores de Document Security crean directivas y conjuntos de directivas, y administran documentos protegidos por directivas para los usuarios según sea necesario. También crean cuentas de usuario invitadas y supervisan eventos del sistema, documento, usuario, directiva, conjunto de directivas y personalizados. También pueden ser responsables de configurar el servidor global y la página web y la configuración de directivas con un administrador del sistema.

  Los administradores pueden asignar a los usuarios las siguientes funciones en el área Administración de usuarios de la consola de administración. Los usuarios a los que se asignan estas funciones realizan sus tareas en el área de la interfaz de usuario de Document Security de la consola de administración.

  **Superadministrador de seguridad de documentos**

  Los usuarios con esta función tienen acceso a toda la configuración de seguridad de los documentos de la consola de administración. Estos permisos están asociados a la función:

   * Administrar configuración
   * Administrar directiva
   * Administrar conjuntos de directivas
   * Administración de documentos
   * Administrar editores de documentos
   * Administrar usuarios invitados y locales
   * Ver eventos
   * Delegar
   * Invitar a usuarios externos

  **Administrador de seguridad de documentos**

  Los usuarios con esta función pueden configurar el servidor de Document Security mediante la página Configuración en la sección Document Security de la consola de administración. Este permiso está asociado a la función Administrar configuración.

  >[!NOTE]
  >
  >Los usuarios con esta función también deben tener la función Usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada.

  **Administrador del conjunto de directivas de Document Security**

  Los usuarios con esta función pueden utilizar la sección Document Security de la consola de administración para editar las directivas de otros usuarios y crear, editar y eliminar conjuntos de directivas. Cuando un administrador de conjuntos de directivas crea un conjunto de directivas, puede asignarle un coordinador. Estos permisos están asociados a la función:

   * Administrar directiva
   * Administrar conjuntos de directivas
   * Administración de documentos
   * Administrar editores de documentos
   * Ver eventos
   * Delegar

  >[!NOTE]
  >
  >Los usuarios con esta función también deben tener la función Usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada.

  **Document Security administra usuarios invitados y locales**

  Los usuarios con esta función pueden realizar las tareas necesarias para administrar todos los usuarios invitados y locales en las páginas web de Document Security relevantes. Estos permisos están asociados a la función:

   * Administrar usuarios invitados y locales
   * Invitar a usuarios externos
   * Acceso a páginas web de usuarios finales

  >[!NOTE]
  >
  >Los usuarios con esta función también deben tener la función Usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada.

  **Usuario de invitación de Document Security**

  Los usuarios con esta función pueden invitar a usuarios. Estos permisos están asociados a la función:

   * Invitar a usuarios externos
   * Acceso a páginas web de usuarios finales

  **Usuario final de Document Security**

  Los usuarios con esta función pueden acceder a las páginas web del usuario final de Document Security. Esta función también se puede asignar a los administradores para que puedan crear directivas con las páginas de usuario final. Este permiso está asociado a la función Acceder a páginas web de usuario final.

* Los usuarios de la organización que tienen cuentas de seguridad de documentos válidas crean sus propias directivas, utilizan directivas para proteger documentos, rastrean y administran sus documentos protegidos por directivas y supervisan eventos relacionados con sus documentos.
* Los coordinadores de conjuntos de directivas administran documentos, ven eventos y administran otros coordinadores de conjuntos de directivas (según sus permisos). Los administradores designan a los usuarios como coordinadores de conjuntos de directivas para conjuntos de directivas concretos.
* Los usuarios externos a su organización (por ejemplo, un socio comercial) pueden utilizar documentos protegidos por directivas si se encuentran en el directorio de Document Security, si el administrador crea una cuenta para ellos o si se registran en Document Security mediante un proceso automatizado de invitación por correo electrónico. Según la forma en que el administrador habilite la configuración de acceso, los usuarios invitados también pueden tener permiso para aplicar directivas a los documentos, crear, modificar y eliminar sus directivas e invitar a otros usuarios externos a utilizar sus documentos protegidos por directivas.
* Los desarrolladores utilizan AEM Forms SDK para integrar aplicaciones personalizadas con la seguridad de los documentos.

Los administradores de Document Security pueden crear funciones personalizadas mediante los siguientes permisos en Administración de usuarios:

* Configuración de administración de seguridad de documentos
* Seguridad de documentos Administrar usuarios invitados y locales
* Seguridad de documentos Administrar conjuntos de directivas
* Seguridad de documentos Administrar conjuntos de directivas
* Eventos del servidor de vista de Document Security
* Seguridad de documentos Cambiar propietario de directiva

## Políticas y documentos protegidos por políticas {#policies-and-policy-protected-documents}

Una *directiva* define un conjunto de configuraciones de confidencialidad y usuarios que pueden tener acceso a un documento al que se aplica la directiva. Una directiva también permite cambiar dinámicamente los permisos de un documento. Otorga a la persona que asegura el documento permiso para cambiar la configuración de confidencialidad para revocar el acceso al documento o cambiar la directiva.

La protección de directivas se puede aplicar a un documento de PDF mediante Adobe Acrobat® Pro y Acrobat Standard. La protección de directivas se puede aplicar a otros tipos de archivo, como archivos de Microsoft® Word, Excel y PowerPoint, mediante la aplicación cliente con las extensiones de Acrobat Reader DC adecuadas instaladas.

### Funcionamiento de las directivas {#how-policies-work}

Las directivas contienen información sobre los usuarios autorizados y los parámetros de confidencialidad que deben aplicarse a los documentos. Los usuarios pueden ser cualquier miembro de la organización y personas externas a la organización que tengan una cuenta de. Si el administrador habilita la función de invitación de usuario, es posible incluso añadir nuevos usuarios a las directivas, iniciando así un proceso de correo electrónico de invitación de registro.

La configuración de confidencialidad de una política determina cómo pueden utilizar el documento los destinatarios. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, realizar cambios o agregar firmas y comentarios a documentos protegidos. La misma directiva también puede especificar diferentes configuraciones de confidencialidad para usuarios específicos.

>[!NOTE]
>
>La configuración de confidencialidad que se aplica a través de una directiva anula cualquier configuración que se haya aplicado a un documento de PDF en Acrobat mediante las opciones de seguridad de contraseña o certificado. (Consulte la Ayuda de Acrobat para obtener más información).

Los usuarios y administradores crean directivas a través de las páginas web de seguridad de los documentos. Sólo se puede aplicar una directiva a la vez a un documento. Puede aplicar una directiva utilizando uno de estos métodos:

* Abra el documento en Acrobat u otra aplicación cliente y seleccione una directiva para proteger el documento.
* Envíe un documento como archivo adjunto de correo electrónico en Microsoft® Outlook. En este caso, puede seleccionar una directiva de una lista de directivas. O bien, puede seleccionar una política generada automáticamente que Acrobat cree con un conjunto predeterminado de configuraciones de confidencialidad para proteger el documento únicamente para los destinatarios de los mensajes de correo electrónico.

Las directivas se pueden quitar de un documento mediante la aplicación cliente.

![rm_psonline_policy](assets/rm_psonline_policy.png)

Los pasos del diagrama son los siguientes:

1. El propietario del documento asegura el documento desde una aplicación cliente compatible con una directiva que permite el uso en línea.
1. Document Security crea una licencia de documento y claves de documento y cifra la directiva. La licencia de documento, la directiva cifrada y la clave de documento se devuelven a la aplicación cliente.
1. El documento se cifra con la clave del documento y esta se descarta. El documento ahora incrusta la licencia y la directiva. Estas tareas se realizan en la aplicación cliente admitida.

Al aplicar una directiva a un documento, la información que contiene, incluidos los archivos contenidos (texto, audio o vídeo) en los documentos de PDF, está protegida por la configuración de confidencialidad especificada en la directiva. Document Security genera una licencia e información de cifrado que luego se incrusta en el documento. Al distribuir el documento, Document Security puede autenticar los destinatarios que intentan abrir el documento y autorizar el acceso según los privilegios especificados en la directiva.

Si el uso sin conexión está habilitado, los destinatarios también pueden utilizar documentos protegidos por directivas sin conexión (sin una conexión activa a Internet o a la red) durante el período de tiempo especificado en la directiva.

### Funcionamiento de los documentos protegidos por directivas {#how-policy-protected-documents-work}

Para abrir y utilizar documentos protegidos por directivas, la directiva debe incluir su nombre como destinatario y debe tener una cuenta de Document Security válida. Para documentos de PDF, necesita Acrobat o Adobe Reader®. Para otros tipos de archivo, necesita la aplicación adecuada para el archivo con las extensiones de Acrobat Reader DC instaladas.

Al abrir un documento protegido por una directiva, Acrobat, Adobe Reader o las extensiones de Acrobat Reader DC se conectan a Document Security para autenticarse. A continuación, puede iniciar sesión. Si se está auditando el uso del documento, aparecerá un mensaje de notificación. Una vez que Document Security determina qué permisos de documento se concederán, administra el descifrado del documento. A continuación, puede utilizar el documento según la configuración de confidencialidad de la política.

![rm_psopen_online](assets/rm_psopen_online.png)

Los pasos del diagrama son los siguientes:

1. El usuario del documento abre el documento en una aplicación cliente compatible y se autentica con el servidor. El identificador de documento se envía al servidor de seguridad de documentos.
1. Document Security autentica a los usuarios, comprueba la directiva para obtener autorización y crea un cupón. El cupón (que contiene la clave de documento y los permisos) se devuelve a la aplicación cliente.
1. El documento se descifra con la clave del documento y esta se descarta. A continuación, el documento se puede utilizar de acuerdo con los parámetros de confidencialidad de la póliza. Estas tareas se realizan en la aplicación cliente admitida.

Puede seguir utilizando un documento en estas condiciones:

* De forma indefinida o para el período de validez especificado en la directiva
* Hasta que el administrador o la persona que aplicó la directiva anulen el acceso al documento o cambien la directiva

También puede utilizar documentos protegidos por directivas sin conexión (sin conexión a Internet o a la red) si la directiva permite el acceso sin conexión. Inicie sesión primero en Document Security para sincronizar el documento. A continuación, puede utilizar el documento durante el período de concesión sin conexión especificado en la directiva.

Cuando finalice el período de concesión sin conexión, vuelva a sincronizar el documento con Document Security, ya sea conectándose y abriendo un documento protegido por una directiva o utilizando un comando en la aplicación cliente. Consulte la *Ayuda de Acrobat* o la *Ayuda de extensiones de Acrobat Reader DC* adecuada para obtener más información.

Si guarda una copia de un documento protegido por una directiva mediante el comando de menú Guardar o Guardar como, la directiva se aplica automáticamente y se aplica al nuevo documento. Los eventos como los intentos de abrir el nuevo documento también se auditan y registran para el documento original.

## Conjuntos de directivas {#policy-sets}

*Los conjuntos de directivas* se utilizan para agrupar un conjunto de directivas que tienen un propósito comercial común. Estos conjuntos de directivas se ponen a disposición de un subconjunto de usuarios del sistema.

Cada conjunto de directivas puede tener uno o varios coordinadores de conjuntos de directivas asociados. El coordinador de conjuntos de directivas es un administrador o un usuario que tiene más permisos. El *coordinador de conjuntos de directivas* suele ser un especialista de la organización que puede crear mejor las directivas en un conjunto de directivas concreto.

Los coordinadores de conjuntos de directivas pueden realizar estas tareas:

* Creación de políticas
* Editar y eliminar cualquier política del conjunto de políticas
* Editar configuración de conjunto de directivas
* Agregar y quitar coordinadores de conjuntos de directivas
* Ver los eventos de directivas y documentos de cualquier directiva o documento del conjunto de directivas
* Revocar acceso a documentos
* Cambiar directivas para el documento.

>[!NOTE]
>
>Puede recuperar un máximo de 1000 nombres de conjuntos de directivas de la base de datos mediante la API `getAllPolicysetnames()`.

Los administradores y coordinadores de conjuntos de directivas que tienen permiso para hacerlo crean y eliminan conjuntos de directivas en las páginas web de administración de Document Security.

Los conjuntos de directivas están disponibles para un número limitado de usuarios al especificar qué usuarios o grupos dentro de un dominio pueden utilizar las directivas del conjunto de directivas para proteger documentos.

Cuando se instala Document Security, se crea un conjunto de directivas predeterminado denominado *Conjunto de directivas globales*. El administrador que instaló el software administra este conjunto de directivas.

## Prácticas recomendadas {#best-practices}

Las directivas son conjuntos reutilizables de permisos y grupos de usuarios que se pueden aplicar a varios documentos. Para los documentos protegidos. Estas políticas garantizan que solo los usuarios autorizados puedan utilizar las funciones permitidas. Se espera que el número de directivas y conjuntos de directivas aumente con el aumento de diferentes funciones de usuario y documentos dentro de un departamento. Para crear y administrar directivas, estas son algunas consideraciones y prácticas recomendadas:

* **Crear directivas reutilizables:** Adobe recomienda reutilizar directivas en varios documentos. Ayuda a reducir al mínimo el número de directivas, proporciona un rendimiento óptimo y facilita su administración. Para crear una directiva reutilizable:

1. Identificar y definir los requisitos de control de acceso en los departamentos y organizaciones.

1. Cree grupos de usuarios y añádalos.

1. Cree un conjunto de políticas.

1. Abra el conjunto de directivas y cree una directiva. Añada grupos de usuarios y establezca la configuración de confidencialidad (control de acceso) para la directiva.

Agregue grupos de usuarios a las directivas en lugar de usuarios individuales. Facilita la administración y aplicación de directivas a muchos usuarios.

* **Crear conjuntos de directivas personalizados:** Un conjunto de directivas combina varias directivas en una entidad manejable. Cree conjuntos de directivas personalizadas para su organización o departamento, utilícelos para agrupar directivas relacionadas y ponerlas a disposición de un subconjunto de usuarios del sistema.

  El uso de conjuntos de directivas facilita la asignación y administración de directivas relacionadas a usuarios específicos de una organización o departamento. Por ejemplo, los conjuntos de políticas independientes para el departamento de finanzas y recursos humanos pueden ayudar a administrar y aplicar fácilmente las políticas relacionadas a los documentos designados para los departamentos correspondientes.

* **Use un autorizador externo para aplicar permisos de forma dinámica:** Puede usar [autorizador externo](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html) para evaluar y aplicar permisos de forma dinámica según una condición externa. Cuando los permisos se evalúan dinámicamente en función de condiciones externas, puede:

   * Proporcionar control de acceso centralizado a los documentos de su organización.

   * Controle el acceso a los documentos protegidos por directivas determinando dinámicamente si un usuario puede acceder a un documento protegido por directivas. Por ejemplo, decide dinámicamente si un usuario puede imprimir un documento protegido por una directiva.

   * Utilice un mecanismo de control de acceso que utilice el sistema de gestión de contenido, además del proceso de evaluación de directivas estándar. Por ejemplo, cuando el servicio determina si un usuario puede imprimir un documento protegido por una directiva, puede utilizar el proceso de evaluación de directivas estándar. También puede utilizar el mecanismo de control de acceso que utiliza su sistema de administración de contenido.

  Aunque es posible reemplazar completamente el proceso de evaluación de directivas de Document Security por un controlador de autorización externo, se recomienda utilizar un controlador de autorización externa con el proceso de evaluación de directivas. Como resultado, el acceso a los documentos se puede controlar mediante el mismo mecanismo de control que utiliza el sistema de gestión de contenido. Por ejemplo, cuando el servicio Document Security determina si un usuario puede imprimir un documento protegido por una directiva, utiliza el proceso de evaluación de directivas estándar. También utiliza el mecanismo de control de acceso que utiliza el sistema de administración de contenido. Para obtener más información, vea [Crear controladores de autorización externos](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html).

* **Mantener los conjuntos de directivas en un número limitado:** Varios factores conducen al crecimiento constante de directivas y conjuntos de directivas. Algunos factores comunes son:

   * Aumento de los roles de usuario, departamentos y documentos dentro de una organización durante un periodo.
   * Los departamentos de una organización trabajan de forma aislada y mantienen un control estricto de las políticas específicas de cada departamento. Esto lleva a políticas idénticas dentro de una organización.

  Adobe recomienda mantener al mínimo el número de directivas y conjuntos de directivas. Ayuda a administrar fácilmente las políticas y los conjuntos de políticas y a proporcionar un mejor rendimiento. Para mantener el número al mínimo:

   * Crear directivas reutilizables. Estas políticas se pueden compartir en varios departamentos.
   * Considere la posibilidad de crear conjuntos de directivas para toda la organización, si algunas directivas se aplican a varios departamentos en lugar de un conjunto de directivas individual para cada departamento.
   * Directivas relacionadas con grupos en un conjunto de directivas. No cree un conjunto de directivas distinto para cada directiva.
   * Utilice un autorizador externo para controlar dinámicamente los permisos de usuario.

  >[!NOTE]
  >
  >Puede usar la API [getAllPolicysetnames()](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/PolicyManager.html) para recuperar un máximo de 1000 nombres de conjuntos de directivas. Internamente, la API recupera un máximo de 1000 directivas para las que el invocador de la API tiene permiso de editor de documentos y, a continuación, crea y devuelve una lista de nombres de conjuntos de directivas únicos asociados a las directivas recuperadas. Por ejemplo, cuando la API recupera 1000 directivas y las directivas recuperadas están asociadas a 200 conjuntos de directivas en total, la API devuelve solo 200 nombres de conjuntos de directivas.
