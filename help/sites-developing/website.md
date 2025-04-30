---
title: Crear un sitio web con todas las funciones (JSP)
description: Este tutorial le enseña a crear un sitio web completo con Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 743645c5-b4c9-45ff-a130-0bf72aa6e6f2
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '4919'
ht-degree: 2%

---

# Crear un sitio web con todas las funciones (JSP){#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>Este artículo describe cómo crear un sitio web con JSP y en función de la IU clásica. Adobe recomienda utilizar las tecnologías de Adobe Experience Manager (AEM) más recientes para sus sitios web, tal como se describe en detalle en el artículo [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md).

Este tutorial le permite crear un sitio web con todas las funciones con AEM. El sitio web se basará en un sitio web genérico y está dirigido principalmente a los desarrolladores web. Todo el desarrollo se realiza dentro de un entorno de creación.

Este tutorial describe cómo:

1. Instale AEM.
1. Acceda a CRXDE Lite (el entorno de desarrollo).
1. Configure la estructura del proyecto en CRXDE Lite.
1. Cree la plantilla, el componente y los scripts utilizados como base para crear páginas de contenido.
1. Cree la página raíz del sitio web y, a continuación, las páginas de contenido.
1. Cree los siguientes componentes para utilizarlos en sus páginas:

   * Navegación superior
   * Lista de secundarios
   * Logotipo
   * Imagen
   * Text-Image
   * Búsqueda

1. Incluir varios componentes de base.

Después de realizar todos los pasos, las páginas deben tener el siguiente aspecto:

![chlimage_1-24](assets/chlimage_1-24.png)

**Descargar el resultado final**

Para seguir junto con el tutorial en lugar de realizar los ejercicios, descargue website-1.0.zip. Este archivo es un paquete de contenido de AEM que contiene los resultados de este tutorial. Use [Administrador de paquetes](/help/sites-administering/package-manager.md) para instalar el paquete en la instancia de autor.

**NOTA:** Al instalar este paquete, se sobrescriben los recursos de la instancia de creación que haya creado mediante este tutorial.

Paquete de contenido del sitio web

[Obtener archivo](assets/website-1_0.zip)

## Instalación de Adobe Experience Manager {#installing-adobe-experience-manager}

Para instalar una instancia de AEM para desarrollar el sitio web, siga las instrucciones para configurar un entorno de implementación [con instancias de autor y publicación](/help/sites-deploying/deploy.md#author-and-publish-installs), o realice una [instalación genérica](/help/sites-deploying/deploy.md#default-local-install). La instalación genérica implica descargar el archivo JAR de Quickstart de AEM, colocar el archivo license.properties en el mismo directorio que el archivo JAR y hacer doble clic en el archivo JAR.

Una vez instalado AEM, acceda al entorno de desarrollo de CRXDE Lite haciendo clic en el vínculo CRXDE Lite en la página de bienvenida:

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>La dirección URL de CRXDE Lite para una instancia de creación de AEM instalada localmente mediante el puerto predeterminado es [https://localhost:4502/crx/de/](https://localhost:4502/crx/de/).

### Configuración de la estructura del proyecto en CRXDE Lite {#setting-up-the-project-structure-in-crxde-lite}

Utilice CRXDE Lite para crear la estructura de la aplicación mywebsite en el repositorio:

1. En el árbol de la izquierda de CRXDE Lite, haga clic con el botón derecho en la carpeta **`/apps`** y luego haga clic en **Crear** > **Crear** **carpeta**. En el cuadro de diálogo **Crear carpeta**, escriba `mywebsite` como nombre de la carpeta y haga clic en **Aceptar**.
1. Haga clic con el botón derecho en la carpeta **`/apps/mywebsite`** y luego haga clic en **Crear** > **Crear carpeta**. En el cuadro de diálogo **Crear carpeta**, escriba `components` como nombre de la carpeta y haga clic en **Aceptar**.
1. Haga clic con el botón derecho en la carpeta **`/apps/mywebsite`** y luego haga clic en **Crear** > **Crear carpeta**. En el cuadro de diálogo **Crear carpeta**, escriba `templates` como nombre de la carpeta y haga clic en **Aceptar**.

   La estructura del árbol debería tener un aspecto similar al siguiente:

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Haga clic en **Guardar todo**.

### Configuración del diseño {#setting-up-the-design}

En esta sección, se crea el diseño para la aplicación mediante la herramienta Designer. El diseño proporciona recursos de CSS e imagen para el sitio web.

>[!NOTE]
>
>Haga clic en el siguiente vínculo para descargar mywebsite.zip. El archivo contiene el archivo static.css y los archivos de imagen para el diseño.

Archivo static.css de muestra e imágenes

[Obtener archivo](assets/mywebsite.zip)

1. En la página de bienvenida de AEM, haga clic en **Herramientas**. ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. En el árbol de carpetas, seleccione la carpeta **Diseños** y, a continuación, haga clic en **Nuevo** > **Nueva página**. Escriba `mywebsite` como título y haga clic en **Crear**.

1. Si el elemento de mi sitio Web no aparece en la tabla, actualice el árbol o la tabla.

1. [Usando WebDAV](/help/sites-administering/webdav-access.md) acceso a la dirección URL en https://localhost:4502, copie el archivo de muestra `static.css` y la carpeta `images` del archivo mywebsite.zip descargado en la carpeta `/etc/designs/mywebsite`.

   ![chlimage_1-28](assets/chlimage_1-28.png)

### Creación de la plantilla, el componente y el script de la página de contenido {#creating-the-contentpage-template-component-and-script}

En esta sección, cree lo siguiente:

* Plantilla de página de contenido que se utiliza para crear páginas de contenido en el sitio web de ejemplo.
* Componente de página de contenido que se utiliza para procesar páginas de contenido.
* El script de la página de contenido.

#### Creación de la plantilla de página de contenido {#creating-the-contentpage-template}

Cree una plantilla para utilizarla como base de las páginas web del sitio.

Una plantilla define el contenido predeterminado de una nueva página. Los sitios web complejos pueden utilizar varias plantillas para crear los distintos tipos de páginas del sitio. En este ejercicio, todas las páginas se basan en una plantilla simple.

1. En el árbol de carpetas de CRXDE Lite, haga clic con el botón secundario en `/apps/mywebsite/templates` y haga clic en **Crear** > **Crear plantilla**.

1. En el cuadro de diálogo Crear plantilla, escriba los siguientes valores y haga clic en **Siguiente**:

   * **Etiqueta**: contentpage
   * **Título**: Plantilla de página de contenido de Mi sitio web
   * **Descripción**: Esta es la plantilla de página de contenido de mi sitio web
   * **Tipo de recurso:** mywebsite/components/contentpage

   Utilice el valor predeterminado para la propiedad Ranking.

   ![chlimage_1-29](assets/chlimage_1-29.png)

   El tipo de recurso identifica el componente que procesa la página. En este caso, el componente `mywebsite/components/contentpage` procesa todas las páginas creadas con la plantilla contentpage.

1. Para especificar las rutas de acceso de las páginas que pueden utilizar esta plantilla, haga clic en el botón más y escriba `/content(/.*)?` en el cuadro de texto que aparece. A continuación, haga clic en **Siguiente**.

   ![chlimage_1-30](assets/chlimage_1-30.png)

   El valor de la propiedad path permitida es una expresión regular *.* Las páginas que tienen una ruta de acceso que coincide con la expresión pueden utilizar la plantilla. En este caso, la expresión regular coincide con la ruta de la carpeta **/content** y todas las subpáginas.

   Cuando un autor crea una página debajo de /content, la plantilla **contentpage** aparece en una lista de plantillas disponibles para usar.

1. Haga clic en **Siguiente** en los paneles **Padres permitidos** y **Hijos permitidos** y haga clic en **Aceptar**. En CRXDE Lite, haga clic en **Guardar todo**.

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### Creación del componente Página de contenido {#creating-the-contentpage-component}

Cree el *componente* que define el contenido y procesa las páginas que utilizan la plantilla contentpage. La ubicación del componente debe corresponder con el valor de la propiedad Tipo de recurso de la plantilla de página de contenido.

1. En CRXDE Lite, haga clic con el botón derecho en `/apps/mywebsite/components` y luego en **Crear** > **Componente**.
1. En el cuadro de diálogo **Crear componente**, escriba los siguientes valores de propiedad:

   * **Etiqueta**: contentpage
   * **Título**: Componente Página de contenido de Mi sitio web
   * **Descripción**: Este es el componente Página de contenido de mi sitio web

   ![chlimage_1-32](assets/chlimage_1-32.png)

   La ubicación del nuevo componente es `/apps/mywebsite/components/contentpage`. Esta ruta corresponde al tipo de recurso de la plantilla contentpage (menos la parte inicial **`/apps/`** de la ruta).

   Esta correspondencia conecta la plantilla con el componente y es crítica para el correcto funcionamiento del sitio web.

1. Haga clic en **Siguiente** hasta que aparezca el panel Elementos secundarios permitidos del cuadro de diálogo y, a continuación, haga clic en **Aceptar**. En CRXDE Lite, haga clic en **Guardar todo**.

   La estructura ahora tiene el siguiente aspecto:

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### Desarrollo del script del componente Contentpage {#developing-the-contentpage-component-script}

Agregue código al script contentpage.jsp para definir el contenido de la página.

1. En CRXDE Lite, abra el archivo `contentpage.jsp` en `/apps/mywebsite/components/contentpage`. El archivo contiene el siguiente código de forma predeterminada:

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. Copie el siguiente código y péguelo en contentpage.jsp después del código predeterminado:

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. Haga clic en **Guardar todo** para guardar los cambios.

### Creación de páginas de sitio web y páginas de contenido {#creating-your-website-page-and-content-pages}

En esta sección, crea las siguientes páginas que utilizan la plantilla de página de contenido: Mi sitio web, Inglés, Productos, Servicios y Clientes.

1. En la página de bienvenida de AEM ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html)), haga clic en Sitios web.

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. En el árbol de carpetas, seleccione la carpeta **Sitios web** y, a continuación, haga clic en **Nuevo** > **Nueva página**.
1. En la ventana **Crear página**, escriba lo siguiente:

   * Título: `My Website`
   * Nombre: `mywebsite`
   * Seleccione el(la) `My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. Haga clic en **Crear**. En el árbol de carpetas, seleccione la página **/Sitios web/Mi sitio web** y haga clic en **Nuevo** > **Nueva página**.
1. En el cuadro de diálogo Crear página, escriba los siguientes valores de propiedad y haga clic en Crear:

   * Título: Español
   * Nombre: en
   * Seleccione la plantilla Página de contenido de Mi sitio web

1. En el árbol de carpetas, seleccione la página **/Sitios web/Mi sitio web/Inglés** y haga clic en **Nueva**> **Nueva página**.
1. En el cuadro de diálogo **Crear página**, escriba los siguientes valores de propiedad y haga clic en **Crear**:

   * Título: Productos
   * Seleccione la plantilla Página de contenido de Mi sitio web

1. En el árbol de carpetas, seleccione la página **/Sitios web/Mi sitio web/Inglés** y haga clic en **Nuevo** > **Nueva página**.
1. En el cuadro de diálogo **Crear página**, escriba los siguientes valores de propiedad y haga clic en **Crear**:

   * Título: Servicios
   * Seleccione la plantilla Página de contenido de Mi sitio web

1. En el árbol de carpetas, seleccione la página **/Sitios web/Mi sitio web/Inglés** y haga clic en **Nuevo** > **Nueva página**.
1. En el cuadro de diálogo **Crear página**, escriba los siguientes valores de propiedad y haga clic en **Crear**:

   * Título: Clientes
   * Seleccione la plantilla Página de contenido de Mi sitio web

   La estructura tiene el siguiente aspecto:

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. Para vincular sus páginas al diseño misitio web, seleccione el nodo `/content/mywebsite/en/jcr:content` en CRXDE Lite. En la ficha Propiedades, escriba los siguientes valores para una nueva propiedad y haga clic en Agregar:

   * Nombre: cq:designPath
   * Tipo: cadena
   * Valor: /etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. En una nueva ficha o ventana del explorador web, abra [https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html) para ver la página Productos:

   ![chlimage_1-38](assets/chlimage_1-38.png)

### Mejora del script de la página de contenido {#enhancing-the-contentpage-script}

En esta sección se describe cómo mejorar el script de la página de contenido mediante los scripts de componentes de base de AEM y escribiendo sus propios scripts.

Cuando haya terminado, la página **Productos** debería tener el siguiente aspecto:

![chlimage_1](assets/chlimage_1.jpeg)

#### Uso de los scripts de página base {#using-the-foundation-page-scripts}

En este ejercicio, configure el componente contenido de página para que su supertipo sea el componente Página de AEM. Dado que los componentes heredan las funciones de su supertipo, el contenido de la página hereda los scripts y las propiedades del componente Página.

Por ejemplo, en el código JSP del componente, puede hacer referencia a los scripts que proporciona el componente de supertipo como si estuvieran incluidos en el componente.

1. En CRXDE Lite, agregue una propiedad al nodo `/apps/mywebsite/components/contentpage`.

   1. Seleccione el nodo `/apps/mywebsite/components/contentpage`.
   1. En la parte inferior de la pestaña Propiedades, escriba los siguientes valores de propiedad y haga clic en Agregar:

      * **Nombre:** sling:resourceSuperType
      * **Tipo:** cadena
      * **Valor:** foundation/components/page

   1. Haga clic en Guardar todo.

1. Abra el archivo `contentpage.jsp` en `/apps/mywebsite/components/contentpage` y reemplace el código existente por el siguiente código:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. Tiene el siguiente aspecto:

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   Abra el origen de la página para ver los elementos de JavaScript y HTML que generaron los scripts head.jsp y body.jsp. El siguiente fragmento de script abre Sidekick al abrir la página:

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### Uso de sus propios scripts {#using-your-own-scripts}

En esta sección se crean varios scripts que generan una parte del cuerpo de la página. A continuación, cree el archivo body.jsp en el componente pagecontent para anular el body.jsp del componente Page de AEM. En el archivo body.jsp, incluye los scripts que generan las diferentes partes del cuerpo de la página.

**Sugerencia:** Cuando un componente incluye un archivo que tiene el mismo nombre y ubicación relativa que un archivo del supertipo del componente, se denomina *superposición*.

1. En CRXDE Lite, cree el archivo `left.jsp` en `/apps/mywebsite/components/contentpage`:

   1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/contentpage` y, a continuación, seleccione **Crear **luego **Crear archivo**.

   1. En la ventana, escriba `left.jsp` como **Nombre** y haga clic en **Aceptar**.

1. Edite el archivo `left.jsp` para eliminar el contenido existente y reemplace con el siguiente código:

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. Guarde los cambios.
1. En CRXDE Lite, cree el archivo `center.jsp` en `/apps/mywebsite/components/contentpage`:

   1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/contentpage`, seleccione **Crear** y, a continuación, **Crear archivo**.

   1. En el cuadro de diálogo, escriba `center.jsp` como **Nombre** y haga clic en **Aceptar**.

1. Edite el archivo `center.jsp` para eliminar el contenido existente y reemplácelo por el siguiente código:

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. Guarde los cambios.
1. En CRXDE Lite, cree el archivo `right.jsp` en `/apps/mywebsite/components/contentpage`:

   1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/contentpage`, seleccione **Crear** y, a continuación, **Crear archivo**.

   1. En el cuadro de diálogo, escriba `right.jsp` como **Nombre** y haga clic en **Aceptar**.

1. Edite el archivo `right.jsp` para eliminar el contenido existente y reemplace con el siguiente código:

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. Guarde los cambios.
1. En CRXDE Lite, cree el archivo `body.jsp` en `/apps/mywebsite/components/contentpage`:
1. Edite el archivo `body.jsp` para eliminar el contenido existente y reemplace con el siguiente código:

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. Tiene el siguiente aspecto:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Creación del componente de navegación superior {#creating-the-top-navigation-component}

En esta sección, se crea un componente que muestra vínculos a todas las páginas de nivel superior del sitio web para facilitar la navegación. Este contenido de componente aparece en la parte superior de todas las páginas que se crean con la plantilla de página de contenido.

En la primera versión del componente de navegación superior (navegación superior), los elementos de navegación solo son vínculos de texto. En la segunda versión, se implementa la navegación superior con vínculos de navegación de imágenes.

Cuando haya terminado, la navegación superior debería tener el siguiente aspecto:

![chlimage_1-39](assets/chlimage_1-39.png)

#### Creación del componente de navegación superior {#creating-the-top-navigation-component-1}

1. En CRXDE Lite, haga clic con el botón derecho en `/apps/mywebsite/components`, seleccione **Crear** y luego **Crear componente**.
1. En la ventana **Crear componente**, escriba lo siguiente:

   * **Etiqueta**: `topnav`

   * **Título**: `My Top Navigation Component`

   * **Descripción**: `This is My Top Navigation Component`

1. Haz clic en **Siguiente** hasta que llegues a la última ventana donde hiciste clic en **Aceptar**. Guarde los cambios.

#### Creación del script de navegación superior con vínculos de texto {#creating-the-top-navigation-script-with-textual-links}

Añada el script de renderización a la barra de navegación superior para generar vínculos de texto a páginas secundarias:

1. En CRXDE Lite, abra el archivo `topnav.jsp` en `/apps/mywebsite/components/topnav`.
1. Reemplace el código que se encuentra allí copiando y pegando el código siguiente:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### Inclusión de la navegación superior en el componente Página de contenido {#including-top-navigation-in-the-contentpage-component}

Para incluir la navegación superior en el componente de página de contenido:

1. En CRXDE Lite, abra `body.jsp` en `/apps/mywebsite/components/contentpage` y reemplace:

   ```xml
   <div class="topnav">topnav</div>
   ```

   con:

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. La navegación superior aparece de la siguiente manera:

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### Mejora de páginas con subtítulos {#enhancing-pages-with-subtitles}

El componente Página define las propiedades que permiten proporcionar subtítulos para las páginas. Agregue subtítulos que proporcionen información sobre el contenido de la página.

1. En su explorador, abra la página **Productos**.
1. En la ficha **Página** de Sidekick, haga clic en **Propiedades de página**.
1. En la ficha Básico del cuadro de diálogo, expanda **Más títulos y descripción** y, para la propiedad **Subtítulo**, escriba **lo que hacemos**. Haga clic en **OK**.
1. Repita los pasos anteriores para agregar el subtítulo **acerca de nuestros servicios** a la página **Servicios**.
1. Repita los pasos anteriores para agregar el subtítulo **la confianza que ganamos** a la página **Clientes**.

   **Sugerencia:** En CRXDE Lite, seleccione el nodo /content/mywebsite/en/products/jcr:content para ver que se agrega la propiedad subtitle.

#### Mejore la navegación superior mediante vínculos de imagen {#enhance-top-navigation-by-using-image-links}

Mejore el script de renderización del componente de navegación superior para utilizar vínculos de imagen en lugar de hipertexto para los controles de navegación. La imagen incluye el título y el subtítulo del destino del vínculo.

Este ejercicio muestra el procesamiento de [solicitudes Sling](/help/sites-developing/the-basics.md#sling-request-processing). El script topnav.jsp se modifica para llamar a un script que genere dinámicamente imágenes que se utilizarán para los vínculos de navegación de la página. En este ejercicio, Sling analiza la dirección URL de los archivos de origen de la imagen para determinar el script que se utilizará para procesar las imágenes.

Por ejemplo, el origen del vínculo de imagen a la página Productos podría ser https://localhost:4502/content/mywebsite/en/products.navimage.png. Sling analiza esta dirección URL para determinar el tipo de recurso y la secuencia de comandos que se utilizará para procesar el recurso:

1. Sling determina la ruta del recurso que se va a `/content/mwebysite/en/products.png.`
1. Sling coincide con esta ruta de acceso con el nodo `/content/mywebsite/en/products`.
1. Sling determina que `sling:resourceType` de este nodo es `mywebsite/components/contentpage`.

1. Sling encuentra el script en este componente que mejor coincide con el selector de URL ( `navimage`) y la extensión de nombre de archivo ( `png`).

En este ejercicio, Sling hace coincidir estas direcciones URL con el script /apps/mywebsite/components/contentpage/navimage.png.java que cree.

1. En CRXDE Lite, abra `topnav.jsp` en `/apps/mywebsite/components/topnav.`Busque el contenido del elemento de anclaje (línea 14):

   ```xml
   <%=child.getTitle() %>
   ```

1. Reemplace el contenido del anclaje con el siguiente código:

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. Guarde los cambios.
1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/contentpage` y haga clic en **Crear** > **Crear archivo**.
1. En la ventana **Crear archivo**, como **Nombre**, escriba `navimage.png.java`.

   La extensión de nombre de archivo .java indica a Sling que la compatibilidad con Apache Sling Scripting Java™ debe utilizarse para compilar el script y crear un servlet.

1. Copie el código siguiente en `navimage.png.java.`El código amplía la clase AbstractImageServlet:

   * [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) crea un objeto ImageContext que almacena las propiedades del recurso actual.
   * La página principal del recurso se extrae del objeto ImageContext. A continuación, se obtienen el título y el subtítulo de la página.
   * [ImageHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/ImageHelper.html) se usa para generar la imagen a partir del archivo navimage_bg.jpg del diseño del sitio, el título de la página y el subtítulo de la página.

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. La navegación superior ahora aparece de la siguiente manera:

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### Creación del componente Lista de elementos secundarios {#creating-the-list-children-component}

Cree el componente listchildren que genera una lista de vínculos de página con el título, la descripción y la fecha de las páginas (por ejemplo, páginas de productos). Los vínculos se dirigen a las páginas secundarias de la página actual o de una página raíz especificada en el cuadro de diálogo del componente.

![chlimage_1-41](assets/chlimage_1-41.png)

#### Creación de páginas de producto {#creating-product-pages}

Cree dos páginas ubicadas debajo de la página Productos. Para cada página que describe dos productos específicos, se establece un título, una descripción y una fecha.

1. En el árbol de carpetas de la página Sitios web, seleccione el elemento Sitios web/Mi sitio web/Inglés/Productos y haga clic en Nuevo > Nueva página.
1. En el cuadro de diálogo, introduzca los siguientes valores de propiedad y haga clic en Crear:

   * Título: Producto 1.
   * Nombre: product1.
   * Seleccionar plantilla de página de contenido de Mi sitio web

1. Cree otra página debajo de Productos con los siguientes valores de propiedad:

   * Título: Producto 2
   * Nombre: product2
   * Seleccionar plantilla de página de contenido de Mi sitio web

1. En CRXDE Lite, defina una descripción y una fecha para la página del producto 1:

   1. Seleccione el nodo `/content/mywebsite/en/products/product1/jcr:content`.
   1. En la ficha **Propiedades**, escriba los siguientes valores:

      * Nombre: `jcr:description`
      * Tipo: `String`
      * Valor: `This is a description of the Product 1!.`

   1. Haga clic en **Agregar**.
   1. En la ficha **Propiedades**, cree otra propiedad con los siguientes valores:

      * Nombre: date
      * Tipo: cadena
      * Valor: 14/02/2008
      * Haga clic en Agregar.

   1. Haga clic en Guardar todo.

1. En CRXDE Lite, defina una descripción y una fecha para la página del producto 2:

   1. Seleccione el nodo /content/mywebsite/en/products/product2/jcr:content.
   1. En la ficha **Propiedades**, escriba los siguientes valores:

      * Nombre: jcr:description
      * Tipo: cadena
      * Valor: Esta es una descripción del producto 2.

   1. Haga clic en **Agregar**.
   1. En los mismos cuadros de texto, reemplace los valores anteriores por los siguientes valores:

      * Nombre: date
      * Tipo: cadena
      * Valor: 11/05/2012
      * Haga clic en Agregar.

   1. Haga clic en Guardar todo.

#### Creación del componente Lista de elementos secundarios {#creating-the-list-children-component-1}

Para crear el componente listchildren:

1. En CRXDE Lite, haga clic con el botón derecho en `/apps/mywebsite/components`, seleccione **Crear** y luego **Crear componente**.
1. En el cuadro de diálogo, introduzca los siguientes valores de propiedad y haga clic en Siguiente:

   * Etiqueta: listchildren.
   * Título: Componente Mis listas secundarias.
   * Descripción: Este es el componente Mis listas de elementos secundarios.

1. Siga haciendo clic en Siguiente hasta que aparezca el panel Elementos secundarios permitidos y, a continuación, haga clic en Aceptar.

#### Creación de la secuencia de comandos List Children {#creating-the-list-children-script}

Desarrolle la secuencia de comandos para el componente listchildren.

1. En CRXDE Lite, abra el archivo `listchildren.jsp` en `/apps/mywebsite/components/listchildren`.
1. Reemplace el código predeterminado por el siguiente código:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. Guarde los cambios.

#### Creación del cuadro de diálogo Lista de secundarios {#creating-the-list-children-dialog}

Cree el cuadro de diálogo que se utiliza para configurar las propiedades del componente listchildren.

1. Cree el nodo de diálogo en el componente listchildren:

   1. En CRXDE Lite, haga clic con el botón derecho en el nodo `/apps/mywebsite/components/listchildren`y haga clic en **Crear** > **Crear cuadro de diálogo**.

   1. En el cuadro de diálogo, introduzca los siguientes valores de propiedad y haga clic en Aceptar

      * **Etiqueta**: `dialog`

      * **Título**: `Edit Component` y haga clic en **Aceptar**.

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   Con las siguientes propiedades:

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. Seleccione el nodo `/apps/mywebsite/components/listchildren/dialog/items/items/tab1`.
1. En la pestaña Propiedades, cambie el valor de la propiedad **title** a `List Children`

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. Seleccione el nodo tab1 y haga clic en Crear > Crear nodo, introduzca los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: elementos
   * Tipo: cq:WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. Cree un nodo debajo del nodo de elementos con los siguientes valores de propiedad:

   * Nombre: listroot
   * Tipo: cq:Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. Agregue propiedades al nodo listroot para configurarlo como un campo de texto. Cada fila de la siguiente tabla representa una propiedad. Cuando termine, haga clic en Guardar todo.

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | fieldLabel | Cadena | Ruta de raíz de lista |
   | name | Cadena | ./listroot |
   | xtype | Cadena | textfield |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### Inclusión de elementos secundarios de lista en el componente Página de contenido {#including-list-children-in-the-contentpage-component}

Para incluir el componente listchildren en el componente de página de contenido, siga este procedimiento:

1. En CRXDE Lite, abra el archivo `left.jsp` en `/apps/mywebsite/components/contentpage` y busque el siguiente código (línea 4):

   ```xml
   <div>newslist</div>
   ```

1. Reemplace ese código con el siguiente código:

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. Guarde los cambios.

#### Visualización de elementos secundarios de lista en una página {#viewing-list-children-in-a-page}

Para ver el funcionamiento completo de este componente, puede ver la página Productos:

* cuando la página principal (&quot;Ruta de la raíz de la lista&quot;) no está definida.
* cuando se define la página principal (&quot;Ruta de raíz de lista&quot;).

1. En el explorador, vuelva a cargar la página Productos. El componente listchildren aparece de la siguiente manera:

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. Como ruta de acceso de la raíz de la lista, escriba: `/content/mywebsite/en`. Haga clic en Aceptar. El componente listchildren de la página ahora tiene el siguiente aspecto:

   ![chlimage_1-45](assets/chlimage_1-45.png)

### Creación del componente Logotipo {#creating-the-logo-component}

Cree un componente que muestre el logotipo de la empresa y proporcione un vínculo a la página principal del sitio. El componente contiene un cuadro de diálogo en modo de diseño para que los valores de propiedad se almacenen en el diseño del sitio (/etc/designs/mywebsite):

* Los valores de propiedad se aplican a todas las instancias del componente que se agregan a las páginas que utilizan el diseño.
* Las propiedades se pueden configurar con cualquier instancia del componente que se encuentre en una página que utilice el diseño.

El cuadro de diálogo en modo de diseño contiene propiedades para configurar la imagen y la ruta del vínculo. El componente de logotipo se coloca en la parte superior izquierda de todas las páginas del sitio web.

Cuando haya terminado, debería tener el siguiente aspecto:

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager proporciona un componente de logotipo con más funciones ( `/libs/foundation/components/logo`).

#### Creación del nodo del componente Logotipo {#creating-the-logo-component-node}

Para crear el componente de logotipo, siga los pasos:

1. En CRXDE Lite, haga clic con el botón derecho en /apps/mywebsite/components, seleccione **Crear** y, a continuación, **Crear componente**.
1. En el cuadro de diálogo Crear componente, escriba los siguientes valores de propiedad y haga clic en Siguiente:

   * Etiqueta: `logo`.
   * Título: `My Logo Component`.
   * Descripción: `This is My Logo Component`.

1. Haga clic en Siguiente hasta que llegue al panel final del cuadro de diálogo y, a continuación, haga clic en **Aceptar**.

#### Creación del script del logotipo {#creating-the-logo-script}

En esta sección se describe cómo crear la secuencia de comandos para mostrar la imagen del logotipo con un vínculo a la página principal.

1. En CRXDE Lite, abra el archivo `logo.jsp` en `/apps/mywebsite/components/logo`.
1. El siguiente código crea el vínculo a la página principal del sitio y agrega una referencia a la imagen del logotipo. Copie el código en `logo.jsp`:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. Guarde los cambios.

#### Creación del cuadro de diálogo Diseño del logotipo {#creating-the-logo-design-dialog}

Cree el cuadro de diálogo para configurar el componente de logotipo en el modo Diseño. Los nodos del cuadro de diálogo en modo de diseño deben llamarse `design_dialog`.

1. Cree el nodo de diálogo en el componente del logotipo:

   1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/logo` y haga clic en **Crear** > **Crear cuadro de diálogo**.

   1. Escriba los siguientes valores de propiedad y haga clic en Aceptar:

      * **Etiqueta:** `design_dialog`

      * **Título:** `Logo (Design)`

1. Haga clic con el botón derecho en el nodo tab1 de la rama design_dialog y haga clic en Eliminar. Haga clic en Guardar todo.
1. En el nodo `design_dialog/items/items`, cree un nodo denominado `img` de tipo `cq:Widget`. Agregue las siguientes propiedades y haga clic en Guardar todo:

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | fileNameParameter | Cadena | ./imageName |
   | fileReferenceParameter | Cadena | ./imageReference |
   | name | Cadena | ./image |
   | título | Cadena | Imagen |
   | xtype | Cadena | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### Creación del script de procesamiento del logotipo {#creating-the-logo-render-script}

Cree la secuencia de comandos que recupera la imagen del logotipo y la escribe en la página.

1. Haga clic con el botón derecho en el nodo del componente logotipo y haga clic en Crear > Crear archivo para crear el archivo de script denominado img.GET.java.
1. Abra el archivo, copie el siguiente código en el archivo y, a continuación, haga clic en Guardar todo:

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* do not create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### Adición del componente Logotipo al componente Página de contenido {#adding-the-logo-component-to-the-contentpage-component}

1. En CRXDE Lite, abra `left.jsp` en `/apps/mywebsite/components/contentpage file` y busque la siguiente línea de código:

   ```xml
   <div>logo</div>
   ```

1. Reemplace ese código con la siguiente línea de código:

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. El logotipo tiene el siguiente aspecto, aunque actualmente solo muestra el vínculo subyacente:

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### Configuración de la imagen del logotipo en una página {#setting-the-logo-image-in-a-page}

En esta sección se describe cómo establecer una imagen como logotipo mediante el cuadro de diálogo de modo de diseño.

1. Con la página Productos abierta en el explorador, haga clic en el botón Diseño en la parte inferior de Sidekick para entrar en el modo de diseño.

   ![Botón Diseño indicado por un cuadrado derecho.](do-not-localize/chlimage_1-1.png)

1. En la barra Diseño del logotipo, haga clic en Editar para utilizar el cuadro de diálogo y editar la configuración del componente Logotipo.
1. En el cuadro de diálogo, haga clic en el panel de la pestaña Imagen, busque la imagen logo.png que ha extraído del archivo mywebsite.zip y haga clic en Aceptar.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Haga clic en el triángulo de la barra de título de Sidekick para volver al modo de edición.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. En CRXDE Lite, vaya al siguiente nodo para ver los valores de las propiedades almacenadas:

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### Inclusión del componente Ruta de exploración {#including-the-breadcrumb-component}

En esta sección, se incluye el componente Ruta de exploración (pista), que es uno de los componentes de base.

1. En CRXDE Lite, vaya a `/apps/mywebsite/components/contentpage`, abra el archivo `center.jsp` y reemplace:

   ```java
   <div>trail</div>
   ```

   con:

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página **Productos 1**. El componente de seguimiento tiene el siguiente aspecto:

   ![chlimage_1-50](assets/chlimage_1-50.png)

### Inclusión del componente Título {#including-the-title-component}

En esta sección, se incluye el componente de título, que es uno de los componentes de base.

1. En CRXDE Lite, vaya a `/apps/mywebsite/components/contentpage`, abra el archivo `center.jsp` y reemplace:

   ```xml
   <div>title</div>
   ```

   con:

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página Productos. El componente de título tiene el siguiente aspecto:

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **Nota**: puede establecer un Título y el Tipo/Tamaño diferentes en el modo de edición.

### Inclusión del componente Sistema de párrafos {#including-the-paragraph-system-component}

El sistema de párrafos (parsys) es una parte significativa de un sitio web, ya que administra una lista de párrafos. Permite a los autores añadir componentes de párrafo a la página y proporciona estructura.

Agregue el componente parsys (uno de los componentes de base) al componente contentpage.

1. En CRXDE Lite, vaya a `/apps/mywebsite/components/contentpage`, abra el archivo `center.jsp` y busque la línea de código siguiente:

   ```xml
   <div>parsys</div>
   ```

1. Reemplace esa línea de código con el siguiente código y, a continuación, guarde los cambios:

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. En el explorador, actualice la página Productos. Ahora tiene el componente parsys, que se ve de la siguiente manera:

   ![chlimage_1-52](assets/chlimage_1-52.png)

### Creación del componente de imagen {#creating-the-image-component}

Cree un componente que muestre una imagen en el sistema de párrafos. Para ahorrar tiempo, el componente de imagen se crea como una copia del componente del logotipo con algunos cambios de propiedad.

>[!NOTE]
>
>Adobe Experience Manager proporciona un componente de imagen con más características completas ( `/libs/foundation/components/image`).

#### Creación del componente de imagen {#creating-the-image-component-1}

1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components/logo` y haga clic en Copiar.
1. Haga clic con el botón derecho en el nodo `/apps/mywebsite/components` y haga clic en Pegar.
1. Haga clic con el botón secundario en el nodo `Copy of logo`, haga clic en Cambiar nombre, elimine el texto existente y escriba `image`.

1. Seleccione el nodo de componente `image` y cambie los siguientes valores de propiedad:

   * `jcr:title:` Mi componente de imagen.
   * `jcr:description`: Este es mi componente de imagen.

1. Agregue una propiedad al nodo `image` con los siguientes valores de propiedad:

   * Nombre: componentGroup
   * Tipo: cadena
   * Valor: MyWebsite

1. Bajo el nodo `image`, cambie el nombre del nodo `design_dialog` a `dialog`.

1. Cambiar nombre de `logo.jsp` a `image.jsp.`

1. Abra img.GET.java y cambie el paquete a `apps.mywebsite.components.image`.

![chlimage_1-53](assets/chlimage_1-53.png)

#### Creación del script de imagen {#creating-the-image-script}

En esta sección se describe cómo crear el script de imagen.

1. Abrir `/apps/mywebsite/components/image/` `image.jsp`
1. Reemplace el código existente por el siguiente código y, a continuación, guarde los cambios:

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. Guarde los cambios.

#### Creación del nodo Image cq:editConfig {#creating-the-image-cq-editconfig-node}

El tipo de nodo `cq:editConfig` le permite configurar ciertos comportamientos de los componentes al editar sus propiedades.

En esta sección, se utiliza un nodo cq:editConfig para permitir arrastrar recursos desde el Buscador de contenido al componente de imagen.

1. En CRXDE Lite, en el nodo /apps/mywebsite/components/image, cree un nodo de la siguiente manera:

   * Nombre: cq:editConfig.
   * Tipo: cq:EditConfig.

1. En el nodo cq:editConfig, cree un nodo como se indica a continuación:

   * Nombre: cq:dropTargets.
   * Tipo: cq:DropTargetConfig.

1. En el nodo cq:dropTargets, cree un nodo como se indica a continuación:

   * Nombre: image.
   * Tipo: nt:unstructured.

1. En CRXDE, establezca las propiedades como se indica a continuación:

| Nombre | Tipo | Valor  |
|---|---|---|
| aceptar | Cadena | image/(gif | jpeg | png) |
| grupos | Cadena | medios |
| propertyName | Cadena | ./imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### Adición del icono {#adding-the-icon}

En esta sección, se agrega el icono para que aparezca junto al componente de imagen cuando aparezca en Sidekick:

1. En CRXDE Lite, haga clic con el botón secundario en el archivo `/libs/foundation/components/image/icon.png` y seleccione **Copiar.**
1. Haga clic con el botón secundario en el nodo `/apps/mywebsite/components/image`, haga clic en **Pegar** y, a continuación, haga clic en **Guardar todo**.

#### Uso del componente de imagen {#using-the-image-component}

En esta sección, verá la página **Productos** y agregará el componente de imagen al sistema de párrafos.

1. En el explorador, vuelva a cargar la página **Productos**.
1. En Sidekick, haga clic en el icono **modo de diseño**.
1. Haga clic en el botón Editar para editar el cuadro de diálogo de diseño de la pieza.
1. En el cuadro de diálogo, se muestra una lista de **Componentes permitidos**; navegue hasta **MyWebsite**, seleccione el **Componente de mi imagen** y haga clic en **Aceptar.**
1. Volver al **modo de edición.**
1. Haga doble clic en el marco parsys (en **Arrastrar componentes o recursos aquí**). Los selectores **Insertar nuevo componente** y **Sidekick** tienen el siguiente aspecto:

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### Inclusión del componente Barra de herramientas {#including-the-toolbar-component}

En esta sección, se incluye el componente barra de herramientas, que es uno de los componentes base.

Tiene varias opciones en los modos de edición y diseño.

1. En CRXDE Lite, vaya a `/apps/mywebsite/components/contentpage`, abra el archivo `body.jsp` y busque el siguiente código:

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. Reemplace ese código con el siguiente código y, a continuación, guarde los cambios.

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. En el árbol de carpetas de la página Sitios web de AEM, seleccione Sitios web/Mi sitio web/Inglés y, a continuación, haga clic en Nuevo > Nueva página. Especifique los siguientes valores de propiedad y haga clic en Crear:

   * Título: Barra de herramientas
   * Seleccionar plantilla de página de contenido de Mi sitio web

1. En la lista de páginas, haga clic con el botón secundario en la página Barra de herramientas y haga clic en Propiedades. Seleccione Ocultar en navegación y haga clic en Aceptar.

   La opción Ocultar en navegación evita que la página aparezca en los componentes de navegación, como la navegación superior y los elementos secundarios de lista.

1. En Barra de herramientas, cree las siguientes páginas:

   * Contactos
   * Comentarios
   * Inicio de sesión
   * Búsqueda

1. En el explorador, vuelva a cargar la página Productos. Tiene el siguiente aspecto:

   ![chlimage_1-55](assets/chlimage_1-55.png)

### Creación del componente Buscar {#creating-the-search-component}

En esta sección, se crea el componente para buscar contenido en el sitio web. Este componente de búsqueda se puede colocar en el sistema de párrafos de cualquier página (por ejemplo, en una página de resultados de búsqueda especializada).

Cuando termine, el cuadro de entrada de búsqueda debería tener el aspecto siguiente en la página **English**:

![chlimage_1-56](assets/chlimage_1-56.png)

#### Creación del componente Buscar {#creating-the-search-component-1}

1. En CRXDE Lite, haga clic con el botón derecho en `/apps/mywebsite/components`, seleccione **Crear** y luego **Crear componente**.
1. Utilice el cuadro de diálogo para configurar el componente:

   1. En el primer panel, especifique los siguientes valores de propiedad:

      * Etiqueta: buscar
      * Título: Componente Mi búsqueda
      * Descripción: Este es mi componente de búsqueda
      * Grupo: Mi sitio web

   1. Haga clic en Siguiente y, a continuación, en Siguiente.
   1. En el panel Principales permitidos, haga clic en el botón + y escriba `*/parsys`.
   1. Haga clic en Siguiente y, a continuación, en Aceptar.

1. Haga clic en Guardar todo.
1. Copie los siguientes nodos y péguelos en el nodo apps/mywebsite/components/search:

   * `/libs/foundation/components/search/dialog`
   * &quot;`/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. Haga clic en Guardar todo.

#### Creación del script de búsqueda {#creating-the-search-script}

En esta sección se describe cómo crear el script de búsqueda:

1. Abra el archivo `/apps/mywebsite/components/search/search.jsp`.
1. Copie el siguiente código en `search.jsp`:

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. Guarde los cambios.

#### Incluir un cuadro de búsqueda en el componente Página de contenido {#including-a-search-box-in-the-contentpage-component}

Para incluir un cuadro de entrada de búsqueda en la sección izquierda de la página de contenido, siga este procedimiento:

1. En CRXDE Lite, abra el archivo `left.jsp` en `/apps/mywebsite/components/contentpage` y busque el siguiente código (línea 2):

   ```xml
   %><div class="left">
   ```

1. Inserte el siguiente código **antes** de esa línea:

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. Busque la siguiente línea de código:

   ```xml
   <div>search</div>
   ```

1. Reemplace ese código con el siguiente código y, a continuación, guarde los cambios.

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. En el explorador, vuelva a cargar la página Productos. El componente de búsqueda tiene el siguiente aspecto:

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### Inclusión del componente Buscar en la página Buscar {#including-the-search-component-in-the-search-page}

En esta sección, agregará el componente de búsqueda al sistema de párrafos.

1. En el explorador, abra la página Buscar.
1. En Sidekick, haga clic en el icono de modo de diseño.
1. En el bloque Diseño de la parte (debajo del título Buscar), haga clic en Editar.
1. En el cuadro de diálogo, desplácese hacia abajo hasta el grupo **Mis sitios web**, seleccione **Mi componente de búsqueda** y haga clic en **Aceptar**.
1. En Sidekick, haga clic en el triángulo para volver al modo de edición.
1. Arrastre el componente Mi búsqueda desde Sidekick al marco parsys. Tiene el siguiente aspecto:

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. Vaya a la página Productos. Busque clientes en el cuadro de entrada y pulse Intro. Se le redirigirá a la página Buscar. Cambiar a modo de vista previa: la salida tiene un formato similar al siguiente:

   ![chlimage_1-59](assets/chlimage_1-59.png)

### Inclusión del componente Iparsys {#including-the-iparsys-component}

En esta sección, se incluye el componente Sistema de párrafos de herencia (iparsys), que es uno de los componentes de base. Este componente permite crear una estructura de párrafos en una página principal y hacer que las páginas secundarias hereden los párrafos.

Para este componente, puede establecer varios parámetros tanto en el modo de edición como en el modo de diseño.

1. En CRXDE Lite, vaya a `/apps/mywebsite/components/contentpage`, abra el archivo `right.jsp` y reemplace:

   ```java
   <div>iparsys</div>
   ```

   con:

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. Guarde los cambios.
1. En el explorador, vuelva a cargar la página ** productos **. Toda la página tiene el siguiente aspecto:

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
