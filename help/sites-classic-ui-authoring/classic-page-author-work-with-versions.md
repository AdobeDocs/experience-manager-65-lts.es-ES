---
title: Uso de versiones de página
description: Obtenga información sobre el control de versiones y cómo crear una instantánea de una página en un momento específico.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 19%

---

# Uso de versiones de página  {#working-with-page-versions}

Al generar una versión, se crea una “instantánea” de una página en un momento determinado. Con las versiones, se pueden realizar las siguientes operaciones:

* Crear una versión de la página.
* Restaurar una página a una versión anterior para poder deshacer los cambios realizados en una página.
* Comparar la versión actual de una página con una versión anterior con diferencias en el texto y las imágenes resaltadas.

## Creación de una versión {#creating-a-new-version}

Para crear una versión de una página:

1. En el explorador, abra la página para la que desea crear una versión.
1. En Sidekick, seleccione la pestaña **Control de versiones** y, a continuación, la subpestaña **Crear versión**.

   ![screen_shot_2012-02-14at40259pm](assets/screen_shot_2012-02-14at40259pm.png)

1. Escriba un **comentario** (opcional).
1. Para establecer una etiqueta en la versión (opcional), haga clic en el botón **Más >>** y establezca la **Etiqueta** para asignar un nombre a la versión. Si no se define la etiqueta, la versión es un número incrementado automáticamente.
1. Haga clic en **Crear versión**. Se muestra un mensaje en gris en la página; por ejemplo:
Versión 1.2 creada para: Camisetas.

>[!NOTE]
>
>Se crea automáticamente una versión cuando se activa la página.

## Restablecer una versión de la página desde Sidekick {#restoring-a-page-version-from-sidekick}

Para restaurar la página a una versión anterior:

1. Abra la página para la que desea restaurar una versión anterior.
1. En la barra de tareas, seleccione la ficha **Control de versiones** y, a continuación, la subpestaña **Restaurar versión**.

   ![screen_shot_2012-02-14at42949pm](assets/screen_shot_2012-02-14at42949pm.png)

1. Seleccione la versión que desea restaurar y seleccione **Restaurar**.

## Restablecer una versión de página desde la consola {#restoring-a-page-version-from-the-console}

Este método se puede utilizar para restaurar una versión de la página. También se puede utilizar para restaurar páginas que se han eliminado anteriormente:

1. En la consola **Sitios web**, vaya a la página que desee restaurar y selecciónela.
1. En el menú superior, selecciona **Herramientas** y luego **Restaurar**:

   ![screen_shot_2012-02-08at41326pm](assets/screen_shot_2012-02-08at41326pm.png)

1. Seleccionando **Restaurar versión...** se enumeran las versiones de los documentos de la carpeta actual. Aunque se haya eliminado una página, se muestra la última versión:

   ![screen_shot_2012-02-08at45743pm](assets/screen_shot_2012-02-08at45743pm.png)

1. Seleccione la versión que desea restaurar y haga clic en **Restaurar**. AEM restaura las versiones (o árboles) que seleccione.

### Restauración de un árbol desde la consola {#restoring-a-tree-from-the-console}

Este método se puede utilizar para restaurar una versión de la página. También se puede utilizar para restaurar páginas que se han eliminado anteriormente:

1. En la consola **Sitios web**, vaya a la carpeta que desee restaurar y selecciónela.
1. En el menú superior, selecciona **Herramientas** y luego **Restaurar**.
1. Al seleccionar **Restaurar árbol...**, se abre el cuadro de diálogo para que pueda seleccionar el árbol que desea restaurar:

   ![screen_shot_2012-02-08at45743pm-1](assets/screen_shot_2012-02-08at45743pm-1.png)

1. Haga clic en **Restaurar**. AEM restaura el árbol que ha seleccionado.

## Comparación con una versión anterior {#comparing-with-a-previous-version}

Para comparar la versión actual de la página con una versión anterior:

1. En el explorador, abra la página para la que desea comparar con una versión anterior.
1. En Sidekick, seleccione la pestaña **Versiones** y, a continuación, la subpestaña **Restaurar versión** n.

   ![screen_shot_2012-02-14at42949pm-1](assets/screen_shot_2012-02-14at42949pm-1.png)

1. Seleccione la versión que desee comparar y haga clic en el botón **Diff**.
1. Las diferencias entre la versión actual y la seleccionada se muestran de la siguiente manera:

   * El texto que se ha eliminado está en rojo y tachado.
   * El texto que se ha agregado es verde y está resaltado.
   * Las imágenes que se han agregado o eliminado aparecen enmarcadas en verde.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. En Sidekick, seleccione la subpestaña **Restaurar versión** y haga clic en el botón **&lt;&lt;Atrás** para mostrar la versión actual.

## Deformación de tiempo   {#timewarp}

Deformación de tiempo es una función diseñada para simular el estado ***publicado*** de una página en periodos específicos en el pasado.

El propósito es permitirle rastrear el sitio web publicado en el momento seleccionado. Utiliza las activaciones de página para determinar el estado del entorno de publicación.

Para ello:

* El sistema busca la versión de página que estaba activa en el momento seleccionado.
* Esto significa que la versión mostrada se creó o activó *antes del* punto temporal seleccionado en Deformación de tiempo.
* Al navegar a una página que se haya eliminado, esto también se procesa, siempre que las versiones anteriores de la página estén disponibles en el repositorio.
* Si no se encuentra ninguna versión publicada, Deformación de tiempo vuelve al estado actual de la página en el entorno de creación (para evitar una página de error/404, lo que significaría que ya no puede examinar).

>[!NOTE]
>
>Si las versiones se eliminan del repositorio, Deformación de tiempo no puede mostrar la vista correcta. Además, si los elementos para procesar el sitio web (código, css e imágenes) han cambiado, la vista difiere de la original, ya que no hay versiones de esos elementos en el repositorio.

### Uso del calendario de Deformación de tiempo {#using-the-timewarp-calendar}

Deformación de tiempo está disponible en la barra de tareas.

La versión del calendario se utiliza si tiene un día específico para ver:

1. Abra la ficha **Versiones** y haga clic en **Deformación de tiempo** (cerca de la parte inferior de la barra de tareas). Se muestra el siguiente cuadro de diálogo:

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Usando los selectores de fecha y hora, especifica la fecha y la hora que deseas y haz clic en **Ir**.

   Deformación de tiempo muestra la página tal como estaba en su estado publicado antes o en la fecha que ha elegido.

   >[!NOTE]
   >
   >Deformación de tiempo solo funciona a la perfección si ya ha publicado la página. En caso contrario, Deformación de tiempo muestra la página actual en el entorno de creación.

   >[!NOTE]
   >
   >Si se desplaza a una página que se ha eliminado del repositorio, se procesa correctamente si aún hay versiones antiguas de la página disponibles en el repositorio.

   >[!NOTE]
   >
   >No puede editar la versión antigua de la página. Tan solo pueden visualizarse. Si desea restaurar la versión anterior, puede hacerlo manualmente usando [restore](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick).

1. Cuando haya terminado de ver la página, haga clic en:

   * **Salir de Deformación de tiempo** para salir y volver a la página de creación actual.
   * [Mostrar escala de tiempo](#using-the-timewarp-timeline) para que pueda ver la escala de tiempo.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Uso de la cronología de deformación {#using-the-timewarp-timeline}

La versión de la cronología se utiliza si desea ver una descripción general de las actividades de publicación de la página.

Si desea ver la cronología del documento:

1. Para mostrar la cronología, siga uno de estos procedimientos:

   1. Abra la ficha **Asignación de versiones** y, a continuación, haga clic en **Deformación de tiempo** (cerca de la parte inferior de la barra de tareas).

   1. Use el cuadro de diálogo de la barra de tareas que se muestra después de [usando el calendario de Deformación de tiempo](#using-the-timewarp-calendar).

1. Haga clic en **Mostrar escala de tiempo**; aparecerá la escala de tiempo del documento; por ejemplo:

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Seleccione y mueva (mantenga pulsada y arrastre) la línea de tiempo para desplazarse por la línea de tiempo del documento.

   * Todas las líneas indican versiones publicadas.
Cuando se activa una página, se inicia una nueva línea. Cada vez que se edita el documento, aparece un nuevo color.
En el ejemplo siguiente, la línea roja indica que la página se editó durante el periodo de tiempo de la versión inicial verde. La línea amarilla indica que la página se editó en algún momento durante la versión roja, etc.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Haga clic:

   1. **Ir** para mostrar el contenido de la página publicada a la hora seleccionada.
   1. Al mostrar ese contenido, use **Deformación de tiempo de salida** para salir y volver a la página de creación actual.

### Limitaciones de Deformación de tiempo {#timewarp-limitations}

Deformación de tiempo realiza el mejor esfuerzo para reproducir una página en un punto temporal seleccionado. Sin embargo, debido a las complejidades de la creación continua de contenido en AEM, esto no siempre es posible. Estas limitaciones deben tenerse en cuenta al utilizar Deformación de tiempo.

* **Deformación de tiempo funciona dependiendo de las páginas publicadas**: deformación de tiempo solo funciona a la perfección si ya ha publicado la página. En caso contrario, Deformación de tiempo muestra la página actual en el entorno de creación.
* **Deformación de tiempo emplea las versiones de página**: si se desplaza a una página que se ha eliminado del repositorio, se procesa correctamente si aún hay versiones antiguas de la página en el repositorio.
* **Las versiones eliminadas afectan a la función Deformación de tiempo**: si las versiones se eliminan del repositorio, Deformación de tiempo no puede mostrar resultados correctos.

* **Deformación de tiempo es de solo lectura**: no se puede editar la versión antigua de la página. Tan solo pueden visualizarse. Si desea restaurar la versión anterior, puede hacerlo manualmente usando [restore](#main-pars-title-1).

* **Deformación de tiempo se basa solamente en el contenido de la página**: si los elementos para procesar el sitio web (como los elementos de código, CSS y recursos de imagen) han cambiado, la vista difiere de la vista original. El motivo es que estos elementos no tienen versiones en el repositorio.

>[!CAUTION]
>
>Deformación de tiempo está diseñada para ayudar a los autores a comprender y crear su contenido. No se trata de un registro de auditoría ni de un registro jurídico.
