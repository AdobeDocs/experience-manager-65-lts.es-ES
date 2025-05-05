---
title: Implementación de la nomenclatura de páginas del lado del servidor para Analytics
description: Adobe Analytics utiliza la propiedad s.pageName para identificar las páginas de forma exclusiva y asociar los datos recopilados para las páginas
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Implementación de la nomenclatura de páginas del lado del servidor para Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utiliza la propiedad `s.pageName` para identificar las páginas de forma única y asociar los datos que se recopilan para las páginas. Normalmente, se realizan las siguientes tareas en AEM para asignar un valor a esta propiedad que AEM envía a Analytics:

* Utilice el marco del servicio en la nube de Analytics para asignar una variable CQ a la propiedad `s.pageName` de Analytics. (Consulte [Asignación de datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)).

* Diseñe el componente de página para que incluya la variable CQ que asigne a la propiedad `s.pageName`. (Consulte [Implementación del seguimiento de Adobe Analytics para componentes personalizados](/help/sites-developing/extending-analytics-components.md)).

Para exponer los datos de los informes de Analytics en la consola Sitios y en la perspectiva de contenido, AEM requiere el valor de la propiedad `s.pageName` para cada página. La API de Java de AEM Analytics define la interfaz `AnalyticsPageNameProvider` que implementa para proporcionar a la consola Sitios y a las Perspectivas de contenido el valor de la propiedad `s.pageName`. El servicio `AnaltyicsPageNameProvider` resuelve la propiedad pageName en el servidor con fines de generación de informes, ya que se puede establecer dinámicamente usando JavaScript en el cliente con fines de seguimiento.

## El servicio de proveedor de nombres de páginas predeterminado de Analytics {#the-default-analytics-page-name-provider-service}

El servicio `DefaultPageNameProvider` es el servicio predeterminado que determina el valor de la propiedad `s.pageName` que se utilizará para recuperar datos de Analytics para una página. El servicio funciona junto con el componente de página de base de AEM ( `/libs/foundation/components/page`). Este componente de página define las siguientes variables de CQ que deben asignarse a la propiedad `s.pageName`:

* `pagedata.path`: el valor se establece en la ruta de acceso de la página.
* `pagedata.title`: el valor se establece en el título de la página.
* `pagedata.navTitle`: el valor se establece en el título de navegación de la página.

El servicio `DefaultPageNameProvider` determina cuál de estas variables CQ se asigna a la propiedad `s.pageName` en el marco del servicio en la nube de Analytics. A continuación, el servicio determina la propiedad de página adecuada que se utilizará para recuperar los datos del informe de análisis:

* `pagedata.path`: el servicio usa `page.getPath()`

* `pagedata.title`: el servicio usa `page.getTitle()`

* `pagedata.navTitle`: el servicio usa `page.getNavigationTitle()`

El objeto `page` es el objeto Java [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/es/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) para la página.

Si no asigna una variable CQ a la propiedad `s.pageName` en el marco de trabajo, el valor de `s.pageName` se genera a partir de la ruta de acceso de la página. Por ejemplo, la página con la ruta de acceso `/content/geometrixx/en` usa el valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>El servicio DefaultPageNameProvider utiliza una clasificación de servicio de 100.

## Mantenimiento de la continuidad en informes de Analytics {#maintaining-continuity-in-analytics-reporting}

Para mantener un historial completo de los datos de análisis de una página, es necesario que el valor de la propiedad s.pageName que se utiliza para una página no cambie nunca. Sin embargo, las propiedades de análisis que define el componente de página de base se pueden cambiar fácilmente. Por ejemplo, al mover una página se cambia el valor de `pagedata.path` y se interrumpe la continuidad del historial de informes:

* Los datos recopilados para la ruta anterior ya no están asociados con la página.
* Si una página diferente utiliza la ruta que otra página utilizó una vez, la página diferente hereda los datos de esa ruta.

Para garantizar la continuidad de la creación de informes, el valor de `s.pageName` debe tener las siguientes características:

* Único.
* Estable.
* Legible en lenguaje natural.

Por ejemplo, un componente de página personalizado puede incluir una propiedad de página que los autores utilizan para especificar un identificador único para la página que se utiliza como valor de la propiedad `s.pageProperties`:

* La página incluye una variable de análisis que se establece en el valor del ID único almacenado en la propiedad de página.
* La variable de Analytics está asignada a la propiedad `s.pageProperties` en el marco de Analytics.
* La implementación de la interfaz AnalyticsPageNameProvider recupera el valor de la propiedad de página que se utilizará para consultar los datos de Analytics de la página.

>[!NOTE]
>
>Pida ayuda a su consultor de Analytics para desarrollar una estrategia eficaz para su valor `s.pageName`.

### Implementación de un servicio de proveedor de nombres de páginas de Analytics {#implementing-an-analytics-page-name-provider-service}

Implemente la interfaz `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` como servicio OSGi para personalizar la lógica que recupera el valor de propiedad `s.pageName`. El análisis de página de Sites y la perspectiva de contenido utilizan el servicio para recuperar datos de informes de Analytics.

La interfaz AnalyticsPageNameProvider define dos métodos que debe implementar:

* `getPageName`: devuelve un valor `String` que representa el valor que se va a usar como propiedad `s.pageName`.

* `getResource`: devuelve un objeto `org.apache.sling.api.resource.Resource` que representa la página asociada a la propiedad `s.pageName`.

Ambos métodos toman un objeto `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` como parámetro. La clase `AnalyticsPageNameContext` proporciona información sobre el contexto de las llamadas de Analytics:

* Ruta base del recurso de página.
* El objeto `Framework` para la configuración del servicio de nube de Analytics.
* El objeto `Resource` de la página.
* El objeto `ResourceResolver` de la página.

La clase también proporciona un establecedor para el nombre de página.

### Ejemplo de implementación de AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

La siguiente implementación de ejemplo `AnalyticsPageNameProvider` es compatible con un componente de página personalizado:

* El componente amplía el componente de página de base.
* El cuadro de diálogo incluye un campo que los autores utilizan para especificar el valor de la propiedad `s.pageName`.
* El valor de la propiedad se almacena en la propiedad pageName del nodo `jcr:content` de las instancias de página.
* La propiedad de Analytics que almacena la propiedad `s.pageName` se llama `pagedata.pagename`. Esta propiedad está asignada a la propiedad `s.pageName` en el marco de Analytics.

La siguiente implementación del método `getPageName` devuelve el valor de la propiedad del nodo pageName si la asignación de marco de trabajo está configurada correctamente:

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

La implementación siguiente del método getResource devuelve el objeto Resource para la página:

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

El siguiente código representa toda la clase, incluidas las anotaciones SCR que configuran el servicio. La clasificación del servicio es 200, que anula el servicio predeterminado.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
