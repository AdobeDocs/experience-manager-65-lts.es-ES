---
title: Optimizar formularios HTML5
description: Puede optimizar el tamaño de salida de los formularios HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 100%

---

# Optimizar formularios HTML5 {#optimizing-html-forms}

Los formularios HTML5 procesan los formularios en formato HTML5. Dependiendo de factores como el tamaño del formulario y las imágenes que este contiene, la salida resultante puede tener un gran tamaño. El método recomendado para optimizar la transferencia de datos es comprimir la respuesta del HTML mediante el servidor web desde el que se suministra la solicitud. Este método reduce el tamaño de la respuesta, el tráfico de red y el tiempo necesario para transmitir los datos entre los equipos cliente y servidor.

Este artículo describe los pasos necesarios para habilitar la compresión en Apache Web Server 2.0 de 32 bits con JBoss.

>[!NOTE]
>
>Las siguientes instrucciones no se aplican a servidores distintos de Apache Web Server 2.0 de 32 bits.

Obtenga el software del servidor web Apache aplicable a su sistema operativo:

* En Windows, descargue el servidor web de Apache del sitio del proyecto Apache HTTP Server.
* En Solaris de 64 bits, descargue el servidor web Apache desde el sitio web de Sunfreeware para Solaris.
* En Linux, el servidor web Apache está preinstalado en el sistema.

Apache puede comunicarse con JBoss mediante HTTP o el protocolo AJP.

1. Elimine los comentarios de las siguientes configuraciones de módulo en el archivo *APACHE_HOME/conf/httpd.conf*.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >En Linux, el directorio APACHE_HOME predeterminado es /etc/httpd/.

1. Configure el proxy en el puerto 8080 de JBoss.

   Agregue la siguiente configuración al archivo de configuración *APACHE_HOME/conf/httpd.conf*.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Cuando utiliza un proxy, se requieren los siguientes cambios de configuración:
   >
   >* Acceso: *https://&lt;server>:&lt;port>/system/console/configMgr*.
   * Edite la configuración del Filtro de referente de Apache Sling.
   * En Permitir hosts, añada la entrada para el servidor proxy.

1. Habilite la Compresión.

   Agregue la siguiente configuración al archivo de configuración *APACHE_HOME/conf/httpd.conf*.

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Para acceder al servidor de AEM, utilice https://[Apache_server]:80.
