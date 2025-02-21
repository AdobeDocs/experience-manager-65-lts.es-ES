---
title: Activar el inicio de sesión único en AEM Forms
description: Obtenga información sobre cómo habilitar el inicio de sesión único (SSO) mediante encabezados HTTP y SPNEGO.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# Activar el inicio de sesión único en AEM Forms{#enabling-single-sign-on-in-aem-forms}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los formularios de AEM proporcionan dos formas de habilitar el inicio de sesión único (SSO): encabezados HTTP y SPNEGO.

Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM Forms no son necesarias y no aparecen si el usuario ya se ha autenticado a través del portal de su empresa.

Si los formularios AEM Forms no pueden autenticar a un usuario mediante cualquiera de estos métodos, se redirigirá al usuario a una página de inicio de sesión.

* [Habilitar SSO mediante encabezados HTTP](#enable-sso-using-http-headers)
* [Habilitar SSO con SPNEGO](#enable-sso-using-spnego)
* [Asignar funciones a usuarios y grupos](#assign-roles-to-users-groups)

## Habilitar SSO mediante encabezados HTTP {#enable-sso-using-http-headers}

Puede utilizar la página Configuración de portal para habilitar el inicio de sesión único (SSO) entre aplicaciones y cualquier aplicación que admita la transmisión de la identidad a través de un encabezado HTTP. Cuando se implementa SSO, las páginas de inicio de sesión del usuario de los formularios AEM Forms no son necesarias y no aparecen si el usuario ya se ha autenticado a través del portal de su empresa.

También puede habilitar SSO mediante SPNEGO. (Consulte [Habilitar SSO con SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego)).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos de portal.
1. Seleccione Sí para activar el SSO. Si selecciona No, el resto de la configuración de la página no estará disponible.
1. Defina las opciones restantes de la página según sea necesario y haga clic en Aceptar:

   * **Tipo de SSO:** (obligatorio) Seleccione el encabezado HTTP para habilitar el SSO mediante encabezados HTTP.
   * **Encabezado HTTP para el identificador del usuario:** (obligatorio) Nombre del encabezado cuyo valor contiene el identificador único del usuario que inició sesión. Administración de usuarios utiliza este valor para buscar el usuario en la base de datos de Administración de usuarios. El valor obtenido de este encabezado debe coincidir con el identificador único del usuario sincronizado desde el directorio LDAP. (Consulte [Configuración de usuario](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **El valor de identificador se asigna al identificador de usuario del usuario en lugar del identificador único del usuario:** Asigna el valor de identificador único del usuario al identificador de usuario. Seleccione esta opción si el identificador único del usuario es un valor binario que no se puede propagar fácilmente a través de encabezados HTTP (por ejemplo, objectGUID si está sincronizando usuarios desde Active Directory).
   * **Encabezado HTTP para el dominio:** (no obligatorio) Nombre del encabezado cuyo valor contiene el nombre de dominio. Utilice esta configuración solo si ningún encabezado HTTP individual identifica de forma exclusiva al usuario. Utilice esta configuración para casos en los que existen varios dominios y el identificador único solo es único dentro de un dominio. En este caso, especifique el nombre del encabezado en este cuadro de texto y especifique la asignación de dominios para varios dominios en el cuadro Asignación de dominios. (Consulte [Edición y conversión de dominios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **Asignación de dominios:** (obligatorio) Especifica la asignación para varios dominios con el formato *header value=domain name*.

     Por ejemplo, considere una situación en la que el encabezado HTTP de un dominio sea domainName y pueda tener valores de domain1, domain2 o domain3. En este caso, utilice la asignación de dominios para asignar los valores domainName a los nombres de dominio de Administración de usuarios. Cada asignación debe estar en una línea diferente:

     domain1=dominioUM1

     domain2=dominioUM2

     domain3=UMdomain3

### Configuración de referentes permitidos {#configure-allowed-referers}

Para ver los pasos para configurar los referentes permitidos, consulte [Configurar referentes permitidos](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

### Asignar funciones a usuarios y grupos

Haga clic para conocer los pasos para [asignar funciones a usuarios y grupos](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups).

## Habilitar SSO con SPNEGO {#enable-sso-using-spnego}

Puede utilizar el Mecanismo de negociación de GSSAPI simple y protegido (SPNEGO) para habilitar el inicio de sesión único (SSO) al usar Active Directory como servidor LDAP en un entorno de Windows. Cuando se habilita el SSO, las páginas de inicio de sesión del usuario de los formularios AEM Forms no son necesarias y no aparecen.

También puede habilitar SSO utilizando encabezados HTTP. (Consulte [Habilitar SSO mediante encabezados HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)).

>[!NOTE]
>
>AEM Forms en JEE no admite la configuración de SSO mediante Kerberos/SPNEGO en varios entornos de dominio secundarios.

1. Decida qué dominio desea utilizar para habilitar SSO. AEM Forms Server y los usuarios deben formar parte del mismo dominio de Windows o dominio de confianza.
1. En Active Directory, cree un usuario que represente al servidor de AEM Forms. (Consulte [Crear una cuenta de usuario](enabling-single-sign-on-aem.md#create-a-user-account).) Si está configurando más de un dominio para utilizar SPNEGO, asegúrese de que las contraseñas de cada uno de estos usuarios sean diferentes. Si las contraseñas no son diferentes, SPNEGO SSO no funciona.
1. Asigne el nombre principal del servicio. (Consulte [Asignar un nombre principal de servicio (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configure el controlador de dominio. (Consulte [Impedir errores de comprobación de integridad Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. Agregue o edite un dominio de empresa como se describe en [Agregar dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains) o [Editar y convertir dominios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Cuando cree o edite el dominio de empresa, realice estas tareas:

   * Agregue o edite un directorio que contenga su información de Active Directory.
   * Añada LDAP como proveedor de autenticación.
   * Agregue Kerberos como proveedor de autenticación. Proporcione la siguiente información en la página Nueva o Editar autenticación para Kerberos:

      * **Proveedor de autenticación:** Kerberos
      * **IP DNS:** Dirección IP DNS del servidor donde se ejecutan los formularios AEM. Puede determinar esta dirección IP ejecutando `ipconfig/all` en la línea de comandos.
      * **Host KDC:** Nombre de host completo o dirección IP del servidor Active Directory utilizado para la autenticación
      * **Usuario de servicio:** El nombre principal de servicio (SPN) pasado a la herramienta KtPass. En el ejemplo utilizado anteriormente, el usuario del servicio es `HTTP/lcserver.um.lc.com`.
      * **Dominio de servicio:** Nombre de dominio para Active Directory. En el ejemplo utilizado anteriormente, el nombre de dominio es `UM.LC.COM.`
      * **Contraseña del servicio:** Contraseña del usuario del servicio. En el ejemplo utilizado anteriormente, la contraseña del servicio es `password`.
      * **Habilitar SPNEGO:** Habilita el uso de SPNEGO para el inicio de sesión único (SSO). Seleccione esta opción.

1. Configure las opciones del explorador del cliente SPNEGO. (Consulte [Configuración del explorador del cliente SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### Crear una cuenta de usuario {#create-a-user-account}

1. En SPNEGO, registre un servicio como usuario en Active Directory en el controlador de dominio para representar formularios de AEM. En el controlador de dominio, vaya al menú Inicio > Herramientas administrativas > Usuarios y equipos de Active Directory. Si Herramientas administrativas no está en el menú Inicio, utilice el Panel de control de Campaign.
1. Haga clic en la carpeta Usuarios para mostrar una lista de usuarios.
1. Haga clic con el botón derecho en la carpeta de usuario y seleccione Nuevo > Usuario.
1. Escriba el Nombre/Apellidos y el Nombre de inicio de sesión del usuario y, a continuación, haga clic en Siguiente. Por ejemplo, establezca los siguientes valores:

   * **Nombre**: umspnego
   * **Nombre de inicio de sesión de usuario**: spnegodemo

1. Escriba una contraseña. Por ejemplo, configúrelo en *password*. Asegúrese de que la opción La contraseña nunca caduca está seleccionada y que no hay otras opciones seleccionadas.
1. Haga clic en Siguiente y, a continuación, en Finalizar.

### Asignar un nombre principal de servicio (SPN) {#map-a-service-principal-name-spn}

1. Obtenga la utilidad KtPass. Esta utilidad se utiliza para asignar un SPN a un REALM. Puede obtener la utilidad KtPass como parte del paquete de herramientas o el kit de recursos de Windows Server. (Consulte [Herramientas de soporte técnico de Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. En un símbolo del sistema, ejecute `ktpass` con los siguientes argumentos:

   `ktpass -princ HTTP/`*host* `@`*REALM* `-mapuser`*usuario*

   Por ejemplo, escriba el siguiente texto:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Los valores que debe proporcionar se describen de la siguiente manera:

   **host:** Nombre completo del servidor de Forms o cualquier dirección URL única. En este ejemplo, se establece en lcserver.um.lc.com.

   **REALM:** dominio de Active Directory para el controlador de dominio. En este ejemplo, se establece en UM.LC.COM. Asegúrese de introducir el dominio en caracteres en mayúsculas. Para determinar el dominio kerberos de Windows 2003, complete los siguientes pasos:

   * Haga clic con el botón derecho en Mi PC y seleccione Propiedades
   * Haga clic en la ficha Nombre de equipo. El valor Nombre de dominio es el nombre de territorio.

   **usuario:** Nombre de inicio de sesión de la cuenta de usuario que creó en la tarea anterior. En este ejemplo, se establece en spnegodemo.

Si aparece este error:

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

intente especificar el usuario como spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Evitar errores de comprobación de integridad de Kerberos {#prevent-kerberos-integrity-check-failures}

1. En el controlador de dominio, vaya al menú Inicio > Herramientas administrativas > Usuarios y equipos de Active Directory. Si Herramientas administrativas no está en el menú Inicio, utilice el Panel de control de Campaign.
1. Haga clic en la carpeta Usuarios para mostrar una lista de usuarios.
1. Haga clic con el botón secundario en la cuenta de usuario que creó en una tarea anterior. En este ejemplo, la cuenta de usuario es `spnegodemo`.
1. Haga clic en Restablecer contraseña.
1. Escriba y confirme la misma contraseña que escribió anteriormente. En este ejemplo, se establece en `password`.
1. Anule la selección de Cambiar contraseña en el siguiente inicio de sesión y haga clic en Aceptar.

### Configuración del explorador del cliente SPNEGO {#configuring-spnego-client-browser-settings}

Para que funcione la autenticación basada en SPNEGO, el equipo cliente debe formar parte del dominio en el que se crea la cuenta de usuario. También debe configurar el explorador del cliente para permitir la autenticación basada en SPNEGO. Además, el sitio que requiere autenticación basada en SPNEGO debe ser de confianza.

Si se obtiene acceso al servidor mediante el nombre del equipo, como https://lcserver:8080, no se requiere ninguna configuración para Internet Explorer. Si escribe una dirección URL que no contiene puntos (&quot;.&quot;), Internet Explorer trata el sitio como un sitio de intranet local. Si utiliza un nombre completo para el sitio, el sitio debe agregarse como sitio de confianza.

**Configurar Internet Explorer 6.x**

1. Vaya a Herramientas > Opciones de Internet y haga clic en la ficha Seguridad.
1. Haga clic en el icono Intranet local y, a continuación, en Sitios.
1. Haga clic en Avanzadas y, en el cuadro Agregar este sitio Web a la zona, escriba la dirección URL del servidor de Forms. Por ejemplo, escriba `https://lcserver.um.lc.com`
1. Haga clic en Aceptar hasta que se cierren todos los cuadros de diálogo.
1. Pruebe la configuración accediendo a la dirección URL del servidor de AEM Forms. Por ejemplo, en el cuadro URL del explorador, escriba `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurar Mozilla Firefox**

1. En el cuadro Dirección URL del explorador, escriba `about:config`

   Aparecerá el cuadro de diálogo about:config - Mozilla Firefox.

1. En el cuadro Filtro, escriba `negotiate`
1. En la lista que se muestra, haga clic en network.Negotiate-auth.trusted-uri y escriba uno de los siguientes comandos según corresponda para su entorno:

   `.um.lc.com`: configura Firefox para permitir SPNEGO para cualquier dirección URL que termine con um.lc.com. Asegúrese de incluir el punto (&quot;.&quot;) al principio.

   `lcserver.um.lc.com`: configura Firefox para permitir SPNEGO solo para su servidor específico. No empiece este valor con un punto (&quot;.&quot;).

1. Pruebe la configuración accediendo a la aplicación. Debe aparecer la página de bienvenida de la aplicación de destino.

Haga clic para conocer los pasos para [asignar funciones a usuarios y grupos](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#assign-roles-to-users-and-groups-assign-roles-to-users-groups).

## Asignar funciones a usuarios y grupos {#assign-roles-to-users-groups}

1. Inicie sesión en AEM Forms en el entorno JEE.
1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Seleccione la configuración de su dominio, por ejemplo, LDAP, y haga clic en él. Encontrará todos los usuarios y grupos creados en el Directorio. Si es necesario, puede crear nuevos usuarios o grupos.
   ![Página de administración de dominios](/help/forms/using/assets/domain-mgmt-page.png)
1. Haga clic en Autenticación. En la nueva página, seleccione un proveedor de autenticación, como LDAP.
1. Vaya a la página Administración de dominios, seleccione LDAP y haga clic en **Sincronizar ahora** para sincronizar el directorio con el esquema de autenticación que configuró para el acceso a AEM.
   ![Sincronizar ldap](/help/forms/using/assets/sync-ldap.png)
1. Vaya a Administración de usuarios y haga clic en Usuarios y grupos.
1. Busque usuarios o grupos con sus nombres, como se muestra en la siguiente imagen.
   ![Buscar grupo de usuarios](/help/forms/using/assets/search-user-group.png)
1. Asigne las funciones a los usuarios o grupos según sea necesario.
   ![Asignación de funciones de usuario](/help/forms/using/assets/user-role-assign.png)

