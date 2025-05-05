---
title: Comprender los conceptos de metadatos
description: Obtenga información acerca de la necesidad de y los tipos de metadatos que facilitan la categorización y organización de los recursos.
contentOwner: AG
role: User, Admin
feature: Metadata
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 7%

---

# Comprender los conceptos de metadatos {#why-we-need-metadata}

Los metadatos son datos sobre datos. A este respecto, los datos hacen referencia a su recurso digital, por ejemplo, una imagen. Los metadatos son esenciales para una administración eficaz de los recursos.

Los metadatos son la recopilación de todos los datos disponibles para un recurso, pero que no están necesariamente contenidos en esa imagen. Algunos ejemplos de metadatos son los siguientes:

* Nombre del recurso.
* Fecha y hora de la última modificación.
* Tamaño del recurso tal como se almacenó en el repositorio.
* Nombre de la carpeta en la que se encuentra.
* Recursos relacionados o etiquetas aplicadas.

Las anteriores son las propiedades de metadatos básicas que [!DNL Experience Manager] puede administrar para los recursos, lo que permite a los usuarios ver todos los recursos. Por ejemplo, ordenar recursos por fecha de última modificación es útil cuando se intenta descubrir recursos añadidos recientemente.

Puede añadir más datos de alto nivel a los recursos digitales, por ejemplo:

* Tipo de recurso (imagen, vídeo, clip de audio o documento).
* Propietario del recurso.
* Título del recurso.
* Descripción del recurso.
* Etiquetas asignadas a un recurso.

Más metadatos le ayudan a categorizar los recursos y son útiles a medida que aumenta la cantidad de información digital. Es posible administrar algunos cientos de archivos basados únicamente en los nombres de archivo. Sin embargo, este enfoque no es escalable. Se queda corto cuando aumenta el número de personas involucradas y el número de recursos administrados.

Con la adición de metadatos, el valor de un recurso digital aumenta, ya que pasa a ser:

* Más accesible: los sistemas y los usuarios pueden encontrarlo fácilmente.
* Más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades más fácilmente y aplicarles cambios.
* Completado: el recurso lleva más información y contexto con más metadatos.

Por estos motivos, [!DNL Assets] le proporciona los medios adecuados para crear, administrar e intercambiar metadatos para sus recursos digitales.

## Tipos de metadatos {#types-of-metadata}

Los dos tipos básicos de metadatos son los metadatos técnicos y los metadatos descriptivos.

Los metadatos técnicos son útiles para aplicaciones de software que tratan con recursos digitales y no deben mantenerse manualmente. [!DNL Experience Manager Assets] y otro software determinan automáticamente los metadatos técnicos, que pueden cambiar cuando se modifica el recurso. Los metadatos técnicos disponibles de un recurso dependen en gran medida del tipo de archivo del recurso. Algunos ejemplos de metadatos técnicos son los siguientes:

* Tamaño de un archivo.
* Dimensiones (altura y anchura) de una imagen.
* Velocidad de bits de un archivo de audio o vídeo.
* Resolución (nivel de detalle) de una imagen.

Los metadatos descriptivos son metadatos relacionados con el dominio de aplicación, por ejemplo, el negocio del que proviene un recurso. Los metadatos descriptivos no se pueden determinar automáticamente. Se crea de forma manual o semiautomática. Por ejemplo, una cámara con GPS puede rastrear automáticamente la latitud y longitud y añadir geotag a la imagen.

El coste de crear manualmente información descriptiva de metadatos es elevado. Por lo tanto, se establecen estándares para facilitar el intercambio de metadatos entre sistemas de software y organizaciones. [!DNL Experience Manager Assets] admite todos los estándares relevantes para la administración de metadatos.

## Estándares de codificación {#encoding-standards}

Existen varias formas de incrustar metadatos en los archivos. Se admite una selección de estándares de codificación:

* XMP: usado por [!DNL Assets] para almacenar los metadatos extraídos dentro del repositorio.
* ID3: para archivos de audio y vídeo.
* EXIF: para archivos de imagen.
* Otro/Heredado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) es un estándar abierto que utiliza [!DNL Experience Manager Assets] para toda la administración de metadatos. El estándar ofrece codificación de metadatos universal que puede incrustarse en todos los formatos de archivo. Adobe y otras empresas admiten el estándar XMP, ya que proporciona un modelo de contenido enriquecido. Los usuarios del estándar XMP y de [!DNL Experience Manager Assets] tienen una potente plataforma sobre la cual construir. Para obtener más información, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Los datos almacenados en estas etiquetas ID3 se muestran cuando reproduce un archivo de audio digital en el equipo o en un reproductor MP3 portátil.

Las etiquetas ID3 están diseñadas para el formato de archivo MP3. Información adicional sobre los formatos:

* Las etiquetas ID3 funcionan en archivos MP3 y mp3PRO.
* WAV no tiene etiquetas.
* WMA tiene etiquetas propietarias que no permiten la implementación de código abierto.
* Ogg Vorbis utiliza comentarios Xiph incrustados en el contenedor Ogg.
* AAC utiliza un formato de etiquetado propio.

### EXIF {#exif}

El formato de archivo de imagen intercambiable (Exif) es el formato de metadatos más utilizado en la fotografía digital. Proporciona una forma de incrustar un vocabulario fijo de propiedades de metadatos en muchos formatos de archivo, como JPEG, TIFF, RIFF y WAV. EXIF almacena los metadatos como pares de un nombre y un valor de metadatos. Estos pares de nombre-valor de metadatos también se denominan etiquetas, no deben confundirse con el etiquetado de [!DNL Experience Manager]. Las cámaras digitales modernas crean metadatos EXIF y el software gráfico moderno lo admite. El formato EXIF es el denominador común más bajo para la administración de metadatos, especialmente para imágenes.

Una limitación importante de EXIF es que algunos formatos de archivo de imagen populares, como BMP, GIF o PNG, no lo admiten.

Los campos de metadatos definidos por EXIF suelen ser de naturaleza técnica y su uso para la gestión descriptiva de metadatos es limitado. Por este motivo, [!DNL Experience Manager Assets] ofrece la asignación de propiedades EXIF en [esquemas de metadatos comunes](metadata-schemas.md) y en [XMP](xmp-writeback.md).

### Otros metadatos {#other-metadata}

Otros metadatos que se pueden incrustar de los archivos son [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

## Comprender los esquemas de metadatos {#metadata-schemata}

Los esquemas de metadatos son conjuntos predefinidos de definiciones de propiedades de metadatos que se pueden utilizar en diversas aplicaciones. Las propiedades siempre están asociadas a un recurso, lo que significa que las propiedades están &quot;alrededor&quot; del recurso.

También puede diseñar sus propios esquemas de metadatos si no existe ninguno que se ajuste a sus necesidades. No duplique la información existente. Dentro de una organización, la separación de esquemas facilita el uso compartido de metadatos. [!DNL Experience Manager] le proporciona una lista predeterminada de los esquemas de metadatos más populares. La lista le ayuda a poner en marcha su estrategia de metadatos y a elegir rápidamente las propiedades de metadatos que necesite.

A continuación se enumeran los esquemas de metadatos admitidos.

### Metadatos estándar {#standard-metadata}

* DC - [!DNL Dublin Core] es un conjunto de metadatos importante y ampliamente utilizado.
* DICOM - Imágenes digitales y comunicaciones en medicina.
* `Iptc4xmpCore` y `iptc4xmpExt` - International Press Communications Standard contiene muchos metadatos específicos de temas.
* RDF, Resource Description Framework, para metadatos web semánticos genéricos.
* XMP: [!DNL Extensible Metadata Platform].
* `xmpBJ` - Oferta de trabajo básica.

### Metadatos específicos de la aplicación {#application-specific-metadata}

Los metadatos específicos de la aplicación incluyen metadatos técnicos y descriptivos. Si utiliza estos metadatos, es posible que otras aplicaciones no puedan utilizarlos. Por ejemplo, es posible que una aplicación de procesamiento de imágenes diferente no pueda acceder a los metadatos de [!DNL Adobe Photoshop]. Puede crear un paso del flujo de trabajo que cambie una propiedad específica de la aplicación a una propiedad estándar.

* ACDSee: metadatos administrados por el programa [!DNL ACDSee]. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Utilizado por [!DNL Experience Manager Assets].
* DAM: Utilizado por [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] es una colección de herramientas para la administración de metadatos y archivos para los sistemas operativos Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/es/camera-raw/using/introduction-camera-raw.html).
* LR: [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto and MP - Microsoft Photo.
* PDF y PDF/X.
* Photoshop y psAux: [!DNL Adobe Photoshop].

### Metadatos de Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Sistema universal de licencias de imágenes](https://www.useplus.com).
* PRISM: [Requisitos de publicación para metadatos estándar del sector](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* PRL - PRISM Rights Language.
* PUR - Derechos de uso de PRISM.
* `xmpPlus`: integración de PLUS con XMP.

### Metadatos específicos de fotografía {#photography-specific-metadata}

* Exif - Información técnica de la cámara, incluyendo la posición GPS.
* CRS: esquema [!DNL Camera Raw].
* `iptc4xmpCore` y `iptc4xmpExt`.
* TIFF: metadatos de imagen (no solo para imágenes de TIFF).

### Metadatos específicos de impresión {#print-specific-metadata}

* PDF y PDF/X: aplicaciones de Adobe PDF y de terceros.
* PRISM: [Requisitos de publicación para metadatos estándar del sector](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* XMP: [!DNL Extensible Metadata Platform].
* `xmpPG`: metadatos de XMP para texto paginado.

### Metadatos específicos de medios múltiples {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Administración de medios.

## Referencia de esquemas de metadatos {#metadata-schemata-reference}

La siguiente referencia incluye información sobre un esquema de metadatos determinado (en orden alfabético) y una lista de propiedades y sus definiciones.

### Dublin Core {#dublin-core}

Los metadatos principales de Dublín proporcionan un conjunto estandarizado de convenciones para describir recursos que facilitan su búsqueda. En [!DNL Assets], Dublin Core describe recursos digitales, incluidos vídeo, sonido, imágenes y documentos.

El conjunto simple de elementos de metadatos principales de Dublín (DCMES) contiene 15 elementos de metadatos, tal como se indica en la siguiente tabla. Cada elemento principal de Dublín es opcional y se puede repetir. Puede agregar o eliminar información de metadatos principales de Dublín como lo haría para metadatos específicos de tipos de medios.

Además del DCMES, existen otros elementos de metadatos creados por la Iniciativa principal de Dublín. Consulte la [Iniciativa principal de Dublín](https://dublincore.org/) para obtener más información.

| Propiedad | Descripción |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| colaborador | La persona o empresa responsable de realizar contribuciones al contenido. |
| cobertura | La ubicación geográfica o el período de tiempo que cubre el recurso. |
| creador | La persona o compañía responsable de la creación del contenido. |
| fecha | Fecha o período de tiempo asociado al recurso. |
| descripción | Más información sobre el recurso. |
| formato | El formato de archivo, el medio físico o las dimensiones del recurso. [!DNL Experience Manager] usa `dc:format` para denotar el tipo MIME del recurso. |
| identificador | Una referencia única al recurso. |
| language | El idioma del recurso (por ejemplo, `en` para inglés). |
| editor | La persona o compañía responsable de poner a disposición el recurso. |
| relation | Un recurso relacionado. |
| derechos | Información sobre quién tiene derechos sobre este recurso. |
| origen | Un recurso relacionado del que se deriva el recurso. |
| asunto | El tema del recurso. |
| Título | Un nombre para el recurso. |
| tipo | La naturaleza o el género del recurso. |

### IPTC {#iptc}

El International Press Telecommunications Council (IPTC) es un consorcio de agencias de noticias de todo el mundo, uno de sus objetivos es desarrollar y mantener estándares técnicos. La IPTC definió un conjunto de estándares de metadatos fotográficos para imágenes que es aceptado casi universalmente entre los fotógrafos. Estos estándares de metadatos formaban parte del estándar más amplio conocido como el Modelo de Intercambio de Información (IIM) de IPTC creado en la década de 1990.

Aunque la información del encabezado de IPTC ha sido reemplazada principalmente por XMP, hay disponibles un esquema principal de IPTC y un esquema de extensión para XMP. En los programas de imagen, las propiedades XMP y IPTC se sincronizan.

## Flujos de trabajo impulsados por metadatos {#metadata-driven-workflows}

La creación de flujos de trabajo impulsados por metadatos le ayuda a automatizar algunos procesos, lo que mejora la eficacia. En un flujo de trabajo controlado por metadatos, el sistema de administración de flujos de trabajo lee el flujo de trabajo y, como resultado, realiza algunas acciones predefinidas. Por ejemplo, algunas de las formas de utilizar flujos de trabajo impulsados por metadatos:

* El flujo de trabajo puede comprobar si una imagen tiene título o no. Si no es así, el sistema le notifica que añada un título.
* El flujo de trabajo puede comprobar si un aviso de copyright en un recurso permite la distribución o no. Por lo tanto, el sistema envía el recurso a un servidor u otro.
* Un flujo de trabajo puede buscar recursos sin metadatos obligatorios predefinidos o recursos con *metadatos no válidos*.

## Metadatos XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) es el estándar de metadatos utilizado por [!DNL Adobe Experience Manager Assets] para la administración de todos los metadatos. XMP proporciona un formato estándar para la creación, el procesamiento y el intercambio de metadatos para una amplia variedad de aplicaciones.

Además de ofrecer codificación de metadatos universal que se puede incrustar en todos los formatos de archivo, XMP proporciona un rico [modelo de contenido](#xmp-core-concepts) y es [compatible con Adobe](#advantages-of-xmp) y otras compañías, de modo que los usuarios de XMP en combinación con [!DNL Assets] tengan una plataforma potente sobre la cual construir.

La [especificación de XMP](https://www.adobe.com/devnet/xmp.html) está disponible en Adobe.

### ¿Qué es XMP? {#what-is-xmp}

Adobe introdujo por primera vez el estándar XMP como parte del producto de software Adobe Acrobat. Desde entonces, el estándar XMP ha sido ampliamente adoptado. [!DNL Assets] es compatible de forma nativa con XMP, la plataforma de metadatos extensible encabezada por Adobe. XMP es un estándar para procesar y almacenar metadatos estandarizados y propios en recursos digitales. XMP está diseñado como el estándar común que permite que varias aplicaciones funcionen con eficacia con los metadatos.

Los profesionales de la producción, por ejemplo, utilizan la compatibilidad integrada con XMP en las aplicaciones de Adobe para pasar información a través de varios formatos de archivo. El repositorio [!DNL Assets] extrae los metadatos de XMP y los utiliza para administrar el ciclo de vida del contenido. Además, ofrece la capacidad de crear flujos de trabajo de automatización.

XMP estandariza la forma en que se definen, crean y procesan los metadatos proporcionando un modelo de datos, un modelo de almacenamiento y esquemas. Todos estos conceptos se tratan en esta sección.

Todos los metadatos heredados de EXIF, ID3 o Microsoft Office se traducen automáticamente a XMP, que se puede ampliar para admitir esquemas de metadatos específicos del cliente, como catálogos de productos.

Los metadatos de XMP constan de un conjunto de propiedades. Estas propiedades siempre se asocian con un
entidad concreta denominada recurso; es decir, las propiedades son &quot;acerca&quot; del recurso. Si hay XMP, el recurso siempre es el recurso.

### ecosistema de XMP {#xmp-ecosystem}

XMP define un modelo de [metadatos](https://es.wikipedia.org/wiki/Metadatos) que se puede utilizar con cualquier conjunto definido de elementos de metadatos. XMP también define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propiedades básicas útiles para registrar el historial de un recurso a medida que pasa por varios pasos de procesamiento, desde ser fotografiado, [escaneado](https://es.wikipedia.org/wiki/Esc%C3%A1ner_inform%C3%A1tico) o creado como texto, pasando por etapas de edición fotográfica (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) o ajuste de color), hasta ensamblarse en una imagen final. XMP permite a cada programa o dispositivo de software añadir su propia información a un recurso digital, que se puede retener en el archivo digital final.

XMP se serializa y almacena con mayor frecuencia mediante un subconjunto del [W3C](https://es.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que a su vez se expresa en [XML](https://en.wikipedia.org/wiki/XML).

### Ventajas de XMP {#advantages-of-xmp}

XMP tiene las siguientes ventajas sobre otros estándares de codificación y esquemas:

* Los metadatos basados en XMP son muy completos y precisos.
* XMP permite tener varios valores para una propiedad.
* XMP tiene una codificación estandarizada, que permite intercambiar fácilmente metadatos.
* XMP es extensible. Puede añadir información adicional a sus recursos.

El estándar de XMP está diseñado para ser extensible, lo que le permite agregar tipos personalizados de metadatos a los datos de XMP. EXIF, por otro lado, no - tiene una lista fija de propiedades que no se pueden ampliar.

>[!NOTE]
>
>XMP generalmente no permite incrustar tipos de datos binarios. Para transportar datos binarios en XMP, por ejemplo, imágenes en miniatura, se deben codificar en un formato compatible con XML como `Base64`.

### Conceptos de XMP {#xmp-core-concepts}

En las secciones siguientes se describen los conceptos principales de XMP, incluidos los espacios de nombres y esquemas, las propiedades y los valores, y las alternativas de lenguaje.

#### Espacios de nombres y esquemas {#namespaces-and-schemata}

Un esquema de XMP es un conjunto de nombres de propiedad en un espacio de nombres XML común que incluye
el tipo de datos y la información descriptiva. Un esquema de XMP se identifica con su URI de espacio de nombres XML. El uso de áreas de nombres evita conflictos entre propiedades en esquemas diferentes que tienen el mismo nombre pero un significado diferente.

Por ejemplo, la propiedad `Creator` en dos esquemas diseñados de forma independiente puede significar la persona que creó el recurso o puede significar la aplicación que creó el recurso (por ejemplo, Adobe Photoshop).

#### Propiedades y valores {#properties-and-values}

XMP puede incluir propiedades de uno o más de los esquemas. Por ejemplo, un subconjunto típico utilizado por muchas aplicaciones de Adobe puede incluir lo siguiente:

* Esquema principal de Dublín: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* Esquema básico de XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Esquema de administración de derechos de XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* Esquema de administración de medios de XMP: `xmpMM:DocumentID`.

#### Alternativas lingüísticas {#language-alternatives}

XMP permite agregar una propiedad `xml:lang` a las propiedades de texto para especificar el idioma del texto.

## Trabajo con metadatos de IPTC {#support-for-iptc-metadata}

Descubra cómo [!DNL Adobe Experience Manager Assets] admite los metadatos de IPTC, las clasificaciones de creativos y las palabras clave agregadas a los recursos mediante [!DNL Adobe Bridge] y otras [!DNL Adobe Creative Cloud] aplicaciones.

[!DNL Adobe Experience Manager Assets] admite el estándar de metadatos de IPTC, que se utiliza ampliamente para describir recursos. De esta manera, [!DNL Assets] mejora la aceptación de sus imágenes entre diversas partes, incluidos fotógrafos, agencias creativas, bibliotecas, museos, etc.

El esquema de metadatos predeterminado para los recursos ahora incorpora los esquemas de metadatos de IPTC Core y IPTC Extension para definir propiedades de metadatos completas que permitan a los usuarios agregar datos precisos y fiables sobre las personas, las ubicaciones y los productos que se muestran en una imagen. También admite fechas, nombres e identificadores con respecto a la creación de la imagen y una forma flexible de expresar la información de derechos.

La página Propiedades de los recursos ahora incluye pestañas independientes para mostrar los metadatos de la extensión de IPTC Core y IPTC en campos editables.

1. En la interfaz de usuario [!DNL Assets], seleccione una imagen.
1. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. Haga clic en la ficha **[!UICONTROL IPTC]** para ver los metadatos de IPTC del recurso.
1. Edite las propiedades de los metadatos de IPTC según sea necesario.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Haga clic en la pestaña **[!UICONTROL Extensión de IPTC]** para ver los metadatos de la extensión de IPTC para el recurso.
1. Edite las propiedades de metadatos de la extensión de IPTC según sea necesario.
1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar los cambios.

### Asistencia de clasificación creativa {#creative-rating-support}

Además de mostrar las clasificaciones de usuarios individuales y las clasificaciones acumuladas, la página Propiedades ahora muestra las clasificaciones asignadas a los recursos a través de Adobe Bridge y otras aplicaciones creativas

Estas clasificaciones están disponibles en la sección **[!UICONTROL Clasificación creativa]** de la pestaña **[!UICONTROL Avanzado]**.

Esta clasificación es de solo lectura y oscila entre 1 y 5. Puede buscar recursos en función de su clasificación creativa en el panel Buscar.

Sin embargo, esta propiedad no está indizada actualmente para evitar conflictos con los cambios personalizados realizados por los usuarios.

### Compatibilidad con palabras clave {#keyword-support}

La pestaña **[!UICONTROL IPTC]** de la página [!UICONTROL Propiedades] también muestra las palabras clave agregadas a los recursos mediante Adobe Bridge y otras aplicaciones de Adobe Creative Cloud. También puede editar estas palabras clave y agregar más desde la pestaña **[!UICONTROL IPTC]**.

![palabras clave](assets/keywords-in-iptc-tab.png)
