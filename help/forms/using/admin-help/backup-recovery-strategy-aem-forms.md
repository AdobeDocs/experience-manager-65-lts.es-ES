---
title: Estrategia de copia de seguridad y recuperación para AEM Forms
description: Obtenga información sobre cómo implementar una estrategia para realizar copias de seguridad de los datos y asegurarse de que permanecen sincronizados con los datos de los formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 3%

---

# Estrategia de copia de seguridad y recuperación para AEM Forms{#backup-and-recovery-strategy-for-aem-forms}

Si la implementación de AEM Forms almacena datos personalizados adicionales en una base de datos diferente, usted es el responsable de implementar una estrategia para realizar una copia de seguridad de estos datos y garantizar que permanezcan sincronizados con los datos de los formularios de AEM. Además, la aplicación debe diseñarse para que sea lo suficientemente sólida como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Se recomienda encarecidamente que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para mantener un estado coherente.

Después de identificar cómo se utilizan los formularios AEM, determine de qué archivos se debe hacer copia de seguridad, con qué frecuencia y la ventana de copia de seguridad que se debe hacer disponible.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de la implementación de los formularios AEM, la estrategia de copia de seguridad y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en la producción, para garantizar que toda la solución funcione según lo esperado sin perder datos.

Adobe Experience Manager (AEM) es una parte integral de los formularios AEM. Por lo tanto, también debe realizar una copia de seguridad de AEM sincronizada con la copia de seguridad de los formularios de AEM, ya que la solución y los servicios de Administración de correspondencia, como el administrador de formularios, se basan en datos almacenados en la parte de AEM de los formularios de AEM.Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios de AEM de forma que se garantice que el GDS y el AEM (repositorio) se correlacionan con las referencias de la base de datos.Los directorios de la base de datos, el GDS, el AEM y el directorio raíz de almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

## Tipos de copias de seguridad {#types-of-backups}

La estrategia de copia de seguridad de formularios de AEM consta de dos tipos de copias de seguridad:

**Imagen del sistema:** Copia de seguridad completa del sistema que puede usar para restaurar el contenido del equipo si el disco duro o todo el equipo deja de funcionar. Una copia de seguridad de imagen del sistema solo es necesaria antes de la implementación de producción de los formularios AEM. Las políticas corporativas internas dictan con qué frecuencia se requieren los backups de imágenes del sistema.

**Datos específicos de formularios de AEM:** Los datos de la aplicación existen en la base de datos, el almacenamiento global de documentos (GDS) y el repositorio de AEM, y se debe realizar una copia de seguridad en tiempo real. GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan dentro de un proceso. Estos archivos pueden incluir PDF, directivas o plantillas de formulario.

>[!NOTE]
>
>Si Content Services (Obsoleto) está instalado, haga también una copia de seguridad del directorio raíz de almacenamiento de contenido. Consulte [Directorio raíz de almacenamiento de contenido (solo servicios de contenido)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de datos se utiliza para almacenar artefactos de formulario, configuraciones de servicio, estados de proceso y referencias de base de datos a archivos GDS. Si ha habilitado el almacenamiento de documentos en la base de datos, los datos persistentes y los documentos del GDS también se almacenan en la base de datos. Se puede realizar una copia de seguridad y recuperar la base de datos utilizando los métodos siguientes:

* El modo **Copia de seguridad de instantáneas** indica que el sistema de formularios de AEM está en modo de copia de seguridad indefinidamente o durante un número determinado de minutos, después de lo cual el modo de copia de seguridad ya no estará habilitado. Para entrar o salir del modo de copia de seguridad de instantánea, puede utilizar una de las siguientes opciones. Después de un escenario de recuperación, el modo de copia de seguridad de instantáneas no debe estar habilitado.

   * Utilice la página Valores de Copia de Seguridad de la Consola de Administración. Para entrar en el modo de instantánea, active la casilla de verificación Operar en modo de copia de seguridad segura. Anule la selección de la casilla de verificación para salir del modo de instantánea.
   * Use el script LCBackupMode (consulte [Realizar una copia de seguridad de la base de datos, GDS y los directorios raíz de almacenamiento de contenido](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Para salir del modo de copia de seguridad de instantáneas, en el argumento script, establezca el parámetro `continuousCoverage` en `false` o use la opción `leaveContinuousCoverage`.
   * Usar la API de copia de seguridad/recuperación proporcionada. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* El modo **Copia de seguridad móvil** indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión en modo de copia de seguridad que se inicia en cuanto se libera la sesión anterior. No hay tiempo de espera asociado al modo de copia de seguridad móvil. Cuando se llama al script LCBackupMode o a las API para dejar el modo de copia de seguridad móvil, se inicia una nueva sesión de modo de copia de seguridad móvil. Este modo es útil para admitir copias de seguridad continuas, pero sigue permitiendo que los documentos antiguos e innecesarios se limpien del directorio GDS. El modo de copia de seguridad móvil no es compatible a través de la página Copia de seguridad y recuperación. Después de un escenario de recuperación, el modo de copia de seguridad móvil sigue habilitado. Puede salir del modo de copia de seguridad continua (modo de copia de seguridad móvil) utilizando el script LCBackupMode con la opción `leaveContinuousCoverage`.

>[!NOTE]
>
>Si se abandona el modo de copia de seguridad móvil inmediatamente, se iniciará una nueva sesión de modo de copia de seguridad. Para deshabilitar completamente el modo de copia de seguridad móvil, use la opción `leaveContinuousCoverage` en el script, que sobrescribe la sesión de copia de seguridad móvil existente. En el modo de copia de seguridad de instantáneas, puede dejar el modo de copia de seguridad como lo hace habitualmente.

Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios de AEM de forma que se garantice que los documentos del directorio raíz de GDS y de almacenamiento de contenido se correlacionen con las referencias de la base de datos.

>[!NOTE]
>
>Cuando el GDS esté almacenado en el sistema de archivos y no en la base de datos, realice la copia de seguridad de la base de datos antes de la copia de seguridad del GDS.

## Consideraciones especiales para el backup y la recuperación {#special-considerations-for-backup-and-recovery}

Siga estas directrices si debe recuperar formularios AEM Forms en un entorno diferente debido a los siguientes cambios:

* Cambio en la dirección IP, el nombre de host o el puerto del servidor de AEM Forms
* Cambio en las letras de unidad o en la ruta de acceso del directorio
* Cambiar a un host, puerto o nombre de base de datos diferente

Normalmente, estos escenarios de recuperación se deben a un error de hardware del servidor que aloja el servidor de aplicaciones, el servidor de base de datos o el servidor de Forms. Además de las configuraciones específicas de los formularios AEM que se describen en esta sección, también debe realizar los cambios necesarios en otras partes de la implementación de AEM Forms, como equilibradores de carga y servidores de seguridad, si cambia el nombre de host o la dirección IP de un servidor AEM Forms.

### Qué no se puede cambiar {#what-cannot-be-changed}

Aunque puede cambiar el servidor de la base de datos y muchos otros parámetros, no puede cambiar el tipo de servidor de aplicaciones ni el tipo de base de datos cuando recupera formularios AEM de una copia de seguridad. Por ejemplo, si está recuperando una copia de seguridad de formularios AEM Forms, no puede cambiar el servidor de aplicaciones de JBoss a WebLogic o la base de datos de Oracle a DB2. Además, los formularios AEM recuperados deben utilizar las mismas rutas del sistema de archivos, como el directorio de fuentes.

### Reinicio tras una recuperación {#restarting-after-a-recovery}

Antes de reiniciar el servidor de Forms después de una recuperación, haga lo siguiente:

1. Inicie el sistema en modo de mantenimiento.
1. Haga lo siguiente para asegurarse de que el administrador de formularios se sincroniza con los formularios de AEM en el modo de mantenimiento:

   1. Vaya a https://&lt;*server*>:&lt;*port*>/lc/fm e inicie sesión con las credenciales de administrador/contraseña.
   1. Haga clic en el nombre del usuario (en este caso, Super Administrator) en la esquina superior derecha.
   1. Haga clic en **Opciones de administración**.
   1. Haga clic en **Iniciar** para sincronizar recursos del repositorio.

1. En un entorno agrupado, el nodo principal (con respecto a AEM) debe estar activo antes que los nodos secundarios.
1. Asegúrese de que no se inician procesos desde orígenes internos o externos como los iniciadores de procesos web, SOAP o EJB hasta que se valide el funcionamiento normal del sistema.

Si la base de datos de formularios de AEM principal se ha movido o cambiado, consulte las guías de instalación correspondientes a su servidor de aplicaciones para obtener información sobre cómo actualizar la información de conexión a la base de datos para las fuentes de datos de formularios de AEM IDP_DS y EDC_DS.

>[!NOTE]
> 
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

### Cambiar el nombre de host o la dirección IP de los formularios AEM {#changing-the-aem-forms-hostname-or-ip-address}

En un clúster, si utiliza el almacenamiento en caché TCP en lugar de UDP, debe actualizar la configuración del localizador de caché. Consulte &quot;Configuración de los localizadores de almacenamiento en caché (almacenamiento en caché solo mediante TCP)&quot; en la guía de configuración correspondiente a su servidor de aplicaciones.

### Cambiar las rutas del sistema de archivos del nodo de formularios de AEM {#changing-the-aem-forms-node-file-system-paths}

Si cambia las rutas del sistema de archivos de un nodo independiente, debe actualizar las referencias adecuadas en preferencias, otras configuraciones del sistema, aplicaciones personalizadas y aplicaciones de formularios AEM Forms implementadas. Por otro lado, para un clúster, todos los nodos deben utilizar la misma configuración de ruta del sistema de archivos. Establezca el directorio raíz de Global Document Storage (GDS) y asegúrese de que apunta a una copia del GDS recuperado que está sincronizado con la base de datos recuperada. La configuración de la ruta de GDS es importante porque el GDS puede contener datos que pretenden persistir tras los reinicios del servidor de aplicaciones.

En un entorno agrupado, la configuración de la ruta del sistema de archivos del repositorio debe ser la misma para todos los nodos del clúster antes de la copia de seguridad y después de la recuperación.

Use el script `LCSetGDS` de la carpeta `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` para establecer la ruta de acceso de GDS después de cambiar las rutas de acceso del sistema de archivos. Consulte el archivo `ReadMe.txt` en la misma carpeta para obtener detalles. Si no se puede usar la ruta de acceso al directorio GDS anterior, se debe usar el script `LCSetGDS` para establecer la nueva ruta de acceso al GDS antes de iniciar AEM Forms.

>[!NOTE]
>
>Esta circunstancia es la única en la que debería usar esta secuencia de comandos para cambiar la ubicación de GDS. Para cambiar la ubicación de GDS mientras se ejecuta AEM Forms, utilice la consola de administración. (Consulte [Configurar la configuración general de los formularios AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.)*

Después de establecer la ruta de acceso de GDS, inicie el servidor de Forms en modo de mantenimiento y utilice la consola de administración para actualizar las rutas de acceso restantes del sistema de archivos para el nuevo nodo. Después de comprobar que se han actualizado todas las configuraciones necesarias, reinicie y pruebe los formularios de AEM.
