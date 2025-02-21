---
title: El exportador de página
description: Aprenda a utilizar el Exportador de páginas de Adobe Experience Manager (AEM).
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# El exportador de página{#the-page-exporter}

Adobe Experience Manager (AEM) le permite exportar una página como una página web completa que incluye imágenes, `.js` y `.css` archivos.

Cuando se configura, solicita una exportación de página desde el explorador reemplazando `html` por `export.zip` en la dirección URL. Esto genera un archivo (zip) que contiene la página procesada en formato html, junto con los recursos a los que se hace referencia. Todas las rutas de la página (por ejemplo, las rutas a imágenes) se vuelven a escribir para que apunten a los archivos incluidos en el archivo o a los recursos del servidor. A continuación, se puede descargar el archivo (zip) desde el explorador.

>[!NOTE]
>
>Según el explorador y la configuración, la descarga puede ser:
>
>* un archivo (`<page-name>.export.zip`)
>* una carpeta (`<page-name>`); en la práctica, el archivo de almacenamiento ya está expandido

## Exportar una página {#exporting-a-page}

Los siguientes pasos describen cómo exportar una página y suponen que existe una plantilla de exportación para el sitio. Una plantilla de exportación define la forma en que se exporta una página y es específica del sitio. Para crear una plantilla de exportación, consulte [Creación de una configuración de exportador de página para su sitio](#creating-a-page-exporter-configuration-for-your-site).

Para exportar una página:

1. Vaya a la página requerida en la consola **Sitios**.

1. Seleccione la página y, a continuación, abra el cuadro de diálogo **Propiedades**.

1. Seleccione la pestaña **Avanzadas**.

1. Expanda el campo **Exportar** para seleccionar una plantilla de exportación.
Seleccione la plantilla requerida para su sitio y, a continuación, confirme con **Aceptar**.

1. Seleccione **Guardar y cerrar** para cerrar el cuadro de diálogo de propiedades de la página.

1. Solicite la exportación de la página reemplazando el sufijo `html` por `export.zip` en la dirección URL.

   Por ejemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   Se accede a él mediante:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Descargue el archivo en su sistema de archivos.

1. En el sistema de archivos, descomprima el archivo si es necesario. Cuando se expande, hay una carpeta con el mismo nombre que la página seleccionada. Esta carpeta contiene:

   * la subcarpeta `content`, que es la raíz de una serie de subcarpetas que reflejan la ruta de acceso a la página en el repositorio

      * dentro de esta estructura se encuentra el archivo html de la página seleccionada (`<page-name>.html`)

   * otros recursos (`.js` archivos, `.css` archivos, imágenes, etc.) se encuentran según la configuración de la plantilla de exportación

1. Abra el archivo HTML de página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) en el explorador para que pueda comprobar la representación.

## Creación de una configuración de exportador de página para el sitio {#creating-a-page-exporter-configuration-for-your-site}

El exportador de páginas se basa en el [marco de sincronización de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Las configuraciones disponibles en el cuadro de diálogo **Propiedades de página** son plantillas de exportación que definen las dependencias requeridas para una página.

Cuando se activa una exportación de página, se hace referencia a la plantilla de exportación. Tanto la ruta de página como la ruta de diseño se aplican de forma dinámica. A continuación, el archivo zip se crea mediante la funcionalidad estándar de sincronización de contenido.

Una instalación predeterminada de AEM incluye una plantilla predeterminada en `/etc/contentsync/templates/default`.

* Esta plantilla es la plantilla de reserva cuando no se encuentra ninguna plantilla de exportación en el repositorio.

* La plantilla `default` le muestra cómo se puede configurar una exportación de página, de modo que puede servir de base para una nueva plantilla de exportación.

* Para ver la estructura de nodos de la plantilla en el explorador como formato JSON, solicite la siguiente URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

El método más sencillo para crear una plantilla de exportador de páginas es:

* copiar la plantilla `default`,

* asignar un nombre nuevo, apropiado para su sitio,

* a continuación, realice las actualizaciones necesarias.

Para crear una plantilla completamente nueva:

1. En **CRXDE Lite**, cree un nodo debajo de `/etc/contentsync/templates`:

   * `Name`: un nombre apropiado para su sitio; por ejemplo, `<mysite>`. El nombre aparece en el cuadro de diálogo de propiedades de página al elegir la plantilla del exportador de página.

   * `Type`: `nt:unstructured`

2. Debajo del nodo de plantilla, llamado aquí `mysite`, cree una estructura de nodos utilizando los nodos de configuración que se describen a continuación.

## Activación de una plantilla del exportador de páginas para las páginas {#activating-a-page-exporter-configuration-for-your-pages}

Cuando la plantilla esté configurada, haga que esté disponible:

1. En CRXDE, vaya a la página requerida en la rama `/content`. Puede ser una página individual o la página raíz de un subárbol.

1. En el nodo `jcr:content` de la página, cree la propiedad:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: ruta a la plantilla; por ejemplo: `/etc/contentsync/templates/mysite`

### Nodos de configuración del exportador de página {#page-exporter-configuration-nodes}

La plantilla consiste en una estructura de nodos, ya que usa el [marco de trabajo de sincronización de contenido](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Cada nodo tiene una propiedad `type` que define una acción específica en el proceso de creación del archivo zip.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

Se pueden utilizar los siguientes nodos para crear una plantilla de exportación:

* `page`
El nodo de página se utiliza para copiar el HTML de página en el archivo zip. Tiene las siguientes características:

   * Un nodo obligatorio.
   * Se encuentra por debajo de `/etc/contentsync/templates/<mysite>`.
   * Definido con la propiedad `Name`establecida en `page`.
   * El tipo de nodo es `nt:unstructured`

  El nodo `page` tiene las siguientes propiedades:

   * Una propiedad `type` establecida con el valor `pages`.

   * No tiene una propiedad `path`, ya que la ruta de acceso de la página actual se copia dinámicamente en la configuración.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
El nodo de reescritura define cómo se reescriben los vínculos en la página exportada. Los vínculos reescritos pueden apuntar a los archivos incluidos en el archivo zip o a los recursos del servidor.
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
El nodo de diseño se utiliza para copiar el diseño utilizado para la página exportada. Tiene las siguientes características:

   * Opcional.
   * Se encuentra por debajo de `/etc/contentsync/templates/<mysite>`.
   * Definido con la propiedad `Name` establecida en `design`.
   * Tipo de nodo `nt:unstructured`.

  El nodo `design` tiene las siguientes propiedades:

   * Una propiedad `type` establecida en el valor `copy`.

   * No tiene una propiedad `path`, ya que la ruta de acceso de la página actual se copia dinámicamente en la configuración.

* `generic`
Se utiliza un nodo genérico para copiar recursos como archivos clientlibs `.js` o `.css` en el archivo zip. Tiene las siguientes características:

   * Opcional.
   * Se encuentra por debajo de `/etc/contentsync/templates/<mysite>`.
   * No hay un nombre específico.
   * Tipo de nodo `nt:unstructured`.
   * Tiene una propiedad `type` y propiedades relacionadas `type`. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Por ejemplo, el siguiente nodo de configuración copia los archivos de `mysite.clientlibs.js` en el archivo zip:

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**Implementar una configuración personalizada**

También son posibles las configuraciones personalizadas.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Para cumplir algunos requisitos específicos, implemente un [controlador de actualización personalizado](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## Exportación de una página mediante programación {#programmatically-exporting-a-page}

Para exportar una página mediante programación, puede usar el servicio OSGI [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Este servicio le permite:

* Exporte una página y escriba en la respuesta del servlet HTTP.
* Exporte una página y guarde el archivo zip en una ubicación específica.

El servlet enlazado al selector `export` y la extensión `zip` utilizan el servicio PageExporter.

## Solución de problemas {#troubleshooting}

Si tiene algún problema con la descarga del archivo zip, puede eliminar el nodo `/var/contentsync` del repositorio y volver a enviar la solicitud de exportación.
