---
title: Pasos de actualización para las instalaciones del servidor de aplicaciones (WLP)
description: Obtenga información sobre cómo actualizar instancias de AEM implementadas mediante Websphere Liberty.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 2a5d9026-49bc-4766-bcbe-38d834c14f72
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Pasos de actualización para las instalaciones del servidor de aplicaciones (WLP) {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5 LTS en WLP (WebSphere® Liberty).

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumpla los [requisitos de AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

Compruebe [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md) y cómo el [Analizador de AEM](/help/sites-deploying/pattern-detector.md) puede ayudarle a calcular la complejidad de la actualización de AEM.

### Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida**: Asegúrese de que ha instalado IBM® Sumeru JRE 17 en el servidor WLP.

### Realización de la actualización {#performing-the-upgrade}

1. Asegúrese de haber completado los [pasos previos a la actualización](#pre-upgrade-steps), como hacer una copia de seguridad del servidor de AEM 6.5, antes de realizar cualquier actividad de actualización
1. Según sus necesidades, elija una de las siguientes rutas de actualización:
   1. **Actualización in situ**: Si el servidor WLP actual admite Servlet 6, puede realizar una actualización in situ y continuar con el paso 3.
   1. **Versión secundaria**: Si prefiere una configuración nueva o si el servidor WLP no es compatible con Servlet 6, configure una nueva instancia WLP con AEM 6.5 LTS y migre el contenido siguiendo la guía [AEM 6.5 a AEM 6.5 LTS Content Migration Using Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md) y vaya a la sección [Implementar base de código actualizada](#deploy-upgraded-codebase)

1. Detenga la instancia de AEM. Normalmente se puede hacer utilizando este comando:

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. Elimine los archivos y carpetas que ya no sean necesarios. Los elementos que debe eliminar específicamente son los siguientes:

   * **cq-quickstart-65.war** de la carpeta `dropins` y la carpeta `expanded` se encuentran generalmente en `<path-to-aem-server>/dropins/cq-quickstart-65.war` y `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war` respectivamente
   * La carpeta `launchpad/startup`. Puede eliminarlo ejecutando el siguiente comando en el terminal suponiendo que se encuentra en la carpeta del servidor:

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * El archivo `base.jar`. Para ello, ejecute los siguientes comandos:

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
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
1. Instale Java 17 y asegúrese de que está correctamente instalado ejecutando:

   ```shell
   java -version
   ```

1. Revise los parámetros de inicio del servidor de AEM y asegúrese de actualizar los parámetros según sus necesidades. Consulte [Consideraciones de Java 17](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations) para obtener más información
1. Descargue el nuevo archivo WAR de 6.5 LTS y cópielo en la carpeta de puntos ubicada en: `/<path-to-aem-server>/dropins/`
1. Inicie la instancia de AEM: se puede hacer generalmente con este comando:

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. Si tiene cambios personalizados en `sling.properties`, siga las instrucciones siguientes:

   1. Detenga la instancia de AEM ejecutando `<path-to-wlp-directory>/bin/server stop server_name`
   1. Aplicar los cambios personalizados de `sling.properties` al archivo `sling.properties` recién generado (consultando el archivo de copia de seguridad creado en el paso 5)
   1. Inicie la instancia de AEM. Se puede realizar normalmente ejecutando: `<path-to-wlp-directory>/bin/server start server_name`

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en [Página de actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar Comprobaciones Y Resolución De Problemas Después De La Actualización {#perform-post-upgrade-checks-and-troubleshooting}

Ver [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
