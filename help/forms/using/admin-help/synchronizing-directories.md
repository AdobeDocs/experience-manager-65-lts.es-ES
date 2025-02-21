---
title: Sincronizar directorios
description: Obtenga información sobre cómo sincronizar la base de datos de administración de usuarios con los cambios en los servidores de directorio de origen mediante la sincronización manual o programada.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6352ade0206afc92e97c7ee0c4344a87b8b2cc83
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---

# Sincronizar directorios {#synchronizing-directories}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Para sincronizar dominios, puede elegir realizar una sincronización manual o programada. Una *sincronización manual* sincroniza los dominios seleccionados. Una *sincronización programada* sincroniza todos los dominios.

La sincronización de directorios se utiliza para extraer detalles de los servidores de directorios especificados en la configuración de directorios de la base de datos de Administración de usuarios. Posteriormente, también puede realizar una sincronización manual si se producen cambios o actualizaciones en los servidores de directorios. Por ejemplo, puede realizar una sincronización manual si se agregan usuarios y grupos o si se realizan cambios en la cuenta de un usuario.

También puede establecer una programación de sincronización diaria para sincronizar automáticamente la base de datos de administración de usuarios con cambios o actualizaciones en los servidores de directorio de origen. Sin embargo, este proceso utiliza recursos de red y de servidor. Elija períodos de tiempo de bajo uso y evite programar sincronizaciones innecesarias que atan los recursos del sistema y de la red. Para minimizar las sincronizaciones innecesarias, utilice la opción de sincronización inmediata en su lugar.

También puede especificar si desea insertar información de usuarios y grupos en Adobe LiveCycle Content Services 9 (obsoleto) al sincronizar dominios.

>[!NOTE]
>
>No cree varios usuarios y grupos locales mientras la sincronización de directorios LDAP esté en curso. Si se intenta este proceso, pueden producirse errores.

>[!NOTE]
>
>Si se interrumpe el proceso de sincronización de dominios (por ejemplo, el servidor de aplicaciones se apaga durante el proceso), espere un poco antes de intentar sincronizar el dominio. Para evaluar el estado de la sincronización, observe el estado. Si Administración de usuarios adquirió un bloqueo antes del apagado, espere 10 minutos a que se libere el bloqueo después de reiniciar el servidor. Si el estado de sincronización es &quot;En curso&quot; pero la sincronización se interrumpe o se detiene, Administración de usuarios reintentará la sincronización pasados 3 minutos. Tras tres intentos fallidos, Administración de usuarios declara un error la sincronización y libera el bloqueo.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (Obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento del ciclo de vida del producto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Habilitar sincronización de directorios delta {#enable-delta-directory-synchronization}

La sincronización de directorios Delta mejora la eficacia de la sincronización de directorios. Cuando la sincronización de directorios delta está habilitada, Administración de usuarios sincroniza sólo los usuarios y grupos que se han agregado o actualizado desde la última sincronización.

Administración de usuarios realiza los siguientes pasos cuando está habilitada la sincronización de directorios delta:

* Recupere todos los usuarios de los servidores de directorios, pero actualice la base de datos de administración de usuarios con solo los usuarios cuya marca de tiempo haya cambiado.
* Recupere todos los grupos, pero actualice la base de datos de administración de usuarios con solo los grupos cuya marca de tiempo haya cambiado.
* Recupere miembros del grupo solo para los grupos cuyas marcas de tiempo hayan cambiado y actualice la base de datos de administración de usuarios con esa información.

>[!NOTE]
>
>* Los usuarios y grupos que se eliminaron del directorio no se eliminarán de la base de datos de Administración de usuarios hasta que realice una sincronización de directorios completa.
>* Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. En Sincronización delta, active la casilla de verificación y haga clic en Guardar.
1. Edite la configuración de directorio para cada uno de los dominios de empresa que utilizarán la función de sincronización de directorios delta. En las páginas Configuración de usuario y Configuración de grupo, busque la opción Modificar marca de tiempo y escriba `modify TimeStamp` como valor. Para obtener más información sobre cómo editar dominios empresariales, consulte [Editar y convertir dominios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Habilitar o deshabilitar el registro detallado durante la sincronización {#enable-or-disable-detailed-logging-during-synchronization}

De forma predeterminada, Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Registro de estadísticas de sincronización, anule la selección de la casilla de verificación para deshabilitar el registro detallado o selecciónelo para habilitar el registro y, a continuación, haga clic en Guardar.

## Configure la opción de reintento de sincronización de directorios {#configure-the-directory-synchronization-retry-option}

Puede configurar Administración de usuarios para que compruebe periódicamente si hay intentos de sincronización de directorios fallidos. A continuación, Administración de usuarios intenta completar las sincronizaciones con errores.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Expresión cron de finalizador de sincronización, introduzca una expresión cron que represente el intervalo en el que Administración de usuarios reintenta las sincronizaciones fallidas. El uso de expresiones cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

   El valor predeterminado es 0 0/13 &amp;ast; ? &amp;ast; , lo que significa que la comprobación se realiza cada 13 minutos.

## Sincronizar directorios manualmente {#manually-synchronize-directories}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. (Opcional) Para insertar información de usuarios y grupos en Content Services (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento principal externos registrados. Esta opción también se aplica cuando se agregan nuevos usuarios y grupos a través de la página Usuarios y grupos.
1. Seleccione la casilla de verificación de cada dominio de empresa para sincronizar y haga clic en Sincronizar ahora.

   Si selecciona varios dominios, la sincronización de dominios para todos los dominios se puede ejecutar al mismo tiempo. Sin embargo, si selecciona los dominios por separado, solo se puede ejecutar una sincronización de dominios a la vez.

## Programar sincronización de directorios {#schedule-directory-synchronization}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Programar sincronización:

   * Para habilitar la sincronización automática diariamente, en Planificador, seleccione Ocurre. Seleccione Cada día de la lista y escriba la hora en formato de 24 horas en el cuadro correspondiente. Al guardar la configuración, este valor se convierte en una expresión cron, que se muestra en el cuadro Expresión cron.
   * Para programar la sincronización en un día concreto de la semana o del mes, o en un mes concreto, seleccione Cron Expression y escriba la expresión adecuada en el cuadro. Por ejemplo, sincronícelo a la 1:30 a.m. del último viernes del mes.

El uso de expresiones cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

* Para desactivar la sincronización automática, seleccione Ocurre y Nunca en la lista.
* (Opcional) Para insertar información de usuarios y grupos en Content Services (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento principal externos registrados. Esta opción también se aplica cuando se agregan nuevos usuarios y grupos a través de la página Usuarios y grupos.
* Haga clic en Guardar.

## Detener todas las sincronizaciones de directorios en curso {#stop-all-directory-synchronizations-currently-in-progress}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Anular. Este botón sólo se muestra mientras se está realizando una sincronización de directorios.
