---
title: Informes
description: Aprenda a trabajar con los informes en Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2782'
ht-degree: 3%

---

# Informes {#reporting}

Para ayudarle a monitorizar y analizar el estado de su instancia, Adobe Experience Manager (AEM) proporciona una selección de informes predeterminados, que se pueden configurar para sus necesidades individuales:

* [Informe sobre componentes](#component-report)
* [Uso del disco](#disk-usage)
* [Comprobación de estado](#health-check)
* [Informe de actividad de la página](#page-activity-report)
* [Informe de contenido generado por el usuario](#user-generated-content-report)
* [Informe del usuario](#user-report)
* [Informe de instancia de flujo de trabajo](#workflow-instance-report)
* [Informe de flujo de trabajo](#workflow-report)

>[!NOTE]
>
>Estos informes solo están disponibles en la IU clásica. Para supervisar el sistema y crear informes en la IU moderna, consulte [Tablero de operaciones](/help/sites-administering/operations-dashboard.md).

Se puede acceder a todos los informes desde la consola **Herramientas**. Seleccione **Informes** en el panel izquierdo y, a continuación, haga doble clic en el informe requerido en el panel derecho para poder abrirlo y verlo, configurarlo o ambos.

También se pueden crear nuevas instancias de un informe desde la consola **Herramientas**. Seleccione **Informes** en el panel izquierdo y, a continuación, **Nuevo...** en la barra de herramientas. Defina un **Título** y un **Nombre**, seleccione el tipo de informe que necesite y haga clic en **Crear**. La nueva instancia de informe aparecerá en la lista. Haga doble clic para abrir y, a continuación, arrastre un componente desde la barra de tareas para crear la primera columna e iniciar la definición del informe.

>[!NOTE]
>
>Además de los informes estándar de AEM disponibles de forma predeterminada, puede [desarrollar sus propios informes (nuevos)](/help/sites-developing/dev-reports.md).

## Aspectos básicos de la personalización de informes {#the-basics-of-report-customization}

Hay varios formatos de informes disponibles. Los siguientes informes utilizan columnas que se pueden personalizar según se detalla en las secciones siguientes:

* [Informe sobre componentes](#component-report)
* [Informe de actividad de la página](#page-activity-report)
* [Informe de contenido generado por el usuario](#user-generated-content-report)
* [Informe del usuario](#user-report)
* [Informe de instancia de flujo de trabajo](#workflow-instance-report)

>[!NOTE]
>
>Cada uno de los siguientes informes tiene su propio formato y personalización:
>
>
>* [Comprobación de estado](#health-check) usa campos de selección para especificar los datos sobre los que desea informar.
>* [Uso del disco](#disk-usage) usa vínculos para explorar en profundidad la estructura del repositorio.
>* [Flujo de trabajo](/help/sites-administering/reporting.md#workflow-report) le ofrece una descripción general de los flujos de trabajo que se ejecutan en su instancia.
>
>Por lo tanto, los siguientes procedimientos para la configuración de columnas no son adecuados. Consulte las descripciones de los informes individuales para obtener más información.

### Selección y colocación de columnas de datos {#selecting-and-positioning-the-data-columns}

Las columnas se pueden agregar, cambiar de posición o quitar de cualquiera de los informes, ya sean estándar o personalizados.

La pestaña **Componentes** de la barra de tareas (disponible en la página del informe) enumera todas las categorías de datos que se pueden seleccionar como columnas.

Para cambiar la selección de datos:

* para agregar una columna, arrastre el componente requerido desde la barra de tareas y suéltelo en la posición que desee

   * una marca de verificación verde indica cuándo es válida la posición y un par de flechas indica exactamente dónde se coloca
   * un símbolo rojo que indica que la posición no es válida

* para mover una columna, haga clic en el encabezado, mantenga pulsada la tecla y arrastre a la nueva posición
* para quitar una columna, haga clic en el título de la columna, mantenga presionada la tecla y arrastre hacia arriba hasta el área del encabezado del informe (un símbolo menos rojo indica que la posición no es válida). Suelte el botón del ratón y el cuadro de diálogo Eliminar componentes solicitará confirmación de que realmente desea eliminar la columna.

### Menú desplegable de columna {#column-drop-down-menu}

Cada columna del informe tiene un menú desplegable. Esto se vuelve visible cuando el cursor del ratón se mueve sobre la celda de título de la columna.

Aparece un cursor de flecha en el extremo derecho de la celda de título (no debe confundirse con el cursor de flecha situado inmediatamente a la derecha del texto de título que indica el [mecanismo de ordenación actual](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

Las opciones disponibles en el menú dependen de la configuración de la columna (como se realiza durante el desarrollo del proyecto), las opciones no válidas aparecen atenuadas (atenuadas).

### Clasificación de los datos {#sorting-the-data}

Los datos se pueden ordenar según una columna específica mediante lo siguiente:

* al hacer clic en el encabezado de columna correspondiente; la ordenación cambia entre ascendente y descendente, y se indica con un encabezado de flecha justo al lado del texto del título
* use el menú desplegable de la columna [columna](#column-drop-down-menu) para seleccionar específicamente **Orden ascendente** o **Orden descendente**; de nuevo, esto se indica con una flecha al lado del texto del título

### Grupos y el gráfico de datos actuales {#groups-and-the-current-data-chart}

En las columnas adecuadas, puede seleccionar **Agrupar por esta columna** del [menú desplegable de la columna](#column-drop-down-menu). Esto agrupa los datos según cada valor distinto dentro de esa columna. Puede seleccionar más de una columna para agruparla. La opción aparece atenuada (atenuada) cuando los datos de la columna no son adecuados. Es decir, cada entrada es distinta y única para que no se puedan formar grupos. Por ejemplo, la columna ID de usuario del informe de usuarios.

Después de agrupar al menos una columna, se genera un gráfico circular de **datos actuales**, basado en esta agrupación. Si se agrupan varias columnas, esto se indica en el gráfico.

![informuser](assets/reportuser.png)

Al mover el cursor sobre el gráfico circular, se muestra el valor agregado para el segmento correspondiente. Utiliza el acumulado definido actualmente para la columna; por ejemplo, recuento, mínimo, promedio, entre otros.

### Filtros y agregados {#filters-and-aggregates}

En las columnas adecuadas, también puede configurar **Configuración de filtro** y/o **Agregados** desde el [menú desplegable de la columna](#column-drop-down-menu).

#### Filtros {#filters}

La configuración de filtro permite especificar los criterios para mostrar las entradas. Los operadores disponibles son:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Para establecer un filtro:

1. Seleccione el operador que desee en la lista desplegable.
1. Introduzca el texto sobre el que desea filtrar.
1. Haga clic en **Aplicar**.

Para desactivar el filtro:

1. Elimine el texto del filtro.
1. Haga clic en **Aplicar**.

#### Agregados {#aggregates}

También puede seleccionar un método de agregación (que puede variar según la columna seleccionada):

![reportaggregate](assets/reportaggregate.png)

### Propiedades de columna {#column-properties}

Esta opción solo está disponible cuando la [columna genérica](#generic-column) se ha usado en el [informe de usuarios](#user-report).

### Datos históricos {#historic-data}

En **Datos históricos** se muestra un gráfico del cambio en los datos a lo largo del tiempo. Se deriva de instantáneas tomadas a intervalos regulares.

Los datos son:

* Recopilado por, si está disponible, la primera columna ordenada; de lo contrario, la primera columna (no agrupada)
* Agrupado por la columna adecuada

El informe se puede generar:

1. Establezca **Grouping** en la columna requerida.
1. **Editar** la configuración para que pueda definir instantáneas por hora o por día.
1. **Finalizar...** la definición para iniciar la recopilación de instantáneas.

   El botón deslizador rojo/verde de la parte superior izquierda indica cuándo se recopilan las instantáneas.

El gráfico resultante se muestra en la parte inferior derecha:

![tendencias de informes](assets/reporttrends.png)

Cuando se inicie la recopilación de datos, puede seleccionar lo siguiente:

* **Período**

  Puede seleccionar las fechas inicial y final para mostrar los datos del informe.

* **Intervalo**

  Se puede seleccionar mes, semana, día y hora para la escala y la agregación del informe.

  Por ejemplo, si hay instantáneas diarias disponibles para febrero de 2011:

   * Si el intervalo se establece en `Day`, cada instantánea se muestra como un valor único en el gráfico.
   * Si el intervalo se establece en `Month`, todas las instantáneas de febrero se agregan en un solo valor (mostrado como un solo &quot;punto&quot; en el gráfico).

Seleccione sus requisitos y haga clic en **Ir** para aplicarlos al informe. Para actualizar la pantalla después de realizar más instantáneas, haz clic de nuevo en **Ir**.

![chlimage_1-43](assets/chlimage_1-43.png)

Cuando se recopilan instantáneas, puede:

* Use **Finalizar...** de nuevo para reiniciar la colección.

  **Finalizar** &quot;bloquea&quot; la estructura del informe (es decir, las columnas asignadas al informe y que se agrupan, ordenan, filtran, etc.) y comienza a tomar instantáneas.

* Abra el cuadro de diálogo **Editar** para que pueda seleccionar **No hay instantáneas** para finalizar la colección hasta que sea necesario.

  **Editar** solo activa o desactiva la toma de instantáneas. Si se vuelve a activar la toma de instantáneas, se utiliza el estado del informe cuando se terminó por última vez para tomar más instantáneas.

>[!NOTE]
>
>Las instantáneas se almacenan en `/var/reports/...`, donde el resto de la ruta de acceso refleja la ruta de acceso del informe respectivo y el identificador creado al finalizar el informe.
>
>
>Las instantáneas antiguas se pueden depurar manualmente si está seguro de que ya no necesita esas instancias.

>[!NOTE]
>
>Los informes preconfigurados no exigen mucho rendimiento, pero se recomienda utilizar instantáneas diarias en un entorno de producción. Si es posible, ejecute estas instantáneas diarias a una hora del día en la que no haya mucha actividad en el sitio web. Esto se puede definir con el parámetro `Daily snapshots (repconf.hourofday)` para la **configuración de informes de CQ de día**. Consulte [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) para obtener más información sobre cómo configurarla.

#### Límites de visualización {#display-limits}

El informe de datos históricos también puede cambiar ligeramente de aspecto debido a los límites que se pueden establecer, según el número de resultados del periodo seleccionado.

Cada línea horizontal se conoce como serie (y corresponde a una entrada de la leyenda del gráfico), cada columna vertical de puntos representa las instantáneas agregadas.

![chlimage_1-44](assets/chlimage_1-44.png)

Para mantener el gráfico limpio durante períodos de tiempo más largos, hay límites que se pueden establecer. Para los informes estándar, estos son:

* serie horizontal: tanto el valor predeterminado como el máximo del sistema son `9`

* instantáneas agregadas verticales: el valor predeterminado es `35` (por serie horizontal)

Por lo tanto, cuando se exceden los límites (adecuados):

* los puntos no se muestran
* la leyenda del gráfico de datos históricos puede mostrar un número de entradas diferente al del gráfico de datos actual

![chlimage_1-45](assets/chlimage_1-45.png)

Los informes personalizados también pueden mostrar el valor **Total** de todas las series. Esto se muestra como una serie (línea horizontal y entrada en la leyenda).

>[!NOTE]
>
>Para los informes personalizados, los límites se pueden establecer de forma diferente.

### Editar (informe) {#edit-report}

El botón **Editar** abre el diálogo **Editar informe**.

Esta es una ubicación en la que se define el período para recopilar instantáneas de [datos históricos](#historic-data), pero también se pueden definir otras opciones de configuración:

![reportedit](assets/reportedit.png)

* **Título**

  Puede definir su propio título.

* **Descripción**

  Puede definir su propia descripción.

* **Ruta raíz** (*solo activa para ciertos informes*)

  Use esto para limitar el informe a una (sub) sección del repositorio.

* **Procesamiento de informes**

   * **actualizar datos automáticamente**

     Los datos del informe se actualizan cada vez que se actualiza la definición del informe.

   * **actualizar datos manualmente**

     Esta opción se puede utilizar para evitar los retrasos causados por las operaciones de actualización automática cuando hay un gran volumen de datos.

     Si selecciona esta opción, los datos del informe deben actualizarse manualmente cuando haya habido cambios en algún aspecto de la configuración del informe. También significa que, cuando cambia cualquier aspecto de la configuración, la tabla del informe aparece en blanco.

     Cuando se selecciona esta opción, se muestra el botón **[Cargar datos](#load-data)** (junto a **Editar** en el informe). **Cargar datos** carga los datos y actualiza los datos del informe que se muestran.

* **Instantáneas**
Puede definir la frecuencia con la que se crean las instantáneas, diariamente, por hora o en absoluto.

### Cargar datos {#load-data}

El botón **Cargar datos** solo está visible cuando se han seleccionado **datos actualizados manualmente** en **[Editar](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

Al hacer clic en **Cargar datos**, se vuelven a cargar los datos y se actualiza el informe que se muestra.

Si selecciona esta opción para actualizar los datos manualmente:

1. Al cambiar la configuración del informe, los datos de la tabla del informe aparecen en blanco.

   Por ejemplo, si cambia el mecanismo de ordenación de una columna, no se muestran los datos.

1. Si desea que los datos del informe se vuelvan a mostrar, debe hacer clic en **Cargar datos** para volver a cargar los datos.

### Finalizar (informe) {#finish-report}

Cuando **termine** el informe:

* La definición de informe *a partir de ese momento* se usa para tomar las instantáneas. Después, puede seguir trabajando en una definición de informe porque es independiente de las instantáneas.
* Se eliminarán todas las instantáneas existentes.
* Se recopilan nuevas instantáneas para los [datos históricos](#historic-data).

Con este cuadro de diálogo, puede definir o actualizar su propio título y descripción para el informe resultante.

![informe finalizado](assets/reportfinish.png)

## Tipos de informes {#report-types}

### Informe sobre componentes {#component-report}

El informe de componentes proporciona información sobre cómo utiliza el sitio web los componentes.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Autor
* Ruta del componente
* Tipo de componente
* Última modificación
* Página

Significa que puede ver lo siguiente:

* Qué componentes se utilizan y dónde.

  Útil, por ejemplo, al realizar pruebas.

* Cómo se distribuyen las instancias de un componente específico.

  Esto puede resultar interesante si páginas específicas (es decir, &quot;páginas pesadas&quot;) están experimentando problemas de rendimiento.

* Identificar las partes del sitio con cambios frecuentes o menos frecuentes.
* Consulte cómo se desarrolla el contenido de la página con el paso del tiempo.

Todos los componentes están incluidos, según el estándar del producto y son específicos del proyecto. Con el cuadro de diálogo **Editar**, el usuario también puede establecer una **ruta raíz** que define el punto de inicio del informe; todos los componentes bajo esa raíz se tienen en cuenta para el informe.

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### Uso del disco {#disk-usage}

El informe de uso del disco muestra información sobre los datos almacenados en el repositorio.

El informe se inicia en la raíz ( / ) del repositorio; al hacer clic en una rama concreta, podrá explorar en profundidad el repositorio (la ruta actual se refleja en el título del informe).

![reportdiskusage](assets/reportdiskusage.png)

### Comprobación de estado {#health-check}

Este informe analiza el registro de solicitudes actual:

`<cq-installation-dir>/crx-quickstart/logs/request.log`

Para ayudarle a identificar las solicitudes más costosas dentro de un periodo determinado.

Para generar el informe, puede especificar lo siguiente:

* **Período (horas)**

  El número de horas (pasadas) que se van a analizar.

  Predeterminado: `24`

* **máx. Resultados**

  Número máximo de líneas de salida.

  Predeterminado: `50`

* **máx. Solicitudes**

  Número máximo de solicitudes que analizar.

  Predeterminado: `-1` (todos)

* **Dirección de correo electrónico**

  Envíe los resultados a una dirección de correo electrónico.

  Opcional; predeterminada: en blanco

* **Ejecutar a diario a las (hh:mm)**

  Especifique la hora a la que el informe se ejecutará automáticamente a diario.

  Opcional; predeterminada: en blanco

![reporthealth](assets/reporthealth.png)

### Informe de actividad de la página {#page-activity-report}

El informe de actividad de página enumera las páginas y las acciones realizadas en ellas.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Página
* Hora
* Tipo
* Usuario

Esto significa que puede monitorizar:

* Las últimas modificaciones.
* Autores que trabajan en páginas específicas.
* Páginas que no se han modificado recientemente, por lo que podría ser necesario realizar alguna acción.
* Páginas que se cambian con mayor o menor frecuencia.
* Usuarios más/menos activos.

El informe de actividad de página toma toda su información del registro de auditoría. De manera predeterminada, la ruta de acceso raíz está configurada en el registro de auditoría en `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### Informe de contenido generado por el usuario {#user-generated-content-report}

Este informe proporciona información sobre el contenido generado por el usuario, ya sean comentarios, clasificaciones o foros.

[Columnas de información](#selecting-and-positioning-the-data-columns) en:

* Fecha
* Dirección IP
* Página
* Remitente del reenvío
* Tipo
* Identificador de usuario

Le permite:

* Ver qué páginas reciben la mayor cantidad de comentarios.
* Obtenga una descripción general de todos los comentarios que los visitantes específicos del sitio están dejando, tal vez los problemas estén relacionados.
* Juzgue si el nuevo contenido provoca comentarios controlando cuándo se realizan comentarios en una página.

![reportusercontent](assets/reportusercontent.png)

### Informe del usuario {#user-report}

Este informe proporciona información sobre todos los usuarios que han registrado una cuenta o un perfil; esto puede incluir autores dentro de la organización y visitantes externos.

[Columnas de información](#selecting-and-positioning-the-data-columns) (donde esté disponible) acerca de:

* Edad
* País
* Dominio
* Correo electrónico
* Apellido
* Sexo
* [Genérica](#generic-column)
* Nombre dado
* Información
* Interés
* Idioma
* Código Hash NTLM
* ID de usuario

Le permite:

* Vea la propagación demográfica de los usuarios.
* Informar sobre los campos personalizados que haya añadido a los perfiles.

![reportusercanned](assets/reportusercanned.png)

#### Columna genérica {#generic-column}

La columna **Genérico** está disponible en el informe del usuario para que pueda obtener acceso a información personalizada, normalmente desde los [perfiles de usuario](/help/sites-administering/identity-management.md#profiles-and-user-accounts); por ejemplo, [Color favorito, como se detalla en Agregar campos a la definición del perfil](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

El cuadro de diálogo Columna genérica (Generic column) se abrirá cuando realice una de las acciones siguientes:

* Arrastre el componente Genérico de la barra de tareas al informe.
* Seleccione Propiedades de columna para una columna genérica existente.

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

En la ficha **Definiciones** puede definir lo siguiente:

* **Título**

  Su propio título para la columna genérica.

* **Propiedad**

  El nombre de la propiedad tal como se almacena en el repositorio, generalmente dentro del perfil del usuario.

* **Ruta**

  Normalmente, la propiedad se toma del `profile`.

* **Tipo**

  Seleccione el tipo de campo de `String`, `Number`, `Integer`, `Date`.

* **Agregado predeterminado**

  Define el agregado utilizado de forma predeterminada si la columna se desagrupa en un informe con al menos una columna agrupada. Seleccione el agregado requerido de `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

  Por ejemplo, *Count* para un campo `String` significa que se muestra el número de valores distintos de `String` para la columna en el estado agregado.

En la ficha **Extended**, también puede definir los agregados y filtros disponibles:

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### Informe de instancia de flujo de trabajo {#workflow-instance-report}

Esto le ofrece una descripción concisa, que proporciona información sobre las instancias individuales de flujos de trabajo, tanto en ejecución como completados.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Completado
* Duración
* Iniciador
* Modelo
* Carga útil
* Iniciado
* Estado

Significa que puede:

* Monitorice la duración media de los flujos de trabajo; si esto sucede con regularidad, puede resaltar problemas con el flujo de trabajo.

![reportworkflowintance](assets/reportworkflowintance.png)

### Informe de flujo de trabajo {#workflow-report}

Esto proporciona estadísticas clave sobre los flujos de trabajo que se ejecutan en la instancia.

![flujo de trabajo del informe](assets/reportworkflow.png)

## Uso de informes en un entorno de publicación {#using-reports-in-a-publish-environment}

Una vez configurados los informes según sus necesidades específicas, puede activarlos para transferir la configuración al entorno de publicación.

>[!CAUTION]
>
>Si desea **datos históricos** para el entorno de publicación, **finalice** el informe en el entorno de creación antes de activar la página.

A continuación, se puede acceder al informe correspondiente en

`/etc/reports`

Por ejemplo, el informe Contenido generado por el usuario se encuentra en:

`http://localhost:4503/etc/reports/ugcreport.html`

Ahora informa de los datos recopilados del entorno de publicación.

Como no se permite ninguna configuración de informe en el entorno de publicación, los botones **Editar** y **Finalizar** no están disponibles. Sin embargo, puede seleccionar los informes **Periodo** e **Intervalo** para los **datos históricos** si se están recopilando instantáneas.

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>El acceso a estos informes puede ser un problema de seguridad; por lo tanto, Adobe recomienda configurar Dispatcher para que `/etc/reports` no esté disponible para los visitantes externos. Consulte la [Lista de comprobación de seguridad](security-checklist.md) para obtener más información.

## Permisos necesarios para ejecutar informes {#permissions-needed-for-running-reports}

Los permisos necesarios dependen de la acción:

* Los datos del informe se recopilan con los privilegios del usuario actual.
* Los datos históricos se recopilan con los privilegios del usuario que finalizó el informe.

En una instalación estándar de AEM, los siguientes permisos están preestablecidos para los informes:

* **Informe de usuario**

  `user administrators` - lectura y escritura

* **Informe de actividad de página**

  `contributors` - lectura y escritura

* **Informe de componente**

  `contributors` - lectura y escritura

* **Informe de contenido generado por el usuario**

  `contributors` - lectura y escritura

* **Informe de instancia de flujo de trabajo**

  `workflow-users` - lectura y escritura

Todos los miembros del grupo `administrators` tienen los derechos necesarios para crear informes.
