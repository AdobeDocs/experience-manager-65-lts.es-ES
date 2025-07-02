---
title: Plantillas de recursos
description: Obtenga información acerca de las plantillas de recursos en  [!DNL Adobe Experience Manager Assets]  y cómo usar plantillas de recursos para crear material promocional.
role: User
feature: Asset Management,Developer Tools
solution: Experience Manager, Experience Manager Assets
exl-id: 8584d5ea-6ef2-4e81-8b18-5aa2d4226ea6
source-git-commit: 9ed889c74a886e1b41c379dac77bb570ef5c2c39
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Plantillas de recursos {#asset-templates}

Las plantillas de recursos son una clase especial de recursos que facilitan la reutilización rápida de contenido visualmente enriquecido para medios digitales e impresos. Una plantilla de activos consta de dos partes, la sección de mensajería fija y la sección editable. La sección de mensajería fija puede contener contenido de propiedad, como el logotipo de la marca y la información de copyright, que no se pueden editar. La sección editable puede contener contenido visual y textual en campos que se pueden editar para personalizar la mensajería.

La flexibilidad para realizar ediciones limitadas y, al mismo tiempo, proteger la señalización global hace que las plantillas de recursos sean los bloques de creación ideales para una adaptación y distribución rápidas del contenido como artefactos de contenido para diversas funciones. La reutilización del contenido ayuda a reducir el coste de gestión de los canales impresos y digitales, y ofrece experiencias integrales y coherentes en todos estos canales.

Como especialista en marketing, puede almacenar y administrar plantillas en [!DNL Experience Manager Assets] y utilizar una sola plantilla base para crear varias experiencias de impresión personalizadas con facilidad. Puede crear varios tipos de material promocional de marketing, incluidos folletos, prospectos, postales, tarjetas de presentación, etc., para transmitir con lucidez su mensaje de marketing a los clientes. También puede montar salidas de impresión de varias páginas a partir de salidas de impresión nuevas o existentes. Por encima de todo, puede ofrecer simultáneamente experiencias digitales e impresas con facilidad para proporcionar una experiencia coherente e integrada para los usuarios.

Aunque las plantillas de recursos son en su mayoría [!DNL Adobe InDesign] archivos, el dominio de [!DNL Adobe InDesign] no es una barrera para la creación de artefactos estelares. No necesita asignar los campos de la plantilla [!DNL Adobe InDesign] con los campos de producto que necesita asignar al crear catálogos. Puede editar las plantillas en el modo WYSIWYG directamente en la interfaz web. Sin embargo, para que [!DNL Adobe InDesign] procese los cambios de edición, primero debe configurar [!DNL Experience Manager Assets] para que se integre con [!DNL Adobe InDesign Server].

La capacidad de editar [!DNL Adobe InDesign] plantillas desde la interfaz web ayuda a fomentar una mayor colaboración entre el personal creativo y de marketing. El aumento de la velocidad de contenido reduce el tiempo de comercialización de las garantías reales de marketing.

Puede lograr lo siguiente con las plantillas de recursos:

* Modifique los campos de plantilla editables desde la interfaz web.
* Controle el estilo básico del texto, por ejemplo, el tamaño de fuente, el estilo y el tipo en el nivel de etiqueta.
* Cambiar imágenes dentro de la plantilla mediante el Selector de contenido.
* Previsualizar ediciones de plantilla.
* Combine varios archivos de plantilla para poder crear un artefacto de varias páginas.

Cuando elige una plantilla para el material colateral, [!DNL Experience Manager Assets] crea una copia de la plantilla que puede editar. La plantilla original se conserva, lo que garantiza que la señalización global permanezca intacta y se pueda reutilizar para reforzar la coherencia de la marca.

Puede exportar el archivo actualizado dentro de la carpeta principal en los formatos INDD, PDF o JPG. También puede descargar la salida en estos formatos en su sistema de archivos local.

## Crear una pieza colateral {#creating-a-collateral}

Imagine un escenario en el que desee crear material promocional imprimible digital, como folletos, prospectos y anuncios para una próxima campaña, y compártalo con tiendas de venta directa de todo el mundo. La creación de material promocional basado en una plantilla ayuda a ofrecer una experiencia de cliente unificada en todos los canales. Los diseñadores pueden crear las plantillas de campaña (de una sola página o de varias páginas) con una solución creativa, como [!DNL InDesign], y cargar las plantillas en [!DNL Experience Manager Assets] por usted. Antes de crear un material colateral, cargue una o más plantillas INDD en y estén disponibles en [!DNL Experience Manager] por adelantado.

1. En la interfaz [!DNL Experience Manager], seleccione [!UICONTROL Assets].

1. En las opciones, elija **[!UICONTROL Plantillas]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Seleccione **[!UICONTROL Crear]** y, a continuación, elija el material promocional que desea crear en el menú. Por ejemplo, elige **[!UICONTROL Folleto]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Tenga una o más plantillas INDD cargadas a y disponibles en [!DNL Experience Manager] por adelantado. Elija una plantilla para su folleto y haga clic en **[!UICONTROL Siguiente]**.
1. Especifique un nombre y una descripción opcional para el folleto.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Opcional) Haga clic en **[!UICONTROL Etiquetas]** y seleccione una o más etiquetas para el folleto. Haga clic en **[!UICONTROL Confirmar]** para confirmar la selección.
1. Haga clic en **[!UICONTROL Crear]**. Un cuadro de diálogo confirma que se ha creado un nuevo folleto. Haga clic en **[!UICONTROL Abrir]** para abrir el folleto en modo de edición.

   <!--![chlimage_1-106](assets/.png) -->

   También puede cerrar el cuadro de diálogo y desplazarse a la carpeta de la página Plantillas con la que comenzó para ver el folleto que ha creado. El tipo de material colateral aparece en la miniatura en la vista de tarjeta. Por ejemplo, en este caso, la palabra [!UICONTROL Folleto] se muestra en la miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Editar una pieza colateral {#editing-a-collateral}

Puede editar un material colateral inmediatamente después de crearlo. También puede abrirlo desde la página [!UICONTROL Plantillas] o la página de recursos.

1. Para abrir el material colateral para editarlo, siga uno de estos procedimientos:

   * Abra el material promocional (folleto en este caso) que creó en el paso 7 de [Crear un material promocional](/help/assets/asset-templates.md#creating-a-collateral).
   * En la página Plantillas, vaya a una carpeta en la que haya creado el material promocional y haga clic en la acción rápida [!UICONTROL Editar] que aparece en la miniatura de un material promocional.
   * En la página de activos de la garantía, haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
   * Seleccione el material promocional y haga clic en **[!UICONTROL Editar]** en la barra de herramientas.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   El buscador de recursos y el editor de texto se muestran a la izquierda de la página. El editor de texto está abierto de forma predeterminada.

   Utilice el editor de texto para modificar el texto que desea mostrar en el campo de texto. Puede modificar el tamaño, el estilo, el color y el tipo de fuente en el nivel de etiqueta.

   Para usar el buscador de recursos, puede examinar o buscar imágenes dentro de [!DNL Experience Manager Assets] y reemplazar las imágenes editables en la plantilla por imágenes de su elección.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Las imágenes editables se muestran a la derecha. Para que un campo se pueda editar en [!DNL Experience Manager Assets], el campo correspondiente de la plantilla debe estar etiquetado en [!DNL InDesign]. En otras palabras, se deben marcar como editables en [!DNL InDesign].

   >[!NOTE]
   >
   >Asegúrese de que la implementación de [!DNL Experience Manager] esté integrada con [!DNL InDesign Server] para permitir que [!DNL Experience Manager Assets] extraiga datos de la plantilla [!DNL InDesign] y que esté disponible para la edición. Para obtener más información, consulte [Integrar Experience Manager Assets con InDesign Server](/help/assets/indesign.md).

1. Para modificar el texto de un campo editable, haga clic en el campo de texto de la lista de campos editables y edite el texto del campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Puede editar las propiedades del texto, por ejemplo, el estilo de fuente, el color y el tamaño, mediante las opciones proporcionadas.

1. Seleccione **[!UICONTROL Vista previa]** para obtener una vista previa de los cambios del texto.

1. Para intercambiar una imagen, selecciona **[!UICONTROL Buscador de recursos]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Seleccione el campo de imagen de la lista de campos editables y, a continuación, arrastre una imagen deseada del selector de recursos al campo editable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   También puede buscar imágenes mediante palabras clave, etiquetas y en función de su estado de publicación. Puede examinar el repositorio [!DNL Experience Manager Assets] y desplazarse a la ubicación de la imagen deseada.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Seleccione **[!UICONTROL Vista previa]** para obtener una vista previa de la imagen.
1. Para editar una página específica en un material colateral de varias páginas, utilice el navegador de páginas en la parte inferior.

1. Seleccione **[!UICONTROL Vista previa]** en la barra de herramientas para obtener una vista previa de todos los cambios. Seleccione **[!UICONTROL Listo]** para guardar los cambios de edición en el material promocional.

   >[!NOTE]
   >
   >Las opciones Vista previa y Listo solo se activan cuando no falta ningún icono en los campos de imagen editables del material colateral. Si faltan iconos en el material colateral, se debe a que [!DNL Experience Manager] no puede resolver las imágenes de la plantilla [!DNL InDesign]. Por lo general, [!DNL Experience Manager] no puede resolver imágenes en los siguientes casos:
   >
   >* Las imágenes no están incrustadas en la plantilla [!DNL InDesign] subyacente.
   >* Las imágenes están vinculadas desde el sistema de archivos local.
   >
   >Para permitir que [!DNL Experience Manager] resuelva imágenes, haga lo siguiente:
   >
   >* Incrustar imágenes al crear [!DNL InDesign] plantillas (vea [Acerca de los vínculos y los gráficos incrustados](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Monte [!DNL Experience Manager] en el sistema de archivos local y, a continuación, asigne los iconos que faltan con los recursos existentes en [!DNL Experience Manager].

1. Para generar una representación de PDF para el folleto, seleccione la opción Acrobat en el cuadro de diálogo y haga clic en **[!UICONTROL Continuar]**.
1. El fragmento de material colateral se crea en la carpeta con la que comenzó. Para ver las representaciones, abra el material promocional y elija **[!UICONTROL Representaciones]** en la lista GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Seleccione la representación de PDF en la lista de representaciones para poder descargar el archivo PDF. Abra el archivo PDF para revisar el material colateral.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Combinar garantía {#merge-collateral}

1. En la interfaz [!DNL Experience Manager], seleccione [!UICONTROL Assets] en la página Navegación.

1. En las opciones, seleccione **[!UICONTROL Plantillas]**.

1. Seleccione **[!UICONTROL Crear]** y luego, en el menú, seleccione **[!UICONTROL Combinar]**.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. En la página [!UICONTROL Combinación de plantillas], seleccione **[!UICONTROL Combinar]** ![agregar recursos](assets/do-not-localize/assets_add_icon.png).

1. Desplácese hasta la ubicación de la parte del material colateral que desee combinar, seleccione las miniaturas del material colateral que desee combinar para seleccionarlas.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   También puede buscar plantillas desde el cuadro Omnisearch.

   Puede examinar el repositorio o las colecciones [!DNL Experience Manager Assets], y desplazarse hasta la ubicación de las plantillas deseadas y, a continuación, seleccionarlas para combinarlas.

   Puede aplicar varios filtros para buscar las plantillas deseadas. Por ejemplo, puede buscar plantillas basadas en el tipo de archivo o en las etiquetas.

1. Seleccione **[!UICONTROL Siguiente]** en la barra de herramientas.
1. En la pantalla **[!UICONTROL Previsualizar y reordenar]**, reorganice las plantillas si es necesario y previsualice la selección de plantillas para combinar. En la barra de herramientas, seleccione **[!UICONTROL Siguiente]**.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. En la pantalla [!UICONTROL Configurar plantilla], especifique un nombre para el material promocional. Si lo desea, especifique las etiquetas que considere adecuadas. Si desea exportar el resultado en formato PDF, seleccione **[!UICONTROL Acrobat (.PDF)]**. De forma predeterminada, el material colateral se exporta en formato JPG y [!DNL InDesign]. Para cambiar la miniatura de visualización del material promocional de varias páginas, haga clic en **[!UICONTROL Cambiar miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Seleccione **[!UICONTROL Guardar]** y, a continuación, cierre el cuadro de diálogo seleccionando **[!UICONTROL Aceptar]**. El material colateral de varias páginas se crea en la carpeta con la que comenzó.

   >[!NOTE]
   >
   >No se puede editar posteriormente un material colateral combinado ni utilizarlo para crear otro material colateral.

## Prácticas recomendadas y limitaciones {#best-practices-limitations-tips}

* El editor [!DNL InDesign] de [!DNL Experience Manager] funciona a nivel de etiqueta y todo el texto de una sola etiqueta se considera una sola entidad. Para conservar el formato y los estilos del texto al editar, etiquete por separado cada párrafo (o texto con un estilo diferente).
