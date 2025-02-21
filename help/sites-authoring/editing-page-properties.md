---
title: Edición de propiedades de página de contenido
description: Defina las propiedades necesarias para una página en Adobe Experience Manager.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 42%

---

# Edición de las propiedades de página  {#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar según la naturaleza de la página. Por ejemplo, algunas páginas podrían estar conectadas a una Live Copy, mientras que otras no lo están y la información de la Live Copy está disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas.

### Básico {#basic}

* **Título**

  El título de la página se muestra en varias ubicaciones. Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.

  Este es un campo obligatorio.

* **Etiquetas**

  Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección:

   * Después de seleccionar una etiqueta, aparece debajo del cuadro de selección. Puede quitar una etiqueta de esta lista utilizando la x.
   * Se puede introducir una etiqueta nueva escribiendo el nombre en un cuadro de selección vacío.

      * La etiqueta nueva se crea al pulsar Intro.
      * La etiqueta nueva se muestra con una pequeña estrella a la derecha que indica que se trata de una etiqueta nueva.

   * Con la funcionalidad desplegable, puede seleccionar entre las etiquetas existentes.
   * Aparece una x cuando pasa el ratón sobre una entrada de etiqueta en el cuadro de selección, que se puede utilizar para quitar esa etiqueta para esa página.

  Para obtener más información sobre las etiquetas, consulte [Uso de etiquetas](/help/sites-authoring/tags.md).

* **Ocultar en navegación**

  Indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante.

* **Marca**

  Aplique una identidad de marca uniforme en todas las páginas adjuntando un slug de marca al título de cada página. Esta funcionalidad requiere el uso del componente de página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)

   * **Sobrescribir**: marque para definir el slug de marca en esta página.
      * El valor lo hereda cualquier página secundaria a menos que también tenga valores establecidos de **Sobrescribir**.
   * **Sobrescribir valor**: el texto del slug de marca que se añadirá al título de la página.
      * El valor se anexa al título de la página después de un carácter de barra vertical como “Ciclismo en Toscana | Siempre listo para WKND”
* **Título de página**

  Título que se utilizará en la página. Normalmente se utiliza en los componentes de título. Si está vacío, se utiliza **Título**.

* **Título de navegación**

  Puede especificar un título independiente para utilizarlo en la navegación (por ejemplo, si desea algo más conciso). Si está vacío, se utiliza **Título**.

* **Subtítulo**

  Un subtítulo para usar en la página.

* **Descripción**

  La descripción de la página, su propósito o cualquier otro detalle que desee agregar.

* **A Tiempo**

  La fecha y la hora en que se activa la página publicada. Cuando se publica, esta página permanece inactiva hasta el momento especificado.

  Deje estos campos vacíos para las páginas que desee publicar inmediatamente (el escenario normal).

* **Tiempo de inactividad**

  Hora a la que se desactiva la página publicada.

  De nuevo, deje estos campos vacíos para una acción inmediata.

* **URL mnemónica**

  Introduzca una URL de vanidad para esta página, que puede permitirle tener una URL más corta o expresiva.

  Por ejemplo, si la URL de vanidad se establece en `welcome` para la página identificada por la ruta de acceso `/v1.0/startpage` para el sitio web `http://example.com,`, `http://example.com/welcome` sería la URL de vanidad de `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >URL de vanidad:
  >
  >* Debe ser único. Asegúrese de que otra página no esté usando ya el valor.
  >* No admiten patrones regex.
  >* No debe configurarse en una página existente.
  >

  Configure Dispatcher para habilitar el acceso a las URL de vanidad. Consulte [Habilitar el acceso a las URL de vanidad](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) para obtener más información.

* **Redirigir URL de vanidad**

  Indica si desea que la página use la URL de vanidad.

### Avanzado  {#advanced}

* **Idioma**

  El idioma de la página.

* **Raíz de idioma**

  Si la página es la raíz de una copia en un idioma, es necesario marcar esta opción.

* **Redirigir**

  Indique la página a la que esta página debe redirigirse automáticamente.

* **Design**

  Indique el [diseño](/help/sites-developing/designer.md) que se usará para esta página.

* **Alias**

  Especifique un alias para utilizarlo con esta página.

   * Por ejemplo, si define un alias de `private` para la página `/content/wknd/us/en/magazine/members-only`, se puede acceder a esta página también mediante `/content/wknd/us/en/magazine/private`
   * La creación de un alias establece la propiedad `sling:alias` en el nodo de página, lo que solo afecta al recurso, no a la ruta del repositorio.
   * No se pueden publicar páginas a las que se accede mediante alias en el editor. Las [Opciones de publicación](/help/sites-authoring/publishing-pages.md) del editor solo están disponibles para las páginas a las que se accede a través de sus rutas reales.
   * Para obtener más información, consulte [Nombres de páginas localizados en Procedimientos recomendados para la administración de direcciones URL y SEO](/help/managing/seo-and-url-management.md#localized-page-names).

* **Heredado de &lt;*ruta*>**

  Indica si la página se hereda. y de dónde.

* **Configuración de la nube**

  La ruta a la configuración.

* **Plantillas permitidas**

  [Defina la lista de plantillas disponibles](/help/sites-authoring/templates.md#allowingatemplate) dentro de esta rama secundaria.

* **Habilitar** (requisito de autenticación)

  Habilite (o deshabilite) el uso de la autenticación para poder acceder a la página.

  >[!NOTE]
  >
  >Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](/help/sites-authoring/editing-page-properties.md#permissions)**.

  >[!CAUTION]
  >
  >La pestaña **[Permisos](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permite editar las configuraciones de CUG en función de la presencia del mixin `granite:AuthenticationRequired`. Si los permisos de página se configuran utilizando configuraciones de CUG obsoletas, según la presencia de la propiedad `cq:cugEnabled`, se muestra un mensaje de advertencia en **Requisito de autenticación** y la opción no se puede editar, como tampoco lo son los [Permisos](/help/sites-authoring/editing-page-properties.md#permissions).
  >
  >
  >En tal caso, los permisos de CUG deben editarse en la [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Página de inicio de sesión**

  La página que se utilizará para iniciar sesión.

* **Configuración de exportación**

  Especifique una configuración de exportación.

### Miniatura    {#thumbnail}

Muestra la miniatura de la página. Puede hacer lo siguiente:

* **Generar vista previa**

  Genere una previsualización de la página que desee utilizar como miniatura.

* **Cargar imagen**

  Cargue una imagen que desee utilizar como miniatura.

* **Seleccionar imagen**

  Seleccione un recurso existente que desee utilizar como miniatura.

* **Revertir**

  Esta opción está disponible después de cambiar la miniatura. Si no desea mantener el cambio, puede revertirlo antes de guardarlo.

### Redes sociales {#social-media}

* **Compartir en redes sociales**

  Define las opciones de uso compartido disponibles en la página. Expone las opciones disponibles para el [componente principal de uso compartido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html).

   * **Habilitar el uso compartido de usuarios en Facebook**
   * **Habilitar el uso compartido de usuarios en Pinterest**
   * **Variación de XF preferida**
Definir la variación del fragmento de experiencia que se utiliza para generar metadatos para una página

### Cloud Services {#cloud-services}

* **Cloud Services**

  Defina propiedades para [servicios en la nube](/help/sites-developing/extending-cloud-config.md).

### Personalización {#personalization}

* **Configuración de ContextHub**

  Seleccione la [configuración de ContextHub](/help/sites-developing/ch-configuring.md) y la [ruta de acceso de los segmentos](/help/sites-administering/segmentation.md).

* **Configuración de ámbito**

  Seleccione una [marca para especificar un ámbito de objetivo](/help/sites-authoring/target-adobe-campaign.md).

  >[!NOTE]
  >Esta opción requiere una cuenta de usuario en el grupo `Target Adminstrators`.

### Permisos    {#permissions}

* **Permisos**

  En esta pestaña puede:

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

* **Modelo**

  Defina propiedades para una página de modelo en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagan las modificaciones a Live Copy.

### Live Copy {#live-copy}

* **Live Copy**

  Defina propiedades para una página Live Copy en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagan las modificaciones desde el modelo.

### Estructura del sitio    {#site-structure}

* Proporcione vínculos a páginas que proporcionan funcionalidad para todo el sitio, como **Página de suscripción**, **Página sin conexión**, entre otros.

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
