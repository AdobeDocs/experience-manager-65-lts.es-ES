---
title: Añadir el seguimiento de Adobe Analytics a los componentes
description: Aprenda a añadir el seguimiento de Adobe Analytics a los componentes de Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# Añadir el seguimiento de Adobe Analytics a los componentes{#adding-adobe-analytics-tracking-to-components}

## Inclusión del módulo Adobe Analytics en un componente de página {#including-the-adobe-analytics-module-in-a-page-component}

Los componentes de plantilla de página (por ejemplo, `head.jsp, body.jsp`) necesitan que JSP incluya para cargar ContextHub y la integración de Adobe Analytics (que forma parte de Cloud Services). Todo incluye la carga de archivos JavaScript.

La entrada de ContextHub debe incluirse inmediatamente debajo de la etiqueta `<head>`, mientras que Cloud Services debe incluirse en la sección `<head>` y antes de la sección `</body>`; por ejemplo:

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

El script `contexthub` que se inserta después del elemento `<head>` agrega las características de ContextHub a la página.

Los scripts `cloudservices` que agrega en las secciones `<head>` y `<body>` se aplican a las configuraciones de servicios en la nube que se agregan a la página. (Si la página utiliza más de una configuración de Cloud Services, debe incluir el jsp de ContextHub y el jsp de Cloud Services solo una vez).

Cuando se agrega un marco de trabajo de Adobe Analytics a la página, los scripts de `cloudservices` generan JavaScript relacionado con Adobe Analytics y referencias a bibliotecas del lado del cliente, de forma similar al siguiente ejemplo:

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

Todos los sitios de muestra de AEM, como Geometrixx Outdoors, tienen este código incluido.

### El evento SiteCatalystAfterCollect {#the-sitecatalystaftercollect-event}

El script `cloudservices` almacena en déclencheur el evento `sitecatalystAfterCollect`:

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

Este evento se activa para indicar que se ha completado el seguimiento de la página. Si está realizando operaciones de seguimiento adicionales en esta página, debe escuchar este evento en lugar del evento de carga de documento o de documento listo. El uso del evento `sitecatalystAfterCollect` evita conflictos u otros comportamientos impredecibles.

>[!NOTE]
>
>La biblioteca `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` incluye el código del archivo `s_code.js` de Adobe Analytics.

## Implementación del seguimiento de Adobe Analytics para componentes personalizados {#implementing-adobe-analytics-tracking-for-custom-components}

Habilite los componentes de AEM para interactuar con el marco de trabajo de Adobe Analytics. A continuación, configure el marco de trabajo para que Adobe Analytics realice un seguimiento de los datos del componente.

Los componentes que interactúan con el marco de trabajo de Adobe Analytics aparecen en Sidekick cuando edita un marco de trabajo. Después de arrastrar el componente al marco de trabajo, aparecen las propiedades del componente y puede asignarlas con las propiedades de Adobe Analytics. (Consulte [Configuración de un marco de trabajo para el seguimiento básico](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework)).

Los componentes pueden interactuar con el marco de Adobe Analytics cuando el componente tiene un nodo secundario denominado `analytics`. El nodo `analytics` tiene las siguientes propiedades:

* `cq:trackevents`: identifica los eventos CQ que expone el componente. (Consulte Eventos personalizados).
* `cq:trackvars`: nombra las variables de CQ asignadas con propiedades de Adobe Analytics.
* `cq:componentName`: nombre del componente que aparece en Sidekick.
* `cq:componentGroup`: grupo en Sidekick que incluye el componente.

El código del componente JSP agrega el JavaScript a la página que almacena en déclencheur el seguimiento y define los datos que se rastrean. El nombre de evento y los nombres de datos utilizados en JavaScript deben coincidir con los valores correspondientes de las propiedades del nodo `analytics`.

* Utilice el atributo de seguimiento de datos para rastrear datos de evento cuando se cargue una página. (Consulte [Seguimiento de eventos personalizados al cargar la página](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)).
* Utilice la función CQ_Analytics.record para realizar un seguimiento de los datos de evento cuando los usuarios interactúen con las funciones de la página. (Consulte [Seguimiento De Eventos Personalizados Después De La Carga De La Página](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)).

Cuando se utilizan estos métodos de seguimiento de datos, el módulo de integración de Adobe Analytics realiza automáticamente las llamadas a Adobe Analytics para registrar los eventos y los datos.

### Ejemplo: Seguimiento de clics de navegación superior {#example-tracking-topnav-clicks}

Amplíe el componente de navegación superior de base para que Adobe Analytics rastree los clics en los vínculos de navegación en la parte superior de la página. Cuando se hace clic en un vínculo de navegación, Adobe Analytics registra el vínculo en el que se hizo clic y la página en la que se hizo clic.

Los siguientes procedimientos requieren que ya haya realizado las siguientes tareas:

* Se ha creado una aplicación CQ.
* Se ha creado una configuración de Adobe Analytics y un marco de trabajo de Adobe Analytics.

#### Copiar el componente de navegación superior {#copy-the-topnav-component}

Copie el componente de navegación superior en la aplicación CQ. El procedimiento requiere que la aplicación esté configurada en CRXDE Lite.

1. Haga clic con el botón derecho en el nodo `/libs/foundation/components/topnav` y haga clic en Copiar.
1. Haga clic con el botón derecho en la carpeta Componentes debajo de la carpeta de la aplicación y haga clic en Pegar.
1. Haga clic en Guardar todo.

#### Integración de la navegación superior con Adobe Analytics Framework {#integrating-topnav-with-the-adobe-analytics-framework}

Configure el componente de navegación superior y edite el archivo JSP para definir los eventos de seguimiento y los datos.

1. Haga clic con el botón derecho en el nodo de navegación superior y haga clic en Crear > Crear nodo. Especifique los siguientes valores de propiedad y haga clic en Aceptar:

   * Nombre: `analytics`
   * Tipo: `nt:unstructured`

1. Agregue la siguiente propiedad al nodo de análisis para poder asignar un nombre al evento de seguimiento:

   * Nombre: cq:trackevents
   * Tipo: cadena
   * Valor: topnavClick

1. Agregue la siguiente propiedad al nodo de Analytics para poder asignar un nombre a las variables de datos:

   * Nombre: cq:trackvars
   * Tipo: cadena
   * Valor: topnavTarget,topnavLocation

1. Agregue la siguiente propiedad al nodo de Analytics para asignar un nombre al componente para Sidekick:

   * Nombre: cq:componentName
   * Tipo: cadena
   * Value: topnav (tracking)

1. Agregue la siguiente propiedad al nodo de Analytics para asignar un nombre al grupo de componentes para Sidekick:

   * Nombre: cq:componentGroup
   * Tipo: cadena
   * Valor: General

1. Haga clic en Guardar todo.
1. Abra el archivo `topnav.jsp`.
1. En el elemento, agregue el atributo siguiente:

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. En la parte inferior de la página, añada el siguiente código JavaScript:

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. Haga clic en Guardar todo.

El contenido del archivo `topnav.jsp` debe aparecer de la siguiente manera:

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>A menudo es deseable realizar un seguimiento de los datos de ContextHub. Para obtener información acerca de cómo usar JavaScript para obtener esta información, vea [Obtener acceso a valores en ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### Adición del componente Seguimiento a Sidekick {#adding-the-tracking-component-to-sidekick}

Agregue a Sidekick los componentes que están habilitados para el seguimiento con Adobe Analytics para que pueda agregarlos al marco de trabajo.

1. Abra el marco de trabajo de Adobe Analytics desde la configuración de Adobe Analytics. ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. En Sidekick, haga clic en el botón Diseño.

   ![Botón Diseño con un cuadrado en ángulo recto.](assets/chlimage_1a.png)

1. En el área Configuración de seguimiento de vínculos, haga clic en Configurar herencia.

   ![chlimage_1](assets/chlimage_1aa.png)

1. En la lista Componentes permitidos, seleccione top nav (seguimiento) en la sección General y, a continuación, haga clic en Aceptar.
1. Expanda Sidekick para entrar en modo de edición. El componente ya está disponible en el grupo General.

#### Adición del componente de navegación superior al marco de trabajo {#adding-the-topnav-component-to-your-framework}

Arrastre el componente de navegación superior al marco de trabajo de Adobe Analytics y asigne las variables y los eventos de componente a las variables y los eventos de Adobe Analytics. (Consulte [Configuración de un marco de trabajo para el seguimiento básico](/help/sites-administering/adobeanalytics-connect.md)).

![chlimage_1-1](assets/chlimage_1-1a.png)

El componente de navegación superior ahora está integrado con el marco de trabajo de Adobe Analytics. Al añadir el componente a una página, hacer clic en los elementos de la barra de navegación superior hace que los datos de seguimiento se envíen a Adobe Analytics.

### Envío de datos de s.products a Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

Los componentes pueden generar datos para la variable s.products que se envía a Adobe Analytics. Diseñe sus componentes para contribuir a la variable s.products:

* Registre un valor denominado `product` de una estructura específica.
* Exponga los miembros de datos del valor `product` para que se puedan asignar con variables de Adobe Analytics en el marco de trabajo de Adobe Analytics.

La variable s.products de Adobe Analytics usa la sintaxis siguiente:

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

El módulo de integración de Adobe Analytics construye la variable `s.products` con los valores `product` que generan los componentes de AEM. El valor `product` en JavaScript que generan los componentes de AEM es una matriz de valores que tienen la siguiente estructura:

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

Cuando se omite un elemento de datos del valor `product`, se envía como una cadena vacía en s.products.

>[!NOTE]
>
>Cuando no hay ningún evento asociado a un valor de producto, Adobe Analytics utiliza el evento `prodView` de forma predeterminada.

El nodo `analytics` del componente debe exponer los nombres de las variables mediante la propiedad `cq:trackvars`:

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

El módulo de comercio electrónico proporciona varios componentes que generan datos de variables s.products. Por ejemplo, el componente `submitorder` ([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)) genera JavaScript similar al siguiente ejemplo:

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### Limitación del tamaño de las llamadas de seguimiento {#limiting-the-size-of-tracking-calls}

Por lo general, los exploradores web limitan el tamaño de las solicitudes de GET. Dado que los valores de producto y SKU de CQ son rutas de repositorio, las matrices de productos que incluyen varios valores pueden superar el límite de tamaño de solicitud. Por lo tanto, los componentes deben limitar el número de elementos en la matriz `product` de cada `CQ_Analytics.record function`. Cree varias funciones si el número de elementos que debe rastrear puede superar el límite.

Por ejemplo, el componente de comercio electrónico `submitorder` limita a cuatro el número de elementos `product` de una llamada. Cuando el carro contiene más de cuatro productos, genera varias funciones `CQ_Analytics.record`.
