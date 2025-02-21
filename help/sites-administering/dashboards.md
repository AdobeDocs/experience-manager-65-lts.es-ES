---
title: Paneles de control
description: Aprenda a crear, configurar y desarrollar nuevos paneles de AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 3%

---

# Paneles de control{#dashboards}

Al utilizar AEM, puede administrar numerosos contenidos de diferentes tipos (por ejemplo, páginas o recursos). Los paneles de AEM proporcionan una forma fácil de usar y personalizable de definir páginas que muestren datos consolidados.

>[!NOTE]
>
>Los paneles de AEM se crean por usuario, de modo que el usuario solo puede acceder a su propio panel.
>
>Sin embargo, [las plantillas de panel](#creating-a-dashboard-template) se pueden usar para compartir la configuración común y el diseño de panel.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Administración de tableros {#administering-dashboards}

### Creación De Un Tablero {#creating-a-dashboard}

1. En la sección **Herramientas**, haga clic en **Consola de configuración**.
1. En el árbol, haga doble clic en **Panel**.
1. Haga clic en **Nuevo panel**.
1. Escriba **Title** (por ejemplo, Mi panel) y **Name**.
1. Haga clic en **Crear**.

### Clonación De Un Tablero {#cloning-a-dashboard}

Es posible que desee tener varios paneles para ver rápidamente información sobre el contenido de diferentes vistas. Para ayudarle a crear un nuevo panel, AEM proporciona una función de clonación que puede utilizar para duplicar un panel existente. Para clonar un tablero, siga estos pasos:

1. En la sección **Herramientas**, haga clic en **Consola de configuración**.

1. En el árbol, haga clic en **Panel**.
1. Haga clic en el tablero que desee clonar.

1. Haga clic en **Clonar**.

1. Escriba **Name** de su nuevo tablero.

### Eliminación De Un Tablero {#removing-a-dashboard}

1. En la sección **Herramientas**, haga clic en **Consola de configuración**.

1. En el árbol, haga clic en **Panel**.
1. Haga clic en el tablero que desee eliminar.

1. Haga clic en **Quitar**.

1. Haga clic en **Sí** para confirmar.

## Componentes del panel {#dashboard-components}

### Información general {#overview}

Los componentes del panel no son más que [componentes de AEM](/help/sites-developing/developing-components-samples.md) normales. En esta sección se describen los componentes de sistema de informes que se envían con AEM.

### Componentes de informes de análisis web {#web-analytics-reporting-components}

AEM se distribuye con un conjunto de componentes que procesan varias métricas de sus datos de [SiteCatalyst](/help/sites-administering/adobeanalytics.md). Estos componentes se enumeran en Sidekick en la sección **Panel**.

Cada componente del sistema de informes proporciona al menos tres pestañas:

* **Básico**: contiene la configuración principal.

* **Informe:** contiene la configuración específica de cada informe.
* **Style**: contiene la configuración de estilo como el tamaño y el margen del gráfico.

Los componentes de creación de informes se inicializan con una configuración predeterminada que le ayuda a configurar rápidamente el panel.

#### Configuración básica {#basic-configuration}

La ficha **Básico** proporciona acceso a las siguientes entradas de configuración:

**Título**: el título se muestra en el panel.

**Tipo de solicitud** Forma en que se solicitan los datos.

**Configuración de SiteCatalyst (opcional)** La configuración que desea usar para conectarse a SiteCatalyst. Si no se proporciona, se supone que la configuración está configurada en la página Tablero (a través de las propiedades de página).

**ID del grupo de informes (opcional)** El grupo de informes de SiteCatalyst que desea utilizar para generar el gráfico.

#### Configuración del informe {#report-configuration}

Para mostrar las estadísticas web, debe definir el intervalo de fechas de los datos que desea recuperar. La ficha **Informe** proporciona dos campos para definir ese intervalo.

>[!NOTE]
>
>La configuración de un intervalo de fechas grande puede disminuir la capacidad de respuesta del panel.

**Fecha desde** Fecha absoluta o relativa desde la cual se recuperaron los datos.

**Fecha hasta** fecha absoluta o relativa a la que se recuperaron los datos.

Cada componente también define configuraciones específicas.

#### Informe de tiempo extra {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularidad de fecha** unidad de tiempo del eje X (por ejemplo, día, hora).

**Métricas** La lista de eventos que desea mostrar.

**Elementos** Lista de elementos que desglosa los datos de métricas en el gráfico.

#### Informe de lista clasificada {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementos**: el elemento que desglosa los datos de las métricas en el gráfico.

**Métricas**: el evento que desea mostrar.

**No. de elementos principales**: número de elementos mostrados por el informe.

#### Informe clasificado {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Métricas**: el evento que desea mostrar.

**Elementos**: el elemento que desglosa los datos de las métricas en el gráfico.

#### Informe de sección de sitio principal {#top-site-section-report}

Este componente muestra un gráfico con la sección más visitada de un sitio web según la siguiente configuración.

![chlimage_1-29](assets/chlimage_1-29a.png)

**No. de los elementos principales** Número de sección mostrada por en el informe.

#### Informe de tendencias {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularidad de fecha** unidad de tiempo del eje X (por ejemplo, día, hora).

**Métricas**: el evento que desea mostrar.

**Elementos**: el elemento que desglosa los datos de las métricas en el gráfico.

## Ampliación del panel {#extending-dashboard}

### Información general {#overview-1}

Los paneles son páginas normales ( `cq:Page`), por lo tanto, cualquier componente se puede utilizar para ensamblar paneles.

Hay un grupo de componentes predeterminado `Dashboard` que contiene componentes de informes de Analytics que están habilitados en la plantilla de forma predeterminada.

### Creación De Una Plantilla De Tablero {#creating-a-dashboard-template}

Una plantilla define el contenido predeterminado de un nuevo panel. Puede utilizar varias plantillas para crear diferentes tipos de paneles.

Las plantillas de tablero se crean como otras plantillas de página, excepto que se almacenan en `/libs/cq/dashboards/templates/`. Consulte la sección [Creando plantilla de página de contenido](/help/sites-developing/website.md#creating-the-contentpage-template).

>[!NOTE]
>
>Las plantillas de panel se comparten entre los usuarios.

### Desarrollo de un componente de panel {#developing-a-dashboard-component}

El desarrollo de un componente Panel consiste en crear un componente de AEM normal. En esta sección se describe un ejemplo de un componente que muestra los 10 principales colaboradores.

![chlimage_1-31](assets/chlimage_1-31a.png)

Los componentes de autor principales se almacenan en el repositorio en `/apps/geometrixx-outdoors/components/reporting` y están compuestos por:

1. un archivo `jsp` que lee datos jcr y define el marcador de posición `html`.

1. una biblioteca del lado del cliente que contiene un archivo de `js` que obtiene y ordena los datos y, a continuación, rellena el marcador de posición `html`.

![chlimage_1-32](assets/chlimage_1-32a.png)

El siguiente archivo JavaScript está definido en la `geout.reporting.topauthors` [Biblioteca de cliente](/help/sites-developing/clientlibs.md) como elemento secundario del componente en sí.

[QueryBuilder](/help/sites-developing/querybuilder-api.md) se usa para consultar el repositorio y leer `cq:AuditEvent` nodos. El resultado de la consulta es un objeto JSON del que se extraen las contribuciones de los autores.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

`JSP` incluye `global.jsp` y `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
