---
title: Personalización de las consolas
description: AEM proporciona varios mecanismos para permitirle personalizar las consolas de su instancia de creación
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 2a94ea8d-2919-4f30-be31-ce559493805d
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# Personalización de las consolas {#customizing-the-consoles}

>[!CAUTION]
>
>Este documento describe cómo personalizar las consolas en la IU moderna y táctil, y no se aplica a la IU clásica.

AEM proporciona varios mecanismos para permitirle personalizar las consolas (y la [funcionalidad de creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)) de su instancia de creación.

* Clientlibs
Clientlibs le permite ampliar la implementación predeterminada para obtener nuevas funcionalidades, mientras reutiliza las funciones, los objetos y los métodos estándar. Al personalizar, puede crear su propia clientlib en `/apps.`. Por ejemplo, puede contener el código necesario para el componente personalizado.

* Superposiciones
Las superposiciones se basan en definiciones de nodo y le permiten superponer la funcionalidad estándar (en `/libs`) con su propia funcionalidad personalizada (en `/apps`). Al crear una superposición, no se requiere una copia 1:1 del original, ya que la fusión de recursos de sling permite la herencia.

Se pueden utilizar de muchas maneras para ampliar las consolas de AEM. Una pequeña selección se cubren a continuación (en un nivel alto).

>[!NOTE]
>
>Para obtener más información, consulte lo siguiente:
>
>* Usando y creando [clientlibs](/help/sites-developing/clientlibs.md).
>* Usando y creando [superposiciones](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html)
>


>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
>
>1. Realizar cambios en `/apps`
>

Por ejemplo, se puede superponer la siguiente ubicación dentro de la estructura `/libs`:

* consolas (cualquier consola basada en páginas de interfaz de usuario de Granite); por ejemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte el artículo de la Base de conocimiento [Solución de problemas de la IU táctil de AEM](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-16935) para obtener más sugerencias y herramientas.

## Personalización de la Vista Predeterminada para una Consola {#customizing-the-default-view-for-a-console}

Puede personalizar la vista predeterminada (columna, tarjeta, lista) de una consola:

1. Puede reordenar las vistas superponiendo la entrada requerida desde:

   `/libs/wcm/core/content/sites/jcr:content/views`

   La primera entrada es la predeterminada.

   Los nodos disponibles se correlacionan con las opciones de vista disponibles:

   * `column`
   * `card`
   * `list`

1. Por ejemplo, en una superposición para la lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina la siguiente propiedad:

   * **Nombre**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**: `column`

### Agregar nueva acción a la barra de herramientas {#add-new-action-to-the-toolbar}

1. Puede crear sus propios componentes e incluir las bibliotecas de cliente correspondientes para las acciones personalizadas. Por ejemplo, una acción **Promocionar a Twitter** en:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   A continuación, se puede conectar a un elemento de la barra de herramientas de la consola:

   `/apps/<yourProject>/admin/ext/launches`

   Por ejemplo, en el modo de selección:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir una acción de barra de herramientas a un grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. Puede utilizar una condición de procesamiento personalizada para superponer la acción estándar e imponer condiciones específicas que deben cumplirse antes de que se procese.

   Por ejemplo, cree un componente para controlar las condiciones de procesamiento según el grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicarlos a la acción Crear sitio en la consola Sitios:

   `/libs/wcm/core/content/sites`

   Cree la superposición:

   `/apps/wcm/core/content/sites`

1. A continuación, añada la condición de procesamiento para la acción:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Con las propiedades de este nodo puede definir `groups` que tiene permiso para realizar la acción específica; por ejemplo, `administrators`

### Personalización de columnas en la vista de lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Esta característica está optimizada para columnas de campos de texto; para otros tipos de datos es posible superponer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` en `/apps`.

Para personalizar las columnas en la vista de lista:

1. Superponga la lista de columnas disponibles.

   * En el nodo:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Añada las columnas nuevas o elimine las existentes.

   Consulte [Uso de superposiciones (y la fusión de recursos de Sling)](/help/sites-developing/overlays.md) para obtener más información.

1. Opcionalmente:

   * Si desea conectar datos adicionales, debe escribir [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con un
     Propiedad `pageInfoProviderType`.

   Por ejemplo, consulte la clase/paquete adjunto (de GitHub) a continuación.

1. Ahora puede seleccionar la columna en el configurador de columnas de la vista de lista.

### Filtrado de recursos {#filtering-resources}

Al utilizar una consola, un caso de uso común es cuando el usuario debe seleccionar entre recursos (por ejemplo, páginas, componentes, recursos, etc.). Esto puede adoptar la forma de una lista, por ejemplo, desde la que el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Consulte [Personalización de la creación de páginas - Filtrado de recursos](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obtener más información.
