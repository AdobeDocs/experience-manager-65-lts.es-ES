---
title: Creación de proyectos de traducción
description: Aprenda a crear proyectos de traducción en  [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Translation
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 13%

---

# Creación de proyectos de traducción {#creating-translation-projects}

Para crear una copia de idioma, déclencheur uno de los siguientes flujos de trabajo de copia de idioma disponibles en el carril Referencias de la interfaz de usuario [!DNL Experience Manager].

* **Crear y traducir**: en este flujo de trabajo, los recursos que se van a traducir se copian a la raíz del idioma al que desea traducirlos. Además, según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción se puede iniciar manualmente o se puede permitir que se ejecute automáticamente en cuanto se cree el proyecto de traducción.

* **Actualizar copias de idioma**: ejecute este flujo de trabajo para traducir un grupo adicional de recursos e incluirlo en una copia de idioma para una configuración regional determinada. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene los recursos traducidos anteriormente.

>[!PREREQUISITES]
>
>* Los usuarios que crean proyectos de traducción son miembros del grupo `projects-administrators`.
>* El proveedor de servicios de traducción admite la traducción de binarios.

## Crear y traducir flujo de trabajo {#create-and-translate-workflow}

El flujo de trabajo de creación y traducción se utiliza para generar copias de idioma para un idioma concreto por primera vez. El flujo de trabajo ofrece las siguientes opciones:

* Crear solo una estructura.
* Cree un proyecto de traducción.
* Añada a un proyecto de traducción existente.

### Crear solo una estructura {#create-structure-only}

Utilice la opción **[!UICONTROL Crear solo estructura]** para diseñar una jerarquía de carpetas de destino dentro de la raíz del idioma de destino para que coincida con la jerarquía de la carpeta de origen dentro de la raíz del idioma de origen. En este caso, los recursos de origen se copian en la carpeta de destino. Sin embargo, no se genera ningún proyecto de traducción.

1. En la interfaz [!DNL Assets], seleccione la carpeta de origen para la que desea crear una estructura en la raíz del idioma de destino.

1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Copias de idioma]** en **[!UICONTROL Copias]**.

   ![Copias de idioma](assets/translation-language-copies.png)

1. Haga clic en **[!UICONTROL Crear y traducir]**. En la lista **[!UICONTROL Idiomas de destino]**, seleccione el idioma para el que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear estructura únicamente]**.

1. Haga clic en **[!UICONTROL Crear]**. La nueva estructura para el idioma de destino se enumera en **[!UICONTROL Copias de idioma]**.

   ![copias de idioma](assets/lang-copy2.png)

1. Haga clic en la estructura de la lista y, a continuación, haga clic en **[!UICONTROL Mostrar en Assets]** para desplazarse a la estructura de carpetas en el idioma de destino.

   ![mostrar recursos](assets/reveal-in-assets.png)

### Crear un proyecto de traducción {#create-a-new-translation-project}

Si utiliza esta opción, los recursos que desea traducir se copian en la raíz del idioma al que desea traducirlo. Según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción se puede iniciar manualmente o se ejecuta automáticamente en cuanto se crea el proyecto de traducción.

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta de origen para la que desea crear una copia de idioma.
1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Copias de idioma]** en **[!UICONTROL Copias]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Haz clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear un nuevo proyecto de traducción]**.

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

1. Haga clic en **[!UICONTROL Crear]**. [!DNL Assets] de la carpeta de origen se copiarán en las carpetas de destino de las configuraciones regionales seleccionadas en el paso 4.

   ![copias de idioma](assets/lang-copy2.png)

1. Para ir a la carpeta, selecciona la copia de idioma y haz clic en **[!UICONTROL Mostrar en Assets]**.

   ![mostrar recursos](assets/reveal-in-assets.png)

1. Vaya a la consola Proyectos. La carpeta de traducción se copia en la consola Proyectos.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Abra la carpeta para ver el proyecto de traducción.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Para obtener más información sobre los estados de los trabajos, consulte [Supervisión del estado de un trabajo de traducción](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Vaya a la interfaz de usuario [!DNL Assets] y abra la página [!UICONTROL Propiedades] de cada uno de los recursos traducidos para ver los metadatos traducidos.

   ![ver los metadatos traducidos en la página Propiedades del recurso](assets/translated-metadata-asset-properties.png)

   *Imagen: metadatos traducidos en la página de propiedades del recurso.*

   >[!NOTE]
   >
   >Esta función está disponible tanto para recursos como para carpetas. Cuando se selecciona un recurso en lugar de una carpeta, se copia toda la jerarquía de carpetas hasta la raíz del idioma para crear una copia de idioma para el recurso.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project}

Si utiliza esta opción, el flujo de trabajo de traducción se ejecuta para los recursos que agrega a la carpeta de origen después de ejecutar un flujo de trabajo de traducción anterior. Solo los recursos recién añadidos se copian en la carpeta de destino que contiene los recursos traducidos anteriormente. En este caso, no se crea ningún proyecto de traducción nuevo.

1. En la interfaz de usuario [!DNL Assets], vaya a la carpeta de origen que contiene los recursos sin traducir.
1. Seleccione un recurso que desee traducir y abra el **[!UICONTROL panel Referencias]**. La sección **[!UICONTROL Textos en idiomas]** muestra el número de traducciones disponibles en ese momento.
1. Haga clic en **[!UICONTROL Copias de idioma]** en **[!UICONTROL Copias]**. Se muestra una lista de las traducciones disponibles.
1. Haz clic en **[!UICONTROL Crear y traducir]** en la parte inferior.

1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.

1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Agregar a proyecto de traducción]** existente para ejecutar el flujo de trabajo de traducción en la carpeta.

   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Agregar a proyecto de traducción existente]**, el proyecto de traducción se agregará a un proyecto preexistente solo si la configuración del proyecto coincide exactamente con la configuración del proyecto preexistente. De lo contrario, se crea un nuevo proyecto.

1. En la lista **[!UICONTROL Proyecto de traducción existente]**, seleccione un proyecto para agregar el recurso para su traducción.

1. Haga clic en **[!UICONTROL Crear]**. Los recursos que se van a traducir se agregan a la carpeta de destino. La carpeta actualizada se muestra en la sección **[!UICONTROL Textos en idiomas]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Vaya a la consola Proyectos y abra el proyecto de traducción existente que agregó a.
1. Haga clic en el proyecto de traducción para ver la página de detalles del proyecto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Haga clic en los puntos suspensivos en la parte inferior del mosaico **Trabajo de traducción** para ver los recursos en el flujo de trabajo de traducción. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

   >[!NOTE]
   >
   >Si elimina la entrada para etiquetas o metadatos, no se traducen etiquetas o metadatos para ninguno de los recursos.

   >[!NOTE]
   >
   >Si el recurso que agrega al trabajo de traducción incluye subrecursos, selecciónelos y elimínelos para que la traducción continúe sin problemas.

1. Para iniciar la traducción de los recursos, haga clic en la flecha del mosaico **[!UICONTROL Trabajo de traducción]** y seleccione **[!UICONTROL Iniciar]** en la lista.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un mensaje notifica el comienzo del trabajo de traducción.

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Para obtener más información, consulte [Supervisión del estado de un trabajo de traducción](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Una vez finalizada la traducción, el estado cambia a Listo para revisión. Vaya a la interfaz de usuario [!DNL Assets] y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

## Actualizar copias de idioma {#update-language-copies}

Ejecute este flujo de trabajo para traducir cualquier conjunto adicional de recursos e incluirlos en una copia de idioma para una configuración regional determinada. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene los recursos traducidos anteriormente. Según la opción de opciones, se crea un proyecto de traducción o se actualiza uno existente para los nuevos recursos. El flujo de trabajo Actualizar copias de idioma incluye las siguientes opciones:

* Crear un proyecto de traducción
* Añadir a un proyecto de traducción existente

### Crear un proyecto de traducción {#create-a-new-translation-project-1}

Si utiliza esta opción, se crea un proyecto de traducción para el conjunto de recursos para el que desea actualizar una copia de idioma.

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta de origen donde agregó un recurso.
1. Abra el panel **[!UICONTROL Referencias]** y haga clic en **[!UICONTROL Copias de idioma]** en **[!UICONTROL Copias]** para mostrar la lista de copias de idioma.
1. Seleccione la casilla de verificación antes de **[!UICONTROL Textos en idiomas]** y, a continuación, seleccione la carpeta de destino correspondiente a la configuración regional adecuada.

   ![seleccionar copia de idioma](assets/lang-copy1.png)

1. Haga clic en **[!UICONTROL Actualizar copias de idioma]** en la parte inferior.

1. En la lista **[!UICONTROL Proyecto]**, elija **[!UICONTROL Crear un nuevo proyecto de traducción]**.

1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.

1. Haga clic en **[!UICONTROL Iniciar]**.
1. Vaya a la consola Proyectos. La carpeta de traducción se copia en la consola Proyectos.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Abra la carpeta para ver el proyecto de traducción.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Haga clic en el proyecto para abrir la página de detalles.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para iniciar la traducción de los recursos, haga clic en la flecha del mosaico **[!UICONTROL Trabajo de traducción]** y seleccione **[!UICONTROL Iniciar]** en la lista.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un mensaje notifica el comienzo del trabajo de traducción.

1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Para obtener más información sobre los estados de los trabajos, consulte [Supervisión del estado de un trabajo de traducción](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Vaya a la interfaz de usuario [!DNL Assets] y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project-1}

Si utiliza esta opción, el conjunto de recursos se agrega a un proyecto de traducción existente para actualizar la copia de idioma de la configuración regional que elija.

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta de origen donde agregó una carpeta de recursos.
1. Abra el **[!UICONTROL panel Referencias]** y haga clic en **[!UICONTROL Copias de idioma]** en **[!UICONTROL Copias]** para mostrar la lista de copias de idioma.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Seleccione la casilla de verificación que se encuentra delante de **[!UICONTROL Textos en idiomas]**, de esta forma, selecciona los textos disponibles en diferentes idiomas. Anule la selección de otros textos excepto el texto (textos) en el idioma correspondiente a las configuraciones regionales a las que desea traducir.

   ![seleccionar copia de idioma](assets/lang-copy1.png)

1. Haga clic en **[!UICONTROL Actualizar copias de idioma]** en la parte inferior.

1. En la lista **[!UICONTROL Proyecto]**, elija **[!UICONTROL Agregar a proyecto de traducción existente]**.

1. En la lista **[!UICONTROL Proyecto de traducción existente]**, seleccione un proyecto para agregar el recurso para su traducción.

1. Haga clic en **[!UICONTROL Iniciar]**.
1. Consulte los pasos 9-14 de [Agregar a un proyecto de traducción existente](translation-projects.md#add-to-existing-translation-project) para completar el resto del procedimiento.

## Creación de copias de idioma temporales {#creating-temporary-language-copies}

Cuando se ejecuta un flujo de trabajo de traducción para actualizar una copia de idioma con versiones editadas de los recursos originales, la copia de idioma existente se conserva hasta que se aprueban los recursos traducidos. [!DNL Adobe Experience Manager Assets] almacena los recursos recién traducidos en una ubicación temporal y actualiza la copia de idioma existente después de aprobar explícitamente los recursos. Si rechaza los recursos, la copia de idioma no se cambiará.

1. Haga clic en la carpeta raíz de origen en **[!UICONTROL Copias de idioma]** para la que ya creó una copia de idioma y, a continuación, haga clic en **[!UICONTROL Mostrar en Assets]** para abrir la carpeta en [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. En la interfaz [!DNL Assets], seleccione un recurso que ya ha traducido y haga clic en **[!UICONTROL Editar]** en la barra de herramientas para abrir el recurso en modo de edición.
1. Edite el recurso y, a continuación, guarde los cambios.
1. Realice los pasos 2-14 del procedimiento [Agregar a proyecto de traducción existente](#add-to-existing-translation-project) para actualizar la copia de idioma.
1. Haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**. Desde la lista de recursos de la página **[!UICONTROL Trabajo de traducción]**, puede ver claramente la ubicación temporal en la que se almacena la versión traducida del recurso.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Seleccione la casilla que está junto a **[!UICONTROL Título]**.
1. En la barra de herramientas, haga clic en **[!UICONTROL Aceptar traducción]** ![aceptar traducción](assets/do-not-localize/thumb-up.png) y luego haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para sobrescribir el recurso traducido en la carpeta de destino con la versión traducida del recurso editado.

   >[!NOTE]
   >
   >Para permitir que el flujo de trabajo de traducción actualice los recursos de destino, acepte el recurso y los metadatos.

   Haga clic en **[!UICONTROL Rechazar traducción]** ![rechazar traducción](assets/do-not-localize/thumb-down.png) para conservar la versión traducida originalmente del recurso en la raíz de la configuración regional de destino y rechazar la versión editada.

1. Para ver los metadatos traducidos, vaya a la consola [!DNL Assets] y abra la página [!UICONTROL Propiedades] para cada uno de los recursos traducidos.

## Sugerencias y limitaciones {#tips-limitations}

* Si inicia un flujo de trabajo de traducción para recursos complejos, como PDF y [!DNL Adobe InDesign] archivos, sus subrecursos o representaciones (si los hay) no se envían para su traducción.
* Si utiliza la traducción automática, los binarios de recursos no se traducen.
