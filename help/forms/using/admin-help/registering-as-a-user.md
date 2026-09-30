---
title: Registrarse como usuario
description: Descubra cómo puede utilizar documentos protegidos por directivas que reciba de un usuario de Document Security, incluso si es externo a la organización del usuario.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 60307c55-50b2-4f23-bc46-58732fee19fc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 7%
---
# Registrarse como usuario {#registering-as-a-user}

Puede utilizar documentos protegidos por directivas que reciba de un usuario de Document Security, incluso si es externo a la organización del usuario. Para utilizar un documento protegido por una directiva, debe registrarse en Document Security. Si no se le ha invitado anteriormente a registrarse, Document Security inicia el proceso de registro cuando se producen estos eventos:

* Un usuario de Document Security que desea enviarle un documento protegido por una directiva le agrega a una directiva.
* Un administrador de Document Security crea una cuenta para usted.

  Después de registrarse y activar la cuenta, puede utilizar documentos protegidos por directivas que esté autorizado a utilizar mediante una directiva. Si el administrador de Document Security habilita estas funciones para usuarios invitados, es posible que tenga permiso para realizar estas tareas:

* Proteger documentos mediante directivas de seguridad de documentos.
* Cree sus propias directivas de usuario que pueda aplicar a sus documentos.
* Invitar a otros usuarios externos a utilizar un documento protegido por una directiva agregándolos a la directiva.

  Además, cuando se registra, no es necesario registrarse de nuevo para utilizar otros documentos protegidos por políticas. Su cuenta permanece activa hasta que un administrador de directivas la deshabilite o elimine.

>[!NOTE]
>
>Si recibe un documento protegido por una directiva pero no recibe una invitación por correo electrónico de registro, póngase en contacto con la persona que le envió el documento para obtener más información.

## Registrarse como usuario invitado {#register-as-an-invited-user}

Si es un usuario invitado y recibe un mensaje de registro por correo electrónico de Document Security, puede registrarse utilizando la URL del mensaje para abrir la página de registro en línea. Después de registrarse, recibirá un segundo aviso sobre la activación de su cuenta.

1. Abra el correo electrónico de registro de Document Security. La dirección URL que contiene el mensaje es un vínculo a la página de registro de usuarios externos en Document Security.
1. Haga clic en la dirección URL o cópiela y péguela en el explorador. Se muestra la página Registro de usuarios externos.
1. Escriba su nombre, número de teléfono, dirección, organización y contraseña en los cuadros correspondientes y, a continuación, vuelva a escribir la contraseña en el cuadro Confirmar contraseña. La contraseña puede ser cualquier combinación de ocho caracteres.
1. Haga clic en Guardar. Aparece un mensaje de agradecimiento que le informa de que debe buscar un mensaje de correo electrónico de activación en su correo electrónico. Ahora activa tu cuenta para finalizar el proceso de registro.

## Activar la cuenta de usuario invitada {#activate-your-invited-user-account}

Después de registrarse, Document Security le enviará un correo electrónico de activación. Active la cuenta utilizando la dirección URL del mensaje. A continuación, puede iniciar sesión en Document Security para utilizar documentos protegidos por directivas a los que tenga acceso. Según las funciones que el administrador habilite para los usuarios externos, puede tener permiso para crear directivas, aplicar directivas a documentos y agregar otros usuarios externos a las directivas.

Su cuenta permanece activa hasta que el administrador la desactiva o elimina.

1. Abra el correo electrónico de confirmación de registro de Document Security.
1. Haga clic en la dirección URL que aparece en el mensaje. Se muestra la página de activación de Document Security.
1. Haga clic en la palabra Here para ir a la página de inicio de sesión.
1. En el cuadro Nombre de usuario, escriba la dirección de correo electrónico en la que se registró con Document Security. Esta dirección de correo electrónico es el nombre de usuario predeterminado de Document Security.
1. En el cuadro Contraseña, escriba la contraseña que creó al registrarse y, a continuación, haga clic en Iniciar sesión.

## Restablecer la contraseña {#reset-your-password}

Si olvida su contraseña, el administrador de políticas puede restablecerla por usted. El restablecimiento de una contraseña genera un correo electrónico que le invita a iniciar sesión con una contraseña temporal. A continuación, puede crear otra contraseña.

Para obtener información sobre cómo ponerse en contacto con un administrador de Document Security para obtener una nueva contraseña, consulte el aviso de activación por correo electrónico u otros avisos de la organización que le invitó a registrarse.

1. Notificar al administrador de directivas que necesita una nueva contraseña.
1. Cuando reciba el correo electrónico sobre la contraseña de Document Security, ábrala y obtenga la nueva contraseña temporal.
1. Inicie sesión en Document Security con la nueva contraseña temporal.
1. Haga clic en Opciones en la esquina superior derecha de la página. Se muestra la página Usuarios externos.
1. Seleccione Cambiar contraseña y escriba la contraseña temporal en el cuadro Contraseña anterior.
1. En el cuadro Nueva contraseña, escriba una nueva contraseña y, a continuación, vuelva a escribirla en el cuadro Confirmar contraseña.
