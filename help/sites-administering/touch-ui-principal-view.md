---
title: Vista principal para la administración de permisos
description: Obtenga información acerca de la nueva interfaz de usuario táctil que facilita la administración de permisos.
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---


# Vista principal para la administración de permisos{#principal-view-for-permissions-management}

## Información general {#overview}

AEM 6.5 presenta la Administración de permisos para usuarios y grupos. La funcionalidad principal sigue siendo la misma que la IU clásica, pero es más fácil de usar y eficiente.

## Usos {#how-to-use}

### Acceso a la IU {#accessing-the-ui}

Se accede a la nueva administración de permisos basada en la interfaz de usuario a través de la tarjeta Permisos en Seguridad, como se muestra a continuación:

![IU de administración de permisos](assets/screen_shot_2019-03-17at63333pm.png)

La nueva vista facilita la visualización de todo el conjunto de privilegios y restricciones para un principal determinado en todas las rutas en las que se han concedido permisos explícitamente. Esto elimina la necesidad de ir a

CRXDE para administrar privilegios y restricciones avanzados. Se ha consolidado en la misma vista. La vista predeterminada es Grupo &quot;todos&quot;.

![Vista del grupo &quot;todos&quot;](assets/unu-1.png)

Hay un filtro que permite al usuario seleccionar el tipo de principales para ver **usuarios**, **grupos** o **todos** y buscar cualquier principal **.**

![Buscar tipos de identidades](assets/image2019-3-20_23-52-51.png)

### Visualización de permisos para una entidad principal {#viewing-permissions-for-a-principal}

El marco de la izquierda permite a los usuarios desplazarse hacia abajo para encontrar cualquier principal o buscar un grupo o un usuario en función del filtro seleccionado, como se muestra a continuación:

![Ver permisos para un principal](assets/doi-1.png)

Al hacer clic en el nombre, se muestran los permisos asignados a la derecha. El panel de permisos muestra la lista de entradas de control de acceso en rutas específicas junto con las restricciones configuradas.

![Ver lista ACL](assets/trei-1.png)

### Agregar una nueva entrada de control de acceso para una entidad principal {#adding-new-access-control-entry-for-a-principal}

Se pueden agregar nuevos permisos agregando una Entrada de control de acceso. Simplemente haga clic en el botón Agregar ACE.

![Agregar nueva ACL para un principal](assets/patru.png)

Esto abre la ventana que se muestra a continuación. El siguiente paso es elegir una ruta en la que se debe configurar el permiso.

![Configurar ruta de acceso de permisos](assets/cinci-1.png)

Aquí se selecciona una ruta donde puede configurar un permiso para **dam-users**:

![Ejemplo de configuración para usuarios dam](assets/sase-1.png)

Una vez seleccionada la ruta de acceso, el flujo de trabajo vuelve a esta pantalla, donde el usuario puede seleccionar uno o más de los privilegios de las áreas de nombres disponibles (como `jcr`, `rep` o `crx`), como se muestra a continuación.

Los privilegios se pueden añadir buscando en el campo de texto y seleccionando a continuación en la lista.

>[!NOTE]
>
>Para obtener una lista completa de privilegios y descripciones, consulte [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![Permiso de búsqueda para una ruta de acceso determinada.](assets/image2019-3-21_0-5-47.png) ![Agregar nueva entrada para &#39;dam-users&#39; como se muestra en una ruta seleccionada en columnas verticales.](assets/image2019-3-21_0-6-53.png)

Una vez seleccionada la lista de privilegios, el usuario puede elegir el Tipo de permiso : Denegar o Permitir, como se muestra a continuación.

![Seleccionar permiso](assets/screen_shot_2019-03-17at63938pm.png) ![Seleccionar permiso](assets/screen_shot_2019-03-17at63947pm.png)

### Uso de restricciones {#using-restrictions}

Además de la lista de privilegios y el Tipo de permiso en una ruta determinada, esta pantalla también le permite agregar restricciones para el control de acceso específico, como se muestra a continuación:

![Agregar restricciones](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Para obtener más información sobre el significado de cada restricción, consulte [la documentación de Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html?lang=es).

Las restricciones se pueden agregar como se muestra a continuación eligiendo el tipo de restricción, introduciendo el valor y pulsando el icono **+**.

![Agregar el tipo de restricción](assets/sapte-1.png) ![Agregar el tipo de restricción](assets/opt-1.png)

La nueva ACE se refleja en la Lista de control de acceso como se muestra a continuación. Tenga en cuenta que `jcr:write` es un privilegio agregado que incluye `jcr:removeNode` que se agregó anteriormente, pero no se muestra a continuación como cubierto en `jcr:write`.

### Edición de ACE {#editing-aces}

Las entradas de control de acceso se pueden editar seleccionando un principal y eligiendo el elemento ACE que desea editar.

Por ejemplo, aquí puede editar la siguiente entrada para **dam-users** haciendo clic en el icono de lápiz a la derecha:

![Agregar restricción](assets/image2019-3-21_0-35-39.png)

La pantalla de edición se muestra con las entradas de control de acceso configuradas preseleccionadas, que se pueden eliminar haciendo clic en el icono en forma de cruz junto a ellas o se pueden añadir nuevos privilegios para la ruta dada, como se muestra a continuación.

![Editar entrada](assets/noua-1.png)

Aquí se agrega el privilegio `addChildNodes` para **dam-users** en la ruta dada.

![Agregar privilegio](assets/image2019-3-21_0-45-35.png)

Los cambios se pueden guardar haciendo clic en el botón **Guardar** de la parte superior derecha, y se reflejan en los nuevos permisos para **dam-users**, como se muestra a continuación:

![Guardar cambios](assets/zece-1.png)

### Eliminación de ACE {#deleting-aces}

Las entradas de control de acceso se pueden eliminar para eliminar todos los permisos otorgados a una entidad de seguridad en una ruta específica. El icono X situado junto a ACE puede utilizarse para eliminarlo, como se muestra a continuación:

![Eliminar elementos ACE](assets/image2019-3-21_0-53-19.png) ![Eliminar elementos ACE](assets/unspe.png)

### Combinaciones de privilegios de IU clásica {#classic-ui-privilege-combinations}

La nueva interfaz de usuario de permisos utiliza explícitamente el conjunto básico de privilegios en lugar de combinaciones predefinidas que no reflejan realmente los privilegios subyacentes exactos que se concedieron.

Causó confusión sobre qué se está configurando exactamente. En la tabla siguiente se muestra la asignación entre las combinaciones de privilegios de la IU clásica a los privilegios reales que las constituyen:

<table>
 <tbody>
  <tr>
   <th>Combinaciones de privilegios de IU clásica</th>
   <th>Privilegio de IU de permisos</th>
  </tr>
  <tr>
   <td>Lectura</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modificar</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Crear</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Leer ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Editar ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Replicar</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
