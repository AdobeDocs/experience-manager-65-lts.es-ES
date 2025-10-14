---
title: Titulares de carrusel
description: Aprenda a trabajar con titulares de carrusel en Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Carousel Banners
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 48cdca14c4e993281ed8c0a4a364aebe7a4611ad
workflow-type: tm+mt
source-wordcount: '4563'
ht-degree: 3%

---

# Titulares de carrusel{#carousel-banners}

Los titulares de carrusel permiten a los especialistas en marketing impulsar la conversión creando fácilmente contenido promocional giratorio interactivo y entregándolo en cualquier pantalla.

Crear y modificar contenido destacado en titulares promocionales puede llevar mucho tiempo, lo que limita la capacidad de publicar rápidamente contenido nuevo o de segmentarlo. Los titulares de carrusel permiten crear o modificar rápidamente titulares giratorios. Puede añadir interactividad, como puntos interactivos que se vinculan a detalles del producto o recursos relacionados, y enviarlos a cualquier pantalla, lo que le permite introducir nuevo contenido promocional en el mercado más rápido.

Los titulares de carrusel se designan mediante un titular con la palabra **[!UICONTROL CAROUSELSET]**

![chlimage_1-438](assets/chlimage_1-438.png)

En el sitio web, un banner de carrusel puede tener el siguiente aspecto:

![chlimage_1-439](assets/chlimage_1-439.png)

Aquí puede navegar por las imágenes (haciendo clic en los números). Además, las diapositivas giran automáticamente en función de un intervalo de tiempo que puede personalizar. Las imágenes que agrega en los titulares del carrusel admiten puntos interactivos y mapas de imagen, donde los usuarios pueden seleccionar o ir a un hipervínculo o acceder a una ventana de vista rápida.

En este ejemplo, un usuario ha pulsado o hecho clic en un mapa de imagen y ha accedido a la ventana de vista rápida para ver si tiene guantes:

![chlimage_1-440](assets/chlimage_1-440.png)

## Vea cómo se crean los titulares de carrusel {#watch-how-carousel-banners-are-created}

Reproducir un tutorial sobre [cómo se crean los titulares del carrusel](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner)&#x200B;(10 minutos y 33 segundos). También aprenderá a obtener una vista previa, editar y distribuir titulares de carrusel.

>[!NOTE]
>
>Los usuarios que no sean administradores deben agregarse al grupo **[!UICONTROL `dam-users`]** para poder crear o editar titulares de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al grupo **[!UICONTROL `dam-users`]**.

## Inicio rápido: Banners de carrusel {#quick-start-carousel-banners}

Para ayudarle a ponerse en marcha rápidamente con titulares de carrusel:

1. [Identificar variables de puntos interactivos y mapas de imagen](#identifying-hotspot-and-image-map-variables) (solo para clientes que usan Experience Manager Assets + Dynamic Media)

   Comience identificando las variables dinámicas utilizadas por la implementación de vista rápida existente para que pueda introducir correctamente los puntos interactivos y los datos del mapa de imagen durante el proceso de creación del banner de carrusel en Adobe Experience Manager Assets.

   >[!NOTE]
   >
   >Si es cliente de Experience Manager Assets y Dynamic Media, debe introducir manualmente datos para puntos interactivos y mapas de imagen y, a continuación, integrar la URL publicada o el código incrustado con el sistema de administración de contenido de terceros.

1. Opcional: [Cree un ajuste preestablecido de visualizador de conjuntos de carrusel](/help/assets/managing-viewer-presets.md), según sea necesario.

   Si es administrador, puede personalizar el comportamiento y el aspecto del carrusel creando su propio ajuste preestablecido de visualizador de carrusel. La principal ventaja es que puede reutilizar este ajuste preestablecido de visualizador personalizado para varios carruseles. Sin embargo, los usuarios pueden personalizar de forma opcional el comportamiento y el aspecto del carrusel directamente durante la creación. Este método es el preferido cuando se desea un diseño específico para un carrusel determinado.

1. [Cargar un titular de imagen](#uploading-image-banners).

   Cargue los titulares de las imágenes que desee hacer interactivos.

1. [Crear conjuntos de carrusel](#creating-carousel-sets).

   En los conjuntos de carruseles, los usuarios navegan por las imágenes del titular y seleccionan zonas interactivas o mapas de imagen para acceder al contenido relevante.

   Para crear un conjunto de carrusel en Assets, seleccione **[!UICONTROL Crear]** y luego **[!UICONTROL Conjuntos de carrusel]**. Agregue recursos a cada diapositiva y seleccione **[!UICONTROL Guardar]**. También puede editar el aspecto y el comportamiento del carrusel directamente en el editor.

1. [Agregar puntos interactivos o mapas de imagen a un titular de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).

   Añada una o más zonas interactivas o mapas de imagen a un titular de imagen y asócielos a una acción, como un vínculo, una vista rápida o un fragmento de experiencia. Después de agregar puntos interactivos o mapas de imagen, finalice esta tarea publicando el conjunto de carrusel. La publicación crea el código incrustado que puede utilizar para copiar y aplicar en la página de aterrizaje del sitio web.

   Ver [(Opcional) vista previa de titulares de carrusel](#optional-previewing-carousel-banners) - Opcional. Si lo desea, puede ver una representación del conjunto de carrusel y probar su interactividad.

1. [Publicar titulares de carrusel](#publishing-carousel-banners).

   Publica un conjunto de carrusel como lo haría con cualquier recurso. En Assets, vaya al conjunto de carrusel, selecciónelo y seleccione **[!UICONTROL Publicar]**. La publicación de un conjunto de carrusel activa la URL y la cadena de incrustación.

1. Realice una de las siguientes acciones:

   * [Agregar un banner de carrusel a la página del sitio web](#adding-a-carousel-banner-to-your-website-page) Puede agregar la URL del banner de carrusel o el código incrustado que ha copiado en la página del sitio web.

      * [Integrar el titular del carrusel con una vista rápida existente](#integrating-the-carousel-banner-with-an-existing-quickview). Si utiliza un sistema de administración de contenido web de terceros, debe integrar el nuevo banner de carrusel con la implementación de Quickview existente en su sitio web.

   * [Agregar un banner de carrusel al sitio web en Experience Manager](/help/assets/adding-dynamic-media-assets-to-pages.md) Si es cliente de Experience Manager Sites, puede agregar el conjunto de carrusel directamente a la página en Experience Manager mediante el componente de medios interactivos.

Para editar conjuntos de carrusel, consulte [edición de conjuntos de carrusel](#editing-carousel-sets). Además, puede ver y editar [propiedades del conjunto de carrusel](manage-assets.md#editing-properties).

## Identificación de variables de puntos interactivos y mapas de imagen {#identifying-hotspot-and-image-map-variables}

Comience identificando las variables dinámicas utilizadas por la implementación de vista rápida existente para que pueda introducir correctamente los puntos interactivos o los datos del mapa de imagen durante el proceso de creación del conjunto de carrusel en Experience Manager Assets.

Cuando añada puntos interactivos o mapas de imagen a una imagen de titular en Experience Manager Assets, asigne un SKU y variables adicionales opcionales a cada punto interactivo o mapa de imagen. Estas variables se utilizan más adelante para hacer coincidir puntos interactivos o mapas de imagen con contenido de vista rápida.

>[!NOTE]
>
>Si es cliente de Experience Manager Assets o Media, publica la URL o el código incrustado y, a continuación, lo integra con el sistema de administración de contenido de terceros e identifica manualmente los puntos interactivos y los mapas de imagen.

Es importante identificar correctamente el número y el tipo de variables que se asociarán a los datos de puntos interactivos o mapas de imagen. Cada punto interactivo o mapa de imagen añadido a una imagen de titular debe llevar suficiente información para identificar de forma inequívoca el producto en el sistema back-end existente. Al mismo tiempo, cada punto interactivo o mapa de imagen no debe incluir más datos de los necesarios. El motivo es que esto haría que el proceso de entrada de datos fuera demasiado complejo y la administración continua de puntos interactivos o mapas de imágenes fuera más propensa a errores.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de puntos interactivos o mapas de imagen.

A veces basta con consultar con los especialistas de TI responsables de la implementación de Quickview existente. Es probable que sepan cuál es el conjunto mínimo de datos necesario para identificar Quickview en el sistema. Sin embargo, normalmente también es posible analizar simplemente el comportamiento existente del código front-end.

La mayoría de las implementaciones de Quickview utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, al tocar un botón **[!UICONTROL Quickview]**.
* El sitio web envía una solicitud Ajax al back-end para cargar los datos o el contenido de Quickview, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su representación en la página web.
* Finalmente, el código front-end procesa visualmente dicho contenido en la pantalla.

A continuación, el método consiste en visitar diferentes áreas del sitio web existente donde se ha implementado la función de vista rápida. Almacene en déclencheur la vista rápida y capture la URL de Ajax que envía la página web para cargar los datos o el contenido de la vista rápida.

Normalmente no es necesario utilizar herramientas de depuración especializadas. Los navegadores web modernos cuentan con inspectores web que hacen un trabajo adecuado. A continuación se muestran algunos ejemplos de exploradores web que incluyen inspectores web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, presione F12 (Windows) o Comando-Opción-I (Mac) para abrir el panel Herramientas para desarrolladores y, a continuación, seleccione la pestaña Red.
* En Firefox, puede activar el complemento Firebug pulsando F12 (Windows) o Comando-Opción-I (Mac) y utilizar su pestaña Red, o bien puede utilizar la herramienta Inspector integrada y su pestaña Red.

Cuando la monitorización de red está activada en el navegador, almacene en déclencheur la vista rápida en la página.

Ahora busque la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para un análisis futuro. Normalmente, cuando se almacena en déclencheur la vista rápida, hay numerosas solicitudes que se envían al servidor. Normalmente, la URL de Ajax de vista rápida es una de las primeras en la lista. Tiene una parte de cadena de consulta o una ruta de acceso compleja y su tipo MIME de respuesta es `text/html`, `text/xml` o `text/javascript`.

Durante este proceso, es importante visitar diferentes áreas del sitio web, con diferentes categorías y tipos de productos. El motivo es que las direcciones URL de Quickview tienen partes que son comunes para una categoría de sitio web determinada, pero que solo cambian si visita una zona diferente del sitio web.

En el caso más simple, la única parte de la variable en la URL de vista rápida es el SKU del producto. En este caso, el valor SKU es el único fragmento de datos que necesita para añadir puntos interactivos o mapas de imagen a la imagen del titular.

Sin embargo, en casos complejos, la dirección URL de vista rápida tiene diferentes elementos que difieren además del SKU, como ID de categoría, código de color y código de tamaño. En estos casos, cada elemento es una variable independiente en la definición de datos de punto interactivo o mapa de imagen en la función de titular del carrusel.

Considere los siguientes ejemplos de direcciones URL de vista rápida y las variables de puntos interactivos o mapas de imagen resultantes:

<table>
 <tbody>
  <tr>
   <td>SKU único, encontrado en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&source=100</code></p> </li>
    </ul> <p>La única parte de la variable en la dirección URL es el valor del parámetro de cadena de consulta <code>productId=</code> y es claramente un valor SKU. Por lo tanto, las zonas interactivas o los mapas de imagen solo necesitan campos SKU con valores como <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU único, encontrado en la ruta URL.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte de la variable se encuentra en la última parte de la ruta y se convierte en el valor SKU de los puntos interactivos o los mapas de imagen: <strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID de categoría en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&prodId=308706</code></p> </li>
    </ul> <p>En este caso, la dirección URL consta de dos partes diferentes. El SKU se almacena en el parámetro <code>prodId</code> y el ID de categoría en el parámetro <code>category=</code>.</p> <p>Como tal, las definiciones de mapa de imagen/punto interactivo son pares. Es decir, un valor SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
     <li><p>El SKU es <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
     <li><p>El SKU es <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
     <li><p>El SKU es <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Cargar titulares de imagen {#uploading-image-banners}

Si ya has subido las imágenes que quieres usar, avanza al siguiente paso: [Crear conjuntos de carrusel](#creating-carousel-sets). Tenga en cuenta que las imágenes utilizadas en el carrusel deben cargarse después de habilitar Dynamic Media.

Para cargar titulares de imagen, consulte [Cargar recursos](/help/assets/manage-assets.md).

## Crear conjuntos de carrusel {#creating-carousel-sets}

>[!NOTE]
>
>Los usuarios que no sean administradores deben agregarse al grupo **[!UICONTROL `dam-users`]** para poder crear o editar titulares de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al grupo **[!UICONTROL `dam-users`]**.

**Para crear conjuntos de carrusel:**

1. En Assets, vaya a la carpeta donde desea crear el conjunto de carrusel y vaya a **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de carrusel]**.
1. En la página del editor de banners de carrusel, seleccione **[!UICONTROL Pulse para abrir el Selector de recursos]** y seleccionar la imagen de la primera diapositiva.

   En la página del editor de banners de carrusel, realice una de las acciones siguientes:

   * Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Agregar diapositiva]**.

   * Cerca de la mitad de la página, seleccione **[!UICONTROL Puntee para abrir el Selector de recursos]**.

   Seleccione para seleccionar los recursos que desea incluir en el conjunto de carrusel. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y pulsando o haciendo clic en **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, seleccione el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, pulse el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md) para obtener más información.

1. Siga agregando diapositivas hasta que haya agregado todas las imágenes por las que desea girar en el conjunto de carrusel.
1. (Opcional) Realice una de las siguientes acciones:

   * Si es necesario, arrastre la diapositiva para reorganizar las imágenes en la lista establecida.
   * Para eliminar una imagen, selecciónela y, a continuación, seleccione **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione la lista desplegable de ajustes preestablecidos y, a continuación, seleccione un ajuste preestablecido para aplicarlo a la vez.

   Para eliminar una diapositiva, selecciónela y, en la barra de herramientas, seleccione **[!UICONTROL Eliminar diapositiva]**. Para mover una diapositiva, seleccione el icono de reordenar y mantenga pulsado y desplácese hasta la ubicación deseada.

1. Después de agregar las imágenes en las diapositivas, puede agregar un punto interactivo, un mapa de imagen o ambos a la imagen. Ver [Agregar puntos interactivos o mapas de imagen a un titular de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Puede cambiar el diseño visual y el comportamiento de los conjuntos de carrusel. Seleccione las pestañas **[!UICONTROL Comportamiento]** y **[!UICONTROL Apariencia]** y ajuste el aspecto del titular del carrusel o el comportamiento de los componentes específicos. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/viewer-presets.md) para obtener más información sobre cómo usar el editor de visor.

   >[!NOTE]
   >
   >Para los titulares de carrusel, puede ajustar lo siguiente:
   >
   >    * Duración que muestra una imagen. De forma predeterminada, cada imagen se muestra durante 9 segundos.
   >    * Animación. De forma predeterminada, cada transición de diapositiva es una transición gradual. Puede cambiarlo a una transición de diapositivas.
   >    * Estilo de los botones. Los usuarios pueden girar a través de los titulares tocando cada punto o número. Puede cambiar el lugar en el que aparecen los botones del indicador de conjunto (y si son numéricos o un estilo de puntos) y el tamaño.
   >    * Cambie el estilo de resaltado de un mapa de imagen o el icono utilizado para las zonas interactivas.
   >    * Antes de editar un ajuste preestablecido de visualizador, elija el estilo en el que desea basarlo. Si no elige un estilo, cuando empiece a editar el ajuste preestablecido de visualizador, perderá todos los cambios si decide cambiar a otro ajuste preestablecido.
   >
   >Consulte [Consideraciones especiales para titulares de carrusel](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) para obtener instrucciones detalladas y más información sobre el editor del visor.

   También puede obtener una vista previa del aspecto del titular del carrusel. Ver [(Opcional) Vista previa de los titulares del carrusel](#optional-previewing-carousel-banners).

1. Seleccione **[!UICONTROL Guardar]** cuando termine.

## Adición de puntos interactivos o mapas de imagen a un titular de imagen {#adding-hotspots-or-image-maps-to-an-image-banner}

Puede añadir zonas interactivas o mapas de imagen a un titular mediante el editor de conjuntos de carrusel.

Al agregar zonas interactivas o mapas de imagen, puede definirlos como una visualización emergente de vista rápida, como un hipervínculo o como un fragmento de experiencia.

Ver [Fragmento de experiencia](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Las herramientas de uso compartido de medios sociales del titular del carrusel no son compatibles cuando se incrusta el visualizador en un fragmento de experiencia.
>
>Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visualizador le permiten incrustarlo correctamente en los fragmentos de experiencias.

Recuerde guardar su trabajo a medida que añada puntos interactivos o mapas de imagen a una imagen. Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación y edición actual.

Cuando termine de crear el titular del carrusel, puede utilizar la opción Previsualizar para ver una representación de cómo se muestra el titular del carrusel a los clientes.

Ver [(Opcional) Vista previa de los titulares del carrusel](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Cuando se agregan puntos interactivos a una imagen de una [imagen interactiva](/help/assets/interactive-images.md) o a un banner de carrusel, la información del punto interactivo se almacena en la misma ubicación de metadatos. Esa ubicación es relativa a la ubicación de la imagen, independientemente de si es una imagen interactiva o un titular de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen, junto con sus datos de punto interactivo definidos, en cualquier visor.
>
>Sin embargo, tenga en cuenta que los titulares de carrusel admiten mapas de imagen en imágenes que también pueden contener puntos interactivos; una imagen interactiva no. Tenga en cuenta esta regla si desea crear una imagen interactiva o un titular de carrusel que utilice la misma imagen. Considere la posibilidad de crear imágenes interactivas y titulares de carrusel con copias independientes de la misma imagen en su lugar.

>[!NOTE]
>
>Si está editando imágenes interactivas con zonas interactivas y recorta la imagen, se eliminan las zonas interactivas.

Consulte también [Agregar mapas de imagen](/help/assets/image-maps.md).

**Para agregar puntos interactivos o mapas de imagen a un titular de imagen:**

1. En Assets, vaya al conjunto de carrusel que desee hacer interactivo.
1. Seleccione el conjunto de carrusel y seleccione **[!UICONTROL Editar]**. Se abre el Editor del visor de carrusel.
1. Seleccione la diapositiva que desea convertir en interactiva.
1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL punto interactivo]** o **[!UICONTROL mapa de imagen]**.
1. Realice una de las acciones siguientes:

   * Para zonas interactivas: en la imagen, seleccione una ubicación en la que desee que aparezca la zona interactiva.
   * Para mapas de imagen: en la imagen, seleccione y, a continuación, arrastre de la parte superior izquierda a la inferior derecha para crear el área del mapa de imagen. Puede ajustar el tamaño del mapa de imagen arrastrando las esquinas.

   Si es necesario, arrastre el punto interactivo o el mapa de imagen a una nueva ubicación. Añada más puntos interactivos o mapas de imagen según sea necesario.

   Para eliminar un punto interactivo o un mapa de imagen, seleccione la pestaña **[!UICONTROL Acciones]**. En el encabezado **[!UICONTROL Mapas y zonas interactivas]**, del menú desplegable **[!UICONTROL Tipo seleccionado]**, seleccione el nombre del punto interactivo o del mapa de imagen que desea eliminar. Seleccione el icono **[!UICONTROL Papelera]** junto al menú y, a continuación, seleccione **[!UICONTROL Eliminar]**.

1. En el campo de texto Nombre, escriba el nombre del punto interactivo o del mapa de imagen. Este nombre también aparece en la lista desplegable **[!UICONTROL Mapas y puntos interactivos]**. Proporcionar un nombre facilita la identificación del punto interactivo o el mapa de imagen si decide cambiarlo en el futuro.
1. Realice una de las siguientes acciones en la ficha **[!UICONTROL Acciones]**:

   * Seleccione **[!UICONTROL Quickview]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Selector de productos (lupa) para abrir la página Seleccionar producto. Seleccione el producto que desea utilizar y, a continuación, seleccione la marca de verificación en la esquina superior derecha de la página para poder volver al editor de banners de carrusel.
      * Si no es cliente de Experience Manager Sites

         * Consulte [Identificar variables de puntos interactivos](#identifying-hotspot-and-image-map-variables) si desea definir estas variables.
         * A continuación, introduzca manualmente el valor SKU. En el campo de texto Valor de SKU, escriba la SKU del producto (unidad de stock), que es un identificador único para cada producto o servicio distinto que ofrece. El valor de SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida para que el sistema sepa que debe asociar el punto interactivo tocado con la vista rápida de una SKU en particular.
         * (Opcional) Si hay otras variables dentro de la vista rápida que debe usar para identificar aún más un producto, seleccione **[!UICONTROL Agregar variable genérica]**. En el campo de texto, especifique una variable adicional. Por ejemplo, category=Mens es una variable agregada.

         * Consulte [Trabajar con selectores](/help/assets/working-with-selectors.md) para obtener más información.

   * Seleccione **[!UICONTROL Hipervínculo]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Selector de sitio (carpeta) para ir a una dirección URL.

        >[!NOTE]
        >
        >El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.

      * Si es cliente independiente, en el campo de texto HREF, especifique la ruta de URL completa a una página web vinculada.

   Asegúrese de especificar si desea abrir el vínculo en una nueva pestaña del explorador (opción predeterminada recomendada) o en la misma pestaña.

   Consulte [Uso de selectores](/help/assets/working-with-selectors.md) para obtener más información.

   * Seleccione **[!UICONTROL Fragmento de experiencia]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Buscar (lupa) para abrir la página Fragmento de experiencia. Seleccione el fragmento de experiencia que desee usar y, a continuación, seleccione **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página para poder volver a la página de administración de puntos interactivos.
Ver [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md).

      * Especifique la anchura y altura del fragmento de experiencia tal como aparece en el banner.

        >[!NOTE]
        >
        >Las herramientas de uso compartido de medios sociales del titular del carrusel no son compatibles cuando se incrusta el visualizador en un fragmento de experiencia.
        >
        >Para solucionar este problema, cree ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visualizador le permiten incrustarlo correctamente en los fragmentos de experiencias.

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   También puede obtener una vista previa del aspecto del titular del carrusel. Consulte [&#x200B; (Opcional) Vista previa de los titulares del carrusel](#optional-previewing-carousel-banners).

1. Seleccione **[!UICONTROL Guardar]**.
1. Publique el conjunto de carrusel. Al publicar, se crea el código incrustado o la dirección URL que puede utilizar en la página del sitio web. Si es cliente de Experience Manager Sites, puede agregar el conjunto de carrusel directamente a la página web.

   Consulte [Publicando recursos](/help/assets/publishing-dynamicmedia-assets.md).

   Ver [Agregar un conjunto de carrusel a la página de aterrizaje del sitio web](#adding-a-carousel-banner-to-your-website-page)

## Editar conjuntos de carrusel {#editing-carousel-sets}

>[!NOTE]
>
>Los usuarios que no sean administradores deben agregarse al grupo **[!UICONTROL `dam-users`]** para poder crear o editar titulares de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al grupo **[!UICONTROL dam-users]**.

Puede realizar varias tareas de edición en los conjuntos de carrusel, como las siguientes:

* Agregar diapositivas a un conjunto de carrusel. Consulte también [Trabajo con selectores](/help/assets/working-with-selectors.md).
* Reordene las diapositivas del conjunto de carrusel.
* Elimine recursos en el conjunto de carrusel.
* Aplique un ajuste preestablecido de visor.
* Elimine el conjunto de carrusel.
* Añada o edite puntos interactivos y mapas de imagen. Consulte también [Trabajo con selectores](/help/assets/working-with-selectors.md).

**Para editar conjuntos de carrusel:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de carrusel y luego seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de carrusel, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, seleccione **[!UICONTROL Editar]** en la barra de herramientas.

   * Seleccione un recurso de conjunto de carrusel y, a continuación, en la esquina superior izquierda de la página, seleccione **[!UICONTROL Editar]** (icono de lápiz).

1. Para editar el conjunto de carrusel, realice una de las siguientes acciones:

   * Para agregar una diapositiva, seleccione el icono **[!UICONTROL Agregar diapositiva]**, desplácese hasta el recurso que desee agregar a esa diapositiva y marque la casilla de verificación.
   * Para reordenar las diapositivas, arrastre una diapositiva a una nueva ubicación (seleccione el icono de reordenar para mover los elementos).
   * Para agregar un punto interactivo o un mapa de imagen, seleccione los iconos del punto interactivo o del mapa de imagen y vea [agregar puntos interactivos y mapas de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Para editar el aspecto o el comportamiento del conjunto de carrusel, seleccione la ficha **[!UICONTROL Aspecto]** o **[!UICONTROL Comportamiento]** y, a continuación, defina las opciones que desee.
   * Para editar las zonas interactivas o los mapas de imagen, en la diapositiva adecuada, seleccione una zona interactiva o un mapa de imagen y cámbielo según sea necesario en la ficha **[!UICONTROL Acciones]**.
   * Para eliminar una diapositiva, selecciónela y, a continuación, seleccione **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione la lista desplegable **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visualizador.
   * Para eliminar un conjunto de carrusel completo, ve al conjunto de carrusel, selecciónalo y, a continuación, selecciona **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Si está editando imágenes interactivas con zonas interactivas y recorta la imagen, se eliminan las zonas interactivas.
   >
   >

## (Opcional) Previsualizar titulares de carrusel {#optional-previewing-carousel-banners}

Puede usar Vista previa para ver cómo aparece el banner del carrusel para los clientes y probar los puntos interactivos de los banners del carrusel y los mapas de imagen para asegurarse de que se comportan según lo esperado.

Cuando esté satisfecho con el titular del carrusel, puede publicarlo.
Ver [Incrustación del visor de vídeo o de imágenes en una página web](/help/assets/embed-code.md).
Ver [URL de vinculación a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Puede obtener una vista previa de los titulares de carrusel desde el Editor de carrusel (método preferido) o desde la lista **[!UICONTROL Visores]**.

**Para obtener una vista previa de los titulares de carrusel:**

1. En **[!UICONTROL Assets]**, navegue hasta un banner de carrusel existente que haya creado y seleccione para abrirlo.
1. Seleccione **[!UICONTROL Editar]**.
1. En la lista de ajustes preestablecidos de visualizador, en la esquina derecha de la barra de herramientas, seleccione un visualizador para previsualizar el titular del carrusel.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Seleccionar **[!UICONTROL vista previa]**.
1. Seleccione las zonas interactivas o los mapas de imagen de la imagen para poder probar sus acciones asociadas.

**Para obtener una vista previa de los titulares de carrusel de la lista de visores:**

1. En **[!UICONTROL Assets]**, navegue hasta un banner de carrusel existente que haya creado y seleccione para abrirlo.
1. Cerca de la esquina superior izquierda de la página Vista previa, seleccione el icono Contenido.
1. En la lista **[!UICONTROL Visualizadores]** del panel situado en la parte izquierda de la página, seleccione el nombre del ajuste preestablecido del visualizador de banners de carrusel que desee utilizar.
1. Seleccione las zonas interactivas o los mapas de imagen de la imagen para poder probar sus acciones asociadas.

## Publicar titulares de carrusel {#publishing-carousel-banners}

Publique el carrusel para poder utilizarlo. La publicación de un conjunto de carrusel activa la URL y el código de incrustación. También publica el carrusel en la nube de Dynamic Media, que está integrada con una CDN para una entrega escalable y con rendimiento.

>[!NOTE]
>
>Si utiliza una imagen interactiva existente con puntos interactivos para el titular del carrusel, debe publicar la imagen interactiva por separado después de publicar el titular del carrusel.
>
>Además, si modifica una imagen interactiva publicada preexistente que esté utilizando en un titular de carrusel, debe publicar la imagen interactiva antes de que esos cambios se reflejen en el titular del carrusel.

Consulte [Publicar Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md) para obtener información sobre cómo publicar titulares de carrusel.

## Añadir un banner de carrusel a la página del sitio web {#adding-a-carousel-banner-to-your-website-page}

Después de cargar imágenes de titular para crear un carrusel, añadir zonas interactivas o mapas de imagen al titular y publicar el conjunto de carrusel, ya puede añadirlo a la página web existente.

>[!NOTE]
>
>Si es cliente de Experience Manager Sites, puede agregar el titular del carrusel directamente a la página arrastrando el componente Medios interactivos a la página. Consulte [Agregar recursos de Dynamic Media a las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

Sin embargo, si es cliente independiente de Experience Manager Assets, puede añadir manualmente el banner de carrusel a la página de aterrizaje del sitio web como se describe en esta sección.

1. Copie el código incrustado del conjunto de carrusel publicado.
Ver [Incrustar el vídeo o el Visor de imágenes en una página web](/help/assets/embed-code.md).

1. Agregue el código incrustado que ha copiado de Experience Manager Assets a su página web.
El código incrustado copiado es adaptable, por lo que debe ajustarse automáticamente al área de incrustación de la página.

## Integración del titular del carrusel con una vista rápida existente {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
>
>Este paso solo se aplica si es cliente independiente de Experience Manager Assets.

El último paso de este proceso es integrar el banner de carrusel con una implementación de Quickview existente en su sitio web. Cada implementación de Quickview es única y se necesita un enfoque específico que implique la asistencia de un profesional de TI front-end.

La implementación de Quickview existente normalmente representa una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario almacena en déclencheur un elemento en la interfaz de usuario del sitio web.
1. El código front-end obtiene una URL de vista rápida basada en el elemento de interfaz de usuario activado en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos de vista rápida o el contenido correspondiente al código front-end.
1. El código front-end carga los datos de vista rápida o el contenido.
1. De forma opcional, el código front-end convierte los datos de vista rápida cargados en una representación de HTML.
1. El código front-end muestra un cuadro de diálogo o panel modal y procesa el contenido de HTML en la pantalla para el usuario final.

Estas llamadas no representan llamadas de API públicas independientes a las que la lógica de página web puede llamar desde un paso arbitrario. En su lugar, es una llamada encadenada en la que cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Al mismo tiempo que el banner de carrusel reemplaza el paso 1 y parcialmente el paso 2, cuando un usuario toque un punto interactivo o un mapa de imagen dentro del banner de carrusel, el visualizador se encargará de esta interacción. El visor devuelve un evento a la página web que contiene todos los datos de puntos interactivos o mapas de imagen añadidos anteriormente.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por el titular del carrusel.
* Construye una URL de vista rápida basada en los datos de puntos interactivos o mapas de imagen.
* Déclencheur el proceso de cargar la vista rápida desde el backend y procesarla en la pantalla para mostrarla.

El código incrustado devuelto por Experience Manager Assets ya tiene un controlador de eventos listo para usar que se comenta.

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio con el código específico de la página web en particular.

El proceso de construir la URL de vista rápida es opuesto al proceso utilizado para identificar las variables de puntos interactivos y mapas de imagen que se trataron anteriormente.

Ver [Identificar variables de puntos interactivos y mapas de imagen](#identifying-hotspot-and-image-map-variables).

El último paso para almacenar en déclencheur la URL de vista rápida y activar el panel de vista rápida muy probablemente requiera la asistencia de una persona de TI front-end de su departamento de TI. Tienen los conocimientos necesarios para saber cómo almacenar en déclencheur con precisión la implementación de Quickview desde el paso adecuado, teniendo una URL de Quickview lista para usar.

## Creación de ventanas emergentes personalizadas con Quickview {#using-quickviews-to-create-custom-pop-ups}

Ver [Crear ventanas emergentes personalizadas con Quickview](/help/assets/custom-pop-ups.md).
