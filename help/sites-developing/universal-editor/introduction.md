---
title: Editor universal
description: Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias sin encabezado con AEM 6.5 LTS.
feature: Developing
role: Developer
exl-id: 495df631-5bdd-456b-b115-ec8561f33488
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 43%

---

# Acerca del editor universal {#universal-editor}

Obtenga información acerca de la flexibilidad del editor universal y cómo puede ayudarle a potenciar sus experiencias sin encabezado con AEM 6.5 LTS.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores editar lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado.

* Los autores se benefician de la flexibilidad del editor universal. Admite la misma edición visual coherente para todas las formas de contenido sin encabezado de AEM.
* Los desarrolladores se benefician de la versatilidad del editor universal, ya que también admite el desacoplamiento verdadero de la implementación. Permite a los desarrolladores utilizar prácticamente cualquier marco o arquitectura de su elección, sin imponer restricciones SDK o tecnológicas.

Consulte la [documentación de AEM as a Cloud Service sobre el editor universal](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para obtener más información.

## Arquitectura {#architecture}

El editor universal es un servicio que funciona junto con AEM para crear contenido headless.

* El editor universal está alojado en `https://experience.adobe.com/#/aem/editor/canvas` y puede editar páginas procesadas por AEM 6.5 LTS.
* El editor universal lee la página de AEM a través de Dispatcher desde la instancia de autor de AEM.
* El servicio de editor universal, que se ejecuta en el mismo host que Dispatcher, vuelve a escribir los cambios en la instancia de autor de AEM.

![Flujo de autor mediante el editor universal](assets/author-flow.png)

## Requisitos {#requirements}

Lo siguiente es compatible con el editor universal:

* AEM 6.5 LTS GA
   * Se admite el alojamiento On-Premise y de Adobe Managed Services (AMS).
* [AEM 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Se admiten tanto el alojamiento on-premise como el alojamiento AMS.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) (versión `2023.8.13099` o superior)

Este documento se centra en la compatibilidad con AEM 6.5 LTS del editor universal. Para utilizar el editor universal con AEM 6.5 LTS, necesita lo siguiente:

* AEM 6.5 LTS GA
* Dispatcher correctamente configurado

## Configuración {#setup}

Para utilizar el editor universal, haga lo siguiente:

1. [Configure los servicios en la instancia de creación de AEM.](#configure-aem)
1. [Configure un servicio de editor universal local.](#set-up-ue)
1. [Ajuste su Dispatcher para permitir el servicio de editor universal.](#update-dispatcher)

Una vez completada la configuración, puede [instrumentar sus aplicaciones para que utilicen el editor universal.](#instrumentation)

### Configurar servicios {#configure-aem}

El editor universal se basa en una serie de servicios que deben configurarse.

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

#### Configuración del controlador de autenticación del parámetro de consulta de Adobe Granite {#query-parameter}

1. Abra el Administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Controlador de autenticación del parámetro de consulta de Adobe Granite** en la lista y haga clic en **Editar los valores de configuración**.
1. En el campo **Ruta** (`path`), añada `/` para habilitarlo.
   * Un valor vacío deshabilita el controlador de autenticación.
1. Haga clic en **Guardar**.

#### Defina las rutas de contenido o `sling:resourceTypes` que se abrirán en el editor universal {#paths}

1. Abra el administrador de configuración. 
   * `http://<host>:<port>/system/console/configMgr`
1. Busque **Servicio de URL del editor universal** en la lista y haga clic en **Editar los valores de configuración**.
1. Defina para qué rutas de contenido o `sling:resourceTypes` se abrirá el editor universal.
   * En el campo **Asignación de apertura del editor universal**, proporcione las rutas para las que se abre el editor universal.
   * En el campo **Sling:resourceTypes que abrirá el editor universal**, escriba una lista de recursos que el editor universal abrirá directamente.
1. Haga clic en **Guardar**.
1. Compruebe su [configuración del externalizador](/help/sites-developing/externalizer.md) y asegúrese, como mínimo, de que tiene los entornos local, de autor y de publicación establecidos como en el siguiente ejemplo:

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una vez completados estos pasos de configuración, AEM abre el Editor universal para páginas en el siguiente orden:

1. AEM comprueba las asignaciones de `Universal Editor Opening Mapping` y, si el contenido se encuentra en alguna de las rutas definidas, se abre el Editor universal para él.

1. Para el contenido fuera de las rutas definidas en `Universal Editor Opening Mapping`, AEM comprueba si el contenido `resourceType` coincide con una entrada de **Sling:resourceTypes que abrirá el editor universal**. Si coincide, AEM abre el contenido en el editor universal en `${author}${path}.html`.
1. De lo contrario, AEM abre el Editor de páginas.

Las siguientes variables están disponibles para definir las asignaciones en `Universal Editor Opening Mapping`.

* `path`: ruta de contenido del recurso que se abre
* `localhost`: entrada del externalizador para `localhost` sin esquema, por ejemplo, `localhost:4502`
* `author`: entrada de externalizador para el autor sin esquema, por ejemplo, `localhost:4502`
* `publish`: entrada del externalizador para la publicación sin esquema, por ejemplo, `localhost:4503`
* `preview`: entrada del externalizador para vista previa sin esquema, por ejemplo, `localhost:4504`
* `env`: `prod`, `stage`, `dev` según los modos de ejecución de Sling definidos
* `token`: token de consulta necesario para `QueryTokenAuthenticationHandler`

Asignaciones de ejemplo:

* Abra todas las páginas de `/content/foo` en AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Resultados al abrir `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Abra todas las páginas de `/content/bar` en un servidor NextJS remoto y proporcione todas las variables como información
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Resultados al abrir `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configuración del servicio de editor universal {#set-up-ue}

Con AEM actualizado y configurado, puede configurar un servicio de editor universal local para sus procesos de desarrollo y pruebas locales.

1. Instale la versión de Node.js >=20.
1. Descargue y desempaquete el servicio de editor universal más reciente de [Distribución de software](https://experienceleague.adobe.com/es/docs/experience-cloud/software-distribution/home)
1. Configure el servicio de editor universal mediante variables de entorno o el archivo `.env`.
   * [Consulte la documentación del editor universal de AEM as a Cloud Service para obtener más información.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Tenga en cuenta que es posible que necesite utilizar la opción `UES_MAPPING` si se requiere una reescritura de IP interna.
1. Ejecute `universal-editor-service.cjs`

### Actualice Dispatcher {#update-dispatcher}

Con AEM configurado y un servicio de editor universal local en ejecución, debe permitir un proxy inverso para el nuevo servicio [ en Dispatcher.](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher)

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

## Instrumente su aplicación {#instrumentation}

Con AEM actualizado y un servicio de editor universal local en ejecución, puede comenzar a editar contenido headless mediante el editor universal.

Sin embargo, la aplicación debe estar instrumentada para aprovechar las ventajas del editor universal. Incluye metaetiquetas para instruir al editor sobre cómo y dónde conservar el contenido. Los detalles de esta instrumentación están disponibles en la [documentación del editor universal para AEM as a Cloud Service.](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Tenga en cuenta que cuando se sigue la documentación del Editor universal con AEM as a Cloud Service, se aplican los siguientes cambios al utilizarlo con AEM 6.5 LTS.

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
>Para obtener una guía completa para desarrolladores sobre el editor universal, consulte [Información general sobre el editor universal para desarrolladores de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) en la documentación de AEM as a Cloud Service. Tenga en cuenta los cambios de AEM 6.5 LTS que se describen en esta sección.

## Diferencias entre AEM 6.5 LTS y AEM as a Cloud Service {#differences}

El editor universal de AEM 6.5 LTS funciona en términos generales igual que en AEM as a Cloud Service, incluida la interfaz de usuario y gran parte de la configuración. Sin embargo, hay diferencias que debe tener en cuenta.

* El editor universal de 6.5 LTS solo admite el caso de uso sin encabezado.
* La configuración del editor universal varía ligeramente para 6.5 LTS ([como se describe](#setup) en el documento actual).
* El editor universal de 6.5 LTS utiliza un selector de recursos y un selector de fragmentos de contenido diferentes a los de AEM as a Cloud Service.
