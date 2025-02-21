---
title: Portal de Forms | Gestión de datos de usuario
description: Obtenga información acerca de la administración de datos de usuario, como acceso, eliminación y almacén de datos en AEM Forms Portal.
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 51%

---

# Portal de Forms | Gestión de datos de usuario {#forms-portal-handling-user-data}

El portal [!DNL AEM Forms] proporciona componentes que puede utilizar para ver una lista de los formularios adaptables, los formularios HTML5 y otros recursos de Forms en la página [!DNL AEM Sites]. Asimismo, puede configurarla para que muestre los borradores, los formularios adaptables enviados y los formularios HTML5 de un usuario que ha iniciado sesión. Para obtener más información sobre el portal de Forms, consulte [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md).

Cuando un usuario que ha iniciado sesión guarda un formulario adaptable como borrador o lo envía, se muestra en las pestañas Borradores y Envíos del portal de Forms. Los datos de los formularios redactados o enviados se almacenan en el almacén de datos configurado para la implementación de AEM. Los borradores y los envíos de los usuarios anónimos no se muestran en la página del portal de Forms; sin embargo, los datos se almacenan en el almacén de datos configurado. Consulte [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

## Almacenamiento de datos y datos de usuarios {#user-data-and-data-stores}

El portal de Forms almacena los datos de los borradores y los formularios enviados en los siguientes casos:

* La acción de envío configurada en el formulario adaptable es **Acción de envío del portal de formularios**.
* Para las acciones de envío distintas de **Acción de envío del portal de Forms**, la opción **[!UICONTROL Almacenar datos en el portal de Forms]** está habilitada en las propiedades **[!UICONTROL Envío]** del contenedor del formulario adaptable.

El portal de Forms almacena los siguientes datos sobre todos los borradores y los formularios enviados de los usuarios anónimos y los usuarios que han iniciado sesión:

* Los metadatos del formulario, como el nombre del formulario, la ruta, el ID de borrador o envío, la ruta de acceso de los archivos adjuntos y el ID de datos de usuario.
* Los archivos adjuntos del formulario como bytes de datos.
* Los datos del formulario como bytes de datos.

Según la persistencia del almacén de datos configurado, los datos de los borradores y los formulario enviados se almacenan en las siguientes ubicaciones.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistencia</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Ubicación</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predeterminado</p> </td>
   <td><p>Repositorio de instancias de autor y publicación de AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Repositorio de AEM de instancias de autor y remotas de AEM</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Base de datos</p> </td>
   <td><p>Repositorio de instancias de autor y tablas de bases de datos de AEM</p> </td>
   <td><code>data</code>, <code>metadata</code> y tablas de bases de datos <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de los borradores y los formularios enviados de los usuarios que han iniciado sesión y los usuarios anónimos desde los almacenes de datos configurados y, si es necesario, eliminarlos.

### Instancias de AEM {#aem-instances}

Todos los datos de los borradores y los formularios enviados de las instancias de AEM (de autor, publicación o remotas) de los usuarios que han iniciado sesión y los usuarios anónimos se almacenan en el nodo `/content/forms/fp/` del repositorio de AEM aplicable. Cada vez que un usuario anónimo o con la sesión iniciada guarda un borrador o envía un formulario, se genera un `draft ID` o `submission ID`, un `user data ID` y un `ID` aleatorio para cada archivo adjunto (si corresponde). Se asocia al borrador o al envío respectivo.

#### Acceder a los datos de usuario {#access-user-data}

Cuando un usuario que ha iniciado sesión guarda un borrador o envía un formulario, se crea un nodo secundario con su ID de usuario. Por ejemplo, los datos de los borradores y los envíos de Sarah Rose, cuyo ID de usuario es `srose`, se almacenan en el nodo `/content/forms/fp/srose/` del repositorio de AEM. En del nodo del ID de usuario, los datos se organizan en una estructura jerárquica.

La siguiente tabla explica cómo se almacenan los datos de todos los borradores de `srose` en el repositorio de AEM.

>[!NOTE]
>
>Una estructura idéntica a `drafts` se replica para los formularios enviados de `srose` en el nodo `/content/forms/fp/srose/submit/`.
>
>Todos los borradores y los envíos de los usuarios `anonymous` se almacenan en el nodo `/content/forms/fp/anonymous/`, el cual organiza los borradores y los envíos de todos los usuarios anónimos en los nodos `draft` y `submit`.

| Nodo | Descripción |
|---|---|
| `/content/forms/fp/srose/drafts` | Los datos de los nodos de contenedor de todos los borradores del usuario |
| `/content/forms/fp/srose/drafts/attachments/` | Organiza todos los archivos adjuntos del usuario en función del ID de borrador |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene un archivo adjunto para el ID seleccionado en formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organiza los metadatos de los formularios del usuario en función del ID de borrador |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene los metadatos de los formularios del ID de borrador seleccionado |
| `/content/forms/fp/srose/drafts/data/` | Organiza los datos de los formularios del usuario en función del ID de datos de usuario |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene los datos de formulario del ID de datos de usuario seleccionado en formato binario |

#### Eliminar los datos de usuario {#delete-user-data}

Para eliminar por completo los datos de usuario de los borradores y los envíos de un usuario que ha iniciado sesión de los sistemas de AEM, debe eliminar el nodo `user ID` de un usuario específico del nodo Autor. Elimine manualmente los datos de todas las instancias de AEM aplicables.

Los datos de los borradores y los envíos de todos los usuarios anónimos se almacenan en los nodos comunes `drafts` y `submit` en `/content/forms/fp/anonymous`. No existe ningún método para buscar los datos de un usuario anónimo en particular a menos que se conozca algún tipo de información identificable. En este caso, puede buscar información que identifique al usuario anónimo en el repositorio de AEM y eliminar manualmente el nodo que lo contiene de todas las instancias de AEM aplicables para eliminar los datos del sistema de AEM. Sin embargo, si desea eliminar los datos de todos los usuarios anónimos, puede eliminar el nodo `anonymous` para eliminar los datos de los borradores y los envíos de todos los usuarios anónimos.

### Base de datos {#database}

Cuando AEM está configurado para almacenar datos en una base de datos, los datos de los borradores y los envíos del portal de Forms se almacenan en las siguientes tablas de bases de datos para los usuarios que han iniciado sesión y los usuarios anónimos:

* data
* metadatos
* metadatos adicionales

#### Acceder a los datos de usuario {#access-user-data-1}

Para acceder a los datos de los borradores y los envíos de un usuario que ha iniciado sesión y un usuario anónimo en las tablas de bases de datos, ejecute el siguiente comando de base de datos. En la consulta, reemplace `logged-in user` por el ID de usuario a cuyos datos desea acceder, o por `anonymous` si se trata de un usuario anónimo.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Eliminar los datos de usuario {#delete-user-data-1}

Para eliminar los datos de los borradores y los envíos de un usuario que ha iniciado sesión desde las tablas de bases de datos, ejecute el siguiente comando de base de datos. En la consulta, reemplace `logged-in user` por el ID de usuario cuyos datos desea eliminar, o por `anonymous` si se trata de un usuario anónimo. Para eliminar los datos de un usuario anónimo en particular de la base de datos, debe encontrarlos utilizando algún tipo de información identificable y eliminarlos de las tablas de bases de datos que contengan la información.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
