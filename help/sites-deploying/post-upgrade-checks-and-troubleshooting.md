---
title: Comprobaciones posteriores a la actualización y solución de problemas
description: Obtenga información sobre cómo solucionar problemas que podrían aparecer después de una actualización.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8b3d8d0f-10f7-4736-881d-8f1f21c69182
source-git-commit: a037dc7cbb13abfeb8a7289baded50d3d788cbf6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Comprobaciones posteriores a la actualización y solución de problemas{#post-upgrade-checks-and-troubleshooting}

## Comprobaciones posteriores a la actualización {#post-upgrade-checks}

Después de la [actualización in situ](/help/sites-deploying/in-place-upgrade.md), se deben ejecutar las siguientes actividades para finalizar la actualización. Se supone que AEM se ha iniciado con el JAR de AEM 6.5 LTS y que se ha implementado la base de código actualizada.

* [Verificar registros para que la actualización se realice correctamente](#verify-logs-for-upgrade-success)

* [Verificar paquetes OSGi](#verify-osgi-bundles)

* [Verificar la versión de Oak](#verify-oak-version)

* [Validación inicial de páginas](#initial-validation-of-pages)

* [Verificar las configuraciones de mantenimiento programadas](#verify-scheduled-maintenance-configurations)

* [Habilitar agentes de replicación](#enable-replication-agents)

* [Habilitar trabajos programados personalizados](#enable-custom-scheduled-jobs)

* [Ejecutar plan de prueba](#execute-test-plan)


### Verificación de registros para actualización correcta {#verify-logs-for-upgrade-success}

**actualización.log**

En el pasado, la inspección del estado posterior a la actualización de la instancia requería una inspección cuidadosa de varios archivos de registro, partes del repositorio y el Launchpad. La generación de un informe posterior a la actualización puede ayudar a detectar actualizaciones defectuosas antes de activarse.

El propósito principal de esta función es reducir la necesidad de interpretación manual o de lógica de análisis compleja en varios extremos necesarios para calificar el éxito de una actualización. La solución tiene como objetivo proporcionar información inequívoca para que los sistemas de automatización externos reaccionen ante el éxito o el fracaso identificado de una actualización.

Más concretamente, garantiza que:

* Los errores de actualización detectados por el marco de actualización están centralizados en un único informe de actualización.
* El informe de actualización incluye indicadores sobre la intervención manual necesaria.

Para dar cabida a esto, se han realizado cambios en la forma en que se generan los registros en el archivo `upgrade.log`.

**error.log**

El error.log debe revisarse cuidadosamente durante y después del inicio de AEM con el JAR de versión de destino. Deben revisarse todas las advertencias o errores. En general, es mejor buscar problemas al principio del registro. Los errores que se producen más adelante en el registro pueden ser en realidad efectos secundarios de una causa raíz que se llama al principio del archivo. Si se producen errores y advertencias repetidos, consulte a continuación [Análisis de problemas con la actualización](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificar paquetes OSGi {#verify-osgi-bundles}

Vaya a la consola OSGi `/system/console/bundles` y compruebe si no se han iniciado los paquetes. Si algún paquete está en estado instalado, consulte `error.log` para determinar el problema de raíz.

### Verificar la versión de Oak {#verify-oak-version}

Después de la actualización, debería ver que la versión de Oak se ha actualizado a **1.68.x**. Para comprobar la versión de Oak, vaya a la consola OSGi y observe la versión asociada a los paquetes de Oak: Oak Core, Oak Commons, Segment TAR de Oak.

### Validación inicial de páginas {#initial-validation-of-pages}

Realice una validación inicial en varias páginas de AEM. Si actualiza un entorno de creación, abra la página de inicio y la página de bienvenida ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). En los entornos de creación y publicación, abra algunas páginas de aplicación y pruebe a fumar para que se representen correctamente. Si ocurre algún problema, consulte `error.log` para solucionar los problemas.

### Verificar las configuraciones de mantenimiento programadas {#verify-scheduled-maintenance-configurations}

#### Activar recolección de basura del almacén de datos {#enable-data-store-garbage-collection}

Si utiliza un almacén de datos de archivos, asegúrese de que la tarea de recolección de elementos no utilizados del almacén de datos esté habilitada y agregada a la lista de mantenimiento semanal. Las instrucciones se describen en [Limpieza de revisión](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Esto no se recomienda para instalaciones de almacenes de datos personalizados S3 o cuando se utiliza un almacén de datos compartido.

#### Activar Limpieza de revisión en línea {#enable-online-revision-cleanup}

Si utiliza MongoMK o el nuevo formato de segmento TarMK, asegúrese de que la tarea Revision Clean Up esté activada y se añada a la lista de mantenimiento diario. Las instrucciones se describen en [Limpieza de revisión](/help/sites-deploying/revision-cleanup.md).

### Habilitar agentes de replicación {#enable-replication-agents}

Una vez que el entorno de publicación se haya actualizado y validado completamente, habilite los agentes de replicación en el entorno de creación. Compruebe que los agentes puedan conectarse a las respectivas instancias de publicación. Consulte [Procedimiento de actualización](/help/sites-deploying/upgrade-procedure.md) para obtener más información sobre el orden de los eventos.

### Habilitar trabajos programados personalizados {#enable-custom-scheduled-jobs}

Cualquier trabajo programado como parte de la base de código puede habilitarse en este momento.

### Ejecutar plan de prueba {#execute-test-plan}

Ejecute el plan de pruebas detallado definido en [Actualización del código y las personalizaciones en la sección **Procedimiento de pruebas**](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure).

## Análisis De Problemas Con La Actualización {#analyzing-issues-with-the-upgrade}

Esta sección contiene algunos escenarios de problemas que se pueden presentar durante el procedimiento de actualización a AEM 6.5 LTS.

### Los paquetes no se pueden actualizar  {#packages-and-bundles-fail-to-update}

Si los paquetes no se instalan durante la actualización, los paquetes que contienen tampoco se actualizarán. Esta categoría de problemas se debe a una configuración incorrecta del almacén de datos. También aparecerán como mensajes de **ERROR** y **ADVERTENCIA** en el error.log. Dado que en la mayoría de estos casos el inicio de sesión predeterminado puede no funcionar, puede utilizar CRXDE directamente para inspeccionar y encontrar los problemas de configuración.

### La Actualización No Se Ha Ejecutado {#the-upgrade-did-not-run}

Antes de iniciar los pasos de preparación, asegúrese de ejecutar primero la instancia de **source** ejecutándola con el comando `java -jar aem-quickstart.jar`. Esto es necesario para asegurarse de que el archivo quickstart.properties se genera correctamente. Si falta, la actualización no funcionará. También puede comprobar si el archivo está presente mirando en `crx-quickstart/conf` en la carpeta de instalación de la instancia de origen. Además, al iniciar AEM para iniciar la actualización, debe ejecutarse con el comando `java -jar <aem-quickstart-6.5-LTS.jar>`. Al iniciar desde un script de inicio, AEM no se iniciará en el modo de actualización.

### Algunos paquetes de AEM no cambian al estado activo {#some-aem-bundles-are-not-switching-to-the-active-state}

Si hay paquetes que no se inician, compruebe si hay dependencias no satisfechas.

En caso de que este problema esté presente, pero se basa en una instalación fallida del paquete que provocó que los paquetes no se actualizaran, se considerarán incompatibles para la nueva versión. Para obtener más información sobre cómo solucionar este problema, consulte **Error al actualizar paquetes y paquetes** más arriba.

También se recomienda comparar la lista de paquetes de una instancia nueva de AEM 6.5 LTS con la actualizada para detectar los paquetes que no se actualizaron. Esto proporcionará un ámbito más cercano de lo que se debe buscar en `error.log`.

### Los paquetes personalizados no cambian al estado activo {#custom-bundles-not-switching-to-the-active-state}

En caso de que los paquetes personalizados no cambien al estado activo, lo más probable es que haya código que no importe la API modificada. Esto suele dar lugar a dependencias no satisfechas.

También es mejor comprobar si el cambio que ha causado el problema fue necesario y revertirlo si no lo es. Compruebe también si el aumento de versión del paquete de exportación se ha aumentado más de lo necesario, siguiendo un control de versiones semántico estricto.

### Analizando error.log y upgrade.log {#analyzing-the-error.log-and-upgrade.log}

En la mayoría de los casos, es necesario consultar los registros para detectar errores y encontrar la causa del problema. Sin embargo, con las actualizaciones, también es necesario monitorizar los problemas de dependencia, ya que es posible que los paquetes antiguos no se actualicen correctamente.

La mejor manera de hacerlo es eliminar el error.log eliminando todos los mensajes que se espera que no estén relacionados con el problema que está enfrentando. Puede hacerlo mediante una herramienta como grep, usando:

```shell
grep -v UnrelatedErrorString
```

Algunos mensajes de error pueden no ser inmediatamente explicativos. En este caso, observar el contexto en el que se producen también puede ayudar a comprender dónde se creó el error. Puede separar el error mediante lo siguiente:

* `grep -B` por agregar líneas antes del error;

o

* `grep -A` para agregar líneas después de.

En algunos casos, también se pueden encontrar mensajes WARN, ya que puede haber casos válidos que conduzcan a este estado y la aplicación no siempre puede decidir si se trata de un error real. Asegúrese de consultar también estos mensajes.

### Contactar con el servicio de soporte técnico de Adobe {#contacting-adobe-support}

Si ha seguido los consejos de esta página y sigue teniendo problemas, póngase en contacto con el Soporte técnico de Adobe. Para proporcionar la mayor cantidad de información posible al ingeniero de soporte técnico que trabaja en su caso, asegúrese de incluir los archivos de `error.log` y `upgrade.log` de su actualización.
