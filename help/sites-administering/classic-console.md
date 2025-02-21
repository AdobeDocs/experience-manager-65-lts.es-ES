---
title: Consola de etiquetado de IU clásica
description: Obtenga información acerca de la consola de etiquetado de IU de Adobe Experience Manager Classic.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---


# Consola de etiquetado de IU clásica{#classic-ui-tagging-console}

Esta sección es para la Consola de etiquetado de IU clásica.

>[!NOTE]
>
>Consulte [Administración de etiquetas](/help/sites-administering/tags.md#tagging-console) para obtener más información sobre la consola de etiquetado de IU táctil.

Para acceder a la consola de etiquetado de IU clásica:

* sobre el autor
* iniciar sesión con privilegios administrativos
* vaya a la consola
por ejemplo, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![Ventana de consola clásica](assets/managing_tags_usingthetagasministrationconsole.png)

## Creación de etiquetas y espacios de nombre {#creating-tags-and-namespaces}

1. Según el nivel en el que comience, puede crear una etiqueta o un área de nombres con **New**:

   Si selecciona **Etiquetas**, puede crear un área de nombres:

   ![Creando un cuadro de diálogo de espacio de nombres](assets/creating_tags_andnamespaces.png)

   Si selecciona un área de nombres (por ejemplo, **Demo**), puede crear una etiqueta dentro de esa área de nombres:

   ![Creando cuadro de diálogo de etiqueta](assets/creating_tags_andnamespacesinnewnamespace.png)

1. En ambos casos, introduzca

   * **Título**
(*Requerido*) El título para mostrar de la etiqueta. Aunque se puede introducir cualquier carácter,
se recomienda no utilizar estos caracteres especiales:

      * `colon (:)` - delimitador de área de nombres
      * `forward slash (/)` - delimitador de subetiqueta

     Estos caracteres no se mostrarán si se introducen.

   * **Nombre**
(*Requerido*) El nombre de nodo para la etiqueta.

   * **Descripción**
(*Opcional*) Una descripción para la etiqueta.

   * seleccionar **Crear**

## Edición de etiquetas {#editing-tags}

1. En el panel derecho, seleccione la etiqueta que desee editar.
1. Haga clic en **Editar**.
1. Puede modificar **Title** y **Description**.
1. Haga clic en **Guardar** para cerrar el cuadro de diálogo.

## Eliminación de etiquetas {#deleting-tags}

1. En el panel derecho, seleccione la etiqueta que desee eliminar.
1. Haga clic en **Eliminar**.
1. Haga clic en **Sí** para cerrar el cuadro de diálogo.

   La etiqueta ya no debería aparecer en la lista.

## Activación y desactivación de etiquetas {#activating-and-deactivating-tags}

1. En el panel derecho, seleccione el área de nombres o la etiqueta que desea activar (publicar) o desactivar (cancelar la publicación).
1. Haga clic en **Activar** o **Desactivar** según sea necesario.

## Lista: mostrar dónde se hace referencia a las etiquetas {#list-showing-where-tags-are-referenced}

**List** abre una nueva ventana que muestra las rutas de todas las páginas que usan la etiqueta resaltada:

![Buscando dónde se hace referencia a las etiquetas](assets/list_showing_wheretagsarereferenced.png)

## Mover etiquetas {#moving-tags}

Para ayudar a los administradores y desarrolladores de etiquetas a limpiar la taxonomía o cambiar el nombre de un ID de etiqueta, es posible mover una etiqueta a una nueva ubicación:

1. Abra la consola **Etiquetado**.
1. Seleccione la etiqueta y haga clic en **Mover...** en la barra de herramientas superior (o en el menú contextual).
1. En el cuadro de diálogo **Mover etiqueta**, defina:

   * **to**, el nodo de destino.
   * **Cambiar nombre a**, el nuevo nombre de nodo.

1. Haga clic en **Mover**.

El cuadro de diálogo **Mover etiqueta** tiene el siguiente aspecto:

![Moviendo una etiqueta](assets/move_tag.png)

>[!NOTE]
>
>Los autores no deben mover etiquetas ni cambiar el nombre de un ID de etiqueta. Si es necesario, los autores solo deben [cambiar los títulos de las etiquetas](#editing-tags).

## Combinación de etiquetas {#merging-tags}

La combinación de etiquetas se puede utilizar cuando una taxonomía tiene duplicados. Cuando la etiqueta A se combina con la etiqueta B, todas las páginas etiquetadas con la etiqueta A se etiquetarán con la etiqueta B y la etiqueta A ya no está disponible para los autores.

Para combinar una etiqueta en otra:

1. Abra la consola **Etiquetado**.
1. Seleccione la etiqueta y haga clic en **Combinar...** en la barra de herramientas superior (o en el menú contextual).
1. En el cuadro de diálogo **Combinar etiqueta**, defina:

   * **en**, el nodo de destino.

1. Haga clic en **Combinar**.

El cuadro de diálogo **Combinar etiqueta** tiene el siguiente aspecto:

![Combinando una etiqueta](assets/mergetag.png)

## Recuento del uso de etiquetas {#counting-usage-of-tags}

Para ver cuántas veces se está utilizando una etiqueta:

1. Abra la consola **Etiquetado**.
1. Haga clic en **Contar uso** en la barra de herramientas superior: la columna Contar muestra el resultado.

## Administración de etiquetas en diferentes idiomas {#managing-tags-in-different-languages}

La propiedad `title` opcional de una etiqueta se puede traducir a varios idiomas. La etiqueta `titles` se puede mostrar según el idioma del usuario o el idioma de la página.

### Definición de títulos de etiquetas en varios idiomas {#defining-tag-titles-in-multiple-languages}

El siguiente procedimiento muestra cómo traducir el `title`de la etiqueta **Animals** al inglés, alemán y francés:

1. Vaya a la consola **Etiquetado**.
1. Edita la etiqueta **Animales** debajo de **Etiquetas** > **Fotografía de archivo**.
1. Añada las traducciones en los siguientes idiomas:

   * **Inglés**: Animales
   * **Alemán**: Tiere
   * **Francés**: Animaux

1. Guarde los cambios.

El cuadro de diálogo tiene el siguiente aspecto:

![Editando una etiqueta](assets/edit_tag.png)

La consola de etiquetado utiliza la configuración de idioma del usuario, por lo que para la etiqueta Animal, se muestra &quot;Animaux&quot; para un usuario que establece el idioma en francés en las propiedades del usuario.

Para agregar un nuevo idioma al cuadro de diálogo, consulte la sección [Agregar un nuevo idioma al cuadro de diálogo Editar etiqueta](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) en la sección **Etiquetado para desarrolladores**.

### Mostrar títulos de etiquetas en las propiedades de página en un idioma especificado {#displaying-tag-titles-in-page-properties-in-a-specified-language}

De forma predeterminada, la etiqueta `titles` de las propiedades de la página se muestra en el idioma de la página. El cuadro de diálogo de etiquetas de las propiedades de página tiene un campo de idioma que permite mostrar la etiqueta `titles` en un idioma diferente. El siguiente procedimiento describe cómo mostrar la etiqueta `titles` en francés:

1. Consulte la sección anterior para agregar la traducción al francés a **Animales** debajo de **Etiquetas** > **Fotografía de archivo**.
1. Abra las propiedades de página de la página **Productos** en la rama en inglés del sitio **Geometrixx**.
1. Abra el cuadro de diálogo **Etiquetas/Palabras clave** (seleccionando el menú desplegable a la derecha del área de visualización Etiquetas/Palabras clave) y seleccione el idioma **Francés** en el menú desplegable de la esquina inferior derecha.
1. Desplácese con las flechas izquierda-derecha hasta que pueda seleccionar la ficha **Fotografías de archivo**

   Seleccione la etiqueta **Animals** (**Animaux**) y seleccione fuera del cuadro de diálogo para cerrarla y agregar la etiqueta a las propiedades de la página.

   ![Editando otra etiqueta](assets/french_tag.png)

De forma predeterminada, el cuadro de diálogo Propiedades de página muestra la etiqueta `titles` según el idioma de la página.

En general, el idioma de la etiqueta se toma del idioma de la página si este está disponible. Cuando el widget [`tag`](/help/sites-developing/building.md#tagging-on-the-client-side) se usa en otros casos (por ejemplo, en formularios o cuadros de diálogo), el idioma de la etiqueta depende del contexto.

>[!NOTE]
>
>La nube de etiquetas y las palabras clave meta en el componente de página estándar usan la etiqueta localizada `titles` en función del idioma de la página, si está disponible.
