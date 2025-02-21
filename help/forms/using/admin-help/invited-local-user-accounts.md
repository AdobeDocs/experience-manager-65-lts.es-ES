---
title: Administrar cuentas de usuario invitadas y locales
description: Con Document Security, puede buscar, ver, editar, bloquear, desbloquear y eliminar cuentas de usuario invitadas y locales.
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 1%

---

# Administrar cuentas de usuario invitadas y locales {#managing-invited-and-local-user-accounts}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Utilice la página Usuarios invitados y locales para administrar los usuarios invitados y locales. Esta página solo se muestra si se cumplen los siguientes requisitos:

* Usted es un administrador al que se le asigna la función Document Security Administrar usuarios invitados y locales y la función Usuario de la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* El registro de usuarios invitados está habilitado. (Consulte [Configuración del registro de usuarios invitados](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

La página Usuarios invitados y locales contiene dos fichas que puede utilizar para buscar, ver, editar, bloquear, desbloquear y eliminar cuentas de usuario invitadas y locales.

También puede enviar manualmente correos electrónicos de registro a los usuarios invitados. Puede que desee hacerlo, por ejemplo, si finaliza el periodo de registro en el que se autoriza el correo electrónico y el usuario no puede utilizar la URL para registrarse. En este caso, puede reenviar un correo electrónico de registro al usuario invitado. Cuando el usuario invitado se registra y activa la cuenta, se convierte en un usuario local.

>[!NOTE]
>
>Los usuarios invitados también se pueden agregar directamente a través del directorio LDAP al que hace referencia la seguridad de los documentos, o cuando un usuario o administrador invita a un nuevo usuario a crear o editar una directiva, iniciando así un correo electrónico de invitación de registro. Los usuarios pueden agregar nuevos usuarios invitados a las directivas si activa la opción Habilitar el registro de usuarios invitados en la página Registro de usuarios invitados.

## Añadir un usuario invitado {#add-an-invited-user}

Puede agregar una o más cuentas de usuario invitadas a Document Security a la vez. Para agregar una cuenta de usuario invitada, necesita la dirección de correo electrónico del usuario. Cuando agrega un usuario, Document Security envía un correo electrónico de registro invitando al usuario a registrarse.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en Invitar nuevo usuario.
1. Escriba las direcciones de correo electrónico de los usuarios que desea invitar. Escriba varias direcciones en una línea, separadas por una coma.

   El mensaje que creó al habilitar el registro de usuarios invitados se envía a los usuarios. (Consulte [Configuración del registro de usuarios invitados](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Haga clic en Aceptar.

## Ver información sobre un usuario local {#view-information-about-a-local-user}

Puede ver información sobre los usuarios locales, incluidos el nombre, la dirección de correo electrónico, la organización, el estado de registro y el dominio.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en Invitar nuevo usuario.
1. Haga clic en la pestaña Usuarios locales y, en la página Administrar usuarios locales, haga clic en la dirección de correo electrónico del usuario que desee ver.

   Se muestran los detalles del usuario, y puede restablecer la contraseña del usuario y desactivar la cuenta.

## Envío de un correo electrónico a un usuario externo no registrado {#send-an-email-to-an-unregistered-external-user}

Cuando agrega un usuario invitado, Document Security envía automáticamente al usuario una solicitud de registro por correo electrónico. También puede generar manualmente un correo electrónico de registro para enviarlo a un usuario invitado que aún no se haya registrado. Puede que desee hacer esto, por ejemplo, para enviar una nueva invitación si caduca el correo electrónico de registro de un usuario invitado.

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales.
1. En la lista de usuarios, active la casilla de verificación de cada usuario al que enviar un correo electrónico de registro y, a continuación, haga clic en Reenviar correo electrónico de invitación.
1. Revise la lista de usuarios seleccionados y haga clic en Aceptar.

## Restablecer la contraseña de un usuario local {#reset-a-local-user-password}

Puede restablecer las contraseñas de los usuarios invitados activados que se registraron con Document Security pero que olvidaron su contraseña. Al restablecer una contraseña, se genera un correo electrónico que contiene una contraseña nueva y temporal para el usuario.

Cuando habilitó el proceso de registro de usuarios invitados, creó un mensaje de correo electrónico que se enviará a los usuarios pidiéndoles que restablezcan sus contraseñas. (Consulte [Configuración del registro de usuarios invitados](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales y, a continuación, haga clic en la pestaña Usuarios locales.
1. En la lista de usuarios, seleccione el usuario adecuado.
1. En la página Administrar usuario local, haga clic en Restablecer contraseña y en Aceptar. Se envía al usuario un correo electrónico para restablecer la contraseña que contiene la nueva contraseña.

## Habilitar o deshabilitar una cuenta de usuario {#enable-or-disable-a-user-account}

Puede deshabilitar las cuentas de usuario locales para restringir temporalmente el inicio de sesión de un usuario a Document Security. Al deshabilitar la cuenta, el usuario no puede utilizar documentos protegidos por directivas ni crear ni aplicar directivas.

Puede habilitar una cuenta de usuario local que esté deshabilitada actualmente. No puede habilitar una cuenta de usuario invitada que aparezca como registrada. El estado registrado indica que el usuario invitado está registrado, pero aún no ha activado la cuenta mediante el vínculo del correo electrónico de activación.

**Restringir una cuenta de usuario**

1. En Administration Console, haga clic en Servicios > Document Security > Usuarios invitados y locales y, a continuación, haga clic en la pestaña Usuarios locales.
1. En la lista de usuarios, seleccione el usuario adecuado.
1. En la página Detalles del usuario local, haga clic en Deshabilitar cuenta.

**Restablecer una cuenta de usuario**

1. Haga clic en Usuarios invitados y locales y, a continuación, en la ficha Usuarios locales.
1. En la lista de usuarios, seleccione el usuario adecuado.
1. En la página Detalles del usuario local, haga clic en Habilitar cuenta.

## Eliminar una cuenta de usuario invitada {#remove-an-invited-user-account}

Puede eliminar cuentas de usuario invitadas de Document Security. Es posible que desee eliminar una cuenta, por ejemplo, cuando un usuario cambia su información personal de cuenta de correo electrónico.

Si elimina una cuenta de usuario, sólo usted u otro administrador podrán restablecer la cuenta seleccionando la opción Agregar usuario invitado en la página Usuarios invitados. Los usuarios no pueden agregar la cuenta de usuario eliminada a una directiva y no se puede iniciar ningún proceso de invitación con ese método.

>[!NOTE]
>
>Los usuarios invitados que se eliminaron a través de la interfaz de administración de usuarios de formularios AEM Forms no pueden volver a ser invitados hasta que se hayan eliminado de nuevo mediante el siguiente procedimiento.

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales y, a continuación, haga clic en la pestaña Usuarios invitados.
1. Active la casilla de verificación situada junto a uno o varios usuarios, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Buscar una cuenta de usuario invitada {#search-for-an-invited-user-account}

Puede buscar cuentas de usuario invitadas utilizando una dirección de correo electrónico.

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales.
1. En el cuadro Buscar correo electrónico, escriba la dirección de correo electrónico del usuario y, a continuación, haga clic en Buscar.

## Buscar una cuenta de usuario local {#search-for-a-local-user-account}

Puede buscar un usuario local utilizando la dirección de correo electrónico o el nombre y dominio del usuario.

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales y, a continuación, haga clic en la pestaña Usuarios locales.
1. Escriba los criterios de búsqueda en el cuadro Buscar, seleccione Nombre o Correo electrónico y, a continuación, haga clic en Buscar.

## Eliminación de una cuenta de usuario local {#remove-a-local-user-account}

Puede eliminar cuentas de usuario locales de Document Security. Es posible que desee eliminar cuentas, por ejemplo, cuando los usuarios cambien su información personal de cuenta de correo electrónico.

1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales y, a continuación, haga clic en la pestaña Usuarios locales.
1. Active la casilla de verificación situada junto a uno o varios usuarios, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Ordenar la lista de usuarios {#sort-the-user-list}

Puede encontrar usuarios más fácilmente ordenando la lista de usuarios por encabezado de columna. Los iconos de triángulo situados junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar:

* Un triángulo que señala hacia arriba indica un orden ascendente.
* Un triángulo que señala hacia abajo indica un orden descendente.

   1. En la consola de administración, haga clic en Servicios > Document Security > Usuarios invitados y locales.
   1. Para ordenar los usuarios invitados, haga clic en la pestaña Usuarios invitados y seleccione el encabezado de columna correspondiente.
   1. Para ordenar los usuarios locales, haga clic en la ficha Usuarios locales y seleccione el encabezado de columna correspondiente.
