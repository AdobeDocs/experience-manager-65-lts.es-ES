---
title: Edición de propiedades de página
description: Las propiedades de una página pueden variar según la naturaleza de la página. Por ejemplo, algunas páginas podrían estar conectadas a una Live Copy, mientras que otras no lo están y la información de la Live Copy estará disponible según corresponda.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 23%

---

# Edición de las propiedades de página  {#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar según la naturaleza de la página. Por ejemplo, algunas páginas podrían estar conectadas a una Live Copy, mientras que otras no lo están y la información de la Live Copy estará disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas:

### Básica {#basic}

* **Título**

  El título de la página se muestra en varias ubicaciones. Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.

  Este es un campo obligatorio.

* **Etiquetas**

  Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección:

   * Después de seleccionar una etiqueta, aparece debajo del cuadro de selección. Puede quitar una etiqueta de esta lista utilizando la x.
   * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.

     La nueva etiqueta se creará cuando pulse Intro. La nueva etiqueta se muestra en un cuadro, con una pequeña estrella a la derecha que indica que es una etiqueta nueva.

   * Con la funcionalidad desplegable puede seleccionar etiquetas existentes.
   * Aparece una x cuando pasa el ratón sobre una entrada de etiqueta en el cuadro de selección; esto se puede utilizar para quitar esa etiqueta de esta página.

* **Ocultar en navegación**

  Conmutador para indicar si se muestra o se oculta la página en la navegación por páginas.

* **Título de página**

  Título que se utilizará en la página.

* **Título de navegación**

  Puede especificar un título independiente para utilizarlo en la navegación (por ejemplo, si desea algo más conciso). Si está vacío, se utiliza **Título**.

* **Subtítulo**

  Un subtítulo para usar en la página.

* **Descripción**

  La descripción de la página, su propósito o cualquier otro detalle que desee añadir.

* **A Tiempo**

  La fecha y hora a las que se activará la página publicada. Cuando se publique, esta página se mantendrá inactiva hasta el momento especificado.

  Deje estos campos vacíos para las páginas que desee publicar inmediatamente (el escenario normal).

* **Tiempo de inactividad**

  Hora a la que se desactivará la página publicada.

  De nuevo, deje estos campos vacíos para las páginas que desee publicar inmediatamente.

* **URL mnemónica**

  Permite introducir una URL de vanidad para esta página. Esto permite tener una URL más corta y expresiva.

  Por ejemplo, si la URL de vanidad se establece en w `elcome` para la página identificada por la ruta / `v1.0/startpage` para el sitio web h `ttp://example.com,`, h `ttp://example.com/welcome` sería la URL de vanidad de h `ttp://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >URL de vanidad:
  >
  >* debe ser único, por lo que debe tener cuidado de que el valor no lo esté utilizando otra página.
  >* no admiten patrones regex.

* **Redirigir URL de vanidad**

  Indica si desea que la página use la URL de vanidad.

### Avanzado  {#advanced}

* **Idioma**

  El idioma de la página.

* **Redirigir**

  Indique la página a la que esta página debe redirigirse automáticamente.

* **Design**

  Indique el [diseño](/help/sites-developing/designer.md) que se usará para esta página.

* **Alias**

  Especifique un alias para utilizarlo con esta página.

* **Habilitar grupo de usuarios cerrado**

  Habilita (o deshabilita) el uso de [grupos de usuarios cerrados](/help/sites-administering/cug.md) (CUG).

* **Página de inicio de sesión**

  La página que se utilizará para iniciar sesión.

* **Grupos admitidos**

  Grupos aptos para iniciar sesión en el CUG.

* **Dominio**

  Nombre de dominio para el CUG.

* **Configuración de exportación**

  Especifique una configuración de exportación.

### Miniatura    {#thumbnail}

* **Miniatura de página**

  Muestra la miniatura de la página. Puede hacer lo siguiente:

   * **Generar vista previa**

     Genere una previsualización de la página para utilizarla como miniatura.

   * **Cargar imagen**

     Cargue una imagen para utilizarla como miniatura.

### Cloud Services {#cloud-services}

* **Cloud Services**

  Defina propiedades para [servicios en la nube](/help/sites-developing/extending-cloud-config.md).

### Personalización {#personalization}

* **Personalización**

  Seleccione una [marca para especificar un ámbito de objetivo](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Permisos   {#permissions}

* **Permisos** (IU táctil optimizada)

  Vea los [permisos efectivos y agregue nuevos permisos](/help/sites-administering/user-group-ac-admin.md).

### Modelo {#blueprint}

* **Modelo**

  Defina propiedades para una página de modelo en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagarán las modificaciones a Live Copy.

### Live Copy    {#live-copy}

* **Live Copy**

  Defina propiedades para una página Live Copy en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las cuales se propagarán las modificaciones desde el modelo.

### Estructura del sitio    {#site-structure}

* Proporcione vínculos a páginas que proporcionan funcionalidad para todo el sitio, como **Página de suscripción**, **Página sin conexión**, entre otros.

## Edición de las propiedades de página   {#editing-page-properties-2}

### Edición de propiedades de página para una página específica {#editing-page-properties-for-a-specific-page}

Propiedades de página define las distintas propiedades de la página, como los títulos, cuando aparecen en el sitio web y en otros.

1. Abra la página que desee editar.

1. En la barra de tareas, abra la pestaña **Página** y, a continuación, seleccione **Propiedades de página...**

   Esto abre un cuadro de diálogo con varias pestañas.

1. Realice los cambios que necesite y, a continuación, haga clic en **Aceptar** para guardar.
