---
title: Pasos de actualización para las instalaciones del servidor de aplicaciones (Tomcat)
description: Obtenga información sobre cómo actualizar instancias de AEM implementadas mediante Tomcat.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 7f8de16f-9e9a-4d37-9978-d26c496b911c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Pasos de actualización para las instalaciones del servidor de aplicaciones (Tomcat) {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>Esta página describe el procedimiento de actualización para AEM 6.5 LTS en Tomcat.

## Pasos previos a la actualización {#pre-upgrade-steps}

Antes de ejecutar la actualización, hay que completar varios pasos. Consulte [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) y [Tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obtener más información. Además, asegúrese de que su sistema cumpla los [requisitos de AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md) y vea las [consideraciones sobre la planificación de la actualización](/help/sites-deploying/upgrade-planning.md) y cómo [Analyzer](/help/sites-deploying/pattern-detector.md) puede ayudarle a calcular la complejidad.


### Requisitos previos de migración {#migration-prerequisites}

* **Versión mínima de Java requerida**: Asegúrese de que ha instalado Oracle® JRE 17 en su servidor Tomcat.
* **Servidor Tomcat**: La versión del servidor Tomcat necesaria para 6.5 LTS es **11.0.x**.

### Realización de la actualización {#performing-the-upgrade}

Todos los ejemplos de este procedimiento utilizan Tomcat como servidor de aplicaciones e implican que ya tiene implementada una versión de trabajo de AEM. El procedimiento está diseñado para documentar las actualizaciones realizadas desde la versión de AEM **6.5** a **6.5 LTS**.

1. Si AEM 6.5 ya está implementado, compruebe que los paquetes funcionen correctamente accediendo a: *`https://<serveraddress:port>/system/console/bundles`*
1. A continuación, detenga AEM 6.5. Esto se puede hacer desde el Administrador de aplicaciones Tomcat en: *`https://<serveraddress:port>/manager/html`*
1. Asegúrese de haber completado las [actividades previas a la actualización](#pre-upgrade-steps), como la copia de seguridad del servidor de AEM 6.5, antes de realizar cualquier actividad de actualización
1. Instale Java 17 y asegúrese de que está correctamente instalado ejecutando el comando:

   ```
   java –version
   ```

1. Configuración de un servidor Tomcat compatible con AEM 6.5 LTS
1. Revise los parámetros de inicio del servidor de AEM y asegúrese de actualizar los parámetros según los requisitos del sistema. Consulte [Consideraciones de Java 17](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations) para obtener más información
1. Implemente la guerra 6.5 LTS recién descargada en el servidor Tomcat mediante Java 17 e inicie el servidor AEM 6.5 LTS Tomcat ejecutando:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Una vez que AEM esté en funcionamiento, asegúrese de que todos los paquetes estén en estado de ejecución accediendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*
1. Detenga el servidor Tomcat de AEM 6.5 LTS. En la mayoría de los casos, puede hacerlo ejecutando el script `./catalina.sh`, ejecutando este comando desde el terminal:

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. Ahora migre su contenido de AEM 6.5 a AEM 6.5 LTS siguiendo los pasos aquí: [AEM 6.5 a AEM 6.5 LTS Content Migration Using Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. Una vez migrado el contenido, aplique los cambios personalizados necesarios en el archivo `sling.properties`
1. Inicie el servidor Tomcat de AEM 6.5 LTS ejecutando:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Monitorice los registros de errores mientras AEM se inicia para comprobar que no haya errores y que AEM se esté ejecutando sin problemas
1. Una vez iniciado AEM 6.5 LTS, compruebe que los paquetes funcionen correctamente accediendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*

## Implementar base de código actualizada {#deploy-upgraded-codebase}

Una vez completado el proceso de actualización, se debe implementar la base de código actualizada. Los pasos para actualizar el código base para que funcione en la versión de destino de AEM se encuentran en [Página de actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

## Realizar Comprobaciones Y Resolución De Problemas Después De La Actualización {#perform-post-upgrade-checks-and-troubleshooting}

Consulte [Comprobaciones posteriores a la actualización y solución de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) para obtener más información.
