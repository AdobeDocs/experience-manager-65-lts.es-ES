---
title: Cómo hacer un lanzamiento con su aplicación sin encabezado
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a implementar una aplicación sin encabezado en directo.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 53%

---

# Cómo hacer un lanzamiento con su aplicación sin encabezado {#go-live}

En esta parte del [Recorrido para desarrolladores sin encabezado de AEM](overview.md), aprenda a implementar una aplicación sin encabezado en directo.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo actualizar su contenido a través de las API de AEM Assets](update-your-content.md) ha aprendido a actualizar el contenido sin encabezado existente en AEM mediante la API y ahora debería:

* Comprender la API HTTP de AEM Assets.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto de AEM sin encabezado para su lanzamiento.

## Objetivo {#objective}

Este documento le ayuda a comprender la canalización de las publicaciones de AEM sin encabezado y las consideraciones de rendimiento que debe tener en cuenta antes de lanzar su aplicación.

* Obtenga información acerca de AEM SDK y las herramientas de desarrollo necesarias
* Configure un tiempo de ejecución de desarrollo local para simular el contenido antes de publicarlo
* Comprender los conceptos básicos de almacenamiento en caché y replicación de contenido AEM
* Asegurar y escalar su aplicación antes del lanzamiento
* Monitorizar los problemas de rendimiento y depuración

## El SDK de AEM {#the-aem-sdk}

El SDK de AEM se utiliza para crear e implementar código personalizado. Es la herramienta principal que debe desarrollar y probar su aplicación sin encabezado antes de lanzarla. Contiene los siguientes artefactos:

* Jar de inicio rápido: un archivo Jar ejecutable que se puede utilizar para configurar una instancia de autor y de publicación
* Herramientas de Dispatcher: el módulo de Dispatcher y sus dependencias para sistemas basados en Windows y UNIX
* Jar de API de Java™: la dependencia Jar/Maven de Java™ que expone todas las API de Java™ permitidas que se pueden usar para desarrollarse con AEM
* Javadoc jar: los javadocs para el Jar de la API de Java™

## Herramientas de desarrollo adicionales {#additional-development-tools}

Además de AEM SDK, necesita herramientas adicionales que faciliten el desarrollo y la prueba del código y el contenido de forma local:

* Java™
* Git
* Apache Maven
* La biblioteca Node.js
* El IDE de su elección

Como AEM es una aplicación Java™, debe instalar Java™ y Java™ SDK para admitir el desarrollo de AEM as a Cloud Service.

Git es lo que se utiliza para administrar el control de origen y para registrar los cambios en Cloud Manager y luego implementarlos en una instancia de producción.

AEM utiliza Apache Maven para crear proyectos generados a partir del arquetipo del proyecto Maven de AEM. Todos los IDE principales proporcionan compatibilidad con la integración de Maven.

Node.js es un entorno de tiempo de ejecución de JavaScript que se utiliza para trabajar con los recursos front-end del subproyecto `ui.frontend` de un proyecto de AEM. Node.js se distribuye con npm, que es el administrador de paquetes de facto de Node.js, que se utiliza para administrar las dependencias de JavaScript.

## Generalidades de los componentes del sistema AEM {#components-of-an-aem-system-at-a-glance}

A continuación, veremos las partes que constituyen el entorno de AEM.

Un entorno de AEM completo está formado por un Autor, una Publicación y un Dispatcher. Estos mismos componentes están disponibles en el tiempo de ejecución de desarrollo local para que sea más fácil obtener una vista previa del código y el contenido antes de publicarlos.

* **El servicio de creación** es donde los usuarios internos crean, administran y previsualizan contenido.

* **El servicio de publicación** se considera el entorno &quot;activo&quot; y suele ser con el que interactúan los usuarios finales. El contenido, después de editarse y aprobarse en el servicio de creación, se distribuye (replica) al de publicación. El patrón de implementación más común con las aplicaciones sin encabezado de AEM es tener la versión de producción de la aplicación conectada a un servicio de publicación de AEM.

* **Dispatcher** es un servidor web estático ampliado con el módulo Dispatcher de AEM. Almacena en la caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

## Flujo de trabajo de desarrollo local {#the-local-development-workflow}

El proyecto de desarrollo local se basa en Apache Maven y utiliza Git para el control de código fuente. Para actualizar el proyecto, los desarrolladores pueden utilizar su entorno de desarrollo integrado preferido, como Eclipse, Visual Studio Code o IntelliJ, entre otros.

Para probar las actualizaciones de código o contenido introducidas por la aplicación sin encabezado, implemente las actualizaciones en el tiempo de ejecución local de AEM. Estas incluyen instancias locales de los servicios de autor y publicación de AEM.

Asegúrese de tomar nota de las distinciones entre cada componente en el tiempo de ejecución de AEM local, ya que es vital probar las actualizaciones allí donde sean más importantes. Por ejemplo, pruebe las actualizaciones de contenido en la instancia de autor o pruebe el nuevo código en la instancia de publicación.

En un sistema de producción, Dispatcher y el servidor de HTTP, Apache, siempre estarán frente a una instancia de publicación de AEM. Proporcionan almacenamiento en caché y servicios de seguridad para el sistema AEM, por lo que es fundamental probar el código y las actualizaciones de contenido para Dispatcher también.

## Vista previa del código y el contenido localmente con el entorno de desarrollo local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar el proyecto sin encabezado de AEM para su lanzamiento, asegúrese de que todas las partes constitutivas del proyecto funcionen correctamente.

Para ello, debe reunir todo: código, contenido y configuración, y probarlo en un entorno de desarrollo local para la preparación para el lanzamiento.

El entorno de desarrollo local se compone de tres áreas principales:

1. El proyecto de AEM: contiene todo el código, la configuración y el contenido personalizados en los que trabajarán los desarrolladores de AEM
1. El tiempo de ejecución local de AEM: versiones locales de los servicios de publicación y autor de AEM que se utilizan para implementar código del proyecto de AEM.
1. Tiempo de ejecución de Dispatcher local: una versión local del HTTPD del servidor web Apache que incluye el módulo de Dispatcher.

Una vez configurado el entorno de desarrollo local, puede simular el contenido que se sirve a la aplicación React implementando un servidor de nodos estático localmente.

Para obtener información más detallada sobre la configuración de un entorno de desarrollo local y todas las dependencias necesarias para la vista previa del contenido, consulte [Documentación de implementación de producción](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html).

## Preparación de la aplicación sin encabezado de AEM para el lanzamiento {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Ahora es el momento de preparar su aplicación sin encabezado de AEM para su lanzamiento, siguiendo las prácticas recomendadas que se describen a continuación.

### Proteja su aplicación sin encabezado antes del lanzamiento {#secure-and-scale-before-launch}

1. Prepare [autenticación](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) para sus solicitudes de GraphQL

### Estructura del modelo frente al output de GraphQL {#structure-vs-output}

* Evite crear consultas que generen más de 15 KB de JSON (gzip comprimido). Los archivos JSON largos consumen muchos recursos para que la aplicación cliente los analice.
* Evite más de cinco niveles anidados de jerarquías de fragmento. Los niveles adicionales hacen que a los autores de contenido les resulte difícil considerar el impacto de sus cambios.
* Utilice consultas de varios objetos en lugar de modelar consultas con jerarquías de dependencia dentro de los modelos. Al hacerlo, se obtiene una mayor flexibilidad a largo plazo para reestructurar la salida de JSON sin tener que realizar muchos cambios en el contenido.

### Maximizar la proporción de visitas en caché de CDN {#maximize-cdn}

* No utilice consultas directas de GraphQL, a menos que solicite contenido activo desde la superficie.
   * Utilice consultas persistentes siempre que sea posible.
   * Proporcione un TTL de CDN superior a 600 segundos para que la CDN pueda almacenarlo en caché.
   * AEM calcula el impacto de un cambio de modelo en las consultas existentes.
* Divida los archivos JSON o las consultas de GraphQL entre una tasa de cambio de contenido baja y alta para reducir el tráfico del cliente a CDN y asignar un TTL más alto. Al hacerlo, se minimiza la revalidación por CDN del JSON con el servidor de origen.
* Para invalidar activamente el contenido de la CDN, utilice Depuración suave. Al hacerlo, la CDN puede volver a descargar el contenido sin provocar una pérdida de caché.

>[!NOTE]
>
>Consulte [Recursos adicionales](#additional-resources) para obtener más información sobre CDN y almacenamiento en caché.

### Mejora del tiempo para descargar contenido sin encabezado {#improve-download-time}

* Asegúrese de que los clientes HTTP utilicen HTTP/2.
* Asegúrese de que los clientes HTTP acepten la solicitud de encabezados para gzip.
* Minimice el número de dominios utilizados para alojar el formato JSON y los artefactos de referencia.
* Use `Last-modified-since` para actualizar recursos.
* Use la salida `_reference` en el archivo JSON para iniciar la descarga de los recursos sin tener que analizar los archivos JSON completos.

<!-- End of CDN Review -->

## Implementación de la producción {#deploy-to-production}

La implementación en producción puede depender de si tiene una instancia de AEM *tradicional* que se implementa mediante Maven o si está en Adobe Managed Services (AMS) y, por lo tanto, utiliza Cloud Manager.

## Implementación en producción mediante Maven {#deploy-to-production-maven}

Para una implementación *tradicional* (que no es AMS) que use Maven, consulte el [Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html#build) para obtener una descripción general.

## Implementación en producción mediante Cloud Manager {#deploy-to-production-cloud-manager}

Si es cliente de AMS que usa Cloud Manager, después de asegurarse de que todo está probado y funciona correctamente, puede insertar las actualizaciones de código en un [repositorio Git centralizado en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

Una vez que las actualizaciones se hayan cargado a Cloud Manager, impleméntelas en AEM mediante [la canalización de CD/CI de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=es).

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively - see the [Overview](/help/implementing/deploying/overview.md) to start.
-->

## Monitorización del rendimiento {#performance-monitoring}

Para que los usuarios tengan la mejor experiencia posible al utilizar la aplicación AEM sin encabezado, es importante que monitorice las métricas clave de rendimiento, tal como se detalla a continuación:

* Valide las versiones de producción y previsualización de la aplicación.
* Verifique las páginas de estado de AEM para el estado actual de disponibilidad del servicio.
* Acceda a los informes de rendimiento.
   * Rendimiento de entrega
      * Servidores de origen: número de llamadas, tasas de error, cargas de CPU, tráfico de carga útil
   * Rendimiento del autor
      * Compruebe el número de usuarios, solicitudes y carga
* Acceso a informes de rendimiento específicos de la aplicación y el espacio
   * Una vez que el servidor esté activo, compruebe si las métricas generales son verdes, naranjas o rojas y, a continuación, identifique los problemas específicos de la aplicación.
   * Abra los mismos informes filtrados anteriormente en la aplicación o el espacio (por ejemplo, escritorio de Photoshop, muro de pago).
   * Utilice las API de registro de Splunk para acceder al rendimiento del servicio y de la aplicación.
   * Póngase en contacto con asistencia al cliente en caso de que surjan otros problemas.

## Solución de problemas {#troubleshooting}

### Depuración {#debugging}

Siga estas prácticas recomendadas como enfoque general de la depuración:

* Valide la funcionalidad y el rendimiento con la versión previa de la aplicación.
* Valide la funcionalidad y el rendimiento con la versión de producción de la aplicación.
* Valide con la vista previa JSON del Editor de fragmentos de contenido.
* Para comprobar la presencia de problemas de aplicación o envío de cliente, inspeccione el JSON en la aplicación cliente
* Para comprobar la presencia de problemas relacionados con el contenido almacenado en caché o con AEM, inspeccione el JSON con GraphQL

### Registro de un error con asistencia {#logging-a-bug-with-support}

Para registrar un error de forma eficaz con Asistencia, en caso de que necesite asistencia adicional, complete los siguientes pasos:

* Tome capturas de pantalla del problema, si es necesario.
* Documente una manera de reproducir el problema.
* Documente el contenido con el que se reproduce el problema.
* Registre un problema a través del portal de asistencia de AEM con la prioridad adecuada.

## El recorrido ha terminado, ¿o no? {#journey-ends}

¡Enhorabuena! Ha completado el recorrido para desarrolladores de AEM sin encabezado. Ahora debe comprender lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.
* Qué hacer una vez completado el lanzamiento.

Ya ha iniciado su primer proyecto de AEM sin encabezado o ahora tiene todos los conocimientos para hacerlo. Buen trabajo.

### Explorar aplicaciones de una sola página {#explore-spa}

Sin embargo, no es necesario detener las tiendas sin encabezado en AEM. En la parte de [Introducción del recorrido](getting-started.md#integration-levels), se discutió cómo AEM no solo admite la entrega sin encabezado y los modelos full-stack tradicionales, sino que también admite modelos híbridos que combinan las ventajas de ambos.

Si necesita este tipo de flexibilidad para su proyecto, continúe con la parte opcional adicional del recorrido, [Cómo crear aplicaciones de una sola página (SPA) con AEM.](create-spa.md)

## Recursos adicionales {#additional-resources}

* [Guía de desarrollo de AEM](https://experienceleague.adobe.com/docs/experience-manager-65-lts/developing/introduction/the-basics.html)

* [Tutorial de WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

* [Cloud Manager para AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)

* Caché de CDN

   * [Controlar una caché de CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Configurando la [reescritura de CDN](https://experienceleague.adobe.com/docs/experience-manager-65-lts/deploying/configuring/osgi-configuration-settings.html) (*buscar reescritura de CDN*)

* [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
