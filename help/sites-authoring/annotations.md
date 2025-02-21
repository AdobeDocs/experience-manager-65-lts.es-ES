---
title: Anotaciones al editar una página de contenido
description: Muchos componentes directamente relacionados con el contenido permiten añadir una anotación.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 31%

---

# Anotaciones al editar una página{#annotations-when-editing-a-page}

La adición de contenido a las páginas del sitio web suele estar sujeta a discusiones antes de que se publique. Para ayudarle, muchos componentes directamente relacionados con el contenido (a diferencia, por ejemplo, del diseño) le permiten añadir una anotación.

Una anotación coloca un marcador de color/nota adhesiva en la página. La anotación le permite (a usted o a otros usuarios) dejar comentarios o preguntas para otros autores o revisores.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

>[!NOTE]
>
>Las anotaciones creadas en la IU clásica se muestran en la IU táctil. Sin embargo, los bocetos son específicos de la interfaz de usuario y solo se muestran en la interfaz en la que se crearon.

>[!CAUTION]
>
>Al eliminar un recurso (por ejemplo, un párrafo), se eliminan todas las anotaciones y bocetos relacionados con ese recurso, independientemente de su posición en la página en general.

>[!NOTE]
>
>En función de sus necesidades, también puede desarrollar un flujo de trabajo para enviar notificaciones cuando estas se añadan, actualicen o eliminen.

## Anotaciones {#annotations}

Se utiliza un modo [especial](/help/sites-authoring/author-environment-tools.md#page-modes) para crear y ver anotaciones.

>[!NOTE]
>
>No olvide que [comentarios](/help/sites-authoring/basic-handling.md#timeline) también están disponibles para proporcionar comentarios sobre una página.

>[!NOTE]
>
>Puede realizar anotaciones en una variedad de recursos:
>
>* [Anotando recursos](/help/assets/manage-assets.md#annotating)
>* [Anotando recursos de vídeo](/help/assets/managing-video-assets.md#annotate-video-assets)
>

### Anotación de un componente {#annotating-a-component}

El modo Anotar permite crear, editar, mover o eliminar anotaciones en el contenido:

1. Puede acceder al modo de anotación mediante el icono de la barra de herramientas (parte superior derecha) al editar una página:

   ![Anotar](do-not-localize/screen_shot_2018-03-22at110414.png)

   Ahora puede ver todas las anotaciones existentes.

   >[!NOTE]
   >
   >Para salir del modo de anotación, haga clic en el icono Anotar (símbolo x) en la parte derecha de la barra de herramientas superior.

1. Haga clic en el icono Añadir anotación (símbolo &quot;+&quot; a la izquierda de la barra de herramientas) para empezar a añadir anotaciones.

   >[!NOTE]
   >
   >Para detener la adición de anotaciones (y volver a la visualización), haga clic en el icono Cancelar (símbolo x en un círculo blanco) a la izquierda de la barra de herramientas superior.

1. Haga clic en el componente requerido (los componentes que se pueden anotar se resaltarán con un borde azul) para añadir la anotación y abrir el cuadro de diálogo:

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   Aquí podrá utilizar el campo o icono apropiados para lo siguiente:

   * Escribir el texto de anotación.
   * Crear un boceto (líneas y formas) para resaltar un área del componente.

     El cursor cambiará a una cruz cuando esté creando un boceto. Puede dibujar varias líneas distintas. Las líneas del boceto reflejan el color de la anotación y pueden ser una flecha, un círculo u ovaladas.

     ![Bosquejo](do-not-localize/screen_shot_2018-03-22at110640.png)

   * Elegir o cambiar el color:

     ![Elegir o cambiar color](do-not-localize/chlimage_1-19.png)

   * Eliminar la anotación.

     ![Eliminar anotación](do-not-localize/screen_shot_2018-03-22at110647.png)

1. Para cerrar el cuadro de diálogo de anotaciones, toque o haga clic fuera del mismo. Se mostrará una vista truncada (la primera palabra) de la anotación, junto con los bocetos, si los hay:

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. Cuando haya terminado de editar una anotación concreta, puede hacer lo siguiente:

   * Haga clic en el marcador de texto para abrir la anotación. Una vez abierto, puede ver el texto completo, realizar cambios o eliminar la anotación.

      * Los bocetos no se pueden eliminar independientemente de la anotación.

   * Cambiar la posición del marcador de texto.
   * Haga clic en una línea de un boceto para seleccionarlo y arrastrarlo a la posición deseada.
   * Mover o copiar un componente

      * Todas las anotaciones relacionadas y sus bocetos también se moverán o copiarán y su posición en relación con el párrafo seguirá siendo la misma.

1. Para salir del modo de anotación y volver al anterior, haga clic en el icono Anotar (símbolo x) en la parte derecha de la barra de herramientas superior.

>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

### Indicador de anotaciones {#annotation-indicator}

Las anotaciones no aparecen en el modo de edición, pero el distintivo de la esquina superior derecha de la barra de herramientas mostrará el número de anotaciones de la página actual. Este distintivo sustituye al icono Anotaciones predeterminado, y además funciona como vínculo rápido que le permite acceder al modo de anotación y salir de él:

![Indicador de anotaciones](assets/chlimage_1-242.png)
