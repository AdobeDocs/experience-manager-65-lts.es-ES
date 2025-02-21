---
title: Arquitectura de los formularios HTML5
description: Los formularios HTML5 se implementan como un paquete en la instancia de AEM incrustada y exponen la funcionalidad como un extremo REST a través de HTTP/S mediante la arquitectura RESTful de Sling Apache.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 96%

---

# Arquitectura de los formularios HTML5{#architecture-of-html-forms}

## Arquitectura {#architecture}

La funcionalidad de los formularios HTML5 se implementa como un paquete en la instancia de AEM incrustada y se expone como un extremo REST a través de HTTP/S mediante la [arquitectura RESTful de Sling Apache.](https://sling.apache.org/).

![02-aem-forms-Architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Uso del marco de Sling {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) se centra en los recursos. Utiliza una URL de solicitud para resolver primero el recurso. Cada recurso tiene una propiedad **sling:resourceType** (o **sling:resourceSuperType**). En función de esta propiedad, el método de solicitud y las propiedades de la URL de solicitud, se selecciona un script de Sling para administrar la solicitud. Este script de Sling puede ser un JSP o un servlet. Para formularios HTML5, los nodos del **perfil** actúan como recursos de Sling y el **procesador de perfiles** actúa como el script de Sling que administra la solicitud para procesar el formulario móvil con un perfil determinado. Un **procesador de perfiles** es un JSP que lee parámetros de una solicitud y llama al servicio OSGi de Forms.

Para obtener más información sobre el extremo REST y los parámetros de solicitud admitidos, consulte [Plantilla de formulario de renderización](/help/forms/using/rendering-form-template.md).

Cuando un usuario realiza una solicitud desde un dispositivo cliente, como un explorador iOS o Android™, Sling resuelve primero el nodo del perfil en función de la dirección URL de la solicitud. En este nodo de perfil, se lee **sling:resourceSuperType** y **sling:resourceType** para determinar todos los scripts disponibles que puedan administrar esta solicitud del procesador de Forms. A continuación, se utilizan selectores de solicitud de Sling junto con el método de solicitud para identificar el script más adecuado para administrar esta solicitud. Una vez que la solicitud llega a un JSP del procesador de perfiles, el JSP llama al servicio OSGi de Forms.

Para obtener más información sobre la resolución de scripts de Sling, consulte [Hoja de características de Sling de AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) o [Descomposición de la URL de Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### Flujo de llamada de procesamiento de formularios típico {#typical-form-processing-call-flow}

Los formularios HTML5 almacenan en la caché todos los objetos intermedios necesarios para procesar (representar o enviar) un formulario en la primera solicitud. No almacenan en caché los objetos que dependen de los datos, ya que es probable que estos objetos cambien.

Un formulario móvil mantiene dos niveles diferentes de caché: la caché de procesamiento previo y la caché de procesamiento. La caché de procesamiento previo contiene todos los fragmentos e imágenes de una plantilla resuelta, y la caché de procesamiento contiene el contenido procesado como HTML.

![Flujo de trabajo de formularios HTML5](assets/cacheworkflow.png)

Flujo de trabajo de formularios HTML5

Los formularios HTML5 no almacenan en caché las plantillas a las que les faltan referencias de fragmentos e imágenes. Si los formularios HTML5 tardan más de lo normal en completarse, compruebe en los registros del servidor si faltan referencias y advertencias. Asegúrese también de que no se alcance el tamaño máximo del objeto.

El servicio OSGi de Forms procesa una solicitud en dos pasos:

* **Diseño y generación del estado del formulario inicial**: el servicio de procesamiento OSGi de Forms llama al componente Caché de Forms para determinar si el formulario ya se ha almacenado en caché y no se ha invalidado. Si el formulario está en la caché y es válido, sirve el HTML generado desde la caché. Si el formulario se invalida, el servicio de procesamiento OSGi de Forms genera el diseño del formulario inicial y el estado de formulario en formato XML. El servicio OSGi de Forms transforma este XML en el diseño HTML y el estado de formulario JSON inicial en la caché para las solicitudes posteriores.
* **Formularios cumplimentados previamente**: durante el procesamiento, si un usuario solicita formularios con datos previamente cumplimentados, el servicio de procesamiento OSGi de Forms llama al contenedor del servicio Forms y genera un nuevo estado de formulario con datos combinados. Sin embargo, como el diseño ya se ha generado en el paso anterior, esta llamada es más rápida que la primera. Esta llamada realiza únicamente la combinación de datos y ejecuta los scripts en los datos.

Si hay alguna actualización en el formulario o en cualquiera de los recursos utilizados en el formulario, el componente Caché de Forms lo detecta, y la caché de ese formulario en particular se invalida. Una vez que el servicio OSGi de Forms termina de procesarse, el jsp del procesador de perfiles agrega referencias de biblioteca JavaScript y estilo a este formulario y devuelve la respuesta al cliente. En este punto, es posible usar un servidor web típico como [Apache](https://httpd.apache.org/) con compresión de HTML activada. Un servidor web reduciría significativamente el tamaño de respuesta, el tráfico de red y el tiempo necesario para transmitir los datos entre el servidor y el equipo cliente.

Cuando un usuario envía el formulario, el explorador envía el estado de formulario en formato JSON al [proxy del servicio de envío](../../forms/using/service-proxy.md); a continuación, este genera un XML de datos utilizando datos JSON y envía ese XML de datos para enviar el extremo.

## Componentes {#components}

Se necesita el paquete de complementos de AEM Forms para habilitar los formularios HTML5. Para obtener más información sobre la instalación del paquete de complementos de AEM Forms, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componentes OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Procesador de formularios XFA de Adobe (com.adobe.livecycle.adobe-lc-forms-core)** es el nombre para mostrar del paquete OSGi de formularios HTML5 cuando se ve desde la vista Paquete de la Consola de administración Felix (https://[host]:[port]/system/console/bundles).

Este componente contiene componentes OSGi para las opciones de procesamiento, administración de caché y configuración.

#### Servicio OSGi de Forms {#forms-osgi-service}

Este servicio OSGi contiene la lógica para procesar un XDP como HTML y administra el envío de un formulario para generar el XML de datos. Este servicio utiliza el contenedor del servicio Forms. El contenedor del servicio Forms llama internamente al componente nativo `XMLFormService.exe`, que realiza el procesamiento.

Si se recibe una solicitud de procesamiento, este componente llama al contenedor del servicio Forms para generar la información de estado y diseño que se procesa más adelante para generar estados DOM de formulario HTML y JSON.

Este componente también es responsable de la generación del XML de datos desde el estado de formulario JSON enviado.

#### Componente Caché {#cache-component}

Los formularios de HTML5 utilizan el almacenamiento en caché para optimizar el rendimiento y el tiempo de respuesta. Puede configurar el nivel del servicio de caché para ajustar el equilibrio entre rendimiento y utilización del espacio.

<table>
 <tbody>
  <tr>
   <th>Estrategia de caché</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Ninguno</td>
   <td>No almacenar en caché los artefactos<br /> </td>
  </tr>
  <tr>
   <td>Conservadora</td>
   <td>Almacenar en caché solo los artefactos intermedios que se generan antes del procesamiento del formulario, como la plantilla que contiene fragmentos e imágenes en línea</td>
  </tr>
  <tr>
   <td>Agresiva</td>
   <td>Almacenar en caché el contenido HTML procesado<br /> Almacene en caché todos los artefactos almacenados en caché en el nivel conservador.<br /> <strong>Nota</strong>: Esta estrategia ofrece el mejor rendimiento, pero consume más memoria para almacenar los artefactos en caché.</td>
  </tr>
 </tbody>
</table>

Los formularios HTML5 realizan el almacenamiento en caché en memoria utilizando la estrategia de LRU. Si la estrategia de caché se establece en Ninguna, no se creará la caché, y los datos de caché existentes, si los hay, se borrarán. Además de la estrategia de almacenamiento en caché, también puede configurar el tamaño total de la caché en memoria, lo que puede resultar útil para establecer el límite máximo del tamaño de la caché y, si se sobrepasa, se utilizará el modo LRU para liberar recursos de caché.

>[!NOTE]
>
>La caché en memoria no se comparte entre nodos de clúster.

#### Servicio de configuración {#configuration-service}

El servicio de configuración permite ajustar los parámetros de configuración y la configuración de caché de los formularios HTML5.

Para actualizar esta configuración, vaya a la Consola de administración Felix CQ (disponible en https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr) y busque y seleccione Configuración de Mobile Forms.

Puede configurar el tamaño de la caché o deshabilitar la caché mediante el servicio de configuración. También puede habilitar la depuración con el parámetro Opciones de depuración. Encontrará más información sobre la depuración de formularios en [Depuración de formularios HTML5](/help/forms/using/debug.md).

### Componentes de tiempo de ejecución (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

El paquete Runtime contiene las bibliotecas del lado del cliente que se utilizan para procesar formularios HTML.

**Componentes importantes disponibles como parte del paquete Runtime:**

#### Motor de scripts {#scripting-engine}

La implementación de Adobe XFA admite dos tipos de lenguajes de scripts para permitir la ejecución de lógica definida por el usuario en formularios: JavaScript y FormCalc.

El motor de scripts de los formularios HTML se escribe en JavaScript para admitir la API de scripts XFA en ambos lenguajes.

En el momento del procesamiento, el script de FormCalc se traduce (y se almacena en caché) en JavaScript en el servidor de forma transparente para el usuario o el diseñador.

Este motor de scripts utiliza algunas funciones de ECMAScript5, como Object.defineProperty. El motor/biblioteca se entrega como una biblioteca de cliente de CQ con el nombre de categoría **xfaforms.profile**. También proporciona la **API de FormBridge** para permitir que los portales o las aplicaciones externas interactúen con el formulario. Con FormBridge, una aplicación externa puede ocultar mediante programación ciertos elementos, obtener o establecer sus valores o cambiar sus atributos.

Para obtener más información, consulte el artículo [Form Bridge](/help/forms/using/form-bridge-apis.md).

#### Motor de diseño {#layout-engine}

La presentación y el aspecto visual de los formularios HTML5 se basan en las funciones de SVG 1.1, jQuery, BackBone y CSS3. El aspecto inicial de un formulario se genera y se almacena en caché en el servidor. La modificación de ese diseño inicial y cualquier cambio adicional en el diseño del formulario se administran en el cliente. Para ello, el paquete Runtime contiene un motor de diseño escrito en JavaScript y basado en jQuery/Backbone. Este motor administra todo el comportamiento dinámico, como Añadir/Eliminar instancias repetibles o el diseño de objetos acumulables. Este motor de diseño procesa una página de formulario cada vez. Al principio, el usuario solo ve una página, y la barra de desplazamiento horizontal corresponde únicamente a la primera página. Sin embargo, cuando un usuario se desplaza hacia abajo, comienza a procesarse la siguiente página. Esta representación página por página reduce el tiempo necesario para procesar la primera página en un explorador y mejora el rendimiento percibido del formulario. Este motor/biblioteca es parte de una biblioteca de cliente de CQ con el nombre de categoría **xfaforms.profile**.

El motor de diseño también contiene un conjunto de widgets utilizados para capturar el valor de los campos de formulario de un usuario. Estos widgets están modelados como [widgets de la interfaz de usuario de jQuery](https://api.jqueryui.com/jQuery.widget/) que implementan ciertos contratos adicionales para funcionar sin problemas con el motor de diseño.

Para obtener más información sobre los widgets y los contratos correspondientes, consulte [Widgets personalizados para formularios HTML5](/help/forms/using/introduction-widgets.md).

#### Estilo {#styling}

El estilo asociado con los elementos de HTML se añade en línea o en función del bloque CSS integrado. Algunos estilos comunes que no dependen del formulario forman parte de la biblioteca de cliente de CQ con el nombre de categoría xfaforms.profile.

Además de las propiedades de estilo predeterminadas, cada elemento de formulario también contiene ciertas clases CSS basadas en el tipo de elemento, el nombre y otras propiedades. Estas clases permiten restaurar los elementos especificando su propio código CSS.

Para obtener más información sobre el estilo y las clases predeterminados, consulte [Introducción a los estilos](/help/forms/using/css-styles.md).

#### Script del lado del servidor y servicios web {#server-side-script-and-web-services}

Todos los scripts que marcados para ejecutarse en el servidor o para llamar a un servicio web (independientemente de dónde estén marcados para ejecutarse) se ejecutan siempre en el servidor.

El motor de scripts de cliente:

1. Realiza una llamada sincrónica al servidor que pasa el estado de formulario actual en forma de JSON.
1. Ejecuta el script o el servicio web en el servidor.
1. Genera un nuevo estado JSON.
1. Combina el nuevo estado JSON en el cliente cuando se devuelve la respuesta.

#### Paquetes de recursos de localización {#localization-resource-bundles}

Los formularios HTML5 admiten los idiomas italiano (it), español (es), portugués brasileño (pt_BR), chino simplificado (zh_CN), chino tradicional (solo soporte limitado) (zh_TW), coreano (ko_KR), inglés (en_US), francés (fr_FR), alemán (de_DE) y japonés (ja). En función de la configuración regional recibida en el encabezado de la solicitud, se envía el paquete de recursos correspondiente al cliente. Este paquete de recursos se agrega al JSP del perfil como una biblioteca de cliente de CQ con el nombre de categoría **xfaforms.I18N**. Puede anular la lógica de selección del paquete de configuración regional en el perfil.

### Componentes de Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

El paquete Sling incluye contenido relacionado con los perfiles y el procesador de perfiles.

#### Perfiles {#profiles}

Los perfiles son nodos de recursos de Sling que representan un formulario o una familia de formularios. En el nivel de CQ, estos perfiles son nodos JCR. Los nodos residen en la carpeta **/content** del repositorio JCR y pueden estar en cualquier subcarpeta de la carpeta **/content**.

#### Procesadores de perfiles {#profile-renderers}

El nodo Perfil tiene una propiedad **sling:resourceSuperType** con el valor **xfaforms/profile**. Esta propiedad envía internamente solicitudes al script de Sling para los nodos de perfil en la carpeta **/libs/xfaforms/profile**. Estos scripts son páginas JSP, las cuales son contenedores para recopilar los formularios HTML y los artefactos JS/CSS requeridos. Las páginas incluyen referencias a:

* **xfaforms.I18N.&lt;locale>**: esta biblioteca contiene datos localizados.
* **xfaforms.profile**: esta biblioteca contiene la implementación para el motor de diseño y los scripts XFA.

Estas bibliotecas están modeladas como bibliotecas de cliente de CQ que aprovechan las capacidades de concatenación, minificación y compresión automáticas de las bibliotecas JavaScript del marco de CQ.
Para obtener más información sobre las bibliotecas de cliente de CQ, consulte [Documentación la biblioteca de cliente de CQ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).

Como se ha descrito anteriormente, el procesador de perfiles JSP llama al servicio Forms a través de una inclusión sling. Este JSP también establece varias opciones de depuración en función de la configuración de administración o los parámetros de solicitud.

Los formularios HTML5 permiten a los desarrolladores crear un procesador de perfiles y perfiles para personalizar la apariencia de los formularios. Por ejemplo, los formularios HTML permiten a los desarrolladores integrar formularios en un panel o una sección &lt;div> de un portal HTML.
Para obtener más información sobre la creación de perfiles personalizados, consulte [Creación de un perfil personalizado](/help/forms/using/custom-profile.md).
