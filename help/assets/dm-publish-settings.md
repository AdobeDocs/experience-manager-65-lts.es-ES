---
title: Configuración del programa de instalación de publicación de Dynamic Media para el servidor de imágenes
description: Obtenga información sobre cómo configurar el programa de instalación de publicación de Dynamic Media para el servidor de imágenes para poder publicar recursos. También puede probar los recursos antes de hacerlos públicos.
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
solution: Experience Manager, Experience Manager Assets
source-git-commit: 54523e507ae818f87032929cf3d28dc34a45eb34
workflow-type: tm+mt
source-wordcount: '3364'
ht-degree: 0%

---

# Configuración del programa de instalación de publicación de Dynamic Media para el servidor de imágenes

Las opciones de configuración de publicación de Dynamic Media solo están disponibles si se cumplen los siguientes criterios:

* Está ejecutando Dynamic Media en modo Scene7. Consulte [Habilitar Dynamic Media en modo Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Tiene una *configuración de Dynamic Media* **[!UICONTROL existente]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager. Consulte [Crear una configuración de Dynamic Media en Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Es administrador del sistema de Experience Manager con privilegios de administrador.

Los desarrolladores y programadores de sitios web con experiencia tienen la intención de utilizar la Configuración de publicación de Dynamic Media. Adobe Dynamic Media recomienda que los usuarios que cambien la configuración de publicación estén familiarizados con Adobe Dynamic Media, las normas y convenciones de protocolo HTTP y la tecnología básica de creación de imágenes.

La página Configuración de publicación de Dynamic Media establece la configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor de Adobe Dynamic Media envía un recurso según una configuración predeterminada que se configuró en la página Configuración de publicación de Dynamic Media.

Consulte también [Opcional: configuración de Dynamic Media: configuración del modo Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) para ver más tareas de configuración opcionales.

>[!NOTE]
>
>¿Desea actualizar de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager? La página [Configuración general](/help/assets/dm-general-settings.md) y la página Configuración de publicación de Dynamic Media se rellenan previamente con los valores tomados de su cuenta de Dynamic Media Classic. Las excepciones son todos los valores enumerados en el área **[!UICONTROL Opciones de carga predeterminadas]** de la página Configuración general. Estos valores ya están en Experience Manager. Como tal, cualquier cambio que realice en **[!UICONTROL Opciones de carga predeterminadas]** en cualquiera de las cinco pestañas, a través de la interfaz de usuario de Experience Manager, se reflejará en Dynamic Media, no en Dynamic Media Classic. El resto de la configuración y los valores de la página [Configuración general](/help/assets/dm-general-settings.md) y la página Configuración de publicación se mantienen entre Dynamic Media Classic y Dynamic Media en Experience Manager.

**Para configurar el servidor de imágenes de instalación de publicación de Dynamic Media:**

1. En el modo Autor de Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, haga clic en el icono Herramientas y, a continuación, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Configuración de publicación de Dynamic Media]**.
1. En la página Servidor de imágenes, en la lista desplegable, elija el contexto de publicación para establecer la configuración predeterminada para enviar imágenes desde los servidores de imágenes.

| Contexto de publicación | Descripción |
| --- | --- |
| Servicio de imágenes | Especifica el contexto para la configuración de publicación. |
| Probar servicio de imágenes | Especifica el contexto para probar la configuración de publicación.<br>Solo para las nuevas cuentas de Dynamic Media, el campo predeterminado **[!UICONTROL Dirección del cliente]** se establece en `127.0.0.1` automáticamente.<br>Consulte [Probar recursos antes de hacerlos públicos](#test-assets-before-making-public). |

1. Utilice las cinco pestañas para configurar el contexto de publicación predeterminado.

   * Ficha [Seguridad](#security-tab)
   * Pestaña [Administración de catálogos](#catalog-management-tab)
   * Pestaña [Atributos de solicitud](#request-attributes-tab)
   * [Pestaña Atributos de miniatura comunes](#common-thumbnail-attributes-tab)
   * Pestaña [Atributos de administración de color](#color-management-attributes-tab)

   ![Página de configuración de publicación de Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Página de configuración de publicación de Dynamic Media, con la ficha **[!UICONTROL Solicitar atributos]**&#x200B;seleccionada.*<br><br>

1. Cuando termine, cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Guardar]**.

## Pestaña Seguridad {#security-tab}

>[!NOTE]
>
>No se admite la configuración de seguridad en el contexto de publicación *Servicio de imágenes*.

Cuando *Probar servicio de imágenes* está establecido como contexto de publicación, puede establecer la siguiente configuración de seguridad:

**[!UICONTROL Dirección del cliente]**: le permite especificar una o más direcciones IP o intervalos de direcciones IP. Cuando se especifica, se rechazan las solicitudes a este catálogo de imágenes que se originan desde un cliente con una dirección IP no incluida. Esta regla se aplica tanto a la entrega de imágenes como a las imágenes procesadas.

![Ficha de seguridad &#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*La ficha de seguridad que muestra el campo &quot;Permitir&quot; de IP.*

## Pestaña Administración de catálogos {#catalog-management-tab}

**[!UICONTROL Ruta del archivo de definición de conjunto de reglas]**: especifica el archivo que contiene las definiciones del conjunto de reglas para el catálogo de imágenes.

Consulte también el parámetro [RuleSetFile](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
>
>Si su cuenta de Dynamic Media Classic tiene seleccionada una **[!UICONTROL ruta de acceso al archivo de definición del conjunto de reglas]** en **[!UICONTROL Configuración]** > **[!UICONTROL Aplicación]** > **[!UICONTROL Configuración de publicación]**, Experience Manager recupera el archivo. Su cuenta de Dynamic Media recupera el archivo de Dynamic Media Classic. A continuación, el archivo se almacena y se pone a disposición en este campo al abrir la página **[!UICONTROL Configuración de publicación de Dynamic Media]** por primera vez.

## Pestaña Atributos de solicitud {#request-attributes-tab}

Estos ajustes pertenecen al aspecto predeterminado de las imágenes.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Límite de tamaño de imagen de respuesta]** | Requerido.<br>Solo para las nuevas cuentas de Dynamic Media, los límites de tamaño predeterminados se establecen automáticamente en Anchura: `3000` y Altura: `3000` tanto para el servicio de imágenes **[!UICONTROL como para el servicio de imágenes de prueba]**&#x200B;**[!UICONTROL 6&rbrace;.]**<br>Especifica la anchura y altura máximas para la imagen de respuesta que se devuelve al cliente. El servidor devuelve un error si una solicitud genera una imagen de respuesta con una anchura, altura o ambas superiores a esta configuración.<br>Consulte también el parámetro [MaxPix](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de ofuscación de solicitud]** | Habilite esta opción si desea aplicar la codificación base64 a solicitudes válidas.<br>Consulte también el parámetro [RequestObfuscation](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Modo de bloqueo de solicitud]** | Habilite esta opción si desea que las solicitudes incluyan un bloqueo hash simple.<br>Consulte también el parámetro [RequestLock](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de solicitud predeterminados]** | |
| **[!UICONTROL Sufijo de archivo de imagen predeterminado]** | Requerido.<br>Extensión de archivo de datos predeterminada que se anexa a los valores de campo de la ruta de acceso y la ruta de máscara del catálogo si la ruta no incluye un sufijo de archivo.<br>Consulte también el parámetro [DefaultExt](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Nombre de fuente predeterminada]** | Especifica la fuente que se utilizará en caso de que la solicitud de capa de texto no proporcione ninguna. Si se especifica, debe ser un valor de nombre de fuente válido en el mapa de fuentes de este catálogo de imágenes o en el mapa de fuentes del catálogo predeterminado.<br>Consulte también el parámetro [DefaultFont](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Imagen predeterminada]** | Se devuelve una imagen predeterminada en respuesta a una solicitud donde la imagen solicitada no se encuentra.<br>Consulte también el parámetro [DefaultImage](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage) en la Guía de referencia de visores de Dynamic Media.<br>**NOTA**: Si su cuenta de Dynamic Media Classic tiene seleccionada una **[!UICONTROL imagen predeterminada]** en **[!UICONTROL Configuración]** > **[!UICONTROL Aplicación]** > **[!UICONTROL Configuración de publicación]**, en el grupo **[!UICONTROL Atributos de solicitud predeterminados]**, Experience Manager recupera el archivo. A continuación, el archivo se almacena y se pone a disposición en este campo cuando abre la página **[!UICONTROL Configuración de publicación de Dynamic Media]** por primera vez. |
| **[!UICONTROL Modo de imagen predeterminado]** | Cuando el cuadro deslizante está habilitado (deslizador a la derecha), la **[!UICONTROL imagen predeterminada]** reemplaza cada capa que falta en la imagen de origen con la imagen predeterminada y devuelve el compuesto de la forma habitual. Cuando el cuadro deslizante está desactivado (deslizador a la izquierda), la imagen predeterminada reemplaza toda la imagen compuesta, incluso si la imagen que falta es solo una de varias capas.<br>Consulte también el parámetro [DefaultImageMode](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de vista predeterminado]** | Requerido.<br>Solo para las nuevas cuentas de Dynamic Media, los tamaños de vista predeterminados se establecen automáticamente en Anchura: `1280` y Altura: `1280` tanto para el **[!UICONTROL servicio de imágenes]** como para el **[!UICONTROL servicio de imágenes de prueba]**.<br>El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que la solicitud especifique el tamaño de vista explícitamente con `wid=`, `hei=` o `scl=`.<br>Consulte también el parámetro [DefaultPix](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tamaño de miniatura predeterminado]** | Requerido.<br>Se usó en lugar del atributo **[!UICONTROL Tamaño de vista predeterminado]** para las solicitudes de miniaturas (`req=tmb`). El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que una solicitud de miniatura (`req=tmb`) especifique el tamaño explícitamente con `wid=`, `hei=` o `scl=`.<br>Consulte también el parámetro [DefaultThumbPix](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Color de fondo predeterminado]** | Especifica el valor de RGB que se utiliza para rellenar las áreas de la imagen de respuesta que no contengan datos de imagen reales.<br>Consulte también el parámetro [BkgColor](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Atributos de codificación de JPEG]** |  |
| **[!UICONTROL Calidad]** | <br>Especifica los atributos predeterminados para las imágenes de respuesta de JPEG.<br>Solo para las nuevas cuentas de Dynamic Media, los valores predeterminados de **[!UICONTROL Calidad]** se establecen automáticamente en `80` tanto para el servicio de imágenes **[!UICONTROL como para el servicio de imágenes de prueba]**&#x200B;**[!UICONTROL 7&rbrace;.]**<br>Este campo está definido en el intervalo de 1 a 100.<br>Consulte también el parámetro [JpegQuality](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Disminución cromática de resolución]** | Habilite o deshabilite la disminución de resolución cromática, que utilizan los codificadores de JPEG. |
| **[!UICONTROL Modo de remuestreo predeterminado]** | Especifica los atributos predeterminados de remuestreo e interpolación que se utilizarán para escalar los datos de imagen. Utilícelo cuando `resMode` no se especifique en una solicitud.<br>Solo para las nuevas cuentas de Dynamic Media, los modos de remuestreo predeterminados se establecen automáticamente en `Sharp2` tanto para **[!UICONTROL servicio de imágenes]** como para **[!UICONTROL servicio de imágenes de prueba]**.<br>Consulte también el parámetro [ResMode](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode) en la Guía de referencia de visores de Dynamic Media. |

## Pestaña Atributos de miniatura comunes {#common-thumbnail-attributes-tab}

Estos ajustes se refieren al aspecto y la alineación predeterminados de las imágenes en miniatura.

| Configuración | Descripción |
| --- | --- |
| **[!UICONTROL Color de fondo predeterminado para la miniatura]** | Especifica el valor de RGB que se utiliza para rellenar el área de una imagen en miniatura de salida que no contiene datos de imagen reales. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando el valor **[!UICONTROL Tipo de miniatura predeterminado]** está establecido en **[!UICONTROL Ajustar]** o **[!UICONTROL Textura]**.<br>Consulte también el parámetro [ThumbBkgColor](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación horizontal]** | Especifica la alineación horizontal de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por los valores `wid=` y `hei=`.<br>Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando el valor de **[!UICONTROL Tipo de miniatura predeterminado]** está establecido en **[!UICONTROL Ajuste]**.<br>Hay tres alineaciones horizontales para elegir: **[!UICONTROL Alineación central]**, **[!UICONTROL Alineación izquierda]** y **[!UICONTROL Alineación derecha]**.<br>Consulte también el parámetro [ThumbHorizAlign](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Alineación vertical]** | Especifica la alineación vertical de la imagen en miniatura en el rectángulo de imagen de respuesta especificado por los valores `wid=` y `hei=`. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando el valor **[!UICONTROL Tipo de miniatura predeterminado]** está establecido en **[!UICONTROL Ajuste]**.<br>Hay tres alineaciones verticales para elegir: **[!UICONTROL Alineación superior]**, **[!UICONTROL Alineación central]** y **[!UICONTROL Alineación inferior]**.<br>Consulte también el parámetro [ThumbVertAlign](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Duración predeterminada de la caché]** | Se proporciona un intervalo de caducidad predeterminado en horas en el caso de que el valor de catálogo Expiration no sea válido en un registro de catálogo determinado. Se establece en `-1` para que nunca caduque. <br>Consulte también el parámetro [Expiration](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Tipo de miniatura predeterminado]** | Se proporciona un valor predeterminado para el tipo de miniatura en el caso de que el valor de catálogo ThumbType no sea válido en un registro de catálogo determinado. Solo se usa para solicitudes de miniaturas (`req=tmb`).<br>Hay tres tipos de miniaturas para elegir: **[!UICONTROL Recortar]**, **[!UICONTROL Ajustar]** y **[!UICONTROL Textura]**.<br>Consulte también el parámetro [ThumbType](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Resolución de miniatura predeterminada]** | Se proporciona una resolución de objeto de miniatura predeterminada en el caso de que el valor de catálogo ThumbRes no sea válido en un registro de catálogo determinado. Solo se usa para solicitudes de miniaturas (`req=tmb`) y cuando la configuración **[!UICONTROL Tipo de miniatura predeterminado]** está establecida en **[!UICONTROL Textura]**.<br>Consulte también el parámetro [ThumbRes](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres) en la Guía de referencia de visores de Dynamic Media. |

## Pestaña Atributos de gestión de color {#color-management-attributes-tab}

Esta configuración determina qué perfiles de color ICC se utilizan para las imágenes.

**Interpretación de conversión de color**
Una interpretación de conversión de color permite anular la interpretación predeterminada de los perfiles de trabajo para determinar cómo se ajustan los colores de origen. Se utiliza cuando:

1. Uno de los perfiles ICC predeterminados es el espacio de color de destino de una conversión de color.
1. Este perfil caracteriza un dispositivo de salida, como una impresora o un monitor.
1. Y la interpretación especificada es válida para este perfil.

Las distintas intenciones de renderización utilizan reglas diferentes para determinar cómo se ajustan los colores de origen.

Consulte también el parámetro [IccRenderIntent](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent) en la Guía de referencia de visores de Dynamic Media.

>[!NOTE]
>
>En general, utilice la interpretación predeterminada para la configuración de color seleccionada, que Adobe ha probado para cumplir con los estándares del sector. Por ejemplo, si elige una configuración de color para Norteamérica o Europa, la interpretación de conversión de color predeterminada es **[!UICONTROL Colorimétrico relativo]**. Si elige una configuración de color para Japón, la interpretación de la conversión de color predeterminada es **[!UICONTROL Perceptual]**.

| Configuración | Características |
| --- | --- |
| **[!UICONTROL Espacio de color predeterminado CMYK]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos CMYK. Si se elige **[!UICONTROL Ninguno especificado]**, se deshabilita la administración de colores en este catálogo de imágenes cuando hay imágenes de origen CMYK. Todos los espacios de trabajo CMYK dependen del dispositivo, lo que significa que se basan en combinaciones reales de tinta y papel. Los espacios de trabajo CMYK suministrados por Adobe se basan en las condiciones estándar de impresión comercial.<br> Consulte también el parámetro [IccProfileCMYK](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado de escala de grises]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos de escala de grises. Si se elige **[!UICONTROL Ninguno especificado]**, se deshabilita la administración de colores en este catálogo de imágenes cuando hay imágenes con origen de escala de grises involucradas.<br>Consulte también el parámetro [IccProfileGray](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Espacio de color predeterminado de RGB]** | Especifica el nombre del perfil de color ICC que se utilizará como perfil de trabajo para los datos de RGB. Si se elige **[!UICONTROL Ninguno especificado]**, se deshabilita la administración de colores en este catálogo de imágenes cuando hay imágenes de orígenes RGB. En general, es mejor elegir **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, en lugar del perfil de un dispositivo específico (como un perfil de monitor). Se recomienda **[!UICONTROL sRGB]** al preparar imágenes para la web o dispositivos móviles, ya que define el espacio de color del monitor estándar utilizado para ver imágenes en la web. **[!UICONTROL sRGB]** también es una buena opción cuando se trabaja con imágenes de cámaras digitales de consumo, ya que la mayoría de estas cámaras utilizan sRGB como espacio de color predeterminado.<br>Consulte también el parámetro [IccProfileRBG](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb) en la Guía de referencia de visores de Dynamic Media. |
| **[!UICONTROL Interpretación de conversión de color]** | **[!UICONTROL Perceptual]**: intenta preservar la relación visual entre los colores para que se perciba como natural para el ojo humano, aunque los valores de color en sí mismos puedan cambiar. Esta intención es adecuada para imágenes fotográficas con muchos colores fuera de gama. Esta configuración es la interpretación estándar para la industria de impresión japonesa. |
|  | **[!UICONTROL Colorimétrico relativo]**: compara el resaltado extremo del espacio de color de origen con el del espacio de color de destino y cambia todos los colores en consecuencia. Los colores fuera de gama se desplazan al color reproducible más cercano en el espacio de color de destino. Colorimétrico relativo conserva más de los colores originales en una imagen que Perceptual. Esta configuración es la interpretación estándar de la impresión en Norteamérica y Europa. |
|  | **[!UICONTROL Saturación]**: intenta producir colores vivos en una imagen a expensas de la precisión del color. Esta interpretación es adecuada para gráficos empresariales como gráficos o gráficos, donde los colores saturados brillantes son más importantes que la relación exacta entre los colores. |
|  | **[!UICONTROL Colorimétrico absoluto]**: deja sin cambios los colores que se encuentran dentro de la gama de destino. Los colores fuera de gama se recortan. No se aplica ninguna escala de colores al punto blanco de destino. Esta intención tiene como objetivo mantener la precisión del color a expensas de preservar las relaciones entre los colores y es adecuada para la prueba para simular la salida de un dispositivo en particular. Esta intención es útil para obtener una vista previa del modo en que el color del papel afecta a los colores impresos. |

## Pruebe los recursos antes de hacerlos públicos {#test-assets-before-making-public}

Las pruebas seguras le ayudan a definir un entorno de prueba seguro y a crear una solución sólida de empresa a empresa, basada en un conjunto configurable de direcciones IP e intervalos. Esta funcionalidad le permite hacer coincidir las implementaciones de Dynamic Media de Adobe con la arquitectura del sistema empresarial y de administración de contenido.

Con Pruebas seguras, puede obtener una vista previa de la versión de ensayo del sitio web con contenido sin publicar.

Si lo desea, cree un entorno de ensayo en lugar de publicar los recursos por los siguientes motivos:

* Previsualizar sitios web antes del lanzamiento público (sitio web de ensayo).
* Proporcione recursos que requieran acceso restringido, como catálogos electrónicos que muestran precios en una aplicación web B2B.
* Utilice recursos detrás de un cortafuegos como parte de un sistema de gestión de la información sobre productos, una aplicación de servicio al cliente, un sitio de formación, etc.

>[!NOTE]
>
>Prueba segura no afecta al acceso a Adobe Dynamic Media Classic. La seguridad de Adobe Dynamic Media Classic sigue siendo coherente y requiere las credenciales habituales para acceder a Adobe Dynamic Media Classic y a los servicios web relacionados.

### Funcionamiento de las pruebas de seguridad {#how-test-assets-works}

La mayoría de las corporaciones manejan su Internet detrás de un cortafuegos. El acceso a Internet es posible a través de determinadas rutas y, por lo general, a través de un rango limitado de direcciones IP públicas.

Desde su red corporativa, puede averiguar su dirección IP pública usando sitios web como [https://www.whatismyip.com](https://www.whatismyip.com/) o solicitar esta información a su organización de TI corporativa.

Con las pruebas seguras, Adobe Dynamic Media establece un servidor de imágenes específico para entornos de ensayo o aplicaciones internas. Cualquier solicitud a este servidor comprueba la dirección IP de origen. Si la solicitud entrante no se encuentra dentro de la lista aprobada de direcciones IP, se devuelve una respuesta de error. El administrador de la empresa de Dynamic Media de Adobe configura la lista aprobada de direcciones IP para el entorno de prueba segura de su empresa.

Dado que la ubicación de la solicitud original debe confirmarse, el tráfico del servicio Prueba segura no se enruta a través de una red de distribución de contenido como el tráfico público del servidor de imágenes de Dynamic Media. Las solicitudes al servicio de pruebas seguras tienen una latencia ligeramente superior en comparación con los servidores de imágenes públicos de Dynamic Media.

Los recursos sin publicar están disponibles inmediatamente en los servicios de prueba segura, sin necesidad de publicarlos. De este modo, puede ejecutar una previsualización antes de que los recursos se publiquen en su servidor de imágenes público.

>[!NOTE]
>
>Los servicios de prueba segura utilizan el servidor de catálogos configurado con un contexto de publicación interno. Por lo tanto, si su empresa está configurada para publicar en pruebas seguras, cualquier recurso cargado en Adobe Dynamic Media estará disponible inmediatamente en los servicios de pruebas seguras. Esta funcionalidad se cumple independientemente de si los recursos se marcan para su publicación durante la carga.

Actualmente, los servicios de prueba segura admiten los siguientes tipos de recursos y funcionalidades:

* Imágenes.
* Viñetas (solicitudes del servidor de procesamiento).
* Los clientes deben solicitar explícitamente la compatibilidad con el servidor de procesamiento, que está disponible.
* Conjuntos, incluidos conjuntos de imágenes, catálogos electrónicos, conjuntos de procesamiento y conjuntos de medios.
* Visores de medios enriquecidos estándar de Adobe Dynamic Media.
* Páginas JSP de Dynamic Media OnDemand de Adobe.
* Contenido estático, como archivos PDF y vídeos servidos progresivamente.
* Streaming de vídeo HTTP.
* Flujo de vídeo progresivo.

Actualmente no se admiten los siguientes tipos de recursos y funcionalidades:

* Búsqueda en catálogo electrónico o información de Adobe Dynamic Media Classic
* Flujo de vídeo RTMP
* Web-to-print
* Servicios de UGC (contenido generado por el usuario)

  >[!IMPORTANT]
  >
  >A partir del 1 de mayo de 2023, los recursos UGC en Dynamic Media estarán disponibles para su uso hasta 60 días después de la fecha de carga. Después de 60 días, los recursos se eliminan.

  >[!NOTE]
  >
  >La compatibilidad con recursos de imagen vectorial UGC nuevos o existentes en Adobe Dynamic Media finalizó el 30 de septiembre de 2021.

### Prueba del servicio Secure Testing {#test-secure-testing-service}

Para asegurarse de que el servicio Prueba segura funciona según lo esperado, haga lo siguiente:

#### Prepare su cuenta

1. Póngase en contacto con el Servicio de atención al cliente de Adobe y solicite que habiliten las pruebas seguras en su cuenta.
1. En Adobe Experience Manager, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuración de publicación de Dynamic Media]**.
1. En la página Servidor de imágenes, en la lista desplegable **[!UICONTROL Contexto de publicación]**, seleccione **[!UICONTROL Probar servicio de imágenes]**.
1. Seleccione la ficha **[!UICONTROL Seguridad]**.
1. Para el filtro **[!UICONTROL Dirección del cliente]**, seleccione **[!UICONTROL Agregar]**.
1. En el campo **[!UICONTROL Dirección IP]**, escriba una dirección IP.
1. En el campo **[!UICONTROL Máscara]**, escriba una máscara de red.

   >[!NOTE]
   >
   >Si agrega más de una dirección IP y máscara de red, permite que *todas* las direcciones IP realicen llamadas de recurso y que todas aparezcan.

1. Realice una de las siguientes acciones:

   * Para agregar más direcciones IP, repita los tres pasos anteriores.
   * Continúe con el paso siguiente.

1. En la esquina superior derecha de la página Servidor de imágenes, seleccione **[!UICONTROL Guardar]**.
1. Cargue las imágenes que desee en su cuenta de Dynamic Media de Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Asegúrese de que algunas imágenes estén marcadas para publicación y otras no, y luego envíe el trabajo de publicación.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine el nombre de su servicio de pruebas seguras en **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En la página **[!UICONTROL Servidor]**, busque el nombre del servidor a la derecha de **[!UICONTROL Nombre del servidor publicado]**.

Póngase en contacto con el servicio de atención al cliente de Adobe si falta el nombre del servidor o si la URL del servidor no funciona.

#### Preparar variaciones de sitios web

Necesita dos variaciones de un sitio web que vincule los recursos publicados y no publicados:

* Versión pública: vincule recursos con la sintaxis tradicional de la URL de Dynamic Media de Adobe.
* Versión de ensayo: vincule los recursos con la misma sintaxis pero con el nombre del sitio de prueba segura.

#### Ejecutar las pruebas

Realice las siguientes pruebas:

1. Compruebe si los recursos son visibles desde la red corporativa.

   Desde la red corporativa identificada por el intervalo de direcciones IP previamente definido, la versión de ensayo del sitio web muestra todas las imágenes, estén marcadas para publicación o no. Como tal, puede realizar pruebas sin poner accidentalmente las imágenes a disposición antes de la aprobación de la vista previa o el lanzamiento del producto.

   Confirme que la versión pública del sitio muestra los recursos publicados como se experimentó anteriormente con Adobe Dynamic Media.

1. Desde fuera de la red corporativa, compruebe que los recursos no publicados (es decir, sin marcar para publicación) estén protegidos frente al acceso de terceros.

   Acceda a su red desde el exterior (por ejemplo, desde su equipo doméstico o a través de una conexión 4G/5G) y, a continuación, compruebe que la versión pública del sitio muestre todos los recursos publicados, pero ninguno del contenido no publicado.

   Confirme que la versión de ensayo no muestra ningún recurso porque está accediendo al servicio de prueba segura desde una dirección IP no aprobada.
