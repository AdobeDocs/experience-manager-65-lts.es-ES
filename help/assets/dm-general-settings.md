---
title: Configuración general de Dynamic Media
description: Obtenga información sobre cómo administrar la configuración general en Dynamic Media. Puede establecer el nombre del servidor de publicación y del servidor de origen aquí y establecer una opción de sobrescritura de imagen. También hay opciones de carga predeterminadas para el enmascaramiento de enfoque de imágenes y opciones de carga para cómo desea procesar los archivos de PostScript, Adobe Photoshop, PDF y Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# Configuración general de Dynamic Media

La configuración de **[!UICONTROL Configuración general de Dynamic Media]** solo está disponible si:

* Está ejecutando Dynamic Media en modo Scene7. Consulte [Habilitar Dynamic Media en modo Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Tiene una *configuración de Dynamic Media* **[!UICONTROL existente]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager 6.5.11 o superior. Consulte [Crear una configuración de Dynamic Media en Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Es administrador del sistema de Experience Manager con privilegios de administrador.

La Configuración general de Dynamic Media está pensada para que la utilicen programadores y desarrolladores de sitios web con experiencia. Adobe Dynamic Media recomienda que los usuarios que cambien esta configuración de publicación estén familiarizados con Dynamic Media en Adobe Experience Manager y con la tecnología básica de creación de imágenes.

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados para su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas de URL son específicas de su cuenta de.

La página Configuración de publicación de Dynamic Media establece la configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor de Adobe Dynamic Media envía un recurso según una configuración predeterminada que se configuró en la página Configuración de publicación de Dynamic Media.

Consulte también [Opcional: configuración de Dynamic Media: configuración del modo Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) para ver más tareas de configuración opcionales.

>[!NOTE]
>
>¿Desea actualizar de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager? La página Configuración general y la página [Configuración de publicación](/help/assets/dm-publish-settings.md) de Dynamic Media se han rellenado previamente con los valores tomados de su cuenta de Dynamic Media Classic. Las excepciones son todos los valores enumerados en el área **[!UICONTROL Opciones de carga predeterminadas]** de la página Configuración general. Estos valores ya están en Experience Manager. Como tal, cualquier cambio que realice en **[!UICONTROL Opciones de carga predeterminadas]** en cualquiera de las cinco pestañas, a través de la interfaz de usuario de Experience Manager, se reflejará en Dynamic Media, no en Dynamic Media Classic. El resto de la configuración y los valores de la página Configuración general y la página [Configuración de publicación](/help/assets/dm-publish-settings.md) se mantienen entre Dynamic Media Classic y Dynamic Media en Experience Manager.

**Para establecer la configuración general de Dynamic Media:**

1. En el modo Autor de Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En la página Servidor, establezca **[!UICONTROL Nombre del servidor publicado]** y **[!UICONTROL Nombre del servidor de origen]** y, a continuación, utilice las cinco pestañas para configurar las opciones de carga predeterminadas de edición de imágenes y de los archivos Postscript, Photoshop, PDF y Illustrator.

   * [Servidor](#server-general-setting)
   * [Cargar a la aplicación](#upload-to-application)
   * Pestaña [Edición de imágenes](#image-editing-tab)
   * Ficha [PostScript](#postscript-tab)
   * Ficha [Photoshop](#photoshop-tab)
   * Ficha [PDF](#pdf-tab)
   * Ficha [Illustrator](#illustrator-tab)

   ![Página de configuración general de Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *Página de configuración general de Dynamic Media, con la ficha **[!UICONTROL Edición de imágenes]**&#x200B;seleccionada.*<br><br>

1. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

## Servidor {#server-general-setting}

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados para su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas de URL son específicas de su cuenta de.

| Opción | Descripción |
| --- | --- |
| **[!UICONTROL Nombre de servidor publicado]** | Requerido.<br>El nombre debe usar `https://` en la ruta.<br>Este servidor es el servidor CDN (red de distribución de contenido) activo que se usa en todas las llamadas URL generadas por el sistema que son específicas de su cuenta. No cambie este nombre de servidor a menos que el soporte técnico de Adobe se lo indique. |
| **[!UICONTROL Nombre del servidor de origen]** | Requerido.<br>Este servidor se usa solamente para las pruebas de control de calidad. No cambie este nombre de servidor a menos que el soporte técnico de Adobe se lo indique. |

## Cargar a la aplicación {#upload-to-application}

* **[!UICONTROL Sobrescribir imágenes]**

  Adobe Dynamic Media no permite que dos archivos tengan el mismo nombre. El ID de Dynamic Media de Adobe de cada elemento (el nombre de imagen menos la extensión del nombre de archivo) debe ser único. Debido a esta regla, **[!UICONTROL la carga en la aplicación]** se ha sobrescrito. El efecto exacto de esta opción depende de la opción Sobrescribir imágenes especificada que haya elegido. Estas opciones especifican cómo se cargan las imágenes de reemplazo: si reemplazan las imágenes originales o se convierten en imágenes duplicadas. Se cambió el nombre de las imágenes duplicadas por `-1`. Por ejemplo, `chair.tif` cambió el nombre a `chair-1.tif`. Estas opciones afectan a las imágenes cargadas en una carpeta diferente a la original o a las imágenes con una extensión de nombre de archivo diferente a la original, como JPG, TIF o PNG.

  >[!NOTE]
  >
  >Para mantener la coherencia con Experience Manager, seleccione la opción Sobrescribir imágenes **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]**.

  | Sobrescribir imágenes, opción | Descripción |
  | --- | --- |
  | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]** | *Predeterminado* solo para las nuevas cuentas de Dynamic Media.<br>Esta opción es la regla más estricta para el reemplazo. Requiere que cargue la imagen de reemplazo en la misma carpeta que el original y que la imagen de reemplazo tenga la misma extensión de nombre de archivo que el original. Si no se cumplen estos requisitos, se crea un duplicado.<br>*Para mantener la coherencia con Experience Manager, seleccione esta opción*. |
  | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre de base independientemente de la extensión]** | Requiere que cargue la imagen de reemplazo en la misma carpeta que el original, aunque la extensión del nombre del archivo puede ser diferente del original. Por ejemplo, chair.tif reemplaza chair.jpg. |
  | **[!UICONTROL Sobrescribir en cualquier carpeta con mismo nombre y extensión de recurso base]** | Requiere que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la imagen original (por ejemplo, chair.jpg debe reemplazar chair.jpg, no chair.tif). Sin embargo, puede cargar la imagen de sustitución en una carpeta diferente a la original. La imagen actualizada reside en la nueva carpeta; el archivo ya no se puede encontrar en su ubicación original. |
  | **[!UICONTROL Sobrescribir en cualquier carpeta, mismo nombre de recurso base independientemente de la extensión]** | Esta opción es la regla de reemplazo más inclusiva. Puede cargar una imagen de reemplazo en una carpeta diferente a la original, cargar un archivo con una extensión de nombre de archivo diferente y reemplazar el archivo original. Si el archivo original está en una carpeta diferente, la imagen de reemplazo reside en la nueva carpeta a la que se cargó. |

* **[!UICONTROL Conservar recorte]**

  Controla la conservación de cualquier definición de recorte manual existente.

  Consulte también `preserveCrop` en [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) y [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambos en la Guía de referencia de visores de Dynamic Media.

## Opciones de carga predeterminadas {#default-upload-options}

### Pestaña Edición de imágenes {#image-editing-tab}

Este filtro le permite ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Ayuda a controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora.

El efecto Máscara de enfoque utiliza las mismas opciones que el filtro Máscara de enfoque de Photoshop. Al contrario de lo que su nombre sugiere, Máscara de enfoque es un filtro de enfoque.

| Opciones de máscara de enfoque | Descripción |
| --- | --- |
| **[!UICONTROL Importe]** | Requerido.<br>Controla la cantidad de contraste que se aplica a los píxeles del borde.<br>Considérelo como la intensidad del efecto. La principal diferencia entre los valores de cantidad de Máscara de enfoque en Adobe Dynamic Media y los valores de cantidad en Adobe Photoshop es que Photoshop tiene un intervalo de cantidad del 1 % al 500 %. Mientras que en Adobe Dynamic Media, el intervalo de valores es de `0.0` a `5.0`. Un valor de 5,0 en Adobe Dynamic Media es el equivalente aproximado de 500% en Photoshop; un valor de 0,9 es el equivalente de 90%, y así sucesivamente. |
| **[!UICONTROL Radio]** | Requerido.<br>Controla el radio del efecto.<br>El intervalo de valores es de `0` a `250`. El efecto se ejecuta en todos los píxeles de una imagen y se irradia desde todos los píxeles en todas las direcciones. El radio se mide en píxeles. Por ejemplo, para obtener un efecto de enfoque similar para una imagen de 2000 x 2000 píxeles e imagen de 500 x 500 píxeles, debe establecer un radio de dos píxeles en la imagen de 2000 x 2000 píxeles. A continuación, defina un valor de radio de un píxel en la imagen de 500 x 500 píxeles. Se utiliza un valor mayor para una imagen que tiene más píxeles. |
| **[!UICONTROL Umbral]** | Requerido.<br>El umbral es un rango de contraste que se ignora cuando se aplica el filtro Máscara de enfoque. Este efecto es importante para que no se introduzca ningún &quot;ruido&quot; en una imagen cuando se utilice este filtro. El intervalo de valores es de `0` a `255`, que es el número de pasos de brillo de una imagen en escala de grises. `0`=negro, `128`=50% gris y `255`=blanco.<br>Un valor de umbral de `12` ignora las ligeras variaciones en el brillo del tono de la piel para evitar agregar ruido, pero agrega contraste al borde de las áreas de contrastes, como cuando las pestañas tocan la piel.<br>Si tiene una foto de la cara de alguien, la máscara de enfoque afecta a las partes de contraste de la imagen. Por ejemplo, donde las pestañas y la piel se juntan para crear una zona obvia de contraste, y la piel lisa en sí misma. Incluso la piel más suave muestra cambios sutiles en los valores de brillo. Si no utiliza un valor de umbral, el filtro acentúa estos cambios sutiles en los píxeles de la piel. A su vez, se crea un efecto ruidoso e indeseable mientras que el contraste en las pestañas aumenta, lo que aumenta la nitidez.<br>Para evitar este problema, se introduce un valor de umbral que indica al filtro que ignore los píxeles que no cambian drásticamente el contraste, como la apariencia suave.<br>En el gráfico de cremallera mostrado anteriormente, observe la textura junto a las cremalleras. El ruido de la imagen se muestra porque los valores de umbral eran demasiado bajos para suprimir el ruido. |
| **[!UICONTROL Monocromo]** | Seleccione esta opción para resaltar el brillo (intensidad) de la imagen con máscara de enfoque.<br>Anule la selección para aplicar máscara de enfoque a cada componente de color por separado. |

Vea también [Enfoque de imágenes en Adobe Dynamic Media y en Image Server](/help/assets/assets/sharpening_images.pdf).

### Pestaña PostScript {#postscript-tab}

Puede rasterizar archivos de Adobe PostScript®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos de Adobe PostScript® (EPS) en Dynamic Media de Adobe. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que se cargan.

Al cargar archivos de imagen de PostScript (EPS), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color.

| Opción PostScript | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Elija Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia de fondo del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]**: conserva el espacio de color del archivo.<br>· **[!UICONTROL Forzar como RGB]**: se convierte al espacio de color de RGB.<br>· **[!UICONTROL Forzar como CMYK]**: se convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]**: se convierte al espacio de color de escala de grises. |

### Pestaña Photoshop {#photoshop-tab}

Puede crear plantillas a partir de archivos de Adobe® Photoshop®, mantener las capas, especificar cómo se asignan los nombres a las capas, extraer texto y especificar cómo se anclan las imágenes en las plantillas.

| Opción Photoshop | Descripción |
| --- | --- |
| **[!UICONTROL Mantener capas]** | Extrae las capas de PSD, si las hay, en recursos individuales. Las capas de recursos permanecen asociadas a PSD. Para verlos, abra el archivo PSD en Vista de detalles y seleccione el panel Capa. Consulte Visualización y edición de capas en un archivo PSD. |
| **[!UICONTROL Crear plantilla]** | Crea una plantilla a partir de las capas del archivo PSD. |
| **[!UICONTROL Extraer texto]** | Extrae el texto para que los usuarios puedan buscar texto en un visor. |
| **[!UICONTROL Extender las capas al tamaño del fondo]** | Amplía el tamaño de las capas de imagen copiadas al tamaño de la capa de fondo. |
| **[!UICONTROL Nomenclatura de capas]** | Amplía el tamaño de las capas de imagen copiadas al tamaño de la capa de fondo.<br>· **[!UICONTROL Nombre de capa]** - Nombra las imágenes después de sus nombres de capa en el archivo PSD. Por ejemplo, una capa denominada Etiqueta de precio del archivo PSD original se convierte en una imagen denominada Etiqueta de precio. Sin embargo, si los nombres de las capas del fichero PSD son nombres de capas Photoshop por defecto (Fondo, Capa 1, Capa 2, etc.), las imágenes recibirán los nombres de sus números de capa en el fichero PSD. <br>· **[!UICONTROL Photoshop y número de capa]**: nombra las imágenes después de sus números de capa en el archivo PSD, omitiendo los nombres de capa originales. Las imágenes se nombran con el nombre de archivo Photoshop y un número de capa anexado. Por ejemplo, la segunda capa de un archivo denominado `Spring Ad.psd` se denomina `Spring Ad_2` aunque no tuviera un nombre predeterminado en Photoshop.<br>· **[!UICONTROL Photoshop y nombre de capa]** - Nombra las imágenes después del archivo PSD seguido del nombre o número de capa. El número de capa se utiliza si los nombres de capa del fichero PSD son nombres de capa Photoshop por defecto. Por ejemplo, una capa denominada `Price Tag` en un archivo de PSD denominado `SpringAd` se denomina `Spring Ad_Price Tag`. Una capa con el nombre predeterminado Capa 2 se llama `Spring Ad_2`. |
| **[!UICONTROL Anclaje]** | Especifique cómo se anclan las imágenes en las plantillas que se generan a partir de la composición por capas producida a partir del archivo PSD. De forma predeterminada, el anclaje es el centro. Un anclaje central permite que las imágenes de reemplazo llenen mejor el mismo espacio, sin importar la proporción de aspecto de la imagen de reemplazo. Las imágenes con un aspecto diferente que reemplazan a esta imagen, al hacer referencia a la plantilla y utilizar la sustitución de parámetros, ocupan efectivamente el mismo espacio. Cambie a una configuración diferente si la aplicación requiere las imágenes de reemplazo para rellenar el espacio asignado en la plantilla. |

### Pestaña PDF {#pdf-tab}

Puede elegir entre rasterizar los archivos, extraer palabras de búsqueda y vínculos, definir la resolución y elegir un espacio de color.

| Opción PDF | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | · **[!UICONTROL Ninguno]**: no se ha completado ningún procesamiento de PDF.<br>· **[!UICONTROL Miniatura]**: rasga cada página del archivo PDF y la convierte en una imagen en miniatura.<br> · **[!UICONTROL Rasterizar]**: rasga las páginas del archivo PDF y convierte los gráficos vectoriales en imágenes de mapa de bits. Para crear un catálogo electrónico, elija esta opción. |
| **[!UICONTROL Extraer]** | · **[!UICONTROL Ninguno]**: no se extraen palabras de búsqueda ni vínculos de PDF.<br>· **[!UICONTROL Palabras de búsqueda]**: extrae palabras de búsqueda del archivo PDF para que se pueda buscar en él por palabra clave en un visor de catálogos electrónicos.<br>· **[!UICONTROL Vínculos]**: extrae vínculos de los archivos PDF y los convierte a mapas de imágenes que se utilizan en un visor de catálogos electrónicos.<br>· **[!UICONTROL Palabras de búsqueda y vínculos]**: extrae tanto las palabras de búsqueda como los vínculos para usarlos en un visor de catálogos electrónicos. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo PDF. El valor predeterminado es 150. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]**: mantiene el espacio de color del archivo PDF.<br>· **[!UICONTROL Forzar como RGB]**: se convierte al espacio de color de RGB.<br>· **[!UICONTROL Forzar como CMYK]**: se convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]**: se convierte al espacio de color de escala de grises. |

### Pestaña Illustrator {#illustrator-tab}

Puede rasterizar archivos de Adobe Illustrator®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos de Adobe® Illustrator® (AI) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que se cargan.

Al cargar archivos de imagen de Illustrator (AI), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color. Las opciones para dar formato a los archivos de PostScript y Illustrator están disponibles en la pantalla Cargar, en Opciones de PostScript y Opciones de Illustrator, en el cuadro Opciones del trabajo de carga.


| Opción Illustrator | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Elija Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia de fondo del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]**: conserva el espacio de color del archivo.<br>· **[!UICONTROL Forzar como RGB]**: se convierte al espacio de color de RGB.<br>· **[!UICONTROL Forzar como CMYK]**: se convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]**: se convierte al espacio de color de escala de grises. |
