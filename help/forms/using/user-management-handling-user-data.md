---
title: Administrar usuarios de Forms | Administración de datos de usuario
description: Descubra cómo el componente Administración de usuarios JEE de AEM Forms le permite crear, autorizar y administrar usuarios que necesitan acceso a AEM Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 72%

---

# Administrar usuarios de Forms | Administración de datos de usuario {#forms-user-management-handling-user-data}

La administración de usuarios es un componente JEE de AEM Forms que permite crear, administrar y autorizar a los usuarios de AEM Forms para que accedan a AEM Forms. La administración de usuarios utiliza los dominios como directorios para obtener información del usuario. Se admiten los siguientes tipos de dominio:

**Dominios locales**: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de Administración de usuarios. Las contraseñas se almacenan localmente y la autenticación se realiza mediante una base de datos local.

**Dominios híbridos**: Este tipo de dominio no está conectado a un sistema de almacenamiento de terceros. En su lugar, los usuarios y grupos se crean localmente y residen en la base de datos de administración de usuarios. A diferencia de los dominios locales, los dominios híbridos utilizan un proveedor de autenticación externa, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

**Dominios empresariales**: Consta de usuarios y grupos que residen en un sistema de almacenamiento de terceros, como un directorio LDAP. Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, Administración de usuarios sincroniza la información de usuarios y grupos con la base de datos de Administración de usuarios. Los dominios empresariales también utilizan un proveedor de autenticación externo, que puede ser LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

Administración de usuarios almacena datos de usuarios en una base de datos, como My Sql, Oracle, MS® SQL Server y IBM® DB2®. Además, cualquier usuario que haya iniciado sesión al menos una vez en aplicaciones de Forms en Autor de AEM en `https://'[server]:[port]'lc`, se crea el usuario en un repositorio de AEM. Por lo tanto, la administración de usuarios se almacena en los siguientes almacenamientos de datos:

* Base de datos
* Repositorio de AEM
* Almacenamiento de terceros como directorio LDAP

>[!NOTE]
>
>Los datos almacenados en almacenes de terceros están fuera de ámbito para este documento. Póngase en contacto directamente con el proveedor de terceros para administrar los datos de usuario en dichos almacenamientos.

### Base de datos {#database}

Administración de usuarios almacena los datos de usuario en las siguientes tablas de base de datos:

<table>
 <tbody>
  <tr>
   <td>Tabla de base de datos</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Almacena información sobre entidades principales. Principal puede ser un usuario, un grupo o una función.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Almacena información de identificación personal (PII) de los usuarios. Contiene una entrada para cada usuario de dominios locales, empresariales e híbridos.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Bases de datos de Oracle y MS® SQL)</p> </td>
   <td>Almacena datos solo para usuarios locales.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Bases de datos de Oracle y MS® SQL)</p> </td>
   <td>Contiene entradas de todos los usuarios de dominios locales, empresariales e híbridos. Contiene los ID de correo electrónico del usuario.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (Bases de datos de Oracle y MS® SQL)</p> </td>
   <td>Almacena la asignación entre usuarios y grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Almacena la asignación entre funciones y principales para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Almacena la asignación entre principales y permisos para usuarios y grupos.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (Bases de datos de Oracle y MS® SQL)</p> </td>
   <td>Almacena los valores de atributo antiguos y nuevos correspondientes a un principal.<br /> </td>
  </tr>
 </tbody>
</table>

### Repositorio de AEM {#aem-repository}

Los datos de administración de usuarios para usuarios que hayan accedido al menos una vez a las aplicaciones de Forms en `https://'[server]:[port]'lc` también se almacenan en el repositorio de AEM.

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de administración de usuarios y exportarlos para los usuarios de las bases de datos de administración de usuarios y repositorio de AEM y, si es necesario, eliminarlos de forma permanente.

### Base de datos {#database-1}

Para exportar o eliminar datos de usuario de la base de datos de administración de usuarios, debe conectarse a la base de datos mediante un cliente de base de datos y averiguar el ID principal en función de alguna PII del usuario. Por ejemplo, para recuperar el ID principal de un usuario mediante un ID de inicio de sesión, ejecute el siguiente comando `select` en la base de datos.

En el comando `select` reemplace `<user_login_id>` con el ID de inicio de sesión del usuario cuyo ID principal desea recuperar.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una vez que conozca el ID principal, puede exportar o eliminar los datos del usuario.

#### Exportar datos de usuario {#export-user-data}

Ejecute los siguientes comandos de base de datos para poder exportar los datos de administración de usuarios para un ID principal desde las tablas de base de datos. En el comando `select`, reemplace `<principal_id>` con el ID principal del usuario cuyos datos desee exportar.

>[!NOTE]
>
>Los siguientes comandos utilizan nombres de tabla de base de datos en bases de datos My SQL y IBM® DB2®. Cuando ejecute estos comandos en bases de datos de Oracle y MS® SQL, reemplace los siguientes nombres de tabla en los comandos:
>
>* Reemplace `EdcPrincipalLocalAccountEntity` por `EdcPrincipalLocalAccount`
>
>* Reemplace `EdcPrincipalEmailAliasEntity` por `EdcPrincipalEmailAliasEn`
>
>* Reemplace `EdcPrincipalMappingEntity` por `EdcPrincipalMappingEntit`
>
>* Reemplace `EdcPrincipalGrpCtmntEntity` por `EdcPrincipalGrpCtmntEnti`
>

```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Eliminar los datos de usuario {#delete-user-data}

Haga lo siguiente para eliminar los datos de administración de usuarios de un ID principal de las tablas de la base de datos.

1. Elimine los datos de usuario del repositorio de AEM, si corresponde, tal como se describe en [Eliminar los datos de usuario](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Apague el servidor de AEM Forms.
1. Ejecute los siguientes comandos de base de datos para poder eliminar los datos de administración de usuarios para un ID principal desde las tablas de base de datos. En el `Delete` comando, reemplace `<principal_id>` por el ID principal del usuario cuyos datos desee eliminar.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Inicie AEM Forms Server.

### Repositorio de AEM {#aem-repository-1}

Los usuarios de JEE de Forms tienen sus datos en el repositorio de AEM si han accedido al menos a una instancia de autor de AEM Forms. Puede acceder a sus datos de usuario y eliminarlos del repositorio de AEM.

#### Acceder a los datos de usuario {#access-user-data}

Para ver el usuario creado en el repositorio de AEM, inicie sesión en `https://'[server]:[port]'/lc/useradmin` con las credenciales de administrador de AEM. Tenga en cuenta que `server` y `port` en la URL son las de la instancia de autor de AEM. Aquí puede buscar usuarios con su nombre de usuario. Haga doble clic en un usuario para poder ver información como propiedades, permisos y grupos para el usuario. La propiedad `Path` para un usuario especifica la ruta al nodo de usuario creado en el repositorio de AEM.

#### Eliminar los datos de usuario {#delete-aem}

Para eliminar un usuario:

1. Vaya a `https://'[server]:[port]'/lc/useradmin` con las credenciales de administrador de AEM.
1. Busque un usuario y haga doble clic en el nombre de usuario para abrir las propiedades de usuario. Copie la propiedad `Path`.
1. Vaya a AEM CRXDE Lite en `https://'[server]:[port]'/lc/crx/de/index.jsp` y navegue o busque la ruta del usuario.
1. Elimine la ruta y haga clic en **[!UICONTROL Guardar todo]** para eliminar permanentemente el usuario del repositorio de AEM.
