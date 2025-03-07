---
title: Configurar atributos de sistema avanzados
description: Utilice la página Configurar Atributos Avanzados del Sistema para modificar ciertas opciones del archivo de configuración sin necesidad de exportar, editar ni importar el archivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f1a68461-c66a-4ea4-902b-644c620ea3f6
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 2%

---

# Configurar atributos de sistema avanzados {#configure-advanced-system-attributes}

Utilice la página Configurar Atributos Avanzados del Sistema para modificar ciertas opciones del archivo de configuración sin necesidad de exportar, editar ni importar el archivo. (Consulte [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema]**.
1. (Opcional) Cambie cualquiera de los siguientes atributos de sesión:

   **Límite de tiempo de espera de sesión (minutos):** Cantidad de tiempo, en minutos, antes de que un usuario cierre sesión automáticamente en el sistema. De forma predeterminada, los componentes de formularios AEM, como Workbench, agotan el tiempo de espera después de dos horas, independientemente de la actividad o la inactividad, y el usuario debe iniciar sesión de nuevo. Los valores válidos son de `1` a `1440`. El valor predeterminado es `120` (2 horas). Esta opción actualiza la clave de entrada `SAML/Producer/assertionValidityInMinutes` en el archivo de configuración.

   >[!NOTE]
   >
   >No debe establecer el límite de tiempo de espera de sesión por debajo de 10 minutos, ya que es posible que el sistema no se comporte correctamente. El valor recomendado es 10-120 (minutos).

   **Umbral de aserción (segundos):** Un tiempo de búfer para compensar los retrasos debido a las diferencias de tiempo del sistema entre el servidor de aplicaciones de formularios de AEM en un clúster. Los formularios AEM antedatan el tiempo de inicio de sesión de un usuario en la cantidad de tiempo (en segundos) especificada en esta propiedad. Los valores válidos son de `0` a `3600`. El valor predeterminado es `60`. Esta opción actualiza la clave de entrada `SAML/Producer/assertionThresholdInSeconds` en el archivo de configuración.

   **Máximo de renovaciones permitidas de una afirmación:** El número máximo de veces que la sesión de un usuario se puede renovar de forma transparente sin necesidad de iniciar sesión. Los valores válidos son de `0` a `9999`. Un valor de `0` significa que no se renuevan las aserciones. El valor predeterminado es 10. Esta opción actualiza la clave de entrada `SAML/Producer/maxAssertionRenewalCount` en el archivo de configuración.

1. (Opcional) Cambie cualquiera de los siguientes atributos de sincronización de directorios:

   **Registro de estadísticas de sincronización:** Especifica si Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización. (Consulte [Habilitar o deshabilitar el registro detallado durante la sincronización](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Expresión Cron de finalizador de sincronización:** El intervalo en el que Administración de usuarios reintenta las sincronizaciones con errores. (Consulte [Configurar la opción de reintento de sincronización de directorios](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)).

   **Tiempo De Espera De Bloqueo De Trabajo De Clúster En Minutos:** Utilizado En Entornos En Clúster. Si falla la sincronización en un nodo y no se libera el bloqueo del clúster, este valor especifica el número de minutos que otro nodo espera antes de adquirir el bloqueo de forma forzada. El valor predeterminado es `15` minutos. Los valores válidos son de `1` a `1440` minutos.

1. (Opcional) Cambie los siguientes atributos y haga clic en **[!UICONTROL Aceptar]**:

   **Auditoría de eventos del administrador de usuarios:** Seleccione esta opción para habilitar la auditoría de los eventos de sincronización de directorios y de los eventos de autenticación como éxito, error y bloqueo. De forma predeterminada, esta opción no está seleccionada a menos que haya instalado un componente que requiera auditoría, como Rights Management. Esta opción actualiza la clave de entrada `APSAuditService` en el archivo de configuración.

   **Creación automática de grupo dinámico:** Permite la creación automática de grupos dinámicos basados en dominios de correo electrónico. (Consulte [Crear un grupo dinámico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

También puede volver a la configuración original de Administración de usuarios haciendo clic en Recargar.
