---
title: Pasos de actualización para instalaciones de Application Server
description: Obtenga información sobre cómo actualizar instancias de AEM implementadas mediante servidores de aplicaciones.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 28701105452c347c5470fdb582d783e7aef1adb0
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Pasos de actualización para instalaciones de Application Server {#upgrade-steps-for-application-server-installations}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para la guerra de AEM 6.5 LTS en WLP (WebSphere Liberty).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumple los requisitos de AEM 6.5 LTS. Consulte cómo Analyser puede ayudarle a calcular la complejidad de la actualización y también puede realizar un plan para la actualización (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md) para obtener más información).

### Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida**: Asegúrese de que ha instalado IBM Sumeru JRE 17 en el servidor WLP.

### Realización de la actualización {#performing-the-upgrade}

1. Realice una copia de seguridad de la instancia antes de iniciar cualquier actividad de actualización.
1. Identifique si necesita una actualización in situ o una actualización secundaria según la versión del servidor WLP que esté utilizando. Si el servidor WLP actual es compatible con Servlet 6, puede realizar una actualización in situ y continuar con esta documentación. De lo contrario, debe realizar una degradación lateral. Para la categoría secundaria, siga la migración de contenido con la documentación de actualización de Oak - [vínculo por determinar que se agregará]
1. Detenga la instancia de AEM. Normalmente se puede hacer utilizando este comando:

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. Elimine los archivos y carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son los siguientes:

   * La carpeta `cq-quickstart-65.war` de `dropins` y la carpeta expandida generalmente se encuentran en `<path-to-aem-server>/dropins/cq-quickstart-65.war` y `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`, respectivamente
   * La carpeta `launchpad/startup`. Puede eliminarlo ejecutando el siguiente comando en el terminal suponiendo que se encuentra en la carpeta del servidor:

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * El archivo `base.jar`. Para ello, ejecute los siguientes comandos:

     ```shell
     find crx-quickstart/launchpad -type f -name 
     "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * El archivo `BootstrapCommandFile_timestamp.txt`:

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * Elimine el archivo `sling.options` ejecutando:

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * Quitar el archivo `sling.bootstrap.txt`:

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. Realice una copia de seguridad del archivo `sling.properties` (normalmente presente en `crx-quickstart/conf/`) y elimínelo
1. Cambiar la versión del servlet a **6.0** en el archivo `server.xml`
1. Revise los parámetros de inicio del servidor de AEM y asegúrese de actualizar los parámetros según los requisitos del sistema. Consulte [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md) para obtener más información
1. Instale Java 17 y asegúrese de que está correctamente instalado ejecutando:

   ```shell
   java -version
   ```

1. Descargue el nuevo archivo WAR 6.5 LTS desde Distribución de software y cópielo en la carpeta Dropins ubicada en: `/<path-to-aem-server>/dropins/`
1. Inicie la instancia de AEM: se puede hacer generalmente con este comando:

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. Si tiene cambios personalizados en `sling.properties`, siga las instrucciones siguientes:

   1. Detenga la instancia de AEM ejecutando `<path-to-wlp-directory>/bin/server stop server_name`
   1. Aplicar los cambios personalizados de `sling.properties` al archivo `sling.properties` recién generado (consultando el archivo de copia de seguridad creado en el paso 6)
   1. Inicie la instancia de AEM. Se puede realizar normalmente ejecutando: `<path-to-wlp-directory>/bin/server start server_name`

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización in situ, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en la página [Actualizar código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar Comprobaciones Y Resolución De Problemas Después De La Actualización {#perform-post-upgrade-checks-and-troubleshooting}

Consulte [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) para obtener más información.