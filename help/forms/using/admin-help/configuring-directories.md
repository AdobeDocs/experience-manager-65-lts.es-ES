---
title: Configurar directorios
description: Obtenga información sobre cómo agregar, editar y eliminar directorios, y configurar la administración de usuarios para utilizar la vista de lista virtual.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2c0dd472-9697-4b96-b3fa-3c50883bf425
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '3253'
ht-degree: 0%

---

# Configurar directorios {#configuring-directories}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Para cada dominio de empresa que configure, especifique los directorios que el proveedor de autenticación consulta para obtener información del usuario. Puede configurar varios directorios para un dominio.

## Adición de directorios o SPI personalizados {#adding-directories-or-custom-spis}

Para cada dominio de empresa que configure, especifique los directorios que el proveedor de autenticación consulta para obtener información del usuario. Puede agregar un directorio a un dominio de empresa existente o a un nuevo dominio de empresa que esté agregando. Puede configurar varios directorios para un dominio. También puede configurar un dominio para utilizar una interfaz de proveedor de servicios (SPI) personalizada para la sincronización.

### Añadir un directorio {#add-a-directory}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa o seleccione un dominio de empresa existente.
1. Haga clic en Agregar directorio.
1. En el cuadro Nombre del perfil, escriba un nombre para distinguir este directorio y, a continuación, haga clic en Siguiente.
1. Configure las opciones del servidor de directorio. (Consulte [Configuración de directorio](configuring-directories.md#directory-settings).)
1. Para comprobar que se puede establecer una conexión con el servidor LDAP, haga clic en Probar. Si la prueba falla, revise la excepción en el archivo de registro del servidor de aplicaciones para determinar la causa raíz del error. Haga clic en Cerrar y, a continuación, en Siguiente.
1. Seleccione Configuración de usuario y establezca la configuración según sea necesario. (Consulte [Configuración de directorio](configuring-directories.md#directory-settings).)
1. Para comprobar que el DN base y otros atributos configurados recopilan el lote correcto de usuarios, haga clic en Probar. LDAP intenta recuperar los primeros 200 registros utilizando la configuración proporcionada (como DN base, filtro de búsqueda y todos los atributos).

   Si se devuelven usuarios, los resultados muestran los valores asignados a cada campo según el conjunto de atributos. Si la prueba falla debido a un nombre de servidor inexistente, información de autorización incorrecta o atributos incorrectos, aparece el siguiente mensaje de error: &quot;Los criterios de búsqueda especificados no arrojaron ningún resultado&quot;. Para determinar la causa raíz del error, revise la excepción en el archivo de registro del servidor de aplicaciones. Haga clic en Cerrar y, a continuación, en Siguiente.

1. Seleccione Configuración de grupo y establezca la configuración según sea necesario. (Consulte [Configuración de directorio](configuring-directories.md#directory-settings).)
1. Para comprobar que el DN base y otros atributos configurados recopilan el lote correcto de grupos, haga clic en Probar. Si se devuelven grupos, los resultados muestran los valores asignados a cada campo según el conjunto de atributos. Haga clic en Cerrar.

### Añadir un SPI personalizado {#add-a-custom-spi}

Para obtener información sobre cómo crear un SPI personalizado, consulte &quot;Desarrollo de SPI para formularios AEM&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63). Para que un SPI personalizado recién implementado esté disponible para asociarlo al dominio, reinicie el servidor.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa o seleccione un dominio de empresa existente.
1. Haga clic en Agregar directorio.
1. Escriba un nombre en el cuadro Nombre del perfil, seleccione Proveedor SPI personalizado y, a continuación, haga clic en Siguiente.
1. Seleccione un proveedor de usuarios personalizado de la lista y haga clic en Siguiente.
1. Seleccione un proveedor de grupos personalizado de la lista y haga clic en Finalizar.

## Edición de un directorio {#edit-a-directory}

Puede editar los detalles de un directorio que haya configurado anteriormente.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente en la lista y, en la página que aparece, seleccione el directorio correspondiente en la lista.
1. Configure el directorio, el usuario y el grupo según sea necesario. (Consulte [Configuración de directorio](configuring-directories.md#directory-settings).)
1. Haga clic en Aceptar.

## Eliminar un directorio {#delete-a-directory}

Al sincronizar los dominios después de eliminar un directorio, todos los usuarios y grupos de ese directorio se marcan como obsoletos en la base de datos. No se devolverán en ninguna búsqueda desde la consola de administración.

>[!NOTE]
>
>Los dominios empresariales requieren al menos un proveedor de autenticación y un proveedor de directorios.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente en la lista.
1. Seleccione la casilla de verificación del directorio correspondiente y haga clic en Eliminar.
1. Haga clic en Aceptar en la página de confirmación que aparece y vuelva a hacer clic en Aceptar.

## Configuración de directorio {#directory-settings}

Cuando agregue un directorio a un dominio, especifique la siguiente configuración de directorio.

**Servidor:** (obligatorio) nombre de dominio completo (FQDN) del servidor de directorio. Por ejemplo, para un equipo llamado x en la red adobe.com, el FQDN es x.adobe.com. Se puede usar una dirección IP en lugar del nombre de servidor FQDN.

**Puerto:** (obligatorio) El puerto que utiliza el servidor de directorio. Normalmente, 389 o 636 si se utiliza el protocolo Secure Sockets Layer (SSL) para enviar información de autenticación a través de la red.

**SSL:** (obligatorio) Especifica si el servidor de directorio utiliza SSL al enviar datos a través de la red. El valor predeterminado es No. Cuando se establece en Yes, el entorno de tiempo de ejecución de Java™ (JRE) del servidor de aplicaciones debe confiar en el certificado del servidor LDAP correspondiente.

**Enlace** (obligatorio) Especifica cómo obtener acceso al directorio.

**Anónimo:** No se requiere ningún nombre de usuario ni contraseña. Es posible que un usuario anónimo solo pueda recuperar una cantidad limitada de datos. Esta opción puede resultar útil para las pruebas iniciales.

**Usuario:** Se requiere autenticación. En el cuadro Nombre, especifique el nombre del registro de usuario que puede acceder al directorio. Es mejor introducir el nombre distinguido completo (DN) de la cuenta de usuario, como cn=Jane Doe, ou=user, dc=can, dc=com. En el cuadro Contraseña, especifique la contraseña asociada. Esta configuración es necesaria cuando selecciona Usuario como opción de enlace.

**Nombre:** Nombre que se puede usar para conectarse a la base de datos LDAP cuando el acceso anónimo no está habilitado. Para Active Directory 2003, especifique `[domain name]\[userid]`. Para Sun™ One, eDirectory o IBM Tivoli Directory Server, especifique el nombre completo del usuario, como uid=lcuser,ou=it,o=company.com.

**Contraseña:** Contraseña que corresponde al nombre especificado para conectarse a la base de datos LDAP cuando el acceso anónimo no está habilitado.

**Rellenar página con:** Cuando se selecciona, rellena los atributos en las páginas de configuración Usuario y Grupo con los valores LDAP predeterminados correspondientes.

**Recuperar DN base:** Recupera los DN base y los muestra en la lista desplegable. Esta configuración es útil cuando tiene varios DN base y necesita seleccionar un valor.

**Habilitar referencia:** Esta configuración es aplicable cuando su organización utiliza varios dominios de Active Directory organizados en una estructura jerárquica y ha especificado la configuración de directorio únicamente para el dominio principal. En este caso, al seleccionar esta opción, Administración de usuarios puede acceder a los detalles de usuarios y grupos desde los dominios secundarios.

>[!NOTE]
>
>Haga clic en Probar para comprobar que se puede establecer una conexión con el servidor LDAP. Para determinar la causa raíz de los errores, revise la excepción en el archivo de registro del servidor de aplicaciones.

### Configuración de usuario {#user-settings}

**Identificador único:** (obligatorio) Atributo único y constante usado para identificar a los usuarios. Utilice un atributo que no sea DN como identificador único, ya que el DN de un usuario puede cambiar si se desplaza a otra parte de la organización. Esta configuración depende del servidor de directorio. El valor es objectGUID para Active Directory 2003, nsuniqueID para Sun™ One y guid para eDirectory.

>[!NOTE]
>
>Asegúrese de introducir un atributo que garantice que sea único en su organización. La introducción de un valor incorrecto puede causar problemas graves en el sistema.

**DN base:** Se ha establecido como punto de partida para sincronizar usuarios y grupos desde la jerarquía LDAP. Es mejor especificar un DN base en el nivel inferior de la jerarquía que incluya todos los usuarios y grupos que necesitan sincronizarse para los servicios.

Si seleccionó la opción Habilitar referencia en la configuración del Directorio, establezca la opción DN base en la parte *dc* del DN. Para que funcione la referencia, la duración de la búsqueda debe incluir los dominios principal y secundario.

>[!NOTE]
>
>No incluya el DN del usuario en esta configuración. Para sincronizar un usuario en particular, utilice la configuración Filtro de búsqueda.

Aunque DN base es una configuración obligatoria en la consola de administración, algunos servidores de directorio como IBM Domino Enterprise Server pueden requerir un DN base vacío. Para especificar un DN base vacío, exporte el archivo config.xml, edite el ajuste en el archivo config.xml y vuelva a importarlo. (Consulte [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de búsqueda:** (obligatorio) Filtro de búsqueda que se utilizará para encontrar el registro asociado al usuario. Puede realizar una búsqueda de un nivel o una búsqueda de subnivel. (Consulte Sintaxis del filtro de búsqueda o RFC 2254). Para obtener información adicional sobre el esquema de Microsoft AD, consulte Esquema de Active Directory.

**Descripción:** Atributo de esquema para la descripción del usuario

**Nombre completo:** (obligatorio) Atributo de esquema para el nombre completo del usuario

**Identificador de inicio de sesión:** (obligatorio) Atributo de esquema para el identificador de inicio de sesión del usuario

**Apellidos:** (obligatorio) Atributo de esquema para el apellido del usuario

**Nombre dado:** (obligatorio) Atributo de esquema para el nombre del usuario

**Iniciales:** Atributo de esquema para las iniciales del usuario

**Calendario empresarial:** Le permite asignar un calendario empresarial a un usuario, según el valor de esta configuración (la clave del calendario empresarial). Los calendarios comerciales definen días laborables y no laborables. Los formularios AEM Forms pueden utilizar calendarios comerciales al calcular las fechas y horas futuras para eventos como recordatorios, plazos y escalaciones. La forma de asignar claves de calendario empresarial a los usuarios depende de si utiliza un dominio empresarial, local o híbrido. (Consulte Configuración de calendarios comerciales.)

Si utiliza un dominio de empresa, puede asignar la configuración del Calendario empresarial a un campo del directorio LDAP. Por ejemplo, si cada registro de usuario del directorio contiene un campo *país* y desea asignar calendarios comerciales basados en el país donde se encuentra el usuario, especifique el nombre de campo *país* como valor de la configuración del Calendario empresarial. A continuación, puede asignar las claves del calendario empresarial (los valores definidos para el campo *country* en el directorio LDAP) a los calendarios empresariales del flujo de trabajo de formularios.

La cantidad de espacio utilizado para mostrar el nombre de la clave del calendario empresarial en las páginas del flujo de trabajo de formularios es limitada. Limite el nombre de la clave del calendario empresarial a menos de 53 caracteres para evitar que se trunque en esas páginas.

**Modificar marca de tiempo:** Para habilitar la sincronización de directorios delta, establezca este valor para modificar la marca de tiempo. (Consulte Habilitar la sincronización de directorios delta.)

**Organización:** Atributo de esquema para el nombre de la organización a la que pertenece el usuario.

**Correo electrónico principal:** Atributo de esquema para la dirección de correo electrónico principal del usuario.

**Correo electrónico secundario:** Atributo de esquema para la dirección de correo electrónico secundaria del usuario.

**Teléfono:** Atributo de esquema para el número de teléfono del usuario.

**Dirección postal:** Atributo de esquema de la dirección de correo del usuario.

**Configuración regional:** Atributo de esquema que contiene la información de configuración regional ISO. El valor es un código de idioma de dos letras o un código de idioma y país.

**Zona horaria:** Atributo de esquema que contiene la zona horaria donde se encuentra el usuario. El valor es una cadena como Ciudad/País.

**Habilitar el control de vista de lista virtual (VLV):** Un control LDAP que permite a los formularios de AEM recuperar datos por lotes del servidor de directorio. Si utiliza Sun One como directorio LDAP y el directorio contiene muchos usuarios, al activar VLV se crea un índice que Administración de usuarios puede utilizar al buscar usuarios. Esta función es útil cuando se utiliza una cuenta de usuario normal que solo puede sincronizar una cantidad limitada de datos. También puede habilitar VLV para grupos. Si selecciona Habilitar el control de vista de lista virtual (VLV), especifique un nombre en el cuadro Ordenar campo.

>[!NOTE]
>
>Para habilitar VLV, configure Sun One. Consulte [Configurar la administración de usuarios para utilizar la vista de lista virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo de ordenación:** Si seleccionó Habilitar el control de vista de lista virtual (VLV), especifique el nombre de atributo utilizado para ordenar el índice. Este nombre de atributo (como uid) es el que especificó al crear un índice para VLV en el servidor de directorios.

### Configuración de grupo {#group-settings}

**Identificador único:** (obligatorio) Atributo único y constante usado para identificar grupos. Utilice un atributo que no sea DN como identificador único. Esta configuración depende del servidor de directorio. El valor es objectGUID para Active Directory 2003, nsuniqueID para Sun One y guid para eDirectory.

>[!NOTE]
>
>Asegúrese de introducir un atributo que garantice que sea único en su organización. La introducción de un valor incorrecto puede causar problemas graves en el sistema.

**DN base:** (obligatorio) Nombre distintivo base del directorio.

Aunque DN base es una configuración obligatoria en la consola de administración, algunos servidores de directorio como IBM Domino Enterprise Server requieren un DN base vacío. Para especificar un DN base vacío, exporte el archivo config.xml, edite el ajuste en el archivo config.xml y vuelva a importarlo. (Consulte [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de búsqueda:** (obligatorio) Filtro de búsqueda que se utilizará para encontrar el registro asociado al grupo. Puede realizar una búsqueda de un nivel o una búsqueda de subnivel.

**Descripción:** Atributo de esquema para la descripción del grupo

**Nombre completo:** (obligatorio) Atributo de esquema para el nombre completo del grupo

**DN de miembro:** (obligatorio) Atributo de esquema para el nombre distintivo de miembros dentro de un grupo

**Identificador único de miembro:** Identificador único de un usuario o grupo que es miembro del grupo seleccionado. Este valor depende del servidor de directorios. El valor es objectSID para AD2003, nsuniqueID para Sun One y guid para eDirectory.

Si se especifica DN de miembro con un atributo que no es DN, User Management utiliza el identificador único de miembro para consultar LDAP y recopilar el DN del usuario, ya que corresponde a un valor de identificador único.

Si DN se especifica como identificador único, no es necesario configurar el identificador único de miembro.

**Organización:** Atributo de esquema para el nombre de la organización a la que pertenece el grupo

**Correo electrónico principal:** Atributo de esquema para la dirección de correo electrónico principal del grupo

**Correo electrónico secundario:** Atributo de esquema para la dirección de correo electrónico secundaria del grupo

**Modificar marca de tiempo:** Para habilitar la sincronización de directorios delta, establezca este valor para modificar la marca de tiempo. (Consulte Habilitar la sincronización de directorios delta.)

**Habilitar el control de vista de lista virtual (VLV):** Un control LDAP que permite a los formularios de AEM recuperar datos por lotes del servidor de directorio. Si utiliza Sun One como directorio LDAP y el directorio contiene muchos grupos, al activar VLV se crea un índice que Administración de usuarios puede utilizar al buscar grupos. Esta función es útil cuando se utiliza una cuenta de usuario normal que solo puede sincronizar una cantidad limitada de datos. También puede habilitar VLV para usuarios de. Si selecciona Habilitar el control de vista de lista virtual (VLV), especifique un nombre de campo de ordenación.

>[!NOTE]
>
>Para habilitar VLV, configure Sun One. Consulte [Configurar la administración de usuarios para utilizar la vista de lista virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nombre del campo de ordenación:** Si seleccionó Habilitar el control de vista de lista virtual (VLV), especifique el nombre de atributo utilizado para ordenar el índice. Este nombre de atributo es el que especificó al crear un índice para VLV en el servidor de directorios.

>[!NOTE]
>
>Haga clic en Probar para comprobar que la configuración del usuario y del grupo se recopila en función del DN base y los criterios de búsqueda.

Si se devuelven usuarios y grupos, los resultados muestran los valores asignados a cada campo según el conjunto de atributos.

>[!NOTE]
>
>Administración de usuarios no admite identificadores de usuario duplicados dentro de un dominio; solo se sincroniza un usuario con el identificador de usuario.

## Configuración de la administración de usuarios para utilizar la vista de lista virtual (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronización de directorios es un requisito importante para la administración de usuarios. Los usuarios y grupos se sincronizan desde un directorio empresarial a la base de datos de formularios de AEM para asignar funciones y permisos. El número de usuarios varía de 100 a 100000 o más según los requisitos y plantea un desafío de ingeniería para sincronizar los datos de forma eficaz.

El protocolo LDAP proporciona un mecanismo para consultar conjuntos de datos grandes de forma paginada mediante controles de solicitud. Al utilizar Microsoft Active Directory, la sincronización de LDAP con la base de datos de formularios de AEM utiliza PagedResultsControl para recuperar datos en lotes de un tamaño determinado. Sun ONE Directory Server no admite este control. Para completar una consulta paginada con Sun ONE Directory Server, utilice el control Vista de lista virtual (VLV). Este control implica tanto la configuración del lado del servidor como la implementación del lado del cliente.

>[!NOTE]
>
>En esta sección se describe el uso del control VLV para Sun ONE Directory Server. Sin embargo, puede utilizar este control para cualquier servidor de directorios que admita el control VLV.

1. Al configurar el directorio, seleccione Activar control de Vista de lista virtual (VLV) en la página Configuración de usuario y en la página Configuración de grupo. Al activar la casilla de verificación, también debe especificar un nombre de ordenación en el cuadro Campo de ordenación. El valor predeterminado es uid. (Consulte [Agregar directorios o SPI personalizados](configuring-directories.md#adding-directories-or-custom-spis) o [Editar un directorio](configuring-directories.md#edit-a-directory)).
1. Utilice la consola de administración de Sun ONE o un script de línea de comandos para crear las entradas VLV de LDAP para usuarios y grupos. Si utiliza un script de línea de comandos, puede utilizar los archivos LDIF de ejemplo de usuarios y grupos. (Consulte [Configuración del servidor de directorio Sun ONE para VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Detenga el servidor y cree el índice necesario. (Consulte [Crear el índice del servidor de directorios para VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configuración de Sun ONE Directory Server para VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creación de un VLV requiere un par de entradas que incluyan las clases de objeto `vlvSearch` y `vlvIndex`. La entrada vlvSearch incluye una base de búsqueda y el atributo `vlvFilter`, que especifica la clase de objeto que contiene los atributos que desea ordenar. La clase de objeto `vlvIndex` incluye el atributo `vlvSort`, que especifica uno o más atributos para ordenar y el orden para ordenarlos. (Un signo menos (-) indica el orden alfabético inverso). El uso de VLV con formularios AEM Forms requiere entradas independientes para usuarios y grupos.

>[!NOTE]
>
>Las entradas Object se pueden crear mediante la interfaz gráfica de usuario (GUI) de Sun ONE o mediante un script de línea de comandos. Para obtener instrucciones sobre la creación de entradas de objeto mediante la interfaz gráfica de usuario, consulte la documentación de Sun ONE.

Este es un ejemplo de script LDIF para la entrada VLV para usuarios:

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**Cree las entradas del objeto mediante un script**

1. El script de ejemplo tiene una entrada LDAP denominada `lcuser`. Esta entrada es para la configuración relacionada con VLV para la sincronización de usuarios en formularios AEM Forms. Modifique las siguientes propiedades en consecuencia:

   **Nombre de entrada:** El nombre de entrada de este ejemplo es `lcuser`. Si se cambia `lcuser`, debe cambiarse en todas las áreas del script de ejemplo.

   **vlvBase:** DN base especificado en la página Configuración de usuario.

   **vlvFilter:** El filtro de búsqueda especificado en la página Configuración de usuario.

   **vlvSort:** Campo de ordenación especificado en la sección Configuración de VLV de la página Configuración de usuario. Un control VLV requiere que especifique un control de ordenación. Este campo se utiliza como parámetro de ordenación para el índice vlv creado.

   **aci:** El control de acceso especificado en el script de ejemplo concede a cualquier usuario autenticado el derecho de acceder a los índices VLV para operaciones de lectura, búsqueda y comparación. El administrador puede restringir el acceso a un usuario de enlace, que se configura en la página Configuración del servidor de directorios especificada en la interfaz de usuario de Administración de usuarios. Si no se conceden permisos, la búsqueda de usuarios no puede utilizar el VLV y el servidor LDAP genera una excepción de permiso.

   >[!NOTE]
   >
   >Como norma, el nombre de la entrada vlvIndex también está establecido en `lcuser`, pero puede darle un nombre diferente. Utilice el mismo nombre en la herramienta vlvindex. (Consulte [Crear el índice del servidor de directorios para VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Con la herramienta `ldapmodify` proporcionada con Sun ONE Server, cree una entrada similar para los grupos utilizando el DN base del grupo, el filtro de búsqueda y el campo de ordenación respectivamente:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Por ejemplo, escriba el siguiente texto:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Crear el índice del servidor de directorios para VLV {#create-the-directory-server-index-for-vlv}

Después de configurar el directorio y crear las entradas LDAP VLV para usuarios y grupos, detenga el servidor y cree el índice requerido.

1. Después de crear las entradas del objeto, detenga Sun ONE Server.
1. Con la herramienta vlvindex, genere el índice escribiendo el siguiente texto:

   *instancia del servidor de directorio* `\vlvindex.bat -n userRoot -T lcuser`

   Se genera el siguiente resultado:

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   La herramienta vlvindex está presente en el directorio de instancias del servidor de directorios. Si Sun ONE Server tiene dos instancias que ejecutan server1 y server2, la herramienta vlvindex se encuentra en el directorio *Sun ONE server directory*\server1. El valor del parámetro `-T` es el valor del atributo `cn` de la entrada vlvindex creada anteriormente en el LDIF de ejemplo. En este caso, es `lcuser`.

1. Si VLV también está habilitado para grupos, cree el índice correspondiente para los grupos. Compruebe si los índices se crean ejecutando el siguiente comando:

   *directorio de servidor sun one* `\shared\bin>ldapsearch -h`*nombre host* `-p`*puerto no* `-s base -b "" objectclass=*`

   Se generan resultados como los siguientes datos de ejemplo:

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
