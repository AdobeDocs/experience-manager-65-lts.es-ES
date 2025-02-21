---
title: Proxy de servicio de formularios HTML5
description: El proxy de servicio de formularios HTML5 es una configuración para registrar un proxy para el servicio de envío. Para configurar el proxy de servicio, especifique la URL del servicio de envío mediante el parámetro de solicitud submissionServiceProxy.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 100%

---

# Proxy de servicio de formularios HTML5{#html-forms-service-proxy}

El proxy de servicio de formularios HTML5 es una configuración para registrar un proxy para el servicio de envío. Para configurar el proxy de servicio, especifique la URL del servicio de envío mediante el parámetro de solicitud *submissionServiceProxy*.

## Ventajas del proxy de servicio {#benefits-of-service-proxy-br}

El proxy de servicio elimina lo siguiente:

* El flujo de trabajo de formularios HTML5 requiere la apertura del servicio de envío “/content/xfaforms/submission/default” para los usuarios de formularios HTML5. Expone servidores de AEM a una audiencia no deseada más amplia.
* La URL del servicio está incrustada en el modelo de tiempo de ejecución del formulario. No es posible cambiar la ruta de la URL del servicio.
* El envío es un proceso de dos pasos. Para enviar los datos del formulario, el envío requiere al menos dos recorridos para el servidor. Por lo tanto, aumenta la carga en el servidor.
* Los formularios HTML5 envían datos en la solicitud POST en lugar de en la solicitud PDF. Para el flujo de trabajo que incluye formularios PDF y HTML5, se requieren dos métodos diferentes de procesamiento de los envíos.

### Topologías {#topologies-br}

Los formularios HTML5 pueden utilizar las siguientes topologías para conectarse a los servidores de AEM.

* Topología en la que los formularios de AEM Server o HTML5 envían datos mediante POST al servidor.
* Topología en la que el servidor proxy envía datos de POST al servidor.

![Topologías de proxy de servicio de formularios HTML5](assets/topology.png)

Topologías de proxy de servicio de formularios HTML5

Los formularios HTML5 se conectan a los servidores de AEM para ejecutar scripts, servicios web y envíos del lado del servidor. El tiempo de ejecución XFA de los formularios HTML5 utiliza llamadas Ajax en el punto final “/bin/xfaforms/submitaction” con varios parámetros para conectarse a los servidores de AEM. Los formularios HTML5 conectan servidores de AEM para realizar las siguientes operaciones:

#### Ejecutar scripts y servicios web del lado del servidor {#execute-server-sided-scripts-and-web-services}

Los scripts marcados para ejecutarse en el servidor se conocen como scripts del lado del servidor. En la siguiente tabla se enumeran todos los parámetros utilizados en scripts del lado del servidor y servicios web.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>Activity contiene los eventos que configuran el activador de la solicitud. Como clic, salida o cambio</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contiene la expresión SOM del objeto donde se ejecutan los eventos.</p> </td>
  </tr>
  <tr>
   <td><p>Template</p> </td>
   <td><p>Template contiene la plantilla utilizada para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot contiene el directorio raíz de la plantilla utilizado para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>Data contiene bytes de datos utilizados para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom contiene el DOM del formulario HTML5 en formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>packet</p> </td>
   <td><p>packet se especifica como formulario.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contiene el directorio de depuración utilizado para procesar el formulario.</p> </td>
  </tr>
 </tbody>
</table>

#### Enviar datos {#submit-data}

Al hacer clic en el botón Enviar, los formularios HTML5 envían datos al servidor. En la siguiente tabla se enumeran todos los parámetros que envían los formularios HTML5 al servidor.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parámetro</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Template</p> </td>
   <td><p>Plantilla utilizada para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>directorio raíz de plantilla que se utiliza para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>Datos</p> </td>
   <td><p>bytes de datos utilizados para procesar el formulario.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM del formulario HTML5 en formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>Dirección URL donde se publican los datos XML.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>Directorio de depuración utilizado para procesar el formulario.</p> </td>
  </tr>
 </tbody>
</table>

#### ¿Cómo funciona el proxy de envío? {#how-nbsp-the-nbsp-submit-proxy-works}

El proxy del servicio de envío actúa como un paso a través si submiturl no está presente en el parámetro de la solicitud. Actúa como una transmisión. Envía la solicitud al punto final /bin/xfaforms/submitaction y envía la respuesta al tiempo de ejecución de XFA.

El proxy del servicio de envío selecciona una topología si el envío está presente en el parámetro de solicitud.

* Si los servidores de AEM publican los datos, el servicio proxy actuará como un paso a través. Envía la solicitud al punto final /bin/xfaforms/submitaction y envía la respuesta al tiempo de ejecución de XFA.
* Si el proxy publica los datos, el servicio proxy pasa todos los parámetros excepto submitUrl al punto final */bin/xfaforms/submitaction* y recibe bytes xml en el flujo de respuesta. A continuación, el servicio proxy envía los bytes xml de datos a submitUrl para su procesamiento.

* Antes de enviar datos (petición POST) a un servidor, los formularios HTML5 comprueban la conectividad y disponibilidad del servidor. Para comprobar la conectividad y la disponibilidad, los formularios HTML envían una solicitud de encabezado vacía al servidor. Si el servidor está disponible, el formulario HTML5 enviará datos (petición POST) al servidor. Si el servidor no está disponible, aparecerá un mensaje de error, *No se pudo conectar al servidor*. La detección avanzada evita que los usuarios tengan que rellenar el formulario. El servlet proxy administra la solicitud del encabezado y no emite excepciones.
