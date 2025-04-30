---
title: Configuraciones de Cloud Service
description: Puede ampliar las instancias existentes para crear sus propias configuraciones
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6b9b8d8c-8cd5-4c21-9b75-acd74d00354a
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 4%

---

# Configuraciones de Cloud Service{#cloud-service-configurations}

Las configuraciones están diseñadas para proporcionar la lógica y la estructura para almacenar configuraciones de servicio.

Puede ampliar las instancias existentes para crear sus propias configuraciones.

## Conceptos  {#concepts}

Los principios utilizados para desarrollar las configuraciones se han basado en los siguientes conceptos:

* Los servicios o adaptadores se utilizan para recuperar las configuraciones.
* Las configuraciones (por ejemplo, propiedades/párrafos) se heredan de los elementos principales.
* Referido desde nodos de análisis por ruta.
* Fácilmente extensible.
* Tiene la flexibilidad de adaptarse a configuraciones más complejas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Compatibilidad con dependencias (por ejemplo, los complementos de [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) necesitan una configuración de [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)).

## Estructura {#structure}

La ruta base de las configuraciones es:

`/etc/cloudservices`.

Para cada tipo de configuración, se proporciona una plantilla y un componente. Esto permite tener plantillas de configuración que pueden satisfacer la mayoría de las necesidades después de personalizarse.

Para proporcionar una configuración para nuevos servicios, haga lo siguiente:

* Creación de una página de servicio en

  `/etc/cloudservices`

* En esta sección:

   * una plantilla de configuración
   * un componente de configuración

La plantilla y el componente deben heredar `sling:resourceSuperType` de la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

O componente base respectivamente

`cq/cloudserviceconfigs/components/configpage`

El proveedor de servicios también debe proporcionar la página de servicio:

`/etc/cloudservices/<service-name>`

### Plantilla {#template}

La plantilla amplía la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

Y defina un `resourceType` que apunte al componente personalizado.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Componentes {#components}

El componente debe ampliar el componente base:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Después de configurar la plantilla y el componente, puede agregar la configuración añadiendo subpáginas en:

`/etc/cloudservices/<service-name>`

### Modelo de contenido {#content-model}

El modelo de contenido se almacena como `cq:Page` en:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Las configuraciones se almacenan en el subnodo `jcr:content`.

* Las propiedades fijas definidas en un cuadro de diálogo deben almacenarse directamente en `jcr:node`.
* Los elementos dinámicos (que utilizan `parsys` o `iparsys`) utilizan un subnodo para almacenar los datos del componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Para obtener documentación de referencia sobre la API, consulte [com.day.cq.wcm.webserviceSupport](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integración de AEM {#aem-integration}

Los servicios disponibles se enumeran en la ficha **Cloud Services** del cuadro de diálogo **Propiedades de página** (de cualquier página que herede de `foundation/components/page` o `wcm/mobile/components/page`).

La pestaña también proporciona lo siguiente:

* un vínculo a la ubicación donde puede habilitar el servicio
* elija una configuración (subnodo del servicio) en un campo de ruta

#### Cifrado de contraseña {#password-encryption}

Al almacenar las credenciales de usuario del servicio, se deben cifrar todas las contraseñas.

Puede conseguirlo si agrega un campo de formulario oculto. Este campo debe tener la anotación `@Encrypted` en el nombre de propiedad; es decir, para el campo `password` el nombre se escribiría como:

`password@Encrypted`

La propiedad será cifrada automáticamente (mediante el servicio `CryptoSupport`) por el `EncryptionPostProcessor`.

>[!NOTE]
>
>Esto es similar a las anotaciones estándar de ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)`.

>[!NOTE]
>
>De manera predeterminada, `EcryptionPostProcessor` solo cifra `POST` solicitudes realizadas a `/etc/cloudservices`.

#### Propiedades adicionales para la página de servicio jcr:nodos de contenido {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Ruta de referencia a un componente que se incluirá automáticamente en la página.<br />: se utiliza para funcionalidad adicional e inclusiones de JS.<br /> Esto incluye el componente en la página donde se incluye <br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> (normalmente antes de la etiqueta <code>body</code>).<br /> En caso de que Adobe Analytics y Adobe Target se comporten de esta manera, se usa para incluir funcionalidades adicionales, como llamadas de JavaScript para rastrear el comportamiento de los visitantes.</td>
  </tr>
  <tr>
   <td>descripción</td>
   <td>Descripción breve del servicio.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Descripción ampliada del servicio.</td>
  </tr>
  <tr>
   <td>clasificación</td>
   <td>Clasificación del servicio que se usa en los anuncios.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filtro para mostrar las configuraciones en el cuadro de diálogo de propiedades de página.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL del sitio web del servicio.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etiqueta para la URL del servicio.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Ruta a la miniatura para el servicio.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Visibilidad en el cuadro de diálogo de propiedades de página; visible de forma predeterminada (opcional)</td>
  </tr>
 </tbody>
</table>

### Casos de uso {#use-cases}

Estos servicios se proporcionan de forma predeterminada:

* [Fragmentos de seguimiento](/help/sites-administering/external-providers.md) (Google, WebTrends, etc.)
* [API de Rest](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte también [Creación de un Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).
