---
title: Perfiles para procesar metadatos, imágenes y vídeos
description: Un perfil define un conjunto de reglas sobre las opciones que se aplicarán a los recursos cargados en una carpeta. Especifique qué perfil de metadatos y perfil de codificación de vídeo aplicar a los recursos de vídeo que carga. En el caso de los recursos de imagen, también puede especificar qué perfil de imagen aplicar a los recursos de imagen para que se recorten correctamente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
role: User, Admin
feature: Workflow,Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Perfiles para procesar metadatos, imágenes y vídeos{#profiles-for-processing-metadata-images-and-videos}

Un perfil es una fórmula para determinar qué opciones aplicar a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar qué perfil de metadatos y perfil de codificación de vídeo aplicar a los recursos de vídeo que carga. O bien, qué perfil de imagen aplicar a los recursos de imagen para que se recorten correctamente.

Estas reglas pueden incluir la adición de metadatos, el recorte inteligente de imágenes o el establecimiento de perfiles de codificación de vídeo. En Adobe Experience Manager, puede crear tres tipos de perfiles, que se tratan en detalle en los siguientes vínculos:

* [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles)
* [Perfiles de imagen](/help/assets/image-profiles.md)
* [Perfiles de vídeo](/help/assets/video-profiles.md)

Necesita derechos de administrador para crear, editar y eliminar metadatos, imágenes o perfiles de vídeo.

Después de crear los metadatos, las imágenes o el perfil de vídeo, debe asignarlos a una o varias carpetas que utilice como destino para los recursos recién cargados.

Un concepto importante con respecto al uso de perfiles en Experience Manager Assets es que se asignan a carpetas. Dentro de un perfil hay ajustes en forma de perfiles de metadatos, junto con perfiles de vídeo o perfiles de imagen. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, el modo de asignar nombres a los archivos y carpetas, organizar las subcarpetas y administrar los archivos de estas carpetas tiene un impacto significativo en la forma en que un perfil procesa esos recursos.
Al utilizar estrategias de nomenclatura de archivos y carpetas coherentes y adecuadas, así como una buena práctica de metadatos, puede sacar el máximo partido a la colección de recursos digitales y asegurarse de que los archivos correctos se procesan mediante el perfil correcto.

>[!NOTE]
>
>Assets que se mueve de una carpeta a otra no se vuelve a procesar. Por ejemplo, supongamos que tiene la carpeta 1 con el perfil A asignado y la carpeta 2 con el perfil B asignado. Si mueve recursos de la carpeta 1 a la carpeta 2, los recursos movidos conservarán su procesamiento original de la carpeta 1.
>
>Lo mismo ocurre incluso cuando se mueven recursos entre dos carpetas que tienen asignado el mismo perfil.

## Volver a procesar recursos en una carpeta {#reprocessing-assets}

>[!NOTE]
>
>Se aplica a *Dynamic Media - Modo Scene7* solo en Experience Manager 6.4.6.0 o posterior.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de procesamiento existente cambiado a posteriori.

Por ejemplo, supongamos que ha creado un perfil de imagen y lo ha asignado a una carpeta. Cualquier recurso de imagen que haya cargado en la carpeta tenía automáticamente el perfil de imagen aplicado a los recursos. Sin embargo, más adelante decide añadir una nueva proporción de recorte inteligente al perfil. Ahora, en lugar de volver a seleccionar y volver a cargar los recursos en la carpeta, simplemente ejecute el flujo de trabajo *Reprocesamiento de Dynamic Media* <!-- *Scene7: Reprocess Assets* -->.

Puede ejecutar el flujo de trabajo de reprocesamiento en un recurso en el que se haya producido un error de procesamiento por primera vez. De este modo, aunque no haya editado un perfil de procesamiento ni aplicado un perfil de procesamiento, puede ejecutar el flujo de trabajo de reprocesamiento en una carpeta de recursos en cualquier momento.

Si lo desea, puede ajustar el tamaño del lote del flujo de trabajo de reprocesamiento desde un valor predeterminado de 50 hasta 1000 recursos. Al ejecutar el flujo de trabajo _Scene7: Reprocesar Assets_ en una carpeta, los recursos se agrupan en lotes y se envían al servidor de Dynamic Media para su procesamiento. Después del procesamiento, los metadatos de cada recurso del conjunto completo de lotes se actualizan en Experience Manager. Si el tamaño del lote es grande, puede experimentar un retraso en el procesamiento. O bien, si el tamaño del lote es demasiado pequeño, puede causar demasiados viajes de ida y vuelta al servidor de Dynamic Media.

Consulte [Ajustar el tamaño del lote del flujo de trabajo de nuevo procesamiento](#adjusting-load).

>[!NOTE]
>
>Si realiza una migración masiva de recursos de Dynamic Media Classic a Experience Manager, debe habilitar el agente de replicación de migración en el servidor de Dynamic Media. Cuando finalice la migración, asegúrese de desactivar el agente.
>
>El agente de publicación de migración debe estar desactivado en el servidor de Dynamic Media para que el flujo de trabajo de reprocesamiento funcione según lo esperado.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job, and so on, until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Para volver a procesar recursos en una carpeta:**

1. En Experience Manager, en la página de Assets, navegue hasta una carpeta de recursos que tenga un perfil de procesamiento asignado y para la que desee aplicar el flujo de trabajo **[!UICONTROL Reprocesamiento de Dynamic Media]**,

   Las carpetas que ya tienen un perfil de procesamiento asignado se indican mostrando el nombre del perfil directamente debajo del nombre de la carpeta en la vista de tarjeta.

1. Seleccione una carpeta.

   * El flujo de trabajo considera recursivamente todos los archivos de la carpeta seleccionada.
   * Si hay una o más subcarpetas con recursos en la carpeta principal seleccionada, el flujo de trabajo vuelve a procesar cada recurso en la jerarquía de carpetas.
   * Se recomienda evitar ejecutar este flujo de trabajo en una jerarquía de carpetas que tenga más de 1000 recursos.

1. Cerca de la esquina superior izquierda de la página, en la lista desplegable, seleccione **[!UICONTROL Cronología]**.
1. Cerca de la esquina inferior izquierda de la página, a la derecha del campo Comentario, seleccione el icono en forma de quilate ( **^** ) .

   ![Volver a procesar recursos del flujo de trabajo 1](/help/assets/assets/reprocess-assets1.png)

1. Seleccione **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la lista desplegable **[!UICONTROL Iniciar flujo de trabajo]**, elija **[!UICONTROL Reprocesar Dynamic Media]**.
1. (Opcional) En el campo de texto **Escriba el título del flujo de trabajo**, escriba un nombre para el flujo de trabajo. Puede utilizar el nombre para hacer referencia a la instancia de flujo de trabajo, si es necesario.

   ![Volver a procesar recursos 2](/help/assets/assets/reprocess-assets2.png)

1. Seleccione **[!UICONTROL Iniciar]** y luego seleccione **[!UICONTROL Confirmar]**.

   Para supervisar el flujo de trabajo o comprobar su progreso, en la página de la consola principal de Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]**. En la página Instancias de flujo de trabajo, seleccione un flujo de trabajo. En la barra de menús, seleccione **[!UICONTROL Abrir historial]**. También puede finalizar, suspender o cambiar el nombre de un flujo de trabajo seleccionado desde la misma página Instancias de flujo de trabajo.

### Ajustar el tamaño del lote del flujo de trabajo de reprocesamiento {#adjusting-load}

(Opcional) El tamaño de lote predeterminado en el flujo de trabajo de reprocesamiento es de 50 recursos por trabajo. Este tamaño de lote óptimo está regido por el tamaño promedio del recurso y los tipos MIME de los recursos en los que se ejecuta el reprocesamiento. Un valor mayor significa que tiene muchos archivos en un solo trabajo de reprocesamiento. Por lo tanto, el banner de procesamiento permanece en los recursos de Experience Manager durante más tiempo. Sin embargo, si el tamaño medio del archivo es pequeño (1 MB o menos), Adobe recomienda aumentar el valor a varios 100, pero nunca más de 1000. Si el tamaño medio del archivo es grande, como cientos de megabytes, Adobe recomienda reducir el tamaño del lote hasta 10.

**Para ajustar opcionalmente el tamaño del lote del flujo de trabajo de reprocesamiento:**

1. En Experience Manager, seleccione **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, seleccione el icono **[!UICONTROL Herramientas]** (martillo) > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo, en Vista de tarjeta o Vista de lista, seleccione **[!UICONTROL Reprocesar Dynamic Media]**.

   ![Página de modelos de flujo de trabajo con flujo de trabajo de reprocesamiento de Dynamic Media seleccionado en la vista de tarjeta](/help/assets/assets-dm/reprocess-assets7.png)

1. En la barra de herramientas, seleccione **[!UICONTROL Editar]**. Una nueva pestaña del explorador abre la página del modelo de flujo de trabajo Reprocesamiento de Dynamic Media.
1. En la página Flujo de trabajo de reprocesamiento de Dynamic Media, cerca de la esquina superior derecha, seleccione **[!UICONTROL Editar]** para &quot;desbloquear&quot; el flujo de trabajo.
1. En el flujo de trabajo, seleccione el componente Carga por lotes de Scene7 para abrir la barra de herramientas y, a continuación, seleccione **[!UICONTROL Configurar]** en la barra de herramientas.

   ![Componente de carga en lote de Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. En el cuadro de diálogo **[!UICONTROL Cargar lotes en Scene7 - Propiedades de la etapa]**, establezca lo siguiente:
   * En los campos de texto **[!UICONTROL Título]** y **[!UICONTROL Descripción]**, escriba un nuevo título y una descripción para el trabajo, si lo desea.
   * Seleccione **[!UICONTROL Avance de controlador]** si su controlador avanzará al siguiente paso.
   * En el campo **[!UICONTROL Tiempo de espera]**, introduzca el tiempo de espera del proceso externo (segundos).
   * En el campo **[!UICONTROL Periodo]**, introduzca un intervalo de sondeo (segundos) para comprobar la finalización del proceso externo.
   * En el campo **[!UICONTROL Lote]**, introduzca el número máximo de recursos (50-1000) que se procesarán en un trabajo de carga por lotes del servidor de Dynamic Media.
   * Seleccione **[!UICONTROL Avanzar en el tiempo de espera]** si desea avanzar cuando se alcance el tiempo de espera. Cancele la selección si desea continuar en la bandeja de entrada cuando se alcance el tiempo de espera.

   ![Cuadro de diálogo Propiedades](/help/assets/assets-dm/reprocess-assets3.png)

1. En la esquina superior derecha del cuadro de diálogo **[!UICONTROL Cargar lotes a Scene7 - Propiedades del paso]**, seleccione **[!UICONTROL Listo]**.

1. En la esquina superior derecha de la página Modelo de flujo de trabajo de reprocesamiento de Dynamic Media, seleccione **[!UICONTROL Sincronizar]**. Cuando vea **[!UICONTROL Sincronizado]**, el modelo de tiempo de ejecución del flujo de trabajo se sincronizará correctamente y estará listo para volver a procesar los recursos de una carpeta.

   ![Sincronizar el modelo de flujo de trabajo](/help/assets/assets-dm/reprocess-assets1.png)

1. Cierre la pestaña del explorador que muestra el modelo de flujo de trabajo de reprocesamiento de Dynamic Media.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.-->
