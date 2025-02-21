---
title: Contenedor de servicio
description: Servicios de AEM Forms en el contenedor de servicios
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 2%

---

# Contenedor de servicio {#service-container}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Los servicios de AEM Forms en el contenedor de servicios (incluidos los servicios estándar como el servicio Encryption y los procesos de larga y corta duración) se pueden invocar mediante varios proveedores, como un proveedor EJB. Un proveedor EJB permite invocar los servicios de AEM Forms a través de RMI/IIOP. Un proveedor de servicios web expone servicios como servicios web (generación de WSDL) mediante estándares como SOAP/HTTP y SOAP/JMS.

En la tabla siguiente se describen las diferentes formas en que se puede invocar mediante programación los servicios de AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Método de invocación</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integración remota</p></td>
   <td><p>La integración remota permite a los clientes de Flex invocar operaciones de servicio. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Invocación de AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting</a>).</p></td>
  </tr>
  <tr>
   <td><p>API de Java</p></td>
   <td><p>Una API de Java puede invocar un servicio de AEM Forms. La API de Java está organizada en bibliotecas de cliente y la API de invocación de Java. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Invocar AEM Forms mediante la API de Java</a>).</p></td>
  </tr>
  <tr>
   <td><p>Servicios web</p></td>
   <td><p>AEM Forms admite estándares de servicios web como SOAP/HTTP. Un servicio se puede exponer como un servicio web, con el WSDL cumpliendo con los estándares de servicio web definidos por W3C.</p><p>Se puede invocar un servicio desde cualquier pila de servicios web, incluidos .NET Framework y Sun™ Web Services SDK. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Invocar AEM Forms mediante servicios web</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Solicitudes REST</p></td>
   <td><p>AEM Forms admite solicitudes REST. Se puede invocar un servicio directamente desde una página de HTML. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Invocación de AEM Forms mediante solicitudes REST</a>).</p></td>
  </tr>
 </tbody>
</table>

La siguiente ilustración proporciona una representación visual de las diferentes formas en que se pueden invocar los servicios de AEM Forms mediante programación.

>[!NOTE]
>
>Además de utilizar AEM Forms SDK para crear aplicaciones cliente que puedan invocar servicios de AEM Forms, también puede crear componentes que se pueden implementar en el contenedor de servicios. Por ejemplo, puede crear un componente Bank que contenga tipos de datos personalizados que se puedan utilizar en procesos. Es decir, puede crear un tipo de datos como `com.adobe.idp.BankAccount`. A continuación, puede crear `com.adobe.idp.BankAccount` instancias en las aplicaciones cliente.

El contenedor de servicio proporciona las siguientes funciones:

* Permite que los servicios de AEM Forms se invoquen mediante diferentes métodos. Puede configurar un servicio estableciendo puntos finales para que se pueda invocar mediante todos los métodos: Remoting, la API de Java, los servicios web y REST. (Consulte [Administrar puntos de conexión mediante programación](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Convierte un mensaje en un formato normalizado denominado solicitud de invocación. Se envía una solicitud de invocación desde una aplicación cliente (u otro servicio) a un servicio en el contenedor de servicios. Una solicitud de invocación contiene información como el nombre del servicio que se va a invocar y los valores de datos necesarios para realizar la operación. Muchos servicios requieren un documento para realizar una operación. Por lo tanto, una solicitud de invocación suele contener un documento, que puede ser datos de PDF, datos XDP, datos XML, etc.
* Enruta las solicitudes de invocación a los servicios adecuados (el nombre del servicio que se va a invocar forma parte de la solicitud de invocación).
* Realiza tareas como determinar si el llamador tiene permiso para invocar la operación de servicio especificada. La solicitud de invocación debe contener un nombre de usuario y una contraseña de formularios AEM válidos.

  Existen diferentes maneras de enviar una solicitud de invocación a un servicio. Además, hay diferentes formas de enviar los valores de entrada necesarios al servicio. Por ejemplo, supongamos que utiliza la API de Java para invocar un servicio que requiere un documento de PDF. El método Java correspondiente contiene un parámetro que acepta un documento de PDF. En este caso, el tipo de datos del parámetro es `com.adobe.idp.Document`. (Consulte [Pasar datos a servicios de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

  Si invoca un servicio mediante carpetas vigiladas, se envía una solicitud de invocación al colocar un archivo en una carpeta vigilada configurada. Si invoca un servicio mediante correo electrónico, se envía una solicitud de invocación a un servicio cuando un mensaje de correo electrónico llega a una bandeja de entrada configurada.

  El contenedor de servicio devuelve una respuesta de invocación una vez realizada la operación. Una respuesta de invocación contiene información como los resultados de la operación. Por ejemplo, si la operación modifica un documento de PDF, la respuesta de invocación contiene el documento de PDF modificado. Si la operación no se realizó correctamente, la respuesta de invocación contiene un mensaje de error.

  Una respuesta de invocación se puede recuperar del mismo modo en que se envía una solicitud de invocación. Es decir, si la solicitud de invocación se envía mediante la API de Java, se puede recuperar una respuesta de invocación mediante la API de Java. Supongamos, por ejemplo, que una operación modifica un documento de PDF. Puede recuperar el documento de PDF modificado obteniendo el valor devuelto del método Java que invocó el servicio.

  Cuando se invoca un proceso de larga duración, una respuesta de invocación contiene un valor de identificador asociado a la solicitud de invocación. Con este valor de identificador, puede comprobar el estado del proceso más adelante. Por ejemplo, considere el servicio de larga duración de MortgageLoan. Con el valor del identificador, puede comprobar si el proceso se ha completado correctamente. (Consulte [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  En el diagrama siguiente se muestra una aplicación cliente (que utiliza la API de Java) que invoca un servicio.

  Cuando una aplicación cliente invoca un servicio, se producen tres eventos:

   1. Una aplicación cliente envía una solicitud de invocación a un servicio.
   1. El servicio realiza la operación especificada en la solicitud de invocación.
   1. El contenedor de servicio devuelve una respuesta de invocación a la aplicación cliente.

**Consulte también**

[Explicar los procesos de AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Invocar AEM Forms mediante (obsoleto para formularios AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Invocar AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Invocar AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocar AEM Forms mediante solicitudes REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
