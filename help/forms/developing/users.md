---
title: Administración de usuarios
description: Utilice la API de administración de usuarios para crear aplicaciones cliente que puedan administrar roles, permisos y principales (que pueden ser usuarios o grupos) y autenticar usuarios.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: e449c6f6-7b75-47ab-9abd-8031b7b151e5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '6201'
ht-degree: 0%

---

# Administración de usuarios {#managing-users}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

**Acerca de la administración de usuarios**

Puede utilizar la API de administración de usuarios para crear aplicaciones cliente que puedan administrar roles, permisos y principales (que pueden ser usuarios o grupos) y autenticar usuarios. La API de administración de usuarios consta de las siguientes API de AEM Forms:

* API de servicio de Directory Manager
* API del servicio Administrador de autenticación
* API del servicio Administrador de autorización

Administración de usuarios permite asignar, quitar y determinar funciones y permisos. También permite asignar, quitar y consultar dominios, usuarios y grupos. Por último, puede utilizar Administración de usuarios para autenticar a los usuarios.

En [Agregar usuarios](users.md#adding-users) comprenderá cómo agregar usuarios mediante programación. Esta sección utiliza la API del servicio de Directory Manager.

En [Eliminación de usuarios](users.md#deleting-users), comprenderá cómo eliminar usuarios mediante programación. Esta sección utiliza la API del servicio de Directory Manager.

En [Administración de usuarios y grupos](users.md#managing-users-and-groups), comprenderá la diferencia entre un usuario local y un usuario de directorio, y verá ejemplos de cómo usar las API de Java y de servicios web para administrar usuarios y grupos mediante programación. Esta sección utiliza la API del servicio de Directory Manager.

En [Administración de funciones y permisos](users.md#managing-roles-and-permissions), obtendrá información sobre las funciones y los permisos del sistema, y sobre lo que puede hacer mediante programación para aumentarlos. También verá ejemplos de cómo usar las API de Java y de servicios web para administrar funciones y permisos mediante programación. Esta sección utiliza tanto la API del servicio de Directory Manager como la API del servicio de Authorization Manager.

En [Autenticar usuarios](users.md#authenticating-users) verá ejemplos de cómo usar las API de Java y del servicio web para autenticar a los usuarios mediante programación. Esta sección utiliza la API del servicio Administrador de autorización.

**Explicación del proceso de autenticación**

Administración de usuarios proporciona funcionalidad de autenticación integrada y la capacidad de conectarse con su propio proveedor de autenticación. Cuando Administración de usuarios recibe una solicitud de autenticación (por ejemplo, un usuario intenta iniciar sesión), pasa la información del usuario al proveedor de autenticación para que se autentique. Administración de usuarios recibe los resultados del proveedor de autenticación después de autenticar al usuario.

En el diagrama siguiente se muestra la interacción entre un usuario final que intenta iniciar sesión, Administración de usuarios y el proveedor de autenticación.

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

En la tabla siguiente se describe cada paso del proceso de autenticación.

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un usuario intenta iniciar sesión en un servicio que invoca la administración de usuarios. El usuario especifica un nombre de usuario y una contraseña. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Administración de usuarios envía el nombre de usuario y la contraseña, así como la información de configuración, al proveedor de autenticación.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>El proveedor de autenticación se conecta al almacén de usuarios y autentica al usuario.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>El proveedor de autenticación devuelve los resultados a Administración de usuarios.</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Administración de usuarios permite que el usuario inicie sesión o deniega el acceso al producto.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si la zona horaria del servidor es diferente de la del cliente, al consumir el WSDL para el servicio AEM Forms Generate PDF en una pila nativa de SOAP con un cliente .NET en un clúster de servidor de aplicaciones de WebSphere, puede producirse el siguiente error de autenticación de User Management:

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**Explicación de la administración de directorios**

La Administración de usuarios está empaquetada con un proveedor de servicios de directorio (DirectoryManagerService) que admite conexiones a directorios LDAP. Si su organización utiliza un repositorio que no sea LDAP para almacenar registros de usuario, puede crear su propio proveedor de servicios de directorio que trabaje con el repositorio.

Los proveedores de servicios de directorio recuperan registros de un almacén de usuarios a petición de Administración de usuarios. Administración de usuarios almacena en caché regularmente los registros de usuarios y grupos en la base de datos para mejorar el rendimiento.

El proveedor de servicios de directorio se puede utilizar para sincronizar la base de datos de Administración de usuarios con el almacén de usuarios. Este paso garantiza que toda la información del directorio de usuario y todos los registros de usuario y grupo estén actualizados.

Además, DirectoryManagerService permite crear y administrar dominios. Los dominios definen diferentes bases de usuario. El límite de un dominio suele definirse según la forma en que esté estructurada su organización o la configuración de su almacén de usuarios. Los dominios de administración de usuarios proporcionan opciones de configuración que utilizan los proveedores de autenticación y los proveedores de servicios de directorio.

En el XML de configuración que exporta Administración de usuarios, el nodo raíz que tiene el valor de atributo de `Domains` contiene un elemento XML para cada dominio definido para Administración de usuarios. Cada uno de estos elementos contiene otros elementos que definen aspectos del dominio asociado con proveedores de servicios específicos.

**Explicación de los valores de objectSID**

Al utilizar Active Directory, es importante comprender que un valor `objectSID` no es un atributo único en varios dominios. Este valor almacena el identificador de seguridad de un objeto. En un entorno de varios dominios (por ejemplo, un árbol de dominios), el valor `objectSID` puede ser diferente.

Un valor `objectSID` cambiaría si un objeto se mueve de un dominio de Active Directory a otro. Algunos objetos tienen el mismo valor `objectSID` en cualquier parte del dominio. Por ejemplo, los grupos como BUILTIN\Administradores, BUILTIN\Usuarios avanzados, etc., tendrían el mismo valor `objectSID` independientemente de los dominios. Estos `objectSID` valores son bien conocidos.

## Adición de usuarios {#adding-users}

Puede utilizar la API del servicio Directory Manager (Java y servicio web) para agregar usuarios a AEM Forms mediante programación. Después de agregar un usuario, puede utilizarlo cuando realice una operación de servicio que requiera un usuario. Por ejemplo, puede asignar una tarea al nuevo usuario.

### Resumen de los pasos {#summary-of-steps}

Para agregar un usuario, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Definir información de usuario.
1. Añada el usuario a AEM Forms.
1. Compruebe que se ha agregado el usuario.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un cliente de DirectoryManagerService**

Para poder realizar mediante programación una operación de servicio de Directory Manager, cree un cliente de API de servicio de Directory Manager.

**Definir información de usuario**

Cuando agregue un nuevo usuario mediante la API del servicio de Directory Manager, defina la información para ese usuario. Normalmente, cuando se agrega un nuevo usuario, se definen los siguientes valores:

* **Nombre de dominio**: Dominio al que pertenece el usuario (por ejemplo, `DefaultDom`).
* **Valor del identificador de usuario**: Valor del identificador del usuario (por ejemplo, `wblue`).
* **Tipo de entidad de seguridad**: El tipo de usuario (por ejemplo, puede especificar `USER)`.
* **Nombre dado**: Un nombre dado para el usuario (por ejemplo, `Wendy`).
* **Nombre de familia**: El nombre de familia del usuario (por ejemplo, `Blue)`.
* **Configuración regional**: Información de configuración regional del usuario.

**Agregar el usuario a AEM Forms**

Después de definir la información del usuario, puede agregarlo a AEM Forms. Para agregar un usuario, invoque el método `createLocalUser` del objeto `DirectoryManagerServiceClient`.

**Compruebe que se agregó el usuario**

Puede comprobar que se agregó el usuario para asegurarse de que no se produjeron problemas. Busque el nuevo usuario utilizando el valor identificador de usuario.

**Consulte también**

[Añadir usuarios mediante la API de Java](users.md#add-users-using-the-java-api)

[Agregar usuarios mediante la API de servicio web](users.md#add-users-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Eliminación de usuarios](users.md#deleting-users)

### Añadir usuarios mediante la API de Java {#add-users-using-the-java-api}

Agregar usuarios mediante la API del servicio de Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente de DirectoryManagerServices.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Definir información de usuario.

   * Crear un objeto `UserImpl` mediante su constructor.
   * Establezca el nombre de dominio invocando el método `setDomainName` del objeto `UserImpl`. Pase un valor de cadena que especifique el nombre de dominio.
   * Establezca el tipo principal invocando el método `setPrincipalType` del objeto `UserImpl`. Pase un valor de cadena que especifique el tipo de usuario. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario invocando el método `setUserid` del objeto `UserImpl`. Pase un valor de cadena que especifique el valor del identificador de usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre canónico invocando el método `setCanonicalName` del objeto `UserImpl`. Pase un valor de cadena que especifique el nombre canónico del usuario. Por ejemplo, puede especificar `wblue`.
   * Establezca el nombre dado invocando el método `setGivenName` del objeto `UserImpl`. Pase un valor de cadena que especifique el nombre de pila del usuario. Por ejemplo, puede especificar `Wendy`.
   * Establezca el nombre de familia invocando el método `setFamilyName` del objeto `UserImpl`. Pase un valor de cadena que especifique el nombre familiar del usuario. Por ejemplo, puede especificar `Blue`.

   >[!NOTE]
   >
   >Invoque un método que pertenezca al objeto `UserImpl` para establecer otros valores. Por ejemplo, puede establecer el valor de configuración regional invocando el método `setLocale` del objeto `UserImpl`.

1. Añada el usuario a AEM Forms.

   Invoque el método `createLocalUser` del objeto `DirectoryManagerServiceClient` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado el usuario.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el valor del identificador de usuario invocando el método `setUserId` del objeto `PrincipalSearchFilter`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Itere por la instancia `java.util.List` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Añadir usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Agregar usuarios mediante la API de servicio web {#add-users-using-the-web-service-api}

Agregar usuarios mediante la API del servicio Directory Manager Service (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL para la referencia del servicio: `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `?blob=mtom`.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Definir información de usuario.

   * Crear un objeto `UserImpl` mediante su constructor.
   * Establezca el nombre de dominio asignando un valor de cadena al campo `domainName` del objeto `UserImpl`.
   * Establezca el tipo principal asignando un valor de cadena al campo `principalType` del objeto `UserImpl`. Por ejemplo, puede especificar `USER`.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `userid` del objeto `UserImpl`.
   * Establezca el valor del nombre canónico asignando un valor de cadena al campo `canonicalName` del objeto `UserImpl`.
   * Establezca el valor del nombre dado asignando un valor de cadena al campo `givenName` del objeto `UserImpl`.
   * Establezca el valor del nombre de familia asignando un valor de cadena al campo `familyName` del objeto `UserImpl`.

1. Añada el usuario a AEM Forms.

   Invoque el método `createLocalUser` del objeto `DirectoryManagerServiceClient` y pase los siguientes valores:

   * El objeto `UserImpl` que representa al nuevo usuario
   * Valor de cadena que representa la contraseña del usuario

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Compruebe que se ha agregado el usuario.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el valor del identificador de usuario del usuario asignando un valor de cadena que represente el valor del identificador de usuario al campo `userId` del objeto `PrincipalSearchFilter`.
   * Invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Recorra en iteración la colección `MyArrayOfUser` para localizar al usuario.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Eliminación de usuarios {#deleting-users}

Puede utilizar la API del servicio Directory Manager (Java y servicio web) para eliminar usuarios de AEM Forms mediante programación. Una vez eliminado un usuario, ya no se puede utilizarlo para realizar una operación de servicio que requiera un usuario. Por ejemplo, no puede asignar una tarea a un usuario eliminado.

### Resumen de los pasos {#summary_of_steps-1}

Para eliminar un usuario, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Especifique el usuario que desea eliminar.
1. Elimine el usuario de AEM Forms.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un cliente de DirectoryManagerService**

Para poder realizar mediante programación una operación de API del servicio Directory Manager, cree un cliente de servicio Directory Manager.

**Especifique el usuario que desea eliminar**

Puede especificar un usuario para eliminarlo utilizando el valor del identificador del usuario.

**Eliminar el usuario de AEM Forms**

Para eliminar un usuario, invoque el método `deleteLocalUser` del objeto `DirectoryManagerServiceClient`.

**Consulte también**

[Eliminar usuarios mediante la API de Java](users.md#delete-users-using-the-java-api)

[Eliminar usuarios mediante la API de servicio web](users.md#delete-users-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de usuarios](users.md#adding-users)

### Eliminar usuarios mediante la API de Java {#delete-users-using-the-java-api}

Eliminar usuarios mediante la API del servicio de Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el usuario que desea eliminar.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el valor del identificador de usuario invocando el método `setUserId` del objeto `PrincipalSearchFilter`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Itere a través de la instancia `java.util.List` para localizar al usuario que desea eliminar.

1. Elimine el usuario de AEM Forms.

   Invoque el método `deleteLocalUser` del objeto `DirectoryManagerServiceClient` y pase el valor del campo `oid` del objeto `User`. Invoque el método `getOid` del objeto `User`. Utilice el objeto `User` recuperado de la instancia `java.util.List`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo EJB): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Inicio rápido (modo SOAP): Eliminación de usuarios mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminar usuarios mediante la API de servicio web {#delete-users-using-the-web-service-api}

Eliminar usuarios mediante la API del servicio Directory Manager Service (servicio Web):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   * Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `DirectoryManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`). No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Asegúrese de especificar `blob=mtom.`
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `DirectoryManagerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique el usuario que desea eliminar.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el valor del identificador de usuario asignando un valor de cadena al campo `userId` del objeto `PrincipalSearchFilter`.
   * Invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` y pase el objeto `PrincipalSearchFilter`. Este método devuelve un objeto de colección `MyArrayOfUser`, donde cada elemento es un objeto `User`. Recorra en iteración la colección `MyArrayOfUser` para localizar al usuario. El objeto `User` recuperado del objeto de colección `MyArrayOfUser` se usa para eliminar al usuario.

1. Elimine el usuario de AEM Forms.

   Elimine el usuario pasando el valor de campo `oid` del objeto `User` al método `deleteLocalUser` del objeto `DirectoryManagerServiceClient`.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creación de grupos {#creating-groups}

Puede utilizar la API del servicio Directory Manager (Java y servicio web) para crear grupos de AEM Forms mediante programación. Después de crear un grupo, puede utilizarlo para realizar una operación de servicio que requiera un grupo. Por ejemplo, puede asignar un usuario al nuevo grupo. (Consulte [Administración de usuarios y grupos](users.md#managing-users-and-groups).)

### Resumen de los pasos {#summary_of_steps-2}

Para crear un grupo, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Determine que el grupo no existe.
1. Cree el grupo.
1. Realice una acción con el grupo.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios.

Los siguientes archivos JAR deben agregarse a la ruta de clase del proyecto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (obligatorio si AEM Forms está implementado en JBoss)
* jbossall-client.jar (requerido si AEM Forms está implementado en JBoss)

Para obtener información sobre la ubicación de estos archivos JAR, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un cliente de DirectoryManagerService**

Para poder realizar mediante programación una operación de servicio de Directory Manager, cree un cliente de API de servicio de Directory Manager.

**Determine si el grupo existe**

Cuando cree un grupo, asegúrese de que el grupo no existe en el mismo dominio. Es decir, dos grupos no pueden tener el mismo nombre dentro del mismo dominio. Para realizar esta tarea, realice una búsqueda y filtre los resultados de búsqueda en función de dos valores. Establezca el tipo principal en `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` para asegurarse de que solo se devuelven grupos. Además, asegúrese de especificar el nombre de dominio.

**Crear el grupo**

Después de determinar que el grupo no existe en el dominio, cree el grupo y especifique los atributos siguientes:

* **CommonName**: el nombre del grupo.
* **Dominio**: Dominio en el que se agrega el grupo.
* **Descripción**: Una descripción del grupo.

**Realizar una acción con el grupo**

Después de crear un grupo, puede realizar una acción con el grupo. Por ejemplo, puede agregar un usuario al grupo. Para añadir un usuario a un grupo, recupere el valor del identificador único del usuario y del grupo. Pase estos valores al método `addPrincipalToLocalGroup`.

**Consulte también**

[Creación de grupos mediante la API de Java](users.md#create-groups-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adición de usuarios](users.md#adding-users)

[Eliminación de usuarios](users.md#deleting-users)

### Creación de grupos mediante la API de Java {#create-groups-using-the-java-api}

Cree un grupo mediante la API de servicio de Directory Manager (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Determine si el grupo existe.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el tipo principal invocando el objeto `setPrincipalType` del objeto `PrincipalSearchFilter`. Pase el valor `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * Establezca el dominio invocando el objeto `setSpecificDomainName` del objeto `PrincipalSearchFilter`. Pase un valor de cadena que especifique el nombre de dominio.
   * Para buscar un grupo, invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` (un principal puede ser un grupo). Pase el objeto `PrincipalSearchFilter` que especifica el tipo principal y el nombre de dominio. Este método devuelve una instancia `java.util.List` en la que cada elemento es una instancia `Group`. Cada instancia de grupo se ajusta al filtro especificado mediante el objeto `PrincipalSearchFilter`.
   * Itere a través de la instancia `java.util.List`. Para cada elemento, recupere el nombre del grupo. Asegúrese de que el nombre del grupo no coincide con el nuevo nombre de grupo.

1. Cree el grupo.

   * Si el grupo no existe, invoque el método `setCommonName` del objeto `Group` y pase un valor de cadena que especifique el nombre del grupo.
   * Invoque el método `setDescription` del objeto `Group` y pase un valor de cadena que especifique la descripción del grupo.
   * Invoque el método `setDomainName` del objeto `Group` y pase un valor de cadena que especifique el nombre de dominio.
   * Invoque el método `createLocalGroup` del objeto `DirectoryManagerServiceClient` y pase la instancia `Group`.

   El método `createLocalUser` devuelve un valor de cadena que especifica el valor del identificador de usuario local.

1. Realice una acción con el grupo.

   * Crear un objeto `PrincipalSearchFilter` mediante su constructor.
   * Establezca el valor del identificador de usuario invocando el método `setUserId` del objeto `PrincipalSearchFilter`. Pase un valor de cadena que represente el valor del identificador de usuario.
   * Invoque el método `findPrincipals` del objeto `DirectoryManagerServiceClient` y pase el objeto `PrincipalSearchFilter`. Este método devuelve una instancia `java.util.List`, donde cada elemento es un objeto `User`. Itere por la instancia `java.util.List` para localizar al usuario.
   * Agregue un usuario al grupo invocando el método `addPrincipalToLocalGroup` del objeto `DirectoryManagerServiceClient`. Pase el valor devuelto del método `getOid` del objeto `User`. Pase el valor devuelto del método `getOid` de los objetos `Group` (utilice la instancia `Group` que representa el nuevo grupo).

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Administración de usuarios y grupos {#managing-users-and-groups}

En este tema se describe cómo puede utilizar (Java) para asignar, quitar y consultar dominios, usuarios y grupos mediante programación.

>[!NOTE]
>
>Al configurar un dominio, debe establecer el identificador único de grupos y usuarios. El atributo elegido no sólo debe ser único dentro del entorno LDAP, sino que también debe ser inmutable y no cambiará dentro del directorio. Este atributo también debe ser de un tipo de datos de cadena simple (la única excepción permitida actualmente para Active Directory 2000/2003 es `"objectsid"`, que es un valor binario). El atributo `"GUID"` de Novell eDirectory, por ejemplo, no es un tipo de datos de cadena simple y, por lo tanto, no funcionará.

* Para Active Directory, use `"objectsid"`.
* Para SunOne, use `"nsuniqueid"`.

>[!NOTE]
>
>No se admite la creación de varios usuarios y grupos locales mientras la sincronización de directorios LDAP está en curso. Si se intenta este proceso, pueden producirse errores.

### Resumen de los pasos {#summary_of_steps-3}

Para administrar usuarios y grupos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente DirectoryManagerService.
1. Invoque las operaciones de usuario o grupo adecuadas.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de DirectoryManagerService**

Para poder realizar mediante programación una operación de servicio de Directory Manager, debe crear un cliente de servicio de Directory Manager. Con la API de Java, esto se logra creando un objeto `DirectoryManagerServiceClient`. Con la API del servicio web, esto se logra creando un objeto `DirectoryManagerServiceService`.

**Invocar las operaciones del usuario o grupo apropiado**

Una vez creado el cliente de servicios, puede invocar las operaciones de administración de usuarios o grupos. El cliente de servicio permite asignar, quitar y consultar dominios, usuarios y grupos. Tenga en cuenta que es posible agregar un principal de directorio o un principal local a un grupo local, pero no es posible agregar un principal local a un grupo de directorios.

**Consulte también**

[Administración de usuarios y grupos mediante la API de Java](users.md#managing-users-and-groups-using-the-java-api)

[Administración de usuarios y grupos mediante la API de servicio web](users.md#managing-users-and-groups-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de usuarios y grupos mediante la API de Java {#managing-users-and-groups-using-the-java-api}

Para administrar mediante programación usuarios, grupos y dominios mediante (Java), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión. Para obtener más información, vea [Configurar propiedades de conexión ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. Invoque las operaciones de usuario o grupo adecuadas.

   Para buscar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceClient` para buscar principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipals` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`).

   Dado que el valor devuelto en este caso es un(a) `java.util.List` que contiene `Principal` objetos, iterar por el resultado y convertir los objetos `Principal` en objetos `User` o `Group`.

   Con el objeto `User` o `Group` resultante (que heredan de la interfaz `Principal`), recupere la información que necesite en los flujos de trabajo. Por ejemplo, los valores de nombre de dominio y nombre canónico, en combinación, identifican de forma exclusiva un principal. Se recuperan invocando los métodos `getDomainName` y `getCanonicalName` del objeto `Principal`, respectivamente.

   Para eliminar un usuario local, invoque el método `deleteLocalUser` del objeto `DirectoryManagerServiceClient` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `deleteLocalGroup` del objeto `DirectoryManagerServiceClient` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de usuarios y grupos mediante la API de servicio web {#managing-users-and-groups-using-the-web-service-api}

Para administrar mediante programación usuarios, grupos y dominios mediante la API del servicio Directory Manager Service (servicio Web), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   * Crear un ensamblado de cliente de Microsoft .NET que consuma el WSDL de Directory Manager. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. (Vea [Crear un ensamblado de cliente .NET que utiliza codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Cree un cliente DirectoryManagerService.

   Cree un objeto `DirectoryManagerServiceService` utilizando el constructor de la clase de proxy.

1. Invoque las operaciones de usuario o grupo adecuadas.

   Para buscar un usuario o grupo, invoque uno de los métodos del objeto `DirectoryManagerServiceService` para buscar principales (ya que una entidad de seguridad puede ser un usuario o un grupo). En el ejemplo siguiente, se llama al método `findPrincipalsWithFilter` mediante un filtro de búsqueda (un objeto `PrincipalSearchFilter`). Cuando se usa un objeto `PrincipalSearchFilter`, las entidades de seguridad locales sólo se devuelven si la propiedad `isLocal` está establecida en `true`. Este comportamiento es diferente al que se produciría con la API de Java.

   >[!NOTE]
   >
   >Si no se especifica el número máximo de resultados en el filtro de búsqueda (a través del campo `PrincipalSearchFilter.resultsMax`), se devuelve un máximo de 1000 resultados. Este comportamiento es diferente al que se produce con la API de Java, en la que 10 resultados es el máximo predeterminado. Además, los métodos de búsqueda como `findGroupMembers` no arrojarán ningún resultado a menos que se especifique el número máximo de resultados en el filtro de búsqueda (por ejemplo, a través del campo `GroupMembershipSearchFilter.resultsMax`). Esto se aplica a todos los filtros de búsqueda que heredan de la clase `GenericSearchFilter`. Para obtener más información, consulte [Referencia de la API de AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Dado que el valor devuelto en este caso es un(a) `object[]` que contiene `Principal` objetos, iterar por el resultado y convertir los objetos `Principal` en objetos `User` o `Group`.

   Con el objeto `User` o `Group` resultante (que heredan de la interfaz `Principal`), recupere la información que necesite en los flujos de trabajo. Por ejemplo, los valores de nombre de dominio y nombre canónico, en combinación, identifican de forma exclusiva un principal. Se recuperan invocando los campos `domainName` y `canonicalName` del objeto `Principal`, respectivamente.

   Para eliminar un usuario local, invoque el método `deleteLocalUser` del objeto `DirectoryManagerServiceService` y pase el identificador del usuario.

   Para eliminar un grupo local, invoque el método `deleteLocalGroup` del objeto `DirectoryManagerServiceService` y pase el identificador del grupo.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Administración de funciones y permisos {#managing-roles-and-permissions}

En este tema se describe cómo puede utilizar la API del servicio Administrador de autorización (Java) para asignar, quitar y determinar funciones y permisos mediante programación.

En AEM Forms, una *función* es un grupo de permisos para acceder a uno o más recursos de nivel de sistema. Estos permisos se crean mediante Administración de usuarios y los aplican los componentes del servicio. Por ejemplo, un administrador podría asignar la función &quot;Autor del conjunto de directivas&quot; a un grupo de usuarios. Rights Management permitiría a los usuarios de ese grupo con esa función crear conjuntos de directivas a través de la consola de administración.

Existen dos tipos de funciones: *funciones predeterminadas* y *funciones personalizadas*. Los roles predeterminados (*roles del sistema)* ya residen en AEM Forms. Se da por hecho que el administrador no puede eliminar ni modificar las funciones predeterminadas y que, por lo tanto, son inmutables. Por lo tanto, las funciones personalizadas creadas por el administrador, que posteriormente puede modificarlas o eliminarlas, son mutables.

Las funciones facilitan la administración de permisos. Cuando se asigna una función a un principal, se asigna automáticamente un conjunto de permisos a ese principal y todas las decisiones específicas relacionadas con el acceso para el principal se basan en ese conjunto general de permisos asignados.

### Resumen de los pasos {#summary_of_steps-4}

Para administrar funciones y permisos, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthorizationManagerService.
1. Invoque las operaciones de rol o permiso correspondientes.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de AuthorizationManagerService**

Antes de poder realizar mediante programación una operación AuthorizationManagerService de User Management, debe crear un cliente AuthorizationManagerService. Con la API de Java, esto se logra creando un objeto `AuthorizationManagerServiceClient`.

**Invocar las operaciones de rol o permiso correspondientes**

Una vez creado el cliente de servicios, puede invocar las operaciones de rol o permiso. El cliente de servicio permite asignar, quitar y determinar funciones y permisos.

**Consulte también**

[Administración de funciones y permisos mediante la API de Java](users.md#managing-roles-and-permissions-using-the-java-api)

[Administración de funciones y permisos mediante la API de servicio web](users.md#managing-roles-and-permissions-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### Administración de funciones y permisos mediante la API de Java {#managing-roles-and-permissions-using-the-java-api}

Para administrar roles y permisos mediante la API del servicio Administrador de autorización (Java), realice las siguientes tareas:

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente AuthorizationManagerService.

   Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invoque las operaciones de rol o permiso correspondientes.

   Para asignar un rol a un principal, invoque el método `assignRole` del objeto `AuthorizationManagerServiceClient` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el identificador de rol
   * Matriz de `java.lang.String` objetos que contiene los identificadores principales.

   Para quitar una función de una entidad de seguridad, invoque el método `unassignRole` del objeto `AuthorizationManagerServiceClient` y pase los siguientes valores:

   * Un objeto `java.lang.String` que contiene el identificador de rol.
   * Matriz de `java.lang.String` objetos que contiene los identificadores principales.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Inicio rápido (modo SOAP): Administración de funciones y permisos mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Administración de funciones y permisos mediante la API de servicio web {#managing-roles-and-permissions-using-the-web-service-api}

Administre funciones y permisos mediante la API del servicio Administrador de autorización (servicio web):

1. Incluir archivos de proyecto.

   Cree un proyecto de Microsoft .NET que utilice MTOM. Asegúrese de utilizar la siguiente definición de WSDL: `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Reemplace `localhost` por la dirección IP del servidor que hospeda AEM Forms.

1. Cree un cliente AuthorizationManagerService.

   * Cree un objeto `AuthorizationManagerServiceClient` utilizando su constructor predeterminado.
   * Cree un objeto `AuthorizationManagerServiceClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms (por ejemplo, `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`). No necesita utilizar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio.
   * Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del campo `AuthorizationManagerServiceClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
   * Establezca el campo `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
   * Habilite la autenticación HTTP básica realizando las siguientes tareas:

      * Asigne el nombre de usuario de los formularios AEM Forms al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * Asigne el valor de contraseña correspondiente al campo `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * Asigne el valor constante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Invoque las operaciones de rol o permiso correspondientes.

   Para asignar un rol a un principal, invoque el método `assignRole` del objeto `AuthorizationManagerServiceClient` y pase los siguientes valores:

   * Un objeto `string` que contiene el identificador de rol
   * Un objeto `MyArrayOf_xsd_string` que contiene los identificadores principales.

   Para quitar una función de una entidad de seguridad, invoque el método `unassignRole` del objeto `AuthorizationManagerServiceService` y pase los siguientes valores:

   * Un objeto `string` que contiene el identificador de rol.
   * Matriz de `string` objetos que contiene los identificadores principales.

**Consulte también**

[Resumen de los pasos](users.md#summary-of-steps)

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Autenticar usuarios {#authenticating-users}

En este tema se describe cómo puede utilizar la API del servicio Administrador de autenticación (Java) para permitir que las aplicaciones cliente autentiquen a los usuarios mediante programación.

Es posible que se requiera autenticación de usuario para interactuar con una base de datos empresarial u otros repositorios empresariales que almacenen datos seguros.

Considere, por ejemplo, un escenario en el que un usuario introduce un nombre de usuario y una contraseña en una página web y envía los valores a un servidor de aplicaciones J2EE que aloja Forms. Una aplicación personalizada de Forms puede autenticar al usuario con el servicio Administrador de autenticación.

Si la autenticación se realiza correctamente, la aplicación tiene acceso a una base de datos empresarial segura. De lo contrario, se envía un mensaje al usuario para informarle de que no es un usuario autorizado.

El diagrama siguiente muestra el flujo lógico de la aplicación.

![au_au_umauth_process](assets/au_au_umauth_process.png)

En la tabla siguiente se describen los pasos de este diagrama

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>El usuario tiene acceso a un sitio web y especifica un nombre de usuario y una contraseña. Esta información se envía a un servidor de aplicaciones J2EE que aloja AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Las credenciales de usuario se autentican con el servicio Administrador de autenticación. Si las credenciales de usuario son válidas, el flujo de trabajo continúa con el paso 3. De lo contrario, se envía un mensaje al usuario para informarle de que no es un usuario autorizado.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>La información del usuario y el diseño de un formulario se recuperan de una base de datos empresarial segura. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>La información del usuario se combina con un diseño de formulario y este se procesa para el usuario. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-5}

Para autenticar mediante programación a un usuario, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente AuthenticationManagerService.
1. Invoque la operación de autenticación.
1. Si es necesario, recupere el contexto para que la aplicación cliente pueda reenviarlo a otro servicio de AEM Forms para la autenticación.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de AuthenticationManagerService**

Para poder autenticar a un usuario mediante programación, debe crear un cliente AuthenticationManagerService. Al usar la API de Java, cree un objeto `AuthenticationManagerServiceClient`.

**Invocar la operación de autenticación**

Una vez creado el cliente de servicios, puede invocar la operación de autenticación. Esta operación necesita información sobre el usuario, como su nombre y contraseña. Si el usuario no se autentica, se genera una excepción.

**Recuperar el contexto de autenticación**

Una vez autenticado el usuario, puede crear un contexto basado en el usuario autenticado. A continuación, puede utilizar el contenido para invocar otros servicios de AEM Forms. Por ejemplo, puede usar el contexto para crear un `EncryptionServiceClient` y cifrar un documento de PDF con una contraseña. Asegúrese de que el usuario autenticado tenga la función denominada `Services User` necesaria para invocar un servicio de AEM Forms.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Autenticar a un usuario mediante la API de Java {#authenticate-a-user-using-the-java-api}

Autenticar a un usuario mediante la API del servicio Administrador de autenticación (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente AuthenticationManagerServices.

   Cree un objeto `AuthenticationManagerServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Invoque la operación de autenticación.

   Invoque el método `authenticate` del objeto `AuthenticationManagerServiceClient` y pase los siguientes valores:

   * Objeto `java.lang.String` que contiene el nombre del usuario.
   * Matriz de bytes (un objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` invocando el método `getBytes` del objeto `java.lang.String`.

   El método authenticate devuelve un objeto `AuthResult`, que contiene información sobre el usuario autenticado.

1. Recupere el contexto de autenticación.

   Invoque el método `getContext` del objeto `ServiceClientFactory`, el cual devolverá un objeto `Context`.

   A continuación, invoque el método `initPrincipal` del objeto `Context` y pase `AuthResult`.

### Autenticar a un usuario mediante la API de servicio web {#authenticate-a-user-using-the-web-service-api}

Autenticar a un usuario mediante la API del servicio Administrador de autenticación (servicio web):

1. Incluir archivos de proyecto.

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de Authentication Manager. (Consulte [Invocación de AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)).
   * Hacer referencia al ensamblado de cliente de Microsoft .NET. (Consulte &quot;Hacer referencia al ensamblado de cliente .NET&quot; en [Invocar AEM Forms mediante codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. Cree un cliente AuthenticationManagerService.

   Cree un objeto `AuthenticationManagerServiceService` utilizando el constructor de la clase de proxy.

1. Invoque la operación de autenticación.

   Invoque el método `authenticate` del objeto `AuthenticationManagerServiceClient` y pase los siguientes valores:

   * Objeto `string` que contiene el nombre del usuario
   * Matriz de bytes (un objeto `byte[]`) que contiene la contraseña del usuario. Puede obtener el objeto `byte[]` convirtiendo un objeto `string` que contenga la contraseña en una matriz `byte[]` mediante la lógica que se muestra en el ejemplo siguiente.
   * El valor devuelto será un objeto `AuthResult`, que se puede usar para recuperar información sobre el usuario. En el ejemplo siguiente, la información del usuario se recupera obteniendo primero el campo `authenticatedUser` del objeto `AuthResult` y, a continuación, los campos `canonicalName` y `domainName` del objeto `User` resultante.

**Consulte también**

[Invocar AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sincronización de usuarios mediante programación {#programmatically-synchronizing-users}

Puede sincronizar usuarios mediante programación utilizando la API de administración de usuarios. Al sincronizar usuarios, está actualizando AEM Forms con los datos de usuario que se encuentran en su repositorio de usuarios. Por ejemplo, supongamos que agrega nuevos usuarios al repositorio de usuarios. Después de realizar una operación de sincronización, los nuevos usuarios se convierten en usuarios de formularios AEM Forms. Además, los usuarios que ya no estén en su repositorio de usuarios se eliminarán de AEM Forms.

El diagrama siguiente muestra la sincronización de AEM Forms con un repositorio de usuario.

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

En la tabla siguiente se describen los pasos de este diagrama

<table>
 <thead>
  <tr>
   <th><p>Paso</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Una aplicación cliente solicita que AEM Forms realice una operación de sincronización.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms realiza una operación de sincronización.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Se ha actualizado la información del usuario.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Un usuario puede ver la información actualizada del usuario. </p></td>
  </tr>
 </tbody>
</table>

### Resumen de los pasos {#summary_of_steps-6}

Para sincronizar usuarios mediante programación, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un cliente UserManagerUtilServiceClient.
1. Especifique el dominio de empresa.
1. Invoque la operación de autenticación.
1. Determine si la operación de sincronización ha finalizado

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un UserManagerUtilServiceClientclient**

Para poder sincronizar usuarios mediante programación, debe crear un objeto `UserManagerUtilServiceClient`.

**Especifique el dominio de empresa**

Antes de realizar una operación de sincronización mediante la API de administración de usuarios, debe especificar el dominio de empresa al que pertenecen los usuarios. Puede especificar uno o varios dominios de empresa. Para poder realizar mediante programación una operación de sincronización, debe configurar un dominio de empresa mediante la consola de administración. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Invocar la operación de sincronización**

Después de especificar uno o varios dominios de empresa, puede realizar la operación de sincronización. El tiempo que se tarda en realizar esta operación depende del número de registros de usuario que hay en el repositorio de usuario.

**Determine si la operación de sincronización se ha completado**

Después de realizar mediante programación una operación de sincronización, puede determinar si la operación ha finalizado.

**Consulte también**

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicios rápidos de API de User Manager](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[Cifrar documentos de PDF con una contraseña](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Sincronización mediante programación de usuarios mediante la API de Java {#programmatically-synchronizing-users-using-the-java-api}

Sincronizar usuarios mediante la API de administración de usuarios (Java):

1. Incluir archivos de proyecto.

   Incluya archivos JAR de cliente, como adobe-usermanager-client.jar y adobe-usermanager-util-client.jar, en la ruta de clase del proyecto Java.

1. Cree un cliente UserManagerUtilServiceClient.

   Cree un objeto `UserManagerUtilServiceClient` utilizando su constructor y pasando un objeto `ServiceClientFactory` que contenga propiedades de conexión.

1. Especifique el dominio de empresa.

   * Invoque el método `scheduleSynchronization` del objeto `UserManagerUtilServiceClient` para iniciar la operación de sincronización de usuarios.
   * Crear una instancia de `java.util.Set` mediante un constructor de `HashSet`. Asegúrese de especificar `String` como tipo de datos. Esta instancia de `Java.util.Set` almacena los nombres de dominio a los que se aplica la operación de sincronización.
   * Para que se agregue cada nombre de dominio, invoque el método add del objeto `java.util.Set` y pase el nombre de dominio.

1. Invoque la operación de sincronización.

   Invoque el método `getContext` del objeto `ServiceClientFactory`, el cual devolverá un objeto `Context`.

   A continuación, invoque el método `initPrincipal` del objeto `Context` y pase `AuthResult`.

**Consulte también**

[Sincronización de usuarios mediante programación](users.md#programmatically-synchronizing-users)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
