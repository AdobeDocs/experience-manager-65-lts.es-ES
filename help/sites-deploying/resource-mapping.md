---
title: Asignación de recursos
description: Obtenga información sobre cómo definir redirecciones, URL mnemónicas y hosts virtuales para Adobe Experience Manager mediante la asignación de recursos.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 90558227-c2c2-4130-9031-03efda5b1d94
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# Asignación de recursos{#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, URL personales y hosts virtuales para Adobe Experience Manager (AEM).

Por ejemplo, puede utilizar estas asignaciones para lo siguiente:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a la página `/content/en/gateway` de su sitio web se redirijan a `https://gbiv.com/`.

Una posible asignación HTTP prefija todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes del sitio web, ya que permite lo siguiente:

`localhost:4503/content/we-retail/en/products.html`

Para acceder a él, utilice:

`localhost:4503/we-retail/en/products.html`

Como la asignación agrega automáticamente el prefijo `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Las URL mnemónicas no admiten patrones de regex.

>[!NOTE]
>
>Consulte la documentación de Sling y [Asignaciones para la resolución de recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) y [Recursos](https://sling.apache.org/documentation/the-sling-engine/resources.html) para obtener más información.

## Visualización de definiciones de asignación {#viewing-mapping-definitions}

Las asignaciones de dos listas que evalúa el JCR Resource Resolver (de arriba a abajo) para encontrar una coincidencia.

Estas listas se pueden ver (junto con información de configuración) en la opción **JCR ResourceResolver** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración
Muestra la configuración actual (tal como se definió para [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prueba de configuración
Esto permite introducir una dirección URL o una ruta de recurso. Haga clic en **Resolver** o en **Mapa** para confirmar cómo transformará el sistema la entrada.

* **Entradas de mapa de resolución**
La lista de entradas utilizadas por los métodos ResourceResolver.resolve para asignar direcciones URL a recursos.

* **Entradas de asignación de asignaciones**
La lista de entradas utilizadas por los métodos ResourceResolver.map para asignar rutas de recursos a las direcciones URL.

Las dos listas muestran varias entradas, incluidas las definidas como predeterminadas por las aplicaciones. Normalmente, pretenden simplificar las direcciones URL del usuario.

Las listas emparejan un **Pattern**, una expresión regular que coincide con la solicitud, con un **Replacement** que define la redirección que se va a imponer.

Por ejemplo, el:

**Patrón** `^[^/]+/[^/]+/welcome$`

Almacenará en déclencheur:

**Reemplazo** `/libs/cq/core/content/welcome.html`.

Para redirigir una solicitud:

`https://localhost:4503/welcome` &quot;

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Se crean nuevas definiciones de asignación dentro del repositorio.

>[!NOTE]
>
>Hay muchos recursos disponibles para explicar cómo definir las expresiones regulares. Por ejemplo, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creación de definiciones de asignación en AEM {#creating-mapping-definitions-in-aem}

En una instalación estándar de AEM puede encontrar la carpeta:

`/etc/map/http`

Esta es la estructura que se utiliza al definir asignaciones para el protocolo HTTP. Se pueden crear otras carpetas ( `sling:Folder`) en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefija cualquier solicitud a https://localhost:4503/ con `/content`:

1. Usando CRXDE, vaya a `/etc/map/http`.

1. Cree un nodo:

   * **Tipo** `sling:Mapping`
Este tipo de nodo está diseñado para este tipo de asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **Agregar** las siguientes propiedades a este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`

   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String[]`

      * **Valor** `/content/`

1. Haga clic en **Guardar todo**.

Esto administra una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/documentation/the-sling-engine/resources.html) en la documentación de Sling para obtener más información sobre las propiedades de Sling disponibles y cómo se pueden configurar.

>[!NOTE]
>
>Puede usar `/etc/map.publish` para guardar las configuraciones del entorno de publicación. Se deben replicar y se debe configurar la nueva ubicación (`/etc/map.publish`) para la **ubicación de asignación** del [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) del entorno de publicación.
