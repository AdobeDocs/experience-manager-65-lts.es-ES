---
title: Preparar AEM Forms para copia de seguridad
description: Aprenda a utilizar el servicio de copia de seguridad y restauración para entrar y salir del modo de copia de seguridad del servidor de AEM Forms mediante la API de Java y la API del servicio web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 0fe1aef7-f607-4c40-bfa9-9ec9ebd8abeb
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 0%

---

# Preparar AEM Forms para copia de seguridad {#preparing-aem-forms-for-backup}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Acerca del servicio de backup y restauración {#about-the-backup-and-restore-service}

El servicio de copia de seguridad y restauración le permite poner AEM Forms en *modo de copia de seguridad*, que permite realizar copias de seguridad en caliente. El servicio de copia de seguridad y restauración no realiza una copia de seguridad de AEM Forms ni restaura el sistema. En su lugar, pone al servidor en un estado de backup coherente y fiable, a la vez que permite que el servidor siga funcionando. Usted es responsable de las acciones para realizar una copia de seguridad de Global Document Storage (GDS) y de la base de datos conectada al servidor de Forms. El GDS es un directorio que se utiliza para almacenar archivos utilizados en un proceso de larga duración.

El modo de copia de seguridad es un estado que introduce el servidor para que los archivos del GDS no se purguen mientras se realiza un procedimiento de copia de seguridad. En su lugar, los subdirectorios se crean en el directorio GDS para mantener un registro de los archivos que se van a purgar una vez finalizado el modo de guardado de copia de seguridad. Un archivo está diseñado para sobrevivir a los reinicios del sistema y puede abarcar días o incluso años. Estos archivos son una parte esencial del estado general del servidor de Forms y pueden incluir archivos de PDF, directivas o plantillas de formulario. Si se pierde o se daña alguno de estos archivos, los procesos del servidor de Forms pueden volverse inestables y los datos podrían perderse.

Puede optar por realizar copias de seguridad de instantáneas, en las que normalmente entraría en modo de copia de seguridad durante un período y, a continuación, dejaría el modo de copia de seguridad después de completar las actividades de copia de seguridad. Se requiere salir del modo de copia de seguridad para que los archivos se puedan purgar del GDS y garantizar que no crezca innecesariamente. Puede dejar el modo de copia de seguridad explícitamente o esperar a que caduque el tiempo en una sesión en modo de copia de seguridad.

También puede dejar el servidor en modo de copia de seguridad perpetua, que es típico de las estrategias de copia de seguridad para copias de seguridad móviles o cobertura continua del sistema. El modo de copia de seguridad móvil indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión de modo de copia de seguridad iniciada en cuanto se libera la sesión anterior. Cuando se encuentra en modo de copia de seguridad continua, se purga un archivo después de dos sesiones en modo de copia de seguridad y ya no se hace referencia a él.

Puede utilizar el servicio Copia de seguridad y restauración para agregar a aplicaciones existentes o nuevas aplicaciones que cree para realizar copias de seguridad del GDS o de la base de datos conectada al servidor de Forms.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de la implementación de AEM Forms, la estrategia de copia de seguridad y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en producción, para garantizar que toda la solución funcione según lo esperado sin perder datos.

Puede realizar estas tareas mediante el servicio Copia de seguridad y restauración:

* Entrar en modo de copia de seguridad.
* Dejar el modo de copia de seguridad.

>[!NOTE]
>
>Para obtener más información acerca de qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio de copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Introducción del modo de copia de seguridad en Forms Server {#entering-backup-mode-on-the-forms-server}

Se entra en modo de copia de seguridad para permitir copias de seguridad en caliente de un servidor de Forms. Al entrar en el modo de copia de seguridad, debe especificar la siguiente información en función de los procedimientos de copia de seguridad de su organización:

* Una etiqueta única para identificar la sesión del modo de copia de seguridad que puede ser útil para los procesos de copia de seguridad.
* Hora a la que se completó el procedimiento de copia de seguridad.
* Un indicador que indica si se debe estar en modo de copia de seguridad continua, lo que resulta útil solo si se realizan copias de seguridad móviles.

Antes de escribir aplicaciones para entrar en modo de copia de seguridad, se recomienda que comprenda los procedimientos de copia de seguridad que se utilizan después de poner el servidor de Forms en modo de copia de seguridad. Para obtener más información acerca de qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio de copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una aplicación que entre en modo de copia de seguridad, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente BackupService.
1. Determine una etiqueta única, la cantidad de tiempo para realizar la copia de seguridad y si debe estar en modo de copia de seguridad continua.
1. Entrar en modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión del modo de copia de seguridad en el servidor.
1. Realizar la copia de seguridad del GDS (almacén de datos global) y de la base de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Es importante incluir estos archivos en el proyecto para compilar el código correctamente y utilizar la API del servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, cree un objeto de cliente BackupService para utilizar la API del servicio de copia de seguridad y restauración.

**Decida una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si desea estar en modo de copia de seguridad continua**

Antes de entrar en el modo de copia de seguridad, debe decidir una etiqueta única, determinar la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decidir si desea que el servidor de Forms permanezca en modo de copia de seguridad. Estas consideraciones son importantes para integrarlas con los procedimientos de copia de seguridad establecidos por su organización. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Ingresar al modo de copia de seguridad**

Introduzca el modo de copia de seguridad con los parámetros que son coherentes con los procedimientos de copia de seguridad de su organización.

**Recuperar información sobre la sesión del modo de copia de seguridad en el servidor**

Después de entrar en el modo de copia de seguridad, puede recuperar información sobre la sesión. Esta información se puede utilizar para integrarla con los procedimientos de copia de seguridad

**Realizar la copia de seguridad del GDS y de la base de datos**

Después de entrar correctamente en el modo de copia de seguridad, puede realizar una copia de seguridad de Global Document Storage (GDS) y de la base de datos a la que está conectado el servidor de Forms. Este paso es específico de su organización, ya que puede realizarlo manualmente o ejecutar otras herramientas para realizar el procedimiento de copia de seguridad.

### Acceder al modo de copia de seguridad mediante la API de Java {#enter-backup-mode-using-the-java-api}

Inicie el modo de copia de seguridad mediante la API del servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   Incluya los archivos JAR de cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clase del proyecto Java. Para crear la aplicación cliente Java, se deben agregar los siguientes archivos JAR a la ruta de clase del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

1. Crear un objeto de API de cliente de BackupService

   Utiliza un objeto `ServiceClientFactory` y el objeto API de cliente BackupService juntos.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un objeto `BackupService` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Decida una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si desea estar en modo de copia de seguridad continua

   Decida una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de Forms permanezca en modo de copia de seguridad continua.

1. Entrar en modo de copia de seguridad

   Especifique el modo de copia de seguridad invocando el método `enterBackupMode` con los parámetros siguientes:

   * Valor de `String` que especifica una etiqueta única legible en lenguaje natural que identifica la sesión del modo de copia de seguridad. Se recomienda no utilizar espacios ni caracteres que no se puedan codificar en formato XML.
   * Valor de `int` que especifica el número de minutos que se mantendrán en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (la cantidad de minutos en una semana). Este valor se omite al utilizar el modo de copia de seguridad continua.
   * Valor de `Boolean` que especifica si se va a realizar una copia de seguridad continua. Un valor de `True` especifica que está en modo de copia de seguridad continua. En el modo de copia de seguridad continua, se omite el valor especificado para el número de minutos que deben permanecer en el modo de copia de seguridad.

     El modo de copia de seguridad continua significa que se inicia una nueva sesión de modo de copia de seguridad después de que se complete la actual. Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos de GDS.

1. Recuperar información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información utilizando el objeto `BackupModeEntryResult` devuelto después de invocar el método `enterBackupMode`. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para la integración con sus procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

1. Realizar la copia de seguridad del GDS y la base de datos

   Haga una copia de seguridad de Global Document Storage (GDS) y de la base de datos a la que está conectado Forms Server. Las acciones para realizar la copia de seguridad no forman parte de AEM Forms SDK y pueden incluso incluir pasos manuales específicos de los procedimientos de copia de seguridad de su organización.

### Acceder al modo de copia de seguridad mediante la API de servicio web {#enter-backup-mode-using-the-web-service-api}

Inicie el modo de copia de seguridad mediante el servicio web proporcionado por la API del servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de la API del servicio de copia de seguridad y restauración.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `BackupServiceService` invocando su constructor predeterminado y especifique las credenciales mediante el método `Credentials`.

1. Decida una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si desea estar en modo de copia de seguridad continua

   Decida una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de Forms permanezca en modo de copia de seguridad continua.

1. Entrar en modo de copia de seguridad

   Para entrar en el modo de copia de seguridad, invoque el método enterBackupMode y pase los siguientes valores:

   * Valor de `String` que especifica una etiqueta única legible en lenguaje natural que identifica la sesión del modo de copia de seguridad. Se recomienda no utilizar espacios ni caracteres que no se puedan codificar en formato XML.
   * Valor de `Uint32` que especifica el número de minutos que deben permanecer en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (cantidad de minutos en una semana). Este valor se omite al utilizar el modo de copia de seguridad continua.
   * Valor de `Boolean` que especifica si se va a realizar una copia de seguridad continua. Un valor de `True` especifica que está en modo de copia de seguridad continua. En el modo de copia de seguridad continua, se omite el valor especificado para el número de minutos que deben permanecer en el modo de copia de seguridad. El modo de copia de seguridad continua significa que se inicia una nueva sesión de modo de copia de seguridad después de que se complete la actual.

     Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos de GDS.

1. Recuperar información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información acerca de la sesión del modo de copia de seguridad después de invocar el método enterBackupMode desde BackupModeEntryResult que se devuelve para comprobar que se realizó correctamente. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para la integración con sus procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

1. Realizar la copia de seguridad del GDS y la base de datos

   Haga una copia de seguridad de Global Document Storage (GDS) y de la base de datos a la que está conectado Forms Server. Las acciones para realizar la copia de seguridad no forman parte de AEM Forms SDK y pueden incluso incluir pasos manuales específicos de los procedimientos de copia de seguridad de su organización.

## Dejar el modo de copia de seguridad en Forms Server {#leaving-backup-mode-on-the-forms-server}

Se abandona el modo de copia de seguridad para que Forms Server reanude la depuración de archivos del GDS (Global Document Storage) en Forms Server.

Antes de escribir las aplicaciones para entrar en el modo de salida, se recomienda que comprenda los procedimientos de copia de seguridad que se utilizan con AEM Forms. Para obtener más información acerca de qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio de copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para salir del modo de copia de seguridad, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente BackupService.
1. Dejar el modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión del modo de copia de seguridad que se estaba ejecutando en el servidor de Forms.

**Incluir archivos de proyecto**

Incluya todos los archivos necesarios en el proyecto de desarrollo. Estos archivos son importantes para compilar el código correctamente y utilizar la API del servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crear un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, cree un objeto de cliente BackupService para utilizar la API del servicio de copia de seguridad y restauración.

**Dejar el modo de copia de seguridad**

Deje el modo de copia de seguridad para reanudar la depuración normal de archivos del almacenamiento global de documentos (GDS). Antes de salir del modo de copia de seguridad, debe comprobar que se han completado los procedimientos de copia de seguridad.

**Recuperar información sobre la sesión del modo de copia de seguridad que finalizó**

Una vez que haya abandonado el modo de copia de seguridad, podrá recuperar información sobre la sesión. Esta información se puede utilizar para integrarla con los procedimientos de copia de seguridad.

### Dejar el modo de copia de seguridad mediante la API de Java {#leave-backup-mode-using-the-java-api}

Dejar el modo de copia de seguridad mediante la API del servicio de copia de seguridad y restauración (Java):

1. Incluir archivos de proyecto

   Incluya los archivos JAR de cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clase del proyecto Java. Para crear una aplicación cliente Java, se deben añadir los siguientes archivos JAR a la ruta de clase del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

1. Crear un objeto de API de cliente de BackupService

   Utiliza un objeto `ServiceClientFactory` y el objeto API de cliente BackupService juntos.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Cree un objeto `BackupService` utilizando su constructor y pasando el objeto `ServiceClientFactory` como parámetro.

1. Entrar en modo de copia de seguridad

   Salga del modo de copia de seguridad invocando el método `leaveBackupMode`.

1. Recuperar información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información sobre la operación utilizando el objeto `BackupModeResult` que se ha devuelto. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para la integración con sus procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

### Dejar el modo de copia de seguridad mediante la API de servicio web {#leave-backup-mode-using-the-web-service-api}

Dejar el modo de copia de seguridad mediante la API del servicio de copia de seguridad y restauración (servicio web):

1. Incluir archivos de proyecto

   Para utilizar servicios web, debe asegurarse de incluir los archivos proxy. Siga estos pasos para configurar el proyecto de modo que utilice la API del servicio de copia de seguridad y restauración como servicio web.

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de la API del servicio de copia de seguridad y restauración.
   * Hacer referencia al ensamblado de cliente de Microsoft .NET.

1. Crear un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `BackupServiceService` invocando su constructor predeterminado.

1. Entrar en modo de copia de seguridad

   Salir del modo de copia de seguridad invocando la operación del servicio web `leaveBackupMode`.

1. Recuperar información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere el identificador del modo de copia de seguridad después de la operación para comprobar que se ha realizado correctamente. La información que puede recuperar después de salir del modo de copia de seguridad puede ser útil para integrarla con los procedimientos de copia de seguridad.
