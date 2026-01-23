---
title: Administración de etiquetas
description: Obtenga información sobre cómo administrar y administrar etiquetas en Adobe Experience Manager.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 6659ca39-f297-40b9-88e2-d942aa653e9b
source-git-commit: abda4a719676f45388e91bbdec1421152433fce8
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 5%

---

# Administración de etiquetas {#administering-tags}

Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web. Se pueden considerar como palabras clave o etiquetas (metadatos) que permiten encontrar el contenido más rápidamente como resultado de una búsqueda.

En Adobe Experience Manager (AEM), una etiqueta puede ser una propiedad de

* un nodo de contenido para una página (consulte [Uso de etiquetas](/help/sites-authoring/tags.md))

* un nodo de metadatos para un recurso (consulte [Administración de metadatos para Assets digital](/help/assets/metadata.md))

## Características de etiquetas {#tag-features}

Algunas de las funciones de las etiquetas en AEM incluyen:

* Las etiquetas se pueden agrupar en varias áreas de nombres. Estas jerarquías permiten crear taxonomías. Estas taxonomías son globales en todo AEM.
* La restricción principal para las etiquetas recién creadas es que deben ser únicas dentro de un área de nombres específica.
* El título de una etiqueta no debe incluir caracteres de separación de rutas de etiquetas (ni se mostrarán si están presentes)

   * dos puntos `:`: delimita la etiqueta de área de nombres
   * barra diagonal `/`: delimita las etiquetas secundarias

* Los autores y visitantes del sitio pueden aplicar las etiquetas. Independientemente de su creador, todas las formas de etiquetas están disponibles para su selección, tanto al asignarlas a una página como al buscar.
* Los miembros del grupo &quot;administradores de etiquetas&quot; y los miembros que tienen derechos de modificación sobre `/content/cq:tags` pueden crear etiquetas y modificar su taxonomía.

   * Una etiqueta que contiene etiquetas secundarias se denomina etiqueta contenedora
   * Una etiqueta que no es una etiqueta contenedora se denomina etiqueta de hoja
   * Un área de nombres de etiqueta es una etiqueta de hoja o una etiqueta contenedora

* El [componente de búsqueda](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) usa las etiquetas para facilitar la búsqueda de contenido.
* El [componente Teaser](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html) utiliza las etiquetas, que supervisa la nube de etiquetas de un usuario para proporcionar contenido de destino.
* Si el etiquetado es un aspecto importante del contenido

   * asegúrese de empaquetar las etiquetas con las páginas que las utilizan
   * asegúrese de que [permisos de etiquetas](#setting-tag-permissions) habiliten el acceso de lectura

## Consola de etiquetado {#tagging-console}

La consola Etiquetado se utiliza para crear y administrar etiquetas y sus taxonomías. Un objetivo es evitar tener muchas etiquetas similares relacionadas básicamente con lo mismo : por ejemplo, páginas y páginas o calzado y zapatos.

Las etiquetas se administran agrupándolas en áreas de nombres, revisando el uso de las etiquetas existentes antes de crear nuevas etiquetas y reorganizándolas sin desconectar la etiqueta del contenido al que se hace referencia actualmente.

Para acceder a la consola de etiquetado:

* sobre el autor
* iniciar sesión con privilegios administrativos
* desde la navegación global

   * seleccionar **`Tools`**
   * seleccionar **`General`**
   * seleccionar **`Tagging`**

![administrar_etiquetas_mediante_thetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Creación de un espacio de nombres {#creating-a-namespace}

Para crear un área de nombres, seleccione el icono **`Create Namespace`**.

El área de nombres es en sí misma una etiqueta y no debe contener ninguna subetiqueta. Sin embargo, para continuar creando una taxonomía, [cree subetiquetas](#creating-tags), que a su vez pueden ser etiquetas de hoja o de contenedor.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creando_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Título**
  *(obligatorio)* Un título para mostrar para el área de nombres.

* **Nombre**
  *(opcional)* Un nombre para el área de nombres. Si no se especifica, se crea un nombre de nodo válido a partir del Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descripción**
  *(opcional)* Una descripción del área de nombres.

Una vez introducida la información requerida

* seleccionar **Crear**

### Operaciones en etiquetas {#operations-on-tags}

Al seleccionar un área de nombres u otra etiqueta, están disponibles las siguientes operaciones:

* [Ver propiedades](#viewing-tag-properties)
* [Referencias](#showing-tag-references)
* [Crear etiqueta](#creating-tags)
* [Editar](#editing-tags)
* [Mover](#moving-tags)
* [Combinar](#merging-tags)
* [Publicación](#publishing-tags)
* [Cancelar la publicación](#unpublishing-tags)
* [Eliminar](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Cuando la ventana del explorador no es lo suficientemente ancha como para mostrar todos los iconos, los iconos situados más a la derecha se agrupan bajo un icono **`... More`**, que mostrará una lista desplegable de los iconos de operación ocultos cuando se seleccionen.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selección de una etiqueta de área de nombres {#selecting-a-namespace-tag}

Cuando se selecciona por primera vez, si el área de nombres no contiene etiquetas, las propiedades se muestran a la derecha; de lo contrario, se muestran las etiquetas secundarias. Cada etiqueta seleccionada mostrará las etiquetas que contiene o sus propiedades si no tiene etiquetas secundarias.

Para seleccionar la etiqueta para las operaciones y para la selección múltiple, seleccione solo el icono situado junto al título. Al seleccionar el título, solo se muestran las propiedades o se abre la etiqueta para mostrar su contenido.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Visualización de propiedades de etiqueta {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Cuando se selecciona un área de nombres u otra etiqueta, al seleccionar el icono **`View Properties`** se muestra información sobre `name`, la hora de la última edición y el número de referencias. Si se publica, se muestra la hora en que se publicó por última vez y el ID del editor. Esta información aparece en una columna a la izquierda de las columnas de etiquetas.

![chlimage_1-189](assets/chlimage_1-189.png)

### Mostrando referencias de etiqueta {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Cuando se selecciona un área de nombres u otra etiqueta, al seleccionar el icono **Referencias** se identificará el contenido al que se ha aplicado la etiqueta.

La visualización inicial es un recuento de etiquetas aplicadas.

![chlimage_1-191](assets/chlimage_1-191.png)

Al seleccionar la flecha a la derecha del recuento, se muestran los nombres de referencia.

La trayectoria hasta la referencia se muestra como información de objeto al pasar el cursor sobre una referencia.

![chlimage_1-192](assets/chlimage_1-192.png)

### Creación de etiquetas {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Cuando se selecciona un área de nombres u otra etiqueta (seleccionando el icono junto al título), se puede crear una etiqueta secundaria para la etiqueta actual seleccionando el icono **`Create Tag`**.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Título**
*(obligatorio) *Un título para mostrar para la etiqueta.

* **Nombre**
*(opcional) *Un nombre para la etiqueta. Si no se especifica, se crea un nombre de nodo válido a partir del Título. Consulte [TagID](/help/sites-developing/framework.md#tagid).

* **Descripción**
*(opcional) * Una descripción de la etiqueta.

Una vez introducida la información requerida

* seleccionar **Crear**

### Edición de etiquetas {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Cuando se selecciona un área de nombres u otra etiqueta, es posible modificar el Título, la Descripción y proporcionar localizaciones del Título seleccionando el icono **`Edit`**.

Una vez realizadas las ediciones, seleccione **Guardar**.

Para obtener más información sobre cómo agregar traducciones de idiomas, consulte la sección sobre [Administración de etiquetas en diferentes idiomas](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Mover etiquetas {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Cuando se selecciona un área de nombres u otra etiqueta, si se selecciona el icono **`Move`**, los administradores y desarrolladores de etiquetas podrán limpiar la taxonomía moviendo la etiqueta a una nueva ubicación o cambiando el nombre. Si la etiqueta seleccionada es una etiqueta contenedora, al mover la etiqueta también se moverán todas las etiquetas secundarias.

>[!NOTE]
>
>Se recomienda que los autores solo puedan [editar](#editing-tags) la etiqueta `title`, no mover ni cambiar el nombre de las etiquetas.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Ruta**
  *(solo lectura)* La ruta actual a la etiqueta seleccionada.

* **Mover a**
Desplácese hasta la nueva ruta en la que desea mover la etiqueta.

* **Cambiar nombre a**
Muestra inicialmente el `name` actual de la etiqueta. Se puede introducir un nuevo `name`.

* seleccionar **Guardar**

### Combinación de etiquetas {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

La combinación de etiquetas se puede utilizar cuando una taxonomía tiene duplicados. Cuando la etiqueta A se combina con la etiqueta B, todas las páginas etiquetadas con la etiqueta A se etiquetarán con la etiqueta B y la etiqueta A ya no estará disponible para los autores.

Cuando se selecciona un área de nombres u otra etiqueta, al seleccionar el icono **Merge** se abre un panel en el que se puede seleccionar la ruta de acceso a la que se va a realizar la combinación.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Ruta**
  *(solo lectura)* Ruta de acceso de la etiqueta seleccionada para combinarse con otra etiqueta.

* **Combinar en**
Busque y seleccione la ruta de la etiqueta en la que desea combinar.

>[!NOTE]
>
>Después de la combinación, la **ruta** seleccionada originalmente dejará de existir (virtualmente).
>
>Cuando se mueve o combina una etiqueta a la que se hace referencia, la etiqueta no se elimina físicamente de modo que sea posible mantener referencias.

### Publicación de etiquetas {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Cuando se selecciona un área de nombres u otra etiqueta, se selecciona el icono **Publish** para activar la etiqueta en el entorno de publicación. Al igual que el contenido de la página, solo se publica la etiqueta seleccionada, independientemente de si es una etiqueta contenedora o no.

Para publicar una taxonomía (un área de nombres y subetiquetas), la práctica recomendada es crear un [paquete](/help/sites-administering/package-manager.md) del área de nombres (consulte [Nodo raíz de taxonomía](/help/sites-developing/framework.md#taxonomy-root-node)). Asegúrese de [aplicar permisos](#setting-tag-permissions) al área de nombres antes de crear el paquete.

### Cancelar publicación de etiquetas {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Cuando se selecciona un área de nombres u otra etiqueta, al seleccionar el icono **Cancelar la publicación**, se desactiva la etiqueta en el entorno de creación y se elimina del entorno de publicación. De forma similar a la operación `Delete`, si la etiqueta seleccionada es una etiqueta contenedora, todas sus etiquetas secundarias se desactivarán en el entorno de creación y se eliminarán del entorno de publicación.

### Eliminación de etiquetas {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Cuando se selecciona un área de nombres u otra etiqueta, al seleccionar el icono **Eliminar** se eliminará permanentemente la etiqueta del entorno de creación. Si la etiqueta se publicó, también se elimina del entorno de publicación. Si la etiqueta seleccionada es una etiqueta contenedora, también se eliminarán todas sus etiquetas secundarias.

## Configuración de permisos de etiquetas {#setting-tag-permissions}

Los permisos de etiqueta son [&#39;seguros (de forma predeterminada)&#39;](/help/sites-administering/production-ready.md); una práctica recomendada para el entorno de publicación que requiere permiso de lectura para permitir explícitamente las etiquetas. Básicamente, esto se realiza creando un paquete del área de nombres de etiqueta después de configurar los permisos en el autor e instalando el paquete en todas las instancias de publicación.

* en la instancia de autor

   * iniciar sesión con privilegios administrativos
   * acceder a la [consola de seguridad](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * por ejemplo, vaya a http://localhost:4502/useradmin

   * en el panel izquierdo, seleccione el grupo (o usuario) para el que se debe otorgar [permiso de lectura](/help/sites-administering/security.md#permissions)
   * en el panel derecho, busque el **Path &#x200B;** to the Tag Namespace

      * por ejemplo, `/content/cq:tags/mycommunity`

   * seleccione `checkbox` en la columna **Leer**
   * seleccionar **Guardar**

![chlimage_1-204](assets/chlimage_1-204.png)

* asegúrese de que todas las instancias de publicación tengan los mismos permisos

   * un enfoque consiste en [crear un paquete](/help/sites-administering/package-manager.md#package-manager) del área de nombres en Author

      * en la ficha `Advanced`, para `AC Handling` seleccione `Overwrite`

   * replicar el paquete

      * elija `Replicate` del administrador de paquetes

## Administración de etiquetas en diferentes idiomas {#managing-tags-in-different-languages}

La propiedad `title` de una etiqueta puede traducirse a varios idiomas. Una vez traducida, la etiqueta apropiada `title` puede mostrarse según el idioma del usuario o el idioma de la página.

### Definición de títulos de etiquetas en varios idiomas {#defining-tag-titles-in-multiple-languages}

A continuación se describe cómo traducir el `title`de la etiqueta **Animals** del inglés al alemán y al francés.

Comience por seleccionar la etiqueta en el área de nombres **Stock Photography** y seleccione el icono **`Edit`** (consulte la sección [Edición de etiquetas](#editing-tags)).

El panel Editar etiqueta presenta la capacidad de elegir los idiomas en los que se localizará el título de la etiqueta.

A medida que se selecciona cada idioma, aparece un cuadro de entrada de texto en el que se puede introducir el título traducido.

Una vez ingresadas todas las traducciones, seleccione **Guardar** para salir del modo de edición.

![chlimage_1-205](assets/chlimage_1-205.png)

En general, el idioma elegido para la etiqueta se toma del idioma de la página, cuando está disponible. Cuando el widget [`tag`](/help/sites-developing/building.md#tagging-on-the-client-side) se usa en otros casos (por ejemplo, en formularios o cuadros de diálogo), el idioma de la etiqueta depende del contexto.

En lugar de utilizar la configuración de idioma de la página, la consola de etiquetado utiliza la configuración de idioma del usuario. En la consola de etiquetado, para la etiqueta &quot;Animales&quot;, se mostraría &quot;Animales&quot; para un usuario que establece el idioma en francés en sus propiedades de usuario.

Para agregar un nuevo idioma al cuadro de diálogo, vea [Agregar un nuevo idioma al cuadro de diálogo Editar etiqueta](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>La nube de etiquetas y las palabras clave meta en el componente de página estándar usan la etiqueta localizada `titles` en función del idioma de la página, si está disponible.

## Recursos {#resources}

* [Etiquetado para desarrolladores](/help/sites-developing/tags.md)

  Información sobre el marco de etiquetado y ampliación e inclusión de etiquetas en aplicaciones personalizadas.

* [Consola de etiquetado de IU clásica](/help/sites-administering/classic-console.md)
