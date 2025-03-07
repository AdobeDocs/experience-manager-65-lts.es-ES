---
title: Configurar SSL para el servidor de aplicaciones WebSphere
description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones WebSphere.
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0caac293-98b4-4e73-9440-f1db68c94054
source-git-commit: 00d0576a5ea24efcfb40a2c9a44d596a5205f52c
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 2%

---

# Configurar SSL para el servidor de aplicaciones WebSphere {#configuring-ssl-for-websphere-application-server}

Esta sección incluye los siguientes pasos para configurar SSL con el servidor de aplicaciones de IBM WebSphere.

## Creación de una cuenta de usuario local en WebSphere {#creating-a-local-user-account-on-websphere}

Para habilitar SSL, WebSphere necesita tener acceso a una cuenta de usuario del Registro de usuarios del sistema operativo local que tenga permiso para administrar el sistema:

* (Windows) Cree un usuario de Windows que forme parte del grupo Administradores y tenga el privilegio de actuar como parte del sistema operativo. (Consulte [Crear un usuario de Windows para WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)).
* (Linux, UNIX) El usuario puede ser un usuario raíz u otro usuario que tenga privilegios de raíz. Cuando habilite SSL en WebSphere, utilice la identificación del servidor y la contraseña de este usuario.

### Creación de un usuario de Linux o UNIX para WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Inicie sesión como usuario raíz.
1. Crear una usuario introduciendo el siguiente comando en un símbolo del sistema:

   * (Linux y Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Configure el contraseña de la nueva usuario introduciéndolo `passwd` en el símbolo del sistema.
1. (Linux y Solaris) Crear un archivo de contraseña instantánea introduciéndolo `pwconv` (sin parámetros) en el símbolo del sistema.

   >[!NOTE]
   >
   >(Linux y Solaris) Para que funcione el registro de seguridad del sistema operativo local de WebSphere Application Server, debe existir un archivo de contraseña de instantánea. El archivo de contraseña de sombra generalmente se llama **/etc/shadow** y se basa en el archivo /etc/passwd. Si el archivo de contraseña de instantánea no existe, se produce un error después de habilitar la seguridad global y configurar el Registro de usuarios como sistema operativo local.

1. Abra el archivo grupo desde el directorio /etc en un editor de texto.
1. añadir al grupo el usuario que creó en el `root` paso 2.
1. Guarde y cierre el archivo.
1. (UNIX con SSL habilitado) Inicie y detenga WebSphere como usuario raíz.

### Crear un usuario de Windows para WebSphere {#create-a-windows-user-for-websphere}

1. Inicie sesión en Windows con una cuenta de usuario de administrador.
1. Seleccione **Inicio > Panel de control de Campaign > Herramientas administrativas > Administración de equipos > Usuarios y grupos locales**.
1. Haga clic con el botón derecho en Usuarios y seleccione **Nuevo usuario**.
1. Escriba un nombre de usuario y una contraseña en los cuadros correspondientes y cualquier otra información que necesite en los cuadros restantes.
1. Anule la selección de **El usuario debe cambiar la contraseña en el siguiente inicio de sesión**, haga clic en **Crear** y, a continuación, haga clic en **Cerrar**.
1. Haga clic en **Usuarios**, haga clic con el botón secundario en el usuario que ha creado y seleccione **Propiedades**.
1. Haga clic en la ficha **Miembro de** y, a continuación, en **Agregar**.
1. En el cuadro Escriba los nombres de objeto que desea seleccionar, escriba `Administrators`, haga clic en Comprobar nombres para asegurarse de que el nombre del grupo es correcto.
1. Haz clic en **Aceptar** y luego haz clic en **Aceptar** de nuevo.
1. Seleccione **Inicio > Panel de control de Campaign > Herramientas administrativas > Directiva de seguridad local > Directivas locales**.
1. Haga clic en Asignación de derechos de usuario y, a continuación, haga clic con el botón secundario en Actuar como parte del sistema operativo y seleccione Propiedades.
1. Haga clic en **Agregar usuario o grupo**.
1. En el cuadro Escriba los nombres de objeto que desea seleccionar, escriba el nombre del usuario que creó en el paso 4, haga clic en **Comprobar nombres** para asegurarse de que el nombre es correcto y, a continuación, haga clic en **Aceptar**.
1. Haga clic en **Aceptar** para cerrar el cuadro de diálogo Propiedades del sistema operativo.

### Configure WebSphere para utilizar el usuario recién creado como administrador {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. En Seguridad administrativa, seleccione **Funciones de usuario administrativo**.
1. Haga clic en Agregar y haga lo siguiente:

   1. Escriba **&amp;ast;** en el cuadro de búsqueda y haga clic en buscar.
   1. Haga clic en **Administrador** en los roles.
   1. Agregue el usuario recién creado a la función Asignado a y asígnelo al administrador.

1. Haga clic en **Aceptar** y guarde los cambios.
1. Reinicie el perfil de WebSphere.

## Habilitar la seguridad administrativa {#enable-administrative-security}

1. En la consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. Haga clic en **Asistente para configuración de seguridad**.
1. Asegúrese de que la casilla de verificación **Habilitar seguridad de la aplicación** esté habilitada. Haga clic en **Siguiente**.
1. Seleccione **Repositorios federados** y haga clic en **Siguiente**.
1. Especifique las credenciales que desea establecer y haga clic en **Siguiente**.
1. Haga clic en **Finalizar**.
1. Reinicie el perfil de WebSphere.

   WebSphere empieza a utilizar el almacén de claves y el almacén de confianza predeterminados.

## Habilitar SSL (clave personalizada y almacén de confianza) {#enable-ssl-custom-key-and-truststore}

Se pueden crear Truststore y keystore con la utilidad ikeyman o Admin Console. Para que ikeyman funcione correctamente, asegúrese de que la ruta de instalación de WebSphere no contenga paréntesis.

1. En la consola administrativa de WebSphere, seleccione **Seguridad > Certificado SSL y administración de claves**.
1. Haga clic en **Almacenes de claves y certificados** en Elementos relacionados.
1. En el menú desplegable **Usos del almacén de claves**, asegúrese de que **Almacenes de claves SSL** esté seleccionado. Haga clic en **Nuevo**.
1. Escriba un nombre lógico y una descripción.
1. Especifique la ruta en la que desea crear el almacén de claves. Si ya ha creado un repositorio de claves mediante ikeyman, especifique la ruta al archivo del repositorio de claves.
1. Especifique y confirme la contraseña.
1. Elija el tipo de almacén de claves y haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Haga clic en **Certificado personal**.
1. Si ya ha creado un repositorio de claves con ikeyman, su certificado aparecerá. De lo contrario, debe agregar un nuevo certificado autofirmado realizando los siguientes pasos:

   1. Seleccione **Crear > certificado** autofirmado.
   1. Especifique los valores adecuados en el formulario de certificado. Asegúrese de mantener Alias y nombre común como nombre de dominio completo de la máquina.
   1. Haga clic en **Aplicar**.

1. Repita los pasos 2 a 10 para crear un almacén de confianza.

## Aplicar almacén de claves personalizado y almacén de confianza al servidor {#apply-custom-keystore-and-truststore-to-the-server}

1. En la consola administrativa de WebSphere, seleccione **Seguridad > Certificado SSL y administración de claves**.
1. Haga clic en Administrar **configuración** de seguridad de endpoints. Se abre el mapa de topología local.
1. En Entrante, seleccione nodo secundario directo de nodos.
1. En Artículos relacionados, seleccione **Configuraciones** SSL.
1. Seleccione **NodeDeafultSSLSetting**.
1. En las listas desplegables nombre de almacén de confianza y nombre de almacén de claves, seleccione el almacén de confianza personalizado y el almacén de claves que ha creado.
1. Haga clic en **Aplicar**.
1. Guarde la configuración maestra.
1. Reinicie el perfil de WebSphere.

   El perfil ahora se ejecuta en la configuración SSL personalizada y en el certificado.

## Habilitar la compatibilidad con nativos de formularios AEM {#enabling-support-for-aem-forms-natives}

1. En la consola administrativa de WebSphere, seleccione **Seguridad > Seguridad global**.
1. En la sección Autenticación, expanda **Seguridad RMI/IIOP** y haga clic en **Comunicaciones entrantes CSIv2**.
1. Asegúrese de que **Compatible con SSL** esté seleccionado en la lista desplegable Transporte.
1. Reinicie el perfil de WebSphere.

## Configuración de WebSphere para convertir direcciones URL que comienzan por https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Para convertir una dirección URL que comience por https, agregue un certificado de firmante para esa dirección URL al servidor de WebSphere.

**Crear un certificado de firmante para un sitio habilitado para https**

1. Asegúrese de que WebSphere se esté ejecutando.
1. En la consola administrativa de WebSphere, vaya a Certificados de firmante y, a continuación, haga clic en Seguridad > Certificados SSL y Administración de claves > Almacenes de claves y certificados > NodeDefaultTrustStore > Certificados de firmante.
1. Haga clic en Recuperar desde puerto y realice estas tareas:

   * En el cuadro Host, escriba la dirección URL. Por ejemplo, escriba `www.paypal.com`.
   * En el cuadro Puerto, escriba `443`. Este puerto es el puerto SSL predeterminado.
   * En el cuadro Alias, escriba un alias.

1. Haga clic en Recuperar información del firmante y, a continuación, compruebe que se ha recuperado la información.
1. Haga clic en Aplicar y, a continuación, en Guardar.

La conversión de HTML a PDF desde el sitio cuyo certificado se agrega ahora funcionará desde el servicio Generate PDF.

>[!NOTE]
>
>Para que una aplicación se conecte a sitios SSL desde WebSphere, se requiere un certificado de firmante. Java Secure Socket Extensions (JSSE) lo utiliza para validar certificados que el lado remoto de la conexión envió durante un protocolo de enlace SSL.

## Configuración de puertos dinámicos {#configuring-dynamic-ports}

IBM WebSphere no permite llamadas múltiples a ORB.init() cuando la seguridad global está habilitada. Puede leer más sobre la restricción permanente en https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Realice los siguientes pasos para configurar el puerto para que sea dinámico y resolver el problema:

1. En la consola administrativa de WebSphere, seleccione **Servidores** > **Tipos de servidor** > **Servidor de aplicaciones WebSphere**.
1. En la sección Preferencias, seleccione el servidor.
1. En la ficha **Configuración**, en la sección **Comunicaciones**, expanda **Puertos** y haga clic en **Detalles**.
1. Haga clic en los siguientes nombres de puerto, cambie el **número de puerto** a 0 y haga clic en **Aceptar**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configuración del archivo sling.properties {#configure-the-sling-properties-file}

1. Abra `[aem-forms_root]`\crx-repository\launchpad\sling.properties para editarlo.
1. Busque la propiedad `sling.bootdelegation.ibm` y agregue `com.ibm.websphere.ssl.*`a su campo de valor. El campo actualizado tiene el siguiente aspecto:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Guarde el archivo y reinicie el servidor.
