---
title: Prácticas recomendadas para la optimización de los motores de búsqueda y administración URL
description: Conozca las prácticas recomendadas de SEO y las recomendaciones sobre una implementación de AEM.
topic-tags: managing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3523'
ht-degree: 65%

---

# Prácticas recomendadas para la optimización de los motores de búsqueda y administración URL{#seo-and-url-management-best-practices}

La SEO (optimización de los motores de búsqueda) se ha convertido en una preocupación clave para muchos especialistas en marketing. Como resultado, las preocupaciones de SEO deben abordarse en muchos proyectos de AEM.

En este documento primero se describen algunas [prácticas recomendadas de SEO](#seo-best-practices) y recomendaciones sobre una implementación de AEM. Luego, se profundiza en algunos de los [pasos de implementación más complejos](#aem-configurations) que se mencionan en la primera sección.

## Prácticas recomendadas de SEO {#seo-best-practices}

Esta sección describe algunas prácticas recomendadas generales de SEO.

### URL {#urls}

Existen algunas prácticas recomendadas aceptadas con las direcciones URL.

En el proyecto de AEM, al evaluar las URL, pregúntese lo siguiente:

&quot;Si un usuario viera esta URL y ningún contenido en la página, ¿podría describir esta página?&quot;

Si la respuesta es sí, es probable que la URL funcione bien en un motor de búsqueda.

A continuación se ofrecen algunas sugerencias generales para crear las URL para SEO:

* Utilice guiones para separar palabras.

   * Nombre las páginas utilizando guiones (-) como separadores.
   * Evite utilizar mayúsculas y minúsculas, guiones bajos y espacios.

* Evite el uso de parámetros de consulta siempre que sea posible. Si es necesario, limítelos a dos o menos.

   * Utilice la estructura de directorio para indicar la arquitectura de la información, cuando esté disponible.
   * Si no se puede utilizar una estructura de directorio, utilice selectores de Sling en la URL, en lugar de cadenas de consulta. Además del valor SEO que proporcionan, los selectores de Sling también hacen que las páginas sean almacenables en la memoria caché para Dispatcher.

* Cuanto más fácil de leer sea una URL, mejor. Tener palabras clave presentes en la URL aumenta el valor.

   * Si se utilizan selectores en una página, se prefieren los selectores que proporcionan un valor semántico.
   * Si un ser humano no puede leer su URL, un motor de búsqueda tampoco podrá.
   * Por ejemplo:
     `mybrand.com/products/product-detail.product-category.product-name.html`
se prefiere en lugar de `mybrand.com/products/product-detail.1234.html`

* Evite los subdominios siempre que sea posible, ya que los motores de búsqueda los tratarán como entidades diferentes y fragmentarán el valor SEO del sitio.

   * En su lugar, utilice subrutas de primer nivel. Por ejemplo, en lugar de `es.mybrand.com/home.html`, utilice `www.mybrand.com/es/home.html`.

   * Planifique la jerarquía de contenido para que coincida con la forma en que se presenta el contenido, según esta guía.

* La eficacia de las palabras clave en las URL disminuye a medida que aumenta la longitud de la URL y la posición de la palabra clave. En otras palabras, cuanto más corto, mejor.

   * Utilice las técnicas y funciones para acortar URL de AEM para eliminar elementos innecesarios en la URL.
   * Por ejemplo, `mybrand.com/en/myPage.html` se prefiere en lugar de `mybrand.com/content/my-brand/en/myPage.html`.

* Utilice URL canónicas.

   * Cuando se puede servir una URL desde diferentes rutas o con diferentes parámetros o selectores, asegúrese de utilizar una `rel=canonical` etiqueta en la página.

   * Incluya direcciones URL canónicas en el código de la plantilla de AEM.

* Haga coincidir las URL con los títulos de las páginas siempre que sea posible.

   * Se debe alentar a los autores de contenido a que sigan esta práctica.

* Admita la función de no distinguir mayúsculas de minúsculas en las solicitudes de URL.

   * Configure Dispatcher para que vuelva a escribir todas las solicitudes entrantes en minúsculas.
   * Capacite a los autores de contenido para crear todas las páginas con letras minúsculas.

* Asegúrese de que cada página solo se proporcione desde un protocolo.

   * A veces, los sitios se proporcionan desde `http` hasta que un usuario llega a una página con un formulario de cierre de compra o de inicio de sesión, por ejemplo, cuando cambia a `https`. Al establecer vínculos desde esta página, si el usuario puede regresar a `http` páginas y tener acceso a ellas a través de `https`, el motor de búsqueda las rastreará como dos páginas separadas.

   * Actualmente, Google prefiere las páginas `https` a las `http`. Ayudan a facilitar las cosas al servir a todo el sitio durante `https`.

### Configuración de servidor {#server-configuration}

En cuanto a la configuración del servidor, puede realizar los siguientes pasos para asegurarse de que solo se rastreando el contenido correcto:

* Utilice un archivo `robots.txt` para bloquear el rastreo de cualquier contenido que no se deba indexar.

   * Bloquee **todo** el rastreo en los entornos de prueba.

* Al lanzar un nuevo sitio con URL actualizadas, implemente redirecciones 301 para asegurarse de que no se pierda la clasificación SEO existente.
* Incluya un icono de favoritos para el sitio.
* Para facilitar que los motores de búsqueda rastreen el contenido, implemente un mapa del sitio XML. Asegúrese de incluir un mapa del sitio móvil para sitios móviles o adaptables.

## Configuraciones de AEM {#aem-configurations}

En esta sección se describen los pasos de implementación para configurar AEM con las siguientes recomendaciones de SEO.

### Uso de selectores de Sling {#using-sling-selectors}

Anteriormente, el uso de parámetros de consulta era la práctica generalmente aceptada al crear una aplicación web empresarial.

La tendencia de los últimos años ha sido eliminar parámetros para que las URL sean más legibles. En muchas plataformas, este proceso de eliminación implica implementar redirecciones en el servidor web o en la red de distribución de contenido (CDN), pero Sling hace que el proceso sea sencillo. Selectores de Sling:

* Facilitan la lectura de las URL.
* Permite almacenar en caché las páginas en Dispatcher y mejorar la seguridad.
* Permite dirigir el contenido directamente, en lugar de tener un servlet genérico que recupera el contenido. Otorga el beneficio de las ACL que aplica al repositorio y a los filtros que aplica en Dispatcher.

#### Uso de selectores para servlets {#using-selectors-for-servlets}

AEM ofrece dos opciones al escribir servlets:

* **Servlets bin**
* **Sling** servlets

Los siguientes ejemplos ilustran cómo registrar servlets que siguen ambos patrones, así como el beneficio que se obtiene por usar servlets de Sling.

#### Servlets bin (un nivel inferior) {#bin-servlets-one-level-down}

Los **servlets bin** siguen el patrón al que muchos desarrolladores están acostumbrados por la programación J2EE. El servlet está registrado en una ruta de acceso específica que, en AEM, suele estar por debajo de `/bin`, y se extraen los parámetros de solicitud necesarios de la cadena de consulta.

La anotación de SCR para este tipo de servlet tendría este aspecto:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Luego extrae los parámetros de la cadena de consulta mediante el objeto `SlingHttpServletRequest` incluido en el método `doGet`; por ejemplo:

```
String myParam = req.getParameter("myParam");
```

La URL resultante utilizada tendría este aspecto:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Hay algunos puntos que hay que tener en cuenta con este enfoque:

* La propia URL pierde el valor SEO. Los usuarios que acceden al sitio, incluidos los motores de búsqueda, no reciben ningún valor semántico de la URL, ya que esta representa una ruta programática y no la jerarquía de contenido.
* La presencia de parámetros de consulta en la URL significa que Dispatcher no puede almacenar la respuesta en caché.
* Si desea proteger este servlet, implemente su propia lógica de seguridad personalizada en el servlet.
* Dispatcher debe configurarse (con cuidado) para que se muestre `/bin/myApp/myServlet`. La simple exposición de `/bin` permitiría el acceso a ciertos servlets que no deberían estar abiertos a los visitantes del sitio.

#### Sling servlets (un nivel más bajo) {#sling-servlets-one-level-down}

Los **servlets Sling** permiten registrar el servlet de manera opuesta. En lugar de dirigirse a un servlet y especificar el contenido que desea que el servlet procese en función de los parámetros de consulta, debe buscar el contenido que desee. Y especifique el servlet que debe representar el contenido en función de los selectores de Sling.

La anotación de SCR para este tipo de servlet tendría este aspecto:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

En este caso, se puede acceder automáticamente al recurso al que se dirige la dirección URL (una instancia del recurso `myPageType`) en el servlet. Para acceder a él, llame al siguiente método:

```
Resource myPage = req.getResource();
```

La URL resultante utilizada tendría este aspecto:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Los beneficios de este enfoque son:

* Puede incluir el valor SEO, obtenido por la semántica presente en la jerarquía del sitio y el nombre de la página.
* Dado que no hay parámetros de consulta presentes, Dispatcher puede almacenar la respuesta en caché. Además, cualquier actualización realizada en la página a la que se dirige anulará esta caché cuando se active la página.
* Todas las ACL aplicadas a `/content/my-brand/my-page` entrarán en vigor cuando un usuario intente acceder a este servlet.
* Dispatcher ya está configurado para servir este contenido como una función del sitio web. No se requiere ninguna configuración adicional.

### Reescribir URL {#url-rewriting}

En AEM, todas las páginas web se almacenan en `/content/my-brand/my-content`. Aunque esta ubicación es útil desde la perspectiva de la administración de datos del repositorio, no es necesariamente la forma en que desea que los clientes vean el sitio. Además, puede entrar en conflicto con las directrices de SEO para que las URL sean lo más cortas posible. Además, es posible que sirva varios sitios web desde la misma instancia de AEM y desde diferentes nombres de dominio.

En esta sección se analizan las opciones disponibles en AEM para administrar estas URL y presentarlas a los usuarios de una forma más fácil de leer y compatible con la optimización de los motores de búsqueda.

#### URL de vanidad {#vanity-urls}

Si un autor desea que una página sea accesible desde una segunda ubicación con fines promocionales, las URL personales de AEM, definidas página por página, pueden resultar útiles. Para agregar una URL de vanidad para una página, navegue hasta ella en la consola **Sitios** y edite las propiedades de la página. En la parte inferior de la pestaña **Básico**, verá una sección en la que se pueden agregar URL de vanidad. Tenga en cuenta que tener la página accesible a través de más de una URL fragmentará el valor SEO de la página, por lo que se debe agregar una etiqueta de URL canónica a la página para evitar este problema.

#### Nombres de páginas localizados {#localized-page-names}

Es posible que desee mostrar nombres de páginas localizados a los usuarios de contenido traducido. Por ejemplo:

* En lugar de hacer que un usuario que habla en español navegue a:
  `www.mydomain.com/es/home.html`

* Sería mejor que la URL fuera:
  `www.mydomain.com/es/casa.html`.

El desafío que supone la localización del nombre de la página es que muchas de las herramientas de localización disponibles en la plataforma AEM dependen de que los nombres de las páginas coincidan en las distintas configuraciones regionales para mantener el contenido sincronizado.

La propiedad `sling:alias` le permite comer pastel de Adobe y también comerlo. Puede agregar `sling:alias` como propiedad a cualquier recurso para permitir un nombre de alias para el recurso. En el ejemplo anterior, tendría lo siguiente:

* Una página del JCR en:
  `…/es/home`

* A continuación, agréguele una propiedad:
  `sling:alias` = `casa`

Este flujo permite a las herramientas de traducción de AEM, como el administrador de varios sitios, seguir manteniendo una relación entre:

* `/en/home`

* `/es/home`

También permite a los usuarios finales interactuar con el nombre de la página en sus idiomas nativos.

>[!NOTE]
>
>La propiedad `sling:alias` se puede establecer con la propiedad de Alias [ al editar Propiedades](/help/sites-authoring/editing-page-properties.md#advanced) de página.

#### /etc/map {#etc-map}

En una instalación estándar de AEM:

* para la configuración OSGi
  **Apache Sling Resource Resolver Factory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* la propiedad
  **Ubicación de asignación** ( `resource.resolver.map.location`)

* va de manera predeterminada a`/etc/map`

En esta ubicación se pueden agregar definiciones de asignación a solicitudes entrantes de asignación, reescribir direcciones URL en páginas de AEM o en ambas.

Para crear una nueva asignación, cree un nodo de `sling:Mapping` en esta ubicación debajo de `/http` o `/https`. En función de las propiedades `sling:match` y `sling:internalRedirect` establecidas en este nodo, AEM redireccionará todo el tráfico de la URL coincidente al valor especificado en la propiedad `internalRedirect`.

Aunque este método está documentado en la documentación oficial de AEM y Sling, el ámbito de la compatibilidad con expresiones regulares que proporciona esta implementación es limitado cuando se compara con las opciones disponibles directamente mediante `SlingResourceResolver`. Además, la implementación de asignaciones de esta manera puede provocar problemas con la invalidación de la caché de Dispatcher.

A continuación se muestra un ejemplo de cómo se produce este problema:

1. Un usuario visita su sitio web y solicita `https://www.mydomain.com/my-page.html`
1. Dispatcher reenvía esta solicitud al servidor de publicación.
1. Con `/etc/map`, el servidor de publicación resuelve esta solicitud en `/content/my-brand/my-page` y produce la página.

1. Dispatcher almacena en la caché la respuesta en `/my-page.html` y le devuelve la respuesta al usuario.
1. Un autor de contenido cambia esta página y la activa.
1. El agente de vaciado de Dispatcher envía una solicitud de anulación para `/content/my-brand/my-page`**.** Debido a que Dispatcher no tiene una página en la caché en esta ruta, el contenido antiguo permanece en la caché y está obsoleto.

Existen maneras de configurar reglas de vaciado de Dispatcher personalizadas que asignarán la URL más corta a la URL más larga para invalidar la caché.

Sin embargo, también hay una forma más sencilla de administrar este problema:

1. **Reglas de SlingResourceResolver**

   Mediante la consola web (por ejemplo, localhost:4502/system/console/configMgr) puede configurar el Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**
     `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.

   Adobe recomienda crear las asignaciones necesarias para acortar las direcciones URL como expresiones regulares y luego definir estas configuraciones en un nodo OsgiConfignode, `config.publish`, que se incluye en la compilación.

   En lugar de definir las asignaciones en `/etc/map`, se pueden asignar directamente a la propiedad Asignaciones **de** URL ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   En este ejemplo sencillo, se elimina `/content/my-brand/` desde el principio de cualquier URL donde esté presente.

   Convierte una dirección URL:

   * de `/content/my-brand/my-page.html`
   * a solo `/my-page.html`

   Esta conversión concuerda con la práctica recomendada de mantener las URL lo más cortas posible.

1. **Asignación de resultados de URL en páginas**

   Después de definir las asignaciones en el Apache Sling Resource Resolver, utilice estas asignaciones en los componentes para asegurarse de que las direcciones URL que se emitan en las páginas sean cortas y ordenadas. Puede realizar esta tarea mediante la función de asignación de `ResourceResolver`.

   Por ejemplo, si estaba implementando un componente de navegación personalizado que detalla los elementos secundarios de la página actual, puede utilizar el método de asignación de la siguiente manera:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Hasta ahora, ha implementado asignaciones junto con la lógica de sus componentes para utilizar estas asignaciones al enviar direcciones URL a las páginas.

La parte final es el manejo de estas URL abreviadas cuando llegan a Dispatcher, que es donde `mod_rewrite` comienza a funcionar. La mayor ventaja de usar `mod_rewrite` es que las URL se asignan de nuevo a su formulario largo *antes* de enviarse al módulo de Dispatcher. Este flujo significa que Dispatcher solicita la URL larga del servidor de publicación y la almacena en la memoria caché correspondiente. Por lo tanto, cualquier solicitud de vaciado de Dispatcher que venga del servidor de publicación, puede invalidar este contenido correctamente.

Para implementar estas reglas, puede agregar elementos `RewriteRule` debajo del host virtual en la configuración de Apache HTTP Server. Si desea expandir las URL abreviadas del ejemplo anterior, puede implementar una regla con este aspecto:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Etiquetas de URL canónicas {#canonical-url-tags}

Las etiquetas de URL canónicas son etiquetas de vínculo colocadas en el encabezado de un documento HTML para aclarar cómo los motores de búsqueda deben tratar una página al indexar el contenido. El beneficio que ofrecen es garantizar que (versiones diferentes) una página se indexe como la misma, aunque la URL de la página pueda contener diferencias.

Por ejemplo: si un sitio tuviera que ofrecer una versión de una página compatible con una impresora, un motor de búsqueda podría indexar esta página por separado desde la versión normal de la página. La etiqueta canónica le dirá al motor de búsqueda que son iguales.

Ejemplos:

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

Ambos aplicarían la siguiente etiqueta al encabezado de la página:

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

El valor `href` puede ser relativo o absoluto. El código debe incluirse en el marcado de la página para determinar la URL canónica de la página y mostrar esta etiqueta.

### Configurar el Dispatcher para la insensibilidad de distinción entre mayúsculas y minúsculas {#configuring-the-dispatcher-for-case-insensitivity}

La práctica recomendada es utilizar letras minúsculas en todas las páginas. Sin embargo, no desea que un usuario obtenga un error 404 cuando acceda al sitio web con letras mayúsculas en su URL. Por este motivo, Adobe recomienda agregar una regla de reescritura en la configuración de Apache HTTP Server para asignar todas las URL entrantes a minúsculas. Además, los autores de contenido deben recibir formación para crear sus páginas con nombres en minúsculas.

Para configurar Apache para que convierta todo el tráfico entrante a minúsculas, agregue lo siguiente a la configuración `vhost`:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Además, agregue lo siguiente a la parte superior del archivo `htaccess`:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementación de robots.txt para proteger los entornos de desarrollo {#implementing-robots-txt-to-protect-development-environments}

Los motores de búsqueda *deben* comprobar la presencia de un archivo `robots.txt` en la raíz del sitio antes de rastrear el sitio. Aunque los principales motores de búsqueda como Google, Yahoo o Bing respetan este archivo, algunos motores de búsqueda extranjeros no lo hacen.

La manera más sencilla de bloquear el acceso a todo el sitio es colocar un archivo denominado `robots.txt` en la raíz del sitio con el siguiente contenido:

```xml
User-agent: *
Disallow: /
```

De lo contrario, en un entorno activo, puede optar por no permitir determinadas rutas que no desee indexar.

La advertencia de colocar el archivo `robots.txt` en la raíz del sitio es que las solicitudes de vaciado de Dispatcher pueden borrar este archivo. Además, es probable que las asignaciones de URL coloquen la raíz del sitio en un lugar diferente de `DOCROOT`, tal como se define en la configuración del servidor HTTP Apache. Por este motivo, es común colocar este archivo en la instancia de autor en la raíz del sitio y replicarlo en la instancia de publicación.

### Crear un mapa del sitio XML en AEM {#building-an-xml-sitemap-on-aem}

Los rastreadores utilizan mapas del sitio en XML para comprender mejor la estructura de los sitios web. Si bien no hay garantías de que proporcionar un mapa del sitio conduzca a mejores clasificaciones de SEO, se trata de una práctica recomendada y reconocida. Puede mantener manualmente un archivo XML en el servidor web para utilizarlo como mapa del sitio. Sin embargo, Adobe recomienda generar el mapa del sitio mediante programación para garantizar que, a medida que los autores crean contenido, el mapa del sitio refleje automáticamente sus cambios.

AEM usa el [módulo de mapa del sitio Apache Sling](https://github.com/apache/sling-org-apache-sling-sitemap) para generar mapas del sitio en XML, que proporciona una amplia gama de opciones para que los desarrolladores y editores mantengan un mapa del sitio en XML de sitios actualizado.

>[!NOTE]
>
>Disponible como característica de producto desde la versión de Adobe Experience Manager 6.5.11.0.
> 
>Para versiones anteriores, puede registrar un Sling Servlet usted mismo para escuchar una llamada de `sitemap.xml`. Utilice el recurso proporcionado mediante la API de servlet para buscar la página actual y sus descendientes y generar un archivo `sitemap.xml`.

El módulo del mapa del sitio Apache Sling distingue entre un mapa del sitio de nivel superior y un mapa del sitio anidado, ambos generados para cualquier recurso que tenga la propiedad `sling:sitemapRoot` establecida en `true`. En general, los mapas del sitio se representan con selectores en la ruta del mapa del sitio de nivel superior del árbol, que es el recurso que no tiene otro antecesor raíz del mapa del sitio. Esta raíz de mapa del sitio de nivel superior también expone el índice de mapa del sitio, que normalmente es lo que el propietario del sitio configuraría en el portal de configuración del motor de búsqueda o añadiría al `robots.txt` del sitio.

Por ejemplo, piense en un sitio que defina una raíz de mapa del sitio de nivel superior en `my-page` y una raíz de mapa del sitio anidada en `my-page/news`, para generar un mapa del sitio dedicado para las páginas del subárbol de noticias. Las direcciones URL relevantes resultantes serían

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>Los selectores `sitemap` y `sitemap-index` pueden interferir con las implementaciones personalizadas. Si no desea utilizar la función de producto, configure su propio servlet que sirva a estos selectores con un `service.ranking` superior a 0.

En la configuración predeterminada, el cuadro de diálogo Propiedades de página proporciona una opción para marcar una página como raíz de mapa del sitio y, por lo tanto, como se describe más arriba, generar un mapa del sitio propio y de sus descendientes. Este comportamiento se implementa mediante las implementaciones de la variable `SitemapGenerator` y se puede ampliar añadiendo implementaciones alternativas. Sin embargo, como la frecuencia con la que se regeneran los mapas del sitio XML depende de los flujos de trabajo y las cargas de trabajo de creación de contenido, el producto no envía ninguna configuración `SitemapScheduler`. Como tal, hace que la función sea de inclusión efectiva.

Para habilitar el trabajo en segundo plano que genera los mapas del sitio XML, debe estar configurado un `SitemapScheduler`. Para ello, cree una configuración OSGi para el `org.apache.sling.sitemap.impl.SitemapScheduler` PID. La expresión del planificador `0 0 0 * * ?` puede utilizarse como punto de partida para regenerar todos los mapas del sitio XML una vez al día a medianoche.

![Mapa del sitio de Apache Sling: planificador](assets/sling-sitemap-scheduler.png)

El trabajo de generación de mapas del sitio se puede ejecutar en instancias de nivel de creación y publicación. Normalmente, se recomienda ejecutar la generación en instancias de nivel de publicación, ya que las URL canónicas adecuadas solo se pueden generar allí (debido a que las reglas de asignación de recursos de Sling normalmente están presentes solo en instancias de nivel de publicación). Sin embargo, es posible añadir una implementación personalizada del mecanismo de externalización utilizado para generar las URL canónicas implementando la interfaz [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html). Si una implementación personalizada puede generar las direcciones URL canónicas de un mapa del sitio en las instancias de nivel de creación, `SitemapScheduler` se puede configurar para el modo de ejecución de creación. Además, la carga de trabajo de generación de mapas del sitio XML se puede distribuir entre las instancias del clúster de servicios de creación. En esta situación, se debe tener cuidado al gestionar contenido que aún no se ha publicado, que se ha modificado o que solo es visible para un grupo restringido de usuarios.

AEM Sites contiene una implementación predeterminada de un `SitemapGenerator` que atraviesa un árbol de páginas para generar un mapa del sitio. Está preconfigurado para mostrar únicamente las URL canónicas de un sitio y las alternativas de idioma si están disponibles. También se puede configurar para incluir la última fecha de modificación de una página si es necesario. Para ello, habilite la opción _Agregar última modificación_ de la configuración _Adobe AEM SEO: generador de mapas de sitios de árbol de páginas_ y seleccione _Última modificación de Source_. Cuando los mapas del sitio se generan en el nivel de publicación, se recomienda usar la fecha `cq:lastModified`.

![Adobe AEM SEO: configuración del generador de mapas del sitio del árbol de páginas](assets/sling-sitemap-pagetreegenerator.png)

Para limitar el contenido de un mapa del sitio, se pueden implementar las siguientes interfaces de servicio cuando sea necesario:

* el [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) se puede implementar para ocultar páginas de mapas del sitio XML generados por el generador específico de mapas del sitio de AEM Sites
* un [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) o [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) se puede implementar para filtrar productos o categorías de los mapas del sitio XML generados por generadores específicos de mapa del sitio de [marcos de integración comercial](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=es)

Si las implementaciones predeterminadas no funcionan en un caso de uso determinado o si los puntos de extensión no son lo suficientemente flexibles, implemente un `SitemapGenerator` personalizado para tener un control total del contenido de un mapa del sitio generado. El siguiente ejemplo utiliza la lógica de implementación predeterminada para AEM Sites. Utiliza el [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) como punto de partida para recorrer un árbol de páginas:

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, and so on
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

Además, la funcionalidad implementada para los mapas del sitio XML también se puede utilizar para diferentes casos de uso, por ejemplo, para añadir el vínculo canónico o las alternativas de idioma al encabezado de una página. Consulte la interfaz [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) para obtener más información.

### Crear redirecciones 301 para URL heredadas {#creating-redirects-for-legacy-urls}

Al lanzar un sitio con una nueva estructura, implementar y probar redirecciones 301 en Apache HTTP Server es importante por dos motivos:

* Las URL heredadas acumularon un valor SEO con el tiempo. Al implementar una redirección, el motor de búsqueda puede aplicar este valor a la nueva URL.
* Es posible que los usuarios del sitio hayan creado marcadores en estas páginas. Al implementar las redirecciones, puede asegurarse de dirigir al usuario a la página del nuevo sitio que más coincida con el lugar en el que intentaba ingresar al sitio antiguo.

Para obtener instrucciones sobre cómo implementar las redirecciones 301, asegúrese de comprobar la sección de recursos adicionales que se muestra a continuación, así como una herramienta para probar que las redirecciones funcionan según lo esperado.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte los siguientes recursos adicionales:

* [Asignación de recursos](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
