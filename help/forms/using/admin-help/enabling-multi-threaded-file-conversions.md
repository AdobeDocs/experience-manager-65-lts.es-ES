---
title: Activar conversiones de archivos con varios subprocesos
description: Obtenga información sobre cómo habilitar las conversiones de archivos con varios subprocesos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# Activar conversiones de archivos con varios subprocesos {#enabling-multi-threaded-file-conversions}

PDF Generator permite habilitar conversiones de archivos con varios procesos para determinados tipos de archivos. La conversión de archivos con varios subprocesos mejora el rendimiento de PDF Generator al permitirle realizar varias conversiones al mismo tiempo.

## Habilitar conversiones de archivos con varios subprocesos para documentos de OpenOffice, Word y PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

De forma predeterminada, PDF Generator solo puede convertir un documento de OpenOffice, Microsoft® Word o PowerPoint a la vez. Si habilita las conversiones multiproceso, PDF Generator puede convertir más de un documento simultáneamente. PDF Generator inicia varias instancias de OpenOffice o PDFMaker (utilizadas para realizar las conversiones de Word y PowerPoint).

>[!NOTE]
>
>Las conversiones de archivos con varios subprocesos no son compatibles con Microsoft® Word 2003 y PowerPoint 2003. Para habilitar las conversiones de archivos multiproceso, actualice a Microsoft® Word 2007 y PowerPoint 2007 o Microsoft® Word 2010 y PowerPoint 2010.

>[!NOTE]
>
>Las conversiones de archivos con varios subprocesos no son compatibles con Microsoft® Excel, Microsoft® Visio, Microsoft® Project o Microsoft® Publisher.

Cada instancia de OpenOffice o PDFMaker se inicia con una cuenta de usuario independiente. Cada cuenta de usuario que agregue debe ser un usuario válido con privilegios administrativos en el equipo Forms Server. En un entorno agrupado, el mismo conjunto de usuarios debe ser válido para todos los nodos del clúster.

En la página Cuentas de usuario de la consola de administración, puede especificar qué cuentas de usuario utilizar para las conversiones de archivos con varios subprocesos. Puede agregar cuentas, eliminarlas o cambiar las contraseñas de las cuentas. Si está ejecutando PDF Generator en Windows Server 2003 o Windows Server 2008, agregue al menos tres cuentas de usuario que tengan privilegios de administrador.

Cuando agregue usuarios para OpenOffice, Microsoft® Word o Microsoft® PowerPoint en Windows Server 2003 o 2008, o para OpenOffice en Linux® o Sun™ Solaris™, descarte los cuadros de diálogo de activación inicial de todos los usuarios.

### Añada el derecho para reemplazar el token de nivel de proceso {#add-the-right-to-replace-the-process-level-token}

En un sistema operativo Windows, las cuentas de usuario de administrador que se utilizan para la conversión de PDF (usuarios de PDFG) deben reemplazar los privilegios de token de nivel de proceso. Puede agregar este derecho mediante el Editor de directivas de grupo:

1. En el menú Inicio de Windows, haga clic en Ejecutar y escriba gpedit.msc.
1. Haga clic en Directiva de equipo local > Configuración del equipo > Configuración de Windows > Configuración de seguridad > Directivas locales > Asignación de derechos de usuario. Edite la directiva *Reemplazar un token de nivel de proceso* para incluir el grupo Administradores.
1. Agregue el usuario a la entrada Reemplazar un símbolo (token) de nivel de proceso.

### Configuración adicional necesaria para OpenOffice, Microsoft® Word y Microsoft® PowerPoint en Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Si está ejecutando OpenOffice, Microsoft® Word o Microsoft® PowerPoint en Windows Server 2008, deshabilite UAC para cada usuario agregado.

1. Haga clic en Panel de control de Campaign > Cuentas de usuario > Activar o desactivar el Control de cuentas de usuario.
1. Anule la selección de la casilla &quot;Usar el Control de cuentas de usuario (UAC) para ayudar a proteger el equipo&quot; y haga clic en Aceptar.
1. Reinicie el equipo para que la configuración surta efecto.

### Configuración adicional necesaria para OpenOffice en Linux® o Solaris™ {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Agregar cuentas de usuario. (Consulte [Agregar una cuenta de usuario](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. A continuación, debe cambiar el archivo /etc/sudoers. El permiso predeterminado para este archivo es 440. Cambie el permiso de este archivo a modificable.
1. Agregue entradas para usuarios adicionales (que no sean el administrador que ejecuta el servidor de Forms) en el archivo /etc/sudoers. Por ejemplo, si está ejecutando formularios AEM Forms como un usuario denominado lcadm y un servidor denominado myhost, y desea suplantar a user1 y user2, agregue las siguientes entradas a /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Esta configuración permite a lcadm ejecutar cualquier comando en el host &#39;myhost&#39; como &#39;user1&#39; o &#39;user2&#39; sin solicitar una contraseña.

   >[!NOTE]
   >
   >Asegúrese de haber asignado los roles de usuario del sistema y usuario de PDFG &quot;user1&quot; y &quot;user2&quot; Para asignar un rol de PDFG a un usuario, consulte [Agregar una cuenta de usuario](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. También en el archivo /etc/sudoers, localice y comente esta línea agregando un signo de número (#) al principio de la línea:

   ```shell
   Defaults requiretty
   ```

   Esto le permite añadir usuarios de Linux®.

1. Vuelva a cambiar el permiso del archivo etc/sudoers a 440.
1. Permitir que todos los usuarios que agregó mediante [Agregar una cuenta de usuario](enabling-multi-threaded-file-conversions.md#add-a-user-account) realicen conexiones al servidor de Forms. Por ejemplo, para permitir que un usuario local denominado user1 tenga permiso para establecer la conexión con el servidor de Forms, utilice el siguiente comando

   `xhost +local:user1@`

   Para obtener más información, consulte la documentación del comando xhost.

1. Reinicie el servidor.

>[!NOTE]
>
>OpenOffice debe estar instalado en una ubicación de directorio a la que todos los usuarios de PDFG puedan acceder. Puede comprobarlo iniciando sesión como usuario de PDFG y comprobando si puede iniciar OpenOffice sin problemas.

### Agregar una cuenta de usuario {#add-a-user-account}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > PDF Generator > Cuentas de usuario.
1. Haga clic en Agregar e introduzca el nombre de usuario y la contraseña de un usuario que tenga privilegios administrativos en el servidor de Forms. Si está configurando usuarios para OpenOffice, descarte los cuadros de diálogo de activación iniciales de OpenOffice.

   >[!NOTE]
   >
   >Si está configurando usuarios para OpenOffice, el número de instancias de OpenOffice no puede ser mayor que el número de cuentas de usuario especificadas en este paso.

1. Reinicie Forms Server.

### Quitar un usuario de la lista utilizada para las conversiones de archivos multiproceso {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. En la consola de administración, haga clic en Servicios > PDF Generator > Cuentas de usuario.
1. Haga clic en la casilla de verificación situada junto al usuario que desee quitar y, a continuación, haga clic en Eliminar.
1. En la página de confirmación, haga clic en Eliminar.
1. Reinicie Forms Server.

### Cambiar la contraseña de una cuenta {#change-the-password-for-an-account}

1. En la consola de administración, haga clic en Servicios > PDF Generator > Cuentas de usuario.
1. Haga clic en el nombre de usuario e introduzca y confirme la nueva contraseña. Esta contraseña debe coincidir con la contraseña del sistema del usuario.
