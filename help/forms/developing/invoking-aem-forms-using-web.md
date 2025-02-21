---
title: Invocar AEM Forms mediante servicios web
description: Invocar procesos de AEM Forms mediante servicios web con compatibilidad total con la generación de WSDL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '9814'
ht-degree: 0%

---

# Invocar AEM Forms mediante servicios web {#invoking-aem-forms-using-web-services}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

La mayoría de los servicios de AEM Forms del contenedor de servicios se configuran para exponer un servicio web, con compatibilidad total con la generación del lenguaje de definición de servicios web (WSDL). Es decir, puede crear objetos proxy que consuman la pila nativa de SOAP de un servicio de AEM Forms. Como resultado, los servicios de AEM Forms pueden intercambiar y procesar los siguientes mensajes de SOAP:

* **Solicitud SOAP**: enviada a un servicio Forms por una aplicación cliente que solicita una acción.
* **Respuesta de SOAP**: un servicio de Forms envía a una aplicación cliente después de que se procese una solicitud de SOAP.

Con los servicios web, puede realizar las mismas operaciones de servicios de AEM Forms que con la API de Java. Una ventaja de utilizar servicios web para invocar servicios de AEM Forms es que puede crear una aplicación cliente en un entorno de desarrollo compatible con SOAP. Una aplicación cliente no está enlazada a un entorno de desarrollo o lenguaje de programación específico. Por ejemplo, puede crear una aplicación cliente utilizando Microsoft Visual Studio .NET y C# como lenguaje de programación.

Los servicios de AEM Forms se exponen a través del protocolo SOAP y son compatibles con WSI Basic Profile 1.1. Interoperabilidad de servicios web (WSI) es una organización de estándares abiertos que promueve la interoperabilidad de servicios web entre plataformas. Para obtener más información, consulte [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms admite los siguientes estándares de servicio web:

* **Codificación**: solo admite codificación literal y de documento (que es la codificación preferida según el perfil básico de WSI). (Consulte [Invocación de AEM Forms mediante codificación Base64](#invoking-aem-forms-using-base64-encoding)).
* **MTOM**: representa una forma de codificar archivos adjuntos con solicitudes de SOAP. (Consulte [Invocar AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: representa otra forma de codificar archivos adjuntos con solicitudes SOAP. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref)).
* **SOAP con datos adjuntos**: admite MIME y DIME (encapsulación directa de mensajes de Internet). Estos protocolos son formas estándar de enviar archivos adjuntos a través de SOAP. Las aplicaciones de Microsoft Visual Studio .NET utilizan DIME. (Consulte [Invocación de AEM Forms mediante codificación Base64](#invoking-aem-forms-using-base64-encoding)).
* **WS-Security**: admite un perfil de token de contraseña de nombre de usuario, que es una forma estándar de enviar nombres de usuario y contraseñas como parte del encabezado de SOAP de seguridad de WS. AEM Forms también admite la autenticación básica HTTP. s

Para invocar los servicios de AEM Forms mediante un servicio web, normalmente se crea una biblioteca proxy que consume el WSDL del servicio. La sección *Invocar AEM Forms mediante servicios web* usa JAX-WS para crear clases de proxy Java para invocar servicios. (Consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)).

Puede recuperar una WDSL de servicio especificando la siguiente definición de URL (los elementos entre corchetes son opcionales):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

donde:

* *your_serverhost* representa la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.
* *your_port* representa el puerto HTTP que usa el servidor de aplicaciones J2EE.
* *service_name* representa el nombre del servicio.
* *version* representa la versión de destino de un servicio (la última versión del servicio se usa de forma predeterminada).
* `async` especifica el valor `true` para habilitar operaciones adicionales para la invocación asincrónica ( `false` de forma predeterminada).
* *lc_version* representa la versión de AEM Forms que desea invocar.

En la tabla siguiente se enumeran las definiciones de WSDL del servicio (suponiendo que AEM Forms se implemente en el host local y que la publicación sea 8080).

<table>
 <thead>
  <tr>
   <th><p>Servicio</p></th>
   <th><p>Definición de WSDL</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assembler</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Atrás y restaurar</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>formularios con códigos de barras</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Convertir PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Cifrado </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Formularios</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integración de datos de formulario</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generar PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generación de PDF 3D</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Salida</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilidades de PDF </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Extensiones de Acrobat Reader DC</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Repositorio</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Firma </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilidades de XMP</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**Definiciones WSDL de procesos de AEM Forms**

Especifique el nombre de la aplicación y el nombre del proceso dentro de la definición de WSDL para acceder a un WSDL que pertenece a un proceso creado en Workbench. Supongamos que el nombre de la aplicación es `MyApplication` y el nombre del proceso es `EncryptDocument`. En este caso, especifique la siguiente definición de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Para obtener información acerca del proceso de corta duración del ejemplo `MyApplication/EncryptDocument`, vea [Ejemplo de proceso de corta duración](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Una aplicación puede contener carpetas. En este caso, especifique los nombres de carpeta en la definición de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Acceder a nueva funcionalidad mediante servicios web**

Se puede acceder a la nueva funcionalidad del servicio AEM Forms mediante servicios web. Por ejemplo, en AEM Forms, se introduce la capacidad de codificar archivos adjuntos mediante MTOM. (Consulte [Invocar AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)

Para acceder a la nueva funcionalidad introducida en AEM Forms, especifique el atributo `lc_version` en la definición de WSDL. Por ejemplo, para acceder a la nueva funcionalidad del servicio (incluida la compatibilidad con MTOM), especifique la siguiente definición de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Al establecer el atributo `lc_version`, asegúrese de utilizar tres dígitos. Por ejemplo, 9.0.1 es igual a la versión 9.0.

**Tipo de datos BLOB del servicio web**

Los WSDL del servicio AEM Forms definen muchos tipos de datos. Uno de los tipos de datos más importantes expuestos en un servicio web es un tipo `BLOB`. Este tipo de datos se asigna a la clase `com.adobe.idp.Document` al trabajar con las API de Java de AEM Forms. (Consulte [Pasar datos a servicios de AEM Forms mediante la API de Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Un objeto `BLOB` envía y recupera datos binarios (por ejemplo, archivos PDF, datos XML, etc.) desde y hacia servicios de AEM Forms. El tipo `BLOB` se define en un WSDL de servicio de la siguiente manera:

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

Los campos `MTOM` y `swaRef` solo son compatibles con AEM Forms. Solo puede usar esos campos nuevos si especifica una dirección URL que incluya la propiedad `lc_version`.

**Suministro de objetos BLOB en solicitudes de servicio**

Si una operación del servicio AEM Forms requiere un tipo `BLOB` como valor de entrada, cree una instancia del tipo `BLOB` en la lógica de la aplicación. (Muchos de los inicios rápidos del servicio web en *Programación con formularios AEM* muestran cómo trabajar con un tipo de datos BLOB.)

Asigne valores a campos que pertenezcan a la instancia `BLOB` de la siguiente manera:

* **Base64**: para pasar datos como texto codificado en formato Base64, establezca los datos en el campo `BLOB.binaryData` y establezca el tipo de datos en formato MIME (por ejemplo, `application/pdf`) en el campo `BLOB.contentType`. (Consulte [Invocación de AEM Forms mediante codificación Base64](#invoking-aem-forms-using-base64-encoding)).
* **MTOM**: para pasar datos binarios en un archivo adjunto MTOM, establezca los datos en el campo `BLOB.MTOM`. Esta configuración adjunta los datos a la solicitud de SOAP mediante el marco de trabajo JAX-WS de Java o la API nativa del marco de trabajo de SOAP. (Consulte [Invocar AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: para pasar datos binarios en un archivo adjunto WS-I SwaRef, establezca los datos en el campo `BLOB.swaRef`. Esta configuración adjunta los datos a la solicitud de SOAP mediante el marco de trabajo Java JAX-WS. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref)).
* **Archivo adjunto MIME o DIME**: Para pasar datos en un archivo adjunto MIME o DIME, adjunte los datos a la solicitud de SOAP mediante la API nativa del marco de trabajo de SOAP. Establezca el identificador de los datos adjuntos en el campo `BLOB.attachmentID`. (Consulte [Invocación de AEM Forms mediante codificación Base64](#invoking-aem-forms-using-base64-encoding)).
* **URL remota**: Si los datos están hospedados en un servidor web y se puede obtener acceso a ellos a través de una URL HTTP, establezca la URL HTTP en el campo `BLOB.remoteURL`. (Consulte [Invocación de AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)).

**Acceso a datos en objetos BLOB devueltos por los servicios**

El protocolo de transmisión para los objetos `BLOB` devueltos depende de varios factores, que se consideran en el siguiente orden, y se detienen cuando se cumple la condición principal:

1. **La dirección URL de destino especifica el protocolo de transmisión**. Si la dirección URL de destino especificada en la invocación de SOAP contiene el parámetro `blob="`*BLOB_TYPE*&quot;, *BLOB_TYPE* determina el protocolo de transmisión. *BLOB_TYPE* es un marcador de posición para base64, dime, mime, http, mtom o swaref.
1. El extremo de **Service SOAP es inteligente**. Si las siguientes condiciones son verdaderas, los documentos de salida se devuelven utilizando el mismo protocolo de transmisión que los documentos de entrada:

   * El protocolo predeterminado del parámetro de extremo de SOAP del servicio para los objetos del blob de salida está establecido en Inteligente.

     Para cada servicio con un extremo de SOAP, la consola de administración le permite especificar el protocolo de transmisión para cualquier blob devuelto. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * El servicio AEM Forms toma uno o más documentos como entrada.

1. El extremo de **Service SOAP no es inteligente**. El protocolo configurado determina el protocolo de transmisión del documento y los datos se devuelven en el campo `BLOB` correspondiente. Por ejemplo, si el extremo de SOAP está establecido en DIME, el blob devuelto está en el campo `blob.attachmentID`, independientemente del protocolo de transmisión de cualquier documento de entrada.
1. **De lo contrario**. Si un servicio no toma el tipo de documento como entrada, los documentos de salida se devuelven en el campo `BLOB.remoteURL` a través del protocolo HTTP.

Como se describe en la primera condición, puede garantizar el tipo de transmisión para cualquier documento devuelto ampliando la URL del extremo de SOAP con un sufijo de la siguiente manera:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Esta es la correlación entre los tipos de transmisión y el campo del que se obtienen los datos:

* **Formato Base64**: establezca el sufijo `blob` en `base64` para devolver los datos en el campo `BLOB.binaryData`.
* **Datos adjuntos MIME o DIME**: establezca el sufijo `blob` en `DIME` o `MIME` para devolver los datos como el tipo de datos adjuntos correspondiente con el identificador de datos adjuntos devuelto en el campo `BLOB.attachmentID`. Utilice la API propietaria del marco de trabajo de SOAP para leer los datos del archivo adjunto.
* **Dirección URL remota**: establezca el sufijo `blob` en `http` para mantener los datos en el servidor de aplicaciones y devuelva la dirección URL que señala a los datos del campo `BLOB.remoteURL`.
* **MTOM o SwaRef**: establezca el sufijo `blob` en `mtom` o `swaref` para devolver los datos como un tipo de datos adjuntos correspondiente con el identificador de datos adjuntos devuelto en los campos `BLOB.MTOM` o `BLOB.swaRef`. Utilice la API nativa del marco de trabajo de SOAP para leer los datos del archivo adjunto.

>[!NOTE]
>
>Se recomienda no exceder los 30 MB al rellenar un objeto `BLOB` invocando su método `setBinaryData`. De lo contrario, es posible que se produzca una excepción `OutOfMemory`.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de una excepción `OutOfMemory`.

**Transmisión MTOM de matrices de bytes codificadas en base64**

Además del objeto `BLOB`, el protocolo MTOM admite cualquier parámetro de matriz de bytes o campo de matriz de bytes de un tipo complejo. Esto significa que los marcos de SOAP cliente que admiten MTOM pueden enviar cualquier elemento `xsd:base64Binary` como un archivo adjunto MTOM (en lugar de un texto codificado en Base64). Los extremos de AEM Forms SOAP pueden leer este tipo de codificación de matriz de bytes. Sin embargo, el servicio AEM Forms siempre devuelve un tipo de matriz de bytes como texto codificado en base64. Los parámetros de matriz de bytes de salida no admiten MTOM.

Los servicios de AEM Forms que devuelven una gran cantidad de datos binarios utilizan el tipo Documento/BLOB en lugar del tipo matriz de bytes. El tipo de documento es mucho más eficiente para transmitir grandes cantidades de datos.

## Tipos de datos del servicio web {#web-service-data-types}

En la tabla siguiente se enumeran los tipos de datos Java y se muestra el tipo de datos del servicio web correspondiente.

<table>
 <thead>
  <tr>
   <th><p>Tipo de datos Java</p></th>
   <th><p>Tipo de datos del servicio web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>El tipo <code>DATE</code>, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación del servicio AEM Forms toma un valor <code>java.util.Date</code> como entrada, la aplicación cliente de SOAP debe pasar la fecha en el campo <code>DATE.date</code>. La configuración del campo <code>DATE.calendar</code> en este caso provoca una excepción de tiempo de ejecución. Si el servicio devuelve un <code>java.util.Date</code>, la fecha se devuelve en el campo <code>DATE.date</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>El tipo <code>DATE</code>, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación del servicio AEM Forms toma un valor <code>java.util.Calendar</code> como entrada, la aplicación cliente de SOAP debe pasar la fecha en el campo <code>DATE.caledendar</code>. La configuración del campo <code>DATE.date</code> en este caso provoca una excepción en tiempo de ejecución. Si el servicio devuelve un <code>java.util.Calendar</code>, entonces la fecha se devuelve en el campo <code>DATE.calendar</code>. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>El <code>apachesoap:Map</code>, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>El mapa se representa como una secuencia de pares clave/valor.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación del servicio AEM Forms acepta un valor <code>org.w3c.dom.Document</code>, pase los datos XML en el campo <code>XML.document</code>.</p><p>Al establecer el campo <code>XML.element</code> se produce una excepción de tiempo de ejecución. Si el servicio devuelve un <code>org.w3c.dom.Document</code>, los datos XML se devuelven en el campo <code>XML.document</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>El tipo XML, que se define en un WSDL de servicio de la siguiente manera:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Si una operación del servicio AEM Forms toma un <code>org.w3c.dom.Element</code> como entrada, pase los datos XML en el campo <code>XML.element</code>.</p><p>Al establecer el campo <code>XML.document</code> se produce una excepción de tiempo de ejecución. Si el servicio devuelve un <code>org.w3c.dom.Element</code>, los datos XML se devuelven en el campo <code>XML.element</code>.</p></td>
  </tr>
 </tbody>
</table>

## Crear clases de proxy Java mediante JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Puede utilizar JAX-WS para convertir un WSDL de servicio de Forms en clases de proxy de Java. Estas clases permiten invocar operaciones de servicios de AEM Forms. Apache Ant permite crear un script de compilación que genera clases de proxy Java haciendo referencia a un WSDL del servicio AEM Forms. Puede generar archivos proxy JAX-WS realizando los siguientes pasos:

1. Instale Apache Ant en el equipo cliente. (Consulte [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Añada el directorio bin a la ruta de clase.
   * Establezca la variable de entorno `ANT_HOME` en el directorio donde instaló Ant.

1. Instale JDK 1.6 o posterior.

   * Añada el directorio JDK bin a la ruta de clase.
   * Añada el directorio bin JRE a la ruta de clase. Este grupo se encuentra en el directorio `[JDK_INSTALL_LOCATION]/jre`.
   * Configure la variable de entorno `JAVA_HOME` en el directorio donde instaló el JDK.

   JDK 1.6 incluye el programa wsimport utilizado en el archivo build.xml. JDK 1.5 no incluye ese programa.

1. Instale JAX-WS en el equipo cliente. (Consulte [API de Java para servicios web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Utilice JAX-WS y Apache Ant para generar clases de proxy de Java. Cree un script de generación de hormigas para realizar esta tarea. El siguiente script es un ejemplo de script de generación de Ant denominado build.xml:

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   Dentro de este script de generación de Ant, observe que la propiedad `url` está configurada para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. Las propiedades `username` y `password` deben establecerse en un nombre de usuario y una contraseña de formularios AEM Forms válidos. Observe que la dirección URL contiene el atributo `lc_version`. Sin especificar la opción `lc_version`, no puede invocar nuevas operaciones del servicio AEM Forms.

   >[!NOTE]
   >
   >Reemplace `EncryptionService` por el nombre de servicio de AEM Forms que desea invocar mediante clases de proxy Java. Por ejemplo, para crear clases de proxy Java para el servicio de Rights Management, especifique:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Cree un archivo BAT para ejecutar el script de generación Ant. El siguiente comando se puede encontrar dentro de un archivo BAT responsable de ejecutar el script de generación Ant:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Coloque el script de generación ANT en el directorio C:\Program Files\Java\jaxws-ri\bin. La secuencia de comandos escribe los archivos JAVA en .Carpeta /classes. El script genera archivos JAVA que pueden invocar el servicio.

1. Empaquete los archivos JAVA en un archivo JAR. Si está trabajando en Eclipse, siga estos pasos:

   * Cree un proyecto Java que se utilice para empaquetar los archivos JAVA proxy en un archivo JAR.
   * Cree una carpeta de origen en el proyecto.
   * Cree un paquete `com.adobe.idp.services` en la carpeta Source.
   * Seleccione el paquete `com.adobe.idp.services` y luego importe los archivos JAVA de la carpeta adobe/idp/services en el paquete.
   * Si es necesario, cree un paquete `org/apache/xml/xmlsoap` en la carpeta Source.
   * Seleccione la carpeta de origen y, a continuación, importe los archivos JAVA desde la carpeta org/apache/xml/xml/xml/xmlsoap.
   * Establezca el nivel de cumplimiento del compilador de Java en 5.0 o superior.
   * Genere el proyecto.
   * Exporte el proyecto como archivo JAR.
   * Importe este archivo JAR en la ruta de clase de un proyecto cliente. Además, importe todos los archivos JAR en &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Todos los inicios rápidos del servicio web de Java (excepto el servicio Forms) en Programación con formularios AEM crean archivos proxy de Java mediante JAX-WS. Además, todos los inicios rápidos del servicio web de Java, utilizan SwaRef. (Consulte [Invocación de AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref)).

**Consulte también**

[Creación de clases de proxy Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)

[Invocar AEM Forms con codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocar AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Invocar AEM Forms mediante SwaRef](#invoking-aem-forms-using-swaref)

## Creación de clases de proxy Java mediante Apache Axis {#creating-java-proxy-classes-using-apache-axis}

Puede utilizar la herramienta WSDL2Java del eje Apache para convertir un servicio de Forms en clases de proxy de Java. Estas clases permiten invocar las operaciones del servicio Forms. Con Apache Ant, puede generar archivos de biblioteca de Axis a partir de un WSDL de servicio. Puede descargar Apache Axis en la dirección URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Los inicios rápidos del servicio web asociados al servicio Forms utilizan clases de proxy Java creadas con Apache Axis. Los inicios rápidos del servicio web de Forms también utilizan Base64 como tipo de codificación. (Consulte [Inicios rápidos de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)).

Puede generar archivos de biblioteca Java de Axis realizando los siguientes pasos:

1. Instale Apache Ant en el equipo cliente. Está disponible en [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Añada el directorio bin a la ruta de clase.
   * Establezca la variable de entorno `ANT_HOME` en el directorio donde instaló Ant.

1. Instale Apache Axis 1.4 en el equipo cliente. Está disponible en [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. Configure la ruta de clase para utilizar los archivos JAR de Axis en su cliente de servicio web, tal como se describe en las instrucciones de instalación de Axis en [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Utilice la herramienta Apache WSDL2Java en Axis para generar clases de proxy Java. Cree un script de generación de hormigas para realizar esta tarea. El siguiente script es un ejemplo de script de generación de Ant denominado build.xml:

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   Dentro de este script de generación de Ant, observe que la propiedad `url` está configurada para hacer referencia al WSDL del servicio de cifrado que se ejecuta en localhost. Las propiedades `username` y `password` deben establecerse en un nombre de usuario y una contraseña de formularios AEM Forms válidos.

1. Cree un archivo BAT para ejecutar el script de generación Ant. El siguiente comando se puede encontrar dentro de un archivo BAT responsable de ejecutar el script de generación Ant:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   Los archivos JAVA se escriben en la carpeta C:\JavaFiles según lo especificado por la propiedad `output`. Para invocar correctamente el servicio Forms, importe estos archivos JAVA en la ruta de clase.

   De manera predeterminada, estos archivos pertenecen a un paquete Java denominado `com.adobe.idp.services`. Se recomienda colocar estos archivos JAVA en un archivo JAR. A continuación, importe el archivo JAR en la ruta de clase de la aplicación cliente.

   >[!NOTE]
   >
   >Existen diferentes maneras de colocar los archivos .JAVA en un JAR. Una forma es usar un IDE de Java como Eclipse. Cree un proyecto Java y un paquete `com.adobe.idp.services` (todos los archivos .JAVA pertenecen a este paquete). A continuación, importe todos los archivos .JAVA en el paquete. Finalmente, exporte el proyecto como archivo JAR.

1. Modifique la dirección URL en la clase `EncryptionServiceLocator` para especificar el tipo de codificación. Por ejemplo, para usar base64, especifique `?blob=base64` para asegurarse de que el objeto `BLOB` devuelve datos binarios. Es decir, en la clase `EncryptionServiceLocator`, busque la línea de código siguiente:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   y cámbielo por:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Agregue los siguientes archivos JAR de eje a la ruta de clase del proyecto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   Estos archivos JAR se encuentran en el directorio `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty`.

**Consulte también**

[Crear clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Invocar AEM Forms con codificación Base64](#invoking-aem-forms-using-base64-encoding)

[Invocar AEM Forms mediante datos BLOB a través de HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Invocar AEM Forms con codificación Base64 {#invoking-aem-forms-using-base64-encoding}

Puede invocar un servicio de AEM Forms utilizando la codificación Base64. La codificación Base64 codifica los archivos adjuntos que se envían con una solicitud de invocación de servicio web. Es decir, los datos de `BLOB` están codificados en Base64, no en todo el mensaje de SOAP.

&quot;Invocar AEM Forms mediante la codificación Base64&quot; describe la invocación del siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument` mediante la codificación Base64.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

### Crear un ensamblado de cliente .NET que utilice codificación Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

Puede crear un ensamblado de cliente de .NET para invocar un servicio de Forms desde un proyecto de Microsoft Visual Studio .NET. Para crear un ensamblado de cliente .NET que utilice codificación base64, realice los siguientes pasos:

1. Cree una clase de proxy basada en una URL de invocación de AEM Forms.
1. Cree un proyecto de Microsoft Visual Studio .NET que produzca el ensamblado de cliente .NET.

**Creando una clase de proxy**

Puede crear una clase de proxy que se utiliza para crear el ensamblado de cliente de .NET mediante una herramienta que acompaña a Microsoft Visual Studio. El nombre de la herramienta es wsdl.exe y se encuentra en la carpeta de instalación de Microsoft Visual Studio. Para crear una clase de proxy, abra el símbolo del sistema y vaya a la carpeta que contiene el archivo wsdl.exe. Para obtener más información acerca de la herramienta wsdl.exe, vea la *Ayuda de MSDN*.

Introduzca el siguiente comando en el símbolo del sistema:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

De forma predeterminada, esta herramienta crea un archivo CSS en la misma carpeta basado en el nombre del WSDL. En este caso, crea un archivo CSS denominado *EncryptDocumentService.cs*. Este archivo CSS se utiliza para crear un objeto proxy que le permite invocar el servicio especificado en la URL de invocación.

Modifique la dirección URL en la clase de proxy para incluir `?blob=base64` a fin de asegurarse de que el objeto `BLOB` devuelva datos binarios. En la clase de proxy, busque la línea de código siguiente:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

y cámbielo por:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

La sección *Invocando AEM Forms usando codificación Base64* usa `MyApplication/EncryptDocument` como ejemplo. Si está creando un ensamblado de cliente .NET para otro servicio de Forms, asegúrese de reemplazar `MyApplication/EncryptDocument` por el nombre del servicio.

**Desarrollar el ensamblado de cliente .NET**

Cree un proyecto de biblioteca de clases de Visual Studio que produzca un ensamblado de cliente de .NET. El archivo CSS que creó con wsdl.exe se puede importar en este proyecto. Este proyecto produce un archivo DLL (el ensamblado de cliente de .NET) que se puede utilizar en otros proyectos de Visual Studio .NET para invocar un servicio.

1. Inicie Microsoft Visual Studio .NET.
1. Cree un proyecto de Biblioteca de clases y asígnele el nombre DocumentService.
1. Importe el archivo CSS que ha creado mediante wsdl.exe.
1. En el menú **Proyecto**, seleccione **Agregar referencia**.
1. En el cuadro de diálogo Agregar referencia, seleccione **System.Web.Services.dll**.
1. Haga clic en **Seleccionar** y, a continuación, haga clic en **Aceptar**.
1. Compile y genere el proyecto.

>[!NOTE]
>
>Este procedimiento crea un ensamblado de cliente .NET denominado DocumentService.dll que puede utilizar para enviar solicitudes de SOAP al servicio `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Asegúrese de agregar `?blob=base64` a la dirección URL de la clase de proxy que se utiliza para crear el ensamblado de cliente de .NET. De lo contrario, no podrá recuperar datos binarios del objeto `BLOB`.

**Haciendo referencia al ensamblado de cliente .NET**

Coloque el ensamblado de cliente de .NET recién creado en el equipo en el que está desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. Haga referencia también a la biblioteca `System.Web.Services` desde el proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado de cliente de .NET para invocar un servicio.

1. En el menú **Proyecto**, seleccione **Agregar referencia**.
1. Haga clic en la ficha **.NET**.
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Haga clic en **Seleccionar** y, a continuación, haga clic en **Aceptar**.

**Invocar un servicio mediante un ensamblado de cliente .NET que utiliza la codificación Base64**

Puede invocar el servicio `MyApplication/EncryptDocument` (que se creó en Workbench) mediante un ensamblado de cliente de .NET que utiliza la codificación Base64. Para invocar el servicio `MyApplication/EncryptDocument`, realice los siguientes pasos:

1. Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL del servicio `MyApplication/EncryptDocument`.
1. Cree un proyecto cliente de Microsoft .NET. Hacer referencia al ensamblado de cliente de Microsoft .NET en el proyecto de cliente. También hacer referencia a `System.Web.Services`.
1. Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `MyApplication_EncryptDocumentService` invocando su constructor predeterminado.
1. Establezca la propiedad `Credentials` del objeto `MyApplication_EncryptDocumentService` con un objeto `System.Net.NetworkCredential`. En el constructor `System.Net.NetworkCredential`, especifique un nombre de usuario de formularios AEM Forms y la contraseña correspondiente. Establezca valores de autenticación para permitir que la aplicación cliente de .NET intercambie correctamente los mensajes de SOAP con AEM Forms.
1. Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un pase de documento de PDF al proceso `MyApplication/EncryptDocument`.
1. Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF y el modo en que se abrirá el archivo.
1. Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
1. Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
1. Rellene el objeto `BLOB` asignando su propiedad `binaryData` con el contenido de la matriz de bytes.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplication_EncryptDocumentService` y pasando el objeto `BLOB` que contiene el documento de PDF. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento cifrado con contraseña.
1. Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `invoke` del objeto `MyApplicationEncryptDocumentService`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `binaryData` del objeto `BLOB`.
1. Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

### Invocar un servicio mediante clases de proxy Java y codificación Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Puede invocar un servicio de AEM Forms mediante las clases de proxy Java y Base64. Para invocar el servicio `MyApplication/EncryptDocument` mediante clases de proxy Java, realice los siguientes pasos:

1. Cree clases de proxy Java mediante JAX-WS que consuma el WSDL del servicio `MyApplication/EncryptDocument`. Utilice el siguiente punto final WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *por la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Empaquete las clases de proxy Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase del proyecto cliente Java.

1. Crear un objeto `MyApplicationEncryptDocumentService` mediante su constructor.
1. Cree un objeto `MyApplicationEncryptDocument` invocando el método `getEncryptDocument` del objeto `MyApplicationEncryptDocumentService`.
1. Establezca los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al campo `ENDPOINT_ADDRESS_PROPERTY` del objeto `javax.xml.ws.BindingProvider`. Para invocar el servicio `MyApplication/EncryptDocument` mediante la codificación Base64, especifique el siguiente valor de dirección URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Asigne el usuario de formularios AEM Forms al campo `USERNAME_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.
   * Asigne el valor de contraseña correspondiente al campo `PASSWORD_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.

   El ejemplo de código siguiente muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento de PDF que se va a enviar al proceso `MyApplication/EncryptDocument` creando un objeto `java.io.FileInputStream` mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento de PDF.
1. Cree una matriz de bytes y rellénela con el contenido del objeto `java.io.FileInputStream`.
1. Crear un objeto `BLOB` mediante su constructor.
1. Rellene el objeto `BLOB` invocando su método `setBinaryData` y pasando la matriz de bytes. El objeto `setBinaryData` de `BLOB` es el método al que se llama cuando se utiliza la codificación Base64. Consulte Suministro de objetos BLOB en solicitudes de servicio.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplicationEncryptDocument`. Pase el objeto `BLOB` que contiene el documento de PDF. El método invoke devuelve un objeto `BLOB` que contiene el documento de PDF cifrado.
1. Cree una matriz de bytes que contenga el documento cifrado de PDF invocando el método `getBinaryData` del objeto `BLOB`.
1. Guarde el documento de PDF cifrado como archivo de PDF. Escriba la matriz de bytes en un archivo.

**Consulte también**

[Inicio rápido: Invocar un servicio mediante archivos proxy Java y codificación Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Crear un ensamblado de cliente .NET que utilice codificación Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Invocar AEM Forms mediante MTOM {#invoking-aem-forms-using-mtom}

Puede invocar los servicios de AEM Forms utilizando el MTOM estándar del servicio web. Este estándar define cómo se transmiten los datos binarios, como un documento de PDF, a través de Internet o de la intranet. Una característica de MTOM es el uso del elemento `XOP:Include`. Este elemento se define en la especificación XML Binary Optimized Packaging (XOP) para hacer referencia a los archivos adjuntos binarios de un mensaje de SOAP.

La discusión aquí trata sobre el uso de MTOM para invocar el siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se ha añadido compatibilidad con MTOM en AEM Forms, versión 9.

>[!NOTE]
>
>Las aplicaciones basadas en JAX WS que utilizan el protocolo de transmisión MTOM están limitadas a 25 MB de datos enviados y recibidos. Esta limitación se debe a un error en JAX-WS. Si el tamaño combinado de los archivos enviados y recibidos supera los 25 MB, utilice el protocolo de transmisión SwaRef en lugar del MTOM. De lo contrario, existe la posibilidad de una excepción `OutOfMemory`.

La discusión aquí trata sobre el uso de MTOM en un proyecto de Microsoft .NET para invocar servicios de AEM Forms. .NET Framework utilizado es 3.5 y el entorno de desarrollo es Visual Studio 2008. Si tiene instaladas las Mejoras de servicios Web (WSE) en el equipo de desarrollo, quítelas. .NET Framework 3.5 admite un marco de trabajo de SOAP denominado Windows Communication Foundation (WCF). Al invocar AEM Forms mediante MTOM, solo se admite WCF (no WSE).

### Crear un proyecto de .NET que invoque un servicio mediante MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Puede crear un proyecto de Microsoft .NET que pueda invocar un servicio de AEM Forms mediante servicios web. Primero, cree un proyecto de Microsoft .NET con Visual Studio 2008. Para invocar un servicio de AEM Forms, cree una referencia de servicio al servicio de AEM Forms que desee invocar en el proyecto. Cuando cree una referencia de servicio, especifique una URL para el servicio de AEM Forms:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Reemplace `localhost` por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms. Reemplazar `MyApplication/EncryptDocument` con el nombre del servicio de AEM Forms que se va a invocar. Por ejemplo, para invocar una operación de Rights Management, especifique:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

La opción `lc_version` garantiza que la funcionalidad de AEM Forms, como MTOM, esté disponible. Sin especificar la opción `lc_version`, no puede invocar AEM Forms mediante MTOM.

Después de crear una Referencia de servicio, los tipos de datos asociados con el servicio AEM Forms se pueden utilizar en el proyecto .NET. Para crear un proyecto de .NET que invoque un servicio de AEM Forms, realice los siguientes pasos:

1. Cree un proyecto de .NET mediante Microsoft Visual Studio 2008.
1. En el menú **Proyecto**, seleccione **Agregar referencia de servicio**.
1. En el cuadro de diálogo **Dirección**, especifique el WSDL al servicio AEM Forms. Por ejemplo,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Haz clic en **Ir** y luego haz clic en **Aceptar**.

### Invocar un servicio mediante MTOM en un proyecto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Considere el proceso `MyApplication/EncryptDocument` que acepta un documento de PDF no protegido y devuelve un documento de PDF cifrado con contraseña. Para invocar el proceso `MyApplication/EncryptDocument` (que se creó en Workbench) mediante MTOM, realice los siguientes pasos:

1. Cree un proyecto de Microsoft .NET.
1. Cree un objeto `MyApplication_EncryptDocumentClient` utilizando su constructor predeterminado.
1. Cree un objeto `MyApplication_EncryptDocumentClient.Endpoint.Address` mediante el constructor `System.ServiceModel.EndpointAddress`. Pase un valor de cadena que especifique el WSDL al servicio AEM Forms y el tipo de codificación:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   No necesita usar el atributo `lc_version`. Este atributo se utiliza al crear una referencia de servicio. Sin embargo, asegúrese de especificar `?blob=mtom`.

   >[!NOTE]
   >
   >Reemplazar `hiro-xp` *por la dirección IP del servidor de aplicaciones J2EE que hospeda AEM Forms.*

1. Cree un objeto `System.ServiceModel.BasicHttpBinding` obteniendo el valor del miembro de datos `EncryptDocumentClient.Endpoint.Binding`. Convertir el valor devuelto en `BasicHttpBinding`.
1. Establezca el miembro de datos `MessageEncoding` del objeto `System.ServiceModel.BasicHttpBinding` en `WSMessageEncoding.Mtom`. Este valor garantiza que se utiliza MTOM.
1. Habilite la autenticación HTTP básica realizando las siguientes tareas:

   * Asigne el nombre de usuario de los formularios AEM Forms al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Asigne el valor de contraseña correspondiente al miembro de datos `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Asigne el valor constante `HttpClientCredentialType.Basic` al miembro de datos `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Asigne el valor constante `BasicHttpSecurityMode.TransportCredentialOnly` al miembro de datos `BasicHttpBindingSecurity.Security.Mode`.

   En el ejemplo de código siguiente se muestran estas tareas.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para almacenar un documento de PDF para pasarlo al proceso `MyApplication/EncryptDocument`.
1. Cree un objeto `System.IO.FileStream` invocando su constructor. Pase un valor de cadena que represente la ubicación del archivo del documento de PDF y el modo en que se abrirá el archivo.
1. Cree una matriz de bytes que almacene el contenido del objeto `System.IO.FileStream`. Puede determinar el tamaño de la matriz de bytes obteniendo la propiedad `Length` del objeto `System.IO.FileStream`.
1. Rellene la matriz de bytes con datos de secuencia invocando el método `Read` del objeto `System.IO.FileStream`. Pase a leer la matriz de bytes, la posición inicial y la longitud de la secuencia.
1. Rellene el objeto `BLOB` asignando su miembro de datos `MTOM` con el contenido de la matriz de bytes.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplication_EncryptDocumentClient`. Pase el objeto `BLOB` que contiene el documento de PDF. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente la ubicación de archivo del documento de PDF protegido.
1. Cree una matriz de bytes que almacene el contenido de datos del objeto `BLOB` devuelto por el método `invoke`. Rellene la matriz de bytes obteniendo el valor del miembro de datos `MTOM` del objeto `BLOB`.
1. Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

>[!NOTE]
>
>La mayoría de las operaciones del servicio AEM Forms tienen un inicio rápido MTOM. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Inicio rápido de salida, vea [Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también**

[Inicio rápido: Invocar un servicio mediante MTOM en un proyecto de .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Acceder a varios servicios mediante servicios web](#accessing-multiple-services-using-web-services)

[Crear una aplicación web ASP.NET que invoque un proceso de larga duración centrado en humanos](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Invocar AEM Forms mediante SwaRef {#invoking-aem-forms-using-swaref}

Puede invocar los servicios de AEM Forms mediante SwaRef. El contenido del elemento XML `wsi:swaRef` se envía como datos adjuntos dentro de un cuerpo de SOAP que almacena la referencia a los datos adjuntos. Al invocar un servicio de Forms mediante SwaRef, cree clases de proxy Java mediante la API de Java para servicios web XML (JAX-WS). (Consulte [API de Java para servicios web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

La discusión aquí trata de invocar el siguiente proceso de corta duración de Forms denominado `MyApplication/EncryptDocument` mediante SwaRef.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se ha añadido compatibilidad con SwaRef en AEM Forms

La siguiente explicación trata sobre cómo invocar los servicios de Forms mediante SwaRef en una aplicación cliente Java. La aplicación Java utiliza clases de proxy creadas mediante JAX-WS.

### Invocar un servicio mediante archivos de biblioteca JAX-WS que utilizan SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Para invocar el proceso `MyApplication/EncryptDocument` mediante archivos proxy Java creados con JAX-WS y SwaRef, realice los siguientes pasos:

1. Cree clases de proxy Java mediante JAX-WS que consuma el WSDL del servicio `MyApplication/EncryptDocument`. Utilice el siguiente punto final WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, vea [Crear clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplace `hiro-xp` *por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.*

1. Empaquete las clases de proxy Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase del proyecto cliente Java.

1. Crear un objeto `MyApplicationEncryptDocumentService` mediante su constructor.
1. Cree un objeto `MyApplicationEncryptDocument` invocando el método `getEncryptDocument` del objeto `MyApplicationEncryptDocumentService`.
1. Establezca los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al campo `ENDPOINT_ADDRESS_PROPERTY` del objeto `javax.xml.ws.BindingProvider`. Para invocar el servicio `MyApplication/EncryptDocument` mediante la codificación SwaRef, especifique el siguiente valor de URL:

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Asigne el usuario de formularios AEM Forms al campo `USERNAME_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.
   * Asigne el valor de contraseña correspondiente al campo `PASSWORD_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.

   El ejemplo de código siguiente muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere el documento de PDF que se va a enviar al proceso `MyApplication/EncryptDocument` creando un objeto `java.io.File` mediante su constructor. Pase un valor de cadena que especifique la ubicación del documento de PDF.
1. Cree un objeto `javax.activation.DataSource` mediante el constructor `FileDataSource`. Pase el objeto `java.io.File`.
1. Cree un objeto `javax.activation.DataHandler` utilizando su constructor y pasando el objeto `javax.activation.DataSource`.
1. Crear un objeto `BLOB` mediante su constructor.
1. Rellene el objeto `BLOB` invocando su método `setSwaRef` y pasando el objeto `javax.activation.DataHandler`.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplicationEncryptDocument` y pasando el objeto `BLOB` que contiene el documento de PDF. El método invoke devuelve un objeto `BLOB` que contiene un documento de PDF cifrado.
1. Rellene un objeto `javax.activation.DataHandler` invocando el método `getSwaRef` del objeto `BLOB`.
1. Convierta el objeto `javax.activation.DataHandler` en una instancia `java.io.InputSteam` invocando el método `getInputStream` del objeto `javax.activation.DataHandler`.
1. Escriba la instancia `java.io.InputSteam` en un archivo PDF que represente el documento cifrado de PDF.

>[!NOTE]
>
>La mayoría de las operaciones del servicio de AEM Forms tienen un inicio rápido de SwaRef. Puede ver estos inicios rápidos en la sección de inicio rápido correspondiente de un servicio. Por ejemplo, para ver la sección Inicio rápido de salida, vea [Inicio rápido de la API del servicio de salida](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte también**

[Inicio rápido: Invocar un servicio mediante SwaRef en un proyecto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Invocar AEM Forms mediante datos BLOB a través de HTTP {#invoking-aem-forms-using-blob-data-over-http}

Puede invocar los servicios de AEM Forms mediante servicios web y pasando datos BLOB a través de HTTP. Pasar datos BLOB a través de HTTP es una técnica alternativa en lugar de utilizar codificación base64, DIME o MIME. Por ejemplo, puede pasar datos a través de HTTP en un proyecto de Microsoft .NET que utiliza la mejora de servicios web 3.0, que no admite DIME ni MIME. Cuando se utilizan datos BLOB a través de HTTP, los datos de entrada se cargan antes de que se invoque el servicio AEM Forms.

&quot;Invocar AEM Forms mediante datos BLOB a través de HTTP&quot; describe la invocación del siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument` al pasar datos BLOB a través de HTTP.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con el ejemplo de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

>[!NOTE]
>
>Se recomienda que esté familiarizado con la invocación de AEM Forms mediante SOAP. (Consulte [Invocar AEM Forms mediante servicios web](#invoking-aem-forms-using-web-services).)

### Crear un ensamblado de cliente .NET que utilice datos a través de HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Para crear un ensamblado de cliente que utilice datos a través de HTTP, siga el proceso especificado en [Invocar AEM Forms mediante la codificación Base64](#invoking-aem-forms-using-base64-encoding). Sin embargo, modifique la dirección URL en la clase de proxy para incluir `?blob=http` en lugar de `?blob=base64`. Esta acción garantiza que los datos se pasen a través de HTTP. En la clase de proxy, busque la línea de código siguiente:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

y cámbielo por:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Hacer referencia al ensamblado clientMyApplication/EncryptDocument de .NET**

Coloque el nuevo ensamblado de cliente .NET en el equipo en el que está desarrollando la aplicación cliente. Después de colocar el ensamblado de cliente .NET en un directorio, puede hacer referencia a él desde un proyecto. Hacer referencia a la biblioteca `System.Web.Services` desde el proyecto. Si no hace referencia a esta biblioteca, no puede utilizar el ensamblado de cliente de .NET para invocar un servicio.

1. En el menú **Proyecto**, seleccione **Agregar referencia**.
1. Haga clic en la ficha **.NET**.
1. Haga clic en **Examinar** y busque el archivo DocumentService.dll.
1. Haga clic en **Seleccionar** y, a continuación, haga clic en **Aceptar**.

**Invocar un servicio mediante un ensamblado de cliente .NET que utiliza datos BLOB a través de HTTP**

Puede invocar el servicio `MyApplication/EncryptDocument` (que se creó en Workbench) mediante un ensamblado de cliente de .NET que utiliza datos a través de HTTP. Para invocar el servicio `MyApplication/EncryptDocument`, realice los siguientes pasos:

1. Cree el ensamblado de cliente de .NET.
1. Hacer referencia al ensamblado de cliente de Microsoft .NET. Cree un proyecto cliente de Microsoft .NET. Hacer referencia al ensamblado de cliente de Microsoft .NET en el proyecto de cliente. También hacer referencia a `System.Web.Services`.
1. Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `MyApplication_EncryptDocumentService` invocando su constructor predeterminado.
1. Establezca la propiedad `Credentials` del objeto `MyApplication_EncryptDocumentService` con un objeto `System.Net.NetworkCredential`. En el constructor `System.Net.NetworkCredential`, especifique un nombre de usuario de formularios AEM Forms y la contraseña correspondiente. Establezca valores de autenticación para permitir que la aplicación cliente de .NET intercambie correctamente los mensajes de SOAP con AEM Forms.
1. Crear un objeto `BLOB` mediante su constructor. El objeto `BLOB` se usa para pasar datos al proceso `MyApplication/EncryptDocument`.
1. Asigne un valor de cadena al miembro de datos `remoteURL` del objeto `BLOB` que especifique la ubicación URI de un documento de PDF que se pasará al servicio `MyApplication/EncryptDocument`.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplication_EncryptDocumentService` y pasando el objeto `BLOB`. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Cree un objeto `System.UriBuilder` utilizando su constructor y pasando el valor del miembro de datos `remoteURL` del objeto `BLOB` devuelto.
1. Convertir el objeto `System.UriBuilder` en un objeto `System.IO.Stream`. (El Inicio rápido de C# que sigue a esta lista ilustra cómo realizar esta tarea.)
1. Cree una matriz de bytes y rellénela con los datos del objeto `System.IO.Stream`.
1. Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
1. Escriba el contenido de la matriz de bytes en un archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

### Invocar un servicio mediante clases de proxy Java y datos BLOB a través de HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Puede invocar un servicio de AEM Forms utilizando clases de proxy Java y datos BLOB a través de HTTP. Para invocar el servicio `MyApplication/EncryptDocument` mediante clases de proxy Java, realice los siguientes pasos:

1. Cree clases de proxy Java mediante JAX-WS que consuma el WSDL del servicio `MyApplication/EncryptDocument`. Utilice el siguiente punto final WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obtener más información, vea [Crear clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Reemplace `hiro-xp` *por la dirección IP del servidor de aplicaciones J2EE que aloja AEM Forms.*

1. Empaquete las clases de proxy Java creadas con JAX-WS en un archivo JAR.
1. Incluya el archivo JAR del proxy Java y los archivos JAR en la siguiente ruta:

   &lt;Directorio de instalación>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   en la ruta de clase del proyecto cliente Java.

1. Crear un objeto `MyApplicationEncryptDocumentService` mediante su constructor.
1. Cree un objeto `MyApplicationEncryptDocument` invocando el método `getEncryptDocument` del objeto `MyApplicationEncryptDocumentService`.
1. Establezca los valores de conexión necesarios para invocar AEM Forms asignando valores a los siguientes miembros de datos:

   * Asigne el extremo WSDL y el tipo de codificación al campo `ENDPOINT_ADDRESS_PROPERTY` del objeto `javax.xml.ws.BindingProvider`. Para invocar el servicio `MyApplication/EncryptDocument` mediante la codificación BLOB sobre HTTP, especifique el siguiente valor de URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Asigne el usuario de formularios AEM Forms al campo `USERNAME_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.
   * Asigne el valor de contraseña correspondiente al campo `PASSWORD_PROPERTY` del objeto `javax.xml.ws.BindingProvider`.

   El ejemplo de código siguiente muestra esta lógica de aplicación:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Crear un objeto `BLOB` mediante su constructor.
1. Rellene el objeto `BLOB` invocando su método `setRemoteURL`. Pase un valor de cadena que especifique la ubicación URI de un documento de PDF para pasar al servicio `MyApplication/EncryptDocument`.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `MyApplicationEncryptDocument` y pasando el objeto `BLOB` que contiene el documento de PDF. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Cree una matriz de bytes para almacenar el flujo de datos que representa el documento cifrado de PDF. Invoque el método `getRemoteURL` del objeto `BLOB` (utilice el objeto `BLOB` devuelto por el método `invoke`).
1. Crear un objeto `java.io.File` mediante su constructor. Este objeto representa el documento cifrado de PDF.
1. Cree un objeto `java.io.FileOutputStream` utilizando su constructor y pasando el objeto `java.io.File`.
1. Invoque el método `write` del objeto `java.io.FileOutputStream`. Pase la matriz de bytes que contiene la secuencia de datos que representa el documento cifrado de PDF.

## Invocar AEM Forms mediante DIME {#invoking-aem-forms-using-dime}

Puede invocar los servicios de AEM Forms mediante SOAP con archivos adjuntos. AEM Forms admite los estándares de servicio web MIME y DIME. DIME permite enviar archivos adjuntos binarios, como documentos de PDF, junto con solicitudes de invocación en lugar de codificar el archivo adjunto. En la sección *Invocación de AEM Forms mediante DIME* se describe la invocación del siguiente proceso de corta duración de AEM Forms denominado `MyApplication/EncryptDocument` mediante DIME.

Cuando se invoca este proceso, realiza las siguientes acciones:

1. Obtiene el documento de PDF no seguro que se pasa al proceso. Esta acción se basa en la operación `SetValue`. El parámetro de entrada para este proceso es una variable de proceso `document` denominada `inDoc`.
1. Cifra el documento de PDF con una contraseña. Esta acción se basa en la operación `PasswordEncryptPDF`. El documento de PDF cifrado con contraseña se devuelve en una variable de proceso denominada `outDoc`.

Este proceso no se basa en un proceso de AEM Forms existente. Para continuar con los ejemplos de código, cree un proceso denominado `MyApplication/EncryptDocument` mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

>[!NOTE]
>
>La invocación de operaciones del servicio AEM Forms mediante DIME está obsoleta. Se recomienda utilizar MTOM. (Consulte [Invocar AEM Forms mediante MTOM](#invoking-aem-forms-using-mtom).)

### Crear un proyecto de .NET que utilice DIME {#creating-a-net-project-that-uses-dime}

Para crear un proyecto de .NET que pueda invocar un servicio de Forms mediante DIME, realice las siguientes tareas:

* Instale las mejoras de Servicios Web 2.0 en el equipo de desarrollo.
* Desde el proyecto de .NET, cree una referencia web al servicio FormsAEM Forms.

**Mejoras en la instalación de servicios web 2.0**

Instale las mejoras de los servicios Web 2.0 en el equipo de desarrollo e integre la aplicación con Microsoft Visual Studio .NET. Puede descargar las mejoras de los servicios web 2.0 desde el [Centro de descarga de Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Desde esta página web, busque Mejoras de servicios web 2.0 y descárguelo en el equipo de desarrollo. Esta descarga coloca un archivo llamado Microsoft WSE 2.0 SPI.msi en el equipo. Ejecute el programa de instalación y siga las instrucciones en línea.

>[!NOTE]
>
>Las mejoras de Web Services 2.0 admiten DIME. La versión admitida de Microsoft Visual Studio es 2003 cuando se trabaja con las mejoras de los servicios web 2.0. Mejoras en los servicios web 3.0 no admite DIME; sin embargo, admite MTOM.

**Creando una referencia web a un servicio de AEM Forms**

Después de instalar las mejoras de Servicios Web 2.0 en el equipo de desarrollo y crear un proyecto de Microsoft .NET, cree una referencia web al servicio de Forms. Por ejemplo, para crear una referencia web al proceso `MyApplication/EncryptDocument` y suponiendo que Forms está instalado en el equipo local, especifique la siguiente dirección URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Después de crear una referencia web, puede usar los dos tipos de datos proxy siguientes en su proyecto .NET: `EncryptDocumentService` y `EncryptDocumentServiceWse`. Para invocar el proceso `MyApplication/EncryptDocument` mediante DIME, use el tipo `EncryptDocumentServiceWse`.

>[!NOTE]
>
>Antes de crear una referencia web al servicio de Forms, asegúrese de hacer referencia a las mejoras de los servicios web 2.0 en su proyecto. (Consulte &quot;Instalación de mejoras de servicios web 2.0&quot;.)

**Hacer referencia a la biblioteca WSE**

1. En el menú Proyecto, seleccione Agregar referencia.
1. En el cuadro de diálogo Agregar referencia, seleccione Microsoft.Web.Services2.dll.
1. Seleccione System.Web.Services.dll.
1. Haga clic en Seleccionar y, a continuación, en Aceptar.

**Crear una referencia web a un servicio de Forms**

1. En el menú Proyecto, seleccione Agregar referencia Web.
1. En el cuadro de diálogo URL, especifique la URL del servicio de Forms.
1. Haga clic en Ir y, a continuación, en Agregar referencia.

>[!NOTE]
>
>Asegúrese de habilitar el proyecto .NET para utilizar la biblioteca WSE. En el explorador de proyectos, haga clic con el botón derecho en el nombre del proyecto y seleccione Habilitar WSE 2.0. Asegúrese de que la casilla de verificación del cuadro de diálogo que aparece está activada.

**Invocando un servicio mediante DIME en un proyecto .NET**

Puede invocar un servicio de Forms mediante DIME. Considere el proceso `MyApplication/EncryptDocument` que acepta un documento de PDF no protegido y devuelve un documento de PDF cifrado con contraseña. Para invocar el proceso `MyApplication/EncryptDocument` mediante DIME, realice los siguientes pasos:

1. Cree un proyecto de Microsoft .NET que permita invocar un servicio de Forms mediante DIME. Asegúrese de incluir las mejoras de los servicios web 2.0 y de crear una referencia web al servicio de AEM Forms.
1. Después de establecer una referencia web en el proceso `MyApplication/EncryptDocument`, cree un objeto `EncryptDocumentServiceWse` con su constructor predeterminado.
1. Establezca el miembro de datos `Credentials` del objeto `EncryptDocumentServiceWse` con un valor `System.Net.NetworkCredential` que especifique el valor de nombre de usuario y contraseña de los formularios AEM Forms.
1. Cree un objeto `Microsoft.Web.Services2.Dime.DimeAttachment` utilizando su constructor y pasando los siguientes valores:

   * Valor de cadena que especifica un valor GUID. Puede obtener un valor GUID invocando el método `System.Guid.NewGuid.ToString`.
   * Un valor de cadena que especifica el tipo de contenido. Dado que este proceso requiere un documento de PDF, especifique `application/pdf`.
   * Un valor de enumeración `TypeFormat`. Especifique `TypeFormat.MediaType`.
   * Valor de cadena que especifica la ubicación del documento de PDF que se va a pasar al proceso de AEM Forms.

1. Crear un objeto `BLOB` mediante su constructor.
1. Agregue el archivo adjunto DIME al objeto `BLOB` asignando el valor de miembro de datos `Id` del objeto `Microsoft.Web.Services2.Dime.DimeAttachment` al miembro de datos `attachmentID` del objeto `BLOB`.
1. Invoque el método `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` y pase el objeto `Microsoft.Web.Services2.Dime.DimeAttachment`.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `EncryptDocumentServiceWse` y pasando el objeto `BLOB` que contiene el archivo adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Obtenga el valor del identificador de datos adjuntos obteniendo el valor del miembro de datos `attachmentID` del objeto `BLOB` devuelto.
1. Recorra en iteración los datos adjuntos de `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` y utilice el valor del identificador de datos adjuntos para obtener el documento cifrado de PDF.
1. Obtenga un objeto `System.IO.Stream` obteniendo el valor del miembro de datos `Stream` del objeto `Attachment`.
1. Cree una matriz de bytes y pase dicha matriz de bytes al método `Read` del objeto `System.IO.Stream`. Este método rellena la matriz de bytes con una secuencia de datos que representa el documento cifrado de PDF.
1. Cree un objeto `System.IO.FileStream` invocando su constructor y pasando un valor de cadena que represente una ubicación de archivo PDF. Este objeto representa el documento cifrado de PDF.
1. Cree un objeto `System.IO.BinaryWriter` invocando su constructor y pasando el objeto `System.IO.FileStream`.
1. Escriba el contenido de la matriz de bytes en el archivo PDF invocando el método `Write` del objeto `System.IO.BinaryWriter` y pasando la matriz de bytes.

### Creación de clases de proxy Java de Apache Axis que utilicen DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Puede utilizar la herramienta WSDL2Java del eje Apache para convertir un WSDL de servicio en clases de proxy de Java para poder invocar operaciones de servicio. Con Apache Ant, puede generar archivos de biblioteca Axis a partir de un WSDL del servicio AEM Forms que le permite invocar el servicio. (Consulte [Creación de clases de proxy Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).

La herramienta Apache Axis WSDL2Java genera archivos JAVA que contienen métodos que se utilizan para enviar solicitudes de SOAP a un servicio. Las bibliotecas generadas por Axis descodifican las solicitudes de SOAP recibidas por un servicio y las devuelven a los métodos y argumentos.

Para invocar el servicio `MyApplication/EncryptDocument` (que se creó en Workbench) mediante archivos de biblioteca generados por el eje y DIME, realice los siguientes pasos:

1. Cree clases de proxy Java que consuman el WSDL del servicio `MyApplication/EncryptDocument` mediante Apache Axis. (Consulte [Creación de clases de proxy Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).
1. Incluya las clases de proxy Java en la ruta de clase.
1. Crear un objeto `MyApplicationEncryptDocumentServiceLocator` mediante su constructor.
1. Cree un objeto `URL` utilizando su constructor y pasando un valor de cadena que especifique la definición WSDL del servicio AEM Forms. Asegúrese de especificar `?blob=dime` al final de la dirección URL del extremo de SOAP. Por ejemplo, use

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Cree un objeto `EncryptDocumentSoapBindingStub` invocando su constructor y pasando el objeto `MyApplicationEncryptDocumentServiceLocator`y el objeto `URL`.
1. Establezca el valor de nombre de usuario y contraseña de los formularios AEM Forms invocando los métodos `setUsername` y `setPassword` del objeto `EncryptDocumentSoapBindingStub`.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recupere el documento de PDF que se enviará al servicio `MyApplication/EncryptDocument` creando un objeto `java.io.File`. Pase un valor de cadena que especifique la ubicación del documento de PDF.
1. Cree un objeto `javax.activation.DataHandler` utilizando su constructor y pasando un objeto `javax.activation.FileDataSource`. El objeto `javax.activation.FileDataSource` se puede crear utilizando su constructor y pasando el objeto `java.io.File` que representa el documento de PDF.
1. Cree un objeto `org.apache.axis.attachments.AttachmentPart` utilizando su constructor y pasando el objeto `javax.activation.DataHandler`.
1. Adjunte los datos adjuntos invocando el método `addAttachment` del objeto `EncryptDocumentSoapBindingStub` y pasando el objeto `org.apache.axis.attachments.AttachmentPart`.
1. Crear un objeto `BLOB` mediante su constructor. Rellene el objeto `BLOB` con el valor del identificador de datos adjuntos invocando el método `setAttachmentID` del objeto `BLOB` y pasando el valor del identificador de datos adjuntos. Este valor se puede obtener invocando el método `getContentId` del objeto `org.apache.axis.attachments.AttachmentPart`.
1. Invoque el proceso `MyApplication/EncryptDocument` invocando el método `invoke` del objeto `EncryptDocumentSoapBindingStub`. Pase el objeto `BLOB` que contiene el archivo adjunto DIME. Este proceso devuelve un documento PDF cifrado dentro de un objeto `BLOB`.
1. Obtenga el valor del identificador de datos adjuntos invocando el método `getAttachmentID` del objeto `BLOB` devuelto. Este método devuelve un valor de cadena que representa el valor identificador del archivo adjunto devuelto.
1. Recupere los datos adjuntos invocando el método `getAttachments` del objeto `EncryptDocumentSoapBindingStub`. Este método devuelve una matriz de `Objects` que representan los archivos adjuntos.
1. Itere en los datos adjuntos (la matriz `Object`) y utilice el valor del identificador de datos adjuntos para obtener el documento cifrado de PDF. Cada elemento es un objeto `org.apache.axis.attachments.AttachmentPart`.
1. Obtenga el objeto `javax.activation.DataHandler` asociado con el archivo adjunto invocando el método `getDataHandler` del objeto `org.apache.axis.attachments.AttachmentPart`.
1. Obtenga un objeto `java.io.FileStream` invocando el método `getInputStream` del objeto `javax.activation.DataHandler`.
1. Cree una matriz de bytes y pase dicha matriz de bytes al método `read` del objeto `java.io.FileStream`. Este método rellena la matriz de bytes con una secuencia de datos que representa el documento cifrado de PDF.
1. Crear un objeto `java.io.File` mediante su constructor. Este objeto representa el documento cifrado de PDF.
1. Cree un objeto `java.io.FileOutputStream` utilizando su constructor y pasando el objeto `java.io.File`.
1. Invoque el método `write` del objeto `java.io.FileOutputStream` y pase la matriz de bytes que contiene la secuencia de datos que representa el documento cifrado de PDF.

**Consulte también**

[Inicio rápido: Invocar un servicio mediante DIME en un proyecto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Uso de la autenticación basada en SAML {#using-saml-based-authentication}

AEM Forms admite varios modos de autenticación de servicios web al invocar servicios de. Un modo de autenticación especifica un nombre de usuario y un valor de contraseña utilizando un encabezado de autorización básico en la llamada al servicio web. AEM Forms también admite la autenticación basada en aserciones SAML. Cuando una aplicación cliente invoca un servicio de AEM Forms mediante un servicio web, la aplicación cliente puede proporcionar información de autenticación de una de las siguientes maneras:

* Pasar credenciales como parte de la autorización básica
* Pasar el token de nombre de usuario como parte del encabezado WS-Security
* Pasar una aserción SAML como parte del encabezado WS-Security
* Pasar el token Kerberos como parte del encabezado WS-Security

AEM Forms no admite la autenticación estándar basada en certificados, pero sí la autenticación basada en certificados en un formulario diferente.

>[!NOTE]
>
>Los inicios rápidos del servicio web en Programación con AEM Forms especifican los valores de nombre de usuario y contraseña para realizar la autorización.

La identidad de los usuarios de formularios AEM Forms se puede representar mediante una aserción SAML firmada con una clave secreta. El siguiente código XML muestra un ejemplo de una afirmación SAML.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Esta afirmación de ejemplo se emite para un usuario administrador. Esta afirmación contiene los siguientes elementos visibles:

* Es válido durante un tiempo determinado.
* Se emite para un usuario en particular.
* Está firmado digitalmente. Así que cualquier modificación que se le haga romperá la firma.
* Se puede presentar a AEM Forms como un token de identidad del usuario similar al nombre de usuario y la contraseña.

Una aplicación cliente puede recuperar la aserción desde cualquier API de AEM Forms AuthenticationManager que devuelva un objeto `AuthResult`. Puede obtener una instancia de `AuthResult` mediante uno de los dos métodos siguientes:

* Autenticar al usuario mediante cualquiera de los métodos de autenticación expuestos por la API AuthenticationManager. Normalmente, se utiliza el nombre de usuario y la contraseña; sin embargo, también se puede utilizar la autenticación de certificado.
* Usando el método `AuthenticationManager.getAuthResultOnBehalfOfUser`. Este método permite que una aplicación cliente obtenga un objeto `AuthResult` para cualquier usuario de formularios AEM Forms.

Un usuario de formularios AEM Forms se puede autenticar mediante un token SAML obtenido. Esta afirmación de SAML (fragmento xml) se puede enviar como parte del encabezado WS-Security con la llamada del servicio web para la autenticación de usuarios. Normalmente, una aplicación cliente ha autenticado a un usuario, pero no ha almacenado sus credenciales. (O el usuario ha iniciado sesión en ese cliente a través de un mecanismo que no sea el uso de un nombre de usuario y una contraseña). En este caso, la aplicación cliente debe invocar AEM Forms y suplantar a un usuario específico que puede invocar AEM Forms.

Para suplantar a un usuario específico, invoque el método `AuthenticationManager.getAuthResultOnBehalfOfUser` mediante un servicio web. Este método devuelve una instancia `AuthResult` que contiene la aserción SAML para ese usuario.

A continuación, utilice esa afirmación de SAML para invocar cualquier servicio que requiera autenticación. Esta acción implica enviar la afirmación como parte del encabezado de SOAP. Cuando se realiza una llamada al servicio web con esta afirmación, AEM Forms identifica al usuario como el representado por esa afirmación. Es decir, el usuario especificado en la afirmación es el usuario que invoca el servicio.

### Uso de clases Apache Axis y autenticación basada en SAML {#using-apache-axis-classes-and-saml-based-authentication}

Puede invocar un servicio de AEM Forms mediante las clases de proxy de Java que se crearon con la biblioteca de Axis. (Consulte [Creación de clases de proxy Java mediante Apache Axis](#creating-java-proxy-classes-using-apache-axis)).

Cuando utilice AXIS que utilice autenticación basada en SAML, registre el controlador de solicitud y respuesta con Axis. Apache Axis invoca el controlador antes de enviar una solicitud de invocación a AEM Forms. Para registrar un controlador, cree una clase Java que extienda `org.apache.axis.handlers.BasicHandler`.

**Crear un AssertionHandler con Axis**

La siguiente clase Java, denominada `AssertionHandler.java`, muestra un ejemplo de una clase Java que extiende `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registrar el controlador**

Para registrar un controlador con Axis, cree un archivo client-config.wsdd. De forma predeterminada, Axis busca un archivo con este nombre. El siguiente código XML es un ejemplo de archivo client-config.wsdd. Consulte la documentación de Axis para obtener más información.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Invocar un servicio de AEM Forms**

El siguiente ejemplo de código invoca un servicio de AEM Forms mediante autenticación basada en SAML.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Utilizar un ensamblado de cliente .NET y autenticación basada en SAML {#using-a-net-client-assembly-and-saml-based-authentication}

Puede invocar un servicio Forms utilizando un ensamblado de cliente .NET y autenticación basada en SAML. Para ello, debe utilizar las Mejoras del servicio web 3.0 (WSE). Para obtener información sobre cómo crear un ensamblado de cliente .NET que utilice WSE, vea [Crear un proyecto .NET que utilice DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>La sección DIME utiliza WSE 2.0. Para utilizar la autenticación basada en SAML, siga las mismas instrucciones especificadas en el tema DIME. Sin embargo, reemplace WSE 2.0 por WSE 3.0. Instale las mejoras de los servicios web 3.0 en el equipo de desarrollo e integre la versión con Microsoft Visual Studio .NET. Puede descargar las mejoras de los servicios web 3.0 desde el [Centro de descarga de Microsoft](https://www.microsoft.com/downloads/search.aspx).

La arquitectura WSE utiliza los tipos de datos Políticas, Afirmaciones y SecurityToken. En resumen, para una llamada al servicio web, especifique una directiva. Una directiva puede tener varias aserciones. Cada aserción puede contener filtros. Se invoca un filtro en determinadas fases de una llamada al servicio web y, en ese momento, pueden modificar la solicitud de SOAP. Para obtener más información, consulte la documentación de Mejoras del servicio web 3.0.

**Crear la afirmación y el filtro**

En el siguiente ejemplo de código de C# se crean clases de filtro y aserción. En este ejemplo de código se crea un SamlAssertionOutputFilter. El marco WSE invoca este filtro antes de enviar la solicitud de SOAP a AEM Forms.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Crear el token de SAML**

Cree una clase para representar la afirmación de SAML. La tarea principal que realiza esta clase es convertir los valores de datos de cadena a xml y conservar el espacio en blanco. Este xml de aserción se importa posteriormente a la solicitud de SOAP.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Invocar un servicio de AEM Forms**

El siguiente ejemplo de código de C# invoca un servicio de Forms mediante la autenticación basada en SAML.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Consideraciones relacionadas al utilizar servicios web {#related-considerations-when-using-web-services}

A veces, se producen problemas al invocar ciertas operaciones de servicios de AEM Forms mediante servicios web. El objetivo de este debate es identificar esas cuestiones y proporcionar una solución, si se dispone de una.

### Invocación asincrónica de operaciones de servicio {#invoking-service-operations-asynchronously}

Si intenta invocar asincrónicamente una operación del servicio AEM Forms, como la operación Generate PDF `htmlToPDF`, se produce un `SoapFaultException`. Para resolver este problema, cree un archivo XML de enlace personalizado que asigne el elemento `ExportPDF_Result` y otros elementos a diferentes clases. El siguiente XML representa un archivo de enlace personalizado.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Utilice este archivo XML al crear archivos proxy Java mediante JAX-WS. (Consulte [Creación de clases de proxy Java mediante JAX-WS](#creating-java-proxy-classes-using-jax-ws)).

Haga referencia a este archivo XML al ejecutar la herramienta JAX-WS (wsimport.exe) mediante la opción de línea de comandos - `b`. Actualice el elemento `wsdlLocation` en el archivo XML de enlace para especificar la dirección URL de AEM Forms.

Para asegurarse de que la invocación asincrónica funciona, modifique el valor de la dirección URL de punto final y especifique `async=true`. Por ejemplo, para los archivos proxy Java creados con JAX-WS, especifique lo siguiente para `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

La siguiente lista especifica otros servicios que necesitan un archivo de enlace personalizado cuando se invocan asincrónicamente:

* PDFG3D
* Administrador de tareas
* Administrador de aplicaciones
* Administrador de directorios
* Distiller
* Rights Management
* Administración de documentos

### Diferencias en los servidores de aplicaciones J2EE {#differences-in-j2ee-application-servers}

A veces, una biblioteca proxy creada con un servidor de aplicaciones J2EE específico no invoca correctamente AEM Forms alojado en un servidor de aplicaciones J2EE diferente. Considere una biblioteca proxy generada con AEM Forms que se implementa en WebSphere. Esta biblioteca proxy no puede invocar correctamente los servicios de AEM Forms implementados en el servidor de aplicaciones JBoss.

Algunos tipos de datos complejos de AEM Forms, como `PrincipalReference`, se definen de forma diferente cuando AEM Forms se implementa en WebSphere en comparación con el servidor de aplicaciones JBoss. Las diferencias en los JDK utilizados por los distintos servicios de aplicaciones J2EE son la razón por la que hay diferencias en las definiciones de WSDL. Como resultado, utilice bibliotecas proxy generadas desde el mismo servidor de aplicaciones J2EE.

### Acceder a varios servicios mediante servicios web {#accessing-multiple-services-using-web-services}

Debido a conflictos de área de nombres, los objetos de datos no se pueden compartir entre varios WSDL de servicio. Los distintos servicios pueden compartir tipos de datos y, por lo tanto, comparten la definición de estos tipos en los WSDL. Por ejemplo, no se pueden agregar dos ensamblados cliente .NET que contengan un tipo de datos `BLOB` al mismo proyecto cliente .NET. Si intenta hacerlo, se produce un error de compilación.

La siguiente lista especifica los tipos de datos que no se pueden compartir entre varios WSDL de servicio:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Para evitar este problema, se recomienda clasificar completamente los tipos de datos. Por ejemplo, considere una aplicación .NET que haga referencia al servicio Forms y al servicio Signature mediante una referencia de servicio. Ambas referencias de servicio contendrán una clase `BLOB`. Para usar una instancia de `BLOB`, active completamente el objeto `BLOB` cuando lo declare. Este método se muestra en el ejemplo de código siguiente. Para obtener información sobre este ejemplo de código, vea [Firmar digitalmente Forms interactivo](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

El siguiente ejemplo de código de C# firma un formulario interactivo que procesa el servicio de Forms. La aplicación cliente tiene dos referencias de servicio. La instancia `BLOB` asociada al servicio Forms pertenece al espacio de nombres `SignInteractiveForm.ServiceReference2`. Del mismo modo, la instancia de `BLOB` asociada al servicio Signature pertenece al espacio de nombres `SignInteractiveForm.ServiceReference1`. El formulario interactivo firmado se guardará como un archivo de PDF denominado *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify an XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify an XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### Los servicios que comienzan con la carta generan archivos proxy no válidos {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

El nombre de algunas clases de proxy generadas por AEM Forms son incorrectos cuando se utilizan Microsoft .Net 3.5 y WCF. Este problema se produce cuando se crean clases de proxy para IBMFilenetContentRepositoryConnector, IDPSchedulerService o cualquier otro servicio cuyo nombre comience por la letra I. Por ejemplo, el nombre del cliente generado si hay IBMFileNetContentRepositoryConnector es `BMFileNetContentRepositoryConnectorClient`. Falta el ID de carta en la clase de proxy generada.
