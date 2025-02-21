---
title: Anotaciones al editar una página
description: La adición de contenido a las páginas del sitio web suele estar sujeta a discusiones antes de publicarse. Para ayudarle, muchos componentes directamente relacionados con el contenido le permiten añadir una anotación.
page-status-flag: de-activated
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 7%

---

# Anotaciones al editar una página{#annotations-when-editing-a-page}

La adición de contenido a las páginas del sitio web suele estar sujeta a discusiones antes de publicarse. Para ayudarle, muchos componentes directamente relacionados con el contenido (a diferencia, por ejemplo, del diseño) le permiten añadir una anotación.

Una anotación coloca un marcador de color/nota adhesiva en la página. La anotación le permite (a usted o a otros usuarios) dejar comentarios o preguntas para otros autores o revisores.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

>[!NOTE]
>
>Las anotaciones creadas en la IU clásica se muestran en la IU táctil optimizada. Sin embargo, los bocetos son específicos de la interfaz de usuario y solo se muestran en la interfaz en la que se crearon.

>[!CAUTION]
>
>Al eliminar un recurso (por ejemplo, un párrafo), se eliminan todas las anotaciones y bocetos relacionados con ese recurso, independientemente de su posición en la página en general.

>[!NOTE]
>
>En función de sus necesidades, también puede desarrollar un flujo de trabajo para enviar notificaciones cuando estas se añadan, actualicen o eliminen.

## Anotaciones {#annotations}

Según el diseño del párrafo, la anotación está disponible como opción en el menú contextual (normalmente, el botón derecho del ratón al pasar el ratón por encima del párrafo requerido) o como botón en la barra de edición del párrafo.

En cualquier caso, seleccione **Anotar**. Se aplica una anotación de nota adhesiva de color al párrafo; se encuentra inmediatamente en el modo Editar, lo que le permite agregar texto directamente:

![chlimage_1-137](assets/chlimage_1-137.png)

Puede mover la anotación a una nueva posición en la página. Haga clic en el área del borde superior, mantenga pulsada la anotación y arrástrela simultáneamente a la nueva posición. Puede estar en cualquier parte de la página, aunque suele ser importante mantenerla conectada al párrafo de alguna manera.

Las anotaciones (incluidos los bocetos relacionados) también se incluyen en cualquier acción de copiar, cortar o eliminar llevada a cabo en el párrafo al que están asociadas. Para las acciones de copiar o cortar, la posición de la anotación (y los bocetos relacionados) conserva su posición en relación con el párrafo de origen.

El tamaño de la anotación también se puede aumentar o reducir arrastrando la esquina inferior derecha.

Para fines de seguimiento, la línea de pie de página indica el usuario que creó la anotación y la fecha. Los autores posteriores pueden editar la misma anotación (se actualiza el pie de página) o crear otra anotación para el mismo párrafo.

Se solicita confirmación cuando selecciona eliminar la anotación (al eliminar una anotación, también se eliminan los bocetos adjuntos a esa anotación).

Los tres iconos de la parte superior izquierda permiten minimizar la anotación (junto con cualquier boceto relacionado), cambiar el color y añadir bocetos.

>[!NOTE]
>
>Las anotaciones solo están visibles en el modo de edición del entorno de creación.
>
>No son visibles en un entorno de publicación, ni en los modos de Previsualización o Diseño disponibles en un entorno de creación.

>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

## Bocetos de anotación {#annotation-sketches}

>[!NOTE]
>
>Los bocetos no están disponibles en Internet Explorer, por lo que:
>
>* el icono no se muestra.
>* los bocetos existentes, creados en otro navegador, no se mostrarán.
>

Los bocetos son una función de las anotaciones que permiten crear gráficos de líneas simples en cualquier parte de la ventana del explorador (parte visible):

![chlimage_1-138](assets/chlimage_1-138.png)

* El cursor cambia a una cruz cuando se encuentra en modo de esbozo. Puede dibujar varias líneas distintas.
* La línea del boceto refleja el color de la anotación y puede ser:

   * a pulso

     el modo predeterminado; termine soltando el botón del mouse.

   * recto:

     mantenga presionado `ALT` y haga clic en los puntos inicial y final; finalice con un doble clic.

* Una vez que haya salido del módulo de esbozo, puede pulsar en una línea de esbozo para seleccionarla.
* Para mover un boceto, selecciónelo y arrástrelo a la posición que desee.
* Un boceto superpone el contenido. Esto significa que, dentro de las cuatro esquinas del boceto, no se puede hacer clic en el párrafo subyacente. Por ejemplo, si debe editar o acceder a un vínculo. Si esto se convierte en un problema (por ejemplo, si tiene un boceto que cubre una gran área de la página), minimice la anotación adecuada, ya que esto también minimizará todos los bocetos relacionados, lo que le dará acceso al área subyacente.
* Para eliminar un boceto individual, selecciona el boceto requerido y luego oprime la tecla **Delete** (**fn**-**backspace** en un Mac).

* Si mueve o copia un párrafo, las anotaciones relacionadas y sus bocetos también se moverán o copiarán; su posición en relación con el párrafo seguirá siendo la misma.
* Si elimina una anotación, también se eliminarán todos los bocetos adjuntos a esa anotación.
