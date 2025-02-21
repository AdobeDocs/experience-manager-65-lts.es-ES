---
title: API del servicio de información del sistema
description: Este documento proporciona información detallada sobre las API proporcionadas por el servicio de información del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 3%

---

# API del servicio de información del sistema {#system-information-service-apis}

El servicio de información del sistema proporciona un conjunto de API de REST para recuperar información. La siguiente tabla proporciona información detallada sobre las API:

<table>
 <thead>
  <tr>
   <th><p>Nombre</p></th>
   <th><p>URL</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>Esta API es un contenedor para la API de Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Recupera la configuración del entorno de trabajo actual. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera todas las variables de entorno del sistema operativo del host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Descarga un archivo zip que contiene los registros del servidor de aplicaciones. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera todo el contenido del archivo config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera el estado y los parámetros de configuración de los servicios de AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Recupera el tiempo activo del servidor, los argumentos de JVM, la memoria del sistema, el tamaño de la pila, el nombre del sistema operativo, el número de subprocesos activos y el recuento de subprocesos. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera valores de las siguientes propiedades:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposeTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>Habilitar FIPS</p></li>
     <li><p>Habilitar WSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Recupera información detallada sobre la base de datos.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Recupera la información de versión y licencia de los componentes de formularios AEM instalados. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Descarga archivos de configuración del servidor de aplicaciones host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera el recuento y el seguimiento de pila de los subprocesos activos. Acepta los siguientes parámetros:</p>
    <ul>
     <li><p>iterations= [n]: especifica el número de iteraciones. Sustituya n por un número. </p></li>
     <li><p>Delay= [n]: especifica el número de milisegundos que hay que esperar antes de iniciar la siguiente iteración. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Esta API es un contenedor para todas las API del servicio de información del sistema. Internamente, ejecuta todas las API de información del sistema y descarga la información en formato zip. </p><p><i><strong>nota</strong>: SystemInfo.info no proporciona seguimiento de recuento y pila de los subprocesos activos. </i></p></td>
  </tr>
 </tbody>
</table>
