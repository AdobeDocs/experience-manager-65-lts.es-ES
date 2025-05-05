---
title: Adición de recursos de Dynamic Media a las páginas
description: Para añadir la funcionalidad Dynamic Media a los recursos que utiliza en sus sitios web, puede agregar el componente Dynamic Media o Interactive Media directamente en la página.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 2%

---

# Adición de recursos de Dynamic Media a las páginas{#adding-dynamic-media-assets-to-pages}

Para agregar la funcionalidad Dynamic Media a los recursos que uses en tus sitios web, puedes agregar el componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Interactive Media]** directamente en la página. Active el modo **[!UICONTROL Diseño]** y habilite los componentes de Dynamic Media. A continuación, puede añadir estos componentes a la página y añadir recursos al componente. Los componentes de Dynamic Media y medios interactivos son inteligentes: saben si va a añadir una imagen o un vídeo y las opciones disponibles cambian en consecuencia.

Los recursos de Dynamic Media se agregan directamente a la página si utiliza Adobe Experience Manager como WCM.

>[!NOTE]
>
>Los mapas de imágenes están disponibles de forma predeterminada para los titulares de carrusel.

## Añadir un componente de Dynamic Media a una página {#adding-a-dynamic-media-component-to-a-page}

Añadir el componente [!UICONTROL Dynamic Media] o [!UICONTROL Interactive Media] a una página es lo mismo que agregar un componente a cualquier página. Los componentes [!UICONTROL Dynamic Media] y [!UICONTROL Interactive Media] se describen en detalle en las siguientes secciones.

Para agregar un componente o visualizador de Dynamic Media a una página:

1. En Experience Manager, abra la página donde desee agregar el componente Dynamic Media.
1. Si no hay ningún componente de Dynamic Media disponible, seleccione la regla en [!UICONTROL Sidekick] para entrar en el modo **[!UICONTROL Diseño]**.
1. Seleccione **[!UICONTROL Edit]** parsys.
1. Seleccione **[!UICONTROL Dynamic Media]** para que pueda hacer que los componentes de Dynamic Media estén disponibles.

   >[!NOTE]
   >
   >Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

1. Vuelva al modo **[!UICONTROL Editar]** haciendo clic en el icono de lápiz en [!UICONTROL Sidekick].
1. Arrastre el componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Interactive Media]** desde el grupo **[!UICONTROL Other]** de la barra de tareas a la página en la ubicación deseada.
1. Seleccione **[!UICONTROL Editar]** para que se abra el componente.
1. [Edite el componente](#dynamic-media-component) según sea necesario.
1. Seleccione **[!UICONTROL Aceptar]** para guardar los cambios.

## Componentes de Dynamic Media {#dynamic-media-components}

[!UICONTROL Dynamic Media] y [!UICONTROL Interactive Media] están disponibles en [!UICONTROL Sidekick] en **[!UICONTROL Dynamic Media]**. Utiliza el componente **[!UICONTROL Medios interactivos]** para cualquier recurso interactivo, como vídeo interactivo, imágenes interactivas o conjuntos de carrusel. Para el resto de los componentes de Dynamic Media, use el componente **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben seleccionarse en el modo Diseño antes de utilizar. [Una vez que estén disponibles en el modo de diseño](/help/sites-authoring/default-components-designmode.md), puede agregar los componentes a su página como lo haría con cualquier otro componente de Experience Manager.

### Componente de Dynamic Media {#dynamic-media-component}

El componente Dynamic Media es inteligente: según si agrega una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visualizador es adaptable. Es decir, el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores basados en HTML5.

>[!NOTE]
>
>Cuando agregue el componente [!UICONTROL Dynamic Media] y **[!UICONTROL Configuración de Dynamic Media]** esté en blanco o no pueda agregar un recurso correctamente, compruebe lo siguiente:
>
>* Ha [habilitado Dynamic Media](/help/assets/config-dynamic.md). Dynamic Media está desactivado de forma predeterminada.
>* La imagen tiene un archivo tiff piramidal. Las imágenes importadas antes de habilitar Dynamic Media no tienen un archivo tiff piramidal.
>

#### Al trabajar con imágenes {#when-working-with-images}

El componente [!UICONTROL Dynamic Media] le permite agregar imágenes dinámicas, incluidos conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos. Puede acercar y alejar la imagen y, si procede, girar una imagen dentro de un conjunto de giros o seleccionar una imagen de otro tipo de conjunto.

También puede configurar el ajuste preestablecido de visualizador, el ajuste preestablecido de imagen o el formato de imagen directamente en el componente. Para que una imagen sea adaptable, puede establecer los puntos de interrupción o aplicar un ajuste preestablecido de imagen adaptable.

![chlimage_1-72](assets/chlimage_1-72a.png)

Para editar la siguiente configuración de Dynamic Media, haga clic en **[!UICONTROL Editar]** en el componente y, a continuación, en la ficha **[!UICONTROL Configuración de Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la ficha **[!UICONTROL Avanzado]** con las propiedades **[!UICONTROL Anchura]** y **[!UICONTROL Altura]**.

**[!UICONTROL Ajuste preestablecido de visor]**: seleccione un ajuste preestablecido de visor existente en el menú desplegable. Si el ajuste preestablecido de visualizador que busca no está visible, debe hacerlo visible. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md). No puede seleccionar un ajuste preestablecido de visualizador si utiliza un ajuste preestablecido de imagen y a la inversa.

Esta opción solo está disponible si ve conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos. Los ajustes preestablecidos del visualizador mostrados son inteligentes. Es decir, solo aparecen los ajustes preestablecidos de visualizador relevantes.

**[!UICONTROL Ajuste preestablecido de imagen]**: seleccione un ajuste preestablecido de imagen existente en el menú desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte [Administrar ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md). No puede seleccionar un ajuste preestablecido de visualizador si utiliza un ajuste preestablecido de imagen y a la inversa.

Esta opción no está disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Modificadores de imagen]**: puede cambiar los efectos de imagen si proporciona comandos de imagen adicionales. Estos comandos se describen en [Administración de ajustes preestablecidos de imagen](/help/assets/managing-viewer-presets.md) y en la [Referencia de comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=es).

Esta opción no está disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Puntos de interrupción]**: si utiliza este recurso en un sitio adaptable, debe agregar los puntos de interrupción de la página. Los puntos de interrupción de imagen están separados por comas (,). Esta opción funciona cuando no hay altura o anchura definida en un ajuste preestablecido de imagen.

Esta opción no está disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

Puede editar las [!UICONTROL configuraciones avanzadas] siguientes haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Título]**: cambie el título de la imagen.

**[!UICONTROL Texto alternativo]**: agregue un título a la imagen para los usuarios que tengan los gráficos desactivados.

Esta opción no está disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL URL, Abrir en]**: puede configurar un recurso desde para abrir un vínculo. Establezca **[!UICONTROL URL]** y **[!UICONTROL Abrir en]** para indicar si desea que se abra en la misma ventana o en una nueva.

Esta opción no está disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

**[!UICONTROL Anchura y altura]**: escriba un valor en píxeles si desea que la imagen tenga un tamaño fijo. Si deja estos valores en blanco, el recurso se adaptará.

#### Al trabajar con vídeo {#when-working-with-video}

Utilice el componente **[!UICONTROL Dynamic Media]** para agregar vídeo dinámico a sus páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visualizador de vídeo para reproducir el vídeo en la página.

![chlimage_1-74](assets/chlimage_1-74a.png)

Puede editar la siguiente [!UICONTROL configuración de Dynamic Media] haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente con **[!UICONTROL Anchura]** y **[!UICONTROL Altura]** en la ficha **[!UICONTROL Avanzada]**.

**[!UICONTROL Ajuste preestablecido de visor]**: seleccione un ajuste preestablecido de visor de vídeo existente en el menú desplegable. Si el ajuste preestablecido de visualizador que busca no está visible, debe hacerlo visible. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

Puede editar la siguiente configuración de [!UICONTROL Advanced] haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Título]**: cambie el título del vídeo.

**[!UICONTROL Anchura y altura]**: escriba un valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si se dejan estos valores en blanco, se vuelve adaptable.

#### Proporcionar vídeo seguro {#how-to-delivery-secure-video}

En Experience Manager 6.2, al instalar [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), puede controlar si un vídeo se envía a través de una conexión SSL segura (HTTPS) o de una conexión no segura (HTTP). De forma predeterminada, el protocolo de entrega de vídeo se hereda automáticamente del protocolo de la página web en la que se incorpora. Si la página web se carga a través de HTTPS, el vídeo también se envía a través de HTTPS. Y a la inversa, si la página web está en HTTP, el vídeo se envía a través de HTTP. Normalmente, este comportamiento predeterminado funciona correctamente y no es necesario realizar ningún cambio en la configuración. Sin embargo, puede anular este comportamiento predeterminado. Anexe `VideoPlayer.ssl=on` al final de la ruta de acceso de una dirección URL o a la lista de otros parámetros de configuración del visor en un fragmento de código incrustado. Cualquiera de las acciones fuerza la entrega de vídeo segura.

Para obtener más información sobre la entrega de vídeo seguro y el uso del atributo de configuración `VideoPlayer.ssl` en la ruta de la URL, consulte [Entrega de vídeo seguro](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html?lang=es) en la Guía de referencia de visores. Además del visualizador de vídeo, hay una entrega de vídeo segura disponible para el visualizador de medios mixtos y el visualizador de vídeo interactivo.

### Componente de medios interactivo {#interactive-media-component}

El componente de medios interactivos es para aquellos recursos que tienen interactividad en ellos, como zonas interactivas o mapas de imagen. Si tiene una imagen interactiva, un vídeo interactivo o un banner de carrusel, use el componente **[!UICONTROL Medios interactivos]**.

El componente [!UICONTROL Medios interactivos] es inteligente; dependiendo de si agrega una imagen o un vídeo, tiene varias opciones. Además, el visualizador es adaptable. Es decir, el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores basados en HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Puede editar la siguiente configuración de **[!UICONTROL General]** haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Ajuste preestablecido de visor]**: seleccione un ajuste preestablecido de visor existente en el menú desplegable. Si el ajuste preestablecido de visualizador que busca no está visible, debe hacerlo visible. Los ajustes preestablecidos del visor deben publicarse para poder utilizarse. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

**[!UICONTROL Título]**: cambie el título del vídeo.

**[!UICONTROL Anchura y altura]**: escriba un valor en píxeles si desea que el vídeo tenga un tamaño fijo. Si se dejan estos valores en blanco, se vuelve adaptable.

Puede editar la siguiente configuración de **[!UICONTROL Agregar al carro]** haciendo clic en **[!UICONTROL Editar]** en el componente.

**[!UICONTROL Mostrar recurso del producto]**: este valor está seleccionado de forma predeterminada. El recurso de producto muestra una imagen del producto tal como se define en el módulo de Commerce. Desactive la marca de verificación para no mostrar el recurso del producto.

**[!UICONTROL Mostrar precio del producto]**: este valor está seleccionado de forma predeterminada. El precio del producto muestra el precio del artículo tal como se define en el módulo Commerce. Desactive la marca de verificación para no mostrar el precio del producto.

**[!UICONTROL Mostrar formulario de productos]**: de forma predeterminada, este valor no está seleccionado. El formulario de producto incluye cualquier variante de producto, como tamaño y color. Desactive la marca de verificación para no mostrar las variantes del producto.
