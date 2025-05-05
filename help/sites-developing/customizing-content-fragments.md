---
title: Personalizar y ampliar fragmentos de contenido
description: Un fragmento de contenido amplía un recurso estándar. Descubra cómo puede personalizarlos.
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
exl-id: 705bffea-ef70-40b5-81d8-b130d3908073
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 1%

---

# Personalizar y ampliar fragmentos de contenido{#customizing-and-extending-content-fragments}

Un fragmento de contenido amplía un recurso estándar; consulte:

* [Creación y administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) y [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md) para obtener más información acerca de los fragmentos de contenido.

* [Administración de Assets](/help/assets/manage-assets.md) y [Personalización y ampliación de Assets](/help/assets/extending-assets.md) para obtener más información sobre los recursos estándar.

## Arquitectura {#architecture}

Las [partes constitutivas](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) básicas de un fragmento de contenido son:

* Un *Fragmento De Contenido,*
* compuesto por uno o más *elementos de contenido* s,
* y que pueden tener una o más *variaciones de contenido* s.

Según el tipo de fragmento, también se utilizan modelos o plantillas:

>[!CAUTION]
>
>Se recomiendan [modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-models.md) para crear todos los fragmentos nuevos.
>
>Los modelos de fragmentos de contenido se utilizan para todos los ejemplos en WKND.

>[!NOTE]
>
>Antes de AEM 6.3, los fragmentos de contenido se creaban en función de plantillas en lugar de modelos.
>
>Las plantillas de fragmento de contenido ya no se utilizan. Todavía se pueden utilizar para crear fragmentos, pero se recomienda utilizar Modelos de fragmentos de contenido en su lugar. No se agregarán nuevas funciones a las plantillas de fragmento y se eliminarán en una versión futura.

* Modelos de fragmento de contenido:

   * Se utiliza para definir fragmentos de contenido que contienen contenido estructurado.
   * Los modelos de fragmento de contenido definen la estructura de un fragmento de contenido cuando se crea.
   * Un fragmento hace referencia al modelo, por lo que los cambios realizados en el modelo pueden afectar a cualquier fragmento dependiente.
   * Los modelos son una compilación de tipos de datos.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.

  >[!CAUTION]
  >
  >Cualquier cambio en un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes, lo que puede generar propiedades huérfanas en esos fragmentos.

* Plantillas de fragmentos de contenido:

   * Se utiliza para definir fragmentos de contenido simples.
   * Las plantillas definen la estructura (básica, de solo texto) de un fragmento de contenido cuando se crea.
   * La plantilla se copia en el fragmento cuando se crea, por lo que los cambios posteriores en la plantilla no se reflejarán en los fragmentos existentes.
   * Las funciones para agregar nuevas variaciones, etc., deben actualizar el fragmento en consecuencia.
      * Cuando se basa en una plantilla, el tipo MIME del contenido se administra en función del contenido real; esto significa que cada elemento y variación puede tener un tipo MIME diferente.

### Integración con Assets {#integration-with-assets}

La administración de fragmentos de contenido (CFM) forma parte de AEM Assets como:

* Los fragmentos de contenido son recursos.
* Utilizan la funcionalidad existente de Assets.
* Están totalmente integrados con Assets (Admin Consoles, etc.).

#### Asignación de fragmentos de contenido estructurados a Assets {#mapping-structured-content-fragments-to-assets}

![fragmento a recursos-estructurado](assets/fragment-to-assets-structured.png)

Los fragmentos de contenido con contenido estructurado (es decir, basados en un modelo de fragmento de contenido) se asignan a un único recurso:

* Todo el contenido se almacena en el nodo `jcr:content/data` del recurso:

   * Los datos del elemento se almacenan en el subnodo principal:

     `jcr:content/data/master`

   * Las variaciones se almacenan en un subnodo que lleva el nombre de la variación:
por ejemplo, `jcr:content/data/myvariation`

   * Los datos de cada elemento se almacenan en el subnodo respectivo como una propiedad con el nombre del elemento:
por ejemplo, el contenido del elemento `text` se almacena como propiedad `text` en `jcr:content/data/master`

* Los metadatos y el contenido asociado se almacenan debajo de `jcr:content/metadata`
Excepto el título y la descripción, que no se consideran metadatos tradicionales y se almacenan en `jcr:content`

#### Asignación de fragmentos de contenido simples a Assets {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

Los fragmentos de contenido simples (basados en una plantilla) se asignan a un compuesto que consta de un recurso principal y de subrecursos (opcionales):

* Toda la información sin contenido de un fragmento (como título, descripción, metadatos, estructura) se administra exclusivamente en el recurso principal.
* El contenido del primer elemento de un fragmento se asigna a la representación original del recurso principal.

   * Las variaciones (si hay alguna) del primer elemento se asignan a otras representaciones del recurso principal.

* Los elementos adicionales (si existen) se asignan a subrecursos del recurso principal.

   * El contenido principal de estos elementos adicionales se asigna a la representación original del subrecurso correspondiente.
   * Otras variaciones (si corresponde) de cualquier elemento adicional se asignan a otras representaciones del subactivo correspondiente.

#### Ubicación del recurso {#asset-location}

Al igual que con los recursos estándar, un fragmento de contenido se encuentra en:

`/content/dam`

#### Permisos de recursos {#asset-permissions}

Para obtener más información, consulte [Fragmento de contenido: eliminar consideraciones](/help/assets/content-fragments/content-fragments-delete.md).

#### Integración de funciones {#feature-integration}

* La función Administración de fragmentos de contenido (CFM) se basa en el núcleo de Assets, pero debe ser lo más independiente posible de él.
* CFM proporciona sus propias implementaciones para elementos en las vistas de tarjeta, columna o lista; estos se conectan a las implementaciones existentes de representación de contenido de Assets.
* Varios componentes de Assets se han ampliado para adaptarse a los fragmentos de contenido.

### Uso de fragmentos de contenido en páginas {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Ahora se recomienda el [componente principal de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es). Consulte [Desarrollar componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) para obtener más información.

Se puede hacer referencia a los fragmentos de contenido desde páginas de AEM, como cualquier otro tipo de recurso. AEM proporciona el componente principal [**Fragmento de contenido**](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es) - un componente [que le permite incluir fragmentos de contenido en sus páginas](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). También puede ampliar este componente principal **Fragmento de contenido**.

* El componente utiliza la propiedad `fragmentPath` para hacer referencia al fragmento de contenido real. La propiedad `fragmentPath` se administra de la misma manera que propiedades similares de otros tipos de recursos; por ejemplo, cuando el fragmento de contenido se mueve a otra ubicación.

* El componente permite seleccionar la variación que se desea mostrar.
* Además, se puede seleccionar un rango de párrafos para restringir la salida; por ejemplo, esto se puede utilizar para la salida de varias columnas.
* El componente permite [contenido intermedio](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Aquí, el componente le permite colocar otros recursos (imágenes, etc.) entre los párrafos del fragmento al que se hace referencia.
   * Para el contenido intermedio, debe:

      * tenga en cuenta la posibilidad de referencias inestables; el contenido intermedio (añadido al crear una página) no tiene relación fija con el párrafo al que se coloca junto, insertando un nuevo párrafo (en el editor de fragmentos de contenido) antes de que la posición del contenido intermedio pueda perder la posición relativa
      * tenga en cuenta los parámetros adicionales (como variaciones y filtros de párrafo) para evitar falsos positivos en los resultados de búsqueda

>[!NOTE]
>
>**Modelo de fragmento de contenido:**
>
>Al utilizar un fragmento de contenido basado en un modelo de fragmento de contenido en una página, se hace referencia al modelo. Esto significa que si el modelo no se ha publicado en el momento de publicar la página, se marcará y el modelo se agregará a los recursos que se publicarán con la página.
>
>**Plantilla de fragmento de contenido:**
>
>Al utilizar un fragmento de contenido basado en una plantilla de fragmento de contenido en una página, no hay ninguna referencia porque la plantilla se copió al crear el fragmento.

#### Configuración mediante la consola OSGi {#configuration-using-osgi-console}

La implementación back-end de fragmentos de contenido es, por ejemplo, responsable de hacer que las instancias de un fragmento utilizado en una página se puedan buscar o de administrar el contenido de medios mixtos. Esta implementación necesita saber qué componentes se utilizan para procesar fragmentos y cómo se parametriza el procesamiento.

Los parámetros para esto se pueden configurar en la [consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), para el paquete OSGi **Configuración del componente de fragmento de contenido**.

* **Tipos de recursos**
Se puede proporcionar una lista de `sling:resourceTypes` para definir los componentes que se utilizan para procesar fragmentos de contenido y a los que se debe aplicar el procesamiento en segundo plano.

* **Propiedades de referencia**
Se puede configurar una lista de propiedades para especificar dónde se almacena la referencia al fragmento para el componente respectivo.

>[!NOTE]
>
>No hay asignación directa entre la propiedad y el tipo de componente.
>
>AEM simplemente toma la primera propiedad que se encuentra en un párrafo. Por lo tanto, debe elegir las propiedades cuidadosamente.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Sigue habiendo algunas directrices que debe seguir para asegurarse de que el componente es compatible con el procesamiento en segundo plano del fragmento de contenido:

* El nombre de la propiedad donde se definen los elementos que se van a representar debe ser `element` o `elementNames`.

* El nombre de la propiedad donde se define la variación que se va a procesar debe ser `variation` o `variationName`.

* Si se admite la salida de varios elementos (utilizando `elementNames` para especificar varios elementos), el modo de visualización real se define mediante la propiedad `displayMode`:

   * Si el valor es `singleText` (y solo hay un elemento configurado), el elemento se representa como un texto con contenido intermedio, compatibilidad de diseño, etc. Esta es la opción predeterminada para los fragmentos en los que solo se procesa un elemento.
   * De lo contrario, se utiliza un método mucho más sencillo (podría denominarse &quot;vista de formulario&quot;), en el que no se admite contenido intermedio y el contenido del fragmento se procesa &quot;tal cual&quot;.

* Si el fragmento se procesa para `displayMode` == `singleText` (implícita o explícitamente), entrarán en juego las siguientes propiedades adicionales:

   * `paragraphScope` define si se deben representar todos los párrafos o solo un intervalo de párrafos (valores: `all` frente a `range`)

   * si `paragraphScope` == `range`, la propiedad `paragraphRange` define el intervalo de párrafos que se va a representar

### Integración con otros marcos {#integration-with-other-frameworks}

Los fragmentos de contenido se pueden integrar con:

* **Traducciones**

  Los fragmentos de contenido están totalmente integrados con el [flujo de trabajo de traducción de AEM](/help/sites-administering/tc-manage.md). A nivel arquitectónico, esto significa:

   * Las traducciones individuales de un fragmento de contenido son en realidad fragmentos independientes; por ejemplo:

      * se encuentran bajo diferentes raíces lingüísticas:

        `/content/dam/<path>/en/<to>/<fragment>`

        frente a

        `/content/dam/<path>/de/<to>/<fragment>`

      * pero comparten exactamente la misma ruta relativa debajo de la raíz del idioma:

        `/content/dam/<path>/en/<to>/<fragment>`

        frente a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Además de las rutas basadas en reglas, no hay ninguna conexión adicional entre las distintas versiones de idioma de un fragmento de contenido; se gestionan como dos fragmentos independientes, aunque la interfaz de usuario proporciona los medios para navegar entre las variantes de idioma.

  >[!NOTE]
  >
  >El flujo de trabajo de traducción de AEM funciona con `/content`:
  >
  >* Como los modelos de fragmento de contenido residen en `/conf`, no se incluyen en dichas traducciones. Puede [internacionalizar las cadenas de la interfaz de usuario](/help/sites-developing/i18n-dev.md).
  >
  >* Las plantillas se copian para crear el fragmento, por lo que está implícito.

* **Esquemas de metadatos**

   * Los fragmentos de contenido (re)utilizan los [esquemas de metadatos](/help/assets/metadata-schemas.md), que se pueden definir con recursos estándar.
   * CFM proporciona su propio esquema específico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     esto se puede ampliar si es necesario.

   * El formulario de esquema respectivo se integra con el editor de fragmentos.

## La API de administración de fragmentos de contenido: del lado del servidor {#the-content-fragment-management-api-server-side}

Puede utilizar la API del lado del servidor para acceder a sus fragmentos de contenido; consulte:

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Se recomienda encarecidamente utilizar la API del lado del servidor en lugar de acceder directamente a la estructura de contenido.

### Interfaces clave {#key-interfaces}

Las tres interfaces siguientes pueden servir como puntos de entrada:

* **Plantilla de fragmento** ([FragmentTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  Usar `FragmentTemplate.createFragment()` para crear un fragmento.

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  Esta interfaz representa:

   * un modelo de fragmento de contenido o una plantilla de fragmento de contenido desde la que crear un fragmento de contenido,
   * y (después de la creación) la información estructural de ese fragmento

  Esta información puede incluir:

   * Acceso a datos básicos (título, descripción)
   * Acceda a las plantillas/modelos para los elementos del fragmento:

      * Plantillas de elementos de lista
      * Obtener información estructural de un elemento determinado
      * Tener acceso a la plantilla de elemento (consulte `ElementTemplate`)

   * Acceda a las plantillas para las variaciones del fragmento:

      * Plantillas de variación de lista
      * Obtener información estructural de una variación determinada
      * Acceder a la plantilla de variación (ver `VariationTemplate`)

   * Obtener contenido asociado inicial

  Interfaces que representan información importante:

   * `ElementTemplate`

      * Obtener datos básicos (nombre, título)
      * Obtener contenido inicial del elemento

   * `VariationTemplate`

      * Obtener datos básicos (nombre, título, descripción)

* **Fragmento de contenido** ([Fragmento de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Esta interfaz permite trabajar con un fragmento de contenido de forma abstracta.

  >[!CAUTION]
  >
  >Es muy recomendable acceder a un fragmento a través de esta interfaz. Se debe evitar cambiar la estructura del contenido directamente.

  La interfaz de le proporciona los medios para lo siguiente:

   * Administrar datos básicos (por ejemplo, obtener nombre; obtener/establecer título/descripción)
   * Acceso a metadatos
   * Elementos de acceso:

      * Lista de elementos
      * Obtener elementos por nombre
      * Crear elementos nuevos (vea [Advertencias](#caveats))

      * Acceder a datos de elementos (consulte `ContentElement`)

   * Variaciones de lista definidas para el fragmento
   * Crear nuevas variaciones globalmente
   * Administrar contenido asociado:

      * Enumerar colecciones
      * Agregar colecciones
      * Quitar colecciones

   * Acceder al modelo o la plantilla del fragmento

  Las interfaces que representan los elementos principales de un fragmento son:

   * **Elemento de contenido** ([Elemento de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Variaciones de acceso de un elemento:

         * Variaciones de lista
         * Obtener variaciones por nombre
         * Crear nuevas variaciones (consulte [Advertencias](#caveats))
         * Eliminar variaciones (consulte [Advertencias](#caveats))
         * Datos de variación de acceso (consulte `ContentVariation`)

      * Método abreviado para resolver variaciones (aplicar alguna lógica de reserva adicional específica de la implementación si la variación especificada no está disponible para un elemento)

   * **Variación de contenido** ([Variación de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Obtener datos básicos (nombre, título, descripción)
      * Obtener/establecer contenido
      * Sincronización simple, basada en la información de la última modificación

  Las tres interfaces ( `ContentFragment`, `ContentElement`, `ContentVariation`) amplían la interfaz `Versionable`, que agrega capacidades de versiones, necesarias para los fragmentos de contenido:

   * Crear nueva versión del elemento
   * Enumerar versiones del elemento
   * Obtener el contenido de una versión específica del elemento con versión

### Adaptación: uso de adaptTo() {#adapting-using-adaptto}

Se pueden adaptar las siguientes opciones:

* `ContentFragment` se puede adaptar a:

   * `Resource`: el recurso de Sling subyacente. Tenga en cuenta que la actualización del objeto de `Resource` subyacente de forma directa requiere la reconstrucción del objeto `ContentFragment`.

   * `Asset`: la abstracción de DAM `Asset` que representa el fragmento de contenido. Tenga en cuenta que la actualización directa de `Asset` requiere la reconstrucción del objeto `ContentFragment`.

* `ContentElement` se puede adaptar a:

   * `ElementTemplate` - para acceder a la información estructural del elemento.

* `FragmentTemplate` se puede adaptar a:

   * `Resource`: el `Resource` que determina el modelo al que se hace referencia o la plantilla original que se copió;

      * los cambios realizados mediante `Resource` no se reflejan automáticamente en `FragmentTemplate`.

* `Resource` se puede adaptar a:

   * `ContentFragment`
   * `FragmentTemplate`

### Advertencias {#caveats}

Cabe señalar que:

* La API se implementa para proporcionar la funcionalidad admitida por la interfaz de usuario de.
* La API completa está diseñada para **no** mantener los cambios automáticamente (a menos que se indique lo contrario en el JavaDoc de la API). Por lo tanto, siempre tendrá que asignar el solucionador de recursos de la solicitud correspondiente (o el solucionador que esté utilizando).
* Tareas que pueden requerir un esfuerzo adicional:

   * La creación o eliminación de nuevos elementos no actualiza la estructura de datos de fragmentos simples (basados en una plantilla de fragmento).
   * La creación de nuevas variaciones a partir de `ContentElement` no actualizará la estructura de datos (pero sí lo hará la creación global a partir de `ContentFragment`).

   * La eliminación de las variaciones existentes no actualizará la estructura de datos.

## La API de administración de fragmentos de contenido: del lado del cliente {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Para AEM 6.5, la API del lado del cliente es interna.

### Información adicional {#additional-information}

Consulte lo siguiente:

* `filter.xml`

  El `filter.xml` para la administración de fragmentos de contenido está configurado de modo que no se superponga con el paquete de contenido principal de Assets.

## Editar sesiones {#edit-sessions}

Se inicia una sesión de edición cuando el usuario abre un fragmento de contenido en una de las páginas del editor. La sesión de edición finaliza cuando el usuario abandona el editor seleccionando **Guardar** o **Cancelar**.

### Requisitos  {#requirements}

Los requisitos para controlar una sesión de edición son:

* La edición de un fragmento de contenido, que puede abarcar varias vistas (= páginas de HTML), debe ser atómica.
* La edición también debe ser *transaccional*; al final de la sesión de edición, los cambios deben confirmarse (guardarse) o revertirse (cancelarse).
* Los casos de Edge deben gestionarse correctamente, incluidas situaciones como cuando el usuario sale de la página introduciendo una URL manualmente o utilizando la navegación global.
* Debe haber disponible un guardado automático periódico (cada x minutos) para evitar la pérdida de datos.
* Si dos usuarios editan un fragmento de contenido simultáneamente, no deben sobrescribir los cambios de los demás.

#### Procesos {#processes}

Los procesos involucrados son:

* Inicio de una sesión

   * Se crea una nueva versión del fragmento de contenido.
   * Se inicia el guardado automático.
   * Se configuran las cookies, que definen el fragmento editado actualmente y que hay una sesión de edición abierta.

* Finalizar una sesión

   * Se ha detenido el guardado automático.
   * Tras la confirmación:

      * Se actualiza la información de la última modificación.
      * Se eliminan las cookies.

   * Tras la reversión:

      * Se restaura la versión del fragmento de contenido que se creó al iniciar la sesión de edición.
      * Se eliminan las cookies.

* Edición

   * Todos los cambios (incluido el guardado automático) se realizan en el fragmento de contenido activo, no en un área protegida separada.
   * Por lo tanto, estos cambios se reflejan inmediatamente en las páginas de AEM que hacen referencia al fragmento de contenido correspondiente

#### Acciones {#actions}

Las acciones posibles son:

* Introducción de una página

   * Compruebe si ya hay una sesión de edición; comprobando la cookie correspondiente.

      * Si existe, compruebe que la sesión de edición se haya iniciado para el fragmento de contenido que se está editando en ese momento

         * Si es el fragmento actual, restablezca la sesión.
         * Si no es así, intente cancelar la edición del fragmento de contenido editado anteriormente y elimine las cookies (no habrá ninguna sesión de edición posterior).

      * Si no existe ninguna sesión de edición, espere al primer cambio realizado por el usuario (consulte a continuación).

   * Compruebe si ya se hace referencia al fragmento de contenido en una página y muestre la información adecuada si es así.

* Cambio de contenido

   * Siempre que el usuario cambia el contenido y no hay ninguna sesión de edición presente, se crea una nueva sesión de edición (consulte [Inicio de una sesión](#processes)).

* Salir de una página

   * Si hay una sesión de edición y los cambios no se han mantenido, se muestra un cuadro de diálogo de confirmación modal para notificar al usuario de la posible pérdida de contenido y permitirle permanecer en la página.

## Ejemplos {#examples}

### Ejemplo: Acceso a un fragmento de contenido existente {#example-accessing-an-existing-content-fragment}

Para lograrlo, puede adaptar el recurso que representa la API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Por ejemplo:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Ejemplo: Creación de un fragmento de contenido {#example-creating-a-new-content-fragment}

Para crear un fragmento de contenido mediante programación, debe utilizar:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Por ejemplo:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Ejemplo: Especificación del intervalo de guardado automático {#example-specifying-the-auto-save-interval}

El intervalo de guardado automático (medido en segundos) se puede definir mediante el administrador de configuración (ConfMgr):

* Nodo: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`
* Tipo: `Long`

* Predeterminado: `600` (10 minutos); definido en `/libs/settings/dam/cfm/jcr:content`

Si desea establecer un intervalo de guardado automático de 5 minutos, debe definir la propiedad en el nodo; por ejemplo:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nombre de propiedad: `autoSaveInterval`

* Tipo: `Long`

* Valor: `300` (5 minutos equivalen a 300 segundos)

## Componentes para la creación de páginas {#components-for-page-authoring}

Para obtener más información, consulte

* [Componentes principales - Componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es) (recomendado)
* [Componentes de fragmentos de contenido: componentes para la creación de páginas](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
