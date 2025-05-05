---
title: Superposiciones
description: Adobe Experience Manager utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Superposiciones{#overlays}

Adobe Experience Manager (AEM), y antes de eso, CQ, ha usado por mucho tiempo el principio de las superposiciones para permitirle ampliar y personalizar las [consolas](/help/sites-developing/customizing-consoles-touch.md) y otras funcionalidades (por ejemplo, [creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)).

Superposición es un término que se utiliza en muchos contextos. En este contexto (ampliación de AEM), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la rama `/apps`. AEM usa una ruta de búsqueda para encontrar un recurso, buscando primero la rama `/apps` y luego la rama `/libs` (la ruta de búsqueda [se puede configurar](#configuring-the-search-paths)). Este mecanismo significa que la superposición (y las personalizaciones definidas) tienen prioridad.

Desde AEM 6.0, se han realizado cambios en la implementación y el uso de las superposiciones:

* AEM 6.0 y posteriores: para superposiciones relacionadas con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) (es decir, la IU táctil)

   * Método

      * Reconstruir la estructura `/libs` adecuada en `/apps`.

        Esto no requiere una copia 1:1; se usa la [fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) para hacer referencia a las definiciones originales que se requieren. La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos con mecanismos de diferencia.

      * En `/apps`, realice cualquier cambio.

   * Ventajas

      * Más seguro para los cambios en `/libs`.
      * Redefina solo lo que sea necesario.

* Superposiciones y superposiciones que no son de Granite antes de AEM 6.0

   * Método

      * Copiar el contenido de `/libs` a `/apps`

        Copie toda la subrama, incluidas las propiedades.

      * En `/apps`, realice cualquier cambio.

   * Desventajas

      * Aunque los cambios no se perderán cuando algo cambie en `/libs`, es posible que tenga que volver a crear ciertos cambios que se producen en la superposición en `/apps`.

>[!CAUTION]
>
>La [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y los métodos relacionados solo se pueden usar con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esto significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la IU táctil estándar.
>
>Las superposiciones de otras áreas (incluida la IU clásica) implican copiar el nodo adecuado y toda la subestructura y, a continuación, realizar los cambios necesarios.

Las superposiciones son el método recomendado para muchos cambios, como [configurar las consolas](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [crear la categoría de selección en el explorador de recursos del panel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilizado al crear páginas). Se requieren como sigue:

* ***No* realice cambios en la rama `/libs`**&#x200B;Cualquier cambio que realice podría perderse, ya que esta rama puede cambiar siempre que haga lo siguiente:

   * actualice en su instancia
   * aplicar una revisión
   * instalación de un paquete de funciones

* Concentran los cambios en una ubicación, lo que facilita el seguimiento, la migración, la copia de seguridad o la depuración de los cambios, según sea necesario.

## Configuración de las rutas de búsqueda {#configuring-the-search-paths}

En el caso de las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda que se puedan definir:

* El recurso **Ruta de búsqueda de Resolver** según se define en la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) para la **fábrica de Apache Sling Resource Resolver**.

   * El orden descendente de las rutas de búsqueda indica sus respectivas prioridades.
   * En una instalación estándar, los valores predeterminados principales son `/apps`, `/libs`, por lo que el contenido de `/apps` tiene una prioridad mayor que la de `/libs` (es decir, lo *superpone*).

* Dos usuarios del servicio necesitan acceso JCR:READ a la ubicación donde se almacenan los scripts. Estos usuarios son: components-search-service (utilizado por los componentes com.day.cq.wcm.core access/cache) y sling-scripting (utilizado por org.apache.sling.servlets.resolver para buscar servlets).
* La siguiente configuración también debe configurarse según dónde coloque los scripts (en este ejemplo, en /etc, /libs o /apps).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* Finalmente, también se debe configurar el Servlet Resolver (en este ejemplo, para añadir /etc a)

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## Ejemplo de uso {#example-of-usage}

Algunos ejemplos se tratan cuando:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)
