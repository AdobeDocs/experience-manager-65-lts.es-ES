---
title: Realización de una actualización in situ
description: Obtenga información sobre cómo realizar una actualización in situ para AEM 6.5 LTS.
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Realización de una actualización in situ {#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5 LTS. Si tiene una instalación implementada en un servidor de aplicaciones, consulte [Pasos de actualización para instalaciones de Application Server](/help/sites-deploying/app-server-upgrade.md).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumple los requisitos de AEM 6.5 LTS. Consulte cómo el Analizador puede ayudarle a estimar la complejidad de su actualización y también consulte la sección Ámbito y requisitos de la actualización de [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md) para obtener más información.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida:** Asegúrese de que tiene instalado el JRE 17 de Oracle en su sistema.

## Preparación del archivo jar de Quickstart de AEM {#prep-quickstart-file}

1. Detenga la instancia si se está ejecutando

1. Descargue el nuevo archivo jar AEM 6.5 LTS y utilícelo para reemplazar el antiguo fuera de la carpeta `crx-quickstart`

1. Realice una copia de seguridad del archivo `sling.properties` (normalmente presente en `crx-quickstart/conf/`) y elimínelo

1. Desempaquete el nuevo JAR de inicio rápido ejecutando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. El comando desempaquetar generará un nuevo archivo de `sling.properties` en la carpeta `crx-quickstart/conf/`. Ahora puede aplicar los cambios personalizados al archivo `sling.properties` recién generado.

<!-- Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## Realización De La Actualización {#performing-the-upgrade}

**Si se usa S3:**

1. Elimine cualquier JAR por debajo de `crx-quickstart/install` asociado con una versión anterior del conector S3.

1. Descargue la última versión del conector 1.60.2 S3 desde [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->

1. Extraiga el conector S3 (versión 1.60.2) y copie el contenido de las siguientes carpetas en `crx-quickstart/install`, de la siguiente manera:

   1. Copiar `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1` en `crx-quickstart/install/1`
   1. Copiar `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15` en `crx-quickstart/install/15`

Ahora, inicie la instancia de AEM con el nuevo comando determinado mediante la información de la sección [Determinación del comando de inicio de actualización correcto](#determining-the-correct-upgrade-start-command).

### Determinar el comando de inicio de actualización correcto {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>La compatibilidad con algunos de los argumentos de Java 8/11 se ha eliminado en Java 17. Consulte Consideraciones sobre los argumentos de Java para AEM 6.5 LTS (código auxiliar de vínculo).

Para ejecutar la actualización, es importante iniciar AEM con el archivo jar para que se muestre la instancia.

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
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.6.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Esto garantizará que se apliquen todos los ajustes de memoria adecuados, los modos de ejecución personalizados y otros parámetros ambientales para la actualización. Una vez completada la actualización, la instancia se puede iniciar desde el script de inicio en futuros inicios.

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización in situ, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en [Página de actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar comprobaciones posteriores a la actualización y solucionar problemas {#perform-post-upgrade-check-troubleshooting}

Ver [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
