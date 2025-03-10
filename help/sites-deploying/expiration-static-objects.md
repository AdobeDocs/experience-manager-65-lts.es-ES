---
title: Caducidad de objetos estáticos
description: Aprenda a configurar Adobe Experience Manager para que los objetos estáticos no caduquen (durante un período de tiempo razonable).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: a279ebed-a116-4719-989e-1b2f79f6caa4
source-git-commit: f145e5f0d70662aa2cbe6c8c09795ba112e896ea
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Caducidad de objetos estáticos{#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, los iconos) no cambian. Por lo tanto, el sistema debe configurarse para que no caduque (durante un periodo de tiempo razonable) y, por lo tanto, reducir el tráfico innecesario.

Esto tiene el siguiente impacto:

* Descarga solicitudes desde la infraestructura del servidor.
* Aumenta el rendimiento de la carga de páginas, ya que el explorador almacena en caché los objetos de la caché del explorador.

El estándar HTTP especifica las caducidades con respecto a la &quot;caducidad&quot; de los archivos (por ejemplo, consulte el capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;). Este estándar utiliza el encabezado para permitir a los clientes almacenar en caché los objetos hasta que se consideren obsoletos; dichos objetos se almacenan en caché durante el tiempo especificado sin que se realice ninguna comprobación de estado en el servidor de origen.

>[!NOTE]
>
>Esta configuración es independiente de (y no funcionará para) Dispatcher.
>
>El propósito de Dispatcher es almacenar en caché los datos delante de Adobe Experience Manager (AEM).

Todos los archivos, que no son dinámicos y que no cambian con el tiempo, se pueden y deben almacenar en caché. La configuración del servidor HTTPD de Apache podría parecerse a una de las siguientes opciones, según el entorno:

>[!CAUTION]
>
>Tenga cuidado al definir el período de tiempo durante el cual se considera que un objeto está actualizado. Como no hay *ninguna comprobación hasta que haya transcurrido el período de tiempo especificado*, el cliente puede terminar presentando contenido antiguo de la caché.

1. **Para una instancia de autor:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Esto permite que la caché intermedia (por ejemplo, la caché del explorador) almacene archivos CSS, JavaScript, PNG y GIF durante un máximo de un mes, hasta que caduquen. Esto significa que no es necesario solicitarlas a AEM o al servidor web, pero pueden permanecer en la memoria caché del explorador.

   Otras secciones del sitio no deben almacenarse en caché en una instancia de autor, ya que están sujetas a cambios en cualquier momento.

1. **Para una instancia de publicación:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   Esto permite que la caché intermedia (por ejemplo, la caché del explorador) almacene archivos CSS, JavaScript, PNG y GIF durante un máximo de un día en las cachés de cliente. Aunque este ejemplo ilustra la configuración global de todo lo que está por debajo de `/content` y `/etc/designs`, debería hacerlo más granular.

   Dependiendo de la frecuencia con la que se actualice el sitio, también puede considerar almacenar en caché las páginas de HTML. Un período de tiempo razonable sería de una hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Después de configurar los objetos estáticos, analice `request.log`, mientras selecciona las páginas que contienen dichos objetos, para confirmar que no se realizan solicitudes (innecesarias) de objetos estáticos.
