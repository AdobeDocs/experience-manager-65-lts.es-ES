---
title: Uso de recursos 3D en Dynamic Media
description: Descubra cómo puede cargar, administrar, ver y distribuir recursos 3D en Dynamic Media como una experiencia envolvente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 2%

---

# Uso de recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media le permite cargar, gestionar, ver y distribuir recursos 3D como experiencias envolventes.

* Publicación en un solo clic (con **[!UICONTROL Publicación rápida]** en la barra de herramientas) de recursos 3D para generar una dirección URL.
* Compatibilidad optimizada para ver recursos 3D con el ajuste preestablecido de visualizador dimensional interactivo de alta calidad con tecnología Adobe Dimension.
* El componente 3D Media WCM permite añadir fácilmente recursos 3D a las páginas de Adobe Experience Manager Sites.

No se requiere ninguna configuración adicional para utilizar recursos 3D en Dynamic Media.

![Zapato en 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *Página de detalles de un zapato tridimensional.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D admitidos en Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos 3D.

Consulte también [formatos 3D compatibles](/help/assets/assets-formats.md).

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | Incluye los materiales y las texturas como un solo recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | *Sólo se admite la ingesta; no hay visualización ni interacción disponible.* USDZ es un formato 3D propietario que los dispositivos Safari y iOS pueden ver de forma nativa. |

>[!NOTE]
>
>El componente WCM de medios en 3D y la vista previa 3D de la página de detalles de un recurso no son compatibles con la última versión de Chrome (97.x). En su lugar, para trabajar con recursos 3D, utilice Firefox o Safari, o bien utilice una versión anterior de Chrome (96.x).

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle a poner en marcha rápidamente los recursos 3D en el modo Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Los recursos 3D no son compatibles con Dynamic Media (modo híbrido).

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que su administrador de Experience Manager ya haya habilitado y configurado los servicios en la nube de Dynamic Media en modo Dynamic Media - Scene7.

Consulte [ConfigurE Servicios de nube de Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) en Configuración de Dynamic Media - Modo Scene7 y [Solucionar problemas de Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).

1. **Cargar recursos 3D**

   * [Cargue sus recursos 3D para usarlos en Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formatos de archivo 3D compatibles para la carga en Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Administrar recursos 3D**

   * Organización y búsqueda de recursos 3D

      * [Organizar recursos digitales](/help/assets/organize-assets.md#organize-digital-assets).
      * [Buscar recursos 3D](/help/assets/search-assets.md).
      * [Use predicados personalizados para filtrar los resultados de búsqueda](/help/assets/search-assets.md#custompredicates).

   * Ver recursos 3D

      * [Ver e interactuar con recursos 3D](#viewing-three-d-assets).
      * [Administrar el ajuste preestablecido de visualizador dimensional](/help/assets/managing-viewer-presets.md).

   * Trabajo con metadatos de recursos 3D

      * [Administrar metadatos de recursos digitales](/help/assets/metadata.md).
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md).

1. **Publicar recursos 3D**

   * [Publicación de recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional](#alternate-publish-methods)

## Visualización e interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo ver recursos 3D e interactuar con ellos de dos formas diferentes: desde la página de detalles de recursos y desde el componente Medios 3D en Experience Manager Sites.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y recorrer el recurso 3D.

El tiempo que se tarda en abrir un recurso 3D en la vista de página Detalles del recurso depende de varios factores. Estos factores incluyen cosas como las siguientes:

* Ancho de banda al servidor.
* Latencias al servidor
* Complejidad de la imagen.

Además, las capacidades del equipo cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes a la hora de manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización 3D interactiva sea más fluida y favorable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visualizador dimensional en el Editor de ajustes preestablecidos de visualizador para practicar la navegación por un recurso 3D sin necesidad de cargar primero ningún archivo 3D. El ajuste preestablecido de visualizador dimensional tiene un recurso 3D integrado con el que puede interactuar.
>
>Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

## Ver e interactuar con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/previewing-assets.md).

**Para ver e interactuar con un recurso 3D desde la página de detalles de recursos:**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.

   Consulte [Cargar recursos 3D para usarlos en Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. Desde Experience Manager, en la página **[!UICONTROL Navegación]**, ve a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Cerca de la esquina superior derecha de la página, en la lista desplegable **[!UICONTROL Ver]**, seleccione **[!UICONTROL Vista de tarjeta]**.
1. Desplácese hasta un recurso 3D que desee ver.
1. Seleccione la tarjeta del recurso 3D.
1. En la página de vista de detalles del recurso 3D, realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gira tu cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica tu cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos + arrastre. |
   | **Haz zoom en tu cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Haga doble clic en. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

1. En la esquina superior derecha de la página, selecciona **[!UICONTROL Cerrar]** para volver a la página de Assets.

## Visualización e interacción de un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en modo **[!UICONTROL Editar]**, no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede usar la característica **[!UICONTROL Vista previa]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios en 3D.

>[!IMPORTANT]
>
>Solo podrá realizar esta tarea una vez que haya añadido un componente de medios 3D a una página web y le haya asignado un recurso 3D. Consulte [Agregar el componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page) y [Asignar un recurso 3D a un componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/previewing-assets.md).

**Para ver e interactuar con un recurso 3D dentro de un componente de medios 3D:**

1. Mientras una página web se encuentra en modo **[!UICONTROL Editar]**, realice una de las acciones siguientes:

   * Cerca de la parte superior derecha de la página, selecciona **[!UICONTROL Vista previa]** para ingresar al modo **[!UICONTROL Vista previa]**.
   * Eliminar `/editor.html` de la dirección URL de la página en el explorador.

   ![Recurso 3D que se muestra dentro del componente de medios 3D](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Un recurso 3D completamente interactivo tal como se muestra en el modo **[!UICONTROL Vista previa]**.

1. En el modo **[!UICONTROL Vista previa]**, realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gira tu cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica tu cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos + arrastre. |
   | **Haz zoom en tu cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Haga doble clic en. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

## Acerca del trabajo con el componente de medios en 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente de Dynamic Media 3D Media que puede utilizar en Adobe Experience Manager Sites para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Añadir el componente Medios 3D a la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: configuración del componente de medios en 3D](#configuring-the-three-d-component)
* [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

## Añadir el componente Medios 3D a la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]**.
1. Desplácese hasta la plantilla de página en la que desea activar el componente 3D y seleccione la plantilla.
1. Seleccione **[!UICONTROL Editar]** para poder abrir la plantilla.
1. Cerca de la parte superior derecha de la página, en el menú desplegable, seleccione el modo **[!UICONTROL Estructura]** si aún no está activo.

   ![estructura-componente-medios-3d](/help/assets/assets-dm/3d-media-component-structure.png)

1. Seleccione un área vacía en la región **[!UICONTROL Contenedor de diseño]** para seleccionarla y abrir su barra de herramientas asociada.
1. En la barra de herramientas, seleccione el icono **[!UICONTROL Directiva]** para abrir el **[!UICONTROL Editor de directivas]**.
1. En la sección **[!UICONTROL Propiedades]**, en la ficha **[!UICONTROL Componentes permitidos]**, desplácese hasta **[!UICONTROL Dynamic Media]**, expanda la lista y verifique **[!UICONTROL 3D Media]**.
1. Seleccione **[!UICONTROL Listo]** para guardar los cambios y cerrar el **[!UICONTROL Editor de directivas]**.

   Ahora puede colocar el componente Dynamic Media 3D Media en todas las páginas que utilicen esta plantilla.

## Adición del componente Medios 3D en una página web {#adding-the-three-d-media-component-to-a-web-page}

Si utiliza Experience Manager como sistema de gestión de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

Consulte también [Agregar recursos de Dynamic Media en las páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para agregar el componente multimedia 3D en una página web:**

1. Abra Experience Manager Sites y seleccione la página web a la que desea agregar el componente Dynamic Media 3D Media.
1. Seleccione el icono **[!UICONTROL Editar]** (lápiz) para poder abrir la página en el editor de páginas. Asegúrese de que el modo **[!UICONTROL Editar]** esté seleccionado cerca de la parte superior derecha de la página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. En la barra de herramientas, seleccione el icono Panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, seleccione el icono del signo más para abrir la lista **[!UICONTROL Componentes]**.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Arrastre el componente **[!UICONTROL Medios 3D]** de la lista **[!UICONTROL Componentes]** a la ubicación de la página donde desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

### Opcional: configuración del componente de medios en 3D {#configuring-the-three-d-component}

1. En el editor de páginas de Experience Manager Sites, seleccione el componente **[!UICONTROL Visor de medios en 3D]** que agregó anteriormente a la página.
1. Seleccione el icono **[!UICONTROL Configuration]** (llave inglesa) para abrir el cuadro de diálogo de configuración del componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. En el cuadro de diálogo Medios en 3D, en la lista desplegable Ajuste preestablecido de visor, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visor dimensional al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. En la esquina superior derecha, seleccione la marca de verificación para guardar los cambios.

## Asignar un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de agregar un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Agregar el componente multimedia 3D a una página web](#adding-the-three-d-media-component-to-a-web-page).

**Para asignar un recurso 3D al componente de medios 3D:**

1. En el editor de páginas de Experience Manager Sites, selecciona el icono **[!UICONTROL Assets]** para abrir **[!UICONTROL Assets]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo los tipos de archivos de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D que desee ver en la página que está editando.
1. Arrastre el recurso 3D desde el panel lateral de Assets y suéltelo en el componente **[!UICONTROL Medios 3D]** que agregó anteriormente a la página.

   ![Asignar recurso 3D al componente de medios 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Mientras una página web se encuentra en modo Experience Manager Sites **[!UICONTROL Edit]**, el componente 3D Media muestra el recurso 3D, pero no es posible interactuar con él. Para que el recurso sea interactivo, puede usar la característica **[!UICONTROL Vista previa]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios en 3D.

## Publicación de recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta varios formatos de archivo 3D compatibles como *contenido estático* en Dynamic Media. Contenido estático significa que puede cargar y publicar recursos 3D, pero no se admite *imágenes de variables* ni ajustes de imagen asociados con el recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La dirección URL del recurso 3D sigue la estructura habitual de direcciones URL de Dynamic Media. Sin embargo, no puede editar ningún parámetro en la dirección URL del recurso, a diferencia de los recursos de imagen tradicionales de Dynamic Media.

Consulte también [Obtener una dirección URL para un recurso estático](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

En la **[!UICONTROL vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de su fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si utiliza Experience Manager como WCM, utilice este método de publicación para agregar los recursos de Dynamic Media 3D directamente en la página web.

Consulte también [Publicar recursos de Dynamic Media](publishing-dynamicmedia-assets.md).

Consulte también [Publicar páginas](/help/sites-authoring/publishing-pages.md).

**Para publicar recursos estáticos de Dynamic Media 3D:**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL) para poder verlo en la página de detalles del recurso.
1. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

   ![publicación rápida de recursos en 3d](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Seleccione **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre de archivo del recurso 3D, seleccione **[!UICONTROL Representaciones]**.

   ![representaciones de recursos en 3d](/help/assets/assets-dm/3d-asset-renditions.png)

1. Seleccione **[!UICONTROL original]**. Cuando se publica un recurso 3D (o &quot;activado&quot;), el botón **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones siguientes para el recurso 3D:
   * El recurso 3D es un formato compatible (GLB, OBJ, STL y USDZ).
   * El recurso 3D se ha introducido en el sistema de producción de imágenes (IPS) de Dynamic Media.
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Seleccione **[!UICONTROL URL]** para poder mostrar la URL de producción directa del recurso 3D, que puede copiar y utilizar en páginas web.

### Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional {#alternate-publish-methods}

Use los dos métodos siguientes para publicar recursos de Dynamic Media 3D si *no* usa Experience Manager como WCM.

* **[!UICONTROL URL]** - Utilice **[!UICONTROL URL]** si está usando un sistema de administración de contenido web de terceros y desea vincular recursos de Dynamic Media 3D a sus páginas web mediante el visualizador dimensional.

  Ver [URL de vínculo a su aplicación web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incrustar]** - Usa **[!UICONTROL Incrustar]** cuando quieras ver un recurso de Dynamic Media 3D incrustado en una página web usando el visor Dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Incrustar]**.

  Ver [Incrustar vídeo, visor de imágenes o visor dimensional de Dynamic Media en una página web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
