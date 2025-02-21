---
title: Pasos de actualización para instalaciones de Application Server
description: Obtenga información sobre cómo actualizar instancias de AEM implementadas mediante servidores de aplicaciones.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Pasos de actualización para instalaciones de Application Server{#upgrade-steps-for-application-server-installations}

En esta sección se describe el procedimiento que debe seguirse para actualizar AEM para instalaciones de Application Server.

Todos los ejemplos de este procedimiento utilizan Tomcat como servidor de aplicaciones e implican que ya tiene implementada una versión de trabajo de AEM. El procedimiento está diseñado para documentar las actualizaciones realizadas desde **AEM versión 6.4 a 6.5**.

1. Primero, inicia TomCat. En la mayoría de los casos, puede hacerlo ejecutando el script de inicio `./catalina.sh`, ejecutando este comando desde el terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Si AEM 6.4 ya está implementado, compruebe que los paquetes funcionan correctamente accediendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. A continuación, anule la implementación de AEM 6.4. Esto se puede hacer desde el Administrador de aplicaciones de TomCat (`http://serveraddress:serverport/manager/html`)

1. Ahora, migre el repositorio con la herramienta de migración crx2oak. Para ello, descargue la versión más reciente de crx2oak desde [esta ubicación](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. Elimine las propiedades necesarias en el archivo sling.properties haciendo lo siguiente:

   1. Abra el archivo ubicado en `crx-quickstart/launchpad/sling.properties`
   1. Texto del paso Elimine las siguientes propiedades y guarde el archivo:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Elimine los archivos y carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son los siguientes:

   * La **carpeta de inicio/bloc de notas**. Puede eliminarlo ejecutando el siguiente comando en el terminal: `rm -rf crx-quickstart/launchpad/startup`

   * El **archivo base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * El **archivo BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Eliminar **sling.options.file** ejecutando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Ahora, cree el almacén de nodos y el almacén de datos que se utiliza con AEM 6.5. Puede hacerlo creando dos archivos con los siguientes nombres bajo `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Estos dos archivos configurarán AEM para utilizar un almacén de nodos TarMK y un almacén de datos de archivo.

1. Edite los archivos de configuración para que estén listos para usarlos. Más concretamente:

   * Agregar la línea siguiente a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

     `customBlobStore=true`

   * Luego agregue las líneas siguientes a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. Ahora debe cambiar los modos de ejecución en el archivo WAR de AEM 6.5. Para ello, cree primero una carpeta temporal que aloje la guerra de AEM 6.5. El nombre de la carpeta en este ejemplo es `temp`. Una vez copiado el archivo WAR, extraiga su contenido ejecutando desde la carpeta temporal:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una vez extraído el contenido, vaya a la carpeta **WEB-INF** y edite el archivo web.xml para cambiar los modos de ejecución. Para encontrar la ubicación donde se establecen en el XML, busque la cadena `sling.run.modes`. Una vez encontrado, cambie los modos de ejecución en la siguiente línea de código, que de forma predeterminada está configurada como author:

   ```bash
   <param-value >author</param-value>
   ```

1. Cambie el valor de autor anterior y establezca los modos de ejecución en: `author,crx3,crx3tar`. El bloque final de código debería tener este aspecto:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Vuelva a crear el frasco con el contenido modificado:

   ```bash
   jar cvf aem65.war
   ```

1. Finalmente, implemente el nuevo archivo de guerra en TomCat.
