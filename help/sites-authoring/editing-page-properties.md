---
title: 'Edición de las propiedades de página  '
description: Defina las propiedades necesarias para una página en Adobe Experience Manager.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 5148afb9-f447-4475-a15c-1fa345325711
mini-toc-levels: 2
source-git-commit: 4817296c00e094a65744a896d798e429d3ab6c7d
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 38%

---


# Edición de las propiedades de página  {#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar según la naturaleza de la página. Por ejemplo, algunas páginas podrían estar conectadas a una Live Copy, mientras que otras no lo están y la información de la Live Copy está disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas.

### Básico {#basic}

#### Título y etiquetas {#tile}

* **Título**: el título de la página se muestra en varias ubicaciones
   * Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.
   * Este es un campo obligatorio.
* **Etiquetas**: aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección.
   * Después de seleccionar una etiqueta, aparece debajo del cuadro de selección. Puede quitar una etiqueta de esta lista utilizando la x.
   * Se puede introducir una etiqueta nueva escribiendo el nombre en un cuadro de selección vacío.
      * La etiqueta nueva se crea al pulsar Intro.
      * La etiqueta nueva se muestra con una pequeña estrella a la derecha que indica que se trata de una etiqueta nueva.
   * Con la lista desplegable, puede seleccionar una de las etiquetas existentes.
   * Aparece una x cuando pasa el ratón sobre una entrada de etiqueta en el cuadro de selección, que se puede utilizar para quitar esa etiqueta para esa página.
   * Para obtener más información sobre las etiquetas, vea [Usar etiquetas.](/help/sites-authoring/tags.md)
* **Ocultar en navegación**: indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante

#### Personalización de marca {#branding}

Aplique una identidad de marca uniforme en todas las páginas adjuntando un slug de marca al título de cada página. Esta funcionalidad requiere el uso del componente de página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)

* **Sobrescribir**: marque para definir el slug de marca en esta página.
   * El valor lo hereda cualquier página secundaria a menos que también tenga valores establecidos de **Sobrescribir**.
* **Sobrescribir valor**: el texto del slug de marca que se agregará al título de la página
   * El valor se anexa al título de la página después de un carácter de barra vertical como `Cycling Tuscany | Always ready for the WKND`

#### Más títulos y descripciones {#more}

* **Título de página**: un título que se usará en la página
   * Normalmente lo utilizan los componentes de título
   * Si está vacío, se utiliza **Título**.
* **Título de navegación**: puede especificar un título independiente para utilizarlo en la navegación (por ejemplo, si desea algo más conciso).
   * Si está vacío, se utiliza **Título**.
* **Subtítulo**: un subtítulo para usar en la página
* **Descripción**: la descripción de la página, su propósito o cualquier otro detalle que desee agregar

#### Tiempo de activación/desactivación {#on-time}

El tiempo de activación/desactivación de una página es una forma cómoda de ocultar temporalmente contenido que ya se ha publicado. El contenido permanece en la instancia de publicación cuando está desactivado. Desactivar una página no cancela la publicación del contenido.

* **Tiempo de activación**: la fecha y hora a las que se hace visible (procesada) la página publicada en el entorno de publicación. La página debe publicarse, ya sea de forma manual o mediante replicación automática preconfigurada.

   * Si ya se ha [publicado,](/help/sites-authoring/publishing-pages.md) esta página está disponible en la instancia de publicación, pero se mantiene inactiva (oculta) hasta que se procese a la hora especificada.
   * Si no se publica y se configura [para la replicación automática](/help/sites-deploying/replication.md), la página se publicará automáticamente y, a continuación, se procesará a la hora especificada.
   * Si no se publica y no se configura para la replicación automática, la página no se publica automáticamente, por lo que se ve un error 404 al intentar acceder a la página.

* **Tiempo de desactivación**: similar a **Tiempo de activación** y usado a menudo en combinación, define el momento en el que la página publicada se oculta en el entorno de publicación.

Deje estos campos (**Tiempo de activación** y **Tiempo de inactividad**) vacíos para las páginas que desee publicar y disponibles de inmediato y disponibles en el entorno de publicación hasta que se desactiven (el escenario normal).

>[!NOTE]
>Si el **Tiempo de activación** o el **Tiempo de desactivación** se sitúan en el pasado y se configura la replicación automática, la acción relevante se activa de inmediato.

>[!TIP]
>
>Los tiempos de activación/desactivación tratan estrictamente el contenido que ya se ha publicado (ya sea de forma manual o mediante replicación automática). Por este motivo, los flujos de trabajo de publicación, como los de aprobación de contenido, no se activan por los tiempos de activación/desactivación y los tiempos de activación/desactivación no afectan al estado de publicación de la página. Por este motivo, los momentos de activación y desactivación son los más adecuados para mostrar u ocultar temporalmente contenido que ya se ha aprobado y publicado.
>
>Si desea publicar contenido nuevo con todos los flujos de trabajo asociados o eliminar por completo (cancelar la publicación) del sitio, considere [administrar la publicación.](/help/sites-authoring/publishing-pages.md#manage-publication)

#### URL mnemónica {#vanity-url}

Introduzca una URL de vanidad para esta página, que puede permitirle tener una URL más corta o expresiva.

Por ejemplo, si la URL de vanidad se establece en `welcome` para la página identificada por la ruta de acceso `/v1.0/startpage` para el sitio web `http://example.com,`, `http://example.com/welcome` sería la URL de vanidad de `http://example.com/content/v1.0/startpage`

>[!CAUTION]
>
>URL de vanidad:
>
>* Debe ser único.
>* No admiten patrones regex.
>* No debe configurarse en una página existente.

Configure Dispatcher para habilitar el acceso a las URL de vanidad. Consulte [Habilitar el acceso a las URL de vanidad](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#enabling-access-to-vanity-urls-vanity-urls) para obtener más información.

* **Agregar**: toque o haga clic para agregar una URL de vanidad.
* **Quitar**: toque o haga clic para quitar una URL de vanidad.
  **Redirigir URL de vanidad**: indica si desea que la página use la URL de vanidad o redirija a la URL real de la página

### Avanzado  {#advanced}

#### Configuración {#settings}

* **Idioma**: el idioma de la página
* **Raíz del idioma**: si la página es la raíz de una copia en un idioma, es necesario marcar esta opción
* **Redirigir**: indica la página a la cual esta deberá redirigirse automáticamente
* **Diseño** - Indica el [diseño](/help/sites-developing/designer.md) que se usará para esta página.
* **Alias**: especifica un alias que se usará con esta página
   * Por ejemplo, si define un alias de `private` para la página `/content/wknd/us/en/magazine/members-only`, se puede acceder a esta página también mediante `/content/wknd/us/en/magazine/private`
   * La creación de un alias establece la propiedad `sling:alias` en el nodo de página, lo que solo afecta al recurso, no a la ruta del repositorio.
   * No se pueden publicar páginas a las que se accede mediante alias en el editor. Las [Opciones de publicación](/help/sites-authoring/publishing-pages.md) del editor solo están disponibles para las páginas a las que se accede a través de sus rutas reales.
   * Para obtener más información, consulte [Nombres de páginas localizados en Procedimientos recomendados para la administración de direcciones URL y SEO](/help/managing/seo-and-url-management.md#localized-page-names).

#### Configuración {#configuration}

* **Heredado de &lt;*ruta*>** - Habilitar/deshabilitar la herencia de **Configuración de nube** para la página
* **Configuración de nube**: la ruta a la configuración

#### Configuración de plantilla {#templates}

* **Plantillas permitidas**: [define la lista de plantillas que están disponibles](/help/sites-authoring/templates.md#allowingatemplate) dentro de esta rama secundaria

#### Requisito de autenticación {#authentication}

* **Habilitar**: habilita (o deshabilita) el uso de la autenticación para que pueda acceder a la página
* **Página de inicio de sesión**: la página que se usará para iniciar sesión

>[!NOTE]
>
>Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](/help/sites-authoring/editing-page-properties.md#permissions)**.

>[!CAUTION]
>
>La pestaña **[Permisos](#permissions)** permite editar las configuraciones de CUG en función de la presencia del mixin `granite:AuthenticationRequired`. Si los permisos de página se configuran utilizando configuraciones de CUG obsoletas, según la presencia de la propiedad `cq:cugEnabled`, se muestra un mensaje de advertencia en **Requisito de autenticación** y la opción no se puede editar, como tampoco lo son los [Permisos](/help/sites-authoring/editing-page-properties.md#permissions).
>
>
>En tal caso, los permisos de CUG deben editarse en la [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

#### Exportar {#export}

* **Configuración** - Especifica una configuración de exportación

#### SEO {#seo}

* **URL canónica**: se usa para sobrescribir la URL canónica de la página
   * Si se deja en blanco, la dirección URL de la página es su dirección URL canónica.
* **Etiquetas de robots**: utilice el menú desplegable para seleccionar las etiquetas de robots y controlar el comportamiento de los rastreadores de los motores de búsqueda
   * Algunas opciones entran en conflicto entre sí, en cuyo caso la opción más permisiva tiene prioridad.
* **Generar mapa de sitio**: cuando se selecciona, se genera un `sitemap.xml` para esta página y sus descendientes.

### Imágenes {#images}

#### Imagen destacada {#featured-image}

Esta sección se utiliza para seleccionar y configurar la imagen que desea mostrar. Se utiliza en los componentes que hacen referencia a la página; por ejemplo, teasers, listas de páginas, etc.

* **Imagen** - Puedes **elegir** un recurso o buscar un archivo para cargar, después **editar** o **borrar** la imagen seleccionada.
* **Texto alternativo**: texto utilizado para representar el significado o la función de la imagen, que suelen utilizar los lectores de pantalla
* **Heredar: valor tomado del recurso DAM**: cuando se selecciona, el texto alternativo se rellena con el valor de los `dc:description`metadatos de DAM.

#### Miniaturas {#thumbnail}

Esta sección se utiliza para seleccionar y configurar la miniatura de la imagen para la página. Se utiliza en los componentes que hacen referencia a la página; por ejemplo, teasers, listas de páginas, etc.

* **Generar vista previa**: genera una vista previa de la página que desea utilizar como miniatura
* **Cargar imagen**: carga una imagen que desea usar como miniatura
* **Seleccionar imagen**: selecciona un recurso existente que desee usar como miniatura
* **Revertir**: esta opción está disponible después de que haya cambiado la miniatura. Si no desea mantener el cambio, puede revertirlo antes de guardarlo.

### Cloud Services {#cloud-services}

* **Configuraciones de Cloud Service**: define qué configuración se usa para los servicios en la nube de la página
* **Heredado de**: para Live Copies y copias de idioma, las configuraciones en la nube se heredan del modelo de forma predeterminada.
   * Anular selección para anular herencia

### Personalización {#personalization}

#### Configuración de ContextHub {#contexthub}

* **Se hereda de**. Las configuraciones de ContextHub se heredan de forma predeterminada de la página principal.
   * Anule la selección para anular la herencia.
* **Ruta de ContextHub** - Selecciona la [configuración de ContextHub](/help/sites-developing/ch-configuring.md)
* **Ruta de segmentos** - Selecciona la [Ruta de segmentos](/help/sites-administering/segmentation.md).

#### Configuración de segmentación {#targeting}

Seleccione una [marca para especificar un ámbito de segmentación.](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>Esta opción requiere una cuenta de usuario en el grupo `Target Adminstrators`.

### Permisos    {#permissions}

Utilice la ficha **Permisos** para definir qué usuarios, grupos o [grupos de usuarios cerrados (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=es) pueden acceder o modificar la página.

* [Agregar permisos](/help/sites-administering/user-group-ac-admin.md)
* [Editar grupo de usuarios cerrado](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
* Ver los [Permisos efectivos](/help/sites-administering/user-group-ac-admin.md)

>[!CAUTION]
>
>La pestaña **Permisos** permite editar las configuraciones de CUG en función de la presencia del mixin `granite:AuthenticationRequired`. Si los permisos de página se configuran utilizando configuraciones de CUG obsoletas, según la presencia de la propiedad `cq:cugEnabled`, se muestra un mensaje de advertencia y los permisos de CUG no se pueden editar, ni se puede editar el requisito de autenticación de la pestaña [Advanced](/help/sites-authoring/editing-page-properties.md#advanced).
>
>
>En tal caso, los permisos de CUG deben editarse en la [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

>[!NOTE]
>
>La pestaña Permisos no permite la creación de grupos de CUG vacíos, lo que puede resultar útil como una forma sencilla de denegar el acceso a todos los usuarios. Para ello, se debe utilizar el Explorador de CRX. Consulte el documento [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md) para obtener más información.

### Modelo {#blueprint}

Esta pestaña solo está visible para páginas que sirven como modelos. Los modelos sirven de base para Live Copies y forman parte de la [Administración de varios sitios](/help/sites-administering/msm.md)

* **Despliegue**: inicia un despliegue del contenido del modelo en Live Copies
* **Información general de Live Copy**: abre una ventana para examinar la estructura de la página de Live Copy
* **Live Copies actuales**: una lista de páginas basadas en (es decir, que son Live Copies de) la página de modelo seleccionada
* **Configuración de despliegue**: define la configuración de despliegue para la página

### Live Copy {#live-copy}

Esta pestaña solo está visible para páginas configuradas como Live Copies. Al igual que con los [modelos,](#blueprint) Live Copies son parte de [Administración de varios sitios.](/help/sites-administering/msm.md)

* **Sincronizar**: sincroniza Live Copy con el modelo, conservando las modificaciones locales
* **Restablecer**: restablece Live Copy al estado del modelo y elimina las modificaciones locales
* **Suspender**: suspende Live Copy de nuevas modificaciones en el despliegue
* **Desasociar** - Desasocia Live Copy del modelo

#### Origen {#source}

* Muestra la ruta del modelo para esta Live Copy

#### Estado {#status}

* Enumera el estado actual de Live Copy de la página

#### Configuración {#live-copy-config}

* **Herencia de Live Copy**: si está marcada, la configuración de Live Copy es efectiva en todas las tareas secundarias.
* **Heredar configuraciones de despliegue de la página principal**: si está marcada, la configuración de despliegue se hereda de la página principal de la página.
* **Elija la configuración de despliegue**: define las circunstancias en las que se propagan las modificaciones desde el modelo y solo está disponible cuando **Heredar configuraciones de despliegue de la página principal** no está seleccionado
* **Lista de rutas excluidas**

## Edición de las propiedades de página   {#editing-page-properties-1}

Puede definir las propiedades de la página:

* Desde la consola **Sitios**:

   * [Creando una página](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un subconjunto de las propiedades)

   * Pulsando o haciendo clic en **Propiedades**

      * Para una sola página
      * Para varias páginas (solo un subconjunto de las propiedades está disponible para su edición en masa)

* Desde el editor de páginas:

   * Utilizando **Información de página** (a continuación, **Abrir propiedades**)

### Desde la consola Sitios: página individual {#from-the-sites-console-single-page}

Tocando o haciendo clic en **Propiedades** para definir las propiedades de la página:

1. Mediante la consola **Sitios**, desplácese hasta la ubicación de la página para la que desee ver y editar las propiedades.

1. Seleccione la opción **Propiedades** de la página requerida mediante:

   * [Acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#selectionmode)

   Las propiedades de página se muestran mediante las pestañas adecuadas.

1. Visualice o edite las propiedades según sea oportuno. 

1. A continuación, usa **Guardar** para guardar las actualizaciones, seguido de **Cerrar** para poder volver a la consola.

### Al editar una página {#when-editing-a-page}

Al editar una página, puede usar **Información de página** para definir las propiedades de la página:

1. Abra la página para la que desee editar las propiedades.

1. Seleccione el icono **Información de página** para abrir el menú de selección:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Seleccione **Abrir propiedades** y se abrirá un cuadro de diálogo que le permitirá editar las propiedades, ordenadas por la pestaña correspondiente. Los siguientes botones también están disponibles en la parte derecha de la barra de herramientas:

   * **Cancelar**
   * **Guardar y cerrar**

1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 

### Desde la consola Sitios: varias páginas {#from-the-sites-console-multiple-pages}

Desde la consola **Sitios**, puede seleccionar varias páginas y luego usar **Ver propiedades** para ver o editar las propiedades de la página. Esto se conoce como edición masiva de propiedades de página.

>[!NOTE]
>
>La edición de propiedades por lotes también está disponible para los archivos. Es similar, pero difiere en unos pocos puntos. Consulte [Edición de propiedades de varios Assets](/help/assets/metadata.md) para obtener más información.
>
>También está el [Editor en lotes](/help/sites-administering/bulk-editor.md). Este editor le permite buscar contenido de varias páginas con GQL (Google Query Language) y, a continuación, editar el contenido directamente con el Editor por lotes antes de guardar los cambios en las páginas de origen.

Puede seleccionar varias páginas para editarlas por lotes mediante varios métodos, entre ellos:

* Al examinar la consola **Sites**
* Después de usar **Buscar** para localizar un conjunto de páginas

![epp-01](assets/epp-01.png)

Después de seleccionar las páginas y luego hacer clic o pulsar la opción **Propiedades**, se muestran las propiedades por lotes:

![epp-02](assets/epp-02.png)

Solo se pueden editar por lotes las siguientes páginas:

* Las que compartan el mismo tipo de recurso.
* Las que no formen parte de una Live Copy.

   * Si alguna de las páginas está en una Live Copy, se muestra un mensaje cuando se abran las propiedades.

Una vez introducida la edición masiva, puede hacer lo siguiente:

* **Ver**

  Cuando vea Propiedades de página para varias páginas, podrá ver lo siguiente:

   * Una lista de las páginas afectadas

      * Si es necesario, puede seleccionar o deseleccionar

   * Pestañas

      * Las propiedades se ordenan en pestañas, al igual que cuando se visualizan las propiedades de una página.

   * Un subconjunto de propiedades

      * Se pueden ver las propiedades que están disponibles en todas las páginas seleccionadas (deben haberse marcado específicamente como disponibles para la edición por lotes).
      * Si reduce la selección de páginas a una sola página, se verán todas las propiedades.

   * Propiedades comunes con un valor común

      * En el modo Ver solo se muestran las propiedades con un valor común.
      * Cuando el campo es de varios valores (por ejemplo, Etiquetas), los valores solo se muestran cuando *todos* son comunes. Si solo algunas son comunes, solo se muestran al editar.

  Cuando no existen propiedades con un valor común, se muestra un mensaje. 

* **Editar**

  Al editar Propiedades de página para varias páginas:

   * Puede actualizar los valores en los campos disponibles.

      * Los nuevos valores se aplican a todas las páginas seleccionadas cuando selecciona **Listo**.
      * Cuando el campo tiene varios valores (por ejemplo, Etiquetas), puede anexar un nuevo valor o quitar un valor común.

   * Los campos que son comunes, pero que tienen valores diferentes en las distintas páginas, se indican con un valor especial como el texto `<Mixed Entries>`.

>[!NOTE]
>
>El componente de página se puede configurar para especificar los campos disponibles para la edición por lotes. Consulte [Configuración de la página para editar las propiedades de la página](/help/sites-developing/bulk-editing.md).
