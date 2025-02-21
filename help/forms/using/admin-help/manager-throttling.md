---
title: Administrador de trabajo y regulación
description: Este documento proporciona información general sobre Work Manager y proporciona instrucciones sobre cómo configurar las opciones de regulación de Work Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# Administrador de trabajo y regulación{#work-manager-and-throttling}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los formularios de AEM (y las versiones anteriores) utilizaban colas de JMS para ejecutar operaciones de forma asíncrona. En los formularios AEM, las colas de JMS se han reemplazado por Work Manager. Este documento proporciona información general sobre Work Manager y proporciona instrucciones sobre cómo configurar las opciones de regulación de Work Manager.

## Acerca de las operaciones de larga duración (asincrónicas) {#about-long-lived-asynchronous-operations}

En los formularios AEM Forms, las operaciones realizadas por los servicios pueden ser de corta duración (sincrónicas) o de larga duración (asincrónicas). Las operaciones de corta duración se completan sincrónicamente en el mismo subproceso desde el que se invocaron. Estas operaciones esperan una respuesta antes de continuar.

Las operaciones de larga duración pueden abarcar sistemas o incluso extenderse más allá de la organización, como cuando un cliente debe completar y enviar un formulario de solicitud de préstamo como parte de una solución más grande que integra múltiples tareas automatizadas y humanas. Estas operaciones deben continuar mientras se espera una respuesta. Las operaciones de larga duración realizan su trabajo subyacente de forma asíncrona, lo que permite comprometer los recursos mientras esperan su finalización. A diferencia de las operaciones de corta duración, Work Manager no considera que una operación de larga duración se haya completado una vez que se invoca. Para completar la operación, debe producirse un déclencheur externo, como un sistema que solicita otra operación en el mismo servicio o un usuario que envía un formulario.

## Acerca de Work Manager {#about-work-manager}

Los formularios de AEM (y las versiones anteriores) utilizaban colas de JMS para ejecutar operaciones de forma asíncrona. Los formularios AEM Forms utilizan Work Manager para programar y ejecutar operaciones asincrónicas mediante subprocesos administrados.

Las operaciones asincrónicas se gestionan de esta manera:

1. Work Manager recibe un elemento de trabajo para su ejecución.
1. Work Manager almacena el elemento de trabajo en una tabla de la base de datos y le asigna un identificador único. El registro de la base de datos contiene toda la información necesaria para ejecutar el elemento de trabajo.
1. Los hilos del Administrador de trabajos extraen elementos de trabajo cuando los hilos quedan libres. Antes de extraer los elementos de trabajo, los subprocesos pueden comprobar si se han iniciado los servicios necesarios, si hay suficiente tamaño de pila para extraer el siguiente elemento de trabajo y si hay suficientes ciclos de CPU para procesar el elemento de trabajo. Work Manager también evalúa los atributos del elemento de trabajo (como su prioridad) al programar su ejecución.

Los administradores de formularios de AEM pueden utilizar el Monitor de estado para comprobar las estadísticas de Work Manager, como el número de elementos de trabajo en la cola y sus estados. También puede utilizar el Monitor de estado para pausar, reanudar, reintentar o eliminar elementos de trabajo. (Consulte [Ver estadísticas relacionadas con Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configurar las opciones de regulación de Work Manager {#configuring-work-manager-throttling-options}

Puede configurar la restricción para Work Manager, de modo que los elementos de trabajo se programen únicamente cuando haya suficientes recursos de memoria disponibles. Puede configurar la restricción estableciendo las siguientes opciones de JVM en su servidor de aplicaciones.

<table>
 <thead>
  <tr>
   <th><p>Propiedad</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>Especifica el intervalo de tiempo, en milisegundos, que Work Manager utiliza al buscar nuevos elementos en la cola.</p><p>El valor de esta opción es un número entero. El valor predeterminado es <code>1000</code> milisegundos (1 segundo). </p><p>Si el volumen de invocaciones asincrónicas es bajo, puede aumentar este valor. Por ejemplo, puede aumentarlo a un valor entre 2000 y 5000 (de 2 a 5 segundos). </p><p>Si el volumen de invocaciones asincrónicas es alto, el valor predeterminado debería ser suficiente, pero puede utilizar un valor inferior si es necesario. Reducir demasiado este valor (por ejemplo, por debajo de 50, lo que resulta en una frecuencia de encuesta de 20 veces por segundo) provoca una sobrecarga sustancial en el sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Establezca esta opción en <code>true</code> para habilitar el modo de depuración, o en false para deshabilitarlo. </p><p>En el modo de depuración, se registran los mensajes relativos a las infracciones de directivas de Work Manager y a las acciones de pausa/reanudación de Work Manager. Establezca esta opción en true solo cuando solucione problemas.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Establezca esta opción en <code>true</code> para habilitar la restricción basada en la configuración de control de memoria que se describe a continuación, o en <code>false</code> para deshabilitar la restricción.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que puede estar en uso antes de que Work Manager restrinja los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>95</code>. Este valor debería ser correcto para la mayoría de los sistemas. Auméntelo solo si su sistema necesita alcanzar su capacidad máxima. Pero tenga en cuenta que, a medida que aumenta este valor, también aumenta el riesgo de problemas de Memoria insuficiente.</p><p>Si está ejecutando formularios AEM Forms en un entorno en clúster, puede que desee establecer la configuración del límite de control de memoria de forma diferente en distintos nodos del clúster. Por ejemplo, podría tener un límite superior inferior en los nodos A y B, que están programados en el equilibrador de carga para el trabajo interactivo. Y podría tener límites altos más altos establecidos en los nodos C y D, que no son utilizados por el equilibrador de carga, sino reservados para el trabajo asincrónico.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que puede estar en uso antes de que Work Manager deje de limitar los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>20</code>. Este valor debería ser correcto para la mayoría de los sistemas.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Especifica el tamaño máximo del lote para workmanager. El tamaño predeterminado del lote es 10.</p><p>Si el estado de un proceso en el administrador de trabajo no se actualiza incluso después de que se haya completado la tarea, establezca el tamaño del lote en 1.</p></td>
  </tr>
 </tbody>
</table>

**Agregar opciones de Java a JBoss**

1. Detenga el servidor de aplicaciones JBoss.
1. Abra *[appserver root]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y agregue cualquiera de las opciones de Java según sea necesario, en el formato `-Dproperty=value`.
1. Reinicie el servidor.

**Agregar opciones de Java a WebLogic**

1. Inicie la consola de administración de WebLogic escribiendo `https://[host name]:[port]/console` en un explorador web.
1. Escriba el nombre de usuario y la contraseña que ha creado para el dominio de WebLogic Server y haga clic en Registrar en Centro de cambios y haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en la pestaña Configuración > pestaña Inicio del servidor.
1. En el cuadro Argumentos, agregue los argumentos necesarios al final del contenido actual. Por ejemplo, para deshabilitar el Monitor de estado, agregue:

   `-Dadobe.healthmonitor.enabled=false` deshabilita el Monitor de estado.

1. Haga clic en Guardar y luego en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

**Agregar opciones de Java a WebSphere**

1. En el árbol de navegación de la consola administrativa de WebSphere, haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones WebSphere.
1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura del servidor, haga clic en Java y flujo de trabajo de formularios > Definición de proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.
