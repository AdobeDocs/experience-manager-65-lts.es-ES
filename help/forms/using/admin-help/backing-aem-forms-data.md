---
title: Copia de seguridad de los datos de Adobe Experience Manager Forms
description: En este documento se describen los pasos necesarios para realizar una copia de seguridad activa o en línea de la base de datos de formularios de Adobe Experience Manager (AEM), el GDS y los directorios raíz del almacenamiento de contenido.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 0%

---

# Copia de seguridad de los datos de Forms de Adobe Experience Manager (AEM) {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

En esta sección se describen los pasos necesarios para realizar una copia de seguridad activa o en línea de la base de datos de AEM Forms, el GDS y los directorios raíz del almacenamiento de contenido.

Una vez instalado AEM Forms e implementado en las áreas de producción, el administrador de la base de datos debe realizar una copia de seguridad inicial completa o en frío de la base de datos. La base de datos debe cerrarse para esta copia de seguridad. A continuación, deben realizarse regularmente copias de seguridad diferenciales o incrementales (o rápidas) de la base de datos.

Para garantizar una copia de seguridad y una recuperación correctas, siempre debe estar disponible una copia de seguridad de imagen del sistema. A continuación, si se produce una pérdida, puede recuperar todo el entorno a un estado coherente.

Realizar una copia de seguridad de la base de datos al mismo tiempo que las copias de seguridad del directorio GDS, del repositorio de AEM y del directorio raíz de almacenamiento de contenido ayuda a mantener estos sistemas sincronizados si alguna vez es necesaria la recuperación.

El procedimiento de copia de seguridad descrito en esta sección requiere que introduzca el modo de copia de seguridad segura antes de realizar la copia de seguridad de la base de datos de AEM Forms, el repositorio de AEM, GDS y los directorios raíz del almacenamiento de contenido. Cuando se complete la copia de seguridad, debe salir del modo de copia de seguridad segura. El modo de copia de seguridad segura se utiliza para marcar documentos persistentes y de larga duración que residen en el GDS. Este modo garantiza que el mecanismo automatizado de limpieza de archivos (el Recolector de archivos) no elimine los archivos caducados hasta que se libere el modo de copia de seguridad segura. Es necesario mantener una copia de seguridad de GDS sincronizada con una copia de seguridad de la base de datos.

La frecuencia con la que se debe realizar una copia de seguridad de la ubicación de GDS depende de cómo se utilice AEM Forms y de las ventanas de copia de seguridad disponibles. La ventana de copia de seguridad puede verse afectada por procesos de larga duración, ya que pueden ejecutarse durante varios días. Si cambia, agrega y quita continuamente archivos de este directorio, debe realizar copias de seguridad de la ubicación de GDS con más frecuencia.

Si la base de datos se está ejecutando en modo de registro, como se describe en la sección anterior, también se debe hacer una copia de seguridad de los registros de la base de datos con frecuencia para que se puedan utilizar para restaurar la base de datos si hay un error de medios.

>[!NOTE]
>
>Los archivos a los que no se hace referencia pueden persistir en el directorio GDS después del proceso de recuperación. Actualmente, esta es una limitación conocida.

## Haga una copia de seguridad de la base de datos, GDS, repositorio de AEM y directorios raíz de almacenamiento de contenido {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Ponga AEM Forms en modo de copia de seguridad segura (instantánea) o de copia de seguridad móvil (cobertura continua). Antes de configurar AEM Forms para que entre en cualquiera de los modos de copia de seguridad, asegúrese de lo siguiente:

* Compruebe la versión del sistema y registre los parches o actualizaciones aplicados desde que se realizó la última copia de seguridad completa de la imagen del sistema.
* Si utiliza copias de seguridad móviles o en modo de instantánea, asegúrese de que la base de datos está configurada con los valores de registro correctos para permitir copias de seguridad rápidas de la base de datos. (Consulte [base de datos de AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Además de esto, observe las siguientes directrices para el proceso de copia de seguridad y restauración.

* Realice una copia de seguridad del directorio GDS mediante un sistema operativo disponible o una utilidad de copia de seguridad de terceros. (Consulte [Ubicación de GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Opcional) Realice una copia de seguridad del directorio raíz de almacenamiento de contenido mediante un sistema operativo disponible o una copia de seguridad y una utilidad de terceros. (Consulte [Ubicación raíz del almacenamiento de contenido (entorno independiente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Ubicación raíz del almacenamiento de contenido (entorno en clúster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Copia de seguridad   instancias de autor y publicación (copia de seguridad del repositorio crx).

  Para realizar una copia de seguridad del entorno de la solución Administración de correspondencia, realice los pasos en las instancias de autor y publicación que se describen en [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md).

  Tenga en cuenta los siguientes puntos al realizar copias de seguridad de las instancias de autor y publicación:

   * Asegúrese de que la copia de seguridad de las instancias de autor y publicación se sincronice para iniciarse al mismo tiempo. Aunque puede seguir utilizando instancias de autor y publicación mientras se realiza la copia de seguridad, se recomienda no publicar ningún recurso durante la copia de seguridad para evitar cualquier cambio no capturado. Espere a que finalice la copia de seguridad de las instancias de autor y publicación antes de publicar nuevos recursos.
   * La copia de seguridad completa del nodo Autor incluye una copia de seguridad de los datos de Forms Manager y AEM Forms Workspace.
   * Los desarrolladores de Workbench pueden seguir trabajando en sus procesos localmente. No deben implementar ningún proceso nuevo durante la fase de copia de seguridad.
   * La decisión sobre la duración de cada sesión de copia de seguridad (para el modo de copia de seguridad móvil) debe basarse en el tiempo total necesario para realizar una copia de seguridad de todos los datos de AEM Forms (BD, GDS, repositorio de AEM y cualquier otro dato personalizado adicional).

Haga una copia de seguridad de la base de datos de AEM Forms, incluidos los registros de transacciones. Ver [base de datos de AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

Para obtener más información, consulte el artículo de la base de conocimiento correspondiente a su base de datos:
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [Copia de seguridad y recuperación de Oracle para AEM Forms](https://www.adobe.com/go/kb403624)
* [Copia de seguridad y recuperación de MySQL para AEM Forms](https://www.adobe.com/go/kb403625)
* [Copia de seguridad y recuperación de Microsoft® SQL Server para AEM Forms](https://www.adobe.com/go/kb403623)
* Copia de seguridad y recuperación de [DB2® para AEM Forms](https://www.adobe.com/go/kb403626)

En estos artículos se proporciona orientación sobre las funciones básicas de la base de datos para la copia de seguridad y recuperación de datos. No están pensados como guías técnicas inclusivas de la función de copia de seguridad y recuperación de la base de datos de un proveedor específico. Describen los comandos necesarios para crear una estrategia de copia de seguridad de base de datos fiable para los datos de la aplicación AEM Forms.

>[!NOTE]
>
>La copia de seguridad de la base de datos debe estar completa antes de comenzar a realizar la copia de seguridad del GDS. Si no se ha completado la copia de seguridad de la base de datos, los datos no están sincronizados.

### Introducción de los modos de copia de seguridad {#entering-the-backup-modes}

Puede utilizar la consola de administración, el comando LCBackupMode o la API disponible con la instalación de AEM Forms para entrar y salir de los modos de copia de seguridad. Para la copia de seguridad móvil (cobertura continua), la opción de la consola de administración no está disponible; debe utilizar la opción de línea de comandos o la API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Si configuró SSL en el servidor de Forms, no puede colocar el servidor de Forms en modo de copia de seguridad mediante el script LCBackupMode.CMD.

**Uso de la consola de administración para entrar en el modo de copia de seguridad segura**

1. Inicie sesión en la consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

   Este método pone AEM Forms en modo de copia de seguridad indefinidamente (sin tiempo de espera) y entra en modo de instantánea en lugar de modo de copia de seguridad móvil.

**Usando la opción de línea de comandos para entrar en el modo de copia de seguridad segura**

Puede usar los scripts de la interfaz de línea de comandos `LCBackupMode` para poner AEM Forms en modo de copia de seguridad seguro.

1. Establezca ADOBE_LIVECYCLE e inicie el servidor de aplicaciones.
1. Vaya a la carpeta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Según el sistema operativo, edite el script `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar los valores predeterminados que sean adecuados para el sistema.
1. En el símbolo del sistema, ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nombre host* `] [-port=`*número de puerto* `] [-user=`*nombre de usuario* `] [-password=`*contraseña* `] [-label=`*nombre de etiqueta* `] [-timeout=`*segundos* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*nombre host* `] [-port=`*número de puerto* `] [-user=`*nombre de usuario* `] [-password=`*contraseña* `] [-label=`*nombre de etiqueta* `]`

   En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

   `Host` es el nombre del host donde se está ejecutando AEM Forms.

   `port` es el puerto WebServices del servidor de aplicaciones en el que se está ejecutando AEM Forms.

   `user` es el nombre de usuario del administrador de AEM Forms.

   `password` es la contraseña del administrador de AEM Forms.

   `label` es la etiqueta de texto, que puede ser cualquier cadena, para esta copia de seguridad.

   `timeout` es el número de segundos después de los cuales se deja automáticamente el modo de copia de seguridad. Puede ser de 0 a 10.080. Si es 0, que es el valor predeterminado, el modo de copia de seguridad nunca agota el tiempo de espera.

   Para obtener más información acerca de la interfaz de línea de comandos para el modo de copia de seguridad, vea el archivo Léame en el directorio BackupRestoreCommandline.

### Dejando los modos de copia {#leaving-backup-modes}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede utilizar la consola de administración o la opción de línea de comandos para dejar los modos de copia de seguridad.

**Dejar el modo de copia de seguridad segura (modo de instantánea)**

Para utilizar la consola de administración para sacar AEM Forms del modo de copia de seguridad segura (modo de instantánea), realice las siguientes tareas.

1. Inicie sesión en la consola de administración.
1. Haga clic en Configuración > Configuración del sistema principal > Utilidades de copia de seguridad.
1. Anule la selección de Operar en modo de copia de seguridad segura y haga clic en Aceptar.

**Dejar todos los modos de copia de seguridad**

Puede utilizar la interfaz de línea de comandos para sacar AEM Forms del modo de copia de seguridad segura (modo de instantánea) o para finalizar la sesión del modo de copia de seguridad actual (modo móvil). No puede utilizar la consola de administración para dejar el modo de copia de seguridad móvil. En el modo de copia de seguridad móvil, los controles Utilidades de copia de seguridad de la consola de administración están desactivados. Utilice la llamada de API o el comando LCBackupMode.

1. Vaya a la carpeta `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. Según el sistema operativo, edite el script `LCBackupMode.cmd` o `LCBackupMode.sh` para proporcionar los valores predeterminados que sean adecuados para el sistema.

   >[!NOTE]
   >
   >Establezca el directorio JAVA_HOME como se describe en el capítulo apropiado para su servidor de aplicaciones en [Preparación para instalar AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Ejecute el siguiente comando en una sola línea:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nombre host* `] [-port=`*número de puerto* `] [-user=`*nombre de usuario* `] [-password=`*contraseña* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nombre host* `] [-port=`*número de puerto* `] [-user=`*nombre de usuario* `] [-password=`*contraseña* `]`

     En los comandos anteriores, los marcadores de posición se definen de la siguiente manera:

     `Host` es el nombre del host donde se está ejecutando AEM Forms.

     `port` es el puerto en el que AEM Forms se está ejecutando en el servidor de aplicaciones.

     `user` es el nombre de usuario del administrador de AEM Forms.

     `password` es la contraseña del administrador de AEM Forms.

     `leaveContinuousCoverage` Utilice esta opción para deshabilitar completamente el modo de copia de seguridad móvil.

   >[!NOTE]
   >
   >Durante el tiempo que el modo de copia de seguridad esté desactivado, no se puede restablecer la cobertura continua. Los cambios realizados durante ese tiempo no están protegidos.

   >[!NOTE]
   >
   >Si habilitó el almacenamiento de documentos en la base de datos, el modo de copia de seguridad instantánea y los modos de copia de seguridad móvil no son aplicables.

   Para obtener más información acerca de la interfaz de línea de comandos para el modo de copia de seguridad, vea el archivo léame en el directorio BackupRestoreCommandline.
