---
title: Introducción a la creación de informes de procesos
description: Pasos para empezar a utilizar Process Reporting de AEM Forms en JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e64a3b6f-7248-4426-9f13-f703eab3632d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 77%

---

# Introducción a la creación de informes de procesos{#getting-started-with-process-reporting}

Process Reporting permite a los usuarios de AEM Forms consultar información sobre los procesos de AEM Forms definidos actualmente en la implementación de AEM Forms. Sin embargo, Process Reporting no accede directamente a los datos del repositorio de AEM Forms. Los datos se publican primero en el repositorio de Process Reporting de forma programada (*mediante los servicios ProcessDataPublisher y ProcessDataStorage*). A continuación, los informes y las consultas de Process Reporting se generan a partir de los datos de Process Reporting publicados en el repositorio. Process Reporting se instala como parte del módulo de Forms Workflow.

Este artículo detalla los pasos para habilitar la publicación de datos de AEM Forms en el repositorio de Process Reporting. Una vez habilitada, podrá usar Process Reporting para ejecutar informes y consultas. El artículo también describe las opciones disponibles para configurar los servicios de Process Reporting.

## Requisitos previos de Process Reporting {#process-reporting-pre-requisites}

### Depuración de procesos no esenciales {#purge-non-essential-processes}

Si está utilizando Forms Workflow, la base de datos de AEM Forms puede contener una gran cantidad de datos

Los servicios de publicación de Process Reporting publican todos los datos de AEM Forms disponibles actualmente en la base de datos. Esto implica que si la base de datos contiene datos heredados sobre los que no desea ejecutar informes y consultas, todos esos datos también se publicarán en el repositorio aunque no sean necesarios para realizar informes. Se recomienda depurar estos datos antes de ejecutar los servicios para publicar los datos en el repositorio de Process Reporting. Al hacerlo, mejora el rendimiento tanto del servicio de publicación como del servicio que consulta los datos para los informes.

Para obtener más información sobre la depuración de datos de procesos de AEM Forms, consulte [Depuración de datos de procesos](/help/forms/using/admin-help/purging-process-data.md).

>[!NOTE]
>
>Para obtener sugerencias y trucos sobre la utilidad de depuración, consulte el artículo de Adobe Developer Connection sobre la [depuración de procesos y trabajos](/help/forms/using/admin-help/purging-process-data.md).

## Configuración de los servicios de Process Reporting {#configuring-process-reporting-services}

### Programar la publicación de datos de proceso {#schedule-process-data-publishing}

Los servicios de Process Reporting publican los datos de la base de datos de AEM Forms en el repositorio de Process Reporting de forma programada.

Esta operación puede consumir muchos recursos y afectar al rendimiento de los servidores de AEM Forms. Se recomienda programarla fuera de las franjas temporales de mayor actividad del servidor de AEM Forms.

De forma predeterminada, la publicación de datos está programada para ejecutarse todos los días a las 2:00 a. m.

Para cambiar la programación de publicación, realice los siguientes pasos:

>[!NOTE]
>
>Si está ejecutando la implementación de AEM Forms en un clúster, realice los siguientes pasos en cada uno de los nodos del clúster.

1. Detenga la instancia de AEM Forms Server.
1. &#x200B;

   * (En Windows) Abra el archivo `[JBoss root]/bin/run.conf.bat` en un editor.
   * (En Linux®, AIX® y Solaris™) `[JBoss root]/bin/run.conf.sh` archivo en un editor.

1. Agregue el argumento JVM `-Dreporting.publisher.cron = <expression>.`.

   Ejemplo: la siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada cinco horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Guarde y cierre el archivo `run.conf.bat`.

1. Reinicie la instancia de AEM Forms Server.

1. Detenga la instancia de AEM Forms Server.
1. Inicie sesión en la consola administrativa de WebSphere®. En el árbol de navegación, haga clic en **Servidores** > **Servidores de aplicaciones** y, a continuación, haga clic en el nombre del servidor en el panel derecho.

1. En Infraestructura del servidor, haga clic en **Java™ y Process Management** > **Definición del proceso**.

1. En Propiedades adicionales, haga clic en **Java™ Virtual Machine**.

   En el cuadro Argumentos genéricos de JVM, añada el argumento `-Dreporting.publisher.cron = <expression>.`.

   **Ejemplo**: la siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada cinco horas:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Aplicar**, haga clic en Aceptar y, a continuación, haga clic en **Guardar directamente en la configuración maestra**.
1. Reinicie la instancia de AEM Forms Server.
1. Detenga la instancia de AEM Forms Server.
1. Inicie sesión en la consola de administración de WebLogic. La dirección predeterminada de la consola de administración de WebLogic es `https://[hostname]:[port]/console`.
1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura de dominio, haga clic en **Entorno** > **Servidores** y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en la pestaña **Configuración** > y luego en la pestaña **Inicio de servidor**.
1. En el cuadro Argumentos, añada el argumento JVM `-Dreporting.publisher.cron = <expression>`.

   **Ejemplo**: la siguiente expresión cron hace que Process Reporting publique los datos de AEM Forms en el repositorio de Process Reporting cada cinco horas:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Haga clic en **Guardar** y luego en **Activar cambios**.
1. Reinicie la instancia de AEM Forms Server.

![servicio_de_publicación_de_datos_de_proceso](assets/processdatapublisherservice.png)

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

### Servicio ProcessDataStorage {#processdatastorage-service}

El servicio ProcessDataStorageProvider recibe datos de proceso del servicio ProcessDataPublisher y los guarda en el repositorio de Process Reporting.

En cada ciclo de publicación, los datos se guardan en subcarpetas de una carpeta raíz predefinida.

Puede utilizar la consola de administración para configurar la ubicación raíz (**predeterminada**: `/content/reporting/pm`) y el formato (**predeterminado**: `/yyyy/mm/dd/hh/mi/ss`) de la jerarquía de la subcarpeta en la que se guardarán los datos de proceso.

#### Configuración de las ubicaciones del repositorio de Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Inicie sesión en la **consola de administración** con credenciales de administrador. La URL predeterminada de la consola de administración es `https://'[server]:[port]'/adminui`
1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** > **Administración de servicios** y abra el servicio **ProcessDataStorageProvider**.

   ![servicio-almacenamiento-datos-procesos](assets/process-data-storage-service.png)

   **CarpetaRaíz**

   La ubicación CRX en la cual se almacenarán los datos de proceso para la creación de informes.

   `Default`: `/content/reporting/pm`

   **Jerarquía de carpetas**

   La jerarquía de carpetas en la cual se almacenarán los datos de proceso en función del tiempo de creación del proceso.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Haga clic en **Guardar**.

### Servicio ReportConfiguration {#reportconfiguration-service}

Process Reporting utiliza el servicio ReportConfiguration para configurar el servicio de consulta de informes de procesos.

#### Configuración del servicio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Inicie sesión en el **Administrador de configuración** con credenciales de administrador CRX. La URL predeterminada del Administrador de configuración es `https://'[server]:[port]'/lc/system/console/configMgr`.
1. Abra el servicio **ReportingConfiguration**.
1. **Número de registros**

   Al ejecutar una consulta en el repositorio, un resultado puede contener potencialmente muchos registros. Si el conjunto de resultados es elevado, la ejecución de la consulta puede consumir recursos del servidor.

   Para gestionar grandes conjuntos de resultados, el servicio ReportConfiguration divide el procesamiento de consultas en lotes de registros. Al hacerlo, se reduce la carga del sistema.

   `Default`: `1000`

   **Ruta de almacenamiento CRX**

   La ubicación CRX en la cual se almacenarán los datos de proceso para la creación de informes.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Esta ubicación es la misma especificada en la opción de configuración ProcessDataStorage **Carpeta raíz**.
   >
   >
   >Si actualiza la opción Carpeta raíz en la configuración de ProcessDataStorage, debe actualizar la ubicación de la ruta de almacenamiento de CRX en el servicio ReportConfiguration.

1. Haga clic en **Guardar** y cierre el **Administrador de configuración CQ**.

### Servicio ProcessDataPublisher {#processdatapublisher-service}

El servicio ProcessDataPublisher importa los datos de proceso de la base de datos de AEM Forms y los publica en el servicio ProcessDataStorageProvider para su almacenamiento.

#### Configuración del servicio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Inicie sesión en la **consola de administración** con credenciales de administrador.

   La URL predeterminada es `https://'server':port]/adminui/`.

1. Vaya a **Inicio** > **Servicios** > **Aplicaciones y servicios** > **Administración de servicios** y abra el servicio **ProcessDataPublisher**.

![servicio-de-publicación-de-datos-de-proceso-1](assets/processdatapublisherservice-1.png)

**Publicar datos**

Active esta opción para iniciar el proceso de publicación de datos. Esta opción está desactivada de forma predeterminada.

Habilite Process Reporting solo cuando todas las configuraciones relacionadas con sus componentes estén correctamente configuradas.

También puede utilizar esta opción para desactivar la publicación de datos de proceso cuando ya no sea necesaria.

`Default`: `Off`

**Intervalo de lotes (s)**

Cada vez que se ejecuta el servicio ProcessDataPublisher, este divide primero el tiempo desde la última ejecución del servicio entre el intervalo de lotes. A continuación, el servicio procesa cada intervalo de datos de AEM Forms de forma independiente para ayudar a controlar el tamaño de los datos que el publicador procesa de extremo a extremo durante cada ejecución (lote) dentro de un ciclo.

Por ejemplo, si el publicador se ejecuta todos los días, en lugar de procesar todos los datos durante el día en una sola ejecución, divide de forma predeterminada el procesamiento en 24 lotes de una hora cada uno.

`Default`: `3600`

`Unit`: `Seconds`

**Tiempo de espera de bloqueo (s)**

El servicio de publicación adquiere un bloqueo cuando comienza a procesar datos para que varias instancias del publicador no empiecen a ejecutar y procesar datos simultáneamente.

Si un servicio de publicación que ha adquirido un bloqueo está inactivo durante el número de segundos definido por el valor Tiempo de espera de bloqueo, el bloqueo se libera para que otras instancias del servicio de publicación puedan continuar procesándose.

`Default`: `3600`

`Unit`: `Seconds`

**Publicar datos de**

El entorno de AEM Forms contiene datos desde el momento en el que se configura el entorno.

De forma predeterminada, el servicio ProcessDataPublisher importa todos los datos de la base de datos de AEM Forms.

Según sus necesidades de creación de informes, si planea ejecutar informes y consultas sobre datos después de una fecha y una hora determinadas, se recomienda especificar la fecha y la hora. A continuación, el servicio de publicación publica la fecha a partir de ese momento.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Acceso a la interfaz de usuario de Process Reporting {#accessing-the-process-reporting-user-interface}

La interfaz de usuario de Process Reporting se basa en explorador.

Después de configurar Process Reporting, puede empezar a trabajar con él en la siguiente ubicación de la instalación de AEM Forms:

`https://<server>:<port>/lc/pr`

### Inicio de sesión en Process Reporting {#log-in-to-process-reporting}

Cuando vaya a la URL de Process Reporting (https://&lt;server>:&lt;port>/lc/pr), se muestra la pantalla de inicio de sesión.

Para iniciar sesión en el módulo Process Reporting, especifique sus credenciales.

>[!NOTE]
>
>Para iniciar sesión en la interfaz de usuario de Process Reporting, necesita el siguiente permiso de AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Inicio de sesión en Process Reporting](assets/capture1_new.png)

Cuando inicia sesión en Process Reporting, se muestra la página **[!UICONTROL Inicio]**.

### Pantalla Inicio de Process Reporting {#process-reporting-home-screen}

![pantalla-inicio-de-process-reporting](assets/process-reporting-home-screen.png)

**Vista de árbol de Process Reporting:** la vista de árbol que aparece a la izquierda de la pantalla Inicio contiene los elementos de los módulos de Process Reporting.

La vista de árbol consta de los siguientes elementos de alto nivel:

**Informes:** este elemento contiene los informes predeterminados que se envían con Process Reporting.

Para obtener más información sobre los informes predefinidos, consulte [Informes predefinidos en informes de proceso](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Consultas ad hoc:** este elemento contiene opciones para realizar búsquedas basadas en filtros en procesos y tareas.

Para obtener más información sobre las consultas ad hoc, consulte [Informes de consultas ad hoc en proceso](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizado:** el nodo Personalizado muestra los informes personalizados que ha creado.

Para ver el procedimiento para crear y mostrar informes personalizados, consulte [Informes personalizados en proceso de informes](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra de título de Process Reporting:** la barra de título de Process Reporting contiene una serie de opciones genéricas que puede utilizar al trabajar en la interfaz de usuario.

**Título de Process Reporting:** el título de Process Reporting se muestra en la esquina izquierda de la barra de título.

Puede hacer clic en el título en cualquier momento para volver a la pantalla Inicio.

**Hora de la última actualización:** los datos de proceso se publican desde la base de datos de AEM Forms en el repositorio de Process Reporting de forma programada.

La hora de la última actualización muestra la última fecha y hora a la que se insertaron las actualizaciones de datos en el repositorio de Process Reporting.

Para obtener más información sobre el servicio de publicación de datos y cómo programarlo, consulte [Programar la publicación de datos de proceso](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) en el artículo Introducción a Process Reporting.

**Usuario de Process Reporting:** el nombre del usuario que ha iniciado sesión se muestra a la derecha de Última actualización.

**Lista desplegable de la barra de título de Process Reporting:** la lista desplegable situada en la esquina derecha de la barra de título de Process Reporting contiene las siguientes opciones:

* **[!UICONTROL Sincronizar]**: sincronice el repositorio de Process Reporting incrustado con la base de datos de AEM Forms.
* **[!UICONTROL Ayuda]**: vea la documentación de la Ayuda de Process Reporting.
* **[!UICONTROL Cerrar sesión]**: cierre sesión en Process Reporting.
