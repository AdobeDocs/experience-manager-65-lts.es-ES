---
title: Aprovisionar usuarios justo a tiempo
description: Utilice el aprovisionamiento Just-In-Time para agregar usuarios a Administración de usuarios después de la autenticación correcta y asignar dinámicamente funciones y grupos relevantes al nuevo usuario.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---

# Aprovisionar usuarios justo a tiempo {#just-in-time-user-provisioning}

Los formularios AEM Forms admiten el aprovisionamiento Just-In-Time de usuarios que aún no existen en Administración de usuarios. Con el aprovisionamiento Just-In-Time, los usuarios se agregan automáticamente a Administración de usuarios después de que sus credenciales se hayan autenticado correctamente. Además, las funciones y los grupos relevantes se asignan dinámicamente al nuevo usuario.

## Necesidad de aprovisionamiento de usuarios justo a tiempo {#need-for-just-in-time-user-provisioning}

Así es como funciona la autenticación tradicional:

1. Cuando un usuario intenta iniciar sesión en los formularios de AEM, Administración de usuarios pasa las credenciales del usuario secuencialmente a todos los proveedores de autenticación disponibles. (Las credenciales de inicio de sesión incluyen una combinación de nombre de usuario y contraseña, vale Kerberos, firma PKCS7, etc.).
1. El proveedor de autenticación valida las credenciales.
1. A continuación, el proveedor de autenticación comprueba si el usuario existe en la base de datos de administración de usuarios. Los siguientes resultados son posibles:

   **Existe:** Si el usuario está actualizado y desbloqueado, Administración de usuarios devuelve la autenticación correcta. Sin embargo, si el usuario no está actualizado o bloqueado, Administración de usuarios devolverá un error de autenticación.

   **No existe:** La administración de usuarios devuelve un error de autenticación.

   **No válido:** La administración de usuarios devuelve un error de autenticación.

1. Se evalúa el resultado devuelto por el proveedor de autenticación. Si el proveedor de autenticación devolvió la autenticación correctamente, el usuario podrá iniciar sesión. De lo contrario, Administración de usuarios consulta con el siguiente proveedor de autenticación (pasos 2-3).
1. Se devuelve un error de autenticación si ningún proveedor de autenticación disponible valida las credenciales del usuario.

Cuando se implementa el aprovisionamiento Just-In-Time, se crea un nuevo usuario de forma dinámica en Administración de usuarios si uno de los proveedores de autenticación valida las credenciales del usuario. (Después del paso 3 del procedimiento de autenticación tradicional, más arriba).

## Implementación del aprovisionamiento de usuarios justo a tiempo {#implement-just-in-time-user-provisioning}

### API para el aprovisionamiento justo a tiempo {#apis-for-just-in-time-provisioning}

Los formularios AEM Forms proporcionan las siguientes API para el aprovisionamiento Just-In-Time:

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Consideraciones al crear un dominio habilitado para justo a tiempo {#considerations-while-creating-a-just-in-time-enabled-domain}

* Al crear un(a) `IdentityCreator` personalizado para un dominio híbrido, asegúrese de especificar una contraseña ficticia para el usuario local. No deje este campo de contraseña vacío.
* Recomendación: utilice `DomainSpecificAuthentication` para validar las credenciales de usuario con un dominio específico.

### Crear un dominio habilitado para justo a tiempo {#create-a-just-in-time-enabled-domain}

1. Escriba un DSC que implemente las API en la sección &quot;API para el aprovisionamiento Just-In-Time&quot;.
1. Implemente el DSC en el servidor de Forms.
1. Cree un dominio habilitado para justo a tiempo:

   * En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios > Nuevo dominio de empresa.
   * Configure el dominio y seleccione Habilitar aprovisionamiento Just In Time. <!--Fix broken link (See Setting up and managing domains).-->
   * Agregar proveedores de autenticación. Al agregar proveedores de autenticación, en la pantalla Nueva autenticación, seleccione un creador de identidad y un proveedor de asignación registrados.

1. Guarde el nuevo dominio.

## Entre bastidores {#behind-the-scenes}

Supongamos que un usuario está intentando iniciar sesión en formularios AEM y que un proveedor de autenticación acepta sus credenciales de usuario. Si el usuario aún no existe en la base de datos de administración de usuarios, se produce un error en la comprobación de identidad del usuario. AEM Forms ahora realiza las siguientes acciones:

1. Cree un objeto `UserProvisioningBO` con los datos de autenticación y colóquelo en un mapa de credenciales.
1. Según la información de dominio devuelta por `UserProvisioningBO`, recupere e invoque los dominios registrados `IdentityCreator` y `AssignmentProvider` para el dominio.
1. Invocar `IdentityCreator`. Si devuelve un `AuthResponse` correcto, extraiga `UserInfo` del mapa de credenciales. Páselo a `AssignmentProvider` para la asignación de grupos/funciones y cualquier otro procesamiento posterior después de crear el usuario.
1. Si el usuario se ha creado correctamente, indique que el intento de inicio de sesión del usuario se ha realizado correctamente.
1. En el caso de los dominios híbridos, extraiga la información del usuario de los datos de autenticación proporcionados al proveedor de autenticación. Si esta información se obtiene correctamente, cree el usuario sobre la marcha.

>[!NOTE]
>
>La característica de aprovisionamiento Just-In-Time se distribuye con una implementación predeterminada de `IdentityCreator` que puede utilizar para crear usuarios de forma dinámica. Los usuarios se crean con la información asociada a los directorios del dominio.
