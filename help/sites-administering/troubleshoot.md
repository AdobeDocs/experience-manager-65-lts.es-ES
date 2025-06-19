---
title: Solución de problemas de Adobe Experience Manager
description: Obtenga información sobre la resolución de algunos problemas que pueden surgir con Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 802130c3-9cb8-46b7-98c2-fd9e83d18ec3
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---

# Solución de problemas de Adobe Experience Manager {#troubleshooting-aem}

La siguiente sección trata algunos problemas que pueden producirse al utilizar AEM (Adobe Experience Manager), así como sugerencias para solucionarlos.

>[!NOTE]
>
>Si está solucionando problemas de creación en AEM, consulte [Solución de problemas para autores.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Si tiene problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) de su instancia (versiones y paquetes de servicio).

## Escenarios de resolución de problemas para administradores {#troubleshooting-scenarios-for-administrators}

En la tabla siguiente se proporciona una descripción general de los problemas que los administradores pueden solucionar:

<table>
 <tbody>
  <tr>
   <td><strong>Función</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Administrador del sistema</td>
   <td><p>Al hacer doble clic en el JAR de inicio rápido no se produce ningún efecto o se abre el archivo JAR con otro programa (por ejemplo, archive manager)</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>Mi aplicación que se ejecuta en CRX genera errores de memoria insuficiente</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> </td>
   <td><p>La pantalla de bienvenida de AEM no se muestra en el explorador después de hacer doble clic en Inicio rápido de AEM CM</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Realización de un volcado de procesos</p> </td>
  </tr>
  <tr>
   <td><p>Administrador del sistema</p> <p>usuario administrador</p> </td>
   <td><p>Comprobación de sesiones JCR sin cerrar</p> </td>
  </tr>
 </tbody>
</table>


## Métodos para el análisis de resolución de problemas {#methods-for-troubleshooting-analysis}

### Realización de un volcado de procesos {#making-a-thread-dump}

El volcado de hilos es una lista de todos los hilos Java™ que están activos actualmente. Si AEM no responde correctamente, el volcado de subprocesos puede ayudarle a identificar interbloqueos u otros problemas.

### Uso del volcado de hilos Sling {#using-sling-thread-dumper}

1. Abra la **consola web de AEM**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione la ficha **Threads** bajo **estado**.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Uso de jstack (línea de comandos) {#using-jstack-command-line}

1. Busque el PID (ID de proceso) de la instancia de AEM Java™.

   Por ejemplo, puede usar `ps -ef` o `jps`.

1. Ejecutar:

   `jstack <pid>`

1. Muestra el volcado de hilos.

>[!NOTE]
>
>Puede anexar los volcados de subprocesos a un archivo de registro utilizando la redirección de salida `>>`:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulte la documentación de [Cómo tomar volcados de procesos de una JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=es) para obtener más información

### Comprobación de sesiones JCR sin cerrar {#checking-for-unclosed-jcr-sessions}

Cuando la funcionalidad está desarrollada para AEM WCM, se pueden abrir sesiones JCR (comparables a la apertura de una conexión a base de datos). Si las sesiones abiertas nunca se cierran, su sistema puede experimentar los siguientes síntomas:

* El sistema se vuelve más lento.
* Puede ver gran parte de CacheManager: resizeAll entradas en el archivo de registro; el siguiente número (size=&lt;x>) muestra el número de cachés, cada sesión abre varias cachés.
* De vez en cuando, el sistema se queda sin memoria (después de unas pocas horas, días o semanas, según la gravedad).

Para empezar a analizar las sesiones no cerradas, consulte el artículo de Knowledge Base [Unclosed Resource Resolver](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23761).

### Uso de la consola web de Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

El estado de los paquetes OSGi también puede proporcionar una indicación temprana de posibles problemas.

1. Abra la **consola web de AEM**; por ejemplo, en `https://localhost:4502/system/console/`.
1. Seleccione **paquetes** en la ficha **OSGI**.
1. Marque:

   * el estado de los paquetes. Si alguno de ellos está Inactivo o Insatisfecho, intente detener y reiniciar el paquete. Si el problema persiste, investigue más a fondo con otros métodos.
   * si alguno de los paquetes tiene dependencias que faltan. Estos detalles se pueden ver haciendo clic en el Nombre del paquete individual, que es un vínculo (el siguiente ejemplo no tiene ningún problema):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
