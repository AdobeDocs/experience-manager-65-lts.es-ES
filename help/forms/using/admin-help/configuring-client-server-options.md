---
title: Configurar las opciones de cliente y servidor
description: Obtenga información sobre cómo configurar las distintas opciones de cliente y servidor, como las opciones de configuración del servidor, las funciones de seguridad de documentos y la auditoría de eventos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 72c31f40-d1b0-47ae-bdeb-e9b92c3d27e1
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '10278'
ht-degree: 0%

---

# Configuración del servidor de Document Security {#configure-the-document-security-server}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > Document Security > Configuración > Configuración del servidor.
1. Configure los ajustes y haga clic en Aceptar.

## Ajustes de configuración del servidor {#server-configuration-settings}

**Dirección URL base:** Dirección URL base de Document Security que contiene el nombre y el puerto del servidor. La información adjunta a la base crea direcciones URL de conexión. Por ejemplo, /edc/Main.do se anexa para tener acceso a las páginas web. Los usuarios también responden a las invitaciones de registro de usuarios externos a través de esta dirección URL.

Si utiliza IPv6, escriba la dirección URL base como nombre del equipo o el nombre DNS. Si utiliza una dirección IP numérica, Acrobat no podrá abrir los archivos protegidos por directivas. Además, utilice una URL HTTP segura (HTTPS) para su servidor.

>[!NOTE]
>
>La dirección URL base está incrustada en archivos protegidos por directivas. Las aplicaciones cliente utilizan la dirección URL base para volver a conectarse al servidor. Los archivos protegidos seguirán conteniendo la dirección URL base, incluso si se cambia más adelante. Si cambia la dirección URL base, la información de configuración debe actualizarse para todos los clientes que se conectan.

**Período de concesión sin conexión predeterminado:** Período de tiempo predeterminado que un usuario puede utilizar un documento protegido sin conexión. Esta configuración determina el valor inicial de la configuración Período de concesión sin conexión automática al crear una directiva. (Consulte Creación y edición de directivas). Cuando caduca el período de concesión, el destinatario debe sincronizar de nuevo el documento para seguir utilizándolo.

Para ver cómo funciona la concesión y sincronización sin conexión, consulte [Manual sobre la configuración de la concesión y sincronización sin conexión](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Período de sincronización sin conexión predeterminado:** Tiempo máximo desde el que se puede utilizar cualquier documento sin conexión cuando se protege inicialmente.

**Tiempo de espera de sesión de cliente:** Período de tiempo, en minutos, tras el cual Document Security se desconecta si un usuario que ha iniciado sesión a través de una aplicación cliente no interactúa con Document Security.

**Permitir el acceso de usuarios anónimos:** Seleccione esta opción para habilitar la capacidad de crear directivas compartidas y personales que permitan a los usuarios anónimos abrir documentos protegidos por directivas. (Los usuarios que no tengan cuentas de pueden acceder al documento, pero no pueden iniciar sesión en Document Security ni utilizar otros documentos protegidos por directivas).

**Deshabilitar el acceso a los clientes de la versión 7:** Especifica si los usuarios pueden usar Acrobat o Reader 7.0 para conectarse al servidor. Cuando se selecciona esta opción, los usuarios deben utilizar Acrobat o Reader 8.0 y versiones posteriores para completar las operaciones de seguridad de los documentos en documentos de PDF. Si las directivas requieren que Acrobat o Reader 8.0 y posteriores se ejecuten en modo certificado al abrir documentos protegidos por directivas, debe deshabilitar el acceso a Acrobat o Reader 7. (Consulte Especificar los permisos de documento para usuarios y grupos).

**Permitir acceso sin conexión por documento** Seleccione esta opción para especificar el acceso sin conexión por documento. Si esta opción está habilitada, el usuario sólo tendrá acceso sin conexión a los documentos que haya abierto en línea al menos una vez.

**Permitir autenticación de contraseña de nombre de usuario:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen la autenticación de nombre de usuario y contraseña al conectarse al servidor.

**Permitir autenticación Kerberos:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen la autenticación Kerberos al conectarse al servidor.

**Permitir autenticación de certificado de cliente:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación de certificado al conectarse al servidor.

**Permitir autenticación extendida** Seleccione esta opción para habilitar la autenticación extendida y, a continuación, escriba la dirección URL de aterrizaje de autenticación extendida.

Al seleccionar esta opción, las aplicaciones cliente pueden utilizar la autenticación extendida. La autenticación extendida proporciona procesos de autenticación personalizados y diferentes opciones de autenticación configuradas en el servidor de AEM Forms. Por ejemplo, ahora los usuarios pueden experimentar la autenticación basada en SAML en lugar del nombre de usuario y la contraseña de los formularios AEM, desde Acrobat y el cliente de Reader. De manera predeterminada, la dirección URL de aterrizaje contiene *localhost* como nombre de servidor. Sustituya el nombre del servidor por un nombre de host completo. El nombre de host de la dirección URL de aterrizaje se rellena automáticamente desde la dirección URL base si la autenticación extendida aún no está habilitada. Consulte [Agregar el proveedor de autenticación extendida](configuring-client-server-options.md#add-the-extended-authentication-provider).

***nota &#x200B;**: La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posterior.*

**Ancho de control de HTML preferido para la autenticación extendida** Especifique el ancho del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales de usuario.

**Altura de control de HTML preferida para la autenticación extendida** Especifique la altura del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales del usuario.

***nota &#x200B;**: Los límites de anchura y altura de este cuadro de diálogo son los siguientes:*
Anchura: mínima = 400, máxima = 900

Altura: mínima = 450; máxima = 800

**Habilitar almacenamiento en caché de credenciales de cliente:** Seleccione esta opción para permitir que los usuarios almacenen en caché sus credenciales (nombre de usuario y contraseña). Cuando las credenciales de los usuarios se almacenan en caché, no tienen que escribirlas cada vez que abren un documento o cuando hacen clic en el botón Actualizar de la página Administrar directivas de seguridad de Adobe Acrobat. Puede especificar el número de días antes de que los usuarios deban proporcionar sus credenciales de nuevo. Si establece el número de días en 0, las credenciales se pueden almacenar en caché indefinidamente.

## Configuración de usuarios y administradores de Document Security {#configuring-document-security-users-and-administrators}

### Asignación de funciones de seguridad de documentos a administradores {#assigning-document-security-roles-to-administrators}

El entorno de formularios AEM Forms contiene uno o varios usuarios administradores que tienen los privilegios adecuados para crear usuarios y grupos. Si su organización utiliza Document Security, también debe asignarse al menos un administrador para administrar los usuarios invitados y locales.

Los administradores también deben tener la función Usuario de la consola de administración para acceder a ella. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuración de usuarios y grupos visibles {#configuring-visible-users-and-groups}

Para ver usuarios y grupos en los dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o administrador de conjuntos de directivas debe seleccionar y agregar dominios (creados en Administración de usuarios) a la lista de usuarios y grupos visibles para cada conjunto de directivas.

La lista de usuarios y grupos visibles está visible para el coordinador de conjuntos de directivas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregarlos a las directivas. Si no se realiza esta tarea, el coordinador del conjunto de directivas no encontrará ningún usuario o grupo que agregar a la directiva. Puede haber más de un coordinador de conjunto de directivas para un conjunto de directivas determinado.

1. Después de instalar y configurar el entorno de AEM Forms con Document Security, configure todos los dominios adecuados en Administración de usuarios. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota &#x200B;**: la creación de dominios debe realizarse antes de poder crear directivas.*

1. En la consola de administración, haga clic en Servicios > Administración de documentos > Directivas y, a continuación, haga clic en la pestaña Conjuntos de directivas.
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.
1. Vaya a Servicios > Document Security > Configuración > Mis directivas y haga clic en la pestaña Usuarios y grupos visibles.
1. Haga clic en Agregar dominio(s) y agregue los dominios existentes según sea necesario.

## Agregar el proveedor de autenticación extendida {#add-the-extended-authentication-provider}

Los formularios AEM Forms proporcionan una configuración de ejemplo que puede personalizar para su entorno. Siga estos pasos:

>[!NOTE]
>
>La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

1. Obtenga el archivo WAR de muestra para implementarlo. Consulte la guía de instalación adecuada para su servidor de aplicaciones.
1. Asegúrese de que el servidor de Forms tiene un nombre completo en lugar de direcciones IP como dirección URL base y que es una dirección URL HTTPS. Consulte [Configuración del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Habilite Autenticación extendida desde la página Configuración del servidor. Consulte [Configuración del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Añada las URL de redireccionamiento de SSO requeridas en el archivo de configuración de User Management. Consulte [Agregar URL de redireccionamiento de SSO para la autenticación extendida](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Añadir URL de redireccionamiento de SSO para la autenticación extendida {#add-sso-redirect-urls-for-extended-authentication}

Con la autenticación extendida habilitada, los usuarios que abren un documento protegido por una directiva en Acrobat XI o Reader XI obtienen un cuadro de diálogo para la autenticación. Este cuadro de diálogo carga la página de HTML que especificó como URL de aterrizaje de autenticación extendida en la configuración del servidor de Document Security. Consulte [Configuración del servidor](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar y guarde el archivo de configuración en el disco.
1. Abra el archivo en un editor y busque el nodo AllowedUrls.
1. En el nodo `AllowedUrls`, agregue las líneas siguientes: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Guarde el archivo y, a continuación, importe el archivo actualizado desde la página Configuración manual: en la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.

## Configuración de la seguridad sin conexión {#configuring-offline-security}

Document Security permite utilizar documentos protegidos por directivas sin conexión sin conexión a Internet o a la red. Esta capacidad requiere que la directiva permita el acceso sin conexión, tal como se describe en [Especifique los permisos de documento para usuarios y grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Para que un documento que tenga una directiva de este tipo pueda utilizarse sin conexión, el destinatario debe abrir el documento mientras está en línea y habilitar el acceso sin conexión haciendo clic en Sí cuando se le solicite. También se puede solicitar al destinatario que autentique su identidad. A continuación, el destinatario puede utilizar los documentos sin conexión durante el período de concesión sin conexión especificado en la directiva.

Cuando finaliza el período de concesión sin conexión, el destinatario debe volver a sincronizarse con Document Security abriendo un documento en línea o utilizando un comando de menú de extensiones de Acrobat o Acrobat Reader DC para sincronizar. (Consulte la *Ayuda de Acrobat* o la *Ayuda de las extensiones de Acrobat Reader DC* correspondiente).

Dado que los documentos que permiten el acceso sin conexión requieren almacenar en caché el material clave en el equipo donde los archivos se almacenan sin conexión, el archivo puede verse potencialmente comprometido si un usuario no autorizado puede obtener el material clave. Para compensar esta posibilidad, se proporcionan opciones de sustitución de claves programadas y manuales que puede configurar para evitar que una persona no autorizada utilice la clave para acceder al documento.

### Establecer un período de concesión sin conexión predeterminado {#set-a-default-offline-lease-period}

Los destinatarios de documentos protegidos por directivas pueden desconectar los documentos durante el número de días especificado en la directiva. Después de sincronizar inicialmente el documento con Document Security, el destinatario puede utilizarlo sin conexión hasta que caduque el período de concesión sin conexión. Cuando caduca el período de concesión, el destinatario debe poner el documento en línea e iniciar sesión para sincronizar con Document Security y continuar utilizando el documento.

Puede configurar un período de concesión sin conexión predeterminado. El período de concesión se puede cambiar del predeterminado cuando cualquier persona crea o edita una directiva.

1. En la página Document Security, haga clic en Configuración > Configuración del servidor.
1. En el cuadro Período de concesión sin conexión predeterminado, escriba el número de días para el período de concesión sin conexión.
1. Haga clic en Aceptar.

### Administración de rollovers de claves {#manage-key-rollovers}

Document Security utiliza algoritmos de cifrado y licencias para proteger los documentos. Cuando cifra un documento, Document Security genera y administra una clave de descifrado denominada *DocKey* que pasa a la aplicación cliente. Si la directiva que protege un documento permite el acceso sin conexión, también se genera una clave sin conexión denominada *clave principal* para cada usuario que tenga acceso sin conexión al documento.

>[!NOTE]
>
>Si no existe una clave principal, Document Security genera una para proteger un documento.

Para abrir un documento protegido por una directiva sin conexión, el equipo del usuario debe tener la clave principal adecuada. El equipo obtiene la clave principal cuando el usuario realiza la sincronización con Document Security (abre un documento protegido en línea). Si esta clave principal está en peligro, cualquier documento al que el usuario tenga acceso sin conexión también podría verse comprometido.

Una forma de reducir la amenaza que supone para los documentos sin conexión es evitar permitir el acceso sin conexión a documentos especialmente confidenciales. Otro método es pasar periódicamente sobre las claves principales. Cuando Document Security transfiere la clave, las claves existentes ya no pueden acceder a los documentos protegidos por directivas. Por ejemplo, si un perpetrador obtiene una clave principal de un portátil robado, esa clave no se puede utilizar para acceder a los documentos protegidos después de la sustitución. Si sospecha que una clave principal específica se ha visto comprometida, puede pasar manualmente sobre la clave.

Sin embargo, una sustitución de claves afecta a todas las claves principales, no solo a una. También reduce la escalabilidad del sistema porque los clientes deben almacenar más claves para el acceso sin conexión. La frecuencia de rollover de clave predeterminada es de 20 días. Se recomienda no establecer este valor por debajo de 14 días, ya que a las personas se les puede impedir ver documentos sin conexión y el rendimiento del sistema puede verse afectado.

En el ejemplo siguiente, Key1 es la carpeta de las dos claves principales y Key2 es la más reciente. Al hacer clic en el botón Claves de desplazamiento ahora la primera vez, Key1 deja de ser válida y se genera una clave principal válida más reciente (Key3). Los usuarios obtienen la clave 3 cuando se sincronizan con Document Security, normalmente abriendo un documento protegido en línea. Sin embargo, los usuarios no están obligados a sincronizar con Document Security hasta que alcancen el período máximo de concesión sin conexión especificado en una directiva. Después de la primera sustitución de claves, los usuarios que permanecen sin conexión pueden seguir abriendo documentos sin conexión, incluidos los protegidos por Key3, hasta que alcancen el período máximo de concesión sin conexión. Cuando haga clic en el botón Claves de rollover ahora por segunda vez, Key2 deja de ser válida y se crea Key4. Los usuarios que permanecen sin conexión durante las dos rollovers de claves no pueden abrir documentos protegidos con Key3 o Key4 hasta que se sincronizan con Document Security.

**Cambiar la frecuencia de sustitución de claves**

Por motivos de confidencialidad, cuando utiliza documentos sin conexión, Document Security proporciona una opción de sustitución automática de claves con un periodo de frecuencia predeterminado de 20 días. Puede cambiar la frecuencia de rollover; sin embargo, evite establecer un valor inferior a 14 días, ya que se puede impedir que las personas vean documentos sin conexión y el rendimiento del sistema puede verse afectado.

1. En la página Document Security, haga clic en Configuración > Administración de claves.
1. En el cuadro Frecuencia de rollover de clave, escriba el número de días para el período de rollover.
1. Haga clic en Aceptar.

**Redistribuir manualmente las claves principales**

Para mantener la confidencialidad de los documentos sin conexión, puede pasar manualmente las claves principales. Es posible que necesite pasar manualmente una clave (por ejemplo, si alguien que la obtenga de un equipo en el que esté almacenada en caché la clave para habilitar el acceso sin conexión a un documento).

>[!NOTE]
>
>Evite utilizar con frecuencia la sustitución manual, ya que hace que todas las claves principales se transfieran, no solo una, y puede impedir temporalmente que los usuarios vean nuevos documentos sin conexión.

Las claves principales se deben renovar dos veces antes de que se invaliden las claves existentes previamente en los equipos cliente. Los equipos cliente que han invalidado claves principales deben volver a sincronizarse con el servicio Document Security para adquirir las nuevas claves principales.

1. En la página Document Security, haga clic en Configuración > Administración de claves.
1. Haga clic en Claves de rollover ahora y, a continuación, en Aceptar.
1. Espere unos 10 minutos. El siguiente mensaje de registro aparece en el registro del servidor: `Done RightsManagement key rollover for`*N* `principals`. Donde *N* es el número de usuarios en el sistema de seguridad de documentos.
1. Haga clic en Claves de rollover ahora y, a continuación, en Aceptar.
1. Espere unos 10 minutos.

## Configuración de la auditoría de eventos y la privacidad {#configuring-event-auditing-and-privacy-settings}

La seguridad de los documentos puede auditar y registrar información sobre eventos relacionados con la interacción con documentos protegidos por directivas, directivas, administradores y el servidor. Puede configurar la auditoría de eventos y especificar los tipos de eventos que desea auditar. Para auditar eventos de un documento concreto, también debe habilitarse la opción de auditoría en la directiva.

Cuando la auditoría está habilitada, puede ver los detalles de los eventos auditados en la página Eventos. los usuarios de document security también pueden ver eventos relacionados específicamente con los documentos protegidos por directivas que utilizan o crean.

Puede seleccionar estos tipos de eventos para realizar auditorías:

* Eventos de documentos protegidos por directivas, como intentos de abrir documentos por usuarios autorizados o no autorizados
* Eventos de directiva, como crear, cambiar, eliminar, habilitar y deshabilitar directivas
* Eventos de usuario, como invitaciones y registros de usuarios externos, cuentas de usuario activadas y desactivadas, cambios en las contraseñas de usuario y actualizaciones de perfiles
* Eventos de formularios AEM Forms, como discrepancias de versiones, servidores de directorios no disponibles y proveedores de autorización, y cambios en la configuración del servidor

### Habilitar o deshabilitar la auditoría de eventos {#enable-or-disable-event-auditing}

Puede habilitar y deshabilitar la auditoría de eventos relacionados con el servidor, documentos protegidos por directivas, directivas, conjuntos de directivas y usuarios. Al habilitar la auditoría de eventos, puede elegir auditar todos los eventos posibles o seleccionar eventos específicos para auditar.

Cuando se habilita la auditoría del servidor, se pueden ver los eventos auditados en la página Eventos.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Configuración de auditoría y privacidad.
1. Para configurar la auditoría del servidor, en Habilitar auditoría de servidor, seleccione Sí o No.
1. Si ha seleccionado Sí, en cada categoría de evento, realice una de las siguientes acciones para seleccionar las opciones que desea auditar:

   * Para auditar todos los eventos de la categoría, seleccione Todos.
   * Para auditar sólo algunos eventos, anule la selección de Todos y, a continuación, active las casillas de verificación situadas junto a los eventos que desee auditar.

     (Consulte [Opciones de auditoría de eventos](configuring-client-server-options.md#event-auditing-options).)

1. Haga clic en Aceptar.

>[!NOTE]
>
>Al trabajar con las páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y la flecha Atrás o Adelante porque esta acción puede causar problemas no deseados de captura de datos y visualización de datos.

### Habilitar o deshabilitar la notificación de privacidad {#enable-or-disable-privacy-notification}

Puede habilitar y deshabilitar un mensaje de notificación de privacidad. Al habilitar la notificación de privacidad, aparece un mensaje cuando un destinatario intenta abrir un documento protegido por una directiva. El aviso informa al usuario de que se está auditando el uso del documento. También puede especificar una dirección URL que el usuario pueda utilizar para ver su página de directivas de privacidad si hay una disponible.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Configuración de auditoría y privacidad.
1. Para configurar la notificación de privacidad, en Habilitar notificación de privacidad, seleccione Sí o No.

   Si la directiva adjunta a un documento permite el acceso anónimo al usuario y la opción Habilitar aviso de privacidad está establecida en No, no se solicitará al usuario que inicie sesión y no se mostrará el mensaje de notificación de privacidad.

   Si la directiva adjunta a un documento no permite el acceso de usuarios anónimos, el usuario verá el mensaje de notificación de privacidad.

1. Si procede, en el cuadro URL de privacidad, escriba la dirección URL de la página de directiva de privacidad. Si se deja en blanco el cuadro URL de privacidad, se muestra la página de privacidad de adobe.com.
1. Haga clic en Aceptar.

>[!NOTE]
>
>La desactivación del aviso de privacidad no desactiva la auditoría del uso de documentos. Las acciones de auditoría y las acciones personalizadas predeterminadas admitidas mediante el seguimiento de uso extendido aún pueden recopilar información de comportamiento del usuario.

### Importar un tipo de evento de auditoría personalizado {#import-a-custom-audit-event-type}

Si utiliza una aplicación habilitada para Document Security que admite la auditoría de eventos adicionales, como eventos específicos de un tipo de archivo determinado, un socio de Adobe puede proporcionarle eventos de auditoría personalizados que puede importar en Document Security. Utilice esta función solo si un socio de Adobe le ha proporcionado tipos de eventos personalizados.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Administración de eventos.
1. Haga clic en Examinar para ir al archivo XML que desea importar y haga clic en Importar.
1. La importación sobrescribe los tipos de eventos de auditoría personalizados existentes en el servidor si se encuentran combinaciones idénticas de espacio de nombres y código de evento.
1. Haga clic en Aceptar.

### Eliminar un tipo de evento de auditoría personalizado {#delete-a-custom-audit-event-type}

1. En la consola de administración, haga clic en Servicios > Document Security > Configuración > Administración de eventos.
1. Seleccione la casilla de verificación situada junto al tipo de evento de auditoría personalizado que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar.

### Exportar eventos de auditoría {#export-audit-events}

Puede exportar eventos de auditoría a un archivo para archivarlos.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Administración de eventos.
1. Edite la configuración en Exportar eventos de auditoría según sea necesario. Puede especificar:

   * la edad mínima de los eventos de auditoría que se van a exportar
   * número máximo de eventos de auditoría que se incluirán en un solo archivo. El servidor genera uno o varios archivos en función de este valor.
   * carpeta en la que se creará el archivo. Esta carpeta se encuentra en el servidor de Forms. Si la ruta de la carpeta es relativa, entonces es relativa al directorio raíz del servidor de aplicaciones.
   * prefijo de archivo que se va a utilizar para los archivos de eventos de auditoría
   * el formato del archivo, ya sea un archivo de valores separados por comas (CSV) compatible con Microsoft Excel o un archivo XML.

1. Haga clic en Exportar. Si desea cancelar la exportación, haga clic en Cancelar exportación. Si otro usuario ha programado una exportación, el botón Cancelar exportación no estará disponible hasta que se complete la exportación. El botón Cancelar exportación no está disponible si otro usuario ha programado una exportación. Para comprobar si ha comenzado o finalizado una exportación o eliminación programadas, haga clic en Actualizar.

### Eliminar eventos de auditoría {#delete-audit-events}

Puede eliminar eventos de auditoría que tengan una antigüedad superior al número de días especificado.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Administración de eventos.
1. En Eliminar eventos de auditoría, especifique el número de días en el cuadro Eliminar eventos de auditoría anteriores a.
1. Haga clic en Eliminar. Haga clic en Exportar. Si desea cancelar la eliminación, haga clic en Cancelar eliminación. Si otro usuario ha programado una eliminación, el botón Cancelar eliminación no estará disponible hasta que se complete la exportación. El botón Cancelar eliminación no está disponible si otro usuario ha programado una exportación. Para comprobar si una eliminación programada ha comenzado o finalizado, haga clic en Actualizar.

### Opciones de auditoría de eventos {#event-auditing-options}

Puede habilitar y deshabilitar la auditoría de eventos y especificar los tipos de eventos que se auditarán.

**Eventos de documento**

**Ver documento:** Un destinatario ve un documento protegido por una directiva.

**Cerrar documento:** Un destinatario cierra un documento protegido por una directiva.

**Imprimir de baja resolución** Un destinatario imprime un documento protegido por una directiva con la opción de baja resolución especificada.

**Imprimir alta resolución:** Un destinatario imprime un documento protegido por una directiva con la opción de alta resolución especificada.

**Agregar anotación al documento:** Un destinatario agrega una anotación a un documento de PDF.

**Revocar documento:** Un usuario o administrador revoca el acceso a un documento protegido por una directiva.

**Anular la revocación del documento:** Un usuario o administrador restablece el acceso a un documento protegido por una directiva.

**Relleno de formularios:** Un destinatario introduce información en un documento de PDF que es un formulario que se puede rellenar.

**Directiva eliminada:** Un editor quita una directiva de un documento para retirar las protecciones de seguridad.

**Cambiar URL de revocación de documento:** Una llamada desde el nivel de API cambia la URL de revocación especificada para obtener acceso a un nuevo documento que reemplaza a un documento revocado.

**Modificar documento:** Un destinatario cambia el contenido de un documento protegido por una directiva.

**Firmar documento:** Un destinatario firma un documento.

**Proteger un documento nuevo:** Un usuario aplica una directiva para proteger un documento.

**Cambiar directiva en el documento:** Un usuario o administrador cambia la directiva adjunta a un documento.

**Publicar documento como:** Un nuevo documento cuyo documentName y licencia son idénticos a un documento existente está registrado en el servidor y los documentos no tienen una relación principal-secundario. Este evento se puede activar mediante la SDK de formularios AEM Forms.

**Documento iterativo:** Un nuevo documento cuyo documentName y licencia son idénticos a un documento existente está registrado en el servidor, y los documentos tienen una relación principal-secundario. Este evento se puede activar mediante la SDK de formularios AEM Forms.

**Eventos de directiva**

**Directiva creada:** Un usuario o administrador crea una directiva.

**Directiva habilitada:** Un administrador hace que una directiva esté disponible.

**Directiva modificada:** Un usuario o administrador cambia una directiva.

**Directiva deshabilitada:** Un administrador hace que una directiva no esté disponible.

**Directiva eliminada:** Un usuario o administrador elimina una directiva.

**Cambiar propietario de directiva:** Una llamada desde el nivel de API cambia el propietario de la directiva.

**Eventos de usuario**

**Usuario eliminado:** Un administrador elimina una cuenta de usuario.

**Registrar usuario invitado:** Un usuario externo se registra con Document Security.

**Inicio de sesión correcto:** intentos de inicio de sesión correctos de administradores o usuarios.

**Usuarios invitados:** Document Security invita a un usuario a registrarse.

**Usuarios activados:** Los usuarios externos activan sus cuentas mediante la dirección URL del correo electrónico de activación o un administrador habilita una cuenta.

**Cambiar contraseña:** Los usuarios invitados cambiarán sus contraseñas o un administrador restablecerá una contraseña para un usuario local.

**Error de inicio de sesión:** intentos de inicio de sesión erróneos por parte de administradores o usuarios.

**Usuarios desactivados:** Un administrador deshabilita una cuenta de usuario local.

**Actualización de perfil:** Los usuarios invitados cambiaron su nombre, nombre de organización y contraseña.

**Cuenta bloqueada:** Un administrador bloquea una cuenta.

**Eventos de conjunto de directivas**

**Creado
Conjunto de directivas:** Un administrador o coordinador de conjuntos de directivas crea un conjunto de directivas.

**Conjunto de directivas eliminado:** Un administrador o coordinador de conjuntos de directivas elimina un conjunto de directivas.

**Conjunto de directivas modificado:** Un administrador o coordinador de conjuntos de directivas cambia un conjunto de directivas.

**Eventos del sistema**

**Directorio
Sincronización completada:** Esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado y la hora de sincronización actual de la última sincronización, se muestra en la página Administración de dominios. Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Cliente habilitado para el acceso sin conexión:** Un usuario habilitó el acceso sin conexión a documentos protegidos contra el servidor en el equipo del usuario.

**La aplicación cliente sincronizada** debe sincronizar la información con el servidor para permitir el acceso sin conexión.

**La versión no coincide:** Una versión de AEM Forms SDK que no es compatible con el servidor intentó conectarse al servidor.

**Información de sincronización de directorios:** Esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado y la hora de sincronización actual de la última sincronización, se muestra en la página Administración de dominios. Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Cambio de configuración del servidor:** cambios en la configuración del servidor que se realizan a través de las páginas web o manualmente mediante la importación de un archivo config.xml. Esto incluye cambios en la dirección URL base, tiempos de espera de sesión, bloqueos de inicio de sesión, configuración de directorios, rollovers de claves, configuración del servidor SMTP para registro externo, configuración de marcas de agua, opciones de visualización, etc.

## Configuración del seguimiento de uso extendido {#configuring-extended-usage-tracking}

La seguridad de los documentos puede realizar un seguimiento de varios eventos personalizados que se pueden realizar en un documento protegido. Puede habilitar el seguimiento de eventos desde el servidor de Document Security a nivel global o a nivel de directiva. A continuación, puede configurar una JavaScript para capturar acciones específicas realizadas dentro del documento protegido de PDF, como hacer clic en un botón o guardar el documento. Estos datos de uso se envían como un archivo XML en pares clave-valor, que puede utilizar para un análisis más amplio. Los usuarios finales que accedan a los documentos protegidos pueden permitir o rechazar dicho seguimiento desde la aplicación cliente.

Si el seguimiento está habilitado a nivel global, puede anular esta configuración a nivel de directiva y deshabilitarla para una directiva en particular. La anulación de nivel de directiva no es posible si el seguimiento está deshabilitado a nivel global. La lista de eventos rastreados se inserta automáticamente en el servidor cuando el recuento de eventos alcanza 25 o cuando se cierra el documento. También puede configurar el script para que inserte explícitamente la lista de eventos según sus necesidades. Puede personalizar el seguimiento de eventos accediendo a las propiedades y los métodos del objeto de seguridad de documentos.

Después de habilitar el seguimiento, todas las directivas que se creen posteriormente tendrán activado el seguimiento de forma predeterminada. Las directivas creadas antes de habilitar el seguimiento en el servidor necesitarán actualizaciones manuales.

### Habilitar o deshabilitar el seguimiento de uso extendido {#enable-or-disable-extended-usage-tracking}

Antes de empezar, asegúrese de que la Auditoría de servidores está habilitada. Consulte [Configuración de auditoría de eventos y configuración de privacidad](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) para obtener más información sobre la auditoría.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Configuración de auditoría y privacidad.
1. Para configurar el seguimiento de uso extendido, en Habilitar seguimiento, seleccione Sí o No.
1. Para establecer la selección de la casilla de verificación Permitir la recopilación de datos de uso detallados en la página de inicio de sesión, en Habilitar el seguimiento predeterminado, seleccione Sí o No.

Para ver los eventos rastreados, puede utilizar el filtro Eventos de documento en la página Eventos. Los eventos rastreados con JavaScript se etiquetan como Seguimiento detallado del uso. Consulte [Supervisar eventos](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) para obtener más información sobre los eventos.

## Configurar la configuración de visualización de Document Security {#configure-document-security-display-settings}

1. En la consola de administración, haga clic en Servicios > Document Security > Configuración > Opciones de visualización.
1. Configure los ajustes y haga clic en Aceptar.

### Configuración de visualización {#display-settings}

**Filas para mostrar para resultados de búsqueda:** Número de filas que aparecen en una página cuando se realizan búsquedas.

**Personalización para el cuadro de diálogo de inicio de sesión de cliente**

Esta configuración controla el texto que se muestra en la solicitud de inicio de sesión que aparece cuando un usuario inicia sesión en Document Security a través de una aplicación cliente.

**Texto de bienvenida:** El texto del mensaje de bienvenida, como &quot;Inicie sesión con su nombre de usuario y contraseña&quot;. El texto del mensaje de bienvenida debe contener información sobre cómo iniciar sesión en Document Security y cómo ponerse en contacto con un administrador u otra persona de soporte designada de su organización para obtener ayuda. Por ejemplo, es posible que los usuarios externos deban ponerse en contacto con un administrador si olvidan sus contraseñas o necesitan ayuda con el proceso de registro o inicio de sesión. La longitud máxima del texto de bienvenida es de 512 caracteres.

**Texto de nombre de usuario:** Etiqueta de texto para el cuadro de nombre de usuario.

**Texto de contraseña:** Etiqueta de texto para el cuadro de contraseña.

**Personalización para el cuadro de diálogo de autenticación de certificado de cliente**

Esta configuración controla el texto mostrado en el cuadro de diálogo de autenticación de certificado.

**Elegir
Texto del tipo de autenticación:** Texto mostrado para indicar al usuario que seleccione un tipo de autenticación.

**Elegir texto de certificado:** Se muestra el texto para indicar al usuario que seleccione un tipo de certificado.

**Certificados no disponibles Texto de error:** Mensaje de hasta 512 caracteres para mostrar cuando el certificado seleccionado no está disponible.

**Personalización para la visualización del certificado de cliente**

**Mostrar solo los emisores de credenciales de confianza:** Cuando se selecciona esta opción, la aplicación cliente presenta al usuario únicamente certificados de emisores de credenciales en los que los formularios de AEM están configurados para confiar (consulte Administración de certificados y credenciales.) Cuando no se selecciona esta opción, se presenta al usuario una lista de todos los certificados del sistema del usuario.

## Configurar marcas de agua dinámicas {#configure-dynamic-watermarks}

Con Document Security, puede configurar los valores predeterminados de la opción de marca de agua dinámica que puede aplicar al crear directivas. Una *marca de agua* es una imagen que se superpone sobre el texto del documento. Resulta útil para rastrear el contenido de un documento y puede ayudar a identificar el uso ilegal del contenido.

Una marca de agua dinámica puede constar de texto compuesto por variables definidas, como ID de usuario y fecha y texto personalizado, o contenido enriquecido en una PDF. Puede configurar marcas de agua con varios elementos, cada uno con su propia posición y formato.

Las marcas de agua no se pueden editar y, por lo tanto, son un método más seguro para garantizar la confidencialidad del contenido del documento. Las marcas de agua dinámicas también garantizan que una marca de agua muestre suficiente información específica del usuario como para actuar como elemento disuasorio para distribuir aún más el documento.

La marca de agua que especifica una directiva aparece en el documento protegido por una directiva cuando un destinatario ve o imprime el documento. A diferencia de las marcas de agua permanentes, una marca de agua dinámica nunca se guarda en el documento, lo que proporciona la flexibilidad necesaria al implementar un documento en un entorno de intranet para garantizar que la aplicación de visualización muestre la identidad del usuario específico. Además, si un documento tiene varios usuarios, el uso de la marca de agua dinámica significa que puede utilizar un documento en lugar de varias versiones, cada una con una marca de agua diferente. La marca de agua que aparece refleja la identidad del usuario actual.

Observe que las marcas de agua dinámicas son diferentes de las marcas de agua que los usuarios pueden agregar directamente al documento en Acrobat. El resultado es que puede tener dos marcas de agua en un documento protegido por una directiva.

### Consideraciones al crear marcas de agua {#considerations-when-creating-watermarks}

Puede crear marcas de agua dinámicas con varios elementos de marca de agua con cada elemento especificado como texto o PDF. Puede incluir hasta cinco elementos en una marca de agua.

Si elige una marca de agua basada en texto, puede especificar varios elementos dentro de la marca de agua con varias entradas de texto y especificar la posición de cada elemento. Asigne nombres descriptivos a estos elementos, como encabezado, pie de página, etc.

Por ejemplo, si desea especificar texto diferente en el encabezado, pie de página, márgenes y en todo el documento como marca de agua, cree varios elementos de marca de agua y especifique sus posiciones. Si desea que el ID de usuario del usuario y la fecha actual de acceso al documento aparezcan en el encabezado, el nombre de la directiva en el margen derecho y un texto personalizado &quot;CONFIDENCIAL&quot; aparezcan diagonalmente en el documento, defina elementos de marca de agua independientes con texto como tipo y especifique su formato y posición. Cuando la marca de agua se aplica a un documento, todos los elementos de la marca de agua se aplican al documento al mismo tiempo, en el orden en que se agregan a la marca de agua.

Normalmente, las marcas de agua basadas en PDF se utilizan para incluir contenido gráfico como logotipos o símbolos especiales como derechos de autor o marcas comerciales registradas.

Puede cambiar los límites del número de elementos de marca de agua y el tamaño del archivo PDF modificando el archivo de configuración de Document Security. Consulte [Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Tenga en cuenta lo siguiente al configurar las marcas de agua:

* No puede utilizar un documento de PDF protegido por contraseña como elemento de marca de agua. Sin embargo, si la marca de agua que crea contiene otros elementos que no están protegidos con contraseña, se aplicarán como parte de la marca de agua.
* Puede cambiar el tamaño máximo del archivo PDF que desee utilizar como elemento de marca de agua. Sin embargo, los documentos de PDF grandes que se utilizan como marcas de agua degradan el rendimiento durante la sincronización sin conexión de los documentos aplicados con dichas marcas de agua. Consulte [Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Solo se utiliza la primera página del PDF seleccionado como marca de agua. Asegúrese de que la información que desea que aparezca como marca de agua esté disponible en la primera página.
* Aunque puede especificar la escala del documento de PDF, tenga en cuenta el tamaño de página y el diseño de PDF si va a utilizarlo como marca de agua en el encabezado, el pie de página o los márgenes.
* Cuando especifique el nombre de la fuente, introduzca el nombre correctamente. Los formularios AEM Forms sustituyen la fuente especificada si no está presente en el equipo cliente donde se abre el documento.
* Si seleccionó texto como contenido de marca de agua, al especificar la opción de escala como Ajustar a página no funcionará con páginas que tengan un ancho diferente.
* Cuando especifique la posición de los elementos de marca de agua, asegúrese de que no haya más de un elemento con la misma posición. Si dos elementos de marca de agua tienen la misma posición, como el centro, aparecen superpuestos en el documento y en el orden en que se agregaron a la marca de agua.
* Al especificar el tamaño y el tipo de fuente, asegúrese de que la longitud del texto sea completamente visible dentro de la página. El contenido del texto se traslada a nuevas líneas, por lo que el contenido de la marca de agua que pretendía que estuviera presente en los márgenes podría superponerse a las áreas de contenido de las páginas. Sin embargo, si el documento se abre en Acrobat 9, el texto situado más allá de la línea única se trunca.

### Limitaciones de las marcas de agua dinámicas {#limitations-of-dynamic-watermarks}

Es posible que algunas aplicaciones cliente no admitan marcas de agua dinámicas. Consulte la Ayuda de las extensiones de Acrobat Reader DC apropiadas. Además, tenga en cuenta lo siguiente sobre las versiones de Acrobat que admiten marcas de agua dinámicas:

* No puede utilizar un documento de PDF protegido por contraseña como elemento de marca de agua.
* Las versiones de Acrobat y Adobe Reader anteriores a la 10 no admiten las siguientes funciones de marca de agua:

   * Marcas de agua PDF
   * Varios elementos en la marca de agua (texto/PDF)
   * Opciones avanzadas como intervalo de páginas u opciones de visualización
   * Opciones de formato de texto como la fuente especificada, el nombre de la fuente y el color. Sin embargo, las versiones anteriores de Acrobat y Reader mostrarán el contenido de texto con la fuente y el color predeterminados.

* Acrobat 9.0 y versiones anteriores: Acrobat 9.0 y versiones anteriores no admiten nombres de directivas en marcas de agua dinámicas. Si Acrobat 9.0 abre un documento protegido por una directiva con una marca de agua dinámica que incluye un nombre de directiva y otros datos dinámicos, la marca de agua se muestra sin el nombre de la directiva. Si la marca de agua dinámica incluye solo el nombre de la directiva, Acrobat muestra un mensaje de error

### Agregar una plantilla de marca de agua dinámica {#add-a-dynamic-watermark-template}

Puede crear plantillas de marcas de agua dinámicas. Estas plantillas siguen estando disponibles como opción de configuración para las directivas que crean los administradores o los usuarios.

>[!NOTE]
>
>La información de configuración de marca de agua dinámica no se captura con el resto de la información de configuración al exportar un archivo de configuración.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Marcas de agua.
1. Haga clic en Nuevo.
1. En el cuadro Nombre, escriba un nombre para la nueva marca de agua.

   ***nota &#x200B;**: no se pueden utilizar algunos caracteres especiales en los nombres o descripciones de marcas de agua o elementos de marcas de agua. Vea las restricciones enumeradas en [Consideraciones para editar directivas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. En Nombre, junto al signo más, escriba un nombre significativo en el elemento de marca de agua, como Encabezado, agregue una descripción y expanda el signo más para mostrar las opciones.
1. En Source, seleccione el tipo de marca de agua como Texto o PDF.
1. Si ha seleccionado Texto, haga lo siguiente:

   * Seleccione los tipos de marcas de agua que desea incluir. Si selecciona Texto personalizado, en el cuadro adyacente, escriba el texto que se mostrará para la marca de agua. Tenga en cuenta la longitud del texto que aparecerá como marca de agua.
   * Especifique las propiedades de formato de texto, como el nombre de la fuente, el tamaño de fuente, el color de primer plano y el color de fondo del contenido del texto de la marca de agua. Especifique el color de primer plano y de fondo como valores hexadecimales.

     ***nota &#x200B;**: Si selecciona la opción de escalado como Ajustar a página, la propiedad de tamaño de fuente no estará disponible para la edición.*

1. Si seleccionó PDF para las opciones de marca de agua enriquecida, haga clic en **Examinar** junto a Seleccionar marca de agua PDF para seleccionar el documento de PDF que desea utilizar como marca de agua.

   ***nota &#x200B;**: no use un documento de PDF protegido por contraseña. Si especifica un PDF protegido por contraseña como elemento de marca de agua, la marca de agua no se aplicará.*

1. En Usar como fondo, seleccione Sí o No.

   **nota**: actualmente, la marca de agua aparece en primer plano independientemente de esta configuración.

1. Para controlar dónde se muestra la marca de agua en el documento, configure las opciones Alineación vertical y Alineación horizontal.
1. Seleccione Ajustar a página o seleccione % y escriba un porcentaje en el cuadro. El valor debe ser un número entero, no una fracción. Para configurar el tamaño de la marca de agua, puede utilizar un valor que sea el porcentaje de la página o establecer la marca de agua para que se ajuste al tamaño de la página.
1. En el cuadro Rotación, escriba los grados que desea girar la marca de agua. El rango va de -180 a 180. Utilice un valor negativo para girar la marca de agua en sentido contrario a las agujas del reloj. El valor debe ser un número entero, no una fracción.
1. En el cuadro Opacidad, escriba un porcentaje. Use un número entero, no una fracción.
1. En Opciones avanzadas, configure lo siguiente:

   **Opciones de intervalo de páginas**

   Establezca el intervalo de páginas donde se debe mostrar la marca de agua. Escriba la página de inicio como 1 y la página final como -1 para que todas las páginas estén marcadas con la marca de agua.

   **Opciones de visualización**

   Seleccione dónde desea que aparezca la marca de agua. De forma predeterminada, la marca de agua aparece tanto en la copia flexible (en línea) como en la impresa (impresa).

1. Haga clic en **Nuevo** en Elementos de filigrana para agregar más elementos de filigrana si es necesario.
1. Haga clic en Aceptar.

### Edición de una plantilla de marca de agua dinámica {#edit-a-dynamic-watermark-template}

1. En la consola de administración, haga clic en Servicios > Document Security > Configuración > Marcas de agua.
1. Haga clic en la marca de agua adecuada de la lista.
1. En la página Editar marcas de agua, cambie la configuración según sea necesario.
1. Haga clic en Aceptar.

### Eliminar una plantilla de marca de agua dinámica {#delete-a-dynamic-watermark-template}

Cuando se elimina una marca de agua dinámica, ya no está disponible para agregarla a una directiva nueva. Sin embargo, la marca de agua permanece en las directivas existentes que la utilizan actualmente y los documentos que la directiva protege actualmente siguen mostrando la marca de agua dinámica hasta que usted o un usuario edita la directiva que contiene la marca de agua eliminada. Una vez editada la directiva, la marca de agua ya no se aplica. Aparece un mensaje que indica que la marca de agua existente se elimina en la directiva y el usuario puede seleccionar otra para reemplazarla.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Marcas de agua.
1. Seleccione la casilla de verificación situada junto a la marca de agua adecuada y haga clic en Eliminar.
1. Haga clic en Aceptar.

## Configuración del registro de usuarios invitados {#configuring-invited-user-registration}

Los usuarios externos a su organización pueden registrarse en Document Security. Los usuarios invitados que se registren y activen sus cuentas pueden iniciar sesión en Document Security utilizando su dirección de correo electrónico y la contraseña que crean al registrarse. Los usuarios invitados registrados pueden utilizar documentos protegidos por directivas para los que tienen permisos.

Cuando se activan los usuarios invitados, estos se convierten en usuarios locales. Los usuarios locales se pueden configurar y administrar utilizando el área Usuarios invitados y locales. (Consulte [Administración de cuentas de usuarios invitados y locales](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

Según las capacidades que habilite para los usuarios invitados, también podrán utilizar estas funciones de seguridad de documentos:

* Aplicar directivas a documentos
* Creación de políticas
* Añadir usuarios invitados a las directivas

Document Security genera automáticamente un correo electrónico de invitación de registro cuando se producen los siguientes eventos a menos que el usuario ya esté en el directorio LDAP de origen o se le haya invitado anteriormente a registrarse:

* Un usuario existente agrega un usuario invitado a una directiva
* Un administrador añade una cuenta de usuario invitada en la página Registro de usuarios invitados

El correo electrónico de registro contiene un vínculo a una página de registro e información sobre cómo registrarse. Una vez que el usuario invitado se registra, Document Security emite un correo electrónico de activación con un vínculo a una página de activación. Cuando se activa, la cuenta sigue siendo válida hasta que se desactiva o elimina.

Si activa el registro integrado, debe especificar el servidor SMTP, los detalles del correo electrónico de registro, las funcionalidades de acceso y restablecer la información del correo electrónico de la contraseña solo una vez. Antes de habilitar el registro integrado, asegúrese de haber creado un dominio local en Administración de usuarios y de haber asignado la función &quot;Invitar usuario&quot; de Document Security a los usuarios y grupos adecuados de su organización. (Consulte [Agregar un dominio local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) y [Crear y configurar funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Si no usa el registro integrado, debe tener su propio sistema de registro de usuario creado con AEM Forms SDK. Consulte la ayuda en &quot;Desarrollo de SPI para formularios AEM&quot; en [Programación con formularios AEM](/help/forms/developing/introducing-java-api-soap-quick.md). Si no utiliza la opción Registro integrado, se recomienda configurar un mensaje en el correo electrónico de activación y en la pantalla de inicio de sesión del cliente para notificar a los usuarios cómo ponerse en contacto con el administrador para obtener una nueva contraseña o para obtener otra información.

**Habilitar y configurar el registro de usuarios invitados**

De forma predeterminada, el proceso de registro de usuarios invitados está desactivado. Puede habilitar y deshabilitar el registro de usuarios invitados para Document Security, según sea necesario.

1. En la consola de administración, haga clic en Servicios > Document Security > Configuración > Registro de usuario invitado.
1. Seleccione Habilitar el registro de usuarios invitados.
1. (Opcional) Actualice la configuración de registro de usuario invitado según sea necesario:

   * [Excluir o incluir un usuario o grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parámetros de servidor y cuenta de registro](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configuración de correo electrónico de invitación de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configuración de correo electrónico de activación](configuring-client-server-options.md#activation-email-settings)
   * [Configurar un correo electrónico de restablecimiento de contraseña](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) En Registro integrado, seleccione Sí para activar esta opción. Si no habilita el registro integrado, debe configurar su propio sistema de registro de usuario.
1. Haga clic en Aceptar.

### Excluir o incluir un usuario o grupo externo {#exclude-or-include-an-external-user-or-group}

Puede restringir el registro con Document Security para determinados usuarios o grupos de usuarios externos. Esta opción es útil, por ejemplo, para permitir el acceso a un determinado grupo de usuarios, pero excluir a personas específicas que forman parte del grupo.

La siguiente configuración se encuentra en el área Filtro de restricción de correo electrónico de la página Registro de usuario invitado.

**Exclusión:** Escriba la dirección de correo electrónico de un usuario o grupo que desee excluir. Para excluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para excluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para excluir todos los usuarios del dominio example.com, escriba &ast;.example.com.

**Inclusión:** Escriba la dirección de correo electrónico de un usuario o grupo que desee incluir. Para incluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para incluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para incluir a todos los usuarios en el dominio example.com, escriba &ast;.example.com.

### Parámetros de servidor y cuenta de registro {#server-and-registration-account-parameters}

La configuración siguiente se encuentra en el área Configuración general de la página Registro de usuario invitado.

**Host SMTP:** El nombre de host del servidor SMTP. El servidor SMTP gestiona los avisos de correo electrónico salientes para registrar y activar cuentas de usuario invitadas.

Si es necesario para el host SMTP, escriba la información necesaria en los cuadros Nombre de cuenta de servidor SMTP y Contraseña de cuenta de servidor SMTP para conectarse al servidor SMTP. Algunas organizaciones no aplican este requisito. Si necesita información, consulte al administrador del sistema.

**Nombre de clase de socket del servidor SMTP:** Nombre de clase de socket para el servidor SMTP. Por ejemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de contenido de correo electrónico:** Tipo MIME aceptado como texto/sin formato o texto/html.

**Codificación de correo electrónico:** Formato de codificación que se utilizará al enviar mensajes de correo electrónico. Puede especificar cualquier codificación, por ejemplo, UTF-8 para Unicode o ISO-8859-1 para latín. El valor predeterminado es UTF-8.

**Dirección de correo electrónico de redirección:** Cuando especifica una dirección de correo electrónico para esta configuración, cualquier nueva invitación se envía a la dirección proporcionada. Esta configuración puede resultar útil para realizar pruebas.

**Usar dominios locales:** Seleccione el dominio apropiado. En una instalación nueva, asegúrese de crear el dominio mediante Administración de usuarios. Si se trata de una actualización, durante la misma se creó un dominio de usuario externo que se puede utilizar.

**Usar SSL para el servidor SMTP:** Seleccione esta opción para habilitar SSL para el servidor SMTP.

**Mostrar vínculo de inicio de sesión en la página de registro:** Muestra un vínculo de inicio de sesión en la página de registro que se muestra a los usuarios invitados.

**Para habilitar la seguridad de la capa de transporte (TLS) para el servidor SMTP**

1. Abra la consola de administración.

   La ubicación predeterminada de la consola de administración es `https://<server>:<port>/adminui`.

1. Vaya a Inicio > Servicios > Document Security > Configuración > Registro de usuario invitado.
1. En el Registro de usuarios invitados, especifique todos los ajustes de configuración y, a continuación, haga clic en Aceptar.

   >[!NOTE]
   >
   >Si utiliza Microsoft Office 365 como servidor SMTP para enviar invitaciones para el registro de usuarios, utilice la siguiente configuración:
   >
   >**Host SMTP:** smtp.office365.com
   >**Puerto:** 587

1. A continuación, debe actualizar el archivo config.xml. Consulte [Configuración para habilitar SMTP para la seguridad de la capa de transporte (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Si realiza cambios en las opciones de registro de usuarios invitados, el archivo config.xml se sobrescribe y TLS se desactiva. Si sobrescribe los cambios, debe realizar el paso anterior para reactivar la compatibilidad con TLS para el registro de usuarios invitados.

### Configuración de correo electrónico de invitación de registro {#registration-invitation-email-settings}

Document Security envía automáticamente un correo electrónico de invitación de registro cuando crea una cuenta de usuario invitada o cuando un usuario existente agrega un destinatario externo que no se ha registrado anteriormente o que se le ha invitado a registrarse en una directiva. El correo electrónico contiene un vínculo que el destinatario puede utilizar para acceder a la página de registro e introducir información personal de la cuenta, incluidos el nombre de usuario y la contraseña. La contraseña puede ser cualquier combinación de ocho caracteres.

Cuando el destinatario activa la cuenta, el usuario se convierte en un usuario local.

Los siguientes ajustes se encuentran en el área Configuración del correo electrónico de invitación de la página Registro de usuario invitado.

**De:** Dirección de correo electrónico desde la que se envía el mensaje de correo electrónico de invitación. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de invitación.

**Tiempo de espera:** Número de días tras los cuales caduca la invitación de registro si el usuario externo no se registra. El valor predeterminado es 30 días.

**Mensaje:** El texto que aparece en el cuerpo del mensaje que invita al usuario a registrarse.

### Configuración de correo electrónico de activación {#activation-email-settings}

Después de que los usuarios invitados se registren, Document Security enviará un correo electrónico de activación. El correo electrónico de activación contiene un vínculo a la página de activación de la cuenta, en la que los usuarios pueden activar su cuenta. Cuando se activan las cuentas, los usuarios pueden iniciar sesión en Document Security utilizando su dirección de correo electrónico y la contraseña que crearon al registrarse.

Cuando el destinatario activa la cuenta de usuario, este se convierte en un usuario local.

Las siguientes opciones se encuentran en el área Configuración del correo electrónico de activación de la página Registro de usuario invitado.

>[!NOTE]
>
>También se recomienda configurar un mensaje en la pantalla de inicio de sesión para aconsejar a los usuarios externos cómo ponerse en contacto con su administrador para obtener una nueva contraseña o para obtener más información.

**De:** Dirección de correo electrónico desde la que se envía el correo electrónico de activación. Esta dirección de correo electrónico recibe notificaciones de envío fallidas del host de correo electrónico del registrante, así como cualquier mensaje que el destinatario envíe en respuesta al correo electrónico de registro. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de activación.

**Tiempo de espera:** Número de días tras los cuales caduca la invitación de activación si el usuario no activa la cuenta. El valor predeterminado es 30 días.

**Mensaje:** El texto que aparece en el cuerpo del mensaje contiene un mensaje que indica que es necesario activar la cuenta de usuario del destinatario. También es posible que desee incluir información como cómo ponerse en contacto con un administrador para obtener una nueva contraseña.

### Configurar un correo electrónico de restablecimiento de contraseña {#configure-a-password-reset-email}

Si tiene que restablecer la contraseña de un usuario invitado, se genera un correo electrónico de confirmación que invita al usuario a elegir una nueva contraseña. No se puede determinar la contraseña de un usuario; si la olvida, debe restablecerla.

La siguiente configuración se encuentra en el área Restablecer correo electrónico de contraseña de la página Registro de usuario invitado.

**De:** Dirección de correo electrónico desde la que se envía el mensaje de correo electrónico para restablecer la contraseña. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico restablecido.

**Mensaje:** El texto que aparece en el cuerpo del mensaje contiene un mensaje que indica que se restablece la contraseña de usuario externo del destinatario.

## Permitir que los usuarios y grupos creen directivas {#enable-users-and-groups-to-create-policies}

La página Configuración tiene un vínculo a la página Mis directivas, donde puede especificar qué usuarios finales pueden crear mis directivas y qué usuarios y grupos están visibles en los resultados de búsqueda. La página Mis directivas tiene dos pestañas:

**Ficha Crear directivas:** Use para configurar permisos de usuario para crear directivas personalizadas.

**Ficha Usuarios y grupos visibles:** Use para controlar qué usuarios y grupos son visibles en los resultados de búsqueda de usuarios. El superusuario o el administrador de conjuntos de directivas deben seleccionar y agregar dominios, creados en Administración de usuarios, al usuario y grupo visibles para cada conjunto de directivas. Esta lista es visible para el coordinador de conjuntos de directivas y se utiliza para establecer límites en los dominios que el coordinador de conjuntos de directivas puede examinar al elegir usuarios para agregarlos a las directivas.

Antes de conceder permiso a los usuarios para crear directivas personalizadas, considere cuánto acceso o control desea que tengan los usuarios individuales. Además, tenga en cuenta la exposición que desea que estén sus usuarios y grupos al hacerlos visibles para las búsquedas.

### Especificar usuarios y grupos que pueden crear directivas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique qué usuarios y grupos pueden crear directivas personalizadas. Este permiso se puede establecer en los niveles de usuario y grupo. La funcionalidad de búsqueda busca usuarios y grupos en la base de datos de Administración de usuarios.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Mis directivas.
1. En la página Mis directivas, haga clic en la ficha Crear directivas y, a continuación, haga clic en Agregar usuarios y grupos.
1. En el cuadro Buscar, escriba el nombre de usuario o la dirección de correo electrónico del usuario o grupo que está buscando. Si no dispone de esta información, deje vacía la casilla. También puede escribir un nombre parcial o una dirección de correo electrónico, como cuando sólo conoce las dos primeras letras de un nombre de usuario.
1. En la lista Usar, seleccione los parámetros de búsqueda Nombre o Correo electrónico.
1. En la lista Tipo, seleccione Grupo o Usuario para limitar la búsqueda.
1. En la lista En, seleccione el dominio que desea buscar. Si no conoce el dominio del usuario o grupo, seleccione Todos los dominios.
1. En la lista Mostrar, especifique el número de resultados de búsqueda que desea mostrar por página y, a continuación, haga clic en Buscar.
1. Para agregar usuarios y grupos a Mis directivas, active la casilla de verificación de cada usuario y grupo que desee agregar.
1. Haga clic en Agregar y, a continuación, en Aceptar.

Los usuarios y grupos seleccionados ahora tienen permiso para crear directivas personalizadas.

### Quitar el permiso Crear directivas personalizadas de un usuario o grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. En la página Document Security, haga clic en Configuración > Mis directivas.
1. En la página Mis directivas, haga clic en la ficha Crear directivas. Se muestran los usuarios y grupos con permisos para crear directivas personalizadas.
1. Active la casilla de verificación situada junto a los usuarios y grupos que desea quitar de este permiso.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

### Especificar usuarios y grupos visibles en las búsquedas {#specify-users-and-groups-that-are-visible-in-searches}

Cuando los usuarios administran sus directivas personalizadas, pueden buscar usuarios y grupos para agregarlos a sus directivas. Especifique los dominios desde los que los usuarios y grupos son visibles en estas búsquedas.

1. En la página Document Security, haga clic en Configuración > Mis directivas.
1. En la página Mis directivas, haga clic en la ficha Usuarios y grupos visibles.
1. Para hacer visibles los usuarios y grupos de un dominio, haga clic en Agregar dominios, seleccione los dominios y haga clic en Agregar. Para quitar un dominio, seleccione la casilla que hay junto al nombre de dominio y haga clic en Eliminar.

## Edición manual del archivo de configuración de Document Security {#manually-editing-the-document-security-configuration-file}

Puede importar y exportar la información de configuración almacenada en la base de datos de Document Security. Por ejemplo, puede que desee realizar una copia de seguridad de la información de configuración cuando pase de un entorno de ensayo a un entorno de producción, o puede que desee editar las opciones avanzadas que solo se pueden configurar al editar este archivo.

Puede realizar los siguientes cambios con el archivo de configuración:

[Mostrar los permisos de CATIA al crear y editar directivas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especificar un período de tiempo de espera para la sincronización sin conexión](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Denegar servicios de seguridad de documentos para aplicaciones específicas](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Cambiar los parámetros de configuración de filigrana](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desactivación de vínculos externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>La importación del archivo de configuración reconfigura el sistema en función de la información contenida en el archivo. Las excepciones son la configuración dinámica de marcas de agua y la información de eventos personalizados, que no se guardan con el archivo de configuración exportado. Configure esta información manualmente en el nuevo sistema. Solamente un administrador del sistema o un consultor de servicios profesionales familiarizado con Document Security y XML debe modificar el contenido de un archivo de configuración, por ejemplo, para volver a configurar una configuración dañada o ajustar los parámetros de un escenario de implementación empresarial determinado.

**Exportar un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > Document Security 11 > Configuración > Configuración manual.
1. Haga clic en Exportar y guarde el archivo de configuración en otra ubicación. El nombre de archivo predeterminado es config.xml.
1. Haga clic en Aceptar.
1. Antes de cambiar el archivo de configuración, realice una copia de seguridad en caso de que necesite volver.

**Importar un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > Document Security 11 > Configuración > Configuración manual.
1. Haga clic en Examinar para ir al archivo de configuración y, a continuación, haga clic en Importar. No puede escribir la ruta de acceso directamente en el cuadro Nombre de archivo.
1. Haga clic en Aceptar.

### Especificar un período de tiempo de espera para la sincronización sin conexión {#specify-a-timeout-period-for-offline-synchronization}

La seguridad de los documentos permite a los usuarios abrir y utilizar documentos protegidos cuando no están conectados al servidor de seguridad de los documentos. La aplicación cliente del usuario debe sincronizarse regularmente con el servidor para mantener los documentos válidos para el uso sin conexión. La primera vez que los usuarios abren un documento protegido, se les pregunta si su equipo debe estar autorizado para realizar la sincronización periódica de clientes.

De forma predeterminada, la sincronización se produce automáticamente cada cuatro horas y según sea necesario cuando un usuario está conectado al servidor de Document Security. Si el período sin conexión de un documento caduca mientras el usuario está sin conexión, el usuario debe volver a conectarse al servidor para permitir que la aplicación cliente se sincronice con el servidor.

En el fichero de configuración de Document Security, se puede especificar la frecuencia por defecto de la sincronización automática en segundo plano. Esta configuración actúa como el período de tiempo de espera predeterminado para las aplicaciones cliente, a menos que el cliente establezca explícitamente su propio valor de tiempo de espera.

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo `PolicyServer`. En ese nodo, busque el nodo `ServerSettings`.
1. En el nodo `ServerSettings`, agregue esta entrada y, a continuación, guarde el archivo:

   `<entry key="BackgroundSyncFrequency" value="`*hora* `"/>`

   donde *time* es el número de segundos entre sincronizaciones automáticas en segundo plano. Si envió este valor a `0`, siempre se produce la sincronización. El valor predeterminado es `14400` segundos (cada cuatro horas).

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Denegar servicios de seguridad de documentos para aplicaciones específicas {#denying-document-security-services-for-specific-applications}

Puede configurar Document Security para denegar servicios a aplicaciones que cumplan criterios específicos. Los criterios pueden especificar un único atributo, como un nombre de plataforma, o varios conjuntos de atributos. Esta función puede ayudarle a controlar las solicitudes que debe gestionar Document Security. Estas son algunas aplicaciones de esta función:

* **Protección de ingresos:** Es posible que desee denegar el acceso a cualquier aplicación cliente que no admita las convenciones de ingresos.
* **Compatibilidad de aplicaciones:** Es posible que algunas aplicaciones sean incompatibles con las directivas o el comportamiento del servidor de Document Security.

Cuando las aplicaciones cliente intentan establecer un vínculo con Document Security, proporcionan información de la aplicación, la versión y la plataforma. Document Security compara esta información con la configuración de denegaciones que obtiene del archivo de configuración de Document Security.

La configuración de Denegaciones puede contener varios conjuntos de condiciones de denegación. Si todos los atributos de un conjunto coinciden, se deniega a la aplicación solicitante el acceso a los servicios de Document Security.

La función de denegación de servicio requiere que las aplicaciones cliente utilicen la versión 8.2 o posterior de Document Security C++ Client SDK. Los siguientes productos de Adobe proporcionan información del producto al solicitar servicios de Document Security:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard y versiones posteriores
* Adobe Reader 9.0 y versiones posteriores
* Extensiones de Acrobat Reader DC para Microsoft Office 8.2 y versiones posteriores

Las aplicaciones cliente utilizan la API de cliente del SDK cliente de C++ de Document Security para solicitar servicios a Document Security. Las solicitudes de la API del cliente incluyen información de la versión de la plataforma y SDK (precompilada en la API del cliente) e información del producto obtenida de la aplicación del cliente.

Las aplicaciones cliente o los complementos proporcionan información del producto en su implementación de una función de devolución de llamada. La aplicación proporciona la siguiente información:

* Nombre del integrador
* Versión de Integrator
* Familia de aplicaciones
* Nombre de aplicación
* Versión de aplicación

Si alguna información no es aplicable, la aplicación cliente deja en blanco el campo correspondiente.

Varias aplicaciones de Adobe incluyen información de productos al solicitar servicios de seguridad de documentos, incluidas las extensiones de Acrobat, Adobe Reader y Acrobat Reader DC para Microsoft Office.

**Acrobat y Adobe Reader**

Cuando Acrobat o Adobe Reader solicitan un servicio a Document Security, proporciona la siguiente información del producto:

* **Integrador:** Adobe Systems, Inc.
* **Versión de Integrator:** 1.0
* **Familia de aplicaciones:** Acrobat
* **Nombre de aplicación:** Acrobat
* **Versión de aplicación:** 9.0.0

**Extensiones de Acrobat Reader DC para Microsoft Office**

Extensiones de Acrobat Reader DC para Microsoft Office es un complemento utilizado con los productos de Microsoft Office Microsoft Word, Microsoft Excel y Microsoft PowerPoint. Cuando solicita un servicio, proporciona la siguiente información:

* **Integrador:** Adobe Systems Incorporated
* **Versión de Integrator:** 8.2
* **Familia de aplicaciones:** extensiones de Acrobat Reader DC para Microsoft Office
* **Nombre de aplicación:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versión de la aplicación:** 2003 o 2007

**Configurar Document Security para denegar servicios a aplicaciones específicas**

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo `PolicyServer`. Agregue un nodo `ClientVersionRules` como elemento secundario inmediato del nodo `PolicyServer`, si no existe:

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   donde:

   `SDKPlatforms` especifica la plataforma que hospeda la aplicación cliente. Los valores posibles son:

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` especifica la versión de la API de cliente de C++ de Document Security utilizada por la aplicación cliente. Por ejemplo, `"8.2"`.

   La API de cliente define `APPFamilies`.

   `AppName` especifica el nombre de la aplicación cliente. Las comas se utilizan como separadores de nombres. Para incluir una coma en un nombre, escríbalo con un carácter de barra invertida (\). Por ejemplo, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` especifica la versión de la aplicación cliente.

   `Integrators` especifica el nombre de la compañía o el grupo que desarrolló el complemento o la aplicación integrada.

   `IntegratorVersions` es la versión del complemento o de la aplicación integrada.

1. Para cada conjunto adicional de datos de denegación, agregue otro elemento *MyEntryName*.
1. Guarde el archivo de configuración.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Ejemplos**

En este ejemplo, se deniega el acceso a todos los clientes de Windows.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

En este ejemplo, se deniega el acceso a Mi aplicación versión 3.0 y a Mi otra aplicación versión 2.0. Se utiliza la misma dirección URL de información de denegación independientemente del motivo de la denegación.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

En este ejemplo, se deniegan todas las solicitudes de una instalación de Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 de extensiones de Acrobat Reader DC para Microsoft Office.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### Cambiar los parámetros de configuración de filigrana {#change-the-watermark-configuration-parameters}

De forma predeterminada, se puede especificar un máximo de cinco elementos en una marca de agua. Además, el tamaño máximo de archivo del documento de PDF que desea utilizar como marca de agua está limitado a 100 KB. Puede cambiar estos parámetros en el archivo config.xml.

***nota &#x200B;**: debe cambiar estos parámetros con precaución.*

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo `ServerSettings`.
1. En el nodo `ServerSettings`, agregue las siguientes entradas y guarde el archivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La primera entrada, *tamaño máximo de archivo* es el tamaño máximo de archivo (en KB) permitido para un elemento de marca de agua de PDF. El valor predeterminado es 100 KB.

   La segunda entrada, *max elements*, es el número máximo de elementos permitidos en una marca de agua. El valor predeterminado es 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Desactivación de vínculos externos {#disabling-external-links}

Muchos usuarios de Document Security no tienen acceso a vínculos externos como **www.adobe.com** mientras usan las interfaces de usuario de Right Management:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Los siguientes cambios en config.xml desactivan todos los vínculos externos de las interfaces de usuario de Right Management.

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo `DisplaySettings`.
1. Para deshabilitar todos los vínculos externos, en el nodo `DisplaySettings`, agregue la siguiente entrada y, a continuación, guarde el archivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configuración para habilitar SMTP para la seguridad de la capa de transporte (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Los siguientes cambios en config.xml habilitan la compatibilidad con TLS para la función Registro de usuarios invitados.

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo `DisplaySettings`.
1. Busque el siguiente nodo: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Establezca el valor de la clave `SmtpUseTls` en el nodo `ExternalUser` en **true**.
1. Establezca el valor de la clave `SmtpUseSsl` en el nodo `ExternalUser` en **false**.
1. Guarde `config.xml`.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Deshabilitar extremos de SOAP para documentos de Document Security {#disable-soap-endpoints-for-document-security-documents}

Los siguientes cambios en config.xml para deshabilitar los extremos de SOAP para los documentos de Document Security.

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el siguiente nodo: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. En el nodo DRM, busque el nodo `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para deshabilitar los extremos de SOAP para los documentos de Document Security, establezca el atributo value en **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Guarde `config.xml`.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Aumento de la escalabilidad del servidor de Document Security {#increasingscalability}

De forma predeterminada, al sincronizar un documento para su uso sin conexión, junto con la información del documento actual, los clientes de Document Security recuperan la información de directivas, marcas de agua, licencias y actualizaciones de revocación de todos los demás documentos a los que el usuario tiene acceso. Si estas actualizaciones y la información no se sincronizan con el cliente, es posible que un documento abierto en modo sin conexión se siga abriendo con información anterior sobre directivas, marcas de agua y revocaciones.

Puede aumentar la escalabilidad del servidor de Document Security limitando la información que se envía al cliente. La reducción de la cantidad de información enviada al cliente mejora la escalabilidad, reduce el tiempo de respuesta y mejora el rendimiento del servidor. Realice los siguientes pasos para aumentar la escalabilidad:

1. Exporte el archivo de configuración de Document Security. (Consulte [Edición manual del archivo de configuración de Document Security](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra el archivo de configuración en un editor y busque el nodo ServerSettings.
1. En el nodo ServerSettings, establezca el valor de la propiedad `DisableGlobalOfflineSynchronizationData`en `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Cuando se establece en true, el servidor de seguridad de documentos envía información solo para el documento actual y la información del resto de los documentos (los demás documentos a los que un usuario tiene acceso) no se envía al cliente.

   >[!NOTE]
   >
   >De manera predeterminada, el valor de la clave `DisableGlobalOfflineSynchronizationData` está establecido en `false`.

1. Guarde e importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
