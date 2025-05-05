---
title: Ampliación del seguimiento de eventos
description: AEM Analytics permite rastrear la interacción del usuario en el sitio web
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Ampliación del seguimiento de eventos{#extending-event-tracking}

AEM Analytics permite rastrear la interacción del usuario en el sitio web. Como desarrollador, es posible que tenga que:

* Rastree cómo los visitantes interactúan con los componentes. Esto se puede hacer con [eventos personalizados.](#custom-events)
* [Valores de acceso en ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Agregar devoluciones de llamadas de registro](#adding-record-callbacks).

>[!NOTE]
>
>Básicamente, esta información es genérica, pero usa [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para ejemplos específicos.
>
>Para obtener información general sobre el desarrollo de componentes y cuadros de diálogo, vea [Desarrollar componentes](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Los eventos personalizados hacen un seguimiento de cualquier elemento que dependa de la disponibilidad de un componente específico en la página. Esto también incluye eventos específicos de la plantilla, ya que el componente de página se trata como otro componente.

### Seguimiento De Eventos Personalizados Al Cargar La Página {#tracking-custom-events-on-page-load}

Esto se puede hacer con el pseudoatributo `data-tracking` (el atributo de registro anterior sigue siendo compatible con la compatibilidad con versiones anteriores). Puede añadir esto a cualquier etiqueta de HTML.

La sintaxis de `data-tracking` es

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Puede pasar cualquier número de pares clave-valor como segundo parámetro, que se denomina carga útil.

Un ejemplo podría tener el siguiente aspecto:

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

Al cargar la página, se recopilarán todos los atributos de `data-tracking` y se agregarán al almacén de eventos de ContextHub, donde se pueden asignar a eventos de Adobe Analytics. Adobe Analytics no rastreará los eventos que no estén asignados. Consulte [Conectarse a Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obtener más información sobre la asignación de eventos.

### Seguimiento de eventos personalizados después de cargar la página {#tracking-custom-events-after-page-load}

Para hacer un seguimiento de los eventos que se producen después de cargar una página (como las interacciones del usuario), use la función JavaScript `CQ_Analytics.record`:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Donde

* `events` es una cadena o una matriz de cadenas (para varios eventos).

* `values` contiene todos los valores que se van a rastrear
* `collect` es opcional y devolverá una matriz que contiene el evento y el objeto de datos.
* `options` es opcional y contiene opciones de seguimiento de vínculos como el elemento HTML `obj` y ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` es un atributo necesario y se recomienda establecerlo en `<%=resource.getResourceType()%>`

Por ejemplo, con la siguiente definición, si un usuario hace clic en el vínculo **Saltar al principio**, se activarán los dos eventos, `jumptop` y `headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acceso a los valores en ContextHub {#accessing-values-in-the-contexthub}

La API de JavaScript de ContextHub tiene una función `getStore(name)` que devuelve el almacén especificado, si está disponible. El almacén tiene una función `getItem(key)` que devuelve el valor de la clave especificada, si está disponible. Mediante la función `getKeys()` es posible recuperar una matriz de claves definidas para el almacén específico.

Se le pueden notificar los cambios de valor en un almacén enlazando una función mediante la función `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

La mejor manera de recibir notificaciones sobre la disponibilidad inicial de ContextHub es utilizar la función `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventos adicionales para ContextHub:**

Todas las tiendas listas:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico de la tienda:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Ver también la [Referencia de la API de ContextHub](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference) completa

## Adición de devoluciones de llamada de registro {#adding-record-callbacks}

Antes y después de registrar las llamadas de retorno mediante las funciones `CQ_Analytics.registerBeforeCallback(callback,rank)` y `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas funciones toman una función como primer argumento y una clasificación como segundo argumento, lo que dicta el orden en que se ejecutan las llamadas de retorno.

Si la llamada de retorno devuelve el valor &quot;False&quot;, no se ejecutarán las llamadas de retorno siguientes en la cadena de ejecución.
