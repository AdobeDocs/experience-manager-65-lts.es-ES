---
title: Ajustar el rendimiento del monitor de estado
description: Aprenda a ajustar el rendimiento del Monitor de estado. Controle las estadísticas del sistema que afectan al rendimiento del entorno de formularios utilizando la opción de configuración JAVA.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 3%

---

# Ajustar el rendimiento del monitor de estado{#fine-tuning-health-monitor-performance}

La recopilación de estadísticas del sistema que rellenan el Monitor de estado afecta en cierto modo al rendimiento del entorno de los formularios AEM Forms. Este impacto se puede controlar configurando las opciones de Java que se enumeran a continuación en su servidor de aplicaciones.

<table>
 <thead>
  <tr>
   <th><p>Propiedad</p></th>
   <th><p>Función</p></th>
   <th><p>Valor predeterminado</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>Activar o desactivar el subproceso Monitor de estado</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Activar o desactivar el almacenamiento en caché de Gemfire</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervalo en milisegundos tras el cual el subproceso Monitor de estado recopila las estadísticas</p></td>
   <td><p>10 minutos (600.000 milisegundos)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Puerto de multidifusión utilizado para comunicarse con otros miembros del sistema distribuido. Si se establece en cero, la multidifusión está deshabilitada tanto para la detección como para la distribución de miembros. </p><p>Nota: Seleccione distintas direcciones y puertos de multidifusión para distintos sistemas distribuidos. No utilice solo direcciones diferentes.</p></td>
   <td><p>No hay valor predeterminado. Los valores válidos van del 0 al 65535.</p></td>
  </tr>
  <tr>
   <td><p>statistics-sample-rate</p></td>
   <td><p>Velocidad en milisegundos a la que se muestrean las estadísticas. Las estadísticas del sistema operativo solo se actualizan cuando se toma una muestra.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Esta propiedad habilita o deshabilita la recopilación de estadísticas de Work Manager, como el recuento de trabajos o elementos de trabajo.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## Agregar opciones de Java a JBoss {#add-java-options-to-jboss}

1. Detenga el servidor de aplicaciones JBoss.
1. Abra *[appserver root]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y agregue cualquiera de las opciones de Java según sea necesario.
1. Reinicie el servidor.

## Añadir opciones de Java a WebLogic {#add-java-options-to-weblogic}

1. Inicie la consola de administración de WebLogic escribiendo https://[nombre de host]:&#39;puerto&#39;/consola en la línea URL de un explorador web.
1. Escriba el nombre de usuario y la contraseña que ha creado para el dominio de WebLogic Server y haga clic en Registrar en Centro de cambios y haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en la pestaña Configuración > pestaña Inicio del servidor.
1. En el cuadro Argumentos, agregue los argumentos necesarios al final del contenido actual. Por ejemplo, al agregar - `Dadobe.healthmonitor.enabled=false` se deshabilita el Monitor de estado.
1. Haga clic en Guardar y luego en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

## Agregar opciones de Java a WebSphere {#add-java-options-to-websphere}

1. En el árbol de navegación de la consola administrativa de WebSphere, haga lo siguiente para su servidor de aplicaciones:

   (WebSphere 6.x) Haga clic en Servidores > Servidores de aplicaciones

   (WebSphere 7.x) Haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones WebSphere

1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura del servidor, haga clic en Java y flujo de trabajo de formularios > Definición de proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.
