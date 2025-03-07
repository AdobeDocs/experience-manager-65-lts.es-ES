---
title: Ver información del sistema
description: Obtenga información sobre cómo ver gráficos de monitorización de recursos e información sobre el servidor que ejecuta formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6be4ce1d-39fe-4a25-9d4e-f1cbc593d2c7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---

# Ver información del sistema {#view-system-information}

La pestaña Sistema muestra gráficos de monitorización de recursos e información sobre el servidor que ejecuta los formularios AEM Forms. Para acceder a esta información, en la consola de administración, haga clic en Monitor de estado en la esquina superior derecha de la página. Si está ejecutando formularios AEM Forms en un entorno en clúster, la información mostrada es para el nodo seleccionado de la lista Servidor.

Para guardar la información actual del sistema como un archivo de propiedades, haga clic en Guardar.

El panel derecho de la pestaña Sistema muestra representaciones gráficas de la siguiente información:

* Elementos de trabajo y recuento de trabajo
* Uso de pila y pila comprometida
* Uso sin montón y sin montón comprometido

Puede arrastrar el puntero a lo largo de la cronología para obtener los valores de un momento determinado.

>[!NOTE]
>
>Los datos de gráficos, los valores de información del servidor y la hora del reloj se actualizan cada 10 minutos. La información no se muestra en tiempo real.

El panel izquierdo de la ficha Sistema muestra la siguiente información sobre el servidor o nodo:

**Máquina virtual:** Versión de máquina virtual Java (JVM) en el servidor.

**Proveedor de máquina virtual:** fabricante de JVM.

**Versión de máquina virtual:** Número de versión de JVM

**Nombre de equipo:** Nombre de host del servidor donde están instalados los formularios AEM Forms.

**Tiempo de actividad:** El tiempo, en horas y minutos, que el servidor ha estado funcionando.

**Compilador Just-In-Time:** nombre del compilador que se está utilizando.

**Tiempo de compilación:** Cantidad de tiempo empleado en la compilación.

**Número de subprocesos de Live Threads:** Número total de subprocesos presentes actualmente en el sistema de AEM Forms.

**Número máximo de Threads:** El mayor número de subprocesos activos registrados en el sistema.

**Número de clases cargadas:** Número de clases cargadas en la JVM.

**Número de clases descargadas:** Número de clases descargadas de JVM.

**Montón mínimo:** Cantidad mínima de montón que se utilizó.

**Montón máximo:** Cantidad máxima de montón que se ha utilizado.

**Nombre del sistema operativo:** El nombre del sistema operativo que se ejecuta en el servidor de AEM Forms.

**Versión del sistema operativo:** Número de versión del sistema operativo que se ejecuta en AEM Forms Server.

**Arco del sistema operativo:** Arquitectura del sistema operativo en la que se está ejecutando JVM.

**Número de procesadores:** El número de procesadores del sistema.

**Argumentos de máquina virtual:** Argumento utilizado por JVM.

**Ruta de clase:** Ruta de clase utilizada por JVM.

**Ruta de biblioteca:** Ruta de biblioteca utilizada por JVM.

**Ruta de clase de arranque:** Ruta de clase de arranque utilizada por JVM.

**Tipo de servidor de aplicaciones:** Tipo de servidor de aplicaciones utilizado para ejecutar formularios AEM.

**Versión del servidor de aplicaciones:** Número de versión del servidor de aplicaciones utilizado para ejecutar formularios AEM.

**Proveedor del servidor de aplicaciones:** Fabricante del servidor de aplicaciones que se usa para ejecutar formularios AEM.

**Fecha de instalación:** Fecha (en formato aaaa-mm-dd) en la que se instalaron los formularios AEM.

**Versión de formularios de AEM:** Versión de formularios de AEM que está instalada.

**Versión del parche:** número de parche de formularios AEM.

**Nombre de base de datos:** Tipo de base de datos utilizada por los formularios de AEM.

**Versión de base de datos:** Número de versión de la base de datos utilizada por los formularios de AEM.

**Nombre de la unidad de base de datos:** Nombre del controlador utilizado por JVM para conectarse a la base de datos.

**Versión del controlador de base de datos:** Versión del controlador utilizado por JVM para conectarse a la base de datos.

El botón **Guardar** le permite guardar esta información del sistema en un archivo de propiedades.
