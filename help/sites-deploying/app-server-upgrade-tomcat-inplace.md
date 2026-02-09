---
title: Pasos de actualización para las instalaciones del servidor de aplicaciones (Tomcat)
description: Obtenga información sobre cómo actualizar instancias de AEM implementadas mediante Tomcat.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Pasos de actualización para las instalaciones del servidor de aplicaciones (Tomcat: actualización local) {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización (actualización local) de AEM 6.5 LTS a AEM 6.5 LTS Servicepack en Tomcat. Para actualizar de AEM 6.5 a 6.5 LTS, [consulte este enlace](/help/sites-deploying/app-server-upgrade-tomcat.md).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumpla con los [requisitos para el Service Pack de AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md) y vea las [consideraciones sobre la planificación de la actualización](/help/sites-deploying/upgrade-planning.md).


### Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida**: Asegúrese de que ha instalado Oracle® JRE 17/21 en su servidor Tomcat.
* **Servidor Tomcat**: Las versiones compatibles del servidor Tomcat para AEM 6.5 LTS y sus ServicePacks son **10.0.x** y **10.1.x**.

### Realización de la actualización {#performing-the-upgrade}

Todos los ejemplos de este procedimiento utilizan Tomcat como servidor de aplicaciones e implican que ya tiene implementada una versión de trabajo de AEM 6.5 LTS. El procedimiento está diseñado para documentar las actualizaciones realizadas desde la versión de AEM **6.5** LTS a **6.5 LTS** Servicepack.

1. Si AEM 6.5 LTS ya está implementado, compruebe que los paquetes funcionen correctamente accediendo a: *`https://<serveraddress:port>/system/console/bundles`*
1. A continuación, detenga AEM 6.5 LTS. Esto se puede hacer desde el Administrador de aplicaciones Tomcat en: *`https://<serveraddress:port>/manager/html`*
1. Asegúrese de haber completado las [actividades previas a la actualización](#pre-upgrade-steps), como la copia de seguridad del servidor AEM 6.5 LTS, antes de realizar cualquier actividad de actualización
1. Detenga el servidor Tomcat de AEM 6.5 LTS. En la mayoría de los casos, puede hacerlo ejecutando el script `./catalina.sh`, ejecutando este comando desde el terminal:

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. Elimine los archivos y carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son los siguientes:

   * El archivo **cq-quickstart-65.war** y la carpeta `cq-quickstart-65` de la carpeta `webapps` suelen encontrarse en `<path-to-aem-server>/webapps`
   * La carpeta `launchpad/startup`. Puede eliminarlo ejecutando el siguiente comando en el terminal suponiendo que se encuentra en la carpeta del servidor:

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * El archivo `base.jar`. Para ello, ejecute los siguientes comandos:

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * El archivo `BootstrapCommandFile_timestamp.txt`:

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * Elimine el archivo `sling.options` ejecutando:

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * Quitar el archivo `sling.bootstrap.txt`:

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. Realice una copia de seguridad del archivo `sling.properties` (normalmente presente en `<path-to-aem-server>/bin/crx-quickstart/launchpad/`) y elimínelo
1. Copie el archivo WAR de AEM 6.5 LTS Servicepack en la carpeta `<path-to-aem-server>/webapps`
1. Inicie el servidor Tomcat de AEM 6.5 LTS ejecutando:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Monitorice los registros de errores mientras AEM se inicia para comprobar que no haya errores y que AEM se esté ejecutando sin problemas
1. Una vez iniciado AEM 6.5 LTS, compruebe que los paquetes funcionen correctamente accediendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*

## Realizar Comprobaciones Y Resolución De Problemas Después De La Actualización {#perform-post-upgrade-checks-and-troubleshooting}

Consulte [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) para obtener más información.
