---
title: Editor universal
description: Descubre la flexibilidad de Universal Editor y cómo puede ayudarte a potenciar tus experiencias descentralizadas utilizando AEM 6.5 LTS.
feature: Developing
role: Developer
exl-id: 495df631-5bdd-456b-b115-ec8561f33488
source-git-commit: 49922325d3cc993d551683fac1effe9fc9590880
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 42%

---

# Acerca del editor universal {#universal-editor}

Descubre la flexibilidad de Universal Editor y cómo puede ayudarte a potenciar tus experiencias descentralizadas utilizando AEM 6.5 LTS.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores editar lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado.

* Los autores se benefician de la flexibilidad del Editor universal. Soporta la misma edición visual consistente para todas las formas de contenido sin cabeza de AEM.
* Los desarrolladores se benefician de la versatilidad del editor universal, ya que también admite el desacoplamiento verdadero de la implementación. Permite a los desarrolladores utilizar prácticamente cualquier marco o arquitectura de su elección, sin imponer ningún SDK o restricciones tecnológicas.

Consulte la [documentación de AEM as a Cloud Service sobre el editor universal](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para obtener más información.

## Arquitectura {#architecture}

El editor universal es un servicio que funciona junto con AEM para crear contenido headless.

* El Editor Universal está alojado en `https://experience.adobe.com/#/aem/editor/canvas` y puede editar páginas representadas por AEM 6.5 LTS.
* El Editor Universal lee la página AEM a través del Dispatcher desde la instancia del autor de AEM.
* El servicio de editor universal, que se ejecuta en el mismo host que Dispatcher, vuelve a escribir los cambios en la instancia de autor de AEM.

![Flujo de autor mediante el editor universal](assets/author-flow.png)

## Requisitos {#requirements}

Lo siguiente es compatible con el Editor universal:

* AEM 6,5 LTS GA
   * Se admiten el alojamiento en instalaciones y el alojamiento de Adobe Managed Services (AMS)*.
* [AEM 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Tanto el alojamiento en el hotel como AMS* están soportados.
* [AEM como servicio en la nube](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) (versión `2023.8.13099` o superior)

Este documento se centra en AEM compatibilidad con LTS 6.5 del Editor universal. Para utilizar Universal Editor con AEM 6.5 LTS, necesita lo siguiente:

* AEM 6,5 LTS GA
* Dispatcher correctamente configurado

>[!NOTE]
>
>* Si utiliza Adobe Managed Services (AMS), póngase en contacto con el ingeniero de éxito de clientes (CSE) si desea utilizar Universal Editor.

## Configuración {#setup}

Para utilizar Universal Editor, haga lo siguiente:

1. [Configure los servicios en su instancia de creación de AEM.](#configure-aem)
1. [Configure un servicio de editor universal local.](#set-up-ue)
1. [Ajuste Dispatcher para permitir el servicio de Editor universal.](#update-dispatcher)

Una vez completada la configuración, puede [instrumentar sus aplicaciones para que utilicen el editor universal.](#instrumentation)

### Configurar servicios {#configure-aem}

El Editor Universal se basa en una serie de servicios que se deben configurar.

#### Establezca el atributo SameSite para la cookie `login-token`. {#samesite-attribute}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación de token de Adobe Granite** en la lista y haga clic en **Cambiar los valores de configuración**.
1. En el cuadro de diálogo, cambie el atributo **SameSite para el valor de la cookie del token de inicio de sesión** (`token.samesite.cookie.attr`) a `Partitioned`.
1. Haga clic en **Guardar**.

#### Quitar la opción X-Frame de encabezados `SAMEORIGIN`. {#sameorigin}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servlet principal de Apache Sling** en la lista y haga clic en **Editar los valores de configuración**.
1. Elimine el valor `X-Frame-Options=SAMEORIGIN` del atributo **Encabezados de respuesta adicionales** (`sling.additional.response.headers`) si existe.
1. Haga clic en **Guardar**.

#### Configurar el controlador de autenticación del parámetro de consulta de Adobe Granite {#query-parameter}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación del parámetro de consulta de Adobe Granite** en la lista y haga clic en **Editar los valores de configuración**.
1. En el campo **Ruta** (`path`), añada `/` para habilitarlo.
   * Un valor vacío deshabilita el controlador de autenticación.
1. Haga clic en **Guardar**.

#### Definir qué rutas de acceso de contenido o `sling:resourceTypes` se abren en el Editor universal {#paths}

1. Abra el administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servicio de URL del editor universal** en la lista y haga clic en **Editar los valores de configuración**.
1. Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal.
   * En el campo **Asignación de apertura del editor universal**, proporcione las rutas para las que se abre el editor universal.
   * En el campo **Sling:resourceTypes que abrirá el Editor universal**, escriba una lista de recursos que el Editor universal abrirá directamente.
1. Haga clic en **Guardar**.
1. Compruebe la configuración [Externalizer](/help/sites-developing/externalizer.md) y asegúrese como mínimo de que los entornos locales, de autor y de publicación están establecidos como en el ejemplo siguiente:

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una vez completados estos pasos de configuración, AEM abre el Editor universal para las páginas en el siguiente orden:

1. AEM comprueba las asignaciones bajo `Universal Editor Opening Mapping` y si el contenido está bajo cualquier ruta de acceso definida allí, se abre el Editor universal.

1. Para el contenido fuera de las rutas de acceso definidas en `Universal Editor Opening Mapping`, AEM si el contenido `resourceType` coincide con una entrada de **Sling:resourceTypes que abrirá Universal Editor**. Si coincide, AEM abre el contenido en el Editor universal en `${author}${path}.html`.
1. De lo contrario, AEM abre el Editor de páginas.

Las siguientes variables están disponibles para definir las asignaciones en `Universal Editor Opening Mapping`.

* `path`: ruta de contenido del recurso que se abre
* `localhost`: entrada del externalizador para `localhost` sin esquema, por ejemplo, `localhost:4502`
* `author`: entrada del externalizador para el autor sin esquema, por ejemplo, `localhost:4502`
* `publish`: entrada de externalizador para publicación sin esquema, por ejemplo, `localhost:4503`
* `preview`: entrada del externalizador para la vista previa sin esquema, por ejemplo, `localhost:4504`
* `env`: `prod`, `stage`, `dev` según los modos de ejecución de Sling definidos
* `token`: token de consulta necesario para `QueryTokenAuthenticationHandler`

Asignaciones de ejemplo:

* Abra todas las páginas de `/content/foo` en AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Resultados de la apertura de `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Abra todas las páginas de `/content/bar` en un servidor NextJS remoto y proporcione todas las variables como información
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Resultados de la apertura de `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configurar el servicio de edición universal {#set-up-ue}

Con AEM actualizado y configurado, puede configurar un servicio de editor universal local para sus procesos de desarrollo y pruebas locales.

1. Instale la versión de Node.js >=20.
1. Descargar y desempaquetar el último servicio de edición universal de [Software Distribution](https://experienceleague.adobe.com/es/docs/experience-cloud/software-distribution/home)
1. Configurar el servicio de edición universal mediante variables de entorno o archivo `.env`.
   * [Consulte la documentación del editor universal de AEM as a Cloud Service para obtener más información.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Tenga en cuenta que es posible que necesite utilizar la opción `UES_MAPPING` si se requiere una reescritura de IP interna.
1. Ejecute `universal-editor-service.cjs`

### Actualice Dispatcher {#update-dispatcher}

Con AEM configurado y un servicio de editor universal local en ejecución, debe permitir un proxy inverso para el nuevo servicio [&#x200B; en Dispatcher.](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher)

1. Ajuste el archivo vhost de la instancia de autor para incluir un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 es el puerto predeterminado. Si ha cambiado esto usando el parámetro `UES_PORT` en [su archivo `.env`,](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) debe ajustar el valor del puerto aquí en consecuencia.

1. Reinicie Apache.

## Instruir tu aplicación {#instrumentation}

Con AEM actualizado y un servicio de editor universal local en ejecución, puede comenzar a editar contenido headless mediante el editor universal.

Sin embargo, su aplicación debe estar instrumentada para aprovechar el Editor Universal. Se incluyen meta etiquetas para indicar al editor cómo y dónde debe persistir el contenido. Los detalles de esta instrumentación están disponibles en la [documentación del editor universal para AEM as a Cloud Service.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Tenga en cuenta que al seguir la documentación del Editor universal con AEM como servicio de nube, se aplican los siguientes cambios cuando se utiliza con AEM 6.5 LTS.

* El protocolo de la metaetiqueta debe ser `aem65`, en lugar de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* El punto final del servicio del editor universal debe anunciarse mediante una metaetiqueta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* En la sección `plugins` de la definición de componentes, se debe usar `aem65`, en lugar de `aem`.

>[!TIP]
>
>Para obtener una guía completa del desarrollador del Editor universal, vea [Información general del Editor universal para desarrolladores de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) en la documentación de AEM como servicio de nube. Observe los cambios de AEM 6.5 LTS descritos en esta sección.

## Diferencias entre AEM 6.5 LTS y AEM como Cloud Service {#differences}

El Universal Editor de AEM 6.5 LTS funciona en términos generales igual que en AEM como Cloud Service, incluida la interfaz de usuario y gran parte de la configuración. Sin embargo, hay diferencias que debe tener en cuenta.

* El Editor universal en 6.5 LTS admite solo el caso de uso sin encabezado.
* La configuración del Editor universal varía ligeramente para 6.5 LTS ([como se describe](#setup) en el documento actual).
* El editor universal de 6.5 LTS utiliza un selector de recursos y un selector de fragmentos de contenido diferentes a los de AEM as a Cloud Service.
