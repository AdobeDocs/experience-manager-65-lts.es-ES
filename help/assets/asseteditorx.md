---
title: Ampliar editor de recursos
description: Obtenga información sobre cómo ampliar las capacidades del Editor de recursos mediante componentes personalizados.
contentOwner: AG
role: User, Admin
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 12%

---

# Ampliar editor de recursos {#extending-asset-editor}

El editor de recursos es la página que se abre cuando se hace clic en un recurso encontrado a través del uso compartido de recursos, lo que permite al usuario editar aspectos del recurso, como metadatos, miniaturas, títulos y etiquetas.

La configuración del editor mediante los componentes de edición predefinidos se explica en [Creación y configuración de una página del editor de recursos](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

Además de utilizar componentes de editor preexistentes, [!DNL Adobe Experience Manager] desarrolladores también pueden crear sus propios componentes.

## Crear una plantilla del editor de recursos {#creating-an-asset-editor-template}

En Geometrixx se incluyen las siguientes páginas de muestra:

* Página de muestra de Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Plantilla de muestra: `/apps/geometrixx/templates/asseteditor`
* Componente de página de muestra: `/apps/geometrixx/components/asseteditor`

### Configurar Clientlib {#configuring-clientlib}

Los componentes de [!DNL Assets] utilizan una extensión de la clientlib de edición de WCM. Los clientlibs generalmente se cargan en `init.jsp`.

En comparación con la carga clientlib predeterminada (en `init.jsp` del núcleo), una plantilla [!DNL Assets] debe tener lo siguiente:

* La plantilla debe incluir `cq.dam.edit` clientlib (en lugar de `cq.wcm.edit`).

* La clientlib también debe incluirse en el modo WCM desactivado (por ejemplo, cargado en la **publicación**) para poder procesar los predicados, las acciones y las lentes.

En la mayoría de los casos, copiar la muestra existente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) debe satisfacer estas necesidades.

### Configuración de acciones de JS {#configuring-js-actions}

Algunos de los componentes [!DNL Assets] requieren funciones JS definidas en `component.js`. Copie este archivo en el directorio de componentes y vincúlelo.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

El ejemplo carga este origen de JavaScript en `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Hojas de estilos adicionales {#additional-style-sheets}

Algunos de los componentes [!DNL Assets] utilizan la biblioteca de widgets. Para que se represente correctamente en el contexto de contenido, se debe cargar una hoja de estilo adicional. El componente de acción de etiqueta requiere uno más.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Hoja de estilos de Geometrixx {#geometrixx-style-sheet}

Los componentes de página de muestra requieren que todos los selectores comiencen con `.asseteditor` de `static.css` (`/etc/designs/geometrixx/static.css`). Práctica recomendada: Copie todos los selectores `.asseteditor` en la hoja de estilos y ajuste las reglas como desee.

### FormChooser: Ajustes para los recursos cargados finalmente {#formchooser-adjustments-for-eventually-loaded-resources}

El editor de recursos utiliza el selector de formularios, que permite editar recursos (en este caso recursos) en la misma página de formulario simplemente añadiendo un selector de formulario y la ruta del formulario a la URL del recurso.

Por ejemplo:

* Página sin formato: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Recurso cargado en la página del formulario: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Los identificadores de ejemplo de `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) hacen lo siguiente:

* Detectan si se carga un recurso o si debe mostrarse el formulario sin formato.
* Si se carga un recurso, se desactiva el modo WCM, ya que parsys solo se puede editar en una página de formulario sin formato.
* Si se carga un recurso, utiliza su título en lugar del de la página del formulario.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

En la parte de HTML, utilice el conjunto de títulos anterior (recurso o título de página):

```html
<title><%= title %></title>
```

## Crear un componente de campo de formulario simple {#creating-a-simple-form-field-component}

En este ejemplo se describe cómo generar un componente que muestra y muestra los metadatos de un recurso cargado.

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo, `/apps/geometrixx/components/samplemeta`.
1. Agregar `content.xml` con el siguiente fragmento:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Agregar `samplemeta.jsp` con el siguiente fragmento:

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Para que el componente esté disponible, hace falta poder editarlo. Para poder editar un componente, en CRXDE Lite, agregue un nodo `cq:editConfig` de tipo principal `cq:EditConfig`. Para poder quitar párrafos, agregue una propiedad de varios valores `cq:actions` con un solo valor de `DELETE`.

1. Vaya al explorador y en la página de muestra (por ejemplo, `asseteditor.html`) cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos.

1. En el modo de **edición**, el nuevo componente (por ejemplo, **Metadatos de muestra**) ya está disponible en la barra de tareas (que se encuentra en el grupo **Editor de recursos**). Inserte el componente. Para poder almacenar los metadatos, estos se deben agregar al formulario de metadatos.

## Modificar opciones de metadatos {#modifying-metadata-options}

Puede modificar las áreas de nombres disponibles en el [formulario de metadatos](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

Los metadatos disponibles actualmente están definidos en `/libs/dam/options/metadata`:

* El primer nivel dentro de este directorio contiene los espacios de nombres.
* Los elementos dentro de cada área de nombres representan un metadato, como los resultados en un elemento de elemento local.
* El contenido de los metadatos contiene la información del tipo y las opciones de varios valores.

Las opciones se pueden sobrescribir en `/apps/dam/options/metadata`:

1. Copie el directorio de `/libs` a `/apps`.

1. Quitar, modificar o agregar elementos.

>[!NOTE]
>
>Si agrega nuevas áreas de nombres, deben estar registradas en su repositorio/CRX. De lo contrario, el envío del formulario de metadatos producirá un error.
