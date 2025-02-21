---
title: Copia de seguridad y restauración
description: Obtenga información sobre cómo realizar copias de seguridad y restaurar el contenido y las configuraciones de AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 0%

---

# Copia de seguridad y restauración{#backup-and-restore}

Existen dos formas de realizar copias de seguridad y restaurar el contenido del repositorio en AEM:

* Puede crear una copia de seguridad externa del repositorio y almacenarla en una ubicación segura. Si el repositorio se desglosa, puede restaurarlo al estado anterior.
* Puede crear versiones internas del contenido del repositorio. Estas versiones se almacenan en el repositorio junto con el contenido, para que pueda restaurar rápidamente los nodos y árboles que haya cambiado o eliminado.

## General {#general}

El enfoque descrito aquí se aplica al backup y la recuperación del sistema.

Si necesita realizar una copia de seguridad o recuperar una pequeña cantidad de contenido, que se pierde, no es necesario recuperar el sistema:

* Puede recuperar los datos de otro sistema mediante un paquete
* Para restaurar la copia de seguridad en un sistema temporal, cree un paquete de contenido e impleméntelo en el sistema donde falte este contenido.

Para obtener más información, consulte [Copia de seguridad de paquetes](/help/sites-administering/backup-and-restore.md#package-backup) a continuación.

## Programación {#timing}

No ejecute la copia de seguridad en paralelo con la recolección de elementos no utilizados del almacén de datos, ya que podría dañar los resultados de ambos procesos.

## Copia de seguridad sin conexión {#offline-backup}

Siempre puede realizar una copia de seguridad sin conexión. Esto requiere un tiempo de inactividad de AEM, pero puede ser bastante eficiente en términos de tiempo requerido en comparación con un backup en línea.

En la mayoría de los casos, se utiliza una instantánea del sistema de archivos para crear una copia de solo lectura del almacenamiento en ese momento. Para crear una copia de seguridad sin conexión, realice estos pasos:

* detener la aplicación
* realizar una copia de seguridad de instantánea
* iniciar la aplicación

Dado que la copia de seguridad de la instantánea solo tarda unos segundos, el tiempo de inactividad completo es inferior a unos minutos.

## Online Backup {#online-backup}

Este método de copia de seguridad crea una copia de seguridad de todo el repositorio, incluidas las aplicaciones implementadas bajo él, como AEM. La copia de seguridad incluye contenido, historial de versiones, configuración, software, revisiones, aplicaciones personalizadas, archivos de registro, índices de búsqueda, etc. Si usa clústeres y la carpeta compartida es un subdirectorio de `crx-quickstart` (ya sea físicamente o mediante un vínculo flexible), también se realizará una copia de seguridad del directorio compartido.

Puede restaurar todo el repositorio (y cualquier aplicación) más adelante.

Este método funciona como una copia de seguridad &quot;activa&quot; o &quot;en línea&quot;, de modo que se puede realizar mientras se ejecuta el repositorio. Por lo tanto, el repositorio se puede utilizar mientras se ejecuta la copia de seguridad. Este método funciona para las instancias de repositorio predeterminadas basadas en el almacenamiento Tar.

Al crear una copia de seguridad, tiene las siguientes opciones:

* Copia de seguridad en un directorio mediante la herramienta de copia de seguridad integrada de AEM.
* Copia de seguridad en un directorio mediante una instantánea del sistema de archivos

En cualquier caso, la copia de seguridad crea una imagen (o instantánea) del repositorio. A continuación, el agente de backup de sistemas debe encargarse de transferir esta imagen a un sistema de backup dedicado (unidad de cinta).

>[!NOTE]
>
>Si se utiliza la función Copia de seguridad en línea de AEM en una instancia de AEM que tiene una configuración de almacén de blobs personalizada, se recomienda configurar la ruta del almacén de datos para que esté fuera del directorio `crx-quickstart` y hacer una copia de seguridad del almacén de datos por separado.

>[!CAUTION]
>
>La copia de seguridad en línea sólo realiza una copia de seguridad del sistema de archivos. Si almacena el contenido del repositorio o los archivos del repositorio en una base de datos, es necesario realizar una copia de seguridad de esa base de datos por separado. Si usa AEM con MongoDB, consulte la documentación sobre cómo usar las [herramientas de copia de seguridad nativas de MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### Backup en línea de AEM {#aem-online-backup}

Una copia de seguridad en línea del repositorio le permite crear, descargar y eliminar archivos de copia de seguridad. Es una función de copia de seguridad &quot;activa&quot; o &quot;en línea&quot;, por lo que se puede ejecutar mientras el repositorio se utiliza normalmente en modo de lectura-escritura.

>[!CAUTION]
>
>No ejecute Copias de seguridad de AEM Online simultáneamente con [Recopilación de elementos no utilizados del almacén de datos](/help/sites-administering/data-store-garbage-collection.md) o [Limpieza de revisiones](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Afectará negativamente al rendimiento del sistema.

Al iniciar una copia de seguridad, puede especificar una **ruta de destino** o un **retraso**.

**Ruta de acceso de destino** Los archivos de copia de seguridad generalmente se guardan en la carpeta principal de la carpeta que contiene el archivo jar de inicio rápido (.jar). Por ejemplo, si tiene el archivo jar de AEM ubicado en /InstallationKits/AEM, la copia de seguridad se generará en /InstallationKits. También puede especificar un destino a una ubicación de su elección.

Si **TargetPath** es un directorio, la imagen del repositorio se creará en este directorio. Si el mismo directorio se utiliza varias veces (o siempre) para almacenar la copia de seguridad,

* Los archivos modificados en el repositorio se modifican en consecuencia en TargetPath
* Los archivos eliminados en el repositorio se eliminan en TargetPath
* Los archivos creados en el repositorio se crean en TargetPath

>[!NOTE]
>
>Si **TargetPath** se establece en el nombre de archivo con la extensión **.zip**, se realiza una copia de seguridad del repositorio en un directorio temporal y, a continuación, el contenido de este directorio temporal se comprime y se almacena en el archivo ZIP.
>
>Este enfoque se desaconseja porque
>
>* requiere almacenamiento en disco adicional durante el proceso de copia de seguridad (directorio temporal más el archivo zip)
>* el proceso de compresión lo realiza el repositorio y puede influir en su rendimiento.
>* Retrasa el proceso de backup.
>* Hasta Java 1.6 Java solo puede crear archivos ZIP de hasta 4 gigabytes.
>
>Si necesita crear un ZIP como formato de copia de seguridad, debe hacer una copia de seguridad en un directorio y, a continuación, utilizar un programa de compresión para crear el archivo zip.

**Retraso** indica un retraso de tiempo (en milisegundos) para que el rendimiento del repositorio no se vea afectado. De forma predeterminada, la copia de seguridad del repositorio se ejecuta a toda velocidad. Puede ralentizar la creación de una copia de seguridad en línea para que no ralentice otras tareas.

Cuando utilice un retraso muy grande, asegúrese de que el backup en línea no tarde más de 24 horas. Si es así, descarte esta copia de seguridad, ya que es posible que no contenga todos los binarios.
Un retraso de 1 milisegundo suele resultar en un 10 % de uso de CPU, y un retraso de 10 milisegundos suele resultar en menos del 3 % de uso de CPU. El retraso total en segundos se puede calcular de la siguiente manera: Tamaño del repositorio en MB, multiplicado por el retraso en milisegundos, dividido por 2 (si se utiliza la opción zip) o dividido por 4 (cuando se realiza la copia de seguridad en un directorio). Esto significa que una copia de seguridad en un directorio de un repositorio de 200 MB con un retraso de 1 ms aumenta el tiempo de copia de seguridad en unos 50 segundos.

>[!NOTE]
>
>Consulte [Funcionamiento de la copia de seguridad en línea de AEM](#how-aem-online-backup-works) para obtener detalles internos del proceso.

Para crear una copia de seguridad:

1. Inicie sesión en AEM como administrador.

1. Vaya a **Herramientas - Operaciones - Copia de seguridad.**
1. Haga clic en **Crear**. Se abrirá la consola de copia de seguridad.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. En la consola de copia de seguridad, especifique la **[Ruta de destino](#aem-online-backup)** y **[Demora](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >La consola de copia de seguridad también está disponible mediante:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Haga clic en **Guardar**, una barra de progreso indicará el progreso de la copia de seguridad.

   >[!NOTE]
   >
   >Puedes **Cancelar** una copia de seguridad en ejecución en cualquier momento.

1. Cuando se completa la copia de seguridad, los archivos zip se muestran en la ventana de copia de seguridad.

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >Los archivos de copia de seguridad que ya no son necesarios se pueden eliminar mediante la consola. Seleccione el archivo de copia de seguridad en el panel izquierdo y haga clic en **Eliminar**.

   >[!NOTE]
   >
   >Si ha realizado una copia de seguridad en un directorio: una vez finalizado el proceso de copia de seguridad, AEM no escribirá en el directorio de destino.

### Automatización de AEM Online Backup {#automating-aem-online-backup}

Si es posible, la copia de seguridad en línea debe ejecutarse cuando haya poca carga en el sistema, por ejemplo, por la mañana.

Las copias de seguridad se pueden automatizar mediante los clientes HTTP `wget` o `curl`. A continuación se muestran ejemplos de cómo automatizar la copia de seguridad mediante curl.

#### Copia de seguridad en el directorio de destino predeterminado {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>En el siguiente ejemplo, es posible que se deban configurar varios parámetros en el comando `curl` para la instancia; por ejemplo, el nombre de host ( `localhost`), el puerto ( `4502`), la contraseña de administrador ( `xyz`) y el nombre de archivo ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

El archivo o directorio de copia de seguridad se crea en el servidor de la carpeta principal de la carpeta que contiene la carpeta `crx-quickstart` (igual que si estuviera creando la copia de seguridad con el explorador). Por ejemplo, si ha instalado AEM en el directorio `/InstallationKits/crx-quickstart/`, la copia de seguridad se creará en el directorio `/InstallationKits`.

El comando curl vuelve inmediatamente, por lo que debe supervisar este directorio para ver cuándo el archivo zip está listo. Mientras se crea la copia de seguridad, se puede ver un directorio temporal (con el nombre basado en el del archivo zip final), al final se comprimirá. Por ejemplo:

* nombre del archivo zip resultante: `backup.zip`
* nombre del directorio temporal: `backup.f4d5.temp`

#### Copia de seguridad en un directorio de destino no predeterminado {#backing-up-to-a-non-default-target-directory}

Normalmente, el archivo o directorio de copia de seguridad se crea en el servidor de la carpeta principal de la carpeta que contiene la carpeta `crx-quickstart`.

Si desea guardar la copia de seguridad (de cualquier tipo) en una ubicación diferente, puede establecer una ruta de acceso absoluta &quot;al parámetro `target` en el comando `curl`.

Por ejemplo, para generar `backupJune.zip` en el directorio `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Al utilizar un servidor de aplicaciones diferente (como JBoss), es posible que la copia de seguridad en línea no funcione según lo esperado porque el directorio de destino no se puede escribir. En este caso, póngase en contacto con Soporte técnico.

>[!NOTE]
>
>También se puede activar una copia de seguridad [ con los MBeans proporcionados por AEM](/help/sites-administering/jmx-console.md).

### Copia de seguridad de instantáneas del sistema {#filesystem-snapshot-backup}

El proceso descrito aquí es especialmente adecuado para repositorios grandes.

>[!NOTE]
>
>Si desea utilizar este método de copia de seguridad, su sistema debe admitir instantáneas del sistema de archivos. Por ejemplo, para Linux esto significa que los sistemas de archivos deben colocarse en un volumen lógico.

1. Realice una instantánea del sistema de archivos en el que está implementado AEM.

1. Monte la instantánea del sistema de archivos.
1. Realice una copia de seguridad y desmonte la instantánea.

### Funcionamiento de AEM Online Backup {#how-aem-online-backup-works}

Copias de seguridad en línea de AEM consta de una serie de acciones internas para garantizar la integridad de los datos de los que se realiza una copia de seguridad y de los archivos de copia de seguridad que se crean. Estos se enumeran a continuación para los interesados.

La copia de seguridad en línea utiliza el siguiente algoritmo:

1. Al crear un archivo zip, el primer paso es crear o localizar el directorio de destino.

   * Si realiza una copia de seguridad en un archivo zip, se crea un directorio temporal. El nombre del directorio comienza con `backup.` y termina con `.temp`; por ejemplo, `backup.f4d3.temp`.
   * Si se realiza una copia de seguridad en un directorio, se utiliza el nombre especificado en la ruta de destino. Se puede utilizar un directorio existente; de lo contrario, se creará un nuevo directorio.

     Se crea un archivo vacío denominado `backupInProgress.txt` en el directorio de destino cuando se inicia la copia de seguridad. Este archivo se elimina cuando finaliza la copia de seguridad.

1. Los archivos se copian del directorio de origen al directorio de destino (o al directorio temporal al crear un archivo zip). El almacén de segmentos se copia antes del almacén de datos para evitar daños en el repositorio. Los datos de índice y de caché se omiten al crear la copia de seguridad. Como resultado, los datos de `crx-quickstart/repository/cache` y `crx-quickstart/repository/index` no se incluyen en la copia de seguridad. El indicador de barra de progreso del proceso está entre 0% y 70% al crear un archivo zip o entre 0% y 100% si no se crea ningún archivo zip.

1. Si la copia de seguridad se realiza en un directorio preexistente, se eliminan los archivos &quot;antiguos&quot; del directorio de destino. Los archivos antiguos son archivos que no existen en el directorio de origen.

Los archivos se copian en el directorio de destino en cuatro fases:

1. En la primera fase de copia (indicador de progreso 0% - 63% al crear un archivo zip o 0% - 90% si no se crea ningún archivo zip), todos los archivos se copian mientras el repositorio se ejecuta normalmente. El proceso consta de dos fases:

   * Fase A: todo se copia excepto el almacén de datos (con retraso).
   * Fase B: solo se copia el almacén de datos (con retraso).

1. En la segunda fase de copia (indicador de progreso 63 % - 65,8 % al crear un archivo zip o 90 % - 94 % si no se crea ningún archivo zip), solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la primera fase de copia. Según la actividad del repositorio, esto puede variar desde la ausencia total de archivos hasta un número significativo de archivos (porque la primera fase de copia de archivos suele ser la que más tiempo tarda). El proceso de copia es similar al de la primera fase (Fase A y Fase B con retraso).
1. En la tercera fase de copia (indicador de progreso 65,8% - 68,6% al crear un archivo zip o 94% - 98% si no se crea ningún archivo zip) solo se copian los archivos que se crearon o modificaron en el directorio de origen desde que se inició la segunda fase de copia. Según la actividad del repositorio, puede que no haya archivos que copiar o que haya un número muy pequeño de archivos (porque la segunda fase de copia de archivos suele ser rápida). El proceso de copia es similar al de la segunda fase: Fase A y Fase B, pero sin demora.
1. Las fases de copia de archivos de uno a tres se realizan simultáneamente mientras se ejecuta el repositorio. Solo se copian los archivos creados o modificados en el directorio de origen desde que se inició la tercera fase de copia. Según la actividad del repositorio, puede que no haya archivos para copiar o que haya un número muy, muy pequeño de archivos (porque la segunda fase de copia de archivos suele ser muy rápida). Indicador de progreso 68,6% - 70% al crear un archivo zip o 98% - 100% si no se crea ningún archivo zip. El proceso de copia es similar al de la tercera fase.
1. Según el objetivo:

   * Si se ha especificado un archivo zip, ahora se crea desde el directorio temporal. Indicador de progreso 70% - 100%. A continuación, se elimina el directorio temporal.
   * Si el destino era un directorio, se elimina el archivo vacío denominado `backupInProgress.txt` para indicar que la copia de seguridad ha finalizado.

## Restauración de la copia de seguridad {#restoring-the-backup}

Puede restaurar una copia de seguridad de la siguiente manera:

* Si ha realizado una copia de seguridad de instantáneas del sistema de archivos, simplemente puede restaurar una imagen del sistema.
* Si ha creado la copia de seguridad como archivo zip, solo tiene que descomprimir el contenido en una nueva carpeta e iniciar AEM desde esa ubicación.

## Copia de seguridad {#package-backup}

Para realizar una copia de seguridad y restaurar contenido, puede utilizar uno de los Administrador de paquetes, que utiliza el formato Paquete de contenido para realizar una copia de seguridad y restaurar contenido. El Administrador de paquetes proporciona más flexibilidad para definir y administrar paquetes.

Para obtener más información sobre las características y las ventajas y desventajas de cada uno de estos formatos de paquete de contenido individual, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

### Ámbito de la copia de seguridad {#scope-of-backup}

Al realizar una copia de seguridad de los nodos mediante el Administrador de paquetes o el Cremallera de contenido, CRX guarda la siguiente información:

* El contenido del repositorio debajo del árbol seleccionado.
* Las definiciones del tipo Nodo que se utilizan para el contenido del que realiza una copia de seguridad.
* Las definiciones de área de nombres que se utilizan para el contenido del que realiza una copia de seguridad.

Al realizar una copia de seguridad, AEM pierde la siguiente información:

* El historial de versiones.
