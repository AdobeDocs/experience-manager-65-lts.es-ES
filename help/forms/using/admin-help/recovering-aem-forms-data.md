---
title: Recuperación de los datos de AEM Forms
description: En este documento se describen los pasos necesarios para recuperar los datos de los formularios AEM Forms.
contentOwner: admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 6345edda-cdc6-4e13-ade6-2dd6de9d9616
source-git-commit: f7adcbe7700d0ea9cbd18eb0b59bcd76f56e8cc5
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---

# Recuperación de los datos de AEM Forms {#recovering-the-aem-forms-data}

En esta sección se describen los pasos necesarios para recuperar los datos de los formularios AEM Forms. Vea también [Consideraciones especiales para la copia de seguridad y la recuperación](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>Los directorios de la base de datos, GDS, repositorio de AEM y raíz de almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

Los formularios AEM Forms se deben recuperar de forma fiable de los siguientes errores:

**Error de disco:** Se requiere el medio de copia de seguridad más reciente para recuperar el contenido de la base de datos.

**Datos dañados:** Los sistemas de archivos no registran transacciones anteriores y los sistemas pueden sobrescribir accidentalmente los datos de proceso necesarios.

**Error de usuario:** La recuperación se limita a los datos que la base de datos pone a disposición. Si los datos se almacenaron y están disponibles, la recuperación se simplifica.

**Corte de energía, bloqueo del sistema:** Las API del sistema de archivos no suelen diseñarse ni utilizarse de manera robusta que proteja contra errores inesperados del sistema. Si se produce un corte de alimentación o un bloqueo del sistema, es más probable que el contenido del documento almacenado en la base de datos esté actualizado que el contenido almacenado en un sistema de archivos.

Si está utilizando el modo de copia de seguridad móvil, aún está en modo de copia de seguridad después de la recuperación. Si está utilizando el modo de copia de seguridad de instantánea, no estará en modo de copia de seguridad después de la recuperación.

Al restaurar desde la copia de seguridad en un sistema nuevo, las siguientes configuraciones pueden ser diferentes. Esta diferencia no debería afectar a la correcta recuperación de la aplicación de AEM Forms:

* Dirección IP
* Configuración del sistema físico (CPU, disco, memoria)
* Ubicación de GDS

>[!NOTE]
>
>La copia de seguridad del directorio raíz de almacenamiento de contenido debe restaurarse a la ubicación de ese directorio tal como se estableció durante la configuración de Content Services.

Si un nodo único de un clúster de varios nodos ha fallado y los nodos restantes del clúster funcionan correctamente, realice el procedimiento de recuperación de nodo único del clúster.

## Recuperar los datos de los formularios AEM {#recover-the-aem-forms-data}

1. Detenga los servicios de formularios AEM Forms y el servidor de aplicaciones si se ejecuta.
1. Si es necesario, vuelva a crear el sistema físico a partir de una imagen del sistema. Por ejemplo, este paso puede no ser necesario si el motivo de la recuperación es un servidor de base de datos defectuoso.
1. Aplique parches o actualizaciones a los formularios de AEM aplicados desde que se creó la imagen. Esta información se registró en el procedimiento de copia de seguridad. Los formularios AEM deben tener parches al mismo nivel que cuando se realizó la copia de seguridad del sistema.
1. (Servidor de aplicaciones WebSphere®) Si se recupera en una nueva instancia de WebSphere®, ejecute el comando restoreConfig.bat/sh.
1. Recupere la base de datos de formularios AEM Forms ejecutando primero una operación de restauración de base de datos utilizando los archivos de copia de seguridad de la base de datos y, a continuación, aplicando los redo logs de transacción a la base de datos recuperada. (Consulte [base de datos de formularios AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Para obtener más información, consulte uno de estos artículos de la base de conocimientos:

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Copia de seguridad y recuperación de Oracle para formularios AEM](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [Copia de seguridad y recuperación de MySQL para formularios AEM](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Recupere el directorio GDS eliminando primero el contenido del directorio GDS en la instalación existente de los formularios AEM Forms y, a continuación, copiando el contenido del directorio GDS del GDS de copia de seguridad. Si cambió la ubicación del directorio GDS, consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Cambie el nombre del directorio de copia de seguridad de GDS que desea restaurar, como se muestra en estos ejemplos:

   >[!NOTE]
   >
   >Si el directorio /restore ya existe, haga una copia de seguridad del mismo y elimínelo antes de cambiar el nombre del directorio /backup que contiene los datos más recientes.

   * (JBoss®) Cambiar el nombre de `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` a:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Cambiar nombre `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` a:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Cambie el nombre de `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` a:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Recupere el directorio raíz de almacenamiento de contenido eliminando primero el contenido del directorio raíz de almacenamiento de contenido en la instalación existente de los formularios de AEM y, a continuación, recuperando el contenido siguiendo las tareas para los entornos independientes o agrupados:

   >[!NOTE]
   >
   >La copia de seguridad del directorio raíz de almacenamiento de contenido debe restaurarse a la ubicación del directorio raíz de almacenamiento de contenido tal como se estableció durante la configuración de Content Services (obsoleto).

   **Independiente:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo una copia de seguridad. Cuando se restauren estos directorios, si el directorio /backup-lucene-indexes está presente, renómbrelo a /lucene-indexes. De lo contrario, el directorio lucene-indexes ya debería existir y no se requiere ninguna acción.

   **Agrupados:** Durante el proceso de recuperación, restaure todos los directorios de los que se hizo una copia de seguridad. Para restaurar el directorio raíz del índice, realice los siguientes pasos en cada nodo del clúster:

   * Elimine todo el contenido del directorio raíz del índice.
   * Si el directorio /backup-lucene-indexes está presente, copie el contenido del directorio *Raíz de almacenamiento de contenido*/backup-lucene-indexes al directorio Raíz de índice y elimine el directorio *Raíz de almacenamiento de contenido*/backup-lucene-indexes.
   * Si el directorio /lucene-indexes está presente, copie el contenido del directorio *Raíz de almacenamiento de contenido*/directorio lucene-indexes al directorio Raíz de índice.

1. Restaurar/recuperar el repositorio de CRX.

   * **Independiente**

     *Restaurar instancias de autor y publicación*: Si se produce un desastre, puede restaurar el repositorio al último estado de copia de seguridad realizando los pasos descritos en [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md).

     La restauración completa del nodo Autor también determina la restauración de los datos de Forms Manager y AEM Forms Workspace.

   * **Agrupado**

     Para la restauración en un entorno en clúster, consulte [Estrategia de copia de seguridad y restauración en un entorno en clúster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Elimine cualquier archivo temporal de formularios AEM Forms que se haya creado en el directorio java.io.temp o en el directorio temporal de Adobe.
1. Iniciar formularios AEM (consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Cambio de la ubicación de GDS durante la recuperación {#changing-the-gds-location-during-recovery}

Si el GDS se restaura en una ubicación distinta a la original, ejecute el script LCSetGDS para establecer el GDS en la nueva ubicación. El script se encuentra en la carpeta `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. El script toma dos parámetros, `defaultGDS` y `newGDS`. Consulte el archivo `ReadMe.txt` en la misma carpeta para obtener instrucciones sobre cómo ejecutar el script.

>[!NOTE]
>
>Si ha habilitado el almacenamiento de documentos en la base de datos, no es necesario cambiar la ubicación de GDS.

>[!NOTE]
>
>Esta circunstancia es la única en la que debería usar esta secuencia de comandos para cambiar la ubicación de GDS. Para cambiar la ubicación de GDS mientras se ejecuta AEM Forms, utilice la consola de administración. (Consulte [Configurar la configuración general de los formularios AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)).

>[!NOTE]
>
>La implementación de componentes fallará en Windows si el directorio GDS se encuentra en la raíz de la unidad (por ejemplo, D:\). Para GDS, debe asegurarse de que el directorio no se encuentra en la raíz de la unidad, sino en un subdirectorio. Por ejemplo, el directorio debe ser D:\GDS y no simplemente D:\.

## Recuperación del GDS en un entorno agrupado {#recovering-the-gds-to-a-clustered-environment}

Para cambiar la ubicación de GDS en un entorno agrupado, apague todo el clúster y ejecute el script LCSetGDS en un solo nodo del clúster. (Consulte [Cambio de la ubicación de GDS durante la recuperación](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Inicie solo ese nodo. Cuando ese nodo esté completamente iniciado, es posible que otros nodos del clúster se inicien de forma segura y apunten correctamente al nuevo GDS.

>[!NOTE]
>
>Si no puede asegurarse de que se inicia un nodo completamente antes de iniciar otros nodos, debe ejecutar el script LCSetGDS en todos los nodos del clúster antes de iniciar el clúster.
