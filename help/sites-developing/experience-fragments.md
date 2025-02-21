---
title: Fragmentos de experiencias en el desarrollo de Adobe Experience Manager Sites
description: Aprenda a personalizar fragmentos de experiencias para Adobe Experience Manager.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ac26c0163309b6cb6c0cfde2098a8cc05955d03f
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---

# Fragmentos de experiencias {#experience-fragments}

## Conceptos básicos {#the-basics}

Un [fragmento de experiencia](/help/sites-authoring/experience-fragments.md) es un grupo de uno o más componentes, incluido el contenido y el diseño, a los que se puede hacer referencia en las páginas.

Un fragmento de experiencia principal o variante utiliza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como no hay `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, vuelve a usarse

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Representación HTML sin formato {#the-plain-html-rendition}

Utilizando el selector `.plain.` en la dirección URL, puede acceder a la representación sin formato de HTML.

Está disponible desde el explorador, pero su propósito principal es permitir que otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) accedan al contenido del fragmento de experiencia directamente, únicamente mediante la dirección URL.

La representación de HTML sin formato agrega el protocolo, el host y la ruta de contexto a las rutas que son:

* del tipo: `src`, `href` o `action`

* o finalizar con: `-src` o `-href`

Por ejemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Los vínculos siempre hacen referencia a la instancia de publicación. Los consumen terceros, por lo que siempre se llama al vínculo desde la instancia de publicación, no desde la instancia de autor.
>
>Para obtener más información, consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

![xf-14](assets/xf-14.png)

El selector de representación sin formato usa un transformador en lugar de scripts adicionales; [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) se usa como transformador. Esto se configura en

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configuración de la generación de representaciones de HTML {#configuring-html-rendition-generation}

La representación de HTML se genera mediante las canalizaciones de reescritura de Sling. La canalización se ha definido en `/libs/experience-fragments/config/rewriter/experiencefragments`. El transformador de HTML admite las siguientes opciones:

* `allowedCssClasses`
   * Expresión de RegEx que coincide con las clases CSS que deben dejarse en la representación final.
   * Esto resulta útil si el cliente desea eliminar algunas clases CSS específicas
* `allowedTags`
   * Una lista de etiquetas HTML que se permitirán en la representación final.
   * De forma predeterminada, se permiten las siguientes etiquetas (no se necesita configuración): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link y script

Se recomienda configurar la reescritura mediante una superposición. Ver [Superposiciones](/help/sites-developing/overlays.md)

## Variaciones sociales {#social-variations}

Las variantes sociales se pueden publicar en las redes sociales (texto e imagen). En Adobe Experience Manager (AEM), estas variantes sociales pueden contener componentes como, por ejemplo, componentes de texto o componentes de imagen.

La imagen y el texto de la publicación social se pueden tomar de cualquier tipo de recurso de imagen o de texto con cualquier nivel de profundidad (en el bloque de creación o en el contenedor de diseño).

Las variaciones sociales también permiten crear bloques y tenerlos en cuenta al realizar acciones sociales (en el entorno de publicación).

Para publicar el texto y la imagen correctos en la red de medios sociales, algunas convenciones deben respetarse si está desarrollando sus propios componentes personalizados.

Para ello, se deben utilizar las siguientes propiedades:

* Para extraer la imagen

   * `fileReference`
   * `fileName`

* Para extraer el texto

   * `text`

Los componentes que no utilizan esta convención no se tienen en cuenta.

## Plantillas para fragmentos de experiencias {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo se admiten*** [plantillas editables](/help/sites-developing/page-templates-editable.md) para los fragmentos de experiencias.
>
>Los fragmentos de experiencias solo se pueden usar en páginas que estén basadas en plantillas editables.

Al desarrollar una nueva plantilla para fragmentos de experiencias, puede seguir las prácticas estándar para una [plantilla editable](/help/sites-developing/page-templates-editable.md).

Para crear una plantilla de fragmento de experiencia detectada por el asistente **Crear fragmento de experiencia**, debe seguir uno de estos conjuntos de reglas:

1. Ambos:

   1. El tipo de recurso de la plantilla (el nodo inicial) debe heredar de:
      `cq/experience-fragments/components/xfpage`

   1. Y el nombre de la plantilla debe comenzar por:
      `experience-fragments`
Esto permite a los usuarios crear fragmentos de experiencias en /content/experience-fragments, ya que la propiedad `cq:allowedTemplates` de esta carpeta incluye todas las plantillas que tienen nombres que comienzan por `experience-fragment`. Los clientes pueden actualizar esta propiedad para incluir sus propios esquemas de nomenclatura o ubicaciones de plantillas.

1. [Las plantillas permitidas](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) se pueden configurar en la consola Fragmentos de experiencias.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiencias {#components-for-experience-fragments}

[El desarrollo de componentes](/help/sites-developing/components.md) para su uso con/en fragmentos de experiencias sigue las prácticas estándar.

La única configuración adicional es garantizar que los componentes estén [permitidos en la plantilla; esto se logra con la directiva de contenido](/help/sites-developing/page-templates-editable.md#content-policies).

## Proveedor de reescritura de vínculos de fragmentos de experiencias de HTML {#the-experience-fragment-link-rewriter-provider-html}

En AEM puede crear fragmentos de experiencias. Un fragmento de experiencia:

* consta de un grupo de componentes junto con un diseño,
* puede existir independientemente de una página de AEM.

Uno de los casos de uso de estos grupos es para incrustar contenido en puntos de contacto de terceros, como Adobe Target.

### Reescritura de vínculos predeterminados {#default-link-rewriting}

Con la característica [Exportar a Target](/help/sites-administering/experience-fragments-target.md), puede:

* crear un fragmento de experiencia,
* añadir componentes a él,
* y, a continuación, exportarla como una oferta de Adobe Target, ya sea en formato HTML o en formato JSON.

Esta característica se puede [habilitar en una instancia de autor de AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Requiere una configuración de Adobe Target válida y configuraciones para el externalizador de vínculos.

El externalizador de vínculos se utiliza para determinar las direcciones URL correctas necesarias al crear la versión de HTML de la oferta de Target, que luego se envía a Adobe Target. Esto es necesario, ya que Adobe Target requiere que se pueda acceder públicamente a todos los vínculos dentro de la oferta de HTML de Target; esto significa que cualquier recurso al que hagan referencia los vínculos y el propio fragmento de experiencia deben publicarse antes de poder utilizarse.

De forma predeterminada, al construir una oferta de HTML de Target, se envía una solicitud a un selector de Sling personalizado en AEM. Este selector se llama `.nocloudconfigs.html`. Como su nombre indica, crea una representación HTML sin formato de un fragmento de experiencia, pero no incluye configuraciones de nube (lo que sería información superflua).

Después de generar la página de HTML, la canalización de reescritura de Sling realiza modificaciones en la salida:

1. Los elementos `html`, `head` y `body` se reemplazan con `div` elementos. Se quitan los elementos `meta`, `noscript` y `title` (son elementos secundarios del elemento `head` original y no se tienen en cuenta cuando se reemplaza por el elemento `div`).

   Esto se hace para garantizar que la oferta de HTML Target se pueda incluir en las actividades de Target.

1. AEM modifica los vínculos internos presentes en HTML, de modo que apunten a un recurso publicado.

   Para determinar los vínculos que se van a modificar, AEM sigue este patrón para los atributos de los elementos de HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src, etc.)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href`, etc.)

   >[!NOTE]
   >
   >Normalmente, los vínculos internos de HTML son vínculos relativos, pero puede haber casos en los que los componentes personalizados proporcionen direcciones URL completas en HTML. De forma predeterminada, AEM ignora estas direcciones URL completas y no realiza modificaciones.

   Los vínculos de estos atributos se ejecutan a través del externalizador de vínculos de AEM `publishLink()` para volver a crear la dirección URL como si estuviera en una instancia publicada y, como tal, disponible públicamente.

Al utilizar una implementación predeterminada, el proceso descrito anteriormente debe ser suficiente para generar la oferta de Target a partir del fragmento de experiencia y luego exportarla a Adobe Target. Sin embargo, hay algunos casos de uso que no se tienen en cuenta en este proceso, como los siguientes:

* Asignación de Sling solo disponible en la instancia de publicación
* Redirecciones de Dispatcher

Para estos casos de uso, AEM proporciona la interfaz del proveedor de reescritura de vínculos.

### Interfaz de proveedor de reescritura de vínculos {#link-rewriter-provider-interface}

Para casos más complicados, no cubiertos por [default](#default-link-rewriting), AEM ofrece la interfaz del proveedor de reescritura de vínculos. Esta es una interfaz de `ConsumerType` que puede implementar en sus paquetes como servicio. Evita las modificaciones que AEM realiza en los vínculos internos de una oferta de HTML tal y como se representa desde un fragmento de experiencia. Esta interfaz le permite personalizar el proceso de reescritura de vínculos internos de HTML para adaptarlos a sus necesidades comerciales.

Algunos ejemplos de casos de uso para implementar esta interfaz como servicio son:

* Las asignaciones de Sling están habilitadas en las instancias de publicación, pero no en la instancia de autor
* Se utiliza un Dispatcher o una tecnología similar para redirigir las URL internamente
* Hay `sling:alias mechanisms` disponibles para los recursos

>[!NOTE]
>
>Esta interfaz solo procesa los vínculos internos de HTML desde la oferta de Target generada.

La interfaz del proveedor de reescritura de vínculos ( `ExperienceFragmentLinkRewriterProvider`) es la siguiente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Cómo utilizar la interfaz del proveedor de reescritura de vínculos {#how-to-use-the-link-rewriter-provider-interface}

Para utilizar la interfaz, primero debe crear un paquete que contenga un nuevo componente de servicio que implemente la interfaz del proveedor de reescritura de vínculos.

Este servicio se utiliza para conectarse a la reescritura de Exportación de fragmentos de experiencias a Target para tener acceso a los distintos vínculos.

Por ejemplo, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Para que el servicio funcione, ahora hay tres métodos que deben implementarse dentro del servicio:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Debe indicar al sistema si debe reescribir los vínculos cuando se realiza una llamada para Exportar a Target en una variación determinada del fragmento de experiencia. Para ello, implemente el método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por ejemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Este método recibe, como parámetro, la variación del fragmento de experiencia que el sistema Exportar a destino está reescribiendo en este momento.

En el ejemplo anterior, nos gustaría reescribir:

* vínculos presentes en `src`

* Solo atributos de `href`

* para un fragmento de experiencia específico:
  `/content/experience-fragment/master`

Cualquier otro fragmento de experiencia que pase por el sistema Exportar a destino se ignorará y no se verá afectado por los cambios implementados en este servicio.

#### rewriteLink {#rewritelink}

Para la variación del fragmento de experiencia afectada por el proceso de reescritura, se permite al servicio gestionar la reescritura de vínculos. Cada vez que se encuentra un vínculo en la HTML interna, se invoca el siguiente método:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, el método recibe los parámetros:

* `link`
La representación `String` del vínculo que se está procesando. Suele ser una dirección URL relativa que señala al recurso en la instancia de autor.

* `tag`
Nombre del elemento HTML que se está procesando.

* `attribute`
El nombre exacto del atributo.

Por ejemplo, si el sistema Exportar a destino está procesando este elemento, puede definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La llamada al método `rewriteLink()` se realiza utilizando estos parámetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Al crear el servicio, puede tomar decisiones basadas en la entrada dada y, a continuación, reescribir el vínculo en consecuencia.

Para nuestro ejemplo, queremos eliminar la parte `/etc.clientlibs` de la dirección URL y agregar el dominio externo correspondiente. Para simplificar las cosas, consideraremos que tenemos acceso a un Resource Resolver para su servicio, como en `rewriteLinkExample2`:

>[!NOTE]
>
>Para obtener más información sobre cómo obtener una resolución de recursos mediante un usuario de servicio, consulte [Usuarios de servicio en AEM](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Si el método anterior devuelve `null`, el sistema Exportar a destino deja el vínculo tal cual, un vínculo relativo a un recurso.

#### Prioridades: getPriority {#priorities-getpriority}

No es raro necesitar varios servicios para atender diferentes tipos de fragmentos de experiencias o incluso tener un servicio genérico que gestione la externalización y la asignación para todos los fragmentos de experiencias. En estos casos, pueden surgir conflictos acerca del servicio que se va a utilizar, por lo que AEM proporciona la posibilidad de definir **Prioridades** para diferentes servicios. Las prioridades se especifican mediante el método:

* `getPriority()`

Este método permite el uso de varios servicios donde el método `shouldRewrite()` devuelve true para el mismo fragmento de experiencia. El servicio que devuelve el número más alto de su método `getPriority()` es el que administra la variación del fragmento de experiencia.

Por ejemplo, puede tener un `GenericLinkRewriterProvider` que administra la asignación básica de todos los fragmentos de experiencias y cuando el método `shouldRewrite()` devuelve `true` para todas las variaciones de fragmentos de experiencias. Para varios fragmentos de experiencias específicos, es posible que desee una administración especial, por lo que en este caso, puede proporcionar un `SpecificLinkRewriterProvider` para el cual el método `shouldRewrite()` devuelva el valor &quot;True&quot; solo para algunas variaciones de fragmentos de experiencias. Para asegurarse de que `SpecificLinkRewriterProvider` se elige para controlar esas variaciones de fragmento de experiencia, debe devolver en su método `getPriority()` un número mayor que `GenericLinkRewriterProvider.`
