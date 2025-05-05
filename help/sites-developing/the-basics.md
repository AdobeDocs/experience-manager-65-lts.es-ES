---
title: Conceptos principales de AEM
description: Una visión general de los conceptos principales de cómo está estructurado Adobe Experience Manager (AEM) y cómo desarrollarlo, incluidos conceptos básicos como JCR, Sling, OSGi, Dispatcher, flujos de trabajo y MSM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: fe3735ff-5c9b-4eb8-bf1d-f2189ec7e26f
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 0%

---

# Conceptos principales de AEM {#aem-core-concepts}

>[!NOTE]
>
>Antes de entrar en los conceptos principales de Adobe Experience Manager (AEM), Adobe recomienda completar el tutorial de WKND en el documento [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md). Incluye una descripción general del proceso de desarrollo de AEM y una introducción a los conceptos principales.

## Requisitos previos para el desarrollo en AEM {#prerequisites-for-developing-on-aem}

Necesita las siguientes habilidades para desarrollar sobre AEM:

* Conocimientos básicos de las técnicas de aplicación web, incluidos:

   * el ciclo de solicitud-respuesta (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conocimientos prácticos de Experience Server (CRX), incluido el Explorador de contenido
* Para desarrollar en la IU clásica, también se requieren conocimientos básicos de JSP (JavaServer Pages), incluida la capacidad de comprender y modificar ejemplos de JSP simples.

También se recomienda que lea y siga las [Directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repositorio de contenido de Java™ {#java-content-repository}

El estándar del repositorio de contenido Java™ (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor e independiente de la implementación para acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido.

El responsable de la especificación es Adobe Research (Suiza) AG.

El paquete [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), javax.jcr.&ast; se utiliza para el acceso directo y la manipulación del contenido del repositorio.

## Experience Server (CRX) y Jackrabbit {#experience-server-crx-and-jackrabbit}

El servidor de experiencia proporciona los servicios de experiencia en los que está basado AEM y que pueden utilizarse para crear aplicaciones personalizadas e incrusta el repositorio de contenido basado en Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) es una implementación de código abierto totalmente conforme de la API 2.0 de JCR.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

### Introducción a Sling {#introduction-to-sling}

AEM se ha creado usando [Sling](https://sling.apache.org/index.html), un marco de trabajo de aplicaciones web basado en los principios de REST que facilita el desarrollo de aplicaciones orientadas a contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit o, si hay AEM, el repositorio de contenido de CRX, como almacén de datos. Sling ha sido colaborador de Apache Software Foundation; puede encontrar más información en Apache.

Con Sling, el tipo de contenido que se procesará no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL responde a un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Esto proporciona una excelente compatibilidad para que los autores de contenido web creen páginas que se personalicen fácilmente según sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando necesita páginas que se puedan personalizar fácilmente. En concreto, al implementar un sistema de administración de contenido web como WCM en la solución AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

El diagrama siguiente explica la resolución de scripts de Sling. Muestra cómo pasar de una solicitud HTTP al nodo de contenido, de un nodo de contenido al tipo de recurso, de un tipo de recurso al script y qué variables de script están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos, pero útiles, que puede utilizar al trabajar con SlingPostServlet. Incluye el controlador predeterminado para todas las peticiones POST que le ofrece un sinfín de opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Usando SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling está *centrado en contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* el primer destino es el recurso (nodo JCR) que contiene el contenido
* en segundo lugar, la representación o script se encuentra en las propiedades del recurso combinadas con ciertas partes de la solicitud (por ejemplo, los selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a la filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* RESTful, no solo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* elimina uno o varios modelos de datos

   * anteriormente se necesitaban los siguientes elementos: estructura URL, objetos empresariales, esquema de base de datos;
   * esto ahora se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se basa en la dirección URL de la solicitud del usuario. Esto define el contenido que deben mostrar los scripts adecuados. Para ello, se extrae información de la dirección URL.

Si analiza la siguiente dirección URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Puede dividirlo en sus partes compuestas:

| protocolo | host | ruta de contenido | selectores | extensión |  | sufijo |  | parámetros |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | herramientas/espía | .printable.a4. | html | / | a/b | ? | x=12 |

**protocolo** HTTP

**host** Nombre del sitio web.

**ruta de contenido** Ruta que especifica el contenido que se procesará. Se utiliza con la extensión. En este ejemplo, se traducen a `tools/spy.html`.

**selectores** se usan para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4.

**extensión** Formato de contenido; también especifica el script que se utilizará para la representación.

**sufijo** se puede usar para especificar información adicional.

**params** Cualquier parámetro necesario para el contenido dinámico.

#### De la URL al contenido y los scripts {#from-url-to-content-and-scripts}

Uso de estos principios:

* la asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso
* cuando se encuentra el recurso adecuado, se extrae el tipo de recurso sling y se utiliza para localizar la secuencia de comandos que se utilizará para representar el contenido

La siguiente imagen ilustra el mecanismo utilizado, que se analiza con más detalle en las secciones siguientes.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, puede especificar qué script procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como lo haría una instrucción SQL en un script PHP), ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca el recurso solicitado en el repositorio (nodo de contenido):

* El primer Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; por ejemplo, `../content/corporate/jobs/developer.html`
* si no se encuentra ningún nodo, se quitará la extensión y se repetirá la búsqueda; por ejemplo, `../content/corporate/jobs/developer`
* si no se encuentra ningún nodo, Sling devuelve el código http 404 (no encontrado).

Sling también permite que otras cosas que no sean nodos JCR sean recursos, pero esta es una función avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae **sling resource type**. Esta es una ruta que localiza el script que se utilizará para procesar el contenido.

La ruta especificada por `sling:resourceType` puede ser:

* absoluto
* relativo a un parámetro de configuración

  Adobe recomienda las rutas relativas a medida que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` o `/libs`, en el cual se busca en este orden (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Otros puntos que hay que tener en cuenta son:

* cuando se requiere el método (GET, POST), se especifica en mayúsculas según la especificación HTTP, por ejemplo, jobs.POST.esp (consulte a continuación)
* se admiten varios motores de scripts:

   * HTL (idioma de plantilla de HTML: sistema de plantillas del lado de servidor recomendado por Adobe Experience Manager para HTML): `.html`
   * Páginas de ECMAScript (JavaScript) (ejecución del lado del servidor): `.esp, .ecma`
   * Java™ Server Pages (ejecución del lado del servidor): `.jsp`
   * Compilador de servlet Java™ (ejecución del lado del servidor): `.java`
   * Plantillas de JavaScript (ejecución del lado del cliente): `.jst`

La lista de motores de scripts admitidos por la instancia determinada de AEM se enumera en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

Además, Apache Sling admite la integración con otros motores de scripts populares (por ejemplo, Groovy, JRuby, Freemarker) y proporciona una forma de integrar nuevos motores de scripts.

En el ejemplo anterior, si `sling:resourceType` es `hr/jobs`, para:

* Solicitudes GET/HEAD y direcciones URL que terminan en .html (tipos de solicitud predeterminados, formato predeterminado)

  La secuencia de comandos es /apps/hr/jobs/jobs.esp; la última sección de sling:resourceType forma el nombre del archivo.

* Solicitudes POST (todos los tipos de solicitud excepto GET/HEAD, el nombre del método debe estar en mayúsculas)

  POST se utiliza en el nombre del script.

  El script es `/apps/hr/jobs/jobs.POST.esp`.

* Direcciones URL en otros formatos que no terminan con .html

  Por ejemplo, `../content/corporate/jobs/developer.pdf`

  El script es `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre del script.

* URL con selectores

  Los selectores se pueden utilizar para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con una impresora, una fuente RSS o un resumen.

  Si mira una versión compatible con la impresora donde el selector podría ser *print*, como en `../content/corporate/jobs/developer.print.html`

  El script es `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre del script.

* Si no se define sling:resourceType:

   * la ruta de contenido se utiliza para buscar un script adecuado (si el ResourceTypeProvider basado en la ruta está activo).

     Por ejemplo, el script de `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.

   * se utiliza el tipo de nodo principal.

* Si no se encuentra ningún script, se utiliza el predeterminado.

  La representación predeterminada es compatible con texto sin formato (.txt), HTML (.html) y JSON (.json), todos los cuales enumeran las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión .res o las solicitudes sin extensión de solicitud es poner en cola el recurso (cuando sea posible).
* Para la gestión de errores http (códigos 403 o 404), Sling busca un script en:

   * la ubicación /apps/sling/servlet/errorhandler para [scripts personalizados](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la ubicación de las secuencias de comandos estándar /libs/sling/servlet/errorhandler/403.esp o 404.esp respectivamente.

Si se aplican varios scripts a una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; es decir, cuanto más coincida el selector, mejor, independientemente de la coincidencia de cualquier extensión de solicitud o nombre de método.

Por ejemplo, considere una solicitud de acceso al recurso
`/content/corporate/jobs/developer.print.a4.html`
de tipo
`sling:resourceType="hr/jobs"`

Suponiendo que tiene la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por la propiedad `sling:resourceType`), también está el supertipo de recursos. Esto se indica mediante la propiedad `sling:resourceSuperType`. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos en la que el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) sea en realidad la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que señala `sling:resourceType`.

Por ejemplo:

* /

   * a
   * b

      * sling:resourceSuperType = a

   * c

      * sling:resourceSuperType = b

   * x

      * sling:resourceType = c

   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a

La jerarquía de tipo de:

* `/x`
   * es `[ c, b, a, <default>]`
* while para `/y`
   * la jerarquía es `[ c, a, <default>]`

Esto se debe a que `/y` tiene la propiedad `sling:resourceSuperType`, mientras que `/x` no la tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### Los scripts de Sling no se pueden llamar directamente {#sling-scripts-cannot-be-called-directly}

En Sling, no se puede llamar directamente a los scripts, ya que esto rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculta el recurso dentro de la secuencia de comandos, por lo que el marco de trabajo (Sling) ya no sabe nada de él. Por lo tanto, se pierden ciertas funciones:

* administración automática de métodos http distintos de GET, incluidos:

   * POST, PUT, DELETE que se gestiona con una implementación predeterminada de sling
   * el script `POST.jsp` en su ubicación sling:resourceType

* su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; es de vital importancia para el desarrollo a gran escala

### API de Sling {#sling-api}

Utiliza el paquete de API de Sling, org.apache.sling.&ast; y bibliotecas de etiquetas.

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los guiones.

Los scripts más complejos (agregar scripts) deben tener acceso a varios recursos (navegación, barra lateral, pie de página, elementos de una lista, por ejemplo) y hacerlo incluyendo *resource*.

Para ello, utilice el comando sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Esto incluye efectivamente la definición del recurso al que se hace referencia, como en la siguiente instrucción que hace referencia a una definición existente para procesar imágenes:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se conoce como Sistema de módulos dinámicos para Java™). Los contenedores OSGi le permiten dividir la aplicación en módulos individuales (que son archivos jar con información meta adicional y llamados paquetes en la terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* servicios implementados dentro del contenedor
* un contrato entre el contenedor y la aplicación

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse dinámicamente entre sí para colaborar.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciarlos.

>[!NOTE]
>
>Encontrará información completa sobre la tecnología OSGi en el [sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. Sling, y por lo tanto CQ5, utiliza la implementación [Apache Felix](https://felix.apache.org/documentation/index.html) de OSGI (iniciativa Open Services Gateway) y se basa en las especificaciones de la versión 4.2 de la plataforma de servicio OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* instalar
* start
* parada
* actualizar
* desinstalar
* ver el estado
* acceda a información más detallada (por ejemplo, nombre simbólico, versión y ubicación) sobre los paquetes específicos

Consulte [la consola web](/help/sites-deploying/web-console.md), [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) y [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener más información.

## Objetos de desarrollo en el entorno de AEM {#development-objects-in-the-aem-environment}

Los siguientes son de interés para el desarrollo:

**Elemento** Un elemento es un nodo o una propiedad.

Para obtener información detallada sobre la manipulación de objetos Item, consulte los [documentos Java™](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) de la interfaz javax.jcr.Item

**Nodo (y sus propiedades)** Los nodos y sus propiedades se definen en la especificación JCR API 2.0 (JSR 283). Almacenan contenido, definiciones de objetos, secuencias de comandos de procesamiento y otros datos.

Los nodos definen la estructura de contenido y sus propiedades almacenan el contenido y los metadatos reales.

Los nodos de contenido dirigen la renderización. Sling obtiene el nodo de contenido de la solicitud entrante. La propiedad sling:resourceType de este nodo señala al componente de procesamiento Sling que se va a utilizar.

Un nodo, que es un nombre JCR, también se denomina recurso en el entorno de Sling.

Por ejemplo, para obtener las propiedades del nodo actual, puede utilizar el siguiente código en el script:

`PropertyIterator properties = currentNode.getProperties();`

CurrentNode es el objeto de nodo actual.

Para obtener más información sobre cómo manipular objetos Node, consulte [Documentos de Java™](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget**: en AEM, todos los widgets administran todas las entradas de usuario. Suelen utilizarse para controlar la edición de un fragmento de contenido.

Los cuadros de diálogo se crean combinando widgets.

AEM se ha desarrollado utilizando la biblioteca de widgets ExtJS.

**Diálogo** Un cuadro de diálogo es un tipo especial de widget.

Para editar contenido, AEM utiliza cuadros de diálogo definidos por el desarrollador de la aplicación. Estos combinan una serie de widgets para presentar al usuario todos los campos y acciones necesarios para editar el contenido relacionado.

Los cuadros de diálogo también se utilizan para editar metadatos y para varias herramientas administrativas.

**Componente** Un componente de software es un elemento del sistema que ofrece un servicio o evento predefinido y que puede comunicarse con otros componentes.

En AEM, a menudo se utiliza un componente para procesar el contenido de un recurso. Cuando el recurso es una página, el componente que lo procesa se denomina componente de nivel superior o componente de página. Sin embargo, un componente no tiene que procesar contenido ni estar vinculado a un recurso específico. Por ejemplo, un componente de navegación muestra información sobre varios recursos.

La definición de un componente incluye lo siguiente:

* el código utilizado para procesar el contenido
* un cuadro de diálogo para la entrada del usuario y la configuración del contenido resultante.

**Plantilla** Una plantilla es la base para un tipo específico de página. Al crear una página en la pestaña Sitios web, el usuario debe seleccionar una plantilla. A continuación, la nueva página se crea copiando esta plantilla.

Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Define el componente de página utilizado para procesar la página y el contenido predeterminado (contenido principal de nivel superior). El contenido define cómo se procesa, ya que AEM está centrado en el contenido.

**Componente de página (componente de nivel superior)** Componente que se utilizará para procesar la página.

**Página** Una página es una &#39;instancia&#39; de una plantilla.

Una página tiene un nodo de jerarquía de tipo cq:Page y un nodo de contenido de tipo cq:PageContent. La propiedad sling:resourceType del nodo de contenido señala al componente de página utilizado para procesar la página.

Por ejemplo, para obtener el nombre de la página actual, puede utilizar el siguiente código en el script:

S`tring pageName = currentPage.getName();`

CurrentPage es el objeto de página actual. Para obtener más información sobre cómo manipular los objetos Page, consulte [Documentos de Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html).

**Administrador de páginas** El administrador de páginas es una interfaz que proporciona métodos para operaciones de nivel de página.

Por ejemplo, para obtener la página contenedora de un recurso, puede utilizar el siguiente código en el script:

Página myPage = pageManager.getContainingPage(myResource);

PageManager, que es el objeto de administrador de páginas, y myResource, un objeto de recurso. Para obtener más información sobre los métodos proporcionados por el administrador de páginas, consulte [Documentos de Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html).

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece información general sobre la estructura que se ve dentro del repositorio.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado.
>
>Los cambios son necesarios cuando está desarrollando, pero debe tener cuidado de comprender completamente las implicaciones de cualquier cambio que realice.

>[!CAUTION]
>
>No cambie nada en la ruta de acceso `/libs`. Para cambios de configuración y de otro tipo, copie el elemento de `/libs` a `/apps` y realice los cambios que desee en `/apps`.

* `/apps`

  Relacionado con la aplicación; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/foundation/components`.

* `/content`

  Contenido creado para su sitio web.

* `/etc`

* `/home`

  Información de usuario y grupo.

* `/libs`

  Bibliotecas y definiciones que pertenecen al núcleo de AEM. Las subcarpetas de `/libs` representan las características de AEM predeterminadas, como la búsqueda o la replicación. El contenido de `/libs` no debe modificarse, ya que afecta al funcionamiento de AEM. Las características específicas del sitio web se deben desarrollar en `/apps` (consulte [Personalización de componentes y otros elementos](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

  Zona de trabajo temporal.

* `/var`

  Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y control de eventos.

## Entornos {#environments}

Con AEM, un entorno de producción a menudo consta de dos tipos diferentes de instancias: una instancia de [autor y una instancia de publicación](/help/sites-deploying/deploy.md#author-and-publish-installs).

## El Dispatcher {#the-dispatcher}

Dispatcher es la herramienta de Adobe para el almacenamiento en caché o el equilibrio de carga. Encontrará más información en [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

## FileVault (sistema de revisión de origen) {#filevault-source-revision-system}

FileVault proporciona a su repositorio JCR la asignación del sistema de archivos y el control de versiones. Se puede utilizar para administrar proyectos de desarrollo de AEM con compatibilidad total para almacenar y crear versiones del código, el contenido, las configuraciones, etc. del proyecto en sistemas estándar de control de versiones (por ejemplo, Subversion).

Consulte la documentación de [FileVault tool](/help/sites-developing/ht-vlttool.md) para obtener información detallada.

## Flujos de trabajo {#workflows}

El contenido suele estar sujeto a procesos organizativos, incluidos pasos como la aprobación y la aprobación por parte de varios participantes. Estos procesos se pueden representar como flujos de trabajo [definidos y desarrollados en AEM](/help/sites-developing/workflows-models.md), que luego se aplican a las [páginas de contenido apropiadas](/help/sites-administering/workflows.md) o a [recursos digitales](/help/assets/assets-workflow.md), según sea necesario.

El motor de flujo de trabajo se utiliza para administrar la implementación de los flujos de trabajo y la aplicación posterior al contenido.

## Administración de varios sitios {#multi-site-management}

El Administrador de varios sitios (MSM) le permite administrar fácilmente varios sitios web que comparten contenido común. MSM le permite definir relaciones entre los sitios para que los cambios de contenido en un sitio se dupliquen automáticamente en otros.

Por ejemplo, los sitios web a menudo se ofrecen en varios idiomas para audiencias internacionales. Cuando el número de sitios en el mismo idioma es bajo (de tres a cinco), es posible realizar un proceso manual de sincronización de contenido entre sitios. Sin embargo, cuando el número de sitios aumenta o cuando hay varios idiomas implicados, es más eficiente automatizar el proceso.

* Gestionar de forma eficaz las distintas versiones lingüísticas de un sitio web.
* Actualizar automáticamente uno o varios sitios en función de un sitio de origen:

   * Haga cumplir una estructura base común y utilice contenido común en varios sitios.
   * Maximice el uso de los recursos disponibles.
   * Mantenga un aspecto común.
   * Centrar los esfuerzos en administrar el contenido que difiere entre los sitios.

Para obtener más información, consulte [Administrador de varios sitios](/help/sites-administering/msm.md).
