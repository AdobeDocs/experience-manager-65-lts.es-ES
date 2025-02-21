---
title: Creación de páginas de contenido con fragmentos de contenido
description: Los fragmentos de contenido de AEM le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Content Fragments
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 63%

---

# Creación de páginas con fragmentos de contenido{#page-authoring-with-content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) se [crean y administran como recursos independientes de la página](/help/assets/content-fragments/content-fragments.md).

Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido.

Junto con el exportador JSON actualizado, los fragmentos de contenido estructurados también se pueden utilizar para distribuir contenidos de AEM mediante servicios de contenido a canales en lugar de páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-authoring/experience-fragments.md)** son funciones distintas de AEM:
>
>* **Los fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Son contenidos puros, sin diseño ni diseño.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web.
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.

>[!CAUTION]
>
>Esta página se debe leer con [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) (y páginas relacionadas) porque presenta terminología y conceptos básicos, así como la creación y administración de fragmentos.

Los fragmentos de contenido permiten lo siguiente:

* **Estrategia de campañas y marketing**

   * Revise el contenido a través de fragmentos de contenido administrados de forma centralizada.

* **Creative Pro**

   * Seguimiento de recursos creativos mediante colecciones asociadas con fragmentos de contenido.

* **Redactores**

   * Escriba en el editor de fragmentos de contenido de AEM.
   * Puede crear variaciones de contenido.
   * Puede asociar contenido relevante con el fragmento de contenido.
   * Puede utilizar el control de versiones/flujo de trabajo.
   * Puede compartir fragmentos de contenido.
   * Puede administrar traducciones de forma centralizada.

* **Productores y gestores de recorridos**

   * Seleccione fragmentos y variaciones predefinidos con la creación en AEM.
   * Puede confiar en que el fragmento y el contenido asociado estarán siempre actualizados, ya que los redactores y creativos realizan sus actualizaciones en fragmentos y activos administrados de forma centralizada.
   * Puede confiar en que el contenido multimedia asociado se seleccione en función de la relevancia.
   * Pueden crear variaciones de contenido ad hoc al instante garantizando al mismo tiempo que las variaciones siguen administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página       {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla.

1. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**.

1. Puede:

   * Abra el navegador **Recursos** y filtre por **Fragmentos de contenido** (el valor predeterminado es Imágenes). A continuación, arrastre el fragmento requerido a la instancia del componente.

   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.

   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto crea automáticamente el componente asociado (fragmento de contenido).

1. Inicialmente se muestra el contenido del elemento **Main** y **Master** (variación). Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Para obtener más información sobre las funciones de edición adicionales, consulte lo siguiente:
   >
   >
   >
   >    * [Diseño adaptable](/help/sites-authoring/responsive-layout.md)
   >    * [Edición del contenido de una página](/help/sites-authoring/editing-content.md)
   >
   >

### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el cuadro de diálogo **Configuración** del fragmento para que pueda configurarlo y utilizarlo en la página actual. El cuadro de diálogo puede depender del componente utilizado.

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, entre los que se incluyen:

* **Fragmento de contenido**

  Especifique el fragmento que se va a utilizar.

* **Modo de visualización**:

   * **Elemento de texto único**

   * **Elemento múltiple**

* **Elemento**

   * El **Principal** predeterminado siempre está disponible.
   * Hay una selección disponible si el fragmento se creó con una plantilla adecuada.

  >[!NOTE]
  >
  >Los elementos disponibles dependen de la plantilla utilizada.

* **Variación**

   * El **Principal** predeterminado siempre está disponible.
   * Hay disponible una selección si se crearon variaciones para el fragmento.

* **Párrafos**: especifique el intervalo de párrafos que desea incluir:

   * **Todos**
   * **Rango**: por ejemplo, `1`, `3-5` o `9-*`

      * **Gestionar encabezados como sus propios párrafos**

* **Gestionar encabezados como sus propios párrafos**

### Conexión rápida con el editor de fragmentos  {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permite [editar y administrar el fragmento de contenido](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento puede afectar a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Añadir contenido intermedio       {#adding-in-between-content}

Cuando se agrega un fragmento de contenido específico a la página, aparece un marcador de posición **Arrastre los componentes aquí** entre cada párrafo HTML (y en la parte superior/inferior) del fragmento.

Esto le permite agregar contenido adicional [intermedio (es decir, contenido intermedio)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) al contenido del fragmento (en cualquiera de los puntos disponibles), sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede hacer lo siguiente:

* Añadir componentes desde el [Explorador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).
* Agregar recursos desde el [Explorador de recursos](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Utilizar [contenido asociado](#using-associated-content) como fuente para el contenido intermedio.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo anterior.

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, aunque varíe el contenido de los párrafos del fragmento.
>
>  Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).
>

### Uso de contenido asociado       {#using-associated-content}

Si tiene [contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) con el [fragmento de contenido](/help/assets/content-fragments/content-fragments.md), estos recursos están disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). El contenido asociado es en realidad una fuente especial de contenido para [contenido intermedio](#adding-in-between-content).

>[!NOTE]
>
>Existen varios métodos para añadir [recursos visuales (por ejemplo, imágenes)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o la página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la ficha **Contenido asociado** muestra los recursos apropiados para todos los fragmentos.

Una vez que haya agregado un fragmento con contenido asociado a la página, se abrirá una nueva pestaña (**Contenido asociado**) en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (a un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![cfm-6420-03](assets/cfm-6420-03.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

Si se insertan recursos (por ejemplo, imágenes) en el propio fragmento, las opciones para editarlos en el editor de páginas son limitadas. <!-- Removed link as it was a 404 on helpx -->

Por ejemplo, para una imagen puede

* Recortar, rotar o voltear la imagen.
* Añadir un título o texto alternativo.
* Especificar un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben efectuarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para que se puedan utilizar en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Recursos](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar el fragmento en este momento.
