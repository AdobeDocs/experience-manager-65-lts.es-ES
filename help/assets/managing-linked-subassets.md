---
title: Administrar recursos compuestos con referencias y varias páginas
description: Obtenga información sobre cómo crear referencias a recursos digitales desde  [!DNL Adobe InDesign], [!DNL Adobe Illustrator] y [!DNL Adobe Photoshop]. Utilice la función Visor de páginas para ver páginas de subrecursos individuales de archivos de varias páginas, como archivos PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Administración de recursos compuestos y de varias páginas {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] puede identificar si un archivo cargado contiene referencias a recursos que ya existen en el repositorio. Esta función solo está disponible para formatos de archivo compatibles. Si el recurso cargado contiene referencias a [!DNL Experience Manager] recursos, se crea un vínculo bidireccional entre los recursos cargados y los referenciados.

Además de eliminar la redundancia, hacer referencia a los recursos en aplicaciones de [!DNL Adobe Creative Cloud] mejora la colaboración y aumenta la eficiencia y productividad de los usuarios.

[!DNL Experience Manager Assets] admite referencias bidireccionales. Puede encontrar recursos a los que se hace referencia en la página de detalles de recursos del archivo cargado. Además, puede ver los archivos de referencia en la página de detalles de recurso del recurso al que se hace referencia.

Las referencias se resuelven en función de la ruta, el ID de documento y el ID de instancia de los recursos a los que se hace referencia.

## [!DNL Adobe Illustrator]: agregar recursos digitales como referencias {#refai}

Puede hacer referencia a recursos digitales existentes desde un archivo de [!DNL Adobe Illustrator].

1. Con [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es), recupere los recursos digitales en el sistema de archivos local. Vaya a la ubicación del sistema de archivos del recurso al que desee hacer referencia.
1. Arrastre el recurso de la carpeta local al archivo [!DNL Illustrator].

1. Guarde el archivo de [!DNL Illustrator] en la unidad montada o [cargue](/help/assets/manage-assets.md#uploading-assets) en el repositorio de [!DNL Experience Manager].

1. Una vez completado el flujo de trabajo, vaya a la página de detalles del recurso para el recurso. Las referencias a recursos digitales existentes se enumeran en **[!UICONTROL Dependencias]** en la columna **[!UICONTROL Referencias]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Los recursos a los que se hace referencia y que aparecen bajo **[!UICONTROL Dependencias]** también pueden ser referenciados por otros archivos que no sean el actual. Para ver una lista de archivos de referencia de un recurso, haga clic en el recurso en el bajo **[!UICONTROL Dependencias]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Haga clic en **[!UICONTROL Ver propiedades]** en la barra de herramientas. En la página [!UICONTROL Propiedades], la lista de archivos que hacen referencia al recurso actual aparece en la columna **[!UICONTROL Referencias]** de la ficha **[!UICONTROL Básico]**.

   ![ver las referencias de Experience Manager Assets en la columna Referencias en los detalles del recurso](assets/asset-references.png)

   *Figura: Referencias de recursos en los detalles del recurso.*

## [!DNL Adobe InDesign]: agregar recursos digitales como referencias {#add-aem-assets-as-references-in-adobe-indesign}

Para hacer referencia a recursos digitales desde un archivo de [!DNL InDesign], arrastre los recursos al archivo de [!DNL InDesign] o exporte el archivo de [!DNL InDesign] como un archivo ZIP.

Los recursos a los que se hace referencia ya existen en [!DNL Experience Manager Assets]. Puede extraer subrecursos al [configurar InDesign Server](indesign.md). Los recursos incrustados en un archivo [!DNL InDesign] se extraen como subrecursos.

>[!NOTE]
>
>Si [!DNL InDesign Server] se procesa como proxy, [!DNL InDesign] archivos tienen su vista previa incrustada en los metadatos de XMP. En este caso, la extracción de miniaturas no es obligatoria de forma explícita. Sin embargo, si [!DNL InDesign Server] no se procesa como proxy, las miniaturas deben extraerse explícitamente para [!DNL InDesign] archivos.

Cuando se carga un archivo INDD, las referencias se recuperan consultando los recursos que tienen las propiedades `xmpMM:InstanceID` y `xmpMM:DocumentID` en el repositorio.

### Creación de referencias arrastrando recursos {#create-references-by-dragging-aem-assets}

Este procedimiento es similar a [agregar recursos digitales como referencias en Adobe Illustrator](#refai).

### Crear referencias a recursos exportando un archivo ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Siga los pasos de [Crear modelos de flujo de trabajo](/help/sites-developing/workflows-models.md) para crear un flujo de trabajo.
1. Use [característica de paquete](https://helpx.adobe.com/es/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] para exportar el documento. [!DNL Adobe InDesign] puede exportar un documento y los recursos vinculados como un paquete. En este caso, la carpeta exportada contiene una carpeta `Links` que contiene subrecursos en el archivo [!DNL InDesign]. La carpeta `Links` está presente en la misma carpeta que el archivo INDD.
1. Cree un archivo ZIP y cárguelo en el repositorio [!DNL Experience Manager].
1. Inicie el flujo de trabajo `Unarchiver`.
1. Cuando se completa el flujo de trabajo, se hace referencia automáticamente a las referencias de la carpeta Links como subrecursos. Para ver una lista de recursos a los que se hace referencia, vaya a la página de detalles del recurso [!DNL InDesign] y cierre el [carril](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: agregar recursos digitales como referencias {#refps}

1. Use la aplicación de escritorio [!DNL Experience Manager] para tener acceso a [!DNL Experience Manager Assets]. Descargue y muestre los recursos en el sistema de archivos local. Use la funcionalidad [!UICONTROL Colocar elemento vinculado] en [!DNL Adobe Photoshop]. Ver [colocar recursos en la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es#place-assets-in-native-documents).

1. Guardar en [!DNL Photoshop] archivo en la unidad montada o [cargar](/help/assets/manage-assets.md#uploading-assets) en el repositorio [!DNL Experience Manager].
1. Una vez completado el flujo de trabajo, las referencias a los recursos existentes [!DNL Experience Manager] se enumeran en la página de detalles del recurso.

   Para ver los recursos a los que se hace referencia, cierre [Rail](/help/sites-authoring/basic-handling.md#rail-selector) en la página de detalles del recurso.

1. Los recursos a los que se hace referencia también contienen la lista de recursos desde la que se hace referencia a ellos. Para ver una lista de los recursos a los que se hace referencia, vaya a la página de detalles del recurso y cierre [Carril](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>También se puede hacer referencia a los recursos de los recursos compuestos en función de su ID de documento e ID de instancia. Esta funcionalidad solo está disponible con [!DNL Adobe Illustrator] y [!DNL Adobe Photoshop] versiones. Para otros, la referencia se realiza en función de la ruta relativa de los recursos vinculados en el recurso compuesto principal, como se hizo en versiones anteriores de [!DNL Experience Manager].

## Creación de subrecursos {#generate-subassets}

Para los recursos admitidos con formatos de varias páginas (archivos PDF, archivos AI, archivos [!DNL Microsoft PowerPoint] y [!DNL Apple Keynote], y archivos [!DNL Adobe InDesign]), [!DNL Experience Manager] puede generar subrecursos que corresponden a cada página individual del recurso original. Estos subrecursos están vinculados al recurso *parent* y facilitan la vista de varias páginas. Para todos los demás fines, los subrecursos se tratan como recursos normales en [!DNL Experience Manager].

La generación de subrecursos está deshabilitada de forma predeterminada. Para habilitar la generación de subrecursos, siga estos pasos:

1. Inicie sesión en [!DNL Experience Manager] como administrador. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Seleccione el flujo de trabajo **[!UICONTROL DAM Update Asset]** y haga clic en **[!UICONTROL Editar]**.
1. Haga clic en **[!UICONTROL Alternar panel lateral]** y busque el paso **[!UICONTROL Crear subrecurso]**. Añada la etapa al flujo de trabajo. Haga clic en **[!UICONTROL Sincronizar]**.

Para generar los subrecursos, realice una de las siguientes acciones:

* Nuevos recursos: El flujo de trabajo [!UICONTROL DAM Update Assets] se ejecuta en cualquier nuevo recurso que se haya cargado en [!DNL Experience Manager]. Los subrecursos se generan automáticamente para los nuevos recursos de varias páginas.
* Recursos de varias páginas existentes: ejecute manualmente el flujo de trabajo [!UICONTROL DAM Update Assets] siguiendo uno de estos pasos:

   * Seleccione un recurso y haga clic en [!UICONTROL Cronología] para abrir el panel izquierdo. También puede usar el método abreviado de teclado `alt + 3`. Haga clic en [!UICONTROL Iniciar flujo de trabajo], seleccione [!UICONTROL Recurso de actualización DAM], haga clic en [!UICONTROL Iniciar] y haga clic en [!UICONTROL Continuar].
   * Seleccione un recurso y haga clic en [!UICONTROL Crear] > [!UICONTROL Flujo de trabajo] en la barra de herramientas. En el cuadro de diálogo emergente, seleccione el flujo de trabajo [!UICONTROL Recurso de actualización DAM], haga clic en [!UICONTROL Iniciar] y haga clic en [!UICONTROL Continuar].

Específicamente para documentos de Microsoft Word, ejecute el flujo de trabajo **[!UICONTROL DAM Analizar documentos de Word]**. Genera un componente `cq:Page` a partir del contenido del documento de Microsoft Word. Se hace referencia a las imágenes extraídas del documento desde el componente `cq:Page`. Estas imágenes se extraen incluso si la generación de subrecursos está desactivada.

>[!NOTE]
>
>En [!UICONTROL Crear proceso de subrecursos - Propiedades de la etapa] en [!UICONTROL Argumentos del proceso], puede especificar el número de subrecursos que [!DNL Experience Manager] genera. El valor predeterminado es 5. Para generar todos los subrecursos, deje vacío el campo. Si el campo tiene un valor negativo, no se generan subrecursos.

## Ver subrecursos {#viewing-subassets}

Los subrecursos solo se muestran si se generan y están disponibles para el recurso de varias páginas seleccionado. Para ver los subrecursos generados, abra el recurso de varias páginas. En el área superior izquierda de la página, haga clic en ![Opción para abrir el carril izquierdo](assets/do-not-localize/aem_leftrail_contentonly.png) y haga clic en **[!UICONTROL Subrecursos]** de la lista. Cuando seleccione **[!UICONTROL Subrecursos]** de la lista. También puede usar el método abreviado de teclado `alt + 5`.

![Ver recursos secundarios de un recurso de varias páginas](assets/view_subassets_simulation.gif)

## Ver páginas de un archivo de varias páginas {#view-pages-of-a-multi-page-file}

Puede ver un archivo de varias páginas, como PDF, INDD, PPT, PPTX y AI, mediante la característica Visor de páginas de [!DNL Experience Manager Assets]. Abra un recurso de varias páginas y haga clic en **[!UICONTROL Ver páginas]** desde la esquina superior izquierda de la página. El visor de páginas que se abre muestra las páginas del recurso y los controles para examinar y ampliar cada página.

![Ver y ver páginas de un recurso de varias páginas](assets/view_multipage_asset_fmr.gif)

Para [!DNL InDesign], puede extraer páginas mediante [!DNL InDesign Server]. Si las vistas previas de las páginas se guardan durante la creación del archivo de [!DNL InDesign], entonces [!DNL InDesign Server] no es necesario para la extracción de páginas.

Las siguientes opciones están disponibles en la barra de herramientas, en el carril izquierdo y en los controles del visor de páginas:

* **[!UICONTROL Acciones de escritorio]** para abrir o mostrar un subrecurso específico mediante la aplicación de escritorio [!DNL Experience Manager]. Consulte cómo [configurar acciones de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es#desktopactions-v2) si usa la aplicación de escritorio [!DNL Experience Manager].

* La opción **[!UICONTROL Propiedades]** abre la página [!UICONTROL Propiedades] del subrecurso específico.

* La opción **[!UICONTROL Anotar]** le permite anotar el subrecurso específico. Las anotaciones que utilice en subrecursos independientes se recopilan y se muestran juntas cuando el recurso principal se abre para su visualización.

* La opción **[!UICONTROL Información general de página]** muestra todos los subrecursos simultáneamente.

* La opción **[!UICONTROL Cronología]** del carril izquierdo después de hacer clic en ![Opción para abrir el carril izquierdo](assets/do-not-localize/aem_leftrail_contentonly.png) muestra el flujo de actividad del archivo.

## Prácticas recomendadas y limitación {#best-practice-limitation-tips}

* La generación de subrecursos puede consumir muchos recursos en cualquier implementación de [!DNL Experience Manager]. Si está generando subrecursos cuando se cargan recursos complejos, agregue el paso en el flujo de trabajo de recursos de actualización de DAM. Si está generando subrecursos bajo demanda, cree un flujo de trabajo independiente para generar subrecursos. Un flujo de trabajo dedicado le permite omitir los demás pasos del flujo de trabajo de recursos de actualización de DAM y guardar recursos de cálculo.

>[!MORELIKETHIS]
>
>* [Usar la aplicación de escritorio de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es)
>* [Configurar acciones de escritorio en Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es#desktopactions-v2)
>* [Crear objetos inteligentes vinculados en Adobe Photoshop](https://helpx.adobe.com/es/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Colocar gráficos en Adobe InDesign](https://helpx.adobe.com/es/indesign/using/placing-graphics.html)
