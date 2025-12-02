---
title: Mitigación de problemas de serialización en AEM
description: Obtenga información sobre cómo mitigar los problemas de serialización en AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: eef69d02-2e88-4f44-98bb-d98fa297e3a2
source-git-commit: ffb467630ee061bce5a9cab4e8a311e70b2aeb38
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# Mitigación de problemas de serialización en AEM{#mitigating-serialization-issues-in-aem}

## Información general {#overview}

El equipo de AEM en Adobe trabajó de cerca con el proyecto de código abierto [NotSoSerial](https://github.com/kantega/notsoserial) para ayudar a mitigar las vulnerabilidades descritas en **CVE-2015-7501**. NotSoSerial tiene licencia con la [licencia de Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e incluye código de ASM con licencia con su propia [licencia similar a BSD](https://asm.ow2.io/).

El jar del agente incluido con este paquete es la distribución modificada de NotSoSerial por Adobe.

NotSoSerial es una solución de nivel Java™ para un problema de nivel Java™ y no es específica de AEM. Agrega una comprobación preliminar a un intento de deserializar un objeto. Esta comprobación comprueba el nombre de una clase comparándolo con una lista de permitidos de estilo cortafuegos, una lista de bloqueados o ambas. Debido al número limitado de clases en la lista de bloqueados predeterminada, es poco probable que esta prueba afecte al sistema o al código.

De forma predeterminada, el agente realiza una comprobación de lista de bloqueados frente a las clases vulnerables conocidas actuales. Esta lista de bloqueados pretende protegerle de la lista actual de vulnerabilidades que utilizan este tipo de vulnerabilidad.

La lista de bloqueados y la lista de permitidos se pueden configurar siguiendo las instrucciones de la sección [Configuración del agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de este artículo.

El agente está diseñado para ayudar a mitigar las últimas clases vulnerables conocidas. Si el proyecto está deserializando datos que no son de confianza, puede seguir siendo vulnerable a ataques de denegación de servicio, ataques de falta de memoria y ataques de deserialización futuros desconocidos.

Adobe admite oficialmente Java™ 6, 7 y 8. Sin embargo, Adobe entiende que NotSoSerial también admite Java™ 5.

>[!WARNING]
>
>NotSoSerial no se debe utilizar con Java™ 17 o versiones posteriores.

## Instalación del agente {#installing-the-agent}

>[!NOTE]
>
>Si ya ha instalado la revisión de serialización para AEM 6.1, quite los comandos de inicio del agente de la línea de ejecución de Java™.

1. Instale el paquete **com.adobe.cq.cq-serialization-tester**.

1. Vaya a la consola web del paquete en `https://server:port/system/console/bundles`
1. Busque el paquete de serialización e inícielo. Al hacerlo, se carga automáticamente el agente NotSoSerial.

## Instalación del agente en servidores de aplicaciones {#installing-the-agent-on-application-servers}

El agente NotSoSerial no se incluye en la distribución estándar de AEM para servidores de aplicaciones. Sin embargo, puede extraerlo de la distribución jar de AEM y utilizarlo con la configuración del servidor de aplicaciones:

1. En primer lugar, descargue el archivo de inicio rápido de AEM y extráigalo:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vaya a la ubicación del inicio rápido de AEM recién descomprimido y copie la carpeta `crx-quickstart/opt/notsoserial/` en la carpeta `crx-quickstart` de la instalación del servidor de aplicaciones de AEM.

1. Cambiar la propiedad de `/opt` al usuario que ejecuta el servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure y compruebe que el agente se ha activado correctamente, tal y como se muestra en las siguientes secciones de este artículo.

## Configuración del agente {#configuring-the-agent}

La configuración predeterminada es adecuada para la mayoría de las instalaciones. Esta configuración incluye una lista de bloqueados de clases vulnerables conocidas de ejecución remota y una lista de permitidos de paquetes en los que la deserialización de datos de confianza es segura.

La configuración del cortafuegos es dinámica y se puede cambiar en cualquier momento mediante:

1. Ir a la consola web a las `https://server:port/system/console/configMgr`
1. Buscando y haciendo clic en **Configuración del firewall de deserialización.**

   >[!NOTE]
   >
   >También puede acceder a la página de configuración directamente accediendo a la dirección URL en:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

Esta configuración contiene los registros de lista de permitidos, lista de bloqueados y deserialización.

**Lista de permitidos**

En la sección de lista de permitidos, estos listados son clases o prefijos de paquete que se permiten para la deserialización. Si está deserializando clases propias, agregue las clases o paquetes a esta lista de permitidos.

**Lista de bloqueados**

En la sección de lista de bloques hay clases que nunca se permiten para la deserialización. El conjunto inicial de estas clases se limita a las clases que se han encontrado vulnerables a ataques de ejecución remota. La lista de bloqueados se aplica antes de las entradas de la lista de permitidos.

**Registro de diagnóstico**

En la sección para el registro de diagnóstico, puede elegir varias opciones para registrar cuando se produce la deserialización. Estas opciones solo se registran la primera vez que se utiliza y no se registran de nuevo en los usos posteriores.

El valor predeterminado de **class-name-only** le informa de las clases que se están deserializando.

También puede establecer la opción **full-stack** que registra una pila Java™ del primer intento de deserialización para informarle dónde se está llevando a cabo la deserialización. Esta opción resulta útil para buscar y quitar la deserialización de su uso.

## Verificación de la activación del agente {#verifying-the-agent-s-activation}

Puede verificar la configuración del agente de deserialización navegando hasta la URL en:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Después de acceder a la dirección URL, se muestra una lista de comprobaciones de estado relacionadas con el agente. Puede determinar si el agente está correctamente activado comprobando que las comprobaciones de estado son correctas. Si están fallando, debe cargar el agente manualmente.

Para obtener más información sobre la solución de problemas con el agente, consulte [Gestión de errores al cargar el agente dinámico](#handling-errors-with-dynamic-agent-loading).

>[!NOTE]
>
>Si agrega `org.apache.commons.collections.functors` a la lista de permitidos, la comprobación de estado siempre falla.

## Gestión de errores al cargar el agente dinámico {#handling-errors-with-dynamic-agent-loading}

Si se exponen errores en el registro o los pasos de verificación detectan un problema al cargar el agente, cargue el agente manualmente. Este flujo de trabajo también se recomienda si utiliza un JRE (entorno de tiempo de ejecución de Java™) en lugar de un JDK (kit de herramientas de desarrollo de Java™), ya que las herramientas para la carga dinámica no están disponibles.

Para cargar el agente manualmente, haga lo siguiente:

1. Edite los parámetros de inicio de JVM del JAR de CQ y añada la siguiente opción:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Requiere que también use la opción -nofork CQ/AEM, junto con la configuración de memoria JVM adecuada, ya que el agente no está habilitado en una JVM ramificada.

   >[!NOTE]
   >
   >La distribución de Adobe del JAR del agente NotSoSerial se encuentra en la carpeta `crx-quickstart/opt/notsoserial/` de la instalación de AEM.

1. Detenga y reinicie JVM;

1. Vuelva a comprobar la activación del agente siguiendo los pasos descritos anteriormente en [Verificación de la activación del agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Otras consideraciones {#other-considerations}

Si está ejecutando una JVM de IBM®, revise la documentación sobre la compatibilidad con la API de Java™ Attach en [esta ubicación](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
