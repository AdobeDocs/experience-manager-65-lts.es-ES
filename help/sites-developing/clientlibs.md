---
title: Uso de bibliotecas del lado del cliente
description: AEM proporciona carpetas de biblioteca del lado del cliente, que permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: cafc7120-114e-487a-8b81-9c695318731e
source-git-commit: a061c19dcb883b94ee61be21459c46e21eaf696a
workflow-type: tm+mt
source-wordcount: '2791'
ht-degree: 1%

---

# Uso de bibliotecas del lado del cliente{#using-client-side-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

## Cómo funcionan las bibliotecas del lado del cliente en AEM {#how-client-side-libraries-work-in-aem}

La forma estándar de incluir una biblioteca del lado del cliente (es decir, un archivo JS o CSS) en el HTML de una página es simplemente incluir una etiqueta `<script>` o `<link>` en el JSP de esa página, que contenga la ruta al archivo en cuestión. Por ejemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Aunque este método funciona en AEM, puede provocar problemas cuando las páginas y sus componentes constitutivos se vuelven complejos. En estos casos, existe el peligro de que se incluyan varias copias de la misma biblioteca JS en la salida final de HTML. Para evitarlo y permitir la organización lógica de las bibliotecas del lado del cliente, AEM usa **carpetas de biblioteca del lado del cliente**.

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio de tipo `cq:ClientLibraryFolder`. Su definición en [notación CND](https://jackrabbit.apache.org/node-type-notation.html) es

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

De forma predeterminada, los nodos `cq:ClientLibraryFolder` se pueden colocar en cualquier lugar dentro de los subárboles `/apps`, `/libs` y `/etc` del repositorio (estos valores predeterminados y otras configuraciones se pueden controlar a través del panel **Adobe Granite HTML Library Manager** de [System Console](https://localhost:4502/system/console/configMgr)).

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS o CSS, junto con algunos archivos auxiliares (ver a continuación). Las propiedades de `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `categories`: identifica las categorías en las que se encuentra el conjunto de archivos JS y/o CSS dentro de este(a) `cq:ClientLibraryFolder`. La propiedad `categories`, al ser de varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (vea a continuación para ver cómo puede resultar de utilidad).

* `dependencies`: es una lista de otras categorías de bibliotecas de cliente de las que depende esta carpeta de biblioteca. Por ejemplo, dados dos nodos `cq:ClientLibraryFolder` `F` y `G`, si un archivo de `F` requiere otro archivo de `G` para funcionar correctamente, al menos uno de los `categories` de `G` debe estar entre los `dependencies` de `F`.

* `embed`: se usa para incrustar código de otras bibliotecas. Si el nodo F incrusta los nodos G y H, el HTML resultante será una concentración de contenido de los nodos G y H.
* `allowProxy`: si una biblioteca de cliente se encuentra en `/apps`, esta propiedad permite el acceso a ella a través del servlet proxy. Consulte [Localizar una carpeta de biblioteca de cliente y usar el servlet de bibliotecas de cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) a continuación.

## Referencia a bibliotecas del cliente {#referencing-client-side-libraries}

Como HTL es la tecnología preferida para desarrollar sitios de AEM, HTL debe utilizarse para incluir bibliotecas del lado del cliente en AEM. Sin embargo, también es posible hacerlo usando JSP.

### Uso de HTL {#using-htl}

En HTL, las bibliotecas de cliente se cargan a través de una plantilla de ayuda proporcionada por AEM, a la que se puede acceder mediante [`data-sly-use`](https://helpx.adobe.com/es/experience-manager/htl/using/block-statements.html#use). Hay tres plantillas disponibles en este archivo a las que se puede llamar mediante [`data-sly-call`](https://helpx.adobe.com/es/experience-manager/htl/using/block-statements.html#template-call):

* **css**: carga solo los archivos CSS de las bibliotecas de cliente a las que se hace referencia.
* **js** - Carga solamente los archivos JavaScript de las bibliotecas cliente a las que se hace referencia.
* **all**: carga todos los archivos de las bibliotecas de cliente a las que se hace referencia (tanto CSS como JavaScript).

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

Para obtener más información y un ejemplo de uso, consulte el documento [Introducción al lenguaje de plantilla de HTML](https://helpx.adobe.com/es/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Uso de JSP {#using-jsp}

Agregue una etiqueta `ui:includeClientLib` a su código JSP para agregar un vínculo a las bibliotecas de cliente en la página de HTML generada. Para hacer referencia a las bibliotecas, utilice el valor de la propiedad `categories` del nodo `ui:includeClientLib`.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por ejemplo, el nodo `/etc/clientlibs/foundation/jquery` es del tipo `cq:ClientLibraryFolder` con una propiedad categories del valor `cq.jquery`. El siguiente código de un archivo JSP hace referencia a las bibliotecas:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La página de HTML generada contiene el siguiente código:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Para obtener información completa, incluidos los atributos para filtrar bibliotecas de temas, CSS o JS, consulte [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, que en el pasado se usaba comúnmente para incluir bibliotecas de cliente, ha quedado obsoleto desde AEM 5.6. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) debe usarse en su lugar como se detalla más arriba.

## Creación de carpetas de biblioteca de cliente {#creating-client-library-folders}

Cree un nodo `cq:ClientLibraryFolder` para definir las bibliotecas de JavaScript y Hoja de estilos en cascada y ponerlas a disposición de las páginas de HTML. Utilice la propiedad `categories` del nodo para identificar las categorías de biblioteca a las que pertenece.

El nodo contiene uno o varios archivos de código fuente que, en tiempo de ejecución, se combinan en un solo archivo JS o CSS. El nombre del archivo generado es el nombre del nodo con la extensión de nombre de archivo `.js` o `.css`. Por ejemplo, el nodo de biblioteca denominado `cq.jquery` genera el archivo generado denominado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca de cliente contienen los siguientes elementos:

* Los archivos de origen JS o CSS que se combinarán.
* Recursos compatibles con los estilos CSS, como archivos de imagen.

  **Nota:** Puede usar subcarpetas para organizar los archivos de origen.
* Un archivo `js.txt` o un archivo `css.txt` que identifica los archivos de origen que se van a combinar en los archivos JS o CSS generados.

![clientlibarch](assets/clientlibarch.png)

Para obtener información acerca de los requisitos específicos de las bibliotecas de cliente para los widgets, vea [Usar y ampliar widgets](/help/sites-developing/widgets.md).

El cliente web debe tener permisos para obtener acceso al nodo `cq:ClientLibraryFolder`. También puede exponer bibliotecas de áreas seguras del repositorio (consulte Incrustar código de otras bibliotecas, a continuación).

### Anular bibliotecas en /lib {#overriding-libraries-in-lib}

Las carpetas de la biblioteca de cliente ubicadas debajo de `/apps` tienen prioridad sobre las carpetas con el mismo nombre que se encuentran de manera similar en `/libs`. Por ejemplo, `/apps/cq/ui/widgets` tiene prioridad sobre `/libs/cq/ui/widgets`. Cuando estas bibliotecas pertenecen a la misma categoría, se utiliza la biblioteca bajo `/apps`.

### Localizar una carpeta de biblioteca de cliente y utilizar el servlet de bibliotecas de cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

En versiones anteriores, las carpetas de la biblioteca de cliente se encontraban debajo de `/etc/clientlibs` en el repositorio. Esto se sigue admitiendo, pero se recomienda que las bibliotecas de cliente ahora se encuentren en `/apps`. Esto sirve para ubicar las bibliotecas de cliente cerca de los otros scripts, que generalmente se encuentran debajo de `/apps` y `/libs`.

>[!NOTE]
>
>Los recursos estáticos situados debajo de la carpeta de la biblioteca de cliente deben estar en una carpeta llamada *resources*. Si no tiene los recursos estáticos, como imágenes, en la carpeta *resources*, no se podrá hacer referencia a ellos en una instancia de publicación. Este es un ejemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para aislar mejor el código del contenido y la configuración, se recomienda localizar las bibliotecas de cliente en `/apps` y exponerlas a través de `/etc.clientlibs` mediante la propiedad `allowProxy`.

Para que se pueda acceder a las bibliotecas de cliente de `/apps`, se utiliza un servlet proxy. Las ACL siguen aplicándose en la carpeta de biblioteca del cliente, pero el servlet permite que el contenido se lea a través de `/etc.clientlibs/` si la propiedad `allowProxy` está establecida en `true`.

Solo se puede acceder a un recurso estático a través del proxy si reside debajo de un recurso debajo de la carpeta de biblioteca del cliente.

A modo de ejemplo:

* Tiene una clientlib en `/apps/myprojects/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

A continuación, establezca la propiedad `allowProxy` de `foo` en true.

* Entonces puede solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* A continuación, puede hacer referencia a la imagen mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Cuando se utilizan bibliotecas de cliente proxy, la configuración de Dispatcher de AEM puede requerir una actualización para garantizar que se permiten los URI con la extensión clientlibs.

>[!CAUTION]
>
>Adobe recomienda buscar bibliotecas de cliente en `/apps` y ponerlas a disposición mediante el servlet proxy. Sin embargo, tenga en cuenta que la práctica recomendada requiere que los sitios públicos nunca incluyan nada que se proporcione directamente en una ruta de acceso de `/apps` o `/libs`.

### Crear una carpeta de biblioteca de cliente {#create-a-client-library-folder}

1. Abra CRXDE Lite en un explorador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Seleccione la carpeta donde desea ubicar la carpeta de la biblioteca de cliente y haga clic en **Crear > Crear nodo**.
1. Escriba un nombre para el archivo de biblioteca y en la lista Tipo seleccione `cq:ClientLibraryFolder`. Haz clic en **Aceptar** y luego haz clic en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione el nodo `cq:ClientLibraryFolder`, agregue la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:

   * Nombre: categories
   * Tipo: cadena
   * Valor: Nombre de la categoría
   * Múltiple: Seleccionar

1. Agregue los archivos de origen a la carpeta de la biblioteca por cualquier medio. Por ejemplo, utilice un cliente WebDav para copiar archivos o cree un archivo y cree el contenido manualmente.

   **Nota:** Si lo desea, puede organizar los archivos de origen en subcarpetas.

1. Seleccione la carpeta de la biblioteca de cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro de nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:

   * **`js.txt`:** Use este nombre de archivo para generar un archivo de JavaScript.
   * **`css.txt`:** Use este nombre de archivo para generar una hoja de estilos en cascada.

1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:

   `#base=*[root]*`

   Reemplace * `[root]`* por la ruta de acceso a la carpeta que contiene los archivos de origen, en relación con el archivo TXT. Por ejemplo, utilice el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:

   `#base=.`

   El siguiente código establece la raíz como la carpeta denominada mobile debajo del nodo `cq:ClientLibraryFolder`:

   `#base=mobile`

1. En las líneas por debajo de `#base=[root]`, escriba las rutas de acceso de los archivos de origen relativos a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca de cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. En JSP, la etiqueta `ui:includeClientLib` que hace referencia a la carpeta de biblioteca del cliente hace que el código HTML incluya un vínculo al archivo de biblioteca generado y a las dependencias.

Las dependencias deben ser otras `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad al nodo `cq:ClientLibraryFolder` con los atributos siguientes:

* **Nombre:** dependencias
* **Tipo:** Cadena[]
* **Valores:** El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, / `etc/clientlibs/myclientlibs/publicmain` depende de la biblioteca `cq.jquery`. El JSP que hace referencia a la biblioteca de cliente principal genera HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustar Código De Otras Bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. En tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código resulta útil para proporcionar acceso a bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de la biblioteca de clientes específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de su aplicación por debajo de `/apps`. También se recomienda denegar el acceso a los visitantes del sitio web a la carpeta `/apps`. Para satisfacer ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de `/apps` y haga que sea accesible a través del servlet proxy como se describe en [Localizar una carpeta de biblioteca de cliente y usar el servlet de bibliotecas de cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Utilice la propiedad categories para identificar la carpeta de biblioteca de cliente que se va a incrustar. Para incrustar la biblioteca, agregue una propiedad al nodo `cq:ClientLibraryFolder` que se está incrustando, utilizando los siguientes atributos de propiedad:

* **Nombre:** incrustado
* **Tipo:** Cadena[]
* **Valor:** Valor de la propiedad categories del nodo `cq:ClientLibraryFolder` que se va a incrustar.

#### Uso de la incrustación para minimizar las solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final que genere la instancia de publicación para la página típica incluya un número relativamente grande de elementos `<script>`, especialmente si el sitio utiliza información de contexto de cliente para el análisis o el direccionamiento. Por ejemplo, en un proyecto no optimizado puede encontrar la siguiente serie de `<script>` elementos en HTML para una página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de ida y vuelta al cargar la página. Para ello, puede `embed` las bibliotecas necesarias en su biblioteca de cliente específica de la aplicación mediante la propiedad embed del nodo `cq:ClientLibraryFolder`.

Con AEM se incluyen las siguientes categorías de bibliotecas de cliente. Solo debe incrustar los que sean necesarios para el funcionamiento de su sitio concreto. Sin embargo, **debe mantener el orden indicado aquí**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a recursos relativos a la biblioteca de incrustación. Por ejemplo, la biblioteca de acceso público `/etc/client/libraries/myclientlibs/publicmain` incrusta la biblioteca de cliente `/apps/myapp/clientlib`:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

El archivo `main.css` contiene el siguiente estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que genera el nodo `publicmain` contiene el siguiente estilo, con la dirección URL de la imagen original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Uso de una biblioteca para grupos móviles específicos {#using-a-library-for-specific-mobile-groups}

Utilice la propiedad `channels` de una carpeta de biblioteca de cliente para identificar el grupo móvil que utiliza la biblioteca. La propiedad `channels` es útil cuando las bibliotecas de la misma categoría están diseñadas para capacidades de dispositivos diferentes.

Para asociar una carpeta de biblioteca de cliente con un grupo de dispositivos, agregue una propiedad al nodo `cq:ClientLibraryFolder` con los atributos siguientes:

* **Nombre:** canales
* **Tipo:** Cadena[]
* **Valores:** Nombre del grupo móvil. Para excluir la carpeta de la biblioteca de un grupo, añada un prefijo al nombre con un signo de exclamación (&quot;!&quot;).

Por ejemplo, en la tabla siguiente se muestra el valor de la propiedad `channels` para cada carpeta de biblioteca de cliente de la categoría `cq.widgets`:

| Carpeta de biblioteca de cliente | Valor de la propiedad de canales |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Uso de preprocesadores {#using-preprocessors}

AEM admite preprocesadores y envíos conectables con compatibilidad con [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI establecido como preprocesador predeterminado de AEM.

Los preprocesadores conectables permiten un uso flexible que incluye:

* Definición de ScriptProcessors que pueden procesar las fuentes de los scripts
* Los procesadores se pueden configurar con opciones
* Los procesadores se pueden utilizar para la minificación, pero también para casos no minificados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>De forma predeterminada, AEM utiliza el compresor YUI. Consulte la [documentación de GitHub del compresor YUI](https://github.com/yui/yuicompressor/issues) para obtener una lista de problemas conocidos. Cambiar al compresor GCC para clientlibs particulares puede resolver algunos problemas observados al utilizar YUI.

>[!CAUTION]
>
>No coloque ninguna biblioteca minificada en una biblioteca de cliente. En su lugar, proporcione la biblioteca sin procesar y, si se requiere la minificación, utilice las opciones de los preprocesadores.

### Uso {#usage}

Puede elegir configurar la configuración de preprocesadores por biblioteca de cliente o en todo el sistema.

* Agregar las propiedades de varios valores `cssProcessor` y `jsProcessor` en el nodo clientlibrary

* O defina la configuración predeterminada del sistema mediante la configuración OSGi de **HTML Library Manager**

Una configuración de preprocesador en el nodo clientlib tiene prioridad sobre la configuración OSGI.

### Formato y ejemplos {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compresor YUI para minificación de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Escriba un script para preprocesar y luego GCC para minimizar y proteger {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Opciones adicionales de GCC {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obtener más información sobre las opciones de GCC, consulte la [documentación de GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Establecer minificador predeterminado del sistema {#set-system-default-minifier}

YUI se establece como el minificador predeterminado en AEM. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración de Apache Felix en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Busque y edite el **Administrador de bibliotecas Adobe Granite HTML**.
1. Habilitar la opción **Minify** (si no está habilitada).
1. Establezca el valor **Configuraciones predeterminadas del procesador JS** en `min:gcc`.

   Las opciones se pueden pasar si se separan con punto y coma, por ejemplo, `min:gcc;obfuscate=true`.

1. Haga clic en **Guardar** para guardar los cambios.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de biblioteca de cliente.

### Consulte Archivos incrustados {#see-embedded-files}

Para realizar un seguimiento del origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas producen los resultados esperados, puede ver los nombres de los archivos que se están incrustando durante la ejecución. Para ver los nombres de archivo, agregue el parámetro `debugClientLibs=true` a la dirección URL de la página web. La biblioteca que se genera contiene `@import` instrucciones en lugar del código incrustado.

En el ejemplo de la sección [Incrustar código de otras bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) anterior, la carpeta de biblioteca de cliente `/etc/client/libraries/myclientlibs/publicmain` incrusta la carpeta de biblioteca de cliente `/apps/myapp/clientlib`. Al anexar el parámetro a la página web, se produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Al abrir el archivo `publicmain.css`, se muestra el siguiente código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de la dirección del navegador web, añada el siguiente texto a la dirección URL de su HTML:

   `?debugClientLibs=true`
1. Cuando se cargue la página, vea el origen de la página.
1. Haga clic en el vínculo proporcionado como href para el elemento de vínculo para abrir el archivo y ver el código fuente.

### Descubrir bibliotecas de cliente {#discover-client-libraries}

El componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una página de información sobre todas las carpetas de la biblioteca de cliente del sistema. El nodo `/libs/granite/ui/content/dumplibs` tiene el componente como tipo de recurso. Para abrir la página, utilice la siguiente URL (cambiando el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de la biblioteca (CSS o JS) y los valores de los atributos de la biblioteca, como las categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El componente `dumplibs` incluye un selector de prueba que muestra el código fuente generado para las etiquetas `ui:includeClientLib`. La página incluye código para diferentes combinaciones de atributos js, css y temáticos.

1. Utilice uno de los siguientes métodos para abrir la página Resultados de la prueba:

   * En la página `dumplibs.html`, haga clic en el vínculo del texto **Haga clic aquí para probar la salida**.

   * Abra la siguiente URL en el explorador web (utilice un host y un puerto diferentes según sea necesario):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La página predeterminada muestra el resultado de las etiquetas sin valor para el atributo categories.

1. Para ver el resultado de una categoría, escriba el valor de la propiedad `categories` de la biblioteca de cliente y haga clic en **Enviar consulta**.

## Configurar la administración de bibliotecas para desarrollo y producción {#configuring-library-handling-for-development-and-production}

El servicio Administrador de bibliotecas de HTML procesa las etiquetas `cq:ClientLibraryFolder` y genera las bibliotecas en tiempo de ejecución. El tipo de entorno, desarrollo o producción, determina cómo debe configurar el servicio:

* Aumentar la seguridad: deshabilitar depuración
* Mejorar el rendimiento: Elimine espacios en blanco y comprima bibliotecas.
* Mejorar la legibilidad: Incluya espacios en blanco y no los comprima.

Para obtener información sobre cómo configurar el servicio, consulte [Administrador de bibliotecas de AEM HTML](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
