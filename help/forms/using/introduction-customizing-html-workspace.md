---
title: Introducción a la personalización de AEM Forms Workspace
description: Una introducción rápida, con información conceptual y técnica, para personalizar LiveCycle AEM Forms Workspace para Process Management.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 97%

---

# Introducción a la personalización de AEM Forms Workspace{#introduction-to-customizing-aem-form-workspace}

AEM Forms Workspace proporciona capacidades para modificar la semántica de presentación y la funcionalidad de su interfaz. A continuación, se describen los tipos de personalizaciones para cambiar el estilo, el diseño, el formato, la personalización de marca y la funcionalidad principal.

![ejemplo_Workspace_personalizado_cu](assets/cu_customized_workspace_example.png)

Ejemplo de personalización de Workspace

## Tipos de personalizaciones {#types-of-customizations}

AEM Forms Workspace admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, su funcionalidad, y mucho más. Las personalizaciones implican actualizar una o más de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes de HTML en otras aplicaciones

### Cambios en la interfaz de usuario {#user-interface-changes}

Puede cambiar el aspecto, el diseño y otra semántica de presentación de AEM Forms Workspace. Cambie el espacio de trabajo personalizando los archivos CSS, HTML y JavaScript™. Todos los archivos predeterminados se proporcionan en la instalación predeterminada.

Los pasos que más suelen aplicarse se explican en [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para ver ejemplos específicos de dichas personalizaciones, incluidos los pasos detallados, consulte los artículos relacionados que aparecen al final de este artículo.

#### Familiarizarse con la hoja de estilos {#understanding-the-style-sheet}

Antes de personalizar Workspace, familiarícese con la hoja de estilos predeterminada que se proporciona con AEM Forms en /libs/ws/css/style.css.

Para personalizar el espacio de trabajo, se recomienda que se familiarice con la hoja de estilo existente, style.css, en la carpeta /libs/ws/css. A continuación se describen algunos componentes destacados.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente de interfaz de usuario modificado</p> </th>
  </tr>
  <tr>
   <td><p>#header</p> </td>
   <td><p>Encabezado de AEM Forms Workspace</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>La lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>El encabezado de la lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>El espacio debajo de la lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoría</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>La categoría seleccionada, con el ratón sobre el estilo de la categoría</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>La página Iniciar proceso (Lista de categorías cerradas)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>La página Tareas pendientes (Lista de filtros cerrada)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>La página Seguimiento (Lista de nombres de proceso cerrada)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>La lista de puntos de inicio o la lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>El encabezado de una lista de puntos de inicio o una lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>El punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>La descripción del punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>El área Tarea</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>El menú desplegable de usuario en el encabezado</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>La lista desplegable Ordenar tarea</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms Workspace toma su apariencia de un archivo CSS. Al personalizar el código CSS, puede cambiar la semántica de presentación de Workspace, como las fuentes, los colores, la personalización de marca y el diseño.

Los pasos de nivel superior para la personalización del código CSS son los siguientes:

* Cree un archivo CSS.
* Agregue elementos de estilo a este archivo CSS. Consulte Familiarizarse con los estilos CSS para obtener más información.
* Actualice sus referencias en `html.jsp`.

Para ver los pasos exactos para realizar estas personalizaciones, consulte [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). El archivo CSS enviado con AEM Forms Workspace se encuentra en /libs/ws/css/. Para llevar a cabo personalizaciones relacionadas con CSS, utilice el [paquete Ship](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Para ver ejemplos específicos de personalizaciones relacionadas con CSS, consulte los temas de la Ayuda relacionados que aparecen al final de este artículo.

#### Imagen {#image}

Puede personalizar AEM Forms Workspace para agregar avatares de usuario o agregar el logotipo de su organización. Para realizar estas personalizaciones, utilice el [paquete Ship](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

Los pasos de nivel superior para la personalización de las imágenes son los siguientes:

* Instale y configure WebDAV.
* Agregue nuevas imágenes.
* Agregue los nuevos estilos correspondientes a las imágenes añadidas.
* Vincule el nuevo archivo CSS al archivo `html.jsp`.

Para empezar a personalizar las imágenes de AEM Forms Workspace, siga las instrucciones que aparecen en [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para ver ejemplos específicos de personalizaciones relacionadas con imágenes, consulte los temas de la Ayuda relacionados que aparecen al final de este artículo.

#### Plantilla HTML {#html-template}

Las plantillas HTML ayudan a definir el aspecto y el diseño de la interfaz de usuario de Workspace. Al actualizar las plantillas HTML predeterminadas, puede personalizar el diseño de la interfaz de usuario predeterminada.

Los pasos de nivel superior para las personalizaciones de la plantilla HTML son los siguientes:

* Realice copias de los archivos predeterminados necesarios en una carpeta creada por el usuario.
* Añada las nuevas plantillas en la carpeta definida por el usuario.
* Realice las actualizaciones relevantes en los archivos copiados; por ejemplo, la ruta de la nueva plantilla.

Para ver ejemplos específicos de estas personalizaciones, consulte los temas de la Ayuda que aparecen al final de este artículo. Elija entre el [paquete Ship](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) o el [paquete Dev](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), según la plantilla que desee personalizar.

### Cambios semánticos {#semantic-changes}

Para modificar la funcionalidad de AEM Forms Workspace, cambie el código fuente JavaScript. Las modificaciones en la funcionalidad principal se etiquetan como cambios semánticos. Los modelos, las vistas y las plantillas se modifican como parte del código fuente de AEM Forms Workspace.

Los pasos de nivel superior para realizar cambios semánticos con el fin de modificar la funcionalidad de AEM Forms Workspace son los siguientes:

* Realice copias de los archivos predeterminados adecuados en una carpeta creada por el usuario.
* Añada los nuevos modelos y vistas en la carpeta definida por el usuario.
* Realice las actualizaciones relevantes, como la actualización de las rutas de los modelos y las vistas recién añadidos en los archivos JavaScript predeterminados.
* Minifique el paquete para optimizar el rendimiento.

Para obtener más información conceptual sobre los componentes que forman parte del código fuente, consulte la [descripción de los componentes reutilizables](/help/forms/using/description-reusable-components.md). Para realizar estas personalizaciones, utilice el paquete Dev.

### Componentes reutilizables {#reusable-components}

Como AEM Forms Workspace es un software basado en componentes, se puede personalizar y reutilizar de forma sencilla. Puede integrar fácilmente los componentes de Workspace con las aplicaciones web.

Para obtener más información conceptual, consulte la [descripción de los componentes reutilizables](/help/forms/using/description-reusable-components.md) y, para obtener instrucciones sobre el uso de los componentes, visite el artículo [Integración de componentes del espacio de trabajo de AEM Forms en aplicaciones web](/help/forms/using/description-reusable-components.md).

## Creación del código de AEM Forms Workspace {#building-html-workspace-code}

### Paquete del SDK {#sdk-package}

El paquete contiene el código fuente de AEM Forms Workspace. El paquete está disponible en `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Está pensado principalmente para las personalizaciones, ya que permite generar lo siguiente:

* Paquetes CRX para los perfiles Ship, Debug y Dev (mencionados a continuación en [Paquetes CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Una versión minificada del código personalizado (para cambios semánticos)

#### Contenido de WS {#ws-content}

* client-pkg:

   * src: contiene los artefactos necesarios para crear nodos CRX.
   * pom.xml: el script para crear paquetes de implementación para varios perfiles y el paquete WS-Deploy.

* client-html:

   * assembly: contiene un zip.xml utilizado por el script para crear el SDK de AEM Forms Workspace.
   * src/main/webapp -

      * css: contiene las hojas de estilo de AEM Forms Workspace.
      * images: contiene las imágenes utilizadas en AEM Forms Workspace.
      * js:

         * libs: contiene todas las bibliotecas de terceros utilizadas en AEM Forms Workspace.
         * licenses: contiene las licencias para archivos HTML y JS, y código para prefijar estas licencias en los respectivos archivos de origen.
         * minifier: se utiliza para la combinación, la minificación y la uglificación del código personalizado JavaScript.
         * resourcejs_optimizer: se utiliza para la combinación, la minificación y la uglificación del origen JavaScript.
         * resource_generator: se utiliza para generar register.js y modelcontrollerpath.js.
         * runtime:

            * inicializer: contiene el archivo initializer.js, utilizado para inicializar las vistas de Backbone y los modelos utilizados en AEM Forms Workspace.
            * models: contiene los modelos de Backbone de todos los componentes presentes en AEM Forms Workspace.
            * routes: contiene los archivos JavaScript y los archivos HTML que cargan páginas Iniciar proceso, Tareas pendientes, Seguimiento y Preferencias en AEM Forms Workspace.
            * services: contiene el archivo service.js, utilizado en AEM Forms Workspace. Todas las llamadas al servidor se realizan mediante service.js.
            * templates: contiene todas las plantillas, es decir, los archivos HTML de todas las vistas de AEM Forms Workspace.
            * util: contiene todos los archivos de utilidad (javascript) que se utilizan en AEM Forms Workspace.
            * views: contiene las vistas de Backbone de todos los componentes de AEM Forms Workspace.

         * main.js
         * router.js

      * libs/ws: pdf.html y pluginPing.pdf se utilizan para cargar formularios PDF en AEM Forms Workspace, y WSNextAdapter.swf se utiliza para cargar formularios y guías SWF.
      * Configuraciones regionales:

         * de-DE: contiene el archivo translation.json para alemán.
         * en-US: contiene el archivo translation.json para inglés.
         * fr-FR: contiene el archivo translation.json para francés.
         * ja-JP: contiene el archivo translation.json para japonés.
         * html.jsp: contiene código para detectar la configuración regional actual del explorador.

      * html.jsp
      * GET.jsp

### Paquete CRX {#crx-package}

El paquete CRX se puede implementar en el repositorio CRX™. Está disponible en `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Este paquete se puede crear utilizando los tres perfiles que se describen a continuación.

| **Perfil** | **Descripción** | **Uso** |
|---|---|---|
| Perfil Ship | Este perfil crea un paquete CRX del tamaño más pequeño posible mediante minificación. Es el paquete más eficiente. Todos los archivos JavaScript™ se combinan y minifican en un solo archivo JS. | Utilice este perfil cuando no sea necesario realizar más cambios semánticos en los archivos JS. |
| Perfil Debug | Este perfil crea un paquete CRX relativamente eficiente. El tamaño del paquete es ligeramente superior al del paquete creado mediante el perfil Ship. Este paquete contiene la mayoría de los archivos JavaScript combinados en un solo archivo JS. | Utilice este perfil para la depuración. |
| Perfil Dev | Este perfil crea un paquete CRX del mayor tamaño posible. Todos los archivos JavaScript están disponibles por separado, tal y como aparecen en el paquete SDK. | Utilice este perfil para incorporar cambios semánticos. |

#### Perfil Ship {#ship-profile}

#### Comando {#command}

* mvn clean: instala el paquete Ship en la carpeta client-pkg del paquete de origen enviado al cliente.
* La ejecución de los comandos del perfil Ship solo funciona en una JVM de 64 bits.

#### Contenido de WS {#ws-content-1}

* css: contiene style.css, ie.css y jquery-ui.css.
* images: contiene todas las imágenes.
* js:

   * libs:

      * need: contiene required.js.
      * jqueryui: contiene jquery.ui.datepicker.ja.js.

   * runtime:

      * templates: contiene todas las plantillas, es decir, los archivos HTML de todos los componentes de AEM Forms Workspace.

   * main.js (combinado, minificado y uglificado).
   * register.js

* libs:

   * ws: contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* Configuraciones regionales:

   * de-DE: contiene el archivo translation.json para alemán.
   * en-US: contiene el archivo translation.json para inglés.
   * fr-FR: contiene el archivo translation.json para francés.
   * ja-JP: contiene el archivo translation.json para japonés.
   * html.jsp: contiene código para detectar la configuración regional actual del explorador.

* Index: contiene .content.xml.
* profile: contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil Debug {#debug-profile}

#### Comando {#command-1}

* mvn clean: instala el paquete Debug en client-pkg.
* La ejecución de los comando del perfil Debug solo funciona en JVM de 64 bits.

#### Contenido de WS {#ws-content-2}

* css: contiene style.css, ie.css y jqueri-ui.css.
* images: contiene todas las imágenes.
* js:

   * libs:

      * need: contiene required.js.
      * jqueryui: contiene jquery.ui.datepicker.ja.js.

   * runtime:

      * templates: contiene todas las plantillas, es decir, los archivos HTML de todos los componentes de AEM Forms Workspace.

   * main.js (combinado).
   * register.js

* libs:

   * ws: contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* Configuraciones regionales:

   * de-DE: contiene el archivo translation.json para alemán.
   * en-US: contiene el archivo translation.json para inglés.
   * fr-FR: contiene el archivo translation.json para francés.
   * ja-JP: contiene el archivo translation.json para japonés.
   * html.jsp: contiene código para detectar la configuración regional actual del explorador.

* Index: contiene .content.xml.
* profile: contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil Dev {#dev-profile}

#### Comando {#command-2}

mvn clean: instala el paquete Dev en client-pkg.

#### Contenido de WS {#ws-content-3}

* css: contiene style.css, ie.css y jqueri-ui.css.
* images: contiene todas las imágenes.
* js:

   * libs: contiene todas las bibliotecas utilizadas en AEM Forms Workspace.
   * require: contiene required.js.
   * jqueryui: contiene jquery.ui.datepicker.ja.js.
   * runtime:

      * inicializer: contiene initializer.js y modelcontrollerpath.js.
      * models: contiene los modelos de todos los componentes de AEM Forms Workspace.
      * routes: contiene los archivos JavaScript y los archivos HTML que cargan páginas Iniciar proceso, Tareas pendientes, Seguimiento y Preferencias en AEM Forms Workspace.
      * services: contiene el archivo service.js, utilizado en AEM Forms Workspace.
      * templates: contiene todas las plantillas, es decir, los archivos HTML de todos los componentes de AEM Forms Workspace.
      * util: contiene todos los archivos de utilidad (JavaScript) que se utilizan en AEM Forms Workspace.
      * views: contiene vistas de todos los componentes de AEM Forms Workspace.

   * main.js
   * register.js
   * router.js

* libs:

   * ws: contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* Configuraciones regionales:

   * de-DE: contiene el archivo translation.json para alemán.
   * en-US: contiene el archivo translation.json para inglés.
   * fr-FR: contiene el archivo translation.json para francés.
   * ja-JP: contiene el archivo translation.json para japonés.
   * html.jsp: contiene código para detectar la configuración regional actual del explorador.

* Index: contiene .content.xml.
* profile: contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
