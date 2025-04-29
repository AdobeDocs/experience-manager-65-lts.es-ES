---
title: Ajustes de configuración de OSGi
description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista sirve de directriz y no es exhaustiva.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: d3356f5f-f80f-4ce0-b4e2-3ee927208ab1
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '3247'
ht-degree: 0%

---

# Ajustes de configuración de OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) es un elemento fundamental en la pila de tecnología de AEM. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona las primitivas estandarizadas que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación e implementarse*&quot;.

Esta funcionalidad permite administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [especificación OSGi](https://docs.osgi.org/specification/)) está contenido en uno de los distintos paquetes. Al trabajar con AEM, existen varios métodos para administrar la configuración de dichos paquetes; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

Las siguientes opciones de configuración de OSGi (enumeradas según el paquete) son relevantes para la implementación del proyecto. No es necesario ajustar todas las configuraciones enumeradas, algunas se mencionan para ayudarle a comprender cómo funciona AEM.

>[!CAUTION]
>
>La lista tiene por objeto servir de directriz y no es exhaustiva. No se enumeran todos los paquetes ni todos los parámetros de algunos de los paquetes que sí lo están.
>
>La configuración necesaria varía según el proyecto.
>
>Consulte la consola web para obtener información detallada sobre los parámetros y los valores utilizados.

>[!NOTE]
>
>Pueden ser necesarios paquetes adicionales para áreas específicas de funcionalidad dentro de AEM. En estos casos, los detalles de configuración se pueden encontrar en la página relacionada con la funcionalidad adecuada.

**Receptor de eventos de replicación de AEM** Configurar:

* **Modos de ejecución**, en los que los eventos de replicación se distribuyen a los oyentes. Por ejemplo, si se define como autor, es el sistema el que &quot;inicia&quot; la replicación.

* Agregue el modo de ejecución **publish** si el código del proyecto procesa eventos de replicación (replicación inversa) en un entorno de publicación. Por ejemplo, cuando se utiliza Dispatcher para vaciar del entorno de publicación o cuando se produce la replicación estándar en otras instancias de publicación.

**Agente de escucha de cambios del repositorio de AEM** Configurar:

* **Rutas**, ubicaciones para detectar eventos de repositorio listos para su distribución.

**Repositorio de cliente de CRX Sling**: configure el acceso al repositorio de contenido subyacente.

* La **contraseña de administrador** debe cambiarse después de la instalación para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de su instancia.
* No deben ser necesarios otros cambios y debe tenerse cuidado, ya que pueden afectar al acceso al repositorio.

**Consola de administración Apache Felix OSGi** Configurar:

* **Plugins**, los elementos de navegación principales (plugins de consola) estarán disponibles en la **Consola de administración web Apache Felix** como elementos de menú de nivel superior. Deshabilite las que no necesite, ya que cada una de ellas requiere espacio y recursos.

>[!CAUTION]
>
>Asegúrese de configurar lo siguiente:
>
>**Nombre de usuario** y **Contraseña**, las credenciales para acceder a la propia consola de administración web de Apache Felix.
>La contraseña debe cambiarse después de la instalación inicial para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de su instancia.

>[!NOTE]
>
>Esta configuración debe realizarse utilizando la consola Felix según sea necesario al inicio, antes de que el repositorio esté disponible.

**Registrador de datos de solicitud personalizable de Apache Sling** Configurar:

* **Nombre del registrador** y **Formato de registro** para configurar la ubicación y el formato del registro de solicitud y acceso (predeterminado: `request.log`). Este archivo de registro es esencial al analizar el rendimiento o la funcionalidad de depuración relacionada con la cadena web. Está emparejado con [Apache Sling Request Logger](#apacheslingrequestlogger).

Ver [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Grupo de subprocesos de Apache Sling** Configurar:

* **Tamaño mínimo del grupo** y **Tamaño máximo del grupo**, el tamaño del grupo utilizado para contener los subprocesos de evento.

* **Tamaño de cola**, el tamaño máximo de la cola de subprocesos si se agota el grupo.
El valor recomendado es `-1` porque establece la cola en ilimitada. Si se establece un límite, pueden producirse pérdidas cuando se supera.

* Cambiar esta configuración puede ayudar al rendimiento en escenarios con un número elevado de eventos. Por ejemplo, uso intensivo de AEM DAM o Flujo de trabajo.
* Los valores específicos de su escenario deben establecerse con pruebas.
* Esta configuración puede afectar al rendimiento de su instancia, por lo que no la cambie sin motivo y teniendo en cuenta los motivos.

**Apache Sling GET Servlet** Configure algunos aspectos del procesamiento:

* **Indexación automática** para habilitar o deshabilitar el procesamiento de directorios para la exploración.
* **Habilitar** (o deshabilitar) las representaciones predeterminadas, como **HTML**, **Texto sin formato**, **JSON** o **XML**.
No deshabilite JSON.

>[!NOTE]
>
>Esta opción se configura automáticamente para las instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Controlador Apache Sling Java Script** Configure las opciones para la compilación de archivos .java como scripts (servlets).

Ciertas configuraciones pueden afectar al rendimiento. Deshabilite esta configuración siempre que sea posible, especialmente en el caso de una instancia de producción.

* **Source VM** y **Target VM**, definen la versión del JDK que se usa como JVM de tiempo de ejecución

* para instancias de producción:

   * deshabilitar **Generar información de depuración**

**Instalador JCR de Apache Sling**: estos parámetros probablemente no necesitan configuración, pero pueden ser útiles para saberlo al desarrollar o depurar. Por ejemplo, las carpetas de instalación pueden ser útiles para proteger o desproteger, o crear un paquete.

* **Nombre de las carpetas de instalación regexp** y **Profundidad máxima de jerarquía de las carpetas de instalación**: especifique dónde y a qué profundidad se buscan los recursos que se van a instalar en las carpetas del repositorio. Cuando se usa un comodín (como en ).&#42;/instalación) se buscan todas las coincidencias apropiadas, por ejemplo, `/libs/sling/install` y `/libs/cq/core/install`.

* **Ruta de búsqueda**, lista de rutas en las que jcrinstall busca los recursos que se van a instalar, junto con un número que indica el factor de ponderación para esa ruta.

**Configuración de la cola de Apache Sling** Configure los parámetros que administran la programación de trabajos:

* **Intervalo de reintento**, **Reintentos máximos**, **Trabajos paralelos máximos**, entre otros.

* Cambiar esta configuración puede mejorar el rendimiento en escenarios con un número elevado de trabajos; por ejemplo, un uso intensivo de DAM y flujos de trabajo de AEM.
* Los valores específicos de su escenario deben establecerse con pruebas.
* No cambie esta configuración sin motivo, solo cambie después de haber tomado las debidas medidas.

**Controlador de scripts JSP de Apache Sling** Configure los ajustes relevantes de rendimiento para el controlador de scripts JSP. Para mejorar el rendimiento, debe deshabilitar tanto como sea posible.

En particular para las instancias de producción:

* deshabilitar **Generar información de depuración**
* deshabilitar **Mantener Java generado™**
* deshabilitar **contenido asignado**
* deshabilitar **Mostrar fragmentos de Source**

>[!NOTE]
>
>Esta opción se configura automáticamente para las instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Configuración de registro de Apache Sling** Configurar:

* **Nivel de registro** y **Archivo de registro**, para definir la ubicación y el nivel de registro de la configuración de registro central (error.log). El nivel se puede establecer en `DEBUG`, `INFO`, `WARN`, `ERROR` y `FATAL`.

* **Número de archivos de registro** y **Umbral de archivo de registro** para definir el tamaño y la rotación de la versión del archivo de registro.

* **Patrón de mensajes** define el formato de los mensajes de registro.

Ver [Registro de AEM](/help/sites-deploying/configure-logging.md#global-logging) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración del registrador de Apache Sling (configuración de fábrica)** Configurar:

* **Nivel de registro**, **Archivo de registro** y **Formato de mensaje** para definir los detalles del archivo de registro y los mensajes.

* **Registrador** para definir la categoría; por ejemplo, registrar solo para com.day.cq.

* Mediante **Configuraciones de fábrica**, se puede agregar cualquier número de configuraciones adicionales para satisfacer los distintos niveles de registro y categorías necesarios.
* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para tener mensajes sobre un servicio específico registrados en un archivo de registro individual para facilitar la monitorización.

Ver [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración del escritor de registro de Apache Sling (configuración de fábrica)** Configurar:

* **Archivo de registro** para definir la existencia de un archivo de registro.
* **Número de archivos de registro** para definir la rotación de la versión.

* Una configuración de **Apache Sling Logging Configuration** puede usar el escritor.

* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para tener mensajes sobre un servicio específico registrados en un archivo de registro individual para facilitar la monitorización.

Ver [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Servlet Principal De Apache Sling** Configurar:

* **Número de llamadas por solicitud** y **Profundidad de recursión** para proteger su sistema contra la recursión infinita y las llamadas de script excesivas.

**Servicio de tipo MIME de Apache Sling Commons** Configurar:

* **Tipos MIME** para agregar al sistema los tipos requeridos por el proyecto. Al hacerlo, se permite una solicitud `GET` en un archivo para establecer el encabezado de tipo de contenido correcto para vincular el tipo de archivo y la aplicación.

**Filtro de referente de Apache Sling** Para abordar problemas de seguridad conocidos con falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe configurar el filtro de referente.

El servicio de filtro de referente es un servicio OSGi que le permite configurar lo siguiente:

* qué métodos http se deben filtrar
* si se permite un encabezado de referente vacío
* y una lista de servidores que se permitirán además del host de servidor.

Consulte la [Lista de comprobación de seguridad - Problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.

>[!NOTE]
>
>El filtro de referente de Apache Sling depende de la instalación de un paquete de correcciones rápidas.

**Registrador de solicitudes de Apache Sling** Configurar:

* varios parámetros para definir cómo se registran las solicitudes.
* **Habilitar el registro de solicitudes** para habilitar o deshabilitar.

* **Habilitar el registro de acceso** para habilitar o deshabilitar.

Junto con [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Ver [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Resource Resolver Factory** Configure los aspectos centrales de la resolución de recursos de Sling:

* **Rutas de búsqueda de recursos**, agregue cualquier ruta específica del proyecto (pero no elimine `/libs` ni `/apps`).

* **URL virtuales** para definir las asignaciones de URL de vanidad.

* **Asignaciones de URL** para definir alias. Por ejemplo, de `/content` a `/`.

* **Ubicación de asignación**, la configuración del asignador externalizada en `/etc/map`.

* Utilice su instalación local (por ejemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qué Resource Resolver está activo.

Consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configure estas opciones en el repositorio.
>
>De lo contrario, los cambios realizados en **asignaciones de URL** mediante la consola Felix podrían ser sobrescritos por AEM en el siguiente inicio.

**Apache Sling Servlet/Script Resolver y controlador de errores** El Sling Servlet y Script Resolver tienen varias tareas:

1. Se utiliza como `ServletResolver` para seleccionar el servlet o script al que llamar para administrar la solicitud.

1. Actúa como `SlingScriptResolver`.

1. Administra la administración de errores implementando la interfaz `ErrorHandler` con el mismo algoritmo para seleccionar los servlets y scripts de administración de errores que se usan para resolver los servlets y scripts de procesamiento de solicitudes.

Se pueden configurar varios parámetros, entre ellos:

* **Rutas de ejecución**: enumera las rutas para buscar scripts ejecutables. Al configurar rutas específicas, puede limitar qué scripts se pueden ejecutar. Si no se configura ninguna ruta de acceso, se usa la predeterminada ( `/` = raíz), lo que permite la ejecución de todos los scripts.
Si un valor de ruta configurado termina con una barra diagonal, se busca en todo el subárbol. Sin esta barra diagonal, la secuencia de comandos solo se ejecuta si coincide exactamente.

* **Extensiones predeterminadas**: lista de extensiones para las que se usa el comportamiento predeterminado. El último segmento de ruta del tipo de recurso se puede utilizar como nombre de script.

**Configuración proxy de componentes HTTP Apache**: la configuración proxy para todo el código que use el cliente HTTP Apache, usado cuando se hace un HTTP. Por ejemplo, en la replicación.

Al crear una configuración, no cambie la configuración de fábrica. En su lugar, cree una configuración de fábrica para este componente con el administrador de configuración disponible aquí: **https://localhost:4502/system/console/configMgr/**. La configuración proxy está disponible en **org.apache.http.proxyconfigurator.**

**Adobe Granite HTML Library Manager** Configúrelo para controlar el manejo de las bibliotecas de cliente (css o js), incluyendo, por ejemplo, cómo se ve la estructura subyacente.

* Para instancias de producción:

   * habilitar **Minify** (para eliminar los caracteres CRLF y de espacio en blanco).
   * habilite **Gzip** (para permitir que se comprima y se acceda a los archivos con una solicitud).
   * deshabilitar **Depuración**
   * deshabilitar **Intervalos**

* Para el desarrollo de JS (especialmente cuando se activa la depuración/depuración):

   * deshabilitar **Minificar**
   * habilite **Debug** para separar los archivos para depurarlos y usarlos con el error de activación.
   * habilita **Tiempo** si estás interesado en el tiempo.
   * habilite la consola **Debug** para ver los mensajes de registro de la consola JS.

>[!CAUTION]
>
>Al cambiar la configuración de **Minify** o **Gzip**, elimine el contenido de la caché de clientlibs. Consulte [Artículo de la base de conocimiento](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html) para obtener detalles.

>[!NOTE]
>
>Esta opción se configura automáticamente para las instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Controlador de autenticación de encabezado HTTP de Adobe Granite** Configuración de todo el sistema para el método de autenticación básico de la solicitud HTTP.

Al usar [grupos de usuarios cerrados](/help/sites-administering/cug.md), puede configurar, entre otros, lo siguiente:

* **Dominio HTTP**
* **Página de inicio de sesión predeterminada**

**Servicio Day CQ Link Checker** Comprobar y, si es necesario, configurar:

* **Periodo del programador** para definir el intervalo en el que se deben comprobar automáticamente los vínculos externos.

* Compruebe **Intervalo de tolerancia de vínculo incorrecto** durante el período después del cual un vínculo externo erróneo se considera incorrecto.
* **Patrones de anulación de comprobación de vínculos** para definir las rutas que se excluirán de la comprobación de vínculos.

**Tarea del verificador de vínculos CQ por día** Configure las opciones para una sola tarea del verificador de vínculos (una tarea que comprueba un vínculo externo):

* Compruebe los intervalos definidos en **Intervalo de prueba de vínculo correcto** e **Intervalo de prueba de vínculo incorrecto**

* Los distintos parámetros relacionados con los proxies para el acceso a Internet y NTLM que son necesarios para el acceso externo al comprobar un vínculo.

**Servicio Day CQ Mail** Configure el nombre de host y los detalles de acceso para el servidor de correo. Consulte la sección Configuración del servicio de correo.

**Boletín Day CQ MCM** Configure las distintas opciones que se usan con el boletín.

**Asignación raíz de CQ de día** Configurar:

* **Ruta de destino** para definir a dónde se redirige una solicitud a &quot;`/`&quot;.

Hay dos interfaces de usuario disponibles en AEM:

* la IU táctil es la IU estándar
* y la IU clásica obsoleta sigue funcionando por completo

Con la asignación raíz de AEM puede configurar la interfaz de usuario que desea tener como predeterminada para su instancia:

* Para que la interfaz de usuario táctil sea la interfaz de usuario predeterminada, **Target Path** debe apuntar a lo siguiente:

  ```shell
     /projects.html
  ```

* Para que la IU clásica sea la IU predeterminada, la **Ruta de destino** debe apuntar a lo siguiente:

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>En una instalación estándar, la IU táctil optimizada es la IU predeterminada.

**Controlador de autenticación SSO de Adobe Granite**: configure los detalles de SSO (inicio de sesión único). Estos detalles suelen ser necesarios en configuraciones de creación empresariales, a menudo con LDAP.

Hay varias propiedades de configuración disponibles:

* **Ruta**
Ruta de acceso para la que está activo este controlador de autenticación. Si este parámetro se deja vacío, el controlador de autenticación se desactiva. Por ejemplo, la ruta / hace que el controlador de autenticación se utilice para todo el repositorio.

* **Clasificación del servicio**
El valor de clasificación del servicio marco OSGi se utiliza para indicar el orden utilizado para llamar a este servicio. Este valor es un valor `int` en el cual los valores más altos designan una prioridad más alta.
El valor predeterminado es `0`.

* **Nombres de encabezado**
Nombres de encabezados que pueden contener un ID de usuario.

* **Nombres de cookies**
Nombres de cookies que podrían contener un ID de usuario.

* **Nombres de parámetros**
Nombres de los parámetros de solicitud que pueden proporcionar el ID de usuario.

* **Mapa de usuario**
Para los usuarios seleccionados, el nombre de usuario extraído de la solicitud HTTP se puede reemplazar por uno diferente en el objeto de credenciales. La asignación se define aquí. Si el nombre de usuario `admin` aparece a ambos lados del mapa, se omite la asignación. El carácter &quot;=&quot; debe tener un carácter de escape &quot;\&quot; inicial.

* **Formato**
Indica el formato en el que se proporciona el ID de usuario. Utilice:

   * `Basic` si el ID de usuario está codificado en el formato de autenticación HTTP Basic
   * `AsIs` si el ID de usuario se proporciona en texto sin formato o si se aplica cualquier valor de expresión regular debe usarse tal cual o cualquier expresión regular

**Filtro de depuración Day CQ WCM** Esto resulta útil al desarrollar, ya que permite el uso de sufijos como ?debug=layout al acceder a una página. Por ejemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout proporciona información de diseño que puede ser de interés para el desarrollador.

* Para garantizar el rendimiento y la seguridad, deshabilite en instancias de producción.

**Filtro WCM CQ de día** Configurar:

* **Modo WCM** para definir el modo predeterminado.
* En una instancia de autor, este modo puede ser `edit`, `disable,preview` o `analytics`.
Se puede acceder a los demás modos desde la barra de tareas o se puede utilizar el sufijo `?wcmmode=disabled` para emular un entorno de producción.

* En una instancia de publicación, este modo debe establecerse en `disabled` para garantizar que no se pueda acceder a ningún otro modo.

>[!NOTE]
>
>Esta opción se configura automáticamente para las instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Verificador de vínculos CQ WCM por día** Configurar:

* **Lista de configuraciones de reescritura** para especificar una lista de ubicaciones para las configuraciones del verificador de vínculos basado en contenido. Las configuraciones se pueden basar en el modo de ejecución. Este hecho es importante para distinguir entre los entornos de creación y publicación, ya que la configuración del verificador de vínculos puede diferir.

**Fábrica del administrador de páginas de CQ WCM por día** Configurar:

* **Comprobación de activación del subárbol de páginas** para que un usuario (sin permisos de replicación) elimine o mueva páginas (incluso si las páginas no están activadas).

**Procesador de páginas CQ WCM por día** Configurar:

* **Rutas**, una lista de ubicaciones donde el sistema escucha las modificaciones de la página antes de activar `jcr:Event`.

**Rastreador de impresiones de página de Adobe** Para una instancia de autor, configúrela de la siguiente manera:

* **sling.auth.requirements**: establezca el valor de esta propiedad en `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Esta configuración permite solicitudes anónimas al servicio de seguimiento.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Estadísticas de página de CQ WCM de día** para una configuración de instancia de publicación:

* **URL para enviar datos** a fin de configurar la URL utilizada para realizar el seguimiento de las estadísticas de la página (es vital si una solicitud del rastreador pasa por Dispatcher); por ejemplo, el valor predeterminado es `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de seguimiento habilitado** para habilitar (`true`) o deshabilitar (`false`) la inclusión del script de seguimiento en las páginas. El valor predeterminado es `false`.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Administrador de versiones de CQ WCM de día** para controlar si las versiones se administran en el sistema y cómo se hacen:

* **Crear versión en la activación**, habilitada en una instalación estándar
* **Habilitar purga**

* **Rutas de purga**, las rutas que busca una acción de búsqueda.
* **Rutas de versiones implícitas**, las rutas en las que está activo el control de versiones implícito.

* **Edad máxima de la versión**, la edad máxima (en días) de una versión

* **Número máximo de versiones**, el número máximo de versiones que se deben conservar

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener más información.

**Servicio de notificación por correo electrónico del flujo de trabajo de CQ por día** Configure los parámetros de correo electrónico para las notificaciones enviadas por un flujo de trabajo.

**Fábrica del analizador de HTML del reescritor de Adobe AEM**

Controla el analizador de HTML para la reescritura CQ.

* **Etiquetas adicionales para procesar**: puede agregar o quitar etiquetas HTML para que las procese el analizador. De forma predeterminada, se procesan las siguientes etiquetas: A, IMG, AREA, FORM, BASE, LINK, SCRIPT, BODY, HEAD.
* **Conservar mayúsculas y minúsculas**: de forma predeterminada, el analizador de HTML convierte los atributos en mayúsculas y minúsculas (por ejemplo, `eBay`) a minúsculas (por ejemplo, `ebay`). Puede desactivar esta configuración para conservar los atributos de mayúsculas y minúsculas. Esta configuración es útil cuando se utilizan marcos de front-end como Angular 2.

**Grupo de conexiones JDBC de Day Commons**: configure el acceso a una base de datos externa que se esté utilizando como fuente de contenido.

Una configuración de fábrica, para que se puedan configurar varias instancias.

**Reescritor de CDN** Debe asegurarse la comunicación entre AEM y una CDN para que los recursos/binarios se entreguen a un usuario final de forma segura. Este proceso implica las dos tareas siguientes:

* Acceso al recurso desde AEM mediante la red de distribución de contenido (CDN) la primera vez (o después de que caducara en la caché).
* Acceder a los recursos almacenados en caché en CDN de forma segura. Una vez que el recurso se almacena en caché en CDN, la solicitud no se envía a AEM y todos los usuarios que tienen acceso a ese recurso en deben recibir servicios desde CDN.

AEM proporciona un reescritor para reescribir las URL de los recursos internos en URL de CDN externas. Reescribe los vínculos para pasarlos a la CDN, incluida una firma JWS y el tiempo de caducidad para permitir que el recurso se acceda de forma segura. Esta función se debe utilizar en instancias de autor.

El flujo total es el siguiente:

1. El usuario se autentica con AEM y solicita una página con recursos.
1. La página solicitada contiene un recurso similar a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter transforma el vínculo en una URL de CDN que contiene una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. A continuación, el explorador del usuario reenvía la solicitud de recurso al servidor CDN
1. CDN debe configurarse para reenviar la solicitud a AEM junto con el parámetro `cdn_sign`.
1. Un controlador de autenticación valida el parámetro `cdn_sign` y devuelve el recurso a CDN, que luego se entrega al usuario

El flujo entre el explorador del usuario, la CDN y AEM se puede visualizar de la siguiente manera.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Esta función solo está habilitada para instancias de autor de AEM.

**CDNConfigServiceImpl** proporciona configuraciones de CDN

La característica de reescritura de CDN se puede habilitar proporcionando **nombre de dominio de distribución de CDN** en la configuración de com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

El servicio también contiene otras opciones de configuración como habilitar/deshabilitar la reescritura de CDN, prefijos de ruta para los que se realiza la reescritura de CDN, valores TTL y protocolo (HTTP o HTTPS).

**CDNRewriter** Un reescritor para reescribir URL de imagen internas en URL de CDN

El valor **Atributos de etiqueta** en com.adobe.cq.cdn.rewriter.impl.CDNRewriter se puede definir de modo que solo se reescriban los vínculos de imagen selectivos.
