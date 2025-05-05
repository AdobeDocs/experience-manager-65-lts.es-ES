---
title: Imágenes interactivas
description: Aprenda a trabajar con imágenes interactivas en Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Interactive Images
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 1d011ae238f213459c97e921740db10640935022
workflow-type: tm+mt
source-wordcount: '4118'
ht-degree: 1%

---

# Imágenes interactivas{#interactive-images}

Puede convertir fácilmente las imágenes estáticas en experiencias atractivas y enriquecidas para los clientes arrastrando y soltando puntos interactivos &quot;de venta&quot; en una imagen. Los puntos de acceso de compra combinan información adicional sobre un producto o servicio con una capacidad directa de punto de venta de &quot;Agregar al carro de compras&quot; o &quot;Comprar&quot;. Los clientes pueden seleccionar estos puntos interactivos y vincularse directamente al producto o servicio, añadirlo a un carro de compras o vincularlo a una página web. Las experiencias directas como estas aumentan la participación de los clientes y las conversiones en el sitio web.

A continuación se muestra un titular de ventas con una ventana emergente de vista rápida. Un usuario activa la vista rápida seleccionando el círculo o la &quot;zona interactiva&quot; en el modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Para ver las imágenes interactivas en acción en la página web anterior, vaya a lo siguiente:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=es)

## Descubra cómo se crean los titulares de imágenes interactivas {#watch-how-interactive-image-banners-are-created}

Reproducir un tutorial sobre [cómo se crean los titulares de imágenes interactivas](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (10 minutos y 33 segundos). También aprenderá a obtener una vista previa, editar y enviar titulares de imágenes interactivas.

## Inicio rápido: imágenes interactivas {#quick-start-interactive-images}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle a ponerse en marcha rápidamente con las imágenes interactivas en Adobe Experience Manager Assets.

Busque el encabezado **Ejemplo** dentro de algunas de las tareas de inicio rápido. Contiene un breve tutorial basado en el siguiente ejemplo de página web que aún no tiene imágenes interactivas agregadas:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es)

El tutorial ayuda a ilustrar los pasos de integración de imágenes interactivas en su propio sitio web.

Pasos de las imágenes interactivas:

1. **(Opcional) Identificar variables de puntos interactivos**: Si utiliza Experience Manager Assets y Dynamic Media de forma independiente, comience identificando las variables dinámicas utilizadas en la implementación de Quickview existente. A continuación, puede introducir datos de puntos interactivos al crear la imagen interactiva. Consulte [(Opcional) Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables).
Sin embargo, si utiliza Adobe Experience Manager Sites, Adobe Experience Manager eCommerce o ambos, este paso no es necesario.

1. **(opcional): cree un ajuste preestablecido de visualizador de imágenes interactivas**. Personalice la imagen gráfica que se usa para representar las zonas interactivas. No es necesario crear su propio ajuste preestablecido de visualizador de imágenes interactivas si desea utilizar el ajuste preestablecido de visualizador de imágenes interactivas predeterminado denominado `Shoppable_Banner` en su lugar.
Consulte [(Opcional) Crear un ajuste preestablecido de visualizador de imágenes interactivo](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Cargar un titular de imagen**: cargue titulares de imagen que desee hacer interactivos.
Ver [Cargar un titular de imagen](#uploading-an-image-banner).

1. **Agregar puntos interactivos a un titular de imagen**: agregue uno o más puntos interactivos a un titular de imagen y asocie cada uno con una acción como un hipervínculo, una vista rápida o un fragmento de experiencia. Después de agregar zonas interactivas, terminará esta tarea publicando la imagen interactiva.

   * Ver [Agregar puntos interactivos a un titular de imagen](#adding-hotspots-to-an-image-banner).
   * Ver [Previsualizar imágenes interactivas](#optional-previewing-interactive-images) - Opcional. Si lo desea, puede ver una representación del titular de la compra y probar su interactividad.
   * Consulte [Publicar Assets](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imágenes interactivas.

1. **Agregar una imagen interactiva al sitio web**: si usa Experience Manager Sites, comercio electrónico o ambos, puede agregar la imagen interactiva a una página web en Experience Manager. Arrastre el componente Medios interactivos a la página. Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

   Si utiliza Experience Manager Assets y Dynamic Media independiente, debe copiar el código incrustado en el sitio web y luego integrarlo con la vista rápida existente. Ver [Integrar una imagen interactiva con el sitio web](#integrating-an-interactive-image-with-your-website).

   Si utiliza un WCM (Administrador de contenido web) de terceros, debe integrar el nuevo vídeo interactivo con la implementación de vista rápida existente que se utiliza en el sitio web. Ver [Integrar una imagen interactiva con una vista rápida existente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Opcional) Identificar variables de puntos interactivos {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Esta tarea solo es necesaria si se cumplen los siguientes criterios:
>
>* Desea añadir interactividad a la imagen activando en la vista rápida.
>* Su implementación de Experience Manager *no* utiliza un marco de integración de comercio electrónico para extraer datos de productos en Experience Manager desde cualquier solución de comercio electrónico como IBM® WebSphere® Commerce, Elastic Path, hybris o Intershop.
>
>Si la implementación de Experience Manager utiliza el comercio electrónico, puede omitir esta tarea y continuar con la siguiente.

Comience identificando las variables dinámicas utilizadas por la implementación de vista rápida existente, de modo que pueda introducir datos de puntos interactivos para crear la imagen interactiva.

Al añadir puntos interactivos a una imagen de titular en Experience Manager Assets, debe asignar un SKU (código de referencia) y variables adicionales opcionales a cada punto interactivo. Estas variables de punto interactivo se utilizan más adelante para hacer coincidir los puntos interactivos con el contenido de vista rápida.

Es importante identificar correctamente el número y el tipo de variables que se asociarán a los datos del punto interactivo. Cada punto interactivo añadido a una imagen de titular debe llevar información suficiente para identificar de forma inequívoca el producto en el sistema back-end existente.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de puntos interactivos.

A veces basta con consultar con los especialistas de TI responsables de la implementación de Quickview existente. Es probable que los especialistas en TI sepan cuál es el conjunto mínimo de datos requerido para identificar Quickview en el sistema. Sin embargo, también es posible simplemente analizar el comportamiento existente del código front-end.

La mayoría de las implementaciones de Quickview utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, seleccionar un botón &quot;Vista rápida&quot;.
* El sitio web envía una solicitud Ajax al back-end para cargar los datos o el contenido de Quickview, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su representación en la página web.
* Finalmente, el código front-end procesa visualmente dicho contenido en la pantalla.

A continuación, el método consiste en visitar diferentes áreas del sitio web existente donde se ha implementado la función de vista rápida. A continuación, almacene en déclencheur la vista rápida y capture la URL de Ajax enviada por la página web para cargar los datos de vista rápida o el contenido.

Normalmente no es necesario utilizar herramientas de depuración especializadas. Los navegadores web modernos cuentan con inspectores web que hacen un trabajo adecuado. A continuación se muestran algunos ejemplos de exploradores web que incluyen inspectores web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, presione F12 para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la pestaña Red.

* En Firefox, puede activar el complemento Firebug pulsando F12 y utilizando su pestaña Red, o bien puede utilizar la herramienta Inspector integrada y su pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la pestaña Inspector.

Cuando la monitorización de red está activada en el navegador, almacene en déclencheur la vista rápida en la página.

Ahora busque la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para un análisis futuro. Normalmente, cuando se almacena en déclencheur la vista rápida, hay numerosas solicitudes que se envían al servidor. Normalmente, la URL de Ajax de vista rápida es una de las primeras en la lista. Tiene una parte de cadena de consulta o una ruta de acceso compleja y su tipo MIME de respuesta es `text/html`, `text/xml` o `text/javascript`.

Durante este proceso, es importante visitar diferentes áreas del sitio web, con diferentes categorías y tipos de productos. El motivo es que las direcciones URL de Quickview pueden tener partes que son comunes para una categoría de sitio web determinada, pero que solo cambian si visita una zona diferente del sitio web.

En el caso más simple, la única parte de la variable en la URL de vista rápida es el SKU del producto. En este caso, el valor SKU es el único fragmento de datos que necesita para añadir puntos interactivos a la imagen del titular.

Sin embargo, en casos complejos, la dirección URL de vista rápida tiene diferentes elementos que difieren además del SKU, como ID de categoría, código de color y código de tamaño. En estos casos, cada elemento es una variable independiente en la definición de datos de punto interactivo en la función de imagen interactiva de ventas en Experience Manager Assets.

Considere los siguientes ejemplos de direcciones URL de vista rápida y las variables de puntos interactivos resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>La única parte de la variable en la URL es el valor del parámetro de cadena de consulta productId= y es claramente un valor SKU. Por lo tanto, las zonas interactivas solo necesitan campos SKU con valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado en la ruta URL.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte de la variable se encuentra en la última parte de la ruta y se convierte en el valor SKU de las zonas interactivas: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoría en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>En este caso, la dirección URL consta de dos partes diferentes. El SKU se almacena en el parámetro <code>prodId</code> y el ID de categoría <code></code> se almacena en el parámetro <code>category=</code>.</p> <p>Como tal, las definiciones de puntos interactivos son pares. Es decir, un valor SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
      <li><p>El SKU es <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
      <li><p>El SKU es <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
      <li><p>El SKU es <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Ejemplo**

Puede aplicar el mismo método utilizado en los tres ejemplos anteriores a la página web de demostración:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es)

La página web de demostración tiene varias miniaturas de productos, cada una con un botón de vista rápida denominado &quot;Ver más&quot;. Con la herramienta de depuración del navegador web aún activada, seleccione cada botón y anote las URL de vista rápida registradas. Después de activar las cuatro vistas rápidas de productos disponibles en la página, tiene la siguiente lista de solicitudes de vista rápida realizadas al servidor:

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

Si observa las llamadas al servidor, verá que la información específica del producto solo está presente en la ruta de solicitud. También verá que la cadena de consulta no se utiliza en absoluto y que hay dos tipos distintos de fragmentos de datos implicados:

* El primer tipo es Masculino o Femenino. Puede llamar a esta &quot;categoría de producto&quot;.
* El segundo tipo es el nombre del producto, como CamoPullover. Puede suponer que esta información es el SKU del producto.

Dada esta información, toda la URL de vista rápida tiene el siguiente patrón:

`/datafeed/$categoryId$-$SKU$.json`

En función de dicho análisis, utilizaría `categoryId` y `SKU` para las zonas interactivas.

Ya está listo para cargar un titular de imagen y añadirle puntos interactivos mediante la función de imagen interactiva de ventas de Experience Manager Assets.

## (Opcional) Cree un ajuste preestablecido de visualizador de imágenes interactivo {#optional-creating-an-interactive-image-viewer-preset}

Puede elegir utilizar el ajuste preestablecido predeterminado e integrado del visualizador de imágenes interactivas denominado `Shoppable_Banner` que se incluye con Experience Manager Assets. O puede crear su propio ajuste preestablecido de visualizador personalizado para utilizarlo con imágenes interactivas.

Al crear un ajuste preestablecido de visualizador de imágenes interactivo personalizado, puede determinar el aspecto de las zonas interactivas en el titular de la imagen. Como parte de la creación del ajuste preestablecido de visualizador, puede elegir utilizar un gráfico de punto interactivo de una galería de imágenes predefinidas.

Después de guardar el ajuste preestablecido de visualizador, se activa automáticamente en la página de lista de Ajustes preestablecidos de visualizador de Experience Manager Assets. Esta funcionalidad significa que está visible en el componente de medios interactivos y siempre que vea un recurso. Sin embargo, para *entregar* un banner interactivo con este ajuste preestablecido de visualizador, también debe *publicar* su ajuste preestablecido de visualizador. Esta regla es verdadera para los ajustes preestablecidos personalizados o listos para usar del visualizador.

**Para crear un ajuste preestablecido de visualizador de imágenes interactivo:**

1. En el carril izquierdo, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.
1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Nuevo ajuste preestablecido de visualizador, escriba un nombre para describir el ajuste preestablecido de visualizador de banner interactivo.

   El título aparece en la página de lista Ajuste preestablecido de visualizador después de guardar.

1. En el menú desplegable Tipo de medio enriquecido, seleccione **[!UICONTROL Imagen interactiva]**.
1. Seleccione **[!UICONTROL Crear]**.
1. En la página Editar ajuste preestablecido de visor, seleccione la ficha **[!UICONTROL Apariencia]**.
1. Realice una de las siguientes acciones:

   * Para cargar su propia imagen de punto interactivo que desee utilizar en las imágenes, seleccione el icono Selector de recursos. En la página Seleccionar contenido, vaya a la imagen de punto interactivo que desee utilizar, selecciónela y, a continuación, seleccione el icono de la marca de verificación en la esquina superior derecha.
   * Para seleccionar una imagen de punto interactivo predefinida, seleccione el icono Galería de puntos interactivos. En la paleta galería de puntos interactivos, seleccione la imagen de punto interactivo que desee utilizar.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   Asegúrese de publicar el nuevo ajuste preestablecido de visualizador.

   Ver [Ajustes Preestablecidos Del Visor De Publicación Que Ha Agregado](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   Ya está listo para cargar un titular de imagen.

## Cargar un titular de imagen {#uploading-an-image-banner}

Si ya has subido las imágenes que quieres usar, avanza al siguiente paso: [Agregar puntos interactivos a un banner de imagen](#adding-hotspots-to-an-image-banner).

**Para cargar un titular de imagen:**

1. Cargue los titulares de las imágenes que desee hacer interactivos.

   Consulte [Cargando recursos](/help/assets/manage-assets.md#uploading-assets).

   Ya está listo para agregar puntos interactivos al titular de la imagen; consulte la siguiente tarea a continuación.

## Añadir puntos interactivos a un titular de imagen {#adding-hotspots-to-an-image-banner}

Puede añadir zonas interactivas a un titular de imagen mediante el editor de la página Gestión de puntos interactivos.

Al añadir zonas interactivas, puede definirlas como una ventana emergente de vista rápida, como un hipervínculo o como un fragmento de experiencia.

Ver [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Las herramientas para compartir en medios sociales de la imagen interactiva no son compatibles cuando se incrusta el visualizador en un fragmento de experiencia. Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visualizador le permiten incrustarlo correctamente en los fragmentos de experiencias.

Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación y edición actual.

Cuando termine de crear la imagen interactiva, puede usar Vista previa para ver una representación de cómo aparece la imagen interactiva a los clientes.

Consulte [ (Opcional) Vista previa de imágenes interactivas](#optional-previewing-interactive-images).

>[!NOTE]
>
>Cuando se añaden puntos interactivos a una imagen en una imagen interactiva o un titular de carrusel, la información del punto interactivo se almacena en la misma ubicación de metadatos. Esa ubicación es relativa a la ubicación de la imagen, independientemente de si es una imagen interactiva o un titular de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen, junto con sus datos de punto interactivo definidos, en cualquier visor.
>
>Los titulares de carrusel admiten mapas de imágenes en imágenes que también pueden contener puntos interactivos; las imágenes interactivas no. Tenga en cuenta esta regla si desea crear una imagen interactiva o un titular de carrusel que utilice la misma imagen. Puede crear imágenes interactivas y titulares de carrusel con copias independientes de la misma imagen.
>
>Consulte también [titulares de carrusel](/help/assets/carousel-banners.md).

>[!NOTE]
>
>Si está editando imágenes interactivas con zonas interactivas y recorta la imagen, se eliminan las zonas interactivas.

**Para agregar puntos interactivos a un titular de imagen:**

1. En la vista de Assets, vaya al titular de la imagen que desee hacer interactivo.
1. Realice una de las siguientes acciones:

   * Pase el ratón sobre la imagen y, a continuación, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación). En la barra de herramientas, seleccione **[!UICONTROL Editar]**.

   * Pase el ratón sobre la imagen y luego seleccione **[!UICONTROL Más acciones]** (icono de tres puntos) **[!UICONTROL Editar]**.

   * Seleccione la imagen para poder abrirla en la página Vista de detalles. En la barra de herramientas, seleccione **[!UICONTROL Editar]**.

1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Agregar punto interactivo]** (icono de selección con el dedo) para abrir la página de administración de puntos interactivos.
1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL punto interactivo]**.

   1. Cerca de la esquina superior izquierda de la página Administración de puntos interactivos, seleccione **[!UICONTROL punto interactivo]**.
   1. En la imagen, seleccione una ubicación en la que desee que aparezca el punto interactivo. Si es necesario, arrastre la zona interactiva para ajustar su ubicación.
   1. Añada puntos interactivos adicionales según sea necesario repitiendo los pasos a y b.
   1. (Opcional) Para eliminar un punto interactivo, selecciónelo en la imagen y, a continuación, seleccione **[!UICONTROL Eliminar]** (icono de la papelera) bajo el encabezado **[!UICONTROL Puntos interactivos]**.

1. En el campo de texto Nombre, escriba el nombre del punto interactivo. Este nombre también aparece en la lista desplegable Punto interactivo seleccionado.
1. Realice una de las siguientes acciones:

   * Seleccione **[!UICONTROL Quickview]**.

      * Si es cliente de Experience Manager Sites o de comercio electrónico, seleccione el icono Selector de productos (lupa) para abrir la página Seleccionar producto. Seleccione el producto que desea usar y luego seleccione **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página para poder volver a la página de administración de puntos interactivos.
      * Si *no es* cliente de Experience Manager Sites o eCommerce

         * Consulte [Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables); debe definir estas variables.
         * A continuación, introduzca manualmente el valor SKU. En el campo de texto Valor de SKU, escriba la SKU del producto (unidad de stock), que es un identificador único para cada producto o servicio distinto que ofrece. El valor de SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida para que el sistema sepa que debe asociar el punto interactivo seleccionado con la vista rápida de un SKU en particular.
         * (Opcional) Si hay otras variables dentro de la vista rápida que debe usar para identificar aún más un producto, seleccione **[!UICONTROL Agregar variable genérica]**. En el campo de texto, especifique una variable adicional. Por ejemplo, `category=Males` es una variable agregada.

   * Seleccione **[!UICONTROL Hipervínculo]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Selector de sitio (carpeta) para ir a una dirección URL. El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
      * Si es cliente independiente, en el campo de texto HREF, especifique la ruta de URL completa a una página web vinculada.

   Asegúrese de especificar si desea abrir el vínculo en una nueva pestaña del explorador (opción predeterminada recomendada) o en la misma pestaña.

   Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md) para obtener más información.

   * Seleccione **[!UICONTROL Fragmento de experiencia]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Buscar (lupa) para abrir la página Fragmento de experiencia. Seleccione el fragmento de experiencia que desee usar y, a continuación, seleccione **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página para poder volver a la página de administración de puntos interactivos.
Ver [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md).

      * Especifique la anchura y altura del fragmento de experiencia tal como desea que aparezca en el titular.

        >[!NOTE]
        >
        >Las herramientas para compartir en medios sociales de la imagen interactiva no son compatibles cuando se incrusta el visualizador en un fragmento de experiencia. Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visualizador le permiten incrustarlo correctamente en los fragmentos de experiencias.

1. Seleccione **[!UICONTROL Guardar]** para guardar su trabajo y volver a la página de exploración.
1. Publique la imagen interactiva. La publicación permite entregar el banner a través de la nube y también genera código incrustado si necesita integrarlo con un sitio web de terceros.

   Consulte [Publicar recursos](/help/assets/manage-assets.md#publishing-assets).

   Después de añadir puntos interactivos y publicar la imagen interactiva, ya puede añadirla al sitio web existente.

   Ver [Integrar una imagen interactiva con el sitio web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Si está editando imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

### (Opcional) Previsualizar imágenes interactivas {#optional-previewing-interactive-images}

Puede usar Vista previa para ver una representación de cómo aparece la imagen interactiva a los clientes y probar los puntos interactivos de la imagen para asegurarse de que se comportan según lo esperado.

Cuando esté satisfecho con la imagen interactiva, puede publicarla.
Ver [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/embed-code.md).
Ver [URL de vínculo a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para obtener una vista previa de imágenes interactivas:**

1. En la vista de Assets, vaya a una imagen interactiva existente que haya creado y seleccione para abrirla en Vista previa.
1. Cerca de la esquina superior izquierda de la página Vista previa, en la lista desplegable Contenido, seleccione **[!UICONTROL Visualizadores]**.
1. En la lista Visualizadores, seleccione **[!UICONTROL Shoppable_Banner]** o el nombre del ajuste preestablecido de visualizador de imágenes interactivo que ha creado.
1. Seleccione zonas interactivas en la imagen si desea probar las acciones asociadas.

## Publicar recursos de imagen interactiva {#publishing-interactive-image-assets}

Consulte [Publicar recursos](/help/assets/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imágenes interactivas.

## Integración de una imagen interactiva con el sitio web {#integrating-an-interactive-image-with-your-website}

Después de cargar una imagen de titular, añadir puntos interactivos a la imagen y publicar la imagen interactiva, ya puede añadirla a la página del sitio web.

Si es cliente de Experience Manager Sites, puede agregar la imagen interactiva arrastrando el componente Medios interactivos a la página. Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Si es cliente independiente de Experience Manager Assets, puede añadir manualmente la imagen interactiva al sitio web como se describe en esta sección.

1. Copie el código incrustado de la imagen interactiva publicada.
Ver [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/embed-code.md).

1. Añada el código incrustado copiado en la ubicación deseada dentro de la página web.
El código incrustado copiado se configura para un entorno interactivo, de modo que se ajusta automáticamente al área asignada.

**Ejemplo**

Uso del sitio web de demostración como ejemplo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=es)

Observe que la imagen de los tres machos es una etiqueta `IMG` estática:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

La integración es tan sencilla como quitar la etiqueta `IMG` y reemplazarla con el código incrustado copiado de Experience Manager Assets. Puede ver el resultado en la siguiente URL que muestra la imagen interactiva de ventas en la página con tres puntos interactivos de círculo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=es)

>[!NOTE]
>
>A partir de este punto, los puntos interactivos de la imagen interactiva de ventas del sitio web de demostración son solo para fines de visualización; aún no están integrados con la vista rápida existente.

Para aplicar un &quot;recorte&quot; a una imagen interactiva de ventas para un entorno interactivo, puede incluir el atributo de configuración de imagen interactiva `ZoomView.iscommand` en la ruta. Se llama al componente `ZoomView` y `iscommand` es el comando de servicio de imágenes de &quot;recorte&quot; que usted aplica.

Consulte el atributo de configuración [ZoomView.iscommand](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand).

Ver [recorte](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop) comando de servicio de imágenes.

Ya está listo para integrar la imagen interactiva con una vista rápida existente en su sitio web.

## Integración de una imagen interactiva con una vista rápida existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Esta tarea solo se aplica si es un cliente independiente de Experience Manager Assets.

El último paso de este proceso es integrar la imagen interactiva con una implementación de vista rápida existente en el sitio web. No hay ninguna solución para la integración que funcione para todos los casos. Cada implementación de Quickview es única y se necesita un enfoque específico. Es probable que implique la asistencia de una persona de TI front-end.

La implementación de Quickview existente normalmente representa una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario almacena en déclencheur un elemento en la interfaz de usuario del sitio web.
1. El código front-end obtiene una URL de vista rápida basada en el elemento de interfaz de usuario activado en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos de vista rápida o el contenido correspondiente al código front-end.
1. El código front-end carga los datos de vista rápida o el contenido.
1. De forma opcional, el código front-end convierte los datos de vista rápida cargados en una representación de HTML.
1. El código front-end muestra un cuadro de diálogo o panel modal y procesa el contenido de HTML en la pantalla para el usuario final.

Estas llamadas no representan llamadas de API públicas independientes a las que la lógica de página web puede llamar desde un paso arbitrario. En su lugar, es una llamada encadenada en la que cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Al mismo tiempo que la imagen interactiva de ventas sustituye al paso 1 y al paso 2 parcialmente, cuando un usuario selecciona un punto interactivo dentro de la imagen de ventas, el visor gestiona dicha interacción de usuario. El visor devuelve un evento a la página web que contiene todos los datos de puntos interactivos previamente añadidos a Experience Manager Assets.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por la imagen interactiva de ventas.
* Construye una URL de vista rápida basada en los datos del punto interactivo.
* Déclencheur el proceso de cargar la vista rápida desde el backend y procesarla en la pantalla para mostrarla.

El código incrustado devuelto por Experience Manager Assets ya tiene un controlador de eventos listo para usar que se comenta, como se ve en el siguiente fragmento de código resaltado:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you must add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //See your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio con el código específico de la página web en particular.

El proceso de construir la URL de vista rápida es opuesto al proceso utilizado para identificar las variables de punto interactivo que se trataron anteriormente.

Consulte [Identificar variables de puntos interactivos](#optional-identifying-hotspot-variables).

Con los ejemplos de URL de vista rápida anteriores, puede ver en los siguientes ejemplos cómo se construye la URL de vista rápida en cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, encontrado en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
   <td><p>SKU único, encontrado en la ruta URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/product/" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID de categoría en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers(&lbrace;
      "quickViewActivate": function(inData) &lbrace;
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      &rbrace;,
      &rbrace;);</code></td>
  </tr>
 </tbody>
</table>

El último paso para almacenar en déclencheur la URL de vista rápida y activar el panel de vista rápida muy probablemente requiera la asistencia de una persona de TI front-end de su departamento de TI. Tienen los conocimientos necesarios para saber cómo almacenar en déclencheur con precisión la implementación de Quickview desde el paso adecuado, teniendo una URL de Quickview lista para usar.

Puede ver cómo se aplican estos pasos al sitio web de demostración para integrar completamente una imagen interactiva de ventas con el código de vista rápida. Anteriormente, la estructura de la URL de vista rápida se identificaba de la siguiente manera:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esta dirección URL dentro del controlador `quickViewActivate`, puede utilizar los campos `categoryId` y `SKU` disponibles en el objeto `inData` que el código del visor pasa al controlador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

El sitio web de demostración está activando el cuadro de diálogo Vista rápida mediante una simple llamada a la función `loadQuickView()`. Esta función solo toma un argumento, que es la URL de datos de vista rápida. Como tal, el último paso para integrar la imagen interactiva de ventas es agregar la siguiente línea de código al controlador `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

El siguiente es el código fuente completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

El sitio web de demostración final con la imagen interactiva completamente integrada tiene el siguiente aspecto:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=es](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=es)

## Utilice la vista rápida para crear ventanas emergentes personalizadas {#using-quickviews-to-create-custom-pop-ups}

Ver [Crear ventanas emergentes personalizadas con Quickview](/help/assets/custom-pop-ups.md).
