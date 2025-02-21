---
title: Fragmentos de contenido Configurar componentes para procesamiento
description: Fragmentos de contenido Configurar componentes para procesamiento
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---

# Fragmentos de contenido Configurar componentes para procesamiento{#content-fragments-configuring-components-for-rendering}

Hay varios [servicios avanzados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) relacionados con la representación de fragmentos de contenido. Para utilizar estos servicios, los tipos de recurso de dichos componentes deben darse a conocer al marco de trabajo de fragmentos de contenido.

Para ello, configure el [servicio OSGi - Configuración del componente Fragmento de contenido](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Si no necesita los [servicios avanzados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) que se describen a continuación, puede ignorar esta configuración.

>[!CAUTION]
>
>Cuando se amplía o se utilizan los componentes predeterminados, no se recomienda cambiar la configuración.

>[!CAUTION]
>
>Puede escribir un componente desde cero que utilice solo la API de fragmentos de contenido, sin servicios avanzados. Sin embargo, en tal caso, deberá desarrollar el componente para que se ocupe del procesamiento adecuado.
>
>Por lo tanto, se recomienda utilizar los componentes principales.

## Definición de servicios avanzados que necesitan configuración {#definition-of-advanced-services-that-need-configuration}

Los servicios que requieren el registro de un componente son:

* Determinar correctamente las dependencias durante la publicación (es decir, asegurarse de que los fragmentos y modelos se puedan publicar automáticamente con una página si han cambiado desde la última publicación).
* Compatibilidad con fragmentos de contenido en la búsqueda de texto completo.
* Administración/administración de *contenido intermedio.*
* Administración de *recursos de medios mixtos.*
* Vaciar Dispatcher para fragmentos a los que se hace referencia (si se vuelve a publicar una página que contiene un fragmento).
* Uso de la renderización basada en párrafos.

Si necesita una o más de estas funciones, (por lo general) es más fácil utilizar la funcionalidad predeterminada, en lugar de desarrollarla desde cero.

## Servicio OSGi: configuración del componente Fragmento de contenido {#osgi-service-content-fragment-component-configuration}

La configuración debe enlazarse al servicio OSGi **Configuración del componente Fragmento de contenido**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Por ejemplo:

![cfm-01](assets/cfm-01.png)

La configuración de OSGi es:

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Configuración de OSGi<br /> </td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><strong>Tipo de medio</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>El tipo de recurso que se va a registrar; por ejemplo, <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propiedad de referencia</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nombre de la propiedad que contiene la referencia al fragmento; por ejemplo, <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de elemento(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Nombre de la propiedad que contiene los nombres de los elementos que se van a representar; por ejemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de variación</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Nombre de la propiedad que contiene el nombre de la variación que se va a procesar; por ejemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algunas funciones (por ejemplo, para procesar solo un intervalo de párrafo) tendrá que adherirse a algunas convenciones:

<table>
 <tbody>
  <tr>
   <td>Nombre de la propiedad</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Propiedad de cadena que define el intervalo de párrafos que se generará si se encuentra en <em>modo de representación de un solo elemento</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code></li>
     <li>solo se evalúa si <code>paragraphScope</code> se establece en <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Propiedad de cadena que define cómo se generarán los párrafos en <em>modo de representación de elemento único</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para procesar todos los párrafos</li>
     <li><code>range</code> : para representar el intervalo de párrafos proporcionado por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una propiedad booleana que define si los encabezados (por ejemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) se cuentan como párrafos (<code>true</code>) o no (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Esto puede cambiar en los hitos 6.5 posteriores.

## Ejemplos {#example}

Por ejemplo, consulte lo siguiente (en una instancia de AEM predeterminada):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene lo siguiente:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
