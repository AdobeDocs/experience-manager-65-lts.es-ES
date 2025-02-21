---
title: Realización de una actualización in situ
description: Obtenga información sobre cómo realizar una actualización in situ para AEM 6.5.
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Realización de una actualización in situ{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5. Si tiene una instalación implementada en un servidor de aplicaciones, consulte [Pasos de actualización para instalaciones de Application Server](/help/sites-deploying/app-server-upgrade.md).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que el sistema cumple los requisitos de la nueva versión de AEM. Consulte cómo Pattern Detector puede ayudarle a estimar la complejidad de su actualización y también consulte la sección Ámbito de la actualización y Requisitos de [Planificación de su Actualización](/help/sites-deploying/upgrade-planning.md) para obtener más información.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida:** La herramienta de migración solo funciona con las versiones 7 y posteriores de Java. Tenga en cuenta que para AEM 6.3 y versiones posteriores, JRE 8 de Oracle y JRE 7 y 8 de IBM son las únicas versiones compatibles.

* **Instancia actualizada:** Si está actualizando desde una versión **anterior a la 5.6**, asegúrese de haber realizado una actualización local a AEM 6.0 siguiendo el procedimiento descrito en la versión 6.0 de la documentación de actualización.

## Preparación del archivo jar de Quickstart de AEM {#prep-quickstart-file}

1. Detenga la instancia si se está ejecutando.

1. Descargue el nuevo archivo jar de AEM y utilícelo para reemplazar el antiguo fuera de la carpeta `crx-quickstart`.

1. Desempaquete el nuevo JAR de inicio rápido ejecutando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migración del repositorio de contenido {#content-repository-migration}

Esta migración no es necesaria si actualiza desde AEM 6.3. En el caso de las versiones anteriores a la 6.3, Adobe proporciona una herramienta que se puede utilizar para migrar el repositorio a la nueva versión de Oak Segment TAR presente en AEM 6.3. Se proporciona como parte del paquete de inicio rápido y es obligatorio para cualquier actualización que utilice TarMK. Las actualizaciones para entornos que utilizan MongoMK no requieren la migración del repositorio. Para obtener más información sobre las ventajas del nuevo formato de Segment Tar, consulte las [Preguntas frecuentes sobre la migración a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migración real se realiza usando el archivo jar estándar de AEM quickstart, ejecutado con una nueva opción `-x crx2oak` que ejecuta la herramienta crx2oak para simplificar la actualización y hacerla más robusta.

>[!NOTE]
>
>Si está realizando una migración de contenido del repositorio TarMK mediante la extensión de inicio rápido CRX2Oak, puede quitar el modo de ejecución **samplecontent** agregando lo siguiente a la línea de comandos de migración:
>
>* `--promote-runmode nosamplecontent`
>

Para determinar el comando que debe ejecutar, utilice el siguiente comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Donde `<<YOUR_PROFILE>>` y `<<ADDITIONAL_FLAGS>>` se reemplazan con el perfil y los indicadores enumerados en la siguiente tabla:

<table>
 <tbody>
  <tr>
   <td><strong>Repositorio de Source</strong></td>
   <td><strong>Repositorio de destino</strong></td>
   <td><strong>Perfil</strong></td>
   <td><strong>Indicadores adicionales</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 o TarMK con <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Consulte la sección Resolución de problemas a continuación</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK o crx2 con <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>Consulte la sección Resolución de problemas a continuación</td>
  </tr>
  <tr>
   <td>TarMK sin almacén de datos</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No es necesaria ninguna migración</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Donde:**

* `mongo-host` es la IP del servidor MongoDB (por ejemplo, 127.0.0.1)

* `mongo-port` es el puerto del servidor MongoDB (por ejemplo: 27017)

* `mongo-database-name` representa el nombre de la base de datos (por ejemplo: aem-author)

**También es posible que necesite modificadores adicionales para los siguientes escenarios:**

* Si está realizando la actualización en un sistema Windows donde la asignación de memoria Java no se administra correctamente, agregue el parámetro `--disable-mmap` al comando.

Para obtener instrucciones adicionales sobre el uso de la herramienta crx2oak, consulte Uso de la [herramienta de migración de CRX2Oak](/help/sites-deploying/using-crx2oak.md). El JAR de ayuda de crx2oak se puede actualizar manualmente si es necesario, reemplazándolo manualmente por versiones más nuevas después de desempaquetar el inicio rápido. Su ubicación en la carpeta de instalación de AEM es: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La versión más reciente de la herramienta de migración CRX2Oak está disponible para su descarga en el repositorio de Adobe en: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Si la migración se ha completado correctamente, la herramienta se cerrará con un código de salida de cero. Además, compruebe si hay mensajes de ADVERTENCIA y ERROR en el archivo `upgrade.log`, ubicado en `crx-quickstart/logs` en el directorio de instalación de AEM, ya que podrían indicar errores no graves que se produjeron durante la migración.

Compruebe los archivos de configuración debajo de la carpeta `crx-quickstart/install`. Si era necesaria una migración, se actualizarán para reflejar el repositorio de destino.

**Nota sobre almacenes de datos:**

Aunque `FileDataStore` es el nuevo valor predeterminado para las instalaciones de AEM 6.3, no es necesario utilizar un almacén de datos externo. Aunque se recomienda utilizar un almacén de datos externo como práctica recomendada para implementaciones de producción, no es un requisito previo para la actualización. Debido a la complejidad que ya supone actualizar AEM, Adobe recomienda realizar la actualización sin realizar una migración del almacén de datos. Si lo desea, se puede ejecutar posteriormente una migración del almacén de datos como un esfuerzo independiente.

## Solución de problemas de migración {#troubleshooting-migration-issues}

Omita esta sección si actualiza desde la versión 6.3. Aunque los perfiles crx2oak proporcionados deben satisfacer las necesidades de la mayoría de los clientes, hay momentos en que se necesitarán parámetros adicionales. Si se produce un error durante la migración, es posible que haya aspectos del entorno que requieran que se proporcionen opciones de configuración adicionales. Si es así, es probable que se produzca el siguiente error:

No se copiaron **puntos de comprobación porque no se especificó ningún almacén de datos externo. Esto conllevará la reindexación completa del repositorio en el primer inicio. Use —skip-checkpoints para forzar la migración o consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obtener más información.**

Por alguna razón, el proceso de migración necesita acceder a los binarios del almacén de datos y no puede encontrarlo. Para especificar la configuración del almacén de datos, incluya los siguientes indicadores en la parte `<<ADDITIONAL_FLAGS>>` del comando de migración:

**Para almacenes de datos S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Donde `/path/to/SharedS3DataStore.config` representa la ruta al archivo de configuración del almacén de datos S3 y `/path/to/datastore` representa la ruta al almacén de datos S3.

**Para almacenes de datos de archivos:**

```shell
--src-datastore=/path/to/datastore
```

Donde `/path/to/datastore` representa la ruta al almacén de datos de archivos.

## Realización De La Actualización {#performing-the-upgrade}

**Si se usa S3:**

1. Elimine cualquier JAR por debajo de `crx-quickstart/install` asociado con una versión anterior del conector S3.

1. Descargue la última versión del conector S3 1.10.x de [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraiga el paquete en una carpeta temporal y copie el contenido de `jcr_root/libs/system/install` en la carpeta `crx-quickstart/install`.

### Determinar el comando de inicio de actualización correcto {#determining-the-correct-upgrade-start-command}

Para ejecutar la actualización, es importante iniciar AEM con el archivo jar para que se muestre la instancia. Para actualizar a la versión 6.5, consulte otras opciones de reestructuración y migración de contenido en [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) que puede elegir con el comando Actualizar.

>[!IMPORTANT]
>
>Si está ejecutando Oracle Java 11 (o versiones de Java más recientes que 8), se deben agregar modificadores adicionales a la línea de comandos al iniciar AEM. Para obtener más información, consulte [Consideraciones sobre Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Tenga en cuenta que iniciar AEM desde el script de inicio no iniciará la actualización. La mayoría de los clientes inician AEM con la secuencia de comandos de inicio y la han personalizado para incluir modificadores para configuraciones de entorno como la configuración de memoria, los certificados de seguridad, etc. Por este motivo, Adobe recomienda seguir este procedimiento para determinar el comando de actualización adecuado:

1. En una instancia de AEM en ejecución, ejecute lo siguiente desde la línea de comandos:

   ```shell
   ps -ef | grep java
   ```

1. Busque el proceso de AEM. Se verá algo así como:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique el comando reemplazando la ruta al jar existente ( `crx-quickstart/app/aem-quickstart*.jar` en este caso) con el nuevo jar que es secundario de la carpeta `crx-quickstart`. Utilizando nuestro comando anterior como ejemplo, nuestro comando sería:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Esto garantizará que se apliquen todos los ajustes de memoria adecuados, los modos de ejecución personalizados y otros parámetros ambientales para la actualización. Una vez completada la actualización, la instancia se puede iniciar desde el script de inicio en futuros inicios.

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización in situ, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en [Página de actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar comprobaciones posteriores a la actualización y solucionar problemas {#perform-post-upgrade-check-troubleshooting}

Ver [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
