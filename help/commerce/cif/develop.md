---
title: Desarrollo de AEM Commerce
description: Obtenga información sobre cómo generar un proyecto de AEM habilitado para el comercio mediante el arquetipo de proyecto de AEM. Aprenda a crear e implementar el proyecto en un entorno de desarrollo local.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 22fcdadf-12c0-4545-a854-76345806386f
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 25%

---

# Desarrollo de AEM Commerce {#develop}

El desarrollo de proyectos de AEM Commerce basados en Commerce integration framework (CIF) para AEM sigue las mismas reglas y prácticas recomendadas que otros proyectos de AEM. Primero revise estos:

- [Guía del usuario de desarrollo de AEM](/help/sites-developing/getting-started.md)
- [Conceptos principales de AEM](/help/sites-developing/the-basics.md)
- [Desarrollo de AEM: directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Cómo crear proyectos de AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Desarrollo local para AEM Commerce {#local}

Se recomienda un entorno de desarrollo local para trabajar con proyectos de CIF.

>[!NOTE]
>
>Las siguientes instrucciones le ayudan a configurar un entorno de desarrollo local de AEM para AEM Commerce mediante CIF con enfoque para AEM 6.5 (LTS). Si usa AEM as a Cloud Service, consulte la [documentación de AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=es).

El complemento de AEM Commerce para AEM, conocido como complemento de CIF, también está disponible para el desarrollo local y se proporciona como paquete de AEM. Se puede descargar del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) como paquete de funciones.

### Software requerido

Lo siguiente debe instalarse de manera local:

- AEM local 6.5 LTS
- [Java 17](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
- [Nodo LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Acceso al complemento de CIF

El complemento de CIF se puede descargar desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Busque &quot;Complemento de AEM Commerce&quot;.

>[!TIP]
>
>Asegúrese de utilizar siempre la última versión del complemento CIF.

### Configuración local

Para el desarrollo de proyectos locales de CIF mediante AEM y el complemento de CIF, siga estos pasos:

1. Desempaquete el archivo .jar de AEM para crear la carpeta `crx-quickstart` , ejecute:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Cree una carpeta `crx-quickstart/install` .

1. Copie todo el paquete del complemento de CIF, descargado del Portal de distribución de software, en la carpeta `crx-quickstart/install`.

>[!TIP]
>
>Como alternativa, el paquete de complementos de CIF también se puede instalar mediante el Administrador de paquetes.

1. Inicio rápido de AEM

Verifique la configuración mediante la consola OSGI: `http://localhost:4502/system/console/osgi-installer`. La lista debe incluir los paquetes relacionados con el complemento de CIF, el paquete de contenido y las configuraciones de OSGI. Asegúrese de que todos los paquetes estén iniciados.

## Configuración del proyecto {#project}

Existen dos maneras de iniciar el proyecto de AEM Commerce con CIF.

### Uso del tipo de archivo del proyecto AEM

El [tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) es la principal herramienta para arrancar un proyecto preconfigurado para comenzar con CIF. Los componentes principales de CIF y todas las configuraciones requeridas se pueden incluir en un proyecto generado con una opción adicional.

>[!TIP]
>
>Utilice un [tipo de archivo del proyecto AEM 25 o posterior](https://github.com/adobe/aem-project-archetype/releases) para generar el proyecto.

Consulte las [instrucciones de uso](https://github.com/adobe/aem-project-archetype#usage) del tipo de archivo del proyecto AEM para saber cómo generar un proyecto AEM. Para incluir CIF en el proyecto, utilice la opción `includeCommerce` .

Por ejemplo:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Los componentes principales de CIF se pueden utilizar en cualquier proyecto incluido el paquete `all` proporcionado o utilizando el paquete de contenido de CIF y los paquetes OSGI relacionados. Para añadir los componentes principales de CIF manualmente a un proyecto, utilice las siguientes dependencias:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Tienda de referencia Venia en AEM

Una segunda opción para el inicio de un proyecto CIF es clonar y utilizar la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia). La Tienda de referencia de Venia de AEM es una aplicación de tienda de referencia que muestra el uso de los componentes principales del CIF de AEM. Está diseñada como un conjunto de ejemplos de prácticas recomendadas y un punto de partida potencial para desarrollar su propia funcionalidad.

Para comenzar con la Tienda de referencia de Venia, simplemente clone el [repositorio Git](https://github.com/adobe/aem-cif-guides-venia) y comience a personalizar el proyecto según sus necesidades.

>[!NOTE]
>
>El proyecto Tienda de referencia de Venia contiene dos perfiles de compilación para AEM as a Cloud Service y AEM 6.5. Compruebe [readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del proyecto para ver cómo se utilizan. Para AEM 6.5, use el perfil `classic`.

### Conexión de AEM al sistema de Commerce

Para conectar el proyecto al sistema de comercio, AEM debe configurarse con el punto final GraphQL del sistema de comercio.

Ambos, un proyecto generado por el [Arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype) o la [Tienda de referencia de Venia en AEM](https://github.com/adobe/aem-cif-guides-venia), ya incluye una [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) que debe ajustarse.

Reemplace el valor de `url` en `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con el extremo GraphQL de su sistema comercial utilizado por el proyecto.

El complemento AEM Commerce y los componentes principales de CIF se conectan al extremo de Commerce GraphQL a través del servidor de AEM y directamente a través del explorador. Los componentes principales de CIF del lado del cliente y las herramientas de creación de complementos de CIF se conectan de forma predeterminada a `/api/graphql`. Si es necesario, esto se puede ajustar a través de la configuración de CIF Cloud Service (consulte a continuación).

El complemento de CIF proporciona un servlet proxy de GraphQL en `/api/graphql`. Si no planea utilizar un Dispatcher de AEM local, se recomienda configurar también el servlet proxy de GraphQL.

Vaya a http://localhost:4502/system/console/configMgr y cree una configuración OSGI para el servicio `Adobe CIF GraphQL Proxy Configuration`. Utilice el mismo punto final de GraphQL de su sistema comercial que se utilizó para el cliente de GraphQL anterior.

## Recursos adicionales

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
