---
title: Configurar una impresora de red PDFG (solo Windows)
description: Aprenda a configurar una impresora de red PDFG ( solo Windows )
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 6e9c42d9-fb1d-432b-95b9-6e21706b2a3e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# Configurar una impresora de red PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La impresora de red PDFG permite a los usuarios generar un documento de PDF desde cualquier aplicación que admita la impresión. Una vez que un usuario instala la impresora de red PDFG, aparece una nueva impresora denominada *generador de PDF* en la sección Impresoras del Panel de control de Campaign de Windows. Si ya existe una impresora con el mismo nombre, se pide al usuario que proporcione otro nombre.

La impresión en esta impresora desde cualquier aplicación envía el documento (en formato PostScript) a PDF Generator, que convierte el archivo de PostScript en PDF. Según la configuración de PDF Generator, envía el documento de PDF al usuario como datos adjuntos a un mensaje de correo electrónico, reenvía el documento de PDF a un servicio o proceso de formularios AEM especificado o realiza ambas acciones.

Se requieren los siguientes pasos para configurar una impresora de red PDFG:

1. Configure las opciones de correo electrónico. (Consulte [Configurar opciones de correo electrónico para la impresora de red PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)).
1. En la consola de administración, configure la impresora de red PDFG. (Consulte [Configurar la configuración de la impresora de red PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)).
1. Asegúrese de que los usuarios estén configurados con una dirección de correo electrónico válida en la base de datos de formularios de AEM y asigne PDFGUserPermission a cada usuario. <!-- Fix broken link See Setting up and organizing users -->
1. Asegúrese de que JRE6 de 32 bits esté instalado en los equipos de los usuarios.
1. Instale la impresora en los equipos de los usuarios. (Consulte [Instalar la impresora de red PDFG en el equipo de un usuario](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Configurar opciones de correo electrónico para la impresora de red PDFG {#configure-email-settings-for-pdfg-network-printer}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en provider.email_sendmail_service, especifique la configuración de SMTP y haga clic en Guardar.

## Configure las opciones de la impresora de red PDFG {#configure-the-pdfg-network-printer-settings}

1. En la consola de administración, haga clic en Servicios > PDF Generator > Impresora de red PDFG
1. En las listas Configuración de Adobe PDF y Configuración de seguridad, seleccione las opciones que desea aplicar al PDF generado. Para obtener detalles sobre esta configuración, consulte [Configuración de Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) y [Configuración de seguridad](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Para devolver los PDF convertidos a los usuarios, seleccione la opción Enviar por correo electrónico el archivo PDF convertido de nuevo al usuario y especifique la siguiente información:

   * La dirección de correo electrónico que se utilizará para enviar archivos PDF a los usuarios
   * Asunto del mensaje de correo electrónico
   * El encabezado, el cuerpo y el pie de página del mensaje de correo electrónico. En el mensaje de correo electrónico, &lt;receiverName> se reemplaza por el nombre completo del usuario que imprimió el documento.

1. Para enviar los PDF convertidos a un servicio o proceso de formularios de AEM, seleccione la opción Reenviar el PDF convertido al servicio o proceso de formularios de AEM especificado y especifique la siguiente información:

   * Nombre del servicio que se va a invocar
   * Nombre de la operación del servicio que se va a invocar
   * Nombre del parámetro de entrada, tal como se especifica en el archivo component.xml del servicio o proceso. El documento de PDF se utiliza como valor para ese parámetro de entrada.

1. Haga clic en Guardar.

Si desea volver al texto de correo electrónico original predeterminado, haga clic en Restaurar contenido del correo electrónico.

## Instalar la impresora de red PDFG en el equipo de un usuario {#install-pdfg-network-printer-on-a-user-s-computer}

Los usuarios que tengan la función Administrador de PDFG o Usuario de PDFG pueden instalar una impresora de red PDFG. Debe tener un JDK de 32 bits instalado en el equipo.

1. (Administradores de PDFG) En la consola de administración, haga clic en Servicios > PDF Generator > Impresora de red PDFG.

   (Usuarios de PDFG) Vaya a `http(s)://[host]:'port'/pdfgui` y haga clic en el vínculo en Instalación de impresora de red de PDFG.

1. En Instalación de impresora de red PDFG, haga clic en el vínculo. Cuando se le pida información de cuenta de usuario, especifique el nombre de usuario y la contraseña que utilizó en el paso 1 para iniciar sesión. Aparece un mensaje que indica que la impresora se ha instalado correctamente.

   ***nota **: Si la contraseña del usuario cambia, los usuarios deben volver a instalar la impresora de red PDFG en sus equipos. No puede actualizar la contraseña desde la consola de administración.*

1. Haga clic en Aceptar.
