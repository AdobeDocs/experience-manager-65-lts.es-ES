---
title: Configurar el tipo de archivo
description: Obtenga información sobre cómo configurar los ajustes de tipo de archivo. En PDF Generator, puede establecer la configuración de la aplicación para los tipos de archivo compatibles y establecer la configuración del tipo de archivo.
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 68896dab-2d46-4998-9918-40efb8554143
source-git-commit: 9d4681c0b184cc7769a8da20a4c50d420e1137c7
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 0%

---

# Configurar el tipo de archivo {#configuring-file-type-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

En PDF Generator, puede establecer la configuración de la aplicación para los tipos de archivo admitidos. En Windows, puede establecer la configuración de la aplicación para cada tipo de archivo compatible. En UNIX y Linux, puede configurar los ajustes de la aplicación para HTML a PDF y OpenOffice.

En la página Configuración de tipo de archivo, puede realizar estas tareas:

* [Crear o editar una configuración de Tipo de archivo](#create-or-edit-file-type-settings)
* Especifique qué configuración de tipo de archivo se usará de forma predeterminada (consulte [Importación y exportación de archivos de configuración de PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Cambiar la configuración predeterminada](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Habilitar compatibilidad con PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminar una configuración de tipo de archivo](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>La configuración del tipo de archivo no está disponible para los convertidores de reserva, como Acrobat para HTML a PDF, Microsoft PowerPoint, Microsoft Word y Microsoft Excel.

## Crear o editar la configuración de Tipo de archivo {#create-or-edit-file-type-settings}

Cree o edite una configuración de tipo de archivo para especificar cómo administra la aplicación la conversión de los tipos de archivo admitidos. En Windows, puede establecer la configuración de la aplicación para cada tipo de archivo compatible. En UNIX y Linux, puede configurar los ajustes de la aplicación para HTML a PDF y OpenOffice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Configuración de tipo de archivo]**.
1. Haga clic en Nuevo o haga clic en el nombre de una configuración.
1. En el cuadro Extensiones de nombre de archivo, escriba las extensiones de nombre de archivo, separadas por comas, para los tipos de archivo aceptados para esta aplicación. No incluya el punto anterior o un espacio entre las extensiones. El valor predeterminado es `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para utilizar el reconocimiento óptico de código (OCR) de texto en gráficos o imágenes, seleccione Usar OCR y defina las siguientes opciones:

**Idioma principal de OCR:** Idioma que debe usar el motor de OCR para identificar los caracteres. El valor predeterminado es Inglés (EE.UU.).

**Estilo de salida de PDF:** Seleccione la imagen que permite búsquedas para tener una imagen de mapa de bits de las páginas en primer plano y el texto digitalizado en una capa invisible debajo. El aspecto de la página no cambia, pero el texto se puede seleccionar y leer. Seleccione Texto y gráficos con formato para reconstruir la página original utilizando texto, fuentes, imágenes y otros elementos gráficos reconocidos. El valor predeterminado es Imagen que permite búsquedas (Exacta).

**Imágenes con disminución de resolución:** Disminuye el número de píxeles en las imágenes en color, en escala de grises y monocromas. La disminución de resolución de imágenes escaneadas se realiza una vez completado el OCR. El valor predeterminado es El más bajo (600 ppp). Esta opción no está disponible si establece el estilo de salida de PDF en Imagen que se puede buscar (Exacto).

1. Rellene la información necesaria en estas secciones:

[Importar y exportar archivos de configuración del generador de PDF](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Configuración de exportación de Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

[Configuración de HTML a PDF](#html-to-pdf-settings)

[Flash de vídeos en la configuración de PDF](#flash-videos-to-pdf-settings)

[Configuración de XPS a PDF](#xps-to-pdf-settings)

[Configuración del optimizador de PDF](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Configuración de Microsoft Excel (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Configuración de Microsoft PowerPoint (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Configuración del proyecto de Microsoft (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Configuración de Microsoft Word (sólo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Configuración de Microsoft Visio (sólo Windows)](#visio)

[Configuración de Microsoft Publisher (sólo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[Configuración de AutoCAD (sólo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[Configuración de OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[Configuración de otras aplicaciones (sólo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Para ir a otra sección, haga clic en su vínculo en la página web o use los botones **[!UICONTROL Siguiente]** o **[!UICONTROL Anterior]**.

1. Después de completar todas las secciones, haz clic en **[!UICONTROL Guardar]** o **[!UICONTROL Guardar como]** y proporciona un nombre para la configuración.

Se puede personalizar la compatibilidad con varios tipos de archivo.

## Cambiar la configuración predeterminada {#change-the-default-settings}

Puede cambiar el valor predeterminado de la configuración de Adobe PDF, la configuración de seguridad y la configuración de tipo de archivo que se aplican a los orígenes recién creados. Cambiar los valores predeterminados no afecta a la configuración de los orígenes existentes.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > PDF Generator]**.
1. En la página **[!UICONTROL Configuración de Adobe PDF]**, **[!UICONTROL Configuración de tipo de archivo]** o **[!UICONTROL Configuración de seguridad]**, haga clic en **[!UICONTROL Establecer configuración predeterminada]**.
1. Seleccione la configuración predeterminada que prefiera. En la página Establecer configuración predeterminada están disponibles una o varias de las opciones siguientes:

   **[!UICONTROL Configuración de Adobe PDF]**: El valor predeterminado original es Estándar (Acrobat 6).

   **[!UICONTROL Configuración de seguridad]**: el valor predeterminado original es Sin seguridad (Acrobat 5).

   **[!UICONTROL Configuración de tipo de archivo]**: el valor predeterminado original es Estándar.

1. Haga clic en **[!UICONTROL Guardar]**.

## Eliminar una configuración de tipo de archivo {#delete-a-file-type-setting}

Puede eliminar una configuración de tipo de archivo que ya no se utilice.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > PDF Generator> Configuración de tipo de archivo]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias fuentes. La configuración que no tiene una casilla de verificación junto a ella siempre se incluye con PDF Generator y no se puede eliminar.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página Confirmación de eliminación, haga clic en **[!UICONTROL Eliminar]**.

## Configuración de imagen a PDF {#image-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos de imagen a PDF. Para obtener instrucciones sobre cómo obtener acceso a esta configuración, consulte [Crear o editar la configuración de tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:** Lista separada por comas de las extensiones de nombre de archivo que se pueden convertir.

**Pruebe el convertidor de reserva:** PDF Generator puede usar Java™ o Acrobat para convertir archivos de imagen a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión utilizando el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

>[!NOTE]
>
>Los archivos de JPEG 2000 sólo se pueden convertir con Acrobat.

**Usar OCR:** Especifica si se debe aplicar OCR (reconocimiento óptico de caracteres) a PDF. El software OCR le permite buscar, corregir y copiar el texto en PDF.

***nota **: La característica PDF de OCR (PDF en el que se pueden realizar búsquedas) solo es compatible con Microsoft Windows.*

**Idioma principal de OCR:** Especifica el idioma que el motor de OCR utilizará para identificar los caracteres.

**Estilo de salida de PDF:** Determina el tipo de PDF que se va a producir. Todos los formatos aplican OCR y reconocimiento de fuentes y páginas a las imágenes de texto y las convierten en texto normal.

**Imagen que permite búsquedas:** Garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original, la recorta según sea necesario y coloca una capa de texto invisible sobre ella. La opción Reducir resolución de imágenes determina si la imagen se reduce de resolución y hasta qué punto.

**Imagen que permite búsquedas (exacta):** Garantiza que el texto se pueda buscar y seleccionar. Esta opción mantiene la imagen original y coloca una capa de texto invisible sobre ella. Recomendado para casos que requieren la máxima fidelidad a la imagen original.

**ClearScan:** Sintetiza una nueva fuente Type 3 que se aproxima mucho al original y conserva el fondo de la página mediante una copia de baja resolución.

**Imágenes de disminución de resolución:** Disminuye el número de píxeles en color, escala de grises e imágenes monocromas una vez completado el OCR. Elija el grado de disminución de resolución que desea aplicar. Las opciones con números más altos reducen la disminución de resolución, lo que produce PDF de mayor resolución.

## Configuración de exportación de Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

La configuración Tipo de archivo de exportación de la sección Configuración de exportación de Adobe PDF se utiliza para convertir un archivo PDF a otro formato. El valor predeterminado es HTML 4.01 con hojas de estilos en cascada (CSS) 1.0 (*.htm, *.html).

Para obtener instrucciones sobre cómo obtener acceso a esta configuración, consulte [Crear o editar la configuración de tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Configuración de HTML a PDF {#html-to-pdf-settings}

Las siguientes opciones determinan cómo se convierten los archivos de HTML en PDF. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Pruebe el convertidor de reserva:** PDF Generator puede usar Java™ o Acrobat para convertir archivos de HTML a PDF. Cuando se selecciona esta opción y una conversión falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión utilizando el método alternativo. Si el método alternativo falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Codificación predeterminada:** Establece la codificación de entrada del texto del archivo desde un menú de sistemas operativos y alfabetos. Utiliza la selección que se muestra en la opción Codificación predeterminada sólo si el archivo de origen de HTML no especifica ningún tipo de codificación.

**Forzar codificación seleccionada:** Omite cualquier codificación especificada en el archivo de origen de HTML y utiliza la selección mostrada en la opción Codificación predeterminada.

### Configuración de Spidering {#spidering-settings}

*Spidering* explora las páginas web en busca de vínculos a otras páginas web. Cuando se encuentra un vínculo a otra página web, se busca la página de destino y se incluye en el documento de PDF que se genera. Active estas opciones para establecer el número de niveles que se recuperarán y convertirán en PDF:

**Obtener solo niveles X:** arañas y convierte páginas hasta una profundidad del nivel especificado desde la dirección URL de la página base. El valor 1 solo convierte la dirección URL proporcionada.

**Obtener sitio completo:** Convierte todo el sitio, a partir de la dirección URL proporcionada.

**Permanecer en la misma ruta:** Los vínculos que apunten a páginas que no se encuentren en la misma ruta relativa que la dirección URL base no se convertirán durante la propagación.

**Permanecer en el mismo servidor:** Los vínculos que apunten a páginas de distintos servidores no se convierten durante la propagación. Solo se convierten los vínculos que apuntan al mismo servidor que la dirección URL especificada.

### Configuración de conversión de página {#page-conversion-settings}

Active estas opciones para especificar cómo se convierten las páginas de HTML. En función del tamaño de página, los valores de anchura, altura y margen se ajustan en consecuencia.

**Tamaño de página:** Elija personalizado y especifique el ancho y el alto, o seleccione dimensiones predefinidas.

**Orientación:** Seleccione vertical u horizontal para el documento de PDF convertido.

**Márgenes:** Especifica los márgenes (superior, inferior, izquierdo y derecho) del documento de PDF generado.

**Agregar marcadores a PDF:** Agrega marcadores al documento de PDF.

**Habilitar PDF etiquetado:** incrusta etiquetas en el documento de PDF.

**Establecer configuración de vista inicial:** Permite configurar opciones de documento, opciones de ventana y opciones de interfaz de usuario. Esta configuración determina cómo se muestra inicialmente el contenido.

### Opciones de documento {#document-options}

Habilite estas opciones para especificar cómo mostrar el contenido, cómo mostrar las páginas en el documento de PDF y cómo especificar el nivel de ampliación:

**Mostrar:** Seleccione los paneles que se abrirán en Acrobat cuando se abra el documento de PDF.

**Diseño de página:** Seleccione el tipo de diseño de página para el documento de PDF.

**Ampliación:** Elija la ampliación preestablecida para la vista inicial del documento de PDF o seleccione un valor personalizado. Si se elige una configuración predeterminada, se utilizará la ampliación de Acrobat predeterminada.

**Abrir a número de página:** Especifique el número de página al que se abre PDF.

### Opciones de ventana {#window-options}

Active estas opciones para especificar el tamaño y la visualización de la ventana.

**Cambiar tamaño de la ventana a la página inicial:** cambia el tamaño de la ventana de Acrobat al tamaño de la página inicial.

**Centrar ventana en pantalla:** Abre la ventana en el centro de la pantalla.

**Abrir en modo de pantalla completa:** Abre la ventana en modo de pantalla completa.

**Mostrar:** Muestra el título o el nombre de archivo del documento en la ventana.

### Opciones de interfaz de usuario {#user-interface-options}

Active estas opciones para especificar el aspecto de la ventana:

**Ocultar barra de menús:** Oculta la barra de menús del documento de PDF.

**Ocultar barras de herramientas:** Oculta las barras de herramientas del documento de PDF.

**Ocultar controles de ventana:** oculta los controles de ventana en el documento de PDF.

## Flash de vídeos en la configuración de PDF {#flash-videos-to-pdf-settings}

PDF Generator admite la capacidad de enviar un vídeo para Adobe Flash (archivo SWF o FLV) y crear un archivo PDF con un vídeo para Adobe Flash incrustado en él. Esta conversión no requiere que Adobe Flash Player esté instalado en el servidor de Forms. Para obtener instrucciones sobre cómo obtener acceso a esta opción, vea [Crear o editar la configuración de tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensiones de nombre de archivo:** Lista separada por comas de las extensiones de nombre de archivo que se pueden convertir.

## Configuración de XPS a PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) se utiliza en la máquina de impresión de Windows. Este es un formato de Microsoft y se puede crear desde cualquier aplicación de Microsoft Office. Los formularios AEM permiten convertir archivos XPS a PDF.

**Extensiones de nombre de archivo:** Lista separada por comas de todas las extensiones de nombre de archivo XPS que se pueden convertir. Actualmente hay un formato: .xps.

## Configuración del optimizador de PDF {#pdf-optimizer-settings}

PDF Generator admite la capacidad de reducir el tamaño de los archivos PDF. El uso de todos estos ajustes o sólo unos pocos depende de cómo se van a utilizar los archivos y de las propiedades esenciales que debe tener un archivo. En la mayoría de los casos, los ajustes predeterminados son adecuados para lograr la máxima eficacia: se ahorra espacio al eliminar fuentes incrustadas, comprimir imágenes y eliminar elementos de los archivos que ya no son necesarios.

>[!NOTE]
>
>Al optimizar un documento firmado digitalmente, se eliminan y se invalidan las firmas digitales.

Para obtener instrucciones sobre cómo obtener acceso a esta configuración, consulte [Crear o editar la configuración de tipo de archivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versión de PDF de destino:** Especifica la versión de Acrobat con la que PDF es compatible.

### Fuentes {#fonts}

1. Seleccionar **fuentes.**
1. Seleccione una de las siguientes opciones:

   **Desincrustar todas las fuentes:** Desincrusta todas las fuentes incrustadas.

   **No desincrustar ninguna fuente:** No desincrusta ninguna fuente.

   **Desincrustar algunas fuentes:** Desincrusta solo las fuentes especificadas. Siga estos pasos para especificar las fuentes que desea desincrustar:

   * Si es necesario, seleccione un directorio de fuentes diferente en el menú desplegable **Fuente**. Este menú desplegable enumera los directorios de fuentes especificados en **Inicio > Configuración > Sistema principal > Configuraciones principales**.
   * Seleccione una o más fuentes de la lista **Fuentes disponibles** y haga clic en **Agregar**. Estas fuentes se agregaron a la lista **Fuentes para desincrustar**.
   * Si desea desincrustar algunas fuentes que no existen en el servidor de Forms, escriba los nombres de esas fuentes en el cuadro **Agregar fuentes a desincrustar**. Haga clic en **Agregar**.

   >[!NOTE]
   >
   >*Si desea desincrustar algunas fuentes cuyos subconjuntos están incrustados en el documento, agregue como prefijo el nombre de la fuente con el signo +. Por ejemplo, &quot;+Helvetica&quot;.*

1. Si desea incrustar sólo los subconjuntos en uso de las fuentes incrustadas, seleccione **Subestablecer todas las fuentes incrustadas**.

   >[!NOTE]
   >
   >*Si está usando esta opción en combinación con **Desincrustar algunas fuentes**, las fuentes de la lista **Agregar fuentes a la incrustación**aún están completamente desincrustadas.*

   >[!NOTE]
   >
   >*El subconjunto de fuentes es la técnica para incrustar sólo una parte de una fuente. Un subconjunto de fuentes contiene sólo los caracteres utilizados en el documento.*

### Transparencia {#transparency}

Si el documento de PDF incluye ilustraciones que contienen transparencias, puede utilizar la configuración de PDF Optimizer para acoplar las transparencias y reducir el tamaño del archivo.

>[!NOTE]
>
>Si Acrobat 4.0 y posterior está seleccionado como la versión de Target PDF, todos los objetos transparentes se acoplan. Para otras versiones de Target PDF, se admite la transparencia y se puede configurar la configuración de transparencia.

Seleccione **Transparencia** para establecer la configuración de transparencia mientras se optimizan los documentos de PDF.

**Nivel de transparencia** Especifica la cantidad de información vectorial que se conservará. Los valores más altos conservan más objetos vectoriales, mientras que los valores más bajos rasterizan más objetos vectoriales; los valores intermedios conservan las áreas simples en forma vectorial y rasterizan las complejas. Seleccione la configuración más baja para rasterizar todas las ilustraciones.

>[!NOTE]
>
>La cantidad de rasterización que se produce depende de la complejidad de la página y de los tipos de objetos superpuestos.

**Texto e imagen en línea** Resolución a la que se rasterizan todos los objetos, incluidas imágenes, ilustraciones vectoriales, texto y degradados. Los valores admitidos son de 1 píxel por pulgada (ppp) a 9600 ppp.

>[!NOTE]
>
>La resolución de texto y arte de líneas debe establecerse generalmente a 600-1200 ppp para proporcionar una rasterización de alta calidad, especialmente en serif o tipo pequeño de tamaño puntual.

**Degradado y mallas** Resolución a la que se rasterizan el degradado y las mallas. Los valores admitidos son de 1 ppp a 1200 ppp.

>[!NOTE]
>
>La resolución de degradado y malla debe establecerse generalmente a 150-300 ppp porque la calidad de los degradados, las sombras paralelas y las plumas no mejoran con resoluciones más altas, pero el tiempo de impresión y el tamaño del archivo aumentan.

**Convertir todo el texto en contornos** Convierte todos los objetos de tipo (tipo de punto, tipo de área y tipo de ruta) en contornos y descarta toda la información de pictogramas de tipo en las páginas que contienen transparencias. Esta opción garantiza que la anchura del texto se mantenga constante durante el acoplamiento. Tenga en cuenta que si activa esta opción, las fuentes pequeñas aparecerán con un grosor ligeramente mayor cuando se visualicen en Acrobat o se impriman en impresoras de escritorio de baja resolución. No afecta a la calidad del tipo impreso en impresoras o filmadoras de alta resolución.

**Convertir todos los trazos en contornos** Convierte todos los trazos en rutas rellenas simples en páginas que contienen transparencia. Esta opción garantiza que la anchura de los trazos se mantenga constante durante el acoplamiento. Tenga en cuenta que, si activa esta opción, los trazos finos aparecerán un poco más gruesos y podrían degradar el rendimiento de acoplamiento.

**Áreas complejas de clip** Garantiza que los límites entre las ilustraciones vectoriales y las ilustraciones rasterizadas caen a lo largo de las rutas de objetos. Esta opción reduce los artefactos de vinculación resultantes de formar parte de un registro

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Algunos controladores de impresión procesan las tramas y las ilustraciones vectoriales de forma diferente, lo que a veces da como resultado la vinculación de color. Es posible que pueda minimizar los problemas de vinculación deshabilitando algunos ajustes de administración de color específicos del controlador de impresión. Estos ajustes varían con cada impresora, así que consulte la documentación incluida con la impresora para obtener más detalles.

Conservar sobreimpresión: fusiona el color de la ilustración transparente con el color de fondo para crear un efecto de sobreimpresión.

En la tabla siguiente se muestran los tipos comunes de impresoras y su resolución medida en ppp, su resolución de pantalla predeterminada medida en líneas por pulgada (lpp) y una resolución de remuestreo para imágenes medidas en píxeles por pulgada (ppi). Por ejemplo, si estuviera imprimiendo en una impresora láser de 600 ppp, escribiría 170 para la resolución con la que volver a muestrear las imágenes.

**Imágenes** Seleccione Imágenes para especificar las opciones de compresión y remuestreo de las imágenes monocromas, en escala de grises y en color. Es posible que desee experimentar con estas opciones para encontrar un equilibrio adecuado entre el tamaño del archivo y la calidad de la imagen. La configuración de resolución para las imágenes en color y escala de grises debe ser de 1,5 a 2 veces la regla de pantalla de línea en la que se imprimirá el archivo. La resolución de las imágenes monocromas debe ser la misma que la del dispositivo de salida, pero si guarda una imagen monocroma con una resolución superior a 1500 ppp, el tamaño del archivo aumenta sin mejorar de forma notable la calidad de la imagen. Las imágenes que se ampliarán, como los mapas, pueden requerir resoluciones más altas.

>[!NOTE]
>
>El remuestreo de imágenes monocromas puede dar lugar a resultados de visualización inesperados, como la ausencia de visualización de imágenes. Si esto sucede, desactive el remuestreo y vuelva a convertir el archivo. Es muy probable que este problema se produzca con el submuestreo y, menos probablemente, con la disminución de resolución bicúbica.

<table>
 <tbody>
  <tr>
   <th><p><strong>Resolución de impresora</strong></p> </th>
   <th><p><strong>Pantalla de línea predeterminada</strong></p> </th>
   <th><p><strong>Resolución de imagen</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 ppp (impresora láser)</p> </td>
   <td><p>60 lpp</p> </td>
   <td><p>120 ppp</p> </td>
  </tr>
  <tr>
   <td><p>600 ppp (impresora láser)</p> </td>
   <td><p>85 lpp</p> </td>
   <td><p>170 ppp</p> </td>
  </tr>
  <tr>
   <td><p>1200 ppp (filmadora)</p> </td>
   <td><p>120 lpp</p> </td>
   <td><p>240 ppp</p> </td>
  </tr>
  <tr>
   <td><p>2.400 ppp (filmadora)</p> </td>
   <td><p>150 lpp</p> </td>
   <td><p>300 ppp</p> </td>
  </tr>
 </tbody>
</table>

#### Descartar objetos {#discard-objects}

* Seleccione **Descartar objetos** para especificar los objetos que desea quitar de PDF y optimizar las líneas curvas en los dibujos CAD.
* **Descartar todas las acciones de envío, importación y restablecimiento de formularios**: deshabilita todas las acciones relacionadas con el envío o la importación de datos de formularios y restablece los campos de formulario. Esta opción conserva los objetos de formulario a los que están vinculadas las acciones.
* **Descartar todas las acciones de JavaScript**: quita de PDF todas las acciones que usan JavaScript.
* **Descartar miniaturas de página incrustadas**: quita las miniaturas de página incrustadas. Esta opción es útil para documentos grandes, que pueden tardar mucho tiempo en dibujar miniaturas de página después de hacer clic en el botón Páginas.
* **Convertir líneas suavizadas en curvas**: reduce el número de puntos de control utilizados para crear curvas en dibujos CAD, lo que da como resultado archivos PDF más pequeños y una representación en pantalla más rápida.
* **Descartar configuración de impresión incrustada**: quita del documento la configuración de impresión incrustada, como el escalado de página y el modo dúplex.
* **Descartar marcadores**: quita todos los marcadores del documento.
* **Acoplar campos de formulario**: hace que los campos de formulario no se puedan utilizar sin cambiar su apariencia. Los datos del formulario se combinan con la página para convertirse en contenido de página.
* **Descartar todas las imágenes alternativas**: quita todas las versiones de una imagen excepto la versión destinada a la visualización en pantalla. Algunos PDF incluyen varias versiones de la misma imagen para diferentes fines, como la visualización en pantalla de baja resolución y la impresión de alta resolución.
* **Descartar etiquetas de documento**: quita etiquetas del documento, lo que también quita la accesibilidad y las capacidades de reflujo del texto.
* **Detectar y combinar fragmentos de imagen**: busca imágenes o máscaras fragmentadas en sectores finos e intenta combinar los sectores en una sola imagen o máscara.
* **Descartar índice de búsqueda incrustada**: quita los índices de búsqueda incrustados, lo que reduce el tamaño del archivo.

#### Descartar datos de usuario {#discard-user-data}

Seleccione **Descartar datos de usuario** para quitar la información personal que no desee distribuir o compartir con otros usuarios.

* **Descartar todos los comentarios, Forms y multimedia**: quita todos los comentarios, formularios, campos de formulario y multimedia de PDF.
* **Descartar todos los datos de objeto**: quita todos los objetos de PDF.
* **Descartar referencias cruzadas externas**: quita los vínculos a otros documentos. Los vínculos que saltan a otras ubicaciones dentro de PDF no se eliminan.
* **Descartar Contenido De Capas Ocultas Y Acoplar Capas Visibles**: Reduce El Tamaño Del Archivo. El documento optimizado se parece al PDF original, pero no contiene información de capas.
* **Descartar información y metadatos de documentos**: quita información del diccionario de información de documentos y de todas las secuencias de metadatos. (Utilice el comando Guardar como para restaurar las secuencias de metadatos en una copia de PDF).
* **Descartar archivos adjuntos**: quita todos los archivos adjuntos, incluidos los adjuntos agregados a PDF como comentarios. (PDF Optimizer no optimiza los archivos adjuntos).
* **Descartar datos privados de otras aplicaciones**: quita información de un documento de PDF que sólo es útil para la aplicación que creó el documento. Esta configuración no afecta a la funcionalidad de PDF, pero reduce el tamaño del archivo.

### Limpiar {#clean-up}

Seleccione **Limpiar** para eliminar los elementos innecesarios del documento.
Estos elementos incluyen elementos obsoletos o innecesarios para el uso previsto del documento. La eliminación de ciertos elementos puede afectar gravemente a la funcionalidad de PDF. De forma predeterminada, solo se seleccionan los elementos que no afectan a la funcionalidad. Si no está seguro de las implicaciones de eliminar otras opciones, utilice las selecciones predeterminadas.

**Compresión**

Seleccione una de las siguientes opciones de compresión Flotante en el menú desplegable:

* Comprimir todo el archivo
* Comprimir la estructura del documento
* Eliminar compresión
* Dejar la compresión intacta

**Usar Flate para codificar flujos que no están codificados**: Aplica la compresión Flate a todos los flujos que no están codificados.

**Descartar marcadores no válidos**: quita los marcadores que apuntan a páginas del documento que se han eliminado.

**Descartar destinos con nombre sin referencia**: quita los destinos con nombre a los que no se hace referencia internamente desde el documento de PDF. Esta opción no comprueba la existencia de vínculos de otros archivos o sitios web de PDF.

**Optimizar PDF para la vista rápida en la web**: Reestructura un documento de PDF para la descarga página a página (servicio de bytes) desde servidores web.

**En los flujos que usan codificación LZW, use Flate en su lugar**: aplica compresión Flate a todos los flujos de contenido e imágenes que usan codificación LZW.

**Descartar vínculos no válidos**: quita los vínculos que saltan a destinos no válidos.

**Optimizar contenido de la página**: Convierte todos los caracteres de fin de línea en caracteres de espacio, lo que mejora la compresión Flate.

## Configuración de Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Excel. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](#create-or-edit-file-type-settings).

**Intentar OpenOffice como convertidor de reserva**: cuando se selecciona esta opción y una conversión que utiliza Microsoft Excel falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones de nombre de archivo**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `xls,xlsx`. No incluya un punto antes o un espacio entre las extensiones.

**Crear archivo compatible con PDF/A-1a**: Fuerza el uso de la configuración de PDF/A-1b:2005 RGB Adobe PDF.

**Agregar marcadores a Adobe PDF**: Convierte los nombres de las hojas de cálculo de Excel en marcadores. Esta opción está seleccionada de forma predeterminada.

**Ajustar hoja de cálculo a una sola página**: reduce el tamaño del texto para que quepa en una sola página.

**Convertir libro completo**: convierte todas las hojas de cálculo del archivo de Excel. Si esta opción no está seleccionada, solo se convierte la página actual.

**Ejecutar macros automáticamente**: ejecuta todas las macros del documento de Excel (por ejemplo, una macro que inserte la hora actual) antes de convertir el documento.

**Convertir información de documento**: agrega propiedades de documento de PDF basadas en la información de documento del archivo de origen. Incluye información como el título del documento, el autor, el asunto y las palabras clave.

**Agregar vínculos a Adobe PDF**: convierte los hipervínculos del archivo de origen en hipervínculos del documento de PDF.

**Adjuntar archivo de Source a Adobe PDF**: cuando se selecciona esta opción, la hoja de cálculo original de Excel se inserta como un archivo adjunto dentro del documento de PDF generado.

**Habilitar accesibilidad y reflujo con Adobe PDF etiquetado**: incrusta etiquetas en el documento de PDF para habilitar la accesibilidad y el reflujo.

**Lista de complementos de Excel para cargar**: de forma predeterminada (por motivos de seguridad), no se ejecutan complementos de Excel cuando se convierte un archivo de Excel a PDF. Para permitir que determinados complementos de Excel se ejecuten durante la conversión, proporcione una lista separada por comas de los nombres de los complementos.

**Lista de hojas de cálculo para convertir**: cuando este cuadro está vacío, todas las hojas de cálculo de la hoja de cálculo de Excel se incluyen en el PDF generado. Para convertir selectivamente un subconjunto de las hojas de cálculo, proporcione una lista de nombres de hoja de cálculo separados por comas.

## Configuración de Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft PowerPoint. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Probar OpenOffice como conversor alternativo]**: cuando se selecciona esta opción y una conversión que utiliza Microsoft PowerPoint falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es ppt,pptx. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información del documento]**: agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluidos título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar marcadores a Adobe PDF]**: Convierte los títulos de PowerPoint en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de Source a Adobe PDF]**: agrega el archivo de origen al archivo de PDF como datos adjuntos. Esta opción no está seleccionada de forma predeterminada.

**[!UICONTROL Habilitar Accesibilidad Y Reflujo Con Etiquetas Adobe PDF]**: Incrusta Etiquetas En El Archivo PDF. Esta opción no está seleccionada de forma predeterminada.

**[!UICONTROL Convertir multimedia a multimedia PDF]**: convierte multimedia a multimedia PDF, siempre que sea posible. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Convertir notas del orador]**: Convierte las notas del orador a PDF.

**[!UICONTROL Ejecutar macros automáticamente]**: ejecuta todas las macros del documento de PowerPoint (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Diseño de PDF basado en la configuración de impresora de PowerPoint]**: utiliza la configuración de impresora de PowerPoint para diseñar el documento de PDF.

**[!UICONTROL Agregar vínculos a Adobe PDF]**: conserva los vínculos existentes cuando se convierte el archivo. El aspecto de los vínculos generalmente no cambia. Los vínculos solo se pueden crear si también está seleccionada la opción Habilitar accesibilidad. Esta opción no está seleccionada de forma predeterminada.

**[!UICONTROL Guardar Transiciones De Diapositivas En Adobe PDF]**: Convierte Las Transiciones De Diapositivas. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Guardar animaciones en Adobe PDF]**: guarda las animaciones convertidas en el archivo PDF.

**[!UICONTROL Convertir diapositivas ocultas en páginas de PDF]**: convierte las diapositivas ocultas.

**[!UICONTROL Crear archivo compatible con PDF/A-1a]**: Fuerza el uso de la configuración de PDF/A-1b:2005 RGB Adobe PDF. Algunas funciones de PowerPoint no se convierten al producir un archivo de PDF. Si una transición de PowerPoint no tiene una transición equivalente en Acrobat, se sustituye una transición similar. Si hay varios efectos de animación en la misma diapositiva, se utiliza un solo efecto. Las transiciones de página y los desplazamientos de viñetas se convierten.

## Configuración del proyecto de Microsoft (solo Windows) {#microsoft-project-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Project. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensiones de nombre de archivo:]** Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `mpp`. No incluya un punto antes o un espacio entre las extensiones.

1. **[!UICONTROL Convertir información del documento]**: agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluidos título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.
1. **[!UICONTROL Adjuntar archivo de Source a Adobe PDF]**: agrega el archivo de origen al archivo de PDF como datos adjuntos.
1. **[!UICONTROL Crear archivo compatible con PDF/A-1a]**: Fuerza el uso de la configuración de PDF/A-1b:2005 RGB Adobe PDF.
1. **[!UICONTROL Ejecutar macros automáticamente]**: ejecuta todas las macros del documento de Microsoft Project (como una macro que inserta la hora actual) antes de convertir el documento.

## Configuración de Microsoft Word (sólo Windows) {#microsoft-word-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Word. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Intentar OpenOffice como conversor alternativo]**: cuando se selecciona esta opción y una conversión con Microsoft Word falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante OpenOffice. Si la conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `doc,docx,rtf,txt`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información del documento]**: agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluidos título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar marcadores a Adobe PDF]**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Adjuntar archivo de Source a Adobe PDF]**: agrega el archivo de origen al archivo de PDF como datos adjuntos.

**[!UICONTROL Convertir referencias cruzadas y tablas de contenido en vínculos]**: Convierte todas las referencias cruzadas y las entradas de tabla de contenido en vínculos. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Habilitar Accesibilidad Y Reflujo Con Etiquetas Adobe PDF]**: Incrusta Etiquetas En El Archivo PDF. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Crear archivo compatible con PDF/A-1a]**: si se selecciona, se fuerza el uso de la configuración de PDF/A-1b:2005 RGB Adobe PDF.

**[!UICONTROL Ejecutar macros automáticamente]**: ejecuta todas las macros del documento de Word (como una macro que inserta la hora actual) antes de convertir el documento.

**[!UICONTROL Conservar marcado de documento en Adobe PDF]**: convierte el marcado del documento de Word en anotaciones en el archivo de PDF.

**[!UICONTROL Agregar vínculos a Adobe PDF]**: convierte los hipervínculos del archivo de origen en hipervínculos del documento de PDF.

**[!UICONTROL Convertir vínculos de notas al pie y notas al final]**: crea vínculos de las citas de notas al pie y notas al final a notas del documento de PDF.

**[!UICONTROL Convertir comentarios mostrados en notas en Adobe PDF]**: convierte los comentarios del documento de Word en notas de texto en el documento de PDF.

**[!UICONTROL Habilitar etiquetado avanzado]**: agrega etiquetas avanzadas para mejorar la accesibilidad.

**[!UICONTROL Convertir todos los estilos en marcadores]**: convierte todos los estilos del documento de Word en marcadores en el documento de PDF.

**[!UICONTROL Convertir estilos especificados en marcadores]**: convierte los estilos definidos en el campo **[!UICONTROL Estilos con niveles]** en marcadores en el documento de PDF.

**[!UICONTROL Estilos con niveles]**: especifica qué estilos del documento de Word se convierten en marcadores en el documento de PDF. También especifica el nivel de los marcadores. Para usar esta característica, anule la selección de la opción **[!UICONTROL Convertir todos los estilos en marcadores]** y especifique los nombres de estilo en el siguiente formato:

**styleName1=level1[,styleName2=level2...]**

Si un nombre de estilo de Microsoft Word incluye una coma (,) o un signo igual (=), anteponga a los caracteres especiales el carácter de escape (&quot;\_). Por ejemplo, especifique un estilo denominado &quot;Heading, 1&quot; como Heading\, 1.

**Codificación de Acrobat PDFMaker:** Especifica el tipo de codificación de los archivos de texto sin formato de entrada en Acrobat PDFMaker. Por ejemplo, si utiliza un archivo codificado en UTF-8, seleccione UTF-8 para obtener los mejores resultados.

## Configuración de Microsoft Visio (sólo Windows) {#visio}

**Convertir información del documento**: agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluidos título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada. Esta opción está habilitada de forma predeterminada.

**Agregar vínculos a Adobe PDF**: Conserva todos los vínculos. Esta opción está seleccionada de forma predeterminada.

**Agregar marcadores a Adobe PDF**: Convierte los encabezados en marcadores. Esta opción está seleccionada de forma predeterminada.

**Adjuntar archivo de Source a Adobe PDF**: agrega el archivo de origen al archivo de PDF como datos adjuntos.

**Acoplar siempre capas en Adobe PDF**: Acoplar todas las capas de Visio.

**Convertir todas las páginas**: convierte todas las páginas del archivo de Visio.

**Abrir el panel Capas cuando se ve en Adobe Acrobat**: Si las capas de Visio no están aplanadas, abre una ventana en la que puede especificar las capas que se conservan en el archivo de PDF al abrirlo con Acrobat. Esta opción está seleccionada de forma predeterminada.

**Crear archivo compatible con PDF/A-1b**: Fuerza el uso de la configuración de Adobe PDF PDF/A-1b:2005 (RGB).

**Convertir comentarios en comentarios de Adobe PDF**: Convierte las notas de Visio en comentarios de PDF.

## Configuración de Microsoft Publisher (sólo Windows) {#microsoft-publisher-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de Microsoft Publisher. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `pub`. No incluya un punto antes o un espacio entre las extensiones.

## Configuración de AutoCAD (sólo Windows) {#autocad-settings-windows-only}

Estas opciones determinan cómo se convierten los archivos de AutoCAD. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensiones de nombre de archivo]**: Especifica las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `dwg`. No incluya un punto antes o un espacio entre las extensiones.

**[!UICONTROL Convertir información del documento]**: agrega información del documento desde el cuadro de diálogo Propiedades del archivo de origen, incluidos título, asunto, autor, palabras clave, administrador, compañía, categoría y comentarios. Esta opción está seleccionada de forma predeterminada.

**[!UICONTROL Agregar marcadores a Adobe PDF]**: Convierte los encabezados en marcadores.

**[!UICONTROL Acoplar siempre capas en Adobe PDF]**: Acoplar todas las capas de AutoCAD.

**[!UICONTROL Abrir panel de capas cuando se ve en Adobe Acrobat]**: muestra la estructura de capas cuando se abre PDF en Acrobat.

**[!UICONTROL Convertir todos los diseños]**: incluye todos los diseños en PDF.

**[!UICONTROL Convertir espacio del modelo en 3D]**: cuando se selecciona, el diseño del espacio del modelo se convierte en una anotación 3D en PDF.

**[!UICONTROL Agregar vínculos a Adobe PDF]**: si está seleccionado, conserva todos los vínculos.

**[!UICONTROL Adjuntar archivo de Source a Adobe PDF]**: agrega el archivo de origen al archivo de PDF como datos adjuntos.

**[!UICONTROL Crear archivo compatible con PDF/A-1b]**: Fuerza el uso de la configuración de Adobe PDF de PDF/A-1b.

**[!UICONTROL Convertir todas las capas]**: De forma predeterminada, PDF Generator convierte sólo la capa predeterminada de archivos de AutoCAD a PDF en lugar de todas las capas del archivo. Seleccione esta opción para convertir todas las capas del archivo.

**[!UICONTROL Incrustar información de escala]**: conserva la información de escala de dibujo.

**[!UICONTROL Convertir diseño actual]**: incluye solo el diseño actual en PDF.

**[!UICONTROL Lista de diseños de AutoCAD que convertir]**: un dibujo de AutoCAD puede tener varios diseños. Cuando este cuadro está vacío, todos los diseños del dibujo de AutoCAD se incluyen en el documento de PDF generado. Para convertir selectivamente un subconjunto de los diseños, proporcione una lista de nombres de diseño separados por comas.

## Configuración de OpenOffice {#openoffice-settings}

Estas opciones determinan cómo se convierten los archivos de OpenOffice. Para obtener instrucciones sobre cómo obtener acceso a estas opciones, vea [Crear o editar la configuración de tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Probar PDFMaker como conversor de reserva**: cuando se selecciona esta opción y una conversión mediante OpenOffice falla o alcanza el límite de tiempo de espera especificado, PDF Generator intenta la conversión mediante PDFMaker. Si la conversión mediante PDFMaker falla o alcanza el límite de tiempo de espera especificado, se escribe una excepción en el archivo de registro.

**Extensiones de nombre de archivo**: especifique las extensiones de nombre de archivo para los tipos de archivo, separados por comas, que se aceptan en esta aplicación. El valor predeterminado es `odt,odp,ods,odg,odf,sxw,sxi,sxd`. No incluya un punto antes o un espacio entre las extensiones.

**Intervalo**: convierta todas las páginas o especifique páginas concretas o un intervalo de páginas. Si no se define un intervalo de páginas, se convierten todas las páginas. Para exportar un intervalo de páginas, utilice el formato 3-6. Para exportar páginas únicas, utilice el formato 7;9;11. Puede exportar una combinación de intervalos de páginas y páginas únicas utilizando un formato como 3-6;8;10;12.

**Orientación de página**: para archivos de texto sin formato solamente, seleccione vertical u horizontal para el documento de PDF convertido.

**Imágenes**: configure cómo se convierten las imágenes. Las imágenes de EPS con vistas previas incrustadas se exportan únicamente como vistas previas. Las imágenes de EPS sin vistas previas incrustadas se exportan como marcadores de posición vacíos. Con la compresión sin pérdidas de las imágenes, se conservan todos los píxeles. Con la compresión de imágenes de JPEG y un nivel de alta calidad, se conservan casi todos los píxeles. Con un nivel de baja calidad, se pierden algunos píxeles y se introducen artefactos, pero se reducen los tamaños de archivo.

**General**: Habilite las opciones para convertir un PDF etiquetado o para exportar notas de documentos de Writer y FormCalc, efectos de transición de diapositivas Impress o páginas en blanco a PDF. Cuando se exportan las etiquetas, el tamaño del archivo puede aumentar en grandes cantidades. Algunas etiquetas exportadas son tablas de contenido, hipervínculos y controles.

También puede especificar cómo se envían los formularios. Las opciones son XML, FDF, PDF o HTML. Esta configuración anula la propiedad URL del control que se establece en el documento. Solo se puede seleccionar una configuración común para el documento de PDF:

* PDF (envía todo el documento)
* FDF (envía el contenido del control)
* HTML
* XML

**PDF etiquetado**: permite crear PDF etiquetado a partir de documentos de OpenOffice. El PDF etiquetado contiene información sobre la estructura del contenido del documento. Esto puede resultar útil cuando se muestra el documento en dispositivos con distintas pantallas y cuando se utiliza software de lector de pantalla. También ayuda al software de accesibilidad a realizar varias operaciones útiles con el documento de PDF, como leer en voz alta el contenido del documento de PDF.

**Exportar notas**: convierte las notas de los documentos de OpenOffice en notas del documento de PDF generado.

**Usar efectos de transición**: Convierte los efectos de transición de diapositivas de las presentaciones de OpenOffice en los efectos de transición de PDF correspondientes.

**Enviar Forms en formato**: crea un formulario de PDF que el usuario del documento de PDF puede rellenar e imprimir.

**Exportar páginas en blanco insertadas automáticamente**: cuando se selecciona esta opción, las páginas en blanco insertadas automáticamente se incluyen en el documento de PDF generado. Esto resulta útil si imprime un documento de PDF a doble cara. Por ejemplo, se puede configurar un libro para que la primera página del capítulo empiece siempre en una página impar. Si el capítulo anterior termina en una página impar, OpenOffice inserta una página par en blanco. Esta opción controla si se debe incluir esa página par en el PDF generado.

## Otra configuración de la aplicación (sólo Windows) {#other-applications-settings-windows-only}

No puede cambiar la configuración de otras aplicaciones a través de la consola de administración; en ellas se muestran las extensiones de nombre de archivo de los tipos de archivo admitidos. Para obtener instrucciones sobre cómo obtener acceso a esta configuración, consulte [Crear o editar la configuración de tipo de archivo](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker de Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Es posible que sea necesario personalizar la compatibilidad con estos tipos de archivos. Para obtener más información, vea &quot;Agregar compatibilidad con formatos de archivo nativos adicionales&quot; en [Programar con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Para obtener ayuda sobre cómo configurar una impresora de red PDFG, consulte [Configuración de una impresora de red PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
