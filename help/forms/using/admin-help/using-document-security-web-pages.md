---
title: Usar las páginas web de seguridad de los documentos
description: Descubra cómo puede iniciar sesión, navegar y utilizar las páginas web de Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 1%

---

# Usar las páginas web de seguridad de los documentos {#using-the-document-security-webpages}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los usuarios y administradores utilizan las páginas web de Document Security para crear y administrar directivas, administrar documentos protegidos por directivas y supervisar eventos asociados a documentos protegidos por directivas. Los administradores también utilizan las páginas web para crear conjuntos de directivas y designar coordinadores de conjuntos de directivas, configurar la configuración predeterminada de Document Security, administrar el registro de usuarios y las cuentas invitados, y supervisar y administrar eventos relacionados con el servidor, las directivas, los usuarios y los documentos.

>[!NOTE]
>
>También puede iniciar sesión en Document Security a través de Acrobat y otras aplicaciones cliente con su cuenta de inicio de sesión de usuario. (Consulte [Configuración del acceso a Document Security desde aplicaciones cliente](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)).

Para abrir las páginas web, necesita un explorador y la dirección URL y la información de inicio de sesión para Document Security. La dirección URL de los usuarios es diferente de la de los administradores.

Debido a que Document Security hace referencia a los directorios existentes de su organización para obtener información del usuario, la información de inicio de sesión de Document Security puede ser la misma que se utiliza para iniciar sesión en la red y en otras aplicaciones. Consulte al administrador del sistema o al administrador para obtener información sobre la cuenta.

Para iniciar sesión como administrador, debe tener asignada la función de administrador. Puede utilizar la cuenta de superadministrador predeterminada que se crea durante el proceso de instalación.

## Inicie sesión en las páginas web {#log-in-to-the-web-pages}

Para iniciar sesión en las páginas web mediante un explorador, necesita la URL de Document Security y una cuenta de. La dirección URL de los usuarios es diferente de la de los administradores. Los administradores también pueden iniciar sesión en las páginas de usuario para crear directivas.

Si tiene acceso a más de una instalación de Document Security, necesita la URL para la instancia de Document Security a la que desea acceder. Consulte al administrador si no dispone de esta información. La dirección URL predeterminada para las páginas de usuario es `https://[host]:[port]/edc`. Es posible que en algunos casos no se requiera el número de puerto. Solicite más información a su administrador.

La dirección URL predeterminada para los administradores es `https://[host]:[port]/adminui`.

Para los administradores, se crea una cuenta de superadministrador predeterminada durante la instalación. Puede utilizar esta cuenta para iniciar sesión cuando Document Security se instale por primera vez.

>[!NOTE]
>
>También puede acceder a las páginas web desde Acrobat y otras aplicaciones cliente. Consulte la Ayuda de Acrobat o la Ayuda de las extensiones de Acrobat Reader DC correspondientes para obtener más información.

1. Escriba la dirección URL en el explorador:

   URL de seguridad de documento: `https://[host]:[port]/edc`

   o la URL de la consola de administración: `https://[host]:[port]/adminui`

1. En la ventana de inicio de sesión, escriba su nombre de usuario y contraseña y haga clic en Aceptar.
1. En la consola de administración, haga clic en Servicios > Document Security.

>[!NOTE]
>
>Al trabajar con las páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Adelante porque esta acción puede causar problemas no deseados de captura de datos y visualización de datos.

## Navegación por las páginas web {#navigating-the-web-pages}

Cuando inicie sesión en las páginas web del usuario, verá vínculos a las páginas de usuario de Directivas, Documentos y Eventos.

Al iniciar sesión en la consola de administración y navegar a la página principal de Document Security, también puede ver uno o dos vínculos adicionales, uno para la página Configuración y otro para la página Usuarios invitados y locales. La página Usuarios invitados y locales solo se muestra si está activado el registro de usuarios invitados.

Utilice estos vínculos para acceder a las distintas páginas, donde puede crear y administrar directivas y documentos protegidos por directivas.

**Mostrar una página**

1. Haga clic en el nombre de la página; por ejemplo, haga clic en Políticas.

**Volver a la página anterior**

1. Haga clic en el vínculo de navegación en la parte superior de la página de la página a la que desea volver.

**Actualizar la lista de datos en una página**

1. En la página principal, haga clic en el vínculo a la página que desee actualizar.

>[!NOTE]
>
>Cuando trabaje con páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Adelante, ya que esta acción puede causar problemas no deseados de captura de datos y visualización de datos.

## Configuración del acceso a Document Security desde aplicaciones cliente {#setting-up-access-to-document-security-from-client-applications}

Las aplicaciones cliente deben configurarse para conectarse a Document Security para proteger documentos, abrir documentos protegidos por directivas y conectarse a las páginas web de Document Security. Consulte la *Ayuda de Acrobat* o la *Ayuda de RightsManagementExtension* adecuada para obtener información sobre cómo configurar la conexión en la aplicación cliente.

Se accede a la seguridad de los documentos a través de Secure Sockets Layer (SSL). Instale el certificado del sitio web en el almacén de certificados para poder acceder a la seguridad de los documentos a través de las aplicaciones cliente.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Estas instrucciones son específicas de Internet Explorer, pero puede instalar el certificado utilizando cualquier explorador web admitido. Para obtener más información, consulte la Ayuda del explorador.

**Instale el certificado de servidor mediante Internet Explorer**

1. Abra el explorador web y escriba la dirección URL base de Document Security en el cuadro Dirección. Por ejemplo, escriba `https://[host]:[port]`. Aparecerá un cuadro de diálogo Alerta de seguridad.
1. Haga clic en Ver certificado y, a continuación, haga clic en Instalar certificado y seleccione los valores predeterminados para la instalación. El certificado debe instalarse en las entidades emisoras de certificados raíz de confianza.
1. Cierre la sesión del explorador.
1. Abra otra ventana del explorador y escriba la misma dirección URL en el cuadro Dirección. No debería aparecer ningún cuadro de diálogo de alerta de seguridad. Esta prueba confirma que el certificado está correctamente instalado.

## Cerrar sesión en las páginas web {#log-out-of-the-web-pages}

Cierre la sesión cuando termine de usar las páginas web para poder usar el explorador web con seguridad para otros fines. Según la configuración de Document Security, es posible que tenga que cerrar el explorador para cerrar sesión por completo.

1. En la esquina superior derecha de la página, haga clic en Cerrar sesión.
1. Si aparece un mensaje en la página Cerrar sesión, cierre la ventana del explorador para cerrar la sesión por completo. De lo contrario, puede continuar utilizando el explorador para otros fines.
