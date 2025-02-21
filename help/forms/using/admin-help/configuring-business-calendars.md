---
title: Configurar calendarios comerciales
description: Los calendarios comerciales definen los días laborables y no laborables de la organización. Obtenga información sobre cómo configurar los calendarios empresariales.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---

# Configurar calendarios comerciales {#configuring-business-calendars}

*Los calendarios comerciales* definen los días laborables y no laborables (por ejemplo, los feriados legales, los fines de semana y los días de cierre de la empresa) de su organización. Al utilizar los calendarios comerciales, los formularios AEM Forms omiten los días no laborables al realizar determinados cálculos de fechas. En Workbench, puede especificar si desea utilizar calendarios comerciales para eventos asociados a usuarios, como recordatorios de tareas, plazos y escalaciones, o para acciones no asociadas a usuarios, como Eventos de temporizador y el Servicio de espera.

Por ejemplo, se configura un recordatorio de tarea para que se produzca tres días hábiles después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. Sin embargo, los tres días siguientes no son días laborables porque el viernes es feriado nacional y los dos días siguientes son días de fin de semana. Por lo tanto, el recordatorio se envía el miércoles de la semana siguiente.

>[!NOTE]
>
>Al calcular fechas y horas mediante calendarios comerciales, los formularios AEM Forms utilizan la fecha y la hora del servidor en el que se está ejecutando y no se ajustan a la diferencia entre las zonas horarias. Por ejemplo, si un recordatorio de tarea está programado para producirse a las 10:00 a. m. en un servidor que se ejecute en Londres, pero el usuario que recibe el recordatorio está en la ciudad de Nueva York, recibirá el recordatorio a las 5:00 a. m. hora local.

## Usar el calendario empresarial predeterminado {#using-the-default-business-calendar}

Los formularios AEM Forms proporcionan un calendario empresarial predeterminado (denominado *Calendario integrado*) que designa los sábados y los domingos como días no laborables. Si todos los usuarios de su organización tienen los mismos días no laborables, puede actualizar el calendario laboral predeterminado para adaptarlo a su organización. Al utilizar únicamente el calendario empresarial predeterminado, no es necesario habilitar los calendarios comerciales en Administración de usuarios ni proporcionar asignaciones. Cuando no se definen otros calendarios comerciales, los formularios AEM Forms utilizan el calendario empresarial predeterminado.

## Configurar varios calendarios comerciales {#setting-up-multiple-business-calendars}

Si algunos usuarios de su organización tienen diferentes días no laborables, puede definir varios calendarios comerciales y configurar asignaciones que permitan la resolución en tiempo de ejecución de un calendario empresarial para un usuario.

### Definir varios calendarios comerciales {#define-multiple-business-calendars}

1. Decida cómo va a asociar el calendario empresarial adecuado a un usuario. Existen dos formas de asociar un calendario empresarial a un usuario:

   **Pertenencia a un grupo:** Puede asignar un calendario empresarial a un usuario según la pertenencia a un grupo del usuario. En este caso, cada usuario del grupo utilizará el mismo calendario empresarial.

   Si un usuario es miembro de dos grupos diferentes y esos grupos están asignados a dos calendarios comerciales diferentes, los formularios AEM Forms utilizarán el primer calendario que encuentre en sus resultados de búsqueda. En este caso, considere la posibilidad de utilizar claves de calendario empresarial para asociar usuarios con calendarios comerciales.

   **Claves del calendario empresarial:** Puede asignar un calendario empresarial a un usuario basándose en una clave de calendario empresarial, que es una configuración especificada en Administración de usuarios. A continuación, asigne la clave del calendario empresarial a un calendario empresarial en el flujo de trabajo de formularios.

   La forma de asignar claves de calendario empresarial a los usuarios depende de si utiliza un dominio empresarial, local o híbrido. Para obtener más información sobre la configuración de dominios, consulte [Agregar dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Si utiliza un dominio local o híbrido, la información sobre los usuarios se almacena únicamente en la base de datos de Administración de usuarios. Para establecer la clave del calendario empresarial para estos usuarios, escriba una cadena en el campo Clave del calendario empresarial al agregar o editar un usuario en Administración de usuarios. (Consulte [Agregar y configurar usuarios](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) A continuación, asigne las claves del calendario empresarial (las cadenas) a los calendarios comerciales en el flujo de trabajo de formularios. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Si utiliza un dominio de empresa, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP, que Administración de usuarios sincroniza con la base de datos Administración de usuarios. Esto permite asignar una clave de calendario empresarial a un campo del directorio LDAP. Por ejemplo, si cada registro de usuario del directorio contiene un campo &quot;país&quot; y desea asignar calendarios comerciales basados en el país donde se encuentra el usuario, especifique el nombre del campo &quot;país&quot; en el campo Clave de calendario empresarial al especificar la configuración de usuario para el directorio. (Consulte [Configuración de directorios](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) A continuación, puede asignar las claves del calendario empresarial (los valores definidos para el campo &quot;país&quot; en el directorio LDAP) a los calendarios empresariales del flujo de trabajo de formularios. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. En el flujo de trabajo de Forms, defina un calendario para cada conjunto de usuarios que compartan los mismos días no laborables. (Consulte [Crear o actualizar un calendario empresarial](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. En el flujo de trabajo de Forms, asigne las claves del calendario empresarial o las pertenencias de grupo de cada calendario. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. En Workbench, el desarrollador de procesos elige si desea utilizar calendarios comerciales para recordatorios, plazos y escalaciones. (Consulte la [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

   Si el desarrollador de procesos decide utilizar calendarios comerciales, los formularios AEM Forms seleccionarán dinámicamente el calendario empresarial adecuado en función de la configuración de Administración de usuarios y las asignaciones de calendario empresarial definidas en la Consola de administración o, si no existe ninguna asignación, utilizarán el calendario predeterminado.

   Si el desarrollador de procesos no utiliza calendarios comerciales, el cálculo de fecha del evento trata cada día como un día hábil. Por ejemplo, se configura una fecha límite de tarea para que se produzca tres días después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. La fecha límite de la tarea es el domingo, aunque sea fin de semana.

## Crear o actualizar un calendario empresarial {#create-or-update-a-business-calendar}

Si su organización contiene diferentes conjuntos de usuarios con diferentes días no laborables, puede definir varios calendarios comerciales. También puede cambiar los calendarios existentes, incluido el calendario integrado predeterminado que se proporciona con los formularios AEM Forms.

>[!NOTE]
>
>* Si no crea un calendario empresarial, se utilizará el predeterminado.
>* Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Calendarios empresariales.
1. Para agregar un nuevo calendario empresarial, haga clic en ![bus_cal_plus](assets/bus_cal_plus.png). El texto *Nuevo calendario* aparece en la lista desplegable. Seleccione el texto y escriba otro nombre para el calendario.

   Para editar un calendario empresarial existente, selecciónelo en la lista desplegable.

1. En Días no laborables predeterminados, seleccione cualquier día no laborable semanal, como fines de semana.
1. [Opcional] Seleccione Usar horario laboral y especifique las horas de inicio y finalización de los días laborables.

   Si selecciona esta opción, un evento que se produce antes del intervalo de tiempo especificado se mueve al principio del intervalo de tiempo y un evento que se produce después de que el intervalo de tiempo se mueva a la hora de inicio del siguiente día laborable.

   Por ejemplo, considere una situación en la que a un usuario se le asigna una tarea a las 2 de la madrugada de un martes y el recordatorio de esa tarea se establece en dos días hábiles. Sin horario laboral, el recordatorio ocurriría a las 2:00 am del jueves. Si el horario laboral es de 8:00 a.m. a 5:00 p.m., el recordatorio se inserta a las 8:00 a.m. del jueves. Sin horario laboral, si se creó un evento de recordatorio a las 18:00 del martes, el recordatorio se produciría después del horario laboral del jueves. Con el horario laboral establecido de 8:00 a.m. a 5:00 p.m., el recordatorio se produciría a las 8:00 a.m. del viernes.

1. En el calendario de la izquierda, haga doble clic en cualquier otro día que no sea laborable, como los festivos. No se pueden seleccionar días del pasado. Los días no laborables que seleccione aparecerán en una lista a la derecha, con la fecha apareciendo dos veces en una línea. Seleccione la fecha de la izquierda para escribir el nombre o la descripción del día no laborable.

   Para quitar de la lista un día no laborable, haga clic en ![bus_cal_trash](assets/bus_cal_trash.png) al lado del día.

1. [Opcional] Si este calendario va a ser el predeterminado, seleccione Calendario predeterminado. El calendario predeterminado se utiliza cuando no existe ninguna otra asignación de calendario para los eventos asociados al usuario o no se especifica ningún calendario empresarial para el evento de temporizador o el servicio de espera. No puede eliminar el calendario predeterminado.
1. Cuando haya terminado de definir los días no laborables, seleccione Calendario habilitado para activarlo y, a continuación, haga clic en Guardar.

   Si está actualizando un calendario existente, la nueva versión surte efecto inmediatamente y se utiliza para todos los cálculos del calendario empresarial, incluso para las tareas que ya se están ejecutando.

   >[!NOTE]
   >
   >Si no habilita el calendario, se utilizará el predeterminado.

## Asignación de usuarios y grupos a un calendario empresarial {#mapping-users-and-groups-to-a-business-calendar}

Puede utilizar dos métodos para asociar un calendario empresarial a un usuario. Puede asignar calendarios comerciales a los usuarios en función de una clave de calendario empresarial o del grupo de directorios al que pertenezca el usuario. La ficha Asignación se utiliza para especificar el método que utilizarán los formularios AEM Forms y también para asignar las claves y los grupos del calendario empresarial a los calendarios empresariales. Para obtener más información sobre cómo asociar claves de calendario empresarial con usuarios, consulte [Configuración de varios calendarios empresariales](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Asociar calendarios comerciales con usuarios según las claves del calendario empresarial {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Calendarios empresariales y, a continuación, haga clic en la pestaña Asignación.
1. En la lista El sistema usará, seleccione la resolución de claves del calendario empresarial del administrador de usuarios.
1. Seleccione Mostrar clave de calendario empresarial del administrador de usuarios. Se muestra una lista que contiene un conjunto único de claves de calendario empresarial que se han definido en Administración de usuarios.

   Para los dominios locales e híbridos, la lista muestra los valores introducidos en el campo Clave del calendario empresarial en Administración de usuarios. En el caso de los dominios empresariales (LDAP), la lista muestra el conjunto único que devuelve el campo LDAP (por ejemplo, &quot;país&quot;) que se configuró en la configuración del dominio LDAP.

   Si el administrador de Administración de usuarios no ha definido ninguna clave de calendario empresarial, la lista estará vacía.

1. Seleccione un calendario para cada elemento de la lista Clave de calendario empresarial de mensajería unificada.
1. Haga clic en Guardar.

### Asociar calendarios de negocios con usuarios y grupos basados en grupos de servicios de directorio {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Calendarios empresariales y, a continuación, haga clic en la pestaña Asignación.
1. En la lista El sistema usará, seleccione los grupos definidos por el servidor de directorio.
1. En la ficha Asignación, seleccione Mostrar grupos de servicios de directorio. Se muestra una lista que contiene los grupos que se han definido en Administración de usuarios. (Consulte [Configuración de directorio](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >En Workbench, si ha configurado un servicio de usuario para utilizar calendarios comerciales y el servicio está asignado a un grupo, los formularios de AEM Forms utilizan las asignaciones de grupo especificadas aquí para resolver el calendario del grupo. Los formularios de AEM siempre utilizan asignaciones de grupos para resolver el calendario de los grupos, incluso cuando se utilizan claves de calendario empresarial para resolver el calendario de los usuarios. Si no se encuentra ninguna asignación de grupo, se utiliza el calendario empresarial predeterminado.

1. Para cada elemento de la lista Grupo de Servicios de Directorio, seleccione un Calendario.
1. Haga clic en Guardar.

## Exportar e importar calendarios comerciales {#exporting-and-importing-business-calendars}

Los formularios AEM Forms permiten exportar e importar calendarios empresariales como archivos XML. Puede utilizar esta función para mover calendarios de un sistema de ensayo a un sistema de producción.

>[!NOTE]
>
>Esta característica exporta e importa todos los calendarios comerciales definidos, incluido el calendario empresarial predeterminado proporcionado por los formularios AEM Forms. Un calendario empresarial importado con el mismo nombre que un calendario existente sobrescribe el calendario existente.

### Exportar calendarios comerciales {#export-business-calendars}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Calendarios empresariales.
1. Haga clic en Exportar y guarde el archivo XML.

### Importar calendarios comerciales {#import-business-calendars}

1. En la consola de administración, haga clic en Servicios > flujo de trabajo de formularios > Calendarios empresariales.
1. Haga clic en Importar.
1. Seleccione el archivo XML que contiene los calendarios comerciales exportados y haga clic en Abrir.

## Eliminar un calendario empresarial {#delete-a-business-calendar}

Puede quitar los calendarios comerciales que su organización ya no necesite. Si elimina un calendario empresarial que aún esté asignado a usuarios y grupos, se utilizará el calendario predeterminado.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Calendarios empresariales.
1. Seleccione el calendario.
1. Haga clic en Eliminar.
