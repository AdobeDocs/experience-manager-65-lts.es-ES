---
title: Ejecutar modos
description: Aprenda a ajustar la instancia de AEM para fines específicos mediante los modos de ejecución.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Ejecutar modos{#run-modes}

Los modos de ejecución permiten ajustar la instancia de AEM para un propósito específico; por ejemplo, crear o publicar, probar, desarrollar, intranet u otros.

Puede hacer lo siguiente:

* [Defina colecciones de parámetros de configuración para cada modo de ejecución](#defining-configuration-properties-for-a-run-mode).

  Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución y, a continuación, puede ajustar conjuntos adicionales para el propósito de su entorno específico. Se aplican según sea necesario.

* [Defina paquetes adicionales para instalar en un modo particular](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Todas las configuraciones y definiciones se almacenan en el único repositorio y se activan estableciendo el **Modo de ejecución**.

## Modos de ejecución de instalación {#installation-run-modes}

Los modos de ejecución de instalación (o fijos) se utilizan en el momento de la instalación y, a continuación, se corrigen durante toda la duración de la instancia; no se pueden cambiar.

Los modos de ejecución de la instalación están disponibles de forma predeterminada:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Son dos pares de modos de ejecución mutuamente excluyentes; por ejemplo, puede:

* definir `author` o `publish`, no ambos al mismo tiempo

* combinar `author` con `samplecontent` o `nosamplecontent` (pero no ambos)

>[!CAUTION]
>
>Al utilizar uno de los modos de ejecución anteriores (author, publish, samplecontent, nosamplecontent), el valor utilizado en el momento de la instalación define el modo de ejecución para *toda la duración* de esa instalación.
>
>Estos modos de ejecución *no pueden* cambiarlos después de la instalación.

## Modos de ejecución personalizados {#customized-run-modes}

También puede crear sus propios modos de ejecución personalizados. Se pueden combinar para cubrir situaciones como las siguientes:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* según sea necesario . .

También se pueden seleccionar modos de ejecución personalizados en cada inicio.

## Uso de samplecontent y nosamplecontent {#using-samplecontent-and-nosamplecontent}

Estos modos permiten controlar el uso del contenido de muestra. El contenido de muestra se define antes de que se genere el inicio rápido y puede incluir paquetes, configuraciones, etc.:

* El modo de ejecución `samplecontent` instala este contenido (el modo predeterminado).

* El modo `nosamplecontent` no instala el contenido de muestra.

El modo de ejecución nosamplecontent está diseñado para instalaciones de producción.

## Definición de propiedades de configuración para un modo de ejecución {#defining-configuration-properties-for-a-run-mode}

Se puede guardar en el repositorio una colección de valores para las propiedades de configuración, utilizados para un modo de ejecución concreto.

El modo de ejecución se indica con un sufijo en el nombre de la carpeta. Esto permite almacenar todas las configuraciones en un repositorio como. Por ejemplo:

* `config`

  Aplicable a todos los modos de ejecución

* `config.author`

  Se utiliza para el modo de ejecución de autor

* `config.publish`

  Se utiliza para el modo de ejecución de publicación

* `config.<run-mode>`

  Se utiliza para el modo de ejecución aplicable; por ejemplo, config

Consulte Configuración de [OSGi en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) para obtener más información sobre cómo definir los nodos de configuración individuales dentro de estas carpetas y crear configuraciones para combinaciones de varios modos de ejecución.

>[!NOTE]
>
>Para [Modos de ejecución de instalación](#installation-run-modes) (por ejemplo, autor), el modo de ejecución no se puede cambiar después de la instalación. Sin embargo, los cambios en las propiedades de configuración individuales surtirán efecto tras el reinicio.

## Definición de paquetes adicionales que se van a instalar para un modo de ejecución {#defining-additional-bundles-to-be-installed-for-a-run-mode}

También se pueden especificar paquetes adicionales que deben instalarse para un modo de ejecución concreto. Para estas definiciones, las carpetas de instalación se utilizan para contener los paquetes. De nuevo, el modo de ejecución se indica con un prefijo:

* `install.author`
* `install.publish`

Estas carpetas son del tipo `nt:folder` y deben contener el paquete apropiado.

## Iniciar CQ con un modo de ejecución específico {#starting-cq-with-a-specific-run-mode}

Si ha definido configuraciones para varios modos de ejecución, debe definir cuál se utilizará al iniciar. Existen varios métodos para especificar qué modo de ejecución utilizar; el orden de resolución es el siguiente:

1. [propiedades del sistema (](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [Detección de nombres de archivo](#filename-detection-renaming-the-jar-file)

Cuando use un servidor de aplicaciones, también puede [definir el modo de ejecución en web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Uso del archivo sling.properties {#using-the-sling-properties-file}

El archivo `sling.properties` se puede usar para definir el modo de ejecución requerido:

1. Edite el archivo de configuración:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Añada las siguientes propiedades; el siguiente ejemplo es para autor:

   `sling.run.modes=author`

### Uso de la opción -r {#using-the-r-option}

Se puede activar un modo de ejecución personalizado utilizando la opción `-r` al iniciar el inicio rápido. Por ejemplo, utilice el siguiente comando para iniciar una instancia de AEM con el modo de ejecución establecido en dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Uso de una propiedad del sistema en el script de inicio {#using-a-system-property-in-the-start-script}

Se puede utilizar una propiedad del sistema en el script de inicio para especificar el modo de ejecución.

* Por ejemplo, utilice lo siguiente para iniciar una instancia como instancia de publicación de producción en Estados Unidos:

  `-Dsling.run.modes=publish,prod,us`

### Detección de nombres de archivo: cambiando el nombre del archivo jar {#filename-detection-renaming-the-jar-file}

Los dos modos de ejecución de instalación siguientes se pueden activar cambiando el nombre del archivo jar de instalación antes de la instalación:

* publicación
* autor

El archivo jar debe utilizar la convención de nombres:

`cq5-<run-mode>-p<port-number>`

Por ejemplo, establezca el modo de ejecución `publish` nombrando el archivo jar:

`cq5-publish-p4503`

### Definición del modo de ejecución en web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Cuando utilice un servidor de aplicaciones, también puede configurar la propiedad:

`sling.run.modes`

en el archivo:

`WEB-INF/web.xml`

Se encuentra en el archivo AEM `war` y debe actualizarse antes de la implementación.

Consulte [Instalar AEM con un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) para obtener más información.
