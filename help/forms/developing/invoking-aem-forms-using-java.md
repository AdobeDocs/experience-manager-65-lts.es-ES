---
title: Invocar AEM Forms mediante la API de Java
description: Utilice la API de Java de AEM Forms para el protocolo de transporte RMI para la invocación remota, el transporte de VM para la invocación local, SOAP para la invocación remota, autenticación diferente, como nombre de usuario y contraseña, y solicitudes de invocación sincrónicas y asincrónicas.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '5333'
ht-degree: 0%

---

# Invocar AEM Forms mediante la API de Java {#invoking-aem-forms-using-the-javaapi}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

AEM Forms se puede invocar mediante la API de Java de AEM Forms. Al utilizar la API de Java de AEM Forms, puede utilizar la API de invocación o las bibliotecas de cliente de Java. Las bibliotecas de cliente Java están disponibles para servicios como el servicio Rights Management. Estas API con establecimiento inflexible de tipos le permiten desarrollar aplicaciones Java que invocan AEM Forms.

La API de invocación son clases que se encuentran en el paquete `com.adobe.idp.dsc`. Con estas clases, se puede enviar una solicitud de invocación directamente a un servicio y controlar una respuesta de invocación que se devuelve. Utilice la API de invocación para invocar procesos de corta o larga duración creados con Workbench.

La forma recomendada de invocar un servicio mediante programación es utilizar una biblioteca de cliente Java que corresponda al servicio en lugar de la API de invocación. Por ejemplo, para invocar el servicio Encryption, utilice la biblioteca de cliente del servicio Encryption. Para realizar una operación del servicio Encryption, invoque un método que pertenezca al objeto de cliente del servicio Encryption. Puede cifrar un documento de PDF con una contraseña invocando el método `encryptPDFUsingPassword` del objeto `EncryptionServiceClient`.

La API de Java admite las siguientes funciones:

* Protocolo de transporte RMI para invocación remota
* Transporte de VM para invocación local
* SOAP para invocación remota
* Autenticación diferente, como nombre de usuario y contraseña
* Solicitudes de invocación sincrónicas y asincrónicas

[Incluir archivos de biblioteca Java de AEM Forms](#including-aem-forms-java-library-files)

[Invocar procesos de larga duración centrados en el ser humano](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocar AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Estableciendo propiedades de conexión](#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar un servicio mediante una biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocación de un proceso de corta duración mediante la API de invocación](#invoking-a-short-lived-process-using-the-invocation-api)

[Creación de una aplicación web Java que invoque un proceso de larga duración centrado en humanos](/help/forms/developing/invoking-human-centric-long-lived.md)

## Incluir archivos de biblioteca Java de AEM Forms {#including-aem-forms-java-library-files}

Para invocar mediante programación un servicio de AEM Forms mediante la API de Java, incluya los archivos de biblioteca necesarios (archivos JAR) en la ruta de clase del proyecto Java. Los archivos JAR que se incluyen en la ruta de clase de la aplicación cliente dependen de varios factores:

* El servicio AEM Forms que se va a invocar. Una aplicación cliente puede invocar uno o varios servicios.
* El modo en el que desea invocar un servicio de AEM Forms. Puede utilizar el modo EJB o SOAP. (Consulte [Establecimiento de propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo llave en mano) Inicie el servidor de AEM Forms con el comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar una IP de servidor para EJB

* Servidor de aplicaciones J2EE en el que está implementado AEM Forms.

### Archivos JAR específicos del servicio {#service-specific-jar-files}

En la tabla siguiente se enumeran los archivos JAR necesarios para invocar los servicios de AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Archivo</p></th>
   <th><p>Descripción</p></th>
   <th><p>Lugar de residencia</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Siempre debe incluirse en la ruta de clase de una aplicación cliente Java.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk//client-libs/&lt;servidor de aplicaciones&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de aplicaciones.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Assembler. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necesario para invocar la API del servicio de backup y restauración.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Forms con códigos de barras. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio ConvertPDF. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Distiller.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necesario para invocar el servicio DocConverter.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de Administración de documentos.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Encryption.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Forms.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de integración de datos de formulario.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate PDF.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Generate 3D PDF.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de trabajos. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Output.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Utilidades de PDF o Utilidades de XMP.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necesario para invocar el servicio de extensiones de Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Necesario para invocar el servicio de repositorio.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs\thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Necesario para invocar el servicio Rights Management.</p><p>Si AEM Forms está implementado en JBoss, incluya todos estos archivos. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p><p>Directorio lib específico de JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Signature.</p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necesario para invocar el servicio Administrador de tareas. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necesario para invocar el servicio Almacén de confianza. </p></td>
   <td><p>&lt;<i>directorio de instalación</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexión y archivos JAR de la aplicación J2EE {#connection-mode-and-j2ee-application-jar-files}

En la tabla siguiente se enumeran los archivos JAR que dependen del modo de conexión y del servidor de aplicaciones J2EE en el que AEM Forms está implementado.

<table>
 <thead>
  <tr>
   <th><p>Archivo</p> </th>
   <th><p>Descripción</p> </th>
   <th><p>Lugar de residencia</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>si se invoca AEM Forms con el modo SOAP, incluya estos archivos JAR.</p> </td>
   <td><p>&lt;<em>directorio de instalación</em>&gt;/sdk/client-libs/third-party</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>si AEM Forms está implementado en el servidor de aplicaciones JBoss, incluya este archivo JAR.</p> <p>El cargador de clases no encontrará las clases requeridas si jboss-client.jar y los archivos .jar a los que se hace referencia no están ubicados conjuntamente.</p> </td>
   <td><p>Directorio de biblioteca del cliente de JBoss</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>si AEM Forms está implementado en BEA WebLogic Server®, incluya este archivo JAR.</p> </td>
   <td><p>Directorio de biblioteca específico de WebLogic</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no es necesario incluir este archivo.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>si AEM Forms está implementado en el servidor de aplicaciones WebSphere, incluya estos archivos JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar es necesario para invocar el servicio web).</p> </li>
    </ul> </td>
   <td><p>Directorio de biblioteca específico de WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Si implementa la aplicación cliente en el mismo servidor de aplicaciones J2EE, no tiene que incluir estos archivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocación de escenarios {#invoking-scenarios}

La siguiente tabla especifica la invocación de escenarios y enumera los archivos JAR necesarios para invocar correctamente AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Servicios</p> </th>
   <th><p>Modo de invocación</p> </th>
   <th><p>Servidor de aplicaciones J2EE</p> </th>
   <th><p>Archivos JAR necesarios</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>servicio de Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servicio de Forms</p> <p>Servicio de extensiones de Acrobat Reader DC</p> <p>Servicio de firmas</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Actualización de archivos JAR {#upgrading-jar-files}

Si actualiza de LiveCycle a AEM Forms, se recomienda incluir los archivos JAR de AEM Forms en la ruta de clase del proyecto Java. Por ejemplo, si utiliza servicios como el servicio Rights Management, encontrará un problema de compatibilidad si no incluye archivos JAR de AEM Forms en la ruta de clase.

Suponiendo que está actualizando a AEM Forms. Para utilizar una aplicación Java que invoque el servicio Rights Management, incluya las versiones de AEM Forms de los siguientes archivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

[Pasar datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Estableciendo propiedades de conexión {#setting-connection-properties}

Las propiedades de conexión se establecen para invocar AEM Forms al utilizar la API de Java. Al establecer las propiedades de conexión, especifique si desea invocar los servicios de forma remota o local, así como el modo de conexión y los valores de autenticación. Se requieren valores de autenticación si la seguridad del servicio está habilitada. Sin embargo, si la seguridad del servicio está deshabilitada, no es necesario especificar los valores de autenticación.

El modo de conexión puede ser SOAP o EJB. El modo EJB utiliza el protocolo RMI/IIOP, y el rendimiento del modo EJB es mejor que el rendimiento del modo SOAP. El modo SOAP se utiliza para eliminar una dependencia del servidor de aplicaciones J2EE o cuando se encuentra un cortafuegos entre AEM Forms y la aplicación cliente. El modo SOAP utiliza el protocolo https como transporte subyacente y puede comunicarse entre los límites del cortafuegos. Si no existe ninguna dependencia del servidor de aplicaciones J2EE o un cortafuegos, se recomienda utilizar el modo EJB.

Para invocar correctamente un servicio de AEM Forms, establezca las siguientes propiedades de conexión:

* **DSC_DEFAULT_EJB_ENDPOINT:** Si está utilizando el modo de conexión EJB, este valor representa la URL del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost`. En función del servidor de aplicaciones J2EE en el que esté implementado AEM Forms, especifique uno de los siguientes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Si está usando el modo de conexión de SOAP, este valor representa el extremo al que se envía una solicitud de invocación. Para invocar AEM Forms de forma remota, especifique el nombre del servidor de aplicaciones J2EE en el que está implementado AEM Forms. Si la aplicación cliente se encuentra en el mismo servidor de aplicaciones J2EE, puede especificar `localhost` (por ejemplo, `http://localhost:8080`).

   * El valor de puerto `8080` es aplicable si la aplicación J2EE es JBoss. Si el servidor de aplicaciones J2EE es IBM® WebSphere®, utilice el puerto `9080`. Igualmente, si el servidor de aplicaciones J2EE es WebLogic, utilice el puerto `7001`. (Estos valores son valores de puerto predeterminados. Si cambia el valor del puerto, utilice el número de puerto aplicable).

* **DSC_TRANSPORT_PROTOCOL**: Si está usando el modo de conexión EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para este valor. Si está usando el modo de conexión de SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica el servidor de aplicaciones J2EE en el que AEM Forms está implementado. Los valores válidos son `JBoss`, `WebSphere`, `WebLogic`.

   * Si establece esta propiedad de conexión en `WebSphere`, el valor `java.naming.factory.initial` se establece en `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Si establece esta propiedad de conexión en `WebLogic`, el valor `java.naming.factory.initial` se establece en `weblogic.jndi.WLInitialContextFactory`.
   * Del mismo modo, si establece esta propiedad de conexión en `JBoss`, el valor `java.naming.factory.initial` se establece en `org.jnp.interfaces.NamingContextFactory`.
   * Puede establecer la propiedad `java.naming.factory.initial` en un valor que cumpla sus requisitos si no desea utilizar los valores predeterminados.

  >[!NOTE]
  >
  >En lugar de utilizar una cadena para establecer la propiedad de conexión `DSC_SERVER_TYPE`, puede utilizar un miembro estático de la clase `ServiceClientFactoryProperties`. Se pueden usar los siguientes valores: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica el nombre de usuario de los formularios AEM Forms. Para que un usuario invoque correctamente un servicio de AEM Forms, necesita la función Usuario de servicios. Un usuario también puede tener otra función que incluya el permiso Invocar servicio. De lo contrario, se produce una excepción cuando intentan invocar un servicio. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_CREDENTIAL_PASSWORD:** Especifica el valor de contraseña correspondiente. Si la seguridad del servicio está deshabilitada, no es necesario especificar esta propiedad de conexión.
* **DSC_REQUEST_TIMEOUT:** El límite de tiempo de espera de solicitud predeterminado para la solicitud de SOAP es de 1200000 milisegundos (20 minutos). En ocasiones, una solicitud puede requerir más tiempo para completar la operación. Por ejemplo, una solicitud de SOAP que recupera un gran conjunto de registros puede requerir un límite de tiempo de espera más largo. Puede usar `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar el límite de tiempo de espera de llamada de solicitud para las solicitudes de SOAP.

  **nota**: solo las invocaciones basadas en SOAP admiten la propiedad DSC_REQUEST_TIMEOUT.

Para establecer las propiedades de conexión, realice las siguientes tareas:

1. Crear un objeto `java.util.Properties` mediante su constructor.
1. Para establecer la propiedad de conexión `DSC_DEFAULT_EJB_ENDPOINT`, invoque el método `setProperty` del objeto `java.util.Properties` y pase los siguientes valores:

   * El valor de enumeración `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Valor de cadena que especifica la dirección URL del servidor de aplicaciones J2EE que aloja AEM Forms

   >[!NOTE]
   >
   >Si está usando el modo de conexión de SOAP, especifique el valor de enumeración `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` en lugar del valor de enumeración `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`.

1. Para establecer la propiedad de conexión `DSC_TRANSPORT_PROTOCOL`, invoque el método `setProperty` del objeto `java.util.Properties` y pase los siguientes valores:

   * El valor de enumeración `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * El valor de enumeración `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`

   >[!NOTE]
   >
   >Si está usando el modo de conexión de SOAP, especifique el valor de enumeración `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL` en lugar del valor de enumeración `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`.

1. Para establecer la propiedad de conexión `DSC_SERVER_TYPE`, invoque el método `setProperty` del objeto `java.util.Properties` y pase los siguientes valores:

   * El valor de enumeración `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Valor de cadena que especifica el servidor de aplicaciones J2EE que aloja AEM Forms (por ejemplo, si AEM Forms está implementado en JBoss, especifique `JBoss`).

      1. Para establecer la propiedad de conexión `DSC_CREDENTIAL_USERNAME`, invoque el método `setProperty` del objeto `java.util.Properties` y pase los siguientes valores:

   * El valor de enumeración `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Valor de cadena que especifica el nombre de usuario necesario para invocar AEM Forms

      1. Para establecer la propiedad de conexión `DSC_CREDENTIAL_PASSWORD`, invoque el método `setProperty` del objeto `java.util.Properties` y pase los siguientes valores:

   * El valor de enumeración `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Un valor de cadena que especifica el valor de contraseña correspondiente

**Estableciendo el modo de conexión de EJB para JBoss**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en JBoss y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Estableciendo el modo de conexión de EJB para WebLogic**

En el siguiente ejemplo de código Java se establecen las propiedades de conexión para invocar AEM Forms implementado en WebLogic y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Estableciendo el modo de conexión de EJB para WebSphere**

El siguiente ejemplo de código Java establece las propiedades de conexión para invocar AEM Forms implementado en WebSphere y utilizar el modo de conexión EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Estableciendo el modo de conexión de SOAP**

El siguiente ejemplo de código Java establece las propiedades de conexión en el modo SOAP para invocar AEM Forms implementado en JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Si selecciona el modo de conexión de SOAP, asegúrese de incluir archivos JAR adicionales en la ruta de clase de la aplicación cliente.

**Estableciendo propiedades de conexión cuando la seguridad del servicio está deshabilitada**

El siguiente ejemplo de código Java establece las propiedades de conexión necesarias para invocar AEM Forms implementado en el servidor de aplicaciones JBoss y cuando la seguridad del servicio está deshabilitada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos los tutoriales rápidos de Java asociados con la programación con AEM Forms muestran la configuración de conexión de EJB y SOAP.

**Estableciendo el modo de conexión de SOAP con límite de tiempo de espera de solicitud personalizado**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Usar un objeto de contexto para invocar AEM Forms**

Puede usar un objeto `com.adobe.idp.Context` para invocar un servicio de AEM Forms con un usuario autenticado (el objeto `com.adobe.idp.Context` representa un usuario autenticado). Al utilizar un objeto `com.adobe.idp.Context`, no es necesario establecer las propiedades `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`. Puede obtener un objeto `com.adobe.idp.Context` al autenticar usuarios mediante el método `authenticate` del objeto `AuthenticationManagerServiceClient`.

El método `authenticate` devuelve un objeto `AuthResult` que contiene los resultados de la autenticación. Puede crear un objeto `com.adobe.idp.Context` invocando su constructor. A continuación, invoque el método `initPrincipal` del objeto `com.adobe.idp.Context` y pase el objeto `AuthResult`, como se muestra en el código siguiente:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

En lugar de establecer las propiedades `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`, puede invocar el método `setContext` del objeto `ServiceClientFactory` y pasar el objeto `com.adobe.idp.Context`. Cuando utilice un usuario de formularios AEM Forms para invocar un servicio, asegúrese de que tiene la función denominada `Services User` necesaria para invocar un servicio de AEM Forms.

En el ejemplo de código siguiente se muestra cómo utilizar un objeto `com.adobe.idp.Context` en la configuración de conexión utilizada para crear un objeto `EncryptionServiceClient`.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Para obtener información detallada sobre cómo autenticar a un usuario, consulte [Autenticar usuarios](/help/forms/developing/users.md#authenticating-users).

### Invocación de escenarios {#invoking_scenarios-1}

Los siguientes escenarios de invocación se analizan en esta sección:

* Una aplicación cliente que se ejecuta en su propia máquina virtual Java (JVM) invoca una instancia de AEM Forms independiente.
* Una aplicación cliente que se ejecuta en su propia JVM invoca instancias de AEM Forms agrupadas.

### Aplicación cliente que invoca una instancia de AEM Forms independiente {#client-application-invoking-a-stand-alone-aem-forms-instance}

El diagrama siguiente muestra una aplicación cliente ejecutándose en su propia JVM e invocando una instancia de AEM Forms independiente.

En esta situación, una aplicación cliente se está ejecutando en su propia JVM e invoca los servicios de AEM Forms.

>[!NOTE]
>
>Este escenario es el escenario de invocación en el que se basan todos los inicios rápidos.

### Aplicación cliente que invoca instancias de AEM Forms agrupadas {#client-application-invoking-clustered-aem-forms-instances}

En el diagrama siguiente se muestra una aplicación cliente ejecutándose en su propia JVM e invocando instancias de AEM Forms en un clúster.

Este escenario es similar a una aplicación cliente que invoca una instancia de AEM Forms independiente. Sin embargo, la dirección URL del proveedor es diferente. Si una aplicación cliente desea conectarse a un servidor de aplicaciones J2EE específico, la aplicación debe cambiar la URL para hacer referencia al servidor de aplicaciones J2EE específico.

No se recomienda hacer referencia a un servidor de aplicaciones J2EE específico porque la conexión entre la aplicación cliente y AEM Forms finaliza si el servidor de aplicaciones se detiene. Se recomienda que la dirección URL del proveedor haga referencia a un administrador JNDI de nivel de celda, en lugar de a un servidor de aplicaciones J2EE específico.

Las aplicaciones cliente que utilizan el modo de conexión de SOAP pueden utilizar el puerto del equilibrador de carga HTTP para el clúster. Las aplicaciones cliente que utilizan el modo de conexión EJB pueden conectarse al puerto EJB de un servidor de aplicaciones J2EE específico. Esta acción administra el equilibrio de carga entre los nodos del clúster.

**WebSphere**

En el ejemplo siguiente se muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms implementado en WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**Lógica web**

El ejemplo siguiente muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se implementa en WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

El ejemplo siguiente muestra el contenido de un archivo jndi.properties que se utiliza para conectarse a AEM Forms que se despliega en JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte al administrador para determinar el nombre y el número de puerto del servidor de aplicaciones J2EE.

**Consulte también**

[Inclusión AEM Forms archivos de biblioteca Java](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Transmisión de datos a servicios de AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Llamada a un servicio mediante un biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Transmisión de datos a servicios de AEM Forms mediante la API de Java {#passing-data-to-aem-forms-services-using-the-java-api}

Las operaciones del servicio AEM Forms suelen consumir o producir documentos de PDF. Al invocar un servicio, a veces es necesario pasar un documento de PDF (u otros tipos de documento como datos XML) al servicio. Del mismo modo, a veces es necesario gestionar un documento de PDF que se devuelve desde el servicio. La clase Java que le permite pasar datos desde y hacia los servicios de AEM Forms es `com.adobe.idp.Document`.

Los servicios de AEM Forms no aceptan un documento de PDF como otros tipos de datos, como un objeto `java.io.InputStream` o una matriz de bytes. Un objeto `com.adobe.idp.Document` también se puede usar para pasar otros tipos de datos, como datos XML, a los servicios.

Un objeto `com.adobe.idp.Document` es un tipo serializable de Java, por lo que se puede pasar a través de una llamada RMI. El lado receptor puede estar ubicado (el mismo host, el mismo cargador de clase), ser local (el mismo host, un cargador de clase diferente) o remoto (un host diferente). La transferencia del contenido del documento está optimizada para cada caso. Por ejemplo, si el remitente y el destinatario se encuentran en el mismo host, el contenido se pasa a través de un sistema de archivos local. (En algunos casos, los documentos se pueden pasar en la memoria).

Según el tamaño del objeto `com.adobe.idp.Document`, los datos se transportan dentro del objeto `com.adobe.idp.Document` o se almacenan en el sistema de archivos del servidor. Cualquier recurso de almacenamiento temporal ocupado por el objeto `com.adobe.idp.Document` se quitará automáticamente al eliminar `com.adobe.idp.Document`. (Consulte [Disponer objetos de documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A veces es necesario conocer el tipo de contenido de un objeto `com.adobe.idp.Document` antes de poder pasarlo a un servicio. Por ejemplo, si una operación requiere un tipo de contenido específico, como `application/pdf`, se recomienda determinar el tipo de contenido. (Consulte [Determinar el tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

El objeto `com.adobe.idp.Document` intenta determinar el tipo de contenido mediante los datos proporcionados. Si no se puede recuperar el tipo de contenido de los datos suministrados (por ejemplo, cuando los datos se suministraron como una matriz de bytes), establezca el tipo de contenido. Para establecer el tipo de contenido, invoque el método `setContentType` del objeto `com.adobe.idp.Document`. (Consulte [Determinar el tipo de contenido de un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Si los archivos auxiliares residen en el mismo sistema de archivos, la creación de un objeto `com.adobe.idp.Document` es más rápida. Si los archivos auxiliares residen en sistemas de archivos remotos, se debe realizar una operación de copia, lo que afecta al rendimiento.

Una aplicación puede contener `com.adobe.idp.Document` y `org.w3c.dom.Document` tipos de datos. Sin embargo, asegúrese de que califica completamente el tipo de datos `org.w3c.dom.Document`. Para obtener información sobre la conversión de un objeto `org.w3c.dom.Document` en un objeto `com.adobe.idp.Document`, consulte [Inicio rápido (modo EJB): rellenar previamente Forms con diseños flexibles mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Para evitar una fuga de memoria en WebLogic mientras se utiliza un objeto `com.adobe.idp.Document`, lea la información del documento en fragmentos de 2048 bytes o menos. Por ejemplo, el siguiente código lee la información del documento en fragmentos de 2048 bytes:

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creación de documentos {#creating-documents}

Cree un objeto `com.adobe.idp.Document` antes de invocar una operación de servicio que requiera un documento de PDF (u otros tipos de documento) como valor de entrada. La clase `com.adobe.idp.Document` proporciona constructores que permiten crear un documento a partir de los siguientes tipos de contenido:

* Una matriz de bytes
* Un objeto `com.adobe.idp.Document` existente
* Un objeto `java.io.File`
* Un objeto `java.io.InputStream`
* Un objeto `java.net.URL`

#### Creación de un documento basado en una matriz de bytes {#creating-a-document-based-on-a-byte-array}

En el ejemplo de código siguiente se crea un objeto `com.adobe.idp.Document` basado en una matriz de bytes.

**Creando un objeto de documento basado en una matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creación de un documento basado en otro documento {#creating-a-document-based-on-another-document}

En el ejemplo de código siguiente se crea un objeto `com.adobe.idp.Document` basado en otro objeto `com.adobe.idp.Document`.

**Creando un objeto de documento basado en otro documento**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Creación de un documento basado en un archivo {#creating-a-document-based-on-a-file}

En el ejemplo de código siguiente se crea un objeto `com.adobe.idp.Document` basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra en la raíz del disco duro C. Este constructor intenta establecer el tipo de contenido MIME del objeto `com.adobe.idp.Document` mediante la extensión de nombre de archivo.

El constructor `com.adobe.idp.Document` que acepta un objeto `java.io.File` también acepta un parámetro Boolean. Al establecer este parámetro en `true`, el objeto `com.adobe.idp.Document` elimina el archivo. Esta acción significa que no tiene que quitar el archivo después de pasarlo al constructor `com.adobe.idp.Document`.

Establecer este parámetro en `false` significa que usted conserva la propiedad de este archivo. Establecer este parámetro en `true` es más eficaz. El motivo es que el objeto `com.adobe.idp.Document` puede mover el archivo directamente al área administrada local en lugar de copiarlo (lo que es más lento).

**Creando un objeto de documento basado en un archivo PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Crear un documento basado en un objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

El siguiente ejemplo de código Java crea un objeto `com.adobe.idp.Document` basado en un objeto `java.io.InputStream`.

**Creando un documento basado en un objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creación de un documento basado en contenido accesible desde una dirección URL {#creating-a-document-based-on-content-accessible-from-an-url}

El siguiente ejemplo de código Java crea un objeto `com.adobe.idp.Document` basado en un archivo PDF denominado *map.pdf*. Este archivo se encuentra dentro de una aplicación web denominada `WebApp` que se está ejecutando en `localhost`. Este constructor intenta establecer el tipo de contenido MIME del objeto `com.adobe.idp.Document` mediante el tipo de contenido devuelto con el protocolo URL.

La dirección URL proporcionada al objeto `com.adobe.idp.Document` siempre se lee en el lado donde se crea el objeto `com.adobe.idp.Document` original, como se muestra en este ejemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

El archivo c:/temp/input.pdf debe estar ubicado en el equipo cliente (no en el equipo servidor). El equipo cliente es donde se lee el URL y donde se crea el `com.adobe.idp.Document` objeto.

**Creación de una documento basada en contenido accesible desde una URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestión de documentos devueltos {#handling-returned-documents}

Las operaciones de servicio que devuelven una documento PDF (u otros tipos de datos, como datos XML) como un valor de salida, devuelven un `com.adobe.idp.Document` objeto. Una vez recibido un `com.adobe.idp.Document` objeto, puede convertir a los formatos siguientes:

* Un `java.io.File` objeto
* Un `java.io.InputStream` objeto
* Una matriz de bytes

La siguiente línea de código convierte un objeto `com.adobe.idp.Document` en un objeto `java.io.InputStream`. Supongamos que `myPDFDocument` representa un objeto `com.adobe.idp.Document`:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Del mismo modo, puede copiar el contenido de un(a) `com.adobe.idp.Document` en un archivo local realizando las siguientes tareas:

1. Crear un objeto `java.io.File`.
1. Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` y pase el objeto `java.io.File`.

En el ejemplo de código siguiente se copia el contenido de un objeto `com.adobe.idp.Document` en un archivo denominado *AnotherMap.pdf*.

**Copiando el contenido de un objeto de documento en un archivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinación del tipo de contenido de un documento {#determining-the-content-type-of-a-document}

Determine el tipo MIME de un objeto `com.adobe.idp.Document` invocando el método `getContentType` del objeto `com.adobe.idp.Document`. Este método devuelve un valor de cadena que especifica el tipo de contenido del objeto `com.adobe.idp.Document`. En la tabla siguiente se describen los diferentes tipos de contenido que devuelve AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Tipo MIME</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>documento de PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>Paquete de datos XML (XDP), que se utiliza para formularios XFA (arquitectura de Forms XML) exportados</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, archivos adjuntos u otros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de datos Forms (FDF), que se utiliza para formularios Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>Formato de datos XML Forms (XFDF), que se utiliza para formularios Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Formato de datos enriquecido y XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Formato de datos genérico</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Tipo MIME no especificado</p></td>
  </tr>
 </tbody>
</table>

En el ejemplo de código siguiente se determina el tipo de contenido de un objeto `com.adobe.idp.Document`.

**Determinar el tipo de contenido de un objeto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Estableciendo propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties)

### Desechar objetos de documento {#disposing-document-objects}

Cuando ya no necesite un objeto `Document`, es recomendable que lo elimine invocando su método `dispose`. Cada objeto `Document` consume un descriptor de archivo y hasta 75 MB de espacio en RAM en la plataforma host de la aplicación. Si un objeto `Document` no está desechado, el proceso de recopilación del garaje Java lo desecha. Sin embargo, si lo elimina antes con el método `dispose`, puede liberar la memoria ocupada por el objeto `Document`.

**Consulte también**

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocar un servicio mediante una biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocar un servicio mediante una biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

Las operaciones del servicio AEM Forms se pueden invocar mediante la API con establecimiento inflexible de tipos de un servicio, que se conoce como biblioteca de cliente Java. Una *biblioteca de cliente Java* es un conjunto de clases concretas que proporcionan acceso a los servicios implementados en el contenedor de servicios. Cree una instancia de un objeto Java que represente el servicio que se va a invocar en lugar de crear un objeto `InvocationRequest` mediante la API de invocación. La API de invocación se utiliza para invocar procesos, como procesos de larga duración, creados en Workbench. (Consulte [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para realizar una operación de servicio, invoque un método que pertenezca al objeto Java. Una biblioteca de cliente Java contiene métodos que generalmente se asignan de uno a uno con operaciones de servicio. Cuando utilice una biblioteca de cliente Java, establezca las propiedades de conexión necesarias. (Consulte [Establecimiento de propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)

Después de establecer las propiedades de conexión, cree un objeto `ServiceClientFactory` que se use para crear una instancia de un objeto Java que le permita invocar un servicio. Cada servicio que tiene una biblioteca de cliente Java tiene un objeto de cliente correspondiente. Por ejemplo, para invocar el servicio Repositorio, cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`. El objeto `ServiceClientFactory` es responsable de mantener la configuración de conexión necesaria para invocar los servicios de AEM Forms.

Aunque la obtención de `ServiceClientFactory` suele ser rápida, se requiere cierta sobrecarga cuando se utiliza la fábrica por primera vez. Este objeto está optimizado para su reutilización y, por lo tanto, cuando sea posible, utilice el mismo objeto `ServiceClientFactory` cuando esté creando varios objetos de cliente Java. Es decir, no cree un objeto `ServiceClientFactory` independiente para cada objeto de biblioteca de cliente que cree.

Hay una configuración del Administrador de usuarios que controla la duración de la aserción de SAML que se encuentra dentro del objeto `com.adobe.idp.Context` que afecta al objeto `ServiceClientFactory`. Esta opción controla todas las duraciones del contexto de autenticación a través de AEM Forms, incluidas todas las invocaciones realizadas mediante la API de Java. De manera predeterminada, el período de tiempo en el que se puede usar un objeto `ServiceCleintFactory` es de dos horas.

>[!NOTE]
>
>Para explicar cómo invocar un servicio mediante la API de Java, se invoca la operación `writeResource` del servicio de repositorio. Esta operación coloca un nuevo recurso en el repositorio.

Puede invocar el servicio de repositorio utilizando un biblioteca de cliente Java y realizando los pasos siguientes:

1. Incluya los archivos JAR del cliente, como adobe-repositorio-client.jar, en la ruta de clase del proyecto Java. Para obtener información sobre la ubicación de estos archivos, consulte [Incluidos AEM Forms archivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) de biblioteca Java.
1. Establezca las propiedades de conexión necesarias para invocar un servicio.
1. Cree un objeto `ServiceClientFactory` invocando el método `createInstance` estático del objeto `ServiceClientFactory` y pasando el objeto `java.util.Properties` que contiene las propiedades de conexión.
1. Cree un objeto `ResourceRepositoryClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`. Utilice el objeto para invocar operaciones de `ResourceRepositoryClient` servicio de repositorio.
1. Crear un `RepositoryInfomodelFactoryBean` objeto utilizando su constructor y pase `null`. Este objeto permite crear un `Resource` objeto que represente el contenido que se añade al repositorio.
1. Crear un `Resource` objeto invocando el `RepositoryInfomodelFactoryBean` método del `newImage` objeto y pasando los siguientes valores:

   * Un valor de ID único especificando `new Id()`.
   * Un valor UUID único especificando `new Lid()`.
   * Nombre del recurso. Puede especificar el nombre del archivo XDP.

   Convertir el valor devuelto en `Resource`.

1. Cree un objeto `ResourceContent` invocando el método `newImage` del objeto `RepositoryInfomodelFactoryBean` y convirtiendo el valor devuelto en `ResourceContent`. Este objeto representa el contenido que se agrega al repositorio.
1. Cree un objeto `com.adobe.idp.Document` pasando un objeto `java.io.FileInputStream` que almacene el archivo XDP que desea agregar al repositorio. (Vea [Crear un documento basado en un objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Agregue el contenido del objeto `com.adobe.idp.Document` al objeto `ResourceContent` invocando el método `setDataDocument` del objeto `ResourceContent`. Pase el objeto `com.adobe.idp.Document`.
1. Establezca el tipo MIME del archivo XDP que se agregará al repositorio invocando el método `setMimeType` del objeto `ResourceContent` y pasando `application/vnd.adobe.xdp+xml`.
1. Agregue el contenido del objeto `ResourceContent` al objeto `Resource` invocando el método `setContent` del objeto `Resource` y pasando el objeto `ResourceContent`.
1. Agregue una descripción del recurso invocando el método `setDescription` del objeto `Resource` y pasando un valor de cadena que represente una descripción del recurso.
1. Agregue el diseño de formulario al repositorio invocando el método `writeResource` del objeto `ResourceRepositoryClient` y pasando los siguientes valores:

   * Valor de cadena que especifica la ruta de acceso a la colección de recursos que contiene el nuevo recurso
   * El objeto `Resource` que se creó

**Consulte también**

[Inicio rápido (modo EJB): Escritura de un recurso mediante la API de Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocar AEM Forms mediante la API de Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Invocación de un proceso de corta duración mediante la API de invocación {#invoking-a-short-lived-process-using-the-invocation-api}

Puede invocar un proceso de corta duración mediante la API de invocación de Java. Cuando invoca un proceso de corta duración mediante la API de invocación, pasa los valores de parámetro necesarios mediante un objeto `java.util.HashMap`. Para que cada parámetro pase a un servicio, invoque el método `put` del objeto `java.util.HashMap` y especifique el par nombre-valor que requiere el servicio para realizar la operación especificada. Especifique el nombre exacto de los parámetros que pertenecen al proceso de corta duración.

>[!NOTE]
>
>Para obtener información acerca de cómo invocar un proceso de larga duración, vea [Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discusión aquí trata sobre el uso de la API de invocación para invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Invocar el proceso de corta duración MyApplication/EncryptDocument mediante la API de invocación de Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Invocar el proceso de corta duración `MyApplication/EncryptDocument` mediante la API de invocación de Java:

1. Incluya archivos JAR de cliente, como adobe-livecycle-client.jar, en la ruta de clase del proyecto Java. (Consulte [Incluyendo archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Establecimiento de propiedades de conexión](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Cree un objeto `ServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`. Un objeto `ServiceClient` le permite invocar una operación de servicio. Administra tareas como localizar, enviar y enrutar solicitudes de invocación.
1. Crear un objeto `java.util.HashMap` mediante su constructor.
1. Invoque el método `put` del objeto `java.util.HashMap` para que cada parámetro de entrada pase al proceso de larga duración. Dado que el proceso de corta duración `MyApplication/EncryptDocument` requiere un parámetro de entrada de tipo `Document`, sólo tiene que invocar el método `put` una vez, como se muestra en el ejemplo siguiente.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Cree un objeto `InvocationRequest` invocando el método `createInvocationRequest` del objeto `ServiceClientFactory` y pasando los siguientes valores:

   * Un valor de cadena que especifica el nombre del proceso de larga duración que se va a invocar. Para invocar el proceso `MyApplication/EncryptDocument`, especifique `MyApplication/EncryptDocument`.
   * Valor de cadena que representa el nombre de la operación de proceso. Normalmente, el nombre de una operación de proceso de corta duración es `invoke`.
   * El objeto `java.util.HashMap` que contiene los valores de parámetro que requiere la operación del servicio.
   * Un valor booleano que especifica `true`, que crea una solicitud sincrónica (este valor es aplicable para invocar un proceso de corta duración).

1. Envíe la solicitud de invocación al servicio invocando el método `invoke` del objeto `ServiceClient` y pasando el objeto `InvocationRequest`. El método `invoke` devuelve un objeto `InvocationReponse`.

   >[!NOTE]
   >
   >Se puede invocar un proceso de larga duración pasando el valor `false` como el cuarto parámetro del método `createInvocationRequest`. Al pasar el valor `false`*se crea una solicitud asincrónica.*

1. Recupere el valor devuelto del proceso invocando el método `getOutputParameter` del objeto `InvocationReponse` y pasando un valor de cadena que especifica el nombre del parámetro de salida. En este caso, especifique `outDoc` ( `outDoc` es el nombre del parámetro de salida para el proceso `MyApplication/EncryptDocument`). Convierta el valor devuelto en `Document`, como se muestra en el ejemplo siguiente.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Cree un objeto `java.io.File` y asegúrese de que la extensión del archivo sea .pdf.
1. Invoque el método `copyToFile` del objeto `com.adobe.idp.Document` para copiar el contenido del objeto `com.adobe.idp.Document` en el archivo. Asegúrese de utilizar el objeto `com.adobe.idp.Document` devuelto por el método `getOutputParameter`.

**Consulte también**

[Inicio rápido: invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocar procesos de larga duración centrados en el ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Incluir archivos de biblioteca Java de AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
