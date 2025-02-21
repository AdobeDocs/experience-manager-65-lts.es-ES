---
title: Personalización de la consola de bienvenida (IU clásica)
description: La consola de bienvenida proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 6%

---

# Personalización de la consola de bienvenida (IU clásica){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Esta página trata sobre la IU clásica de.
>
>Consulte [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md) para obtener más información sobre la IU táctil estándar.

La consola de bienvenida proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

Es posible configurar los vínculos que son visibles. Esto se puede definir para usuarios o grupos específicos. Las acciones que se deben realizar dependen del tipo de destino (que se correlaciona con la sección de la consola en la que se encuentran):

* [Consolas principales](#links-in-main-console-left-pane) - Vínculos en la consola principal (panel izquierdo)
* [Recursos, documentación y referencia, características](#links-in-sidebar-right-pane) - Vínculos en la barra lateral (panel derecho)

## Vínculos en la consola principal (panel izquierdo) {#links-in-main-console-left-pane}

Esta lista enumera las consolas principales de AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Configuración de si los vínculos de la consola principal están visibles {#configuring-whether-main-console-links-are-visible}

Los permisos de nivel de nodo determinan si el vínculo se puede ver o no. Los nodos en cuestión son:

* **Sitios web:** `/libs/wcm/core/content/siteadmin`

* **Assets digital:** `/libs/wcm/core/content/damadmin`

* **Comunidad:** `/libs/collab/core/content/admin`

* **Campañas:** `/libs/mcm/content/admin`

* **Bandeja de entrada:** `/libs/cq/workflow/content/inbox`

* **Usuarios:** `/libs/cq/security/content/admin`

* **Herramientas:** `/libs/wcm/core/content/misc`

* **Etiquetado:** `/libs/cq/tagging/content/tagadmin`

Por ejemplo:

* Para restringir el acceso a **Herramientas**, quite el acceso de lectura de

  `/libs/wcm/core/content/misc`

Consulte la [sección Seguridad](/help/sites-administering/security.md) para obtener más información sobre cómo establecer los permisos deseados.

### Vínculos en la barra lateral (panel derecho) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Estos vínculos se basan en la existencia de *y* acceso de lectura a los nodos en la siguiente ruta:

`/libs/cq/core/content/welcome`

Hay tres secciones (separadas ligeramente) proporcionadas de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td><strong>Recursos</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Services</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Flujos de trabajo</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Administración de tareas</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Replicación</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Informes</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Publicaciones</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manuscritos</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Documentación y referencia</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Documentación</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Medios del desarrollador</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Características</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Paquetes</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Uso compartido de paquetes</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Clúster</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Copia de seguridad</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Consola web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Volcado de estado de la consola web <br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Configurar si los vínculos de la barra lateral son visibles {#configuring-whether-sidebar-links-are-visible}

Es posible ocultar un vínculo de usuarios o grupos específicos eliminando el acceso de lectura a los nodos que representan el vínculo.

* Recursos: eliminar acceso a:

  `/libs/cq/core/content/welcome/resources/<link-target>`

* Documentos: eliminar acceso a:

  `/libs/cq/core/content/welcome/docs/<link-target>`

* Funciones: eliminar acceso a:

  `/libs/cq/core/content/welcome/features/<link-target>`

Por ejemplo:

* Para quitar el vínculo a **Informes**, quite el acceso de lectura de

  `/libs/cq/core/content/welcome/resources/reports`

* Para quitar el vínculo a **Paquetes**, quite el acceso de lectura de

  `/libs/cq/core/content/welcome/features/packages`

Consulte la [sección Seguridad](/help/sites-administering/security.md) para obtener más información sobre cómo establecer los permisos deseados.

### Mecanismo de selección de vínculos {#link-selection-mechanism}

En `/libs/cq/core/components/welcome/welcome.jsp` se usa [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), que ejecuta una consulta en nodos que tienen la propiedad:

* `jcr:mixinTypes` con el valor: `cq:Console`

>[!NOTE]
>
>Ejecute la siguiente consulta para ver la lista existente:
>
>* `select * from cq:Console`
>

Cuando un usuario o grupo no tiene permiso de lectura en un nodo con el mixin `cq:Console`, la búsqueda `ConsoleUtil` no recupera ese nodo, por lo que no aparece en la consola.

### Agregar un elemento personalizado {#adding-a-custom-item}

El [mecanismo de selección de vínculos](#link-selection-mechanism) se puede usar para agregar su propio elemento personalizado a la lista de vínculos.

Agregue su elemento personalizado a la lista agregando el mixin `cq:Console` a su widget o recurso. Esto se hace definiendo la propiedad:

* `jcr:mixinTypes` con el valor: `cq:Console`
