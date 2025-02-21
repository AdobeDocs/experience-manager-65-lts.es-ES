---
title: Bibliotecas de etiquetas
description: Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para utilizarlas en el script JSP de sus plantillas y componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Tagging
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 0%

---

# Bibliotecas de etiquetas{#tag-libraries}

Las bibliotecas de etiquetas Granite, CQ y Sling le proporcionan acceso a funciones específicas para utilizarlas en el script JSP de sus plantillas y componentes.

## Biblioteca de etiquetas de Granite {#granite-tag-library}

La biblioteca de etiquetas Granite contiene funciones útiles.

Al desarrollar el script jsp de un componente de la interfaz de usuario de Granite, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

La biblioteca global también declara la [biblioteca Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

La etiqueta `<ui:includeClientLib>` incluye una biblioteca de cliente HTML de AEM, que puede ser una biblioteca js, css o de temáticas. Para varias inclusiones de diferentes tipos, por ejemplo, js y css, esta etiqueta debe utilizarse varias veces en jsp. Esta etiqueta es un envoltorio práctico para la interfaz de servicio ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Tiene los atributos siguientes:

**categorías**: una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas de JavaScript y CSS para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema**: una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas relacionadas con temáticas (tanto CSS como JS) para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js**: una lista de categorías de biblioteca de cliente separadas por coma. Esto incluye todas las bibliotecas de JavaScript para las categorías dadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**: una lista de categorías de biblioteca de cliente separadas por coma. Esto incluye todas las bibliotecas CSS para las categorías dadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temático**: se debe incluir un indicador que indique que solo se deben incluir bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a inclusiones JS o CSS puras (no para categorías ni inclusiones de temas).

La etiqueta `<ui:includeClientLib>` se puede usar de la siguiente manera en un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## Biblioteca de etiquetas CQ {#cq-tag-library}

La biblioteca de etiquetas CQ contiene funciones útiles.

Para utilizar la biblioteca de etiquetas CQ en el script, este debe comenzar con el siguiente código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Cuando se incluye el archivo `/libs/foundation/global.jsp` en el script, la biblioteca de etiquetas se declara automáticamente.

Al desarrollar el script jsp de un componente de AEM, se recomienda incluir el siguiente código en la parte superior del script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Declara las etiquetas sling, CQ y jstl y expone los objetos de script utilizados con regularidad definidos por la etiqueta [`<cq:defineObjects />`](#amp-lt-cq-defineobjects). Esto acorta y simplifica el código jsp del componente.

### &lt;cq:text> {#cq-text}

La etiqueta `<cq:text>` es una etiqueta de conveniencia que genera texto de componente en un JSP.

Tiene los siguientes atributos opcionales:

**propiedad** - Nombre de la propiedad que se va a usar. El nombre es relativo al recurso actual.

**value**: valor que se usará para la salida. Si este atributo está presente, sobrescribe el uso del atributo property.

**oldValue**: valor que se utilizará para la salida de diferencia. Si este atributo está presente, sobrescribe el uso del atributo property.

**escapeXml**: define si los caracteres &lt;, >, &amp;, &#39; y &quot; de la cadena resultante deben convertirse a sus códigos de entidad de carácter correspondientes. El valor predeterminado es false. El escape se aplica después del formato opcional.

**format**: java.text.Format opcional que se utilizará para dar formato al texto.

**noDiff**: suprime el cálculo de una salida de diferencia, aunque haya información de diferencia.

**tagClass**: nombre de clase CSS de un elemento que rodeará una salida no vacía. Si está vacío, no se agrega ningún elemento.

**tagName**: nombre del elemento que rodeará una salida no vacía. El valor predeterminado es DIV.

**placeholder**: valor predeterminado que se usará para texto nulo o vacío en el modo de edición, es decir, el marcador de posición. La comprobación predeterminada se realiza después del formato opcional y el escape, es decir, se escribe tal cual en la salida. El valor predeterminado es:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default**: valor predeterminado que se usará para texto nulo o vacío. La comprobación predeterminada se realiza después del formato opcional y el escape, es decir, se escribe tal cual en la salida.

Algunos ejemplos de cómo se puede utilizar la etiqueta `<cq:text>` en un JSP:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

La etiqueta `<cq:setContentBundle>` crea un contexto de localización i18n y lo almacena en la variable de configuración `javax.servlet.jsp.jstl.fmt.localizationContext`.

Tiene los atributos siguientes:

**idioma**: idioma de la configuración regional para la que se recuperará el paquete de recursos.

**origen**: origen desde el que se debe tomar la configuración regional. Se puede establecer en uno de los siguientes valores:

* **static**: la configuración regional se toma del atributo `language` si está disponible; de lo contrario, se toma de la configuración regional predeterminada del servidor.

* **página**: la configuración regional se toma del idioma de la página o del recurso actual si está disponible; de lo contrario, se toma del atributo `language` si está disponible; de lo contrario, se toma de la configuración regional predeterminada del servidor.

* **solicitud** - la configuración regional se toma de la configuración regional de la solicitud ( `request.getLocale()`).

* **auto**: la configuración regional se toma del atributo `language` si está disponible; de lo contrario, se toma del idioma de la página o el recurso actual si está disponible; de lo contrario, se toma de la solicitud.

Si el atributo `source` no está establecido:

* Si se establece el atributo `language`, el atributo `source` toma como valor predeterminado &quot;`static`.

* Si no se establece el atributo `language`, el valor predeterminado del atributo `source` es `auto`.

Las etiquetas JSTL estándar `<fmt:message>` pueden utilizar el &quot;paquete de contenido&quot;. La búsqueda de mensajes por claves es doble:

1. En primer lugar, se buscan traducciones en las propiedades JCR del recurso subyacente que se procesa. Esto permite definir un cuadro de diálogo de componente simple para editar esos valores.
1. Si el nodo no contiene una propiedad denominada exactamente como la clave, la alternativa es cargar un paquete de recursos desde la solicitud de sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). El idioma o la configuración regional de este paquete se define mediante los atributos de idioma y origen de la etiqueta `<cq:setContentBundle>`.

La etiqueta `<cq:setContentBundle>` se puede usar de la siguiente manera en un jsp.

Para páginas que definen su idioma:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Para páginas personalizadas de usuario:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

La etiqueta `<cq:include>` incluye un recurso en la página actual.

Tiene los atributos siguientes:

**vaciar**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**ruta**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuyo script incluye el recurso dado. Se debe especificar la ruta y el tipo de recurso o el script.

**resourceType**

* El tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo de ruta que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y de este tipo de recurso.
* Se debe especificar la ruta y el tipo de recurso o el script.

**script**

* Script jsp que se va a incluir. Se debe especificar la ruta y el tipo de recurso o el script.

**ignoreComponentHierarchy**

* Un booleano que controla si la jerarquía de componentes debe ignorarse para la resolución de scripts. Si es true, solo se respetan las rutas de búsqueda.

**Ejemplo:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

¿Debería usar `<%@ include file="myScript.jsp" %>` o `<cq:include script="myScript.jsp" %>` para incluir un script?

* La directiva `<%@ include file="myScript.jsp" %>` indica al compilador JSP que incluya un archivo completo en el archivo actual. Es como si el contenido del archivo incluido se hubiera pegado directamente en el archivo original.
* Con la etiqueta `<cq:include script="myScript.jsp">`, el archivo se incluye durante la ejecución.

¿Debería usar `<cq:include>` o `<sling:include>`?

* Al desarrollar componentes de AEM, Adobe recomienda usar `<cq:include>`.
* `<cq:include>` le permite incluir directamente archivos de script por su nombre cuando se utiliza el atributo script. Esto tiene en cuenta la herencia de componentes y tipos de recursos, y a menudo es más sencillo que el cumplimiento estricto de la resolución de scripts de Sling mediante selectores y extensiones.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` obsoleto desde AEM 5.6. Se debe usar [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) en su lugar.

La etiqueta `<cq:includeClientLib>` incluye una biblioteca de cliente HTML de AEM, que puede ser una biblioteca js, css o de temáticas. Para varias inclusiones de diferentes tipos, por ejemplo, js y css, esta etiqueta debe utilizarse varias veces en jsp. Esta etiqueta es un envoltorio práctico para la interfaz de servicio `com.day.cq.widget.HtmlLibraryManager`.

Tiene los atributos siguientes:

**categorías**: una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas de JavaScript y CSS para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema**: una lista de categorías de biblioteca de cliente separadas por comas. Esto incluye todas las bibliotecas relacionadas con temáticas (tanto CSS como JS) para las categorías dadas. El nombre de la temática se extrae de la solicitud.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js**: una lista de categorías de biblioteca de cliente separadas por coma. Esto incluye todas las bibliotecas de JavaScript para las categorías dadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**: una lista de categorías de biblioteca de cliente separadas por coma. Esto incluye todas las bibliotecas CSS para las categorías dadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temático**: se debe incluir un indicador que indique que solo se deben incluir bibliotecas temáticas o no temáticas. Si se omite, se incluyen ambos conjuntos. Solo se aplica a inclusiones JS o CSS puras (no para categorías ni inclusiones de temas).

La etiqueta `<cq:includeClientLib>` se puede usar de la siguiente manera en un jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

La etiqueta `<cq:defineObjects>` expone los siguientes objetos de script, que se utilizan con regularidad y a los que el desarrollador puede hacer referencia. También expone los objetos definidos por la etiqueta [`<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* el objeto de contexto del componente actual de la solicitud (com.day.cq.wcm.api.components.ComponentContext.interface).

**componente**

* el objeto del componente AEM actual del recurso actual (com.day.cq.wcm.api.components.Component interfaz).

**currentDesign**

* el objeto de diseño actual de la página actual (com.day.cq.wcm.api.designer.Design interface).

**currentPage**

* el objeto de página WCM de AEM actual (interfaz com.day.cq.wcm.api.Page).

**currentStyle**

* el objeto style actual de la celda actual (interfaz com.day.cq.wcm.api.designer.Style).

**diseñador**

* el objeto designer utilizado para tener acceso a la información de diseño (interfaz com.day.cq.wcm.api.designer.Designer).

**editContext**

* el objeto de contexto de edición del componente AEM (com.day.cq.wcm.api.components.EditContext.interface).

**pageManager**

* el objeto administrador de páginas para operaciones de nivel de página (interfaz com.day.cq.wcm.api.PageManager).

**pageProperties**

* el objeto page properties de la página actual (org.apache.sling.api.resource.ValueMap).

**propiedades**

* el objeto properties del recurso actual (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* el objeto design de la página de recursos (com.day.cq.wcm.api.designer.Design interface).

**resourcePage**

* el objeto de página de recursos (interfaz com.day.cq.wcm.api.Page).
* Tiene los atributos siguientes:

**requestName**

* heredado de sling

**responseName**

* heredado de sling

**resourceName**

* heredado de sling

**nombreDeNodo**

* heredado de sling

**logName**

* heredado de sling

**resourceResolverName**

* heredado de sling

**slingName**

* heredado de sling

**componentContextName**

* específico de wcm

**editContextName**

* específico de wcm

**propertiesName**

* específico de wcm

**pageManagerName**

* específico de wcm

**currentPageName**

* específico de wcm

**resourcePageName**

* específico de wcm

**pagePropertiesName**

* específico de wcm

**componentName**

* específico de wcm

**designerName**

* específico de wcm

**currentDesignName**

* específico de wcm

**resourceDesignName**

* específico de wcm

**currentStyleName**

* específico de wcm

**Ejemplo**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Cuando el archivo `/libs/foundation/global.jsp` se incluye en el script, la etiqueta `<cq:defineObjects />` se incluye automáticamente.

### &lt;cq:requestURL> {#cq-requesturl}

La etiqueta `<cq:requestURL>` escribe la dirección URL de la solicitud actual en JspWriter. Las dos etiquetas [`<cq:addParam>`](#amp-lt-cq-addparam) y [`<cq:removeParam>`](#amp-lt-cq-removeparam) y se pueden usar dentro del cuerpo de esta etiqueta para modificar la dirección URL de la solicitud actual antes de que se escriba.

Permite crear vínculos a la página actual con distintos parámetros. Por ejemplo, permite transformar la solicitud:

`mypage.html?mode=view&query=something` en `mypage.html?query=something`.

El uso de `addParam` o `removeParam` solo cambia la aparición del parámetro dado; el resto de parámetros no se ven afectados.

`<cq:requestURL>` no tiene ningún atributo.

Por ejemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

La etiqueta `<cq:addParam>` agrega un parámetro de solicitud con el nombre y valor dados a la etiqueta [`<cq:requestURL>`](#amp-lt-cq-requesturl) que lo incluye.

Tiene los atributos siguientes:

**nombre**

* nombre del parámetro que se va a agregar

**valor**

* valor del parámetro que se va a agregar

**Ejemplo:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

La etiqueta `<cq:removeParam>` quita un parámetro de solicitud con el nombre y valor dados de la etiqueta [`<cq:requestURL>`](#amp-lt-cq-requesturl) que lo incluye. Si no se proporciona ningún valor, se eliminan todos los parámetros con el nombre dado.

Tiene los atributos siguientes:

**nombre**

* nombre del parámetro que se va a eliminar

Ejemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Biblioteca de etiquetas de Sling {#sling-tag-library}

La biblioteca de etiquetas Sling contiene funciones Sling útiles.

Cuando se utiliza la biblioteca de etiquetas Sling en el script, este debe comenzar con el siguiente código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Cuando se incluye el archivo `/libs/foundation/global.jsp` en el script, la biblioteca de etiquetas de sling se declara automáticamente.

### &lt;sling:include> {#sling-include}

La etiqueta `<sling:include>` incluye un recurso en la página actual.

Tiene los atributos siguientes:

**vaciar**

* Un booleano que define si se debe vaciar la salida antes de incluir el destino.

**recurso**

* El objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**ruta**

* Ruta al objeto de recurso que se va a incluir en el procesamiento de solicitud actual. Si esta ruta es relativa, se anexa a la ruta del recurso actual cuyo script incluye el recurso dado. Se debe especificar el recurso o la ruta. Si se especifican ambos, el recurso tiene prioridad.

**resourceType**

* El tipo de recurso del recurso que se va a incluir. Si se establece el tipo de recurso, la ruta debe ser la ruta exacta a un objeto de recurso: en este caso, no se admite la adición de parámetros, selectores y extensiones a la ruta.
* Si el recurso que se va a incluir se especifica con el atributo de ruta que no se puede resolver en un recurso, la etiqueta puede crear un objeto de recurso sintético fuera de la ruta y de este tipo de recurso.

**replaceSelectors**

* Al realizar el envío, los selectores se sustituyen por el valor de este atributo.

**addSelectors**

* Al realizar el envío, el valor de este atributo se añade a los selectores.

**replaceSuffix**

* Al realizar el envío, el sufijo se reemplaza por el valor de este atributo.

>[!NOTE]
>
>La resolución del recurso y el script que se incluyen con la etiqueta `<sling:include>` es la misma que para una resolución de URL normal de sling. De forma predeterminada, los selectores, la extensión, etc. de la solicitud actual también se utilizan para el script incluido. Se pueden modificar mediante los atributos de etiqueta: por ejemplo, `replaceSelectors="foo.bar"` permite sobrescribir los selectores.

Por ejemplo:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

La etiqueta `<sling:defineObjects>` expone los siguientes objetos de scripts que el desarrollador puede hacer referencia y que se utilizan con regularidad:

**slingRequest**

* El objeto SlingHttpServletRequest, que proporciona acceso a la información del encabezado de solicitud HTTP (amplía el objeto HttpServletRequest estándar) y proporciona acceso a elementos específicos de Sling como recursos, información de ruta y selector.

**slingResponse**

* Objeto SlingHttpServletResponse, que proporciona acceso a la respuesta HTTP creada por el servidor. Es igual que el HttpServletResponse desde el que se extiende.**solicitud**
* El objeto de solicitud JSP estándar que es HttpServletRequest puro.**respuesta**
* El objeto de respuesta JSP estándar que es HttpServletResponse puro.

**resourceResolver**

* El objeto ResourceResolver actual. Es lo mismo que slingRequest.getResourceResolver()

.**sling**

* Un objeto SlingScriptHelper, que contiene métodos de conveniencia para scripts, principalmente sling.include(&#39;/some/other/resource&#39;) para incluir las respuestas de otros recursos dentro de esta respuesta (por ejemplo, incrustar fragmentos html de encabezado) y sling.getService(foo.bar.Service.class) para recuperar los servicios OSGi disponibles en Sling (notación de clase según el lenguaje de script).

**recurso**

* el objeto Resource actual que se va a controlar, según la dirección URL de la solicitud. Es lo mismo que slingRequest.getResource().

**nodoActual**

* Si el recurso actual apunta a un nodo JCR (como suele ocurrir en Sling), proporciona acceso directo al objeto Node. De lo contrario, este objeto no está definido.

**registro**

* Proporciona un registrador SLF4J para registrar en el sistema de registro de Sling desde scripts, por ejemplo, log.info(&quot;Ejecutando mi script&quot;).

* Tiene los atributos siguientes:

**requestName**

**responseName**

**nombreDeNodo**

l **ogName resourceResolverName**

**slingName**

**Ejemplo:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Biblioteca de etiquetas JSTL {#jstl-tag-library}

La [Biblioteca de etiquetas estándar de páginas de JavaServer](https://www.oracle.com/java/technologies/java-server-tag-library.html) contiene muchas etiquetas útiles y estándar. Las etiquetas principales, de formato y de funciones están definidas por `/libs/foundation/global.jsp` tal como se muestra en el siguiente fragmento de código.

### Extracto de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Después de importar el archivo `/libs/foundation/global.jsp` como se describió anteriormente, puede usar los prefijos `c`, `fmt` y `fn` para tener acceso a esas etiquetas. La documentación oficial de JSTL está disponible en [The Java™ EE 5 Tutorial - JavaServer Pages Standard Tag Library](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
