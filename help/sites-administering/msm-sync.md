---
title: Configuración de la sincronización de Live Copy
description: Obtenga información acerca de la configuración de la sincronización de Live Copy.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
docset: aem65
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 25%

---

# Configuración de la sincronización de Live Copy{#configuring-live-copy-synchronization}

Realice las siguientes tareas para controlar cómo y cuándo se sincronizan las Live Copies con su contenido de origen.

* Decida si las configuraciones de despliegue existentes cumplen los requisitos o si necesita crear una o más.
* Especifique las configuraciones de despliegue que se utilizarán para las Live Copies.

## Configuraciones de despliegue instaladas y personalizadas {#installed-and-custom-rollout-configurations}

En esta sección se proporciona información sobre las configuraciones de despliegue instaladas, las acciones de sincronización que utilizan y cómo crear configuraciones personalizadas si es necesario.

>[!CAUTION]
>
>Se recomienda **no** actualizar o cambiar una configuración de despliegue predeterminada (instalada). Si hay algún requisito para una acción en directo personalizada, debe añadirse en una configuración de despliegue personalizada.

### Activadores de despliegue {#rollout-triggers}

Cada configuración de lanzamiento utiliza un activador de lanzamiento que hace que se produzca el lanzamiento. Las configuraciones de despliegue pueden utilizar uno de los siguientes activadores:

* **En el despliegue**: El comando **Despliegue** se usa en la página del modelo, o el comando **Sincronizar** se usa en la página de Live Copy.

* **En la modificación**: la página de origen se modifica.

* **En la activación**: la página de origen se activa.

* **En la desactivación**: la página de origen se desactiva.

>[!NOTE]
>
>El uso del déclencheur En la modificación puede afectar al rendimiento. Consulte [las prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md#onmodify) para obtener más información.

### Configuraciones de despliegue instaladas {#installed-rollout-configurations}

En la tabla siguiente se enumeran las opciones de configuración de despliegue que se instalan con AEM. La tabla incluye las acciones de déclencheur y sincronización de cada configuración de lanzamiento. Si las acciones de configuración de despliegue instaladas no cumplen con sus requisitos, puede [crear una configuración de despliegue](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>Nombre</th>
   <th>Descripción</th>
   <th>Activador</th>
   <th>Acciones de sincronización<br /> <br /> vea también <a href="#installed-synchronization-actions">Acciones de sincronización instaladas</a></th>
  </tr>
  <tr>
   <td>Configuración de lanzamiento estándar</td>
   <td>Configuración de lanzamiento estándar que permite iniciar procesos de lanzamiento en el déclencheur de lanzamiento y ejecuta acciones: crear, actualizar, eliminar contenido y ordenar nodos secundarios.</td>
   <td>En el despliegue</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Activar si se activa el modelo</td>
   <td>Publica la Live Copy cuando se publica el origen.</td>
   <td>En la activación</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>Desactivar si se desactiva el modelo</td>
   <td>Desactiva la Live Copy cuando se desactiva el origen.</td>
   <td>Al desactivar</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>Insertar al modificar</td>
   <td><p>Inserta el contenido en la Live Copy cuando se modifica el origen.</p> <p>Utilice esta configuración de despliegue con moderación, ya que utiliza el déclencheur En la modificación.</p> </td>
   <td>En la modificación</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>Insertar al modificar (superficial)</td>
   <td><p>Inserta el contenido en la Live Copy cuando se modifica la página del modelo, sin actualizar las referencias (por ejemplo, para copias superficiales).</p> <p>Utilice esta configuración de despliegue con moderación, ya que utiliza el déclencheur En la modificación.</p> </td>
   <td>En la modificación</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Promocionar lanzamiento</td>
   <td>Configuración de despliegue estándar para promocionar páginas con dicho fin.</td>
   <td>En el despliegue</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>Configuración de despliegue de contenido de página de catálogo</td>
   <td>Aplica plantillas de página de un modelo de catálogo.</td>
   <td>En el despliegue</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Configuración de despliegue de actualización de la página del catálogo</td>
   <td>Aplica propiedades de destino de un modelo de catálogo. Debe ejecutarse después de la configuración de despliegue de contenido de página de catálogo.</td>
   <td>En el despliegue</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>Configuración de despliegue de publicaciones de DPS</td>
   <td>Configuración de despliegue de publicación de DPS que permite iniciar el proceso de despliegue en el déclencheur de despliegue mientras se excluyen las propiedades de enlace de FolioProducer en el despliegue inicial</td>
   <td>En el despliegue</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>Configuración de despliegue de catálogo heredado (5.6.0)</td>
   <td>Obsoleto. Utilice el Generador de catálogos en lugar de MSM para los lanzamientos de catálogos.</td>
   <td>En el despliegue</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### Acciones de sincronización instaladas {#installed-synchronization-actions}

En la tabla siguiente se enumeran las acciones de sincronización que se instalan con AEM. Si las acciones instaladas no cumplen con sus requisitos, puede [Crear una nueva acción de sincronización](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>Nombre de la acción</th>
   <th>Descripción</th>
   <th>Propiedades<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>Cuando los nodos de origen no existen en la Live Copy, los copia en esta. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el servicio de acción de copia de contenido de CQ MSM</a> para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>Elimina nodos de la Live Copy que no existen en el origen. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el servicio de acción de eliminación de contenido de CQ MSM</a> para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>Actualiza el contenido de Live Copy con los cambios del origen. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el servicio de acción de actualización de contenido de CQ MSM</a> para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>Edita las propiedades de la Live Copy. La propiedad editMap determina qué propiedades se editan y su valor. El valor de la propiedad editMap debe utilizar el formato siguiente:</p> <p><code>[property_name_1]#[current_value]#</code>[nuevo_valor],<br /> <code>[property_name_2]#[current_value]#</code>[nuevo_valor],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[nuevo_valor]</p> <p>Los elementos <code>current_value</code> y <code>new_value</code> son expresiones regulares. <br /> </p> <p>Por ejemplo, considere el siguiente valor para editMap:</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>Este valor edita las propiedades de los nodos de Live Copy de la siguiente manera:</p>
    <ul>
     <li>Las propiedades de <code>sling:resourceType</code> que se han establecido en <code>contentpage</code> o en <code>homepage</code> se han establecido en <code>mobilecontentpage.</code></li>
     <li>Las propiedades de <code>cq:template</code> que se han establecido en <code>contentpage</code> se han establecido en <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap: (cadena) identifica la propiedad, el valor actual y el nuevo valor. Vea la descripción para obtener información.<br /> </p> </td>
  </tr>
  <tr>
   <td>notificar</td>
   <td>Envía un evento de página que indica que la página se ha desplegado. Para recibir notificaciones, primero debe suscribirse a los eventos de lanzamiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>En la Live Copy, ordena los elementos secundarios (nodos) según el orden del modelo <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>En la Live Copy, esta acción de sincronización actualiza referencias como los vínculos.<br /> Busca rutas de acceso en las páginas de Live Copy que apuntan a un recurso dentro del modelo. Cuando se encuentran, se actualiza la ruta de acceso para que apunte al recurso relacionado dentro de la Live Copy (en lugar del modelo). Las referencias que tienen los destinos fuera del modelo no cambian.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure el servicio de acción de actualización de referencias de CQ MSM</a> para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>Crea una versión de la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>Activa la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>Desactiva la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>flujo de trabajo</td>
   <td><p>Inicia el flujo de trabajo definido por la propiedad de destino (solo para páginas) y toma la Live Copy como carga útil.</p> <p>La ruta de destino es la ruta del nodo del modelo.</p> </td>
   <td>target: (cadena) ruta de acceso al modelo de flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td><p>Establece el permiso de varias ACL en la página de Live Copy como de solo lectura para un grupo de usuarios específico. Se configuran las siguientes ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Utilice esta acción solo para páginas.</p> </td>
   <td>target: (cadena) ID del grupo para el que se definen los permisos. <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>Establece el permiso de varias ACL en la página de Live Copy como de solo lectura para un grupo de usuarios específico. Se configuran las siguientes ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Utilice esta acción solo para páginas.</p> </td>
   <td>target: (cadena) ID del grupo para el que se definen los permisos. </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>Establece el permiso de la ACL ActionSet.ACTION_NAME_REMOVE en la página de Live Copy como de solo lectura para un grupo de usuarios específico. Utilice esta acción solo para páginas.</td>
   <td>target: (cadena) ID del grupo para el que se definen los permisos. </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>Si la página de origen o el modelo se ha publicado al menos una vez, crea una página de Live Copy con la versión publicada. Nota: Esta acción solo está disponible para crear una página de Live Copy basada en una página de origen publicada, no para actualizar una página de Live Copy existente. </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>PageMoveAction se aplica cuando una página se ha movido en el modelo.</p> <p>La acción copia la página de LiveCopy (relacionada) en lugar de moverla desde la ubicación, antes de realizar el traslado a la ubicación posterior.</p> <p>PageMoveAction no cambia la página de LiveCopy a la ubicación antes del movimiento. Por lo tanto, para RolloutConfigurations consecutivas, tiene el estado de una LiveRelationship sin modelo.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure el servicio de acción de movimiento de página de CQ MSM</a> para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. </p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td><p>prop_referenceUpdate: (booleano) establézcalo en true para actualizar referencias. El valor predeterminado es True.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>Crea o actualiza recursos de producto dentro de un catálogo. Esta acción está pensada para utilizarse en una de las siguientes situaciones:
    <ul>
     <li>Generación o despliegue de un catálogo (o sección de catálogo)</li>
     <li>Un usuario restaura la herencia de sincronización de un componente de producto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>Indica que existe una relación activa para el contenido creado para el lanzamiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>Ejecuta los vínculos de despliegue específicos de la generación del catálogo. Llama a los métodos executePageRolloutHooks y executeProductRolloutHooks de CatalogGenerator.<br /> Consulte com.adobe.cq.commerce.pim.api.CatalogGenerator en AEM Javadocs.</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>Actualiza las páginas de producto en una Live Copy de un catálogo de productos</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Creación de una configuración de despliegue {#creating-a-rollout-configuration}

Puede [crear una configuración de despliegue](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) cuando las configuraciones de despliegue instaladas no cumplan con los requisitos de la aplicación:

* [Crear la configuración de despliegue](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [Agregar acciones de sincronización a la configuración de despliegue](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

La nueva configuración de despliegue está disponible al establecer configuraciones de despliegue en una página de modelo o Live Copy.

### Exclusión de propiedades y tipos de nodos de la sincronización {#excluding-properties-and-node-types-from-synchronization}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes para que no afecten a los tipos de nodos y propiedades específicos. Por ejemplo, muchas propiedades y subnodos relacionados con el funcionamiento interno de AEM no deben incluirse en una Live Copy. Solo se debe copiar el contenido relevante para el usuario de la página.

Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

En la tabla siguiente se enumeran las acciones de sincronización para las que se pueden especificar los nodos que se excluirán. La tabla proporciona los nombres de los servicios que se van a configurar mediante la consola web y el PID para configurar mediante un nodo del repositorio.

| Acción de sincronización | Nombre del servicio en la consola web | PID de servicio |
|---|---|---|
| contentCopy | Acción de copia de contenido de CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | Acción de eliminación de contenido de CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | Acción de actualización de contenido de CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | Acción de movimiento de página de CQ MSM | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | Acción de actualización de referencias de CQ MSM | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

En la tabla siguiente se describen las propiedades que se pueden configurar:

<table>
 <tbody>
  <tr>
   <th>Propiedad de la consola web/propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>Nodetypes excluidos</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>Expresión regular que coincide con los tipos de nodo que se van a excluir de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Elementos de párrafo excluidos</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>Expresión regular que coincide con los elementos de párrafo que se van a excluir de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Propiedades de página excluidas</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>Expresión regular que coincide con las propiedades de página que se van a excluir de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Tipos de nodos de Mixin ignorados</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>Disponible solo para la acción de actualización de contenido de CQ MSM. Expresión regular que coincide con los nombres de los tipos de nodos de mezcla que se van a excluir de la acción de sincronización.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>En la IU clásica, el icono de candado que aparece en el cuadro de diálogo Propiedades de página para páginas de LiveCopy no refleja la configuración de la propiedad Propiedades de página excluidas. El icono de bloqueo aparece incluso para propiedades excluidas de la acción de sincronización.

>[!NOTE]
>
>En la IU táctil optimizada, vea también [Configuración de bloqueos MSM en las propiedades de página(IU táctil optimizada)](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### Acción de actualización de contenido de CQ MSM: exclusiones {#cq-msm-content-update-action-exclusions}

De forma predeterminada, se excluyen varias propiedades y tipos de nodos, que se definen en la configuración OSGi de **Acción de actualización de contenido de CQ MSM**, en **Propiedades de página excluidas**.

De forma predeterminada, las propiedades que coinciden con las siguientes expresiones regulares se excluyen (es decir, no se actualizan) en el despliegue:

![Acción de actualización de contenido de CQ MSM](assets/chlimage_1.png)

Puede cambiar las expresiones que definen la lista de exclusión según sea necesario.

Por ejemplo, si quiere que el **título** de la página se incluya en los cambios considerados para el lanzamiento, elimine `jcr:title` de las exclusiones. Por ejemplo, con la expresión regular:

`jcr:(?!(title)$).*`

### Configuración de la sincronización de actualización de referencias {#configuring-synchronization-for-updating-references}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes relacionadas con la actualización de referencias.

Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

En la siguiente tabla se enumeran las acciones de sincronización para las que se puede especificar la actualización de referencia. La tabla proporciona los nombres de los servicios que se van a configurar mediante la consola web y el PID para configurar mediante un nodo del repositorio.

<table>
 <tbody>
  <tr>
   <th>Propiedad de la consola web/propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>Actualizar referencia en LiveCopies anidadas</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>Solo está disponible para la acción de actualización de referencias de CQ MSM. Seleccione esta opción (Consola web) o establezca esta propiedad boolean como true (configuración del repositorio) para reemplazar referencias que estén orientadas a cualquier recurso que se encuentre dentro de la rama de la LiveCopy más importante.</td>
  </tr>
  <tr>
   <td><p>Actualizar páginas de referencia</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>Solo disponible para la acción de movimiento de página de CQ MSM. Seleccione esta opción (Consola web) o establezca esta propiedad booleana en <code>true</code> (configuración del repositorio) para actualizar cualquier referencia que utilice la página original para hacer referencia en su lugar a la página de LiveCopy.</td>
  </tr>
 </tbody>
</table>

## Especificación de las opciones de configuración de lanzamiento que se van a utilizar {#specifying-the-rollout-configurations-to-use}

MSM le permite especificar conjuntos de configuraciones de despliegue que suelen utilizarse y, cuando sea necesario, puede anularlos para Live Copies específicas. MSM proporciona varias ubicaciones para especificar las opciones de configuración de lanzamiento que se deben utilizar. La ubicación determina si la configuración se aplica a una Live Copy específica.

En la siguiente lista de ubicaciones en la que se pueden especificar las opciones de configuración de lanzamiento que se deben utilizar, se describe cómo MSM determina qué opciones de configuración de lanzamiento se deben utilizar para una Live Copy:

* **[Propiedades de la página Live Copy](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):** Cuando una página Live Copy está configurada para usar una o más configuraciones de despliegue, MSM las usa.
* **[Propiedades de la página de modelo](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):** Cuando una página de Live Copy se basa en un modelo y la página de Live Copy no está configurada con una configuración de despliegue, se utiliza la configuración de despliegue asociada con la página de origen del modelo.
* **Propiedades de la página principal de Live Copy:** Cuando ni la página de Live Copy ni la página de origen del modelo tienen una configuración de despliegue, se utiliza la configuración de despliegue que se aplica a la página principal de la página de Live Copy.
* **[Sistema predeterminado](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration):** Cuando no se puede determinar la configuración de despliegue de la página principal de Live Copy, se utiliza la configuración de despliegue predeterminada del sistema.

Por ejemplo, un modelo utiliza el sitio de referencia de We.Retail como contenido de origen. Se crea un sitio a partir del modelo. Cada elemento de la siguiente lista describe un escenario diferente con respecto al uso de configuraciones de despliegue:

* Ninguna de las páginas del modelo ni de Live Copy están configuradas para utilizar una configuración de despliegue. MSM utiliza la configuración de despliegue predeterminada del sistema para todas las páginas de Live Copy.
* La página raíz del sitio de referencia de We.Retail se configura con varias opciones de configuración de despliegue. MSM utiliza estas configuraciones de despliegue para todas las páginas de Live Copy.
* La página raíz del sitio de referencia de We.Retail se configura con varias opciones de configuración de despliegue, mientras que la página raíz del sitio de Live Copy se configura con un conjunto diferente. MSM utiliza las opciones de configuración de despliegue que se encuentran en la página raíz del sitio de Live Copy.

### Configuración de las opciones de configuración de lanzamiento para una página de Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Configure una página de Live Copy con las opciones de configuración de despliegue que se utilizarán cuando se lance la página de origen. Las páginas secundarias heredan la configuración de forma predeterminada. Al configurar la configuración de despliegue para su uso, se anula la configuración que la página de Live Copy hereda de su elemento principal.

También puede configurar las opciones de configuración de despliegue para una página de Live Copy al [crear Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. Utilice la consola **Sites** para seleccionar la página de Live Copy.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la pestaña **Live Copy**.

   La sección **Configuración** muestra las opciones de configuración de lanzamiento que hereda la página.

   ![Configuración](assets/chlimage_1-1.png)

1. Si es necesario, ajuste el indicador **Herencia de Live Copy**. Si se selecciona, la configuración de la Live Copy es eficaz en todas las páginas secundarias.

1. Borre la propiedad **Heredar configuración de despliegue del elemento principal** y, a continuación, seleccione una o varias opciones de configuración de despliegue de la lista.

   Las configuraciones de despliegue seleccionadas aparecen debajo de la lista desplegable.

   ![Configuraciones de despliegue seleccionadas](assets/chlimage_1-2.png)

1. Haga clic en **Guardar**.

### Configuración de despliegue para una página de modelo {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure una página modelo con las configuraciones de despliegue que se usarán cuando se lance la página modelo.

Las páginas secundarias de la página de modelo heredan la configuración. Al establecer la configuración de despliegue para su uso, se anula la configuración que la página hereda de su elemento principal.

1. Utilice la consola **Sitios** para seleccionar la página de modelo.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la pestaña **Modelo**.
1. Seleccione una o más **opciones de configuración de lanzamiento** con el selector desplegable.
1. Para almacenar las actualizaciones, seleccione **Guardar**.

### Opciones de la configuración de lanzamiento predeterminada del sistema {#setting-the-system-default-rollout-configuration}

Especifique una configuración de despliegue para utilizarla como predeterminada del sistema. Para especificar el valor predeterminado, configure el servicio OSGi:

* **Administrador de relaciones activas de CQ WCM por día**
el PID de servicio es `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure el servicio mediante la [consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo de repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* En la consola web, el nombre de la propiedad que se va a configurar es Configuración de despliegue predeterminada.
* Mediante un nodo del repositorio, el nombre de la propiedad que se va a configurar es `liverelationshipmgr.relationsconfig.default`.

Establezca este valor de la propiedad en la ruta de la configuración de lanzamiento que se utilizará como valor predeterminado del sistema. El valor predeterminado es `/libs/msm/wcm/rolloutconfigs/default`, que es la **Configuración de despliegue estándar**.
