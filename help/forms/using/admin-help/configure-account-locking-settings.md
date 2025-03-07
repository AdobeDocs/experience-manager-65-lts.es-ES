---
title: Configurar el bloqueo de cuentas
description: Utilice la opción Habilitar bloqueo de cuentas para bloquear las cuentas de usuario después de un número determinado de errores de autenticación consecutivos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e78860dc-9375-465c-b1fa-2a4827ca8dce
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 8%

---

# Configurar el bloqueo de cuentas {#configure-account-locking-settings}


>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Cuando agregue un dominio, especifique si desea habilitar el bloqueo de cuentas. Cuando se selecciona la opción Habilitar bloqueo de cuentas, las cuentas de usuario se bloquean después de un número determinado de errores de autenticación consecutivos. Después de un período de tiempo especificado, el usuario puede intentar autenticarse de nuevo. Esta función evita que los usuarios intenten varias combinaciones de credenciales para acceder al sistema.

Use la configuración de la página Administración de dominios para especificar el número máximo de errores de autenticación y el período de tiempo que las cuentas están bloqueadas. Esta configuración se aplica a todos los dominios que tienen habilitado el bloqueo de cuentas.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Administración de dominios]**.
1. En el cuadro Máximo de errores de autenticación consecutivos, escriba el número de veces consecutivas que un usuario puede intentar iniciar sesión sin éxito antes de que se bloquee su cuenta. El valor predeterminado es 20.
1. En el cuadro Desbloquear la cuenta después de (minutos), escriba el número de minutos que la cuenta de usuario está bloqueada. Después del número de minutos especificado, el usuario puede intentar iniciar sesión de nuevo. El valor predeterminado es 30.
1. Haga clic en **[!UICONTROL Guardar]**.
