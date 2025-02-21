---
title: Supervisar las implementaciones de AEM Forms
description: Puede supervisar las implementaciones de formularios AEM Forms tanto a nivel del sistema como a nivel interno. Obtenga más información sobre la supervisión de implementaciones de formularios AEM Forms en este documento.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# Supervisar las implementaciones de AEM Forms {#monitoring-aem-forms-deployments}

Puede supervisar las implementaciones de formularios AEM Forms tanto a nivel del sistema como a nivel interno. Puede utilizar herramientas de administración especializadas como HP OpenView, IBM® Tivoli, CA UniCenter y un monitor JMX de terceros llamado *JConsole* para supervisar específicamente la actividad de Java™. La implementación de una estrategia de monitorización mejora la disponibilidad, la fiabilidad y el rendimiento de las implementaciones de los formularios AEM Forms.

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## Monitorización mediante MBeans {#monitoring-using-mbeans}

AEM Forms proporciona dos MBeans registrados que proporcionan información estadística y de navegación. Estas partes son los únicos MBeans compatibles con la integración y la inspección:

* **ServiceStatistics:** Este MBean proporciona información sobre el nombre del servicio y su versión.
* **OperationStatistics:** Este MBean proporciona las estadísticas de todos los servicios de AEM Forms Server. En este MBean los administradores pueden obtener información sobre un servicio concreto, como el tiempo de invocación y el número de errores.

### Interfaces públicas de ServiceStatisticsMbean {#servicestatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas del MBean ServiceStatistics para realizar pruebas:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas de OperationStatisticsMbean {#operationstatisticmbean-public-interfaces}

Se puede acceder a estas interfaces públicas del MBean OperationStatistics para realizar pruebas:

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### Estadísticas de árbol y funcionamiento de MBean {#mbean-tree-operation-statistics}

Mediante una consola JMX (JConsole), las estadísticas del MBean OperationStatistics están disponibles. Estas estadísticas son atributos de MBean y se pueden navegar en el siguiente árbol de jerarquías:

**Árbol MBean**

**Nombre de dominio de Adobe:** depende del servidor de aplicaciones. Si Application Server no define el dominio, el valor predeterminado es adobe.com.

**ServiceType:** AdobeService es el nombre que se usa para enumerar todos los servicios.

**AdobeServiceName:** nombre de servicio o ID de servicio.

**Versión:** Versión del servicio.

**Estadísticas de operación**

**Tiempo de invocación:** Tiempo empleado para la ejecución del método. Esta invocación no incluye el tiempo en que la solicitud se serializa, se transfiere del cliente al servidor y se deserializa.

**Recuento de invocaciones:** Número de veces que se invoca el servicio.

**Tiempo promedio de invocación:** Tiempo promedio de todas las invocaciones que se han ejecutado desde que se inició el servidor.

**Tiempo máximo de invocación:** Duración de la invocación más larga que se ha ejecutado desde que se inició el servidor.

**Tiempo mínimo de invocación:** Duración de la invocación más corta que se haya ejecutado desde que se inició el servidor.

**Recuento de excepciones:** Número de invocaciones que han producido errores.

**Mensaje de excepción:** Mensaje de error de la última excepción que se produjo.

**Hora de la última fecha de muestreo:** La fecha de la última invocación.

**Unidad de tiempo:** El valor predeterminado es de milisegundos.

Para habilitar la monitorización JMX, los servidores de aplicaciones suelen necesitar alguna configuración. Consulte la documentación del servidor de aplicaciones para conocer los detalles específicos.

### Ejemplos de cómo configurar el acceso JMX abierto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - configurar el inicio de JVM**

Para ver MBeans desde JConsole, configure los parámetros de inicio de JVM del servidor de aplicaciones JBoss. Asegúrese de que JBoss se inicia desde el archivo run.bat/sh.

1. Edite el archivo run.bat ubicado en InstallJBoss/bin.
1. Busque la línea JAVA_OPTS y añada lo siguiente:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configurar el inicio de JVM**

1. Edite el archivo startWebLogic.bat ubicado en `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Busque la línea JAVA_OPTS y añada lo siguiente:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Reinicie WebLogic.

>[!NOTE]
>
>Para WebLogic, puede acceder al MBean mediante Remote o IIOP.

**Acceder al MBean de forma remota**

1. Inicie JConsole para una nueva conexión y haga clic en la pestaña remota.
1. Introduzca el nombre de host y el puerto (9088, el número que especifique durante las opciones de inicio de JVM).

**WebSphere® 6.1: configurar el inicio de JVM**

1. En Admin Console (Application server > server1 > Process Definition > JVM), añada la línea siguiente al campo Argumento de JVM genérico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Añada o quite los comentarios de las tres líneas siguientes en el archivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;Your Websphere JRE>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie WebSphere.
