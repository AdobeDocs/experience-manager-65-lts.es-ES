---
title: Seguridad de los documentos | Administrar datos de usuario
description: Obtenga información sobre cómo AEM Forms Document Security le permite administrar los datos de usuario y los almacenes de datos, así como acceder, eliminar y exportar datos de usuario.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 69%

---

# Seguridad de los documentos | Administrar datos de usuario {#document-security-handling-user-data}

AEM Forms Document Security permite crear, almacenar y aplicar configuraciones de seguridad predefinidas a los documentos. Garantiza que solo los usuarios autorizados puedan utilizar los documentos. Puede proteger los documentos mediante políticas. Una directiva es una recopilación de información que incluye configuraciones de seguridad y una lista de usuarios autorizados. Puede aplicar una directiva a uno o varios documentos y autorizar a los usuarios que se agregan en la administración de usuarios JEE de AEM Forms.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

La seguridad de los documentos almacena directivas y datos relacionados con documentos protegidos, incluidos datos de usuario, en una base de datos, como My Sql, Oracle, MS® SQL Server y IBM® DB2®. Además, los datos de los usuarios autorizados en una directiva se almacenan en la administración de usuarios. Para obtener información sobre los datos almacenados en la administración de usuarios, consulte [Administrar usuarios de Forms: Administrar datos de usuario](/help/forms/using/user-management-handling-user-data.md).

La siguiente tabla muestra cómo la seguridad de documentos organiza los datos en las tablas de la base de datos.

<table>
 <tbody>
  <tr>
   <td>Tabla de base de datos</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Almacena información sobre claves principales para los usuarios. Las claves se utilizan en flujos de trabajo de seguridad de documentos sin conexión.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Almacena información sobre la auditoría de eventos como eventos de usuario, eventos de documento y eventos de directivas.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Almacena el registro de un documento protegido. Almacena los detalles de licencia de cada documento protegido.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>Almacena el nombre del documento para cada licencia creada en el sistema.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>Almacena información sobre la revocación y la reincorporación de documentos protegidos.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>Almacena información sobre los usuarios que pueden crear directivas personales que aparecen en la pestaña Mis directivas de la página Directivas. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Almacena información sobre directivas. Cada directiva corresponde a una fila de esta tabla.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Almacena archivos XML para directivas activas. Un XML de directiva<sup> </sup>contiene referencias a ID principales de usuarios asociados a ella. El XML de directiva se almacena como objeto Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Almacena información sobre directivas archivadas. Una directiva archivada contiene su XML de directiva almacenado como objeto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code><br /> (Bases de datos de Oracle y MS® SQL)</p> </td>
   <td>Almacena la asignación entre el conjunto de directivas y los usuarios.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Almacena información sobre usuarios invitados.</td>
  </tr>
 </tbody>
</table>

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de seguridad de los documentos y exportarlos para los usuarios de las bases de datos, y si es necesario, eliminarlos de forma permanente.

Para exportar o eliminar datos de usuario de una base de datos, debe conectarse a la base de datos mediante un cliente de la base de datos y averiguar el ID principal en función de alguna información personal del usuario. Por ejemplo, para recuperar el ID principal de un usuario mediante un ID de inicio de sesión, ejecute el siguiente comando `select` en la base de datos.

En el comando `select` sustituya `<user_login_id>` con el ID de inicio de sesión del usuario cuyo ID principal desee recuperar de la tabla de la base de datos `EdcPrincipalUserEntity`.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una vez que conozca el ID principal, puede exportar o eliminar los datos del usuario.

### Exportar datos de usuario {#export-user-data}

Ejecute los siguientes comandos de base de datos para poder exportar los datos de usuario para un ID principal desde las tablas de base de datos. En el comando `select`, reemplace `<principal_id>` con el ID principal del usuario cuyos datos desee exportar.

>[!NOTE]
>
>Los siguientes comandos utilizan nombres de tabla de base de datos en bases de datos My SQL y IBM® DB2®. Cuando ejecute estos comandos en bases de datos de Oracle y MS® SQL, reemplace `EdcPolicySetPrincipalEntity` por `EdcPolicySetPrincipalEnt` en los comandos.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>Para exportar datos desde la tabla `EdcAuditEntity`, utilice la API [EventManager.exportEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que toma [EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parámetro para exportar datos de auditoría basados en `principalId`, `policyId`o `licenseId`.

Para obtener datos completos sobre un usuario del sistema, debe acceder a los datos de la base de datos de administración de usuarios y exportarlos. Para obtener más información, consulte [Administrar usuarios de Forms: Administrar datos de usuario](/help/forms/using/user-management-handling-user-data.md).

### Eliminar los datos de usuario {#delete-user-data}

Haga lo siguiente para eliminar los datos de seguridad del documento para un ID principal de las tablas de la base de datos.

1. Apague el servidor de AEM Forms.
1. Ejecute los siguientes comandos de base de datos para poder eliminar los datos del ID principal de las tablas de base de datos para la seguridad del documento. En el `Delete` comando, reemplace `<principal_id>` por el ID principal del usuario cuyos datos desee eliminar.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Para eliminar datos de la tabla `EdcAuditEntity`, utilice la API [EventManager.deleteEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que toma [EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parámetro para eliminar datos de auditoría basados en `principalId`, `policyId` o `licenseId`.

1. Los archivos XML de directivas activas y archivadas se almacenan en las tabla de la base de datos `EdcPolicyXmlEntity` y `EdcPolicyArchiveEntity`, respectivamente. Para eliminar datos de un usuario de estas tablas, haga lo siguiente:

   1. Abra el blob XML de cada fila en la tabla `EdcPolicyXMLEntity` o `EdcPolicyArchiveEntity` y extraiga el archivo XML. El archivo XML es similar al que se muestra a continuación.
   1. Edite el archivo XML para poder quitar el blob del ID principal.
   1. Repita los pasos 1 y 2 para el otro archivo.

   >[!NOTE]
   >
   >Elimine el blob completo dentro de la etiqueta `Principal` para un ID principal o el XML de directiva podría dañarse o inutilizarse.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   Además de eliminar datos directamente de la tabla `EdcPolicyXmlEntity`, hay dos formas más de hacerlo:

   **Usar la consola de administración**

   1. Inicie sesión como administrador en la consola de administración de Forms JEE en https://[*server*]:[*port*]/adminui.
   1. Navegue hasta **[!UICONTROL Servicios > Seguridad de documentos > Conjuntos de directivas]**.
   1. Abra un conjunto de directivas y elimine el usuario de la directiva.

   **Usar la página web de seguridad de documentos**

   Los usuarios de seguridad de documentos que tengan permisos para crear directivas personales pueden eliminar datos de usuario de sus directivas. Para ello:

   1. Los usuarios que tengan directivas personales deben iniciar sesión en su página web de seguridad de documentos en https://[*server*]:[*port*]/edc.
   1. Navegar hasta **[!UICONTROL Servicios > Seguridad de documentos > Mis directivas]**.
   1. Abrir una directiva y eliminar el usuario de ella.

   >[!NOTE]
   >
   >Los administradores pueden buscar, acceder y eliminar datos de usuario de las directivas personales de otros usuarios en **[!UICONTROL Servicios > Seguridad de documentos > Mis directivas]** mediante la consola de administración.

1. Eliminar los datos del ID principal de la base de datos de administración de usuarios. Para ver los pasos detallados, consulte [Administrar usuarios de Forms | Administrar datos de usuario](/help/forms/using/user-management-handling-user-data.md).
1. Inicie AEM Forms Server.
